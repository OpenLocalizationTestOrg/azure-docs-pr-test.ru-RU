---
title: "aaaRetrain машинного обучения моделей программным способом | Документы Microsoft"
description: "Узнайте, как tooprogrammatically повторного обучения модели и обновление hello web service toouse hello вновь обученной модели в машинном обучении Azure."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: 7ae4f977-e6bf-4d04-9dde-28a66ce7b664
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raymondl;garye;v-donglo
ms.openlocfilehash: edbb64c08f7d9edf3c76e23e0cc7e14c0125d697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a>Программное переобучение моделей машинного обучения
В этом пошаговом руководстве вы узнаете, как tooprogrammatically обучение машины обучения веб-службы Azure с помощью C# и hello машины обучения Пакетное выполнение службы.

Повторное Обучение модели hello, следующие пошаговые руководства hello отображены как tooupdate hello модели в прогнозирующем веб-службы:

* При развертывании классического веб-службы на портале веб-службы обучения машины hello. в разделе [обучение классического веб-службы](machine-learning-retrain-a-classic-web-service.md). 
* Если вы развернули веб-службу, см. раздел [обучение новых веб-службы с помощью командлетов управления обучения машины hello](machine-learning-retrain-new-web-service-using-powershell.md).

Обзор hello переподготовки процесса см. в разделе [Обучение модели машинного обучения](machine-learning-retrain-machine-learning-model.md).

Если вы хотите toostart с существующие новый диспетчер ресурсов Azure на основе веб-службы см. в разделе [обучение существующих прогнозирующей веб-службы](machine-learning-retrain-existing-resource-manager-based-web-service.md).

## <a name="create-a-training-experiment"></a>Создание обучающего эксперимента
В этом примере используется «пример 5: обучение теста оценки для двоичной классификации: для взрослых набора данных» из примеров hello машинного обучения Microsoft Azure. 

эксперимент hello toocreate:

1. Войдите с tooMicrosoft студии машинного обучения Azure. 
2. Щелкните hello нижнем правом углу панели мониторинга hello **New**.
3. Выберите 5 образец hello образцы Microsoft.
4. toorename hello эксперименте вверху hello hello холст эксперимента, выберите имя эксперимента hello «пример 5: обучение теста оценки для двоичной классификации: для взрослых набора данных».
5. Введите "Модель ценза".
6. Внизу hello холст эксперимента hello, нажмите кнопку **запуска**.
7. Щелкните **Set Up Web Service** (Настроить веб-службу) и выберите **Retraining Web Service** (Переобучение веб-службы). 

Hello ниже показан эксперимент начальной hello.
   
   ![Исходный эксперимент][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a>Создание прогнозного эксперимента и его публикация в виде веб-службы
Теперь нужно создать прогнозный эксперимент.

1. Внизу hello холст эксперимента hello, нажмите кнопку **настройки веб-службы** и выберите **прогнозной веб-службы**. Это сохраняет hello модели как обученной модели и добавляет веб-службы: модули ввода и вывода. 
2. Щелкните **Выполнить**. 
3. После эксперимента hello закончит работу, нажмите кнопку **развертывание веб-службы [классический]** или **развертывания [новое] веб-службы**.

> [!NOTE] 
> toodeploy новую веб-службу, необходимо иметь достаточные разрешения в toowhich hello подписки вы развертывание hello веб-службы. Дополнительные сведения см. в разделе [управление веб-службы с помощью портала веб-службы Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

## <a name="deploy-hello-training-experiment-as-a-training-web-service"></a>Развертывание эксперимента обучения hello обучения веб-службы
tooretrain hello обученной модели, необходимо развернуть эксперимента обучения hello, созданный Retraining веб-службы. Эта веб-служба должна *вывод веб-службы* модуль подключен toohello  *[Обучение модели] [ train-model]*  модуль, может tooproduce toobe новый обученных моделей.

1. эксперимента обучения toohello tooreturn значок экспериментов hello hello левой панели выберите hello эксперимент с именем модели переписи населения.  
2. В поле поиска поиск элементов эксперимента hello введите веб-службы. 
3. Перетащите *входных данных для службы Web* модуля на hello экспериментов холст и подключения его toohello выходные данные *Очистка недостающих данных* модуля.  Это гарантирует, что цикл данных обрабатывается hello таким же, как и исходный обучающих данных.
4. Перетащите два *веб-службы вывода* модулей на hello поэкспериментировать холста. Подсоедините hello выход hello *Обучение модели* модуль tooone и hello выходные данные hello *модель оценки* модуль toohello других. Здравствуйте, вывод службы web для **Обучение модели** дает нам hello новой обученной модели. Здравствуйте, выходных данных, вложенные слишком**модель оценки** возвращает выходных этого модуля, который является результаты производительности hello.
5. Щелкните **Выполнить**. 

Далее необходимо развернуть эксперимента обучения hello как веб-службу, которая создает обученной модели и результаты оценки модели. tooaccomplish это ваш следующий набор действий зависят от используемой классического веб-службы или веб-службу.  

**Классическая веб-служба**

Внизу hello холст эксперимента hello, нажмите кнопку **настройки веб-службы** и выберите **развертывание веб-службы [классический]**. Hello веб-службы **мониторинга** отображается страница справки hello ключ API и hello API для пакетного обновления. Только hello способ выполнения пакета можно использовать для создания обученных моделей.

**Новая веб-служба**

Внизу hello холст эксперимента hello, нажмите кнопку **настройки веб-службы** и выберите **развертывания [новое] веб-службы**. портал веб-службы Web службы Azure Machine Learning Hello открывается страница toohello развернуть веб-службы. Введите имя веб-службы и выберите план платежей, а затем нажмите кнопку **Deploy**(Развернуть). Только hello способ выполнения пакета можно использовать для создания обученных моделей

В любом случае после завершения выполнения эксперимента hello полученный рабочий процесс должен выглядеть следующим образом:

![Итоговый рабочий процесс после выполнения][4]



## <a name="retrain-hello-model-with-new-data-using-bes"></a>Обучение модели hello новыми данными, с помощью СРЕД
Например вы используете C# toocreate hello переподготовки приложения. Также можно hello Python или R образец кода tooaccomplish этой задачи.

toocall hello переподготовки API-интерфейсы:

1. Создайте консольное приложение C# в Visual Studio (**Создать** > **Проект** > **Visual C#** > **Классический рабочий стол Windows** > **Консольное приложение (.NET Framework**).
2. Войдите в систему toohello портала машины обучения веб-службы.
3. Если вы работаете с классической веб-службой, щелкните **Classic Web Services**(Классические веб-службы).
   1. Щелкните hello веб-службы, которой вы работаете.
   2. Щелкните конечную точку по умолчанию hello.
   3. Щелкните **Consume**(Использование).
   4. Внизу hello hello **использование** страницы в hello **образец кода** щелкните **пакета**.
   5. По-прежнему toostep 5 этой процедуры.
4. Если вы работаете с новой веб-службой, щелкните **Web Services**(Веб-службы).
   1. Щелкните hello веб-службы, которой вы работаете.
   2. Щелкните **Consume**(Использование).
   3. Hello нижней части страницы Consume hello в hello **образец кода** щелкните **пакета**.
5. Скопируйте hello пример кода C# для пакетного выполнения и вставьте его в файл Program.cs hello, убедившись, что пространство имен hello остается без изменений.

Добавьте пакет Nuget hello Microsoft.AspNet.WebApi.Client, как указано в комментариях hello. tooMicrosoft.WindowsAzure.Storage.dll ссылки tooadd hello, сначала для может потребоваться tooinstall hello клиентской библиотеки службы хранилища Microsoft Azure. Дополнительные сведения см. в документации о [Службе хранилища Windows Azure](https://www.nuget.org/packages/WindowsAzure.Storage).

### <a name="update-hello-apikey-declaration"></a>Обновление декларации apikey hello
Найдите hello **apikey** объявления.

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

В hello **потребления основные сведения о** раздел hello **использование** найдите hello первичный ключ и скопируйте его toohello **apikey** объявления.

### <a name="update-hello-azure-storage-information"></a>Обновить сведения о хранилище Azure hello
Hello BES образец кода отправляет файл с локального диска (например, «C:\temp\CensusIpnput.csv») tooAzure хранилища, обрабатывает его и записывает hello результаты назад tooAzure хранилища.  

tooaccomplish этой задачи необходимо получить hello данных учетной записи хранения имя ключа и контейнер для вашей учетной записи хранения из классического портала Azure hello и соответствующие значения в коде hello обновления hello. 

1. Войдите на классический портал Azure toohello.
2. В столбце hello навигации слева щелкните **хранения**.
3. Из списка hello учетных записей хранения выберите один toostore hello повторное Обучение модели.
4. Внизу hello страницы приветствия щелкните **управление ключами доступа**.
5. Скопируйте и сохраните hello **первичный ключ доступа** и hello закрыть диалоговое окно. 
6. В начале hello страницы приветствия, нажмите кнопку **контейнеры**.
7. Выберите существующий контейнер или создайте новую и сохраните имя hello.

Найдите hello *StorageAccountName*, *StorageAccountKey*, и *StorageContainerName* объявления и обновлять значения hello, сохраненный при выполнении hello портал Azure.

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

Также необходимо убедиться, что входной файл hello доступен в месте hello, указанных в коде hello. 

### <a name="specify-hello-output-location"></a>Укажите расположение выходных данных hello
При указании расположения вывода hello в полезных данных запроса hello, hello расширение файла hello, указанный в *RelativeLocation* должен быть указан как ilearner. 

См. следующий пример hello.

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you would like toouse for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> имена Hello вашего расположения вывода может отличаться от hello в этом пошаговом руководстве на основе hello порядка добавления hello веб-службы вывода модули в. Поскольку настройка этого эксперимента обучения с двумя выходами, hello результаты содержат сведения о расположении хранилища для них.  
> 
> 

![Выходные данные переобучения][6]

Схема 4. Выходные данные переобучения

## <a name="evaluate-hello-retraining-results"></a>Оценка результатов переподготовки hello
При запуске приложения hello hello выходные данные содержат hello URL-адрес и маркера необходимые tooaccess SAS hello результаты оценки.

Можно просмотреть результаты производительности hello hello повторное Обучение модели путем объединения hello *BaseLocation*, *RelativeLocation*, и *SasBlobToken* из hello выходных результатов для *output2* (как показано в предыдущем переподготовки изображения вывода hello) и вставка hello полный URL-адрес в адресной строке браузера hello.  

Проверьте результаты toodetermine hello ли вновь обученной модели hello выполняет также достаточно hello tooreplace один существующий.

Копировать hello *BaseLocation*, *RelativeLocation*, и *SasBlobToken* из hello выходные результаты, будет использовать их во время процесса переподготовки hello.

## <a name="next-steps"></a>Дальнейшие действия
При развертывании hello прогнозирующей веб-службы, щелкнув **развертывание веб-службы [классический]**, в разделе [обучение классического веб-службы](machine-learning-retrain-a-classic-web-service.md).

При развертывании hello прогнозирующей веб-службы, щелкнув **развертывания [новое] веб-службы**, см. [обучение новых веб-службы с помощью командлетов управления обучения машины hello](machine-learning-retrain-new-web-service-using-powershell.md).

<!-- Retrain a New web service using hello Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
