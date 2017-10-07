---
title: "aaaLoad данных в хранилище Azure среды для аналитики | Документы Microsoft"
description: "Tooand перемещения данных из хранилища больших двоичных объектов"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b8fbef77-3e80-4911-8e84-23dbf42c9bee
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 0fea2290991f9fa63d9e46c3a657000e27d95289
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a>Загрузка данных в среды хранения для аналитики
Hello командного процесса обработки и анализа данных требуется, полученный или данные загружаются в различные хранилища различных сред toobe обработки или проанализировать в наиболее подходящий способ hello на каждом этапе процесса hello. Для обработки обычно используются следующие места хранения данных: хранилище больших двоичных объектов Azure, базы данных SQL Azure, SQL Server на виртуальной машине Azure, HDInsight (Hadoop) и Машинное обучение Azure. 

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

Это **меню** связывает tootopics, которые описывают, как tooingest данные в этих целевых средах, где hello данные хранятся и обрабатываются.

Технические и бизнес-требований, а также hello исходное расположение, форматирования и объемом данных определяют hello целевых средах, в которых hello данные должны toobe полученный tooachieve hello целей анализа. Довольно часто для данных toobe toorequire сценарий, перемещать между несколько сред tooachieve hello разнообразных задач требуется tooconstruct прогнозной модели. Эта последовательность задач может включать в себя, например, просмотр данных, предварительную обработку, очистку, понижение частоты выборки и обучение модели.

