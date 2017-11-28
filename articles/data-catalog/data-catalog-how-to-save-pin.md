---
title: "aaaSave поиск и ресурсы данных ПИН-код в каталоге данных Azure | Документы Microsoft"
description: "Как tooarticle выделения возможности в каталоге данных Azure для сохранения источники данных и ресурсы данных для последующего использования."
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
ms.openlocfilehash: 0ad0a31d4b84782fed9d80acc2734912eecd6d74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a><span data-ttu-id="cc118-103">Сохранение поисков и закрепление ресурсов данных в каталоге данных Azure</span><span class="sxs-lookup"><span data-stu-id="cc118-103">Save searches and pin data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="cc118-104">Введение</span><span class="sxs-lookup"><span data-stu-id="cc118-104">Introduction</span></span>
<span data-ttu-id="cc118-105">Каталог данных Azure предоставляет возможности для обнаружения источников данных.</span><span class="sxs-lookup"><span data-stu-id="cc118-105">Azure Data Catalog provides capabilities for data source discovery.</span></span> <span data-ttu-id="cc118-106">Можно быстро поиска и фильтрации источников данных toolocate каталога hello и понимать их назначение, сделав его проще правильные данные toofind hello для задания hello под рукой.</span><span class="sxs-lookup"><span data-stu-id="cc118-106">You can quickly search and filter hello catalog toolocate data sources and understand their intended purpose, making it easier toofind hello right data for hello job at hand.</span></span>

<span data-ttu-id="cc118-107">Но что делать, если необходимо tooregularly работать с hello же данных?</span><span class="sxs-lookup"><span data-stu-id="cc118-107">But what if you need tooregularly work with hello same data?</span></span> <span data-ttu-id="cc118-108">Что делать, если вы и другие пользователи регулярно входят toohello вашей базы знаний и же источники данных в каталоге hello?</span><span class="sxs-lookup"><span data-stu-id="cc118-108">And what if you and other users regularly contribute your knowledge toohello same data sources in hello catalog?</span></span> <span data-ttu-id="cc118-109">В таких ситуациях возникла проблема toorepeatedly hello же поиск может быть неэффективным.</span><span class="sxs-lookup"><span data-stu-id="cc118-109">In these situations, having toorepeatedly issue hello same searches can be inefficient.</span></span> <span data-ttu-id="cc118-110">Здесь вам могут помочь сохраненные поиски и закрепленные ресурсы данных.</span><span class="sxs-lookup"><span data-stu-id="cc118-110">This is where saved search and pinned data assets can help.</span></span>

## <a name="saved-searches"></a><span data-ttu-id="cc118-111">Сохраненные поисковые запросы</span><span class="sxs-lookup"><span data-stu-id="cc118-111">Saved searches</span></span>
<span data-ttu-id="cc118-112">Сохраненный поиск в каталоге данных — это многократно используемое каким-либо пользователем определение поиска.</span><span class="sxs-lookup"><span data-stu-id="cc118-112">A saved search in Data Catalog is a reusable, per-user search definition.</span></span> <span data-ttu-id="cc118-113">Вы можете определить поиск, включая условия поиска, теги и другие фильтры, а затем сохранить его.</span><span class="sxs-lookup"><span data-stu-id="cc118-113">You can define a search, including search terms, tags, and other filters, and then save it.</span></span> <span data-ttu-id="cc118-114">Можно повторно запустить определения поиска hello сохранить более поздней версии tooreturn активы любые данные, соответствующие условиям поиска.</span><span class="sxs-lookup"><span data-stu-id="cc118-114">You can re-run hello saved search definition later tooreturn any data assets that match its search criteria.</span></span>

### <a name="create-a-saved-search"></a><span data-ttu-id="cc118-115">Создание сохраненного поиска</span><span class="sxs-lookup"><span data-stu-id="cc118-115">Create a saved search</span></span>
<span data-ttu-id="cc118-116">toocreate сохраненного поиска hello следующие:</span><span class="sxs-lookup"><span data-stu-id="cc118-116">toocreate a saved search, do hello following:</span></span>
1. <span data-ttu-id="cc118-117">На портале каталога данных Azure hello в hello **текущего поиска** окно, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cc118-117">In hello Azure Data Catalog portal, in hello **Current Search** window, click **Save**.</span></span> 

    ![Ссылка "Сохранить" в параметрах текущего поиска](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. <span data-ttu-id="cc118-119">Введите критерии поиска hello требуется tooreuse и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cc118-119">Enter hello search criteria that you want tooreuse, and then click **Save**.</span></span>

    ![Имя сохраненного поиска в параметрах текущего поиска](./media/data-catalog-how-to-save-pin/02-name.png)

3. <span data-ttu-id="cc118-121">Когда вам будет предложено, введите имя сохраненного поиска hello.</span><span class="sxs-lookup"><span data-stu-id="cc118-121">When you are prompted, enter a name for hello saved search.</span></span> <span data-ttu-id="cc118-122">Выберите понятное имя и, описывающий hello ресурсов данных, возвращаемых при поиске hello.</span><span class="sxs-lookup"><span data-stu-id="cc118-122">Pick a name that is meaningful and that describes hello data assets that will be returned by hello search.</span></span>

### <a name="manage-saved-searches"></a><span data-ttu-id="cc118-123">Управление сохраненными поисками</span><span class="sxs-lookup"><span data-stu-id="cc118-123">Manage saved searches</span></span>
<span data-ttu-id="cc118-124">После сохранения одного или нескольких результатов поиска, **сохраненные поиски** параметр отображается под hello **текущего поиска** поле.</span><span class="sxs-lookup"><span data-stu-id="cc118-124">After you have saved one or more searches, a **Saved Searches** option is displayed beneath hello **Current Search** box.</span></span> <span data-ttu-id="cc118-125">При развертывании списка hello отображаются все сохраненные поисковые запросы.</span><span class="sxs-lookup"><span data-stu-id="cc118-125">When hello list is expanded, all saved searches are displayed.</span></span>

 ![Список сохраненных поисковых запросов](./media/data-catalog-how-to-save-pin/03-list.png)

<span data-ttu-id="cc118-127">Выполните одно из следующих hello.</span><span class="sxs-lookup"><span data-stu-id="cc118-127">Do any of hello following:</span></span>

* <span data-ttu-id="cc118-128">tooexecute поиска выберите сохраненный запрос поиска в списке hello.</span><span class="sxs-lookup"><span data-stu-id="cc118-128">tooexecute a search, select a saved search in hello list.</span></span>

* <span data-ttu-id="cc118-129">tooview список параметров управления сохраненного поиска щелкните hello вниз стрелку далее имя поиска toohello.</span><span class="sxs-lookup"><span data-stu-id="cc118-129">tooview a list of management options for a saved search, click hello down arrow next toohello search name.</span></span>

    ![Команды для управления сохраненными поисковыми запросами](./media/data-catalog-how-to-save-pin/04-managing.png)

* <span data-ttu-id="cc118-131">Выберите новое имя для поиска сохранены hello tooenter **переименование**.</span><span class="sxs-lookup"><span data-stu-id="cc118-131">tooenter a new name for hello saved search, select **Rename**.</span></span> <span data-ttu-id="cc118-132">Определение поиска Hello не изменяется.</span><span class="sxs-lookup"><span data-stu-id="cc118-132">hello search definition is not changed.</span></span>

* <span data-ttu-id="cc118-133">tooremove hello сохранен поиска из списка, выберите **удалить**, а затем подтвердите удаление hello.</span><span class="sxs-lookup"><span data-stu-id="cc118-133">tooremove hello saved search from your list, select **Delete**, and then confirm hello deletion.</span></span>

* <span data-ttu-id="cc118-134">toomark hello сохраненные условия поиска в виде поиска по умолчанию, выберите **Сохранить как значение по умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="cc118-134">toomark hello saved search as your default search, select **Save As Default**.</span></span> <span data-ttu-id="cc118-135">Если выполнить поиск по «empty» на домашней странице hello каталога данных Azure, при выполнении поиска по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cc118-135">If you perform an “empty” search from hello Azure Data Catalog home page, your default search is executed.</span></span> <span data-ttu-id="cc118-136">Кроме того, Здравствуйте, поиск, который помечен как поиска по умолчанию hello отображается вверху hello hello **сохраненные поиски** списка.</span><span class="sxs-lookup"><span data-stu-id="cc118-136">In addition, hello search that's marked as hello default search is displayed at hello top of hello **Saved Searches** list.</span></span>

### <a name="organizational-saved-searches"></a><span data-ttu-id="cc118-137">Сохраненные поиски организации</span><span class="sxs-lookup"><span data-stu-id="cc118-137">Organizational saved searches</span></span>
<span data-ttu-id="cc118-138">Каждый пользователь вашей организации может сохранять поиски для собственных нужд.</span><span class="sxs-lookup"><span data-stu-id="cc118-138">All user in your organization can save searches for their own use.</span></span> <span data-ttu-id="cc118-139">Администраторы каталога данных можно также сохранить ищет всех пользователей в организации hello.</span><span class="sxs-lookup"><span data-stu-id="cc118-139">Data Catalog administrators can also save searches for all users within hello organization.</span></span> <span data-ttu-id="cc118-140">Когда администраторы сохранение условий поиска, они предоставляются с **общего ресурса в пределах компании hello** параметр.</span><span class="sxs-lookup"><span data-stu-id="cc118-140">When administrators save a search, they're presented with a **Share within hello company** option.</span></span> <span data-ttu-id="cc118-141">Выбрав этот параметр hello общих папок, сохраненного поиска для всех пользователей в организации hello.</span><span class="sxs-lookup"><span data-stu-id="cc118-141">Selecting this option shares hello saved search for all users in hello organization.</span></span>

 ![Сохраненные поиски организации](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a><span data-ttu-id="cc118-143">Закрепленные ресурсы данных</span><span class="sxs-lookup"><span data-stu-id="cc118-143">Pinned data assets</span></span>
<span data-ttu-id="cc118-144">С помощью сохраненных поисков можно сохранять и использовать повторно определения поиска.</span><span class="sxs-lookup"><span data-stu-id="cc118-144">With saved searches, you can save and reuse search definitions.</span></span> <span data-ttu-id="cc118-145">Hello ресурсов данных, возвращаемых при поиске hello может измениться по мере того как содержимое hello hello изменения каталога.</span><span class="sxs-lookup"><span data-stu-id="cc118-145">hello data assets that are returned by hello searches might change over time as hello contents of hello catalog change.</span></span> <span data-ttu-id="cc118-146">При закреплении ресурсов данных toomake активы конкретных данных явным образом указывать их проще tooaccess без необходимости toouse поиска.</span><span class="sxs-lookup"><span data-stu-id="cc118-146">When you pin data assets, you can explicitly identify specific data assets toomake them easier tooaccess without needing toouse a search.</span></span>

<span data-ttu-id="cc118-147">Закрепление ресурса данных не представляет никаких трудностей.</span><span class="sxs-lookup"><span data-stu-id="cc118-147">Pinning a data asset is straightforward.</span></span> <span data-ttu-id="cc118-148">список закрепленных tooyour активов данных hello tooadd, нужно просто щелкнуть hello **ПИН-код** значок.</span><span class="sxs-lookup"><span data-stu-id="cc118-148">tooadd hello data asset tooyour pinned list, you simply click hello **pin** icon.</span></span> <span data-ttu-id="cc118-149">Hello значок отображается в углу hello hello активов плитки в представлении tile hello и в hello самый левый столбец в представлении списка hello hello портале каталога данных Azure.</span><span class="sxs-lookup"><span data-stu-id="cc118-149">hello icon is displayed in hello corner of hello asset tile in hello tile view, and in hello left-most column in hello list view in hello Azure Data Catalog portal.</span></span>

![значок булавки Hello ресурса данных](./media/data-catalog-how-to-save-pin/05-pinning.png)

<span data-ttu-id="cc118-151">Открепление ресурса данных выполняется так же просто.</span><span class="sxs-lookup"><span data-stu-id="cc118-151">Unpinning a data asset is equally straightforward.</span></span> <span data-ttu-id="cc118-152">Просто щелкните hello **открепить** приветствия tootoggle значок для выбранного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="cc118-152">Simply click hello **unpin** icon tootoggle hello setting for hello selected asset.</span></span>

![значок «открепить» ресурса данных Hello](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="hello-my-assets-section"></a><span data-ttu-id="cc118-154">Мои ресурсы раздел Hello</span><span class="sxs-lookup"><span data-stu-id="cc118-154">hello My Assets section</span></span>
<span data-ttu-id="cc118-155">Hello включает домашней страницы портала каталога данных **Мои активы** раздел, в котором перечислены ресурсы, представляющие интерес toohello текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="cc118-155">hello Data Catalog portal home page includes a **My Assets** section that displays assets of interest toohello current user.</span></span> <span data-ttu-id="cc118-156">Этот раздел включает как закрепленные ресурсы, так и сохраненные поисковые запросы.</span><span class="sxs-lookup"><span data-stu-id="cc118-156">This section includes both pinned assets and saved searches.</span></span>

![Hello разделе Мои активов на домашней странице приветствия](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a><span data-ttu-id="cc118-158">Сводка</span><span class="sxs-lookup"><span data-stu-id="cc118-158">Summary</span></span>
<span data-ttu-id="cc118-159">Каталог данных Azure предоставляет возможности, которые позволяют проще toodiscover hello источники данных, которые необходимо, чтобы вы и другие члены организации могут тратить меньше времени, поиск данных и работы с ней еще раз.</span><span class="sxs-lookup"><span data-stu-id="cc118-159">Azure Data Catalog provides capabilities that make it easier toodiscover hello data sources you need, so you and other organization members can spend less time looking for data and more time working with it.</span></span> <span data-ttu-id="cc118-160">На базе этих основных возможностей реализованы функции сохраненных поисков и закрепленных ресурсов данных, позволяющие пользователям легко находить источники данных, с которыми они работают регулярно.</span><span class="sxs-lookup"><span data-stu-id="cc118-160">Saved searches and pinned data assets build on these core capabilities so users can easily identify data sources that they work with repeatedly.</span></span>
