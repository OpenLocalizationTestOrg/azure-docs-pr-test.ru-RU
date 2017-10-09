
## <a name="start-your-powershell-session"></a>Запуск сеанса PowerShell
Сначала необходимо toohave hello, последняя версия [Azure PowerShell](http://msdn.microsoft.com/library/mt619274.aspx) установлена и запущена. Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs).

> [!NOTE]
> Здравствуйте, примеры в этом разделе используют [модели развертывания диспетчера ресурсов Azure](../articles/azure-resource-manager/resource-group-overview.md), поэтому примеры используют hello [командлеты диспетчера ресурсов Azure](http://msdn.microsoft.com/library/azure/mt125356.aspx). 
> 
> 

Запустите hello [ **добавить AzureRmAccount** ](http://msdn.microsoft.com/library/mt619267.aspx) командлета и предоставят вход tooenter экрана учетные данные. Используйте hello же учетные данные, используемые toosign в toohello портал Azure.

    Add-AzureRmAccount

При наличии нескольких подписок используйте hello [ **набор AzureRmContext** ](http://msdn.microsoft.com/library/mt619263.aspx) tooselect командлета какие подписки следует использовать сеанс PowerShell. какие подписки hello текущего PowerShell в сеансе используется toosee запуска [ **Get AzureRmContext**](http://msdn.microsoft.com/library/mt619265.aspx). toosee все подписки, запустите [ **Get AzureRmSubscription**](http://msdn.microsoft.com/library/mt619284.aspx).

    Set-AzureRmContext -SubscriptionId '4cac86b0-1e56-bbbb-aaaa-000000000000'

