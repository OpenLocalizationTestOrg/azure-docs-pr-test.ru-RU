---
title: "tooSQL Excel aaaConnect базы данных | Документы Microsoft"
description: "Узнайте, как Microsoft Excel tooconnect tooAzure SQL базы данных в облаке hello. Импортируйте данные в Excel для создания отчетов и просмотра данных."
services: sql-database
keywords: "подключение excel toosql, импорт данных tooexcel"
documentationcenter: 
author: joseidz
manager: jhubbard
editor: 
ms.assetid: 906924bc-2707-48d3-bac6-397976a0409d
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: jhubbard
ms.openlocfilehash: 0048849432023145bd1009d45b6d9b64a9c7ac3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-tooan-azure-sql-database-and-create-a-report"></a><span data-ttu-id="6e86a-105">Подключение базы данных Azure SQL tooan Excel и Создание отчета</span><span class="sxs-lookup"><span data-stu-id="6e86a-105">Connect Excel tooan Azure SQL database and create a report</span></span>

<span data-ttu-id="6e86a-106">Соединение Excel tooa базы данных SQL в облаке hello и импорт данных и создайте таблицы и диаграммы на основе значений в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="6e86a-106">Connect Excel tooa SQL database in hello cloud and import data and create tables and charts based on values in hello database.</span></span> <span data-ttu-id="6e86a-107">В данном руководстве, вы настроите hello соединение между Excel и таблицы базы данных сохранить файл hello, который хранит сведения о соединении hello и данных для Excel и создайте сводной диаграммы из hello значений базы данных.</span><span class="sxs-lookup"><span data-stu-id="6e86a-107">In this tutorial you will set up hello connection between Excel and a database table, save hello file that stores data and hello connection information for Excel, and then create a pivot chart from hello database values.</span></span>

<span data-ttu-id="6e86a-108">Чтобы начать работу, вам понадобится база данных SQL в Azure.</span><span class="sxs-lookup"><span data-stu-id="6e86a-108">You'll need a SQL database in Azure before you get started.</span></span> <span data-ttu-id="6e86a-109">Если у вас нет, см. раздел [создания первой базы данных SQL](sql-database-get-started-portal.md) tooget базы данных с образцами данных, работающий через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="6e86a-109">If you don't have one, see [Create your first SQL database](sql-database-get-started-portal.md) tooget a database with sample data up and running in a few minutes.</span></span> <span data-ttu-id="6e86a-110">Следуя инструкциям в этой статье, вы импортируете демонстрационные данные в Excel, но те же действия можно выполнять и с собственными данными.</span><span class="sxs-lookup"><span data-stu-id="6e86a-110">In this article, you'll import sample data into Excel from that article, but you can follow similar steps with your own data.</span></span>

<span data-ttu-id="6e86a-111">Вам также понадобится копия Excel.</span><span class="sxs-lookup"><span data-stu-id="6e86a-111">You'll also need a copy of Excel.</span></span> <span data-ttu-id="6e86a-112">В этой статье используется [Microsoft Excel 2016](https://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="6e86a-112">This article uses [Microsoft Excel 2016](https://products.office.com/).</span></span>

## <a name="connect-excel-tooa-sql-database-and-create-an-odc-file"></a><span data-ttu-id="6e86a-113">Подключения базы данных SQL tooa Excel и создания odc-файл</span><span class="sxs-lookup"><span data-stu-id="6e86a-113">Connect Excel tooa SQL database and create an odc file</span></span>
1. <span data-ttu-id="6e86a-114">tooconnect Excel tooSQL базы данных, откройте Excel и затем создать новую книгу или существующей книги Excel.</span><span class="sxs-lookup"><span data-stu-id="6e86a-114">tooconnect Excel tooSQL database, open Excel and then create a new workbook or open an existing Excel workbook.</span></span>
2. <span data-ttu-id="6e86a-115">В строке меню hello вверху hello страницы приветствия щелкните **данных**, нажмите кнопку **из других источников**, а затем нажмите кнопку **из SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="6e86a-115">In hello menu bar at hello top of hello page click **Data**, click **From Other Sources**, and then click **From SQL Server**.</span></span>
   
   ![Выберите источник данных: подключение базы данных tooSQL Excel.](./media/sql-database-connect-excel/excel_data_source.png)
   
   <span data-ttu-id="6e86a-117">Откроется мастер подключения данных Hello.</span><span class="sxs-lookup"><span data-stu-id="6e86a-117">hello Data Connection Wizard opens.</span></span>
3. <span data-ttu-id="6e86a-118">В hello **подключения сервера tooDatabase** диалоговом hello тип базы данных SQL **имя сервера** необходимо tooconnect tooin hello <*servername* > **. database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="6e86a-118">In hello **Connect tooDatabase Server** dialog box, type hello SQL Database **Server name** you want tooconnect tooin hello form <*servername*>**.database.windows.net**.</span></span> <span data-ttu-id="6e86a-119">Например, **adworkserver.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="6e86a-119">For example, **adworkserver.database.windows.net**.</span></span>
4. <span data-ttu-id="6e86a-120">В разделе **учетные сведения**, нажмите кнопку **hello используйте следующие имя пользователя и пароль**, тип hello **имя пользователя** и **пароль** настроена для Здравствуйте базы данных SQL server при его создании и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6e86a-120">Under **Log on credentials**, click **Use hello following User Name and Password**, type hello **User Name** and **Password** you set up for hello SQL Database server when you created it, and then click **Next**.</span></span>
   
   ![Введите учетные данные имя и имя входа сервера hello](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > <span data-ttu-id="6e86a-122">В зависимости от сетевой среды не может быть может tooconnect или могут терять соединение hello, если hello базы данных SQL server не разрешает трафик от IP-адреса клиента.</span><span class="sxs-lookup"><span data-stu-id="6e86a-122">Depending on your network environment, you may not be able tooconnect or you may lose hello connection if hello SQL Database server doesn't allow traffic from your client IP address.</span></span> <span data-ttu-id="6e86a-123">Go toohello [портал Azure](https://portal.azure.com/)щелкните серверы SQL Server, щелкните сервер, щелкните в настройках брандмауэра и добавить ваш IP-адрес клиента.</span><span class="sxs-lookup"><span data-stu-id="6e86a-123">Go toohello [Azure portal](https://portal.azure.com/), click SQL servers, click your server, click firewall under settings and add your client IP address.</span></span> <span data-ttu-id="6e86a-124">В разделе [как параметры брандмауэра tooconfigure](sql-database-configure-firewall-settings.md) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="6e86a-124">See [How tooconfigure firewall settings](sql-database-configure-firewall-settings.md) for details.</span></span>
   > 
   > 
5. <span data-ttu-id="6e86a-125">В hello **Выбор базы данных и таблицы** диалоговое окно, выберите hello базы данных вы toowork с из списка hello и нажмите кнопку hello таблиц или представлений, которые должны toowork с (мы выбрали **vGetAllCategories**), а затем Нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6e86a-125">In hello **Select Database and Table** dialog, select hello database you want toowork with from hello list, and then click hello tables or views you want toowork with (we chose **vGetAllCategories**), and then click **Next**.</span></span>
   
    ![Выберите базу данных и таблицу.](./media/sql-database-connect-excel/select-database-and-table.png)
   
    <span data-ttu-id="6e86a-127">Hello **сохранение файла подключения данных и завершение** откроется диалоговое окно, которое необходимо ввести сведения о подключения (*.odc) файла hello Office базы данных, который использует Excel.</span><span class="sxs-lookup"><span data-stu-id="6e86a-127">hello **Save Data Connection File and Finish** dialog box opens, where you provide information about hello Office database connection (*.odc) file that Excel uses.</span></span> <span data-ttu-id="6e86a-128">Можно оставить значения по умолчанию hello или Настройка пользовательских параметров.</span><span class="sxs-lookup"><span data-stu-id="6e86a-128">You can leave hello defaults or customize your selections.</span></span>
6. <span data-ttu-id="6e86a-129">Можно оставить значения по умолчанию hello, но hello Примечание **имя файла** в частности.</span><span class="sxs-lookup"><span data-stu-id="6e86a-129">You can leave hello defaults, but note hello **File Name** in particular.</span></span> <span data-ttu-id="6e86a-130">Объект **описание**, **понятное имя**, и **ключевые слова для поиска** помочь вам и другим пользователям следует помнить при подключении tooand найти подключение hello.</span><span class="sxs-lookup"><span data-stu-id="6e86a-130">A **Description**, a **Friendly Name**, and **Search Keywords** help you and other users remember what you're connecting tooand find hello connection.</span></span> <span data-ttu-id="6e86a-131">Нажмите кнопку **всегда попытка toouse данные файла toorefresh** следует ли сведения о соединении, хранящиеся в hello odc-файл, чтобы можно было обновить при подключении tooit и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="6e86a-131">Click **Always attempt toouse this file toorefresh data** if you want connection information stored in hello odc file so it can update when you connect tooit, and then click **Finish**.</span></span>
   
    ![Сохранение ODC-файла](./media/sql-database-connect-excel/save-odc-file.png)
   
    <span data-ttu-id="6e86a-133">Hello **импорта данных** откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="6e86a-133">hello **Import data** dialog box appears.</span></span>

## <a name="import-hello-data-into-excel-and-create-a-pivot-chart"></a><span data-ttu-id="6e86a-134">Импорт данных hello в Excel и Создание сводной диаграммы</span><span class="sxs-lookup"><span data-stu-id="6e86a-134">Import hello data into Excel and create a pivot chart</span></span>
<span data-ttu-id="6e86a-135">Теперь, когда установлено соединение hello и созданный hello файл с данными и сведения о соединении, вы читаете tooimport hello данных.</span><span class="sxs-lookup"><span data-stu-id="6e86a-135">Now that you've established hello connection and created hello file with data and connection information, you're reading tooimport hello data.</span></span>

1. <span data-ttu-id="6e86a-136">В hello **импорта данных** диалоговое окно, выберите hello параметры для представления данных в лист hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="6e86a-136">In hello **Import Data** dialog, click hello option you want for presenting your data in hello worksheet and then click **OK**.</span></span> <span data-ttu-id="6e86a-137">Мы выбрали режим **Сводная диаграмма**.</span><span class="sxs-lookup"><span data-stu-id="6e86a-137">We chose **PivotChart**.</span></span> <span data-ttu-id="6e86a-138">Вы также можете toocreate **новый лист** или слишком**добавить этот tooa данных модели данных**.</span><span class="sxs-lookup"><span data-stu-id="6e86a-138">You can also choose toocreate a **New worksheet** or too**Add this data tooa Data Model**.</span></span> <span data-ttu-id="6e86a-139">Дополнительные сведения о моделях данных см. в статье [Создание модели данных в Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span><span class="sxs-lookup"><span data-stu-id="6e86a-139">For more information on Data Models, see [Create a data model in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span></span> <span data-ttu-id="6e86a-140">Нажмите кнопку **свойства** tooexplore сведения о hello odc-файл, созданный в hello предыдущего шага и toochoose параметров для обновления данных hello.</span><span class="sxs-lookup"><span data-stu-id="6e86a-140">Click **Properties** tooexplore information about hello odc file you created in hello previous step and toochoose options for refreshing hello data.</span></span>
   
    ![Выбор формата hello для данных в Excel](./media/sql-database-connect-excel/import-data.png)
   
    <span data-ttu-id="6e86a-142">лист Hello теперь включает пустая сводная таблица и диаграмма.</span><span class="sxs-lookup"><span data-stu-id="6e86a-142">hello worksheet now has an empty pivot table and chart.</span></span>
2. <span data-ttu-id="6e86a-143">В разделе **полей сводной таблицы**, выберите все hello флажки для hello нужных tooview полей.</span><span class="sxs-lookup"><span data-stu-id="6e86a-143">Under **PivotTable Fields**, select all hello check-boxes for hello fields you want tooview.</span></span>
   
    ![Настройте отчет базы данных.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> <span data-ttu-id="6e86a-145">Tooconnect других Excel книги и листы toohello базы данных, нажмите кнопку **данные**, нажмите кнопку **подключений**, нажмите кнопку **добавить**, выберите созданную соединение hello в списке hello и нажмите кнопку **откройте**.</span><span class="sxs-lookup"><span data-stu-id="6e86a-145">If you want tooconnect other Excel workbooks and worksheets toohello database, click **Data**, click **Connections**, click **Add**, choose hello connection you created from hello list, and then click **Open**.</span></span>
> <span data-ttu-id="6e86a-146">![Открытие подключения из другой книги](./media/sql-database-connect-excel/open-from-another-workbook.png)</span><span class="sxs-lookup"><span data-stu-id="6e86a-146">![Open a connection from another workbook](./media/sql-database-connect-excel/open-from-another-workbook.png)</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6e86a-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6e86a-147">Next steps</span></span>
* <span data-ttu-id="6e86a-148">Узнайте, каким образом слишком[подключения tooSQL базы данных с SQL Server Management Studio](sql-database-connect-query-ssms.md) для сложных запросов и анализа.</span><span class="sxs-lookup"><span data-stu-id="6e86a-148">Learn how too[Connect tooSQL Database with SQL Server Management Studio](sql-database-connect-query-ssms.md) for advanced querying and analysis.</span></span>
* <span data-ttu-id="6e86a-149">Дополнительные сведения о преимуществах hello [эластичные пулы](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="6e86a-149">Learn about hello benefits of [elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="6e86a-150">Узнайте, каким образом слишком[Создание веб-приложения, который подключается tooSQL базы данных на внутреннем hello](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="6e86a-150">Learn how too[create a web application that connects tooSQL Database on hello back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span>

