### <a name="create-a-new-logical-sql-server-in-hello-azure-portal"></a>Создание нового логического сервера SQL в hello портал Azure

1. Щелкните **Создать**, выполните поиск по запросу **логический сервер** и нажмите клавишу **ВВОД**.

    ![поиск логического сервера](./media/sql-data-warehouse-create-logical-server/search-logical-server.png)
2. Выберите **SQL Server (логический сервер)**. 

    ![выбор логического сервера](./media/sql-data-warehouse-create-logical-server/select-logical-server.png)
  
3. Нажмите кнопку **создать** tooopen hello Новая колонка SQL Server (логический сервер).

   <kbd>![открыть колонку логический сервер](./media/sql-data-warehouse-create-logical-server/open-logical-server-blade.png) </kbd> <kbd> ![колонке логический сервер](./media/sql-data-warehouse-create-logical-server/logical-server-blade.png)</kbd>
  
3. В текстовом поле имя сервера SQL Server (логический сервер) колонке hello укажите допустимое имя для нового логического сервера hello. Зеленый флажок указывает, что выбрано допустимое имя.
    
    ![Имя нового сервера](./media/sql-data-warehouse-create-logical-server/new-name-logical-server.png)

    > [!IMPORTANT]
    > Hello полное имя для нового сервера будет < your_server_name >. database.windows.net.
    >
    
4. В hello Server admin входа текстовом поле Укажите имя пользователя для входа проверки подлинности SQL hello для этого сервера. Это имя входа называется именем входа субъекта сервера hello. Зеленый флажок указывает, что выбрано допустимое имя.
    
    ![Учетные данные администратора SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-login.png)
5. В hello **пароль** и **подтверждение пароля** текстовых полей, укажите пароль для учетной записи имени входа субъекта сервера hello. Зеленый флажок указывает, что выбран допустимый пароль.
    
    ![Пароль администратора SQL](./media/sql-data-warehouse-create-logical-server/sql-admin-password.png)
6. Выберите подписку, в котором имеется разрешение toocreate объектов.

    ![Подписка](./media/sql-data-warehouse-create-logical-server/subscription.png)
7. В текстовом поле Группа ресурсов hello, выберите **создать новый** и в текстовом поле Группа ресурсов hello, укажите допустимое имя для hello (может использоваться существующая группа ресурсов, если вы уже создали сами) новой группы ресурсов. Зеленый флажок указывает, что выбрано допустимое имя.

    ![Создание группы ресурсов](./media/sql-data-warehouse-create-logical-server/new-resource-group.png)

8. В hello **расположение** текстовое поле, выберите данные центру соответствующие tooyour расположение — например «Австралия East».
    
    ![Расположение сервера](./media/sql-data-warehouse-create-logical-server/server-location.png)
    
    > [!TIP]
    > Здравствуйте, флажок для **tooaccess сервера разрешить службам azure** нельзя изменить на эту колонку. Можно изменить эту настройку в колонке брандмауэра сервера hello. Дополнительные сведения см. в статье [Руководство по базам данных SQL: создание учетных записей пользователей базы данных SQL для доступа к базе данных и управления ею с помощью портала Azure](../articles/sql-database/sql-database-manage-servers-portal.md).
    >
    
9. Щелкните **Создать**.

    ![кнопка "Создать"](./media/sql-data-warehouse-create-logical-server/create.png)

