<span data-ttu-id="33145-101">Перед началом этой конфигурации, необходимо войти в tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="33145-101">Before beginning this configuration, you must log in tooyour Azure account.</span></span> <span data-ttu-id="33145-102">Hello командлет запросит hello учетные данные входа для учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="33145-102">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="33145-103">После входа в систему, он загружает параметры учетной записи, таким образом, они будут доступны tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="33145-103">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span> <span data-ttu-id="33145-104">Дополнительные сведения см. в статье [Использование Azure PowerShell с диспетчером ресурсов Azure](../articles/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="33145-104">For more information, see [Using Windows PowerShell with Resource Manager](../articles/powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="33145-105">toolog, откройте консоль PowerShell с повышенными привилегиями и подключите tooyour учетную запись.</span><span class="sxs-lookup"><span data-stu-id="33145-105">toolog in, open your PowerShell console with elevated privileges, and connect tooyour account.</span></span> <span data-ttu-id="33145-106">Используйте следующий пример toohelp подключении hello.</span><span class="sxs-lookup"><span data-stu-id="33145-106">Use hello following example toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="33145-107">Если у вас несколько подписок Azure, проверьте hello подписки для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="33145-107">If you have multiple Azure subscriptions, check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="33145-108">Укажите требуемый toouse подписки hello.</span><span class="sxs-lookup"><span data-stu-id="33145-108">Specify hello subscription that you want toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```