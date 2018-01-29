---
title: "Преобразование данных с помощью Hive в виртуальной сети Azure | Документация Майкрософт"
description: "В этом руководстве представлены пошаговые инструкции по преобразованию данных с использованием действия Hive в фабрике данных Azure."
services: data-factory
documentationcenter: 
author: shengcmsft
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/04/2018
ms.author: shengc
ms.openlocfilehash: 4b8f7a66f220b57ac914a9f5475c680679b8bf03
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/23/2018
---
# <a name="transform-data-in-azure-virtual-network-using-hive-activity-in-azure-data-factory"></a>Преобразование данных в виртуальной сети Azure с помощью действия Hive в фабрике данных Azure
В этом руководстве с помощью портала Azure вы создадите конвейер фабрики данных, который преобразует данные, используя действие Hive в кластере HDInsight, находящемся в виртуальной сети Azure (VNet). В этом руководстве вы выполните следующие шаги:

> [!div class="checklist"]
> * Создадите фабрику данных. 
> * Создание локальной среды выполнения интеграции
> * Создание связанных службы хранилища Azure и службы Azure HDInsight.
> * Создание конвейера с действием Hive.
> * Активация выполнения конвейера.
> * Выполнили мониторинг конвейера. 
> * Проверка выходных данных

> [!NOTE]
> Эта статья относится к версии 2 фабрики данных, которая в настоящее время доступна в предварительной версии. Если вы используете общедоступную версию 1 службы фабрики данных, ознакомьтесь с [документацией по фабрике данных версии 1](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Если у вас еще нет подписки Azure, создайте [бесплатную](https://azure.microsoft.com/free/) учетную запись Azure, прежде чем начинать работу.

## <a name="prerequisites"></a>предварительным требованиям
- **Учетная запись хранения Azure.** Создайте скрипт Hive и отправьте его в хранилище Azure. Выходные данные скрипта Hive хранятся в этой учетной записи хранения. В этом примере кластер HDInsight использует эту учетную запись хранения Azure в качестве основного хранилища. 
- **Виртуальная сеть Azure.** Если у вас нет виртуальной сети Azure, создайте ее, выполнив [эти инструкции](../virtual-network/virtual-network-get-started-vnet-subnet.md). В этом примере HDInsight находится в виртуальной сети Azure. Ниже приведен образец конфигурации виртуальной сети Azure. 

    ![Создание виртуальной сети](media/tutorial-transform-data-using-hive-in-vnet-portal/create-virtual-network.png)
- **Кластер HDInsight.** Создайте кластер HDInsight и присоедините его к виртуальной сети, созданной на предыдущем шаге, следуя указаниям в статье [Расширение возможностей HDInsight с помощью виртуальной сети Azure](../hdinsight/hdinsight-extend-hadoop-virtual-network.md). Ниже приведен образец конфигурации HDInsight в виртуальной сети. 

    ![HDInsight в виртуальной сети](media/tutorial-transform-data-using-hive-in-vnet-portal/hdinsight-virtual-network-settings.png)
- **Azure PowerShell**. Следуйте инструкциям по [установке и настройке Azure PowerShell](/powershell/azure/install-azurerm-ps).
- **Виртуальная машина**. Создайте виртуальную машину Azure и присоедините ее к той же виртуальной сети, которая содержит кластер HDInsight. Дополнительные сведения см. в разделе [Создание виртуальных машин](../virtual-network/virtual-network-get-started-vnet-subnet.md#create-vms). 

### <a name="upload-hive-script-to-your-blob-storage-account"></a>Отправка скрипта Hive в вашу учетную запись хранилища BLOB-объектов

1. Создайте файл Hive SQL с именем **hivescript.hql** со следующим содержимым:

   ```sql
   DROP TABLE IF EXISTS HiveSampleOut; 
   CREATE EXTERNAL TABLE HiveSampleOut (clientid string, market string, devicemodel string, state string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' 
   STORED AS TEXTFILE LOCATION '${hiveconf:Output}';

   INSERT OVERWRITE TABLE HiveSampleOut
   Select 
       clientid,
       market,
       devicemodel,
       state
   FROM hivesampletable
   ```
2. В хранилище BLOB-объектов Azure создайте контейнер с именем **adftutorial**, если он не существует.
3. Создайте папку с именем **hivescripts**.
4. Отправьте файл **hivescript.hql** во вложенную папку **hivescripts**.

## <a name="create-a-data-factory"></a>Создание фабрики данных
1. Войдите на [портал Azure](https://portal.azure.com/).    
2. В меню слева щелкните **Создать**, выберите **Данные+аналитика** и щелкните **Фабрика данных**. 
   
   ![Создать -> Фабрика данных](./media/tutorial-transform-data-using-hive-in-vnet-portal/new-data-factory-menu.png)
3. На странице **Новая фабрика данных** введите **ADFTutorialHiveFactory** в поле **Имя**. 
      
     ![Страница "Новая фабрика данных"](./media/tutorial-transform-data-using-hive-in-vnet-portal/new-azure-data-factory.png)
 
   Имя фабрики данных Azure должно быть **глобально уникальным**. Если вы получите указанную ниже ошибку, введите другое имя фабрики данных (например, ваше_имя_MyAzureSsisDataFactory) и попробуйте создать фабрику данных снова. Ознакомьтесь со статьей [Фабрика данных Azure — правила именования](naming-rules.md), чтобы узнать правила именования для артефактов службы "Фабрика данных".
  
       `Data factory name “MyAzureSsisDataFactory” is not available`
3. Выберите **подписку** Azure, в рамках которой вы хотите создать фабрику данных. 
4. Для **группы ресурсов** выполните одно из следующих действий.
     
      - Выберите **Использовать существующую**и укажите существующую группу ресурсов в раскрывающемся списке. 
      - Выберите **Создать новую**и укажите имя группы ресурсов.   
         
      Сведения о группах ресурсов см. в статье, где описывается [использование групп ресурсов для управления ресурсами Azure](../azure-resource-manager/resource-group-overview.md).  
4. Выберите **V2 (Preview)** (V2 (предварительная версия)) для **версии**.
5. Укажите **расположение** фабрики данных. В списке отображаются только те расположения, в которых можно создать фабрики данных.
6. Кроме того, установите флажок **Закрепить на панели мониторинга**.     
7. Нажмите кнопку **Создать**.
8. На панели мониторинга вы увидите приведенный ниже элемент с состоянием **Deploying data factory** (Развертывание фабрики данных). 

    ![Элемент Deploying data factory (Развертывание фабрики данных)](media/tutorial-transform-data-using-hive-in-vnet-portal/deploying-data-factory.png)
9. Когда завершится создание, откроется страница **Фабрика данных**, как показано на рисунке ниже.
   
   ![Домашняя страница фабрики данных](./media/tutorial-transform-data-using-hive-in-vnet-portal/data-factory-home-page.png)
10. Щелкните **Создание и мониторинг**, чтобы открыть на отдельной вкладке пользовательский интерфейс фабрики данных.
11. На странице **начала работы** перейдите на вкладку **Изменить** на панели слева, как показано на следующем рисунке: 

   ![Вкладка редактирования](./media/tutorial-transform-data-using-hive-in-vnet-portal/get-started-page.png)

## <a name="create-a-self-hosted-integration-runtime"></a>Создание локальной среды выполнения интеграции
Поскольку кластер Hadoop находится в виртуальной сети, локальную среду выполнения интеграции (IR) следует устанавливать в той же виртуальной сети. В этом разделе вы создадите виртуальную машину, присоедините ее к этой же виртуальной сети и установите на ней локальную среду выполнения интеграции. Локальная среда IR позволяет службе фабрики данных передавать запросы на обработку службе вычислений (например, HDInsight) в пределах виртуальной сети. Она также позволяет перемещать данные в пределах виртуальной сети из Azure в хранилища данных и наоборот. Локальная среда IR используется в том случае, когда хранилище данных или вычислительный ресурс находятся в той же локальной среде. 

1. В пользовательском интерфейсе фабрики данных Azure щелкните **Подключения** в нижней части окна, перейдите на вкладку **Integration Runtimes** (Среды выполнения интеграции) и нажмите кнопку **+ Создать** на панели инструментов. 

   ![Меню создания среды IR](./media/tutorial-transform-data-using-hive-in-vnet-portal/new-integration-runtime-menu.png)
2. В окне **Integration Runtime Setup** (Настройка среды выполнения интеграции) выберите вариант **Perform data movement and dispatch activities to external computes** (Выполнить перемещение данных и передать действия на внешние вычислительные ресурсы), затем щелкните **Next** (Далее). 

   ![Выбор варианта Perform data movement and dispatch activities to external computes (Выполнить перемещение данных и передать действия на внешние вычислительные ресурсы)](./media/tutorial-transform-data-using-hive-in-vnet-portal/select-perform-data-movement-compute-option.png)
3. Выберите **Private Network** (Частная сеть) и щелкните **Next** (Далее).
    
   ![Выбор частной сети](./media/tutorial-transform-data-using-hive-in-vnet-portal/select-private-network.png)
4. Введите **MySelfHostedIR** для параметра **Name** (Имя) и щелкните **Next** (Далее). 

   ![Ввод имени среды IR](./media/tutorial-transform-data-using-hive-in-vnet-portal/integration-runtime-name.png) 
5. Скопируйте **ключ аутентификации** для среды IR, нажав кнопку Copy (Копировать), и сохраните этот ключ. Оставьте это окно открытым. Ключ вам потребуется для регистрации среды IR, установленной на виртуальной машине. 

   ![Копирование ключа аутентификации](./media/tutorial-transform-data-using-hive-in-vnet-portal/copy-key.png)

### <a name="install-ir-on-a-virtual-machine"></a>Установка среды IR на виртуальной машине

1. На виртуальной машине Azure скачайте [локальную среду выполнения интеграции](https://www.microsoft.com/download/details.aspx?id=39717). Используйте **ключ аутентификации**, полученный на предыдущем шаге, чтобы вручную зарегистрировать локальную среду IR. 

    ![Регистрация среды выполнения интеграции](media/tutorial-transform-data-using-hive-in-vnet-portal/register-integration-runtime.png)

2. Когда локальная среда IR будет успешно зарегистрирована, вы увидите следующее сообщение. 
   
    ![Успешно зарегистрирована](media/tutorial-transform-data-using-hive-in-vnet-portal/registered-successfully.png)
3. Щелкните **Запустить Configuration Manager**. Когда узел будет подключен к облачной службе, отобразится следующая страница: 
   
    ![Узел подключен](media/tutorial-transform-data-using-hive-in-vnet-portal/node-is-connected.png)

### <a name="self-hosted-ir-in-the-azure-data-factory-ui"></a>Локальная среда IR в пользовательском интерфейсе фабрики данных Azure

1. В **пользовательском интерфейсе фабрики данных Azure** вы можете найти имя и текущее состояние локальной виртуальной машины.

   ![Существующие локальные узлы](./media/tutorial-transform-data-using-hive-in-vnet-portal/existing-self-hosted-nodes.png)
2. Щелкните **Finish** (Готово), чтобы закрыть окно **Integration Runtime Setup** (Настройка среды выполнения интеграции). Теперь вы увидите созданную локальную среду в списке сред IR.

   ![Список, в котором указана локальная среда IR](./media/tutorial-transform-data-using-hive-in-vnet-portal/self-hosted-ir-in-list.png)


## <a name="create-linked-services"></a>Создание связанных служб

Создайте и разверните две связанные службы в этом разделе:
- **Связанную службу хранилища Azure**, которая связывает учетную запись хранения Azure с фабрикой данных. Это основное хранилище, которое использует кластер HDInsight. В нашем примере эта же учетная запись хранения Azure пригодится еще для хранения скрипта Hive и его выходных данных.
- **Связанная служба HDInsight**. Фабрика данных Azure отправляет скрипт Hive в этот кластер HDInsight для выполнения.

### <a name="create-azure-storage-linked-service"></a>Создание связанной службы хранения Azure

1. Перейдите на вкладку **Связанные службы** и щелкните **Создать**.

   ![Кнопка создания связанной службы](./media/tutorial-transform-data-using-hive-in-vnet-portal/new-linked-service.png)    
2. В окне **New Linked Service** (Новая связанная служба) выберите **хранилище BLOB-объектов Azure** и щелкните **Continue** (Продолжить). 

   ![Выбор хранилища BLOB-объектов Azure](./media/tutorial-transform-data-using-hive-in-vnet-portal/select-azure-storage.png)
3. В окне **New Linked Service** (Новая связанная служба) выполните следующие действия:

    1. Введите **AzureStorageLinkedService** в поле **имени**.
    2. Выберите **MySelfHostedIR** для параметра **Connect via integration runtime** (Подключиться через среду выполнения интеграции).
    3. В поле **Storage account name** (Имя учетной записи хранения) выберите нужную учетную запись хранения. 
    4. Щелкните **Test connection** (Проверить подключение), чтобы проверить подключение к учетной записи хранения.
    5. Выберите команду **Сохранить**.
   
        ![Выбор учетной записи хранилища BLOB-объектов Azure](./media/tutorial-transform-data-using-hive-in-vnet-portal/specify-azure-storage-account.png)

### <a name="create-hdinsight-linked-service"></a>Создание связанной службы HDInsight

1. Снова щелкните **Создать**, чтобы создать еще одну связанную службу. 
    
   ![Кнопка создания связанной службы](./media/tutorial-transform-data-using-hive-in-vnet-portal/new-linked-service.png)    
2. Перейдите на вкладку **Compute** (Вычисления), выберите **Azure HDInsight** и щелкните **Continue** (Продолжить).

    ![Выбор Azure HDInsight](./media/tutorial-transform-data-using-hive-in-vnet-portal/select-hdinsight.png)
3. В окне **New Linked Service** (Новая связанная служба) выполните следующие действия:

    1. Введите **AzureHDInsightLinkedService** в поле **имени**.
    2. Выберите **Bring your own HDInsight** (Подключить свой кластер HDInsight). 
    3. Выберите кластер HDInsight в поле **HDI cluster** (Кластер HDI). 
    4. Введите **имя пользователя** для кластера HDInsight.
    5. Введите **пароль** для этого пользователя. 
    
        ![Настройки Azure HDInsight](./media/tutorial-transform-data-using-hive-in-vnet-portal/specify-azure-hdinsight.png)

В этой статье предполагается, что у вас есть доступ к кластеру через Интернет. Например, что вы можете подключиться к кластеру по адресу `https://clustername.azurehdinsight.net`. Этот адрес использует общедоступный шлюз, который будет недоступен, если вы использовали группы безопасности сети или определяемые пользователем маршруты для ограничения доступа через Интернет. Чтобы фабрика данных могла отправлять задания в кластер HDInsight в виртуальной сети Azure, необходимо настроить виртуальную сеть Azure таким образом, чтобы URL-адрес был разрешен в частный IP-адрес шлюза, используемого HDInsight.

1. На портале Azure откройте виртуальную сеть, в которой находится HDInsight. Откройте сетевой интерфейс, используя имя, которое начинается с `nic-gateway-0`. Запишите частный IP-адрес. Например, 10.6.0.15. 
2. Если ваша виртуальная сеть Azure имеет DNS-сервер, обновите запись DNS, чтобы URL-адрес кластера HDInsight `https://<clustername>.azurehdinsight.net` можно было разрешить в `10.6.0.15`. Если у вас нет DNS-сервера в виртуальной сети Azure, вы можете применить временное решение. Отредактируйте файлы hosts (C:\Windows\System32\drivers\etc) на всех виртуальных машинах, зарегистрированных в качестве узлов локальной среды IR, добавив в них следующую запись: 

    `10.6.0.15 myHDIClusterName.azurehdinsight.net`

## <a name="create-a-pipeline"></a>Создание конвейера 
На этом этапе создайте конвейер с действием Hive. Это действие выполняет скрипт Hive для получения данных из примера таблицы и сохранения их по пути, который вы определили.

Обратите внимание на следующие моменты.

- **scriptPath** указывает путь к скрипту Hive в учетной записи хранения Azure, используемой для MyStorageLinkedService. Путь следует вводить с учетом регистра.
- **Выходные данные** выступают в качестве аргумента, используемого в скрипте Hive. Используйте формат `wasb://<Container>@<StorageAccount>.blob.core.windows.net/outputfolder/`, который должен указывать на существующую папку в службе хранилища Azure. Путь следует вводить с учетом регистра. 

1. В пользовательском интерфейсе фабрики данных щелкните знак **+** (плюс) на панели слева и выберите вариант **Конвейер**. 

    ![Меню создания конвейера](./media/tutorial-transform-data-using-hive-in-vnet-portal/new-pipeline-menu.png)
2. На панели инструментов **Действия** разверните **HDInsight** и перетащите действие **Hive** в область конструктора конвейера. 

    ![Перетаскивание действия Hive](./media/tutorial-transform-data-using-hive-in-vnet-portal/drag-drop-hive-activity.png)
3. В окне свойств перейдите на вкладку **HDI Cluster** (Кластер HDI) и выберите **AzureHDInsightLinkedService** в качестве **связанной службы HDInsight**.

    ![Выбор связанной службы HDInsight](./media/tutorial-transform-data-using-hive-in-vnet-portal/select-hdinsight-linked-service.png)
4. Переключитесь на вкладку **Scripts** (Скрипты) и выполните следующие действия: 

    1. Введите **AzureStorageLinkedService** в качестве **имени связанной службы**. 
    2. В области **File Path** (Путь к файлу) щелкните **Browse Storage** (Поиск в хранилище). 
 
        ![Поиск в хранилище](./media/tutorial-transform-data-using-hive-in-vnet-portal/browse-storage-hive-script.png)
    3. В окне **Choose a file or folder** (Выберите файл или папку) перейдите к папке **hivescripts** контейнера **adftutorial**, выберите файл **hivescript.hql** и щелкните **Finish** (Готово).  
        
        ![Выбор файла или папки](./media/tutorial-transform-data-using-hive-in-vnet-portal/choose-file-folder.png) 
    4. Убедитесь, что в поле **File Path** (Путь к файлу) появилось значение **adftutorial/hivescripts/hivescript.hql**.

        ![Параметры скрипта](./media/tutorial-transform-data-using-hive-in-vnet-portal/confirm-hive-script-settings.png)
    5. На вкладке **Script** (Скрипт) разверните раздел **Advanced** (Дополнительно). 
    6. Щелкните действие **Auto-fill from script** (Заполнить автоматически из скрипта) в области **Parameters** (Параметры). 
    7. Введите значение для параметра **Output** (Вывод) в следующем формате: `wasb://<Blob Container>@<StorageAccount>.blob.core.windows.net/outputfolder/`. Например, `wasb://adftutorial@mystorageaccount.blob.core.windows.net/outputfolder/`.
 
        ![Аргументы сценария](./media/tutorial-transform-data-using-hive-in-vnet-portal/script-arguments.png)
1. Чтобы опубликовать артефакты в фабрике данных, щелкните **Опубликовать**.

    ![Опубликовать](./media/tutorial-transform-data-using-hive-in-vnet-portal/publish.png)

## <a name="trigger-a-pipeline-run"></a>Активация выполнения конвейера

1. Прежде всего проверьте работу конвейера, нажав кнопку **Проверить** на панели инструментов. Закройте окно **Pipeline Validation Output** (Выходные данные проверки конвейера) щелкнув **стрелку вправо (>>)**. 

    ![Проверка конвейера](./media/tutorial-transform-data-using-hive-in-vnet-portal/validate-pipeline.png) 
2. Чтобы активировать конвейер, щелкните "Триггер" на панели инструментов, а затем Trigger Now (Активировать сейчас). 

    ![Trigger Now (Активировать сейчас)](./media/tutorial-transform-data-using-hive-in-vnet-portal/trigger-now-menu.png)

## <a name="monitor-the-pipeline-run"></a>Выполнили мониторинг конвейера.

1. Перейдите на вкладку **Мониторинг** слева. Вы увидите, что запуск конвейера появится в списке **Pipeline Runs** (Запуски конвейера). 

    ![Мониторинг выполнений конвейера](./media/tutorial-transform-data-using-hive-in-vnet-portal/monitor-pipeline-runs.png)
2. Щелкните **Refresh** (Обновить), чтобы обновить этот список.
4. Чтобы просмотреть запуски действий, связанные с этим запуском конвейера, щелкните **View Activity Runs** (Просмотр запусков действий) в столбце **Действие**. Другие ссылки в столбце действий позволяют остановить и заново запустить конвейер. 

    ![Просмотр выполнений действий](./media/tutorial-transform-data-using-hive-in-vnet-portal/view-activity-runs-link.png)
5. Здесь вы видите сведения об одном выполнении действия, поскольку в конвейере типа **HDInsightHive** определено только одно действие. Чтобы вернуться к представлению запусков конвейера, щелкните ссылку **Pipelines** (Конвейеры) в верхней части окна.

    ![Выполнение действия](./media/tutorial-transform-data-using-hive-in-vnet-portal/view-activity-runs.png)
6. Убедитесь, что выходной файл появился в папке **outputfolder** конвейера **adftutorial**. 

    ![Выходной файл](./media/tutorial-transform-data-using-hive-in-vnet-portal/output-file.png)

## <a name="next-steps"></a>Дополнительная информация
В этом руководстве вы выполнили следующие шаги: 

> [!div class="checklist"]
> * Создадите фабрику данных. 
> * Создание локальной среды выполнения интеграции
> * Создание связанных службы хранилища Azure и службы Azure HDInsight.
> * Создание конвейера с действием Hive.
> * Активация выполнения конвейера.
> * Выполнили мониторинг конвейера. 
> * Проверка выходных данных

Перейдите к следующему руководству, чтобы узнать о преобразовании данных с помощью кластера Spark в Azure:

> [!div class="nextstepaction"]
>[Branching and chaining activities in a Data Factory pipeline](tutorial-control-flow-portal.md) (Ветвление и создание цепного потока управления фабрики данных)



