---
title: "Источники данных aaaSupported в каталоге данных Azure | Документы Microsoft"
description: "В этой статье перечислены спецификации источников данных в настоящее время поддерживается hello."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: jstevens
editor: 
tags: 
ms.assetid: fd4345ca-2ed8-4c5e-9c4b-f954be2fc9f9
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 4bfcabf31bf9fd781c939a5026abc42a5407df32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="supported-data-sources-in-azure-data-catalog"></a><span data-ttu-id="ceb8b-103">Источники данных, поддерживаемые в каталоге данных Azure</span><span class="sxs-lookup"><span data-stu-id="ceb8b-103">Supported data sources in Azure Data Catalog</span></span>

<span data-ttu-id="ceb8b-104">Можно публиковать метаданные с помощью открытого API-средства регистрации один раз, или путем ввода вручную сведения непосредственно toohello каталога данных Azure, веб-портала.</span><span class="sxs-lookup"><span data-stu-id="ceb8b-104">You can publish metadata by using a public API or a click-once registration tool, or by manually entering information directly toohello Azure Data Catalog web portal.</span></span> <span data-ttu-id="ceb8b-105">Hello следующей таблице перечислены все источники данных, поддерживаемых каталога hello сегодня и hello возможностей публикации для каждого.</span><span class="sxs-lookup"><span data-stu-id="ceb8b-105">hello following table summarizes all data sources that are supported by hello catalog today, and hello publishing capabilities for each.</span></span> <span data-ttu-id="ceb8b-106">Кроме того, содержатся hello внешние данные, предназначенные для каждого источника данных можно запустить из опыта наших портала «открыть в».</span><span class="sxs-lookup"><span data-stu-id="ceb8b-106">Also listed are hello external data tools that each data source can launch from our portal "open-in" experience.</span></span> <span data-ttu-id="ceb8b-107">Вторая таблица Hello содержит более подробные технические спецификации для каждого свойства соединения источника данных.</span><span class="sxs-lookup"><span data-stu-id="ceb8b-107">hello second table contains a more technical specification of each data-source connection property.</span></span>


## <a name="list-of-supported-data-sources"></a><span data-ttu-id="ceb8b-108">Список поддерживаемых источников данных</span><span class="sxs-lookup"><span data-stu-id="ceb8b-108">List of supported data sources</span></span>

<table>
    <tr>
       <td><span data-ttu-id="ceb8b-109"><b>Объект источника данных</b></span><span class="sxs-lookup"><span data-stu-id="ceb8b-109"><b>Data source object</b></span></span></td>
       <td><span data-ttu-id="ceb8b-110"><b>API</b></span><span class="sxs-lookup"><span data-stu-id="ceb8b-110"><b>API</b></span></span></td>
       <td><span data-ttu-id="ceb8b-111"><b>Ручной ввод</b></span><span class="sxs-lookup"><span data-stu-id="ceb8b-111"><b>Manual entry</b></span></span></td>
       <td><span data-ttu-id="ceb8b-112"><b>Средство регистрации</b></span><span class="sxs-lookup"><span data-stu-id="ceb8b-112"><b>Registration tool</b></span></span></td>
       <td><span data-ttu-id="ceb8b-113"><b>Средства Open-In</b></span><span class="sxs-lookup"><span data-stu-id="ceb8b-113"><b>Open-in tools</b></span></span></td>
       <td><span data-ttu-id="ceb8b-114"><b>Примечания</b></span><span class="sxs-lookup"><span data-stu-id="ceb8b-114"><b>Notes</b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-115">Каталог Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ceb8b-115">Azure Data Lake Store directory</span></span></td>
      <td><span data-ttu-id="ceb8b-116">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-116">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-117">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-117">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-118">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-118">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-119">Файл Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ceb8b-119">Azure Data Lake Store file</span></span></td>
      <td><span data-ttu-id="ceb8b-120">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-120">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-121">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-121">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-122">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-122">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-123">Хранилище больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="ceb8b-123">Azure Blob storage</span></span></td>
      <td><span data-ttu-id="ceb8b-124">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-124">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-125">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-125">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-126">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-126">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-127"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-127"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-128">Каталог службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="ceb8b-128">Azure Storage directory</span></span></td>
      <td><span data-ttu-id="ceb8b-129">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-129">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-130">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-130">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-131">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-131">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-132"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-132"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-133">Таблица служба хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="ceb8b-133">Azure Storage table</span></span></td>
      <td><span data-ttu-id="ceb8b-134">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-134">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-135">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-135">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-136">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-136">✓</span></span></td>
      <td>
        <font size="2"></font>
      </td>
      <td>
        <font size="2"></font>
      </td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-137">Каталог HDFS</span><span class="sxs-lookup"><span data-stu-id="ceb8b-137">HDFS directory</span></span></td>
      <td><span data-ttu-id="ceb8b-138">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-138">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-139">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-139">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-140">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-140">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-141">Файл HDFS</span><span class="sxs-lookup"><span data-stu-id="ceb8b-141">HDFS file</span></span></td>
      <td><span data-ttu-id="ceb8b-142">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-142">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-143">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-143">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-144">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-144">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-145">Таблица Hive</span><span class="sxs-lookup"><span data-stu-id="ceb8b-145">Hive table</span></span></td>
      <td><span data-ttu-id="ceb8b-146">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-146">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-147">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-147">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-148">✓</span><span class="sxs-lookup"><span data-stu-id="ceb8b-148">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-149"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-149"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-150">Представление Hive</span><span class="sxs-lookup"><span data-stu-id="ceb8b-150">Hive view</span></span></td>
      <td><span data-ttu-id="ceb8b-151">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-151">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-152">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-152">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-153">✓</span><span class="sxs-lookup"><span data-stu-id="ceb8b-153">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-154"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-154"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-155">Таблица MySQL</span><span class="sxs-lookup"><span data-stu-id="ceb8b-155">MySQL table</span></span></td>
      <td><span data-ttu-id="ceb8b-156">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-156">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-157">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-157">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-158">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-158">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-159"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-159"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-160">Представление MySQL</span><span class="sxs-lookup"><span data-stu-id="ceb8b-160">MySQL view</span></span></td>
      <td><span data-ttu-id="ceb8b-161">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-161">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-162">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-162">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-163">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-163">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-164"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-164"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-165">Таблица базы данных Oracle</span><span class="sxs-lookup"><span data-stu-id="ceb8b-165">Oracle Database table</span></span></td>
      <td><span data-ttu-id="ceb8b-166">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-166">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-167">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-167">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-168">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-168">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-169"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-169"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-170">Представление базы данных Oracle</span><span class="sxs-lookup"><span data-stu-id="ceb8b-170">Oracle Database view</span></span></td>
      <td><span data-ttu-id="ceb8b-171">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-171">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-172">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-172">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-173">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-173">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-174"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-174"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-175">Другие (универсальный ресурс)</span><span class="sxs-lookup"><span data-stu-id="ceb8b-175">Other (generic asset)</span></span></td>
      <td><span data-ttu-id="ceb8b-176">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-176">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-177">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-177">✓</span></span></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-178">Таблица хранилища данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="ceb8b-178">Azure SQL Data Warehouse table</span></span></td>
      <td><span data-ttu-id="ceb8b-179">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-179">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-180">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-180">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-181">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-181">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-182"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-182"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-183">Представление хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="ceb8b-183">SQL Data Warehouse view</span></span></td>
      <td><span data-ttu-id="ceb8b-184">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-184">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-185">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-185">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-186">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-186">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-187"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-187"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-188">Размерность SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-188">SQL Server Analysis Services dimension</span></span></td>
      <td><span data-ttu-id="ceb8b-189">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-189">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-190">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-190">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-191">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-191">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-192"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-192"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-193">Ключевые показатели эффективности SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-193">SQL Server Analysis Services KPI</span></span></td>
      <td><span data-ttu-id="ceb8b-194">✓</span><span class="sxs-lookup"><span data-stu-id="ceb8b-194">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-195">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-195">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-196">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-196">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-197"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-197"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-198">Измерение SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-198">SQL Server Analysis Services measure</span></span></td>
      <td><span data-ttu-id="ceb8b-199">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-199">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-200">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-200">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-201">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-201">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-202"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-202"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-203">Таблица SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-203">SQL Server Analysis Services table</span></span></td>
      <td><span data-ttu-id="ceb8b-204">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-204">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-205">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-205">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-206">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-206">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-207"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-207"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-208">Отчет для служб SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-208">SQL Server Reporting Services report</span></span></td>
      <td><span data-ttu-id="ceb8b-209">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-209">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-210">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-210">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-211">✓</span><span class="sxs-lookup"><span data-stu-id="ceb8b-211">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-212"><font size=2>"Обзор"</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-212"><font size=2>Browser</font></span></span></td>
      <td><span data-ttu-id="ceb8b-213"><font size=2>Только серверы в основном режиме. Режим SharePoint не поддерживается.</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-213"><font size=2>Native mode servers only. SharePoint mode is not supported.</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-214">Таблица SQL Server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-214">SQL Server table</span></span></td>
      <td><span data-ttu-id="ceb8b-215">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-215">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-216">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-216">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-217">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-217">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-218"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-218"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-219">Представление SQL Server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-219">SQL Server view</span></span></td>
      <td><span data-ttu-id="ceb8b-220">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-220">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-221">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-221">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-222">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-222">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-223"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-223"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-224">Таблица Teradata</span><span class="sxs-lookup"><span data-stu-id="ceb8b-224">Teradata table</span></span></td>
      <td><span data-ttu-id="ceb8b-225">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-225">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-226">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-226">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-227">✓</span><span class="sxs-lookup"><span data-stu-id="ceb8b-227">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-228"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-228"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-229">Представление Teradata</span><span class="sxs-lookup"><span data-stu-id="ceb8b-229">Teradata view</span></span></td>
      <td><span data-ttu-id="ceb8b-230">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-230">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-231">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-231">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-232">✓</span><span class="sxs-lookup"><span data-stu-id="ceb8b-232">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-233"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-233"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-234">Представление SAP Hana</span><span class="sxs-lookup"><span data-stu-id="ceb8b-234">SAP HANA view</span></span></td>
      <td><span data-ttu-id="ceb8b-235">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-235">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-236">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-236">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-237">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-237">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-238"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-238"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-239">Таблица DB2</span><span class="sxs-lookup"><span data-stu-id="ceb8b-239">DB2 table</span></span></td>
      <td><span data-ttu-id="ceb8b-240">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-240">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-241">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-241">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-242">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-242">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-243">Представление DB2</span><span class="sxs-lookup"><span data-stu-id="ceb8b-243">DB2 view</span></span></td>
      <td><span data-ttu-id="ceb8b-244">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-244">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-245">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-245">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-246">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-246">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-247">Файл файловой системы</span><span class="sxs-lookup"><span data-stu-id="ceb8b-247">File system file</span></span></td>
      <td><span data-ttu-id="ceb8b-248">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-248">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-249">Каталог FTP</span><span class="sxs-lookup"><span data-stu-id="ceb8b-249">FTP directory</span></span></td>
      <td><span data-ttu-id="ceb8b-250">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-250">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-251">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-251">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-252">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-252">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-253">Файл FTP</span><span class="sxs-lookup"><span data-stu-id="ceb8b-253">FTP file</span></span></td>
      <td><span data-ttu-id="ceb8b-254">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-254">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-255">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-255">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-256">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-256">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-257">Отчет HTTP</span><span class="sxs-lookup"><span data-stu-id="ceb8b-257">HTTP report</span></span></td>
      <td><span data-ttu-id="ceb8b-258">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-258">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-259">Конечная точка HTTP</span><span class="sxs-lookup"><span data-stu-id="ceb8b-259">HTTP endpoint</span></span></td>
      <td><span data-ttu-id="ceb8b-260">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-260">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-261">Файл HTTP</span><span class="sxs-lookup"><span data-stu-id="ceb8b-261">HTTP file</span></span></td>
      <td><span data-ttu-id="ceb8b-262">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-262">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-263">Набор сущностей OData</span><span class="sxs-lookup"><span data-stu-id="ceb8b-263">OData entity set</span></span></td>
      <td><span data-ttu-id="ceb8b-264">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-264">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-265">Функция OData</span><span class="sxs-lookup"><span data-stu-id="ceb8b-265">OData function</span></span></td>
      <td><span data-ttu-id="ceb8b-266">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-266">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-267">Таблица PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ceb8b-267">PostgreSQL table</span></span></td>
      <td><span data-ttu-id="ceb8b-268">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-268">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-269">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-269">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-270">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-270">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-271">Представление PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ceb8b-271">PostgreSQL view</span></span></td>
      <td><span data-ttu-id="ceb8b-272">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-272">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-273">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-273">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-274">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-274">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-275">Представление SAP Hana</span><span class="sxs-lookup"><span data-stu-id="ceb8b-275">SAP HANA view</span></span></td>
      <td><span data-ttu-id="ceb8b-276">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-276">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td> <span data-ttu-id="ceb8b-277">Объект SalesForce</span><span class="sxs-lookup"><span data-stu-id="ceb8b-277">Salesforce object</span></span></td>
      <td><span data-ttu-id="ceb8b-278">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-278">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-279">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-279">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-280">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-280">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-281">Список SharePoint</span><span class="sxs-lookup"><span data-stu-id="ceb8b-281">SharePoint list</span></span> </td>
      <td><span data-ttu-id="ceb8b-282">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-282">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-283">Коллекция Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ceb8b-283">Azure Cosmos DB collection</span></span></td>
      <td><span data-ttu-id="ceb8b-284">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-284">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-285">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-285">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-286">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-286">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-287">Универсальная таблица ODBC</span><span class="sxs-lookup"><span data-stu-id="ceb8b-287">Generic ODBC table</span></span></td>
      <td><span data-ttu-id="ceb8b-288">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-288">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-289">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-289">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-290">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-290">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-291">Универсальное представление ODBC</span><span class="sxs-lookup"><span data-stu-id="ceb8b-291">Generic ODBC view</span></span></td>
      <td><span data-ttu-id="ceb8b-292">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-292">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-293">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-293">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-294">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-294">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-295">Таблица Cassandra</span><span class="sxs-lookup"><span data-stu-id="ceb8b-295">Cassandra table</span></span></td>
      <td><span data-ttu-id="ceb8b-296">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-296">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-297">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-297">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-298">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-298">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="ceb8b-299"><font size=2>Публикация в качестве ресурса ODBC</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-299"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-300">Представление Cassandra</span><span class="sxs-lookup"><span data-stu-id="ceb8b-300">Cassandra view</span></span></td>
      <td><span data-ttu-id="ceb8b-301">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-301">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-302">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-302">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-303">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-303">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="ceb8b-304"><font size=2>Публикация в качестве ресурса ODBC</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-304"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-305">Таблица Sybase</span><span class="sxs-lookup"><span data-stu-id="ceb8b-305">Sybase table</span></span></td>
      <td><span data-ttu-id="ceb8b-306">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-306">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-307">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-307">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-308">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-308">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-309">Представление Sybase</span><span class="sxs-lookup"><span data-stu-id="ceb8b-309">Sybase view</span></span></td>
      <td><span data-ttu-id="ceb8b-310">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-310">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-311">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-311">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-312">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-312">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-313">Таблица MongoDB</span><span class="sxs-lookup"><span data-stu-id="ceb8b-313">MongoDB table</span></span></td>
      <td><span data-ttu-id="ceb8b-314">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-314">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-315">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-315">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-316">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-316">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="ceb8b-317"><font size=2>Публикация в качестве ресурса ODBC</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-317"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-318">Представление MongoDB</span><span class="sxs-lookup"><span data-stu-id="ceb8b-318">MongoDB view</span></span></td>
      <td><span data-ttu-id="ceb8b-319">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-319">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-320">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-320">✓</span></span></td>
      <td><span data-ttu-id="ceb8b-321">✓ </span><span class="sxs-lookup"><span data-stu-id="ceb8b-321">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="ceb8b-322"><font size=2>Публикация в качестве ресурса ODBC</font></span><span class="sxs-lookup"><span data-stu-id="ceb8b-322"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
</table>

<span data-ttu-id="ceb8b-323">Если необходима поддержка дополнительных источников отправки запроса компонент toohello [форуме каталога данных Azure](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="ceb8b-323">If you need support for additional sources, submit a feature request toohello [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span></span>


## <a name="data-source-reference-specification"></a><span data-ttu-id="ceb8b-324">Спецификация ссылки на источник данных</span><span class="sxs-lookup"><span data-stu-id="ceb8b-324">Data-source reference specification</span></span>
> [!NOTE]
> <span data-ttu-id="ceb8b-325">Hello **структуры DSL** столбце hello в следующей таблице перечислены только hello свойства соединения для «address» в контейнере свойств, используемых каталога данных Azure.</span><span class="sxs-lookup"><span data-stu-id="ceb8b-325">hello **DSL structure** column in hello following table lists only hello connection properties for "address" property bag that are used by Azure Data Catalog.</span></span> <span data-ttu-id="ceb8b-326">То есть контейнер свойств «адрес» может содержать другие свойства соединения источника данных hello, которое каталога данных Azure сохраняется, но не использует.</span><span class="sxs-lookup"><span data-stu-id="ceb8b-326">That is, "address" property bag can contain other connection properties of hello data source which Azure Data Catalog persists, but does not use.</span></span>

<table>
    <tr>
       <td><span data-ttu-id="ceb8b-327"><b>Тип источника</b></span><span class="sxs-lookup"><span data-stu-id="ceb8b-327"><b>Source type</b></span></span></td>
       <td><span data-ttu-id="ceb8b-328"><b>Тип ресурса</b></span><span class="sxs-lookup"><span data-stu-id="ceb8b-328"><b>Asset type</b></span></span></td>
       <td><span data-ttu-id="ceb8b-329"><b>Типы объектов</b></span><span class="sxs-lookup"><span data-stu-id="ceb8b-329"><b>Object types</b></span></span></td>
       <td><span data-ttu-id="ceb8b-330"><b>Структура DSL<b></span><span class="sxs-lookup"><span data-stu-id="ceb8b-330"><b>DSL structure<b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-331">Хранилище озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="ceb8b-331">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="ceb8b-332">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-332">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-333">Озеро данных</span><span class="sxs-lookup"><span data-stu-id="ceb8b-333">Data Lake</span></span></td>
      <td><span data-ttu-id="ceb8b-334">
        <font size=2> Протокол: webhdfs</span><span class="sxs-lookup"><span data-stu-id="ceb8b-334">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="ceb8b-335">Аутентификация: {basic, oauth}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-335">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="ceb8b-336">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-336">Address:</span></span> <br><span data-ttu-id="ceb8b-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-338">Хранилище озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="ceb8b-338">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="ceb8b-339">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-339">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-340">Каталог, файл</span><span class="sxs-lookup"><span data-stu-id="ceb8b-340">Directory, file</span></span></td>
      <td><span data-ttu-id="ceb8b-341">
        <font size=2> Протокол: webhdfs</span><span class="sxs-lookup"><span data-stu-id="ceb8b-341">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="ceb8b-342">Аутентификация: {basic, oauth}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-342">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="ceb8b-343">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-343">Address:</span></span> <br><span data-ttu-id="ceb8b-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-345">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="ceb8b-345">Azure Storage</span></span></td>
      <td><span data-ttu-id="ceb8b-346">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-346">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-347">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-347">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-348">
        <font size=2> Протокол: azure-blobs</span><span class="sxs-lookup"><span data-stu-id="ceb8b-348">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="ceb8b-349">Аутентификация: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-349">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="ceb8b-350">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-350">Address:</span></span> <br><span data-ttu-id="ceb8b-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="ceb8b-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="ceb8b-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span><span class="sxs-lookup"><span data-stu-id="ceb8b-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="ceb8b-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-354">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="ceb8b-354">Azure Storage</span></span></td>
      <td><span data-ttu-id="ceb8b-355">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-355">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-356">Большой двоичный объект, каталог</span><span class="sxs-lookup"><span data-stu-id="ceb8b-356">Blob, directory</span></span></td>
      <td><span data-ttu-id="ceb8b-357">
        <font size=2> Протокол: azure-blobs</span><span class="sxs-lookup"><span data-stu-id="ceb8b-357">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="ceb8b-358">Аутентификация: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-358">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="ceb8b-359">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-359">Address:</span></span> <br><span data-ttu-id="ceb8b-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="ceb8b-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="ceb8b-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span><span class="sxs-lookup"><span data-stu-id="ceb8b-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="ceb8b-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container</span><span class="sxs-lookup"><span data-stu-id="ceb8b-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container</span></span> <br><span data-ttu-id="ceb8b-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-364">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="ceb8b-364">Azure Storage</span></span></td>
      <td><span data-ttu-id="ceb8b-365">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-365">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-366">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-366">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-367">
        <font size=2> Протокол: azure-tables</span><span class="sxs-lookup"><span data-stu-id="ceb8b-367">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="ceb8b-368">Аутентификация: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-368">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="ceb8b-369">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-369">Address:</span></span> <br><span data-ttu-id="ceb8b-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="ceb8b-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="ceb8b-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-372">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="ceb8b-372">Azure Storage</span></span></td>
      <td><span data-ttu-id="ceb8b-373">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-373">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-374">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-374">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-375">
        <font size=2> Протокол: azure-tables</span><span class="sxs-lookup"><span data-stu-id="ceb8b-375">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="ceb8b-376">Аутентификация: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-376">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="ceb8b-377">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-377">Address:</span></span> <br><span data-ttu-id="ceb8b-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="ceb8b-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="ceb8b-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span><span class="sxs-lookup"><span data-stu-id="ceb8b-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="ceb8b-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-381">Cosmos</span><span class="sxs-lookup"><span data-stu-id="ceb8b-381">Cosmos</span></span></td>
      <td><span data-ttu-id="ceb8b-382">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-382">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-383">Виртуальный кластер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-383">Virtual cluster</span></span></td>
      <td><span data-ttu-id="ceb8b-384">
        <font size=2> Протокол: cosmos</span><span class="sxs-lookup"><span data-stu-id="ceb8b-384">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="ceb8b-385">Аутентификация: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-385">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="ceb8b-386">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-386">Address:</span></span> <br><span data-ttu-id="ceb8b-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-388">Cosmos</span><span class="sxs-lookup"><span data-stu-id="ceb8b-388">Cosmos</span></span></td>
      <td><span data-ttu-id="ceb8b-389">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-389">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-390">Поток, набор потоков, представление</span><span class="sxs-lookup"><span data-stu-id="ceb8b-390">Stream, stream set, view</span></span></td>
      <td><span data-ttu-id="ceb8b-391">
        <font size=2> Протокол: cosmos</span><span class="sxs-lookup"><span data-stu-id="ceb8b-391">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="ceb8b-392">Аутентификация: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-392">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="ceb8b-393">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-393">Address:</span></span> <br><span data-ttu-id="ceb8b-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-395">DataZen</span><span class="sxs-lookup"><span data-stu-id="ceb8b-395">Datazen</span></span></td>
      <td><span data-ttu-id="ceb8b-396">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-396">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-397">Сайт</span><span class="sxs-lookup"><span data-stu-id="ceb8b-397">Site</span></span></td>
      <td><span data-ttu-id="ceb8b-398">
        <font size=2> Протокол: http</span><span class="sxs-lookup"><span data-stu-id="ceb8b-398">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="ceb8b-399">Аутентификация: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-399">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="ceb8b-400">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-400">Address:</span></span> <br><span data-ttu-id="ceb8b-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-402">DataZen</span><span class="sxs-lookup"><span data-stu-id="ceb8b-402">Datazen</span></span></td>
      <td><span data-ttu-id="ceb8b-403">Отчет</span><span class="sxs-lookup"><span data-stu-id="ceb8b-403">Report</span></span></td>
      <td><span data-ttu-id="ceb8b-404">Отчет, панель мониторинга</span><span class="sxs-lookup"><span data-stu-id="ceb8b-404">Report, dashboard</span></span></td>
      <td><span data-ttu-id="ceb8b-405">
        <font size=2> Протокол: http</span><span class="sxs-lookup"><span data-stu-id="ceb8b-405">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="ceb8b-406">Аутентификация: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-406">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="ceb8b-407">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-407">Address:</span></span> <br><span data-ttu-id="ceb8b-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-409">DB2</span><span class="sxs-lookup"><span data-stu-id="ceb8b-409">DB2</span></span></td>
      <td><span data-ttu-id="ceb8b-410">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-410">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-411">База данных</span><span class="sxs-lookup"><span data-stu-id="ceb8b-411">Database</span></span></td>
      <td><span data-ttu-id="ceb8b-412">
        <font size=2> Протокол: DB2</span><span class="sxs-lookup"><span data-stu-id="ceb8b-412">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="ceb8b-413">Аутентификация: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-413">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="ceb8b-414">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-414">Address:</span></span> <br><span data-ttu-id="ceb8b-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-417">DB2</span><span class="sxs-lookup"><span data-stu-id="ceb8b-417">DB2</span></span></td>
      <td><span data-ttu-id="ceb8b-418">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-418">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-419">Таблица, представление</span><span class="sxs-lookup"><span data-stu-id="ceb8b-419">Table, view</span></span></td>
      <td><span data-ttu-id="ceb8b-420">
        <font size=2> Протокол: DB2</span><span class="sxs-lookup"><span data-stu-id="ceb8b-420">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="ceb8b-421">Аутентификация: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-421">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="ceb8b-422">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-422">Address:</span></span> <br><span data-ttu-id="ceb8b-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="ceb8b-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="ceb8b-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-427">Файловая система</span><span class="sxs-lookup"><span data-stu-id="ceb8b-427">File system</span></span></td>
      <td><span data-ttu-id="ceb8b-428">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-428">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-429">Файл</span><span class="sxs-lookup"><span data-stu-id="ceb8b-429">File</span></span></td>
      <td><span data-ttu-id="ceb8b-430">
        <font size=2> Протокол: файл</span><span class="sxs-lookup"><span data-stu-id="ceb8b-430">
        <font size=2> Protocol: file</span></span> <br><span data-ttu-id="ceb8b-431">Аутентификация: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-431">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="ceb8b-432">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-432">Address:</span></span> <br><span data-ttu-id="ceb8b-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-434">FTP</span><span class="sxs-lookup"><span data-stu-id="ceb8b-434">FTP</span></span></td>
      <td><span data-ttu-id="ceb8b-435">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-435">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-436">Каталог, файл</span><span class="sxs-lookup"><span data-stu-id="ceb8b-436">Directory, file</span></span></td>
      <td><span data-ttu-id="ceb8b-437">
        <font size=2> Протокол: ftp</span><span class="sxs-lookup"><span data-stu-id="ceb8b-437">
        <font size=2> Protocol: ftp</span></span> <br><span data-ttu-id="ceb8b-438">Аутентификация: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-438">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="ceb8b-439">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-439">Address:</span></span> <br><span data-ttu-id="ceb8b-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-441">Распределенная файловая система Hadoop</span><span class="sxs-lookup"><span data-stu-id="ceb8b-441">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="ceb8b-442">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-442">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-443">HDInsight</span><span class="sxs-lookup"><span data-stu-id="ceb8b-443">Cluster</span></span></td>
      <td><span data-ttu-id="ceb8b-444">
        <font size=2> Протокол: webhdfs</span><span class="sxs-lookup"><span data-stu-id="ceb8b-444">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="ceb8b-445">Аутентификация: {basic, oauth}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-445">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="ceb8b-446">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-446">Address:</span></span> <br><span data-ttu-id="ceb8b-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-448">Распределенная файловая система Hadoop</span><span class="sxs-lookup"><span data-stu-id="ceb8b-448">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="ceb8b-449">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-449">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-450">Каталог, файл</span><span class="sxs-lookup"><span data-stu-id="ceb8b-450">Directory, file</span></span></td>
      <td><span data-ttu-id="ceb8b-451">
        <font size=2> Протокол: webhdfs</span><span class="sxs-lookup"><span data-stu-id="ceb8b-451">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="ceb8b-452">Аутентификация: {basic, oauth}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-452">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="ceb8b-453">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-453">Address:</span></span> <br><span data-ttu-id="ceb8b-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-455">Hive</span><span class="sxs-lookup"><span data-stu-id="ceb8b-455">Hive</span></span></td>
      <td><span data-ttu-id="ceb8b-456">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-456">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-457">База данных</span><span class="sxs-lookup"><span data-stu-id="ceb8b-457">Database</span></span></td>
      <td><span data-ttu-id="ceb8b-458">
        <font size=2> Протокол: hive</span><span class="sxs-lookup"><span data-stu-id="ceb8b-458">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="ceb8b-459">Аутентификация: {hdinsight, basic, username, none}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-459">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="ceb8b-460">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-460">Address:</span></span> <br><span data-ttu-id="ceb8b-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-463">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-463">connectionProperties:</span></span> <br><span data-ttu-id="ceb8b-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-465">Hive</span><span class="sxs-lookup"><span data-stu-id="ceb8b-465">Hive</span></span></td>
      <td><span data-ttu-id="ceb8b-466">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-466">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-467">Таблица, представление</span><span class="sxs-lookup"><span data-stu-id="ceb8b-467">Table, view</span></span></td>
      <td><span data-ttu-id="ceb8b-468">
        <font size=2> Протокол: hive</span><span class="sxs-lookup"><span data-stu-id="ceb8b-468">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="ceb8b-469">Аутентификация: {hdinsight, basic, username, none}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-469">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="ceb8b-470">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-470">Address:</span></span> <br><span data-ttu-id="ceb8b-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="ceb8b-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="ceb8b-474">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-474">connectionProperties:</span></span> <br><span data-ttu-id="ceb8b-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-476">HTTP</span><span class="sxs-lookup"><span data-stu-id="ceb8b-476">HTTP</span></span></td>
      <td><span data-ttu-id="ceb8b-477">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-477">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-478">Сайт</span><span class="sxs-lookup"><span data-stu-id="ceb8b-478">Site</span></span></td>
      <td><span data-ttu-id="ceb8b-479">
        <font size=2> Протокол: http</span><span class="sxs-lookup"><span data-stu-id="ceb8b-479">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="ceb8b-480">Аутентификация: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-480">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="ceb8b-481">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-481">Address:</span></span> <br><span data-ttu-id="ceb8b-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-483">HTTP</span><span class="sxs-lookup"><span data-stu-id="ceb8b-483">HTTP</span></span></td>
      <td><span data-ttu-id="ceb8b-484">Отчет</span><span class="sxs-lookup"><span data-stu-id="ceb8b-484">Report</span></span></td>
      <td><span data-ttu-id="ceb8b-485">Отчет, панель мониторинга</span><span class="sxs-lookup"><span data-stu-id="ceb8b-485">Report, dashboard</span></span></td>
      <td><span data-ttu-id="ceb8b-486">
        <font size=2> Протокол: http</span><span class="sxs-lookup"><span data-stu-id="ceb8b-486">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="ceb8b-487">Аутентификация: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-487">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="ceb8b-488">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-488">Address:</span></span> <br><span data-ttu-id="ceb8b-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-490">HTTP</span><span class="sxs-lookup"><span data-stu-id="ceb8b-490">HTTP</span></span></td>
      <td><span data-ttu-id="ceb8b-491">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-491">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-492">Конечная точка, файл</span><span class="sxs-lookup"><span data-stu-id="ceb8b-492">Endpoint, file</span></span></td>
      <td><span data-ttu-id="ceb8b-493">
        <font size=2> Протокол: http</span><span class="sxs-lookup"><span data-stu-id="ceb8b-493">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="ceb8b-494">Аутентификация: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-494">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="ceb8b-495">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-495">Address:</span></span> <br><span data-ttu-id="ceb8b-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-497">MySQL</span><span class="sxs-lookup"><span data-stu-id="ceb8b-497">MySQL</span></span></td>
      <td><span data-ttu-id="ceb8b-498">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-498">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-499">База данных</span><span class="sxs-lookup"><span data-stu-id="ceb8b-499">Database</span></span></td>
      <td><span data-ttu-id="ceb8b-500">
        <font size=2> Протокол: mysql</span><span class="sxs-lookup"><span data-stu-id="ceb8b-500">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="ceb8b-501">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-501">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ceb8b-502">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-502">Address:</span></span> <br><span data-ttu-id="ceb8b-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-505">MySQL</span><span class="sxs-lookup"><span data-stu-id="ceb8b-505">MySQL</span></span></td>
      <td><span data-ttu-id="ceb8b-506">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-506">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-507">Таблица, представление</span><span class="sxs-lookup"><span data-stu-id="ceb8b-507">Table, view</span></span></td>
      <td><span data-ttu-id="ceb8b-508">
        <font size=2> Протокол: mysql</span><span class="sxs-lookup"><span data-stu-id="ceb8b-508">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="ceb8b-509">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-509">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ceb8b-510">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-510">Address:</span></span> <br><span data-ttu-id="ceb8b-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-514">OData</span><span class="sxs-lookup"><span data-stu-id="ceb8b-514">OData</span></span></td>
      <td><span data-ttu-id="ceb8b-515">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-515">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-516">Контейнер сущностей</span><span class="sxs-lookup"><span data-stu-id="ceb8b-516">Entity container</span></span></td>
      <td><span data-ttu-id="ceb8b-517">
        <font size=2> Протокол: odata</span><span class="sxs-lookup"><span data-stu-id="ceb8b-517">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="ceb8b-518">Аутентификация: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-518">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="ceb8b-519">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-519">Address:</span></span> <br><span data-ttu-id="ceb8b-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-521">OData</span><span class="sxs-lookup"><span data-stu-id="ceb8b-521">OData</span></span></td>
      <td><span data-ttu-id="ceb8b-522">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-522">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-523">Набор сущностей, функция</span><span class="sxs-lookup"><span data-stu-id="ceb8b-523">Entity set, function</span></span></td>
      <td><span data-ttu-id="ceb8b-524">
        <font size=2> Протокол: odata</span><span class="sxs-lookup"><span data-stu-id="ceb8b-524">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="ceb8b-525">Аутентификация: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-525">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="ceb8b-526">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-526">Address:</span></span> <br><span data-ttu-id="ceb8b-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="ceb8b-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="ceb8b-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-529">База данных Oracle</span><span class="sxs-lookup"><span data-stu-id="ceb8b-529">Oracle Database</span></span></td>
      <td><span data-ttu-id="ceb8b-530">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-530">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-531">База данных</span><span class="sxs-lookup"><span data-stu-id="ceb8b-531">Database</span></span></td>
      <td><span data-ttu-id="ceb8b-532">
        <font size=2> Протокол: oracle</span><span class="sxs-lookup"><span data-stu-id="ceb8b-532">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="ceb8b-533">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-533">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ceb8b-534">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-534">Address:</span></span> <br><span data-ttu-id="ceb8b-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-537">База данных Oracle</span><span class="sxs-lookup"><span data-stu-id="ceb8b-537">Oracle Database</span></span></td>
      <td><span data-ttu-id="ceb8b-538">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-538">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-539">Таблица, представление</span><span class="sxs-lookup"><span data-stu-id="ceb8b-539">Table, view</span></span></td>
      <td><span data-ttu-id="ceb8b-540">
        <font size=2> Протокол: oracle</span><span class="sxs-lookup"><span data-stu-id="ceb8b-540">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="ceb8b-541">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-541">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ceb8b-542">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-542">Address:</span></span> <br><span data-ttu-id="ceb8b-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="ceb8b-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="ceb8b-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-547">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ceb8b-547">PostgreSQL</span></span></td>
      <td><span data-ttu-id="ceb8b-548">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-548">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-549">База данных</span><span class="sxs-lookup"><span data-stu-id="ceb8b-549">Database</span></span></td>
      <td><span data-ttu-id="ceb8b-550">
        <font size=2> Протокол: postgresql</span><span class="sxs-lookup"><span data-stu-id="ceb8b-550">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="ceb8b-551">Аутентификация: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-551">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="ceb8b-552">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-552">Address:</span></span> <br><span data-ttu-id="ceb8b-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-555">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="ceb8b-555">PostgreSQL</span></span></td>
      <td><span data-ttu-id="ceb8b-556">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-556">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-557">Таблица, представление</span><span class="sxs-lookup"><span data-stu-id="ceb8b-557">Table, view</span></span></td>
      <td><span data-ttu-id="ceb8b-558">
        <font size=2> Протокол: postgresql</span><span class="sxs-lookup"><span data-stu-id="ceb8b-558">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="ceb8b-559">Аутентификация: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-559">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="ceb8b-560">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-560">Address:</span></span> <br><span data-ttu-id="ceb8b-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="ceb8b-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="ceb8b-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-565">Power BI</span><span class="sxs-lookup"><span data-stu-id="ceb8b-565">Power BI</span></span></td>
      <td><span data-ttu-id="ceb8b-566">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-566">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-567">Сайт</span><span class="sxs-lookup"><span data-stu-id="ceb8b-567">Site</span></span></td>
      <td><span data-ttu-id="ceb8b-568">
        <font size=2> Протокол: http</span><span class="sxs-lookup"><span data-stu-id="ceb8b-568">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="ceb8b-569">Аутентификация: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-569">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="ceb8b-570">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-570">Address:</span></span> <br><span data-ttu-id="ceb8b-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-572">Power BI</span><span class="sxs-lookup"><span data-stu-id="ceb8b-572">Power BI</span></span></td>
      <td><span data-ttu-id="ceb8b-573">Отчет</span><span class="sxs-lookup"><span data-stu-id="ceb8b-573">Report</span></span></td>
      <td><span data-ttu-id="ceb8b-574">Отчет, панель мониторинга</span><span class="sxs-lookup"><span data-stu-id="ceb8b-574">Report, dashboard</span></span></td>
      <td><span data-ttu-id="ceb8b-575">
        <font size=2> Протокол: http</span><span class="sxs-lookup"><span data-stu-id="ceb8b-575">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="ceb8b-576">Аутентификация: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-576">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="ceb8b-577">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-577">Address:</span></span> <br><span data-ttu-id="ceb8b-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-579">Power Query</span><span class="sxs-lookup"><span data-stu-id="ceb8b-579">Power Query</span></span></td>
      <td><span data-ttu-id="ceb8b-580">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-580">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-581">Гибридные данные</span><span class="sxs-lookup"><span data-stu-id="ceb8b-581">Data mashup</span></span></td>
      <td><span data-ttu-id="ceb8b-582">
        <font size=2> Протокол: power-query</span><span class="sxs-lookup"><span data-stu-id="ceb8b-582">
        <font size=2> Protocol: power-query</span></span> <br><span data-ttu-id="ceb8b-583">Аутентификация: {oauth}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-583">Authentication: {oauth}</span></span> <br><span data-ttu-id="ceb8b-584">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-584">Address:</span></span> <br><span data-ttu-id="ceb8b-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-586">Salesforce</span><span class="sxs-lookup"><span data-stu-id="ceb8b-586">Salesforce</span></span></td>
      <td><span data-ttu-id="ceb8b-587">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-587">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-588">Объект</span><span class="sxs-lookup"><span data-stu-id="ceb8b-588">Object</span></span></td>
      <td><span data-ttu-id="ceb8b-589">
        <font size=2> Протокол: salesforce-com</span><span class="sxs-lookup"><span data-stu-id="ceb8b-589">
        <font size=2> Protocol: salesforce-com</span></span> <br><span data-ttu-id="ceb8b-590">Аутентификация: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-590">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="ceb8b-591">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-591">Address:</span></span> <br><span data-ttu-id="ceb8b-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span><span class="sxs-lookup"><span data-stu-id="ceb8b-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span></span> <br><span data-ttu-id="ceb8b-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span><span class="sxs-lookup"><span data-stu-id="ceb8b-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span></span> <br><span data-ttu-id="ceb8b-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-595">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="ceb8b-595">SAP HANA</span></span></td>
      <td><span data-ttu-id="ceb8b-596">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-596">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-597">сервер;</span><span class="sxs-lookup"><span data-stu-id="ceb8b-597">Server</span></span></td>
      <td><span data-ttu-id="ceb8b-598">
        <font size=2> Протокол: sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="ceb8b-598">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="ceb8b-599">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-599">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ceb8b-600">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-600">Address:</span></span> <br><span data-ttu-id="ceb8b-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-602">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="ceb8b-602">SAP HANA</span></span></td>
      <td><span data-ttu-id="ceb8b-603">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-603">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-604">Просмотр</span><span class="sxs-lookup"><span data-stu-id="ceb8b-604">View</span></span></td>
      <td><span data-ttu-id="ceb8b-605">
        <font size=2> Протокол: sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="ceb8b-605">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="ceb8b-606">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-606">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ceb8b-607">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-607">Address:</span></span> <br><span data-ttu-id="ceb8b-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="ceb8b-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="ceb8b-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-611">SharePoint</span><span class="sxs-lookup"><span data-stu-id="ceb8b-611">SharePoint</span></span></td>
      <td><span data-ttu-id="ceb8b-612">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-612">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-613">список</span><span class="sxs-lookup"><span data-stu-id="ceb8b-613">List</span></span></td>
      <td><span data-ttu-id="ceb8b-614">
        <font size=2> Протокол: sharepoint-list</span><span class="sxs-lookup"><span data-stu-id="ceb8b-614">
        <font size=2> Protocol: sharepoint-list</span></span> <br><span data-ttu-id="ceb8b-615">Аутентификация: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-615">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="ceb8b-616">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-616">Address:</span></span> <br><span data-ttu-id="ceb8b-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-618">Хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="ceb8b-618">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="ceb8b-619">Команда</span><span class="sxs-lookup"><span data-stu-id="ceb8b-619">Command</span></span></td>
      <td><span data-ttu-id="ceb8b-620">Хранимая процедура</span><span class="sxs-lookup"><span data-stu-id="ceb8b-620">Stored procedure</span></span></td>
      <td><span data-ttu-id="ceb8b-621">
        <font size=2> Протокол: tds</span><span class="sxs-lookup"><span data-stu-id="ceb8b-621">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="ceb8b-622">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-622">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ceb8b-623">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-623">Address:</span></span> <br><span data-ttu-id="ceb8b-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="ceb8b-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="ceb8b-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-628">Хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="ceb8b-628">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="ceb8b-629">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="ceb8b-629">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="ceb8b-630">Функция с табличным значением</span><span class="sxs-lookup"><span data-stu-id="ceb8b-630">Table-valued function</span></span></td>
      <td><span data-ttu-id="ceb8b-631">
        <font size=2> Протокол: tds</span><span class="sxs-lookup"><span data-stu-id="ceb8b-631">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="ceb8b-632">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-632">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ceb8b-633">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-633">Address:</span></span> <br><span data-ttu-id="ceb8b-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="ceb8b-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="ceb8b-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-638">Хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="ceb8b-638">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="ceb8b-639">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-639">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-640">База данных</span><span class="sxs-lookup"><span data-stu-id="ceb8b-640">Database</span></span></td>
      <td><span data-ttu-id="ceb8b-641">
        <font size=2> Протокол: tds</span><span class="sxs-lookup"><span data-stu-id="ceb8b-641">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="ceb8b-642">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-642">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ceb8b-643">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-643">Address:</span></span> <br><span data-ttu-id="ceb8b-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-646">Хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="ceb8b-646">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="ceb8b-647">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-647">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-648">Таблица, представление</span><span class="sxs-lookup"><span data-stu-id="ceb8b-648">Table, view</span></span></td>
      <td><span data-ttu-id="ceb8b-649">
        <font size=2> Протокол: tds</span><span class="sxs-lookup"><span data-stu-id="ceb8b-649">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="ceb8b-650">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-650">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ceb8b-651">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-651">Address:</span></span> <br><span data-ttu-id="ceb8b-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="ceb8b-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="ceb8b-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-656">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-656">SQL Server</span></span></td>
      <td><span data-ttu-id="ceb8b-657">Команда</span><span class="sxs-lookup"><span data-stu-id="ceb8b-657">Command</span></span></td>
      <td><span data-ttu-id="ceb8b-658">Хранимая процедура</span><span class="sxs-lookup"><span data-stu-id="ceb8b-658">Stored procedure</span></span></td>
      <td><span data-ttu-id="ceb8b-659">
        <font size=2> Протокол: tds</span><span class="sxs-lookup"><span data-stu-id="ceb8b-659">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="ceb8b-660">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-660">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ceb8b-661">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-661">Address:</span></span> <br><span data-ttu-id="ceb8b-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="ceb8b-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="ceb8b-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-666">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-666">SQL Server</span></span></td>
      <td><span data-ttu-id="ceb8b-667">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="ceb8b-667">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="ceb8b-668">Функция с табличным значением</span><span class="sxs-lookup"><span data-stu-id="ceb8b-668">Table-valued function</span></span></td>
      <td><span data-ttu-id="ceb8b-669">
        <font size=2> Протокол: tds</span><span class="sxs-lookup"><span data-stu-id="ceb8b-669">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="ceb8b-670">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-670">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ceb8b-671">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-671">Address:</span></span> <br><span data-ttu-id="ceb8b-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="ceb8b-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="ceb8b-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-676">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-676">SQL Server</span></span></td>
      <td><span data-ttu-id="ceb8b-677">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-677">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-678">База данных</span><span class="sxs-lookup"><span data-stu-id="ceb8b-678">Database</span></span></td>
      <td><span data-ttu-id="ceb8b-679">
        <font size=2> Протокол: tds</span><span class="sxs-lookup"><span data-stu-id="ceb8b-679">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="ceb8b-680">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-680">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ceb8b-681">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-681">Address:</span></span> <br><span data-ttu-id="ceb8b-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-684">SQL Server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-684">SQL Server</span></span></td>
      <td><span data-ttu-id="ceb8b-685">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-685">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-686">Таблица, представление</span><span class="sxs-lookup"><span data-stu-id="ceb8b-686">Table, view</span></span></td>
      <td><span data-ttu-id="ceb8b-687">
        <font size=2> Протокол: tds</span><span class="sxs-lookup"><span data-stu-id="ceb8b-687">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="ceb8b-688">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-688">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ceb8b-689">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-689">Address:</span></span> <br><span data-ttu-id="ceb8b-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="ceb8b-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="ceb8b-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-694">Многомерная модель служб SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-694">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="ceb8b-695">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-695">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-696">Модель</span><span class="sxs-lookup"><span data-stu-id="ceb8b-696">Model</span></span></td>
      <td><span data-ttu-id="ceb8b-697">
        <font size=2> Протокол: analysis-services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-697">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="ceb8b-698">Аутентификация: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-698">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="ceb8b-699">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-699">Address:</span></span> <br><span data-ttu-id="ceb8b-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-703">Многомерная модель служб SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-703">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="ceb8b-704">Ключевой показатель эффективности</span><span class="sxs-lookup"><span data-stu-id="ceb8b-704">KPI</span></span></td>
      <td><span data-ttu-id="ceb8b-705">Ключевой показатель эффективности</span><span class="sxs-lookup"><span data-stu-id="ceb8b-705">KPI</span></span></td>
      <td><span data-ttu-id="ceb8b-706">
        <font size=2> Протокол: analysis-services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-706">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="ceb8b-707">Аутентификация: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-707">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="ceb8b-708">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-708">Address:</span></span> <br><span data-ttu-id="ceb8b-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="ceb8b-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="ceb8b-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="ceb8b-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="ceb8b-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-714">Многомерная модель служб SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-714">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="ceb8b-715">Measure</span><span class="sxs-lookup"><span data-stu-id="ceb8b-715">Measure</span></span></td>
      <td><span data-ttu-id="ceb8b-716">Measure</span><span class="sxs-lookup"><span data-stu-id="ceb8b-716">Measure</span></span></td>
      <td><span data-ttu-id="ceb8b-717">
        <font size=2> Протокол: analysis-services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-717">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="ceb8b-718">Аутентификация: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-718">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="ceb8b-719">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-719">Address:</span></span> <br><span data-ttu-id="ceb8b-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="ceb8b-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="ceb8b-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="ceb8b-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="ceb8b-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-725">Многомерная модель служб SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-725">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="ceb8b-726">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-726">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-727">Измерение</span><span class="sxs-lookup"><span data-stu-id="ceb8b-727">Dimension</span></span></td>
      <td><span data-ttu-id="ceb8b-728">
        <font size=2> Протокол: analysis-services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-728">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="ceb8b-729">Аутентификация: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-729">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="ceb8b-730">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-730">Address:</span></span> <br><span data-ttu-id="ceb8b-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="ceb8b-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="ceb8b-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="ceb8b-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="ceb8b-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-736">Таблица SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-736">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="ceb8b-737">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-737">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-738">Модель</span><span class="sxs-lookup"><span data-stu-id="ceb8b-738">Model</span></span></td>
      <td><span data-ttu-id="ceb8b-739">
        <font size=2> Протокол: analysis-services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-739">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="ceb8b-740">Аутентификация: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-740">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="ceb8b-741">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-741">Address:</span></span> <br><span data-ttu-id="ceb8b-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-745">Таблица SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-745">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="ceb8b-746">Ключевой показатель эффективности</span><span class="sxs-lookup"><span data-stu-id="ceb8b-746">KPI</span></span></td>
      <td><span data-ttu-id="ceb8b-747">Ключевой показатель эффективности</span><span class="sxs-lookup"><span data-stu-id="ceb8b-747">KPI</span></span></td>
      <td><span data-ttu-id="ceb8b-748">
        <font size=2> Протокол: analysis-services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-748">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="ceb8b-749">Аутентификация: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-749">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="ceb8b-750">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-750">Address:</span></span> <br><span data-ttu-id="ceb8b-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="ceb8b-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="ceb8b-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="ceb8b-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="ceb8b-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-756">Таблица SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-756">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="ceb8b-757">Measure</span><span class="sxs-lookup"><span data-stu-id="ceb8b-757">Measure</span></span></td>
      <td><span data-ttu-id="ceb8b-758">Measure</span><span class="sxs-lookup"><span data-stu-id="ceb8b-758">Measure</span></span></td>
      <td><span data-ttu-id="ceb8b-759">
        <font size=2> Протокол: analysis-services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-759">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="ceb8b-760">Аутентификация: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-760">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="ceb8b-761">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-761">Address:</span></span> <br><span data-ttu-id="ceb8b-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="ceb8b-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="ceb8b-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="ceb8b-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="ceb8b-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-767">Таблица SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-767">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="ceb8b-768">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-768">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-769">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-769">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-770">
        <font size=2> Протокол: analysis-services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-770">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="ceb8b-771">Аутентификация: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-771">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="ceb8b-772">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-772">Address:</span></span> <br><span data-ttu-id="ceb8b-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="ceb8b-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="ceb8b-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="ceb8b-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="ceb8b-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-778">Службы отчетов SQL Server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-778">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="ceb8b-779">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-779">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-780">сервер;</span><span class="sxs-lookup"><span data-stu-id="ceb8b-780">Server</span></span></td>
      <td><span data-ttu-id="ceb8b-781">
        <font size=2> Протокол: reporting-services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-781">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="ceb8b-782">Аутентификация: {windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-782">Authentication: {windows}</span></span> <br><span data-ttu-id="ceb8b-783">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-783">Address:</span></span> <br><span data-ttu-id="ceb8b-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-786">Службы отчетов SQL Server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-786">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="ceb8b-787">Отчет</span><span class="sxs-lookup"><span data-stu-id="ceb8b-787">Report</span></span></td>
      <td><span data-ttu-id="ceb8b-788">Отчет</span><span class="sxs-lookup"><span data-stu-id="ceb8b-788">Report</span></span></td>
      <td><span data-ttu-id="ceb8b-789">
        <font size=2> Протокол: reporting-services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-789">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="ceb8b-790">Аутентификация: {windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-790">Authentication: {windows}</span></span> <br><span data-ttu-id="ceb8b-791">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-791">Address:</span></span> <br><span data-ttu-id="ceb8b-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span><span class="sxs-lookup"><span data-stu-id="ceb8b-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span></span> <br><span data-ttu-id="ceb8b-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-795">Teradata</span><span class="sxs-lookup"><span data-stu-id="ceb8b-795">Teradata</span></span></td>
      <td><span data-ttu-id="ceb8b-796">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-796">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-797">База данных</span><span class="sxs-lookup"><span data-stu-id="ceb8b-797">Database</span></span></td>
      <td><span data-ttu-id="ceb8b-798">
        <font size=2> Протокол: teradata</span><span class="sxs-lookup"><span data-stu-id="ceb8b-798">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="ceb8b-799">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-799">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ceb8b-800">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-800">Address:</span></span> <br><span data-ttu-id="ceb8b-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-803">Teradata</span><span class="sxs-lookup"><span data-stu-id="ceb8b-803">Teradata</span></span></td>
      <td><span data-ttu-id="ceb8b-804">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-804">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-805">Таблица, представление</span><span class="sxs-lookup"><span data-stu-id="ceb8b-805">Table, view</span></span></td>
      <td><span data-ttu-id="ceb8b-806">
        <font size=2> Протокол: teradata</span><span class="sxs-lookup"><span data-stu-id="ceb8b-806">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="ceb8b-807">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-807">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="ceb8b-808">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-808">Address:</span></span> <br><span data-ttu-id="ceb8b-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-812">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-812">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="ceb8b-813">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-813">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-814">Модель</span><span class="sxs-lookup"><span data-stu-id="ceb8b-814">Model</span></span></td>
      <td><span data-ttu-id="ceb8b-815">
        <font size="2"> Протокол: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="ceb8b-815">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="ceb8b-816">Аутентификация: {windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-816">Authentication: {windows}</span></span> <br><span data-ttu-id="ceb8b-817">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-817">Address:</span></span> <br><span data-ttu-id="ceb8b-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="ceb8b-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="ceb8b-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="ceb8b-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="ceb8b-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-821">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="ceb8b-821">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="ceb8b-822">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-822">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-823">Сущность</span><span class="sxs-lookup"><span data-stu-id="ceb8b-823">Entity</span></span></td>
      <td><span data-ttu-id="ceb8b-824">
        <font size="2"> Протокол: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="ceb8b-824">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="ceb8b-825">Аутентификация: {windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-825">Authentication: {windows}</span></span> <br><span data-ttu-id="ceb8b-826">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-826">Address:</span></span> <br><span data-ttu-id="ceb8b-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="ceb8b-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="ceb8b-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="ceb8b-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="ceb8b-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span><span class="sxs-lookup"><span data-stu-id="ceb8b-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span></span> <br><span data-ttu-id="ceb8b-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-831">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ceb8b-831">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="ceb8b-832">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-832">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-833">База данных</span><span class="sxs-lookup"><span data-stu-id="ceb8b-833">Database</span></span></td>
      <td><span data-ttu-id="ceb8b-834">
        <font size=2> Протокол: document-db</span><span class="sxs-lookup"><span data-stu-id="ceb8b-834">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="ceb8b-835">Аутентификация: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-835">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="ceb8b-836">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-836">Address:</span></span> <br><span data-ttu-id="ceb8b-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="ceb8b-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="ceb8b-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-839">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ceb8b-839">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="ceb8b-840">Коллекция</span><span class="sxs-lookup"><span data-stu-id="ceb8b-840">Collection</span></span></td>
      <td><span data-ttu-id="ceb8b-841">Коллекция</span><span class="sxs-lookup"><span data-stu-id="ceb8b-841">Collection</span></span></td>
      <td><span data-ttu-id="ceb8b-842">
        <font size=2> Протокол: document-db</span><span class="sxs-lookup"><span data-stu-id="ceb8b-842">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="ceb8b-843">Аутентификация: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-843">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="ceb8b-844">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-844">Address:</span></span> <br><span data-ttu-id="ceb8b-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="ceb8b-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="ceb8b-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; collection </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; collection </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-848">Универсальные данные ODBC</span><span class="sxs-lookup"><span data-stu-id="ceb8b-848">Generic ODBC</span></span></td>
      <td><span data-ttu-id="ceb8b-849">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-849">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-850">База данных</span><span class="sxs-lookup"><span data-stu-id="ceb8b-850">Database</span></span></td>
      <td><span data-ttu-id="ceb8b-851">
        <font size=2> Протокол: odbc</span><span class="sxs-lookup"><span data-stu-id="ceb8b-851">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="ceb8b-852">Аутентификация: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-852">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="ceb8b-853">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-853">Address:</span></span> <br><span data-ttu-id="ceb8b-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span><span class="sxs-lookup"><span data-stu-id="ceb8b-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="ceb8b-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-856">Универсальные данные ODBC</span><span class="sxs-lookup"><span data-stu-id="ceb8b-856">Generic ODBC</span></span></td>
      <td><span data-ttu-id="ceb8b-857">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-857">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-858">Таблица, представление</span><span class="sxs-lookup"><span data-stu-id="ceb8b-858">Table, View</span></span></td>
      <td><span data-ttu-id="ceb8b-859">
        <font size=2> Протокол: odbc</span><span class="sxs-lookup"><span data-stu-id="ceb8b-859">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="ceb8b-860">Аутентификация: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-860">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="ceb8b-861">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-861">Address:</span></span> <br><span data-ttu-id="ceb8b-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span><span class="sxs-lookup"><span data-stu-id="ceb8b-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="ceb8b-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="ceb8b-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="ceb8b-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-866">Sybase</span><span class="sxs-lookup"><span data-stu-id="ceb8b-866">Sybase</span></span></td>
      <td><span data-ttu-id="ceb8b-867">Контейнер</span><span class="sxs-lookup"><span data-stu-id="ceb8b-867">Container</span></span></td>
      <td><span data-ttu-id="ceb8b-868">База данных</span><span class="sxs-lookup"><span data-stu-id="ceb8b-868">Database</span></span></td>
      <td><span data-ttu-id="ceb8b-869">
        <font size=2> Протокол: sybase</span><span class="sxs-lookup"><span data-stu-id="ceb8b-869">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="ceb8b-870">Проверка подлинности: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-870">authentication: {basic, windows}</span></span> <br><span data-ttu-id="ceb8b-871">адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-871">address:</span></span> <br><span data-ttu-id="ceb8b-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-874">Sybase</span><span class="sxs-lookup"><span data-stu-id="ceb8b-874">Sybase</span></span></td>
      <td><span data-ttu-id="ceb8b-875">Таблица</span><span class="sxs-lookup"><span data-stu-id="ceb8b-875">Table</span></span></td>
      <td><span data-ttu-id="ceb8b-876">Таблица, представление</span><span class="sxs-lookup"><span data-stu-id="ceb8b-876">Table, View</span></span></td>
      <td><span data-ttu-id="ceb8b-877">
        <font size=2> Протокол: sybase</span><span class="sxs-lookup"><span data-stu-id="ceb8b-877">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="ceb8b-878">Проверка подлинности: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="ceb8b-878">authentication: {basic, windows}</span></span> <br><span data-ttu-id="ceb8b-879">адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-879">address:</span></span> <br><span data-ttu-id="ceb8b-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="ceb8b-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="ceb8b-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="ceb8b-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="ceb8b-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="ceb8b-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="ceb8b-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="ceb8b-884">Другой (нет для hello выше)</span><span class="sxs-lookup"><span data-stu-id="ceb8b-884">Other (none of hello above)</span></span></td>
      <td>\*</td>
      <td>\*</td>
      <td><span data-ttu-id="ceb8b-885">
        <font size=2> Протокол: generic-asset</span><span class="sxs-lookup"><span data-stu-id="ceb8b-885">
        <font size=2> Protocol: generic-asset</span></span> <br><span data-ttu-id="ceb8b-886">Адрес:</span><span class="sxs-lookup"><span data-stu-id="ceb8b-886">Address:</span></span> <br><span data-ttu-id="ceb8b-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span><span class="sxs-lookup"><span data-stu-id="ceb8b-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span></span></td>
    </tr>
</table>
