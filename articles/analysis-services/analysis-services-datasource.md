---
title: "Источники данных, поддерживаемые в службах Azure Analysis Services | Документы Майкрософт"
description: "Описание источников данных, поддерживаемых для моделей данных в службах Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 6ec63319-ff9b-4b01-a1cd-274481dc8995
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 8bd6c3b5a923ce2f3cd0f60af82e59c5cc27cbb4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="data-sources-supported-in-azure-analysis-services"></a><span data-ttu-id="87f4d-103">Источники данных, поддерживаемые в службах Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="87f4d-103">Data sources supported in Azure Analysis Services</span></span>
<span data-ttu-id="87f4d-104">Серверы служб Azure Analysis Services поддерживают подключение к локальным и облачным источникам данных.</span><span class="sxs-lookup"><span data-stu-id="87f4d-104">Azure Analysis Services servers support connecting to data sources in the cloud and on-premises in your organization.</span></span> <span data-ttu-id="87f4d-105">Дополнительные поддерживаемые источники данных добавляются на постоянной основе.</span><span class="sxs-lookup"><span data-stu-id="87f4d-105">Additional supported data sources are being added all the time.</span></span> <span data-ttu-id="87f4d-106">Следите за обновлениями.</span><span class="sxs-lookup"><span data-stu-id="87f4d-106">Check back often.</span></span> 

<span data-ttu-id="87f4d-107">В настоящее время поддерживаются следующие источники данных:</span><span class="sxs-lookup"><span data-stu-id="87f4d-107">The following data sources are currently supported:</span></span>

| <span data-ttu-id="87f4d-108">Облако</span><span class="sxs-lookup"><span data-stu-id="87f4d-108">Cloud</span></span>  |
|---|
| <span data-ttu-id="87f4d-109">Хранилище BLOB-объектов Azure*</span><span class="sxs-lookup"><span data-stu-id="87f4d-109">Azure Blob Storage*</span></span>  |
| <span data-ttu-id="87f4d-110">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="87f4d-110">Azure SQL Database</span></span>  |
| <span data-ttu-id="87f4d-111">Хранилище данных Azure</span><span class="sxs-lookup"><span data-stu-id="87f4d-111">Azure Data Warehouse</span></span> |


| <span data-ttu-id="87f4d-112">Локальная система</span><span class="sxs-lookup"><span data-stu-id="87f4d-112">On-premises</span></span>  |   |   |   |
|---|---|---|---|
| <span data-ttu-id="87f4d-113">База данных Access</span><span class="sxs-lookup"><span data-stu-id="87f4d-113">Access Database</span></span>  | <span data-ttu-id="87f4d-114">Папка*</span><span class="sxs-lookup"><span data-stu-id="87f4d-114">Folder*</span></span> | <span data-ttu-id="87f4d-115">База данных Oracle</span><span class="sxs-lookup"><span data-stu-id="87f4d-115">Oracle Database</span></span>  | <span data-ttu-id="87f4d-116">База данных Teradata</span><span class="sxs-lookup"><span data-stu-id="87f4d-116">Teradata Database</span></span> |
| <span data-ttu-id="87f4d-117">Active Directory*</span><span class="sxs-lookup"><span data-stu-id="87f4d-117">Active Directory*</span></span>  | <span data-ttu-id="87f4d-118">Документ JSON*</span><span class="sxs-lookup"><span data-stu-id="87f4d-118">JSON document*</span></span>  | <span data-ttu-id="87f4d-119">База данных SQL Postgre*</span><span class="sxs-lookup"><span data-stu-id="87f4d-119">Postgre SQL Database*</span></span>  |<span data-ttu-id="87f4d-120">Таблица XML*</span><span class="sxs-lookup"><span data-stu-id="87f4d-120">XML table*</span></span> |
| <span data-ttu-id="87f4d-121">службы Analysis Services</span><span class="sxs-lookup"><span data-stu-id="87f4d-121">Analysis Services</span></span>  | <span data-ttu-id="87f4d-122">Строки из двоичного файла*</span><span class="sxs-lookup"><span data-stu-id="87f4d-122">Lines from binary*</span></span>  | <span data-ttu-id="87f4d-123">SAP HANA*</span><span class="sxs-lookup"><span data-stu-id="87f4d-123">SAP HANA*</span></span>  |
| <span data-ttu-id="87f4d-124">Система платформы аналитики</span><span class="sxs-lookup"><span data-stu-id="87f4d-124">Analytics Platform System</span></span>  | <span data-ttu-id="87f4d-125">База данных MySQL</span><span class="sxs-lookup"><span data-stu-id="87f4d-125">MySQL Database</span></span>  | <span data-ttu-id="87f4d-126">SAP Business Warehouse*</span><span class="sxs-lookup"><span data-stu-id="87f4d-126">SAP Business Warehouse*</span></span>  | |
| <span data-ttu-id="87f4d-127">Dynamics CRM*</span><span class="sxs-lookup"><span data-stu-id="87f4d-127">Dynamics CRM*</span></span>  | <span data-ttu-id="87f4d-128">Веб-канал OData*</span><span class="sxs-lookup"><span data-stu-id="87f4d-128">OData Feed*</span></span>  | <span data-ttu-id="87f4d-129">SharePoint*</span><span class="sxs-lookup"><span data-stu-id="87f4d-129">SharePoint*</span></span>  |
| <span data-ttu-id="87f4d-130">Книга Excel</span><span class="sxs-lookup"><span data-stu-id="87f4d-130">Excel workbook</span></span>  | <span data-ttu-id="87f4d-131">Запрос ODBC</span><span class="sxs-lookup"><span data-stu-id="87f4d-131">ODBC query</span></span>  | <span data-ttu-id="87f4d-132">База данных SQL</span><span class="sxs-lookup"><span data-stu-id="87f4d-132">SQL Database</span></span>  |
| <span data-ttu-id="87f4d-133">Exchange*</span><span class="sxs-lookup"><span data-stu-id="87f4d-133">Exchange*</span></span>  | <span data-ttu-id="87f4d-134">OLE DB</span><span class="sxs-lookup"><span data-stu-id="87f4d-134">OLE DB</span></span>  | <span data-ttu-id="87f4d-135">База данных Sybase</span><span class="sxs-lookup"><span data-stu-id="87f4d-135">Sybase Database</span></span>  |

<span data-ttu-id="87f4d-136">\* Только для табличных моделей 1400.</span><span class="sxs-lookup"><span data-stu-id="87f4d-136">\* Tabular 1400 models only.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="87f4d-137">Для подключения к локальным источникам данных требуется [локальный шлюз данных](analysis-services-gateway.md), установленный на компьютере в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="87f4d-137">Connecting to on-premises data sources require an [On-premises data gateway](analysis-services-gateway.md) installed on a computer in your environment.</span></span>

## <a name="data-providers"></a><span data-ttu-id="87f4d-138">Поставщики данных</span><span class="sxs-lookup"><span data-stu-id="87f4d-138">Data providers</span></span>

<span data-ttu-id="87f4d-139">Моделям данных в службах Azure Analysis Services могут требоваться разные поставщики данных при подключении к определенным источникам данных.</span><span class="sxs-lookup"><span data-stu-id="87f4d-139">Data models in Azure Analysis Services may require different data providers when connecting to certain data sources.</span></span> <span data-ttu-id="87f4d-140">В некоторых случаях табличные модели, которые подключаются к источникам данных с помощью собственных поставщиков, таких как собственный клиент SQL Server (SQLNCLI11), могут возвращать ошибку.</span><span class="sxs-lookup"><span data-stu-id="87f4d-140">In some cases, tabular models connecting to data sources using native providers such as SQL Server Native Client (SQLNCLI11) may return an error.</span></span>

<span data-ttu-id="87f4d-141">При наличии моделей данных, которые подключаются к облачному источнику данных, такому как база данных SQL Azure, если используются собственные поставщики, кроме SQLOLEDB, может отображаться сообщение об ошибке: **"The provider 'SQLNCLI11.1' is not registered"** (Поставщик "SQLNCLI11.1" не зарегистрирован).</span><span class="sxs-lookup"><span data-stu-id="87f4d-141">For data models that connect to a cloud data source such as Azure SQL Database, if you use native providers other than SQLOLEDB, you may see error message: **“The provider 'SQLNCLI11.1' is not registered.”**</span></span> <span data-ttu-id="87f4d-142">Если же при наличии модели DirectQuery, подключающейся к локальным источникам данных, используются собственные поставщики, может появиться сообщение об ошибке: **"Error creating OLE DB row set. Incorrect syntax near 'LIMIT'"** (Ошибка при создании набора строк OLE DB. Неверный синтаксис рядом с "LIMIT").</span><span class="sxs-lookup"><span data-stu-id="87f4d-142">Or, if you have a DirectQuery model connecting to on-premises data sources, if you use native providers you may see error message: **“Error creating OLE DB row set. Incorrect syntax near 'LIMIT'”**.</span></span>

<span data-ttu-id="87f4d-143">При подключении к локальным или облачным источникам данных поддерживаются следующие поставщики источников данных для моделей данных в памяти или моделей данных DirectQuery:</span><span class="sxs-lookup"><span data-stu-id="87f4d-143">The following datasource providers are supported for in-memory or DirectQuery data models when connecting to data sources in the cloud or on-premises:</span></span>

### <a name="cloud"></a><span data-ttu-id="87f4d-144">Облако</span><span class="sxs-lookup"><span data-stu-id="87f4d-144">Cloud</span></span>
| <span data-ttu-id="87f4d-145">**Источник данных**</span><span class="sxs-lookup"><span data-stu-id="87f4d-145">**Datasource**</span></span> | <span data-ttu-id="87f4d-146">**В памяти**</span><span class="sxs-lookup"><span data-stu-id="87f4d-146">**In-memory**</span></span> | <span data-ttu-id="87f4d-147">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="87f4d-147">**DirectQuery**</span></span> |
|  --- | --- | --- |
| <span data-ttu-id="87f4d-148">Хранилище данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="87f4d-148">Azure SQL Data Warehouse</span></span> |<span data-ttu-id="87f4d-149">Поставщик данных .NET Framework для SQL Server</span><span class="sxs-lookup"><span data-stu-id="87f4d-149">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="87f4d-150">Поставщик данных .NET Framework для SQL Server</span><span class="sxs-lookup"><span data-stu-id="87f4d-150">.NET Framework Data Provider for SQL Server</span></span> |
| <span data-ttu-id="87f4d-151">База данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="87f4d-151">Azure SQL Database</span></span> |<span data-ttu-id="87f4d-152">Поставщик данных .NET Framework для SQL Server</span><span class="sxs-lookup"><span data-stu-id="87f4d-152">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="87f4d-153">Поставщик данных .NET Framework для SQL Server</span><span class="sxs-lookup"><span data-stu-id="87f4d-153">.NET Framework Data Provider for SQL Server</span></span> | |

### <a name="on-premises-via-gateway"></a><span data-ttu-id="87f4d-154">Локально (через шлюз)</span><span class="sxs-lookup"><span data-stu-id="87f4d-154">On-premises (via Gateway)</span></span>
|<span data-ttu-id="87f4d-155">**Источник данных**</span><span class="sxs-lookup"><span data-stu-id="87f4d-155">**Datasource**</span></span> | <span data-ttu-id="87f4d-156">**В памяти**</span><span class="sxs-lookup"><span data-stu-id="87f4d-156">**In-memory**</span></span> | <span data-ttu-id="87f4d-157">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="87f4d-157">**DirectQuery**</span></span> |
|  --- | --- | --- |
| <span data-ttu-id="87f4d-158">SQL Server</span><span class="sxs-lookup"><span data-stu-id="87f4d-158">SQL Server</span></span> |<span data-ttu-id="87f4d-159">SQL Server Native Client 11.0</span><span class="sxs-lookup"><span data-stu-id="87f4d-159">SQL Server Native Client 11.0</span></span> |<span data-ttu-id="87f4d-160">Поставщик данных .NET Framework для SQL Server</span><span class="sxs-lookup"><span data-stu-id="87f4d-160">.NET Framework Data Provider for SQL Server</span></span> |
| <span data-ttu-id="87f4d-161">SQL Server</span><span class="sxs-lookup"><span data-stu-id="87f4d-161">SQL Server</span></span> |<span data-ttu-id="87f4d-162">Поставщик Microsoft OLE DB для SQL Server</span><span class="sxs-lookup"><span data-stu-id="87f4d-162">Microsoft OLE DB Provider for SQL Server</span></span> |<span data-ttu-id="87f4d-163">Поставщик данных .NET Framework для SQL Server</span><span class="sxs-lookup"><span data-stu-id="87f4d-163">.NET Framework Data Provider for SQL Server</span></span> | |
| <span data-ttu-id="87f4d-164">SQL Server</span><span class="sxs-lookup"><span data-stu-id="87f4d-164">SQL Server</span></span> |<span data-ttu-id="87f4d-165">Поставщик данных .NET Framework для SQL Server</span><span class="sxs-lookup"><span data-stu-id="87f4d-165">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="87f4d-166">Поставщик данных .NET Framework для SQL Server</span><span class="sxs-lookup"><span data-stu-id="87f4d-166">.NET Framework Data Provider for SQL Server</span></span> | |
| <span data-ttu-id="87f4d-167">Oracle</span><span class="sxs-lookup"><span data-stu-id="87f4d-167">Oracle</span></span> |<span data-ttu-id="87f4d-168">Поставщик Microsoft OLE DB для Oracle</span><span class="sxs-lookup"><span data-stu-id="87f4d-168">Microsoft OLE DB Provider for Oracle</span></span> |<span data-ttu-id="87f4d-169">Поставщик данных Oracle для .NET</span><span class="sxs-lookup"><span data-stu-id="87f4d-169">Oracle Data Provider for .NET</span></span> | |
| <span data-ttu-id="87f4d-170">Oracle</span><span class="sxs-lookup"><span data-stu-id="87f4d-170">Oracle</span></span> |<span data-ttu-id="87f4d-171">Поставщик данных Oracle для .NET</span><span class="sxs-lookup"><span data-stu-id="87f4d-171">Oracle Data Provider for .NET</span></span> |<span data-ttu-id="87f4d-172">Поставщик данных Oracle для .NET</span><span class="sxs-lookup"><span data-stu-id="87f4d-172">Oracle Data Provider for .NET</span></span> | |
| <span data-ttu-id="87f4d-173">Teradata</span><span class="sxs-lookup"><span data-stu-id="87f4d-173">Teradata</span></span> |<span data-ttu-id="87f4d-174">Поставщик OLE DB для Teradata</span><span class="sxs-lookup"><span data-stu-id="87f4d-174">OLE DB Provider for Teradata</span></span> |<span data-ttu-id="87f4d-175">Поставщик данных Teradata для .NET</span><span class="sxs-lookup"><span data-stu-id="87f4d-175">Teradata Data Provider for .NET</span></span> | |
| <span data-ttu-id="87f4d-176">Teradata</span><span class="sxs-lookup"><span data-stu-id="87f4d-176">Teradata</span></span> |<span data-ttu-id="87f4d-177">Поставщик данных Teradata для .NET</span><span class="sxs-lookup"><span data-stu-id="87f4d-177">Teradata Data Provider for .NET</span></span> |<span data-ttu-id="87f4d-178">Поставщик данных Teradata для .NET</span><span class="sxs-lookup"><span data-stu-id="87f4d-178">Teradata Data Provider for .NET</span></span> | |
| <span data-ttu-id="87f4d-179">Система платформы аналитики</span><span class="sxs-lookup"><span data-stu-id="87f4d-179">Analytics Platform System</span></span> |<span data-ttu-id="87f4d-180">Поставщик данных .NET Framework для SQL Server</span><span class="sxs-lookup"><span data-stu-id="87f4d-180">.NET Framework Data Provider for SQL Server</span></span> |<span data-ttu-id="87f4d-181">Поставщик данных .NET Framework для SQL Server</span><span class="sxs-lookup"><span data-stu-id="87f4d-181">.NET Framework Data Provider for SQL Server</span></span> | |

> [!NOTE]
> <span data-ttu-id="87f4d-182">При использовании локального шлюза убедитесь, что установлены 64-разрядные версии поставщиков.</span><span class="sxs-lookup"><span data-stu-id="87f4d-182">Ensure 64-bit providers are installed when using On-premises gateway.</span></span>
> 
> 

<span data-ttu-id="87f4d-183">При переносе локальной табличной модели служб SQL Server Analysis Services в службы Azure Analysis Services может потребоваться изменить поставщика.</span><span class="sxs-lookup"><span data-stu-id="87f4d-183">When migrating an on-premises SQL Server Analysis Services tabular model to Azure Analysis Services, it may be necessary to change the provider.</span></span>

<span data-ttu-id="87f4d-184">**Указание поставщика источников данных**</span><span class="sxs-lookup"><span data-stu-id="87f4d-184">**To specify a datasource provider**</span></span>

1. <span data-ttu-id="87f4d-185">В разделе SSDT > **Tabular Model Explorer (Обозреватель табличных моделей)** > **Data Sources (Источники данных)** щелкните правой кнопкой подключение к источнику данных и выберите **Edit Data Source (Изменить источник данных)**.</span><span class="sxs-lookup"><span data-stu-id="87f4d-185">In SSDT > **Tabular Model Explorer** > **Data Sources**, right-click a data source connection, and then click **Edit Data Source**.</span></span>
2. <span data-ttu-id="87f4d-186">В окне **Edit Connection** (Изменение подключения) щелкните **Advanced** (Дополнительно), чтобы открыть окно дополнительных свойств.</span><span class="sxs-lookup"><span data-stu-id="87f4d-186">In **Edit Connection**, click **Advanced** to open the Advance properties window.</span></span>
3. <span data-ttu-id="87f4d-187">В разделе **Set Advanced Properties (Настройка дополнительных свойств)** > **Providers (Поставщики)** выберите соответствующего поставщика.</span><span class="sxs-lookup"><span data-stu-id="87f4d-187">In **Set Advanced Properties** > **Providers**, then select the appropriate provider.</span></span>

## <a name="impersonation"></a><span data-ttu-id="87f4d-188">Олицетворение</span><span class="sxs-lookup"><span data-stu-id="87f4d-188">Impersonation</span></span>
<span data-ttu-id="87f4d-189">В некоторых случаях может быть необходимо указать другую учетную запись олицетворения.</span><span class="sxs-lookup"><span data-stu-id="87f4d-189">In some cases, it may be necessary to specify a different impersonation account.</span></span> <span data-ttu-id="87f4d-190">Учетную запись олицетворения можно указать в SSDT или SSMS.</span><span class="sxs-lookup"><span data-stu-id="87f4d-190">Impersonation account can be specified in SSDT or SSMS.</span></span>

<span data-ttu-id="87f4d-191">Для локальных источников данных:</span><span class="sxs-lookup"><span data-stu-id="87f4d-191">For on-premises data sources:</span></span>

* <span data-ttu-id="87f4d-192">При использовании проверки подлинности SQL олицетворением должна быть учетная запись службы.</span><span class="sxs-lookup"><span data-stu-id="87f4d-192">If using SQL authentication, impersonation should be Service Account.</span></span>
* <span data-ttu-id="87f4d-193">При использовании проверки подлинности Windows задайте пользователя и пароль Windows.</span><span class="sxs-lookup"><span data-stu-id="87f4d-193">If using Windows authentication, set Windows user/password.</span></span> <span data-ttu-id="87f4d-194">Для SQL Server проверка подлинности Windows с использованием конкретной учетной записи олицетворения поддерживается только для моделей данных в памяти.</span><span class="sxs-lookup"><span data-stu-id="87f4d-194">For SQL Server, Windows authentication with a specific impersonation account is supported only for in-memory data models.</span></span>

<span data-ttu-id="87f4d-195">Для облачных источников данных</span><span class="sxs-lookup"><span data-stu-id="87f4d-195">For cloud data sources:</span></span>

* <span data-ttu-id="87f4d-196">При использовании проверки подлинности SQL олицетворением должна быть учетная запись службы.</span><span class="sxs-lookup"><span data-stu-id="87f4d-196">If using SQL authentication, impersonation should be Service Account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87f4d-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="87f4d-197">Next steps</span></span>
<span data-ttu-id="87f4d-198">При наличии локальных источников данных не забудьте установить [локальный шлюз](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="87f4d-198">If you have on-premises data sources, be sure to install the [On-premises gateway](analysis-services-gateway.md).</span></span>   
<span data-ttu-id="87f4d-199">Дополнительные сведения об управлении сервером в SSDT или SSMS см. в разделе об [управлении сервером](analysis-services-manage.md).</span><span class="sxs-lookup"><span data-stu-id="87f4d-199">To learn more about managing your server in SSDT or SSMS, see [Manage your server](analysis-services-manage.md).</span></span>

