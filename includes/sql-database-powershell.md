
## <a name="start-your-powershell-session"></a>Запуск сеанса PowerShell
Во-первых вы должны иметь hello последнюю версию Azure PowerShell установлена и запущена. Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs).

> [!NOTE]
> Множество новых функций базы данных SQL поддерживаются только в том случае, если вы используете hello [модели развертывания диспетчера ресурсов Azure](../articles/azure-resource-manager/resource-group-overview.md), поэтому примеры используют hello [базы данных SQL Azure PowerShell командлеты](https://msdn.microsoft.com/library/azure/mt574084\(v=azure.300\).aspx) для диспетчера ресурсов . модель развертывания Hello службы управления (классические) [командлетов для управления службой базы данных SQL Azure](https://msdn.microsoft.com/library/azure/dn546723\(v=azure.300\).aspx) поддерживаются для обеспечения обратной совместимости, но мы рекомендуем использовать hello командлеты диспетчера ресурсов.
> 
> 

Запустите hello [ **добавить AzureRmAccount** ](https://msdn.microsoft.com/library/azure/mt619267\(v=azure.300\).aspx) командлет и откроется tooenter экрана входа учетные данные. Используйте hello же учетные данные, используемые toosign в toohello портал Azure.

```PowerShell
Add-AzureRmAccount
```

Если у вас несколько подписок, используйте hello [ **набор AzureRmContext** ](https://msdn.microsoft.com/library/azure/mt619263\(v=azure.300\).aspx) tooselect командлета какие подписки следует использовать сеанс PowerShell. какие подписки hello текущего PowerShell в сеансе используется toosee запуска [ **Get AzureRmContext**](https://msdn.microsoft.com/library/azure/mt619265\(v=azure.300\).aspx). toosee все подписки, запустите [ **Get AzureRmSubscription**](https://msdn.microsoft.com/library/azure/mt619284\(v=azure.300\).aspx).

```PowerShell
Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'
```
