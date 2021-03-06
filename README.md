# ansible-vault lookup module
This is a lookup module for generic secrets in [Vault](https://vaultproject.io/)(the HashiCorp project).

The plugin is currently written for ansible 2.0 but a working version for ansible 1.9 exist under the 1.0.0 tag.

### Installation
lookup plugins can be loaded from several different locations similar to $PATH, see [docs](http://docs.ansible.com/ansible/intro_configuration.html#lookup-plugins).

### Usage
The address to the Vault server and the auth token are fetched from environment variables

    export VAULT_ADDR=http://192.168.33.10:8200/
    export VAULT_TOKEN=56f48aef-8ad3-a0c4-447b-8e96990776ff

ansible-vault then works as any other lookup plugin.

```yaml
- debug: msg="{{lookup('vault', 'secret/foo', 'value')}}"
```

```yaml
# templates/example.j2

# Generic secrets
{{ lookup('vault', 'secret/hello').value }} # world
# Specify field inside lookup
{{ lookup('vault', 'secret/hello', 'value') }} # world

# Dynamic secret
{% set aws = lookup('vault', 'aws/creds/deploy') %}
access_key = {{ aws.access_key }} # AKSCAIZSFSYHFGA
secret_key = {{ aws.secret_key }} # 4XSLxDUS+hyXgoIHEhCKExHDGAJDHFiUA/adi
```
