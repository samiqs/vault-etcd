## run docker-compose
```
$ docker-compose up
$ docker-compose up -d/docker-compose stop
```

## set vault address to local
```
$ export VAULT_ADDR=http://127.0.0.1:8200
```
## initiate new vault instance
```
$ vault init
Unseal Key 1: ############################################
Unseal Key 2: ############################################
Unseal Key 3: ############################################
Unseal Key 4: ############################################
Unseal Key 5: ############################################
Initial Root Token: ######################################

Vault initialized with 5 keys and a key threshold of 3. Please
securely distribute the above keys. When the vault is re-sealed,
restarted, or stopped, you must provide at least 3 of these keys
to unseal it again.

Vault does not store the master key. Without at least 3 keys,
your vault will remain permanently sealed.
```

## unseal the vault
### you will need to run vault unseal 3 times with different unseal keys
```
$ vault unseal
Key (will be hidden):
```
## authenticate with root token
```
$ vault auth
Token (will be hidden):
```

## quick into to writing and reading secrets
```
$ vault write secret/hello value=world
Success! Data written to: secret/hello

$ vault read secret/hello
Key                 Value
---                 -----
refresh_interval    768h0m0s
excited             yes
value               world

# via api

$ curl \
    -H "X-Vault-Token: #####-#####-####-###-#########" \
    -H "Content-Type: application/json" \
    -X POST \
    -d '{"value":"bar"}' \
    https://127.0.0.1:8200/v1/secret/foo

$ curl \
    -H "X-Vault-Token: #####-#####-####-###-#########" \
    -H "Content-Type: application/json" \
    -X GET \
    https://127.0.0.1:8200/v1/secret/foo
```
