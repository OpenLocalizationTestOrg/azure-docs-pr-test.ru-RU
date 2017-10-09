## <a name="setting-up-powershell-for-resource-manager-templates"></a>Настройка PowerShell для шаблонов диспетчера ресурсов
Прежде чем использовать Azure PowerShell с помощью диспетчера ресурсов, необходимо будет toohave hello нужные Azure PowerShell и Windows PowerShell версии.

### <a name="verify-powershell-versions"></a>Проверка версий PowerShell
Убедитесь, что Windows PowerShell имеет версию 3.0 или 4.0. toofind hello версии Windows PowerShell, введите эту команду в командной строке Windows PowerShell.

    $PSVersionTable

Вы получите hello следующий тип данных:

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


Убедитесь, что значение hello объекта **PSVersion** 3.0 или 4.0. Если указано другое значение, см. статью [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) или [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).

### <a name="set-your-azure-account-and-subscription"></a>Настройка учетной записи и подписки Azure
Если у вас нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или зарегистрироваться в [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).

Откройте командную строку Azure PowerShell и войти в систему tooAzure с помощью этой команды.

    Login-AzureRmAccount

Если у вас есть несколько подписок Azure, их список можно получить с помощью такой команды:

    Get-AzureRmSubscription

Вы получите hello следующий тип данных:

    SubscriptionId            : fd22919d-eaca-4f2b-841a-e4ac6770g92e
    SubscriptionName          : Visual Studio Ultimate with MSDN
    Environment               : AzureCloud
    SupportedModes            : AzureServiceManagement,AzureResourceManager
    DefaultAccount            : johndoe@contoso.com
    Accounts                  : {johndoe@contoso.com}
    IsDefault                 : True
    IsCurrent                 : True
    CurrentStorageAccountName :
    TenantId                  : 32fa88b4-86f1-419f-93ab-2d7ce016dba7

Можно задать hello текущую подписку Azure, выполнив эти команды в командной строке Azure PowerShell hello. Замените весь код внутри кавычек hello, включая hello < и > символы, с правильным именем hello.

    $subscr="<SubscriptionName from hello display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

Дополнительные сведения о подписках Azure и учетных записей см. в разделе [как: подключение подписки tooyour](/powershell/azureps-cmdlets-docs#step-3-connect).

