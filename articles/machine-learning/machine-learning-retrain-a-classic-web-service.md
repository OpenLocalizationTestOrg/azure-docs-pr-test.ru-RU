---
title: "aaaRetrain классического веб-службы | Документы Microsoft"
description: "Узнайте, как tooprogrammatically повторного обучения модели и обновление hello web service toouse hello вновь обученной модели в машинном обучении Azure."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: d3ba21ed75f02868535cb2fcac607643303a9554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-classic-web-service"></a>Переобучение классической веб-службы
Hello прогнозной веб-службы, развертываемые — оценки конечной точки по умолчанию hello. Конечные точки по умолчанию сохраняются в соответствии с hello исходного обучения и оценки экспериментов и поэтому hello обученной модели для конечной точки по умолчанию hello не может быть заменен. tooretrain hello веб-службы, необходимо добавить новую конечную точку веб-службу toohello. 

## <a name="prerequisites"></a>Предварительные требования
Вы уже настроили обучающий и прогнозный эксперименты, как показано в статье [Программное переобучение моделей машинного обучения](machine-learning-retrain-models-programmatically.md). 

> [!IMPORTANT]
> Hello прогнозной эксперимента необходимо развернуть как классический машинного обучения веб-службы. 
> 
> 

Дополнительную информацию о развертывании веб-служб см. в статье [Развертывание веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="add-a-new-endpoint"></a>Добавление новой конечной точки
Hello прогнозной веб-службы, который был развернут содержит оценки конечную точку, которая синхронизируется с исходной обучения hello и оценки экспериментов обученной модели по умолчанию. tooupdate вашей toowith новый обученной модели службы web необходимо создать новую конечную точку для оценки. 

toocreate новой конечной точки оценки, на hello прогнозной веб-службы, которая может быть обновлена с помощью обученной модели hello:

> [!NOTE]
> Убедитесь, что вы добавляете toohello hello конечную точку прогнозируемого веб-службы, hello обучения веб-службы. Если вы правильно установили обучающую и прогнозную веб-службы, вы увидите две отдельные веб-службы. Hello прогнозной веб-службы должно заканчиваться «[прогнозной exp.]».
> 
> 

Существует три способа, в которых можно добавить новую конечную точку веб-службу tooa:

1. Программным образом
2. С помощью портала hello веб-службы Microsoft Azure
3. Hello используйте классический портал Azure

### <a name="programmatically-add-an-endpoint"></a>Добавление конечной точки программно
Можно добавить оценки конечные точки, использующие hello кода примера, приведенного в этом [репозитории github](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).

### <a name="use-hello-microsoft-azure-web-services-portal-tooadd-an-endpoint"></a>Использование портала tooadd веб-службы Microsoft Azure hello конечной точки
1. В студии машинного обучения на столбце hello навигации слева, нажмите кнопку веб-служб.
2. Внизу hello hello мониторинга веб-службы, нажмите кнопку **Управление конечными точками preview**.
3. Щелкните **Добавить**.
4. Введите имя и описание для новой конечной точки hello. Выберите уровень ведения журнала hello и включена ли образец данных. Дополнительные сведения о ведении журнала см. в статье [Включение функции ведения журналов для веб-служб машинного обучения](machine-learning-web-services-logging.md).

### <a name="use-hello-azure-classic-portal-tooadd-an-endpoint"></a>Использовать hello Azure классического портала tooadd конечной точки
1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).
2. В левом меню hello, щелкните **машинного обучения**.
3. В поле "Имя" выберите рабочую область, а затем щелкните **Веб-службы**.
4. В поле "Имя" щелкните **Модель ценза [predictive exp.]**.
5. Внизу hello страницы приветствия щелкните **добавить конечную точку**. Дополнительные сведения о добавлении конечных точек см. в статье [Создание конечных точек](machine-learning-create-endpoint.md). 

## <a name="update-hello-added-endpoints-trained-model"></a>Обновление hello добавлены обученной модели конечной точки
Цикл процесса toocomplete hello, необходимо обновить hello обученной модели hello новую конечную точку, которая была добавлена.

* Если вы добавили hello новую конечную точку, с помощью классического портала Azure hello, можно щелкнуть hello новое имя конечной точки на портале hello, затем hello **UpdateResource** hello tooget URL-адрес, потребовалось бы модели tooupdate hello конечной точки ссылки.
* Если вы добавили hello конечной точки с использованием примера кода hello, в нем расположение определяется hello URL-адрес справки hello *HelpLocationURL* значение в выходных данных hello.

tooretrieve hello путь URL-адрес:

1. Скопируйте и вставьте hello URL-адрес в адресную строку браузера.
2. Щелкните ссылку hello обновления ресурса.
3. Скопируйте hello POST URL-адрес запроса PATCH hello. Например:
   
     URL-адрес запроса PATCH: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2

Теперь можно использовать hello обученной модели tooupdate hello оценки конечную точку, созданную ранее.

Следующий образец кода Hello показано, как toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*и конечная точка hello tooupdate ИСПРАВЛЕНИЯ URL-адрес.

    private async Task OverwriteModel()
    {
        var resourceLocations = new
        {
            Resources = new[]
            {
                new
                {
                    Name = "Census Model [trained model]",
                    Location = new AzureBlobDataReference()
                    {
                        BaseLocation = "https://esintussouthsus.blob.core.windows.net/",
                        RelativeLocation = "your endpoint relative location", //from hello output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from hello output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
                    }
                }
            }
        };

        using (var client = new HttpClient())
        {
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", apiKey);

            using (var request = new HttpRequestMessage(new HttpMethod("PATCH"), endpointUrl))
            {
                request.Content = new StringContent(JsonConvert.SerializeObject(resourceLocations), System.Text.Encoding.UTF8, "application/json");
                HttpResponseMessage response = await client.SendAsync(request);

                if (!response.IsSuccessStatusCode)
                {
                    await WriteFailedResponse(response);
                }

                // Do what you want with a successful response here.
            }
        }
    }

Hello *apiKey* и hello *endpointUrl* для hello вызов может быть получен из панели мониторинга конечной точки.

Здравствуйте, значение hello *имя* параметр в *ресурсы* должен hello соответствия ресурсов с именем hello сохранен обученной модели в эксперименте прогнозной hello. hello tooget имя ресурса:

1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).
2. В левом меню hello, щелкните **машинного обучения**.
3. В поле "Имя" выберите рабочую область, а затем щелкните **Веб-службы**.
4. В поле "Имя" щелкните **Модель ценза [predictive exp.]**.
5. Щелкните новую конечную точку hello, добавленными.
6. На панели мониторинга endpoint hello, нажмите кнопку **обновления ресурса**.
7. На странице документации по API обновление ресурсов hello hello веб-службы, можно найти hello **имя ресурса** под **обновляемых ресурсов**.

Если срок действия токена SAS истекает до завершения обновления hello конечной точки, необходимо выполнить GET с ИД задания hello tooobtain новый маркер.

После успешного выполнения кода hello hello новую конечную точку следует начать использовать hello повторное Обучение модели приблизительно через 30 секунд.

## <a name="summary"></a>Сводка
С помощью API-интерфейсы переподготовки "hello", вы можете обновить hello обученной модели прогнозирования Включение сценариев, таких как веб-службы:

* Периодическое переобучение модели с использованием новых данных.
* Распределение toocustomers модели с целью hello. Однако обучение модели hello, используя свои собственные данные.

## <a name="next-steps"></a>Дальнейшие действия
[Устранение неполадок hello переподготовки классического веб-службы машинного обучения Azure](machine-learning-troubleshooting-retraining-models.md)

