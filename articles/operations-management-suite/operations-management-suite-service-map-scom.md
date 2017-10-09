---
title: "aaaService карты интеграции с System Center Operations Manager | Документы Microsoft"
description: "Схемы услуг — это решение Operations Management Suite, который автоматически обнаруживает компонентов приложений в Windows и системами Linux и карты hello обмен данными между службами. В этой статье описывается с помощью схемы услуг tooautomatically Создание диаграмм распределенных приложений в Operations Manager."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: cff9cce2559448ec3a5fd14087b867f314716560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a><span data-ttu-id="4e846-104">Интеграция схемы услуги с System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="4e846-104">Service Map integration with System Center Operations Manager</span></span>
  > [!NOTE]
  > <span data-ttu-id="4e846-105">Эта функция предоставляется в общедоступной предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="4e846-105">This feature is in public preview.</span></span>
  > 
  
<span data-ttu-id="4e846-106">Схемы услуг Operations Management Suite автоматическое обнаружение компонентов приложения в системах Windows и Linux и сопоставляет hello обмен данными между службами.</span><span class="sxs-lookup"><span data-stu-id="4e846-106">Operations Management Suite Service Map automatically discovers application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="4e846-107">Схемы услуг можно tooview образом hello серверов можно считать из них, соединенных друг с другом систем, доставляющих критически важных служб.</span><span class="sxs-lookup"><span data-stu-id="4e846-107">Service Map allows you tooview your servers hello way you think of them, as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="4e846-108">Схемы услуг показаны соединения между серверами, процессы и порты через любой архитектуры TCP-подключения без настройки помимо hello установки агента.</span><span class="sxs-lookup"><span data-stu-id="4e846-108">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture, with no configuration required besides hello installation of an agent.</span></span> <span data-ttu-id="4e846-109">Дополнительные сведения см. в разделе hello [документации схемы услуг](operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="4e846-109">For more information, see hello [Service Map documentation](operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="4e846-110">С этой интеграции между схемы услуг и System Center Operations Manager можно автоматически создать диаграммах распределенных приложений в Operations Manager, которые основаны на картах hello динамических зависимостей на карте службы.</span><span class="sxs-lookup"><span data-stu-id="4e846-110">With this integration between Service Map and System Center Operations Manager, you can automatically create distributed application diagrams in Operations Manager that are based on hello dynamic dependency maps in Service Map.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e846-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4e846-111">Prerequisites</span></span>
* <span data-ttu-id="4e846-112">Группа управления Operations Manager, управляющая набором серверов.</span><span class="sxs-lookup"><span data-stu-id="4e846-112">An Operations Manager management group that is managing a set of servers.</span></span>
* <span data-ttu-id="4e846-113">Рабочая область Operations Management Suite с hello включено решение схемы услуг.</span><span class="sxs-lookup"><span data-stu-id="4e846-113">An Operations Management Suite workspace with hello Service Map solution enabled.</span></span>
* <span data-ttu-id="4e846-114">Набор серверов (по крайней мере, один), которые находятся под управлением Operations Manager и отправки данных tooService карты.</span><span class="sxs-lookup"><span data-stu-id="4e846-114">A set of servers (at least one) that are being managed by Operations Manager and sending data tooService Map.</span></span> <span data-ttu-id="4e846-115">Поддерживаются серверы Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="4e846-115">Windows and Linux servers are supported.</span></span>
* <span data-ttu-id="4e846-116">Участника службы с toohello доступа к подписке Azure, связанный с рабочей области Operations Management Suite hello.</span><span class="sxs-lookup"><span data-stu-id="4e846-116">A service principal with access toohello Azure subscription that is associated with hello Operations Management Suite workspace.</span></span> <span data-ttu-id="4e846-117">Дополнительные сведения см. слишком[Создание субъекта-службы](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="4e846-117">For more information, go too[Create a service principal](#creating-a-service-principal).</span></span>

## <a name="install-hello-service-map-management-pack"></a><span data-ttu-id="4e846-118">Установите пакет управления hello схемы услуг</span><span class="sxs-lookup"><span data-stu-id="4e846-118">Install hello Service Map management pack</span></span>
<span data-ttu-id="4e846-119">Включить hello интеграцию между Operations Manager и схемы услуг, импортировав набор пакетов управления hello Microsoft.SystemCenter.ServiceMap (Microsoft.SystemCenter.ServiceMap.mpb).</span><span class="sxs-lookup"><span data-stu-id="4e846-119">You enable hello integration between Operations Manager and Service Map by importing hello Microsoft.SystemCenter.ServiceMap management pack bundle (Microsoft.SystemCenter.ServiceMap.mpb).</span></span> <span data-ttu-id="4e846-120">Hello пакет содержит следующие пакеты управления hello:</span><span class="sxs-lookup"><span data-stu-id="4e846-120">hello bundle contains hello following management packs:</span></span>
* <span data-ttu-id="4e846-121">Microsoft.ServiceMap.Application.Views;</span><span class="sxs-lookup"><span data-stu-id="4e846-121">Microsoft Service Map Application Views</span></span>
* <span data-ttu-id="4e846-122">Microsoft.System.Center.ServiceMap.Internal;</span><span class="sxs-lookup"><span data-stu-id="4e846-122">Microsoft System Center Service Map Internal</span></span>
* <span data-ttu-id="4e846-123">Microsoft.System.Center.ServiceMap.Overrides;</span><span class="sxs-lookup"><span data-stu-id="4e846-123">Microsoft System Center Service Map Overrides</span></span>
* <span data-ttu-id="4e846-124">Microsoft.System.Center.ServiceMap.</span><span class="sxs-lookup"><span data-stu-id="4e846-124">Microsoft System Center Service Map</span></span>

## <a name="configure-hello-service-map-integration"></a><span data-ttu-id="4e846-125">Настройка интеграции службы карты hello</span><span class="sxs-lookup"><span data-stu-id="4e846-125">Configure hello Service Map integration</span></span>
<span data-ttu-id="4e846-126">После установки пакета управления схемы услуг hello, новый узел **схемы услуг**, отображается в столбце **Operations Management Suite** в hello **администрирования** области.</span><span class="sxs-lookup"><span data-stu-id="4e846-126">After you install hello Service Map management pack, a new node, **Service Map**, is displayed under **Operations Management Suite** in hello **Administration** pane.</span></span> 

<span data-ttu-id="4e846-127">tooconfigure интеграции схемы услуг hello следующие:</span><span class="sxs-lookup"><span data-stu-id="4e846-127">tooconfigure Service Map integration, do hello following:</span></span>

1. <span data-ttu-id="4e846-128">Мастер настройки hello tooopen в hello **Общие сведения о службе карты** области, нажмите кнопку **добавить рабочую область**.</span><span class="sxs-lookup"><span data-stu-id="4e846-128">tooopen hello configuration wizard, in hello **Service Map Overview** pane, click **Add workspace**.</span></span>  

    ![Область "Service Map Overview" (Обзор схемы услуги)](media/oms-service-map/scom-configuration.png)

2. <span data-ttu-id="4e846-130">В hello **конфигурация подключения** окно, введите имя клиента hello или идентификатор, идентификатор приложения (также известный как имя пользователя hello или clientID) и пароль субъекта-службы hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="4e846-130">In hello **Connection Configuration** window, enter hello tenant name or ID, application ID (also known as hello username or clientID), and password of hello service principal, and then click **Next**.</span></span> <span data-ttu-id="4e846-131">Дополнительные сведения см. слишком[Создание субъекта-службы](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="4e846-131">For more information, go too[Create a service principal](#creating-a-service-principal).</span></span>

    ![окно конфигурации соединения Hello](media/oms-service-map/scom-config-spn.png)

3. <span data-ttu-id="4e846-133">В hello **выбора подписки** окно, выберите hello подписки Azure, группы ресурсов Azure (hello, содержащей рабочей области Operations Management Suite hello) и рабочей области Operations Management Suite и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="4e846-133">In hello **Subscription Selection** window, select hello Azure subscription, Azure resource group (hello one that contains hello Operations Management Suite workspace), and Operations Management Suite workspace, and then click **Next**.</span></span>

    ![Hello рабочей конфигурации Operations Manager](media/oms-service-map/scom-config-workspace.png)

4. <span data-ttu-id="4e846-135">В hello **Выбор группы машины** окно, выберите группы компьютеров карты какие службы требуется toosync tooOperations диспетчера.</span><span class="sxs-lookup"><span data-stu-id="4e846-135">In hello **Machine Group Selection** window, you choose which Service Map Machine Groups you want toosync tooOperations Manager.</span></span> <span data-ttu-id="4e846-136">Нажмите кнопку **Добавление или удаление группы компьютеров**, выбрать группы из списка hello **доступных групп машины**и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="4e846-136">Click **Add/Remove Machine Groups**, choose groups from hello list of **Available Machine Groups**, and click **Add**.</span></span>  <span data-ttu-id="4e846-137">После завершения выбора групп нажмите кнопку **ОК** toofinish.</span><span class="sxs-lookup"><span data-stu-id="4e846-137">When you are finished selecting groups, click **Ok** toofinish.</span></span>
    
    ![Hello групп Operations Manager конфигурации компьютера](media/oms-service-map/scom-config-machine-groups.png)
    
5. <span data-ttu-id="4e846-139">В hello **Выбор сервера** окна, настройке hello группы серверов служб карты с серверами hello, что требуется toosync между Operations Manager и схемы услуг.</span><span class="sxs-lookup"><span data-stu-id="4e846-139">In hello **Server Selection** window, you configure hello Service Map Servers Group with hello servers that you want toosync between Operations Manager and Service Map.</span></span> <span data-ttu-id="4e846-140">Нажмите кнопку **Добавление и удаление серверов**.</span><span class="sxs-lookup"><span data-stu-id="4e846-140">Click **Add/Remove Servers**.</span></span>   
    
    <span data-ttu-id="4e846-141">Для toobuild интеграции hello схеме распределенного приложения на сервере должны быть hello server:</span><span class="sxs-lookup"><span data-stu-id="4e846-141">For hello integration toobuild a distributed application diagram for a server, hello server must be:</span></span>

    * <span data-ttu-id="4e846-142">находиться под управлением Operations Manager;</span><span class="sxs-lookup"><span data-stu-id="4e846-142">Managed by Operations Manager</span></span>
    * <span data-ttu-id="4e846-143">находиться под управлением решения "Сопоставление служб";</span><span class="sxs-lookup"><span data-stu-id="4e846-143">Managed by Service Map</span></span>
    * <span data-ttu-id="4e846-144">Перечисленные в hello группы серверов служб карты</span><span class="sxs-lookup"><span data-stu-id="4e846-144">Listed in hello Service Map Servers Group</span></span>

    ![Hello конфигурации группы Operations Manager](media/oms-service-map/scom-config-group.png)

6. <span data-ttu-id="4e846-146">Необязательно: Установите toocommunicate пула ресурсов hello сервера управления с помощью Operations Management Suite и нажмите кнопку **Добавление рабочей области**.</span><span class="sxs-lookup"><span data-stu-id="4e846-146">Optional: Select hello Management Server resource pool toocommunicate with Operations Management Suite, and then click **Add Workspace**.</span></span>

    ![Пул ресурсов Operations Manager конфигурации Hello](media/oms-service-map/scom-config-pool.png)

    <span data-ttu-id="4e846-148">Может потребовать минуты tooconfigure и зарегистрировать рабочей области Operations Management Suite hello.</span><span class="sxs-lookup"><span data-stu-id="4e846-148">It might take a minute tooconfigure and register hello Operations Management Suite workspace.</span></span> <span data-ttu-id="4e846-149">После настройки, Operations Manager инициирует hello первой синхронизации схемы услуг от Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="4e846-149">After it is configured, Operations Manager initiates hello first Service Map sync from Operations Management Suite.</span></span>

    ![Пул ресурсов Operations Manager конфигурации Hello](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a><span data-ttu-id="4e846-151">Мониторинг схемы услуги</span><span class="sxs-lookup"><span data-stu-id="4e846-151">Monitor Service Map</span></span>
<span data-ttu-id="4e846-152">После подключения рабочей области Operations Management Suite hello новую папку схемы услуг отображается в hello **мониторинг** hello консоли Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="4e846-152">After hello Operations Management Suite workspace is connected, a new folder, Service Map, is displayed in hello **Monitoring** pane of hello Operations Manager console.</span></span>

![панели мониторинга Operations Manager Hello](media/oms-service-map/scom-monitoring.png)

<span data-ttu-id="4e846-154">Папка схемы услуг Hello имеет четыре узла:</span><span class="sxs-lookup"><span data-stu-id="4e846-154">hello Service Map folder has four nodes:</span></span>
* <span data-ttu-id="4e846-155">**Активные предупреждения**: список всех активных предупреждений hello hello соединения между Operations Manager и схемы услуг.</span><span class="sxs-lookup"><span data-stu-id="4e846-155">**Active Alerts**: Lists all hello active alerts about hello communication between Operations Manager and Service Map.</span></span>  <span data-ttu-id="4e846-156">Обратите внимание, что эти оповещения не оповещения Operations Management Suite, синхронизированных tooOperations диспетчера.</span><span class="sxs-lookup"><span data-stu-id="4e846-156">Note that these alerts are not Operations Management Suite alerts being synced tooOperations Manager.</span></span> 

* <span data-ttu-id="4e846-157">**Серверы**: списки hello отслеживаемых серверов, которые являются настроен toosync из схемы услуг.</span><span class="sxs-lookup"><span data-stu-id="4e846-157">**Servers**: Lists hello monitored servers that are configured toosync from Service Map.</span></span>

    ![панель мониторинга серверов Operations Manager Hello](media/oms-service-map/scom-monitoring-servers.png)

* <span data-ttu-id="4e846-159">**Machine Group Dependency Views** (Представления зависимостей групп компьютеров): здесь указаны группы компьютеров, синхронизируемых с решением "Сопоставление служб".</span><span class="sxs-lookup"><span data-stu-id="4e846-159">**Machine Group Dependency Views**: Lists all machine groups that are synced from Service Map.</span></span> <span data-ttu-id="4e846-160">Можно щелкнуть любой группы tooview его схема распределенного приложения.</span><span class="sxs-lookup"><span data-stu-id="4e846-160">You can click any group tooview its distributed application diagram.</span></span>

    ![Схема распределенного приложения Hello Operations Manager](media/oms-service-map/scom-group-dad.png)

* <span data-ttu-id="4e846-162">**Server Dependency Views** (Представления зависимости серверов): список всех серверов, синхронизируемых из схемы услуги.</span><span class="sxs-lookup"><span data-stu-id="4e846-162">**Server Dependency Views**: Lists all servers that are synced from Service Map.</span></span> <span data-ttu-id="4e846-163">Можно щелкнуть любой сервер tooview его схема распределенного приложения.</span><span class="sxs-lookup"><span data-stu-id="4e846-163">You can click any server tooview its distributed application diagram.</span></span>

    ![Схема распределенного приложения Hello Operations Manager](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-hello-workspace"></a><span data-ttu-id="4e846-165">Изменить или удалить рабочую область hello</span><span class="sxs-lookup"><span data-stu-id="4e846-165">Edit or delete hello workspace</span></span>
<span data-ttu-id="4e846-166">Можно изменить или удалить рабочую область hello настроен через hello **Общие сведения о службе карты** области (**администрирования** области > **Operations Management Suite**  >  **Службы карты**).</span><span class="sxs-lookup"><span data-stu-id="4e846-166">You can edit or delete hello configured workspace through hello **Service Map Overview** pane (**Administration** pane > **Operations Management Suite** > **Service Map**).</span></span> <span data-ttu-id="4e846-167">Пока можно настроить только одну рабочую область Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="4e846-167">You can configure only one Operations Management Suite workspace for now.</span></span>

![Hello Operations Manager изменение рабочей области](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a><span data-ttu-id="4e846-169">Настройка правил и переопределений</span><span class="sxs-lookup"><span data-stu-id="4e846-169">Configure rules and overrides</span></span>
<span data-ttu-id="4e846-170">Правило, _Microsoft.SystemCenter.ServiceMapImport.Rule_, создается tooperiodically информация выборки из схемы услуг.</span><span class="sxs-lookup"><span data-stu-id="4e846-170">A rule, _Microsoft.SystemCenter.ServiceMapImport.Rule_, is created tooperiodically fetch information from Service Map.</span></span> <span data-ttu-id="4e846-171">toochange синхронизации времени можно настроить переопределения правила hello (**Authoring** области > **правила** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span><span class="sxs-lookup"><span data-stu-id="4e846-171">toochange sync timings, you can configure overrides of hello rule (**Authoring** pane > **Rules** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span></span>

![окно свойств переопределения Operations Manager Hello](media/oms-service-map/scom-overrides.png)

* <span data-ttu-id="4e846-173">**Enabled**: позволяет включить или отключить автоматическое обновление.</span><span class="sxs-lookup"><span data-stu-id="4e846-173">**Enabled**: Enable or disable automatic updates.</span></span> 
* <span data-ttu-id="4e846-174">**IntervalMinutes**: сброс времени hello между обновлениями.</span><span class="sxs-lookup"><span data-stu-id="4e846-174">**IntervalMinutes**: Reset hello time between updates.</span></span> <span data-ttu-id="4e846-175">Интервал по умолчанию Hello составляет один час.</span><span class="sxs-lookup"><span data-stu-id="4e846-175">hello default interval is one hour.</span></span> <span data-ttu-id="4e846-176">Если требуется maps сервер toosync чаще, можно изменить значение hello.</span><span class="sxs-lookup"><span data-stu-id="4e846-176">If you want toosync server maps more frequently, you can change hello value.</span></span>
* <span data-ttu-id="4e846-177">**Время тайм-аута**: сброс hello отрезок времени до времени ожидания запроса hello.</span><span class="sxs-lookup"><span data-stu-id="4e846-177">**TimeoutSeconds**: Reset hello length of time before hello request times out.</span></span> 
* <span data-ttu-id="4e846-178">**TimeWindowMinutes**: сброс hello временное окно для запроса данных.</span><span class="sxs-lookup"><span data-stu-id="4e846-178">**TimeWindowMinutes**: Reset hello time window for querying data.</span></span> <span data-ttu-id="4e846-179">Значение по умолчанию — 60 минут.</span><span class="sxs-lookup"><span data-stu-id="4e846-179">Default is a 60-minute window.</span></span> <span data-ttu-id="4e846-180">Hello допустимому значению схемы услуг — 60 минут.</span><span class="sxs-lookup"><span data-stu-id="4e846-180">hello maximum value allowed by Service Map is 60 minutes.</span></span>

## <a name="known-issues-and-limitations"></a><span data-ttu-id="4e846-181">Известные проблемы и ограничения</span><span class="sxs-lookup"><span data-stu-id="4e846-181">Known issues and limitations</span></span>

<span data-ttu-id="4e846-182">Hello текущего конструктора представляет hello следующие проблемы и ограничения:</span><span class="sxs-lookup"><span data-stu-id="4e846-182">hello current design presents hello following issues and limitations:</span></span>
* <span data-ttu-id="4e846-183">Можно подключиться только tooa одной рабочей области Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="4e846-183">You can only connect tooa single Operations Management Suite workspace.</span></span>
* <span data-ttu-id="4e846-184">Несмотря на то, что можно добавить серверы toohello группы серверов служб карты вручную с помощью hello **Authoring** немедленно синхронизируются области карты hello для этих серверов.</span><span class="sxs-lookup"><span data-stu-id="4e846-184">Although you can add servers toohello Service Map Servers Group manually through hello **Authoring** pane, hello maps for those servers are not synced immediately.</span></span>  <span data-ttu-id="4e846-185">Они будут синхронизированы из службы сопоставления во время следующего цикла синхронизации hello.</span><span class="sxs-lookup"><span data-stu-id="4e846-185">They will be synced from Service Map during hello next sync cycle.</span></span>
* <span data-ttu-id="4e846-186">Если вы внесли изменения схемы распределенного приложения toohello, созданные пакетом управления hello, эти изменения будут перезаписаны скорее всего на hello следующей синхронизации с помощью схемы услуг.</span><span class="sxs-lookup"><span data-stu-id="4e846-186">If you make any changes toohello Distributed Application Diagrams created by hello management pack, those changes will likely be overwritten on hello next sync with Service Map.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="4e846-187">Создание субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="4e846-187">Create a service principal</span></span>
<span data-ttu-id="4e846-188">Официальная документация Azure по созданию субъекта-службы представлена в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="4e846-188">For official Azure documentation about creating a service principal, see:</span></span>
* [<span data-ttu-id="4e846-189">Использование Azure PowerShell для создания субъекта-службы и доступа к ресурсам</span><span class="sxs-lookup"><span data-stu-id="4e846-189">Create a service principal by using PowerShell</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="4e846-190">Использование интерфейса командной строки Azure для создания субъекта-службы и доступа к ресурсам</span><span class="sxs-lookup"><span data-stu-id="4e846-190">Create a service principal by using Azure CLI</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [<span data-ttu-id="4e846-191">Создание участника службы с помощью hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="4e846-191">Create a service principal by using hello Azure portal</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a><span data-ttu-id="4e846-192">Отзыв</span><span class="sxs-lookup"><span data-stu-id="4e846-192">Feedback</span></span>
<span data-ttu-id="4e846-193">У вас есть комментарии относительно схемы услуги или этой документации?</span><span class="sxs-lookup"><span data-stu-id="4e846-193">Do you have any feedback for us about Service Map or this documentation?</span></span> <span data-ttu-id="4e846-194">Посетите [страницу пользовательских мнений](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), где можно предложить функции или проголосовать за существующие предложения.</span><span class="sxs-lookup"><span data-stu-id="4e846-194">Visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote on existing suggestions.</span></span>
