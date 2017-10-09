<span data-ttu-id="55ef7-101">Создание [веб-приложения](../articles/app-service-web/app-service-web-overview.md) в hello `myAppServicePlan` план служб приложений с hello [создать веб-приложение az](/cli/azure/webapp#create) команды.</span><span class="sxs-lookup"><span data-stu-id="55ef7-101">Create a [web app](../articles/app-service-web/app-service-web-overview.md) in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="55ef7-102">веб-приложения Hello место размещения для кода и предоставляет URL-адрес tooview hello развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="55ef7-102">hello web app provides a hosting space for your code and provides a URL tooview hello deployed app.</span></span>

<span data-ttu-id="55ef7-103">В hello следующую команду, замените  *\<имя_приложения >* с уникальным именем (допустимые символы — `a-z`, `0-9`, и `-`).</span><span class="sxs-lookup"><span data-stu-id="55ef7-103">In hello following command, replace *\<app_name>* with a unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="55ef7-104">Если `<app_name>` является не уникален, вы получаете сообщение hello «Веб-сайт с данным именем < имя_приложения > уже существует.»</span><span class="sxs-lookup"><span data-stu-id="55ef7-104">If `<app_name>` is not unique, you get hello error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="55ef7-105">Здравствуйте, по умолчанию используется URL-адрес веб-приложения hello `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="55ef7-105">hello default URL of hello web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="55ef7-106">При создании веб-приложения hello hello Azure CLI показано toohello аналогичные сведения, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="55ef7-106">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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

<span data-ttu-id="55ef7-107">Обзор узла toosee toohello только что созданный веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="55ef7-107">Browse toohello site toosee your newly created web app.</span></span>

```bash
http://<app_name>.azurewebsites.net
```
