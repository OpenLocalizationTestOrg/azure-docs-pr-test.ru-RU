---
title: "Использование примеров экспериментов машинного обучения в Azure | Документация Майкрософт"
description: "Узнайте, как использовать примеры экспериментов машинного обучения из коллекции Cortana Intelligence для создания экспериментов с использованием Машинного обучения Microsoft Azure."
keywords: machine learning examples, sample experiment, machine learning sample
services: machine-learning
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: 81e6c1d8-682c-4db3-bfd5-d7bfb1150ff3
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: cgronlun
ms.openlocfilehash: 55f9bd2ed0d555a14d31bf3d262707d65bd70244
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="copy-example-experiments-to-create-new-machine-learning-experiments"></a>Использование примеров экспериментов для создания новых экспериментов машинного обучения
Узнайте, как использовать примеры экспериментов машинного обучения из [коллекции Cortana Intelligence](https://gallery.cortanaintelligence.com/), чтобы не создавать собственные решения с нуля. Эти примеры помогут вам создать решение машинного обучения.

В коллекции содержатся примеры экспериментов, предоставленные как рабочей группой Машинного обучения Microsoft Azure, так и участниками сообщества машинного обучения. Также можно задавать вопросы и публиковать комментарии об экспериментах.

Чтобы узнать, как использовать коллекцию, просмотрите 3-минутное видео [Копирование работы других пользователей для обработки и анализа данных](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) из серии [Обработка и анализ данных для начинающих](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="find-an-experiment-to-copy-in-cortana-intelligence-gallery"></a>Поиск эксперимента для копирования в коллекции Cortana Intelligence
Чтобы просмотреть доступные эксперименты, перейдите в раздел [Коллекция](https://gallery.cortanaintelligence.com/) и щелкните **Эксперименты** в верхней части страницы.

### <a name="find-the-newest-or-most-popular-experiments"></a>Поиск последних и самых популярных экспериментов
На этой странице можно просмотреть **недавно добавленные** эксперименты, а также **популярные эксперименты** или последние **популярные эксперименты Майкрософт**.

### <a name="look-for-an-experiment-that-meets-specific-requirements"></a>Поиск эксперимента, соответствующего определенным требованиям
Для просмотра всех экспериментов выполните следующие действия.

1. В верхней части страницы щелкните **Просмотреть все** .
2. В левой части окна в разделе **Refine by** (Отфильтровать по) в разделе **Категории** выберите **Эксперимент**, чтобы просмотреть все эксперименты в коллекции.
3. Эксперименты, соответствующие определенным требованиям, можно найти несколькими различными способами.
   * **Выберите фильтры в левой части окна.** Например, чтобы просмотреть эксперименты, в которых используется алгоритм обнаружения аномалий на основе PCA, выберите **Эксперимент** в разделе **Категории** и щелкните **Показать все**. Затем. в разделе **Algorithms Used** (Используемые алгоритмы) выберите **PCA-Based Anomaly Detection** (Обнаружение аномалий на основе анализа первичных компонентов). <br></br>
     ![Выбор фильтров](./media/machine-learning-sample-experiments/refine-the-view.png)
   * **Используйте поле поиска.** Например, чтобы найти эксперименты, предоставленные корпорацией Майкрософт и относящиеся к распознаванию цифр с использованием алгоритма двухклассовой машины опорных векторов, введите "распознавание цифр" в поле поиска. Затем выберите фильтры **Experiment** (Эксперимент), **Microsoft content only** (Только содержимое Майкрософт) и **Two-Class Support Vector Machine** (Двухклассовая машина опорных векторов).<br></br>
     ![Используйте поле поиска.](./media/machine-learning-sample-experiments/search-for-experiments.png)
4. Щелкните эксперимент, чтобы узнать о нем подробнее.
5. Чтобы запустить или изменить эксперимент, щелкните **Open in Studio** (Открыть в Студии) на странице эксперимента. <br></br>

    ![Пример эксперимента](./media/machine-learning-sample-experiments/example-experiment.png)

    > [!NOTE]
    > При первом открытии эксперимента в Студии машинного обучения можно испытать его бесплатно или приобрести подписку Azure. Дополнительные сведения о бесплатной пробной и платной версии Студии машинного обучения см. на странице [цен на машинное обучение](https://azure.microsoft.com/pricing/details/machine-learning/).
    >
    >

## <a name="create-a-new-experiment-using-an-example-as-a-template"></a>Создание эксперимента, используя в качестве шаблона пример
Эксперимент в студии машинного обучения также можно создать, используя пример из коллекции в качестве шаблона.

1. Войдите в [Студию](https://studio.azureml.net) с использованием учетной записи Майкрософт, после чего щелкните **Создать**, чтобы создать эксперимент.
2. Просмотрите примеры содержимого и выберите то, что вам подходит.

В рабочей области студии машинного обучения будет создан эксперимент на основе выбранного примера в качестве шаблона.

## <a name="next-steps"></a>Дальнейшие действия
* [Импорт обучающих данных в Студию машинного обучения Azure из разных источников данных](machine-learning-data-science-import-data.md)
* [Краткое руководство по языку программирования R для службы машинного обучения Azure](machine-learning-r-quickstart.md)
* [Развертывание веб-службы машинного обучения Azure](machine-learning-publish-a-machine-learning-web-service.md)
