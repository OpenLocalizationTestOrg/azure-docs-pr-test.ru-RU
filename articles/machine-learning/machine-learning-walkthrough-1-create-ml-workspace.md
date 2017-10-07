---
title: "Шаг 1. Создание рабочей области машинного обучения | Документация Майкрософт"
description: "Шаг 1 из hello разработка прогнозирующего решения Пошаговое руководство: Узнайте, как tooset копирование новую рабочую область студии машинного обучения Azure."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b3c97e3d-16ba-4e42-9657-2562854a1e04
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 93d2e240826db9768e85b00cab0eb62510b4efb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-1-create-a-machine-learning-workspace"></a>Шаг 1. Создание рабочей области машинного обучения
Это первый шаг hello hello пошагового руководства, [разрабатывать решения для прогнозирующего анализа в машинном обучении Azure](machine-learning-walkthrough-develop-predictive-solution.md).

1. **Создание рабочей области машинного обучения**
2. [Отправка существующих данных](machine-learning-walkthrough-2-upload-data.md)
3. [Создание нового эксперимента](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Обучать и оценивать модели hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Развернуть веб-службу hello](machine-learning-walkthrough-5-publish-web-service.md)
6. [Доступ к веб-службе hello](machine-learning-walkthrough-6-access-web-service.md)

- - -
<!-- This needs toobe updated toorefer toohello new way of creating workspaces in hello Ibiza portal -->

toouse студии машинного обучения, необходимо toohave рабочей области машинного обучения Microsoft Azure. Эта рабочая область содержит hello средства toocreate, управлять и публиковать экспериментов.  

<!--
## toocreate a workspace
1. Sign in toohello [Azure classic portal](https://manage.windowsazure.com).
2. In hello  Azure services panel, click **MACHINE LEARNING**.  
   ![Create workspace][1]
3. Click **CREATE AN ML WORKSPACE**.
4. On hello **QUICK CREATE** page, enter your workspace information and then click **CREATE AN ML WORKSPACE**.
-->

Здравствуйте, администратор вашей подписки Azure требуется рабочая область toocreate hello и добавить вас в качестве владельца или участника. Подробные сведения см. в статье [Создание рабочей области машинного обучения Azure и предоставление к ней общего доступа](machine-learning-create-workspace.md).

Создав рабочую область, откройте Студию машинного обучения ([https://studio.azureml.net/Home](https://studio.azureml.net/Home)). При наличии более чем одной рабочей области, можно выбрать hello рабочей области в панели инструментов hello в правом верхнем углу hello окна hello.

![Выбор рабочей области в Студии][2]

> [!TIP]
> Если были внесены владельца рабочей области hello, вы можете совместно использовать hello экспериментов, над которыми вы работаете с приглашение других пользователей toohello рабочей области. Это можно сделать в студии машинного обучения на hello **параметры** страницы. Необходимо просто hello учетную запись Майкрософт или организации для каждого пользователя.
> 
> На hello **параметры** щелкните **пользователей**, нажмите кнопку **ПРИГЛАШЕНИЯ более пользователей** hello нижней части окна hello.
> 
> 

- - -
**Далее:[ отправка имеющихся данных](machine-learning-walkthrough-2-upload-data.md)**

[1]: ./media/machine-learning-walkthrough-1-create-ml-workspace/create1.png
[2]: ./media/machine-learning-walkthrough-1-create-ml-workspace/open-workspace.png
