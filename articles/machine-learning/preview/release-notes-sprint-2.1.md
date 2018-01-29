---
title: "Заметки о выпуске Azure Machine Learning Workbench для исправления QFE спринта 2 за декабрь 2017 г."
description: "В этом документе описаны обновления QFE, выпущенные для спринта 2 службы \"Машинное обучение Azure\""
services: machine-learning
author: hning86
ms.author: haining
manager: mwinkle
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.workload: data-services
ms.topic: article
ms.date: 12/15/2017
ms.openlocfilehash: b0916f565d91f5a59d1bfb4653f29bfbdb573443
ms.sourcegitcommit: 48fce90a4ec357d2fb89183141610789003993d2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/12/2018
---
# <a name="sprint-2-qfe---december-2017"></a>Исправление QFE для Sprint 2 — декабрь 2017 г. 

#### <a name="version-number-01171115323"></a>Номер версии: 0.1.1711.15323

>Узнать, как найти номер версии, можно из статьи [Azure Machine Learning Workbench: руководство по устранению неполадок и описание известных проблем](https://docs.microsoft.com/azure/machine-learning/preview/known-issues-and-troubleshooting-guide).

Представляем вам третье обновление QFE (Quick Fix Engineering), выпущенное для Azure Machine Learning Workbench. Этот выпуск является вспомогательным. Здесь рассматриваются некоторые проблемы телеметрии, что помогает команде разработчиков понять, как используется продукт. Эти знания могут быть использованы в будущем для улучшения качества продукта. 

Кроме того, существует два важных обновления:

- При подготовке данных была исправлена ​​ошибка, при которой инспектор временных рядов не отображался в пакетах подготовки данных.
- Вам больше не нужно быть владельцем подписки Azure в программе командной строки, чтобы подготовить кластеры машинного обучения для вычислений ACS. 
