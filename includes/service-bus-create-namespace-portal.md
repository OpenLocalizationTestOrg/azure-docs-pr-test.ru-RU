<span data-ttu-id="6a4ab-101">с помощью Service Bus toobegin очереди в Azure, необходимо сначала создать пространство имен с именем, которое является уникальным в Azure.</span><span class="sxs-lookup"><span data-stu-id="6a4ab-101">toobegin using Service Bus queues in Azure, you must first create a namespace with a name that is unique across Azure.</span></span> <span data-ttu-id="6a4ab-102">Пространство имен предоставляет контейнер для адресации ресурсов служебной шины в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="6a4ab-102">A namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="6a4ab-103">toocreate пространство имен:</span><span class="sxs-lookup"><span data-stu-id="6a4ab-103">toocreate a namespace:</span></span>

1. <span data-ttu-id="6a4ab-104">Войдите на toohello [портал Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="6a4ab-104">Log on toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="6a4ab-105">В области навигации слева hello hello портала щелкните **New**, нажмите кнопку **интеграции Enterprise**и нажмите кнопку **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="6a4ab-105">In hello left navigation pane of hello portal, click **New**, then click **Enterprise Integration**, and then click **Service Bus**.</span></span>
3. <span data-ttu-id="6a4ab-106">В hello **создать пространство имен** диалоговое окно, введите имя пространства имен.</span><span class="sxs-lookup"><span data-stu-id="6a4ab-106">In hello **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="6a4ab-107">система Hello немедленно проверяет toosee, доступно ли имя hello.</span><span class="sxs-lookup"><span data-stu-id="6a4ab-107">hello system immediately checks toosee if hello name is available.</span></span>
4. <span data-ttu-id="6a4ab-108">После внесения убедиться, что имя пространства имен hello недоступна, выберите hello ценовой категории (Basic, Standard или Premium).</span><span class="sxs-lookup"><span data-stu-id="6a4ab-108">After making sure hello namespace name is available, choose hello pricing tier (Basic, Standard, or Premium).</span></span>
5. <span data-ttu-id="6a4ab-109">В hello **подписки** выберите подписку Azure в какие toocreate hello пространств имен.</span><span class="sxs-lookup"><span data-stu-id="6a4ab-109">In hello **Subscription** field, choose an Azure subscription in which toocreate hello namespace.</span></span>
6. <span data-ttu-id="6a4ab-110">В hello **группы ресурсов** выберите существующую группу ресурсов в какой hello пространство имен будет live или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="6a4ab-110">In hello **Resource group** field, choose an existing resource group in which hello namespace will live, or create a new one.</span></span>      
7. <span data-ttu-id="6a4ab-111">В **расположение**, выберите hello страну или регион, в котором должна размещаться пространства имен.</span><span class="sxs-lookup"><span data-stu-id="6a4ab-111">In **Location**, choose hello country or region in which your namespace should be hosted.</span></span>
   
    ![Создание пространства имен][create-namespace]
8. <span data-ttu-id="6a4ab-113">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="6a4ab-113">Click **Create**.</span></span> <span data-ttu-id="6a4ab-114">система Hello теперь создает пространство имен и включает его.</span><span class="sxs-lookup"><span data-stu-id="6a4ab-114">hello system now creates your namespace and enables it.</span></span> <span data-ttu-id="6a4ab-115">Может потребоваться toowait несколько минут, как hello система выделяет ресурсы для вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6a4ab-115">You might have toowait several minutes as hello system provisions resources for your account.</span></span>

### <a name="obtain-hello-management-credentials"></a><span data-ttu-id="6a4ab-116">Получить учетные данные управления hello</span><span class="sxs-lookup"><span data-stu-id="6a4ab-116">Obtain hello management credentials</span></span>

1. <span data-ttu-id="6a4ab-117">В списке hello пространств имен выберите hello созданное имя пространства имен.</span><span class="sxs-lookup"><span data-stu-id="6a4ab-117">In hello list of namespaces, click hello newly created namespace name.</span></span>
2. <span data-ttu-id="6a4ab-118">В колонке приветствия имен щелкните **политики общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="6a4ab-118">In hello namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="6a4ab-119">В hello **политики общего доступа** колонка, щелкните **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="6a4ab-119">In hello **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![Сведения о подключении][connection-info]
4. <span data-ttu-id="6a4ab-121">В hello **политики: RootManageSharedAccessKey** колонке нажмите кнопку "Копировать" hello Далее слишком**строка — первичный ключ подключения**, toocopy подключения hello строка буфера обмена tooyour для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="6a4ab-121">In hello **Policy: RootManageSharedAccessKey** blade, click hello copy button next too**Connection string–primary key**, toocopy hello connection string tooyour clipboard for later use.</span></span> <span data-ttu-id="6a4ab-122">Вставьте на время эти значения в Блокноте или любом другом месте.</span><span class="sxs-lookup"><span data-stu-id="6a4ab-122">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![Строка подключения][connection-string]

5. <span data-ttu-id="6a4ab-124">Повторите hello предыдущего шага, скопировав и вставив значение hello **первичного ключа** tooa временное расположение для дальнейшего использования.</span><span class="sxs-lookup"><span data-stu-id="6a4ab-124">Repeat hello previous step, copying and pasting hello value of **Primary key** tooa temporary location for later use.</span></span>

<!--Image references-->

[create-namespace]: ./media/service-bus-create-namespace-portal/create-namespace.png
[connection-info]: ./media/service-bus-create-namespace-portal/connection-info.png
[connection-string]: ./media/service-bus-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
