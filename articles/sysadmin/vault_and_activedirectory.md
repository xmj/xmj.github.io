# Hashicorp Vault and Active Directory: How to Use Role-Based Access Control to manage access to Vault secrets

## Introduction

Secrets management and access control is one of the more important necessities
in systems infrastructure. Not only do you want to store secrets safely, you
may also want to be able to limit access to them based on a set of policies
defined in a central location. Group membership in a centrally defined
directory remains one of the most popular ways to authorize users to create,
read, update and delete data.

In this guide, I will show you how to integrate Hashicorp Vault, one of the
most popular secrets management engines, with Microsoft Active Directory, the
most enterprise directory service known to the author. 

I will further assume you have a running instance of Hashicorp Vault, and an
Active Directory server with a directory tree fitting your business needs.
Setting up either of those is out of scope for the purposes of this guide -
contact your friendly sysadmin to help you with it.

## Step 1

Create a script `ldap.sh` that will register the LDAP configuration within Vault.

```sh
#!/bin/sh

export VAULT_ADDR=https://<hostname>:8200
export VAULT_TOKEN=<root token here>

LDAP_ADDR=ldaps://your.ldap.server:636
USER_DN="OU=users,DC=yourfirm,DC=com"
GROUP_DN="OU=groups,DC=yourfirm,DC=com"

BIND_DN="yourbinduser@yourfirm.com"
BIND_PW="$ecret_b1nd_pa55"
UPN_DOMAIN="yourfirm.com"

vault write auth/ldap/config \
  url="${LDAP_ADDR}" \
  userdn="${USER_DN}" \
  binddn="${BIND_DN}" \
  bindpw="${BIND_PW}" \
  groupdn="${GROUP_DN}" \
  groupfilter="(member:1.2.840.113556.1.4.1941:={{.UserDN}})" \
  groupattr="cn" \
  upndomain="${UPN_DOMAIN}" \
  certificate=@ldap_ca_cert.pem
```

Assuming you replaced all the necessary inputs in the first few lines, and put
your LDAP server's CA certificate as `ldap_ca_cert.pem` within the current
working directory, running `sh ldap.sh` will set up your Vault instance to use
Active Directory for LDAP authentication.

Verify that this works by logging in with your email handle.

## Step 2

Log in to the Vault UI (`https://<hostname>:8200`) with your root token, create
a new group `ldap-admins` - this must be an external group - and add an alias
to the LDAP group you want to authorize as admins.

## Step 3

Create an `admin` policy. It should have at least the following permissions:
```hcl
# Manage auth methods broadly across Vault
path "auth/*"
{
  capabilities = ["create", "read", "update", "delete", "list", "sudo"]
}

# Create, update, and delete auth methods
path "sys/auth/*"
{
  capabilities = ["create", "update", "delete", "sudo"]
}

# List auth methods
path "sys/auth"
{
  capabilities = ["read"]
}

# Create and manage ACL policies
path "sys/policies/acl/*"
{
  capabilities = ["create", "read", "update", "delete", "list", "sudo"]
}

# To list policies
path "sys/policies/acl"
{
  capabilities = ["list"]
}

# List, create, update, and delete key/value secrets
path "secret/*"
{
  capabilities = ["create", "read", "update", "delete", "list", "sudo"]
}

# Create and manage secret engines broadly across Vault.
path "sys/mounts/*"
{
  capabilities = ["create", "read", "update", "delete", "list", "sudo"]
}

# Read health checks
path "sys/health"
{
  capabilities = ["read", "sudo"]
}

path "sys/capabilities"
{
  capabilities = ["create", "update"]
}

path "sys/capabilities-self"
{
  capabilities = ["create", "update"]
}

# Create and manage identities and groups
path "identity/*" { 
  capabilities = [ "create", "read", "update", "delete", "list" ]
}
```

## Step 4

Assign the above policy to the external group `ldap-admins`. Open a new private
window and verify that your LDAP user now authorized as admin can view
everything.

Congrats, you're done.
