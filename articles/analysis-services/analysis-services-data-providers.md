---
title: "Клиентские библиотеки, требуемые для подключения к службам Azure Analysis Services | Документы Майкрософт"
description: "Описываются клиентские библиотеки, необходимые для подключения клиентских приложений и средств к службам Azure Analysis Services"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: a96e7fe671dc051da35168fa7b49ecba53b4c4a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="client-libraries-for-connecting-to-azure-analysis-services"></a><span data-ttu-id="b137d-103">Клиентские библиотеки для подключения к службам Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="b137d-103">Client libraries for connecting to Azure Analysis Services</span></span>

<span data-ttu-id="b137d-104">Клиентские библиотеки требуются клиентским приложениям и средствам для подключения к серверам служб Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="b137d-104">Client libraries are necessary for client applications and tools to connect to Analysis Services servers.</span></span> 

<span data-ttu-id="b137d-105">Службы Analysis Services используют три типа клиентских библиотек.</span><span class="sxs-lookup"><span data-stu-id="b137d-105">Analysis Services utilize three client libraries.</span></span> <span data-ttu-id="b137d-106">ADOMD.NET и объекты управления служб Analysis Services — это управляемые клиентские библиотеки.</span><span class="sxs-lookup"><span data-stu-id="b137d-106">ADOMD.NET and Analysis Services Management Objects (AMO), are managed client libraries.</span></span> <span data-ttu-id="b137d-107">Поставщик OLE DB служб Analysis Services (MSOLAP DLL) — это собственная клиентская библиотека.</span><span class="sxs-lookup"><span data-stu-id="b137d-107">The Analysis Services OLE DB provider (MSOLAP DLL) is a native client library.</span></span> <span data-ttu-id="b137d-108">Как правило, все три библиотеки устанавливаются одновременно.</span><span class="sxs-lookup"><span data-stu-id="b137d-108">Typically, all three are installed at the same time.</span></span> <span data-ttu-id="b137d-109">Службам Azure Analysis Services требуются последние версии библиотек.</span><span class="sxs-lookup"><span data-stu-id="b137d-109">Azure Analysis Services requires the latest versions.</span></span> 

<span data-ttu-id="b137d-110">Клиентские приложения Майкрософт, такие как Power BI Desktop и Excel, устанавливают все три клиентские библиотеки.</span><span class="sxs-lookup"><span data-stu-id="b137d-110">Microsoft client applications such as Power BI Desktop and Excel install all three client libraries.</span></span> <span data-ttu-id="b137d-111">Однако в зависимости от версии или частоты обновлений могут устанавливаться устаревшие, а не новые версии клиентских библиотек, необходимые для служб Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="b137d-111">However, depending on the version or frequency of updates, client libraries may not be the latest versions required by Azure Analysis Services.</span></span> <span data-ttu-id="b137d-112">Это же касается и пользовательских приложений или других интерфейсов, таких как AsCmd, TOM, ADOMD.NET.</span><span class="sxs-lookup"><span data-stu-id="b137d-112">The same applies to custom applications or other interfaces such as AsCmd, TOM, ADOMD.NET.</span></span> <span data-ttu-id="b137d-113">Для этих приложений клиентские библиотеки требуется устанавливать вручную.</span><span class="sxs-lookup"><span data-stu-id="b137d-113">These applications require manually installing the libraries.</span></span> <span data-ttu-id="b137d-114">Клиентские библиотеки, устанавливаемые вручную, включены в пакеты дополнительных компонентов SQL Server в качестве распространяемых пакетов.</span><span class="sxs-lookup"><span data-stu-id="b137d-114">The client libraries for manual installation are included in SQL Server feature packs as distributable packages.</span></span> <span data-ttu-id="b137d-115">Однако они зависят от версии SQL Server, поэтому версия в пакетах может быть не последней.</span><span class="sxs-lookup"><span data-stu-id="b137d-115">However, these client libraries are tied to the SQL Server version and may not be the latest.</span></span>  

<span data-ttu-id="b137d-116">Клиентские библиотеки для клиентских подключений отличаются от поставщиков данных, требуемых для подключения с сервера служб Azure Analysis Services к источнику данных.</span><span class="sxs-lookup"><span data-stu-id="b137d-116">Client libraries for client connections are different from data providers required to connect from an Azure Analysis Services server to a data source.</span></span> <span data-ttu-id="b137d-117">Дополнительные сведения о подключениях к источнику данных см. в [этой статье](analysis-services-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="b137d-117">To learn more about datasource connections, see [Datasource connections](analysis-services-datasource.md).</span></span>

## <a name="download-the-latest-client-libraries"></a><span data-ttu-id="b137d-118">Скачивание последних версий клиентских библиотек</span><span class="sxs-lookup"><span data-stu-id="b137d-118">Download the latest client libraries</span></span>  
<span data-ttu-id="b137d-119">Используйте перечисленные ниже клиентские библиотеки, если в рабочей среде требуются полностью выпущенные и поддерживаемые версии.</span><span class="sxs-lookup"><span data-stu-id="b137d-119">Use the following client libraries if you are in a production environment and require fully released and supported versions.</span></span>

[<span data-ttu-id="b137d-120">MSOLAP (amd64)</span><span class="sxs-lookup"><span data-stu-id="b137d-120">MSOLAP (amd64)</span></span>](https://go.microsoft.com/fwlink/?linkid=829576)</br><span data-ttu-id="b137d-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span><span class="sxs-lookup"><span data-stu-id="b137d-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span></span></br><span data-ttu-id="b137d-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span><span class="sxs-lookup"><span data-stu-id="b137d-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span></span></br><span data-ttu-id="b137d-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span><span class="sxs-lookup"><span data-stu-id="b137d-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="b137d-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b137d-124">Next steps</span></span>
<span data-ttu-id="b137d-125">[Подключение с помощью Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="b137d-125">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
[<span data-ttu-id="b137d-126">Подключение с помощью Power BI</span><span class="sxs-lookup"><span data-stu-id="b137d-126">Connect with Power BI</span></span>](analysis-services-connect-pbi.md)
