1. <span data-ttu-id="dd8bf-101">Войдите на toohello [портал Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="dd8bf-101">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="dd8bf-102">В области навигации слева hello hello портала щелкните **New**, нажмите кнопку **интеграцию**и нажмите кнопку **ретрансляции**.</span><span class="sxs-lookup"><span data-stu-id="dd8bf-102">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Relay**.</span></span>
3. <span data-ttu-id="dd8bf-103">В hello **создать пространство имен** диалоговое окно, введите имя пространства имен.</span><span class="sxs-lookup"><span data-stu-id="dd8bf-103">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="dd8bf-104">система Hello немедленно проверяет toosee, доступно ли имя hello.</span><span class="sxs-lookup"><span data-stu-id="dd8bf-104">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="dd8bf-105">В hello **подписки** выберите подписку Azure в какие toocreate hello пространств имен.</span><span class="sxs-lookup"><span data-stu-id="dd8bf-105">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
5. <span data-ttu-id="dd8bf-106">В hello  **[группы ресурсов](../articles/azure-resource-manager/resource-group-portal.md)**  выберите существующую группу ресурсов в какой hello пространство имен будет live или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="dd8bf-106">In hello **[Resource group](../articles/azure-resource-manager/resource-group-portal.md)** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
6. <span data-ttu-id="dd8bf-107">В **расположение**, выберите hello страну или регион, в котором должна размещаться пространства имен.</span><span class="sxs-lookup"><span data-stu-id="dd8bf-107">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![Создание пространства имен][create-namespace]
7. <span data-ttu-id="dd8bf-109">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dd8bf-109">Click **Create**.</span></span> <span data-ttu-id="dd8bf-110">система Hello теперь создает пространство имен и включает его.</span><span class="sxs-lookup"><span data-stu-id="dd8bf-110">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="dd8bf-111">Через несколько минут hello система выделяет ресурсы для вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="dd8bf-111">After a few minutes, hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-management-credentials"></a><span data-ttu-id="dd8bf-112">Получить учетные данные управления hello</span><span class="sxs-lookup"><span data-stu-id="dd8bf-112">Obtain hello management credentials</span></span>
1. <span data-ttu-id="dd8bf-113">В списке hello пространств имен выберите hello созданное имя пространства имен.</span><span class="sxs-lookup"><span data-stu-id="dd8bf-113">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="dd8bf-114">В колонке приветствия имен щелкните **политики общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="dd8bf-114">In hello namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="dd8bf-115">В hello **политики общего доступа** колонка, щелкните **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="dd8bf-115">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![Сведения о подключении][connection-info]
4. <span data-ttu-id="dd8bf-117">В hello **политики: RootManageSharedAccessKey** колонке нажмите кнопку "Копировать" hello Далее слишком**строка — первичный ключ подключения**, toocopy подключения hello строка буфера обмена tooyour для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="dd8bf-117">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span> <span data-ttu-id="dd8bf-118">Вставьте на время эти значения в Блокноте или любом другом месте.</span><span class="sxs-lookup"><span data-stu-id="dd8bf-118">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![Строка подключения][connection-string]

5. <span data-ttu-id="dd8bf-120">Повторите hello предыдущего шага, скопировав и вставив значение hello **первичного ключа** tooa временное расположение для дальнейшего использования.</span><span class="sxs-lookup"><span data-stu-id="dd8bf-120">Repeat hello previous step, copying and pasting hello value of **Primary key** tooa temporary location for later use.</span></span>  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
