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
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a><span data-ttu-id="b897e-103">Как tooview связаны ресурсов данных в каталоге данных Azure?</span><span class="sxs-lookup"><span data-stu-id="b897e-103">How tooview related data assets in Azure Data Catalog?</span></span>
<span data-ttu-id="b897e-104">Каталог данных Azure позволяет tooview данных активы связанные tooa выбранных данных активов и представления отношений между ними.</span><span class="sxs-lookup"><span data-stu-id="b897e-104">Azure Data Catalog allows you tooview data assets related tooa selected data asset and view relationships between them.</span></span> 

## <a name="supported-data-sources"></a><span data-ttu-id="b897e-105">Поддерживаемые источники данных</span><span class="sxs-lookup"><span data-stu-id="b897e-105">Supported data sources</span></span> 
<span data-ttu-id="b897e-106">При регистрации ресурсов данных от hello следующие источники данных каталога данных Azure автоматически регистрирует метаданные о связи соединения между ресурсами hello выбранных данных.</span><span class="sxs-lookup"><span data-stu-id="b897e-106">When you register data assets from hello following data sources, Azure Data Catalog automatically registers metadata about join relationships between hello selected data assets.</span></span> 

- <span data-ttu-id="b897e-107">SQL Server</span><span class="sxs-lookup"><span data-stu-id="b897e-107">SQL Server</span></span>
- <span data-ttu-id="b897e-108">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="b897e-108">Azure SQL Database</span></span>
- <span data-ttu-id="b897e-109">MySQL</span><span class="sxs-lookup"><span data-stu-id="b897e-109">MySQL</span></span>
- <span data-ttu-id="b897e-110">Oracle</span><span class="sxs-lookup"><span data-stu-id="b897e-110">Oracle</span></span>

## <a name="view-related-data-assets"></a><span data-ttu-id="b897e-111">Просмотр связанных ресурсов данных</span><span class="sxs-lookup"><span data-stu-id="b897e-111">View related data assets</span></span>
<span data-ttu-id="b897e-112">ресурсы данных tooview, связанные tooa выбранного набора данных, используйте hello **связи** вкладки, как показано в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="b897e-112">tooview data assets that are related tooa selected dataset, use hello **Relationships** tab as shown in hello following image:</span></span> 

![Просмотр связанных ресурсов данных в каталоге данных Azure](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

<span data-ttu-id="b897e-114">В этом примере имеются два отношения для выбранных hello **ProductSubcategory** ресурса данных:</span><span class="sxs-lookup"><span data-stu-id="b897e-114">In this example, there are two relationships for hello selected **ProductSubcategory** data asset:</span></span> 

- <span data-ttu-id="b897e-115">ProductSubcategoryID столбец из таблицы Product hello имеет связь по внешнему ключу со столбцом ProductSubcategoryID hello выбранные таблицы ProductSubcategory.</span><span class="sxs-lookup"><span data-stu-id="b897e-115">ProductSubcategoryID column of hello Product table has a foreign key relationship with ProductSubcategoryID column of hello selected ProductSubcategory table.</span></span> 
- <span data-ttu-id="b897e-116">Столбец ProductCategoryID таблицы ProductSubCategory hello имеет связь по внешнему ключу со столбцом ProductCategoryID hello выбранные таблицы ProductCategory.</span><span class="sxs-lookup"><span data-stu-id="b897e-116">ProductCategoryID column of hello ProductSubCategory table has a foreign key relationship with ProductCategoryID column of hello selected ProductCategory table.</span></span>

> [!NOTE]
> <span data-ttu-id="b897e-117">Обратите внимание, hello направление стрелки hello в древовидном представлении связей hello.</span><span class="sxs-lookup"><span data-stu-id="b897e-117">Notice hello direction of hello arrow in hello relationships tree view.</span></span>  

<span data-ttu-id="b897e-118">toosee Дополнительные сведения, такие как полное имя столбца hello hello наведите указатель мыши hello и вывести примерно toohello всплывающее окно, следуя образа:</span><span class="sxs-lookup"><span data-stu-id="b897e-118">toosee more details such as hello fully qualified name of hello column, move hello mouse over and you see a popup similar toohello following image:</span></span> 

![Извлечение отношений в каталоге данных Azure](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

<span data-ttu-id="b897e-120">tooinclude связи между ресурсами, которые уже были зарегистрированы, повторите регистрацию этих ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b897e-120">tooinclude relationships between assets that have already been registered, re-register those assets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b897e-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b897e-121">Next steps</span></span>
- [<span data-ttu-id="b897e-122">Как toomanage ресурсов данных</span><span class="sxs-lookup"><span data-stu-id="b897e-122">How toomanage data assets</span></span>](data-catalog-how-to-manage.md)
