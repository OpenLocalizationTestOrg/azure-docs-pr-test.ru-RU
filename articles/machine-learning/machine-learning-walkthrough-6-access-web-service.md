---
title: "Шаг 6. Доступ к веб-службе машинного обучения | Документация Майкрософт"
description: "Шестой этап разработки прогнозного решения: доступ к активной веб-службе машинного обучения Azure."
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
ms.openlocfilehash: d309f6c4749a80c81859b693a2bd5927e8fe0e54
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-6-access-the-azure-machine-learning-web-service"></a>Шаг 6 пошагового руководства: доступ к веб-службе Машинного обучения Azure

Это последний этап пошагового руководства [Разработка решения для прогнозной аналитики в службе машинного обучения Azure](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Создание рабочей области машинного обучения](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Отправка существующих данных](machine-learning-walkthrough-2-upload-data.md)
3. [Создание нового эксперимента](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Обучение и анализ моделей](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Развертывание веб-службы](machine-learning-walkthrough-5-publish-web-service.md)
6. **Доступ к веб-службе**

- - -
На предыдущем шаге в этом руководстве мы развернули веб-службу, использующую модель прогнозирования риска некредитоспособности. Теперь пользователи могут отправлять в нее данные и получать результаты. 

Это веб-служба Azure, которая может получать и возвращать данные с помощью REST API одним из двух способов:  

* **Запрос и ответ** — пользователь отправляет одну или несколько строк данных о кредитах в службу с помощью протокола HTTP, а служба в качестве ответа возвращает один или несколько наборов результатов.
* **Пакетное выполнение** — пользователь сохраняет одну или несколько строк данных о кредитах в BLOB-объекте Azure, а затем отправляет адрес BLOB-объекта в Azure. Служба оценивает все строки данных во входном BLOB-объекте, сохраняет результаты в другом BLOB-объекте и возвращает URL-адрес данного контейнера.  

Быстрее и проще всего получить доступ к классической веб-службе через [веб-приложение службы "запрос-ответ" машинного обучения Azure](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) или [шаблон веб-приложения службы пакетного выполнения машинного обучения Azure](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).

С помощью шаблонов веб-служб можно создать пользовательское веб-приложение, которое "знает" входные данные вашей веб-службы и ожидаемые результаты. Вам нужно всего лишь предоставить доступ к веб-службе и данным, а шаблон выполнит все остальные действия.

Дополнительные сведения об использовании шаблонов веб-приложений см.в статье [Использование веб-службы машинного обучения Azure с шаблоном веб-приложения](machine-learning-consume-web-service-with-web-app-template.md).

Можно также разработать настраиваемое приложение для доступа к веб-службе с помощью стартового кода в языках программирования R, C# и Python.

Дополнительные сведения см. в статье [Как использовать веб-службу машинного обучения Azure](machine-learning-consume-web-services.md).

