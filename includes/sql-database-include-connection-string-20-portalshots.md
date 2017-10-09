
<!--
includes/sql-database-include-connection-string-20-portalshots.md

Latest Freshness check:  2015-09-02 , GeneMi.

## Connection string
-->


### <a name="obtain-hello-connection-string-from-hello-azure-portal"></a>Получить строку подключения hello hello портал Azure
Используйте hello [портал Azure](https://portal.azure.com/) строка подключения hello tooobtain, необходимые для вашего клиента toointeract программы, с базой данных SQL Azure: 

1. Выберите **ОБЗОР** > **Базы данных SQL**.
2. Введите имя базы данных hello в hello фильтра текстовое поле рядом с левого верхнего hello hello **баз данных SQL** колонку.
3. Щелкните строку hello для базы данных.
4. После появления hello колонке базы данных для удобства visual, можно нажать кнопку hello Стандартная свести к минимуму колонках hello toocollapse элементы управления используются для просмотра и фильтрации базы данных. 
   
    ![Фильтрация tooisolate базы данных][10-FilterDatabase]
5. В колонке hello для базы данных, нажмите кнопку **Показать строки подключения базы данных**.
6. Если библиотека подключения ADO.NET toouse hello, скопируйте строку hello с меткой **ADO**. 
   
    ![Скопируйте строку подключения ADO hello для базы данных][20-CopyAdoConnectionString]
7. В той или иной одного формата вставьте строку hello подключения в коде программы клиента.

Дополнительные сведения можно найти в разделе <br/>[Строки подключения и файлы конфигурации](http://msdn.microsoft.com/library/ms254494.aspx).

<!-- Image references. -->

[10-FilterDatabase]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-a.png

[20-CopyAdoConnectionString]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-b.png


<!--
These three includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-connection-string-20-portalshots.md
includes/sql-database-include-connection-string-30-compare.md
includes/sql-database-include-connection-string-40-config.md
-->
