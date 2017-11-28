---
title: "Интеграция схемы услуги с System Center Operations Manager | Документация Майкрософт"
description: "Схема услуги — это решение Operations Management Suite, которое автоматически обнаруживает компоненты приложений в системах Windows и Linux и сопоставляет взаимодействие между службами. В этой статье описывается использование схемы услуги для автоматического создания схем распределенных приложений в Operations Manager."
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
ms.openlocfilehash: a7dbe54ffb4daa941c19b51ba263dd3d23b7a98b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a><span data-ttu-id="35d5a-104">Интеграция схемы услуги с System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="35d5a-104">Service Map integration with System Center Operations Manager</span></span>
  > [!NOTE]
  > <span data-ttu-id="35d5a-105">Эта функция предоставляется в общедоступной предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="35d5a-105">This feature is in public preview.</span></span>
  > 
  
<span data-ttu-id="35d5a-106">Схема услуги Operations Management Suite автоматически обнаруживает компоненты приложений в системах Windows и Linux и сопоставляет взаимодействие между службами.</span><span class="sxs-lookup"><span data-stu-id="35d5a-106">Operations Management Suite Service Map automatically discovers application components on Windows and Linux systems and maps the communication between services.</span></span> <span data-ttu-id="35d5a-107">Схема услуги позволяет рассматривать серверы как взаимосвязанные системы, предоставляющие важные услуги.</span><span class="sxs-lookup"><span data-stu-id="35d5a-107">Service Map allows you to view your servers the way you think of them, as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="35d5a-108">Схема услуги отображает сведения о подключениях между серверами, процессами и портами в любой подключенной по протоколу TCP архитектуре без дополнительной настройки. Пользователям требуется только установить агент.</span><span class="sxs-lookup"><span data-stu-id="35d5a-108">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture, with no configuration required besides the installation of an agent.</span></span> <span data-ttu-id="35d5a-109">Дополнительные сведения см. в [документации по схеме услуги](operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="35d5a-109">For more information, see the [Service Map documentation](operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="35d5a-110">С помощью этой интеграции схемы услуги и System Center Operations Manager можно автоматически создавать схемы распределенных приложений в Operations Manager, которые основаны на динамических сопоставлениях зависимостей в схеме услуги.</span><span class="sxs-lookup"><span data-stu-id="35d5a-110">With this integration between Service Map and System Center Operations Manager, you can automatically create distributed application diagrams in Operations Manager that are based on the dynamic dependency maps in Service Map.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35d5a-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="35d5a-111">Prerequisites</span></span>
* <span data-ttu-id="35d5a-112">Группа управления Operations Manager, управляющая набором серверов.</span><span class="sxs-lookup"><span data-stu-id="35d5a-112">An Operations Manager management group that is managing a set of servers.</span></span>
* <span data-ttu-id="35d5a-113">Рабочая область Operations Management Suite с включенным решением схемы услуги.</span><span class="sxs-lookup"><span data-stu-id="35d5a-113">An Operations Management Suite workspace with the Service Map solution enabled.</span></span>
* <span data-ttu-id="35d5a-114">Набор серверов (по крайней мере один), которые находятся под управлением Operations Manager и отправляют данные в схему услуги.</span><span class="sxs-lookup"><span data-stu-id="35d5a-114">A set of servers (at least one) that are being managed by Operations Manager and sending data to Service Map.</span></span> <span data-ttu-id="35d5a-115">Поддерживаются серверы Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="35d5a-115">Windows and Linux servers are supported.</span></span>
* <span data-ttu-id="35d5a-116">Субъект-служба с доступом к подписке Azure, связанной с рабочей областью Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="35d5a-116">A service principal with access to the Azure subscription that is associated with the Operations Management Suite workspace.</span></span> <span data-ttu-id="35d5a-117">Дополнительные сведения см. в руководстве по [созданию субъекта-службы](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="35d5a-117">For more information, go to [Create a service principal](#creating-a-service-principal).</span></span>

## <a name="install-the-service-map-management-pack"></a><span data-ttu-id="35d5a-118">Установка пакета управления схемы услуги</span><span class="sxs-lookup"><span data-stu-id="35d5a-118">Install the Service Map management pack</span></span>
<span data-ttu-id="35d5a-119">Интеграция Operations Manager и схемы услуг обеспечивается путем импорта набора пакетов управления Microsoft.SystemCenter.ServiceMap (Microsoft.SystemCenter.ServiceMap.mpb).</span><span class="sxs-lookup"><span data-stu-id="35d5a-119">You enable the integration between Operations Manager and Service Map by importing the Microsoft.SystemCenter.ServiceMap management pack bundle (Microsoft.SystemCenter.ServiceMap.mpb).</span></span> <span data-ttu-id="35d5a-120">Этот набор содержит следующие пакеты управления:</span><span class="sxs-lookup"><span data-stu-id="35d5a-120">The bundle contains the following management packs:</span></span>
* <span data-ttu-id="35d5a-121">Microsoft.ServiceMap.Application.Views;</span><span class="sxs-lookup"><span data-stu-id="35d5a-121">Microsoft Service Map Application Views</span></span>
* <span data-ttu-id="35d5a-122">Microsoft.System.Center.ServiceMap.Internal;</span><span class="sxs-lookup"><span data-stu-id="35d5a-122">Microsoft System Center Service Map Internal</span></span>
* <span data-ttu-id="35d5a-123">Microsoft.System.Center.ServiceMap.Overrides;</span><span class="sxs-lookup"><span data-stu-id="35d5a-123">Microsoft System Center Service Map Overrides</span></span>
* <span data-ttu-id="35d5a-124">Microsoft.System.Center.ServiceMap.</span><span class="sxs-lookup"><span data-stu-id="35d5a-124">Microsoft System Center Service Map</span></span>

## <a name="configure-the-service-map-integration"></a><span data-ttu-id="35d5a-125">Настройка интеграции схемы услуги</span><span class="sxs-lookup"><span data-stu-id="35d5a-125">Configure the Service Map integration</span></span>
<span data-ttu-id="35d5a-126">После установки пакета управления схемы услуги в области **Администрирование** в разделе **Operations Management Suite** отобразится новый узел — **Схема услуги**.</span><span class="sxs-lookup"><span data-stu-id="35d5a-126">After you install the Service Map management pack, a new node, **Service Map**, is displayed under **Operations Management Suite** in the **Administration** pane.</span></span> 

<span data-ttu-id="35d5a-127">Чтобы настроить интеграцию схемы услуги, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="35d5a-127">To configure Service Map integration, do the following:</span></span>

1. <span data-ttu-id="35d5a-128">Чтобы открыть мастер настройки, щелкните **Добавить рабочую область** в области **Service Map Overview** (Обзор схемы услуги).</span><span class="sxs-lookup"><span data-stu-id="35d5a-128">To open the configuration wizard, in the **Service Map Overview** pane, click **Add workspace**.</span></span>  

    ![Область "Service Map Overview" (Обзор схемы услуги)](media/oms-service-map/scom-configuration.png)

2. <span data-ttu-id="35d5a-130">В окне **Настройка подключения** введите имя или идентификатор клиента, идентификатор приложения (имя пользователя или clientID) и пароль субъекта-службы, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="35d5a-130">In the **Connection Configuration** window, enter the tenant name or ID, application ID (also known as the username or clientID), and password of the service principal, and then click **Next**.</span></span> <span data-ttu-id="35d5a-131">Дополнительные сведения см. в руководстве по [созданию субъекта-службы](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="35d5a-131">For more information, go to [Create a service principal](#creating-a-service-principal).</span></span>

    ![Окно "Настройка подключения"](media/oms-service-map/scom-config-spn.png)

3. <span data-ttu-id="35d5a-133">В окне **Subscription Selection** (Выбор подписки) выберите подписку Azure, группу ресурсов Azure (которая содержит рабочую область Operations Management Suite) и саму рабочую область Operations Management Suite, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="35d5a-133">In the **Subscription Selection** window, select the Azure subscription, Azure resource group (the one that contains the Operations Management Suite workspace), and Operations Management Suite workspace, and then click **Next**.</span></span>

    ![Настройка Operations Manager: рабочая область](media/oms-service-map/scom-config-workspace.png)

4. <span data-ttu-id="35d5a-135">В окне **Machine Group Selection** (Выбор группы компьютеров) выберите группы компьютеров решения "Сопоставление служб", которые необходимо синхронизировать с Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="35d5a-135">In the **Machine Group Selection** window, you choose which Service Map Machine Groups you want to sync to Operations Manager.</span></span> <span data-ttu-id="35d5a-136">Нажмите кнопку **Add/Remove Machine Groups** (Добавить или удалить группы компьютеров), выберите группы из списка **доступных групп компьютеров**и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="35d5a-136">Click **Add/Remove Machine Groups**, choose groups from the list of **Available Machine Groups**, and click **Add**.</span></span>  <span data-ttu-id="35d5a-137">Выбрав группы, нажмите кнопку **ОК** для завершения.</span><span class="sxs-lookup"><span data-stu-id="35d5a-137">When you are finished selecting groups, click **Ok** to finish.</span></span>
    
    ![Настройка групп компьютеров в Operations Manager](media/oms-service-map/scom-config-machine-groups.png)
    
5. <span data-ttu-id="35d5a-139">В окне **Выбор сервера** настройте группу серверов схемы услуги для синхронизации между Operations Manager и схемой услуги.</span><span class="sxs-lookup"><span data-stu-id="35d5a-139">In the **Server Selection** window, you configure the Service Map Servers Group with the servers that you want to sync between Operations Manager and Service Map.</span></span> <span data-ttu-id="35d5a-140">Нажмите кнопку **Добавление и удаление серверов**.</span><span class="sxs-lookup"><span data-stu-id="35d5a-140">Click **Add/Remove Servers**.</span></span>   
    
    <span data-ttu-id="35d5a-141">Для интеграции и успешного построения схемы распределенного приложения для сервера он должен:</span><span class="sxs-lookup"><span data-stu-id="35d5a-141">For the integration to build a distributed application diagram for a server, the server must be:</span></span>

    * <span data-ttu-id="35d5a-142">находиться под управлением Operations Manager;</span><span class="sxs-lookup"><span data-stu-id="35d5a-142">Managed by Operations Manager</span></span>
    * <span data-ttu-id="35d5a-143">находиться под управлением решения "Сопоставление служб";</span><span class="sxs-lookup"><span data-stu-id="35d5a-143">Managed by Service Map</span></span>
    * <span data-ttu-id="35d5a-144">входить в группу серверов решения "Сопоставление служб".</span><span class="sxs-lookup"><span data-stu-id="35d5a-144">Listed in the Service Map Servers Group</span></span>

    ![Настройка Operations Manager: группа](media/oms-service-map/scom-config-group.png)

6. <span data-ttu-id="35d5a-146">Необязательно. Выберите пул ресурсов сервера управления для взаимодействия с Operations Management Suite, а затем нажмите кнопку **Добавить рабочую область**.</span><span class="sxs-lookup"><span data-stu-id="35d5a-146">Optional: Select the Management Server resource pool to communicate with Operations Management Suite, and then click **Add Workspace**.</span></span>

    ![Настройка Operations Manager: пул ресурсов](media/oms-service-map/scom-config-pool.png)

    <span data-ttu-id="35d5a-148">Для настройки и регистрации рабочей области Operations Management Suite может потребоваться около минуты.</span><span class="sxs-lookup"><span data-stu-id="35d5a-148">It might take a minute to configure and register the Operations Management Suite workspace.</span></span> <span data-ttu-id="35d5a-149">После ее настройки Operations Manager инициирует первую синхронизацию схемы услуги из Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="35d5a-149">After it is configured, Operations Manager initiates the first Service Map sync from Operations Management Suite.</span></span>

    ![Настройка Operations Manager: пул ресурсов](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a><span data-ttu-id="35d5a-151">Мониторинг схемы услуги</span><span class="sxs-lookup"><span data-stu-id="35d5a-151">Monitor Service Map</span></span>
<span data-ttu-id="35d5a-152">После подключения рабочей области Operations Management Suite в области **Мониторинг** консоли Operations Manager отобразится новая папка — "Схема услуги".</span><span class="sxs-lookup"><span data-stu-id="35d5a-152">After the Operations Management Suite workspace is connected, a new folder, Service Map, is displayed in the **Monitoring** pane of the Operations Manager console.</span></span>

![Operations Manager: область "Мониторинг"](media/oms-service-map/scom-monitoring.png)

<span data-ttu-id="35d5a-154">Папка "Сопоставление служб" имеет четыре узла:</span><span class="sxs-lookup"><span data-stu-id="35d5a-154">The Service Map folder has four nodes:</span></span>
* <span data-ttu-id="35d5a-155">**Активные оповещения:** список всех активных оповещений об обмене данными между Operations Manager и решением "Сопоставление служб".</span><span class="sxs-lookup"><span data-stu-id="35d5a-155">**Active Alerts**: Lists all the active alerts about the communication between Operations Manager and Service Map.</span></span>  <span data-ttu-id="35d5a-156">Обратите внимание, что оповещения Operations Management Suite не отображаются в Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="35d5a-156">Note that these alerts are not Operations Management Suite alerts being synced to Operations Manager.</span></span> 

* <span data-ttu-id="35d5a-157">**Серверы**: список отслеживаемых серверов, настроенных для синхронизации из схемы услуги.</span><span class="sxs-lookup"><span data-stu-id="35d5a-157">**Servers**: Lists the monitored servers that are configured to sync from Service Map.</span></span>

    ![Operations Manager: область "Серверы"](media/oms-service-map/scom-monitoring-servers.png)

* <span data-ttu-id="35d5a-159">**Machine Group Dependency Views** (Представления зависимостей групп компьютеров): здесь указаны группы компьютеров, синхронизируемых с решением "Сопоставление служб".</span><span class="sxs-lookup"><span data-stu-id="35d5a-159">**Machine Group Dependency Views**: Lists all machine groups that are synced from Service Map.</span></span> <span data-ttu-id="35d5a-160">Вы можете щелкнуть любую группу, чтобы просмотреть распределенные диаграммы приложения.</span><span class="sxs-lookup"><span data-stu-id="35d5a-160">You can click any group to view its distributed application diagram.</span></span>

    ![Схема распределенного приложения Operations Manager](media/oms-service-map/scom-group-dad.png)

* <span data-ttu-id="35d5a-162">**Server Dependency Views** (Представления зависимости серверов): список всех серверов, синхронизируемых из схемы услуги.</span><span class="sxs-lookup"><span data-stu-id="35d5a-162">**Server Dependency Views**: Lists all servers that are synced from Service Map.</span></span> <span data-ttu-id="35d5a-163">Вы можете щелкнуть любой сервер, чтобы просмотреть его схему распределенного приложения.</span><span class="sxs-lookup"><span data-stu-id="35d5a-163">You can click any server to view its distributed application diagram.</span></span>

    ![Схема распределенного приложения Operations Manager](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-the-workspace"></a><span data-ttu-id="35d5a-165">Изменение или удаление рабочей области</span><span class="sxs-lookup"><span data-stu-id="35d5a-165">Edit or delete the workspace</span></span>
<span data-ttu-id="35d5a-166">Вы можете изменить или удалить настроенную рабочую область с помощью области **Service Map Overview** (Обзор схемы услуги) (область **Администрирование** > **Operations Management Suite** > **Схема услуги**).</span><span class="sxs-lookup"><span data-stu-id="35d5a-166">You can edit or delete the configured workspace through the **Service Map Overview** pane (**Administration** pane > **Operations Management Suite** > **Service Map**).</span></span> <span data-ttu-id="35d5a-167">Пока можно настроить только одну рабочую область Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="35d5a-167">You can configure only one Operations Management Suite workspace for now.</span></span>

![Operations Manager: область изменения рабочей области](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a><span data-ttu-id="35d5a-169">Настройка правил и переопределений</span><span class="sxs-lookup"><span data-stu-id="35d5a-169">Configure rules and overrides</span></span>
<span data-ttu-id="35d5a-170">Правило _Microsoft.SystemCenter.ServiceMapImport.Rule_ создается для периодического извлечения сведений из схемы услуги.</span><span class="sxs-lookup"><span data-stu-id="35d5a-170">A rule, _Microsoft.SystemCenter.ServiceMapImport.Rule_, is created to periodically fetch information from Service Map.</span></span> <span data-ttu-id="35d5a-171">Чтобы изменить время синхронизации, можно настроить переопределения правила (область **Разработка** > **Правила** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span><span class="sxs-lookup"><span data-stu-id="35d5a-171">To change sync timings, you can configure overrides of the rule (**Authoring** pane > **Rules** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span></span>

![Operations Manager: окно свойств переопределений](media/oms-service-map/scom-overrides.png)

* <span data-ttu-id="35d5a-173">**Enabled**: позволяет включить или отключить автоматическое обновление.</span><span class="sxs-lookup"><span data-stu-id="35d5a-173">**Enabled**: Enable or disable automatic updates.</span></span> 
* <span data-ttu-id="35d5a-174">**IntervalMinutes**: позволяет сбросить настройки времени между обновлениями.</span><span class="sxs-lookup"><span data-stu-id="35d5a-174">**IntervalMinutes**: Reset the time between updates.</span></span> <span data-ttu-id="35d5a-175">Значение по умолчанию — один час.</span><span class="sxs-lookup"><span data-stu-id="35d5a-175">The default interval is one hour.</span></span> <span data-ttu-id="35d5a-176">Если необходимо чаще синхронизировать карты серверов, можно изменить это значение.</span><span class="sxs-lookup"><span data-stu-id="35d5a-176">If you want to sync server maps more frequently, you can change the value.</span></span>
* <span data-ttu-id="35d5a-177">**TimeoutSeconds**: позволяет сбросить настройки времени ожидания запроса.</span><span class="sxs-lookup"><span data-stu-id="35d5a-177">**TimeoutSeconds**: Reset the length of time before the request times out.</span></span> 
* <span data-ttu-id="35d5a-178">**TimeWindowMinutes**: позволяет сбросить настройки временного окна для запроса данных.</span><span class="sxs-lookup"><span data-stu-id="35d5a-178">**TimeWindowMinutes**: Reset the time window for querying data.</span></span> <span data-ttu-id="35d5a-179">Значение по умолчанию — 60 минут.</span><span class="sxs-lookup"><span data-stu-id="35d5a-179">Default is a 60-minute window.</span></span> <span data-ttu-id="35d5a-180">Максимальное значение, разрешенное схемой услуги, — 60 минут.</span><span class="sxs-lookup"><span data-stu-id="35d5a-180">The maximum value allowed by Service Map is 60 minutes.</span></span>

## <a name="known-issues-and-limitations"></a><span data-ttu-id="35d5a-181">Известные проблемы и ограничения</span><span class="sxs-lookup"><span data-stu-id="35d5a-181">Known issues and limitations</span></span>

<span data-ttu-id="35d5a-182">В текущей версии существуют следующие проблемы и ограничения:</span><span class="sxs-lookup"><span data-stu-id="35d5a-182">The current design presents the following issues and limitations:</span></span>
* <span data-ttu-id="35d5a-183">Можно подключиться только к одной рабочей области Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="35d5a-183">You can only connect to a single Operations Management Suite workspace.</span></span>
* <span data-ttu-id="35d5a-184">Хотя пользователи могут вручную добавить серверы в группу серверов решения "Сопоставление служб" с помощью области **Разработка**, сопоставления для этих серверов синхронизируются не сразу.</span><span class="sxs-lookup"><span data-stu-id="35d5a-184">Although you can add servers to the Service Map Servers Group manually through the **Authoring** pane, the maps for those servers are not synced immediately.</span></span>  <span data-ttu-id="35d5a-185">Они будут синхронизированы из решения "Сопоставление служб" во время следующего цикла синхронизации.</span><span class="sxs-lookup"><span data-stu-id="35d5a-185">They will be synced from Service Map during the next sync cycle.</span></span>
* <span data-ttu-id="35d5a-186">Если внести изменения в схемы распределенного приложения, созданные в пакете управления, скорее всего, эти изменения будут перезаписаны при следующей синхронизации с решением "Сопоставление служб".</span><span class="sxs-lookup"><span data-stu-id="35d5a-186">If you make any changes to the Distributed Application Diagrams created by the management pack, those changes will likely be overwritten on the next sync with Service Map.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="35d5a-187">Создание субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="35d5a-187">Create a service principal</span></span>
<span data-ttu-id="35d5a-188">Официальная документация Azure по созданию субъекта-службы представлена в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="35d5a-188">For official Azure documentation about creating a service principal, see:</span></span>
* [<span data-ttu-id="35d5a-189">Использование Azure PowerShell для создания субъекта-службы и доступа к ресурсам</span><span class="sxs-lookup"><span data-stu-id="35d5a-189">Create a service principal by using PowerShell</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="35d5a-190">Использование интерфейса командной строки Azure для создания субъекта-службы и доступа к ресурсам</span><span class="sxs-lookup"><span data-stu-id="35d5a-190">Create a service principal by using Azure CLI</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [<span data-ttu-id="35d5a-191">Создание приложения Azure Active Directory и субъекта-службы с доступом к ресурсам с помощью портала</span><span class="sxs-lookup"><span data-stu-id="35d5a-191">Create a service principal by using the Azure portal</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a><span data-ttu-id="35d5a-192">Отзыв</span><span class="sxs-lookup"><span data-stu-id="35d5a-192">Feedback</span></span>
<span data-ttu-id="35d5a-193">У вас есть комментарии относительно схемы услуги или этой документации?</span><span class="sxs-lookup"><span data-stu-id="35d5a-193">Do you have any feedback for us about Service Map or this documentation?</span></span> <span data-ttu-id="35d5a-194">Посетите [страницу пользовательских мнений](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), где можно предложить функции или проголосовать за существующие предложения.</span><span class="sxs-lookup"><span data-stu-id="35d5a-194">Visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote on existing suggestions.</span></span>
