Настройте локальное веб-приложение toohello Git развертывания с hello [развертывания источника az webapp config локальной git](/cli/azure/webapp/deployment/source#config-local-git) команды.

Службы приложений поддерживает несколько способов toodeploy tooa содержимого веб-приложения, таких как FTP, local Git, GitHub, Visual Studio Team Services и Bitbucket. В рамках этого краткого руководства выполним развертывание с помощью локального репозитория Git. Это означает, что развертывание выполняется с помощью команды Git toopush из репозитория tooa локального репозитория в Azure. 

В hello следующую команду, замените  *\<имя_приложения >* с именем веб-приложения.

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

Выход Hello имеет hello следующий формат:

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

Hello `<username>` — hello [пользователя развертывания](#configure-a-deployment-user) , созданный на предыдущем шаге.

Скопируйте hello URI показано; оно будет использоваться в следующем шаге hello.
