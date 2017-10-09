<span data-ttu-id="9c926-101">При использовании значения параметра toopass файл во время развертывания необходимо toocreate JSON-файла с аналогичные toohello формата, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="9c926-101">If you use a parameter file toopass parameter values during deployment, you need toocreate a JSON file with a format similar toohello following example:</span></span>

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

<span data-ttu-id="9c926-102">размер Hello hello параметр файла не может быть более 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="9c926-102">hello size of hello parameter file cannot be more than 64 KB.</span></span>

<span data-ttu-id="9c926-103">Если вам требуется tooprovide конфиденциальное значение для параметра (например, пароля), добавьте хранилище ключей, значение tooa.</span><span class="sxs-lookup"><span data-stu-id="9c926-103">If you need tooprovide a sensitive value for a parameter (such as a password), add that value tooa key vault.</span></span> <span data-ttu-id="9c926-104">Получить hello хранилища ключей во время развертывания, как показано в предыдущем примере hello.</span><span class="sxs-lookup"><span data-stu-id="9c926-104">Retrieve hello key vault during deployment as shown in hello previous example.</span></span> <span data-ttu-id="9c926-105">Дополнительные сведения см. в статье [Передача безопасных значений в процессе развертывания](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="9c926-105">For more information, see [Pass secure values during deployment](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span> 

