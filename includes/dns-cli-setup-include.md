## <a name="set-up-azure-cli-for-azure-dns"></a><span data-ttu-id="6bbac-101">Настройка интерфейса командной строки Azure для Azure DNS</span><span class="sxs-lookup"><span data-stu-id="6bbac-101">Set up Azure CLI for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="6bbac-102">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="6bbac-102">Before you begin</span></span>

<span data-ttu-id="6bbac-103">Перед началом настройки убедитесь, что у вас есть следующие компоненты.</span><span class="sxs-lookup"><span data-stu-id="6bbac-103">Verify that you have the following items before beginning your configuration.</span></span>

* <span data-ttu-id="6bbac-104">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="6bbac-104">An Azure subscription.</span></span> <span data-ttu-id="6bbac-105">Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6bbac-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="6bbac-106">Установите последнюю версию интерфейса командной строки Azure для Windows, Linux или Mac.</span><span class="sxs-lookup"><span data-stu-id="6bbac-106">Install the latest version of the Azure CLI, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="6bbac-107">Дополнительные сведения см. в статье [Установка Azure CLI](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="6bbac-107">More information is available at [Install the Azure CLI](../articles/cli-install-nodejs.md).</span></span>

### <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="6bbac-108">Вход в учетную запись Azure</span><span class="sxs-lookup"><span data-stu-id="6bbac-108">Sign in to your Azure account</span></span>

<span data-ttu-id="6bbac-109">Откройте окно консоли и пройдите проверку подлинности с помощью своих учетных данных.</span><span class="sxs-lookup"><span data-stu-id="6bbac-109">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="6bbac-110">Дополнительную информацию см. в статье о [входе в Azure из командной строки Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="6bbac-110">For more information, see [Log in to Azure from the Azure CLI](../articles/xplat-cli-connect.md)</span></span>

```azurecli
azure login
```

### <a name="switch-cli-mode"></a><span data-ttu-id="6bbac-111">Переключение режима интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="6bbac-111">Switch CLI mode</span></span>

<span data-ttu-id="6bbac-112">Azure DNS использует диспетчер ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="6bbac-112">Azure DNS uses Azure Resource Manager.</span></span> <span data-ttu-id="6bbac-113">Обязательно переключите интерфейс командной строки (CLI) в режим использования команд Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6bbac-113">Make sure you switch CLI mode to use Azure Resource Manager commands.</span></span>

```azurecli
azure config mode arm
```

### <a name="select-the-subscription"></a><span data-ttu-id="6bbac-114">Выбор подписки</span><span class="sxs-lookup"><span data-stu-id="6bbac-114">Select the subscription</span></span>

<span data-ttu-id="6bbac-115">Просмотрите подписки учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6bbac-115">Check the subscriptions for the account.</span></span>

```azurecli
azure account list
```

<span data-ttu-id="6bbac-116">Выберите подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="6bbac-116">Choose which of your Azure subscriptions to use.</span></span>

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="6bbac-117">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="6bbac-117">Create a resource group</span></span>

<span data-ttu-id="6bbac-118">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="6bbac-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="6bbac-119">Оно используется в качестве расположения по умолчанию для всех ресурсов данной группы.</span><span class="sxs-lookup"><span data-stu-id="6bbac-119">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="6bbac-120">Но так как все ресурсы DNS глобальные, а не региональные, выбор расположения группы ресурсов не влияет на Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6bbac-120">However, because all DNS resources are global, not regional, the choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="6bbac-121">Если используется существующая группа ресурсов, можно пропустить этот шаг.</span><span class="sxs-lookup"><span data-stu-id="6bbac-121">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="6bbac-122">Регистрация поставщика ресурсов</span><span class="sxs-lookup"><span data-stu-id="6bbac-122">Register resource provider</span></span>

<span data-ttu-id="6bbac-123">Служба Azure DNS управляется поставщиком ресурсов Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="6bbac-123">The Azure DNS service is managed by the Microsoft.Network resource provider.</span></span> <span data-ttu-id="6bbac-124">Вашу подписку Azure необходимо зарегистрировать, чтобы использовать этот поставщик ресурсов, прежде чем работать с Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6bbac-124">Your Azure subscription must be registered to use this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="6bbac-125">Эта операция выполняется один раз для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="6bbac-125">This is a one-time operation for each subscription.</span></span>

```azurecli
azure provider register --namespace Microsoft.Network
```

