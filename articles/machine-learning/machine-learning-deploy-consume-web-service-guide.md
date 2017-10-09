---
title: "Развертывание и использование веб-служб машинного обучения Azure | Документация Майкрософт"
description: "Ресурсы для развертывания и использования веб-служб."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 539c2abb053a0f981be0374defe45cf4d96b740b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a>Развертывание и использование веб-служб Машинного обучения Azure
Рабочие процессы машинного обучения toodeploy машинного обучения Azure и модели можно использовать как веб-службы. Эти веб-службы затем можно использовать toocall hello машинного обучения моделей из приложений через hello Internet toodo прогнозов в реальном времени или в пакетном режиме. Поскольку категории RESTful hello веб-служб, их можно вызывать из различных языков программирования и платформах, например .NET и Java и из приложений, таких как Excel.

Hello далее разделах содержатся ссылки toowalkthroughs, кода и документации toohelp приступить к работе.

## <a name="deploy-a-web-service"></a>Развертывание веб-службы
### <a name="with-azure-machine-learning-studio"></a>С помощью Студии машинного обучения Azure
Портал веб-службы Microsoft Azure Machine Learning hello и студии машинного обучения поможет вам развернуть и управлять веб-службы без написания кода.

Hello следующие ссылки предоставляют общие сведения о том, как toodeploy веб-службу:

* Общие сведения о том, как toodeploy новую веб-службу, которая основана на Azure Resource Manager отображается [развернуть веб-службу](machine-learning-webservice-deploy-a-web-service.md).
* Пошаговые инструкции о том, как toodeploy веб-службы, в разделе [развертывания веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).
* Полное Пошаговое руководство о том, как toocreate и развернуть веб-службы см. в разделе [шаг 1 пошагового руководства: Создание рабочей области машинного обучения](machine-learning-walkthrough-1-create-ml-workspace.md).
* Конкретные примеры развертывания веб-службы см. в следующих статьях:

  * [Пошаговое руководство шаг 5: Развертывание веб-службы машинного обучения Azure hello](machine-learning-walkthrough-5-publish-web-service.md)
  * [Как toodeploy веб-сайт службы toomultiple областей](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a>С помощью интерфейсов API поставщика ресурсов веб-служб (интерфейсов API Azure Resource Manager)
поставщик ресурсов Hello машинного обучения Azure для веб-служб обеспечивает развертывания и управления веб-служб с помощью вызовов REST API. Дополнительные сведения см. в статье [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) (Веб-служба машинного обучения (REST)).

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a>С помощью командлетов PowerShell
Поставщик ресурсов Машинного обучения Azure для веб-служб позволяет развертывать веб-службы и управлять ими с помощью командлетов PowerShell.

командлеты hello toouse, необходимо сначала войти в учетную запись Azure из среды PowerShell hello tooyour с помощью hello [AzureRmAccount добавить](https://msdn.microsoft.com/library/mt619267.aspx) командлета. Если вы не знакомы с как toocall PowerShell команды основаны на диспетчера ресурсов см. в разделе [с помощью Azure PowerShell с помощью диспетчера ресурсов Azure](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).

tooexport вашей прогнозной поэкспериментировать, используйте [этот пример кода](https://github.com/ritwik20/AzureML-WebServices). После создания файла .exe hello из кода hello, можно ввести:

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

Запуск приложения hello создает JSON шаблона веб-службы. шаблон toodeploy hello toouse веб-службы, необходимо добавить hello следующую информацию:

* Имя и ключ учетной записи хранения.

    Имя учетной записи хранения hello и ключ можно получить из любой hello [портал Azure](https://portal.azure.com/) или hello [классический портал Azure](http://manage.windowsazure.com/).
* Идентификатор плана предложения.

    Можно получить идентификатор плана hello hello [веб-службы Azure Machine Learning](https://services.azureml.net) портала, войдя в систему и выбрать имя плана.

Добавить шаблон toohello JSON как дочерние элементы hello *свойства* узел на hello же уровня как hello *MachineLearningWorkspace* узла.

Ниже приведен пример:

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

См. следующие статьи hello и образцы кода для получения дополнительных сведений:

* [Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) (Командлеты Машинного обучения Azure) на сайте MSDN.
* Пример [пошагового руководства](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) на сайте GitHub.

## <a name="consume-hello-web-services"></a>Использование hello веб-служб
### <a name="from-hello-azure-machine-learning-web-services-ui-testing"></a>Из hello Azure машины обучения веб-интерфейса служб (тестирования)
Можно проверить веб-службу из веб-службы Azure Machine Learning портала hello. Сюда входят тестирование службы hello запрос-ответ (RR) и интерфейсы службы пакетного выполнения (BES).

* [Развертывание новой веб-службы](machine-learning-webservice-deploy-a-web-service.md)
* [Развертывание веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md)
* [Пошаговое руководство шаг 5: Развертывание веб-службы машинного обучения Azure hello](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a>Из Excel
Можно загрузить шаблон Excel, использующего hello веб-службы:

* [Использование веб-службы Машинного обучения Azure в Excel](machine-learning-consuming-from-excel.md)
* [Надстройка Excel для веб-служб машинного обучения Azure](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a>Из клиента на основе REST
Веб-службы Машинного обучения Azure представляют собой интерфейсы API RESTful. Можно использовать эти API-интерфейсы из различных платформ, таких как .NET, Python, R, Java, т. д. hello **использование** страницы веб-службы на hello [портал веб-службы Microsoft Azure Machine Learning](https://services.azureml.net) образец код, который поможет вам приступить к работе. Дополнительные сведения см. в разделе [как tooconsume в Azure Machine обучения, веб-службу](machine-learning-consume-web-services.md).
