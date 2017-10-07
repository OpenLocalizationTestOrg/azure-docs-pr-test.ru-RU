---
title: "aaaConsume веб-службы машинного обучения с веб-приложения шаблона | Документы Microsoft"
description: "Используйте веб-шаблона приложения в Azure Marketplace tooconsume прогнозирующей веб-службы в машинном обучении Azure."
keywords: "веб-служба, ввод в эксплуатацию, REST API, машинное обучение"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e0d71683-61b9-4675-8df5-09ddc2f0d92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;raymondl
ms.openlocfilehash: 1199377bead470807d58ca7f7a667175cbb88450
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-azure-machine-learning-web-service-with-a-web-app-template"></a>Использование веб-службы машинного обучения Azure с шаблоном веб-приложения

Один раз после разработки прогнозной модели и развернуть его как веб-службу Azure с помощью студии машинного обучения, или с помощью средств, таких как R или Python, можно открыть hello развернутых моделей с помощью REST API.

Существует несколько способов tooconsume hello REST API и доступа hello веб-службы. Например, можно написать пользовательское приложение в C#, R, или Python, с помощью hello пример кода, созданный для вас при развертывании hello веб-службы (в hello [службы веб-портал для машины обучения](https://services.azureml.net/quickstart) или в hello мониторинга веб-службы в Студия машинного обучения). Или можно использовать hello образца электронной таблицы Microsoft Excel при hello то же время.

Но hello tooaccess быстрее и проще всего, является веб-службу через hello веб-приложения шаблоны доступны в hello [Azure Web App Marketplace](https://azure.microsoft.com/marketplace/web-applications/all/).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-azure-machine-learning-web-app-templates"></a>Hello Azure Machine Learning веб-приложения шаблонов
Hello веб-приложения шаблоны доступны в hello Azure Marketplace можно создавать пользовательские веб-приложения, который знает входных данных веб-службы и ожидаемые результаты. Все, что нужно toodo — предоставить hello web app доступа tooyour веб-службы и данных, а шаблон hello hello rest.

Доступны два шаблона:

* [шаблон веб-приложения службы «запрос — ответ» Azure ML;](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/)
* [шаблон веб-приложения службы пакетного выполнения Azure ML.](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/)

Каждый шаблон создает образец приложения ASP.NET, с помощью API URI hello и ключ для веб-службу и развертывает ее как tooAzure веб-сайта. шаблон запрос-ответ службы (RR) Hello создает веб-приложения, позволяющий toosend один ряд данных toohello web service tooget один результат. шаблон службы пакетного выполнения (BES) Hello создает веб-приложения, который позволяет вам toosend большого количества строк данных tooget несколько результатов.

Без написания кода является обязательным toouse этих шаблонов. Необходимо только указать hello ключ API и URI и hello шаблона построения приложение hello автоматически.

ключ hello API tooget и URI запроса для веб-службы:

1. В hello [веб-портале служб](https://services.azureml.net/quickstart), веб-службу, щелкните **веб-службы** вверху hello. А для классической веб-службы щелкните **Classic Web Services** (Классические веб-службы).
2. Щелкните hello веб-службы требуется tooaccess.
3. Классического веб-службы щелкните конечную точку hello требуется tooaccess.
4. Нажмите кнопку **использование** вверху hello.
5. Копировать hello **основной** или **вторичный ключ** и сохраните его.
6. Если вы создаете шаблон запрос-ответ службы (RR), скопируйте hello **запрос-ответ** URI и сохраните его. При создании шаблона службы пакетного выполнения (BES), скопируйте hello **пакетных запросов** URI и сохраните его.


## <a name="how-toouse-hello-request-response-service-rrs-template"></a>Как toouse hello шаблон запрос-ответ службы (RR)
Выполните эти шаги toouse hello записей Ресурсов веб-приложения шаблона, как показано в hello следующие схемы.

![Процесс toouse записей Ресурсов веб-шаблона][image1]


<!--    ![API Key][image3] -->

<!-- This value will look like this:
   
        https://ussouthcentral.services.azureml.net/workspaces/<workspace-id>/services/<service-id>/execute?api-version=2.0&details=true
   
    ![Request URI][image4] -->

1. Go toohello [портал Azure](https://portal.azure.com), **входа**, нажмите кнопку **New**, поиска и выбора **веб-приложения Azure ML запрос-ответ службы**, нажмите кнопку **Создания**. 
   
   * Присвойте веб-приложению уникальное имя. Hello URL-адрес веб-приложения hello будет это имя, за которым следует `.azurewebsites.net.` например,`http://carprediction.azurewebsites.net.`
   * Выберите hello подписки Azure и службы, под которыми работает веб-службу.
   * Щелкните **Создать**.
     
     ![Создание веб-приложения][image5]

4. После завершения развертывания веб-приложения hello Azure щелкните hello **URL-адрес** hello веб-страницы параметров приложения в Azure, или введите URL-адрес hello в веб-браузере. Например, `http://carprediction.azurewebsites.net.`
5. Здравствуйте, когда веб-приложение первый выполняется он запросит hello **URL-адрес Post API** и **ключ API**.
   Введите значения hello, сохраненный ранее (**URI запроса** и **ключ API**соответственно).
     
     Нажмите кнопку **Submit**(Отправить).
     
     ![Введите Post URI и ключ API][image6]

6. Hello web app отображает его **веб-приложение конфигурация** страницы с помощью параметров hello текущей веб-службы. Здесь можно изменять параметры toohello, используемые веб-приложения hello.
   
   > [!NOTE]
   > Здесь параметры hello только изменение действует для этого веб-приложения. Он не изменяет параметры по умолчанию hello веб-службу. Например, если изменения hello **описание** здесь не будет изменена hello описание, отображаемое на hello мониторинга веб-службы в студии машинного обучения.
   > 
   > 
   
    После завершения нажмите кнопку **сохранить изменения**, а затем нажмите кнопку **Go tooHome страницы**.

7. Из hello домашней страницы, которое можно ввести значения toosend tooyour веб-службы. Нажмите кнопку **отправить** после завершения и будет возвращен результат hello.

Если требуется, чтобы tooreturn toohello **конфигурации** страницы, перейдите toohello `setting.aspx` страницы приветствия веб-приложения. Например: `http://carprediction.azurewebsites.net/setting.aspx.` запрашиваемые tooenter hello API ключ будет снова — нужно что tooaccess hello страницы и обновить параметры hello.

Можно остановить, перезапустить или удалить веб-приложение hello в hello портал Azure, такие как веб-приложения. При условии, что он работает можно просмотреть toohello домашний веб-адрес и введите новые значения.

## <a name="how-toouse-hello-batch-execution-service-bes-template"></a>Как toouse hello шаблона службы пакетного выполнения (BES)
Можно использовать hello BES веб-приложения шаблона в hello таким же способом, как шаблон hello записей Ресурсов, за исключением hello веб-приложения, созданный разрешить toosubmit несколько строк данных и получать несколько результатов.

Hello входных значений для пакетного выполнения веб-службы могут поступать из хранилища Azure или локальный файл; Hello результаты сохраняются в контейнер хранилища Azure.
Таким образом, вам потребуется выполнить необходимые результаты, возвращенные веб-приложения hello hello toohold контейнер хранилища Azure, и потребуется tooget входные данные готовы.

![Обработать toouse BES веб-шаблона][image2]

1. Выполните hello же hello toocreate процедуры BES веб-приложения, как и для записи Ресурсов шаблона hello, за исключением go слишком[Azure ML пакетного выполнения службы веб-приложения шаблона](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/) tooopen hello BES шаблона в Azure Marketplace и нажмите кнопку **Создание веб-приложения** .

2. toospecify место hello результаты, сохраненные, введите сведения о контейнере назначения hello на hello веб-приложения домашней страницы. Также укажите, где hello веб-приложения можно получить hello входных значений, либо в локальный файл или контейнер хранилища Azure.
   Нажмите кнопку **Submit**(Отправить).
   
    ![Сведения о хранилище][image7]

веб-приложения Hello, отображается страница с состоянием задания.
После завершения задания hello будет предоставляться расположение hello hello результатов в хранилище больших двоичных объектов. Также имеется возможность загрузки локального файла hello результаты tooa hello.

## <a name="for-more-information"></a>Дополнительные сведения
Дополнительные сведения о toolearn...

* Создание эксперимента машинного обучения в Студии машинного обучения — см. статью [Руководство по машинному обучению. Создание первого эксперимента по обработке и анализу данных в Студии машинного обучения Azure](machine-learning-create-experiment.md).
* toodeploy вашей машинного обучения поэкспериментировать веб-службы. в статье [развертывание на веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md)
* другие способы tooaccess веб-службу. в разделе [как tooconsume Azure машины обучения, веб-службы](machine-learning-consume-web-services.md)

[image1]: media/machine-learning-consume-web-service-with-web-app-template/rrs-web-template-flow.png
[image2]: media/machine-learning-consume-web-service-with-web-app-template/bes-web-template-flow.png
[image3]: media/machine-learning-consume-web-service-with-web-app-template/api-key.png
[image4]: media/machine-learning-consume-web-service-with-web-app-template/post-uri.png
[image5]: media/machine-learning-consume-web-service-with-web-app-template/create-web-app.png
[image6]: media/machine-learning-consume-web-service-with-web-app-template/web-service-info.png
[image7]: media/machine-learning-consume-web-service-with-web-app-template/storage.png
