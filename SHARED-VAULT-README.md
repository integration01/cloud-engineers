# Shared OCI Vault
All engineers can use shared Vaults within the `cloud-engineering-vault` compartment.  We have these for both Ashburn and Phoenix. This prevents everyone from needing to maintain their own vault.  All services requiring vault access should be enabled and working with keys from the vault.

* Do not attempt to create a Virtual Private Vault, as these have a high additional cost.

## Using the Vault
Simply navigate to Vaults and change compartment to `cloud-engineering-vault`.  Depending on region, select the vault to use.  Create Keys and secrets here.  Within any resource requiring a vault, you have access to these keys. Simply select the correct compartment and secret when requiring a key.  For example, when standing up a resource stack, you might need to change the compartment to find your key. 

### Master Encryption Keys
It is recommended to create a Madster Key (MEK) with your initials at the front, ie `AG-MEK`, so it is easy to find when creating secrets.  

### Secrets
Secrets can be created for various database and middleware products.  Follow the same strategy as above, prepending your initials.  The secret should reflect what it is.  Example: `AG-WLS-PWD` or `AG-DATABASE-SYS`.

### Examples (Needed for SQL Worksheet and DB Management)
![Vault Sys](images/Vault-Database-SysPassword.png)
![DBM Vault](images/Vault-Database-DbsnmpPassword.png)
