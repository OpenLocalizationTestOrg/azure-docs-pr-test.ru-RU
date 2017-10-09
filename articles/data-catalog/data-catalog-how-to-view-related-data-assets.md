---
title: "ресурсы данных в каталоге данных Azure, связанных с aaaHow tooview | Документы Microsoft"
description: "В этой статье объясняется, как tooview связанные ресурсы данных выбранные данные средства в каталоге данных Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: b69686737070ac563a0318f48e693215c605f90b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a>Как tooview связаны ресурсов данных в каталоге данных Azure?
Каталог данных Azure позволяет tooview данных активы связанные tooa выбранных данных активов и представления отношений между ними. 

## <a name="supported-data-sources"></a>Поддерживаемые источники данных 
При регистрации ресурсов данных от hello следующие источники данных каталога данных Azure автоматически регистрирует метаданные о связи соединения между ресурсами hello выбранных данных. 

- SQL Server
- База данных SQL Azure
- MySQL
- Oracle

## <a name="view-related-data-assets"></a>Просмотр связанных ресурсов данных
ресурсы данных tooview, связанные tooa выбранного набора данных, используйте hello **связи** вкладки, как показано в hello после изображения: 

![Просмотр связанных ресурсов данных в каталоге данных Azure](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

В этом примере имеются два отношения для выбранных hello **ProductSubcategory** ресурса данных: 

- ProductSubcategoryID столбец из таблицы Product hello имеет связь по внешнему ключу со столбцом ProductSubcategoryID hello выбранные таблицы ProductSubcategory. 
- Столбец ProductCategoryID таблицы ProductSubCategory hello имеет связь по внешнему ключу со столбцом ProductCategoryID hello выбранные таблицы ProductCategory.

> [!NOTE]
> Обратите внимание, hello направление стрелки hello в древовидном представлении связей hello.  

toosee Дополнительные сведения, такие как полное имя столбца hello hello наведите указатель мыши hello и вывести примерно toohello всплывающее окно, следуя образа: 

![Извлечение отношений в каталоге данных Azure](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

tooinclude связи между ресурсами, которые уже были зарегистрированы, повторите регистрацию этих ресурсов.

## <a name="next-steps"></a>Дальнейшие действия
- [Как toomanage ресурсов данных](data-catalog-how-to-manage.md)
