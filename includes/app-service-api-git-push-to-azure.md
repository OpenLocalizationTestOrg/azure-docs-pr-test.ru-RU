<span data-ttu-id="15c73-101">Используйте URL-адрес hello Azure CLI tooget hello удаленного развертывания для приложения API.</span><span class="sxs-lookup"><span data-stu-id="15c73-101">Use hello Azure CLI tooget hello remote deployment URL for your API App.</span></span> <span data-ttu-id="15c73-102">В hello следующую команду, замените  *\<имя_приложения >* с именем веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="15c73-102">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="15c73-103">Настройте ваш локальный Git развертывания toobe может toopush toohello удаленной.</span><span class="sxs-lookup"><span data-stu-id="15c73-103">Configure your local Git deployment toobe able toopush toohello remote.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="15c73-104">Принудительно toohello Azure toodeploy удаленного приложения.</span><span class="sxs-lookup"><span data-stu-id="15c73-104">Push toohello Azure remote toodeploy your app.</span></span> <span data-ttu-id="15c73-105">Запрашивается пароль hello, созданную ранее при создании пользователя развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="15c73-105">You are prompted for hello password you created earlier when you created hello deployment user.</span></span> <span data-ttu-id="15c73-106">Убедитесь, что введено hello пароль, созданный в более ранней версии в кратком руководстве hello и не hello использовать toolog в toohello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="15c73-106">Make sure that you enter hello password you created in earlier in hello quickstart, and not hello password you use toolog in toohello Azure portal.</span></span>

```bash
git push azure master
```
