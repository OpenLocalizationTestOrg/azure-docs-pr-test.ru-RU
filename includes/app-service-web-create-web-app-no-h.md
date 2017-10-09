Создание [веб-приложения](../articles/app-service-web/app-service-web-overview.md) в hello `myAppServicePlan` план служб приложений с hello [создать веб-приложение az](/cli/azure/webapp#create) команды. 

веб-приложения Hello место размещения для кода и предоставляет URL-адрес tooview hello развертывания приложения.

В hello следующую команду, замените  *\<имя_приложения >* с уникальным именем (допустимые символы — `a-z`, `0-9`, и `-`). Если `<app_name>` является не уникален, вы получаете сообщение hello «Веб-сайт с данным именем < имя_приложения > уже существует.» Здравствуйте, по умолчанию используется URL-адрес веб-приложения hello `https://<app_name>.azurewebsites.net`. 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

При создании веб-приложения hello hello Azure CLI показано toohello аналогичные сведения, следующий пример:

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

Обзор узла toosee toohello только что созданный веб-приложения.

```bash
http://<app_name>.azurewebsites.net
```
