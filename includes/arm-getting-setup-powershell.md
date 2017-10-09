## <a name="setting-up-powershell-for-resource-manager-templates"></a><span data-ttu-id="a2ecb-101">Настройка PowerShell для шаблонов диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="a2ecb-101">Setting up PowerShell for Resource Manager templates</span></span>
<span data-ttu-id="a2ecb-102">Прежде чем использовать Azure PowerShell с помощью диспетчера ресурсов, необходимо будет toohave hello нужные Azure PowerShell и Windows PowerShell версии.</span><span class="sxs-lookup"><span data-stu-id="a2ecb-102">Before you can use Azure PowerShell with Resource Manager, you will need toohave hello right Windows PowerShell and Azure PowerShell versions.</span></span>

### <a name="verify-powershell-versions"></a><span data-ttu-id="a2ecb-103">Проверка версий PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2ecb-103">Verify PowerShell versions</span></span>
<span data-ttu-id="a2ecb-104">Убедитесь, что Windows PowerShell имеет версию 3.0 или 4.0.</span><span class="sxs-lookup"><span data-stu-id="a2ecb-104">Verify you have Windows PowerShell version 3.0 or 4.0.</span></span> <span data-ttu-id="a2ecb-105">toofind hello версии Windows PowerShell, введите эту команду в командной строке Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a2ecb-105">toofind hello version of Windows PowerShell, type this command at a Windows PowerShell command prompt.</span></span>

    $PSVersionTable

<span data-ttu-id="a2ecb-106">Вы получите hello следующий тип данных:</span><span class="sxs-lookup"><span data-stu-id="a2ecb-106">You will receive hello following type of information:</span></span>

    Name                           Value
    ----                           -----
    PSVersion                      3.0
    WSManStackVersion              3.0
    SerializationVersion           1.1.0.1
    CLRVersion                     4.0.30319.18444
    BuildVersion                   6.2.9200.16481
    PSCompatibleVersions           {1.0, 2.0, 3.0}
    PSRemotingProtocolVersion      2.2


<span data-ttu-id="a2ecb-107">Убедитесь, что значение hello объекта **PSVersion** 3.0 или 4.0.</span><span class="sxs-lookup"><span data-stu-id="a2ecb-107">Verify that hello value of **PSVersion** is 3.0 or 4.0.</span></span> <span data-ttu-id="a2ecb-108">Если указано другое значение, см. статью [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) или [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="a2ecb-108">If not, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="a2ecb-109">Настройка учетной записи и подписки Azure</span><span class="sxs-lookup"><span data-stu-id="a2ecb-109">Set your Azure account and subscription</span></span>
<span data-ttu-id="a2ecb-110">Если у вас нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или зарегистрироваться в [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2ecb-110">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="a2ecb-111">Откройте командную строку Azure PowerShell и войти в систему tooAzure с помощью этой команды.</span><span class="sxs-lookup"><span data-stu-id="a2ecb-111">Open an Azure PowerShell command prompt and log on tooAzure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="a2ecb-112">Если у вас есть несколько подписок Azure, их список можно получить с помощью такой команды:</span><span class="sxs-lookup"><span data-stu-id="a2ecb-112">If you have multiple Azure subscriptions, you can list your Azure subscriptions with this command.</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="a2ecb-113">Вы получите hello следующий тип данных:</span><span class="sxs-lookup"><span data-stu-id="a2ecb-113">You will receive hello following type of information:</span></span>

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

<span data-ttu-id="a2ecb-114">Можно задать hello текущую подписку Azure, выполнив эти команды в командной строке Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="a2ecb-114">You can set hello current Azure subscription by running these commands at hello Azure PowerShell command prompt.</span></span> <span data-ttu-id="a2ecb-115">Замените весь код внутри кавычек hello, включая hello < и > символы, с правильным именем hello.</span><span class="sxs-lookup"><span data-stu-id="a2ecb-115">Replace everything within hello quotes, including hello < and > characters, with hello correct name.</span></span>

    $subscr="<SubscriptionName from hello display of Get-AzureRmSubscription>"
    Select-AzureRmSubscription -SubscriptionName $subscr -Current

<span data-ttu-id="a2ecb-116">Дополнительные сведения о подписках Azure и учетных записей см. в разделе [как: подключение подписки tooyour](/powershell/azureps-cmdlets-docs#step-3-connect).</span><span class="sxs-lookup"><span data-stu-id="a2ecb-116">For more information about Azure subscriptions and accounts, see [How to: Connect tooyour subscription](/powershell/azureps-cmdlets-docs#step-3-connect).</span></span>

