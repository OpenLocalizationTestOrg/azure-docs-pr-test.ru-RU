---
title: "Устранение прерывания работы служб с помощью заданий Azure Stream Analytics | Документация Майкрософт"
description: "Руководство по обеспечению надежности заданий Stream Analytics при установке новых версий служб."
services: stream-analytics
documentationCenter: 
authors: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3ac65c93ecb47e93e963dd9869a7af70f73b19c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a><span data-ttu-id="e2a9e-103">Обеспечение надежности заданий Stream Analytics во время обновления служб</span><span class="sxs-lookup"><span data-stu-id="e2a9e-103">Guarantee Stream Analytics job reliability during service updates</span></span>

<span data-ttu-id="e2a9e-104">Выполняется полностью управляемую службу входит hello возможность toointroduce новые функции, службы и улучшения в быструю темпе.</span><span class="sxs-lookup"><span data-stu-id="e2a9e-104">Part of being a fully managed service is hello capability toointroduce new service functionality and improvements at a rapid pace.</span></span> <span data-ttu-id="e2a9e-105">Это позволяет Stream Analytics осуществлять обновление служб еженедельно (или даже чаще).</span><span class="sxs-lookup"><span data-stu-id="e2a9e-105">As a result, Stream Analytics can have a service update deploy on a weekly (or more frequent) basis.</span></span> <span data-ttu-id="e2a9e-106">Независимо от того, какую часть тестирования выполняется по-прежнему есть риск, что существующий, выполнение задания может быть поврежден из-за появлением toohello ошибки.</span><span class="sxs-lookup"><span data-stu-id="e2a9e-106">No matter how much testing is done there is still a risk that an existing, running job may break due toohello introduction of a bug.</span></span> <span data-ttu-id="e2a9e-107">Для пользователей, выполняющих важные потоковых заданий обработки этих рисков должны избегать toobe.</span><span class="sxs-lookup"><span data-stu-id="e2a9e-107">For customers who run critical streaming processing jobs these risks need toobe avoided.</span></span> <span data-ttu-id="e2a9e-108">Механизм клиенты могут использовать tooreduce этот риск будет Azure  **[парном регионе](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  модели.</span><span class="sxs-lookup"><span data-stu-id="e2a9e-108">A mechanism customers can use tooreduce this risk is Azure’s **[paired region](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** model.</span></span> 

## <a name="how-do-azure-paired-regions-address-this-concern"></a><span data-ttu-id="e2a9e-109">Как сопряженные регионы Azure помогают устранить эту проблему?</span><span class="sxs-lookup"><span data-stu-id="e2a9e-109">How do Azure paired regions address this concern?</span></span>

<span data-ttu-id="e2a9e-110">Stream Analytics гарантирует, что задания в сопряженных регионах обновляются в разных пакетах.</span><span class="sxs-lookup"><span data-stu-id="e2a9e-110">Stream Analytics guarantees jobs in paired regions are updated in separate batches.</span></span> <span data-ttu-id="e2a9e-111">В результате имеется достаточно временной промежуток между обновлениями hello tooidentify потенциальных критические ошибки и исправлять их.</span><span class="sxs-lookup"><span data-stu-id="e2a9e-111">As a result there is a sufficient time gap between hello updates tooidentify potential breaking bugs and remediate them.</span></span>

<span data-ttu-id="e2a9e-112">_За исключением hello из центральной Индии_ (которого парном регионе, Южной Индии и не имеет присутствия Stream Analytics), hello развертывания обновления tooStream Analytics не будет находиться во hello одновременную в набор парных регионов.</span><span class="sxs-lookup"><span data-stu-id="e2a9e-112">_With hello exception of Central India_ (whose paired region, South India, does not have Stream Analytics presence), hello deployment of an update tooStream Analytics would not occur at hello same time in a set of paired regions.</span></span> <span data-ttu-id="e2a9e-113">Развертывание в нескольких регионах **в hello одной группе** может возникнуть **в hello одновременно**.</span><span class="sxs-lookup"><span data-stu-id="e2a9e-113">Deployments in multiple regions **in hello same group** may occur **at hello same time**.</span></span>

<span data-ttu-id="e2a9e-114">Hello статьи на  **[доступности и парных регионов](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  имеет hello наиболее актуальные сведения, в которой сопоставляются области.</span><span class="sxs-lookup"><span data-stu-id="e2a9e-114">hello article on **[availability and paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** has hello most up-to-date information on which regions are paired.</span></span>

<span data-ttu-id="e2a9e-115">Клиенты, желательно toodeploy идентичные задания tooboth пару областей.</span><span class="sxs-lookup"><span data-stu-id="e2a9e-115">Customers are advised toodeploy identical jobs tooboth paired regions.</span></span> <span data-ttu-id="e2a9e-116">В дополнение к этому tooStream Analytics внутренней мониторингу, клиентов, также рекомендуется toomonitor hello задания как если бы **оба** рабочих заданий.</span><span class="sxs-lookup"><span data-stu-id="e2a9e-116">In addition tooStream Analytics internal monitoring capabilities, customers are also advised toomonitor hello jobs as if **both** are production jobs.</span></span> <span data-ttu-id="e2a9e-117">Если разрыв идентифицированных toobe результат обновления службы Stream Analytics hello, повышать уровень соответствующим образом и перенести никаких выходных данных задания работоспособное toohello потребителей потока данных.</span><span class="sxs-lookup"><span data-stu-id="e2a9e-117">If a break is identified toobe a result of hello Stream Analytics service update, escalate appropriately and fail over any downstream consumers toohello healthy job output.</span></span> <span data-ttu-id="e2a9e-118">Укрупнение toosupport предотвращения влияния, новое развертывание hello парном регионе hello и сохраняет целостность hello hello пару заданий.</span><span class="sxs-lookup"><span data-stu-id="e2a9e-118">Escalation toosupport will prevent hello paired region from being affected by hello new deployment and maintain hello integrity of hello paired jobs.</span></span>
