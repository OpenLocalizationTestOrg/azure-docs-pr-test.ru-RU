---
title: "aaaRetrain новый машинного обучения Azure веб-службы с помощью PowerShell | Документы Microsoft"
description: "Узнайте, как tooprogrammatically повторного обучения моделей и обновления hello web service toouse hello вновь обученной модели в машинном обучении Azure с помощью командлетов PowerShell для управления обучения машины hello."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: 3953a398-6174-4d2d-8bbd-e55cf1639415
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 5b77fa82cfe17f0b4e90007ef81c506ab712475b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-new-resource-manager-based-web-service-using-hello-machine-learning-management-powershell-cmdlets"></a>Обучение с помощью командлетов PowerShell для управления обучения машины hello новый диспетчер ресурсов на основе веб-службы
При веб-службу, обучение, следует обновить hello прогнозной модели веб-служб определения tooreference hello новый обучения.  

## <a name="prerequisites"></a>Предварительные требования
Необходимо настроить обучающий и прогнозный эксперименты, как показано в статье [Программное переобучение моделей машинного обучения](machine-learning-retrain-models-programmatically.md). 

> [!IMPORTANT]
> Hello прогнозной эксперимента необходимо развернуть как диспетчера ресурсов Azure (новая) на основе веб-службе машинного обучения. toodeploy новую веб-службу, необходимо иметь достаточные разрешения в toowhich hello подписки вы развертывание hello веб-службы. Дополнительные сведения см. в разделе [управление веб-службы с помощью портала веб-службы Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

Дополнительную информацию о развертывании веб-служб см. в статье [Развертывание веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).

Этот процесс требует, что вы установили hello командлеты обучения машины Azure. Установка командлетов машинного обучения hello подробнее hello [обучения командлеты Azure машины](https://msdn.microsoft.com/library/azure/mt767952.aspx) ссылку на сайте MSDN.

Скопированный hello следующую информацию из hello переподготовки выходные данные:

* BaseLocation
* RelativeLocation

Hello выполнить действия, являются:

1. Войдите в tooyour учетной записи диспетчера ресурсов Azure.
2. Получить определение hello веб-службы
3. Экспорт hello определение веб-службы как JSON
4. Обновление hello ссылка toohello ilearner большой двоичный объект в hello JSON.
5. Импортировать hello JSON в определении веб-службы
6. Обновить hello веб-службы с помощью нового определения веб-службы

## <a name="sign-in-tooyour-azure-resource-manager-account"></a>Войдите в tooyour учетной записи диспетчера ресурсов Azure
Необходимо сначала войти в учетную запись Azure с hello среды PowerShell, с помощью hello tooyour [AzureRmAccount добавить](https://msdn.microsoft.com/library/mt619267.aspx) командлета.

## <a name="get-hello-web-service-definition"></a>Получить hello определение веб-службы
Затем следует получить hello веб-службы путем вызова hello [Get AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) командлета. Hello определение веб-службы имеет внутреннее представление hello обученной модели hello веб-службы и не может быть непосредственно изменен. Убедитесь, что при получении hello определение веб-службы для прогнозирования эксперимента и не эксперимента обучения.

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

toodetermine hello группу ресурсов с именем существующей веб-службе, используйте командлет Get-AzureRmMlWebService hello без параметров toodisplay hello веб-служб в вашей подписке. Найдите hello веб-службы, а затем найдите на идентификатор его web service. Hello имя группы ресурсов hello — hello четвертый элемент в качестве идентификатора hello сразу после hello *resourceGroups* элемента. В следующем примере hello имя группы ресурсов hello — по умолчанию-MachineLearning-SouthCentralUS.

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

Кроме того toodetermine hello группу ресурсов с именем существующей веб-службы в журнал на портале веб-службы Microsoft Azure Machine Learning toohello. Выберите веб-службу hello. Имя группы ресурсов Hello — пятый элемент hello hello и URL-адрес веб-службы hello, сразу после hello *resourceGroups* элемента. В следующем примере hello имя группы ресурсов hello — по умолчанию-MachineLearning-SouthCentralUS.

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-as-json"></a>Экспорт hello определение веб-службы как JSON
toomodify hello определения toohello Обучение модели toouse вновь Здравствуйте обученной модели, необходимо сначала использовать hello [AzureRmMlWebService экспорта](https://msdn.microsoft.com/library/azure/mt767935.aspx) tooexport командлет его tooa формат JSON-файла.

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob-in-hello-json"></a>Обновление hello ссылка toohello ilearner большой двоичный объект в hello JSON.
В средствах hello найдите hello [обученной модели], обновление hello *uri* значение в hello *locationInfo* узел с hello URI большого двоичного объекта ilearner hello. Hello URI создается путем объединения hello *BaseLocation* и hello *RelativeLocation* из вывода hello hello BES повторную вызова. Это обновляет hello путь tooreference hello новой обученной модели.

     "asset3": {
        "name": "Retrain Samp.le [trained model]",
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

## <a name="import-hello-json-into-a-web-service-definition"></a>Импортировать hello JSON в определении веб-службы
Необходимо использовать hello [AzureRmMlWebService импорта](https://msdn.microsoft.com/library/azure/mt767925.aspx) hello tooconvert командлет измененного JSON-файл обратно в определение веб-службы, которые можно использовать tooupdate hello определение веб-службы.

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service-with-new-web-service-definition"></a>Обновить hello веб-службы с помощью нового определения веб-службы
Наконец, можно использовать [AzureRmMlWebService обновление](https://msdn.microsoft.com/library/azure/mt767922.aspx) hello tooupdate командлет определение веб-службы.

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'  -ServiceUpdates $wsd

## <a name="summary"></a>Сводка
С помощью командлетов управления PowerShell обучения машины hello, нужно обновить hello обученной модели прогнозирования Включение сценариях, например веб-службы.

* Периодическое переобучение модели с использованием новых данных.
* Распределение toocustomers модели с целью hello. Однако обучение модели hello, используя свои собственные данные.

