---
title: "приложение контейнера DC/OS tooAzure доступа aaaEnable | Документы Microsoft"
description: "Как tooenable общий доступ к tooDC/OS контейнеры в контейнере службы Azure."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 1ba251ba5a176a6a5e1c7831655164e380a62b27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-public-access-tooan-azure-container-service-application"></a><span data-ttu-id="1f06c-104">Включение общего доступа tooan Azure контейнера службы приложения</span><span class="sxs-lookup"><span data-stu-id="1f06c-104">Enable public access tooan Azure Container Service application</span></span>
<span data-ttu-id="1f06c-105">Любой контроллер домена/OS контейнера в hello ACS [пул общих агентов](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) автоматически предоставляется toohello является Интернет.</span><span class="sxs-lookup"><span data-stu-id="1f06c-105">Any DC/OS container in hello ACS [public agent pool](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) is automatically exposed toohello internet.</span></span> <span data-ttu-id="1f06c-106">По умолчанию порты **80**, **443**, **8080** открыты, поэтому можно получить доступ к любым контейнерам (частным), выполняющим прослушивание на этих портах.</span><span class="sxs-lookup"><span data-stu-id="1f06c-106">By default, ports **80**, **443**, **8080** are opened, and any (public) container listening on those ports are accessible.</span></span> <span data-ttu-id="1f06c-107">В этой статье показано, как tooopen более портов для приложений в службе контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="1f06c-107">This article shows you how tooopen more ports for your applications in Azure Container Service.</span></span>

## <a name="open-a-port-portal"></a><span data-ttu-id="1f06c-108">Открытие порта (портал)</span><span class="sxs-lookup"><span data-stu-id="1f06c-108">Open a port (portal)</span></span>
<span data-ttu-id="1f06c-109">Во-первых мы должны tooopen hello порт, к которому мы хотим.</span><span class="sxs-lookup"><span data-stu-id="1f06c-109">First, we need tooopen hello port we want.</span></span>

1. <span data-ttu-id="1f06c-110">Войдите в портал toohello.</span><span class="sxs-lookup"><span data-stu-id="1f06c-110">Log in toohello portal.</span></span>
2. <span data-ttu-id="1f06c-111">Найти группу ресурсов hello развернутым hello контейнера службы Azure.</span><span class="sxs-lookup"><span data-stu-id="1f06c-111">Find hello resource group that you deployed hello Azure Container Service to.</span></span>
3. <span data-ttu-id="1f06c-112">Выберите подсистемы балансировки нагрузки агента hello (которая называется аналогичные слишком**XXXX-агента-балансировки нагрузки XXXX**).</span><span class="sxs-lookup"><span data-stu-id="1f06c-112">Select hello agent load balancer (which is named similar too**XXXX-agent-lb-XXXX**).</span></span>
   
    ![балансировщик нагрузки Службы контейнеров Azure](./media/container-service-enable-public-access/agent-load-balancer.png)
4. <span data-ttu-id="1f06c-114">Щелкните **Зонды**, а затем — **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1f06c-114">Click **Probes** and then **Add**.</span></span>
   
    ![зонды балансировщика нагрузки Службы контейнеров Azure](./media/container-service-enable-public-access/add-probe.png)
5. <span data-ttu-id="1f06c-116">Заполните форму проверки hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1f06c-116">Fill out hello probe form and click **OK**.</span></span>
   
   | <span data-ttu-id="1f06c-117">Поле</span><span class="sxs-lookup"><span data-stu-id="1f06c-117">Field</span></span> | <span data-ttu-id="1f06c-118">Описание</span><span class="sxs-lookup"><span data-stu-id="1f06c-118">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="1f06c-119">Имя</span><span class="sxs-lookup"><span data-stu-id="1f06c-119">Name</span></span> |<span data-ttu-id="1f06c-120">Описательное имя пробы hello.</span><span class="sxs-lookup"><span data-stu-id="1f06c-120">A descriptive name of hello probe.</span></span> |
   | <span data-ttu-id="1f06c-121">Порт</span><span class="sxs-lookup"><span data-stu-id="1f06c-121">Port</span></span> |<span data-ttu-id="1f06c-122">порт Hello tootest hello контейнера.</span><span class="sxs-lookup"><span data-stu-id="1f06c-122">hello port of hello container tootest.</span></span> |
   | <span data-ttu-id="1f06c-123">Путь</span><span class="sxs-lookup"><span data-stu-id="1f06c-123">Path</span></span> |<span data-ttu-id="1f06c-124">(Если в режиме HTTP) hello tooprobe путь относительный веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="1f06c-124">(When in HTTP mode) hello relative website path tooprobe.</span></span> <span data-ttu-id="1f06c-125">HTTPS не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="1f06c-125">HTTPS not supported.</span></span> |
   | <span data-ttu-id="1f06c-126">Интервал</span><span class="sxs-lookup"><span data-stu-id="1f06c-126">Interval</span></span> |<span data-ttu-id="1f06c-127">пытается Hello промежуток времени между проверки в секундах.</span><span class="sxs-lookup"><span data-stu-id="1f06c-127">hello amount of time between probe attempts, in seconds.</span></span> |
   | <span data-ttu-id="1f06c-128">Пороговое значение сбоя</span><span class="sxs-lookup"><span data-stu-id="1f06c-128">Unhealthy threshold</span></span> |<span data-ttu-id="1f06c-129">Количество пробных последовательных попыток перед неисправной hello контейнера.</span><span class="sxs-lookup"><span data-stu-id="1f06c-129">Number of consecutive probe attempts before considering hello container unhealthy.</span></span> |
6. <span data-ttu-id="1f06c-130">Назад в свойства hello подсистемы балансировки нагрузки hello агента, нажмите кнопку **правила подсистемы балансировки нагрузки** и затем **добавить**.</span><span class="sxs-lookup"><span data-stu-id="1f06c-130">Back at hello properties of hello agent load balancer, click **Load balancing rules** and then **Add**.</span></span>
   
    ![правила балансировщика нагрузки Службы контейнеров Azure](./media/container-service-enable-public-access/add-balancer-rule.png)
7. <span data-ttu-id="1f06c-132">Заполните форму подсистемы балансировки нагрузки, hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1f06c-132">Fill out hello load balancer form and click **OK**.</span></span>
   
   | <span data-ttu-id="1f06c-133">Поле</span><span class="sxs-lookup"><span data-stu-id="1f06c-133">Field</span></span> | <span data-ttu-id="1f06c-134">Описание</span><span class="sxs-lookup"><span data-stu-id="1f06c-134">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="1f06c-135">Имя</span><span class="sxs-lookup"><span data-stu-id="1f06c-135">Name</span></span> |<span data-ttu-id="1f06c-136">Описательное имя подсистемы балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="1f06c-136">A descriptive name of hello load balancer.</span></span> |
   | <span data-ttu-id="1f06c-137">Порт</span><span class="sxs-lookup"><span data-stu-id="1f06c-137">Port</span></span> |<span data-ttu-id="1f06c-138">общий входящий порт Hello.</span><span class="sxs-lookup"><span data-stu-id="1f06c-138">hello public incoming port.</span></span> |
   | <span data-ttu-id="1f06c-139">Серверный порт</span><span class="sxs-lookup"><span data-stu-id="1f06c-139">Backend port</span></span> |<span data-ttu-id="1f06c-140">Hello внутренней общий порт tooroute трафика hello контейнера.</span><span class="sxs-lookup"><span data-stu-id="1f06c-140">hello internal-public port of hello container tooroute traffic to.</span></span> |
   | <span data-ttu-id="1f06c-141">Серверный пул</span><span class="sxs-lookup"><span data-stu-id="1f06c-141">Backend pool</span></span> |<span data-ttu-id="1f06c-142">контейнеры Hello в этом пуле будет hello цель для этой подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="1f06c-142">hello containers in this pool will be hello target for this load balancer.</span></span> |
   | <span data-ttu-id="1f06c-143">Проба</span><span class="sxs-lookup"><span data-stu-id="1f06c-143">Probe</span></span> |<span data-ttu-id="1f06c-144">Здравствуйте toodetermine пробы используется, если целевой объект в hello **внутренний пул** находится в работоспособном состоянии.</span><span class="sxs-lookup"><span data-stu-id="1f06c-144">hello probe used toodetermine if a target in hello **Backend pool** is healthy.</span></span> |
   | <span data-ttu-id="1f06c-145">Сохранение сеанса</span><span class="sxs-lookup"><span data-stu-id="1f06c-145">Session persistence</span></span> |<span data-ttu-id="1f06c-146">Определяет способ обработки трафика от клиента hello время сеанса hello.</span><span class="sxs-lookup"><span data-stu-id="1f06c-146">Determines how traffic from a client should be handled for hello duration of hello session.</span></span><br><br><span data-ttu-id="1f06c-147">**Нет**: последовательные запросы от одного клиента могут обрабатываться любой контейнер hello.</span><span class="sxs-lookup"><span data-stu-id="1f06c-147">**None**: Successive requests from hello same client can be handled by any container.</span></span><br><span data-ttu-id="1f06c-148">**Клиент IP**: последовательные запросы от hello же IP-адрес клиента, обрабатываются hello одного контейнера.</span><span class="sxs-lookup"><span data-stu-id="1f06c-148">**Client IP**: Successive requests from hello same client IP are handled by hello same container.</span></span><br><span data-ttu-id="1f06c-149">**Клиент IP и протокола**: последовательные запросы от hello же сочетанием IP-адрес и протокол клиента обрабатываются hello одного контейнера.</span><span class="sxs-lookup"><span data-stu-id="1f06c-149">**Client IP and protocol**: Successive requests from hello same client IP and protocol combination are handled by hello same container.</span></span> |
   | <span data-ttu-id="1f06c-150">Время ожидания перед переходом в режим простоя</span><span class="sxs-lookup"><span data-stu-id="1f06c-150">Idle timeout</span></span> |<span data-ttu-id="1f06c-151">(TCP) В минутах, hello tookeep времени, откройте TCP или HTTP-клиента, не полагаясь на *активности* сообщений.</span><span class="sxs-lookup"><span data-stu-id="1f06c-151">(TCP only) In minutes, hello time tookeep a TCP/HTTP client open without relying on *keep-alive* messages.</span></span> |

## <a name="add-a-security-rule-portal"></a><span data-ttu-id="1f06c-152">Добавление правила безопасности (портал)</span><span class="sxs-lookup"><span data-stu-id="1f06c-152">Add a security rule (portal)</span></span>
<span data-ttu-id="1f06c-153">Теперь нам нужны tooadd правило безопасности, который перенаправляет трафик из наших открытый порт в брандмауэре hello.</span><span class="sxs-lookup"><span data-stu-id="1f06c-153">Next, we need tooadd a security rule that routes traffic from our opened port through hello firewall.</span></span>

1. <span data-ttu-id="1f06c-154">Войдите в портал toohello.</span><span class="sxs-lookup"><span data-stu-id="1f06c-154">Log in toohello portal.</span></span>
2. <span data-ttu-id="1f06c-155">Найти группу ресурсов hello развернутым hello контейнера службы Azure.</span><span class="sxs-lookup"><span data-stu-id="1f06c-155">Find hello resource group that you deployed hello Azure Container Service to.</span></span>
3. <span data-ttu-id="1f06c-156">Выберите hello **открытый** агента сетевой группы безопасности (которая называется аналогичные слишком**XXXX-агента public-nsg-XXXX**).</span><span class="sxs-lookup"><span data-stu-id="1f06c-156">Select hello **public** agent network security group (which is named similar too**XXXX-agent-public-nsg-XXXX**).</span></span>
   
    ![группа безопасности сети Службы контейнеров Azure](./media/container-service-enable-public-access/agent-nsg.png)
4. <span data-ttu-id="1f06c-158">Выберите **Правила безопасности для входящего трафика**, а затем щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1f06c-158">Select **Inbound security rules** and then **Add**.</span></span>
   
    ![правила группы безопасности сети Службы контейнеров Azure](./media/container-service-enable-public-access/add-firewall-rule.png)
5. <span data-ttu-id="1f06c-160">Заполните tooallow правило брандмауэра hello открытый порт и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1f06c-160">Fill out hello firewall rule tooallow your public port and click **OK**.</span></span>
   
   | <span data-ttu-id="1f06c-161">Поле</span><span class="sxs-lookup"><span data-stu-id="1f06c-161">Field</span></span> | <span data-ttu-id="1f06c-162">Описание</span><span class="sxs-lookup"><span data-stu-id="1f06c-162">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="1f06c-163">Имя</span><span class="sxs-lookup"><span data-stu-id="1f06c-163">Name</span></span> |<span data-ttu-id="1f06c-164">Описательное имя правила брандмауэра hello.</span><span class="sxs-lookup"><span data-stu-id="1f06c-164">A descriptive name of hello firewall rule.</span></span> |
   | <span data-ttu-id="1f06c-165">Приоритет</span><span class="sxs-lookup"><span data-stu-id="1f06c-165">Priority</span></span> |<span data-ttu-id="1f06c-166">Ранг приоритет для правила hello.</span><span class="sxs-lookup"><span data-stu-id="1f06c-166">Priority rank for hello rule.</span></span> <span data-ttu-id="1f06c-167">Hello hello номеров hello выше hello низкоприоритетные.</span><span class="sxs-lookup"><span data-stu-id="1f06c-167">hello lower hello number hello higher hello priority.</span></span> |
   | <span data-ttu-id="1f06c-168">Источник</span><span class="sxs-lookup"><span data-stu-id="1f06c-168">Source</span></span> |<span data-ttu-id="1f06c-169">Ограничьте hello входящих IP адрес диапазона toobe разрешаться или запрещаться этим правилом.</span><span class="sxs-lookup"><span data-stu-id="1f06c-169">Restrict hello incoming IP address range toobe allowed or denied by this rule.</span></span> <span data-ttu-id="1f06c-170">Используйте **любой** toonot определения ограничения.</span><span class="sxs-lookup"><span data-stu-id="1f06c-170">Use **Any** toonot specify a restriction.</span></span> |
   | <span data-ttu-id="1f06c-171">служба</span><span class="sxs-lookup"><span data-stu-id="1f06c-171">Service</span></span> |<span data-ttu-id="1f06c-172">Выберите набор стандартных служб, для которых предназначено это правило безопасности.</span><span class="sxs-lookup"><span data-stu-id="1f06c-172">Select a set of predefined services this security rule is for.</span></span> <span data-ttu-id="1f06c-173">В противном случае используйте **настраиваемый** toocreate свои собственные.</span><span class="sxs-lookup"><span data-stu-id="1f06c-173">Otherwise use **Custom** toocreate your own.</span></span> |
   | <span data-ttu-id="1f06c-174">Протокол</span><span class="sxs-lookup"><span data-stu-id="1f06c-174">Protocol</span></span> |<span data-ttu-id="1f06c-175">Ограничьте трафик по **TCP** или **UDP**.</span><span class="sxs-lookup"><span data-stu-id="1f06c-175">Restrict traffic based on **TCP** or **UDP**.</span></span> <span data-ttu-id="1f06c-176">Используйте **любой** toonot определения ограничения.</span><span class="sxs-lookup"><span data-stu-id="1f06c-176">Use **Any** toonot specify a restriction.</span></span> |
   | <span data-ttu-id="1f06c-177">Диапазон портов</span><span class="sxs-lookup"><span data-stu-id="1f06c-177">Port range</span></span> |<span data-ttu-id="1f06c-178">При **службы** — **настраиваемый**, указывает hello диапазон портов, которые затрагивает это правило.</span><span class="sxs-lookup"><span data-stu-id="1f06c-178">When **Service** is **Custom**, specifies hello range of ports that this rule affects.</span></span> <span data-ttu-id="1f06c-179">Можно использовать один порт, например **80**, или диапазон портов, например **1024–1500**.</span><span class="sxs-lookup"><span data-stu-id="1f06c-179">You can use a single port, such as **80**, or a range like **1024-1500**.</span></span> |
   | <span data-ttu-id="1f06c-180">Действие</span><span class="sxs-lookup"><span data-stu-id="1f06c-180">Action</span></span> |<span data-ttu-id="1f06c-181">Разрешить или запретить трафик, соответствующий критериям hello.</span><span class="sxs-lookup"><span data-stu-id="1f06c-181">Allow or deny traffic that meets hello criteria.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1f06c-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1f06c-182">Next steps</span></span>
<span data-ttu-id="1f06c-183">Дополнительные сведения о hello разницу между [общедоступных и частных агентов DC/OS](container-service-dcos-agents.md).</span><span class="sxs-lookup"><span data-stu-id="1f06c-183">Learn about hello difference between [public and private DC/OS agents](container-service-dcos-agents.md).</span></span>

<span data-ttu-id="1f06c-184">Узнайте больше об [управлении контейнерами DC/OS](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="1f06c-184">Read more information about [managing your DC/OS containers](container-service-mesos-marathon-ui.md).</span></span>

