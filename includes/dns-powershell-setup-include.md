## <a name="set-up-azure-powershell-for-azure-dns"></a><span data-ttu-id="f0883-101">Настройка Azure PowerShell для Azure DNS</span><span class="sxs-lookup"><span data-stu-id="f0883-101">Set up Azure PowerShell for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="f0883-102">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="f0883-102">Before you begin</span></span>

<span data-ttu-id="f0883-103">Перед началом настройки убедитесь, что у вас есть следующие компоненты.</span><span class="sxs-lookup"><span data-stu-id="f0883-103">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="f0883-104">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="f0883-104">An Azure subscription.</span></span> <span data-ttu-id="f0883-105">Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f0883-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f0883-106">Вам потребуется установить последнюю версию командлетов PowerShell Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f0883-106">You need to install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="f0883-107">Дополнительные сведения см. в статье [Установка и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="f0883-107">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="f0883-108">Вход в учетную запись Azure</span><span class="sxs-lookup"><span data-stu-id="f0883-108">Sign in to your Azure account</span></span>

<span data-ttu-id="f0883-109">Откройте консоль PowerShell и подключитесь к своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f0883-109">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="f0883-110">Дополнительные сведения см. в статье [Использование Azure PowerShell с диспетчером ресурсов Azure](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f0883-110">For more information, see [Using PowerShell with Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="select-the-subscription"></a><span data-ttu-id="f0883-111">Выбор подписки</span><span class="sxs-lookup"><span data-stu-id="f0883-111">Select the subscription</span></span>
 
<span data-ttu-id="f0883-112">Просмотрите подписки учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f0883-112">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="f0883-113">Выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="f0883-113">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="f0883-114">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="f0883-114">Create a resource group</span></span>

<span data-ttu-id="f0883-115">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="f0883-115">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="f0883-116">Это расположение используется в качестве расположения по умолчанию для всех ресурсов данной группы.</span><span class="sxs-lookup"><span data-stu-id="f0883-116">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="f0883-117">Но так как все ресурсы DNS глобальные, а не региональные, выбор расположения группы ресурсов не влияет на Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="f0883-117">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="f0883-118">Если используется существующая группа ресурсов, можно пропустить этот шаг.</span><span class="sxs-lookup"><span data-stu-id="f0883-118">You can skip this step if you are using an existing resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="f0883-119">Регистрация поставщика ресурсов</span><span class="sxs-lookup"><span data-stu-id="f0883-119">Register resource provider</span></span>

<span data-ttu-id="f0883-120">Служба Azure DNS управляется поставщиком ресурсов Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="f0883-120">The Azure DNS service is managed by the Microsoft.Network resource provider.</span></span> <span data-ttu-id="f0883-121">Вашу подписку Azure необходимо зарегистрировать, чтобы использовать этот поставщик ресурсов, прежде чем работать с Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="f0883-121">Your Azure subscription must be registered to use this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="f0883-122">Эта операция выполняется один раз для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="f0883-122">This is a one-time operation for each subscription.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```