---
title: "aaa \"Создание перспектив Azure Analysis Services занятие учебника 8 | Документы Microsoft»"
description: "Описывает, как toocreate перспективы в hello проекта tutorial служб Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 25391813e1969ecb22af4d6f9c1ccd8358d812fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-8-create-perspectives"></a>Занятие 8. Создание перспектив

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

В этом занятии вы создадите перспективу Internet Sales. Перспектива определяет просматриваемое подмножество модели, предоставляющее точки наблюдения, сосредоточенные на определенном объекте, аспекте бизнеса или приложении. Когда пользователь подключается tooa модели с помощью перспективы, они видят только те объекты модели (таблицы, столбцы, меры, иерархии и ключевые показатели эффективности) как поля, определенные в перспективе. toolearn более, в разделе [перспективы](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).
  
Hello перспективы Internet Sales, создаваемая на этом занятии исключает объект таблицы DimCustomer hello. При создании перспективы, которая исключает из представления определенные объекты, объекты продолжают существовать в модели hello. но не отображаются в списке полей для клиента отчетов. Вычисляемые столбцы и меры, как включенные, так и не включенные в перспективу, по-прежнему могут проводить расчеты на основе исключенных данных.  
  
Hello цель этого занятия — toodescribe как toocreate перспектив и ознакомиться со средствами разработки табличных моделей hello. Если потом развернуть дополнительные таблицы tooinclude этой модели, можно создать дополнительные перспективы toodefine разных точек обзора модели hello, например, инвентаризации и продажи.  
  
Предполагаемое время toocomplete на этом занятии: **пять минут**  
  
## <a name="prerequisites"></a>Предварительные требования  
Этот раздел входит в учебник по табличному моделированию, который следует изучать в предложенном порядке. Перед выполнением задачи hello на этом занятии, необходимо завершить предыдущее занятие hello: [занятии 7: Создание ключевых показателей эффективности](../tutorials/aas-lesson-7-create-key-performance-indicators.md).  
  
## <a name="create-perspectives"></a>Создание перспектив  
  
#### <a name="toocreate-an-internet-sales-perspective"></a>toocreate перспективы Internet Sales  
  
1.  Нажмите кнопку hello **модель** меню > **перспективы** > **Создание и управление**.  
  
2.  В hello **перспективы** диалоговое окно, нажмите кнопку **новую перспективу**.  
  
3.  Дважды щелкните hello **новую перспективу** заголовок столбца и переименовать **продажи через Интернет**.  
  
4.  Здравствуйте, выберите все таблицы hello *за исключением* **DimCustomer**.  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    В одном из следующих занятий вы использовать hello анализ в Excel функции tootest этой перспективы. Hello список полей сводной таблицы Excel включает в себя все таблицы, кроме таблица DimCustomer hello.  

## <a name="whats-next"></a>Что дальше?
[Занятие 9. Создание иерархий](../tutorials/aas-lesson-9-create-hierarchies.md).
  
  
  
  
