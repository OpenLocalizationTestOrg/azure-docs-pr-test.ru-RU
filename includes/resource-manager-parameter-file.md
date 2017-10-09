При использовании значения параметра toopass файл во время развертывания необходимо toocreate JSON-файла с аналогичные toohello формата, следующий пример:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "webSiteName": {
            "value": "ExampleSite"
        },
        "webSiteHostingPlanName": {
            "value": "DefaultPlan"
        },
        "webSiteLocation": {
            "value": "West US"
        },
        "adminPassword": {
            "reference": {
               "keyVault": {
                  "id": "/subscriptions/{guid}/resourceGroups/{group-name}/providers/Microsoft.KeyVault/vaults/{vault-name}"
               }, 
               "secretName": "sqlAdminPassword" 
            }   
        }
   }
}
```

размер Hello hello параметр файла не может быть более 64 КБ.

Если вам требуется tooprovide конфиденциальное значение для параметра (например, пароля), добавьте хранилище ключей, значение tooa. Получить hello хранилища ключей во время развертывания, как показано в предыдущем примере hello. Дополнительные сведения см. в статье [Передача безопасных значений в процессе развертывания](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md). 

