1. <span data-ttu-id="00910-101">Войдите на [портал Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="00910-101">Log on to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="00910-102">На портале в области навигации слева щелкните последовательно **Создать**, **Интеграция Enterprise**, **Ретранслятор**.</span><span class="sxs-lookup"><span data-stu-id="00910-102">In the left navigation pane of the portal, click **New**, then click **Enterprise Integration**, and then click **Relay**.</span></span>
3. <span data-ttu-id="00910-103">В диалоговом окне **Создание пространства имен** укажите имя пространства имен.</span><span class="sxs-lookup"><span data-stu-id="00910-103">In the **Create namespace** dialog, enter a namespace name.</span></span> <span data-ttu-id="00910-104">Система немедленно проверит, доступно ли это имя.</span><span class="sxs-lookup"><span data-stu-id="00910-104">The system immediately checks to see if the name is available.</span></span>
4. <span data-ttu-id="00910-105">Выберите **подписку** Azure, в рамках которой будет создано пространство имен.</span><span class="sxs-lookup"><span data-stu-id="00910-105">In the **Subscription** field, choose an Azure subscription in which to create the namespace.</span></span>
5. <span data-ttu-id="00910-106">В соответствующем поле выберите существующую **[группу ресурсов](../articles/azure-resource-manager/resource-group-portal.md)**, в которую будет включено это пространство имен, или создайте новую.</span><span class="sxs-lookup"><span data-stu-id="00910-106">In the **[Resource group](../articles/azure-resource-manager/resource-group-portal.md)** field, choose an existing resource group in which the namespace will live, or create a new one.</span></span>      
6. <span data-ttu-id="00910-107">Укажите **расположение**— страну или регион для размещения пространства имен.</span><span class="sxs-lookup"><span data-stu-id="00910-107">In **Location**, choose the country or region in which your namespace should be hosted.</span></span>
   
    ![Создание пространства имен][create-namespace]
7. <span data-ttu-id="00910-109">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="00910-109">Click **Create**.</span></span> <span data-ttu-id="00910-110">Теперь система создает пространство имен и включает его.</span><span class="sxs-lookup"><span data-stu-id="00910-110">The system now creates your namespace and enables it.</span></span> <span data-ttu-id="00910-111">Через несколько минут система подготовит к работе ресурсы для вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="00910-111">After a few minutes, the system provisions resources for your account.</span></span>

### <a name="obtain-the-management-credentials"></a><span data-ttu-id="00910-112">Получение учетных данных управления</span><span class="sxs-lookup"><span data-stu-id="00910-112">Obtain the management credentials</span></span>
1. <span data-ttu-id="00910-113">В списке пространств имен щелкните имя только что созданного пространства имен.</span><span class="sxs-lookup"><span data-stu-id="00910-113">In the list of namespaces, click the newly created namespace name.</span></span>
2. <span data-ttu-id="00910-114">В колонке пространства имен щелкните **Политики общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="00910-114">In the namespace blade, click **Shared access policies**.</span></span>
3. <span data-ttu-id="00910-115">В колонке **Политики общего доступа** щелкните **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="00910-115">In the **Shared access policies** blade, click **RootManageSharedAccessKey**.</span></span>
   
    ![Сведения о подключении][connection-info]
4. <span data-ttu-id="00910-117">В колонке **Политика: RootManageSharedAccessKey** нажмите кнопку копирования рядом с полем **Строка подключения — первичный ключ**, чтобы скопировать строку подключения в буфер обмена для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="00910-117">In the **Policy: RootManageSharedAccessKey** blade, click the copy button next to **Connection string–primary key**, to copy the connection string to your clipboard for later use.</span></span> <span data-ttu-id="00910-118">Вставьте на время эти значения в Блокноте или любом другом месте.</span><span class="sxs-lookup"><span data-stu-id="00910-118">Paste this value into Notepad or some other temporary location.</span></span>
   
    ![Строка подключения][connection-string]

5. <span data-ttu-id="00910-120">Повторите предыдущий шаг, скопировав и вставив значение **первичного ключа** во временное расположение для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="00910-120">Repeat the previous step, copying and pasting the value of **Primary key** to a temporary location for later use.</span></span>  

<!--Image references-->

[create-namespace]: ./media/relay-create-namespace-portal/create-namespace.png
[connection-info]: ./media/relay-create-namespace-portal/connection-info.png
[connection-string]: ./media/relay-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
