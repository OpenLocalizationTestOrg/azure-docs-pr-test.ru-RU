---
title: "Источники данных, поддерживаемые в каталоге данных Azure | Документация Майкрософт"
description: "В этой статье перечислены спецификации источников данных, поддерживаемых в настоящее время."
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
ms.openlocfilehash: d6867c73bc6ea3c238cceef8a68466d451f3365c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="supported-data-sources-in-azure-data-catalog"></a><span data-ttu-id="78ee1-103">Источники данных, поддерживаемые в каталоге данных Azure</span><span class="sxs-lookup"><span data-stu-id="78ee1-103">Supported data sources in Azure Data Catalog</span></span>

<span data-ttu-id="78ee1-104">Вы можете публиковать метаданные с помощью общедоступного API или средства быстрой регистрации, или вручную, указав данные непосредственно на веб-портале каталога данных Azure.</span><span class="sxs-lookup"><span data-stu-id="78ee1-104">You can publish metadata by using a public API or a click-once registration tool, or by manually entering information directly to the Azure Data Catalog web portal.</span></span> <span data-ttu-id="78ee1-105">В следующей таблице перечислены все источники данных, поддерживаемые каталогом в настоящее время, и возможности публикации для каждого из них.</span><span class="sxs-lookup"><span data-stu-id="78ee1-105">The following table summarizes all data sources that are supported by the catalog today, and the publishing capabilities for each.</span></span> <span data-ttu-id="78ee1-106">Здесь же перечислены внешние средства работы с данными, которые каждый источник данных может запускать из портала.</span><span class="sxs-lookup"><span data-stu-id="78ee1-106">Also listed are the external data tools that each data source can launch from our portal "open-in" experience.</span></span> <span data-ttu-id="78ee1-107">Во второй таблице содержатся технические характеристики свойств подключения каждого источника данных.</span><span class="sxs-lookup"><span data-stu-id="78ee1-107">The second table contains a more technical specification of each data-source connection property.</span></span>


## <a name="list-of-supported-data-sources"></a><span data-ttu-id="78ee1-108">Список поддерживаемых источников данных</span><span class="sxs-lookup"><span data-stu-id="78ee1-108">List of supported data sources</span></span>

<table>
    <tr>
       <td><span data-ttu-id="78ee1-109"><b>Объект источника данных</b></span><span class="sxs-lookup"><span data-stu-id="78ee1-109"><b>Data source object</b></span></span></td>
       <td><span data-ttu-id="78ee1-110"><b>API</b></span><span class="sxs-lookup"><span data-stu-id="78ee1-110"><b>API</b></span></span></td>
       <td><span data-ttu-id="78ee1-111"><b>Ручной ввод</b></span><span class="sxs-lookup"><span data-stu-id="78ee1-111"><b>Manual entry</b></span></span></td>
       <td><span data-ttu-id="78ee1-112"><b>Средство регистрации</b></span><span class="sxs-lookup"><span data-stu-id="78ee1-112"><b>Registration tool</b></span></span></td>
       <td><span data-ttu-id="78ee1-113"><b>Средства Open-In</b></span><span class="sxs-lookup"><span data-stu-id="78ee1-113"><b>Open-in tools</b></span></span></td>
       <td><span data-ttu-id="78ee1-114"><b>Примечания</b></span><span class="sxs-lookup"><span data-stu-id="78ee1-114"><b>Notes</b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-115">Каталог Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="78ee1-115">Azure Data Lake Store directory</span></span></td>
      <td><span data-ttu-id="78ee1-116">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-116">✓</span></span></td>
      <td><span data-ttu-id="78ee1-117">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-117">✓</span></span></td>
      <td><span data-ttu-id="78ee1-118">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-118">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-119">Файл Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="78ee1-119">Azure Data Lake Store file</span></span></td>
      <td><span data-ttu-id="78ee1-120">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-120">✓</span></span></td>
      <td><span data-ttu-id="78ee1-121">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-121">✓</span></span></td>
      <td><span data-ttu-id="78ee1-122">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-122">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-123">Хранилище больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="78ee1-123">Azure Blob storage</span></span></td>
      <td><span data-ttu-id="78ee1-124">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-124">✓</span></span></td>
      <td><span data-ttu-id="78ee1-125">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-125">✓</span></span></td>
      <td><span data-ttu-id="78ee1-126">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-126">✓</span></span></td>
      <td><span data-ttu-id="78ee1-127"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-127"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-128">Каталог службы хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="78ee1-128">Azure Storage directory</span></span></td>
      <td><span data-ttu-id="78ee1-129">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-129">✓</span></span></td>
      <td><span data-ttu-id="78ee1-130">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-130">✓</span></span></td>
      <td><span data-ttu-id="78ee1-131">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-131">✓</span></span></td>
      <td><span data-ttu-id="78ee1-132"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-132"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-133">Таблица служба хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="78ee1-133">Azure Storage table</span></span></td>
      <td><span data-ttu-id="78ee1-134">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-134">✓</span></span></td>
      <td><span data-ttu-id="78ee1-135">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-135">✓</span></span></td>
      <td><span data-ttu-id="78ee1-136">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-136">✓</span></span></td>
      <td>
        <font size="2"></font>
      </td>
      <td>
        <font size="2"></font>
      </td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-137">Каталог HDFS</span><span class="sxs-lookup"><span data-stu-id="78ee1-137">HDFS directory</span></span></td>
      <td><span data-ttu-id="78ee1-138">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-138">✓</span></span></td>
      <td><span data-ttu-id="78ee1-139">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-139">✓</span></span></td>
      <td><span data-ttu-id="78ee1-140">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-140">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-141">Файл HDFS</span><span class="sxs-lookup"><span data-stu-id="78ee1-141">HDFS file</span></span></td>
      <td><span data-ttu-id="78ee1-142">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-142">✓</span></span></td>
      <td><span data-ttu-id="78ee1-143">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-143">✓</span></span></td>
      <td><span data-ttu-id="78ee1-144">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-144">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-145">Таблица Hive</span><span class="sxs-lookup"><span data-stu-id="78ee1-145">Hive table</span></span></td>
      <td><span data-ttu-id="78ee1-146">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-146">✓</span></span></td>
      <td><span data-ttu-id="78ee1-147">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-147">✓</span></span></td>
      <td><span data-ttu-id="78ee1-148">✓</span><span class="sxs-lookup"><span data-stu-id="78ee1-148">✓</span></span></td>
      <td><span data-ttu-id="78ee1-149"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-149"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-150">Представление Hive</span><span class="sxs-lookup"><span data-stu-id="78ee1-150">Hive view</span></span></td>
      <td><span data-ttu-id="78ee1-151">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-151">✓</span></span></td>
      <td><span data-ttu-id="78ee1-152">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-152">✓</span></span></td>
      <td><span data-ttu-id="78ee1-153">✓</span><span class="sxs-lookup"><span data-stu-id="78ee1-153">✓</span></span></td>
      <td><span data-ttu-id="78ee1-154"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-154"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-155">Таблица MySQL</span><span class="sxs-lookup"><span data-stu-id="78ee1-155">MySQL table</span></span></td>
      <td><span data-ttu-id="78ee1-156">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-156">✓</span></span></td>
      <td><span data-ttu-id="78ee1-157">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-157">✓</span></span></td>
      <td><span data-ttu-id="78ee1-158">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-158">✓</span></span></td>
      <td><span data-ttu-id="78ee1-159"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-159"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-160">Представление MySQL</span><span class="sxs-lookup"><span data-stu-id="78ee1-160">MySQL view</span></span></td>
      <td><span data-ttu-id="78ee1-161">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-161">✓</span></span></td>
      <td><span data-ttu-id="78ee1-162">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-162">✓</span></span></td>
      <td><span data-ttu-id="78ee1-163">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-163">✓</span></span></td>
      <td><span data-ttu-id="78ee1-164"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-164"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-165">Таблица базы данных Oracle</span><span class="sxs-lookup"><span data-stu-id="78ee1-165">Oracle Database table</span></span></td>
      <td><span data-ttu-id="78ee1-166">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-166">✓</span></span></td>
      <td><span data-ttu-id="78ee1-167">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-167">✓</span></span></td>
      <td><span data-ttu-id="78ee1-168">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-168">✓</span></span></td>
      <td><span data-ttu-id="78ee1-169"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-169"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-170">Представление базы данных Oracle</span><span class="sxs-lookup"><span data-stu-id="78ee1-170">Oracle Database view</span></span></td>
      <td><span data-ttu-id="78ee1-171">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-171">✓</span></span></td>
      <td><span data-ttu-id="78ee1-172">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-172">✓</span></span></td>
      <td><span data-ttu-id="78ee1-173">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-173">✓</span></span></td>
      <td><span data-ttu-id="78ee1-174"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-174"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-175">Другие (универсальный ресурс)</span><span class="sxs-lookup"><span data-stu-id="78ee1-175">Other (generic asset)</span></span></td>
      <td><span data-ttu-id="78ee1-176">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-176">✓</span></span></td>
      <td><span data-ttu-id="78ee1-177">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-177">✓</span></span></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-178">Таблица хранилища данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="78ee1-178">Azure SQL Data Warehouse table</span></span></td>
      <td><span data-ttu-id="78ee1-179">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-179">✓</span></span></td>
      <td><span data-ttu-id="78ee1-180">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-180">✓</span></span></td>
      <td><span data-ttu-id="78ee1-181">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-181">✓</span></span></td>
      <td><span data-ttu-id="78ee1-182"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-182"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-183">Представление хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="78ee1-183">SQL Data Warehouse view</span></span></td>
      <td><span data-ttu-id="78ee1-184">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-184">✓</span></span></td>
      <td><span data-ttu-id="78ee1-185">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-185">✓</span></span></td>
      <td><span data-ttu-id="78ee1-186">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-186">✓</span></span></td>
      <td><span data-ttu-id="78ee1-187"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-187"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-188">Размерность SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="78ee1-188">SQL Server Analysis Services dimension</span></span></td>
      <td><span data-ttu-id="78ee1-189">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-189">✓</span></span></td>
      <td><span data-ttu-id="78ee1-190">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-190">✓</span></span></td>
      <td><span data-ttu-id="78ee1-191">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-191">✓</span></span></td>
      <td><span data-ttu-id="78ee1-192"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-192"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-193">Ключевые показатели эффективности SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="78ee1-193">SQL Server Analysis Services KPI</span></span></td>
      <td><span data-ttu-id="78ee1-194">✓</span><span class="sxs-lookup"><span data-stu-id="78ee1-194">✓</span></span></td>
      <td><span data-ttu-id="78ee1-195">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-195">✓</span></span></td>
      <td><span data-ttu-id="78ee1-196">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-196">✓</span></span></td>
      <td><span data-ttu-id="78ee1-197"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-197"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-198">Измерение SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="78ee1-198">SQL Server Analysis Services measure</span></span></td>
      <td><span data-ttu-id="78ee1-199">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-199">✓</span></span></td>
      <td><span data-ttu-id="78ee1-200">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-200">✓</span></span></td>
      <td><span data-ttu-id="78ee1-201">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-201">✓</span></span></td>
      <td><span data-ttu-id="78ee1-202"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-202"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-203">Таблица SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="78ee1-203">SQL Server Analysis Services table</span></span></td>
      <td><span data-ttu-id="78ee1-204">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-204">✓</span></span></td>
      <td><span data-ttu-id="78ee1-205">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-205">✓</span></span></td>
      <td><span data-ttu-id="78ee1-206">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-206">✓</span></span></td>
      <td><span data-ttu-id="78ee1-207"><font size=2>Excel, Power BI</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-207"><font size=2>Excel, Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-208">Отчет для служб SQL Server Reporting Services</span><span class="sxs-lookup"><span data-stu-id="78ee1-208">SQL Server Reporting Services report</span></span></td>
      <td><span data-ttu-id="78ee1-209">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-209">✓</span></span></td>
      <td><span data-ttu-id="78ee1-210">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-210">✓</span></span></td>
      <td><span data-ttu-id="78ee1-211">✓</span><span class="sxs-lookup"><span data-stu-id="78ee1-211">✓</span></span></td>
      <td><span data-ttu-id="78ee1-212"><font size=2>"Обзор"</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-212"><font size=2>Browser</font></span></span></td>
      <td><span data-ttu-id="78ee1-213"><font size=2>Только серверы в основном режиме. Режим SharePoint не поддерживается.</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-213"><font size=2>Native mode servers only. SharePoint mode is not supported.</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-214">Таблица SQL Server</span><span class="sxs-lookup"><span data-stu-id="78ee1-214">SQL Server table</span></span></td>
      <td><span data-ttu-id="78ee1-215">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-215">✓</span></span></td>
      <td><span data-ttu-id="78ee1-216">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-216">✓</span></span></td>
      <td><span data-ttu-id="78ee1-217">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-217">✓</span></span></td>
      <td><span data-ttu-id="78ee1-218"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-218"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-219">Представление SQL Server</span><span class="sxs-lookup"><span data-stu-id="78ee1-219">SQL Server view</span></span></td>
      <td><span data-ttu-id="78ee1-220">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-220">✓</span></span></td>
      <td><span data-ttu-id="78ee1-221">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-221">✓</span></span></td>
      <td><span data-ttu-id="78ee1-222">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-222">✓</span></span></td>
      <td><span data-ttu-id="78ee1-223"><font size=2>Excel, Power BI, SQL Server Data Tools</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-223"><font size=2>Excel, Power BI, SQL Server data tools</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-224">Таблица Teradata</span><span class="sxs-lookup"><span data-stu-id="78ee1-224">Teradata table</span></span></td>
      <td><span data-ttu-id="78ee1-225">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-225">✓</span></span></td>
      <td><span data-ttu-id="78ee1-226">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-226">✓</span></span></td>
      <td><span data-ttu-id="78ee1-227">✓</span><span class="sxs-lookup"><span data-stu-id="78ee1-227">✓</span></span></td>
      <td><span data-ttu-id="78ee1-228"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-228"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-229">Представление Teradata</span><span class="sxs-lookup"><span data-stu-id="78ee1-229">Teradata view</span></span></td>
      <td><span data-ttu-id="78ee1-230">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-230">✓</span></span></td>
      <td><span data-ttu-id="78ee1-231">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-231">✓</span></span></td>
      <td><span data-ttu-id="78ee1-232">✓</span><span class="sxs-lookup"><span data-stu-id="78ee1-232">✓</span></span></td>
      <td><span data-ttu-id="78ee1-233"><font size=2>Excel</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-233"><font size=2>Excel</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-234">Представление SAP Hana</span><span class="sxs-lookup"><span data-stu-id="78ee1-234">SAP HANA view</span></span></td>
      <td><span data-ttu-id="78ee1-235">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-235">✓</span></span></td>
      <td><span data-ttu-id="78ee1-236">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-236">✓</span></span></td>
      <td><span data-ttu-id="78ee1-237">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-237">✓</span></span></td>
      <td><span data-ttu-id="78ee1-238"><font size=2>Power BI</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-238"><font size=2>Power BI</font></span></span></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-239">Таблица DB2</span><span class="sxs-lookup"><span data-stu-id="78ee1-239">DB2 table</span></span></td>
      <td><span data-ttu-id="78ee1-240">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-240">✓</span></span></td>
      <td><span data-ttu-id="78ee1-241">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-241">✓</span></span></td>
      <td><span data-ttu-id="78ee1-242">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-242">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-243">Представление DB2</span><span class="sxs-lookup"><span data-stu-id="78ee1-243">DB2 view</span></span></td>
      <td><span data-ttu-id="78ee1-244">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-244">✓</span></span></td>
      <td><span data-ttu-id="78ee1-245">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-245">✓</span></span></td>
      <td><span data-ttu-id="78ee1-246">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-246">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-247">Файл файловой системы</span><span class="sxs-lookup"><span data-stu-id="78ee1-247">File system file</span></span></td>
      <td><span data-ttu-id="78ee1-248">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-248">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-249">Каталог FTP</span><span class="sxs-lookup"><span data-stu-id="78ee1-249">FTP directory</span></span></td>
      <td><span data-ttu-id="78ee1-250">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-250">✓</span></span></td>
      <td><span data-ttu-id="78ee1-251">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-251">✓</span></span></td>
      <td><span data-ttu-id="78ee1-252">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-252">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-253">Файл FTP</span><span class="sxs-lookup"><span data-stu-id="78ee1-253">FTP file</span></span></td>
      <td><span data-ttu-id="78ee1-254">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-254">✓</span></span></td>
      <td><span data-ttu-id="78ee1-255">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-255">✓</span></span></td>
      <td><span data-ttu-id="78ee1-256">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-256">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-257">Отчет HTTP</span><span class="sxs-lookup"><span data-stu-id="78ee1-257">HTTP report</span></span></td>
      <td><span data-ttu-id="78ee1-258">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-258">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-259">Конечная точка HTTP</span><span class="sxs-lookup"><span data-stu-id="78ee1-259">HTTP endpoint</span></span></td>
      <td><span data-ttu-id="78ee1-260">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-260">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-261">Файл HTTP</span><span class="sxs-lookup"><span data-stu-id="78ee1-261">HTTP file</span></span></td>
      <td><span data-ttu-id="78ee1-262">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-262">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-263">Набор сущностей OData</span><span class="sxs-lookup"><span data-stu-id="78ee1-263">OData entity set</span></span></td>
      <td><span data-ttu-id="78ee1-264">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-264">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-265">Функция OData</span><span class="sxs-lookup"><span data-stu-id="78ee1-265">OData function</span></span></td>
      <td><span data-ttu-id="78ee1-266">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-266">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-267">Таблица PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="78ee1-267">PostgreSQL table</span></span></td>
      <td><span data-ttu-id="78ee1-268">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-268">✓</span></span></td>
      <td><span data-ttu-id="78ee1-269">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-269">✓</span></span></td>
      <td><span data-ttu-id="78ee1-270">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-270">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-271">Представление PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="78ee1-271">PostgreSQL view</span></span></td>
      <td><span data-ttu-id="78ee1-272">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-272">✓</span></span></td>
      <td><span data-ttu-id="78ee1-273">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-273">✓</span></span></td>
      <td><span data-ttu-id="78ee1-274">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-274">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-275">Представление SAP Hana</span><span class="sxs-lookup"><span data-stu-id="78ee1-275">SAP HANA view</span></span></td>
      <td><span data-ttu-id="78ee1-276">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-276">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td> <span data-ttu-id="78ee1-277">Объект SalesForce</span><span class="sxs-lookup"><span data-stu-id="78ee1-277">Salesforce object</span></span></td>
      <td><span data-ttu-id="78ee1-278">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-278">✓</span></span></td>
      <td><span data-ttu-id="78ee1-279">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-279">✓</span></span></td>
      <td><span data-ttu-id="78ee1-280">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-280">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-281">Список SharePoint</span><span class="sxs-lookup"><span data-stu-id="78ee1-281">SharePoint list</span></span> </td>
      <td><span data-ttu-id="78ee1-282">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-282">✓</span></span></td>
      <td></td>
      <td></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-283">Коллекция Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="78ee1-283">Azure Cosmos DB collection</span></span></td>
      <td><span data-ttu-id="78ee1-284">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-284">✓</span></span></td>
      <td><span data-ttu-id="78ee1-285">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-285">✓</span></span></td>
      <td><span data-ttu-id="78ee1-286">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-286">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-287">Универсальная таблица ODBC</span><span class="sxs-lookup"><span data-stu-id="78ee1-287">Generic ODBC table</span></span></td>
      <td><span data-ttu-id="78ee1-288">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-288">✓</span></span></td>
      <td><span data-ttu-id="78ee1-289">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-289">✓</span></span></td>
      <td><span data-ttu-id="78ee1-290">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-290">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-291">Универсальное представление ODBC</span><span class="sxs-lookup"><span data-stu-id="78ee1-291">Generic ODBC view</span></span></td>
      <td><span data-ttu-id="78ee1-292">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-292">✓</span></span></td>
      <td><span data-ttu-id="78ee1-293">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-293">✓</span></span></td>
      <td><span data-ttu-id="78ee1-294">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-294">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-295">Таблица Cassandra</span><span class="sxs-lookup"><span data-stu-id="78ee1-295">Cassandra table</span></span></td>
      <td><span data-ttu-id="78ee1-296">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-296">✓</span></span></td>
      <td><span data-ttu-id="78ee1-297">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-297">✓</span></span></td>
      <td><span data-ttu-id="78ee1-298">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-298">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="78ee1-299"><font size=2>Публикация в качестве ресурса ODBC</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-299"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-300">Представление Cassandra</span><span class="sxs-lookup"><span data-stu-id="78ee1-300">Cassandra view</span></span></td>
      <td><span data-ttu-id="78ee1-301">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-301">✓</span></span></td>
      <td><span data-ttu-id="78ee1-302">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-302">✓</span></span></td>
      <td><span data-ttu-id="78ee1-303">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-303">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="78ee1-304"><font size=2>Публикация в качестве ресурса ODBC</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-304"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-305">Таблица Sybase</span><span class="sxs-lookup"><span data-stu-id="78ee1-305">Sybase table</span></span></td>
      <td><span data-ttu-id="78ee1-306">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-306">✓</span></span></td>
      <td><span data-ttu-id="78ee1-307">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-307">✓</span></span></td>
      <td><span data-ttu-id="78ee1-308">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-308">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-309">Представление Sybase</span><span class="sxs-lookup"><span data-stu-id="78ee1-309">Sybase view</span></span></td>
      <td><span data-ttu-id="78ee1-310">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-310">✓</span></span></td>
      <td><span data-ttu-id="78ee1-311">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-311">✓</span></span></td>
      <td><span data-ttu-id="78ee1-312">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-312">✓</span></span></td>
      <td><font size=2></font></td>
      <td><font size=2></font></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-313">Таблица MongoDB</span><span class="sxs-lookup"><span data-stu-id="78ee1-313">MongoDB table</span></span></td>
      <td><span data-ttu-id="78ee1-314">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-314">✓</span></span></td>
      <td><span data-ttu-id="78ee1-315">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-315">✓</span></span></td>
      <td><span data-ttu-id="78ee1-316">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-316">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="78ee1-317"><font size=2>Публикация в качестве ресурса ODBC</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-317"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-318">Представление MongoDB</span><span class="sxs-lookup"><span data-stu-id="78ee1-318">MongoDB view</span></span></td>
      <td><span data-ttu-id="78ee1-319">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-319">✓</span></span></td>
      <td><span data-ttu-id="78ee1-320">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-320">✓</span></span></td>
      <td><span data-ttu-id="78ee1-321">✓ </span><span class="sxs-lookup"><span data-stu-id="78ee1-321">✓</span></span></td>
      <td><font size=2></font></td>
      <td><span data-ttu-id="78ee1-322"><font size=2>Публикация в качестве ресурса ODBC</font></span><span class="sxs-lookup"><span data-stu-id="78ee1-322"><font size=2>Publish as a generic ODBC asset</font></span></span></td>
    </tr>
</table>

<span data-ttu-id="78ee1-323">Если вам требуется поддержка дополнительных источников, отправьте запрос функции на [форум по каталогу данных Azure](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="78ee1-323">If you need support for additional sources, submit a feature request to the [Azure Data Catalog forum](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).</span></span>


## <a name="data-source-reference-specification"></a><span data-ttu-id="78ee1-324">Спецификация ссылки на источник данных</span><span class="sxs-lookup"><span data-stu-id="78ee1-324">Data-source reference specification</span></span>
> [!NOTE]
> <span data-ttu-id="78ee1-325">Столбец **Структура DSL** в приведенной ниже таблице содержит только свойства подключения для контейнера свойств address, используемые каталогом данных Azure.</span><span class="sxs-lookup"><span data-stu-id="78ee1-325">The **DSL structure** column in the following table lists only the connection properties for "address" property bag that are used by Azure Data Catalog.</span></span> <span data-ttu-id="78ee1-326">Т. е. контейнер свойств address может содержать другие свойства подключения источника данных, которые хранятся в каталоге данных Azure, но не используются.</span><span class="sxs-lookup"><span data-stu-id="78ee1-326">That is, "address" property bag can contain other connection properties of the data source which Azure Data Catalog persists, but does not use.</span></span>

<table>
    <tr>
       <td><span data-ttu-id="78ee1-327"><b>Тип источника</b></span><span class="sxs-lookup"><span data-stu-id="78ee1-327"><b>Source type</b></span></span></td>
       <td><span data-ttu-id="78ee1-328"><b>Тип ресурса</b></span><span class="sxs-lookup"><span data-stu-id="78ee1-328"><b>Asset type</b></span></span></td>
       <td><span data-ttu-id="78ee1-329"><b>Типы объектов</b></span><span class="sxs-lookup"><span data-stu-id="78ee1-329"><b>Object types</b></span></span></td>
       <td><span data-ttu-id="78ee1-330"><b>Структура DSL<b></span><span class="sxs-lookup"><span data-stu-id="78ee1-330"><b>DSL structure<b></span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-331">Хранилище озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="78ee1-331">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="78ee1-332">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-332">Container</span></span></td>
      <td><span data-ttu-id="78ee1-333">Озеро данных</span><span class="sxs-lookup"><span data-stu-id="78ee1-333">Data Lake</span></span></td>
      <td><span data-ttu-id="78ee1-334">
        <font size=2> Протокол: webhdfs</span><span class="sxs-lookup"><span data-stu-id="78ee1-334">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="78ee1-335">Аутентификация: {basic, oauth}</span><span class="sxs-lookup"><span data-stu-id="78ee1-335">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="78ee1-336">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-336">Address:</span></span> <br><span data-ttu-id="78ee1-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-337">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-338">Хранилище озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="78ee1-338">Azure Data Lake Store</span></span></td>
      <td><span data-ttu-id="78ee1-339">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-339">Table</span></span></td>
      <td><span data-ttu-id="78ee1-340">Каталог, файл</span><span class="sxs-lookup"><span data-stu-id="78ee1-340">Directory, file</span></span></td>
      <td><span data-ttu-id="78ee1-341">
        <font size=2> Протокол: webhdfs</span><span class="sxs-lookup"><span data-stu-id="78ee1-341">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="78ee1-342">Аутентификация: {basic, oauth}</span><span class="sxs-lookup"><span data-stu-id="78ee1-342">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="78ee1-343">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-343">Address:</span></span> <br><span data-ttu-id="78ee1-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-344">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-345">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="78ee1-345">Azure Storage</span></span></td>
      <td><span data-ttu-id="78ee1-346">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-346">Container</span></span></td>
      <td><span data-ttu-id="78ee1-347">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-347">Container</span></span></td>
      <td><span data-ttu-id="78ee1-348">
        <font size=2> Протокол: azure-blobs</span><span class="sxs-lookup"><span data-stu-id="78ee1-348">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="78ee1-349">Аутентификация: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="78ee1-349">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="78ee1-350">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-350">Address:</span></span> <br><span data-ttu-id="78ee1-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="78ee1-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="78ee1-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span><span class="sxs-lookup"><span data-stu-id="78ee1-352">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="78ee1-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-353">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-354">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="78ee1-354">Azure Storage</span></span></td>
      <td><span data-ttu-id="78ee1-355">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-355">Table</span></span></td>
      <td><span data-ttu-id="78ee1-356">Большой двоичный объект, каталог</span><span class="sxs-lookup"><span data-stu-id="78ee1-356">Blob, directory</span></span></td>
      <td><span data-ttu-id="78ee1-357">
        <font size=2> Протокол: azure-blobs</span><span class="sxs-lookup"><span data-stu-id="78ee1-357">
        <font size=2> Protocol: azure-blobs</span></span> <br><span data-ttu-id="78ee1-358">Аутентификация: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="78ee1-358">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="78ee1-359">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-359">Address:</span></span> <br><span data-ttu-id="78ee1-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="78ee1-360">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="78ee1-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span><span class="sxs-lookup"><span data-stu-id="78ee1-361">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="78ee1-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container</span><span class="sxs-lookup"><span data-stu-id="78ee1-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; container</span></span> <br><span data-ttu-id="78ee1-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-364">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="78ee1-364">Azure Storage</span></span></td>
      <td><span data-ttu-id="78ee1-365">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-365">Container</span></span></td>
      <td><span data-ttu-id="78ee1-366">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-366">Container</span></span></td>
      <td><span data-ttu-id="78ee1-367">
        <font size=2> Протокол: azure-tables</span><span class="sxs-lookup"><span data-stu-id="78ee1-367">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="78ee1-368">Аутентификация: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="78ee1-368">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="78ee1-369">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-369">Address:</span></span> <br><span data-ttu-id="78ee1-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="78ee1-370">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="78ee1-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-371">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-372">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="78ee1-372">Azure Storage</span></span></td>
      <td><span data-ttu-id="78ee1-373">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-373">Table</span></span></td>
      <td><span data-ttu-id="78ee1-374">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-374">Table</span></span></td>
      <td><span data-ttu-id="78ee1-375">
        <font size=2> Протокол: azure-tables</span><span class="sxs-lookup"><span data-stu-id="78ee1-375">
        <font size=2> Protocol: azure-tables</span></span> <br><span data-ttu-id="78ee1-376">Аутентификация: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="78ee1-376">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="78ee1-377">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-377">Address:</span></span> <br><span data-ttu-id="78ee1-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span><span class="sxs-lookup"><span data-stu-id="78ee1-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; domain</span></span> <br><span data-ttu-id="78ee1-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span><span class="sxs-lookup"><span data-stu-id="78ee1-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; account</span></span> <br><span data-ttu-id="78ee1-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-380">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; name </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-381">Cosmos</span><span class="sxs-lookup"><span data-stu-id="78ee1-381">Cosmos</span></span></td>
      <td><span data-ttu-id="78ee1-382">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-382">Container</span></span></td>
      <td><span data-ttu-id="78ee1-383">Виртуальный кластер</span><span class="sxs-lookup"><span data-stu-id="78ee1-383">Virtual cluster</span></span></td>
      <td><span data-ttu-id="78ee1-384">
        <font size=2> Протокол: cosmos</span><span class="sxs-lookup"><span data-stu-id="78ee1-384">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="78ee1-385">Аутентификация: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-385">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="78ee1-386">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-386">Address:</span></span> <br><span data-ttu-id="78ee1-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-387">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-388">Cosmos</span><span class="sxs-lookup"><span data-stu-id="78ee1-388">Cosmos</span></span></td>
      <td><span data-ttu-id="78ee1-389">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-389">Table</span></span></td>
      <td><span data-ttu-id="78ee1-390">Поток, набор потоков, представление</span><span class="sxs-lookup"><span data-stu-id="78ee1-390">Stream, stream set, view</span></span></td>
      <td><span data-ttu-id="78ee1-391">
        <font size=2> Протокол: cosmos</span><span class="sxs-lookup"><span data-stu-id="78ee1-391">
        <font size=2> Protocol: cosmos</span></span> <br><span data-ttu-id="78ee1-392">Аутентификация: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-392">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="78ee1-393">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-393">Address:</span></span> <br><span data-ttu-id="78ee1-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-395">DataZen</span><span class="sxs-lookup"><span data-stu-id="78ee1-395">Datazen</span></span></td>
      <td><span data-ttu-id="78ee1-396">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-396">Container</span></span></td>
      <td><span data-ttu-id="78ee1-397">Сайт</span><span class="sxs-lookup"><span data-stu-id="78ee1-397">Site</span></span></td>
      <td><span data-ttu-id="78ee1-398">
        <font size=2> Протокол: http</span><span class="sxs-lookup"><span data-stu-id="78ee1-398">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="78ee1-399">Аутентификация: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="78ee1-399">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="78ee1-400">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-400">Address:</span></span> <br><span data-ttu-id="78ee1-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-401">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-402">DataZen</span><span class="sxs-lookup"><span data-stu-id="78ee1-402">Datazen</span></span></td>
      <td><span data-ttu-id="78ee1-403">Отчет</span><span class="sxs-lookup"><span data-stu-id="78ee1-403">Report</span></span></td>
      <td><span data-ttu-id="78ee1-404">Отчет, панель мониторинга</span><span class="sxs-lookup"><span data-stu-id="78ee1-404">Report, dashboard</span></span></td>
      <td><span data-ttu-id="78ee1-405">
        <font size=2> Протокол: http</span><span class="sxs-lookup"><span data-stu-id="78ee1-405">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="78ee1-406">Аутентификация: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="78ee1-406">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="78ee1-407">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-407">Address:</span></span> <br><span data-ttu-id="78ee1-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-408">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-409">DB2</span><span class="sxs-lookup"><span data-stu-id="78ee1-409">DB2</span></span></td>
      <td><span data-ttu-id="78ee1-410">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-410">Container</span></span></td>
      <td><span data-ttu-id="78ee1-411">База данных</span><span class="sxs-lookup"><span data-stu-id="78ee1-411">Database</span></span></td>
      <td><span data-ttu-id="78ee1-412">
        <font size=2> Протокол: DB2</span><span class="sxs-lookup"><span data-stu-id="78ee1-412">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="78ee1-413">Аутентификация: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-413">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="78ee1-414">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-414">Address:</span></span> <br><span data-ttu-id="78ee1-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-415">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-416">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-417">DB2</span><span class="sxs-lookup"><span data-stu-id="78ee1-417">DB2</span></span></td>
      <td><span data-ttu-id="78ee1-418">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-418">Table</span></span></td>
      <td><span data-ttu-id="78ee1-419">Таблица, представление</span><span class="sxs-lookup"><span data-stu-id="78ee1-419">Table, view</span></span></td>
      <td><span data-ttu-id="78ee1-420">
        <font size=2> Протокол: DB2</span><span class="sxs-lookup"><span data-stu-id="78ee1-420">
        <font size=2> Protocol: db2</span></span> <br><span data-ttu-id="78ee1-421">Аутентификация: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-421">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="78ee1-422">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-422">Address:</span></span> <br><span data-ttu-id="78ee1-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-423">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-424">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="78ee1-425">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="78ee1-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-426">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-427">Файловая система</span><span class="sxs-lookup"><span data-stu-id="78ee1-427">File system</span></span></td>
      <td><span data-ttu-id="78ee1-428">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-428">Table</span></span></td>
      <td><span data-ttu-id="78ee1-429">Файл</span><span class="sxs-lookup"><span data-stu-id="78ee1-429">File</span></span></td>
      <td><span data-ttu-id="78ee1-430">
        <font size=2> Протокол: файл</span><span class="sxs-lookup"><span data-stu-id="78ee1-430">
        <font size=2> Protocol: file</span></span> <br><span data-ttu-id="78ee1-431">Аутентификация: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-431">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="78ee1-432">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-432">Address:</span></span> <br><span data-ttu-id="78ee1-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-433">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-434">FTP</span><span class="sxs-lookup"><span data-stu-id="78ee1-434">FTP</span></span></td>
      <td><span data-ttu-id="78ee1-435">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-435">Table</span></span></td>
      <td><span data-ttu-id="78ee1-436">Каталог, файл</span><span class="sxs-lookup"><span data-stu-id="78ee1-436">Directory, file</span></span></td>
      <td><span data-ttu-id="78ee1-437">
        <font size=2> Протокол: ftp</span><span class="sxs-lookup"><span data-stu-id="78ee1-437">
        <font size=2> Protocol: ftp</span></span> <br><span data-ttu-id="78ee1-438">Аутентификация: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-438">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="78ee1-439">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-439">Address:</span></span> <br><span data-ttu-id="78ee1-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-440">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-441">Распределенная файловая система Hadoop</span><span class="sxs-lookup"><span data-stu-id="78ee1-441">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="78ee1-442">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-442">Container</span></span></td>
      <td><span data-ttu-id="78ee1-443">HDInsight</span><span class="sxs-lookup"><span data-stu-id="78ee1-443">Cluster</span></span></td>
      <td><span data-ttu-id="78ee1-444">
        <font size=2> Протокол: webhdfs</span><span class="sxs-lookup"><span data-stu-id="78ee1-444">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="78ee1-445">Аутентификация: {basic, oauth}</span><span class="sxs-lookup"><span data-stu-id="78ee1-445">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="78ee1-446">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-446">Address:</span></span> <br><span data-ttu-id="78ee1-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-447">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-448">Распределенная файловая система Hadoop</span><span class="sxs-lookup"><span data-stu-id="78ee1-448">Hadoop Distributed File System</span></span></td>
      <td><span data-ttu-id="78ee1-449">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-449">Table</span></span></td>
      <td><span data-ttu-id="78ee1-450">Каталог, файл</span><span class="sxs-lookup"><span data-stu-id="78ee1-450">Directory, file</span></span></td>
      <td><span data-ttu-id="78ee1-451">
        <font size=2> Протокол: webhdfs</span><span class="sxs-lookup"><span data-stu-id="78ee1-451">
        <font size=2> Protocol: webhdfs</span></span> <br><span data-ttu-id="78ee1-452">Аутентификация: {basic, oauth}</span><span class="sxs-lookup"><span data-stu-id="78ee1-452">Authentication: {basic, oauth}</span></span> <br><span data-ttu-id="78ee1-453">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-453">Address:</span></span> <br><span data-ttu-id="78ee1-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-454">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-455">Hive</span><span class="sxs-lookup"><span data-stu-id="78ee1-455">Hive</span></span></td>
      <td><span data-ttu-id="78ee1-456">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-456">Container</span></span></td>
      <td><span data-ttu-id="78ee1-457">База данных</span><span class="sxs-lookup"><span data-stu-id="78ee1-457">Database</span></span></td>
      <td><span data-ttu-id="78ee1-458">
        <font size=2> Протокол: hive</span><span class="sxs-lookup"><span data-stu-id="78ee1-458">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="78ee1-459">Аутентификация: {hdinsight, basic, username, none}</span><span class="sxs-lookup"><span data-stu-id="78ee1-459">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="78ee1-460">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-460">Address:</span></span> <br><span data-ttu-id="78ee1-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-461">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-462">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-463">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="78ee1-463">connectionProperties:</span></span> <br><span data-ttu-id="78ee1-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-464">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-465">Hive</span><span class="sxs-lookup"><span data-stu-id="78ee1-465">Hive</span></span></td>
      <td><span data-ttu-id="78ee1-466">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-466">Table</span></span></td>
      <td><span data-ttu-id="78ee1-467">Таблица, представление</span><span class="sxs-lookup"><span data-stu-id="78ee1-467">Table, view</span></span></td>
      <td><span data-ttu-id="78ee1-468">
        <font size=2> Протокол: hive</span><span class="sxs-lookup"><span data-stu-id="78ee1-468">
        <font size=2> Protocol: hive</span></span> <br><span data-ttu-id="78ee1-469">Аутентификация: {hdinsight, basic, username, none}</span><span class="sxs-lookup"><span data-stu-id="78ee1-469">Authentication: {HDInsight, basic, username, none}</span></span> <br><span data-ttu-id="78ee1-470">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-470">Address:</span></span> <br><span data-ttu-id="78ee1-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-471">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-472">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="78ee1-473">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="78ee1-474">connectionProperties:</span><span class="sxs-lookup"><span data-stu-id="78ee1-474">connectionProperties:</span></span> <br><span data-ttu-id="78ee1-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-475">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; serverProtocol: {hive2} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-476">HTTP</span><span class="sxs-lookup"><span data-stu-id="78ee1-476">HTTP</span></span></td>
      <td><span data-ttu-id="78ee1-477">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-477">Container</span></span></td>
      <td><span data-ttu-id="78ee1-478">Сайт</span><span class="sxs-lookup"><span data-stu-id="78ee1-478">Site</span></span></td>
      <td><span data-ttu-id="78ee1-479">
        <font size=2> Протокол: http</span><span class="sxs-lookup"><span data-stu-id="78ee1-479">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="78ee1-480">Аутентификация: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="78ee1-480">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="78ee1-481">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-481">Address:</span></span> <br><span data-ttu-id="78ee1-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-482">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-483">HTTP</span><span class="sxs-lookup"><span data-stu-id="78ee1-483">HTTP</span></span></td>
      <td><span data-ttu-id="78ee1-484">Отчет</span><span class="sxs-lookup"><span data-stu-id="78ee1-484">Report</span></span></td>
      <td><span data-ttu-id="78ee1-485">Отчет, панель мониторинга</span><span class="sxs-lookup"><span data-stu-id="78ee1-485">Report, dashboard</span></span></td>
      <td><span data-ttu-id="78ee1-486">
        <font size=2> Протокол: http</span><span class="sxs-lookup"><span data-stu-id="78ee1-486">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="78ee1-487">Аутентификация: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="78ee1-487">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="78ee1-488">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-488">Address:</span></span> <br><span data-ttu-id="78ee1-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-489">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-490">HTTP</span><span class="sxs-lookup"><span data-stu-id="78ee1-490">HTTP</span></span></td>
      <td><span data-ttu-id="78ee1-491">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-491">Table</span></span></td>
      <td><span data-ttu-id="78ee1-492">Конечная точка, файл</span><span class="sxs-lookup"><span data-stu-id="78ee1-492">Endpoint, file</span></span></td>
      <td><span data-ttu-id="78ee1-493">
        <font size=2> Протокол: http</span><span class="sxs-lookup"><span data-stu-id="78ee1-493">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="78ee1-494">Аутентификация: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="78ee1-494">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="78ee1-495">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-495">Address:</span></span> <br><span data-ttu-id="78ee1-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-496">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-497">MySQL</span><span class="sxs-lookup"><span data-stu-id="78ee1-497">MySQL</span></span></td>
      <td><span data-ttu-id="78ee1-498">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-498">Container</span></span></td>
      <td><span data-ttu-id="78ee1-499">База данных</span><span class="sxs-lookup"><span data-stu-id="78ee1-499">Database</span></span></td>
      <td><span data-ttu-id="78ee1-500">
        <font size=2> Протокол: mysql</span><span class="sxs-lookup"><span data-stu-id="78ee1-500">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="78ee1-501">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-501">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="78ee1-502">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-502">Address:</span></span> <br><span data-ttu-id="78ee1-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-503">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-504">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-505">MySQL</span><span class="sxs-lookup"><span data-stu-id="78ee1-505">MySQL</span></span></td>
      <td><span data-ttu-id="78ee1-506">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-506">Table</span></span></td>
      <td><span data-ttu-id="78ee1-507">Таблица, представление</span><span class="sxs-lookup"><span data-stu-id="78ee1-507">Table, view</span></span></td>
      <td><span data-ttu-id="78ee1-508">
        <font size=2> Протокол: mysql</span><span class="sxs-lookup"><span data-stu-id="78ee1-508">
        <font size=2> Protocol: mysql</span></span> <br><span data-ttu-id="78ee1-509">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-509">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="78ee1-510">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-510">Address:</span></span> <br><span data-ttu-id="78ee1-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-511">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-512">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-513">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-514">OData</span><span class="sxs-lookup"><span data-stu-id="78ee1-514">OData</span></span></td>
      <td><span data-ttu-id="78ee1-515">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-515">Container</span></span></td>
      <td><span data-ttu-id="78ee1-516">Контейнер сущностей</span><span class="sxs-lookup"><span data-stu-id="78ee1-516">Entity container</span></span></td>
      <td><span data-ttu-id="78ee1-517">
        <font size=2> Протокол: odata</span><span class="sxs-lookup"><span data-stu-id="78ee1-517">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="78ee1-518">Аутентификация: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-518">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="78ee1-519">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-519">Address:</span></span> <br><span data-ttu-id="78ee1-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-520">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-521">OData</span><span class="sxs-lookup"><span data-stu-id="78ee1-521">OData</span></span></td>
      <td><span data-ttu-id="78ee1-522">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-522">Table</span></span></td>
      <td><span data-ttu-id="78ee1-523">Набор сущностей, функция</span><span class="sxs-lookup"><span data-stu-id="78ee1-523">Entity set, function</span></span></td>
      <td><span data-ttu-id="78ee1-524">
        <font size=2> Протокол: odata</span><span class="sxs-lookup"><span data-stu-id="78ee1-524">
        <font size=2> Protocol: odata</span></span> <br><span data-ttu-id="78ee1-525">Аутентификация: {none, basic, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-525">Authentication: {none, basic, windows}</span></span> <br><span data-ttu-id="78ee1-526">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-526">Address:</span></span> <br><span data-ttu-id="78ee1-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="78ee1-527">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="78ee1-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-528">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; resource </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-529">База данных Oracle</span><span class="sxs-lookup"><span data-stu-id="78ee1-529">Oracle Database</span></span></td>
      <td><span data-ttu-id="78ee1-530">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-530">Container</span></span></td>
      <td><span data-ttu-id="78ee1-531">База данных</span><span class="sxs-lookup"><span data-stu-id="78ee1-531">Database</span></span></td>
      <td><span data-ttu-id="78ee1-532">
        <font size=2> Протокол: oracle</span><span class="sxs-lookup"><span data-stu-id="78ee1-532">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="78ee1-533">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-533">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="78ee1-534">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-534">Address:</span></span> <br><span data-ttu-id="78ee1-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-535">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-536">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-537">База данных Oracle</span><span class="sxs-lookup"><span data-stu-id="78ee1-537">Oracle Database</span></span></td>
      <td><span data-ttu-id="78ee1-538">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-538">Table</span></span></td>
      <td><span data-ttu-id="78ee1-539">Таблица, представление</span><span class="sxs-lookup"><span data-stu-id="78ee1-539">Table, view</span></span></td>
      <td><span data-ttu-id="78ee1-540">
        <font size=2> Протокол: oracle</span><span class="sxs-lookup"><span data-stu-id="78ee1-540">
        <font size=2> Protocol: oracle</span></span> <br><span data-ttu-id="78ee1-541">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-541">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="78ee1-542">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-542">Address:</span></span> <br><span data-ttu-id="78ee1-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-543">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-544">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="78ee1-545">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="78ee1-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-546">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-547">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="78ee1-547">PostgreSQL</span></span></td>
      <td><span data-ttu-id="78ee1-548">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-548">Container</span></span></td>
      <td><span data-ttu-id="78ee1-549">База данных</span><span class="sxs-lookup"><span data-stu-id="78ee1-549">Database</span></span></td>
      <td><span data-ttu-id="78ee1-550">
        <font size=2> Протокол: postgresql</span><span class="sxs-lookup"><span data-stu-id="78ee1-550">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="78ee1-551">Аутентификация: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-551">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="78ee1-552">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-552">Address:</span></span> <br><span data-ttu-id="78ee1-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-553">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-554">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-555">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="78ee1-555">PostgreSQL</span></span></td>
      <td><span data-ttu-id="78ee1-556">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-556">Table</span></span></td>
      <td><span data-ttu-id="78ee1-557">Таблица, представление</span><span class="sxs-lookup"><span data-stu-id="78ee1-557">Table, view</span></span></td>
      <td><span data-ttu-id="78ee1-558">
        <font size=2> Протокол: postgresql</span><span class="sxs-lookup"><span data-stu-id="78ee1-558">
        <font size=2> Protocol: postgresql</span></span> <br><span data-ttu-id="78ee1-559">Аутентификация: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-559">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="78ee1-560">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-560">Address:</span></span> <br><span data-ttu-id="78ee1-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-561">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-562">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="78ee1-563">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="78ee1-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-564">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-565">Power BI</span><span class="sxs-lookup"><span data-stu-id="78ee1-565">Power BI</span></span></td>
      <td><span data-ttu-id="78ee1-566">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-566">Container</span></span></td>
      <td><span data-ttu-id="78ee1-567">Сайт</span><span class="sxs-lookup"><span data-stu-id="78ee1-567">Site</span></span></td>
      <td><span data-ttu-id="78ee1-568">
        <font size=2> Протокол: http</span><span class="sxs-lookup"><span data-stu-id="78ee1-568">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="78ee1-569">Аутентификация: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="78ee1-569">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="78ee1-570">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-570">Address:</span></span> <br><span data-ttu-id="78ee1-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-571">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-572">Power BI</span><span class="sxs-lookup"><span data-stu-id="78ee1-572">Power BI</span></span></td>
      <td><span data-ttu-id="78ee1-573">Отчет</span><span class="sxs-lookup"><span data-stu-id="78ee1-573">Report</span></span></td>
      <td><span data-ttu-id="78ee1-574">Отчет, панель мониторинга</span><span class="sxs-lookup"><span data-stu-id="78ee1-574">Report, dashboard</span></span></td>
      <td><span data-ttu-id="78ee1-575">
        <font size=2> Протокол: http</span><span class="sxs-lookup"><span data-stu-id="78ee1-575">
        <font size=2> Protocol: http</span></span> <br><span data-ttu-id="78ee1-576">Аутентификация: {none, basic, windows, oauth}</span><span class="sxs-lookup"><span data-stu-id="78ee1-576">Authentication: {none, basic, windows, oauth}</span></span> <br><span data-ttu-id="78ee1-577">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-577">Address:</span></span> <br><span data-ttu-id="78ee1-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-578">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-579">Power Query</span><span class="sxs-lookup"><span data-stu-id="78ee1-579">Power Query</span></span></td>
      <td><span data-ttu-id="78ee1-580">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-580">Table</span></span></td>
      <td><span data-ttu-id="78ee1-581">Гибридные данные</span><span class="sxs-lookup"><span data-stu-id="78ee1-581">Data mashup</span></span></td>
      <td><span data-ttu-id="78ee1-582">
        <font size=2> Протокол: power-query</span><span class="sxs-lookup"><span data-stu-id="78ee1-582">
        <font size=2> Protocol: power-query</span></span> <br><span data-ttu-id="78ee1-583">Аутентификация: {oauth}</span><span class="sxs-lookup"><span data-stu-id="78ee1-583">Authentication: {oauth}</span></span> <br><span data-ttu-id="78ee1-584">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-584">Address:</span></span> <br><span data-ttu-id="78ee1-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-585">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-586">Salesforce</span><span class="sxs-lookup"><span data-stu-id="78ee1-586">Salesforce</span></span></td>
      <td><span data-ttu-id="78ee1-587">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-587">Table</span></span></td>
      <td><span data-ttu-id="78ee1-588">Объект</span><span class="sxs-lookup"><span data-stu-id="78ee1-588">Object</span></span></td>
      <td><span data-ttu-id="78ee1-589">
        <font size=2> Протокол: salesforce-com</span><span class="sxs-lookup"><span data-stu-id="78ee1-589">
        <font size=2> Protocol: salesforce-com</span></span> <br><span data-ttu-id="78ee1-590">Аутентификация: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-590">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="78ee1-591">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-591">Address:</span></span> <br><span data-ttu-id="78ee1-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span><span class="sxs-lookup"><span data-stu-id="78ee1-592">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; loginServer</span></span> <br><span data-ttu-id="78ee1-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span><span class="sxs-lookup"><span data-stu-id="78ee1-593">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; class</span></span> <br><span data-ttu-id="78ee1-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-594">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; itemName </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-595">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="78ee1-595">SAP HANA</span></span></td>
      <td><span data-ttu-id="78ee1-596">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-596">Container</span></span></td>
      <td><span data-ttu-id="78ee1-597">сервер;</span><span class="sxs-lookup"><span data-stu-id="78ee1-597">Server</span></span></td>
      <td><span data-ttu-id="78ee1-598">
        <font size=2> Протокол: sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="78ee1-598">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="78ee1-599">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-599">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="78ee1-600">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-600">Address:</span></span> <br><span data-ttu-id="78ee1-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-601">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-602">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="78ee1-602">SAP HANA</span></span></td>
      <td><span data-ttu-id="78ee1-603">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-603">Table</span></span></td>
      <td><span data-ttu-id="78ee1-604">Просмотр</span><span class="sxs-lookup"><span data-stu-id="78ee1-604">View</span></span></td>
      <td><span data-ttu-id="78ee1-605">
        <font size=2> Протокол: sap-hana-sql</span><span class="sxs-lookup"><span data-stu-id="78ee1-605">
        <font size=2> Protocol: sap-hana-sql</span></span> <br><span data-ttu-id="78ee1-606">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-606">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="78ee1-607">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-607">Address:</span></span> <br><span data-ttu-id="78ee1-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-608">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="78ee1-609">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="78ee1-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-610">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-611">SharePoint</span><span class="sxs-lookup"><span data-stu-id="78ee1-611">SharePoint</span></span></td>
      <td><span data-ttu-id="78ee1-612">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-612">Table</span></span></td>
      <td><span data-ttu-id="78ee1-613">список</span><span class="sxs-lookup"><span data-stu-id="78ee1-613">List</span></span></td>
      <td><span data-ttu-id="78ee1-614">
        <font size=2> Протокол: sharepoint-list</span><span class="sxs-lookup"><span data-stu-id="78ee1-614">
        <font size=2> Protocol: sharepoint-list</span></span> <br><span data-ttu-id="78ee1-615">Аутентификация: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-615">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="78ee1-616">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-616">Address:</span></span> <br><span data-ttu-id="78ee1-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-617">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-618">Хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="78ee1-618">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="78ee1-619">Команда</span><span class="sxs-lookup"><span data-stu-id="78ee1-619">Command</span></span></td>
      <td><span data-ttu-id="78ee1-620">Хранимая процедура</span><span class="sxs-lookup"><span data-stu-id="78ee1-620">Stored procedure</span></span></td>
      <td><span data-ttu-id="78ee1-621">
        <font size=2> Протокол: tds</span><span class="sxs-lookup"><span data-stu-id="78ee1-621">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="78ee1-622">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-622">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="78ee1-623">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-623">Address:</span></span> <br><span data-ttu-id="78ee1-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-624">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-625">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="78ee1-626">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="78ee1-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-627">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-628">Хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="78ee1-628">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="78ee1-629">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="78ee1-629">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="78ee1-630">Функция с табличным значением</span><span class="sxs-lookup"><span data-stu-id="78ee1-630">Table-valued function</span></span></td>
      <td><span data-ttu-id="78ee1-631">
        <font size=2> Протокол: tds</span><span class="sxs-lookup"><span data-stu-id="78ee1-631">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="78ee1-632">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-632">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="78ee1-633">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-633">Address:</span></span> <br><span data-ttu-id="78ee1-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-634">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-635">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="78ee1-636">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="78ee1-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-637">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-638">Хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="78ee1-638">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="78ee1-639">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-639">Container</span></span></td>
      <td><span data-ttu-id="78ee1-640">База данных</span><span class="sxs-lookup"><span data-stu-id="78ee1-640">Database</span></span></td>
      <td><span data-ttu-id="78ee1-641">
        <font size=2> Протокол: tds</span><span class="sxs-lookup"><span data-stu-id="78ee1-641">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="78ee1-642">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-642">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="78ee1-643">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-643">Address:</span></span> <br><span data-ttu-id="78ee1-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-644">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-645">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-646">Хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="78ee1-646">SQL Data Warehouse</span></span></td>
      <td><span data-ttu-id="78ee1-647">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-647">Table</span></span></td>
      <td><span data-ttu-id="78ee1-648">Таблица, представление</span><span class="sxs-lookup"><span data-stu-id="78ee1-648">Table, view</span></span></td>
      <td><span data-ttu-id="78ee1-649">
        <font size=2> Протокол: tds</span><span class="sxs-lookup"><span data-stu-id="78ee1-649">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="78ee1-650">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-650">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="78ee1-651">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-651">Address:</span></span> <br><span data-ttu-id="78ee1-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-652">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-653">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="78ee1-654">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="78ee1-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-655">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-656">SQL Server</span><span class="sxs-lookup"><span data-stu-id="78ee1-656">SQL Server</span></span></td>
      <td><span data-ttu-id="78ee1-657">Команда</span><span class="sxs-lookup"><span data-stu-id="78ee1-657">Command</span></span></td>
      <td><span data-ttu-id="78ee1-658">Хранимая процедура</span><span class="sxs-lookup"><span data-stu-id="78ee1-658">Stored procedure</span></span></td>
      <td><span data-ttu-id="78ee1-659">
        <font size=2> Протокол: tds</span><span class="sxs-lookup"><span data-stu-id="78ee1-659">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="78ee1-660">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-660">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="78ee1-661">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-661">Address:</span></span> <br><span data-ttu-id="78ee1-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-662">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-663">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="78ee1-664">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="78ee1-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-665">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-666">SQL Server</span><span class="sxs-lookup"><span data-stu-id="78ee1-666">SQL Server</span></span></td>
      <td><span data-ttu-id="78ee1-667">TableValuedFunction</span><span class="sxs-lookup"><span data-stu-id="78ee1-667">TableValuedFunction</span></span></td>
      <td><span data-ttu-id="78ee1-668">Функция с табличным значением</span><span class="sxs-lookup"><span data-stu-id="78ee1-668">Table-valued function</span></span></td>
      <td><span data-ttu-id="78ee1-669">
        <font size=2> Протокол: tds</span><span class="sxs-lookup"><span data-stu-id="78ee1-669">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="78ee1-670">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-670">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="78ee1-671">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-671">Address:</span></span> <br><span data-ttu-id="78ee1-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-672">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-673">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="78ee1-674">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="78ee1-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-675">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-676">SQL Server</span><span class="sxs-lookup"><span data-stu-id="78ee1-676">SQL Server</span></span></td>
      <td><span data-ttu-id="78ee1-677">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-677">Container</span></span></td>
      <td><span data-ttu-id="78ee1-678">База данных</span><span class="sxs-lookup"><span data-stu-id="78ee1-678">Database</span></span></td>
      <td><span data-ttu-id="78ee1-679">
        <font size=2> Протокол: tds</span><span class="sxs-lookup"><span data-stu-id="78ee1-679">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="78ee1-680">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-680">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="78ee1-681">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-681">Address:</span></span> <br><span data-ttu-id="78ee1-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-682">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-683">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-684">SQL Server</span><span class="sxs-lookup"><span data-stu-id="78ee1-684">SQL Server</span></span></td>
      <td><span data-ttu-id="78ee1-685">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-685">Table</span></span></td>
      <td><span data-ttu-id="78ee1-686">Таблица, представление</span><span class="sxs-lookup"><span data-stu-id="78ee1-686">Table, view</span></span></td>
      <td><span data-ttu-id="78ee1-687">
        <font size=2> Протокол: tds</span><span class="sxs-lookup"><span data-stu-id="78ee1-687">
        <font size=2> Protocol: tds</span></span> <br><span data-ttu-id="78ee1-688">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-688">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="78ee1-689">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-689">Address:</span></span> <br><span data-ttu-id="78ee1-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-690">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-691">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="78ee1-692">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="78ee1-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-693">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-694">Многомерная модель служб SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="78ee1-694">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="78ee1-695">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-695">Container</span></span></td>
      <td><span data-ttu-id="78ee1-696">Модель</span><span class="sxs-lookup"><span data-stu-id="78ee1-696">Model</span></span></td>
      <td><span data-ttu-id="78ee1-697">
        <font size=2> Протокол: analysis-services</span><span class="sxs-lookup"><span data-stu-id="78ee1-697">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="78ee1-698">Аутентификация: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="78ee1-698">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="78ee1-699">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-699">Address:</span></span> <br><span data-ttu-id="78ee1-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-700">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-701">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-702">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-703">Многомерная модель служб SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="78ee1-703">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="78ee1-704">Ключевой показатель эффективности</span><span class="sxs-lookup"><span data-stu-id="78ee1-704">KPI</span></span></td>
      <td><span data-ttu-id="78ee1-705">Ключевой показатель эффективности</span><span class="sxs-lookup"><span data-stu-id="78ee1-705">KPI</span></span></td>
      <td><span data-ttu-id="78ee1-706">
        <font size=2> Протокол: analysis-services</span><span class="sxs-lookup"><span data-stu-id="78ee1-706">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="78ee1-707">Аутентификация: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="78ee1-707">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="78ee1-708">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-708">Address:</span></span> <br><span data-ttu-id="78ee1-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-709">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-710">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="78ee1-711">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="78ee1-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="78ee1-712">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="78ee1-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-713">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-714">Многомерная модель служб SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="78ee1-714">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="78ee1-715">Measure</span><span class="sxs-lookup"><span data-stu-id="78ee1-715">Measure</span></span></td>
      <td><span data-ttu-id="78ee1-716">Measure</span><span class="sxs-lookup"><span data-stu-id="78ee1-716">Measure</span></span></td>
      <td><span data-ttu-id="78ee1-717">
        <font size=2> Протокол: analysis-services</span><span class="sxs-lookup"><span data-stu-id="78ee1-717">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="78ee1-718">Аутентификация: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="78ee1-718">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="78ee1-719">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-719">Address:</span></span> <br><span data-ttu-id="78ee1-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-720">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-721">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="78ee1-722">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="78ee1-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="78ee1-723">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="78ee1-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-724">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-725">Многомерная модель служб SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="78ee1-725">SQL Server Analysis Services multidimensional</span></span></td>
      <td><span data-ttu-id="78ee1-726">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-726">Table</span></span></td>
      <td><span data-ttu-id="78ee1-727">Измерение</span><span class="sxs-lookup"><span data-stu-id="78ee1-727">Dimension</span></span></td>
      <td><span data-ttu-id="78ee1-728">
        <font size=2> Протокол: analysis-services</span><span class="sxs-lookup"><span data-stu-id="78ee1-728">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="78ee1-729">Аутентификация: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="78ee1-729">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="78ee1-730">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-730">Address:</span></span> <br><span data-ttu-id="78ee1-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-731">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-732">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="78ee1-733">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="78ee1-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="78ee1-734">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="78ee1-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-735">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Dimension} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-736">Таблица SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="78ee1-736">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="78ee1-737">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-737">Container</span></span></td>
      <td><span data-ttu-id="78ee1-738">Модель</span><span class="sxs-lookup"><span data-stu-id="78ee1-738">Model</span></span></td>
      <td><span data-ttu-id="78ee1-739">
        <font size=2> Протокол: analysis-services</span><span class="sxs-lookup"><span data-stu-id="78ee1-739">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="78ee1-740">Аутентификация: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="78ee1-740">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="78ee1-741">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-741">Address:</span></span> <br><span data-ttu-id="78ee1-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-742">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-743">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-744">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-745">Таблица SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="78ee1-745">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="78ee1-746">Ключевой показатель эффективности</span><span class="sxs-lookup"><span data-stu-id="78ee1-746">KPI</span></span></td>
      <td><span data-ttu-id="78ee1-747">Ключевой показатель эффективности</span><span class="sxs-lookup"><span data-stu-id="78ee1-747">KPI</span></span></td>
      <td><span data-ttu-id="78ee1-748">
        <font size=2> Протокол: analysis-services</span><span class="sxs-lookup"><span data-stu-id="78ee1-748">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="78ee1-749">Аутентификация: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="78ee1-749">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="78ee1-750">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-750">Address:</span></span> <br><span data-ttu-id="78ee1-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-751">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-752">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="78ee1-753">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="78ee1-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="78ee1-754">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="78ee1-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-755">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {KPI} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-756">Таблица SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="78ee1-756">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="78ee1-757">Measure</span><span class="sxs-lookup"><span data-stu-id="78ee1-757">Measure</span></span></td>
      <td><span data-ttu-id="78ee1-758">Measure</span><span class="sxs-lookup"><span data-stu-id="78ee1-758">Measure</span></span></td>
      <td><span data-ttu-id="78ee1-759">
        <font size=2> Протокол: analysis-services</span><span class="sxs-lookup"><span data-stu-id="78ee1-759">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="78ee1-760">Аутентификация: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="78ee1-760">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="78ee1-761">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-761">Address:</span></span> <br><span data-ttu-id="78ee1-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-762">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-763">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="78ee1-764">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="78ee1-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="78ee1-765">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="78ee1-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-766">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Measure} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-767">Таблица SQL Server Analysis Services</span><span class="sxs-lookup"><span data-stu-id="78ee1-767">SQL Server Analysis Services tabular</span></span></td>
      <td><span data-ttu-id="78ee1-768">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-768">Table</span></span></td>
      <td><span data-ttu-id="78ee1-769">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-769">Table</span></span></td>
      <td><span data-ttu-id="78ee1-770">
        <font size=2> Протокол: analysis-services</span><span class="sxs-lookup"><span data-stu-id="78ee1-770">
        <font size=2> Protocol: analysis-services</span></span> <br><span data-ttu-id="78ee1-771">Аутентификация: {windows, basic, anonymous, none}</span><span class="sxs-lookup"><span data-stu-id="78ee1-771">Authentication: {windows, basic, anonymous, none}</span></span> <br><span data-ttu-id="78ee1-772">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-772">Address:</span></span> <br><span data-ttu-id="78ee1-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-773">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-774">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="78ee1-775">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="78ee1-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="78ee1-776">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="78ee1-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-777">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; objectType: {Table} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-778">Службы отчетов SQL Server</span><span class="sxs-lookup"><span data-stu-id="78ee1-778">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="78ee1-779">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-779">Container</span></span></td>
      <td><span data-ttu-id="78ee1-780">сервер;</span><span class="sxs-lookup"><span data-stu-id="78ee1-780">Server</span></span></td>
      <td><span data-ttu-id="78ee1-781">
        <font size=2> Протокол: reporting-services</span><span class="sxs-lookup"><span data-stu-id="78ee1-781">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="78ee1-782">Аутентификация: {windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-782">Authentication: {windows}</span></span> <br><span data-ttu-id="78ee1-783">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-783">Address:</span></span> <br><span data-ttu-id="78ee1-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-784">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-785">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-786">Службы отчетов SQL Server</span><span class="sxs-lookup"><span data-stu-id="78ee1-786">SQL Server Reporting Services</span></span></td>
      <td><span data-ttu-id="78ee1-787">Отчет</span><span class="sxs-lookup"><span data-stu-id="78ee1-787">Report</span></span></td>
      <td><span data-ttu-id="78ee1-788">Отчет</span><span class="sxs-lookup"><span data-stu-id="78ee1-788">Report</span></span></td>
      <td><span data-ttu-id="78ee1-789">
        <font size=2> Протокол: reporting-services</span><span class="sxs-lookup"><span data-stu-id="78ee1-789">
        <font size=2> Protocol: reporting-services</span></span> <br><span data-ttu-id="78ee1-790">Аутентификация: {windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-790">Authentication: {windows}</span></span> <br><span data-ttu-id="78ee1-791">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-791">Address:</span></span> <br><span data-ttu-id="78ee1-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-792">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span><span class="sxs-lookup"><span data-stu-id="78ee1-793">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; path</span></span> <br><span data-ttu-id="78ee1-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-794">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version: {ReportingService2010} </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-795">Teradata</span><span class="sxs-lookup"><span data-stu-id="78ee1-795">Teradata</span></span></td>
      <td><span data-ttu-id="78ee1-796">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-796">Container</span></span></td>
      <td><span data-ttu-id="78ee1-797">База данных</span><span class="sxs-lookup"><span data-stu-id="78ee1-797">Database</span></span></td>
      <td><span data-ttu-id="78ee1-798">
        <font size=2> Протокол: teradata</span><span class="sxs-lookup"><span data-stu-id="78ee1-798">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="78ee1-799">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-799">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="78ee1-800">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-800">Address:</span></span> <br><span data-ttu-id="78ee1-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-801">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-802">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-803">Teradata</span><span class="sxs-lookup"><span data-stu-id="78ee1-803">Teradata</span></span></td>
      <td><span data-ttu-id="78ee1-804">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-804">Table</span></span></td>
      <td><span data-ttu-id="78ee1-805">Таблица, представление</span><span class="sxs-lookup"><span data-stu-id="78ee1-805">Table, view</span></span></td>
      <td><span data-ttu-id="78ee1-806">
        <font size=2> Протокол: teradata</span><span class="sxs-lookup"><span data-stu-id="78ee1-806">
        <font size=2> Protocol: teradata</span></span> <br><span data-ttu-id="78ee1-807">Аутентификация: {protocol, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-807">Authentication: {protocol, windows}</span></span> <br><span data-ttu-id="78ee1-808">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-808">Address:</span></span> <br><span data-ttu-id="78ee1-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-809">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-810">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-811">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-812">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="78ee1-812">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="78ee1-813">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-813">Container</span></span></td>
      <td><span data-ttu-id="78ee1-814">Модель</span><span class="sxs-lookup"><span data-stu-id="78ee1-814">Model</span></span></td>
      <td><span data-ttu-id="78ee1-815">
        <font size="2"> Протокол: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="78ee1-815">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="78ee1-816">Аутентификация: {windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-816">Authentication: {windows}</span></span> <br><span data-ttu-id="78ee1-817">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-817">Address:</span></span> <br><span data-ttu-id="78ee1-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="78ee1-818">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="78ee1-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="78ee1-819">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="78ee1-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-820">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-821">SQL Server Master Data Services</span><span class="sxs-lookup"><span data-stu-id="78ee1-821">SQL Server Master Data Services</span></span></td>
      <td><span data-ttu-id="78ee1-822">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-822">Table</span></span></td>
      <td><span data-ttu-id="78ee1-823">Сущность</span><span class="sxs-lookup"><span data-stu-id="78ee1-823">Entity</span></span></td>
      <td><span data-ttu-id="78ee1-824">
        <font size="2"> Протокол: mssql-mds</span><span class="sxs-lookup"><span data-stu-id="78ee1-824">
        <font size="2"> Protocol: mssql-mds</span></span> <br><span data-ttu-id="78ee1-825">Аутентификация: {windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-825">Authentication: {windows}</span></span> <br><span data-ttu-id="78ee1-826">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-826">Address:</span></span> <br><span data-ttu-id="78ee1-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="78ee1-827">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="78ee1-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span><span class="sxs-lookup"><span data-stu-id="78ee1-828">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; model</span></span> <br><span data-ttu-id="78ee1-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span><span class="sxs-lookup"><span data-stu-id="78ee1-829">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; version</span></span> <br><span data-ttu-id="78ee1-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-830">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entity </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-831">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="78ee1-831">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="78ee1-832">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-832">Container</span></span></td>
      <td><span data-ttu-id="78ee1-833">База данных</span><span class="sxs-lookup"><span data-stu-id="78ee1-833">Database</span></span></td>
      <td><span data-ttu-id="78ee1-834">
        <font size=2> Протокол: document-db</span><span class="sxs-lookup"><span data-stu-id="78ee1-834">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="78ee1-835">Аутентификация: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="78ee1-835">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="78ee1-836">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-836">Address:</span></span> <br><span data-ttu-id="78ee1-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="78ee1-837">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="78ee1-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-838">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-839">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="78ee1-839">Azure Cosmos DB</span></span></td>
      <td><span data-ttu-id="78ee1-840">Коллекция</span><span class="sxs-lookup"><span data-stu-id="78ee1-840">Collection</span></span></td>
      <td><span data-ttu-id="78ee1-841">Коллекция</span><span class="sxs-lookup"><span data-stu-id="78ee1-841">Collection</span></span></td>
      <td><span data-ttu-id="78ee1-842">
        <font size=2> Протокол: document-db</span><span class="sxs-lookup"><span data-stu-id="78ee1-842">
        <font size=2> Protocol: document-db</span></span> <br><span data-ttu-id="78ee1-843">Аутентификация: {azure-access-key}</span><span class="sxs-lookup"><span data-stu-id="78ee1-843">Authentication: {azure-access-key}</span></span> <br><span data-ttu-id="78ee1-844">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-844">Address:</span></span> <br><span data-ttu-id="78ee1-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span><span class="sxs-lookup"><span data-stu-id="78ee1-845">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; url</span></span> <br><span data-ttu-id="78ee1-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-846">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; collection </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-847">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; collection </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-848">Универсальные данные ODBC</span><span class="sxs-lookup"><span data-stu-id="78ee1-848">Generic ODBC</span></span></td>
      <td><span data-ttu-id="78ee1-849">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-849">Container</span></span></td>
      <td><span data-ttu-id="78ee1-850">База данных</span><span class="sxs-lookup"><span data-stu-id="78ee1-850">Database</span></span></td>
      <td><span data-ttu-id="78ee1-851">
        <font size=2> Протокол: odbc</span><span class="sxs-lookup"><span data-stu-id="78ee1-851">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="78ee1-852">Аутентификация: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-852">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="78ee1-853">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-853">Address:</span></span> <br><span data-ttu-id="78ee1-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span><span class="sxs-lookup"><span data-stu-id="78ee1-854">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="78ee1-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-855">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-856">Универсальные данные ODBC</span><span class="sxs-lookup"><span data-stu-id="78ee1-856">Generic ODBC</span></span></td>
      <td><span data-ttu-id="78ee1-857">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-857">Table</span></span></td>
      <td><span data-ttu-id="78ee1-858">Таблица, представление</span><span class="sxs-lookup"><span data-stu-id="78ee1-858">Table, View</span></span></td>
      <td><span data-ttu-id="78ee1-859">
        <font size=2> Протокол: odbc</span><span class="sxs-lookup"><span data-stu-id="78ee1-859">
        <font size=2> Protocol: odbc</span></span> <br><span data-ttu-id="78ee1-860">Аутентификация: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-860">Authentication: {basic, windows}</span></span> <br><span data-ttu-id="78ee1-861">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-861">Address:</span></span> <br><span data-ttu-id="78ee1-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span><span class="sxs-lookup"><span data-stu-id="78ee1-862">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; options</span></span> <br><span data-ttu-id="78ee1-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-863">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span><span class="sxs-lookup"><span data-stu-id="78ee1-864">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object</span></span> <br><span data-ttu-id="78ee1-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-865">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-866">Sybase</span><span class="sxs-lookup"><span data-stu-id="78ee1-866">Sybase</span></span></td>
      <td><span data-ttu-id="78ee1-867">Контейнер</span><span class="sxs-lookup"><span data-stu-id="78ee1-867">Container</span></span></td>
      <td><span data-ttu-id="78ee1-868">База данных</span><span class="sxs-lookup"><span data-stu-id="78ee1-868">Database</span></span></td>
      <td><span data-ttu-id="78ee1-869">
        <font size=2> Протокол: sybase</span><span class="sxs-lookup"><span data-stu-id="78ee1-869">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="78ee1-870">Проверка подлинности: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-870">authentication: {basic, windows}</span></span> <br><span data-ttu-id="78ee1-871">адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-871">address:</span></span> <br><span data-ttu-id="78ee1-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-872">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-873">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-874">Sybase</span><span class="sxs-lookup"><span data-stu-id="78ee1-874">Sybase</span></span></td>
      <td><span data-ttu-id="78ee1-875">Таблица</span><span class="sxs-lookup"><span data-stu-id="78ee1-875">Table</span></span></td>
      <td><span data-ttu-id="78ee1-876">Таблица, представление</span><span class="sxs-lookup"><span data-stu-id="78ee1-876">Table, View</span></span></td>
      <td><span data-ttu-id="78ee1-877">
        <font size=2> Протокол: sybase</span><span class="sxs-lookup"><span data-stu-id="78ee1-877">
        <font size=2> protocol: sybase</span></span> <br><span data-ttu-id="78ee1-878">Проверка подлинности: {basic, windows}</span><span class="sxs-lookup"><span data-stu-id="78ee1-878">authentication: {basic, windows}</span></span> <br><span data-ttu-id="78ee1-879">адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-879">address:</span></span> <br><span data-ttu-id="78ee1-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span><span class="sxs-lookup"><span data-stu-id="78ee1-880">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; server</span></span> <br><span data-ttu-id="78ee1-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span><span class="sxs-lookup"><span data-stu-id="78ee1-881">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; database</span></span> <br><span data-ttu-id="78ee1-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span><span class="sxs-lookup"><span data-stu-id="78ee1-882">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; schema</span></span> <br><span data-ttu-id="78ee1-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-883">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; object </font>
      </span></span></td>
    </tr>
    <tr>
      <td><span data-ttu-id="78ee1-884">Другой (ни один из указанных выше)</span><span class="sxs-lookup"><span data-stu-id="78ee1-884">Other (none of the above)</span></span></td>
      <td>\*</td>
      <td>\*</td>
      <td><span data-ttu-id="78ee1-885">
        <font size=2> Протокол: generic-asset</span><span class="sxs-lookup"><span data-stu-id="78ee1-885">
        <font size=2> Protocol: generic-asset</span></span> <br><span data-ttu-id="78ee1-886">Адрес:</span><span class="sxs-lookup"><span data-stu-id="78ee1-886">Address:</span></span> <br><span data-ttu-id="78ee1-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span><span class="sxs-lookup"><span data-stu-id="78ee1-887">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; assetId </font>
      </span></span></td>
    </tr>
</table>
