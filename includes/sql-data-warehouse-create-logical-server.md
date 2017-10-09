### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a><span data-ttu-id="9c52b-101">Создание нового логического сервера SQL в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="9c52b-101">Create a new logical SQL server in hello Azure portal</span></span>

1. <span data-ttu-id="9c52b-102">Щелкните **Создать**, выполните поиск по запросу **логический сервер** и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="9c52b-102">Click **New**, search **logical server**, and then hit **ENTER**.</span></span>

    ![поиск логического сервера](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. <span data-ttu-id="9c52b-104">Выберите **SQL Server (логический сервер)**.</span><span class="sxs-lookup"><span data-stu-id="9c52b-104">Select **SQL server (logical server)**</span></span> 

    ![выбор логического сервера](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. <span data-ttu-id="9c52b-106">Нажмите кнопку **создать** tooopen hello Новая колонка SQL Server (логический сервер).</span><span class="sxs-lookup"><span data-stu-id="9c52b-106">Click **Create** tooopen hello new SQL Server (logical server) blade.</span></span>

   <span data-ttu-id="9c52b-107"><kbd>![открыть колонку логический сервер](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![колонке логический сервер](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd></span><span class="sxs-lookup"><span data-stu-id="9c52b-107"><kbd> ![open logical server blade](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd>![logical server blade](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png) </kbd></span></span>
  
3. <span data-ttu-id="9c52b-108">В текстовом поле имя сервера SQL Server (логический сервер) колонке hello укажите допустимое имя для нового логического сервера hello.</span><span class="sxs-lookup"><span data-stu-id="9c52b-108">In hello SQL Server (logical server) blade's server name text box, provide a valid name for hello new logical server.</span></span> <span data-ttu-id="9c52b-109">Зеленый флажок указывает, что выбрано допустимое имя.</span><span class="sxs-lookup"><span data-stu-id="9c52b-109">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![Имя нового сервера](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > <span data-ttu-id="9c52b-111">Hello полное имя для нового сервера будет < your_server_name >. database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="9c52b-111">hello fully qualified name for your new server will be <your_server_name>.database.windows.net.</span></span>
    >
    
4. <span data-ttu-id="9c52b-112">В hello Server admin входа текстовом поле Укажите имя пользователя для входа проверки подлинности SQL hello для этого сервера.</span><span class="sxs-lookup"><span data-stu-id="9c52b-112">In hello Server admin login text box, provide a user name for hello SQL authentication login for this server.</span></span> <span data-ttu-id="9c52b-113">Это имя входа называется именем входа субъекта сервера hello.</span><span class="sxs-lookup"><span data-stu-id="9c52b-113">This login is known as hello server principal login.</span></span> <span data-ttu-id="9c52b-114">Зеленый флажок указывает, что выбрано допустимое имя.</span><span class="sxs-lookup"><span data-stu-id="9c52b-114">A green check mark indicates that you have provided a valid name.</span></span>
    
    ![Учетные данные администратора SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. <span data-ttu-id="9c52b-116">В hello **пароль** и **подтверждение пароля** текстовых полей, укажите пароль для учетной записи имени входа субъекта сервера hello.</span><span class="sxs-lookup"><span data-stu-id="9c52b-116">In hello **Password** and **Confirm password** text boxes, provide a password for hello server principal login account.</span></span> <span data-ttu-id="9c52b-117">Зеленый флажок указывает, что выбран допустимый пароль.</span><span class="sxs-lookup"><span data-stu-id="9c52b-117">A green check mark indicates that you have provided a valid password.</span></span>
    
    ![Пароль администратора SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. <span data-ttu-id="9c52b-119">Выберите подписку, в котором имеется разрешение toocreate объектов.</span><span class="sxs-lookup"><span data-stu-id="9c52b-119">Select a subscription in which you have permission toocreate objects.</span></span>

    ![Подписка](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. <span data-ttu-id="9c52b-121">В текстовом поле Группа ресурсов hello, выберите **создать новый** и в текстовом поле Группа ресурсов hello, укажите допустимое имя для hello (может использоваться существующая группа ресурсов, если вы уже создали сами) новой группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9c52b-121">In hello Resource group text box, select **Create new** and then, in hello resource group text box, provide a valid name for hello new resource group (you can also use an existing resource group if you have already created one for yourself).</span></span> <span data-ttu-id="9c52b-122">Зеленый флажок указывает, что выбрано допустимое имя.</span><span class="sxs-lookup"><span data-stu-id="9c52b-122">A green check mark indicates that you have provided a valid name.</span></span>

    ![Создание группы ресурсов](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. <span data-ttu-id="9c52b-124">В hello **расположение** текстовое поле, выберите данные центру соответствующие tooyour расположение — например «Австралия East».</span><span class="sxs-lookup"><span data-stu-id="9c52b-124">In hello **Location** text box, select a data center appropriate tooyour location - such as "Australia East".</span></span>
    
    ![Расположение сервера](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > <span data-ttu-id="9c52b-126">Здравствуйте, флажок для **tooaccess сервера разрешить службам azure** нельзя изменить на эту колонку.</span><span class="sxs-lookup"><span data-stu-id="9c52b-126">hello checkbox for **Allow azure services tooaccess server** cannot be changed on this blade.</span></span> <span data-ttu-id="9c52b-127">Можно изменить эту настройку в колонке брандмауэра сервера hello.</span><span class="sxs-lookup"><span data-stu-id="9c52b-127">You can change this setting on hello server firewall blade.</span></span> <span data-ttu-id="9c52b-128">Дополнительные сведения см. в статье [Руководство по базам данных SQL: создание учетных записей пользователей базы данных SQL для доступа к базе данных и управления ею с помощью портала Azure](../articles/sql-database/sql-database-manage-servers-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9c52b-128">For more information, see [Get started with security](../articles/sql-database/sql-database-manage-servers-portal.md).</span></span>
    >
    
9. <span data-ttu-id="9c52b-129">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9c52b-129">Click **Create**.</span></span>

    ![кнопка "Создать"](./media/sql-data-warehouse-create-logical-server/create.png)

