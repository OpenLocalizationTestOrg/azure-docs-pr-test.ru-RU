---
title: "aaaStream данные из Stream Analytics в хранилище Озера данных | Документы Microsoft"
description: "Использование Azure Stream Analytics toostream данных в хранилище Озера данных Azure"
services: data-lake-store,stream-analytics
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: edb58e0b-311f-44b0-a499-04d7e6c07a90
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 68c727d4807db0abe6efa90145d68c78902eb789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a>Потоковая передача данных из большого двоичного объекта службы хранилища Azure в хранилище озера данных с помощью Azure Stream Analytics
В этой статье вы узнаете, как toouse Azure Озера данных хранения в качестве выходных данных для задания Azure Stream Analytics. В этой статье демонстрируется простой сценарий, который считывает данные из большого двоичного объекта хранилища Azure (input) и записывает hello хранилища Озера данных tooData (output).

> [!NOTE]
> В настоящее время создание и Настройка хранилища Озера данных выводит для Stream Analytics поддерживается только в hello [классический портал Azure](https://manage.windowsazure.com). Таким образом некоторые части этого учебника будет использовать hello классический портал Azure.
>
>

## <a name="prerequisites"></a>Предварительные требования
Прежде чем начать работу с учебником, необходимо иметь следующие hello.

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Учетная запись хранения Azure.** Контейнер больших двоичных объектов на основе данных tooinput учетная запись используется для задания Stream Analytics. Для этого учебника Предположим, что учетную запись хранилища **storageforasa** и именем контейнера в учетной записи hello **storageforasacontainer**. После создания контейнера hello, отправьте файл tooit образца данных. 
  
* **Учетная запись хранилища озера данных Azure**. Следуйте инструкциям hello в [Приступая к работе с хранилища Озера данных Azure, с помощью портала Azure hello](data-lake-store-get-started-portal.md). Предположим, у вас есть учетная запись хранилища Data Lake Store **asadatalakestore**. 

## <a name="create-a-stream-analytics-job"></a>Создание задания Stream Analytics
Для начала нужно создать задание Stream Analytics с источником входных данных и целевым объектом для выходных данных. В этом учебнике hello источник представляет собой контейнер больших двоичных объектов Azure и назначение hello — хранилище Озера данных.

1. Войдите на toohello [портала Azure](https://portal.azure.com).

2. Hello левой панели щелкните **заданий Stream Analytics**, а затем нажмите кнопку **добавить**.

    ![Создание задания Stream Analytics](./media/data-lake-store-stream-analytics/create.job.png "Создание задания Stream Analytics")

    > [!NOTE]
    > Убедитесь, что создание задания в hello же регионе, что учетная запись хранения hello, или вы повлечет за собой дополнительные затраты на перемещение данных между регионами.
    >

## <a name="create-a-blob-input-for-hello-job"></a>Создание входных данных больших двоичных объектов для задания hello

1. Привет открыть страницу для задания Stream Analytics hello, hello левой панели щелкните hello **входов** , а затем щелкните **добавить**.

    ![Добавьте задание входных tooyour](./media/data-lake-store-stream-analytics/create.input.1.png "добавить задание входных tooyour")

2. На hello **вводимые** колонке предоставляют hello следующие значения.

    ![Добавьте задание входных tooyour](./media/data-lake-store-stream-analytics/create.input.2.png "добавить задание входных tooyour")

    * Для **входных псевдонимов**, введите уникальное имя для входных данных задания hello.
    * **Тип источника** — выберите **Поток данных**.
    * **Источник** — выберите **Хранилище больших двоичных объектов**.
    * **Подписка** — выберите **Использовать хранилище BLOB-объектов из текущей подписки**.
    * Для **учетной записи хранилища**, выберите учетную запись хранения hello, созданный в рамках hello необходимых компонентов. 
    * Для **контейнера**выберите контейнер hello, созданную в hello выбранную учетную запись хранилища.
    * **Формат сериализации событий** — выберите **CSV**.
    * **Разделитель** — выберите **Табуляция**.
    * **Кодировка** — выберите **UTF-8**.

    Щелкните **Создать**. портал Hello теперь добавляет hello входных данных и проверяет подключение tooit hello.


## <a name="create-a-data-lake-store-output-for-hello-job"></a>Создание хранилища Озера данных вывода для задания hello

1. Откройте страницу приветствия для задания Stream Analytics hello, щелкните hello **выходов** , а затем щелкните **добавить**.

    ![Добавьте Задание вывода tooyour](./media/data-lake-store-stream-analytics/create.output.1.png "добавить задание tooyour выходных данных")

2. На hello **новый Выход** колонке предоставляют hello следующие значения.

    ![Добавьте Задание вывода tooyour](./media/data-lake-store-stream-analytics/create.output.2.png "добавить задание tooyour выходных данных")

    * Для **Псевдоним выхода**, введите уникальное имя для выходных данных задания hello. Это понятное имя, используемое в выходных данных запроса toothis хранилища Озера данных запросов toodirect hello.
    * **Приемник** — выберите **Data Lake Store**.
    * Появится запрос tooauthorize доступ к учетной записи хранилища Озера tooData. Щелкните **Авторизовать**.

3. На hello **новый Выход** колонке продолжить hello tooprovide следующие значения.

    ![Добавьте Задание вывода tooyour](./media/data-lake-store-stream-analytics/create.output.3.png "добавить задание tooyour выходных данных")

    * Для **имя учетной записи**, выберите учетную запись хранилища Озера данных hello, уже созданных место toobe выходные данные задания hello, отправляемые.
    * Для **шаблон префикс пути**, введите путь, используемый файл toowrite файлов в пределах hello указанного хранилища Озера данных.
    * Для **формат даты**, если вы использовали токен даты hello префикс пути, можно выбрать формат даты hello, в котором упорядочены файлов.
    * Для **формат времени**, если вы использовали токен времени hello префикс пути, укажите формат времени hello, в котором упорядочены файлов.
    * **Формат сериализации событий** — выберите **CSV**.
    * **Разделитель** — выберите **Табуляция**.
    * **Кодировка** — выберите **UTF-8**.
    
    Щелкните **Создать**. портал Hello теперь добавляет выход hello и проверяет подключение tooit hello.
    
## <a name="run-hello-stream-analytics-job"></a>Запустить задание Stream Analytics hello

1. toorun задания Stream Analytics, необходимо выполнить запрос из hello **запроса** вкладки. В этом учебнике, можно выполнить запрос образец hello, заменив заполнители hello hello задания входных и выходных псевдонимов, как показано на снимке экрана приветствия ниже.

    ![Выполнение запроса](./media/data-lake-store-stream-analytics/run.query.png "Выполнение запроса")

2. Нажмите кнопку **Сохранить** от hello в верхней части экрана приветствия, а затем из hello **Обзор** щелкните **запустить**. В диалоговом окне приветствия выберите **время пользовательского**и задайте hello текущую дату и время.

    ![Установка времени задания](./media/data-lake-store-stream-analytics/run.query.2.png "Установка времени задания")

    Нажмите кнопку **запустить** toostart hello задания. Он может занять tooa пару минут toostart hello задания.

3. данные tootrigger hello задания toopick hello из большого двоичного объекта hello, скопируйте toohello файла образца данных BLOB-контейнере. Образец файла данных можно получить из hello [репозитории Озера данных Azure](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt). В этом учебнике, давайте скопируйте файл hello **vehicle1_09142014.csv**. Можно использовать различные клиенты, такие как [обозреватель хранилищ Azure](http://storageexplorer.com/), контейнер больших двоичных объектов tooa tooupload данных.

4. Из hello **Обзор** в разделе **мониторинг**, обработкой данных hello в разделе.

    ![Мониторинг задания](./media/data-lake-store-stream-analytics/run.query.3.png "Мониторинг задания")

5. Наконец можно проверить, что выходные данные задания hello доступен в учетной записи хранилища Озера данных hello. 

    ![Проверка выходных данных](./media/data-lake-store-stream-analytics/run.query.4.png "Проверка выходных данных")

    Панели обозревателя данных hello, обратите внимание на то, что hello вывода письменного tooa путь к папке, как указывается в hello хранилища Озера данных параметры вывода (`streamanalytics/job/output/{date}/{time}`).  

## <a name="see-also"></a>См. также
* [Создание toouse кластера HDInsight хранилища Озера данных](data-lake-store-hdinsight-hadoop-use-portal.md)
