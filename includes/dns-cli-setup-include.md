## <a name="set-up-azure-cli-for-azure-dns"></a><span data-ttu-id="a2a92-101">Настройка интерфейса командной строки Azure для Azure DNS</span><span class="sxs-lookup"><span data-stu-id="a2a92-101">Set up Azure CLI for Azure DNS</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="a2a92-102">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="a2a92-102">Before you begin</span></span>

<span data-ttu-id="a2a92-103">Проверьте наличие следующих элементов перед началом настройки hello.</span><span class="sxs-lookup"><span data-stu-id="a2a92-103">Verify that you have hello following items before beginning your configuration.</span></span>

* <span data-ttu-id="a2a92-104">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="a2a92-104">An Azure subscription.</span></span> <span data-ttu-id="a2a92-105">Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2a92-105">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a2a92-106">Установите последнюю версию hello hello Azure CLI, доступные для Windows, Linux или MAC.</span><span class="sxs-lookup"><span data-stu-id="a2a92-106">Install hello latest version of hello Azure CLI, available for Windows, Linux, or MAC.</span></span> <span data-ttu-id="a2a92-107">Дополнительные сведения можно найти по адресу [Install hello Azure CLI](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a2a92-107">More information is available at [Install hello Azure CLI](../articles/cli-install-nodejs.md).</span></span>

### <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="a2a92-108">Войдите в tooyour учетная запись Azure</span><span class="sxs-lookup"><span data-stu-id="a2a92-108">Sign in tooyour Azure account</span></span>

<span data-ttu-id="a2a92-109">Откройте окно консоли и пройдите проверку подлинности с помощью своих учетных данных.</span><span class="sxs-lookup"><span data-stu-id="a2a92-109">Open a console window and authenticate with your credentials.</span></span> <span data-ttu-id="a2a92-110">Дополнительные сведения см. в разделе [входа tooAzure из hello Azure CLI](../articles/xplat-cli-connect.md)</span><span class="sxs-lookup"><span data-stu-id="a2a92-110">For more information, see [Log in tooAzure from hello Azure CLI](../articles/xplat-cli-connect.md)</span></span>

```azurecli
azure login
```

### <a name="switch-cli-mode"></a><span data-ttu-id="a2a92-111">Переключение режима интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="a2a92-111">Switch CLI mode</span></span>

<span data-ttu-id="a2a92-112">Azure DNS использует диспетчер ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="a2a92-112">Azure DNS uses Azure Resource Manager.</span></span> <span data-ttu-id="a2a92-113">Убедитесь, что переключение команд диспетчера ресурсов Azure toouse режиме CLI.</span><span class="sxs-lookup"><span data-stu-id="a2a92-113">Make sure you switch CLI mode toouse Azure Resource Manager commands.</span></span>

```azurecli
azure config mode arm
```

### <a name="select-hello-subscription"></a><span data-ttu-id="a2a92-114">Выберите подписку hello</span><span class="sxs-lookup"><span data-stu-id="a2a92-114">Select hello subscription</span></span>

<span data-ttu-id="a2a92-115">Проверьте hello подписки для учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="a2a92-115">Check hello subscriptions for hello account.</span></span>

```azurecli
azure account list
```

<span data-ttu-id="a2a92-116">Выберите, какие toouse вашей подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="a2a92-116">Choose which of your Azure subscriptions toouse.</span></span>

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a><span data-ttu-id="a2a92-117">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="a2a92-117">Create a resource group</span></span>

<span data-ttu-id="a2a92-118">В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение.</span><span class="sxs-lookup"><span data-stu-id="a2a92-118">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="a2a92-119">Используется как расположение по умолчанию hello для ресурсов в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a2a92-119">This is used as hello default location for resources in that resource group.</span></span> <span data-ttu-id="a2a92-120">Тем не менее так как все ресурсы DNS глобального, не язык, выбор hello расположение группы ресурсов не оказывает влияния на Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="a2a92-120">However, because all DNS resources are global, not regional, hello choice of resource group location has no impact on Azure DNS.</span></span>

<span data-ttu-id="a2a92-121">Если используется существующая группа ресурсов, можно пропустить этот шаг.</span><span class="sxs-lookup"><span data-stu-id="a2a92-121">You can skip this step if you are using an existing resource group.</span></span>

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a><span data-ttu-id="a2a92-122">Регистрация поставщика ресурсов</span><span class="sxs-lookup"><span data-stu-id="a2a92-122">Register resource provider</span></span>

<span data-ttu-id="a2a92-123">Служба Azure DNS Hello управляется поставщика ресурсов Microsoft.Network hello.</span><span class="sxs-lookup"><span data-stu-id="a2a92-123">hello Azure DNS service is managed by hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="a2a92-124">Ваша подписка Azure должен быть зарегистрированных toouse этого поставщика ресурсов, прежде чем можно будет использовать Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="a2a92-124">Your Azure subscription must be registered toouse this resource provider before you can use Azure DNS.</span></span> <span data-ttu-id="a2a92-125">Эта операция выполняется один раз для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="a2a92-125">This is a one-time operation for each subscription.</span></span>

```azurecli
azure provider register --namespace Microsoft.Network
```

