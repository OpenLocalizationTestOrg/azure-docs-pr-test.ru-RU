---
title: "aaaSupportability добавить существующую группу доступности виртуальных машин Azure tooan | Документы Microsoft"
description: "Возможности поддержки добавления виртуальных машин Azure tooan существующую группу доступности."
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/15/2017
ms.author: delhan
ms.openlocfilehash: dc2bd86b916f1d1a0a0d4c9e870df829434c96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a>Возможности поддержки добавления виртуальных машин Azure tooan существующий набор доступности

Ограничения может столкнуться при добавлении новых виртуальных машин (ВМ) tooan существующую группу доступности. Здравствуйте, приведенные ниже сведения диаграммы Здравствуйте, какому ряду виртуальной Машины, можно сочетать в одной группе доступности.

Вот hello Матрица поддержки toomix различных типов виртуальных машин.

Серии и группа доступности|Вторая виртуальная машина|Файл ,|Av2|D|Dv2|Dv3|
|---|---|---|---|---|---|---|
|Первая виртуальная машина|||||||
|Файл ,||ОК|ОК|ОК|ОК|ОК|
|Av2||ОК|ОК|ОК|ОК|ОК|
|D||ОК|ОК|ОК|ОК|ОК|
|Dv2||ОК|ОК|ОК|ОК|ОК|
|Dv3||ОК|ОК|ОК|ОК|ОК|

Все ряды не могут содержаться в hello набор же доступности, так как они требуют определенного оборудования.
