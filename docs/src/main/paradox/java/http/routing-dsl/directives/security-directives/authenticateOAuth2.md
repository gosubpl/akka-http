<a id="authenticateoauth2-java"></a>
# authenticateOAuth2

Wraps the inner route with OAuth Bearer Token authentication support using a given `AuthenticatorPF<T>`

## Description

Provides support for extracting the so-called "*Bearer Token*" from the `Authorization` HTTP Header,
which is used to initiate an OAuth2 authorization.

@@@ warning
This directive does not implement the complete OAuth2 protocol, but instead enables implementing it,
by extracting the needed token from the HTTP headers.
@@@

Given a function returning a non empty`Optional<T>` upon successful authentication and `None` otherwise,
respectively applies the inner route or rejects the request with a `AuthenticationFailedRejection` rejection,
which by default is mapped to an `401 Unauthorized` response.

Longer-running authentication tasks (like looking up credentials in a database) should use the @ref[authenticateOAuth2Async](authenticateOAuth2Async.md#authenticateoauth2async-java)
variant of this directive which allows it to run without blocking routing layer of Akka HTTP, freeing it for other requests.

See @ref[Credentials and password timing attacks](index.md#credentials-and-timing-attacks-java) for details about verifying the secret.

For more information on how OAuth2 works see [RFC 6750](https://tools.ietf.org/html/rfc6750).

## Example

Usage in code is exactly the same as @ref[authenticateBasic](authenticateBasic.md#authenticatebasic-java),
with the difference that one must validate the token as OAuth2 dictates (which is currently not part of Akka HTTP itself).
