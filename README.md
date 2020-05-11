# vault-consul-docker

### This is meant to be used as a local development environment for Vault/Consul, to be used to try out new things without making changes in production

Dependencies

1) Download and install Docker CE on your machine. You can find the latest copy here: https://docs.docker.com/docker-for-mac/release-notes/
2) Download and install Vault CLI via brew: `brew install vault` (you will need this to interact with vault via CLI, both for Enova vault or your local vault)
3) Insert the following into your environment file. This will allow you to connect to your local vault via the CLI. You can also change this value to connect to Enova's vault server when you are ready to make changes: `export VAULT_ADDR="http://localhost:8200"`

Short how to get started:

1) Start up Vault and Consul:
  docker-compose up -d --build
2) Create a new bash session within Vault itself:
  docker-compose exec vault bash
3) 'init' vault (start the vault backend and prepares it to recieve data)(***NOTE! ONLY FOR FIRST TIME RUN!***):
  vault operator init
4) Unseal (enter 3 of the keys provided by step 3, you will need to run this command until the vault is unsealed):
  vault operator unseal
5) Authenticate to vault (enter root key):
  vault login
6) For testing, add a static secret:
  vault kv put secret/foo bar=precious
7) Read it back:
  vault kv get secret/foo

Using Vault

If you made the change to your environmental file and installed vault's cli on your computer, you should be able to run commands to vault directly in your local terminal, just like you would on the staging vault. You should also be able to run commands against consul as well.

Here is a good resource if you want to play around with what Vault is capable of: https://testdriven.io/blog/managing-secrets-with-vault-and-consul/

You can also try the official "Learn Vault" docs: https://learn.hashicorp.com/vault/
