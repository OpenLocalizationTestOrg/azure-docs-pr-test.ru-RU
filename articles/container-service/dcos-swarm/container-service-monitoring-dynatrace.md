---
title: "кластер Azure DC/OS aaaMonitor - Dynatrace | Документы Microsoft"
description: "Мониторинг кластера DC/OS Службы контейнеров Azure с помощью Dynatrace. Развертывание hello Dynatrace OneAgent с помощью панели мониторинга DC/OS hello."
services: container-service
documentationcenter: 
author: MartinGoodwell
manager: 
editor: 
tags: acs, azure-container-service
keywords: "Контейнеры, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 9e2e2d1c8b454422d1db30dac7c385d31d336853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a><span data-ttu-id="fcb91-105">Мониторинг кластера DC/OS в Службе контейнеров Azure с помощью Dynatrace SaaS/Managed</span><span class="sxs-lookup"><span data-stu-id="fcb91-105">Monitor an Azure Container Service DC/OS cluster with Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="fcb91-106">В этой статье мы покажем, как toodeploy hello [Dynatrace](https://www.dynatrace.com/) OneAgent toomonitor все hello агента узлов в кластере служба контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="fcb91-106">In this article, we show you how toodeploy hello [Dynatrace](https://www.dynatrace.com/) OneAgent toomonitor all hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="fcb91-107">Для работы с этой конфигурацией вам понадобится учетная запись с Dynatrace SaaS/Managed.</span><span class="sxs-lookup"><span data-stu-id="fcb91-107">You need an account with Dynatrace SaaS/Managed for this configuration.</span></span> 

## <a name="dynatrace-saasmanaged"></a><span data-ttu-id="fcb91-108">Dynatrace SaaS/Managed</span><span class="sxs-lookup"><span data-stu-id="fcb91-108">Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="fcb91-109">DynaTrace — облачное решение для мониторинга, предназначенное для высокодинамичных сред контейнеров и кластеров.</span><span class="sxs-lookup"><span data-stu-id="fcb91-109">Dynatrace is a cloud-native monitoring solution for highly dynamic container and cluster environments.</span></span> <span data-ttu-id="fcb91-110">Оно позволяет оптимизировать toobetter развертывания контейнера и выделения памяти с помощью данных об использовании в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="fcb91-110">It allows you toobetter optimize your container deployments and memory allocations by using real-time usage data.</span></span> <span data-ttu-id="fcb91-111">Это решение способно автоматически выявлять проблемы приложений и инфраструктуры, обеспечивая автоматизированное задание базовых показателей, обобщение проблем и определение первопричин.</span><span class="sxs-lookup"><span data-stu-id="fcb91-111">It is capable of automatically pinpointing application and infrastructure issues by providing automated baselining, problem correlation, and root-cause detection.</span></span>

<span data-ttu-id="fcb91-112">Hello следующем рисунке показано hello Dynatrace пользовательского интерфейса:</span><span class="sxs-lookup"><span data-stu-id="fcb91-112">hello following figure shows hello Dynatrace UI:</span></span>

![Пользовательский интерфейс Dynatrace](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a><span data-ttu-id="fcb91-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fcb91-114">Prerequisites</span></span> 
<span data-ttu-id="fcb91-115">[Развертывание](container-service-deployment.md) и [подключения](./../container-service-connect.md) tooa кластер настроен службой контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="fcb91-115">[Deploy](container-service-deployment.md) and [connect](./../container-service-connect.md) tooa cluster configured by Azure Container Service.</span></span> <span data-ttu-id="fcb91-116">Просмотр hello [Marathon пользовательского интерфейса](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="fcb91-116">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="fcb91-117">Go слишком[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset Dynatrace SaaS учетной записи.</span><span class="sxs-lookup"><span data-stu-id="fcb91-117">Go too[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset up a Dynatrace SaaS account.</span></span>  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a><span data-ttu-id="fcb91-118">Настройка развертывания Dynatrace с использованием Marathon</span><span class="sxs-lookup"><span data-stu-id="fcb91-118">Configure a Dynatrace deployment with Marathon</span></span>
<span data-ttu-id="fcb91-119">Следующие шаги показывают, как tooconfigure и развернуть кластер tooyour Dynatrace приложений с Marathon.</span><span class="sxs-lookup"><span data-stu-id="fcb91-119">These steps show you how tooconfigure and deploy Dynatrace applications tooyour cluster with Marathon.</span></span>

1. <span data-ttu-id="fcb91-120">Откройте пользовательский интерфейс DC/OS по адресу [http://localhost:80/](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="fcb91-120">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="fcb91-121">Один раз в hello DC/OS пользовательского интерфейса, перехода toohello **Universe** и затем найдите **Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="fcb91-121">Once in hello DC/OS UI, navigate toohello **Universe** tab and then search for **Dynatrace**.</span></span>

    ![Dynatrace на вкладке "Universe" (Вселенная) DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. <span data-ttu-id="fcb91-123">Конфигурация toocomplete hello, необходим учетной записи Dynatrace SaaS бесплатную пробную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="fcb91-123">toocomplete hello configuration, you need a Dynatrace SaaS account or a free trial account.</span></span> <span data-ttu-id="fcb91-124">После входа в панель мониторинга Dynatrace hello выберите **развертывание Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="fcb91-124">Once you log into hello Dynatrace dashboard, select **Deploy Dynatrace**.</span></span>

    ![Настройка интеграции PaaS для Dynatrace](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. <span data-ttu-id="fcb91-126">На странице приветствия выберите **Настройте интеграцию PaaS**.</span><span class="sxs-lookup"><span data-stu-id="fcb91-126">On hello page, select **Set up PaaS integration**.</span></span> 

    ![Маркер API Dynatrace](./media/container-service-monitoring-dynatrace/api-token.png) 

4. <span data-ttu-id="fcb91-128">Введите токен API в конфигурацию Dynatrace OneAgent внутри hello вселенной DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="fcb91-128">Enter your API token into hello Dynatrace OneAgent configuration within hello DC/OS Universe.</span></span> 

    ![Конфигурация dynaTrace OneAgent в hello вселенной DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. <span data-ttu-id="fcb91-130">Номер toohello набора экземпляров hello узлов предполагается toorun.</span><span class="sxs-lookup"><span data-stu-id="fcb91-130">Set hello instances toohello number of nodes you intend toorun.</span></span> <span data-ttu-id="fcb91-131">Установка более высокий номер также работает, но DC/OS попытки будут продолжаться новые экземпляры toofind до достижения этого числа фактически.</span><span class="sxs-lookup"><span data-stu-id="fcb91-131">Setting a higher number also works, but DC/OS will keep trying toofind new instances until that number is actually reached.</span></span> <span data-ttu-id="fcb91-132">При желании можно также задать это значение tooa как 1000000.</span><span class="sxs-lookup"><span data-stu-id="fcb91-132">If you prefer, you can also set this tooa value like 1000000.</span></span> <span data-ttu-id="fcb91-133">В этом случае каждый раз, когда toohello кластер добавляется новый узел, Dynatrace автоматически развертывает агент toothat новый узел, по цене hello постоянно работаем дополнительные экземпляры toodeploy контроллера домена или ОС.</span><span class="sxs-lookup"><span data-stu-id="fcb91-133">In this case, whenever a new node is added toohello cluster, Dynatrace automatically deploys an agent toothat new node, at hello price of DC/OS constantly trying toodeploy further instances.</span></span>

    ![Конфигурация dynaTrace в hello контроллера домена, среда операционной системы-экземпляров](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a><span data-ttu-id="fcb91-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fcb91-135">Next steps</span></span>

<span data-ttu-id="fcb91-136">После установки пакета hello, перейдите назад toohello Dynatrace мониторинга.</span><span class="sxs-lookup"><span data-stu-id="fcb91-136">Once you've installed hello package, navigate back toohello Dynatrace dashboard.</span></span> <span data-ttu-id="fcb91-137">Вы можете просмотреть hello метрики использования разных контейнеров hello в пределах кластера.</span><span class="sxs-lookup"><span data-stu-id="fcb91-137">You can explore hello different usage metrics for hello containers within your cluster.</span></span> 
