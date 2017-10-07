---
title: "aaaPorts за пределы 1433 для базы данных SQL | Документы Microsoft"
description: "Подключения клиентов из tooAzure ADO.NET базы данных SQL иногда использование прокси-сервера hello и взаимодействовать непосредственно с базой данных hello. Порты, отличные от 1433, становятся важными."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.assetid: 3f17106a-92fd-4aa4-b6a9-1daa29421f64
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: a35ff2d827ae3fa29b3ea855dbb7ed78583c82eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a><span data-ttu-id="e3d0e-104">Порты для ADO.NET 4.5, отличные от порта 1433</span><span class="sxs-lookup"><span data-stu-id="e3d0e-104">Ports beyond 1433 for ADO.NET 4.5</span></span>
<span data-ttu-id="e3d0e-105">В этом разделе описываются hello работу подключения к базе данных SQL Azure для клиентов, использующих ADO.NET 4.5 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e3d0e-105">This topic describes hello Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e3d0e-106">Сведения об архитектуре подключения см. в статье [Azure SQL Database Connectivity Architecture](sql-database-connectivity-architecture.md) (Архитектура подключения базы данных SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="e3d0e-106">For information about connectivity architecture, see [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md).</span></span>
>

## <a name="outside-vs-inside"></a><span data-ttu-id="e3d0e-107">Снаружи или внутри</span><span class="sxs-lookup"><span data-stu-id="e3d0e-107">Outside vs inside</span></span>
<span data-ttu-id="e3d0e-108">Для подключения tooAzure базы данных SQL, мы должны запросить запускается ли клиентская программа *за пределами* или *внутри* границ hello облако Azure.</span><span class="sxs-lookup"><span data-stu-id="e3d0e-108">For connections tooAzure SQL Database, we must first ask whether your client program runs *outside* or *inside* hello Azure cloud boundary.</span></span> <span data-ttu-id="e3d0e-109">Hello подразделах рассматриваются два распространенных сценария.</span><span class="sxs-lookup"><span data-stu-id="e3d0e-109">hello subsections discuss two common scenarios.</span></span>

#### <a name="outside-client-runs-on-your-desktop-computer"></a><span data-ttu-id="e3d0e-110">*Внешняя программа.* Клиент работает на настольном компьютере</span><span class="sxs-lookup"><span data-stu-id="e3d0e-110">*Outside:* Client runs on your desktop computer</span></span>
<span data-ttu-id="e3d0e-111">Порт 1433 — hello только порт, который должен быть открыт на компьютере, на котором размещена база данных SQL клиентское приложение.</span><span class="sxs-lookup"><span data-stu-id="e3d0e-111">Port 1433 is hello only port that must be open on your desktop computer that hosts your SQL Database client application.</span></span>

#### <a name="inside-client-runs-on-azure"></a><span data-ttu-id="e3d0e-112">*Внутренняя программа.* Клиент работает в Azure</span><span class="sxs-lookup"><span data-stu-id="e3d0e-112">*Inside:* Client runs on Azure</span></span>
<span data-ttu-id="e3d0e-113">При запуске клиента внутри границы hello облако Azure использует так мы называем *прямого маршрута* toointeract с hello базы данных SQL server.</span><span class="sxs-lookup"><span data-stu-id="e3d0e-113">When your client runs inside hello Azure cloud boundary, it uses what we can call a *direct route* toointeract with hello SQL Database server.</span></span> <span data-ttu-id="e3d0e-114">После установления соединения для дальнейшего взаимодействия между клиентом hello и базы данных включает в себя без прокси-сервера по промежуточного слоя.</span><span class="sxs-lookup"><span data-stu-id="e3d0e-114">After a connection is established, further interactions between hello client and database involve no middleware proxy.</span></span>

<span data-ttu-id="e3d0e-115">последовательность Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e3d0e-115">hello sequence is as follows:</span></span>

1. <span data-ttu-id="e3d0e-116">ADO.NET 4.5 (или более поздней версии) инициирует краткое взаимодействие с hello облако Azure и получает номер динамически определенного порта.</span><span class="sxs-lookup"><span data-stu-id="e3d0e-116">ADO.NET 4.5 (or later) initiates a brief interaction with hello Azure cloud, and receives a dynamically identified port number.</span></span>
   
   * <span data-ttu-id="e3d0e-117">Hello динамически определяемого используется порт в диапазоне hello 11000 11999 или 14000 14999.</span><span class="sxs-lookup"><span data-stu-id="e3d0e-117">hello dynamically identified port number is in hello range of 11000-11999 or 14000-14999.</span></span>
2. <span data-ttu-id="e3d0e-118">ADO.NET затем подключается toohello базы данных SQL server напрямую, не по промежуточного слоя между ними.</span><span class="sxs-lookup"><span data-stu-id="e3d0e-118">ADO.NET then connects toohello SQL Database server directly, with no middleware in between.</span></span>
3. <span data-ttu-id="e3d0e-119">Запросы отправляются напрямую toohello базы данных, а результаты возвращаются непосредственно toohello клиента.</span><span class="sxs-lookup"><span data-stu-id="e3d0e-119">Queries are sent directly toohello database, and results are returned directly toohello client.</span></span>

<span data-ttu-id="e3d0e-120">Убедитесь, что порта hello, диапазонов 11000 11999 и 14000-14999 на компьютере клиента Azure, остаются доступными для взаимодействия клиента ADO.NET 4.5 с базой данных SQL.</span><span class="sxs-lookup"><span data-stu-id="e3d0e-120">Ensure that hello port ranges of 11000-11999 and 14000-14999 on your Azure client machine are left available for ADO.NET 4.5 client interactions with SQL Database.</span></span>

* <span data-ttu-id="e3d0e-121">В частности должно быть никаких других исходящих препятствия порты из диапазона hello.</span><span class="sxs-lookup"><span data-stu-id="e3d0e-121">In particular, ports in hello range must be free of any other outbound blockers.</span></span>
* <span data-ttu-id="e3d0e-122">На ВМ Azure, hello **брандмауэр Windows в режиме повышенной безопасности** элементы управления hello параметры порта.</span><span class="sxs-lookup"><span data-stu-id="e3d0e-122">On your Azure VM, hello **Windows Firewall with Advanced Security** controls hello port settings.</span></span>
  
  * <span data-ttu-id="e3d0e-123">Можно использовать hello [брандмауэра пользовательский интерфейс](http://msdn.microsoft.com/library/cc646023.aspx) tooadd a правило, для которого указывается hello **TCP** как протокол, а также диапазон портов с синтаксисом hello **11000 11999**.</span><span class="sxs-lookup"><span data-stu-id="e3d0e-123">You can use hello [firewall's user interface](http://msdn.microsoft.com/library/cc646023.aspx) tooadd a rule for which you specify hello **TCP** protocol along with a port range with hello syntax like **11000-11999**.</span></span>

## <a name="version-clarifications"></a><span data-ttu-id="e3d0e-124">Уточнение версии</span><span class="sxs-lookup"><span data-stu-id="e3d0e-124">Version clarifications</span></span>
<span data-ttu-id="e3d0e-125">В этом разделе поясняются моникеров hello, которые ссылаются tooproduct версии.</span><span class="sxs-lookup"><span data-stu-id="e3d0e-125">This section clarifies hello monikers that refer tooproduct versions.</span></span> <span data-ttu-id="e3d0e-126">В нем также перечисляются некоторые пары версий продуктов.</span><span class="sxs-lookup"><span data-stu-id="e3d0e-126">It also lists some pairings of versions between products.</span></span>

#### <a name="adonet"></a><span data-ttu-id="e3d0e-127">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="e3d0e-127">ADO.NET</span></span>
* <span data-ttu-id="e3d0e-128">ADO.NET 4.0 поддерживает протокол TDS 7.3 hello, но не 7.4.</span><span class="sxs-lookup"><span data-stu-id="e3d0e-128">ADO.NET 4.0 supports hello TDS 7.3 protocol, but not 7.4.</span></span>
* <span data-ttu-id="e3d0e-129">ADO.NET 4.5 и более поздних версий поддерживает протокол TDS 7.4 hello.</span><span class="sxs-lookup"><span data-stu-id="e3d0e-129">ADO.NET 4.5 and later supports hello TDS 7.4 protocol.</span></span>

## <a name="related-links"></a><span data-ttu-id="e3d0e-130">Связанные ссылки</span><span class="sxs-lookup"><span data-stu-id="e3d0e-130">Related links</span></span>
* <span data-ttu-id="e3d0e-131">20 июля 2015 г. был выпущен ADO.NET 4.6.</span><span class="sxs-lookup"><span data-stu-id="e3d0e-131">ADO.NET 4.6 was released on July 20, 2015.</span></span> <span data-ttu-id="e3d0e-132">Доступно с извещение блога от службы технической поддержки .NET hello [здесь](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3d0e-132">A blog announcement from hello .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span></span>
* <span data-ttu-id="e3d0e-133">15 августа 2012 г. был выпущен ADO.NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="e3d0e-133">ADO.NET 4.5 was released on August 15, 2012.</span></span> <span data-ttu-id="e3d0e-134">Доступно с извещение блога от службы технической поддержки .NET hello [здесь](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3d0e-134">A blog announcement from hello .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span></span>
  
  * <span data-ttu-id="e3d0e-135">Запись блога об ADO.NET 4.5.1 доступна [здесь](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3d0e-135">A blog post about ADO.NET 4.5.1 is available [here](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span></span>
* [<span data-ttu-id="e3d0e-136">Список версий протокола TDS</span><span class="sxs-lookup"><span data-stu-id="e3d0e-136">TDS protocol version list</span></span>](http://www.freetds.org/userguide/tdshistory.htm)
* [<span data-ttu-id="e3d0e-137">Общие сведения о разработке базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="e3d0e-137">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="e3d0e-138">Брандмауэр базы данных SQL Azure</span><span class="sxs-lookup"><span data-stu-id="e3d0e-138">Azure SQL Database firewall</span></span>](sql-database-firewall-configure.md)
* [<span data-ttu-id="e3d0e-139">Практическое руководство. Настройка параметров брандмауэра для Базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="e3d0e-139">How to: Configure firewall settings on SQL Database</span></span>](sql-database-configure-firewall-settings.md)

