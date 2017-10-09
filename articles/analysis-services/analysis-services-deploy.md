---
title: "tooAzure aaaDeploy служб Analysis Services с помощью SSDT | Документы Microsoft"
description: "Узнайте, как toodeploy tooan табличной модели Azure служб Analysis Services с помощью SSDT."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a><span data-ttu-id="c23dc-103">Развертывание модели из SSDT</span><span class="sxs-lookup"><span data-stu-id="c23dc-103">Deploy a model from SSDT</span></span>
<span data-ttu-id="c23dc-104">После создания сервера в вашей подписке Azure, вы готовы toodeploy tooit базы данных табличной модели.</span><span class="sxs-lookup"><span data-stu-id="c23dc-104">Once you've created a server in your Azure subscription, you're ready toodeploy a tabular model database tooit.</span></span> <span data-ttu-id="c23dc-105">Можно использовать SQL Server Data Tools (SSDT) toobuild и развертывание проекта табличной модели, над которым вы работаете.</span><span class="sxs-lookup"><span data-stu-id="c23dc-105">You can use SQL Server Data Tools (SSDT) toobuild and deploy a tabular model project you're working on.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c23dc-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c23dc-106">Prerequisites</span></span>
<span data-ttu-id="c23dc-107">tooget работы, необходимо:</span><span class="sxs-lookup"><span data-stu-id="c23dc-107">tooget started, you need:</span></span>

* <span data-ttu-id="c23dc-108">**Сервер Analysis Services** в Azure.</span><span class="sxs-lookup"><span data-stu-id="c23dc-108">**Analysis Services server** in Azure.</span></span> <span data-ttu-id="c23dc-109">toolearn более, в разделе [создать сервер служб Azure Analysis Services](analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="c23dc-109">toolearn more, see [Create an Azure Analysis Services server](analysis-services-create-server.md).</span></span>
* <span data-ttu-id="c23dc-110">**Проект табличной модели** в SSDT или существующей табличной модели hello 1200 или высоким уровнем совместимости.</span><span class="sxs-lookup"><span data-stu-id="c23dc-110">**Tabular model project** in SSDT or an existing tabular model at hello 1200 or higher compatibility level.</span></span> <span data-ttu-id="c23dc-111">Не создавали такую модель ранее?</span><span class="sxs-lookup"><span data-stu-id="c23dc-111">Never created one?</span></span> <span data-ttu-id="c23dc-112">Повторите hello [учебник по Adventure Works Интернет продаж табличного моделирования](https://msdn.microsoft.com/library/hh231691.aspx).</span><span class="sxs-lookup"><span data-stu-id="c23dc-112">Try hello [Adventure Works Internet sales tabular modeling tutorial](https://msdn.microsoft.com/library/hh231691.aspx).</span></span>
* <span data-ttu-id="c23dc-113">**Локальный шлюз** -Если один или несколько источников данных в локальной сети вашей организации, необходимо tooinstall [локального шлюза данных](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="c23dc-113">**On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span> <span data-ttu-id="c23dc-114">Hello шлюз необходим для tooyour локальной данных источников tooprocess и обновления данных в модели hello подключиться к серверу в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="c23dc-114">hello gateway is necessary for your server in hello cloud connect tooyour on-premises data sources tooprocess and refresh data in hello model.</span></span>

> [!TIP]
> <span data-ttu-id="c23dc-115">Перед развертыванием, убедитесь, что может обрабатывать данные hello в таблицах.</span><span class="sxs-lookup"><span data-stu-id="c23dc-115">Before you deploy, make sure you can process hello data in your tables.</span></span> <span data-ttu-id="c23dc-116">В средстве SSDT последовательно выберите элементы **Модель** > **Обработать** > **Обработать все**.</span><span class="sxs-lookup"><span data-stu-id="c23dc-116">In SSDT, click **Model** > **Process** > **Process All**.</span></span> <span data-ttu-id="c23dc-117">Если обработка завершается сбоем, вы не сможете выполнить развертывание.</span><span class="sxs-lookup"><span data-stu-id="c23dc-117">If processing fails, you cannot successfully deploy.</span></span>
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a><span data-ttu-id="c23dc-118">toodeploy табличной модели из SSDT</span><span class="sxs-lookup"><span data-stu-id="c23dc-118">toodeploy a tabular model from SSDT</span></span>

1. <span data-ttu-id="c23dc-119">Перед развертыванием, нужно имя сервера tooget hello.</span><span class="sxs-lookup"><span data-stu-id="c23dc-119">Before you deploy, you need tooget hello server name.</span></span> <span data-ttu-id="c23dc-120">В **портал Azure** > сервера > **Обзор** > **имя сервера**, имя сервера hello копирования.</span><span class="sxs-lookup"><span data-stu-id="c23dc-120">In **Azure portal** > server > **Overview** > **Server name**, copy hello server name.</span></span>
   
    ![Получение имени сервера в Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="c23dc-122">В SSDT > **обозревателе решений**, щелкните правой кнопкой мыши проект hello > **свойства**.</span><span class="sxs-lookup"><span data-stu-id="c23dc-122">In SSDT > **Solution Explorer**, right-click hello project > **Properties**.</span></span> <span data-ttu-id="c23dc-123">Затем в **развертывания** > **сервера** вставьте имя сервера hello.</span><span class="sxs-lookup"><span data-stu-id="c23dc-123">Then in **Deployment** > **Server** paste hello server name.</span></span>   
   
    ![Вставьте имя сервера в свойства сервера развертывания](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. <span data-ttu-id="c23dc-125">В окне **Обозреватель решений** щелкните правой кнопкой мыши элемент **Свойства** и выберите команду **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="c23dc-125">In **Solution Explorer**, right-click **Properties**, then click **Deploy**.</span></span> <span data-ttu-id="c23dc-126">Возможно, запрошенные toosign в tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c23dc-126">You may be prompted toosign in tooAzure.</span></span>
   
    ![Развертывание tooserver](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    <span data-ttu-id="c23dc-128">Состояние развертывания отображается в окне вывода обоих hello и в развертывание.</span><span class="sxs-lookup"><span data-stu-id="c23dc-128">Deployment status appears in both hello Output window and in Deploy.</span></span>
   
    ![Состояния развертывания](./media/analysis-services-deploy/aas-deploy-status.png)

<span data-ttu-id="c23dc-130">Это все, имеется tooit!</span><span class="sxs-lookup"><span data-stu-id="c23dc-130">That's all there is tooit!</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="c23dc-131">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="c23dc-131">Troubleshooting</span></span>
<span data-ttu-id="c23dc-132">Если происходит сбой развертывания при развертывании метаданных, вполне вероятно, так как SSDT не удалось подключиться к серверу tooyour.</span><span class="sxs-lookup"><span data-stu-id="c23dc-132">If deployment fails when deploying metadata, it's likely because SSDT couldn't connect tooyour server.</span></span> <span data-ttu-id="c23dc-133">Убедитесь, что можно подключить сервер tooyour, с помощью среды SSMS.</span><span class="sxs-lookup"><span data-stu-id="c23dc-133">Make sure you can connect tooyour server using SSMS.</span></span> <span data-ttu-id="c23dc-134">Убедитесь в правильности hello свойства сервера развертывания для проекта hello.</span><span class="sxs-lookup"><span data-stu-id="c23dc-134">Then make sure hello Deployment Server property for hello project is correct.</span></span>

<span data-ttu-id="c23dc-135">Если развертывание завершается ошибкой на таблице, вполне вероятно, так как серверу не удалось подключиться к tooa источника данных.</span><span class="sxs-lookup"><span data-stu-id="c23dc-135">If deployment fails on a table, it's likely because your server couldn't connect tooa data source.</span></span> <span data-ttu-id="c23dc-136">Если источником данных является локальной в сети вашей организации, быть убедиться, что tooinstall [локального шлюза данных](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="c23dc-136">If your data source is on-premises in your organization's network, be sure tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c23dc-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c23dc-137">Next steps</span></span>
<span data-ttu-id="c23dc-138">Теперь, когда сервер tooyour развернутой табличной модели, вы готовы tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="c23dc-138">Now that you have your tabular model deployed tooyour server, you're ready tooconnect tooit.</span></span> <span data-ttu-id="c23dc-139">Вы можете [подключитесь к SSMS tooit](analysis-services-manage.md) toomanage его.</span><span class="sxs-lookup"><span data-stu-id="c23dc-139">You can [connect tooit with SSMS](analysis-services-manage.md) toomanage it.</span></span> <span data-ttu-id="c23dc-140">И вы можете [подключиться с помощью клиентского средства tooit](analysis-services-connect.md) , такие как Power BI, Power BI Desktop или Excel и начала создания отчетов.</span><span class="sxs-lookup"><span data-stu-id="c23dc-140">And, you can [connect tooit using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.</span></span>

