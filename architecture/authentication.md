---
layout: page
title: Authentication Architecture Document
author: tilgovi
---

Overview
--------------

Our architecture is meant to adapt to many different authentication systems. The core elements are a pluggable OAuth Provider in Python (using pyramid_oauthlib) and a pluggable BrowserID-like module in JavaScript.

While our current deployment uses traditional, cookie-based sessions, the goal is to accommodate such legacy architectures while providing a smooth upgrade path an OpenID Connect system.

At present, the plan is to utilize the JSON Web Token Profile for OAuth 2.0 Client Authentication and Authorization Grants. This specification is a draft of a grant type for OAuth 2.0. Since OpenID Connect is, at its core, a set of core OAuth 2.0 scopes and claims, it is good to start with a solid OAuth foundation.

Since Annotator has historically used JWT tokens for authenticating API requests and our current deployment uses this, the draft-ietf-oauth-jwt-bearer specification is a great bridge.

Technical Background
-------------------------------

The JWT Profile mentioned above is in draft stage. You can find it here: <http://tools.ietf.org/html/draft-ietf-oauth-jwt-bearer-10>

Notice that these grants have an audience (the site the user wishes to sign in to), an issuer (the identity authority), and a subject (the user identity).

In section 5 of the specification, Interoperability Considerations, agreeing on what form these fields take and what keys should be used to sign and verify the JWT is left deliberately outside this specification. It links to OpenID Connect, but I think it provides a common foundation for BrowserID and OpenID Connect to claim to each make use of it.

BrowserID does specify how keys are determined. It uses two (or more) JWTs forming something like a certificate chain. That specification is here: <https://github.com/mozilla/id-specs/blob/prod/browserid/index.md>

An Identity Assertion contains the audience. A user creates her own key pair and signs this assertion with her private key.

After authenticating with her identity provider to agree on a principal (userid), she sends her public key to her provider. The provider adds this key to the payload of a new JWT containing the identity of the provider (issuer) and signed by the provider's private key.

A JWT containing a public key and an issuer is an Identity Certificate. Any number of these may be chained until the issuer is a publicly resolvable domain with a /.well-known/browserid endpoint where its public key can be discovered.

The Identity Assertion contains the audience and is signed by the user.
The Identity Certificate contains the user's public key, principal and issuer and is signed by the issuer.

The Certificate and the Assertion together contain all the claims that draft-ietf-oauth-jwt-bearer requires for an Authorization Grant along with a mechanism for resolving the keys through the certificate chain and DNS as per the Interoperability Considerations.

Implementation
----------------------

Our proposed Single Sign On backend uses pyramid_oauthlib to implement the JWT grant type.
That code is here: <https://github.com/hypothesis/h/pull/1437>

Our proposed front end authentication modules implement a Persona API split into two parts, `h.identity` and `h.auth.` Our main application depends on `h.auth` which is expected to configure the `identityProvider` defined by `h.identity` during the configuration phase of the application. The `identityProvider` is then used by angular to create the `identity` service, which is used by the application. I have an open PR for this work here: <https://github.com/hypothesis/h/pull/1539>

The separation on the front end allows for "swapping out" `h.auth` module implementations that set different adapter functions on the `identityProvider`. The simplest such module would delegate to `window.navigator.id`, using Persona for log in. Our current implementation uses our cookie session.

From the perspective of the core `identity` service and the application using it, sign in happens through an unspecified process that results in an assertion. This assertion is passed as a query parameter to the token endpoint by the application in order to get an Annotator Auth token (also a JWT), which we use as a normal OAuth Bearer Token for accessing protected resources.

(Aside: the draft JWT Profile for OAuth is about using a JWT as an identity authorization grant when communicating with a token endpoint. A conventional token endpoint issues a Bearer Token, which can be any opaque token verifiable by the server. In our case, we use a JWT as the Bearer Token, but it's worth noting that these uses of JWT are performing separate functions.)

At present, our back end sends the cross site request forgery token from the user's session as the assertion. It is verified by checking that the user submitting it to the token endpoint also has a session that matches. This implementation is less than ideal because it relies on cookies that may be blocked in our 3rd-party, sidebar context. This process has been the same for a while. However, using pyramid_oauthlib, the implementation is straightforward and can be swapped out as we merge further development. This transitional grant type is implemented here: <https://github.com/hypothesis/h/blob/master/h/auth/local/oauth.py#L19>

We are providing three things: a client application, an identity provider, and an API server. Our API is best seen a separate application, a relying party to our identity provider. A user first authenticates with the backend and then signs in to our application. Once it has contacted the token endpoint and provided it with a valid grant in exchange for an access token, the user is "signed in" to the application.

*There is, at present, no additional confirmation required to authorize the application beyond authenticating with the identity provider, because we issue both, but this need not be the case. As we expand the `identityProvider` and `identity` services to make the provider side pluggable, we can achieve additional deployment flexibility, such as deploying one sidebar application but allowing users to sign in to our API server using an identity provider of their choice.

Result
---------

Currently, our only authentication is through username / password and our API authorization is through the resulting session. By abstracting the various components of our authentication and authorization on the front and back end we enable agile integrations.

Partners can be given access to our APIs from their own applications by deploying the Authorization Code or Implicit grant types of core OAuth 2.0, as is done with most OAuth 2.0 APIs in the wild.

Single Sign On can be achieved by allowing partners to pass a JWT through our embed code and using the JWT grant type.

Persona deployment can be achieved by implementing a grant type that uses the Persona verifier code while the front end can simply delegate to `window.navigator.id` (or the Mozilla shim).

Partners who might deploy the sidebar from their own domains, and thus not suffer from cross domain limitations, may wish to perform authentication directly from the sidebar by implementing their own adapter  functions for the `identityProvider`.
