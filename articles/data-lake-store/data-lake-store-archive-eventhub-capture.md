---
title: "aaaCapture данные из концентраторов событий в хранилище Озера данных Azure | Документы Microsoft"
description: "Хранилище Озера данных Azure используйте toocapture данные из концентраторов событий"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a>Хранилище Озера данных Azure используйте toocapture данные из концентраторов событий

Узнайте, как toouse данных toocapture хранилища Озера данных Azure полученных концентраторов событий Azure.

## <a name="prerequisites"></a>Предварительные требования

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Учетная запись Azure Data Lake Store.** Инструкции о том, как один, см. в разделе toocreate [Приступая к работе с хранилища Озера данных Azure](data-lake-store-get-started-portal.md).

*  **Пространство имен концентраторов событий.** Дополнительные сведения см. в разделе [Создание пространства имен концентраторов событий](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace). Убедитесь, что учетная запись хранилища Озера данных hello и пространство имен hello концентраторов событий в hello одной подписке.


## <a name="assign-permissions-tooevent-hubs"></a>Назначение разрешений tooEvent концентраторы

В этом разделе создайте папку в пределах учетной записи hello toocapture hello данные из концентраторов событий. Можно также назначить разрешения tooEvent концентраторы, чтобы его можно записать данные в учетной записи хранилища Озера данных. 

1. Открыть учетную запись хранилища Озера данных hello где toocapture данные из концентраторов событий и выберите команду **обозреватель данных**.

    ![Обозреватель данных Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data Lake Store data explorer")

2.  Нажмите кнопку **новую папку** и введите имя папки, где требуется сохранить данные hello toocapture.

    ![Создание папки в Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Create a new folder in Data Lake Store")

3. Назначьте разрешения на корневой hello объекта hello хранилища Озера данных. 

    а. Нажмите кнопку **обозреватель данных**выберите корень hello hello хранилища Озера данных и нажмите кнопку **доступа**.

    ![Назначение разрешений корневой папке Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Assign permissions for Data Lake Store root")

    b. В разделе **Доступ** выберите **Добавить**, щелкните **Выберите пользователя или группу**, а затем найдите `Microsoft.EventHubs`. 

    ![Назначение разрешений корневой папке Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store root")
    
    Нажмите кнопку **Выбрать**.

    c. В разделе **Назначение разрешений** выберите **Выбор разрешений**. Задать **разрешений** слишком**Execute**. Задать **добавить** слишком**эту папку и все дочерние элементы**. Задать **добавить в качестве** слишком**запись разрешения доступа, а элемент разрешения по умолчанию**.

    ![Назначение разрешений корневой папке Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Assign permissions for Data Lake Store root")

    Нажмите кнопку **ОК**.

4. Назначение разрешений для папки hello под учетной записью хранилища Озера данных место toocapture данных.

    а. Нажмите кнопку **обозреватель данных**, выберите папку hello в hello хранилища Озера данных и нажмите кнопку **доступа**.

    ![Назначение разрешений в папке Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Assign permissions for Data Lake Store folder")

    b. В разделе **Доступ** выберите **Добавить**, щелкните **Выберите пользователя или группу**, а затем найдите `Microsoft.EventHubs`. 

    ![Назначение разрешений в папке Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Assign permissions for Data Lake Store folder")
    
    Нажмите кнопку **Выбрать**.

    c. В разделе **Назначение разрешений** выберите **Выбор разрешений**. Задать **разрешений** слишком**чтение, запись и** и **Execute**. Задать **добавить** слишком**эту папку и все дочерние элементы**. Задайте **добавить в качестве** слишком**запись разрешения доступа, а элемент разрешения по умолчанию**.

    ![Назначение разрешений в папке Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Assign permissions for Data Lake Store folder")
    
    Нажмите кнопку **ОК**. 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a>Настройка хранилища Озера tooData данных toocapture концентраторов событий

В этом разделе вы создаете концентратор событий в пространстве имен концентраторов событий. Можно также настроить hello концентратора событий toocapture данных tooan хранилища Озера данных Azure. В этом разделе предполагается, что вы уже создали пространство имен концентраторов событий.

2. Из hello **Обзор** области пространства имен hello концентраторов событий, выберите **+ концентратора событий**.

    ![Создание концентратора событий](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Create Event Hub")

3. Предоставляют следующие hello значения хранилища Озера данных tooData tooconfigure концентраторов событий toocapture.

    ![Создание концентратора событий](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Create Event Hub")

    а. Введите имя для hello концентратора событий.
    
    b. В этом учебнике значение **количество разделов** и **хранение сообщений** toohello значения по умолчанию.
    
    c. Задать **захвата** слишком**на**. Набор hello **временное окно** (как часто toocapture) и **размер окна** (toocapture размер данных). 
    
    d. Для **записи поставщика**выберите **хранилища Озера данных Azure** и hello выберите hello хранилища Озера данных, созданной ранее. Для **пути Озера данных**, введите имя hello hello папку, созданную в hello хранилища Озера данных. Требуется только относительный путь toohello tooprovide hello папки.

    д. Оставьте hello **имя образца отслеживания форматах** toohello значение по умолчанию. Этот параметр определяет структуру папок hello, созданному в папку отслеживания hello.

    f. Щелкните **Создать**.

## <a name="test-hello-setup"></a>Программа установки hello теста

Теперь можно проверить hello решения путем отправки данных toohello концентратор событий Azure. Следуйте инструкциям hello в [отправки событий концентраторов событий tooAzure](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md). После начала отправки данных hello появиться hello данные отражаются в хранилище Озера данных hello структуру папок, указанные с помощью. Просмотреть структуру папок, например, как показано на следующий снимок экрана, находящихся в хранилище Озера данных hello.

![Пример данных концентратора событий в Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Sample EventHub data in Data Lake Store")

> [!NOTE]
> Даже если нет сообщений, поступающих в концентраторы событий, концентраторы событий записывает пустые файлы с только что hello заголовки в hello хранилища Озера данных. Hello файлы записываются в hello же интервал времени, который был предоставлен при создании hello концентраторов событий.
> 
>

## <a name="analyze-data-in-data-lake-store"></a>Анализ данных в хранилище озера данных

После загрузки данных hello в хранилище Озера данных, аналитических задания можно выполнять tooprocess и обработайте данные hello. В разделе [USQL Avro пример](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) о том, как toodo этот с помощью аналитики Озера данных Azure.
  

## <a name="see-also"></a>См. также
* [Защита данных в хранилище озера данных](data-lake-store-secure-data.md)
* [Копирование данных из хранилища Озера tooData больших двоичных объектов хранилища Azure](data-lake-store-copy-data-azure-storage-blob.md)
