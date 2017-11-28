---
title: "Очистка конечной точки Azure CDN | Документация Майкрософт"
description: "Узнайте, как удалить все кэшированное содержимое из конечной точки Azure CDN."
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
ms.openlocfilehash: b035c232bb58d653960190d4974cc3789d55a51d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a><span data-ttu-id="abc9d-103">Очистка конечной точки сети CDN Azure</span><span class="sxs-lookup"><span data-stu-id="abc9d-103">Purge an Azure CDN endpoint</span></span>
## <a name="overview"></a><span data-ttu-id="abc9d-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="abc9d-104">Overview</span></span>
<span data-ttu-id="abc9d-105">Пограничные узлы Azure CDN кэшируют ресурсы до истечения срока жизни (TTL) ресурса.</span><span class="sxs-lookup"><span data-stu-id="abc9d-105">Azure CDN edge nodes will cache assets until the asset's time-to-live (TTL) expires.</span></span>  <span data-ttu-id="abc9d-106">Когда после истечения срока TTL ресурса клиент запрашивает ресурс с пограничного узла, этот узел извлекает новую обновленную копию ресурса для обработки клиентского запроса и сохраняет обновление в кэше.</span><span class="sxs-lookup"><span data-stu-id="abc9d-106">After the asset's TTL expires, when a client requests the asset from the edge node, the edge node will retrieve a new updated copy of the asset to serve the client request and store refresh the cache.</span></span>

<span data-ttu-id="abc9d-107">Лучший способ убедиться, что пользователи всегда получают последнюю версию ресурсов — изменять версию ресурсов при каждом обновлении и публиковать их в виде нового URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="abc9d-107">The best practice to make sure your users always obtain the latest copy of your assets is to version your assets for each update and publish them as new URLs.</span></span>  <span data-ttu-id="abc9d-108">CDN будет незамедлительно получать ресурсы для следующих клиентских запросов.</span><span class="sxs-lookup"><span data-stu-id="abc9d-108">CDN will immediately retrieve the new assets for the next client requests.</span></span>  <span data-ttu-id="abc9d-109">Иногда может потребоваться очистить кэшированное содержимое со всех пограничных узлов и сделать так, чтобы узлы получили новые обновленные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="abc9d-109">Sometimes you may wish to purge cached content from all edge nodes and force them all to retrieve new updated assets.</span></span>  <span data-ttu-id="abc9d-110">Это может быть вызвано обновлениями веб-приложения или быстрого обновления ресурсов, которые содержат неверные сведения.</span><span class="sxs-lookup"><span data-stu-id="abc9d-110">This might be due to updates to your web application, or to quickly update assets that contain incorrect information.</span></span>

> [!TIP]
> <span data-ttu-id="abc9d-111">Обратите внимание, что во время процесса очистки ресурсов с пограничных серверов CDN будет удалено только кэшированное содержимое.</span><span class="sxs-lookup"><span data-stu-id="abc9d-111">Note that purging only clears the cached content on the CDN edge servers.</span></span>  <span data-ttu-id="abc9d-112">В любых подчиненных кэшах, например кешах прокси-серверов и локального браузера, по-прежнему могут содержаться кэшированные копии файла.</span><span class="sxs-lookup"><span data-stu-id="abc9d-112">Any downstream caches, such as proxy servers and local browser caches, may still hold a cached copy of the file.</span></span>  <span data-ttu-id="abc9d-113">Это необходимо учитывать при указании срока жизни файла.</span><span class="sxs-lookup"><span data-stu-id="abc9d-113">It's important to remember this when you set a file's time-to-live.</span></span>  <span data-ttu-id="abc9d-114">Вы можете принудительно запросить с подчиненного клиента последнюю версию файла, задавая ему при каждом обновлении уникальное имя или воспользовавшись преимуществами функции [кэширования строк запроса](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="abc9d-114">You can force a downstream client to request the latest version of your file by giving it a unique name every time you update it, or by taking advantage of [query string caching](cdn-query-string.md).</span></span>  
> 
> 

<span data-ttu-id="abc9d-115">В этом учебнике приведен процесс очистки ресурсов со всех пограничных узлов конечной точки.</span><span class="sxs-lookup"><span data-stu-id="abc9d-115">This tutorial walks you through purging assets from all edge nodes of an endpoint.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="abc9d-116">Пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="abc9d-116">Walkthrough</span></span>
1. <span data-ttu-id="abc9d-117">На [портале Azure](https://portal.azure.com)перейдите к профилю сети CDN, содержащему конечную точку, которую необходимо очистить.</span><span class="sxs-lookup"><span data-stu-id="abc9d-117">In the [Azure Portal](https://portal.azure.com), browse to the CDN profile containing the endpoint you wish to purge.</span></span>
2. <span data-ttu-id="abc9d-118">В колонке профиля сети CDN нажмите кнопку "Очистить".</span><span class="sxs-lookup"><span data-stu-id="abc9d-118">From the CDN profile blade, click the purge button.</span></span>
   
    ![Колонка профиля сети CDN](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    <span data-ttu-id="abc9d-120">Откроется колонка "Очистка".</span><span class="sxs-lookup"><span data-stu-id="abc9d-120">The Purge blade opens.</span></span>
   
    ![Колонка очистки CDN](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. <span data-ttu-id="abc9d-122">В колонке "Очистка" выберите адрес службы для удаления из раскрывающегося списка URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="abc9d-122">On the Purge blade, select the service address you wish to purge from the URL dropdown.</span></span>
   
    ![Форма очистки](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > <span data-ttu-id="abc9d-124">Можно также перейти к колонке "Очистка", нажав кнопку **Очистить** в колонке конечной точки CDN.</span><span class="sxs-lookup"><span data-stu-id="abc9d-124">You can also get to the Purge blade by clicking the **Purge** button on the CDN endpoint blade.</span></span>  <span data-ttu-id="abc9d-125">В этом случае в поле **URL-адрес** будет вставлен адрес службы этой конкретной конечной точки.</span><span class="sxs-lookup"><span data-stu-id="abc9d-125">In that case, the **URL** field will be pre-populated with the service address of that specific endpoint.</span></span>
   > 
   > 
4. <span data-ttu-id="abc9d-126">Выберите, какие ресурсы нужно удалить из пограничных узлов.</span><span class="sxs-lookup"><span data-stu-id="abc9d-126">Select what assets you wish to purge from the edge nodes.</span></span>  <span data-ttu-id="abc9d-127">Чтобы очистить все ресурсы, установите флажок **Очистить все** .</span><span class="sxs-lookup"><span data-stu-id="abc9d-127">If you wish to clear all assets, click the **Purge all** checkbox.</span></span>  <span data-ttu-id="abc9d-128">В противном случае в поле **Путь** введите путь к каждому ресурсу, который нужно очистить.</span><span class="sxs-lookup"><span data-stu-id="abc9d-128">Otherwise, type the path of each asset you wish to purge in the **Path** textbox.</span></span> <span data-ttu-id="abc9d-129">В поле "Путь" поддерживаются следующие форматы.</span><span class="sxs-lookup"><span data-stu-id="abc9d-129">Below formats are supported in the path.</span></span>
    1. <span data-ttu-id="abc9d-130">**Очистка отдельного URL-адреса.** Очищает отдельный ресурс, указав полный URL-адрес с расширением файла или без него, например,`/pictures/strasbourg.png` или `/pictures/strasbourg`.</span><span class="sxs-lookup"><span data-stu-id="abc9d-130">**Single URL purge**: Purge individual asset by specifying the full URL, with or without the file extension, e.g.,`/pictures/strasbourg.png`; `/pictures/strasbourg`</span></span>
    2. <span data-ttu-id="abc9d-131">**Очистка по подстановочным знакам.** В качестве подстановочного знака можно использовать звездочку (\*).</span><span class="sxs-lookup"><span data-stu-id="abc9d-131">**Wildcard purge**: Asterisk (\*) may be used as a wildcard.</span></span> <span data-ttu-id="abc9d-132">Очищает все папки, вложенные папки и файлы конечной точки, в пути которой есть знак `/*`, или очищает все вложенные папки и файлы в определенной папке, указав в соответствующей папке `/*`, например `/pictures/*`.</span><span class="sxs-lookup"><span data-stu-id="abc9d-132">Purge all folders, sub-folders and files under an endpoint with `/*` in the path or purge all sub-folders and files under a specific folder by specifying the folder followed by `/*`, e.g.,`/pictures/*`.</span></span>  <span data-ttu-id="abc9d-133">Обратите внимание, что в настоящее время в Azure CDN от Akamai не поддерживается очистка по подстановочным знакам.</span><span class="sxs-lookup"><span data-stu-id="abc9d-133">Note that wildcard purge is not supported by Azure CDN from Akamai currently.</span></span> 
    3. <span data-ttu-id="abc9d-134">**Очистка корневого домена.** Очищает содержимое в корне конечной точки, в пути которой есть знак "/".</span><span class="sxs-lookup"><span data-stu-id="abc9d-134">**Root domain purge**: Purge the root of the endpoint with "/" in the path.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="abc9d-135">Пути должны быть указаны для очистки и быть относительными URL-адресами, которые соответствуют следующему [регулярному выражению](https://msdn.microsoft.com/library/az24scfc.aspx).</span><span class="sxs-lookup"><span data-stu-id="abc9d-135">Paths must be specified for purge and must be a relative URL that fit the following [regular expression](https://msdn.microsoft.com/library/az24scfc.aspx).</span></span> <span data-ttu-id="abc9d-136">**Очистить все** и **Очистка по подстановочным знакам** в настоящее время не поддерживается в **Azure CDN от Akamai**.</span><span class="sxs-lookup"><span data-stu-id="abc9d-136">**Purge all** and **Wildcard purge** not supported by **Azure CDN from Akamai** currently.</span></span>
   > > <span data-ttu-id="abc9d-137">Очистка отдельного URL-адреса: `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span><span class="sxs-lookup"><span data-stu-id="abc9d-137">Single URL purge `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`</span></span>  
   > > <span data-ttu-id="abc9d-138">Строка запроса: `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span><span class="sxs-lookup"><span data-stu-id="abc9d-138">Query string `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`</span></span>  
   > > <span data-ttu-id="abc9d-139">Очистка по подстановочным знакам: `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span><span class="sxs-lookup"><span data-stu-id="abc9d-139">Wildcard purge `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`.</span></span> 
   > 
   > <span data-ttu-id="abc9d-140">После ввода текста появятся дополнительные поля **Путь** для формирования списка из нескольких ресурсов.</span><span class="sxs-lookup"><span data-stu-id="abc9d-140">More **Path** textboxes will appear after you enter text to allow you to build a list of multiple assets.</span></span>  <span data-ttu-id="abc9d-141">Ресурсы можно удалить из списка, нажав кнопку с многоточием (...).</span><span class="sxs-lookup"><span data-stu-id="abc9d-141">You can delete assets from the list by clicking the ellipsis (...) button.</span></span>
   > 
5. <span data-ttu-id="abc9d-142">Нажмите кнопку **Очистить** .</span><span class="sxs-lookup"><span data-stu-id="abc9d-142">Click the **Purge** button.</span></span>
   
    ![Кнопка очистки](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> <span data-ttu-id="abc9d-144">Запросы на очистку для **Azure CDN от Verizon** обрабатываются приблизительно 2–3 минуты (уровня "Стандартный" и "Премиум") и приблизительно 7 минут для **Azure CDN от Akamai**.</span><span class="sxs-lookup"><span data-stu-id="abc9d-144">Purge requests take approximately 2-3 minutes to process with **Azure CDN from Verizon** (Standard and Premium), and approximately 7 minutes with **Azure CDN from Akamai**.</span></span>  <span data-ttu-id="abc9d-145">Azure CDN может выполнять до 50 одновременных запросов на очистку в любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="abc9d-145">Azure CDN has a limit of 50 concurrent purge requests at any given time.</span></span> 
> 
> 

## <a name="see-also"></a><span data-ttu-id="abc9d-146">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="abc9d-146">See also</span></span>
* [<span data-ttu-id="abc9d-147">Предварительная загрузка ресурсов на конечной точке CDN Azure</span><span class="sxs-lookup"><span data-stu-id="abc9d-147">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="abc9d-148">Справочник по API REST CDN. Очистка и предварительная загрузка конечной точки</span><span class="sxs-lookup"><span data-stu-id="abc9d-148">Azure CDN REST API reference - Purge or Pre-Load an Endpoint</span></span>](https://msdn.microsoft.com/library/mt634451.aspx)

