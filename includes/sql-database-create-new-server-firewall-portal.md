
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, hello following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Создание правила брандмауэра уровня сервера в hello портал Azure

1. В колонке сервера SQL hello в разделе Параметры щелкните **брандмауэра** tooopen hello брандмауэра колонке hello SQL server.

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. Просмотрите отображается IP-адрес клиента hello и проверить, что это ваш IP-адрес на hello Интернета в браузере по вашему выбору (Узнайте, «какова свой IP-адрес). Иногда адреса могут не совпадать по тем или иным причинам.

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. Предположим, что соответствует hello IP-адреса, нажмите кнопку **добавить IP-адрес клиента** на панели инструментов hello.

    ![Кнопка "Добавить IP-адрес клиента"](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > Можно открыть брандмауэр базы данных SQL hello на hello tooa один IP-адрес сервера или весь диапазон адресов. Открытие hello брандмауэра позволяет администраторам SQL и базы данных tooany toologin пользователей на hello toowhich сервера, они имеют допустимые учетные данные.
    >

4. Нажмите кнопку **Сохранить** на hello инструментов toosave этого правила брандмауэра уровня сервера и нажмите кнопку **ОК**.

    ![Кнопка "Добавить IP-адрес клиента"](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> Подробное руководство см. в статье [Руководство по базам данных SQL: создание базы данных SQL за несколько минут с помощью портала Azure](../articles/sql-database/sql-database-get-started.md).    
>
