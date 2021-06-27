# vault_basics

# Vault installation
  Download appropriate package from https://www.vaultproject.io/downloads
  
# Vault Start Server:
  > vault server -dev
  > Copy the root token and unseal key safely
  > update the env variables VAULT_ADDRESS to use it in any shell.

# Create secret
kv (key value v2 secret engine) --> path should be prefixed by secret/ for to determine kv type --> it can have n number of key value pairs stored in one secret
  >  vault kv put secret/hello foo=world excited=yes

To enable at a different path
 > vault secrets enable -path=kv kv
 > vault secrets enable kv

# Listing all the secret paths

PS C:\Users\212801747> vault secrets list
Path          Type         Accessor              Description
----          ----         --------              -----------
cubbyhole/    cubbyhole    cubbyhole_8a471874    per-token private secret storage
identity/     identity     identity_cb9170e0     identity store
kv/           kv           kv_c6963ae1           n/a
secret/       kv           kv_a2b353d8           key/value secret storage
sys/          system       system_5e997db5       system endpoints used for control, policy and debugging

# Retreive Secret
  > vault kv get secret/hello
  >  vault kv get -field=excited secret/hello
  >  vault kv get --format=json secret/hello | jq -r .data.data.excited

# Delete secret
  > vault kv delete secret/hello

# Disabling a secret path:
  > vault secrets disable kv/
here kv/ is the path created. It will revoke all the secrets stored in the path

PS C:\Users\212801747> vault secrets disable kv/
Success! Disabled the secrets engine (if it existed) at: kv/
PS C:\Users\212801747> vault kv get kv/abc
Error making API request.

URL: GET http://127.0.0.1:8200/v1/sys/internal/ui/mounts/kv/abc
Code: 403. Errors:

* preflight capability check returned 403, please ensure client's policies grant access to path "kv/abc/"
* 

Automatically all the secrets stored are revoked once after disabled and wont be restored after enabling it back
> PS C:\Users\212801747> vault secrets enable kv
Success! Enabled the kv secrets engine at: kv/
PS C:\Users\212801747> vault kv get kv/abc
No value found at kv/abc
