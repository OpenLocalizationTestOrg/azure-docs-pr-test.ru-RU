---
title: "Инструменты для работы со службой хранилища Azure | Документация Майкрософт"
description: "Список инструментов, позволяющих просматривать данные в службе хранилища Azure и взаимодействовать с ними."
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
ms.openlocfilehash: 620efda06d8225b21b6bb9b104b79061ebb6515c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-client-tools"></a><span data-ttu-id="88b98-103">Клиентские инструменты службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="88b98-103">Azure Storage Client Tools</span></span>
<span data-ttu-id="88b98-104">Пользователям службы хранилища Azure часто требуется просматривать свои данные или взаимодействовать с ними с помощью клиентского инструмента службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="88b98-104">Users of Azure Storage frequently want to be able to view/interact with their data using an Azure Storage client tool.</span></span> <span data-ttu-id="88b98-105">В приведенных ниже таблицах перечислен ряд инструментов, которые позволяют это сделать.</span><span class="sxs-lookup"><span data-stu-id="88b98-105">In the tables below, we list a number of tools that allow you to do this.</span></span> <span data-ttu-id="88b98-106">Соответствующее поле содержит "X", если инструмент позволяет перечислить абстракцию данных и (или) предоставить к ней доступ.</span><span class="sxs-lookup"><span data-stu-id="88b98-106">We put an "X" in each block if it provides the ability to either enumerate and/or access the data abstraction.</span></span> <span data-ttu-id="88b98-107">В таблице также показано, являются ли инструменты бесплатными.</span><span class="sxs-lookup"><span data-stu-id="88b98-107">The table also shows if the tools is free or not.</span></span> <span data-ttu-id="88b98-108">"Пробная версия" означает, что доступна бесплатная пробная версия, но полная версия продукта платная.</span><span class="sxs-lookup"><span data-stu-id="88b98-108">"Trial" indicates that there is a free trial, but the full product is not free.</span></span> <span data-ttu-id="88b98-109">"Да/нет" указывает, что есть как платная, так и бесплатная версии.</span><span class="sxs-lookup"><span data-stu-id="88b98-109">"Y/N" indicates that a version is available for free, while a different version is available for purchase.</span></span>

<span data-ttu-id="88b98-110">Мы предоставляем только набор клиентских инструментов службы хранилища Azure, доступных на данный момент.</span><span class="sxs-lookup"><span data-stu-id="88b98-110">We've only provided a snapshot of the available Azure Storage client tools.</span></span> <span data-ttu-id="88b98-111">Развитие этих инструментов и расширение их функций может продолжаться.</span><span class="sxs-lookup"><span data-stu-id="88b98-111">These tools may continue to evolve and grow in functionality.</span></span> <span data-ttu-id="88b98-112">Если необходимо внести какие-либо исправления или были выпущены обновления, оставьте комментарий для нас.</span><span class="sxs-lookup"><span data-stu-id="88b98-112">If there are corrections or updates, please leave a comment to let us know.</span></span> <span data-ttu-id="88b98-113">Кроме того, если вы знаете об инструментах, которые должны быть в этой статье, мы с радостью добавим их.</span><span class="sxs-lookup"><span data-stu-id="88b98-113">The same is true if you know of tools that ought to be here - we'd be happy to add them.</span></span>

<span data-ttu-id="88b98-114">**Клиентские инструменты службы хранилища Microsoft Azure**</span><span class="sxs-lookup"><span data-stu-id="88b98-114">**Microsoft Azure Storage Client Tools**</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="88b98-115">Клиентский инструмент службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="88b98-115">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="88b98-116">Блочный BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="88b98-116">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="88b98-117">Страничный BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="88b98-117">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="88b98-118">Добавление больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="88b98-118">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="88b98-119">Таблицы</span><span class="sxs-lookup"><span data-stu-id="88b98-119">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="88b98-120">Очереди</span><span class="sxs-lookup"><span data-stu-id="88b98-120">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="88b98-121">Файлы</span><span class="sxs-lookup"><span data-stu-id="88b98-121">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="88b98-122">Бесплатно</span><span class="sxs-lookup"><span data-stu-id="88b98-122">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="88b98-123">Платформа</span><span class="sxs-lookup"><span data-stu-id="88b98-123">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="88b98-124">Web</span><span class="sxs-lookup"><span data-stu-id="88b98-124">Web</span></span></td>
    <td><span data-ttu-id="88b98-125">Windows</span><span class="sxs-lookup"><span data-stu-id="88b98-125">Windows</span></span></td>
    <td><span data-ttu-id="88b98-126">OSX</span><span class="sxs-lookup"><span data-stu-id="88b98-126">OSX</span></span></td>
    <td><span data-ttu-id="88b98-127">Linux</span><span class="sxs-lookup"><span data-stu-id="88b98-127">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="88b98-128"><a href="https://azure.microsoft.com/features/azure-portal/">Портал Microsoft Azure</a></span><span class="sxs-lookup"><span data-stu-id="88b98-128"><a href="https://azure.microsoft.com/features/azure-portal/">Microsoft Azure Portal</a></span></span></td>
    <td><span data-ttu-id="88b98-129">X</span><span class="sxs-lookup"><span data-stu-id="88b98-129">X</span></span></td>
    <td><span data-ttu-id="88b98-130">X</span><span class="sxs-lookup"><span data-stu-id="88b98-130">X</span></span></td>
    <td><span data-ttu-id="88b98-131">X</span><span class="sxs-lookup"><span data-stu-id="88b98-131">X</span></span></td>
    <td><span data-ttu-id="88b98-132">X</span><span class="sxs-lookup"><span data-stu-id="88b98-132">X</span></span></td>
    <td><span data-ttu-id="88b98-133">X</span><span class="sxs-lookup"><span data-stu-id="88b98-133">X</span></span></td>
    <td><span data-ttu-id="88b98-134">X</span><span class="sxs-lookup"><span data-stu-id="88b98-134">X</span></span></td>
    <td><span data-ttu-id="88b98-135">Да</span><span class="sxs-lookup"><span data-stu-id="88b98-135">Y</span></span></td>
    <td><span data-ttu-id="88b98-136">X</span><span class="sxs-lookup"><span data-stu-id="88b98-136">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="88b98-137"><a href="http://storageexplorer.com/">Обозреватель службы хранилища Microsoft Azure</a></span><span class="sxs-lookup"><span data-stu-id="88b98-137"><a href="http://storageexplorer.com/">Microsoft Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="88b98-138">X</span><span class="sxs-lookup"><span data-stu-id="88b98-138">X</span></span></td>
    <td><span data-ttu-id="88b98-139">X</span><span class="sxs-lookup"><span data-stu-id="88b98-139">X</span></span></td>
    <td><span data-ttu-id="88b98-140">X</span><span class="sxs-lookup"><span data-stu-id="88b98-140">X</span></span></td>
    <td><span data-ttu-id="88b98-141">X</span><span class="sxs-lookup"><span data-stu-id="88b98-141">X</span></span></td>
    <td><span data-ttu-id="88b98-142">X</span><span class="sxs-lookup"><span data-stu-id="88b98-142">X</span></span></td>
    <td><span data-ttu-id="88b98-143">X</span><span class="sxs-lookup"><span data-stu-id="88b98-143">X</span></span></td>
    <td><span data-ttu-id="88b98-144">Да</span><span class="sxs-lookup"><span data-stu-id="88b98-144">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="88b98-145">X</span><span class="sxs-lookup"><span data-stu-id="88b98-145">X</span></span></td>
    <td><span data-ttu-id="88b98-146">X</span><span class="sxs-lookup"><span data-stu-id="88b98-146">X</span></span></td>
    <td><span data-ttu-id="88b98-147">X</span><span class="sxs-lookup"><span data-stu-id="88b98-147">X</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="88b98-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Обозреватель сервера Microsoft Visual Studio</a></span><span class="sxs-lookup"><span data-stu-id="88b98-148"><a href="https://www.visualstudio.com/features/azure-tools-vs.aspx">Microsoft Visual Studio Server Explorer</a></span></span></td>
    <td><span data-ttu-id="88b98-149">X</span><span class="sxs-lookup"><span data-stu-id="88b98-149">X</span></span></td>
    <td><span data-ttu-id="88b98-150">X</span><span class="sxs-lookup"><span data-stu-id="88b98-150">X</span></span></td>
    <td><span data-ttu-id="88b98-151">X</span><span class="sxs-lookup"><span data-stu-id="88b98-151">X</span></span></td>
    <td><span data-ttu-id="88b98-152">X</span><span class="sxs-lookup"><span data-stu-id="88b98-152">X</span></span></td>
    <td><span data-ttu-id="88b98-153">X</span><span class="sxs-lookup"><span data-stu-id="88b98-153">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="88b98-154">Да</span><span class="sxs-lookup"><span data-stu-id="88b98-154">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="88b98-155">X</span><span class="sxs-lookup"><span data-stu-id="88b98-155">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
</table>

<span data-ttu-id="88b98-156">**Сторонние клиентские инструменты службы хранилища Azure**</span><span class="sxs-lookup"><span data-stu-id="88b98-156">**Third-Party Azure Storage Client Tools**</span></span>

<span data-ttu-id="88b98-157">Мы не проверяли функциональные возможности или качество, заявленные для следующих инструментов сторонних производителей, и их наличие в списке не означает поддержку корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="88b98-157">We have not verified the functionality or quality claimed by the following third-party tools and their listing does not imply an endorsement by Microsoft.</span></span>

<table>
  <tr>
    <th rowspan="2"><span data-ttu-id="88b98-158">Клиентский инструмент службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="88b98-158">Azure Storage Client Tool</span></span></th>
    <th rowspan="2"><span data-ttu-id="88b98-159">Блочный BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="88b98-159">Block Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="88b98-160">Страничный BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="88b98-160">Page Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="88b98-161">Добавление больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="88b98-161">Append Blob</span></span></th>
    <th rowspan="2"><span data-ttu-id="88b98-162">Таблицы</span><span class="sxs-lookup"><span data-stu-id="88b98-162">Tables</span></span></th>
    <th rowspan="2"><span data-ttu-id="88b98-163">Очереди</span><span class="sxs-lookup"><span data-stu-id="88b98-163">Queues</span></span></th>
    <th rowspan="2"><span data-ttu-id="88b98-164">Файлы</span><span class="sxs-lookup"><span data-stu-id="88b98-164">Files</span></span></th>
    <th rowspan="2"><span data-ttu-id="88b98-165">Бесплатно</span><span class="sxs-lookup"><span data-stu-id="88b98-165">Free</span></span></th>
    <th colspan="4"><span data-ttu-id="88b98-166">Платформа</span><span class="sxs-lookup"><span data-stu-id="88b98-166">Platform</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="88b98-167">Web</span><span class="sxs-lookup"><span data-stu-id="88b98-167">Web</span></span></td>
    <td><span data-ttu-id="88b98-168">Windows</span><span class="sxs-lookup"><span data-stu-id="88b98-168">Windows</span></span></td>
    <td><span data-ttu-id="88b98-169">OSX</span><span class="sxs-lookup"><span data-stu-id="88b98-169">OSX</span></span></td>
    <td><span data-ttu-id="88b98-170">Linux</span><span class="sxs-lookup"><span data-stu-id="88b98-170">Linux</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="88b98-171"><a href="http://www.cloudportam.com/">Cloud Portam</a></span><span class="sxs-lookup"><span data-stu-id="88b98-171"><a href="http://www.cloudportam.com/">Cloud Portam</a></span></span></td>
    <td><span data-ttu-id="88b98-172">X</span><span class="sxs-lookup"><span data-stu-id="88b98-172">X</span></span></td>
    <td><span data-ttu-id="88b98-173">X</span><span class="sxs-lookup"><span data-stu-id="88b98-173">X</span></span></td>
    <td><span data-ttu-id="88b98-174">X</span><span class="sxs-lookup"><span data-stu-id="88b98-174">X</span></span></td>
    <td><span data-ttu-id="88b98-175">X</span><span class="sxs-lookup"><span data-stu-id="88b98-175">X</span></span></td>
    <td><span data-ttu-id="88b98-176">X</span><span class="sxs-lookup"><span data-stu-id="88b98-176">X</span></span></td>
    <td><span data-ttu-id="88b98-177">X</span><span class="sxs-lookup"><span data-stu-id="88b98-177">X</span></span></td>
    <td><span data-ttu-id="88b98-178">Пробная версия</span><span class="sxs-lookup"><span data-stu-id="88b98-178">Trial</span></span></td>
    <td><span data-ttu-id="88b98-179">X</span><span class="sxs-lookup"><span data-stu-id="88b98-179">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="88b98-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span><span class="sxs-lookup"><span data-stu-id="88b98-180"><a href="http://www.cerebrata.com/products/azure-management-studio/introduction">Cerabrata: Azure Management Studio</a></span></span></td>
    <td><span data-ttu-id="88b98-181">X</span><span class="sxs-lookup"><span data-stu-id="88b98-181">X</span></span></td>
    <td><span data-ttu-id="88b98-182">X</span><span class="sxs-lookup"><span data-stu-id="88b98-182">X</span></span></td>
    <td><span data-ttu-id="88b98-183">X</span><span class="sxs-lookup"><span data-stu-id="88b98-183">X</span></span></td>
    <td><span data-ttu-id="88b98-184">X</span><span class="sxs-lookup"><span data-stu-id="88b98-184">X</span></span></td>
    <td><span data-ttu-id="88b98-185">X</span><span class="sxs-lookup"><span data-stu-id="88b98-185">X</span></span></td>
    <td><span data-ttu-id="88b98-186">X</span><span class="sxs-lookup"><span data-stu-id="88b98-186">X</span></span></td>
    <td><span data-ttu-id="88b98-187">Пробная версия</span><span class="sxs-lookup"><span data-stu-id="88b98-187">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="88b98-188">X</span><span class="sxs-lookup"><span data-stu-id="88b98-188">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="88b98-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Azure Explorer</a></span><span class="sxs-lookup"><span data-stu-id="88b98-189"><a href="http://www.cerebrata.com/products/azure-explorer/introduction">Cerabrata: Azure Explorer</a></span></span></td>
    <td><span data-ttu-id="88b98-190">X</span><span class="sxs-lookup"><span data-stu-id="88b98-190">X</span></span></td>
    <td><span data-ttu-id="88b98-191">X</span><span class="sxs-lookup"><span data-stu-id="88b98-191">X</span></span></td>
    <td><span data-ttu-id="88b98-192">X</span><span class="sxs-lookup"><span data-stu-id="88b98-192">X</span></span></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="88b98-193">X</span><span class="sxs-lookup"><span data-stu-id="88b98-193">X</span></span></td>
    <td><span data-ttu-id="88b98-194">Да</span><span class="sxs-lookup"><span data-stu-id="88b98-194">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="88b98-195">X</span><span class="sxs-lookup"><span data-stu-id="88b98-195">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="88b98-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure Storage Explorer;</a></span><span class="sxs-lookup"><span data-stu-id="88b98-196"><a href="https://github.com/sebagomez/azurestorageexplorer">Azure Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="88b98-197">X</span><span class="sxs-lookup"><span data-stu-id="88b98-197">X</span></span></td>
    <td><span data-ttu-id="88b98-198">X</span><span class="sxs-lookup"><span data-stu-id="88b98-198">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="88b98-199">X</span><span class="sxs-lookup"><span data-stu-id="88b98-199">X</span></span></td>
    <td><span data-ttu-id="88b98-200">X</span><span class="sxs-lookup"><span data-stu-id="88b98-200">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="88b98-201">Да</span><span class="sxs-lookup"><span data-stu-id="88b98-201">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="88b98-202">X</span><span class="sxs-lookup"><span data-stu-id="88b98-202">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="88b98-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></span><span class="sxs-lookup"><span data-stu-id="88b98-203"><a href="http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx">CloudBerry Explorer</a></span></span></td>
    <td><span data-ttu-id="88b98-204">X</span><span class="sxs-lookup"><span data-stu-id="88b98-204">X</span></span></td>
    <td><span data-ttu-id="88b98-205">X</span><span class="sxs-lookup"><span data-stu-id="88b98-205">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="88b98-206">X</span><span class="sxs-lookup"><span data-stu-id="88b98-206">X</span></span></td>
    <td><span data-ttu-id="88b98-207">Да/нет</span><span class="sxs-lookup"><span data-stu-id="88b98-207">Y/N</span></span></td>
    <td></td>
    <td><span data-ttu-id="88b98-208">X</span><span class="sxs-lookup"><span data-stu-id="88b98-208">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="88b98-209"><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></span><span class="sxs-lookup"><span data-stu-id="88b98-209"><a href="http://www.gapotchenko.com/cloudcombine">Cloud Combine</a></span></span></td>
    <td><span data-ttu-id="88b98-210">X</span><span class="sxs-lookup"><span data-stu-id="88b98-210">X</span></span></td>
    <td><span data-ttu-id="88b98-211">X</span><span class="sxs-lookup"><span data-stu-id="88b98-211">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="88b98-212">X</span><span class="sxs-lookup"><span data-stu-id="88b98-212">X</span></span></td>
    <td><span data-ttu-id="88b98-213">X</span><span class="sxs-lookup"><span data-stu-id="88b98-213">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="88b98-214">Пробная версия</span><span class="sxs-lookup"><span data-stu-id="88b98-214">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="88b98-215">X</span><span class="sxs-lookup"><span data-stu-id="88b98-215">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="88b98-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span><span class="sxs-lookup"><span data-stu-id="88b98-216"><a href="http://clumsyleaf.com">ClumsyLeaf: AzureXplorer, CloudXplorer, TableXplorer</a></span></span></td>
    <td><span data-ttu-id="88b98-217">X</span><span class="sxs-lookup"><span data-stu-id="88b98-217">X</span></span></td>
    <td><span data-ttu-id="88b98-218">X</span><span class="sxs-lookup"><span data-stu-id="88b98-218">X</span></span></td>
    <td><span data-ttu-id="88b98-219">X</span><span class="sxs-lookup"><span data-stu-id="88b98-219">X</span></span></td>
    <td><span data-ttu-id="88b98-220">X</span><span class="sxs-lookup"><span data-stu-id="88b98-220">X</span></span></td>
    <td><span data-ttu-id="88b98-221">X</span><span class="sxs-lookup"><span data-stu-id="88b98-221">X</span></span></td>
    <td><span data-ttu-id="88b98-222">X</span><span class="sxs-lookup"><span data-stu-id="88b98-222">X</span></span></td>
    <td><span data-ttu-id="88b98-223">Да</span><span class="sxs-lookup"><span data-stu-id="88b98-223">Y</span></span></td>
    <td></td>
    <td><span data-ttu-id="88b98-224">X</span><span class="sxs-lookup"><span data-stu-id="88b98-224">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="88b98-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></span><span class="sxs-lookup"><span data-stu-id="88b98-225"><a href="http://www.gladinet.com/Azure-Storage/index.htm">Gladinet Cloud</a></span></span></td>
    <td><span data-ttu-id="88b98-226">X</span><span class="sxs-lookup"><span data-stu-id="88b98-226">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td><span data-ttu-id="88b98-227">Пробная версия</span><span class="sxs-lookup"><span data-stu-id="88b98-227">Trial</span></span></td>
    <td></td>
    <td><span data-ttu-id="88b98-228">X</span><span class="sxs-lookup"><span data-stu-id="88b98-228">X</span></span></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="88b98-229"><a href="http://storageexplorer.codeplex.com/">Azure Web Storage Explorer</a></span><span class="sxs-lookup"><span data-stu-id="88b98-229"><a href="http://storageexplorer.codeplex.com/">Azure Web Storage Explorer</a></span></span></td>
    <td><span data-ttu-id="88b98-230">X</span><span class="sxs-lookup"><span data-stu-id="88b98-230">X</span></span></td>
    <td><span data-ttu-id="88b98-231">X</span><span class="sxs-lookup"><span data-stu-id="88b98-231">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="88b98-232">X</span><span class="sxs-lookup"><span data-stu-id="88b98-232">X</span></span></td>
    <td><span data-ttu-id="88b98-233">X</span><span class="sxs-lookup"><span data-stu-id="88b98-233">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="88b98-234">Да</span><span class="sxs-lookup"><span data-stu-id="88b98-234">Y</span></span></td>
    <td><span data-ttu-id="88b98-235">X</span><span class="sxs-lookup"><span data-stu-id="88b98-235">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><span data-ttu-id="88b98-236"><a href="https://zudio.co/">Zudio</a></span><span class="sxs-lookup"><span data-stu-id="88b98-236"><a href="https://zudio.co/">Zudio</a></span></span></td>
    <td><span data-ttu-id="88b98-237">X</span><span class="sxs-lookup"><span data-stu-id="88b98-237">X</span></span></td>
    <td><span data-ttu-id="88b98-238">X</span><span class="sxs-lookup"><span data-stu-id="88b98-238">X</span></span></td>
    <td></td>
    <td><span data-ttu-id="88b98-239">X</span><span class="sxs-lookup"><span data-stu-id="88b98-239">X</span></span></td>
    <td><span data-ttu-id="88b98-240">X</span><span class="sxs-lookup"><span data-stu-id="88b98-240">X</span></span></td>
    <td><span data-ttu-id="88b98-241">X</span><span class="sxs-lookup"><span data-stu-id="88b98-241">X</span></span></td>
    <td><span data-ttu-id="88b98-242">Пробная версия</span><span class="sxs-lookup"><span data-stu-id="88b98-242">Trial</span></span></td>
    <td><span data-ttu-id="88b98-243">X</span><span class="sxs-lookup"><span data-stu-id="88b98-243">X</span></span></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>
