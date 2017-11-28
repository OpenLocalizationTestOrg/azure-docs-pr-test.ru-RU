
1. <span data-ttu-id="b76cd-101">Нажмите кнопку **службы приложений** кнопку выберите вашей серверной части мобильных приложений, выберите **краткое руководство**и затем выберите клиентскую платформу (iOS, Android, Xamarin, Cordova).</span><span class="sxs-lookup"><span data-stu-id="b76cd-101">Click the **App Services** button, select your Mobile Apps back end, select **Quickstart**, and then select your client platform (iOS, Android, Xamarin, Cordova).</span></span>

    ![Портал Azure с примеры использования мобильных приложений выделен][quickstart]

2. <span data-ttu-id="b76cd-103">Если не настроено подключение к базе данных, создайте следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b76cd-103">If a database connection is not configured, create one by doing the following:</span></span>

    ![Портал Azure с помощью мобильного приложения подключения к базе данных][connect]

    <span data-ttu-id="b76cd-105">а.</span><span class="sxs-lookup"><span data-stu-id="b76cd-105">a.</span></span> <span data-ttu-id="b76cd-106">Создание новой базы данных SQL и сервера.</span><span class="sxs-lookup"><span data-stu-id="b76cd-106">Create a new SQL database and server.</span></span>

    ![Портал Azure с мобильным приложениям Создание новой базы данных и сервера][server]

    <span data-ttu-id="b76cd-108">b.</span><span class="sxs-lookup"><span data-stu-id="b76cd-108">b.</span></span> <span data-ttu-id="b76cd-109">Подождите, пока подключение к данным не будет успешно создано.</span><span class="sxs-lookup"><span data-stu-id="b76cd-109">Wait until the data connection is successfully created.</span></span>

    ![Azure портала уведомление об успешном создании подключение к данным][notification]

    <span data-ttu-id="b76cd-111">c.</span><span class="sxs-lookup"><span data-stu-id="b76cd-111">c.</span></span> <span data-ttu-id="b76cd-112">Подключение к данным должно быть успешными.</span><span class="sxs-lookup"><span data-stu-id="b76cd-112">Data connection must be successful.</span></span>

    ![Уведомления на портале Azure, «уже есть подключение к данным»][already-connection]

3. <span data-ttu-id="b76cd-114">В разделе **2. Создание API таблицы** выберите **язык серверной части** — Node.js.</span><span class="sxs-lookup"><span data-stu-id="b76cd-114">Under **2. Create a table API**, select Node.js for **Backend language**.</span></span> 
 
4. <span data-ttu-id="b76cd-115">Примите подтверждение, а затем выберите **таблицы TodoItem создания**.</span><span class="sxs-lookup"><span data-stu-id="b76cd-115">Accept the acknowledgment, and then select **Create TodoItem table**.</span></span>  
    <span data-ttu-id="b76cd-116">Это действие создает новую таблицу элемент задачи в базе данных.</span><span class="sxs-lookup"><span data-stu-id="b76cd-116">This action creates a new to-do item table in your database.</span></span> 

    >[!IMPORTANT]
    > <span data-ttu-id="b76cd-117">Переключение существующей серверной части для Node.js перезаписывает все содержимое.</span><span class="sxs-lookup"><span data-stu-id="b76cd-117">Switching an existing back end to Node.js overwrites all contents.</span></span> <span data-ttu-id="b76cd-118">Вместо этого создать серверной части .NET в разделе [работы с сервером серверной части .NET SDK для мобильных приложений][instructions].</span><span class="sxs-lookup"><span data-stu-id="b76cd-118">To create a .NET back end instead, see [Work with the .NET back-end server SDK for Mobile Apps][instructions].</span></span>

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
