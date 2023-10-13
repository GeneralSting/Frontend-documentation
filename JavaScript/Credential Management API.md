# Credential Management API

- lets a website store and retrieve password, public key, and federated credentials. These capabilities allow users to sign in without typing passwords, see the federated account they used to sign in to a site, and resume a session without the explicit sign-in flow of an expired session.
- interact with the user agent's password system directly

## Credential interface

- `Credential`
  - `Credential` interface of the `Credential Management API` provides information about the entity normally as a prerequsite to a trust decision
  - may be of four different types:
    - `FederatedCredential`
      - provides information about credentials from a federated indetity provider
      - federated identity provider is an entity that a website trusts to correctly authenticate user and provides an API for that purpose
      - <b>FederatedCredential -> Credential </b>
    - `IdentityCredential`
      - <b>Federrated Credential Management API (FedCM)</b>
      - represents a user identify credential arising from a successful federated sign-in
      - successful `navigator.credentials.get()` call that includes an identity option fulfills with an `IdentityCredential instance`
      - <b>IdentityCredential -> Credential</b>
    - `PasswordCredential`
      - provides information about a username/password pair
      - <b>PasswordCredential -> Credential</b>
    - `PublicKeyCredential`
      - provides information about a public key/private key pair, which is a credential for logging in to a service using an un-phisable and data-breach resistant asymmetric key pair instead of a password
      - inherits `Credential`, part of the `Web Authentication API` extension to the Credential Management API
      - this API is restricted to top-level contexts.
      - <b>PublicKeyCredential -> Credential</b>

### Instance properties

- Credential.id
  - returns a string containing the credential's identifie
    - GUID, username, email
    - read only
- Credential.type
  - returns a string containing the credential's type
  - valid values are
    - password, `PasswordCredential`
    - federated, `FederatedCredential`
    - public-key, `PublicKeyCredential`
