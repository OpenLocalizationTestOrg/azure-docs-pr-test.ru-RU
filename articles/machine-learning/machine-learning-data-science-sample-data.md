---
title: "aaaSample данные в Azure, контейнеры, SQL Server, больших двоичных объектов и куст таблицы | Документы Microsoft"
description: "Управление хранением данных tooexplore в различных enviromnents Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 80a9dfae-e3a6-4cfb-aecc-5701cfc7e39d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5a5295b59fa02f91da680fc7495a92ca135e26c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Выборка данных в контейнерах больших двоичных объектов Azure, SQL Server и таблицах Hive
В этом документе связывает tootopics, рассматриваются как toosample данные, которые хранятся в одном из трех разных местах Azure:

* **данных контейнера больших двоичных объектов Azure** осуществляется путем их программного скачивания и последующей выборки с помощью примера кода на языке Python.
* **Данные SQL Server** выборки с помощью SQL и hello языка программирования Python. 
* **данных таблицы Hive** осуществляется с помощью запросов Hive.

следующие Hello **меню** связывает toohello разделы, описывающие, как toosample данных от каждого из этих сред хранилища Azure. 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

Эта задача выборка является этапом hello [процесса обработки и анализа данных Team (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

**Для чего нужна выборка данных?**

При планировании tooanalyze dataset hello имеет большой размер, это обычно tooreduce данных рекомендуется toodown образец hello его tooa размер меньший, но репрезентативный и управляемость. Это способствует пониманию данных, их исследованию и проектированию характеристик. Его роль в hello процесса Cortana Analytics — tooenable быстрого создания прототипов функций обработки данных hello и машинного обучения моделей.

