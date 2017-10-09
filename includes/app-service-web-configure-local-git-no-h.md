<span data-ttu-id="538f0-101">Настройте локальное веб-приложение toohello Git развертывания с hello [развертывания источника az webapp config локальной git](/cli/azure/webapp/deployment/source#config-local-git) команды.</span><span class="sxs-lookup"><span data-stu-id="538f0-101">Configure local Git deployment toohello web app with hello [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command.</span></span>

<span data-ttu-id="538f0-102">Службы приложений поддерживает несколько способов toodeploy tooa содержимого веб-приложения, таких как FTP, local Git, GitHub, Visual Studio Team Services и Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="538f0-102">App Service supports several ways toodeploy content tooa web app, such as FTP, local Git, GitHub, Visual Studio Team Services, and Bitbucket.</span></span> <span data-ttu-id="538f0-103">В рамках этого краткого руководства выполним развертывание с помощью локального репозитория Git.</span><span class="sxs-lookup"><span data-stu-id="538f0-103">For this quickstart, you deploy by using local Git.</span></span> <span data-ttu-id="538f0-104">Это означает, что развертывание выполняется с помощью команды Git toopush из репозитория tooa локального репозитория в Azure.</span><span class="sxs-lookup"><span data-stu-id="538f0-104">That means you deploy by using a Git command toopush from a local repository tooa repository in Azure.</span></span> 

<span data-ttu-id="538f0-105">В hello следующую команду, замените  *\<имя_приложения >* с именем веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="538f0-105">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="538f0-106">Выход Hello имеет hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="538f0-106">hello output has hello following format:</span></span>

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

<span data-ttu-id="538f0-107">Hello `<username>` — hello [пользователя развертывания](#configure-a-deployment-user) , созданный на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="538f0-107">hello `<username>` is hello [deployment user](#configure-a-deployment-user) that you created in a previous step.</span></span>

<span data-ttu-id="538f0-108">Скопируйте hello URI показано; оно будет использоваться в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="538f0-108">Copy hello URI shown; you'll use it in hello next step.</span></span>
