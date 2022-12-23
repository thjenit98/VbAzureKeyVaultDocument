##VB.NET Get & Set Azure Key Vault
> #### 1. Setup Azure Portal
**1.1 Create service KeyVault**
- Create service Key Vault from Azure Portal Resource
- Setting service
![Setting sevice!](/Imgs/4-setting-service.png)
  * Choose your subscription
  * Create new Resource group or choose your Resource group exist
  * Create key vault name
  * Choose region

**1.2 Create service Managed Identity**
- Create service Managed Identity from Azure Portal Resource
- Setting service
![Setting sevice!](/Imgs/5-setting-managed-identity.png)
  * Choose your subscription
  * Create new Resource group or choose your Resource group exist
  * Choose region
  * Create name for managed identity
- Config Azure Role Assignments
![Setting sevice!](/Imgs/6-config-role-assignments.png)
  * Choose Scope => Key Vault
  * Choose your subscription
  * Choose your key vault resource
  * Choose role assigned

> #### 1. Setup Azure Cli
``az login``

> #### 2. Setup VB.NET Project
- Create VB.NET Console App
- Install 2 nuget packages
  * Azure.Identity
  * Azure.Security.KeyVault.Secrets
- Implement code below
```
Dim managedIdentityClientId As String = "893810b9-99d7-40fb-9e83-c162b92957fc"
Dim vaultUrl As String = "https://keylab83825ae1b3260e4.vault.azure.net/"

Sub Main()
    Dim credentialOption As DefaultAzureCredentialOptions = New DefaultAzureCredentialOptions()
    credentialOption.ManagedIdentityClientId = managedIdentityClientId

    Dim credential As DefaultAzureCredential = New DefaultAzureCredential(credentialOption)

    Dim client As SecretClient = New SecretClient(New Uri(vaultUrl), credential)

    Dim secret As KeyVaultSecret = client.SetSecret("keylab83825ae1b3260e4", "thjenit98")
    Dim secretValue As KeyVaultSecret = client.GetSecret("keylab83825ae1b3260e4")
    Dim secretValue1 As KeyVaultSecret = client.GetSecret("keylab83825ae1b3260e4")

    Console.WriteLine("Key vault secret value: " & secretValue.Value)
    Console.WriteLine("Key vault secret value 1: " & secretValue1.Value)

    Console.ReadLine()
End Sub
```
- Run you can get value of secret name **keylab83825ae1b3260e4** and create new secret **keylab83825ae1b3260e4**
![Result!](/Imgs/7-result.png)