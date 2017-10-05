---
title: "Мониторинг устройств Surface Hub с помощью Azure Log Analytics | Документация Майкрософт"
description: "Решение Surface Hub позволяет отслеживать работоспособность устройств Surface Hub и понимать, как они используются."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6ecd0d09589fec85c1633f528afc1165c346b7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-to-track-their-health"></a><span data-ttu-id="4cd3f-103">Мониторинг работоспособности устройств Surface Hub с помощью Log Analytics</span><span class="sxs-lookup"><span data-stu-id="4cd3f-103">Monitor Surface Hubs with Log Analytics to track their health</span></span>

![Символ решения Surface Hub](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

<span data-ttu-id="4cd3f-105">В этой статье описывается использование решения Surface Hub в службе Log Analytics для мониторинга устройств Microsoft Surface Hub с помощью пакета Microsoft Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="4cd3f-105">This article describes how you can use the Surface Hub solution in Log Analytics to monitor Microsoft Surface Hub devices with the Microsoft Operations Management Suite (OMS).</span></span> <span data-ttu-id="4cd3f-106">Log Analytics позволяет отслеживать работоспособность устройств Surface Hub и понимать, как они используются.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-106">Log Analytics helps you track the health of your Surface Hubs as well as understand how they are being used.</span></span>

<span data-ttu-id="4cd3f-107">На каждом устройстве Surface Hub установлен агент Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-107">Each Surface Hub has the Microsoft Monitoring Agent installed.</span></span> <span data-ttu-id="4cd3f-108">Именно через этот агент можно отправлять данные с устройства Surface Hub в OMS.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-108">Its through the agent that you can send data from your Surface Hub to OMS.</span></span> <span data-ttu-id="4cd3f-109">Файлы журнала считываются с устройств Surface Hub и затем отправляются в службу OMS.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-109">Log files are read from your Surface Hubs and are then are sent to the OMS service.</span></span> <span data-ttu-id="4cd3f-110">Проблемы, такие как отключение серверов от сети, отсутствие синхронизации календаря или невозможность войти в Skype с использованием учетной записи устройства, отображаются в OMS на панели мониторинга Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-110">Issues like servers being offline, the calendar not syncing, or if the device account is unable to log into Skype are shown in OMS in the Surface Hub dashboard.</span></span> <span data-ttu-id="4cd3f-111">С помощью данных на панели мониторинга можно определить устройства, которые не работают или столкнулись с другими проблемами, и, возможно, применить исправления обнаруженных проблем.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-111">By using the data in the dashboard, you can identify devices that are not running, or that are having other problems, and potentially apply fixes for the detected issues.</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="4cd3f-112">Установка и настройка решения</span><span class="sxs-lookup"><span data-stu-id="4cd3f-112">Installing and configuring the solution</span></span>
<span data-ttu-id="4cd3f-113">Для установки и настройки решений используйте указанные ниже данные.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-113">Use the following information to install and configure the solution.</span></span> <span data-ttu-id="4cd3f-114">Для управления устройствами Surface Hub из пакета Microsoft Operations Management Suite (OMS) потребуются следующие компоненты.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-114">In order to manage your Surface Hubs from the Microsoft Operations Management Suite (OMS), you'll need the following:</span></span>

* <span data-ttu-id="4cd3f-115">Действующая подписка на [OMS](http://www.microsoft.com/oms).</span><span class="sxs-lookup"><span data-stu-id="4cd3f-115">A valid subscription to [OMS](http://www.microsoft.com/oms).</span></span>
* <span data-ttu-id="4cd3f-116">Уровень [подписки OMS](https://azure.microsoft.com/pricing/details/log-analytics/), поддерживающий количество устройств, которые требуется отслеживать.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-116">An [OMS subscription](https://azure.microsoft.com/pricing/details/log-analytics/) level that will support the number of devices you want to monitor.</span></span> <span data-ttu-id="4cd3f-117">Цены на OMS зависят от количества зарегистрированных устройств и объема обрабатываемых данных.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-117">OMS pricing varies depending on how many devices are enrolled, and how much data it processes.</span></span> <span data-ttu-id="4cd3f-118">Это необходимо учитывать при планировании развертывания Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-118">You'll want to take this into consideration when planning your Surface Hub rollout.</span></span>

<span data-ttu-id="4cd3f-119">Затем следует либо добавить подписку OMS в существующую подписку Microsoft Azure, либо создать новую рабочую область непосредственно через портал OMS.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-119">Next, you will either add an OMS subscription to your existing Microsoft Azure subscription or create a new workspace directly through the OMS portal.</span></span> <span data-ttu-id="4cd3f-120">Подробные инструкции по использованию любого из этих методов содержатся в статье [Начало работы с Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4cd3f-120">Detailed instructions for using either method is at [Get started with Log Analytics](log-analytics-get-started.md).</span></span> <span data-ttu-id="4cd3f-121">После настройки подписки OMS вы можете зарегистрировать устройства Surface Hub двумя способами:</span><span class="sxs-lookup"><span data-stu-id="4cd3f-121">Once the OMS subscription is set up, there are two ways to enroll your Surface Hub devices:</span></span>

* <span data-ttu-id="4cd3f-122">автоматически с помощью InTune;</span><span class="sxs-lookup"><span data-stu-id="4cd3f-122">Automatically through Intune</span></span>
* <span data-ttu-id="4cd3f-123">вручную в приложении **Settings** на устройстве Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-123">Manually through **Settings** on your Surface Hub device.</span></span>

## <a name="set-up-monitoring"></a><span data-ttu-id="4cd3f-124">Настройка мониторинга</span><span class="sxs-lookup"><span data-stu-id="4cd3f-124">Set up monitoring</span></span>
<span data-ttu-id="4cd3f-125">Работоспособность и активность устройств Surface Hub можно отслеживать с помощью Log Analytics в OMS.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-125">You can monitor the health and activity of your Surface Hub using Log Analytics in OMS.</span></span> <span data-ttu-id="4cd3f-126">Surface Hub в OMS можно зарегистрировать с помощью Intune или локально в **параметрах** устройства Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-126">You can enroll the Surface Hub in OMS by using Intune, or locally by using **Settings** on the Surface Hub.</span></span>

## <a name="connect-surface-hubs-to-oms-through-intune"></a><span data-ttu-id="4cd3f-127">Подключение устройств Surface Hub к OMS через Intune</span><span class="sxs-lookup"><span data-stu-id="4cd3f-127">Connect Surface Hubs to OMS through Intune</span></span>
<span data-ttu-id="4cd3f-128">Вам потребуется идентификатор и ключ для рабочей области OMS, которая будет управлять устройствами Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-128">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="4cd3f-129">Их можно получить на портале OMS.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-129">You can get those from the OMS portal.</span></span>

<span data-ttu-id="4cd3f-130">Intune — это продукт Microsoft, который позволяет централизованно управлять параметрами конфигурации OMS, применяемыми к одному или нескольким устройствам.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-130">Intune is a Microsoft product that allows you to centrally manage the OMS configuration settings that are applied to one or more of your devices.</span></span> <span data-ttu-id="4cd3f-131">Чтобы настроить устройства через Intune, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4cd3f-131">Follow these steps to configure your devices through Intune:</span></span>

1. <span data-ttu-id="4cd3f-132">Войдите в Intune.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-132">Sign in to Intune.</span></span>
2. <span data-ttu-id="4cd3f-133">Перейдите в раздел **Settings (Параметры)** > **Connected Sources (Подключенные источники)**.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-133">Navigate to **Settings** > **Connected Sources**.</span></span>
3. <span data-ttu-id="4cd3f-134">Создайте или отредактируйте политику на основе шаблона Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-134">Create or edit a policy based on the Surface Hub template.</span></span>
4. <span data-ttu-id="4cd3f-135">Перейдите к разделу OMS (оперативной аналитики Azure) политики и добавьте *идентификатор рабочей области* и *ключ рабочей области* в политику.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-135">Navigate to the OMS (Azure Operational Insights) section of the policy, and add the *Workspace ID* and *Workspace Key* to the policy.</span></span>
5. <span data-ttu-id="4cd3f-136">Сохраните политику.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-136">Save the policy.</span></span>
6. <span data-ttu-id="4cd3f-137">Свяжите политику с соответствующей группой устройств.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-137">Associate the policy with the appropriate group of devices.</span></span>

   ![Политика Intune](./media/log-analytics-surface-hubs/intune.png)

<span data-ttu-id="4cd3f-139">Затем Intune синхронизирует настройки OMS с устройствами в целевой группе, регистрируя их в рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-139">Intune then syncs the OMS settings with the devices in the target group, enrolling them in your OMS workspace.</span></span>

## <a name="connect-surface-hubs-to-oms-using-the-settings-app"></a><span data-ttu-id="4cd3f-140">Подключение устройств Surface Hub к OMS с помощью приложения Settings</span><span class="sxs-lookup"><span data-stu-id="4cd3f-140">Connect Surface Hubs to OMS using the Settings app</span></span>
<span data-ttu-id="4cd3f-141">Вам потребуется идентификатор и ключ для рабочей области OMS, которая будет управлять устройствами Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-141">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="4cd3f-142">Их можно получить на портале OMS.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-142">You can get those from the OMS portal.</span></span>

<span data-ttu-id="4cd3f-143">Если для управления средой не используется Intune, вы можете зарегистрировать устройства вручную в **параметрах** каждого устройства Surface Hub:</span><span class="sxs-lookup"><span data-stu-id="4cd3f-143">If you don't use Intune to manage your environment, you can enroll devices manually through **Settings** on each Surface Hub:</span></span>

1. <span data-ttu-id="4cd3f-144">На устройстве Surface Hub откройте приложение **Settings**.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-144">From your Surface Hub, open **Settings**.</span></span>
2. <span data-ttu-id="4cd3f-145">Введите учетные данные администратора устройства при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-145">Enter the device admin credentials when prompted.</span></span>
3. <span data-ttu-id="4cd3f-146">Щелкните **This device** (Это устройство), затем в разделе **Monitoring** (Мониторинг) нажмите кнопку **Configure OMS Settings** (Настроить параметры OMS).</span><span class="sxs-lookup"><span data-stu-id="4cd3f-146">Click **This device**, and the under **Monitoring**, click **Configure OMS Settings**.</span></span>
4. <span data-ttu-id="4cd3f-147">Выберите **Enable monitoring** (Включить мониторинг).</span><span class="sxs-lookup"><span data-stu-id="4cd3f-147">Select **Enable monitoring**.</span></span>
5. <span data-ttu-id="4cd3f-148">В диалоговом окне настроек OMS введите **Workspace ID** (Идентификатор рабочей области) и **Workspace Key** (Ключ рабочей области).</span><span class="sxs-lookup"><span data-stu-id="4cd3f-148">In the OMS settings dialog, type the **Workspace ID** and type the **Workspace Key**.</span></span>  
   <span data-ttu-id="4cd3f-149">![параметры](./media/log-analytics-surface-hubs/settings.png)</span><span class="sxs-lookup"><span data-stu-id="4cd3f-149">![settings](./media/log-analytics-surface-hubs/settings.png)</span></span>
6. <span data-ttu-id="4cd3f-150">Нажмите кнопку **ОК**, чтобы завершить настройку.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-150">Click **OK** to complete the configuration.</span></span>

<span data-ttu-id="4cd3f-151">Появится подтверждение с сообщением о том, удалось ли применить конфигурацию OMS к устройству.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-151">A confirmation appears telling you whether or not the OMS configuration was successfully applied to the device.</span></span> <span data-ttu-id="4cd3f-152">Если да, появится сообщение о том, что агент успешно подключен к службе OMS.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-152">If it was, a message appears stating that the agent successfully connected to the OMS service.</span></span> <span data-ttu-id="4cd3f-153">Затем устройство начнет отправку данных в OMS, где эти данные можно просматривать и обрабатывать.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-153">The device then starts sending data to OMS where you can view and act on it.</span></span>

## <a name="monitor-surface-hubs"></a><span data-ttu-id="4cd3f-154">Мониторинг устройств Surface Hub</span><span class="sxs-lookup"><span data-stu-id="4cd3f-154">Monitor Surface Hubs</span></span>
<span data-ttu-id="4cd3f-155">Мониторинг устройств Surface Hub с помощью OMS во многом напоминает мониторинг любых других зарегистрированных устройств.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-155">Monitoring your Surface Hubs using OMS is much like monitoring any other enrolled devices.</span></span>

1. <span data-ttu-id="4cd3f-156">Войдите на портал OMS.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-156">Sign in to the OMS portal.</span></span>
2. <span data-ttu-id="4cd3f-157">Перейдите на панель мониторинга пакета решений Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-157">Navigate to the Surface Hub solution pack dashboard.</span></span>
3. <span data-ttu-id="4cd3f-158">Отобразится состояние работоспособности устройства.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-158">Your device's health is displayed.</span></span>

   ![Панель мониторинга Surface Hub](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

<span data-ttu-id="4cd3f-160">Можно создавать [оповещения](log-analytics-alerts.md) на основе существующих или настраиваемых поисковых запросов к журналу.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-160">You can create [alerts](log-analytics-alerts.md) based on existing or custom log searches.</span></span> <span data-ttu-id="4cd3f-161">Используя данные, собираемые службой OMS с устройств Surface Hubs, можно выполнять поиск проблем и получать оповещения, которые отправляются при выполнении условий, заданных вами для устройств.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-161">Using the data the OMS collects from your Surface Hubs, you can search for issues and alert on the conditions that you define for your devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4cd3f-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4cd3f-162">Next steps</span></span>
* <span data-ttu-id="4cd3f-163">Используйте [Поиск по журналам в Log Analytics](log-analytics-log-searches.md) для просмотра подробных данных о Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-163">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Surface Hub data.</span></span>
* <span data-ttu-id="4cd3f-164">Создайте [оповещения](log-analytics-alerts.md), которые будут уведомлять вас о возникновении проблем с устройствами Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="4cd3f-164">Create [alerts](log-analytics-alerts.md) to notify you when issues occur with your Surface Hubs.</span></span>
