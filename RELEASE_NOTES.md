Release Notes
=============

0.4.0
-----

### Deprecated configuration options

The following configuration options have been deprecated:
* `oauth.tokens.not.jwt` is now called `oauth.access.token.is.jwt` and has a reverse meaning.
* `oauth.validation.skip.type.check` is now called `oauth.check.access.token.type` and has a reverse meaning.


See: Align configuration with Kafka Operator PR ([#36](https://github.com/strimzi/strimzi-kafka-oauth/pull/36)).

### Compatibility improvements

Scope claim is no longer required in an access token. ([#30](https://github.com/strimzi/strimzi-kafka-oauth/pull/30))
That improves compatibility with different authorization servers, since the attribute is not required by OAuth 2.0 specification neither is it used by validation logic.

### Updated dependencies

`jackson-core`, and `jackson-databind` libraries have been updated to latest versions. ([#33](https://github.com/strimzi/strimzi-kafka-oauth/pull/33))

### Instructions for developers added

Instructions for preparing the environment, building and deploying the latest version of Strimzi Kafka OAuth library with Strimzi Kafka Operator have been added.

See: Hacking on OAuth and deploying with Strimzi Kafka Operator PR ([#34](https://github.com/strimzi/strimzi-kafka-oauth/pull/34))

### Improvements to examples and documentation

Fixed enabled remote debugging mode in example `compose-authz.yml` ([#39](https://github.com/strimzi/strimzi-kafka-oauth/pull/39))

0.3.0
-----

### Token-based authorization with Keycloak Authorization Services

It is now possible to use Keycloak Authorization Services to centrally manage access control to resources on Kafka Brokers ([#24](https://github.com/strimzi/strimzi-kafka-oauth/pull/24))
See the [tutorial](examples/README-authz.md) which explains many concepts.
For configuration details also see [KeycloakRBACAuthorizer JavaDoc](oauth-keycloak-authorizer/src/main/java/io/strimzi/kafka/oauth/server/authorizer/KeycloakRBACAuthorizer.java). 

### ECDSA signature verification support

The JWTSignatureValidator now supports ECDSA signatures, but requires explicit enablement of BouncyCastle security provider ([#25](https://github.com/strimzi/strimzi-kafka-oauth/pull/25))
To enable BouncyCastle set `oauth.crypto.provider.bouncycastle` to `true`.
Optionally you may control the order where the provider is installed by using `oauth.crypto.provider.bouncycastle.position` - by default it is installed at the end of the list of existing providers.

0.2.0
-----

### Testsuite with integration tests

A testsuite based on Arquillian Cube, and using docker containers was added.
 
### Examples improvements

Added Ory Hydra authorization server to examples. 

0.1.0
-----

### Initial OAuth 2 authentication support for Kafka

Support for token-based authentication that plugs into Kafka's SASL_OAUTHBEARER mechanism to provide:
* Different ways of access token retrieval for Kafka clients (clientId + secret, refresh token, or direct access token)
* Fast signature-checking token validation mechanism (using authorization server's JWKS endpoint)
* Introspection based token validation mechanism (using authorization server's introspection endpoint)

See the [tutorial](examples/README.md).