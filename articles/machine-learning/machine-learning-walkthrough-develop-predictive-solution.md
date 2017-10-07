---
title: "aaaA прогнозирующего решения для кредитного риска с машинного обучения | Документы Microsoft"
description: "Подробное пошаговое руководство отображаются как toocreate решения для прогнозирующего анализа для кредита оценка рисков в студии машинного обучения Azure."
keywords: "кредитный риск, решение прогнозной аналитики, оценка рисков"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 43300854-a14e-4cd2-9bb1-c55c779e0e93
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 00ed39081e6952b8d03b37a8285d8dc3ddff2cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a>Пошаговое руководство по разработке решения для прогнозной аналитики в службе машинного обучения Azure для оценки кредитных рисков

В этом пошаговом руководстве мы рассмотрим расширенные hello процесс разработки решения для прогнозирующего анализа в студии машинного обучения. Мы разработка простого модели в студии машинного обучения и затем развернуть его как веб-службы машинного обучения Azure, где hello модели можно сделать прогноз, с помощью новых данных. 

В этом руководстве предполагается, что вы уже работали со Студией машинного обучения и имеете некоторое представление о машинном обучении. При этом предполагается, что вы не являетесь специалистом в этой области.

Если вы раньше не использовали **студии машинного обучения Azure** перед toostart hello учебник, может потребоваться [создать первый обработки и анализа данных эксперимента в студии машинного обучения Azure](machine-learning-create-experiment.md). Этот учебник поможет выполнить студии машинного обучения для hello первый раз. Он показывает, основы hello модулей как toodrag перетаскивания в свой эксперимент соединять их запуска эксперимента hello и просмотрите результаты hello. Другое средство, которое может быть полезен для Приступая к работе — это схема, общие сведения о возможностях hello студии машинного обучения. Ее можно скачать и распечатать в статье [Обзорная схема возможностей Студии машинного обучения Azure](machine-learning-studio-overview-diagram.md).
 
Если вы новое поле toohello машинного обучения в целом, есть ряд видео, которые могут быть полезными tooyou. Он вызывается [обработки и анализа данных для начинающих](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) и он может предоставлять обучения toomachine значительные введение, с использованием естественного языка и понятий.


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="hello-problem"></a>проблема Hello

Предположим, вам необходимо toopredict отдельного кредитного риска на основе hello введенных в приложении кредит на нее.  

Оценка кредитных рисков — это сложная проблема. Для этого пошагового руководства мы немного упростим ее. Мы используем ее в качестве примера для создания решения прогнозной аналитики с помощью машинного обучения Microsoft Azure. toodo это, мы используем студии машинного обучения Azure и веб-службы машинного обучения.  

## <a name="hello-solution"></a>решение Hello

В рамках этого руководства мы начнем с общедоступных данных кредитного риска и на их основе разработаем и обучим прогнозную модель. Затем мы развертывание hello модели в виде веб-службы, он может использоваться другими пользователями для оценки рисков кредит.

toocreate это решение оценки риска кредитной мы выполните следующие действия:  

1. [Создание рабочей области машинного обучения](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Отправка существующих данных](machine-learning-walkthrough-2-upload-data.md)
3. [Создание эксперимента](machine-learning-walkthrough-3-create-new-experiment.md)
4. [Обучать и оценивать модели hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Развернуть веб-службу hello](machine-learning-walkthrough-5-publish-web-service.md)
6. [Веб-службы доступа hello](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> В этом пошаговом руководстве в hello можно найти рабочую копию hello эксперимента, в ходе разработки мы [коллекции аналитики Cortana](https://gallery.cortanaintelligence.com). Go слишком**[Пошаговое руководство: прогноз риска кредитной](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)**  и нажмите кнопку **в Studio** toodownload копию hello эксперимента в рабочую область студии машинного обучения.
> 
> Это пошаговое руководство основано на упрощенную версию hello примере эксперимента [двоичной классификации: кредита прогнозирования рисков](http://go.microsoft.com/fwlink/?LinkID=525270), которые также доступны в hello [коллекции](http://gallery.cortanaintelligence.com/).
