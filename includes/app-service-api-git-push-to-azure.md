<span data-ttu-id="82279-101">С помощью Azure CLI получите URL-адрес удаленного развертывания для своего приложения API.</span><span class="sxs-lookup"><span data-stu-id="82279-101">Use the Azure CLI to get the remote deployment URL for your API App.</span></span> <span data-ttu-id="82279-102">В следующей команде замените *\<имя_приложения>* именем своего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="82279-102">In the following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="82279-103">Настройте локальное развертывание Git, чтобы вы могли принудительно отправлять данные в удаленный репозиторий.</span><span class="sxs-lookup"><span data-stu-id="82279-103">Configure your local Git deployment to be able to push to the remote.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="82279-104">Отправьте код в удаленную службу приложений Azure, чтобы развернуть приложение.</span><span class="sxs-lookup"><span data-stu-id="82279-104">Push to the Azure remote to deploy your app.</span></span> <span data-ttu-id="82279-105">После этого введите пароль, указанный ранее при создании пользователя развертывания.</span><span class="sxs-lookup"><span data-stu-id="82279-105">You are prompted for the password you created earlier when you created the deployment user.</span></span> <span data-ttu-id="82279-106">Следует ввести пароль, созданный в рамках краткого руководства, а не тот, который использовался для входа на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="82279-106">Make sure that you enter the password you created in earlier in the quickstart, and not the password you use to log in to the Azure portal.</span></span>

```bash
git push azure master
```
