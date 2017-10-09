### <a name="prerequisites"></a>Предварительные требования
* Учетная запись Azure. Вы можете создать [бесплатную учетную запись](https://azure.microsoft.com/free).
* [Базы данных SQL Azure](../articles/sql-database/sql-database-get-started.md) с его информацией о соединении, включая hello имя сервера, имя базы данных и имя пользователя и пароль. Эти сведения включаются в hello строку подключения базы данных SQL:
  
    Server=tcp:*имя_вашего_сервера_SQL_Server*.database.windows.net,1433;Initial Catalog=*имя_вашей_БД_SQL*;Persist Security Info=False;User ID={ваше_имя_пользователя};Password={ваш_пароль};MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
  
    Узнайте больше о [базах данных SQL Azure](https://azure.microsoft.com/services/sql-database).

> [!NOTE]
> При создании базы данных SQL Azure, можно также создать образцы баз данных hello, входящий в состав SQL. 
> 
> 

Перед использованием базы данных SQL Azure в приложение логики, подключите tooyour базы данных SQL. Это легко сделать в приложении логику на hello портал Azure.  

Подключение tooyour, база данных SQL Azure с помощью hello следующие шаги:  

1. Создайте приложение логики. В конструкторе логики приложения hello добавить триггер, а затем действие. Выберите **Показать Microsoft управляемых API** в hello раскрывающемся списке, а затем введите «sql» в поле поиска hello. Выберите одно из действий hello:  
   
    ![Этап создания подключения SQL Azure](./media/connectors-create-api-sqlazure/sql-actions.png)
2. Если ранее вы еще не создали все tooSQL подключения базы данных, запрашиваются сведения о подключении hello:  
   
    ![Этап создания подключения SQL Azure](./media/connectors-create-api-sqlazure/connection-details.png) 
3. Введите сведения о базе данных SQL hello. Свойства со звездочкой обязательные.
   
   | Свойство | Сведения |
   | --- | --- |
   | Подключение через шлюз |Не устанавливайте этот флажок. Это используется при подключении tooan локального SQL Server. |
   | Имя подключения* |Введите имя подключения |
   | Имя SQL Server* |Введите имя сервера hello; Это примерно *servername.database.windows.net*. Имя сервера Hello отображается в свойствах базы данных SQL hello в hello портал Azure, а также отображается в строке подключения hello. |
   | Имя базы данных SQL* |Введите имя hello Вы дали базы данных SQL. Указывается в свойствах базы данных SQL hello в строке подключения hello: Initial Catalog =*yoursqldbname*. |
   | Имя пользователя* |Введите имя пользователя hello, созданный при создании hello базы данных SQL. Указывается в свойствах базы данных SQL hello в hello портал Azure. |
   | Пароль* |Введите пароль hello, созданный при создании hello базы данных SQL. |
   
    Эти учетные данные являются используется tooauthorize вашей tooconnect логики приложения и доступа к данным SQL. После завершения вашего сведения о подключении выглядеть аналогично toohello следующие:  
   
    ![Этап создания подключения SQL Azure](./media/connectors-create-api-sqlazure/sample-connection.png) 
4. Нажмите кнопку **Создать**. 
5. Уведомление hello подключения была создана. Теперь, продолжить hello другие действия в приложении логики: 
   
    ![Этап создания подключения SQL Azure](./media/connectors-create-api-sqlazure/table.png)

