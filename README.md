# SQL-AzureBackup-Disable-using-Powershell
#Collection of commands given below will remove Recovery points of all the databases configured under given "server_name". Helpful when you have to disable thousands of DBs coming from a given server without which deleting the server from Server protection will not work.
$vault=Get-AzRecoveryServicesVault -name <Vault-Name>
Set-AzRecoveryServicesVaultContext -Vault $vault
$bkpItem = Get-AzRecoveryServicesBackupItem -BackupManagementType AzureWorkload -WorkloadType MSSQL -VaultId $vault.ID
$Item=$bkpItem| Where-Object { $_.ServerName -eq "server_name"}
foreach ($i in $Item)
{
Disable-AzRecoveryServicesBackupProtection -Item $i -VaultId $vault.ID -RemoveRecoveryPoints -Force 
}
Testing Pull request
