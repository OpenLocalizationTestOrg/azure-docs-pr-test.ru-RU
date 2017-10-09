
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. Войдите в toohello [портал Azure](https://portal.azure.com/) на http://portal.azure.com/.
2. В hello слева щелкните **ПРОСМОТРЕТЬ все**. Hello **Обзор** колонке отображается.
3. Найдите и выберите **Серверы SQL Server**. Hello **серверов SQL Server** колонке отображается.
   
    ![Найдите сервер базы данных SQL Azure на портале hello][b21-FindServerInPortal]
4. Для удобства щелкните hello свести к минимуму управления на ранее hello **Обзор** колонку.
5. В текстовом поле фильтра hello начните вводить имя сервера hello. Отобразится строка.
6. Щелкните строку hello для вашего сервера. Отобразится колонка для вашего сервера.
7. На колонке вашего сервера нажмите кнопку **Параметры**. Hello **параметры** колонке отображается.
8. Щелкните пункт **Брандмауэр**. Hello **параметры брандмауэра** колонке отображается.
   
    ![Последовательно выберите пункты "Параметры" > "Брандмауэр"][b31-SettingsFirewallNavig]
9. Щелкните **Добавить IP-адрес клиента**. Введите имя для нового правила в первом текстовом поле hello.
10. Тип в hello низким и высоким IP-адрес значения для hello диапазон tooenable.
    
    * Это может быть удобно toohave hello низкое значение заканчиваться **.0** и hello высокого уровня с **.255**.
    
    ![Добавить tooallow диапазона адресов IP][b41-AddRange]
11. Щелкните **Сохранить**.

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
