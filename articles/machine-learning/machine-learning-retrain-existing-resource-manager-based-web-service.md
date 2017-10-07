---
title: "существующий прогнозной aaaRetrain веб-службы | Документы Microsoft"
description: "Узнайте, как tooretrain модели и обновление hello web toouse службы hello вновь обученной модели машинного обучения Azure."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: fb0760d0a2adc34fc5f3df1ae41bdac075f91bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a>Переобучение прогнозной веб-службы
В этом документе описываются hello переподготовки процесс для hello следующие сценарии:

* Есть обучающий и прогнозный эксперименты, развернутые в качестве веб-службы, готовой к эксплуатации.
* У вас есть новые данные, которые должны вашей прогнозной web service toouse tooperform его оценки.

> [!NOTE] 
> toodeploy новую веб-службу, необходимо иметь достаточные разрешения в toowhich hello подписки вы развертывание hello веб-службы. Дополнительные сведения см. в разделе [управление веб-службы с помощью портала веб-службы Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

Начиная с существующей веб-службы и экспериментов, требуется toofollow следующие действия:

1. Обновление модели hello.
   1. Измените ваш tooallow эксперимента обучения для web service входов и выходов.
   2. Развертывание эксперимента обучения hello повторную веб-службы.
   3. Модель эксперимента обучения hello пакетного выполнения службы (BES) tooretrain hello.
2. Используйте прогнозирующее эксперимента hello Azure Machine Learning PowerShell командлеты tooupdate hello.
   1. Войдите в tooyour учетной записи диспетчера ресурсов Azure.
   2. Получите определение hello веб-службы.
   3. Экспорт определения hello веб-службы как JSON.
   4. Обновление hello ссылка toohello ilearner большой двоичный объект в hello JSON.
   5. Импортируйте hello JSON в определении веб-службы.
   6. Обновите hello веб-службы с помощью нового определения веб-службы.

## <a name="deploy-hello-training-experiment"></a>Разверните эксперимент обучения hello
toodeploy эксперимента обучения hello повторную веб-службы, необходимо добавить модели веб-служб входы и выходы toohello. Подключив *вывод веб-службы* toohello эксперименте модуль  *[Обучение модели] [ train-model]*  модуля, включите hello эксперимента обучения tooproduce новый обученную модель, которую можно использовать в эксперименте прогнозирования. Если у вас есть *модель оценки* модуля, вы также можете присоединить web service вывода tooget hello результаты оценки в качестве выходных данных.

tooupdate эксперимента обучения:

1. Подключения *Web Service входной* данные tooyour модуля ввода (например, *Очистка недостающих данных* модуля). Как правило, требуется tooensure, обрабатываемых в качестве входных данных hello таким же, как и исходный обучающих данных.
2. Подключение *вывод веб-службы* выходные данные модуля toohello из вашего *Обучение модели* модуля.
3. При наличии *модель оценки* модуля вы результаты оценки toooutput hello, необходимо подключиться *вывод веб-службы* выходные данные модуля toohello из вашего *модель оценки* модуль.

Запустите эксперимент.

После этого необходимо развернуть эксперимента обучения hello как веб-службу, которая создает обученной модели и результаты оценки модели.  

Внизу hello холст эксперимента hello, нажмите кнопку **настройки веб-службы**и выберите **развертывания [новое] веб-службы**. Откроется портал веб-службы Azure Machine Learning Hello toohello **развертывание веб-службы** страницы. Введите имя веб-службы, выберите план платежей, а затем щелкните **Развернуть**. Hello способ выполнения пакета можно использовать только для создания обученных моделей.

## <a name="retrain-hello-model-with-new-data-by-using-bes"></a>Обучение модели hello новыми данными, с помощью СРЕД
В этом примере мы используем hello toocreate C#, переподготовки приложения. Можно также использовать Python или R tooaccomplish образец кода эта задача.

toocall hello переподготовки API-интерфейсы:

1. Создайте консольное приложение C# в Visual Studio (**Создать** > **Проект** > **Visual C#** > **Классический рабочий стол Windows** > **Консольное приложение (.NET Framework**).
2. Войдите в систему toohello портала машины обучения веб-служб.
3. Щелкните hello веб-службы, которым вы работаете.
4. Щелкните **Consume**(Использование).
5. Внизу hello hello **использование** страницы в hello **образец кода** щелкните **пакета**.
6. Скопируйте hello пример кода C# для пакетного выполнения и вставьте его в файл Program.cs hello. Убедитесь, что это пространство имен hello остается без изменений.

Добавьте пакет NuGet hello Microsoft.AspNet.WebApi.Client, как указано в комментариях hello. tooMicrosoft.WindowsAzure.Storage.dll ссылки tooadd hello, сначала необходимо tooinstall hello [клиентской библиотеки для служб хранилища Azure](https://www.nuget.org/packages/WindowsAzure.Storage).

Hello следующем снимке экрана показано hello **использование** портале веб-службы Azure Machine Learning hello.

![Страница Consume (Использование)][1]

### <a name="update-hello-apikey-declaration"></a>Обновление декларации apikey hello
Найдите hello **apikey** объявление:

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

В hello **потребления основные сведения о** раздел hello **использование** найдите hello первичный ключ и скопируйте его toohello **apikey** объявления.

### <a name="update-hello-azure-storage-information"></a>Обновить сведения о хранилище Azure hello
Hello BES образец кода отправляет файл с локального диска (например, «C:\temp\CensusIpnput.csv») tooAzure хранилища, обрабатывает его и записывает hello результаты назад tooAzure хранилища.  

сведения о tooupdate hello хранилища Azure, необходимо получить hello учетной записи хранения, имя ключа и контейнер сведения для учетной записи хранения из классического портала Azure hello и correspondi hello обновления после выполнения эксперимента, Здравствуйте, возникающие в рабочий процесс должен быть примерно toohello следующее:

![Итоговый рабочий процесс после запуска][4]ng значения в коде hello.

1. Войдите в систему toohello классический портал Azure.
2. В столбце hello навигации слева щелкните **хранения**.
3. Из списка hello учетных записей хранения выберите один toostore hello повторное Обучение модели.
4. Внизу hello страницы приветствия щелкните **управление ключами доступа**.
5. Скопируйте и сохраните hello **первичный ключ доступа** и hello закрыть диалоговое окно.
6. В начале hello страницы приветствия, нажмите кнопку **контейнеры**.
7. Выберите существующий контейнер, или создайте новую и сохраните имя hello.

Найдите hello *StorageAccountName*, *StorageAccountKey*, и *StorageContainerName* объявления и обновлять значения hello, которые были сохранены из классического портала hello .

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

Также необходимо убедиться, что в расположении hello, указанных в коде hello доступен hello входного файла.

### <a name="specify-hello-output-location"></a>Укажите расположение выходных данных hello
При указании расположения вывода hello в полезных данных запроса hello hello расширение файла hello, которая указана в *RelativeLocation* должен быть указан как `ilearner`. См. следующий пример hello.

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you want toouse for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

Hello ниже приведен пример выходных данных переподготовки: ![переподготовки выходных данных][6]

## <a name="evaluate-hello-retraining-results"></a>Привет, переподготовки результаты оценки
При запуске приложения hello hello выводятся hello URL-адрес и маркер подписи общего доступа, которые результаты оценки необходимости tooaccess hello.

Можно просмотреть результаты производительности hello hello повторное Обучение модели путем объединения hello *BaseLocation*, *RelativeLocation*, и *SasBlobToken* из hello выходных результатов для *output2* (как показано в предыдущем переподготовки изображения вывода hello) и вставка hello полный URL-адрес в адресной строке браузера hello.  

Проверьте результаты toodetermine hello ли вновь обученной модели hello выполняет также достаточно hello tooreplace один существующий.

Копировать hello *BaseLocation*, *RelativeLocation*, и *SasBlobToken* из hello выходные результаты.

## <a name="retrain-hello-web-service"></a>Обучение hello веб-службы
При веб-службу, обучение, следует обновить hello прогнозной модели веб-служб определения tooreference hello новый обучения. Hello определение веб-службы – это внутреннее представление hello обученной модели hello веб-службы и не может быть непосредственно изменен. Убедиться, что для прогнозирования эксперимента и не эксперимента обучения извлекаются hello определение веб-службы.

## <a name="sign-in-tooazure-resource-manager"></a>Войдите в tooAzure диспетчера ресурсов
Необходимо сначала войти в учетную запись Azure из среды PowerShell hello tooyour с помощью hello [AzureRmAccount добавить](https://msdn.microsoft.com/library/mt619267.aspx) командлета.

## <a name="get-hello-web-service-definition-object"></a>Получение hello объекта определения веб-службы
Затем следует получить hello объекта определения веб-службы путем вызова hello [Get AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) командлета.

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

toodetermine hello группу ресурсов с именем существующей веб-службе, используйте командлет Get-AzureRmMlWebService hello без параметров toodisplay hello веб-служб в вашей подписке. Найдите hello веб-службы, а затем найдите на идентификатор его web service. Hello имя группы ресурсов hello — hello четвертый элемент в качестве идентификатора hello сразу после hello *resourceGroups* элемента. В следующем примере hello имя группы ресурсов hello — по умолчанию-MachineLearning-SouthCentralUS.

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

Кроме того, toodetermine hello группу ресурсов с именем существующей веб-службы, войдите в портал веб-службы Azure Machine Learning toohello. Выберите веб-службу hello. Имя группы ресурсов Hello — пятый элемент hello hello и URL-адрес веб-службы hello, сразу после hello *resourceGroups* элемента. В следующем примере hello имя группы ресурсов hello — по умолчанию-MachineLearning-SouthCentralUS.

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-object-as-json"></a>Экспорт объекта hello определение веб-службы как JSON
Определение hello toomodify hello обученной модели toouse hello вновь обучения модели, необходимо сначала использовать hello [AzureRmMlWebService экспорта](https://msdn.microsoft.com/library/azure/mt767935.aspx) tooexport командлет его файла tooa формат JSON.

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob"></a>Обновить hello ilearner toohello эталонный BLOB-объект
В средствах hello найдите hello [обученной модели], обновление hello *uri* значение в hello *locationInfo* узел с hello URI большого двоичного объекта ilearner hello. Hello URI создается путем объединения hello *BaseLocation* и hello *RelativeLocation* из вывода hello hello BES повторную вызова.

     "asset3": {
        "name": "Retrain Sample [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition-object"></a>Импортируйте hello JSON в объект определения веб-службы
Необходимо использовать hello [AzureRmMlWebService импорта](https://msdn.microsoft.com/library/azure/mt767925.aspx) hello tooconvert командлет изменения файла JSON обратно в объект определения веб-службы, которые можно использовать tooupdate hello predicative эксперимента.

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service"></a>Обновить hello веб-службы
Наконец, используйте hello [AzureRmMlWebService обновление](https://msdn.microsoft.com/library/azure/mt767922.aspx) tooupdate командлет hello прогнозной эксперимента.

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
