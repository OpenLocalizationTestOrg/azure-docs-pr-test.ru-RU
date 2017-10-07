---
title: "aaaTroubleshoot переподготовки Azure Machine Learning классического веб-службы | Документы Microsoft"
description: "Определить и устранить распространенные проблемы обнаружено при переподготовки модели hello Azure Machine Learning веб-службы."
services: machine-learning
documentationcenter: 
author: VDonGlover
manager: raymondl
editor: 
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 2b6a78eaba161877106dccdc23437b5e454fca7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a>Устранение неполадок hello переподготовки машины Azure обучения классического веб-службы
## <a name="retraining-overview"></a>Сведения о повторном обучении
Когда вы развертываете прогнозный эксперимент в качестве оценивающей веб-службы, вы получаете статическую модель. По мере появления новых данных или hello потребитель hello API имеет свои собственные данные модели hello должен toobe обучить повторно. 

Полное Пошаговое руководство hello переподготовки процесса классического веб-службы см. в разделе [обучение машины обучения моделей программным способом](machine-learning-retrain-models-programmatically.md).

## <a name="retraining-process"></a>Процесс повторного обучения
Если вам требуется tooretrain hello веб-службы, необходимо добавить некоторые дополнительные элементы:

* Веб-служба, развернутых из hello эксперимента обучения. должен иметь эксперимента Hello **вывод веб-службы** модуль присоединенного выходные данные toohello hello **Обучение модели** модуля.  
  
    ![Присоедините Обучение модели toohello вывода hello веб-служб.][image1]
* Новая конечная точка добавлен tooyour оценки веб-службы.  Добавить конечную точку hello можно программным образом с использованием примера кода hello, на которые ссылается hello машинного обучения, повторного обучения моделей программным способом раздела или с помощью классического портала Azure hello.

Затем можно использовать hello пример кода C# из модели tooretrain страницы справки API hello обучения веб-службы. После оценивал результаты hello и их пригодности обновлении hello обученной модели оценки с помощью hello новую конечную точку, которая была добавлена веб-службы.

С все составляющие hello в месте hello основных шагов, необходимо выполнить tooretrain модели hello связаны следующим образом:

1. Вызовите hello обучения веб-службы: hello вызовов toohello службы пакетного выполнения (BES), не hello запроса ответа службы (RR). При вызове функции hello toomake страницы справки hello API можно использовать hello пример кода C#. 
2. Найти значение hello для hello *BaseLocation*, *RelativeLocation*, и *SasBlobToken*: эти значения возвращаются в выходных данных hello из вашего вызова toohello обучения веб Служба. 
   ![отображая выходные данные hello hello переподготовки образец и hello BaseLocation, RelativeLocation и SasBlobToken значения.][image6]
3. Обновление hello добавить конечную точку из hello новые оценки веб-службы с hello обученной модели: с использованием примера кода hello, входящем в hello обучение машинного обучения моделей программным способом, обновить hello новой конечной точки добавлены toohello вновь оценки модели с hello обученной модели из hello обучения веб-службы.

## <a name="common-obstacles"></a>Распространенные затруднения
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a>Проверьте toosee при наличии hello исправьте ИСПРАВЛЕНИЯ URL-адрес
Hello ИСПРАВЛЕНИЯ URL-адрес используется должен быть связан с hello hello новой конечной точки оценки вы добавили toohello оценки веб-службы. Существует ряд способов tooobtain hello ИСПРАВЛЕНИЯ URL-адрес:

**Вариант 1: программно**

tooget hello исправьте ИСПРАВЛЕНИЯ URL-адрес:

1. Запустите hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) пример кода.
2. Из вывода hello AddEndpoint, найти hello *HelpLocation* значение и скопируйте URL-адрес hello.
   
   ![HelpLocation в выходных данных hello addEndpoint образца hello.][image2]
3. Вставьте URL-адрес hello в браузере страницу tooa toonavigate, предоставляющий ссылки на справку для hello веб-службы.
4. Нажмите кнопку hello **обновления ресурса** страницы справки исправления hello tooopen ссылку.

**Вариант 2: Использование hello классический портал Azure**

1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).
2. Привет открыть вкладку машинного обучения. ![Вкладка "Машинное обучение".][image4]
3. Щелкните имя рабочей области, а затем выберите **Веб-службы**.
4. Щелкните hello оценки веб-службы, которой вы работаете. (Если не удалось изменить имя по умолчанию hello hello веб-службы, он будет помещен в [Exp оценки.].)
5. Щелкните **Добавить конечную точку**.
6. После добавления конечной точки hello, щелкните имя конечной точки hello. Нажмите кнопку **обновления ресурса** tooopen hello исправления страницы справки.

> [!NOTE]
> При добавлении конечной точки hello toohello обучения веб-службы вместо hello прогнозной веб-службы, появится следующая ошибка при нажатии кнопки hello hello **обновления ресурса** ссылку: к сожалению, но эта функция не поддерживается или доступные в данном контексте. Эта веб-служба не содержит обновляемых ресурсов. Мы приносим свои извинения за неудобства hello и работают на улучшение этот рабочий процесс.
> 
> 

![Панель мониторинга новой конечной точки.][image3]

страницы справки ИСПРАВЛЕНИЯ Hello содержит hello исправление для URL-адреса необходимо использовать и примеры кода можно использовать toocall его.

![URL-адрес исправления.][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a>Проверьте toosee, что выполняется обновление конечной точки оценки правильный hello
* Не patch hello обучения веб-службы: hello исправление операция должна выполняться на hello оценки веб-службы.
* Не исправление для конечной точки по умолчанию hello в веб-службы: hello исправление операция должна выполняться на новые оценки конечной веб-службы, которая была добавлена hello.

Вы можете проверить, какие hello конечной веб-службы включена по обходу hello классический портал Azure. 

> [!NOTE]
> Убедитесь, что вы добавляете toohello hello конечную точку прогнозируемого веб-службы, hello обучения веб-службы. Если вы правильно развернули обучающую и прогнозную веб-службы, вы увидите две отдельные веб-службы. Hello прогнозной веб-службы должно заканчиваться «[прогнозной exp.]».
> 
> 

1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).
2. Привет открыть вкладку машинного обучения. ![Пользовательский интерфейс рабочей области машинного обучения.][image4]
3. Щелкните рабочую область.
4. Щелкните **Веб-службы**.
5. Выберите нужную прогнозную веб-службу.
6. Убедитесь, что новой конечной точкой, добавлено toohello веб-службы.

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a>Проверьте hello рабочее пространство, веб-службу в tooensure, где находится необходимый регион hello
1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).
2. Выберите меню hello машинного обучения.
   ![Пользовательский интерфейс региона машинного обучения.][image4]
3. Проверьте расположение hello рабочей области.

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
