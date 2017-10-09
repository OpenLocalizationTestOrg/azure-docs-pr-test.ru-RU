<span data-ttu-id="1a4c8-101">Создать план служб приложений с hello [создать план служб приложений az](/cli/azure/appservice/plan#create) команды.</span><span class="sxs-lookup"><span data-stu-id="1a4c8-101">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span>

[!INCLUDE [app-service-plan](app-service-plan.md)]

<span data-ttu-id="1a4c8-102">Hello следующий пример создает план службы приложений с именем `myAppServicePlan` в hello **Free** ценовой категории:</span><span class="sxs-lookup"><span data-stu-id="1a4c8-102">hello following example creates an App Service plan named `myAppServicePlan` in hello **Free** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="1a4c8-103">При создании плана служб приложений hello hello Azure CLI показано toohello аналогичные сведения, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="1a4c8-103">When hello App Service plan has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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