## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a><span data-ttu-id="87fd5-101">Подготовка tooauthenticate запросов диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="87fd5-101">Prepare tooauthenticate Azure Resource Manager requests</span></span>
<span data-ttu-id="87fd5-102">Вы должны пройти проверку подлинности всех hello операций, выполняемых с ресурсами с помощью hello [диспетчера ресурсов Azure] [ lnk-authenticate-arm] с Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="87fd5-102">You must authenticate all hello operations that you perform on resources using hello [Azure Resource Manager][lnk-authenticate-arm] with Azure Active Directory (AD).</span></span> <span data-ttu-id="87fd5-103">Здравствуйте, наиболее простым способом tooconfigure toouse PowerShell или Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="87fd5-103">hello easiest way tooconfigure this is toouse PowerShell or Azure CLI.</span></span>

<span data-ttu-id="87fd5-104">Установка hello [командлетов Azure PowerShell] [ lnk-powershell-install] перед продолжением.</span><span class="sxs-lookup"><span data-stu-id="87fd5-104">Install hello [Azure PowerShell cmdlets][lnk-powershell-install] before you continue.</span></span>

<span data-ttu-id="87fd5-105">Здравствуйте, следующие шаги Показать как tooset проверку подлинности пароль для приложения AD с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="87fd5-105">hello following steps show how tooset up password authentication for an AD application using PowerShell.</span></span> <span data-ttu-id="87fd5-106">Эти команды можно выполнять в обычном сеансе PowerShell.</span><span class="sxs-lookup"><span data-stu-id="87fd5-106">You can run these commands in a standard PowerShell session.</span></span>

1. <span data-ttu-id="87fd5-107">Вход tooyour подписку Azure с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="87fd5-107">Log in tooyour Azure subscription using hello following command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="87fd5-108">Если у вас несколько подписок Azure, предоставляет доступ tooall вход tooAzure hello подписок Azure, связанных с учетными данными.</span><span class="sxs-lookup"><span data-stu-id="87fd5-108">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="87fd5-109">Используйте следующую команду, toolist hello подписки Azure доступны для вас toouse hello.</span><span class="sxs-lookup"><span data-stu-id="87fd5-109">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="87fd5-110">Используется следующая команда tooselect подписки требуется toouse toorun hello команды toomanage концентратор IoT hello.</span><span class="sxs-lookup"><span data-stu-id="87fd5-110">Use hello following command tooselect subscription that you want toouse toorun hello commands toomanage your IoT hub.</span></span> <span data-ttu-id="87fd5-111">Можно использовать имя подписки hello или идентификатор из hello выходные данные предыдущей команды hello:</span><span class="sxs-lookup"><span data-stu-id="87fd5-111">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. <span data-ttu-id="87fd5-112">Обратите внимание на **TenantId** и **SubscriptionId**.</span><span class="sxs-lookup"><span data-stu-id="87fd5-112">Make a note of your **TenantId** and **SubscriptionId**.</span></span> <span data-ttu-id="87fd5-113">Они потребуются вам позднее.</span><span class="sxs-lookup"><span data-stu-id="87fd5-113">You need them later.</span></span>
3. <span data-ttu-id="87fd5-114">Создайте новое приложение Azure Active Directory с помощью hello следующую команду, заменив заполнителями hello:</span><span class="sxs-lookup"><span data-stu-id="87fd5-114">Create a new Azure Active Directory application using hello following command, replacing hello place holders:</span></span>
   
   * <span data-ttu-id="87fd5-115">**{Display name}:** отображаемое имя вашего приложения, например **MySampleApp**.</span><span class="sxs-lookup"><span data-stu-id="87fd5-115">**{Display name}:** a display name for your application such as **MySampleApp**</span></span>
   * <span data-ttu-id="87fd5-116">**{URL-адрес домашней страницы}:** hello URL-адрес домашней страницы приложения hello, таких как **http://mysampleapp/home**.</span><span class="sxs-lookup"><span data-stu-id="87fd5-116">**{Home page URL}:** hello URL of hello home page of your app such as **http://mysampleapp/home**.</span></span> <span data-ttu-id="87fd5-117">Этот URL-адрес не обязательно toopoint tooa реальному приложению.</span><span class="sxs-lookup"><span data-stu-id="87fd5-117">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="87fd5-118">**{Application identifier}:** уникальный идентификатор, например **http://mysampleapp**.</span><span class="sxs-lookup"><span data-stu-id="87fd5-118">**{Application identifier}:** A unique identifier such as **http://mysampleapp**.</span></span> <span data-ttu-id="87fd5-119">Этот URL-адрес не обязательно toopoint tooa реальному приложению.</span><span class="sxs-lookup"><span data-stu-id="87fd5-119">This URL does not need toopoint tooa real application.</span></span>
   * <span data-ttu-id="87fd5-120">**{Password}:** пароль, использовать tooauthenticate вместе с приложением.</span><span class="sxs-lookup"><span data-stu-id="87fd5-120">**{Password}:** A password that you use tooauthenticate with your app.</span></span>
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. <span data-ttu-id="87fd5-121">Запишите hello **ApplicationId** приложения hello, вы создали.</span><span class="sxs-lookup"><span data-stu-id="87fd5-121">Make a note of hello **ApplicationId** of hello application you created.</span></span> <span data-ttu-id="87fd5-122">Этот идентификатор потребуется позднее.</span><span class="sxs-lookup"><span data-stu-id="87fd5-122">You need this later.</span></span>
5. <span data-ttu-id="87fd5-123">Создание нового субъекта-службы с помощью hello следующую команду, заменив **{MyApplicationId}** с hello **ApplicationId** из предыдущего шага hello:</span><span class="sxs-lookup"><span data-stu-id="87fd5-123">Create a new service principal using hello following command, replacing **{MyApplicationId}** with hello **ApplicationId** from hello previous step:</span></span>
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. <span data-ttu-id="87fd5-124">Настройка назначения роли с помощью hello следующую команду, заменив **{MyApplicationId}** с вашей **ApplicationId**.</span><span class="sxs-lookup"><span data-stu-id="87fd5-124">Set up a role assignment using hello following command, replacing **{MyApplicationId}** with your **ApplicationId**.</span></span>
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

<span data-ttu-id="87fd5-125">Создание приложения hello Azure AD, позволяющая tooauthenticate из вашего приложения C# завершена.</span><span class="sxs-lookup"><span data-stu-id="87fd5-125">You have now finished creating hello Azure AD application that enables you tooauthenticate from your custom C# application.</span></span> <span data-ttu-id="87fd5-126">Необходимы следующие значения в этом руководстве позднее hello.</span><span class="sxs-lookup"><span data-stu-id="87fd5-126">You need hello following values later in this tutorial:</span></span>

* <span data-ttu-id="87fd5-127">TenantId</span><span class="sxs-lookup"><span data-stu-id="87fd5-127">TenantId</span></span>
* <span data-ttu-id="87fd5-128">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="87fd5-128">SubscriptionId</span></span>
* <span data-ttu-id="87fd5-129">ApplicationId</span><span class="sxs-lookup"><span data-stu-id="87fd5-129">ApplicationId</span></span>
* <span data-ttu-id="87fd5-130">Пароль</span><span class="sxs-lookup"><span data-stu-id="87fd5-130">Password</span></span>

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
