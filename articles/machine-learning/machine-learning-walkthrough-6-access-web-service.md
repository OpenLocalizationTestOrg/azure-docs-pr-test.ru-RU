---
title: "Шаг 6: Доступ к службе Web обучения машины hello | Документы Microsoft"
description: "Шаг 6 hello разработка прогнозирующего решения Пошаговое руководство: доступ к активную службу Azure Machine Learning веб."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a65c89a-40ab-4673-8dd8-8eee0a150e3b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 211de0294092c6a6b5e6eb608d5d3b88107674c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-6-access-hello-azure-machine-learning-web-service"></a>Пошаговое руководство шаг 6: Доступ к веб-службы машинного обучения Azure hello

Это последний шаг hello hello пошагового руководства, [разрабатывать решения для прогнозирующего анализа в машинном обучении Azure](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Создание рабочей области машинного обучения](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Отправка существующих данных](machine-learning-walkthrough-2-upload-data.md)
3. [Создание нового эксперимента](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Обучать и оценивать модели hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Развернуть веб-службу hello](machine-learning-walkthrough-5-publish-web-service.md)
6. **Доступ к веб-службе hello**

- - -
Hello на предыдущем шаге в этом пошаговом руководстве мы развернуть веб-службы, использующей модель прогнозирования риск нашей кредита. Теперь пользователи могут toosend tooit данных и получения результатов. 

Hello веб-службы — это служба Azure web, которое может принимать и возвращать данные с помощью API REST в одном из двух способов:  

* **Запрос-ответ** - hello пользователь отправляет один или более строк toohello данных кредитной службы с помощью протокола HTTP и hello отвечает службы с одного или нескольких наборов результатов.
* **Пакетное выполнение** - hello пользователь сохраняет одну или несколько строк данных кредита в Azure BLOB-объектов, а затем отправляет расположение toohello hello BLOB-объектов. оценки службы Hello, все hello строки данных в Здравствуйте входного BLOB-объекта, магазины hello приводит к другой большой двоичный объект и возвращает hello URL-адрес этого контейнера.  

Здравствуйте tooaccess быстрее и проще всего классического веб-службе осуществляется через hello [веб-приложения Azure ML запрос-ответ службы](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) или [Azure ML пакетного выполнения службы веб-приложения шаблона](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).

С помощью шаблонов веб-служб можно создать пользовательское веб-приложение, которое "знает" входные данные вашей веб-службы и ожидаемые результаты. Все, что нужно toodo — обеспечить доступ tooyour веб-службы и обработки данных и шаблон hello hello rest.

Дополнительные сведения об использовании hello веб-приложения шаблонов см. в разделе [Azure Machine Learning Web службы с веб-приложения шаблон потребителя](machine-learning-consume-web-service-with-web-app-template.md).

Можно также разработать пользовательское приложение tooaccess hello веб-службы с помощью начальный код, предоставляются в R, C# и языка программирования Python.

Можно найти подробные сведения в [как tooconsume в Azure Machine обучения, веб-службу](machine-learning-consume-web-services.md).

