---
title: "aaaLoad данных в хранилище данных SQL Azure — фабрики данных | Документы Microsoft"
description: "Этот учебник загружает данные в хранилище данных SQL Azure с помощью фабрики данных Azure и использует базы данных SQL Server в качестве источника данных hello."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 471871d3ee00ab34cc84bb63fbd13a323d14c2b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a>Загрузка данных в хранилище данных SQL с помощью фабрики данных

Можно использовать данные tooload фабрики данных Azure в хранилище данных SQL Azure из любого hello [поддерживается хранилищ данных источника](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats). Например, с помощью фабрики данных можно загрузить данные из базы данных SQL Azure или базы данных Oracle в хранилище данных SQL. Учебник, в этой статье показано, как tooload данных с сервера SQL в локальной базы данных в хранилище данных SQL.

**Примерное время**: учебником занимает около 10 – 15 минут toocomplete после hello предварительных условий.

## <a name="prerequisites"></a>Предварительные требования

- Требуется **базы данных SQL Server** с таблицами, содержащими данные hello toobe копируются toohello хранилище данных SQL.  

- **Хранилище данных SQL.** Если вы еще нет в хранилище данных, узнайте, как слишком[создать хранилище данных SQL Azure](sql-data-warehouse-get-started-provision.md).

- **Учетная запись хранения Azure.** Если у вас еще нет учетной записи хранилища, узнайте, как слишком[создать учетную запись хранилища](../storage/common/storage-create-storage-account.md). Для наилучшей производительности, найдите учетную запись хранилища hello и хранилища данных hello в hello же регионе Azure.

## <a name="configure-a-data-factory"></a>Настройка фабрики данных
1. Войдите в toohello [портал Azure][].
2. Найдите хранилищем данных и щелкните tooopen его.
3. В главной колонке hello щелкните **загрузки данных** > **фабрики данных Azure**.

    ![Запуск мастера загрузки данных](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. Если у вас фабрики данных в вашей подписке Azure, вы увидите **новую фабрику данных** диалоговое на отдельной вкладке браузера hello. Заполните hello запрошенных сведения и нажмите кнопку **создать**. После создания фабрики данных hello hello **новую фабрику данных** диалоговое окно закрывается, и вы видите hello **выберите фабрики данных** диалоговое окно.

    Если у вас есть один или несколько фабрик данных уже находится в hello подписки Azure, вы увидите hello **выберите фабрики данных** диалоговое окно. В этом диалоговом окне можно выбрать существующую фабрику данных или нажмите кнопку **создать новую фабрику данных** toocreate новый.

    ![Настройка фабрики данных](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. В hello **выберите фабрики данных** диалоговое окно, hello **загрузки данных** параметр выбран по умолчанию. Нажмите кнопку **Далее** toostart создание данных при загрузке задачи.

## <a name="configure-hello-data-factory-properties"></a>Настройка свойств фабрики данных hello
После создания фабрики данных hello следующим шагом является загрузка расписание tooconfigure hello данных.

1. В качестве **имени задачи** введите **DWLoadData-fromSQLServer**.
2. Использовать значение по умолчанию hello **запустить один раз сейчас** , нажмите кнопку **Далее**.

    ![Настройка расписания загрузки](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a>Настройка хранилища данных источника hello и шлюза
Теперь вы указываете фабрики данных о базе данных SQL Server в локальной среде hello tooload данные из которого нужно получить.

1. Выберите **SQL Server** из исходных данных поддерживается hello хранения каталога и нажмите кнопку **Далее**.

    ![Выбор источника SQL Server](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. Объект **базы данных SQL Server укажите hello локальной** откроется диалоговое окно. Здравствуйте, сначала **имя подключения** поле будет заполнено автоматически. Второе поле Hello запрашивает имя hello hello **шлюза**. При использовании существующей фабрики данных, уже содержит шлюз можно повторно использовать hello шлюза, выбрав необходимую из раскрывающегося списка hello. Нажмите кнопку hello **создать шлюз** связать toocreate шлюз управления данными.  

    > [!NOTE]
    > Если хранилище данных источника hello локально или на виртуальной машине Azure IaaS требуется шлюз управления данными. Шлюз связан с фабрикой данных по схеме "один к одному". Не может использоваться из другого фабрики данных, но он может использоваться несколько загрузки задач с hello данных же фабрику данных. Шлюз может быть хранилищ данных toomultiple tooconnect используется при выполнении задачи загрузки данных.
    >
    > Подробные сведения о шлюзе hello. в разделе [шлюз управления данными](../data-factory/data-factory-data-management-gateway.md) статьи.

3. Откроется диалоговое окно **Создание шлюза**. В качестве имени введите **GatewayForDWLoading** и нажмите кнопку **Создать**.

4. Откроется диалоговое окно **Настройка шлюза**. Нажмите кнопку **запуска экспресс-установку на этом компьютере** tooautomatically загрузить, установить и зарегистрировать шлюз управления данными на текущем компьютере. во всплывающем окне отображается ход выполнения Hello. Hello компьютера не удается подключиться toohello хранилища данных, можно вручную [скачать и установить шлюз hello](https://www.microsoft.com/download/details.aspx?id=39717) на компьютере, который можно подключить данные toohello хранения, а затем использовать ключа tooregister hello.
    > [!NOTE]
    > экспресс-установку Hello изначально работает с Microsoft Edge и Internet Explorer. При использовании Google Chrome сначала установите расширение ClickOnce hello из Chrome веб-хранилища.

    ![Запуск экспресс-установки](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. Дождитесь установки toocomplete hello шлюза. После hello шлюз успешно зарегистрирован и находится в оперативном режиме, hello всплывающее окно закрывается, а новый шлюз hello отображается в hello шлюза. Затем заполните hello остальные обязательные поля следующим образом, нажмите кнопку **Далее**.
    - **Имя сервера**: hello имя локального SQL Server.
    - **Имя базы**: имя базы данных сервера SQL.
    - **Учетными данными шифрования**: используется по умолчанию hello «веб-браузер».
    - **Тип проверки подлинности**: выберите тип проверки подлинности, вы используете hello.
    - **Имя пользователя** и **пароль**: Введите hello имя пользователя и пароль для пользователя, имеющего разрешение toocopy hello данных.

    ![Запуск экспресс-установки](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. Hello следующим шагом является toochoose hello таблиц, из которых данные toocopy hello. Можно фильтровать hello таблицы с помощью ключевых слов. И вы можете просмотреть схему таблицы и данным hello hello нижней панели. Выбрав нужные элементы, нажмите кнопку **Далее**.

    ![Выбор таблиц](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a>Настройка назначения «hello» в хранилище данных SQL

Теперь вы указываете фабрики данных о сведения о назначении hello.

1. Сведения о подключении к хранилищу данных SQL будут заполнены автоматически. Введите hello пароль для имени пользователя hello. а затем нажмите кнопку **Далее**.

    ![Настройка назначения](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. Сопоставление интеллектуальной таблицы появляется соответствие исходных toodestination таблиц на основе имен таблиц. Если таблица hello не существует в месте назначения hello, по умолчанию ADF создаст с hello таким же именем (применяется tooSQL сервера или базы данных SQL Azure в качестве источника). Также можно выбрать существующую таблицу tooan toomap. Просмотрите результат и нажмите кнопку **Далее**.

    ![Сопоставление таблиц](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. Проверьте соответствие схемы hello и проверьте наличие ошибок или предупреждений. Интеллектуальное сопоставление основано на имени столбца. Если преобразование типов данных не поддерживается между исходной и целевой столбец hello, вы видите сообщение об ошибке наряду с соответствующей таблицы hello. При выборе toolet фабрики данных автоматически создать таблицу hello, правильное преобразование типов может произойти при необходимости toofix hello несовместимости между хранилищами источника и назначения.

    ![Сопоставление схем](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. Щелкните **Далее**.

## <a name="configure-hello-performance-settings"></a>Настройка параметров производительности hello
В конфигурациях производительности hello, настройте учетную запись хранилища Azure, используемую для промежуточных hello данных перед загрузкой в хранилище данных SQL с помощью performantly [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly). После завершения копирования hello hello промежуточных данных в хранилище будут очищены автоматически.

Выберите существующую учетную запись хранения Azure и нажмите кнопку **Далее**.

![Настройка промежуточного BLOB-объекта](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a>Просмотрите сводные данные и развертывание конвейера hello

Проверьте конфигурацию hello и нажмите кнопку **Готово** кнопку toodeploy hello конвейера.

![Развертывание фабрики данных](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a>Мониторинг загрузки данных

Можно просмотреть ход выполнения развертывания hello и результаты в hello **развертывания** страницы.

1. После завершения развертывания hello по ссылке hello потребовал **щелкните здесь конвейера копирования toomonitor** загрузки выполняется toomonitor данных.

    ![Отслеживание конвейера](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. вновь созданные Hello **DWLoadData fromSQLServer** конвейера загрузки данных выбирается автоматически из левой hello **обозреватель ресурсов**.

    ![Представление конвейера](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. Щелкните в конвейер hello в середине hello hello toosee панель, сведения о состоянии для каждой таблицы, которая сопоставляет tooan действия.

    ![Просмотр действия таблицы](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. Далее щелкните в действие и позволяет просматривать данные hello загрузка сведений о hello правой панели, включая размер данных, строки, пропускной способности, и т. д.

    ![Просмотр сведений о действии таблицы](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. toolaunch этого мониторинга представление более поздней версии, выберите tooyour хранилище данных SQL, щелкните **загрузки данных > фабрики данных Azure**выберите фабрики и выберите **отслеживать существующие задачи загрузки**.

## <a name="next-steps"></a>Дальнейшие действия

toomigrate tooSQL вашей базы данных хранилища данных, в разделе [Общие сведения о миграции](sql-data-warehouse-overview-migrate.md).

toolearn Дополнительные сведения о фабрики данных Azure и его возможности перемещения данных, см. следующие статьи hello.

- [Введение tooAzure фабрики данных](../data-factory/data-factory-introduction.md)
- [Перемещение данных с помощью действия копирования](../data-factory/data-factory-data-movement-activities.md)
- [Tooand перемещения данных из хранилища данных SQL Azure, с помощью фабрики данных Azure](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

tooexplore данные в хранилище данных SQL, в разделе hello следующие статьи:

- [Подключиться с помощью Visual Studio и SSDT tooSQL хранилища данных](sql-data-warehouse-query-visual-studio.md)
- [Визуализация данных с помощью Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)

<!-- Azure references -->
[портал Azure]: https://portal.azure.com
