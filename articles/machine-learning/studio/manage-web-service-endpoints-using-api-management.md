---
title: "Сведения об управлении веб-службами AzureML с помощью управления API | Документация Майкрософт"
description: "Руководство по управлению веб-службами AzureML с помощью управления API."
keywords: "машинное обучение, управление api"
services: machine-learning
documentationcenter: 
author: roalexan
manager: jhubbard
editor: 
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/03/2017
ms.author: roalexan
ms.openlocfilehash: b2c9f53de1abd2aea5fabbefecc5bbb144148a7b
ms.sourcegitcommit: 5a6e943718a8d2bc5babea3cd624c0557ab67bd5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/01/2017
---
# <a name="learn-how-to-manage-azureml-web-services-using-api-management"></a>Сведения об управлении веб-службами AzureML с помощью управления API
## <a name="overview"></a>Обзор
Это руководство поможет быстро начать работу с управлением API, чтобы управлять веб-службами AzureML.

## <a name="what-is-azure-api-management"></a>Что собой представляет управление Azure API
Управление API Azure — это служба Azure, которая позволяет управлять конечными точками REST API, настраивая доступ пользователей, регулирование использования и мониторинг панели мониторинга. Сведения об управлении API Azure см. [здесь](https://azure.microsoft.com/services/api-management/). Руководство по началу работы с управлением API Azure находится [здесь](../../api-management/api-management-get-started.md). Это руководство, на котором основана данная статья, содержит больше разделов, включая информацию о конфигурациях оборудования, ценовых категориях, обработке ответов, проверке подлинности пользователей, создании продуктов, подписках разработчика и компактном отображении данных об использовании.

## <a name="what-is-azureml"></a>Что такое AzureML
AzureML — это служба Azure для машинного обучения, которая позволяет вам легко создавать и развертывать решения аналитики и предоставлять к ним доступ. Сведения о службе AzureML см. [здесь](https://azure.microsoft.com/services/machine-learning/).

## <a name="prerequisites"></a>Предварительные требования
Вот что вам нужно, чтобы выполнить инструкции, приведенные в этом руководстве:

* Учетная запись Azure. Если у вас нет учетной записи Azure, щелкните [здесь](https://azure.microsoft.com/pricing/free-trial/) , чтобы узнать, как создать бесплатную пробную учетную запись.
* Учетная запись AzureML. Если у вас нет учетной записи AzureML, щелкните [здесь](https://studio.azureml.net/) , чтобы узнать, как создать бесплатную пробную учетную запись.
* Рабочая область, служба и ключ API для эксперимента AzureML, развернутого в качестве веб-службы. Сведения о том, как создать эксперимент AzureML, см. [здесь](create-experiment.md). Сведения о том, как развернуть эксперимент AzureML в качестве веб-службы, см. [здесь](publish-a-machine-learning-web-service.md). Инструкции по созданию и тестированию простого эксперимента AzureML и его развертывания в качестве веб-службы содержатся также в дополнении А.

## <a name="create-an-api-management-instance"></a>Создание экземпляра API Management

Вы можете управлять веб-службой машинного обучения Azure с помощью экземпляра службы управления API.

1. Выполните вход на [портал Azure](https://portal.azure.com).
2. Выберите действие **Создать ресурс**.
3. В поле поиска введите "Управление API", а затем выберите ресурс "Служба управления API".
4. Щелкните **Создать**.
5. На основе значения **Имя** будет создан уникальный URL-адрес (в нашем примере это demoazureml).
6. Выберите значения полей **Подписка**, **Группа ресурсов** и **Расположение** для своего экземпляра службы.
7. Укажите значение для параметра **Название организации** (в нашем примере используется demoazureml).
8. Введите **адрес электронной почты администратора**, на который будут отправляться уведомления из системы управления API.
9. Щелкните **Создать**.

Создание службы может занять до 30 минут.

![Создание службы](./media/manage-web-service-endpoints-using-api-management/create-service.png)


## <a name="create-the-api"></a>Создание API
После создания службы нужно создать API. API представляет набор операций, которые могут быть вызваны клиентскими приложениями. Операции API передаются существующей веб-службе. В этом руководстве продемонстрировано создание интерфейсов API, которые играют роль посредников между вами и существующими веб-службами AzureML RRS и BES.

Чтобы создать API, выполните следующие действия.

1. На портале Azure откройте только что созданный экземпляр службы.
2. В области навигации слева щелкните **API**.

   ![api-management-menu](./media/manage-web-service-endpoints-using-api-management/api-management.png)

1. Щелкните **Добавить API**.
2. Введите **Имя веб-API** (а нашем примере это API Demo AzureML).
3. Для параметра **URL-адрес веб-службы** введите значение `https://ussouthcentral.services.azureml.net`.
4. Введите значение для параметра "Суффикс URL-адреса веб-API". Это значение будет последней частью URL-адреса, по которому клиенты отправляют запросы к этому экземпляру службы (в нашем примере используется суффикс azureml-demo).
5. В поле **Схема URL-адресов API** выберите значение **HTTPS**.
6. В поле **Продукты** выберите значение **Starter** (Начальный комплект)
7. Щелкните **Сохранить**.


## <a name="add-the-operations"></a>Добавление операций

Операции добавляются и настраиваются для API на портале издателя. На портале Azure для службы управления API щелкните **Publisher portal** (Портал издателя), чтобы открыть портал издателя, а затем выберите **API**, **Операции**, **Добавить операцию**.

![add-operation](./media/manage-web-service-endpoints-using-api-management/add-an-operation.png)

Появится окно **New operation** (Новая операция), а вкладка **Signature** (Сигнатура) будет выбрана по умолчанию.

## <a name="add-rrs-operation"></a>Добавление операции RRS
Сначала создайте операцию для службы AzureML RRS.

1. В поле **HTTP verb** (HTTP-команда) выберите значение **POST**.
2. В поле **URL-адрес шаблона** введите `/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}`.
3. Введите **Отображаемое имя** (RRS Execute в нашем примере).

   ![add-rrs-operation-signature](./media/manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

4. Слева щелкните **Ответы** > **Добавить** и выберите значение **200 OK**.
5. Чтобы сохранить эту операцию, нажмите кнопку **Сохранить** .

   ![add-rrs-operation-response](./media/manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a>Добавление операций BES

> [!NOTE]
> К инструкциям по добавлению операций BES снимки экрана здесь не прилагаются, так как они совпадают с теми, которые представлены для добавления операции RRS.

### <a name="submit-but-not-start-a-batch-execution-job"></a>Отправка (но не запуск) задачи выполнения пакетов

1. Чтобы добавить к API операцию BES, щелкните **Добавить операцию**.
2. В поле **HTTP verb** (HTTP-команда) выберите значение **POST**.
3. В поле **URL-адрес шаблона** введите `/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}`.
4. Введите **Отображаемое имя** (BES Submit в нашем примере).
5. Слева щелкните **Ответы** > **Добавить** и выберите значение **200 OK**.
6. Щелкните **Сохранить**.

### <a name="start-a-batch-execution-job"></a>Запуск задачи выполнения пакетов

1. Чтобы добавить к API операцию BES, щелкните **Добавить операцию**.
2. В поле **HTTP verb** (HTTP-команда) выберите значение **POST**.
3. Введите значение `/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}` в поле **HTTP verb** (HTTP-команда).
4. Введите **Отображаемое имя** (BES Start в нашем примере).
6. Слева щелкните **Ответы** > **Добавить** и выберите значение **200 OK**.
7. Щелкните **Сохранить**.

### <a name="get-the-status-or-result-of-a-batch-execution-job"></a>Получение состояния или результата задания пакетного выполнения

1. Чтобы добавить к API операцию BES, щелкните **Добавить операцию**.
2. В поле **HTTP verb** (HTTP-команда) выберите значение **GET**.
3. В поле **URL-адрес шаблона** введите `/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}`.
4. Введите **Отображаемое имя** (BES Start в нашем примере).
6. Слева щелкните **Ответы** > **Добавить** и выберите значение **200 OK**.
7. Щелкните **Сохранить**.

### <a name="delete-a-batch-execution-job"></a>Удаление задачи выполнения пакетов

1. Чтобы добавить к API операцию BES, щелкните **Добавить операцию**.
2. В поле **HTTP verb** (HTTP-команда) выберите значение **DELETE**.
3. В поле **URL-адрес шаблона** введите `/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}`.
4. Введите **Отображаемое имя** (BES Delete в нашем примере).
5. Слева щелкните **Ответы** > **Добавить** и выберите значение **200 OK**.
6. Щелкните **Сохранить**.

## <a name="call-an-operation-from-the-developer-portal"></a>Вызов операции с портала разработчика

Операции могут быть вызваны из портала разработчика, где предоставляется удобный способ для просмотра и проверки операций API. Инструкции на этом шаге описывают вызов метода **RRS Execute**, который мы добавили в элемент **AzureML Demo API**. 

1. Щелкните **Портал разработчика**.

   ![developer-portal](./media/manage-web-service-endpoints-using-api-management/developer-portal.png)

2. Щелкните **Интерфейсы API** в меню сверху, а затем щелкните **AzureML Demo API** (Демонстрационный API AzureML), чтобы отобразились доступные операции.

   ![demoazureml-api](./media/manage-web-service-endpoints-using-api-management/demoazureml-api.png)

3. Выберите операцию **RRS Execute** . Щелкните **Попробовать**.

   ![try-it](./media/manage-web-service-endpoints-using-api-management/try-it.png)

4. В разделе **Параметры запроса** введите значения в полях **workspace** (рабочая область) и **service** (служба). В поле **apiversion** (версия API) введите значение 2.0, а в поле **details** (сведения) — true. Название ваших **рабочей области** и **службы** отображается на панели мониторинга веб-службы AzureML (см. раздел **Тестирование веб-службы** в приложении A).

   В поле **Заголовки запроса** щелкните действие **Добавить заголовок** и введите "Content-Type" и "application/json". Снова щелкните **Добавить заголовок** и введите значения "Authorization" и "Bearer *\<your service API-KEY\>*". Название ключа API (API-KEY) отображается на панели мониторинга веб-службы AzureML (см. раздел **Test the web service** (Тестирование веб-службы) в приложении A).

   В поле **Текст запроса** введите `{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}`.

   ![azureml-demo-api](./media/manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

5. Нажмите кнопку **Отправить**.

   ![Отправить](./media/manage-web-service-endpoints-using-api-management/send.png)

После вызова операции портал разработчика выводит **запрошенный URL-адрес** от фоновой службы, **состояние ответа**, **заголовки ответа** и **содержимое ответа**.

![response-status](./media/manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a>Дополнение А — создание и тестирование простой веб-службы AzureML
### <a name="creating-the-experiment"></a>Создание эксперимента
Ниже описаны действия, которые нужно выполнить, чтобы создать простой эксперимент AzureML и развернуть его в качестве веб-службы. Веб-служба принимает столбец случайного текста и возвращает набор функций в виде целых чисел. Например:

| текст | Хэшированный текст |
| --- | --- |
| This is a good day |1 1 2 2 0 0 2 1 |

Сначала перейдите на веб-сайт [https://studio.azureml.net/](https://studio.azureml.net/) и, чтобы выполнить вход, введите свои учетные данные. Затем создайте пустой эксперимент.

![search-experiment-templates](./media/manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

Измените его имя на **SimpleFeatureHashingExperiment**. Разверните список **Saved Datasets** (Сохраненные наборы данных) и перетащите элемент **Book Reviews from Amazon** (Обзоры книг на Amazon) в свой эксперимент.

![simple-feature-hashing-experiment](./media/manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

Разверните списки **Преобразование данных** и **Manipulation** (Работа с данными) и перетащите элемент **Select Columns in Dataset** (Выбор столбцов в наборе данных) в свой эксперимент. Соедините элемент **Book Reviews from Amazon** (Обзоры книг на Amazon) с элементом **Select Columns in Dataset** (Выбор столбцов в наборе данных).

![select-columns](./media/manage-web-service-endpoints-using-api-management/project-columns.png)

Последовательно щелкните **Select Columns in Dataset** (Выбор столбцов в наборе данных), **Launch column selector** (Запустить средство выбора столбцов), а затем выберите **Col2**. Чтобы изменения вступили в силу, щелкните значок флажка.

![select-columns](./media/manage-web-service-endpoints-using-api-management/select-columns.png)

Разверните список **Text Analytics** (Аналитика текста) и перетащите элемент **Feature Hashing** (Хеширование признаков) в свой эксперимент. Соедините элемент **Select Columns in Dataset** (Выбор столбцов в наборе данных) с элементом **Feature Hashing** (Хэширование признаков).

![connect-project-columns](./media/manage-web-service-endpoints-using-api-management/connect-project-columns.png)

В поле **Hashing bitsize** (Размер бита хеширования) укажите значение **3**. Будет создано 8 столбцов (23).

![hashing-bitsize](./media/manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

На этом этапе рекомендуется протестировать эксперимент, нажав кнопку **Запустить** .

![Запустить](./media/manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a>Создание веб-службы
Теперь создайте веб-службу. Разверните список **Веб-служба** и перетащите элемент **Входные данные** в свой эксперимент. Соедините элемент **Входные данные** с элементом **Feature Hashing** (Хеширование признаков). Перетащите в свой эксперимент также элемент **Вывод** . Соедините элемент **Вывод** с элементом **Feature Hashing** (Хеширование признаков).

![output-to-feature-hashing](./media/manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

Щелкните **Опубликовать веб-службу**.

![publish-web-service](./media/manage-web-service-endpoints-using-api-management/publish-web-service.png)

Чтобы опубликовать веб-службу, щелкните **Да** .

![yes-to-publish](./media/manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-the-web-service"></a>Тестирование веб-службы
Веб-служба AzureML состоит из конечных точек RSS (служба запросов и ответов) и BES (служба выполнения пакетов). Конечные точки RSS предназначены для синхронного выполнения задач. Конечные точки BES — для асинхронного. Чтобы протестировать веб-службу с помощью приведенного ниже примера кода на языке Python, вам может понадобиться скачать и установить пакет Azure SDK для Python (см. статью [Способы установки Python](../../python-how-to-install.md)).

Для примера кода ниже потребуется указать также **рабочую область**, **службу** и **ключ API** вашего эксперимента. Вы можете узнать название рабочей области и службы, щелкнув **Запрос-ответ** или **Выполнение пакета** для своего эксперимента на панели мониторинга веб-службы.

![find-workspace-and-service](./media/manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

Чтобы отобразился **ключ API**, щелкните свой эксперимент на панели мониторинга веб-службы.

![find-api-key](./media/manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a>Тестирование конечной точки RRS
##### <a name="test-button"></a>Кнопка тестирования
Простой способ протестировать конечную точку RRS — это нажать кнопку **Тестировать** на панели мониторинга веб-службы.

![test](./media/manage-web-service-endpoints-using-api-management/test.png)

В поле **col2** введите текст **This is a good day**. Щелкните значок флажка.

![enter-data](./media/manage-web-service-endpoints-using-api-management/enter-data.png)

Отобразится примерно такой текст:

![sample-output](./media/manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a>Пример кода
Протестировать конечную точку RRS вы можете также с помощью клиентского кода. Если на панели мониторинга щелкнуть **Запрос-ответ** и прокрутить страницу до самого низа, отобразится образец кода для C#, Python и R. Отобразится также и синтаксис запроса RRS, в том числе URI, заголовки и текст запроса.

В этом руководстве приведен рабочий экземпляр кода на языке Python. В нем нужно будет изменить название **рабочей области**, **службы** и **ключа API** эксперимента.

    import urllib2
    import json
    workspace = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE WORKSPACE ID>"
    service = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE SERVICE ID>"
    api_key = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE API KEY>"
    data = {
    "Inputs": {
        "input1": {
            "ColumnNames": ["Col2"],
            "Values": [ [ "This is a good day" ] ]
        },
    },
    "GlobalParameters": { }
    }
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace + "/services/" + service + "/execute?api-version=2.0&details=true"
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}
    body = str.encode(json.dumps(data))
    try:
        req = urllib2.Request(url, body, headers)
        response = urllib2.urlopen(req)
        result = response.read()
        print "result:" + result
            except urllib2.HTTPError, error:
        print("The request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a>Тестирование конечной точки BES
На панели мониторинга щелкните **Выполнение пакета** и прокрутите страницу до самого низа. Отобразится пример кода на языках C#, Python и R. Отобразится также синтаксис запроса BES на отправку задачи, запуск задачи, получение статуса или результата выполнения задачи и на удаление задачи.

В этом руководстве приведен рабочий экземпляр кода на языке Python. В нем нужно изменить название **рабочей области**, **службы** и **ключа API** эксперимента. Кроме того, нужно изменить **имя учетной записи хранения**, **ключ учетной записи хранения** и **имя контейнера хранилища**. Наконец, вам понадобится изменить расположение **входного файла** и **выходного файла**.

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH THE API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH THE LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH THE LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("The request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading the result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written to the file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("The results for " + outputName + " are available at the following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "The results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading the input to blob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded the input to blob storage"
    input_blob_path = "/" + storage_container_name + "/" + input_blob_name
    connection_string = "DefaultEndpointsProtocol=https;AccountName=" + storage_account_name + ";AccountKey=" + storage_account_key
    payload =  {
        "Input": {
            "ConnectionString": connection_string,
            "RelativeLocation": input_blob_path
        },
        "Outputs": {
            "output1": { "ConnectionString": connection_string, "RelativeLocation": "/" + storage_container_name + "/" + output_blob_name },
        },
        "GlobalParameters": {
        }
    }
        body = str.encode(json.dumps(payload))
    headers = { "Content-Type":"application/json", "Authorization":("Bearer " + api_key)}
    print("Submitting the job...")
    # submit the job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove the enclosing double-quotes
    print("Job ID: " + job_id)
    # start the job
    print("Starting the job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking the job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in the follwing code
        req = urllib2.Request(url2, headers = { "Authorization":("Bearer " + api_key) })
        try:
            response = urllib2.urlopen(req)
        except urllib2.HTTPError, error:
            printHttpError(error)
            return
        result = json.loads(response.read())
        status = result["StatusCode"]
        print "status:" + status
        if (status == 0 or status == "NotStarted"):
            print("Job " + job_id + " not yet started...")
        elif (status == 1 or status == "Running"):
            print("Job " + job_id + " running...")
        elif (status == 2 or status == "Failed"):
            print("Job " + job_id + " failed!")
            print("Error details: " + result["Details"])
            break
        elif (status == 3 or status == "Cancelled"):
            print("Job " + job_id + " cancelled!")
            break
        elif (status == 4 or status == "Finished"):
            print("Job " + job_id + " finished!")
            processResults(result)
            break
        time.sleep(1) # wait one second
    return
    invokeBatchExecutionService()
