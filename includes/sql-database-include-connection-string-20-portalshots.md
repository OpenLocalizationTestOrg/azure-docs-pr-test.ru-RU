
<!--
includes/sql-database-include-connection-string-20-portalshots.md

Latest Freshness check:  2015-09-02 , GeneMi.

## Connection string
-->


### <a name="obtain-the-connection-string-from-the-azure-portal"></a><span data-ttu-id="5741b-101">Получение строки подключения на портале Azure</span><span class="sxs-lookup"><span data-stu-id="5741b-101">Obtain the connection string from the Azure portal</span></span>
<span data-ttu-id="5741b-102">Для получения строки подключения, необходимой для взаимодействия клиентской программы с Базой данных SQL Azure, используйте [портал Azure](https://portal.azure.com/) .</span><span class="sxs-lookup"><span data-stu-id="5741b-102">Use the [Azure portal](https://portal.azure.com/) to obtain the connection string necessary for your client program to interact with Azure SQL Database:</span></span> 

1. <span data-ttu-id="5741b-103">Выберите **ОБЗОР** > **Базы данных SQL**.</span><span class="sxs-lookup"><span data-stu-id="5741b-103">Click **BROWSE** > **SQL databases**.</span></span>
2. <span data-ttu-id="5741b-104">Введите имя базы данных в текстовое поле фильтра рядом с верхней левой частью колонки **базы данных SQL** .</span><span class="sxs-lookup"><span data-stu-id="5741b-104">Enter the name of your database into the filter text box near the upper-left of the **SQL databases** blade.</span></span>
3. <span data-ttu-id="5741b-105">Щелкните строку с вашей базой данных.</span><span class="sxs-lookup"><span data-stu-id="5741b-105">Click the row for your database.</span></span>
4. <span data-ttu-id="5741b-106">Для наглядности после появления колонки для базы данных можно щелкнуть стандартный элемент управления, чтобы свернуть колонки, используемые для просмотра и фильтрации базы данных.</span><span class="sxs-lookup"><span data-stu-id="5741b-106">After the blade appears for your database, for visual convenience you can click the standard minimize controls to collapse the blades  you used for browsing and database filtering.</span></span> 
   
    ![Фильтр для определения базы данных][10-FilterDatabase]
5. <span data-ttu-id="5741b-108">На колонке для базы данных нажмите **Показать строки подключения к базе данных**.</span><span class="sxs-lookup"><span data-stu-id="5741b-108">On the blade for your database, click **Show database connection strings**.</span></span>
6. <span data-ttu-id="5741b-109">Если вы планируете использовать библиотеку подключений ADO.NET, скопируйте строку с меткой **ADO**.</span><span class="sxs-lookup"><span data-stu-id="5741b-109">If you intend to use the ADO.NET connection library, copy the string labeled **ADO**.</span></span> 
   
    ![Копирование строки подключения ADO для базы данных][20-CopyAdoConnectionString]
7. <span data-ttu-id="5741b-111">Вставьте строку подключения в код клиентской программы в одном или другом формате.</span><span class="sxs-lookup"><span data-stu-id="5741b-111">In one format or another, paste the connection string information into your client program code.</span></span>

<span data-ttu-id="5741b-112">Дополнительные сведения можно найти в разделе </span><span class="sxs-lookup"><span data-stu-id="5741b-112">For more information, see:</span></span><br/><span data-ttu-id="5741b-113">[Строки подключения и файлы конфигурации](http://msdn.microsoft.com/library/ms254494.aspx).</span><span class="sxs-lookup"><span data-stu-id="5741b-113">[Connection Strings and Configuration Files](http://msdn.microsoft.com/library/ms254494.aspx).</span></span>

<!-- Image references. -->

[10-FilterDatabase]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-a.png

[20-CopyAdoConnectionString]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-b.png


<!--
These three includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-connection-string-20-portalshots.md
includes/sql-database-include-connection-string-30-compare.md
includes/sql-database-include-connection-string-40-config.md
-->
