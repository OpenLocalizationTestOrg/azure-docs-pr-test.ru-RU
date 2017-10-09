Перед началом этой конфигурации, необходимо войти в tooyour учетная запись Azure. Hello командлет запросит hello учетные данные входа для учетной записи Azure. После входа в систему, он загружает параметры учетной записи, таким образом, они будут доступны tooAzure PowerShell. Дополнительные сведения см. в статье [Использование Azure PowerShell с диспетчером ресурсов Azure](../articles/powershell-azure-resource-manager.md).

toolog, откройте консоль PowerShell с повышенными привилегиями и подключите tooyour учетную запись. Используйте следующий пример toohelp подключении hello.

```powershell
Login-AzureRmAccount
```

Если у вас несколько подписок Azure, проверьте hello подписки для учетной записи hello.

```powershell
Get-AzureRmSubscription
```

Укажите требуемый toouse подписки hello.

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
 ```