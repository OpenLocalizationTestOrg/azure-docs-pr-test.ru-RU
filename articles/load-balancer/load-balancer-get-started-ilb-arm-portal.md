---
title: "aaaCreate внутренний балансировщик нагрузки - портал Azure | Документы Microsoft"
description: "Узнайте, как в диспетчере ресурсов с помощью портала Azure hello подсистемы балансировки нагрузки, toocreate для внутреннего использования"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ac14fb9-8d14-4892-bfe6-8bc74c48ae2c
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 80124217a84857b542eb41cb814ec97234176dd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="5ea86-103">Создать внутренний балансировщик нагрузки в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="5ea86-103">Create an Internal load balancer in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5ea86-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="5ea86-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="5ea86-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ea86-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="5ea86-106">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="5ea86-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="5ea86-107">Шаблон</span><span class="sxs-lookup"><span data-stu-id="5ea86-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="5ea86-108">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5ea86-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="5ea86-109">В этой статье описывается использование модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello [классической модели развертывания](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5ea86-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a><span data-ttu-id="5ea86-110">Приступая к созданию внутреннего балансировщика нагрузки с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="5ea86-110">Get started creating an Internal load balancer using Azure portal</span></span>

<span data-ttu-id="5ea86-111">Используйте следующую toocreate действия внутренний балансировщик нагрузки из портала Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="5ea86-111">Use hello following steps toocreate an internal load balancer from hello Azure Portal.</span></span>

1. <span data-ttu-id="5ea86-112">Откройте браузер, перейдите в каталог toohello [портал Azure](http://portal.azure.com)и выполните вход с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="5ea86-112">Open a browser, navigate toohello [Azure portal](http://portal.azure.com), and sign in with your Azure account.</span></span>
2. <span data-ttu-id="5ea86-113">В hello верхней левой части экрана приветствия, щелкните **New** > **сети** > **балансировки нагрузки**.</span><span class="sxs-lookup"><span data-stu-id="5ea86-113">In hello upper left hand side of hello screen, click **New** > **Networking** > **Load balancer**.</span></span>
3. <span data-ttu-id="5ea86-114">В hello **балансировки нагрузки создать** колонке введите **имя** для балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="5ea86-114">In hello **Create load balancer** blade, enter a **Name** for your load balancer.</span></span>
4. <span data-ttu-id="5ea86-115">В разделе **Схема** щелкните **Внутренний**.</span><span class="sxs-lookup"><span data-stu-id="5ea86-115">Under **Scheme**, click **Internal**.</span></span>
5. <span data-ttu-id="5ea86-116">Нажмите кнопку **виртуальная сеть**, а затем выберите hello место балансировки нагрузки hello toocreate виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="5ea86-116">Click **Virtual network**, and then select hello virtual network where you want toocreate hello load balancer.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5ea86-117">Если требуется toouse виртуальной сети hello не отображается, проверьте hello **расположение** используются для балансировки нагрузки hello и измените его соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="5ea86-117">If you do not see hello virtual network you want toouse, check hello **Location** you are using for hello load balancer, and change it accordingly.</span></span>

6. <span data-ttu-id="5ea86-118">Нажмите кнопку **подсети**, а затем выберите место балансировки нагрузки hello toocreate подсети hello.</span><span class="sxs-lookup"><span data-stu-id="5ea86-118">Click **Subnet**, and then select hello subnet where you want toocreate hello load balancer.</span></span>
7. <span data-ttu-id="5ea86-119">В разделе **назначения IP-адресов**, кнопками **динамическое** или **статических**, в зависимости от того, hello IP-адрес для hello нагрузки балансировки toobe фиксированной (статический) или нет.</span><span class="sxs-lookup"><span data-stu-id="5ea86-119">Under **IP address assignment**, click either **Dynamic** or **Static**, depending on whether you want hello IP address for hello load balancer toobe fixed (static) or not.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5ea86-120">При выборе toouse статический IP-адрес будет иметь tooprovide адрес подсистемы балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="5ea86-120">If you select toouse a static IP address, you will have tooprovide an address for hello load balancer.</span></span>

8. <span data-ttu-id="5ea86-121">В разделе **группы ресурсов** укажите hello имя группы ресурсов для подсистемы балансировки нагрузки hello, или нажмите кнопку **выбрать существующий** и выберите существующую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5ea86-121">Under **Resource group** either specify hello name of a new resource group for hello load balancer, or click **select existing** and select an existing resource group.</span></span>
9. <span data-ttu-id="5ea86-122">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5ea86-122">Click **Create**.</span></span>

## <a name="configure-load-balancing-rules"></a><span data-ttu-id="5ea86-123">Настройка правил балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="5ea86-123">Configure load balancing rules</span></span>

<span data-ttu-id="5ea86-124">После hello загрузить создания балансировки, переходы tooconfigure ресурсов для подсистемы балансировки нагрузки toohello его.</span><span class="sxs-lookup"><span data-stu-id="5ea86-124">After hello load balancer creation, navigate toohello load balancer resource tooconfigure it.</span></span>
<span data-ttu-id="5ea86-125">Требуется tooconfigure сначала пул адресов серверной части и зонда перед настройкой правила балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="5ea86-125">You need tooconfigure first a back-end address pool and a probe before configuring a load balancing rule.</span></span>

### <a name="step-1-configure-a-back-end-pool"></a><span data-ttu-id="5ea86-126">Шаг 1. Настройка внутреннего пула</span><span class="sxs-lookup"><span data-stu-id="5ea86-126">Step 1: Configure a back-end pool</span></span>

1. <span data-ttu-id="5ea86-127">Hello портал Azure, щелкните **Обзор** > **подсистем балансировки нагрузки**, а затем нажмите кнопку hello балансировки нагрузки, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="5ea86-127">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="5ea86-128">В hello **параметры** колонка, щелкните **внутренние пулы**.</span><span class="sxs-lookup"><span data-stu-id="5ea86-128">In hello **Settings** blade, click **Backend pools**.</span></span>
3. <span data-ttu-id="5ea86-129">В hello **серверных пулов адресов** колонка, щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="5ea86-129">In hello **Backend address pools** blade, click **Add**.</span></span>
4. <span data-ttu-id="5ea86-130">В hello **Добавление внутреннего пула** колонке введите **имя** hello внутреннего пула, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5ea86-130">In hello **Add backend pool** blade, enter a **Name** for hello backend pool, and then click **OK**.</span></span>

### <a name="step-2-configure-a-probe"></a><span data-ttu-id="5ea86-131">Шаг 2. Настройка пробы</span><span class="sxs-lookup"><span data-stu-id="5ea86-131">Step 2: Configure a probe</span></span>

1. <span data-ttu-id="5ea86-132">Hello портал Azure, щелкните **Обзор** > **подсистем балансировки нагрузки**, а затем нажмите кнопку hello балансировки нагрузки, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="5ea86-132">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="5ea86-133">В hello **параметры** колонка, щелкните **проверяет**.</span><span class="sxs-lookup"><span data-stu-id="5ea86-133">In hello **Settings** blade, click **Probes**.</span></span>
3. <span data-ttu-id="5ea86-134">В hello **проверяет** колонка, щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="5ea86-134">In hello **Probes**  blade, click **Add**.</span></span>
4. <span data-ttu-id="5ea86-135">В hello **пробы добавить** колонке введите **имя** для пробы hello.</span><span class="sxs-lookup"><span data-stu-id="5ea86-135">In hello **Add probe** blade, enter a **Name** for hello probe.</span></span>
5. <span data-ttu-id="5ea86-136">В разделе **Протокол** выберите **HTTP** (для веб-сайтов) или **TCP** (для других приложений на основе TCP).</span><span class="sxs-lookup"><span data-stu-id="5ea86-136">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="5ea86-137">В разделе **порт**, указывать порт toouse hello, при доступе к пробы hello.</span><span class="sxs-lookup"><span data-stu-id="5ea86-137">Under **Port**, specify hello port toouse when accessing hello probe.</span></span>
7. <span data-ttu-id="5ea86-138">В разделе **путь** (для HTTP только проверки), укажите путь toouse hello в качестве зонда.</span><span class="sxs-lookup"><span data-stu-id="5ea86-138">Under **Path** (for HTTP probes only), specify hello path toouse as a probe.</span></span>
8. <span data-ttu-id="5ea86-139">В разделе **интервал** укажите, как часто tooprobe hello приложения.</span><span class="sxs-lookup"><span data-stu-id="5ea86-139">Under **Interval** specify how frequently tooprobe hello application.</span></span>
9. <span data-ttu-id="5ea86-140">В разделе **порог состояния неработоспособности**, укажите число попыток должно не выполняться hello серверной виртуальной машины будет отмечен как неработоспособный.</span><span class="sxs-lookup"><span data-stu-id="5ea86-140">Under **Unhealthy threshold**, specify how many attempts should fail before hello backend virtual machine is marked as unhealthy.</span></span>
10. <span data-ttu-id="5ea86-141">Нажмите кнопку **ОК** toocreate проверки.</span><span class="sxs-lookup"><span data-stu-id="5ea86-141">Click **OK** toocreate probe.</span></span>

### <a name="step-3-configure-load-balancing-rules"></a><span data-ttu-id="5ea86-142">Шаг 3. Настройка правил балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="5ea86-142">Step 3: Configure load balancing rules</span></span>

1. <span data-ttu-id="5ea86-143">Hello портал Azure, щелкните **Обзор** > **подсистем балансировки нагрузки**, а затем нажмите кнопку hello балансировки нагрузки, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="5ea86-143">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="5ea86-144">В hello **параметры** колонка, щелкните **правила подсистемы балансировки нагрузки**.</span><span class="sxs-lookup"><span data-stu-id="5ea86-144">In hello **Settings** blade, click **Load balancing rules**.</span></span>
3. <span data-ttu-id="5ea86-145">В hello **правила подсистемы балансировки нагрузки** колонка, щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="5ea86-145">In hello **Load balancing rules** blade, click **Add**.</span></span>
4. <span data-ttu-id="5ea86-146">В hello **правило балансировки нагрузки добавить** колонке введите **имя** для правила hello.</span><span class="sxs-lookup"><span data-stu-id="5ea86-146">In hello **Add load balancing rule** blade, enter a **Name** for hello rule.</span></span>
5. <span data-ttu-id="5ea86-147">В разделе **Протокол** выберите **HTTP** (для веб-сайтов) или **TCP** (для других приложений на основе TCP).</span><span class="sxs-lookup"><span data-stu-id="5ea86-147">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="5ea86-148">В разделе **порт**, указать hello порт клиенты подключаются балансировки нагрузки tooin hello.</span><span class="sxs-lookup"><span data-stu-id="5ea86-148">Under **Port**, specify hello port clients connect tooin hello load balancer.</span></span>
7. <span data-ttu-id="5ea86-149">В разделе **внутренний порт**, укажите порт toobe hello, используются в пуле внутренних hello (обычно порт подсистемы балансировки нагрузки hello и внутренний порт hello hello же).</span><span class="sxs-lookup"><span data-stu-id="5ea86-149">Under **Backend port**, specify hello port toobe used in hello backend pool (usually, hello load balancer port and hello backend port are hello same).</span></span>
8. <span data-ttu-id="5ea86-150">В разделе **внутренний пул**выберите hello внутреннего пула, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="5ea86-150">Under **Backend pool**, select hello backend pool you created above.</span></span>
9. <span data-ttu-id="5ea86-151">В разделе **Сохранение сеанса**, укажите, каким должно toopersist сеансы.</span><span class="sxs-lookup"><span data-stu-id="5ea86-151">Under **Session persistence**, select how you want sessions toopersist.</span></span>
10. <span data-ttu-id="5ea86-152">В разделе **время ожидания простоя (в минутах)**, тайм-аут простоя hello.</span><span class="sxs-lookup"><span data-stu-id="5ea86-152">Under **Idle timeout (minutes)**, specify hello idle timeout.</span></span>
11. <span data-ttu-id="5ea86-153">В разделе **Плавающий IP-адрес (для конфигурации с прямым ответом от сервера)** щелкните **Отключен** или **Включен**.</span><span class="sxs-lookup"><span data-stu-id="5ea86-153">Under **Floating IP (direct server return)**, click **Disabled** or **Enabled**.</span></span>
12. <span data-ttu-id="5ea86-154">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="5ea86-154">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ea86-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5ea86-155">Next steps</span></span>

[<span data-ttu-id="5ea86-156">Настройка режима распределения подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="5ea86-156">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="5ea86-157">Настройка параметров времени ожидания простоя TCP для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="5ea86-157">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

