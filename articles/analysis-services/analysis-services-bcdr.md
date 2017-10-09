---
title: "aaaAzure высокий уровень доступности служб Analysis Services | Документы Microsoft"
description: "Обеспечение высокой доступности служб Analysis Services Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 6e09536c5bd7dc7f88f9b662e1a9f42d2b8c969b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analysis-services-high-availability"></a><span data-ttu-id="a96d5-103">Высокая доступность служб Analysis Services</span><span class="sxs-lookup"><span data-stu-id="a96d5-103">Analysis Services high availability</span></span>
<span data-ttu-id="a96d5-104">Эта статья описывает обеспечение высокой доступности для серверов служб Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="a96d5-104">This article describes assuring high availability for Azure Analysis Services servers.</span></span> 


## <a name="assuring-high-availability-during-a-service-disruption"></a><span data-ttu-id="a96d5-105">Обеспечение высокой доступности во время перерывов в обслуживании</span><span class="sxs-lookup"><span data-stu-id="a96d5-105">Assuring high availability during a service disruption</span></span>
<span data-ttu-id="a96d5-106">В редких случаях возможен сбой центра обработки данных Azure.</span><span class="sxs-lookup"><span data-stu-id="a96d5-106">While rare, an Azure data center can have an outage.</span></span> <span data-ttu-id="a96d5-107">Он вызывает нарушение работы организации, которое может длиться от считанных минут до нескольких часов.</span><span class="sxs-lookup"><span data-stu-id="a96d5-107">When an outage occurs, it causes a business disruption that might last a few minutes or might last for hours.</span></span> <span data-ttu-id="a96d5-108">Высокая доступность чаще всего достигается за счет избыточности сервера.</span><span class="sxs-lookup"><span data-stu-id="a96d5-108">High availability is most often achieved with server redundancy.</span></span> <span data-ttu-id="a96d5-109">При работе со службами Azure Analysis Services избыточности можно добиться путем создания дополнительных серверов-получателей в одном или нескольких регионах.</span><span class="sxs-lookup"><span data-stu-id="a96d5-109">With Azure Analysis Services, you can achieve redundancy by creating additional, secondary servers in one or more regions.</span></span> <span data-ttu-id="a96d5-110">При создании избыточных серверов, tooassure hello данные и метаданные на этих серверах в синхронизации с сервером hello в регионе, которое вышло вне сети, вы можете:</span><span class="sxs-lookup"><span data-stu-id="a96d5-110">When creating redundant servers, tooassure hello data and metadata on those servers is in-sync with hello server in a region that has gone offline, you can:</span></span>

* <span data-ttu-id="a96d5-111">Развертывание серверов tooredundant модели в других регионах.</span><span class="sxs-lookup"><span data-stu-id="a96d5-111">Deploy models tooredundant servers in other regions.</span></span> <span data-ttu-id="a96d5-112">При таком методе для обеспечения общей синхронизации требуется параллельная обработка данных как на сервере-источнике, так и на избыточных серверах.</span><span class="sxs-lookup"><span data-stu-id="a96d5-112">This method requires processing data on both your primary server and redundant servers in-parallel, assuring all servers are in-sync.</span></span>

* <span data-ttu-id="a96d5-113">Заархивируйте базы данных с сервера-источника и восстановите их на избыточных серверах.</span><span class="sxs-lookup"><span data-stu-id="a96d5-113">Back up databases from your primary server and restore on redundant servers.</span></span> <span data-ttu-id="a96d5-114">Например можно автоматизировать хранилища tooAzure ночного резервного копирования и восстановления tooother избыточных серверов в других регионах.</span><span class="sxs-lookup"><span data-stu-id="a96d5-114">For example, you can automate nightly backups tooAzure storage, and restore tooother redundant servers in other regions.</span></span> 

<span data-ttu-id="a96d5-115">В любом случае если основной сервер отключается сбоя, необходимо изменить hello строки подключения в reporting server toohello tooconnect клиентов в разных регионального центра обработки данных.</span><span class="sxs-lookup"><span data-stu-id="a96d5-115">In either case, if your primary server experiences an outage, you must change hello connection strings in reporting clients tooconnect toohello server in a different regional datacenter.</span></span> <span data-ttu-id="a96d5-116">Такое изменение следует рассматривать как крайнюю меру на случай катастрофического сбоя в региональном центре обработки данных.</span><span class="sxs-lookup"><span data-stu-id="a96d5-116">This change should be considered a last resort and only if a catastrophic regional data center outage occurs.</span></span> <span data-ttu-id="a96d5-117">Вероятнее всего, центр с вашим сервером-источником возобновит работу до того, как вы внесете изменения для всех клиентов.</span><span class="sxs-lookup"><span data-stu-id="a96d5-117">It's more likely a data center outage hosting your primary server would come back online before you could update connections on all clients.</span></span> 



## <a name="related-information"></a><span data-ttu-id="a96d5-118">Связанные сведения</span><span class="sxs-lookup"><span data-stu-id="a96d5-118">Related information</span></span>
<span data-ttu-id="a96d5-119">[Архивация и восстановление](analysis-services-backup.md) </span><span class="sxs-lookup"><span data-stu-id="a96d5-119">[Backup and restore](analysis-services-backup.md) </span></span>  
[<span data-ttu-id="a96d5-120">Управление службами Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="a96d5-120">Manage Azure Analysis Services</span></span>](analysis-services-manage.md) 

