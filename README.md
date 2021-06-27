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

# Retreive Secret
  > vault kv get secret/hello
  >  vault kv get -field=excited secret/hello
  >  vault kv get --format=json secret/hello | jq -r .data.data.excited

# Delete secret
  > vault kv delete secret/hello
