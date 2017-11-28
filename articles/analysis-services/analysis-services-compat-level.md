---
title: "уровень совместимости модели aaaData в Azure Analysis Services | Документы Microsoft"
description: "Основные сведения об уровне совместимости табличной модели данных."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/16/2017
ms.author: owend
ms.openlocfilehash: bfaf0c60666729d1e6e0baf082c046ea9faa4e86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a><span data-ttu-id="6d1a6-103">Уровень совместимости табличных моделей Analysis Services</span><span class="sxs-lookup"><span data-stu-id="6d1a6-103">Compatibility level for Analysis Services tabular models</span></span>

<span data-ttu-id="6d1a6-104">*Уровень совместимости* ссылается toorelease поведения в hello ядро служб Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-104">*Compatibility level* refers toorelease-specific behaviors in hello Analysis Services engine.</span></span> <span data-ttu-id="6d1a6-105">Уровень совместимости toohello изменения обычно совпадают с основные выпуски SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-105">Changes toohello compatibility level typically coincide with major releases of SQL Server.</span></span> <span data-ttu-id="6d1a6-106">Эти изменения также реализованы в Azure Analysis Services toomaintain четность между обеих платформах.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-106">These changes are also implemented in Azure Analysis Services toomaintain parity between both platforms.</span></span> <span data-ttu-id="6d1a6-107">Изменения уровня совместимости также влияют на функции, доступные в табличных моделях.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-107">Compatibility level changes also affect features available in your tabular models.</span></span> <span data-ttu-id="6d1a6-108">Например DirectQuery и метаданные табличных объектов имеют разные реализации в зависимости от уровня совместимости hello.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-108">For example, DirectQuery and tabular object metadata have different implementations depending on hello compatibility level.</span></span> 

<span data-ttu-id="6d1a6-109">Azure службы Analysis Services поддерживают табличные модели с уровнем совместимости hello 1200 и 1400.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-109">Azure Analysis Services supports tabular models at hello 1200 and 1400 compatibility levels.</span></span>

<span data-ttu-id="6d1a6-110">Последний уровень совместимости Hello — 1400.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-110">hello latest compatibility level is 1400.</span></span> <span data-ttu-id="6d1a6-111">Этот уровень совпадает с уровнем SQL Server 2017 Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-111">This level coincides with SQL Server 2017 Analysis Services.</span></span> <span data-ttu-id="6d1a6-112">Основные функции на уровне совместимости 1400 hello:</span><span class="sxs-lookup"><span data-stu-id="6d1a6-112">Major features in hello 1400 compatibility level include:</span></span>

*  <span data-ttu-id="6d1a6-113">Новая инфраструктура подключения к данным и импорта в табличные модели с поддержкой интерфейсов API TOM и сценариев TMSL.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-113">New infrastructure for data connectivity and import into tabular models with support for TOM APIs and TMSL scripting.</span></span> <span data-ttu-id="6d1a6-114">Эта новая функция обеспечивает поддержку дополнительных источников данных, таких как хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-114">This new feature enables support for additional data sources such as Azure Blob storage.</span></span>
*  <span data-ttu-id="6d1a6-115">Возможности преобразования и комбинирования данных с помощью выражений Get Data и M.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-115">Data transformation and data mashup capabilities by using Get Data and M expressions.</span></span>
*  <span data-ttu-id="6d1a6-116">Меры поддерживают свойство "Строки детализации" с использованием выражения DAX.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-116">Measures support a Detail Rows property with a DAX expression.</span></span> <span data-ttu-id="6d1a6-117">Это свойство включает клиентские средства, как Microsoft Excel toodrill вниз toodetailed данные из объединенного отчета.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-117">This property enables client tools like Microsoft Excel toodrill down toodetailed data from an aggregated report.</span></span> <span data-ttu-id="6d1a6-118">Например при просмотре общий объем продаж по региону и месяц, они могут просматривать связанные hello подробности заказа.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-118">For example, when users view total sales for a region and month, they can view hello associated order details.</span></span> 
*  <span data-ttu-id="6d1a6-119">Безопасность на уровне объекта для таблицы и столбца имен, кроме toohello содержащихся в них данных.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-119">Object-level security for table and column names, in addition toohello data within them.</span></span>
*  <span data-ttu-id="6d1a6-120">Расширенная поддержка несбалансированных иерархий.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-120">Enhanced support for ragged hierarchies.</span></span>
*  <span data-ttu-id="6d1a6-121">Усовершенствованный мониторинг и повышение производительности.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-121">Performance and monitoring improvements.</span></span>
  
## <a name="set-compatibility-level"></a><span data-ttu-id="6d1a6-122">Установка уровня совместимости</span><span class="sxs-lookup"><span data-stu-id="6d1a6-122">Set compatibility level</span></span> 
 <span data-ttu-id="6d1a6-123">При создании нового проекта табличной модели в SSDT, вы можете указать уровень совместимости hello на hello **конструктор табличных моделей** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-123">When creating a new tabular model project in SSDT, you can specify hello compatibility level on hello **Tabular model designer** dialog.</span></span> 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 <span data-ttu-id="6d1a6-125">При выборе hello **больше не показывать это сообщение** , во всех последующих проектах использовать указанное по умолчанию hello уровень совместимости hello.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-125">If you select hello **Do not show this message again** option, all subsequent projects use hello compatibility level you specified as hello default.</span></span> <span data-ttu-id="6d1a6-126">Можно изменить уровень совместимости по умолчанию hello в SSDT в **средства** > **параметры**.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-126">You can change hello default compatibility level in SSDT in **Tools** > **Options**.</span></span>  
  
 <span data-ttu-id="6d1a6-127">tooupgrade существующего проекта табличной модели в SSDT, набор hello **уровень совместимости** свойства в модели hello **свойства** окна.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-127">tooupgrade an existing tabular model project in SSDT, set  hello **Compatibility Level** property in hello model **Properties** window.</span></span> <span data-ttu-id="6d1a6-128">Имейте в виду, обновление уровня совместимости hello является необратимым.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-128">Keep in-mind, upgrading hello compatibility level is irreversible.</span></span>
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a><span data-ttu-id="6d1a6-129">Проверка уровня совместимости базы данных табличной модели в SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="6d1a6-129">Check compatibility level for a tabular model database in SQL Server Management Studio</span></span> 
 <span data-ttu-id="6d1a6-130">В среде SSMS щелкните правой кнопкой мыши имя базы данных hello > **свойства** > **уровень совместимости**.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-130">In SSMS, right-click hello database name > **Properties** > **Compatibility Level**.</span></span>  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a><span data-ttu-id="6d1a6-131">Проверка поддерживаемого уровня совместимости сервера в SSMS</span><span class="sxs-lookup"><span data-stu-id="6d1a6-131">Check supported compatibility level for a server in SSMS</span></span>  
 <span data-ttu-id="6d1a6-132">В среде SSMS щелкните правой кнопкой мыши имя сервера hello > **свойства** > **поддерживаемый уровень совместимости**.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-132">In SSMS, right-click hello server name>  **Properties** > **Supported Compatibility Level**.</span></span>  
  
 <span data-ttu-id="6d1a6-133">Это свойство указывает hello наивысший уровень совместимости базы данных, которая будет выполняться на сервере hello (без предварительной версии).</span><span class="sxs-lookup"><span data-stu-id="6d1a6-133">This property specifies hello highest compatibility level of a database that will run on hello server (excluding preview).</span></span> <span data-ttu-id="6d1a6-134">Невозможно изменить уровень совместимости Hello поддерживается.</span><span class="sxs-lookup"><span data-stu-id="6d1a6-134">hello supported compatibility level cannot be changed.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="6d1a6-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6d1a6-135">Next steps</span></span>
  <span data-ttu-id="6d1a6-136">[Создание модели на портале Azure](analysis-services-create-model-portal.md) </span><span class="sxs-lookup"><span data-stu-id="6d1a6-136">[Create a model in Azure portal](analysis-services-create-model-portal.md) </span></span>  
  [<span data-ttu-id="6d1a6-137">Управление службами Analysis Services</span><span class="sxs-lookup"><span data-stu-id="6d1a6-137">Manage Analysis Services</span></span>](analysis-services-manage.md)  
