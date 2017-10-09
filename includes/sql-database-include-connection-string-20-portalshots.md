
<!--
includes/sql-database-include-connection-string-20-portalshots.md

Latest Freshness check:  2015-09-02 , GeneMi.

## Connection string
-->


### <a name="obtain-hello-connection-string-from-hello-azure-portal"></a><span data-ttu-id="1fce2-101">Получить строку подключения hello hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="1fce2-101">Obtain hello connection string from hello Azure portal</span></span>
<span data-ttu-id="1fce2-102">Используйте hello [портал Azure](https://portal.azure.com/) строка подключения hello tooobtain, необходимые для вашего клиента toointeract программы, с базой данных SQL Azure:</span><span class="sxs-lookup"><span data-stu-id="1fce2-102">Use hello [Azure portal](https://portal.azure.com/) tooobtain hello connection string necessary for your client program toointeract with Azure SQL Database:</span></span> 

1. <span data-ttu-id="1fce2-103">Выберите **ОБЗОР** > **Базы данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="1fce2-103">Click **BROWSE** > **SQL databases**.</span></span>
2. <span data-ttu-id="1fce2-104">Введите имя базы данных hello в hello фильтра текстовое поле рядом с левого верхнего hello hello **баз данных SQL** колонку.</span><span class="sxs-lookup"><span data-stu-id="1fce2-104">Enter hello name of your database into hello filter text box near hello upper-left of hello **SQL databases** blade.</span></span>
3. <span data-ttu-id="1fce2-105">Щелкните строку hello для базы данных.</span><span class="sxs-lookup"><span data-stu-id="1fce2-105">Click hello row for your database.</span></span>
4. <span data-ttu-id="1fce2-106">После появления hello колонке базы данных для удобства visual, можно нажать кнопку hello Стандартная свести к минимуму колонках hello toocollapse элементы управления используются для просмотра и фильтрации базы данных.</span><span class="sxs-lookup"><span data-stu-id="1fce2-106">After hello blade appears for your database, for visual convenience you can click hello standard minimize controls toocollapse hello blades  you used for browsing and database filtering.</span></span> 
   
    ![Фильтрация tooisolate базы данных][10-FilterDatabase]
5. <span data-ttu-id="1fce2-108">В колонке hello для базы данных, нажмите кнопку **Показать строки подключения базы данных**.</span><span class="sxs-lookup"><span data-stu-id="1fce2-108">On hello blade for your database, click **Show database connection strings**.</span></span>
6. <span data-ttu-id="1fce2-109">Если библиотека подключения ADO.NET toouse hello, скопируйте строку hello с меткой **ADO**.</span><span class="sxs-lookup"><span data-stu-id="1fce2-109">If you intend toouse hello ADO.NET connection library, copy hello string labeled **ADO**.</span></span> 
   
    ![Скопируйте строку подключения ADO hello для базы данных][20-CopyAdoConnectionString]
7. <span data-ttu-id="1fce2-111">В той или иной одного формата вставьте строку hello подключения в коде программы клиента.</span><span class="sxs-lookup"><span data-stu-id="1fce2-111">In one format or another, paste hello connection string information into your client program code.</span></span>

<span data-ttu-id="1fce2-112">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="1fce2-112">For more information, see:</span></span><br/><span data-ttu-id="1fce2-113">[Строки подключения и файлы конфигурации](http://msdn.microsoft.com/library/ms254494.aspx).</span><span class="sxs-lookup"><span data-stu-id="1fce2-113">[Connection Strings and Configuration Files](http://msdn.microsoft.com/library/ms254494.aspx).</span></span>

<!-- Image references. -->

[10-FilterDatabase]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-a.png

[20-CopyAdoConnectionString]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-b.png


<!--
These three includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-connection-string-20-portalshots.md
includes/sql-database-include-connection-string-30-compare.md
includes/sql-database-include-connection-string-40-config.md
-->
