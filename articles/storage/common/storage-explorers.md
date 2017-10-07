---
title: "aaaTools для работы со службой хранилища Azure | Документы Microsoft"
description: "Список средств, позволяющих tooview и работать с данными хранилища Azure."
services: storage
documentationcenter: 
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: e4748642-98c4-437e-b0ed-4f9641c2e894
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: dineshmurthy
ms.openlocfilehash: 3308de2153099a05a676ab1d76426bd932e8a96c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-client-tools"></a><span data-ttu-id="ce7ea-103">Клиентские инструменты службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="ce7ea-103">Azure Storage Client Tools</span></span>
<span data-ttu-id="ce7ea-104">Пользователи хранилища Azure в большинстве случаев используется toobe может tooview и взаимодействовать с свои данные с помощью средства клиента хранилищ Azure.</span><span class="sxs-lookup"><span data-stu-id="ce7ea-104">Users of Azure Storage frequently want toobe able tooview/interact with their data using an Azure Storage client tool.</span></span> <span data-ttu-id="ce7ea-105">В следующих таблицах hello перечислены ряд средств, позволяющих toodo это.</span><span class="sxs-lookup"><span data-stu-id="ce7ea-105">In hello tables below, we list a number of tools that allow you toodo this.</span></span> <span data-ttu-id="ce7ea-106">Мы поместили «X» в каждом блоке, если оно предоставляет возможность hello tooeither перечислить или доступ к абстракции данных hello.</span><span class="sxs-lookup"><span data-stu-id="ce7ea-106">We put an "X" in each block if it provides hello ability tooeither enumerate and/or access hello data abstraction.</span></span> <span data-ttu-id="ce7ea-107">Hello таблице также указано, если средства hello предоставляется бесплатно или нет.</span><span class="sxs-lookup"><span data-stu-id="ce7ea-107">hello table also shows if hello tools is free or not.</span></span> <span data-ttu-id="ce7ea-108">«Пробной версии» указывает, что бесплатной пробной версии, но не освобождается hello полной версии продукта.</span><span class="sxs-lookup"><span data-stu-id="ce7ea-108">"Trial" indicates that there is a free trial, but hello full product is not free.</span></span> <span data-ttu-id="ce7ea-109">"Да/нет" указывает, что есть как платная, так и бесплатная версии.</span><span class="sxs-lookup"><span data-stu-id="ce7ea-109">"Y/N" indicates that a version is available for free, while a different version is available for purchase.</span></span>

<span data-ttu-id="ce7ea-110">Здесь представлено только моментальный снимок hello доступные средства клиента хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="ce7ea-110">We've only provided a snapshot of hello available Azure Storage client tools.</span></span> <span data-ttu-id="ce7ea-111">Эти средства могут продолжить tooevolve и увеличиваются в размере функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="ce7ea-111">These tools may continue tooevolve and grow in functionality.</span></span> <span data-ttu-id="ce7ea-112">Если исправления или обновления, оставьте toolet комментариев, которые нам знать.</span><span class="sxs-lookup"><span data-stu-id="ce7ea-112">If there are corrections or updates, please leave a comment toolet us know.</span></span> <span data-ttu-id="ce7ea-113">Hello аналогичным образом, если вы знаете, средства, которые с головой toobe здесь — мы бы довольны tooadd их.</span><span class="sxs-lookup"><span data-stu-id="ce7ea-113">hello same is true if you know of tools that ought toobe here - we'd be happy tooadd them.</span></span>

<span data-ttu-id="ce7ea-114">**Клиентские инструменты службы хранилища Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="ce7ea-114">**Microsoft Azure Storage Client Tools**</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="ce7ea-115">Клиентский инструмент службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="ce7ea-115">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="ce7ea-116">Блочный BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="ce7ea-116">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="ce7ea-117">Страничный BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="ce7ea-117">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="ce7ea-118">Добавление больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="ce7ea-118">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="ce7ea-119">Таблицы</span><span class="sxs-lookup"><span data-stu-id="ce7ea-119">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="ce7ea-120">Очереди</span><span class="sxs-lookup"><span data-stu-id="ce7ea-120">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="ce7ea-121">Файлы</span><span class="sxs-lookup"><span data-stu-id="ce7ea-121">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="ce7ea-122">Бесплатно</span><span class="sxs-lookup"><span data-stu-id="ce7ea-122">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="ce7ea-123">Платформа</span><span class="sxs-lookup"><span data-stu-id="ce7ea-123">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="ce7ea-124">Web</span><span class="sxs-lookup"><span data-stu-id="ce7ea-124">Web</span></span></td>
    <td><span data-ttu-id="ce7ea-125">Windows</span><span class="sxs-lookup"><span data-stu-id="ce7ea-125">Windows</span></span></td>
    <td><span data-ttu-id="ce7ea-126">OSX</span><span class="sxs-lookup"><span data-stu-id="ce7ea-126">OSX</span></span></td>
    <td><span data-ttu-id="ce7ea-127">Linux</span><span class="sxs-lookup"><span data-stu-id="ce7ea-127">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ce7ea-128"><a href="https://azure.microsoft.com/features/azure-portal/">Портал Microsoft Azure</a></span><span class="sxs-lookup"><span data-stu-id="ce7ea-128"><a href="https://azure.microsoft.com/features/azure-portal/">Microsoft Azure Portal</a></span></span></td>
    <td><span data-ttu-id="ce7ea-129">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-129">X</span></span></td>
    <td><span data-ttu-id="ce7ea-130">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-130">X</span></span></td>
    <td><span data-ttu-id="ce7ea-131">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-131">X</span></span></td>
    <td><span data-ttu-id="ce7ea-132">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-132">X</span></span></td>
    <td><span data-ttu-id="ce7ea-133">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-133">X</span></span></td>
    <td><span data-ttu-id="ce7ea-134">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-134">X</span></span></td>
    <td><span data-ttu-id="ce7ea-135">Да</span><span class="sxs-lookup"><span data-stu-id="ce7ea-135">Y</span></span></td>
    <td><span data-ttu-id="ce7ea-136">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-136">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ce7ea-137"><a href="http://storageexplorer.com/">Обозреватель службы хранилища Microsoft Azure</a></span><span class="sxs-lookup"><span data-stu-id="ce7ea-137"><a href="http://storageexplorer.com/">Microsoft Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="ce7ea-138">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-138">X</span></span></td>
    <td><span data-ttu-id="ce7ea-139">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-139">X</span></span></td>
    <td><span data-ttu-id="ce7ea-140">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-140">X</span></span></td>
    <td><span data-ttu-id="ce7ea-141">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-141">X</span></span></td>
    <td><span data-ttu-id="ce7ea-142">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-142">X</span></span></td>
    <td><span data-ttu-id="ce7ea-143">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-143">X</span></span></td>
    <td><span data-ttu-id="ce7ea-144">Да</span><span class="sxs-lookup"><span data-stu-id="ce7ea-144">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="ce7ea-145">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-145">X</span></span></td>
    <td><span data-ttu-id="ce7ea-146">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-146">X</span></span></td>
    <td><span data-ttu-id="ce7ea-147">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-147">X</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ce7ea-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Обозреватель сервера Microsoft Visual Studio</a></span><span class="sxs-lookup"><span data-stu-id="ce7ea-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Microsoft Visual Studio Server Explorer</a></span></span></td>
    <td><span data-ttu-id="ce7ea-149">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-149">X</span></span></td>
    <td><span data-ttu-id="ce7ea-150">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-150">X</span></span></td>
    <td><span data-ttu-id="ce7ea-151">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-151">X</span></span></td>
    <td><span data-ttu-id="ce7ea-152">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-152">X</span></span></td>
    <td><span data-ttu-id="ce7ea-153">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-153">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="ce7ea-154">Да</span><span class="sxs-lookup"><span data-stu-id="ce7ea-154">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="ce7ea-155">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-155">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
</table>

<span data-ttu-id="ce7ea-156">**Сторонние клиентские инструменты службы хранилища Azure**</span><span class="sxs-lookup"><span data-stu-id="ce7ea-156">**Third-Party Azure Storage Client Tools**</span></span>

<span data-ttu-id="ce7ea-157">Не мы проверили, что функции hello или качество заявленным hello, выполнив сторонних средств, а также их список не означает поддержку корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="ce7ea-157">We have not verified hello functionality or quality claimed by hello following third-party tools and their listing does not imply an endorsement by Microsoft.</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="ce7ea-158">Клиентский инструмент службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="ce7ea-158">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="ce7ea-159">Блочный BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="ce7ea-159">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="ce7ea-160">Страничный BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="ce7ea-160">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="ce7ea-161">Добавление больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="ce7ea-161">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="ce7ea-162">Таблицы</span><span class="sxs-lookup"><span data-stu-id="ce7ea-162">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="ce7ea-163">Очереди</span><span class="sxs-lookup"><span data-stu-id="ce7ea-163">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="ce7ea-164">Файлы</span><span class="sxs-lookup"><span data-stu-id="ce7ea-164">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="ce7ea-165">Бесплатно</span><span class="sxs-lookup"><span data-stu-id="ce7ea-165">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="ce7ea-166">Платформа</span><span class="sxs-lookup"><span data-stu-id="ce7ea-166">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="ce7ea-167">Web</span><span class="sxs-lookup"><span data-stu-id="ce7ea-167">Web</span></span></td>
    <td><span data-ttu-id="ce7ea-168">Windows</span><span class="sxs-lookup"><span data-stu-id="ce7ea-168">Windows</span></span></td>
    <td><span data-ttu-id="ce7ea-169">OSX</span><span class="sxs-lookup"><span data-stu-id="ce7ea-169">OSX</span></span></td>
    <td><span data-ttu-id="ce7ea-170">Linux</span><span class="sxs-lookup"><span data-stu-id="ce7ea-170">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ce7ea-171"><a href="http://www.cloudportam.com/">Cloud Portam</a></span><span class="sxs-lookup"><span data-stu-id="ce7ea-171"><a href="http://www.cloudportam.com/">Cloud Portam</a></span></span></td>
    <td><span data-ttu-id="ce7ea-172">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-172">X</span></span></td>
    <td><span data-ttu-id="ce7ea-173">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-173">X</span></span></td>
    <td><span data-ttu-id="ce7ea-174">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-174">X</span></span></td>
    <td><span data-ttu-id="ce7ea-175">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-175">X</span></span></td>
    <td><span data-ttu-id="ce7ea-176">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-176">X</span></span></td>
    <td><span data-ttu-id="ce7ea-177">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-177">X</span></span></td>
    <td><span data-ttu-id="ce7ea-178">Пробная версия</span><span class="sxs-lookup"><span data-stu-id="ce7ea-178">Trial</span></span></td>
    <td><span data-ttu-id="ce7ea-179">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-179">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ce7ea-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span><span class="sxs-lookup"><span data-stu-id="ce7ea-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span></span></td>
    <td><span data-ttu-id="ce7ea-181">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-181">X</span></span></td>
    <td><span data-ttu-id="ce7ea-182">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-182">X</span></span></td>
    <td><span data-ttu-id="ce7ea-183">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-183">X</span></span></td>
    <td><span data-ttu-id="ce7ea-184">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-184">X</span></span></td>
    <td><span data-ttu-id="ce7ea-185">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-185">X</span></span></td>
    <td><span data-ttu-id="ce7ea-186">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-186">X</span></span></td>
    <td><span data-ttu-id="ce7ea-187">Пробная версия</span><span class="sxs-lookup"><span data-stu-id="ce7ea-187">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="ce7ea-188">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-188">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ce7ea-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Azure Explorer</a></span><span class="sxs-lookup"><span data-stu-id="ce7ea-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Azure Explorer</a></span></span></td>
    <td><span data-ttu-id="ce7ea-190">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-190">X</span></span></td>
    <td><span data-ttu-id="ce7ea-191">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-191">X</span></span></td>
    <td><span data-ttu-id="ce7ea-192">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-192">X</span></span></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="ce7ea-193">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-193">X</span></span></td>
    <td><span data-ttu-id="ce7ea-194">Да</span><span class="sxs-lookup"><span data-stu-id="ce7ea-194">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="ce7ea-195">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-195">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ce7ea-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure Storage Explorer;</a></span><span class="sxs-lookup"><span data-stu-id="ce7ea-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="ce7ea-197">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-197">X</span></span></td>
    <td><span data-ttu-id="ce7ea-198">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-198">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="ce7ea-199">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-199">X</span></span></td>
    <td><span data-ttu-id="ce7ea-200">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-200">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="ce7ea-201">Да</span><span class="sxs-lookup"><span data-stu-id="ce7ea-201">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="ce7ea-202">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-202">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ce7ea-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></span><span class="sxs-lookup"><span data-stu-id="ce7ea-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></span></span></td>
    <td><span data-ttu-id="ce7ea-204">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-204">X</span></span></td>
    <td><span data-ttu-id="ce7ea-205">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-205">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="ce7ea-206">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-206">X</span></span></td>
    <td><span data-ttu-id="ce7ea-207">Да/нет</span><span class="sxs-lookup"><span data-stu-id="ce7ea-207">Y/N</span></span></td>
    <td></td>
    <td><span data-ttu-id="ce7ea-208">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-208">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ce7ea-209"><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></span><span class="sxs-lookup"><span data-stu-id="ce7ea-209"><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></span></span></td>
    <td><span data-ttu-id="ce7ea-210">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-210">X</span></span></td>
    <td><span data-ttu-id="ce7ea-211">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-211">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="ce7ea-212">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-212">X</span></span></td>
    <td><span data-ttu-id="ce7ea-213">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-213">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="ce7ea-214">Пробная версия</span><span class="sxs-lookup"><span data-stu-id="ce7ea-214">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="ce7ea-215">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-215">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ce7ea-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span><span class="sxs-lookup"><span data-stu-id="ce7ea-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span></span></td>
    <td><span data-ttu-id="ce7ea-217">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-217">X</span></span></td>
    <td><span data-ttu-id="ce7ea-218">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-218">X</span></span></td>
    <td><span data-ttu-id="ce7ea-219">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-219">X</span></span></td>
    <td><span data-ttu-id="ce7ea-220">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-220">X</span></span></td>
    <td><span data-ttu-id="ce7ea-221">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-221">X</span></span></td>
    <td><span data-ttu-id="ce7ea-222">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-222">X</span></span></td>
    <td><span data-ttu-id="ce7ea-223">Да</span><span class="sxs-lookup"><span data-stu-id="ce7ea-223">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="ce7ea-224">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-224">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ce7ea-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></span><span class="sxs-lookup"><span data-stu-id="ce7ea-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></span></span></td>
    <td><span data-ttu-id="ce7ea-226">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-226">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="ce7ea-227">Пробная версия</span><span class="sxs-lookup"><span data-stu-id="ce7ea-227">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="ce7ea-228">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-228">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ce7ea-229"><a href="http://storageexplorer.codeplex.com/">Azure Web Storage Explorer</a></span><span class="sxs-lookup"><span data-stu-id="ce7ea-229"><a href="http://storageexplorer.codeplex.com/">Azure Web Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="ce7ea-230">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-230">X</span></span></td>
    <td><span data-ttu-id="ce7ea-231">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-231">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="ce7ea-232">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-232">X</span></span></td>
    <td><span data-ttu-id="ce7ea-233">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-233">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="ce7ea-234">Да</span><span class="sxs-lookup"><span data-stu-id="ce7ea-234">Y</span></span></td>
    <td><span data-ttu-id="ce7ea-235">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-235">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="ce7ea-236"><a href="https://zudio.co/">Zudio</a></span><span class="sxs-lookup"><span data-stu-id="ce7ea-236"><a href="https://zudio.co/">Zudio</a></span></span></td>
    <td><span data-ttu-id="ce7ea-237">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-237">X</span></span></td>
    <td><span data-ttu-id="ce7ea-238">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-238">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="ce7ea-239">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-239">X</span></span></td>
    <td><span data-ttu-id="ce7ea-240">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-240">X</span></span></td>
    <td><span data-ttu-id="ce7ea-241">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-241">X</span></span></td>
    <td><span data-ttu-id="ce7ea-242">Пробная версия</span><span class="sxs-lookup"><span data-stu-id="ce7ea-242">Trial</span></span></td>
    <td><span data-ttu-id="ce7ea-243">X</span><span class="sxs-lookup"><span data-stu-id="ce7ea-243">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>
