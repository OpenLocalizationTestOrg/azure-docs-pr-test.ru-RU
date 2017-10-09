---
title: "aaaPurge конечной точки Azure CDN | Документы Microsoft"
description: "Узнайте, как кэшируются toopurge все содержимое из конечной точки Azure CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 0b50230b-fe82-4740-90aa-95d4dde8bd4f
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a09f4a49aa1e2d7655ecae44b5126c11c28fd599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a><span data-ttu-id="39461-103">Очистка конечной точки сети CDN Azure</span><span class="sxs-lookup"><span data-stu-id="39461-103">Purge an Azure CDN endpoint</span></span>
## <a name="overview"></a><span data-ttu-id="39461-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="39461-104">Overview</span></span>
<span data-ttu-id="39461-105">Край узлов Azure CDN кэширует активы до истечения срока действия hello активов срока жизни (TTL).</span><span class="sxs-lookup"><span data-stu-id="39461-105">Azure CDN edge nodes will cache assets until hello asset's time-to-live (TTL) expires.</span></span>  <span data-ttu-id="39461-106">После истечения срока ЖИЗНИ hello активов, когда клиент запрашивает активов hello из граничного узла hello, hello граничного узла извлечет новых обновленную копию hello активов tooserve hello клиентского запроса и хранения hello обновления кэша.</span><span class="sxs-lookup"><span data-stu-id="39461-106">After hello asset's TTL expires, when a client requests hello asset from hello edge node, hello edge node will retrieve a new updated copy of hello asset tooserve hello client request and store refresh hello cache.</span></span>

<span data-ttu-id="39461-107">Hello лучший подход toomake убедиться, что пользователи всегда получать последнюю копию hello активов — tooversion активы для каждого обновления и публиковать их в виде новые URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="39461-107">hello best practice toomake sure your users always obtain hello latest copy of your assets is tooversion your assets for each update and publish them as new URLs.</span></span>  <span data-ttu-id="39461-108">CDN будет получать немедленно hello новым средствам hello Далее клиентских запросов.</span><span class="sxs-lookup"><span data-stu-id="39461-108">CDN will immediately retrieve hello new assets for hello next client requests.</span></span>  <span data-ttu-id="39461-109">Иногда можно назвать toopurge кэшированного содержимого со всех узлов edge и применения к ним активы новых обновленную все tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="39461-109">Sometimes you may wish toopurge cached content from all edge nodes and force them all tooretrieve new updated assets.</span></span>  <span data-ttu-id="39461-110">Это может произойти из-за tooupdates tooyour веб-приложение или tooquickly обновления активы, которые содержат неверные сведения.</span><span class="sxs-lookup"><span data-stu-id="39461-110">This might be due tooupdates tooyour web application, or tooquickly update assets that contain incorrect information.</span></span>

> [!TIP]
> <span data-ttu-id="39461-111">Обратите внимание, что только очистки очищает hello кэшированного содержимого на пограничных серверов CDN hello.</span><span class="sxs-lookup"><span data-stu-id="39461-111">Note that purging only clears hello cached content on hello CDN edge servers.</span></span>  <span data-ttu-id="39461-112">Все кэши подчиненных, например прокси-серверы и кэши локальный браузер по-прежнему может содержаться кэшированную копию файла hello.</span><span class="sxs-lookup"><span data-stu-id="39461-112">Any downstream caches, such as proxy servers and local browser caches, may still hold a cached copy of hello file.</span></span>  <span data-ttu-id="39461-113">Это важные tooremember это при задании файла срока жизни.</span><span class="sxs-lookup"><span data-stu-id="39461-113">It's important tooremember this when you set a file's time-to-live.</span></span>  <span data-ttu-id="39461-114">Можно принудительно подчиненных клиентов toorequest hello последнюю версию файла, указав его уникальное имя, каждый раз при обновлении или используя преимущества [запроса кэширование строки](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="39461-114">You can force a downstream client toorequest hello latest version of your file by giving it a unique name every time you update it, or by taking advantage of [query string caching](cdn-query-string.md).</span></span>  
> 
> 

<span data-ttu-id="39461-115">В этом учебнике приведен процесс очистки ресурсов со всех пограничных узлов конечной точки.</span><span class="sxs-lookup"><span data-stu-id="39461-115">This tutorial walks you through purging assets from all edge nodes of an endpoint.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="39461-116">Пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="39461-116">Walkthrough</span></span>
1. <span data-ttu-id="39461-117">В hello [портала Azure](https://portal.azure.com), Обзор профиля CDN toohello, содержащий конечную точку hello нужно toopurge.</span><span class="sxs-lookup"><span data-stu-id="39461-117">In hello [Azure Portal](https://portal.azure.com), browse toohello CDN profile containing hello endpoint you wish toopurge.</span></span>
2. <span data-ttu-id="39461-118">В колонке профиля CDN hello нажмите кнопку очистки hello.</span><span class="sxs-lookup"><span data-stu-id="39461-118">From hello CDN profile blade, click hello purge button.</span></span>
   
    ![Колонка профиля сети CDN](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    <span data-ttu-id="39461-120">Открывает колонку очистки Hello.</span><span class="sxs-lookup"><span data-stu-id="39461-120">hello Purge blade opens.</span></span>
   
    ![Колонка очистки CDN](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. <span data-ttu-id="39461-122">На hello очистки колонки, установите адрес службы hello нужно toopurge из раскрывающегося списка hello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="39461-122">On hello Purge blade, select hello service address you wish toopurge from hello URL dropdown.</span></span>
   
    ![Форма очистки](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > <span data-ttu-id="39461-124">Toohello Очистка колонки можно также получить, щелкнув hello **очистки** кнопки в колонке конечной точки CDN hello.</span><span class="sxs-lookup"><span data-stu-id="39461-124">You can also get toohello Purge blade by clicking hello **Purge** button on hello CDN endpoint blade.</span></span>  <span data-ttu-id="39461-125">В этом случае hello **URL-адрес** поле будет вставлено hello адрес службы этой определенной конечной точки.</span><span class="sxs-lookup"><span data-stu-id="39461-125">In that case, hello **URL** field will be pre-populated with hello service address of that specific endpoint.</span></span>
   > 
   > 
4. <span data-ttu-id="39461-126">Выбор ресурсов toopurge из hello краевым узлам.</span><span class="sxs-lookup"><span data-stu-id="39461-126">Select what assets you wish toopurge from hello edge nodes.</span></span>  <span data-ttu-id="39461-127">Tooclear все ресурсы, нажмите кнопку hello **все** флажок.</span><span class="sxs-lookup"><span data-stu-id="39461-127">If you wish tooclear all assets, click hello **Purge all** checkbox.</span></span>  <span data-ttu-id="39461-128">В противном случае текст hello контуру каждого средства нужно toopurge в hello **путь** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="39461-128">Otherwise, type hello path of each asset you wish toopurge in hello **Path** textbox.</span></span> <span data-ttu-id="39461-129">Ниже форматов поддерживаются в пути hello.</span><span class="sxs-lookup"><span data-stu-id="39461-129">Below formats are supported in hello path.</span></span>
    1. <span data-ttu-id="39461-130">**Очистка один URL-адрес**: очистка отдельных средств, указав hello полный URL-адрес с или без расширения файла hello, например,`/pictures/strasbourg.png`;`/pictures/strasbourg`</span><span class="sxs-lookup"><span data-stu-id="39461-130">**Single URL purge**: Purge individual asset by specifying hello full URL, with or without hello file extension, e.g.,`/pictures/strasbourg.png`; `/pictures/strasbourg`</span></span>
    2. <span data-ttu-id="39461-131">**Очистка по подстановочным знакам.** В качестве подстановочного знака можно использовать звездочку (\*).</span><span class="sxs-lookup"><span data-stu-id="39461-131">**Wildcard purge**: Asterisk (\*) may be used as a wildcard.</span></span> <span data-ttu-id="39461-132">Очистка всех папок, вложенных папок и файлов в конечную точку с `/*` в hello путь или очистить все вложенные папки и файлы в определенной папке, указав папку hello, за которым следует `/*`, например,`/pictures/*`.</span><span class="sxs-lookup"><span data-stu-id="39461-132">Purge all folders, sub-folders and files under an endpoint with `/*` in hello path or purge all sub-folders and files under a specific folder by specifying hello folder followed by `/*`, e.g.,`/pictures/*`.</span></span>  <span data-ttu-id="39461-133">Обратите внимание, что в настоящее время в Azure CDN от Akamai не поддерживается очистка по подстановочным знакам.</span><span class="sxs-lookup"><span data-stu-id="39461-133">Note that wildcard purge is not supported by Azure CDN from Akamai currently.</span></span> 
    3. <span data-ttu-id="39461-134">**Очистка домена корневого**: корневой hello очистки hello конечной точки с «/» в пути hello.</span><span class="sxs-lookup"><span data-stu-id="39461-134">**Root domain purge**: Purge hello root of hello endpoint with "/" in hello path.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="39461-135">Путь должен быть указан для очистки и должен быть относительным URL-адресом, который умещается hello следующие [регулярное выражение](https://msdn.microsoft.com/library/az24scfc.aspx).</span><span class="sxs-lookup"><span data-stu-id="39461-135">Paths must be specified for purge and must be a relative URL that fit hello following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx).</span></span> <span data-ttu-id="39461-136">**Очистить все** и **Очистка по подстановочным знакам** в настоящее время не поддерживается в **Azure CDN от Akamai**.</span><span class="sxs-lookup"><span data-stu-id="39461-136">**Purge all** and **Wildcard purge** not supported by **Azure CDN from Akamai** currently.</span></span>
   > > <span data-ttu-id="39461-137">Очистка отдельного URL-адреса: `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span><span class="sxs-lookup"><span data-stu-id="39461-137">Single URL purge `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span></span>  
   > > <span data-ttu-id="39461-138">Строка запроса: `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="39461-138">Query string `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span></span>  
   > > <span data-ttu-id="39461-139">Очистка по подстановочным знакам: `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span><span class="sxs-lookup"><span data-stu-id="39461-139">Wildcard purge `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span></span> 
   > 
   > <span data-ttu-id="39461-140">Дополнительные **путь** текстовые поля будут отображаться после ввода текста tooallow toobuild в списке несколько ресурсов.</span><span class="sxs-lookup"><span data-stu-id="39461-140">More **Path** textboxes will appear after you enter text tooallow you toobuild a list of multiple assets.</span></span>  <span data-ttu-id="39461-141">Ресурсы можно удалить из списка hello, нажав кнопку с многоточием (...) hello.</span><span class="sxs-lookup"><span data-stu-id="39461-141">You can delete assets from hello list by clicking hello ellipsis (...) button.</span></span>
   > 
5. <span data-ttu-id="39461-142">Нажмите кнопку hello **очистки** кнопки.</span><span class="sxs-lookup"><span data-stu-id="39461-142">Click hello **Purge** button.</span></span>
   
    ![Кнопка очистки](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> <span data-ttu-id="39461-144">Очистка запросы выполняться приблизительно 2-3 минуты tooprocess с **CDN Azure из Verizon** (Standard и Premium) и примерно 7 минут с **Azure CDN с Akamai**.</span><span class="sxs-lookup"><span data-stu-id="39461-144">Purge requests take approximately 2-3 minutes tooprocess with **Azure CDN from Verizon** (Standard and Premium), and approximately 7 minutes with **Azure CDN from Akamai**.</span></span>  <span data-ttu-id="39461-145">Azure CDN может выполнять до 50 одновременных запросов на очистку в любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="39461-145">Azure CDN has a limit of 50 concurrent purge requests at any given time.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="39461-146">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="39461-146">See also</span></span>
* [<span data-ttu-id="39461-147">Предварительная загрузка ресурсов на конечной точке CDN Azure</span><span class="sxs-lookup"><span data-stu-id="39461-147">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="39461-148">Справочник по API REST CDN. Очистка и предварительная загрузка конечной точки</span><span class="sxs-lookup"><span data-stu-id="39461-148">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

