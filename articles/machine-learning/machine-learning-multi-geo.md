---
title: "Географическая aaaMulti справочной документации | Документы Microsoft"
description: "Узнайте, как toocreate рабочей области и публикации веб-службы в регион Azure отличается от hello Юг центральной США (SCUS) регионе Azure."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: rmca14
tags: 
ms.assetid: ed0ca8a8-fa53-4e56-b824-2d7e44641967
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/6/2017
ms.author: tedway; neerajkh
ms.openlocfilehash: 77b055950ebfe329131b40e5f0a2f6be1e33c51e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="multi-geo-help-documentation"></a>Справка по размещению в различных регионах
В этой статье описывается создание рабочей области и публикация веб-службы в других регионах Azure.  Hello [Azure продукты по области страницы](https://azure.microsoft.com/en-us/regions/services/) список регионов, где находится машинного обучения Azure.

## <a name="create-a-workspace"></a>Создание рабочей области
1. Войдите в toohello классический портал Azure.
2. Щелкните **+ Создать** > **Службы данных** > **Машинное обучение** > **Быстрое создание**.  В списке **Расположение** выберите другой регион, например **Юго-Восточная Азия**.
   ![Справка по размещению в различных регионах, изображение 1][1]
3. Выберите рабочую область hello и нажмите кнопку **входа tooML Studio**.
   ![Справка по размещению в различных регионах, изображение 2][2]
4. Вы создали рабочую область в другом регионе, которую можно использовать наряду с другими рабочими областями. tooswitch между рабочими областями вид toohello правой верхней части экрана. Щелкните раскрывающийся список hello, выберите hello региона и рабочей области выберите hello. Все уже toohello локальной рабочей области.  Например все вашего веб-службы, созданные из рабочей области, будут в hello одной рабочей области hello, расположенный в.
   ![Справка по размещению в различных регионах, изображение 3][3]

## <a name="open-an-experiment-from-gallery"></a>Доступ к эксперименту из коллекции
При открытии эксперимент из коллекции, можно выбрать область, которая требуется toocopy hello эксперимента.

![Справка по размещению в различных регионах, изображение 4][4a]

## <a name="web-service-management"></a>Управление веб-службой
tooprogrammatically управление веб-служб, таких как для переустановки, использовать адрес конкретного региона hello:

* https://asiasoutheast.management.azureml.net
* https://europewest.management.azureml.net

### <a name="things-toonote"></a>Toonote действия
1. Можно копировать только экспериментов между рабочих областей, которые принадлежат toohello одного региона таким образом. Если вам требуется toocopy эксперимента между областями в разных регионах, можно использовать hello [PowerShell](http://aka.ms/amlps) командлетов для [ *копирования AmlExperiment* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish. Другое решение — toopublish hello эксперимента в коллекцию в режиме, отсутствующие в списке, а затем открыть его в рабочей области hello из hello другой области.
2. Селектор Hello области будут отображаться только рабочих областей для одного региона одновременно.  
3. Бесплатные или гостевые (анонимные) рабочие области создаются и размещаются в юго-центральном регионе США.  
4. Веб-службы, развертываемые из рабочей области, расположенной в Юго-Восточной Азии, также будут размещены в Юго-Восточной Азии.  

## <a name="more-information"></a>Дополнительные сведения
Задать вопрос о hello [форум машинного обучения Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
