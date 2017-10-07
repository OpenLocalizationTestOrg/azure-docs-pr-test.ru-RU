---
title: "aaaConnect tooa веб-службы обучения машины | Документы Microsoft"
description: "С помощью C# или Python подключаться tooan Azure машины обучения, веб-службы, с помощью ключа авторизации."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 59b07bab-b60f-48c4-a385-a162e50ec7c2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: garye
ROBOTS: NOINDEX
redirect_url: machine-learning-consume-web-services
redirect_document_id: True
ms.openlocfilehash: 0108e71e30a05539a8c0ee93d5aadb07e3d1efa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-azure-machine-learning-web-service"></a>Подключение веб-служба Azure Machine Learning tooan
Hello опыт разработки машинного обучения Azure является прогнозы веб-службы API toomake из входных данных в режиме реального времени или в пакетном режиме. Используйте прогнозы toocreate студии машинного обучения Azure и развертывания служб Azure Machine Learning Web.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

toolearn о том, как toocreate и развертывать веб-машины обучения службы с помощью студии машинного обучения:

* Учебник по toocreate эксперимента в студии машинного обучения. в статье [создать свой первый эксперимент](machine-learning-create-experiment.md).
* Дополнительные сведения о том, как toodeploy веб-службы, в разделе [развертывание веб-машины обучения службы](machine-learning-publish-a-machine-learning-web-service.md).
* Дополнительные сведения о машинного обучения в целом посетите hello [центр документации машинного обучения](https://azure.microsoft.com/documentation/services/machine-learning/).

## <a name="azure-machine-learning-web-service"></a>Веб-служба машинного обучения Azure
С hello Azure Machine Learning, веб-службы внешнее приложение взаимодействует с оценки модели машинного обучения рабочего процесса в режиме реального времени. Вызов веб-машины обучения службы возвращает результаты прогноза tooan внешнее приложение. toomake вызов веб-машины обучения службы передать ключ API, который создается при развертывании прогноз. Hello веб-машины обучения служба основана на REST является вариантом популярных архитектура веб-программирования проектов.

Машинное обучение Azure содержит два типа служб:

* Запрос-ответ службы (RR) — небольшую задержку, высокую масштабируемость службы, которая предоставляет интерфейс toohello без сохранения состояния модели созданы и развертываются из hello студии машинного обучения.
* Служба пакетного выполнения (BES) — асинхронная служба, оценивающая пакет записей данных.

Дополнительные сведения о веб-службах машинного обучения приведены в статье [Развертывание веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="get-an-azure-machine-learning-authorization-key"></a>Получение ключа авторизации машинного обучения Azure
При развертывании эксперимента ключи API создаются для hello веб-службы. Можно получить hello ключи из нескольких мест.

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a>Из портала веб-службы Microsoft Azure Machine Learning hello
Войдите в toohello [веб-службы Microsoft Azure Machine Learning](https://services.azureml.net) портала.

ключ hello API tooretrieve новый обучения машины веб-службы:

1. На портале веб-службы Azure Machine Learning hello щелкните **веб-службы** hello верхнем меню.
2. Щелкните hello веб-службы, для которого требуется ключ tooretrieve hello.
3. Hello верхнего меню **использование**.
4. Скопируйте и сохраните hello **первичный ключ**.

ключ hello API tooretrieve классический обучения машины веб-службы:

1. На портале веб-службы Azure Machine Learning hello щелкните **классического веб-служб** hello верхнем меню.
2. Щелкните hello веб-службы, с которым вы работаете.
3. Щелкните конечную точку hello, для которого требуется ключ tooretrieve hello.
4. Hello верхнего меню **использование**.
5. Скопируйте и сохраните hello **первичный ключ**.

### <a name="classic-web-service"></a>Классическая веб-служба
 Также можно извлечь ключ для классического веб-службы из студии машинного обучения или hello классический портал Azure.

#### <a name="machine-learning-studio"></a>Студия машинного обучения
1. В студии машинного обучения, нажмите кнопку **веб-службы** hello левой части экрана.
2. Щелкните веб-службу. Hello **ключ API** на hello **МОНИТОРИНГА** вкладки.

#### <a name="azure-classic-portal"></a>Классический портал Azure
1. Нажмите кнопку **МАШИННОГО ОБУЧЕНИЯ** hello левой части экрана.
2. Щелкните рабочую область hello, в котором находится веб-службу.
3. Щелкните **ВЕБ-СЛУЖБЫ**.
4. Щелкните веб-службу.
5. Щелкните конечную точку. Hello «API-ключ» не работает в правый нижний hello.

## <a id="connect"></a>Подключение tooa веб-машины обучения службы
Можно подключить tooa веб-машины обучения службы, с помощью любого языка программирования, которая поддерживает HTTP-запроса и ответа. Примеры на языках C#, Python и R можно просмотреть на странице справки веб-службы машинного обучения.

**Справка по API машинного обучения.** Страница справки по API машинного обучения Azure создается при развертывании веб-службы. См. статью [Шаг 5. Развертывание веб-службы машинного обучения Azure](machine-learning-walkthrough-5-publish-web-service.md).
Hello API обучения машины справки содержит сведения об прогноз веб-службы.

1. Щелкните hello веб-службы, с которым вы работаете.
2. Щелкните конечную точку hello, для которого требуется hello tooview страница справки по API.
3. Hello верхнего меню **использование**.
4. Нажмите кнопку **страница справки по API** hello запрос-ответ или конечные точки выполнения пакета.

**tooview API обучения машины справки для нового веб-службы**

В hello Azure машины обучения веб-служб портала:

1. Нажмите кнопку **веб-службы** hello верхнем меню.
2. Щелкните hello веб-службы, для которого требуется ключ tooretrieve hello.

Нажмите кнопку **использование** tooget hello идентификаторы URI для hello Reposonse запрос и службы выполнения пакета и образец кода на C#, R и Python.

Нажмите кнопку **Swagger API** tooget Swagger документации hello API-интерфейсы на основе вызова из hello предоставленный идентификаторы URI.

### <a name="c-sample"></a>Пример на языке C#
Используйте tooconnect tooa веб-машины обучения службы **HttpClient** ScoreData передачи. ScoreData содержит FeatureVector n мерный вектор числовые функции, представляющий hello ScoreData. Можно проверить подлинность службы машинного обучения toohello ключ API.

hello tooconnect tooa веб-машины обучения службы **Microsoft.AspNet.WebApi.Client** необходимо установить пакет NuGet.

**Установка Microsoft.AspNet.WebApi.Client NuGet в Visual Studio**

1. Опубликовать данные загрузки hello из UCI: dataset для взрослых 2 класса веб-службы.
2. Выберите **Инструменты** > **Диспетчер пакетов NuGet** > **Консоль диспетчера пакетов**.
3. Выберите **Установить пакет Microsoft.AspNet.WebApi.Client**.

**Образец кода hello toorun**

1. Опубликовать «пример 1: загрузить набора данных UCI: взрослого 2 класса dataset» эксперимент, являющееся частью коллекции машинного обучения образец hello.
2. Назначьте apiKey с ключом hello из веб-службы. См. раздел **Получение ключа авторизации Машинного обучения Azure** выше.
3. Назначьте serviceUri с hello URI запроса.

### <a name="python-sample"></a>Пример на Python
tooconnect tooa веб-машины обучения службы, используйте hello **urllib2** передачи ScoreData библиотеки. ScoreData содержит FeatureVector n мерный вектор числовые функции, представляющий hello ScoreData. Можно проверить подлинность службы машинного обучения toohello ключ API.

**Образец кода hello toorun**

1. Развертывание «пример 1: загрузить набора данных UCI: взрослого 2 класса dataset» эксперимент, являющееся частью коллекции машинного обучения образец hello.
2. Назначьте apiKey с ключом hello из веб-службы. В разделе hello **получить ключ авторизации машинного обучения Azure** раздел hello начале этой статьи.
3. Назначьте serviceUri с hello URI запроса.

