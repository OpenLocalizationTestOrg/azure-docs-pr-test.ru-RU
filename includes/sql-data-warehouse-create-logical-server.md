### <a name="create-a-new-logical-sql-server-in-the-azure-portal"></a><span data-ttu-id="2cd0b-101">Создание логического сервера SQL Server на портале Azure</span><span class="sxs-lookup"><span data-stu-id="2cd0b-101">Create a new logical SQL server in the Azure portal</span></span>

1. <span data-ttu-id="2cd0b-102">Щелкните **Создать**, выполните поиск по запросу **логический сервер** и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="2cd0b-102">Click **New**, search **logical server**, and then hit **ENTER**.</span></span>

    ![поиск логического сервера](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. <span data-ttu-id="2cd0b-104">Выберите **SQL Server (логический сервер)**.</span><span class="sxs-lookup"><span data-stu-id="2cd0b-104">Select **SQL server (logical server)**</span></span> 

    ![выбор логического сервера](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. <span data-ttu-id="2cd0b-106">Щелкните **Создать**, чтобы открыть колонку создания логического сервера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2cd0b-106">Click **Create** to open the new SQL Server (logical server) blade.</span></span>

   <span data-ttu-id="2cd0b-107"><kbd>![открыть колонку логический сервер](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![колонке логический сервер](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd></span><span class="sxs-lookup"><span data-stu-id="2cd0b-107"><kbd> ![open logical server blade](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd>![logical server blade](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png) </kbd></span></span>
  
3. <span data-ttu-id="2cd0b-108">В поле "Имя сервера" сервера SQL Server (логический сервер) введите допустимое имя для нового логического сервера.</span><span class="sxs-lookup"><span data-stu-id="2cd0b-108">In the SQL Server (logical server) blade's server name text box, provide a valid name for the new logical server.</span></span> <span data-ttu-id="2cd0b-109">Зеленый флажок указывает, что выбрано допустимое имя.</span><span class="sxs-lookup"><span data-stu-id="2cd0b-109">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![Имя нового сервера](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > <span data-ttu-id="2cd0b-111">Полным именем нового сервера будет <имя_вашего_сервера>.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="2cd0b-111">The fully qualified name for your new server will be <your_server_name>.database.windows.net.</span></span>
    >
    
4. <span data-ttu-id="2cd0b-112">В текстовом поле "Имя входа администратора сервера" укажите имя пользователя, которое будет использоваться сервером при проверке подлинности SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2cd0b-112">In the Server admin login text box, provide a user name for the SQL authentication login for this server.</span></span> <span data-ttu-id="2cd0b-113">Это имя называется именем субъекта сервера.</span><span class="sxs-lookup"><span data-stu-id="2cd0b-113">This login is known as the server principal login.</span></span> <span data-ttu-id="2cd0b-114">Зеленый флажок указывает, что выбрано допустимое имя.</span><span class="sxs-lookup"><span data-stu-id="2cd0b-114">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![Учетные данные администратора SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. <span data-ttu-id="2cd0b-116">В полях **Пароль** и **Подтверждение пароля** укажите пароль для входа в учетную запись субъекта сервера.</span><span class="sxs-lookup"><span data-stu-id="2cd0b-116">In the **Password** and **Confirm password** text boxes, provide a password for the server principal login account.</span></span> <span data-ttu-id="2cd0b-117">Зеленый флажок указывает, что выбран допустимый пароль.</span><span class="sxs-lookup"><span data-stu-id="2cd0b-117">A green check mark indicates that you have provided a valid password.</span></span>
    
    ![Пароль администратора SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. <span data-ttu-id="2cd0b-119">Выберите подписку, в которой у вас есть разрешение на создание объектов.</span><span class="sxs-lookup"><span data-stu-id="2cd0b-119">Select a subscription in which you have permission to create objects.</span></span>

    ![Подписка](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. <span data-ttu-id="2cd0b-121">Над полем "Группа ресурсов" установите переключатель **Создать новую**, а затем в текстовом поле введите допустимое имя новой группы ресурсов. Также можно использовать существующую группу, если она уже создана.</span><span class="sxs-lookup"><span data-stu-id="2cd0b-121">In the Resource group text box, select **Create new** and then, in the resource group text box, provide a valid name for the new resource group (you can also use an existing resource group if you have already created one for yourself).</span></span> <span data-ttu-id="2cd0b-122">Зеленый флажок указывает, что выбрано допустимое имя.</span><span class="sxs-lookup"><span data-stu-id="2cd0b-122">A green check mark indicates that you have provided a valid name.</span></span>

    ![Создание группы ресурсов](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. <span data-ttu-id="2cd0b-124">В списке **Расположение** выберите центр обработки данных, соответствующий вашему расположению, например "Восточная Австралия".</span><span class="sxs-lookup"><span data-stu-id="2cd0b-124">In the **Location** text box, select a data center appropriate to your location - such as "Australia East".</span></span>
    
    ![Расположение сервера](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > <span data-ttu-id="2cd0b-126">Параметр **Разрешить службам Azure доступ к серверу** невозможно изменить в этой колонке.</span><span class="sxs-lookup"><span data-stu-id="2cd0b-126">The checkbox for **Allow azure services to access server** cannot be changed on this blade.</span></span> <span data-ttu-id="2cd0b-127">Его можно изменить в колонке брандмауэра сервера.</span><span class="sxs-lookup"><span data-stu-id="2cd0b-127">You can change this setting on the server firewall blade.</span></span> <span data-ttu-id="2cd0b-128">Дополнительные сведения см. в статье [Руководство по базам данных SQL: создание учетных записей пользователей базы данных SQL для доступа к базе данных и управления ею с помощью портала Azure](../articles/sql-database/sql-database-manage-servers-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2cd0b-128">For more information, see [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md).</span></span>
    >
    
9. <span data-ttu-id="2cd0b-129">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2cd0b-129">Click **Create**.</span></span>

    ![кнопка "Создать"](./media/sql-data-warehouse-create-logical-server/create.png)

