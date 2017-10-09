
<span data-ttu-id="d9757-101">Создание [приложения API](../articles/app-service-api/app-service-api-apps-why-best-platform.md) в hello `myAppServicePlan` план служб приложений с hello [создать веб-приложение az](/cli/azure/appservice/web#create) команды.</span><span class="sxs-lookup"><span data-stu-id="d9757-101">Create a [API app](../articles/app-service-api/app-service-api-apps-why-best-platform.md) in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/appservice/web#create) command.</span></span> 

<span data-ttu-id="d9757-102">веб-приложения Hello место размещения для API и предоставляет URL-адрес tooview hello развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="d9757-102">hello web app provides a hosting space for your API and provides a URL tooview hello deployed app.</span></span>

<span data-ttu-id="d9757-103">В hello следующую команду, замените  *\<имя_приложения >* с уникальным именем.</span><span class="sxs-lookup"><span data-stu-id="d9757-103">In hello following command, replace *\<app_name>* with a unique name.</span></span> <span data-ttu-id="d9757-104">Если `<app_name>` является не уникален, вы получаете сообщение hello «Веб-сайт с данным именем < имя_приложения > уже существует.»</span><span class="sxs-lookup"><span data-stu-id="d9757-104">If `<app_name>` is not unique, you get hello error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="d9757-105">Здравствуйте, по умолчанию используется URL-адрес веб-приложения hello `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="d9757-105">hello default URL of hello web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="d9757-106">При создании веб-приложения hello hello Azure CLI показано toohello аналогичные сведения, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="d9757-106">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "<app_name>.azurewebsites.net",
    "<app_name>.scm.azurewebsites.net"
  ],
  "gatewaySiteName": null,
  "hostNameSslStates": [
    {
      "hostType": "Standard",
      "name": "<app_name>.azurewebsites.net",
      "sslState": "Disabled",
      "thumbprint": null,
      "toUpdate": null,
      "virtualIp": null
    }
    < JSON data removed for brevity. >
}
```