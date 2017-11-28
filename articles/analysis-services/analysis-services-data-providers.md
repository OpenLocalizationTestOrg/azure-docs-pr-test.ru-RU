---
title: "aaaClient библиотеки, необходимые для соединения служб Analysis Services tooAzure | Документы Microsoft"
description: "Описывает клиентские библиотеки, необходимые для клиентского приложения и средства tooconnect Azure Analysis Services"
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
ms.openlocfilehash: 74ba5c05ba76c6587c5aed38f200a1ba469aa4f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="client-libraries-for-connecting-tooazure-analysis-services"></a><span data-ttu-id="066fc-103">Клиентские библиотеки для соединения служб Analysis Services tooAzure</span><span class="sxs-lookup"><span data-stu-id="066fc-103">Client libraries for connecting tooAzure Analysis Services</span></span>

<span data-ttu-id="066fc-104">Клиентские библиотеки необходимы для клиентских приложений и серверов служб tooAnalysis tooconnect средства.</span><span class="sxs-lookup"><span data-stu-id="066fc-104">Client libraries are necessary for client applications and tools tooconnect tooAnalysis Services servers.</span></span> 

<span data-ttu-id="066fc-105">Службы Analysis Services используют три типа клиентских библиотек.</span><span class="sxs-lookup"><span data-stu-id="066fc-105">Analysis Services utilize three client libraries.</span></span> <span data-ttu-id="066fc-106">ADOMD.NET и объекты управления служб Analysis Services — это управляемые клиентские библиотеки.</span><span class="sxs-lookup"><span data-stu-id="066fc-106">ADOMD.NET and Analysis Services Management Objects (AMO), are managed client libraries.</span></span> <span data-ttu-id="066fc-107">Поставщик OLE DB служб Analysis Services Hello (MSOLAP DLL) — это библиотека собственного клиента.</span><span class="sxs-lookup"><span data-stu-id="066fc-107">hello Analysis Services OLE DB provider (MSOLAP DLL) is a native client library.</span></span> <span data-ttu-id="066fc-108">Как правило, все три устанавливаются в hello то же время.</span><span class="sxs-lookup"><span data-stu-id="066fc-108">Typically, all three are installed at hello same time.</span></span> <span data-ttu-id="066fc-109">Azure Analysis Services требует hello последних версий.</span><span class="sxs-lookup"><span data-stu-id="066fc-109">Azure Analysis Services requires hello latest versions.</span></span> 

<span data-ttu-id="066fc-110">Клиентские приложения Майкрософт, такие как Power BI Desktop и Excel, устанавливают все три клиентские библиотеки.</span><span class="sxs-lookup"><span data-stu-id="066fc-110">Microsoft client applications such as Power BI Desktop and Excel install all three client libraries.</span></span> <span data-ttu-id="066fc-111">Тем не менее в зависимости от версии hello или частота обновления, клиентские библиотеки не может быть hello последние версии необходимых служб Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="066fc-111">However, depending on hello version or frequency of updates, client libraries may not be hello latest versions required by Azure Analysis Services.</span></span> <span data-ttu-id="066fc-112">Hello применимо и к toocustom приложений или другие интерфейсы, такие как AsCmd TOM, ADOMD.NET.</span><span class="sxs-lookup"><span data-stu-id="066fc-112">hello same applies toocustom applications or other interfaces such as AsCmd, TOM, ADOMD.NET.</span></span> <span data-ttu-id="066fc-113">Эти приложения требуют установки библиотеки hello вручную.</span><span class="sxs-lookup"><span data-stu-id="066fc-113">These applications require manually installing hello libraries.</span></span> <span data-ttu-id="066fc-114">Hello клиентские библиотеки для ручной установки включаются в пакеты дополнительных компонентов SQL Server в качестве распространяемых пакетов.</span><span class="sxs-lookup"><span data-stu-id="066fc-114">hello client libraries for manual installation are included in SQL Server feature packs as distributable packages.</span></span> <span data-ttu-id="066fc-115">Однако эти клиентские библиотеки равноценных toohello версии SQL Server и не может быть hello последняя версия.</span><span class="sxs-lookup"><span data-stu-id="066fc-115">However, these client libraries are tied toohello SQL Server version and may not be hello latest.</span></span>  

<span data-ttu-id="066fc-116">Клиентские библиотеки для клиентских подключений, отличаются от tooconnect необходимые поставщики данных из источника данных tooa сервера Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="066fc-116">Client libraries for client connections are different from data providers required tooconnect from an Azure Analysis Services server tooa data source.</span></span> <span data-ttu-id="066fc-117">toolearn Дополнительные сведения о подключения источника данных, в разделе [подключения источника данных](analysis-services-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="066fc-117">toolearn more about datasource connections, see [Datasource connections](analysis-services-datasource.md).</span></span>

## <a name="download-hello-latest-client-libraries"></a><span data-ttu-id="066fc-118">Загрузить последние библиотеки клиента hello</span><span class="sxs-lookup"><span data-stu-id="066fc-118">Download hello latest client libraries</span></span>  
<span data-ttu-id="066fc-119">Используйте следующие клиентские библиотеки, если в рабочей среде и требующих полностью выпущенных и поддерживаемых версий hello.</span><span class="sxs-lookup"><span data-stu-id="066fc-119">Use hello following client libraries if you are in a production environment and require fully released and supported versions.</span></span>

[<span data-ttu-id="066fc-120">MSOLAP (amd64)</span><span class="sxs-lookup"><span data-stu-id="066fc-120">MSOLAP (amd64)</span></span>](https://go.microsoft.com/fwlink/?linkid=829576)</br><span data-ttu-id="066fc-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span><span class="sxs-lookup"><span data-stu-id="066fc-121">
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</span></span></br><span data-ttu-id="066fc-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span><span class="sxs-lookup"><span data-stu-id="066fc-122">
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</span></span></br><span data-ttu-id="066fc-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span><span class="sxs-lookup"><span data-stu-id="066fc-123">
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="066fc-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="066fc-124">Next steps</span></span>
<span data-ttu-id="066fc-125">[Подключение с помощью Excel](analysis-services-connect-excel.md)  </span><span class="sxs-lookup"><span data-stu-id="066fc-125">[Connect with Excel](analysis-services-connect-excel.md)  </span></span>  
[<span data-ttu-id="066fc-126">Подключение с помощью Power BI</span><span class="sxs-lookup"><span data-stu-id="066fc-126">Connect with Power BI</span></span>](analysis-services-connect-pbi.md)
