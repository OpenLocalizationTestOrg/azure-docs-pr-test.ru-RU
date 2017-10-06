---
title: "веб-службы обучения машины из Excel aaaConsume | Документы Microsoft"
description: "Использование веб-службы Машинного обучения Azure в Excel"
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a>Использование веб-службы Машинного обучения Azure в Excel
 Студия машинного обучения позволяет легко toocall веб-службы непосредственно из Excel без hello требуется toowrite любого кода.

Если вы используете Excel 2013 (или более поздней версии) или Excel Online, то рекомендуется использовать hello Excel [надстройка Excel](machine-learning-excel-add-in-for-web-services.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a>Действия
Опубликуйте веб-службу. [Эта страница](machine-learning-walkthrough-5-publish-web-service.md) объясняет, как toodo его. В настоящее время функция книги Excel hello поддерживается только для запросов и ответов службы, имеющие один выход (то есть одну оценки метку). 

При наличии веб-службы, щелкните hello **веб-службы** статьи hello левой стороны hello studio, а затем выберите hello web service tooconsume из Excel.

**Классическая веб-служба**

1. На hello **МОНИТОРИНГА** вкладке hello веб-службы по одной строке на hello **запрос-ОТВЕТ** службы. Если эта служба имеет один выход, вы увидите hello **загрузить книгу Excel** ссылку в этой строке.
   
    ![][1]
2. Щелкните **Download Excel Workbook**(Скачать книгу Excel).

**Новая веб-служба**

1. Веб-служба Azure Machine Learning hello портале выберите **использование**.
2. На странице приветствия использование в hello **веб-параметров службы потребления** щелкните значок Excel hello.

**С помощью книги hello**

1. Привет открыть книгу.
2. Появляется предупреждение системы безопасности; Щелкните hello **Разрешить изменение** кнопки.
   
    ![][2]
3. Отобразится предупреждение системы безопасности. Щелкните hello **включить содержимое** кнопку макросы toorun электронной таблицы.
   
    ![][3]
4. После включения макросов будет создана таблица. Столбцы в синей являются требуется в качестве входных данных в hello записей Ресурсов веб-службы, или **параметры**. Обратите внимание, выходные данные hello hello обновления записей Ресурсов **ПРОГНОЗИРУЕМЫЕ значения** зеленым цветом. Когда все столбцы для строки заполняются, hello книги автоматически вызывает API оценки hello и отображает hello оцененных результатов.
   
    ![][4]
5. tooscore более одной строки, вторая строка hello заполнения с данными и hello спрогнозировала, что созданные значения. Можно даже вставить несколько строк одновременно.

Функциональные возможности Excel hello (диаграммы, карты power, условного форматирования, т. д.) можно использовать с hello прогнозируемые значения toohelp визуализации данных hello.    

## <a name="sharing-your-workbook"></a>Предоставление общего доступа к книге
Чтобы toowork макросы hello ваш ключ API должна входить hello электронной таблицы. Это означает, что должно использовать hello книги только с сущностями и частных лиц, которым вы доверяете.

## <a name="automatic-updates"></a>Автоматическое обновление
Служба RRS вызывается в двух следующих случаях:

1. Здравствуйте, первый раз, когда строка имеет содержимое во всех его **параметров**
2. Каждый раз любой hello **параметры** изменения в строку, которая имеет все его **параметры** введены.

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
