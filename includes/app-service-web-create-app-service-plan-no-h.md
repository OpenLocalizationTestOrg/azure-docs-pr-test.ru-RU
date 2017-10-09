Создать план служб приложений с hello [создать план служб приложений az](/cli/azure/appservice/plan#create) команды.

[!INCLUDE [app-service-plan](app-service-plan.md)]

Hello следующий пример создает план службы приложений с именем `myAppServicePlan` в hello **Free** ценовой категории:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

При создании плана служб приложений hello hello Azure CLI показано toohello аналогичные сведения, следующий пример:

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "West Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  < JSON data removed for brevity. >
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
} 
```