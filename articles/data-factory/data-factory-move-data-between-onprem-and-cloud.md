---
title: "данные aaaMove - шлюз управления данными | Документы Microsoft"
description: "Настройка шлюза данных toomove данных между локальными и hello облака. Используйте шлюз управления данными в toomove фабрики данных Azure данные."
keywords: "шлюз данных, интеграции данных, перемещение данных, учетные данные шлюза"
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 7bf6d8fd-04b5-499d-bd19-eff217aa4a9c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 314341c142d5260c785b7e82081774f044450e81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-between-on-premises-sources-and-hello-cloud-with-data-management-gateway"></a>Перемещение данных между локальным источникам и hello облако с помощью шлюза управления данными
Эта статья содержит общие сведения об интеграции данных, хранящихся в локальных и облачных хранилищах данных, с помощью фабрики данных. Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) других данных фабрики основных понятий статей: [наборы данных](data-factory-create-datasets.md) и [конвейеры](data-factory-create-pipelines.md).

## <a name="data-management-gateway"></a>Шлюз управления данными
Шлюз управления данными необходимо установить на перемещение данных из хранилища данных в локальной машины tooenable вашей локальной система. можно установить шлюз Hello на приветствия же компьютера как hello хранилища данных или на другом компьютере, до тех пор, пока шлюз hello может подключаться toohello хранилища данных.

> [!IMPORTANT]
> Дополнительные сведения о шлюзе управления данными см. в статье [Шлюз управления данными](data-factory-data-management-gateway.md). 

Hello следующем пошаговом руководстве показано, как toocreate фабрики данных с конвейером, который перемещает данные из локальной среды **SQL Server** tooan хранилище больших двоичных объектов базы данных. В рамках пошагового руководства hello установите и настройте hello шлюз управления данными на компьютере.

## <a name="walkthrough-copy-on-premises-data-toocloud"></a>Пошаговое руководство: копирование локальных данных toocloud
В этом пошаговом руководстве hello следующие действия: 

1. Создадите фабрику данных.
2. Создадите шлюз управления данными. 
3. Создадите связанные службы для хранилища данных-источника и приемника.
4. Создания наборов данных toorepresent входных и выходных данных.
5. Создайте конвейер данными hello toomove действия копирования.

## <a name="prerequisites-for-hello-tutorial"></a>Необходимые условия для учебника hello
Прежде чем начать в данном пошаговом руководстве, необходимо иметь hello следующие предварительные требования:

* **Подписка Azure**.  Если у вас нет подписки, вы можете создать бесплатную пробную версию учетной записи всего за несколько минут. В разделе hello [бесплатной пробной версии](http://azure.microsoft.com/pricing/free-trial/) Дополнительные сведения см.
* **исходного**хранилища данных. Использовать хранилище больших двоичных объектов hello как **назначения и приемника** хранилище данных в этом учебнике. При отсутствии учетной записи хранилища Azure в разделе hello [создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account) статьи для действия toocreate один.
* **SQL Server.** В этом руководстве используйте локальную базу данных SQL Server в качестве **исходного** хранилища данных. 

## <a name="create-data-factory"></a>Создание фабрики данных
На этом шаге используется hello Azure портала toocreate экземпляр фабрики данных Azure с именем **ADFTutorialOnPremDF**.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Щелкните **+ New** (+ Создать), **Аналитика**, а затем — **Фабрика данных**.

   ![Создать -> Фабрика данных](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. В hello **новую фабрику данных** введите **ADFTutorialOnPremDF** для hello имя.

    ![Добавить tooStartboard](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > Имя фабрики данных Azure hello Hello должно быть глобально уникальным. Если ошибка hello: **имя фабрики данных «ADFTutorialOnPremDF» недоступен**, измените имя hello hello фабрики данных (например, yournameADFTutorialOnPremDF) и повторите попытку создания. Выполняя оставшиеся действия, описанные в этом руководстве, вместо ADFTutorialOnPremDF используйте именно это имя.
   >
   > Имя фабрики данных hello Hello может быть зарегистрирован как **DNS** имя в будущем hello и поэтому становятся общедоступен.
   >
   >
4. Выберите hello **подписки Azure** место hello данных фабрики toobe создан.
5. Выберите имеющуюся **группу ресурсов** или создайте новую. Hello учебник, создать группу ресурсов с именем: **ADFTutorialResourceGroup**.
6. Нажмите кнопку **создать** на hello **новую фабрику данных** страницы.

   > [!IMPORTANT]
   > экземпляры toocreate фабрики данных, необходимо быть членом hello [участника фабрики данных](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) роли на уровне группы hello подписки или ресурса.
   >
   >
7. После завершения создания вы видите hello **фабрики данных** страницы, как показано в hello после изображения:

   ![Домашняя страница фабрики данных](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a>Создание шлюза
1. В hello **фабрики данных** щелкните **автор и развернуть** hello toolaunch плитки **редактор** для фабрики данных hello.

    ![Плитка "Создание и развертывание"](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. В hello редактор фабрики данных, нажмите кнопку **... Дополнительные** на hello панели инструментов, а затем нажмите кнопку **шлюз данных**. Кроме того, можно щелкнуть **шлюзы данных** в hello представление в виде дерева и нажмите кнопку **шлюз данных**.

   ![«Новый шлюз данных» на панели инструментов](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. В hello **создать** введите **adftutorialgateway** для hello **имя**и нажмите кнопку **ОК**.     

    ![Страница "Создать шлюз"](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > В этом пошаговом руководстве создается логический шлюза hello с только один узел (Windows на локальном компьютере). Шлюз управления данными можно масштабировать, объединяя несколько локальных компьютеров с hello шлюза. Чтобы увеличить масштаб, увеличьте число заданий перемещения данных, которые могут выполняться одновременно на узле. Эта функция также доступна для логического шлюза с одним узлом. Дополнительные сведения см. в статье [Шлюз управления данными: высокий уровень доступности и масштабируемость (предварительная версия)](data-factory-data-management-gateway-high-availability-scalability.md).  
4. В hello **Настройка** щелкните **установки непосредственно на этом компьютере**. Это действие загружает установочный пакет шлюза hello hello, устанавливает, настраивает и регистрирует hello шлюз на компьютере hello.  

   > [!NOTE]
   > Используйте Internet Explorer или другой веб-браузер, совместимый с Microsoft ClickOnce.
   >
   > При использовании Chrome go toohello [Chrome веб-хранилище](https://chrome.google.com/webstore/)поиска с ключевым словом «ClickOnce», выбрав один из модулей ClickOnce hello и установить его.
   >
   > Здравствуйте же для Firefox (установка надстройки). Нажмите кнопку **открыть меню** кнопку на панели инструментов hello (**три горизонтальные линии** в правом верхнем углу hello), нажмите кнопку **надстройки**, поиска с ключевым словом «ClickOnce», выберите один из hello Расширения ClickOnce и установить его.    
   >
   >

    ![Шлюз — страница "Настройка"](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    Таким образом является наиболее простым способом (одним щелчком) toodownload hello, установить, настроить и зарегистрировать шлюз hello один один шаг. Вы увидите hello **диспетчера конфигурации шлюза управления данными Майкрософт** на вашем компьютере установлено приложение. Можно также найти hello исполняемый **ConfigManager.exe** в папке hello: **C:\Program Files\Microsoft данных управления Gateway\2.0\Shared**.

    Можно также загрузить и установить шлюз вручную, используя hello ссылки на этой странице и зарегистрируйте его с помощью ключа hello показано hello **новый ключ** текстовое поле.

    В разделе [шлюз управления данными](data-factory-data-management-gateway.md) статьи для всех hello сведения о шлюзе hello.

   > [!NOTE]
   > Необходимо иметь права администратора на локальном компьютере tooinstall hello и успешно настроить hello шлюз управления данными. Можно добавить дополнительных пользователей toohello **пользователи шлюза управления данными** локальной группе Windows. Hello члены этой группы могут использовать hello диспетчера конфигурации шлюза управления данными средства tooconfigure hello шлюза.
   >
   >
5. Подождите несколько минут или подождать, пока вы видите hello следующие сообщения уведомления:

    ![Установка шлюза успешно выполнена](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. Запустите на компьютере приложение **Диспетчер конфигурации шлюза управления данными**. В hello **поиска** введите **шлюз управления данными** tooaccess этом служебной программы. Можно также найти hello исполняемый **ConfigManager.exe** в папке hello: **C:\Program Files\Microsoft данных управления Gateway\2.0\Shared**

    ![Диспетчер конфигурации шлюза](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. Убедитесь, что отображается сообщение `adftutorialgateway is connected toohello cloud service`. Здравствуйте, строка hello нижней отображает состояния **подключен toohello облачной службы** вместе с **зеленый**.

    На hello **Главная** вкладку, можно также сделать hello следующие операции:

   * **Зарегистрировать** шлюз с помощью ключа из hello портал Azure с помощью кнопки регистрации hello.
   * **Остановить** hello служба шлюза управления данными узла выполняется на компьютере шлюза.
   * **Расписание обновления** toobe установлен в определенное время дня hello.
   * Просмотр момент шлюза hello **последнего обновления**.
   * Укажите время, можно установить шлюз toohello обновления.
8. Переключение toohello **параметры** вкладку hello сертификат, указанный в hello **сертификат** раздел является используется tooencrypt и расшифровки учетных данных для хранилища данных в локальной среде hello, укажите на портале hello. (необязательно) Нажмите кнопку **изменений** toouse собственный сертификат вместо него. По умолчанию hello шлюз использует сертификат hello, автоматически создаваемое hello служба фабрики данных.

    ![Конфигурация сертификата шлюза](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    Вы также можете выполнить следующие действия с hello hello **параметры** вкладки:

   * Просмотр или экспорт hello сертификата, используемого шлюза hello.
   * Изменить конечную точку HTTPS hello, используемый шлюзом hello.    
   * Задайте toobe прокси-сервера HTTP, используемый шлюзом hello.     
9. (необязательно) Переключение toohello **диагностики** проверьте hello **включите подробное ведение журнала** Если tooenable требуется расширенное ведение журнала, tootroubleshoot можно использовать любые проблемы с hello шлюза. Hello сведения о ведении журнала можно найти в **средство просмотра событий** под **журналы приложений и служб** -> **шлюз управления данными** узла.

    ![Вкладка «Диагностика»](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    Можно также выполнить следующие действия в hello hello **диагностики** вкладки:

   * Используйте **проверить подключение** раздел tooan на локальному источнику данных с помощью шлюза hello.
   * Нажмите кнопку **Просмотр журналов** toosee hello шлюз управления данными журнала в окне просмотра событий.
   * Нажмите кнопку **отправить журналы** tooupload ZIP-файл с журналами последние семь дней tooMicrosoft toofacilitate устранения неполадок проблем.
10. На hello **диагностики** hello на вкладке **проверить подключение** выберите **SqlServer** для типа hello hello данных хранения, введите имя сервера базы данных hello, имя hello Здравствуйте, базы данных, укажите тип проверки подлинности, введите имя пользователя и пароль и нажмите кнопку **тест** tootest ли шлюз hello может подключаться toohello базы данных.
11. Коммутатор toohello веб-браузер и в hello **портал Azure**, нажмите кнопку **ОК** на hello **Настройка** страницы и затем на hello **шлюз данных** страница.
12. Вы увидите **adftutorialgateway** под **шлюзы данных** в древовидном представлении hello слева hello.  Если щелкнуть его, вы увидите hello связанную JSON.

## <a name="create-linked-services"></a>Создание связанных служб
На этом этапе вы создадите две связанные службы: **AzureStorageLinkedService** и **SqlServerLinkedService**. Hello **SqlServerLinkedService** локальной базы данных SQL Server и hello ссылок **AzureStorageLinkedService** фабрикой данных Azure BLOB-объекта хранилища toohello связывает связанной службы. Далее в этом руководстве, копирующего данные из хранилища BLOB-объектов Azure toohello базы данных SQL Server hello локальной создать конвейер.

#### <a name="add-a-linked-service-tooan-on-premises-sql-server-database"></a>Добавить tooan связанная служба локальной базы данных SQL Server
1. В hello **редактор фабрики данных**, нажмите кнопку **новое хранилище данных** на hello и отметьте **SQL Server**.

   ![Создать связанную службу SQL Server](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. В hello **редактор JSON** на правом hello, hello следующие действия:

   1. Для hello **gatewayName**, укажите **adftutorialgateway**.    
   2. В hello **connectionString**, hello следующие действия:    

      1. Для **servername**, введите имя hello hello сервера, на котором размещена база данных SQL Server hello.
      2. Для **databasename**, введите имя hello hello базы данных.
      3. Нажмите кнопку **Encrypt** на инструментов «hello». Вы видите приложение hello диспетчер учетных данных.

         ![Приложение "Диспетчер учетных данных"](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. В hello **задать учетные данные** диалоговое окно, укажите тип проверки подлинности, имя пользователя и пароль и нажмите кнопку **ОК**. При успешном выполнении подключения hello hello зашифрованные учетные данные хранятся в hello JSON и закрывает диалоговое окно «hello».
      5. Закрытие вкладки браузера пустой hello, запустить диалоговое окно «hello», если оно не закрывается автоматически и вернуть toohello вкладка с hello портал Azure.

         На компьютере шлюза hello, эти учетные данные являются **зашифрованные** с помощью сертификата, который hello фабрики данных является владельцем службы. Toouse hello сертификат, связанный с hello шлюз управления данными, вместо этого, в статье [задать учетные данные безопасно](#set-credentials-and-security).    
   3. Нажмите кнопку **развернуть** на панели toodeploy hello связанной службы SQL Server hello команд. Вы увидите службы hello связаны в представлении дерева hello.

      ![Связанной службы SQL Server в представлении дерева hello](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a>Добавление связанной службы для учетной записи хранения Azure
1. В hello **редактор фабрики данных**, нажмите кнопку **новое хранилище данных** hello панели команд и нажмите кнопку **хранилища Azure**.
2. Введите имя учетной записи хранилища Azure hello для hello **имя учетной записи**.
3. Введите ключ hello для вашей учетной записи хранилища Azure для hello **ключ учетной записи**.
4. Нажмите кнопку **развернуть** toodeploy hello **AzureStorageLinkedService**.

## <a name="create-datasets"></a>Создание наборов данных
На этом шаге создания входных и выходных данных наборы данных, которые представляют входные и выходные данные для операции копирования hello (база данных SQL Server в локальной среде = > хранилище больших двоичных объектов). Прежде чем создавать наборы данных, hello следующие шаги (Подробное описание действий следует за списком hello):

* Создать таблицу с именем **emp** в hello был добавлен в качестве фабрики данных toohello связанной службы базы данных SQL Server и вставить несколько записей в таблицу hello.
* Создание контейнера BLOB-объекта с именем **adftutorial** в hello Azure BLOB-объектов учетной записи хранилища, которые были добавлены в качестве фабрики данных toohello связанной службы.

### <a name="prepare-on-premises-sql-server-for-hello-tutorial"></a>Подготовка локального SQL Server для учебника hello
1. В базе данных hello, указанной для hello локального SQL Server связанная служба (**SqlServerLinkedService**), используйте следующие hello toocreate скрипт SQL hello **emp** таблицы в базе данных hello.

    ```SQL   
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
        CONSTRAINT PK_emp PRIMARY KEY (ID)
    )
    GO
    ```
2. Некоторые образцы вставьте в таблицу hello:

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a>Создание входного набора данных

1. В hello **редактор фабрики данных**, нажмите кнопку **... Дополнительные**, нажмите кнопку **новый набор данных** hello панели команд и нажмите кнопку **таблицы SQL Server**.
2. Замените hello JSON в правой области hello hello следующий текст:

    ```JSON   
    {        
        "name": "EmpOnPremSQLTable",
        "properties": {
            "type": "SqlServerTable",
            "linkedServiceName": "SqlServerLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }     
    ```     
   Обратите внимание hello после точки.

   * **Тип** задано слишком**SqlServerTable**.
   * **tableName** задано слишком**emp**.
   * **linkedServiceName** задано слишком**SqlServerLinkedService** (эта связанная служба был создан ранее в этом руководстве.).
   * Для входного набора данных, которая не создается другой конвейера в фабрике данных Azure, необходимо задать **внешних** слишком**true**. Он обозначает hello входные данные — производимых внешних toohello служба фабрики данных Azure. Можно указать любой политики внешних данных, с помощью hello **externalData** элемент в hello **политики** раздела.    

   Дополнительные сведения о свойствах файлов JSON см. в статье [Перемещение данных в базу данных SQL Server и обратно на локальных компьютерах и виртуальных машинах Azure IaaS с помощью фабрики данных Azure](data-factory-sqlserver-connector.md).
3. Нажмите кнопку **развернуть** на панели наборов данных hello toodeploy hello команд.  

### <a name="create-output-dataset"></a>Создание выходного набора данных

1. В hello **редактор фабрики данных**, нажмите кнопку **новый набор данных** hello панели команд и нажмите кнопку **хранилища больших двоичных объектов Azure**.
2. Замените hello JSON в правой области hello hello следующий текст:

    ```JSON   
    {
        "name": "OutputBlobTable",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "adftutorial/outfromonpremdf",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```   
   Обратите внимание hello после точки.

   * **Тип** задано слишком**AzureBlob**.
   * **linkedServiceName** задано слишком**AzureStorageLinkedService** (на шаге 2 был создан эта связанная служба).
   * **folderPath** задано слишком**adftutorial/outfromonpremdf** где outfromonpremdf — папка hello в контейнере adftutorial hello. Создать hello **adftutorial** контейнера, если он еще не существует.
   * Hello **доступности** задано слишком**каждый час** (**частоты** значение слишком**час** и **интервал** значение слишком **1**).  Hello служба фабрики данных приводит к возникновению ошибки срез данных вывода каждый час в hello **emp** таблицы в hello базы данных SQL Azure.

   Если вы не укажете **fileName** для **выходной таблицы**, hello созданные файлы в hello **folderPath** именуются в кодировке hello: данные.<Guid>. txt (например:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).

   tooset **folderPath** и **fileName** динамически на основании hello **SliceStart** время, используйте свойство partitionedBy hello. В следующем примере hello folderPath использует год, месяц и день из hello SliceStart (время начала среза hello обрабатывается) и имя файла использует час из hello SliceStart. Например, если срез создается для 2014-10-20T08:00:00, hello имя папки имеет значение toowikidatagateway/wikisampledataout/2014-10-20 и hello fileName является too08.csv.

    ```JSON
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy":
    [

        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
    ],
    ```

    Дополнительные сведения о свойствах файлов JSON см. в статье [Перемещение данных в базу данных SQL Server и обратно на локальных компьютерах и виртуальных машинах Azure IaaS с помощью фабрики данных Azure](data-factory-azure-blob-connector.md).
3. Нажмите кнопку **развернуть** на панели наборов данных hello toodeploy hello команд. Подтвердите, что вы видите оба набора данных hello в представлении дерева hello.  

## <a name="create-pipeline"></a>Создание конвейера
На этом шаге вы создадите **конвейер** одним **действием копирования**, для выполнения которого **EmpOnPremSQLTable** будет использоваться как входные данные, а **OutputBlobTable** — как выходные данные.

1. В редакторе фабрики данных нажмите кнопку **... Дополнительно** и **Новый конвейер**.
2. Замените hello JSON в правой области hello hello следующий текст:    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL tooAzure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server tooblob",
             "type": "Copy",
             "inputs": [
               {
                 "name": "EmpOnPremSQLTable"
               }
             ],
             "outputs": [
               {
                 "name": "OutputBlobTable"
               }
             ],
             "typeProperties": {
               "source": {
                 "type": "SqlSource",
                 "sqlReaderQuery": "select * from emp"
               },
               "sink": {
                 "type": "BlobSink"
               }
             },
             "Policy": {
               "concurrency": 1,
               "executionPriorityOrder": "NewestFirst",
               "style": "StartOfInterval",
               "retry": 0,
               "timeout": "01:00:00"
             }
           }
         ],
         "start": "2016-07-05T00:00:00Z",
         "end": "2016-07-06T00:00:00Z",
         "isPaused": false
       }
     }
    ```   
   > [!IMPORTANT]
   > Замените значение hello hello **запустить** свойство с hello текущего дня и **окончания** значение с hello следующего дня.
   >
   >

   Обратите внимание hello после точки.

   * В разделе "действия" hello, есть только у действия которого **тип** задано слишком**копирования**.
   * **Входные данные** для hello действия установлено слишком**EmpOnPremSQLTable** и **вывода** для hello действия установлено слишком**OutputBlobTable**.
   * В hello **typeProperties** разделе **SqlSource** указывается как hello **тип источника** и ** BlobSink ** указывается как hello **типприемника**.
   * SQL-запрос `select * from emp` указан для hello **sqlReaderQuery** свойство **SqlSource**.

   Даты начала и окончания должны быть в [формате ISO](http://en.wikipedia.org/wiki/ISO_8601). Например, 2014-10-14T16:32:41Z. Hello **окончания** времени является необязательным, но мы используем в этом учебнике.

   Если не указать значение для hello **окончания** свойство, оно вычисляется как «**start + 48 часов**». конвейер hello toorun неопределенно долгое время, укажите **9/9/9999** как значение hello для hello **окончания** свойство.

   Вы определяете hello продолжительность времени, в которой hello обрабатываются срезы данных основании hello **доступности** свойства, которые были определены для каждого набора данных фабрики данных Azure.

   В примере hello нет 24 срезы данных, как каждый срез данных создается каждый час.        
3. Нажмите кнопку **развернуть** на панели наборов данных hello toodeploy hello команд (таблица представляет собой прямоугольный набор данных). Подтвердите конвейера hello отображается в представлении дерева hello в **конвейеры** узла.  
4. Теперь щелкните **X** дважды tooclose hello страницы tooget назад toohello **фабрики данных** страница hello **ADFTutorialOnPremDF**.

**Поздравляем!** Успешно создана фабрикой данных Azure, связанные службы, наборы данных и конвейера и запланированных hello конвейера.

#### <a name="view-hello-data-factory-in-a-diagram-view"></a>Фабрика данных hello представления в представлении диаграммы
1. В hello **портал Azure**, нажмите кнопку **схема** плитки на домашней странице приветствия для hello **ADFTutorialOnPremDF** фабрики данных. :

    ![Ссылка на схему](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. Вы увидите примерно toohello hello диаграммы после изображения:

    ![Представление схемы](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    Увеличить масштаб, уменьшить масштаб масштаба too100% toofit масштаба, автоматически позиции конвейеры и наборы данных и отображения сведений журнала обращений и преобразований (выделяет восходящие и нисходящие для выбранных элементов).  Его можно дважды щелкнуть свойства toosee объекта (набор данных ввода вывода или конвейера).

## <a name="monitor-pipeline"></a>Отслеживание конвейера
На этом шаге используется hello Azure портала toomonitor, происходящем в фабрикой данных Azure. Можно также использовать командлеты PowerShell toomonitor-наборы данных и конвейеры. Дополнительные сведения о мониторинге см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими](data-factory-monitor-manage-pipelines.md).

1. В диаграмме hello, дважды щелкните **EmpOnPremSQLTable**.  

    ![Срезы EmpOnPremSQLTable](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. Обратите внимание, что все данные hello срезы копии находятся в **готовности** состоянии, так как длительность конвейера hello (время начала время tooend) находится в прошлом hello. Можно также из-за вставки данных hello в базе данных SQL Server hello и есть ли все время hello. Убедитесь, что нет срезов показываться в hello **фрагменты проблема** раздела внизу hello. Щелкните все срезы hello tooview **разделе более** hello нижней части списка hello фрагментов.
3. Теперь в hello **наборы данных** щелкните **OutputBlobTable**.

    ![Срезы OputputBlobTable](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. Щелкните любой сегмент данных из списка hello и вы увидите hello **срез данных** страницы. Вы увидите, что действие выполняется срез hello. Как правило, в этом разделе отображается только одно действие.  

    ![Колонка среза данных](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    Если срез hello не hello **готовности** состояние, можно увидеть hello восходящие срезы, которые еще не готовы и блокируют hello текущего среза выполнения в hello **восходящие срезы, которые не готовы** списка.
5. Нажмите кнопку hello **при выполнении действия** из списка hello hello нижней toosee **сведения о выполнении действия**.

   ![Страница "Подробности о выполнении операции"](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   Вы увидите сведения, например пропускную способность, продолжительность и шлюза hello использовать tootransfer hello данных.
6. Нажмите кнопку **X** tooclose все Здравствуйте страниц, пока не будет
7. вернуться к домашней странице toohello hello **ADFTutorialOnPremDF**.
8. (Необязательно.) Щелкните **Конвейеры**, а затем — **ADFTutorialOnPremDF** и просмотрите параметры входных таблиц (**Использовано**) или выходных наборов данных (**Выполнено**).
9. Использовать инструменты, такие как [обозреватель хранилищ Microsoft](http://storageexplorer.com/) tooverify, что большой двоичный объект или файл создается за каждый час.

   ![обозреватель хранилищ Azure](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a>Дальнейшие действия
* В разделе [шлюз управления данными](data-factory-data-management-gateway.md) статьи для всех hello сведения о hello шлюз управления данными.
* В разделе [копирования данных из больших двоичных объектов Azure tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn о как toouse действие копирования toomove данных из источника данных в хранилище tooa приемник данных.
