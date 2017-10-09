
<!--
includes/sql-database-create-new-server-firewall-portal.md

Latest Freshness check:  2016-11-28 , rickbyh.

As of circa 2016-04-11, hello following topics might include this include:
articles/sql-database/sql-database-get-started.md
articles/sql-database/sql-database-configure-firewall-settings
articles/sql-data-warehouse-get-started-provision.md

-->
### <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="40352-101">Создание правила брандмауэра уровня сервера в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="40352-101">Create a server-level firewall rule in hello Azure portal</span></span>

1. <span data-ttu-id="40352-102">В колонке сервера SQL hello в разделе Параметры щелкните **брандмауэра** tooopen hello брандмауэра колонке hello SQL server.</span><span class="sxs-lookup"><span data-stu-id="40352-102">On hello SQL server blade, under Settings, click **Firewall** tooopen hello Firewall blade for hello SQL server.</span></span>

    <!-- ![sql server firewall](../articles/sql-database/media/sql-database-get-started/sql-server-firewall.png) -->

2. <span data-ttu-id="40352-103">Просмотрите отображается IP-адрес клиента hello и проверить, что это ваш IP-адрес на hello Интернета в браузере по вашему выбору (Узнайте, «какова свой IP-адрес).</span><span class="sxs-lookup"><span data-stu-id="40352-103">Review hello client IP address displayed and validate that this is your IP address on hello Internet using a browser of your choice (ask "what is my IP address).</span></span> <span data-ttu-id="40352-104">Иногда адреса могут не совпадать по тем или иным причинам.</span><span class="sxs-lookup"><span data-stu-id="40352-104">Occasionally they do not match for a various reasons.</span></span>

    <!-- ![your IP address](../articles/sql-database/media/sql-database-get-started/your-ip-address.png) -->

3. <span data-ttu-id="40352-105">Предположим, что соответствует hello IP-адреса, нажмите кнопку **добавить IP-адрес клиента** на панели инструментов hello.</span><span class="sxs-lookup"><span data-stu-id="40352-105">Assuming that hello IP addresses match, click **Add client IP** on hello toolbar.</span></span>

    ![Кнопка "Добавить IP-адрес клиента"](../articles/sql-data-warehouse/media/sql-data-warehouse-get-started-provision/add-client-ip.png)

    > [!NOTE]
    > <span data-ttu-id="40352-107">Можно открыть брандмауэр базы данных SQL hello на hello tooa один IP-адрес сервера или весь диапазон адресов.</span><span class="sxs-lookup"><span data-stu-id="40352-107">You can open hello SQL Database firewall on hello server tooa single IP address or an entire range of addresses.</span></span> <span data-ttu-id="40352-108">Открытие hello брандмауэра позволяет администраторам SQL и базы данных tooany toologin пользователей на hello toowhich сервера, они имеют допустимые учетные данные.</span><span class="sxs-lookup"><span data-stu-id="40352-108">Opening hello firewall enables SQL administrators and users toologin tooany database on hello server toowhich they have valid credentials.</span></span>
    >

4. <span data-ttu-id="40352-109">Нажмите кнопку **Сохранить** на hello инструментов toosave этого правила брандмауэра уровня сервера и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="40352-109">Click **Save** on hello toolbar toosave this server-level firewall rule and then click **OK**.</span></span>

    ![Кнопка "Добавить IP-адрес клиента"](../articles/sql-database/media/sql-database-get-started-portal/server-firewall-rule.png)

> [!Tip]
> <span data-ttu-id="40352-111">Подробное руководство см. в статье [Руководство по базам данных SQL: создание базы данных SQL за несколько минут с помощью портала Azure](../articles/sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="40352-111">For a tutorial, see [SQL Database tutorial: Create a server, a server-level firewall rule, a sample database, a database-level firewall rule and connect with SQL Server](../articles/sql-database/sql-database-get-started.md).</span></span>    
>
