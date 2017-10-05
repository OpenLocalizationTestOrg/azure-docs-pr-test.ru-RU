---
title: "Как просматривать связанные ресурсы данных в каталоге данных Azure | Документация Майкрософт"
description: "В этой статье объясняется, как просматривать связанные ресурсы данных в каталоге данных Azure."
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
ms.openlocfilehash: d45f2cabe712a7982f99a9d280fed4494fc4d377
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-view-related-data-assets-in-azure-data-catalog"></a><span data-ttu-id="f7eaf-103">Как просматривать связанные ресурсы данных в каталоге данных Azure</span><span class="sxs-lookup"><span data-stu-id="f7eaf-103">How to view related data assets in Azure Data Catalog?</span></span>
<span data-ttu-id="f7eaf-104">Каталог данных Azure позволяет просматривать ресурсы данных, связанные с выбранным ресурсом, и связи между ними.</span><span class="sxs-lookup"><span data-stu-id="f7eaf-104">Azure Data Catalog allows you to view data assets related to a selected data asset and view relationships between them.</span></span> 

## <a name="supported-data-sources"></a><span data-ttu-id="f7eaf-105">Поддерживаемые источники данных</span><span class="sxs-lookup"><span data-stu-id="f7eaf-105">Supported data sources</span></span> 
<span data-ttu-id="f7eaf-106">При регистрации ресурсов данных из следующих источников данных каталог данных Azure автоматически регистрирует метаданные о связях соединения между выбранными ресурсами данных.</span><span class="sxs-lookup"><span data-stu-id="f7eaf-106">When you register data assets from the following data sources, Azure Data Catalog automatically registers metadata about join relationships between the selected data assets.</span></span> 

- <span data-ttu-id="f7eaf-107">SQL Server</span><span class="sxs-lookup"><span data-stu-id="f7eaf-107">SQL Server</span></span>
- <span data-ttu-id="f7eaf-108">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="f7eaf-108">Azure SQL Database</span></span>
- <span data-ttu-id="f7eaf-109">MySQL</span><span class="sxs-lookup"><span data-stu-id="f7eaf-109">MySQL</span></span>
- <span data-ttu-id="f7eaf-110">Oracle</span><span class="sxs-lookup"><span data-stu-id="f7eaf-110">Oracle</span></span>

## <a name="view-related-data-assets"></a><span data-ttu-id="f7eaf-111">Просмотр связанных ресурсов данных</span><span class="sxs-lookup"><span data-stu-id="f7eaf-111">View related data assets</span></span>
<span data-ttu-id="f7eaf-112">Для просмотра ресурсов данных, связанных с выбранным набором данных, используйте вкладку **Связи**, как показано на следующем рисунке:</span><span class="sxs-lookup"><span data-stu-id="f7eaf-112">To view data assets that are related to a selected dataset, use the **Relationships** tab as shown in the following image:</span></span> 

![Просмотр связанных ресурсов данных в каталоге данных Azure](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

<span data-ttu-id="f7eaf-114">В этом примере у выбранного ресурса данных **ProductSubcategory** имеется две связи:</span><span class="sxs-lookup"><span data-stu-id="f7eaf-114">In this example, there are two relationships for the selected **ProductSubcategory** data asset:</span></span> 

- <span data-ttu-id="f7eaf-115">Столбец ProductSubcategoryID таблицы Product имеет связь по внешнему ключу со столбцом ProductSubcategoryID выбранной таблицы ProductSubcategory.</span><span class="sxs-lookup"><span data-stu-id="f7eaf-115">ProductSubcategoryID column of the Product table has a foreign key relationship with ProductSubcategoryID column of the selected ProductSubcategory table.</span></span> 
- <span data-ttu-id="f7eaf-116">Столбец ProductCategoryID таблицы ProductSubCategory имеет связь по внешнему ключу со столбцом ProductCategoryID выбранной таблицы ProductCategory.</span><span class="sxs-lookup"><span data-stu-id="f7eaf-116">ProductCategoryID column of the ProductSubCategory table has a foreign key relationship with ProductCategoryID column of the selected ProductCategory table.</span></span>

> [!NOTE]
> <span data-ttu-id="f7eaf-117">Обратите внимание на направление стрелки в древовидном представлении связей.</span><span class="sxs-lookup"><span data-stu-id="f7eaf-117">Notice the direction of the arrow in the relationships tree view.</span></span>  

<span data-ttu-id="f7eaf-118">Для получения дополнительных сведений, таких как полное имя столбца, наведите на него указатель мыши, и появится всплывающее окно, как на следующем рисунке:</span><span class="sxs-lookup"><span data-stu-id="f7eaf-118">To see more details such as the fully qualified name of the column, move the mouse over and you see a popup similar to the following image:</span></span> 

![Извлечение отношений в каталоге данных Azure](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

<span data-ttu-id="f7eaf-120">Для включения связей между зарегистрированными ресурсами зарегистрируйте их повторно.</span><span class="sxs-lookup"><span data-stu-id="f7eaf-120">To include relationships between assets that have already been registered, re-register those assets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7eaf-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f7eaf-121">Next steps</span></span>
- [<span data-ttu-id="f7eaf-122">Как управлять ресурсами данных</span><span class="sxs-lookup"><span data-stu-id="f7eaf-122">How to manage data assets</span></span>](data-catalog-how-to-manage.md)