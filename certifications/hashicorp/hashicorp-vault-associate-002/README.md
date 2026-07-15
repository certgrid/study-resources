# HashiCorp Vault Associate (002) - Study Cheatsheet

The HashiCorp Vault Associate (002) exam validates foundational knowledge of secrets management with Vault: its architecture and seal model, authentication methods, ACL policies, secrets engines, and the token/lease lifecycle. It targets cloud engineers, DevOps practitioners, and security professionals who deploy or operate Vault, and it is a 60-minute, multiple-choice exam scored on a scaled basis with 700 as the passing mark.

## Exam at a glance

| Item | Detail |
|---|---|
| Exam code | HashiCorp Vault Associate (002) |
| Credential | HashiCorp Vault Associate (002) |
| Level | Associate |
| Practice mock length | ~57 questions |
| Duration | ~60 minutes |
| Passing score | 700 out of 1000 |
| Notes reviewed | 2026-07-12 |

## Domains

| # | Domain | Approx. weight |
|---|---|---|
| 1 | Vault Architecture | ~25% |
| 2 | Authentication | ~20% |
| 3 | Policies | ~17% |
| 4 | Secrets Engines | ~19% |
| 5 | Tokens and Leases | ~19% |

_Weightings are approximate, based on the question distribution in the CertGrid practice bank. Confirm official objectives on the vendor site._

## Key concepts by domain

### Domain 1 - Vault Architecture

- Vault starts in a sealed state and cannot decrypt any stored data until it is unsealed; sealing is also the safety mechanism that locks Vault down during a compromise.
- The default Shamir unseal splits the master key into key shares (e.g., 5 shares with a threshold of 3); unsealing requires reassembling enough shares to reconstruct the key.
- vault operator init -key-shares=5 -key-threshold=3 initializes Vault, returning the unseal key shares and the initial root token exactly once.
- Vault encrypts all data with a barrier key before writing to storage, so the storage backend only ever holds ciphertext and never sees plaintext.
- Auto-unseal delegates protection of the master key to a cloud KMS or HSM (AWS KMS, Azure Key Vault, GCP KMS), removing the need to manually enter unseal key shares at startup.
- An auto-unseal seal stanza looks like: seal "awskms" { region = "us-east-1" kms_key_id = "..." }.

### Domain 2 - Authentication

- Auth methods authenticate clients (humans or machines) and, on success, issue a Vault token with attached policies and a TTL that is used for all subsequent requests.
- AppRole is purpose-built for machine/application auth using a RoleID (like a username) and a SecretID (like a password); the SecretID is decoupled and rotatable for automated workflows.
- Enable and configure AppRole with: vault auth enable approle, then vault write auth/approle/role/web token_policies="web-policy", read the role-id with vault read auth/approle/role/web/role-id, and generate a secret-id with vault write -f auth/approle/role/web/secret-id.
- Log in with AppRole using: vault write auth/approle/login role_id="..." secret_id="...", which returns a token.
- The Kubernetes auth method validates a pod's ServiceAccount JWT (against the cluster's TokenReview API or via local JWT validation using the cluster's public keys/issuer) and maps it to a role and policies, so no static secrets are distributed to pods.
- The root token has unrestricted access and no TTL; use it only for initial setup, then revoke it and operate with scoped, least-privilege tokens.

### Domain 3 - Policies

- Vault policies are deny by default: a token has no access to any path unless a policy explicitly grants capabilities on it.
- Policies grant capabilities on paths; valid ACL capabilities are read, create, update, delete, list, sudo, deny, and patch.
- An explicit deny always overrides any grant, regardless of how the access was granted on other matching paths.
- When multiple policy rules match a request, the most specific matching path wins, and an explicit deny on that path overrides grants.
- Write a policy from a file with vault policy write app policy.hcl, where the file contains stanzas like path "secret/data/app/*" { capabilities = ["read", "list"] }.
- Use the '+' wildcard to match a single path segment and '*' to match a suffix; '*' only matches at the end of a path, not in the middle.

### Domain 4 - Secrets Engines

- The KV (Key/Value) secrets engine stores arbitrary key-value data; KV v2 adds versioning, metadata, and soft delete, while KV v1 performs immediate, irreversible deletes with no history.
- Enable KV v2 with vault secrets enable -path=myapp kv-v2 (or vault secrets enable -version=2 kv, or vault secrets enable kv-v2).
- Write and read KV data with vault kv put secret/myapp foo=bar and read a specific version with vault kv get -version=3 secret/myapp.
- On a KV v2 mount, set max_versions to cap retained versions per secret and delete_version_after to auto-delete versions after a duration, bounding storage growth.
- The transit secrets engine provides encryption as a service: applications send plaintext to be encrypted/decrypted, but Vault never stores the data, only manages and rotates the keys.
- Transit supports batch input, letting you submit many plaintext items in one transit/encrypt request, and batch operations on transit/verify for multiple input/signature pairs.

### Domain 5 - Tokens and Leases

- A token is the primary credential used to authenticate to Vault and carries the policies and TTL that govern what the holder can do and for how long.
- Every dynamic secret and most tokens have a lease with a TTL that defines how long it remains valid before expiring or needing renewal; expiry triggers automatic revocation.
- Revoking a lease immediately invalidates the associated secret (e.g., deletes the dynamic database credential) before its TTL would naturally expire.
- Create a token with policies and a TTL using vault token create -policy=app -ttl=1h.
- Renew a lease with vault lease renew <lease_id> and revoke with vault lease revoke <lease_id>; revoke a token with vault token revoke <token>.
- vault lease revoke -prefix <mount-path> revokes all leases under that prefix at once, useful for invalidating every credential from an engine.

## Study tips

- Memorize the exact CLI verbs and paths: vault auth enable, vault secrets enable, vault policy write, vault kv put/get, vault lease renew/revoke, vault token create/revoke - the exam tests precise command syntax.
- Know the KV v2 path quirk cold: the secret data lives at secret/data/<path>, so policies and API calls must include the data/ segment that the kv CLI hides for you.
- When a policy question shows conflicting rules, apply the precedence order: most specific path wins and an explicit deny always beats any grant.
- Distinguish service vs. batch tokens by their properties (persistence, renewability, child tokens, replication cost) - several questions hinge on these differences.
- For 'best practice' or scenario questions, favor least privilege, dynamic short-lived secrets, auto-unseal/TLS/audit-on, and revoking the root token after setup.

---

Want the full breakdown? See the complete **[HashiCorp Vault Associate (002) study guide](https://certgrid.app/study-guide/hashicorp-vault-associate-002)** and **[free practice questions](https://certgrid.app/practice/hashicorp-vault-associate-002)** on CertGrid.

Maintained by the team behind **[CertGrid](https://certgrid.app)**, a certification practice-exam platform where every question explains why each wrong answer is wrong, not just the right one. Free plan to start. _(Disclosure: we build CertGrid.)_

