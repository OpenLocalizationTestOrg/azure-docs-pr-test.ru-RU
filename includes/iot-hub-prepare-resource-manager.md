## <a name="prepare-to-authenticate-azure-resource-manager-requests"></a><span data-ttu-id="3ff53-101">Подготовка к проверке подлинности запросов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3ff53-101">Prepare to authenticate Azure Resource Manager requests</span></span>
<span data-ttu-id="3ff53-102">Необходимо выполнять проверку подлинности всех операций, выполняемых с ресурсами с помощью [Azure Resource Manager][lnk-authenticate-arm], используя Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3ff53-102">You must authenticate all the operations that you perform on resources using the [Azure Resource Manager][lnk-authenticate-arm] with Azure Active Directory (AD).</span></span> <span data-ttu-id="3ff53-103">Для такой настройки проще всего использовать PowerShell или интерфейс командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="3ff53-103">The easiest way to configure this is to use PowerShell or Azure CLI.</span></span>

<span data-ttu-id="3ff53-104">Прежде чем продолжать, установите [командлеты Azure PowerShell][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="3ff53-104">Install the [Azure PowerShell cmdlets][lnk-powershell-install] before you continue.</span></span>

<span data-ttu-id="3ff53-105">Ниже показано, как настроить проверку пароля для приложения AD с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ff53-105">The following steps show how to set up password authentication for an AD application using PowerShell.</span></span> <span data-ttu-id="3ff53-106">Эти команды можно выполнять в обычном сеансе PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ff53-106">You can run these commands in a standard PowerShell session.</span></span>

1. <span data-ttu-id="3ff53-107">Выполните следующую команду для входа в подписку Azure:</span><span class="sxs-lookup"><span data-stu-id="3ff53-107">Log in to your Azure subscription using the following command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="3ff53-108">Если у вас есть несколько подписок Azure, то при входе в Azure вы получите доступ ко всем подпискам Azure, связанным с вашими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="3ff53-108">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="3ff53-109">Используйте следующую команду, чтобы просмотреть подписки Azure, доступные для использования:</span><span class="sxs-lookup"><span data-stu-id="3ff53-109">Use the following command to list the Azure subscriptions available for you to use:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="3ff53-110">Используйте следующую команду, чтобы выбрать подписку, с помощью которой будут выполняться команды для управления Центром Интернета вещей.</span><span class="sxs-lookup"><span data-stu-id="3ff53-110">Use the following command to select subscription that you want to use to run the commands to manage your IoT hub.</span></span> <span data-ttu-id="3ff53-111">Вы можете использовать имя подписки или идентификатор из выходных данных предыдущей команды:</span><span class="sxs-lookup"><span data-stu-id="3ff53-111">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. <span data-ttu-id="3ff53-112">Обратите внимание на **TenantId** и **SubscriptionId**.</span><span class="sxs-lookup"><span data-stu-id="3ff53-112">Make a note of your **TenantId** and **SubscriptionId**.</span></span> <span data-ttu-id="3ff53-113">Они потребуются вам позднее.</span><span class="sxs-lookup"><span data-stu-id="3ff53-113">You need them later.</span></span>
3. <span data-ttu-id="3ff53-114">Воспользуйтесь следующей командой для создания нового приложения Azure Active Directory, заменив в ней заполнители:</span><span class="sxs-lookup"><span data-stu-id="3ff53-114">Create a new Azure Active Directory application using the following command, replacing the place holders:</span></span>
   
   * <span data-ttu-id="3ff53-115">**{Display name}:** отображаемое имя вашего приложения, например **MySampleApp**.</span><span class="sxs-lookup"><span data-stu-id="3ff53-115">**{Display name}:** a display name for your application such as **MySampleApp**</span></span>
   * <span data-ttu-id="3ff53-116">**{Home page URL}:** URL-адрес домашней страницы вашего приложения, например **http://mysampleapp/home**.</span><span class="sxs-lookup"><span data-stu-id="3ff53-116">**{Home page URL}:** the URL of the home page of your app such as **http://mysampleapp/home**.</span></span> <span data-ttu-id="3ff53-117">Этот URL-адрес необязательно должен указывать на реальное приложение.</span><span class="sxs-lookup"><span data-stu-id="3ff53-117">This URL does not need to point to a real application.</span></span>
   * <span data-ttu-id="3ff53-118">**{Application identifier}:** уникальный идентификатор, например **http://mysampleapp**.</span><span class="sxs-lookup"><span data-stu-id="3ff53-118">**{Application identifier}:** A unique identifier such as **http://mysampleapp**.</span></span> <span data-ttu-id="3ff53-119">Этот URL-адрес необязательно должен указывать на реальное приложение.</span><span class="sxs-lookup"><span data-stu-id="3ff53-119">This URL does not need to point to a real application.</span></span>
   * <span data-ttu-id="3ff53-120">**{Password}:** пароль, который используется для проверки подлинности в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="3ff53-120">**{Password}:** A password that you use to authenticate with your app.</span></span>
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. <span data-ttu-id="3ff53-121">Запишите значение **ApplicationId** для созданного приложения.</span><span class="sxs-lookup"><span data-stu-id="3ff53-121">Make a note of the **ApplicationId** of the application you created.</span></span> <span data-ttu-id="3ff53-122">Этот идентификатор потребуется позднее.</span><span class="sxs-lookup"><span data-stu-id="3ff53-122">You need this later.</span></span>
5. <span data-ttu-id="3ff53-123">Создайте новую субъект-службу с помощью следующей команды, заменив **{MyApplicationId}** на значением **ApplicationId** из предыдущего шага.</span><span class="sxs-lookup"><span data-stu-id="3ff53-123">Create a new service principal using the following command, replacing **{MyApplicationId}** with the **ApplicationId** from the previous step:</span></span>
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. <span data-ttu-id="3ff53-124">Настройте назначение роли с помощью следующей команды, заменив **{MyApplicationId}** своим значением **ApplicationId**.</span><span class="sxs-lookup"><span data-stu-id="3ff53-124">Set up a role assignment using the following command, replacing **{MyApplicationId}** with your **ApplicationId**.</span></span>
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

<span data-ttu-id="3ff53-125">Вы завершили создание приложения Azure AD, которое позволит вам осуществлять проверку подлинности из своего пользовательского приложения C#.</span><span class="sxs-lookup"><span data-stu-id="3ff53-125">You have now finished creating the Azure AD application that enables you to authenticate from your custom C# application.</span></span> <span data-ttu-id="3ff53-126">Позднее в рамках изучения данного руководства вам потребуются следующие значения:</span><span class="sxs-lookup"><span data-stu-id="3ff53-126">You need the following values later in this tutorial:</span></span>

* <span data-ttu-id="3ff53-127">TenantId</span><span class="sxs-lookup"><span data-stu-id="3ff53-127">TenantId</span></span>
* <span data-ttu-id="3ff53-128">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="3ff53-128">SubscriptionId</span></span>
* <span data-ttu-id="3ff53-129">ApplicationId</span><span class="sxs-lookup"><span data-stu-id="3ff53-129">ApplicationId</span></span>
* <span data-ttu-id="3ff53-130">Пароль</span><span class="sxs-lookup"><span data-stu-id="3ff53-130">Password</span></span>

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
