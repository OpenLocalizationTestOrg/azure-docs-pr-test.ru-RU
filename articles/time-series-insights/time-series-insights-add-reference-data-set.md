---
title: "aaaAdd набор данных ссылается на tooyour аналитики ряда времени Azure среду | Документы Microsoft"
description: "В этом учебнике добавить набор данных ссылается на среду аналитики ряда времени tooyour"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 05e626ed81a22f2a8710b23a931ccd17c0f38ca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a><span data-ttu-id="2eff8-103">Создание эталонного набора данных для среды времени серии аналитики портале Ibiza hello</span><span class="sxs-lookup"><span data-stu-id="2eff8-103">Create a reference data set for your Time Series Insights environment using hello Ibiza portal</span></span>

<span data-ttu-id="2eff8-104">Эталонного набора данных — это совокупность элементов, которые вместе со hello события из источника событий.</span><span class="sxs-lookup"><span data-stu-id="2eff8-104">A Reference Data Set is a collection of items that are augmented with hello events from your event source.</span></span> <span data-ttu-id="2eff8-105">Обработчик входящего трафика Time Series Insights соединяет событие из источника события с элементом в эталонном наборе данных.</span><span class="sxs-lookup"><span data-stu-id="2eff8-105">Time Series Insights ingress engine joins an event from your event source with an item in your reference data set.</span></span> <span data-ttu-id="2eff8-106">Это дополненное событие становится доступным для запроса.</span><span class="sxs-lookup"><span data-stu-id="2eff8-106">This augmented event is then available for query.</span></span> <span data-ttu-id="2eff8-107">Это соединение основано на hello ключи, определенные в наборе данных ссылок.</span><span class="sxs-lookup"><span data-stu-id="2eff8-107">This join is based on hello keys defined in your reference data set.</span></span>

## <a name="steps-tooadd-a-reference-data-set-tooyour-environment"></a><span data-ttu-id="2eff8-108">Tooadd действия tooyour набор данных ссылается на среду</span><span class="sxs-lookup"><span data-stu-id="2eff8-108">Steps tooadd a reference data set tooyour environment</span></span>

1. <span data-ttu-id="2eff8-109">Войдите в toohello [портал Ibiza](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2eff8-109">Sign in toohello [Ibiza portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2eff8-110">Выберите «Все ресурсы» в меню hello hello левой части портала Ibiza hello.</span><span class="sxs-lookup"><span data-stu-id="2eff8-110">Click “All resources” in hello menu on hello left side of hello Ibiza portal.</span></span>
3. <span data-ttu-id="2eff8-111">Выберите среду Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="2eff8-111">Select your Time Series Insights environment.</span></span>

    ![Создание аналитики ряда времени hello эталонного набора данных](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. <span data-ttu-id="2eff8-113">Выберите "Эталонные наборы данных" и щелкните "+ Добавить".</span><span class="sxs-lookup"><span data-stu-id="2eff8-113">Select “Reference Data Sets”, click “+ Add.”</span></span>

    ![Создать набор данных ссылки аналитики ряда времени hello - подробные сведения](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. <span data-ttu-id="2eff8-115">Укажите имя hello hello эталонного набора данных.</span><span class="sxs-lookup"><span data-stu-id="2eff8-115">Specify hello name of hello reference data set.</span></span>
6. <span data-ttu-id="2eff8-116">Укажите имя ключа hello и его тип.</span><span class="sxs-lookup"><span data-stu-id="2eff8-116">Specify hello key name and its type.</span></span> <span data-ttu-id="2eff8-117">Эти имя и тип — правильный свойство используется toopick hello из события hello в источник события.</span><span class="sxs-lookup"><span data-stu-id="2eff8-117">This name and type is used toopick hello correct property from hello event in your event source.</span></span> <span data-ttu-id="2eff8-118">Например если вы указали имя ключа как «DeviceId» и типом «String», hello аналитики ряда времени ядра входящих ищет свойство с именем hello «DeviceId» типа «Строка» hello входящего события.</span><span class="sxs-lookup"><span data-stu-id="2eff8-118">For instance, if you provide key name as “DeviceId” and type as “String”, then hello Time Series Insights ingress engine looks for a property with hello name “DeviceId” of type “String” in hello incoming event.</span></span> <span data-ttu-id="2eff8-119">Вы можете предоставить более одного ключа toojoin hello событий.</span><span class="sxs-lookup"><span data-stu-id="2eff8-119">You can provide more than one key toojoin with hello event.</span></span> <span data-ttu-id="2eff8-120">совпадение имени свойства Hello учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="2eff8-120">hello property name match is case-sensitive.</span></span>

     ![Создать набор данных ссылки аналитики ряда времени hello - подробные сведения](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. <span data-ttu-id="2eff8-122">Щелкните "Создать".</span><span class="sxs-lookup"><span data-stu-id="2eff8-122">Click “Create.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="2eff8-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2eff8-123">Next steps</span></span>

* <span data-ttu-id="2eff8-124">[Управление эталонными данными](time-series-insights-manage-reference-data-csharp.md) программными средствами.</span><span class="sxs-lookup"><span data-stu-id="2eff8-124">[Manage reference data](time-series-insights-manage-reference-data-csharp.md) programmatically.</span></span>
* <span data-ttu-id="2eff8-125">Hello полный Справочник по API, в разделе [Справочник по API-Интерфейс данных](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) документа.</span><span class="sxs-lookup"><span data-stu-id="2eff8-125">For hello complete API reference, see [Reference Data API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) document.</span></span>
