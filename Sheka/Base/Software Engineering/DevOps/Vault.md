23.12.2020  13:19
Tags:  #dev | #job 
____

# Vault
## Log in to Vault using Active Directory

```shell
vault auth enable ldap
	
vault write auth/ldap/config userattr="userPrincipalName" binddn="sheka@sam-solutions.net" bindpass="KJdh232xzxc213lm" url="ldaps://a78.sam-solutions.net:636" userdn="OU=SamSol,OU=Belcaf,DC=sam-solutions,DC=net" groupattr="cn" groupdn="OU=SamSol,OU=Belcaf,DC=sam-solutions,DC=net" groupfilter="(&(objectClass=group)(member:1.2.840.113556.1.4.1941:={{.UserDN}}))" starttls="true" certificate="-----BEGIN CERTIFICATE-----
MIIE3DCCA8SgAwIBAgIQZD5BiLcBNLpDHGC2K+vPbTANBgkqhkiG9w0BAQsFADBb
MRIwEAYKCZImiZPyLGQBGRYCYnkxFTATBgoJkiaJk/IsZAEZFgVtaW5zazEWMBQG
CgmSJomT8ixkARkWBmJlbGNhZjEWMBQGA1UEAxMNU2FNLVNvbHV0aW9uczAeFw0x
MTA1MjUwNTI1NThaFw0yNjExMDMwNzEyNTZaMFsxEjAQBgoJkiaJk/IsZAEZFgJi
eTEVMBMGCgmSJomT8ixkARkWBW1pbnNrMRYwFAYKCZImiZPyLGQBGRYGYmVsY2Fm
MRYwFAYDVQQDEw1TYU0tU29sdXRpb25zMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8A
MIIBCgKCAQEA4gULx9u8Kj0+t5kBFuFzupRNctv2OeG209lcbOSosne4wa97U/3E
D+7X+tXGTnlbT3qjulf0wDr78yBSyF8sClyZCXxN1IJHErqvLExFTOQOGN/Lfiqd
RVVFVICpqcB0eW6xGhikxzE20snCZQJy5QL3zVK8HYjNG0LUt1eiUOUjB6xDPzFU
lVKtRGAb7Ad0ZwmwPEzudqzSvs4e5JguDTDe3C2vZyprX6GrmU52JGLuo07R8LBd
to3KoQ2Nc75mpTaQusuqDyG8K+ZePwheOGGElgVSKTpg6AG6bd0zIsXEDuE8VvpO
RHm7524y1jie9VmOZiXBfbeyMn3WEgKx/wIDAQABo4IBmjCCAZYwEwYJKwYBBAGC
NxQCBAYeBABDAEEwCwYDVR0PBAQDAgGGMA8GA1UdEwEB/wQFMAMBAf8wHQYDVR0O
BBYEFEumqiHDo2Mc/gHu3ZgikMpA0kZmMIIBBwYDVR0fBIH/MIH8MIH5oIH2oIHz
hoG3bGRhcDovLy9DTj1TYU0tU29sdXRpb25zLENOPWE3MSxDTj1DRFAsQ049UHVi
bGljJTIwS2V5JTIwU2VydmljZXMsQ049U2VydmljZXMsQ049Q29uZmlndXJhdGlv
bixEQz1iZWxjYWYsREM9bWluc2ssREM9Ynk/Y2VydGlmaWNhdGVSZXZvY2F0aW9u
TGlzdD9iYXNlP29iamVjdENsYXNzPWNSTERpc3RyaWJ1dGlvblBvaW50hjdodHRw
Oi8vYTcxLmJlbGNhZi5taW5zay5ieS9DZXJ0RW5yb2xsL1NhTS1Tb2x1dGlvbnMu
Y3JsMBIGCSsGAQQBgjcVAQQFAgMBAAIwIwYJKwYBBAGCNxUCBBYEFFgwMJglp6dn
LIY58ciSjIBHLZn/MA0GCSqGSIb3DQEBCwUAA4IBAQARjL9nn06THs3fXsFyk0TL
7KAyE5Dcw1Fapg6oPEKa2znlSH35xfpIU5IZbMZoHhLFhz+jSRxdkPpHIfGbDnSX
La0QHf8GthK718+1VSIbfh15aUfH71iCcG7W0SAgGDIG3FZiCoWLkCqZkhIUTvq7
OOFhhj0xvxbImT/VzE9jY77C01zQ53UEOeXr7pq0s0AAZC3cmrfaxlsjIAjwAF/a
F65hxofJcURW05EIsY5ZSrKGJXmCY3lrBWowLfEzoIscrlbi4f5pNzaWbsf1r42/
kInz1QAoJbok29hQpzYfv7d0+gpq7ADe8xJxhpe1wbNQaNKLEUgm3nBWVPPKxI5g
-----END CERTIFICATE-----"
	 
vault login -method=ldap username=sheka@sam-solutions.net password=KJdh232xzxc213lm


ASDF1234zxcv

port 389
https://sourceforge.net/p/ldapadmin/discussion/305548/thread/49955d79/?limit=25#20d7
```
Y.Sheka@sam-solutions.com

`vault server -dev -dev-listen-address=0.0.0.0:8200 -dev-root-token-id=root`


## Policy structure  (https://www.hashicorp.com/resources/policies-vault)

### administrator-policy
```shell
# Read system health check
path "sys/health"
{
 capabilities = ["read", "sudo"]
}
# Create and manage ACL policies broadly across Vault
# List existing policies
path "sys/policies/acl"
{
 capabilities = ["list"]
}
# Create and manage ACL policies
path "sys/policies/acl/*"
{
 capabilities = ["create", "read", "update", "delete", "list", "sudo"]
}
# Enable and manage authentication methods broadly across Vault
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
# Enable and manage the key/value secrets engine at `secret/` path
# List, create, update, and delete key/value secrets
path "secret/*"
{
 capabilities = ["create", "read", "update", "delete", "list", "sudo"]
}
# Manage secrets engines
path "sys/mounts/*"
{
 capabilities = ["create", "read", "update", "delete", "list", "sudo"]
}
# List existing secrets engines.
path "sys/mounts"

{
capabilities = ["read"]
}
# Create and manage entities and groups
path "identity/*" {

 capabilities = [ "create", "read", "update", "delete", "list" ]
}
```
### manager-policy
```shell
path "sys/policies/acl/administrator-policy"
{
 capabilities = ["deny"]
}
# Create and manage ACL policies broadly across Vault
# List existing policies
path "sys/policies/acl"
{
 capabilities = ["list"]
}
# Create and manage ACL policies
path "sys/policies/acl/*"
{
 capabilities = ["create", "read", "update", "delete", "list", "sudo"]
}
# Enable and manage authentication methods broadly across Vault
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
# Enable and manage the key/value secrets engine at `secret/` path
# List, create, update, and delete key/value secrets
path "secrets/*"
{
 capabilities = ["create", "read", "update", "delete", "list", "sudo"]
}
# Manage secrets engines
path "sys/mounts/*"
{
 capabilities = ["create", "read", "update", "delete", "list", "sudo"]
}
# List existing secrets engines.
path "sys/mounts"

{
capabilities = ["read"]
}
# Create and manage entities and groups
path "identity/*" {

 capabilities = [ "create", "read", "update", "delete", "list" ]
}
```
### moderator-policy
```shell
path "sys/policies/acl/administrator-policy"
{
 capabilities = ["deny"]
}
# Create and manage ACL policies broadly across Vault
# List existing policies
path "sys/policies/acl"
{
 capabilities = ["list"]
}
# Create and manage ACL policies
path "sys/policies/acl/*"
{
 capabilities = ["create", "read", "update", "delete", "list", "sudo"]
}
# Enable and manage authentication methods broadly across Vault
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
# Enable and manage the key/value secrets engine at `secret/` path
# List, create, update, and delete key/value secrets
path "secrets/*"
{
 capabilities = ["create", "read", "update", "delete", "list", "sudo"]
}
# Manage secrets engines
path "sys/mounts/*"
{
 capabilities = ["create", "read", "update", "delete", "list", "sudo"]
}
# List existing secrets engines.
path "sys/mounts"

{
capabilities = ["read"]
}
# Create and manage entities and groups
path "identity/*" {

 capabilities = [ "create", "read", "update", "delete", "list" ]
}
```
#### some Sam-solutions LDAP's groups

name | OU | participant
------------ | ------------ | ---------
9pc16  | Common | Oleg, Egor
samsoltr | Common | Oleg
wireless | Common | Oleg
homedirs| systems|Egor

```shell
vault write identity/group name="9pc16" type="external" policies="9pc16"
vault write identity/group name="samsoltr" type="external" policies="samsoltr"
vault write identity/group name="wireless" type="external" policies="wireless"
vault write identity/group name="homedirs" type="external" policies="homedirs"

```

#### Guest 
```
vault write auth/token/roles/guest allowed_policies="admin" period="10m"
vault token create -role=guest
vault token lookup
vault list auth/token/roles/guest

```


#### AD secrets

```
vault write ad/config binddn='sheka@sam-solutions.net' bindpass='ASDF1234zxcv' url=ldap://adldap.sam-solutions.net:389 userdn='OU=SamSol,OU=Belcaf,DC=sam-solutions,DC=net'
```


1. Пока что нет возможности делаить админа через токины. как хранить эти токены.
2. Пропал userpass 
3. Нет возможности добавлять сущности в группы + связка с AD
4. Неудобный функционал поиска.
5. член группы пропал
6. баг с участинком группы, надо именно кликнуть на id участника

https://www.vaultproject.io/docs/concepts/policies

https://www.hashicorp.com/resources/a-vault-policy-masterclass






 



##  OAuth2
This feature requires [Vault Enterprise](https://www.hashicorp.com/products/vault/) with the Governance & Policy Module.
https://www.hashicorp.com/products/vault/pricing

vault write sys/mfa/method/duo/my_duo   mount_accessor=auth_userpass_763b7ff9 integration_key=BIACEUEAXI20BNWTEYXT  secret_key=HIGTHtrIigh2rPZQMbguugt8IUftWhMRCOBzbuyz api_hostname=api-2b5c39f5.duosecurity.com


https://habr.com/ru/company/flant/blog/475942/

##  AZURA
https://nedinthecloud.com/2019/01/23/using-azure-active-directory-authentication-with-hashicorp-vault-part-1/

```

az account list


az ad sp create-for-rbac --name http://vaultsp --role reader --scopes /subscriptions/0cb7d2f9-96eb-4889-b4d4-cb3d259cefb3



export AZURE_SUBSCRIPTION_ID = 0cb7d2f9-96eb-4889-b4d4-cb3d259cefb3
export AZURE_TENANT_ID = 2a78cc87-d03f-4765-8d1a-111bae13a3bc

export AZURE_CLIENT_ID = 658d01c4-fd17-4755-8bbf-dc99037cfc66
export AZURE_CLIENT_SECRET = ykg_2U9wF2YsCGaX3J8Nt03TTy5_TvsqC-



https://docs.microsoft.com/en-us/rest/api/azure/

vault write auth/azure/config tenant_id=645e4888-741e-4b49-a564-82ff42b5e5ba resource="https://management.core.windows.net/ client_id=49bc53b8-be0e-49fd-9649-3354c8e75652 client_secret=ODrwCpvSv9LzwtJuHYG93Vr-Y\_.8thZ~~6


vault write auth/azure/role/web-role policies="web" bound_subscription_ids=0cb7d2f9-96eb-4889-b4d4-cb3d259cefb3 bound_resource_groups=vault


vault write auth/azure/login role="web-role" jwt="eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Im5PbzNaRHJPRFhFSzFqS1doWHNsSFJfS1hFZyIsImtpZCI6Im5PbzNaRHJPRFhFSzFqS1doWHNsSFJfS1hFZyJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuY29yZS53aW5kb3dzLm5ldC8iLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC8yYTc4Y2M4Ny1kMDNmLTQ3NjUtOGQxYS0xMTFiYWUxM2EzYmMvIiwiaWF0IjoxNjEyNTQyNzI3LCJuYmYiOjE2MTI1NDI3MjcsImV4cCI6MTYxMjU0NjYyNywiYWNyIjoiMSIsImFpbyI6IkFVUUF1LzhUQUFBQTl1am1pZlBQZHBnWlZzMllGdjVOUjN3Wis3cmVZQUlYODIwYS9lNk9OZFRNalltWU16VmVlVWdZNzRaVTg1cEVrNG4zVzh3THZiRURSaWdaMjZyd1p3PT0iLCJhbHRzZWNpZCI6IjE6bGl2ZS5jb206MDAwM0JGRkRGNkI3OTE1MyIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJjNDRiNDA4My0zYmIwLTQ5YzEtYjQ3ZC05NzRlNTNjYmRmM2MiLCJhcHBpZGFjciI6IjIiLCJlbWFpbCI6ImVnb3JzaGVrYUBvdXRsb29rLmNvbSIsImZhbWlseV9uYW1lIjoiU2hla2EiLCJnaXZlbl9uYW1lIjoiRWdvciIsImdyb3VwcyI6WyI2NjAxZmRiNi03ZjcyLTQ5NzYtYWZiOS0wNTIwY2UyOTI2MWIiXSwiaWRwIjoibGl2ZS5jb20iLCJpcGFkZHIiOiI5My4xMjUuMTA3LjQ4IiwibmFtZSI6IkVnb3IgU2hla2EiLCJvaWQiOiI1NmFkODM3OS1kNDgzLTQ3YmYtODE0NC1kOWRhNDg3ZDVjZTYiLCJwdWlkIjoiMTAwMzIwMDExNDBFOUFBRiIsInJoIjoiMC5BQUFBaDh4NEtqX1FaVWVOR2hFYnJoT2p2SU5BUzhTd084Rkp0SDJYVGxQTDN6eUJBTkUuIiwic2NwIjoidXNlcl9pbXBlcnNvbmF0aW9uIiwic3ViIjoic1ZSQUFFek9ZeldYUFgzT1Q2RzBROVBCRUhONHBSbUxoS2x1Qnhvczg2OCIsInRpZCI6IjJhNzhjYzg3LWQwM2YtNDc2NS04ZDFhLTExMWJhZTEzYTNiYyIsInVuaXF1ZV9uYW1lIjoibGl2ZS5jb20jZWdvcnNoZWthQG91dGxvb2suY29tIiwidXRpIjoibTY1dlkzUjJwRTJDT0l2ZEVPSXNBQSIsInZlciI6IjEuMCIsIndpZHMiOlsiNjJlOTAzOTQtNjlmNS00MjM3LTkxOTAtMDEyMTc3MTQ1ZTEwIl0sInhtc190Y2R0IjoxNjEyNTM1NDcyfQ.U9ho4DRQdqBqPVqJ7kqPHJVZh62R9nqw6x6oTzuACtDUzn4oVRZmzVCa5KvnlnTrfsse3GgFYbeEoqPYOWTeoojUMBL48NzKR_0BjagVrtlrTCRxR7JmwRgYoiLGFlIx34-f99sNF7e2ZLRoqe9k3SEo-jO021CtP3205KzuTpej9cRgOsoobMgVv65uZpvgRqHuSKrLCmgo8pqt6Eyxq5sk6UxT1O3LUhcyUBs827OLDexsfG8mug_svwKwEMTBHuEOj1OsibPZrHcbOjDbZJk8zj8q9zmerQmDFQfCb4-0CmVVKPJNuEiuCsd0dxv9LD_5erikGI00NAJSfUIsEA" subscription_id="0cb7d2f9-96eb-4889-b4d4-cb3d259cefb3" resource_group_name="vault" vm_name="vault_demo"




645e4888-741e-4b49-a564-82ff42b5e5ba
sam-solutions.net

curl -s 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fmanagement.core.windows.net%2F' -H Metadata:true




https://docs.microsoft.com/en-us/rest/api/azure/


vault write auth/azure/config tenant_id=2a78cc87-d03f-4765-8d1a-111bae13a3bc resource=https://management.core.windows.net/ client_id=2c3e0b4c-9902-4c4c-a69e-4b5fdb084479 client_secret=yw-5HRb2C-RyJBXvGoS-Mq.osW~43eUT7Y

vault write auth/azure/role/dev-role  policies="azure" bound_subscription_ids="0cb7d2f9-96eb-4889-b4d4-cb3d259cefb3" bound_resource_groups="vault" ttl=24h max_ttl=48h

vault write auth/azure/login role="dev-role" jwt="eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Im5PbzNaRHJPRFhFSzFqS1doWHNsSFJfS1hFZyIsImtpZCI6Im5PbzNaRHJPRFhFSzFqS1doWHNsSFJfS1hFZyJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuY29yZS53aW5kb3dzLm5ldC8iLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC8yYTc4Y2M4Ny1kMDNmLTQ3NjUtOGQxYS0xMTFiYWUxM2EzYmMvIiwiaWF0IjoxNjE0NjIyNDM4LCJuYmYiOjE2MTQ2MjI0MzgsImV4cCI6MTYxNDYyNjMzOCwiYWNyIjoiMSIsImFpbyI6IkFXUUFtLzhUQUFBQVRQMHRDVmhjdmpBVE5yK05GdDVlVVlsbVJwV1d6Y0g5UkNlcnBzQXdGZGczZWZWVDdTeGp6SVVXZzlyUE1pajdzZGZ3bEJlWnBDZmw0SmZvRUR1MFJHYXUxZW5VdjE1M2VYWkxJNHhSckd4NGFOT3ZwdVZCZ0xwbmdTR00rKzdRIiwiYWx0c2VjaWQiOiIxOmxpdmUuY29tOjAwMDNCRkZERjZCNzkxNTMiLCJhbXIiOlsicHdkIiwibWZhIl0sImFwcGlkIjoiYzQ0YjQwODMtM2JiMC00OWMxLWI0N2QtOTc0ZTUzY2JkZjNjIiwiYXBwaWRhY3IiOiIyIiwiZW1haWwiOiJlZ29yc2hla2FAb3V0bG9vay5jb20iLCJmYW1pbHlfbmFtZSI6IlNoZWthIiwiZ2l2ZW5fbmFtZSI6IkVnb3IiLCJncm91cHMiOlsiNjYwMWZkYjYtN2Y3Mi00OTc2LWFmYjktMDUyMGNlMjkyNjFiIl0sImlkcCI6ImxpdmUuY29tIiwiaXBhZGRyIjoiOTMuMTI1LjEwNy40OCIsIm5hbWUiOiJFZ29yIFNoZWthIiwib2lkIjoiNTZhZDgzNzktZDQ4My00N2JmLTgxNDQtZDlkYTQ4N2Q1Y2U2IiwicHVpZCI6IjEwMDMyMDAxMTQwRTlBQUYiLCJyaCI6IjAuQUFBQWg4eDRLal9RWlVlTkdoRWJyaE9qdklOQVM4U3dPOEZKdEgyWFRsUEwzenlCQU5FLiIsInNjcCI6InVzZXJfaW1wZXJzb25hdGlvbiIsInN1YiI6InNWUkFBRXpPWXpXWFBYM09UNkcwUTlQQkVITjRwUm1MaEtsdUJ4b3M4NjgiLCJ0aWQiOiIyYTc4Y2M4Ny1kMDNmLTQ3NjUtOGQxYS0xMTFiYWUxM2EzYmMiLCJ1bmlxdWVfbmFtZSI6ImxpdmUuY29tI2Vnb3JzaGVrYUBvdXRsb29rLmNvbSIsInV0aSI6ImllQmVQNDlaOTBhVVNwdmQwMHRsQUEiLCJ2ZXIiOiIxLjAiLCJ3aWRzIjpbIjYyZTkwMzk0LTY5ZjUtNDIzNy05MTkwLTAxMjE3NzE0NWUxMCJdLCJ4bXNfdGNkdCI6MTYxMjUzNTQ3Mn0.Gcu_vofdERucE8dBUsD18E-OnXzx4eX28CaOG-rFvYy4rA5Qm2tXUL1lg3znq9PagYmLlMlioCKeop4iA562zRzJ43dAILNSmvOLyGwN5hRsmUtTamCGe_ssxQBKltx3jugmB1rj_BxcT6WHGxH3Lx1JsHthUcJg7r19FbrYl5CNCgQJd8VyFX1_vMfCjjmLAlpV6-5DhrnJEvMZ7GMVNKwKj5GfJK-ukP7J1FKjgMJaVCn1pbagRptxU9F8qRegZt2oDnfoChmyhYeiAgVby63YT7rGFOZOESBqHtyGvDG760P8rlbMlmDxToq37RbVW_2hkuMu2JvhY6YosNHvzw" subscription_id="0cb7d2f9-96eb-4889-b4d4-cb3d259cefb3" resource_group_name="vault" vm_name="vault"



 unable to retrieve virtual machine metadata: compute.VirtualMachinesClient#Get: Failure responding to request: StatusCode=403 -- Original Error: autorest/azure: Service returned an error. Status=403 Code="AuthorizationFailed" Message="The client '59a6f283-cfd2-4b56-9d46-f808552692e3' with object id '59a6f283-cfd2-4b56-9d46-f808552692e3' does not have authorization to perform action 'Microsoft.Compute/virtualMachines/read' over scope '/subscriptions/0cb7d2f9-96eb-4889-b4d4-cb3d259cefb3/resourceGroups/vault/providers/Microsoft.Compute/virtualMachines/vault' or the scope is invalid. If access was recently granted, please refresh your credentials."
 
 
 https://github.com/hashicorp/vault-plugin-auth-azure/issues/26


az account set --subscription="0cb7d2f9-96eb-4889-b4d4-cb3d259cefb3"








vault write azure/config  subscription_id=0cb7d2f9-96eb-4889-b4d4-cb3d259cefb3  tenant_id=2a78cc87-d03f-4765-8d1a-111bae13a3bc  client_id=2c3e0b4c-9902-4c4c-a69e-4b5fdb084479  client_secret=yw-5HRb2C-RyJBXvGoS-Mq.osW~43eUT7Y



https://learn.hashicorp.com/tutorials/vault/azure-secrets








vault auth list -detailed

vault write sys/mfa/method/duo/my_duo  mount_accessor=auth_userpass_fc02f590 integration_key=DIUTZCP5J5XZ3Y7TC85L secret_key=PvYN0RQ6NehjlYc4V9M9NsvbSqjDskZjvABV6Led  api_hostname=api-beae8b85.duosecurity.com





Authentication failed: 1 error occurred: \* error connecting to host "ldap://adldap.sam-solutions.net:636": LDAP Result Code 200 "Network Error": dial tcp 192.168.111.19:636: i/o timeout



![[Pasted image 20210302111653.png]]



```

vault write auth/azure/role/web-role bound_subscription_ids=0cb7d2f9-96eb-4889-b4d4-cb3d259cefb3 bound_resource_groups=vault


3. разобрать что за группы(security и distribution) в ldap и обрабатываются ли они в vault
  ![[Pasted image 20210202173440.png]]
  
  **В vault нет возможности работы с данными параметрами**
  (настройки-парамтеры-общие-группы рассылки (создвние тестовой группы))
4. как убрать все аунтификации, оставить root, ldap, username   **не нашёл**
5. делать доку - вопрос ответ 
6. какая интеграция в AZURA https://www.itinsights.org/HashiCorp-Vault-Authenticate-and-authorize-AzureAD-Users/ можно также сделать как и в ldap.
7. 2auth
8. найти обёртку на vault. (vault ui manager)





Хотя в настоящее время прямой реализации Azure AD для пользователей-людей не существует, метод аутентификации JWT / OIDC обеспечивает способ включения аутентификации и авторизации для пользователей Azure AD в HashiCorp Vault.
## Находки
можно создавать группы в auth/ldap

почитать про wrap инг, возможность упоковывать и отправлять пароли 




### Проблема делегирования 
https://github.com/hashicorp/vault/issues/1043

https://www.youtube.com/watch?v=oDdDPU6moTs&t=2111s
Единственное, что я могу предложить на данный момент, - это настроить экземпляр Vault для каждого пользователя, если вам нужна такая функциональность

____ 
### Links
- [[00 DevOps]]https://www.youtube.com/watch?v=G46ovYs_9hs