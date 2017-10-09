
1. <span data-ttu-id="b0879-101">Нажмите кнопку hello **службы приложений** кнопку выберите вашей серверной части мобильных приложений, выберите **краткое руководство**и затем выберите клиентскую платформу (iOS, Android, Xamarin, Cordova).</span><span class="sxs-lookup"><span data-stu-id="b0879-101">Click hello **App Services** button, select your Mobile Apps back end, select **Quickstart**, and then select your client platform (iOS, Android, Xamarin, Cordova).</span></span>

    ![Портал Azure с выделенным пунктом "Mobile Apps Quickstart" (Быстрый запуск мобильных приложений)][quickstart]

2. <span data-ttu-id="b0879-103">Если подключение к базе данных не настроена, создайте, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="b0879-103">If a database connection is not configured, create one by doing hello following:</span></span>

    ![Портал Azure с toodatabase подключения мобильных приложений][connect]

    <span data-ttu-id="b0879-105">а.</span><span class="sxs-lookup"><span data-stu-id="b0879-105">a.</span></span> <span data-ttu-id="b0879-106">Создайте сервер и базу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="b0879-106">Create a new SQL database and server.</span></span>

    ![Создание базы данных и сервера для мобильных приложений на портале Azure][server]

    <span data-ttu-id="b0879-108">b.</span><span class="sxs-lookup"><span data-stu-id="b0879-108">b.</span></span> <span data-ttu-id="b0879-109">Подождите, пока подключение к данным hello успешно создан.</span><span class="sxs-lookup"><span data-stu-id="b0879-109">Wait until hello data connection is successfully created.</span></span>

    ![Уведомление портала Azure об успешном создании подключения к данным][notification]

    <span data-ttu-id="b0879-111">c.</span><span class="sxs-lookup"><span data-stu-id="b0879-111">c.</span></span> <span data-ttu-id="b0879-112">Подключение к данным должно быть успешными.</span><span class="sxs-lookup"><span data-stu-id="b0879-112">Data connection must be successful.</span></span>

    ![Уведомление на портале Azure: "Уже имеется подключение к данным"][already-connection]

3. <span data-ttu-id="b0879-114">В разделе **2. Создание API таблицы** выберите **язык серверной части** — Node.js.</span><span class="sxs-lookup"><span data-stu-id="b0879-114">Under **2. Create a table API**, select Node.js for **Backend language**.</span></span> 
 
4. <span data-ttu-id="b0879-115">Примите hello подтверждения, а затем выберите **таблицы TodoItem создания**.</span><span class="sxs-lookup"><span data-stu-id="b0879-115">Accept hello acknowledgment, and then select **Create TodoItem table**.</span></span>  
    <span data-ttu-id="b0879-116">В базе данных будет создана таблица с элементами списка дел.</span><span class="sxs-lookup"><span data-stu-id="b0879-116">This action creates a new to-do item table in your database.</span></span> 

    >[!IMPORTANT]
    > <span data-ttu-id="b0879-117">Переключение существующей серверной части tooNode.js перезаписывает все содержимое.</span><span class="sxs-lookup"><span data-stu-id="b0879-117">Switching an existing back end tooNode.js overwrites all contents.</span></span> <span data-ttu-id="b0879-118">серверной части .NET см. Вместо этого toocreate [работать с сервером hello серверной части .NET SDK для мобильных приложений][instructions].</span><span class="sxs-lookup"><span data-stu-id="b0879-118">toocreate a .NET back end instead, see [Work with hello .NET back-end server SDK for Mobile Apps][instructions].</span></span>

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
