<span data-ttu-id="dbf6f-101">Войдите в подписку Azure совместно с hello tooyour [входа az](/cli/azure/#login) команды и выполните hello на экране инструкциям.</span><span class="sxs-lookup"><span data-stu-id="dbf6f-101">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> <span data-ttu-id="dbf6f-102">Дополнительные сведения о входе в систему см. в статье [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli) (Приступая к работе с Azure CLI 2.0).</span><span class="sxs-lookup"><span data-stu-id="dbf6f-102">For more information about logging in, see [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

```azurecli
az login
```

<span data-ttu-id="dbf6f-103">При наличии более чем одной подписки Azure, список hello подписки для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="dbf6f-103">If you have more than one Azure subscription, list hello subscriptions for hello account.</span></span>

```azurecli
az account list --all
```

<span data-ttu-id="dbf6f-104">Укажите требуемый toouse подписки hello.</span><span class="sxs-lookup"><span data-stu-id="dbf6f-104">Specify hello subscription that you want toouse.</span></span>

```azurecli
az account set --subscription <replace_with_your_subscription_id>
```