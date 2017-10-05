---
title: "Сохранение поисков и закрепление ресурсов данных в каталоге данных Azure | Документы Майкрософт"
description: "Это практическое руководство описывает возможности каталога данных Azure, позволяющие сохранять источники и ресурсы данных для последующего использования."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 8c319d0dcbe8b95af11b8be2368a9348b260446c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a><span data-ttu-id="0af94-103">Сохранение поисков и закрепление ресурсов данных в каталоге данных Azure</span><span class="sxs-lookup"><span data-stu-id="0af94-103">Save searches and pin data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="0af94-104">Введение</span><span class="sxs-lookup"><span data-stu-id="0af94-104">Introduction</span></span>
<span data-ttu-id="0af94-105">Каталог данных Azure предоставляет возможности для обнаружения источников данных.</span><span class="sxs-lookup"><span data-stu-id="0af94-105">Azure Data Catalog provides capabilities for data source discovery.</span></span> <span data-ttu-id="0af94-106">Вы можете выполнять быстрый поиск и фильтрацию в каталоге, чтобы находить источники данных и понимать их назначение. Это упрощает поиск нужной информации для текущего задания.</span><span class="sxs-lookup"><span data-stu-id="0af94-106">You can quickly search and filter the catalog to locate data sources and understand their intended purpose, making it easier to find the right data for the job at hand.</span></span>

<span data-ttu-id="0af94-107">Но что делать, если нужно регулярно работать с одними и теми же данными?</span><span class="sxs-lookup"><span data-stu-id="0af94-107">But what if you need to regularly work with the same data?</span></span> <span data-ttu-id="0af94-108">А если при этом вы и другие пользователи регулярно добавляете информацию в одни и те же источники данных в каталоге?</span><span class="sxs-lookup"><span data-stu-id="0af94-108">And what if you and other users regularly contribute your knowledge to the same data sources in the catalog?</span></span> <span data-ttu-id="0af94-109">В таких ситуациях повторный поиск по одним и тем же запросам может оказаться неэффективным.</span><span class="sxs-lookup"><span data-stu-id="0af94-109">In these situations, having to repeatedly issue the same searches can be inefficient.</span></span> <span data-ttu-id="0af94-110">Здесь вам могут помочь сохраненные поиски и закрепленные ресурсы данных.</span><span class="sxs-lookup"><span data-stu-id="0af94-110">This is where saved search and pinned data assets can help.</span></span>

## <a name="saved-searches"></a><span data-ttu-id="0af94-111">Сохраненные поисковые запросы</span><span class="sxs-lookup"><span data-stu-id="0af94-111">Saved searches</span></span>
<span data-ttu-id="0af94-112">Сохраненный поиск в каталоге данных — это многократно используемое каким-либо пользователем определение поиска.</span><span class="sxs-lookup"><span data-stu-id="0af94-112">A saved search in Data Catalog is a reusable, per-user search definition.</span></span> <span data-ttu-id="0af94-113">Вы можете определить поиск, включая условия поиска, теги и другие фильтры, а затем сохранить его.</span><span class="sxs-lookup"><span data-stu-id="0af94-113">You can define a search, including search terms, tags, and other filters, and then save it.</span></span> <span data-ttu-id="0af94-114">Позднее вы можете повторно использовать сохраненное определение поиска, чтобы найти все ресурсы данных, соответствующие условиям поиска.</span><span class="sxs-lookup"><span data-stu-id="0af94-114">You can re-run the saved search definition later to return any data assets that match its search criteria.</span></span>

### <a name="create-a-saved-search"></a><span data-ttu-id="0af94-115">Создание сохраненного поиска</span><span class="sxs-lookup"><span data-stu-id="0af94-115">Create a saved search</span></span>
<span data-ttu-id="0af94-116">Чтобы создать сохраненный поиск, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="0af94-116">To create a saved search, do the following:</span></span>
1. <span data-ttu-id="0af94-117">В окне **Текущий поиск** на портале каталога данных Azure щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0af94-117">In the Azure Data Catalog portal, in the **Current Search** window, click **Save**.</span></span> 

    ![Ссылка "Сохранить" в параметрах текущего поиска](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. <span data-ttu-id="0af94-119">Введите условия поиска, которые хотите использовать повторно, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0af94-119">Enter the search criteria that you want to reuse, and then click **Save**.</span></span>

    ![Имя сохраненного поиска в параметрах текущего поиска](./media/data-catalog-how-to-save-pin/02-name.png)

3. <span data-ttu-id="0af94-121">При появлении запроса введите имя сохраненного поиска.</span><span class="sxs-lookup"><span data-stu-id="0af94-121">When you are prompted, enter a name for the saved search.</span></span> <span data-ttu-id="0af94-122">Выберите информативное описательное имя для ресурсов данных, которые будут возвращаться при выполнении поиска.</span><span class="sxs-lookup"><span data-stu-id="0af94-122">Pick a name that is meaningful and that describes the data assets that will be returned by the search.</span></span>

### <a name="manage-saved-searches"></a><span data-ttu-id="0af94-123">Управление сохраненными поисками</span><span class="sxs-lookup"><span data-stu-id="0af94-123">Manage saved searches</span></span>
<span data-ttu-id="0af94-124">После сохранения одного или нескольких поисков под полем **Текущий поиск** отображается параметр **Сохраненные условия поиска**.</span><span class="sxs-lookup"><span data-stu-id="0af94-124">After you have saved one or more searches, a **Saved Searches** option is displayed beneath the **Current Search** box.</span></span> <span data-ttu-id="0af94-125">При развертывании списка отображаются все сохраненные поиски.</span><span class="sxs-lookup"><span data-stu-id="0af94-125">When the list is expanded, all saved searches are displayed.</span></span>

 ![Список сохраненных поисковых запросов](./media/data-catalog-how-to-save-pin/03-list.png)

<span data-ttu-id="0af94-127">Выполните одно из следующих действий.</span><span class="sxs-lookup"><span data-stu-id="0af94-127">Do any of the following:</span></span>

* <span data-ttu-id="0af94-128">Чтобы выполнить поиск, выберите сохраненный поиск в списке.</span><span class="sxs-lookup"><span data-stu-id="0af94-128">To execute a search, select a saved search in the list.</span></span>

* <span data-ttu-id="0af94-129">Чтобы просмотреть список параметров управления для сохраненного поиска, щелкните стрелку вниз рядом с именем поиска.</span><span class="sxs-lookup"><span data-stu-id="0af94-129">To view a list of management options for a saved search, click the down arrow next to the search name.</span></span>

    ![Команды для управления сохраненными поисковыми запросами](./media/data-catalog-how-to-save-pin/04-managing.png)

* <span data-ttu-id="0af94-131">Чтобы ввести новое имя для сохраненного поиска, выберите **Переименовать**.</span><span class="sxs-lookup"><span data-stu-id="0af94-131">To enter a new name for the saved search, select **Rename**.</span></span> <span data-ttu-id="0af94-132">Определение поиска не меняется.</span><span class="sxs-lookup"><span data-stu-id="0af94-132">The search definition is not changed.</span></span>

* <span data-ttu-id="0af94-133">Чтобы удалить сохраненный поиск из списка, выберите **Удалить** и подтвердите операцию.</span><span class="sxs-lookup"><span data-stu-id="0af94-133">To remove the saved search from your list, select **Delete**, and then confirm the deletion.</span></span>

* <span data-ttu-id="0af94-134">Чтобы пометить сохраненный поиск в качестве используемого по умолчанию, выберите **Сохранить по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="0af94-134">To mark the saved search as your default search, select **Save As Default**.</span></span> <span data-ttu-id="0af94-135">Если вы выполняете поиск с пустыми условиями на домашней странице каталога данных Azure, выполняется ваш поиск по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="0af94-135">If you perform an “empty” search from the Azure Data Catalog home page, your default search is executed.</span></span> <span data-ttu-id="0af94-136">Кроме того, поиск, помеченный как используемый по умолчанию, отображается в верхней части списка **Сохраненные условия поиска**.</span><span class="sxs-lookup"><span data-stu-id="0af94-136">In addition, the search that's marked as the default search is displayed at the top of the **Saved Searches** list.</span></span>

### <a name="organizational-saved-searches"></a><span data-ttu-id="0af94-137">Сохраненные поиски организации</span><span class="sxs-lookup"><span data-stu-id="0af94-137">Organizational saved searches</span></span>
<span data-ttu-id="0af94-138">Каждый пользователь вашей организации может сохранять поиски для собственных нужд.</span><span class="sxs-lookup"><span data-stu-id="0af94-138">All user in your organization can save searches for their own use.</span></span> <span data-ttu-id="0af94-139">Администраторы каталога данных могут также сохранять поиски всех пользователей в организации.</span><span class="sxs-lookup"><span data-stu-id="0af94-139">Data Catalog administrators can also save searches for all users within the organization.</span></span> <span data-ttu-id="0af94-140">Когда администраторы сохраняют поиск, им доступен параметр **Поделиться в компании**.</span><span class="sxs-lookup"><span data-stu-id="0af94-140">When administrators save a search, they're presented with a **Share within the company** option.</span></span> <span data-ttu-id="0af94-141">При его выборе сохраненный поиск предоставляется для общего доступа всем пользователям в организации.</span><span class="sxs-lookup"><span data-stu-id="0af94-141">Selecting this option shares the saved search for all users in the organization.</span></span>

 ![Сохраненные поиски организации](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a><span data-ttu-id="0af94-143">Закрепленные ресурсы данных</span><span class="sxs-lookup"><span data-stu-id="0af94-143">Pinned data assets</span></span>
<span data-ttu-id="0af94-144">С помощью сохраненных поисков можно сохранять и использовать повторно определения поиска.</span><span class="sxs-lookup"><span data-stu-id="0af94-144">With saved searches, you can save and reuse search definitions.</span></span> <span data-ttu-id="0af94-145">Ресурсы данных, возвращаемые при поиске, могут меняться со временем, при изменении содержимого каталога.</span><span class="sxs-lookup"><span data-stu-id="0af94-145">The data assets that are returned by the searches might change over time as the contents of the catalog change.</span></span> <span data-ttu-id="0af94-146">Когда вы закрепляете ресурсы данных, то можете явно указывать конкретные ресурсы, что обеспечивает удобный доступ к ним без необходимости использовать поиск.</span><span class="sxs-lookup"><span data-stu-id="0af94-146">When you pin data assets, you can explicitly identify specific data assets to make them easier to access without needing to use a search.</span></span>

<span data-ttu-id="0af94-147">Закрепление ресурса данных не представляет никаких трудностей.</span><span class="sxs-lookup"><span data-stu-id="0af94-147">Pinning a data asset is straightforward.</span></span> <span data-ttu-id="0af94-148">Чтобы добавить ресурс данных в закрепленный список, просто щелкните значок **Закрепить**.</span><span class="sxs-lookup"><span data-stu-id="0af94-148">To add the data asset to your pinned list, you simply click the **pin** icon.</span></span> <span data-ttu-id="0af94-149">Этот значок отображается в углу плитки ресурсов в представлении плиток, а также в крайнем левом столбце в представлении списка на портале каталога данных Azure.</span><span class="sxs-lookup"><span data-stu-id="0af94-149">The icon is displayed in the corner of the asset tile in the tile view, and in the left-most column in the list view in the Azure Data Catalog portal.</span></span>

![Значок закрепления ресурса данных](./media/data-catalog-how-to-save-pin/05-pinning.png)

<span data-ttu-id="0af94-151">Открепление ресурса данных выполняется так же просто.</span><span class="sxs-lookup"><span data-stu-id="0af94-151">Unpinning a data asset is equally straightforward.</span></span> <span data-ttu-id="0af94-152">Щелкните значок **Открепить**, чтобы переключить параметр для выбранного ресурса.</span><span class="sxs-lookup"><span data-stu-id="0af94-152">Simply click the **unpin** icon to toggle the setting for the selected asset.</span></span>

![Значок открепления ресурса данных](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="the-my-assets-section"></a><span data-ttu-id="0af94-154">Раздел "Мои ресурсы"</span><span class="sxs-lookup"><span data-stu-id="0af94-154">The My Assets section</span></span>
<span data-ttu-id="0af94-155">На портале каталога данных есть домашняя страница с разделом **Мои ресурсы**. Здесь отображаются ресурсы, которые представляют интерес для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="0af94-155">The Data Catalog portal home page includes a **My Assets** section that displays assets of interest to the current user.</span></span> <span data-ttu-id="0af94-156">Этот раздел включает как закрепленные ресурсы, так и сохраненные поисковые запросы.</span><span class="sxs-lookup"><span data-stu-id="0af94-156">This section includes both pinned assets and saved searches.</span></span>

![Раздел "Мои ресурсы" на домашней странице](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a><span data-ttu-id="0af94-158">Сводка</span><span class="sxs-lookup"><span data-stu-id="0af94-158">Summary</span></span>
<span data-ttu-id="0af94-159">Каталог данных Azure предоставляет возможности, которые упрощают поиск нужных источников данных. Поэтому вы и другие сотрудники организации можете тратить меньше времени на поиск данных и больше — на работу с ними.</span><span class="sxs-lookup"><span data-stu-id="0af94-159">Azure Data Catalog provides capabilities that make it easier to discover the data sources you need, so you and other organization members can spend less time looking for data and more time working with it.</span></span> <span data-ttu-id="0af94-160">На базе этих основных возможностей реализованы функции сохраненных поисков и закрепленных ресурсов данных, позволяющие пользователям легко находить источники данных, с которыми они работают регулярно.</span><span class="sxs-lookup"><span data-stu-id="0af94-160">Saved searches and pinned data assets build on these core capabilities so users can easily identify data sources that they work with repeatedly.</span></span>
