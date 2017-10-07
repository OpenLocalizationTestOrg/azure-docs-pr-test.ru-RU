---
title: "как toomanage AzureML web services с помощью API управления aaaLearn | Документы Microsoft"
description: "Руководство, показывающий, как toomanage AzureML web services с помощью API управления."
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
ms.date: 01/19/2017
ms.author: roalexan
ms.openlocfilehash: 6e764fbfd71be6cc908a1c8d3d8889969fc651a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="learn-how-toomanage-azureml-web-services-using-api-management"></a>Узнайте, как toomanage AzureML web services с помощью API-Интерфейс управления
## <a name="overview"></a>Обзор
В этом руководстве показано, как tooquickly приступить к работе с API управления toomanage AzureML веб-служб.

## <a name="what-is-azure-api-management"></a>Что собой представляет управление Azure API
Управление API Azure — это служба Azure, которая позволяет управлять конечными точками REST API, настраивая доступ пользователей, регулирование использования и мониторинг панели мониторинга. Сведения об управлении API Azure см. [здесь](https://azure.microsoft.com/services/api-management/). Нажмите кнопку [здесь](../api-management/api-management-get-started.md) руководство о том, как tooget работы с API управления Azure. Это руководство, на котором основана данная статья, содержит больше разделов, включая информацию о конфигурациях оборудования, ценовых категориях, обработке ответов, проверке подлинности пользователей, создании продуктов, подписках разработчика и компактном отображении данных об использовании.

## <a name="what-is-azureml"></a>Что такое AzureML
AzureML — это служба Azure, для машинного обучения, которая позволяет tooeasily построения, развертывания и совместно использовать решениями углубленной аналитики. Сведения о службе AzureML см. [здесь](https://azure.microsoft.com/services/machine-learning/).

## <a name="prerequisites"></a>Предварительные требования
toocomplete этого руководства требуется:

* Учетная запись Azure. Если у вас нет учетной записи Azure, щелкните [здесь](https://azure.microsoft.com/pricing/free-trial/) подробные сведения о том, как toocreate бесплатную пробную учетную запись.
* Учетная запись AzureML. Если нет AzureML учетную запись, нажмите кнопку [здесь](https://studio.azureml.net/) подробные сведения о том, как toocreate бесплатную пробную учетную запись.
* Рабочая область Hello, службы и api_key для эксперимента машинного обучения Azure, развернутые как веб-службы. Нажмите кнопку [здесь](machine-learning-create-experiment.md) сведения о как поэкспериментировать toocreate AzureML. Нажмите кнопку [здесь](machine-learning-publish-a-machine-learning-web-service.md) сведения о как toodeploy AzureML поэкспериментировать веб-службы. Кроме того приложение A имеет инструкции toocreate и тестирования простых AzureML поэкспериментировать и развернуть его как веб-службы.

## <a name="create-an-api-management-instance"></a>Создание экземпляра API Management
Ниже приведены шаги использования API управления toomanage hello веб-службу машинного обучения Azure. Сначала создайте экземпляр службы. Войдите в toohello [классический портал](https://manage.windowsazure.com/) и нажмите кнопку **New** > **службы приложений** > **управления API**  >  **Создания**.

![create-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

Укажите уникальное значение в поле **URL-адрес**. В этом руководстве используется **demoazureml** — вам потребуется toochoose другим. Выберите требуемого hello **подписки** и **область** для вашего экземпляра службы. После выделения нужных элементов, нажмите кнопку "Далее" hello.

![create-service-1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

Укажите значение для hello **название организации**. В этом руководстве используется **demoazureml** — вам потребуется toochoose другим. Введите адрес электронной почты в hello **адрес электронной почты администратора** поля. Этот адрес электронной почты используется для получения уведомлений из системы управления API hello.

![create-service-2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

Щелкните флажок toocreate hello вашего экземпляра службы. *Он занимает toothirty минут для новой службы toobe создан*.

## <a name="create-hello-api"></a>Создать hello API
После создания экземпляра службы hello hello следующим шагом является toocreate hello API. API представляет набор операций, которые могут быть вызваны клиентскими приложениями. Операции API-интерфейса — tooexisting через прокси веб-службы. В этом руководстве создает интерфейсы API, toohello прокси существующих записей Ресурсов AzureML и BES веб-служб.

API-интерфейсы создаются и настраиваются с портала издателя hello API, который можно получить с помощью hello классический портал Azure. tooreach hello портала, выберите издателя вашего экземпляра службы.

![select-service-instance](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

Нажмите кнопку **управление** в hello классический портал Azure для службы управления API.

![manage-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

Нажмите кнопку **API-интерфейсы** из hello **API управления** меню hello слева, а затем нажмите **добавить API**.

![api-management-menu](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

Тип **AzureML демонстрация API** как hello **имя веб-API**. Тип **https://ussouthcentral.services.azureml.net** как hello **веб-URL-адрес службы**. Тип **azureml Демонстрация** как hello **суффикс URL-адрес API**. Проверьте **HTTPS** как hello **URL-адрес API** схемы. Выберите **Starter** (Начальный комплект) в поле **Продукты**. По завершении нажмите кнопку **Сохранить** toocreate hello API.

![add-new-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-hello-operations"></a>Добавьте операции hello
Нажмите кнопку **операция добавления** toothis tooadd операции API.

![add-operation](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

Hello **новую операцию** окна будут отображены и hello **подписи** вкладка будет выбран по умолчанию.

## <a name="add-rrs-operation"></a>Добавление операции RRS
Сначала создайте операцию для hello службы AzureML записи Ресурсов. Выберите **POST** как hello **HTTP-команду**. Тип **/services/ /workspaces/ {рабочей} {службы} / execute? api-version = {apiversion} & сведения = {сведения}** как hello **URL-адрес шаблона**. Тип **выполнение записи Ресурсов** как hello **отображаемое имя**.

![add-rrs-operation-signature](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

Нажмите кнопку **ответов** > **добавить** на hello слева и выберите **200 ОК**. Нажмите кнопку **Сохранить** toosave этой операции.

![add-rrs-operation-response](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a>Добавление операций BES
Снимки экрана, не включаются в hello BES операций, как они являются очень похожа toothose для добавления записей Ресурсов операции hello.

### <a name="submit-but-not-start-a-batch-execution-job"></a>Отправка (но не запуск) задачи выполнения пакетов
Нажмите кнопку **операция добавления** tooadd hello AzureML BES операции toohello API. Выберите **POST** для hello **HTTP-команду**. Тип **/services/ /workspaces/ {рабочей} {службы} / заданий? api-version = {apiversion}** для hello **URL-адрес шаблона**. Тип **отправить BES** для hello **отображаемое имя**. Нажмите кнопку **ответов** > **добавить** на hello слева и выберите **200 ОК**. Нажмите кнопку **Сохранить** toosave этой операции.

### <a name="start-a-batch-execution-job"></a>Запуск задачи выполнения пакетов
Нажмите кнопку **операция добавления** tooadd hello AzureML BES операции toohello API. Выберите **POST** для hello **HTTP-команду**. Тип **/jobs/ /services/ {служба} /workspaces/ {рабочей} {jobid} / start? api-version = {apiversion}** для hello **URL-адрес шаблона**. Тип **запуск BES** для hello **отображаемое имя**. Нажмите кнопку **ответов** > **добавить** на hello слева и выберите **200 ОК**. Нажмите кнопку **Сохранить** toosave этой операции.

### <a name="get-hello-status-or-result-of-a-batch-execution-job"></a>Получить состояние hello или результат выполнения пакетного задания
Нажмите кнопку **операция добавления** tooadd hello AzureML BES операции toohello API. Выберите **получить** для hello **HTTP-команду**. Тип **/jobs/ /services/ {служба} /workspaces/ {рабочей} {jobid}? api-version = {apiversion}** для hello **URL-адрес шаблона**. Тип **состояние BES** для hello **отображаемое имя**. Нажмите кнопку **ответов** > **добавить** на hello слева и выберите **200 ОК**. Нажмите кнопку **Сохранить** toosave этой операции.

### <a name="delete-a-batch-execution-job"></a>Удаление задачи выполнения пакетов
Нажмите кнопку **операция добавления** tooadd hello AzureML BES операции toohello API. Выберите **удаление** для hello **HTTP-команду**. Тип **/jobs/ /services/ {служба} /workspaces/ {рабочей} {jobid}? api-version = {apiversion}** для hello **URL-адрес шаблона**. Тип **удалить BES** для hello **отображаемое имя**. Нажмите кнопку **ответов** > **добавить** на hello слева и выберите **200 ОК**. Нажмите кнопку **Сохранить** toosave этой операции.

## <a name="call-an-operation-from-hello-developer-portal"></a>Вызов операции из hello портал разработчиков
Операции могут вызываться непосредственно из портала разработчиков hello, который предоставляет удобный способ tooview и протестировать hello операции API-интерфейса. На этом шаге руководства вы будете вызывать hello **выполнение записи Ресурсов** метода, который был добавлен toohello **AzureML демонстрация API**. Нажмите кнопку **портал разработчиков** меню hello hello верхнему правому углу hello классического портала.

![developer-portal](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

Нажмите кнопку **API-интерфейсы** hello верхнем меню, и нажмите кнопку **AzureML демонстрация API** доступные операции toosee hello.

![demoazureml-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

Выберите **выполнение записи Ресурсов** для операции hello. Щелкните **Попробовать**.

![try-it](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

Параметры запроса, введите ваш **рабочей**, **службы**, **2.0** для hello **apiversion**, и **true**для hello **сведения**. Можно найти на **рабочей** и **службы** в мониторинга hello AzureML веб-службы (см. **проверить веб-службу hello** в приложении А).

В разделе Request headers (Заголовки запросов) щелкните **Добавить заголовок** и введите текст **Content-Type** и **application/json**. Затем щелкните **Добавить заголовок** и введите текст **Authorization** и **Bearer<YOUR AZUREML SERVICE API-KEY>**. Можно найти на **ключ api** в мониторинга hello AzureML веб-службы (см. **проверить веб-службу hello** в приложении А).

Тип **{«Входные данные»: {«input1»: {«ColumnNames»: [«Col2»] «значения»: [[«это хороший день»]]}}, «GlobalParameters»: {}}** для hello текст запроса.

![azureml-demo-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

Нажмите кнопку **Отправить**.

![Отправить](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

После вызова операции портал разработчиков hello отображает hello **запрошенный URL-адрес** внутренней службой hello hello **состояние ответа**, hello **заголовки ответа**, а также **содержимого отклика**.

![response-status](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a>Дополнение А — создание и тестирование простой веб-службы AzureML
### <a name="creating-hello-experiment"></a>Создание экспериментов hello
Ниже перечислены основные шаги hello для создания простого эксперимента машинного обучения Azure и развертывания его как веб-службы. Hello web service принимает в качестве входного столбца произвольного текста и возвращает набор возможностей, представленных в виде целых чисел. Например:

| текст | Хэшированный текст |
| --- | --- |
| This is a good day |1 1 2 2 0 0 2 1 |

Во-первых, с помощью браузера по своему усмотрению, перейдите к: [https://studio.azureml.net/](https://studio.azureml.net/) и введите ваш toolog учетные данные в. Затем создайте пустой эксперимент.

![search-experiment-templates](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

Переименуйте ее слишком**SimpleFeatureHashingExperiment**. Разверните список **Saved Datasets** (Сохраненные наборы данных) и перетащите элемент **Book Reviews from Amazon** (Обзоры книг на Amazon) в свой эксперимент.

![simple-feature-hashing-experiment](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

Разверните списки **Преобразование данных** и **Manipulation** (Работа с данными) и перетащите элемент **Select Columns in Dataset** (Выбор столбцов в наборе данных) в свой эксперимент. Подключение **рецензий из Amazon** слишком**Выбор столбцов в наборе данных**.

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

Последовательно щелкните **Select Columns in Dataset** (Выбор столбцов в наборе данных), **Launch column selector** (Запустить средство выбора столбцов), а затем выберите **Col2**. Щелкните флажок tooapply hello эти изменения.

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

Разверните **анализа текста** и перетащите **хэширование признаков** на hello эксперимента. Подключение **Выбор столбцов в наборе данных** слишком**хэширование признаков**.

![connect-project-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

Тип **3** для hello **разрядность хэширования**. Будет создано 8 столбцов (23).

![hashing-bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

На этом этапе вы можете tooclick **запуска** tootest hello эксперимента.

![Запустить](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a>Создание веб-службы
Теперь создайте веб-службу. Разверните список **Веб-служба** и перетащите элемент **Входные данные** в свой эксперимент. Подключение **ввода** слишком**хэширование признаков**. Перетащите в свой эксперимент также элемент **Вывод** . Подключение **вывода** слишком**хэширование признаков**.

![output-to-feature-hashing](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

Щелкните **Опубликовать веб-службу**.

![publish-web-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

Нажмите кнопку **Да** toopublish hello эксперимента.

![yes-to-publish](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-hello-web-service"></a>Проверить веб-службу hello
Веб-служба AzureML состоит из конечных точек RSS (служба запросов и ответов) и BES (служба выполнения пакетов). Конечные точки RSS предназначены для синхронного выполнения задач. Конечные точки BES — для асинхронного. tootest веб-службы с источником Python образец hello ниже, может потребоваться toodownload и hello установки пакета Azure SDK для Python (см.: [как tooinstall Python](../python-how-to-install.md)).

Необходимо также hello **рабочей**, **службы**, и **api_key** из эксперимента для hello Образец исходного кода ниже. Hello рабочей области и службы можно найти, выбрав **запрос-ответ** или **Пакетное выполнение** для эксперимента в hello мониторинга веб-службы.

![find-workspace-and-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

Можно найти hello **api_key** , щелкнув эксперимента в hello мониторинга веб-службы.

![find-api-key](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a>Тестирование конечной точки RRS
##### <a name="test-button"></a>Кнопка тестирования
Конечная точка записей Ресурсов hello легко tootest — tooclick **тест** на hello мониторинга веб-службы.

![test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

В поле **col2** введите текст **This is a good day**. Нажмите кнопку Далее hello.

![enter-data](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

Отобразится примерно такой текст:

![sample-output](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a>Пример кода
Другой способ tootest вашей записи Ресурсов — в коде клиента. Если щелкнуть **запрос ответ** снизу hello панели мониторинга и прокрутки toohello, вы увидите пример кода для C#, Python и R. Также вы увидите hello синтаксис запроса записей Ресурсов hello, включая URI запроса hello, заголовки и текст.

В этом руководстве приведен рабочий экземпляр кода на языке Python. Вам потребуется toomodify с hello **рабочей**, **службы**, и **api_key** из эксперимента.

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
        print("hello request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a>Тестирование конечной точки BES
Нажмите кнопку **Пакетное выполнение** нижней toohello панели мониторинга и прокрутите страницу приветствия. Вы увидите пример кода для C#, Python и R. Вы также увидите hello синтаксис hello toosubmit запросы BES задания, запуск задания, состояние hello или результатам задания и удалить задание.

В этом руководстве приведен рабочий экземпляр кода на языке Python. Требуется toomodify его с hello **рабочей**, **службы**, и **api_key** из эксперимента. Кроме того, вы должны toomodify hello **имя учетной записи хранения**, **ключ учетной записи хранения**, и **имя контейнера хранилища**. Наконец, необходимо будет расположение hello toomodify hello **входной файл** и расположение hello hello **выходной файл**.

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH hello API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH hello LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH hello LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("hello request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading hello result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written toohello file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("hello results for " + outputName + " are available at hello following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "hello results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading hello input tooblob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded hello input tooblob storage"
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
    print("Submitting hello job...")
    # submit hello job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove hello enclosing double-quotes
    print("Job ID: " + job_id)
    # start hello job
    print("Starting hello job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking hello job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in hello follwing code
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
