---
title: "aaaCopy данные из хранилища больших двоичных объектов tooSQL база данных — Azure | Документы Microsoft"
description: "Этот учебник показывает, как toouse действие копирования в фабрике данных Azure конвейера toocopy данные из базы данных tooSQL хранилища Blob."
keywords: "BLOB-объект, SQL, хранилище BLOB-объектов, копирование данных"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e4035060-93bf-4e8d-bf35-35e2d15c51e0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: a2c3fb8a4ddd63b0b6b3e75903b7a7eaf188fda4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-copy-data-from-blob-storage-toosql-database-using-data-factory"></a>Учебник: Копирование данных из хранилища больших двоичных объектов tooSQL базы данных с помощью фабрики данных
> [!div class="op_single_selector"]
> * [Обзор и предварительные требования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Мастер копирования](data-factory-copy-data-wizard-tutorial.md)
> * [Портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Шаблон Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [ИНТЕРФЕЙС REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

В этом учебнике создать фабрику данных данными конвейера toocopy из базы данных tooSQL хранилища больших двоичных объектов.

Действие копирования Hello выполняет перемещение данных hello в фабрике данных Azure. Это действие выполняется с помощью глобально доступной службы, обеспечивающей безопасное, надежное и масштабируемое копирование данных между разными хранилищами. В разделе [действия перемещения данных](data-factory-data-movement-activities.md) статьи приведены сведения о действии копирования hello.  

> [!NOTE]
> Подробный обзор hello служба фабрики данных см. в разделе hello [tooAzure введение фабрики данных](data-factory-introduction.md) статьи.
>
>

## <a name="prerequisites-for-hello-tutorial"></a>Необходимые условия для учебника hello
Прежде чем начать работу с учебником, необходимо иметь hello следующие предварительные требования:

* **Подписка Azure**.  Если у вас нет подписки, вы можете создать бесплатную пробную версию учетной записи всего за несколько минут. В разделе hello [бесплатной пробной версии](http://azure.microsoft.com/pricing/free-trial/) Дополнительные сведения см.
* **исходного**хранилища данных. Использовать хранилище больших двоичных объектов hello как **источника** хранилище данных в этом учебнике. При отсутствии учетной записи хранилища Azure в разделе hello [создать учетную запись хранилища](../storage/common/storage-create-storage-account.md#create-a-storage-account) статьи для действия toocreate один.
* **База данных SQL Azure**. В этом учебнике используется база данных SQL Azure в качестве **конечного** хранилища данных. Если у вас нет базы данных Azure SQL, можно использовать в hello учебника, см. в разделе [как toocreate и настроить базу данных SQL Azure](../sql-database/sql-database-get-started.md) toocreate один.
* **SQL Server 2012/2014 или Visual Studio 2013**. Используйте SQL Server Management Studio или Visual Studio toocreate образца базы данных и tooview hello результирующие данные в базе данных hello.  

## <a name="collect-blob-storage-account-name-and-key"></a>Получение имени и ключа учетной записи хранения BLOB-объектов
Требуется учетная запись hello, имя и ключ учетной записи хранилища Azure учетной записи toodo этого учебника. Запишите **имя** и **ключ учетной записи** для своей учетной записи хранения Azure.

1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Нажмите кнопку **дополнительные службы** на hello слева и выбрать пункт **учетные записи хранения**.

    !["Обзор" — "Учетные записи хранения"](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. В hello **учетные записи хранения** колонки, выберите hello **учетной записи хранилища Azure** требуется toouse в этом учебнике.
4. В разделе **Параметры** выберите ссылку **Ключи доступа**.
5. Нажмите кнопку **копирования** (изображение) рядом слишком**имя учетной записи хранения** текста поле, сохранить и вставка его где-нибудь (например: в текстовом файле).
6. Повторите предыдущие шаг toocopy hello или запишите hello **key1**.

    ![Ключ доступа к хранилищу](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. Закройте все колонках hello, нажав кнопку **X**.

## <a name="collect-sql-server-database-user-names"></a>Получение имени сервера SQL, имени базы данных и имени пользователя
Должны иметь имена hello Azure SQL server, базы данных и toodo пользователя этого учебника. Запишите имена **сервера**, **базы данных** и **пользователя** базы данных SQL Azure.

1. В hello **портал Azure**, нажмите кнопку **дополнительные службы** на hello слева и выберите **баз данных SQL**.
2. В hello **колонки баз данных SQL**выберите hello **базы данных** требуется toouse в этом учебнике. Запишите hello **имя базы данных**.  
3. В hello **базы данных SQL** колонка, щелкните **свойства** под **параметры**.
4. Запишите значения hello **имя сервера** и **имя входа АДМИНИСТРАТОРА сервера**.
5. Закройте все колонках hello, нажав кнопку **X**.

## <a name="allow-azure-services-tooaccess-sql-server"></a>Разрешить службам Azure tooaccess SQL server
Убедитесь, что **разрешить доступ службы tooAzure** включен параметр **ON** для вашего сервера Azure SQL, так что hello служба фабрики данных можно получить доступ к серверу Azure SQL. tooverify и включение этого параметра hello следующие действия:

1. Нажмите кнопку **дополнительные службы** концентратора hello слева и щелкните **серверов SQL Server**.
2. Выберите сервер и щелкните **Брандмауэр** в разделе **Параметры**.
3. В hello **параметры брандмауэра** колонка, щелкните **ON** для **разрешить доступ службы tooAzure**.
4. Закройте все колонках hello, нажав кнопку **X**.

## <a name="prepare-blob-storage-and-sql-database"></a>Подготовка хранилища BLOB-объектов и базы данных SQL
Теперь Подготовьте хранилище больших двоичных объектов и базы данных Azure SQL для учебника hello, выполнив следующие шаги hello:  

1. Запустите Блокнот. Скопируйте следующий текст hello и сохраните его как **emp.txt** слишком**C:\ADFGetStarted** папку на жестком диске.

    ```
    John, Doe
    Jane, Doe
    ```
2. Использовать инструменты, такие как [обозреватель хранилищ Azure](http://storageexplorer.com/) toocreate hello **adftutorial** hello контейнера и tooupload **emp.txt** toohello файла контейнера.

    ![Обозреватель хранилищ Azure Копирование данных из базы данных tooSQL хранилища Blob](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. Используйте hello, следуя hello toocreate скрипт SQL **emp** таблицы в базе данных SQL Azure.  

    ```SQL
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

    **Если у вас есть SQL Server 2012 и 2014 установлены на компьютере:** следуйте инструкциям из [управление базой данных SQL Azure с помощью SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL и запустите hello скрипт SQL. В этой статье используется hello [классический портал Azure](http://manage.windowsazure.com), не hello [новый портал Azure](https://portal.azure.com), tooconfigure брандмауэра для сервера Azure SQL.

    Если клиент не может быть tooaccess hello Azure SQL server, необходимо tooconfigure брандмауэра для Azure SQL server tooallow доступ с вашего компьютера (IP-адрес). В разделе [в этой статье](../sql-database/sql-database-configure-firewall-settings.md) действия tooconfigure hello брандмауэра для сервера Azure SQL.

## <a name="create-a-data-factory"></a>Создать фабрику данных
Предварительные требования hello завершена. Можно создать фабрику данных, с помощью одного из следующих способов hello. Выберите один из вариантов hello в hello раскрывающегося списка в верхней hello или hello следующие ссылки tooperform hello учебника.     

* [Мастер копирования](data-factory-copy-data-wizard-tutorial.md)
* [Портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
* [Шаблон Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [ИНТЕРФЕЙС REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
* [API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> конвейер данных Hello в этом учебнике копирует данные из источника данных хранилища tooa целевое хранилище данных. Он не выполняет преобразование входных данных tooproduce выходных данных. Учебник о том, как tootransform данных с помощью фабрики данных Azure, см. [учебника: построение первые данные конвейера tootransform использование кластера Hadoop](data-factory-build-your-first-pipeline.md).
> 
> Вы можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия. Подробные сведения см. в статье [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md). 
