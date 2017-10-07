---
title: "Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных | Документация Майкрософт"
description: "В этом учебнике используемого при создании конвейера фабрики данных Azure с помощью операции копирования приветствия мастера копирования, поддерживаемые фабрикой данных"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 567b89e7a54c245c134cd0674690e6f3499b46d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a>Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных
> [!div class="op_single_selector"]
> * [Обзор и предварительные требования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Мастер копирования](data-factory-copy-data-wizard-tutorial.md)
> * [Портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Шаблон Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [ИНТЕРФЕЙС REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

В этом учебнике показано как toouse hello **мастер копирования** toocopy данных из базы данных Azure SQL tooan хранилища BLOB-объектов Azure. 

Hello фабрики данных Azure **мастер копирования** позволяет tooquickly создания данных конвейера, который копирует данные из поддерживаемого источника данных хранилища поддерживается tooa целевое хранилище данных. Таким образом рекомендуется использовать мастер hello как первый шаг-toocreate пример конвейера для вашего сценария перемещения данных. Список хранилищ данных, которые поддерживаются в качестве исходных и целевых, см. в разделе [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats).  

Этот учебник показывает, как toocreate фабрикой данных Azure hello запуска мастера копирования пройти несколько шагов tooprovide особенности сценария приема и перемещения данных. После завершения мастера hello hello автоматическое создание конвейера с toocopy действие копирования данных из базы данных Azure SQL tooan хранилища BLOB-объектов Azure. Дополнительные сведения о действии копирования см. в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md).

## <a name="prerequisites"></a>Предварительные требования
Выполните предварительные требования, перечисленные в hello [Обзор учебника](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) статьи перед выполнением этого учебника.

## <a name="create-data-factory"></a>Создание фабрики данных
На этом шаге используется hello Azure портала toocreate фабрикой данных Azure с именем **ADFTutorialDataFactory**.

1. Войдите в слишком[портал Azure](https://portal.azure.com).
2. Нажмите кнопку **+ создать** в левом верхнем углу hello, выберите **данные + аналитика**и нажмите кнопку **фабрики данных**. 
   
   ![Создать -> Фабрика данных](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. В hello **новую фабрику данных** колонки:
   
   1. Введите **ADFTutorialDataFactory** для hello **имя**.
       Имя фабрики данных Azure hello Hello должно быть глобально уникальным. Если ошибка hello: `Data factory name “ADFTutorialDataFactory” is not available`, измените имя hello hello фабрики данных (например, yournameADFTutorialDataFactoryYYYYMMDD) и повторите попытку создания. Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](data-factory-naming-rules.md) , чтобы узнать о правилах именования артефактов фабрики данных.  
      
       ![Имя фабрики данных недоступно](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. Выберите свою **подписку Azure**.
   3. Для группы ресурсов выполните одно из действий hello. 
      
      - Выберите **использовать существующие** tooselect существующую группу ресурсов.
      - Выберите **создать новый** tooenter имя для группы ресурсов.
          
        Некоторые шаги hello в этом учебнике предполагается использовать имя hello: **ADFTutorialResourceGroup** для группы ресурсов hello. toolearn о группах ресурсов. в разделе [с помощью ресурса группы toomanage ресурсам Azure](../azure-resource-manager/resource-group-overview.md).
   4. Выберите **расположение** для фабрики данных hello.
   5. Выберите **toodashboard ПИН-код** флажок hello нижней части колонки hello.  
   6. Щелкните **Создать**.
      
       ![Создать колонку "Фабрика данных"](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. После завершения создания hello, вы видите hello **фабрики данных** колонки, как показано в hello после изображения:
   
   ![Домашняя страница фабрики данных](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a>Запуск мастера копирования
1. В колонке hello фабрики данных, нажмите кнопку **копирование данных [Предварительная версия]** toolaunch hello **мастер копирования**. 
   
   > [!NOTE]
   > При появлении этого веб-браузер hello застряла в «Авторизации...», отключить или снимите **блокировать сторонние файлы cookie и данным сайта** в параметры браузера hello (или) оставьте она включена и создание исключения для  **Login.microsoftonline.com** , затем попытайтесь еще раз запустить мастер hello.
2. В hello **свойства** страницы:
   
   1. В качестве **имени задачи** введите **CopyFromBlobToAzureSql**.
   2. Введите **описание** (необязательно).
   3. Изменение hello **Дата-время начала** и hello **время Дата окончания** так, чтобы дата окончания hello tootoday установите и запустите даты ранее toofive дней.  
   4. Щелкните **Далее**.  
      
      ![Средство копирования — страница "Свойства"](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. На hello **хранилище данных источника** щелкните **хранилища больших двоичных объектов** плитки. Использовать хранилище страницы toospecify hello источника данных для копирования задачу hello. 
   
    ![Средство копирования — страница "Хранилище данных источников"](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. На hello **укажите учетную запись хранилища больших двоичных объектов Azure hello** страницы:
   
   1. В качестве **имени связанной службы** введите **AzureStorageLinkedService**.
   2. Убедитесь, что в качестве **метода выбора учетной записи** выбран вариант **From Azure subscriptions** (Из подписок Azure).
   3. Выберите свою **подписку Azure**.  
   4. Выберите **учетной записи хранилища Azure** из hello список хранилища Azure учетные записи, доступные в hello выбранной подписки. Можно также выбрать tooenter параметры учетной записи хранилища вручную, выбрав **вручную ввести** параметр для hello **учетной записи метод выбора**и нажмите кнопку **Далее**. 
      
      ![Средство копирования — указать учетную запись хранилища больших двоичных объектов Azure hello](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. На **выбрать hello входной файл или папку** страницы:
   
   1. Дважды щелкните папку **adftutorial**.
   2. Выберите **emp.txt** и нажмите кнопку **Выбрать**.
      
      ![Средство копирования: Выбор hello входного файла или папки](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. На hello **выбрать hello входной файл или папку** щелкните **Далее**. Не устанавливайте флажок **Binary copy**(Двоичное копирование). 
   
    ![Средство копирования: Выбор hello входного файла или папки](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. На hello **настроек формата файла** страницы, появятся разделители hello и hello схему, которая определяется автоматически мастером hello путем синтаксического анализа файла hello. Можно также ввести разделители hello вручную для hello копирования мастера toostop автоматическое определение или toooverride. Нажмите кнопку **Далее** после проверки разделители hello и предварительного просмотра данных. 
   
    ![Средство копирования — параметры формата файла](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. В данных назначения hello хранения страницы, выберите **базы данных SQL Azure**и нажмите кнопку **Далее**.
   
    ![Средство копирования — выбор целевого хранилища](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. На **базы данных Azure SQL укажите hello** страницы:
   
   1. Введите **AzureSqlLinkedService** для hello **имя подключения** поля.
   2. В качестве **метода выбора базы данных или сервера** должен быть выбран вариант **From Azure subscriptions** (Из подписок Azure).
   3. Выберите свою **подписку Azure**.  
   4. Выберите **имя сервера** и **базу данных**.
   5. Введите **имя пользователя** и **пароль**.
   6. Щелкните **Далее**.  
      
      ![Средство копирования — указание базы данных SQL Azure](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. На hello **сопоставление таблицы** выберите **emp** для hello **назначения** из раскрывающегося списка hello, щелкните **стрелка вниз** (необязательно) toosee hello схемы и toopreview hello данные.
    
     ![Средство копирования — сопоставление таблиц](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. На hello **сопоставление схемы** щелкните **Далее**.
    
    ![Средство копирования — сопоставление схем](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. На hello **параметры производительности** щелкните **Далее**. 
    
    ![Средство копирования — параметры производительности](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. Просмотрите сведения в hello **Сводка** и нажмите кнопку **Готово**. Hello мастер создает две связанные службы, два набора данных (ввода и вывода) и один конвейер в фабрике данных hello (из которой запущено приветствия мастера копирования). 
    
    ![Средство копирования — параметры производительности](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a>Запуск приложения для отслеживания и управления
1. На hello **развертывания** щелкните ссылку hello: `Click here toomonitor copy pipeline`.
   
   ![Средство копирования — развертывание выполнено](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. мониторинг приложения Hello запускается на отдельной вкладке в веб-браузере.   
   
   ![Приложение мониторинга](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. Последнее состояние toosee hello почасовой секторов, нажмите кнопку **обновление** кнопку в hello **действия WINDOWS** списке нижней hello. Вы увидите пять действий windows пять дней между значениями времени начала и окончания для конвейера hello. Hello списка не обновляется автоматически, поэтому вы можете требуется tooclick обновления несколько раз, чтобы увидеть все windows hello действия в состоянии готовности hello. 
4. Выберите окно действия в списке hello. . В разделе hello сведения о ней в hello **действия окно обозревателя** на hello справа.

    ![Сведения об окне действия](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    Обратите внимание, что даты hello 11, 12, 13, 14 и 15 зеленым цветом, это означает, что hello ежедневного срезы выходных данных для этих дат уже было произведено. Также см. это выделение цветом в конвейер hello и hello выходной набор данных в представлении диаграммы hello. В предыдущем шаге hello Обратите внимание, что двух фрагментов уже создан, один срез обрабатывается в данный момент, hello других двух, ожидающих обработки toobe (с учетом hello цветовое кодирование). 

    Дополнительные сведения об использовании этого приложения см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью приложения для мониторинга и управления](data-factory-monitor-manage-app.md).

## <a name="next-steps"></a>Дальнейшие действия
В этом руководстве в ходе операции копирования вы использовали хранилище BLOB-объектов Azure как исходное хранилище данных, а базу данных SQL Azure — как целевое хранилище данных. Hello следующей таблице приведен список хранилищ данных, поддерживаемые действием копирования hello как источники и назначения: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

Дополнительные сведения о полей и свойств, которые можно увидеть в мастер копирования hello для хранилища данных щелкните ссылку hello hello хранилища данных в таблице hello. 
