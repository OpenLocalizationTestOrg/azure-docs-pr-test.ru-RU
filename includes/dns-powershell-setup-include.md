## <a name="set-up-azure-powershell-for-azure-dns"></a><span data-ttu-id="00ddc-101">Настройка Azure PowerShell для Azure DNS</span><span class="sxs-lookup"><span data-stu-id="00ddc-101">Set up Azure PowerShell for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="00ddc-102">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="00ddc-102">Before you begin</span></span>

<span data-ttu-id="00ddc-103">Проверьте наличие следующих элементов перед началом настройки hello.</span><span class="sxs-lookup"><span data-stu-id="00ddc-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="00ddc-104">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="00ddc-104">An Azure subscription.</span></span> <span data-ttu-id="00ddc-105">Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="00ddc-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="00ddc-106">Необходимо tooinstall hello последнюю версию hello командлеты PowerShell диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="00ddc-106">You need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="00ddc-107">Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="00ddc-107">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="00ddc-108">Войдите в tooyour учетная запись Azure</span><span class="sxs-lookup"><span data-stu-id="00ddc-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="00ddc-109">Откройте консоль PowerShell и подключить tooyour учетную запись.</span><span class="sxs-lookup"><span data-stu-id="00ddc-109">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="00ddc-110">Дополнительные сведения см. в статье [Использование Azure PowerShell с диспетчером ресурсов Azure](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="00ddc-110">For more information, see [Using PowerShell with Resource Manager](../articles/azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a><span data-ttu-id="00ddc-111">Выберите подписку hello</span><span class="sxs-lookup"><span data-stu-id="00ddc-111">Select hello subscription</span></span>
 
<span data-ttu-id="00ddc-112">Проверьте hello подписки для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="00ddc-112">Check hello subscriptions for hello account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="00ddc-113">Выберите, какие toouse вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="00ddc-113">Choose which of your Azure subscriptions toouse.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="00ddc-114">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="00ddc-114">Create a resource group</span></span>

<span data-ttu-id="00ddc-115">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="00ddc-115">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="00ddc-116">Это расположение используется в качестве расположения по умолчанию hello для ресурсов в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="00ddc-116">This location is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="00ddc-117">Тем не менее так как все ресурсы DNS глобального, не язык, выбор hello расположение группы ресурсов не оказывает влияния на Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="00ddc-117">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="00ddc-118">Если используется существующая группа ресурсов, можно пропустить этот шаг.</span><span class="sxs-lookup"><span data-stu-id="00ddc-118">You can skip this step if you are using an existing resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="00ddc-119">Регистрация поставщика ресурсов</span><span class="sxs-lookup"><span data-stu-id="00ddc-119">Register resource provider</span></span>

<span data-ttu-id="00ddc-120">Служба Azure DNS Hello управляется поставщика ресурсов Microsoft.Network hello.</span><span class="sxs-lookup"><span data-stu-id="00ddc-120">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="00ddc-121">Ваша подписка Azure должен быть зарегистрированных toouse этого поставщика ресурсов, прежде чем можно будет использовать Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="00ddc-121">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="00ddc-122">Эта операция выполняется один раз для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="00ddc-122">This is a one-time operation for each subscription.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```