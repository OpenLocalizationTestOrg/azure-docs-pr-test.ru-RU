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
# <a name="connect-excel-tooan-azure-sql-database-and-create-a-report"></a>Подключение базы данных Azure SQL tooan Excel и Создание отчета

Соединение Excel tooa базы данных SQL в облаке hello и импорт данных и создайте таблицы и диаграммы на основе значений в базе данных hello. В данном руководстве, вы настроите hello соединение между Excel и таблицы базы данных сохранить файл hello, который хранит сведения о соединении hello и данных для Excel и создайте сводной диаграммы из hello значений базы данных.

Чтобы начать работу, вам понадобится база данных SQL в Azure. Если у вас нет, см. раздел [создания первой базы данных SQL](sql-database-get-started-portal.md) tooget базы данных с образцами данных, работающий через несколько минут. Следуя инструкциям в этой статье, вы импортируете демонстрационные данные в Excel, но те же действия можно выполнять и с собственными данными.

Вам также понадобится копия Excel. В этой статье используется [Microsoft Excel 2016](https://products.office.com/).

## <a name="connect-excel-tooa-sql-database-and-create-an-odc-file"></a>Подключения базы данных SQL tooa Excel и создания odc-файл
1. tooconnect Excel tooSQL базы данных, откройте Excel и затем создать новую книгу или существующей книги Excel.
2. В строке меню hello вверху hello страницы приветствия щелкните **данных**, нажмите кнопку **из других источников**, а затем нажмите кнопку **из SQL Server**.
   
   ![Выберите источник данных: подключение базы данных tooSQL Excel.](./media/sql-database-connect-excel/excel_data_source.png)
   
   Откроется мастер подключения данных Hello.
3. В hello **подключения сервера tooDatabase** диалоговом hello тип базы данных SQL **имя сервера** необходимо tooconnect tooin hello <*servername* > **. database.windows.net**. Например, **adworkserver.database.windows.net**.
4. В разделе **учетные сведения**, нажмите кнопку **hello используйте следующие имя пользователя и пароль**, тип hello **имя пользователя** и **пароль** настроена для Здравствуйте базы данных SQL server при его создании и нажмите кнопку **Далее**.
   
   ![Введите учетные данные имя и имя входа сервера hello](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > В зависимости от сетевой среды не может быть может tooconnect или могут терять соединение hello, если hello базы данных SQL server не разрешает трафик от IP-адреса клиента. Go toohello [портал Azure](https://portal.azure.com/)щелкните серверы SQL Server, щелкните сервер, щелкните в настройках брандмауэра и добавить ваш IP-адрес клиента. В разделе [как параметры брандмауэра tooconfigure](sql-database-configure-firewall-settings.md) подробные сведения.
   > 
   > 
5. В hello **Выбор базы данных и таблицы** диалоговое окно, выберите hello базы данных вы toowork с из списка hello и нажмите кнопку hello таблиц или представлений, которые должны toowork с (мы выбрали **vGetAllCategories**), а затем Нажмите кнопку **Далее**.
   
    ![Выберите базу данных и таблицу.](./media/sql-database-connect-excel/select-database-and-table.png)
   
    Hello **сохранение файла подключения данных и завершение** откроется диалоговое окно, которое необходимо ввести сведения о подключения (*.odc) файла hello Office базы данных, который использует Excel. Можно оставить значения по умолчанию hello или Настройка пользовательских параметров.
6. Можно оставить значения по умолчанию hello, но hello Примечание **имя файла** в частности. Объект **описание**, **понятное имя**, и **ключевые слова для поиска** помочь вам и другим пользователям следует помнить при подключении tooand найти подключение hello. Нажмите кнопку **всегда попытка toouse данные файла toorefresh** следует ли сведения о соединении, хранящиеся в hello odc-файл, чтобы можно было обновить при подключении tooit и нажмите кнопку **Готово**.
   
    ![Сохранение ODC-файла](./media/sql-database-connect-excel/save-odc-file.png)
   
    Hello **импорта данных** откроется диалоговое окно.

## <a name="import-hello-data-into-excel-and-create-a-pivot-chart"></a>Импорт данных hello в Excel и Создание сводной диаграммы
Теперь, когда установлено соединение hello и созданный hello файл с данными и сведения о соединении, вы читаете tooimport hello данных.

1. В hello **импорта данных** диалоговое окно, выберите hello параметры для представления данных в лист hello и нажмите кнопку **ОК**. Мы выбрали режим **Сводная диаграмма**. Вы также можете toocreate **новый лист** или слишком**добавить этот tooa данных модели данных**. Дополнительные сведения о моделях данных см. в статье [Создание модели данных в Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B). Нажмите кнопку **свойства** tooexplore сведения о hello odc-файл, созданный в hello предыдущего шага и toochoose параметров для обновления данных hello.
   
    ![Выбор формата hello для данных в Excel](./media/sql-database-connect-excel/import-data.png)
   
    лист Hello теперь включает пустая сводная таблица и диаграмма.
2. В разделе **полей сводной таблицы**, выберите все hello флажки для hello нужных tooview полей.
   
    ![Настройте отчет базы данных.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> Tooconnect других Excel книги и листы toohello базы данных, нажмите кнопку **данные**, нажмите кнопку **подключений**, нажмите кнопку **добавить**, выберите созданную соединение hello в списке hello и нажмите кнопку **откройте**.
> ![Открытие подключения из другой книги](./media/sql-database-connect-excel/open-from-another-workbook.png)
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
* Узнайте, каким образом слишком[подключения tooSQL базы данных с SQL Server Management Studio](sql-database-connect-query-ssms.md) для сложных запросов и анализа.
* Дополнительные сведения о преимуществах hello [эластичные пулы](sql-database-elastic-pool.md).
* Узнайте, каким образом слишком[Создание веб-приложения, который подключается tooSQL базы данных на внутреннем hello](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).

