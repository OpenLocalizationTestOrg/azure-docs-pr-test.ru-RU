---
title: "tooAzure компьютеры Windows aaaConnect анализа журналов | Документы Microsoft"
description: "В этой статье показано компьютеров Windows hello tooconnect действия hello в вашей локальной инфраструктуры toohello службы анализа журналов с помощью настроенной версии hello агента наблюдения Майкрософт (MMA)."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a><span data-ttu-id="1d859-103">Подключение службы анализа журналов toohello компьютеров Windows в Azure</span><span class="sxs-lookup"><span data-stu-id="1d859-103">Connect Windows computers toohello Log Analytics service in Azure</span></span>

<span data-ttu-id="1d859-104">В этой статье представлены действия hello tooconnect Windows компьютеры в рабочих областях tooOMS локальной инфраструктуры с помощью настроенной версии hello агента наблюдения Майкрософт (MMA).</span><span class="sxs-lookup"><span data-stu-id="1d859-104">This article shows hello steps tooconnect Windows computers in your on-premises infrastructure tooOMS workspaces by using a customized version of hello Microsoft Monitoring Agent (MMA).</span></span> <span data-ttu-id="1d859-105">Требуется tooinstall и подключения агентов для всех компьютеров hello требуется tooonboard для них службы анализа журналов toohello toosend данных и tooview и act на этих данных.</span><span class="sxs-lookup"><span data-stu-id="1d859-105">You need tooinstall and connect agents for all of hello computers that you want tooonboard in order for them toosend data toohello Log Analytics service and tooview and act on that data.</span></span> <span data-ttu-id="1d859-106">Каждый агент может передавать toomultiple рабочих областей.</span><span class="sxs-lookup"><span data-stu-id="1d859-106">Each agent can report toomultiple workspaces.</span></span>

<span data-ttu-id="1d859-107">Установить агенты можно с помощью программы установки, командной строки или DSC (настройки требуемого состояния) в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="1d859-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span></span>  

>[!NOTE]
<span data-ttu-id="1d859-108">Для виртуальных машин, работающих в Azure, можно упростить установку с помощью hello [расширение виртуальной машины](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="1d859-108">For virtual machines running in Azure, you can simplify installation by using hello [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="1d859-109">На компьютерах с подключением к Интернету hello агент использует данные hello подключения toohello Internet toosend tooOMS.</span><span class="sxs-lookup"><span data-stu-id="1d859-109">On computers with Internet connectivity, hello agent uses hello connection toohello Internet toosend data tooOMS.</span></span> <span data-ttu-id="1d859-110">Для компьютеров, не подключен к Интернету, можно использовать прокси-сервер или hello [шлюза OMS](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="1d859-110">For computers that do not have Internet connectivity, you can use a proxy or hello [OMS Gateway](log-analytics-oms-gateway.md).</span></span>

<span data-ttu-id="1d859-111">Подключение к tooOMS компьютеров Windows выполняется просто с помощью трех простых шагов:</span><span class="sxs-lookup"><span data-stu-id="1d859-111">Connecting your Windows computers tooOMS is straightforward using three simple steps:</span></span>

1. <span data-ttu-id="1d859-112">Загрузка файла установки агента hello из портала OMS hello</span><span class="sxs-lookup"><span data-stu-id="1d859-112">Download hello agent setup file from hello OMS portal</span></span>
2. <span data-ttu-id="1d859-113">Установка агента hello, с помощью выбранного метода hello</span><span class="sxs-lookup"><span data-stu-id="1d859-113">Install hello agent using hello method you choose</span></span>
3. <span data-ttu-id="1d859-114">Настройка агента hello или добавление дополнительных рабочих областей, при необходимости</span><span class="sxs-lookup"><span data-stu-id="1d859-114">Configure hello agent or add additional workspaces, if necessary</span></span>

<span data-ttu-id="1d859-115">Hello следующей схеме показаны hello отношения между компьютерами Windows и OMS после установки и агенты.</span><span class="sxs-lookup"><span data-stu-id="1d859-115">hello following diagram shows hello relationship between your Windows computers and OMS after you’ve installed and configured agents.</span></span>

![oms-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

<span data-ttu-id="1d859-117">Если политики безопасности ИТ запретить компьютеры toohello tooconnect вашей сети Интернет, можно настроить вашей toohello tooconnect компьютеров OMS шлюза.</span><span class="sxs-lookup"><span data-stu-id="1d859-117">If your IT security policies do not allow computers on your network tooconnect toohello Internet, you can configure your computers tooconnect toohello OMS Gateway.</span></span> <span data-ttu-id="1d859-118">Дополнительные сведения и инструкции по tooconfigure вашей toocommunicate серверы через службу OMS toohello шлюза OMS. в статье [подключения tooOMS компьютеров с помощью шлюза OMS hello](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="1d859-118">For more information and steps on how tooconfigure your servers toocommunicate through an OMS Gateway toohello OMS service, see [Connect computers tooOMS using hello OMS Gateway](log-analytics-oms-gateway.md).</span></span>

## <a name="system-requirements-and-required-configuration"></a><span data-ttu-id="1d859-119">Системные требования и необходимая конфигурация</span><span class="sxs-lookup"><span data-stu-id="1d859-119">System requirements and required configuration</span></span>
<span data-ttu-id="1d859-120">Перед началом установки или развертывания агентов, просмотрите следующие сведения о tooensure требованиям hello hello.</span><span class="sxs-lookup"><span data-stu-id="1d859-120">Before you install or deploy agents, review hello following details tooensure you meet hello requirements.</span></span>

- <span data-ttu-id="1d859-121">Hello OMS MMA можно установить только на компьютерах под управлением Windows Server 2008 (SP2), 1 или более поздней версии или Windows 7 с пакетом обновления 1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="1d859-121">You can only install hello OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span></span>
- <span data-ttu-id="1d859-122">Вам понадобится подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="1d859-122">You need an Azure subscription.</span></span>  <span data-ttu-id="1d859-123">Дополнительные сведения см. в статье [Начало работы с Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1d859-123">For more information, see [Get started with Log Analytics](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="1d859-124">Каждый компьютер Windows должен быть toohello может tooconnect Интернет с помощью протокола HTTPS или toohello OMS шлюза.</span><span class="sxs-lookup"><span data-stu-id="1d859-124">Each Windows computer must be able tooconnect toohello Internet using HTTPS or toohello OMS Gateway.</span></span> <span data-ttu-id="1d859-125">Это подключение может быть прямой через прокси-сервер, или hello OMS шлюза.</span><span class="sxs-lookup"><span data-stu-id="1d859-125">This connection can be direct, via a proxy, or through hello OMS Gateway.</span></span>
- <span data-ttu-id="1d859-126">Hello OMS MMA можно установить на автономных компьютерах, серверах и виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="1d859-126">You can install hello OMS MMA on stand-alone computers, servers, and virtual machines.</span></span> <span data-ttu-id="1d859-127">Если tooOMS tooconnect виртуальных машин, размещенных в Azure, см. [tooLog виртуальных машин подключение Azure Analytics](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="1d859-127">If you want tooconnect Azure-hosted virtual machines tooOMS, see [Connect Azure virtual machines tooLog Analytics](log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="1d859-128">Hello агент должен toouse TCP-порт 443 для различных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1d859-128">hello agent needs toouse TCP port 443 for various resources.</span></span>

### <a name="network"></a><span data-ttu-id="1d859-129">Сеть</span><span class="sxs-lookup"><span data-stu-id="1d859-129">Network</span></span>

<span data-ttu-id="1d859-130">Windows агентов регистрации tooand tooconnect со службой OMS hello они должны иметь доступ к ресурсам toonetwork, включая номера портов hello и URL-адреса домена.</span><span class="sxs-lookup"><span data-stu-id="1d859-130">For Windows agents tooconnect tooand register with hello OMS service, they must have access toonetwork resources, including hello port numbers and domain URLs.</span></span>

- <span data-ttu-id="1d859-131">Для прокси-серверов необходимо tooensure, hello нужный прокси-сервер, ресурсы настраиваются в параметрах агента.</span><span class="sxs-lookup"><span data-stu-id="1d859-131">For proxy servers, you need tooensure that hello appropriate proxy server resources are configured in agent settings.</span></span>
- <span data-ttu-id="1d859-132">Брандмауэры, ограничивающие toohello доступа к Интернету вы или сетевых специалистов должны tooconfigure tooOMS доступа toopermit вашего брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="1d859-132">For firewalls that restrict access toohello Internet, you or your networking engineers need tooconfigure your firewall toopermit access tooOMS.</span></span> <span data-ttu-id="1d859-133">Настройка параметров агента не требуется.</span><span class="sxs-lookup"><span data-stu-id="1d859-133">No action is needed in agent settings.</span></span>

<span data-ttu-id="1d859-134">Привет, в следующей таблице показаны ресурсы, необходимые для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="1d859-134">hello following table shows resources needed for communication.</span></span>

>[!NOTE]
><span data-ttu-id="1d859-135">Некоторые из hello следующие ресурсы ссылаются оперативной аналитики, который был ранее назывался анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="1d859-135">Some of hello following resources mention Operational Insights, which was a previous name for Log Analytics.</span></span>

| <span data-ttu-id="1d859-136">Ресурс агента</span><span class="sxs-lookup"><span data-stu-id="1d859-136">Agent Resource</span></span> | <span data-ttu-id="1d859-137">порты;</span><span class="sxs-lookup"><span data-stu-id="1d859-137">Ports</span></span> | <span data-ttu-id="1d859-138">Обход проверки HTTPS</span><span class="sxs-lookup"><span data-stu-id="1d859-138">Bypass HTTPS inspection</span></span> |
|---|---|---|
| <span data-ttu-id="1d859-139">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="1d859-139">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="1d859-140">443</span><span class="sxs-lookup"><span data-stu-id="1d859-140">443</span></span> | <span data-ttu-id="1d859-141">Да</span><span class="sxs-lookup"><span data-stu-id="1d859-141">Yes</span></span> |
| <span data-ttu-id="1d859-142">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="1d859-142">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="1d859-143">443</span><span class="sxs-lookup"><span data-stu-id="1d859-143">443</span></span> | <span data-ttu-id="1d859-144">Да</span><span class="sxs-lookup"><span data-stu-id="1d859-144">Yes</span></span> |
| <span data-ttu-id="1d859-145">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="1d859-145">*.blob.core.windows.net</span></span> | <span data-ttu-id="1d859-146">443</span><span class="sxs-lookup"><span data-stu-id="1d859-146">443</span></span> | <span data-ttu-id="1d859-147">Да</span><span class="sxs-lookup"><span data-stu-id="1d859-147">Yes</span></span> |
| <span data-ttu-id="1d859-148">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="1d859-148">*.azure-automation.net</span></span> | <span data-ttu-id="1d859-149">443</span><span class="sxs-lookup"><span data-stu-id="1d859-149">443</span></span> | <span data-ttu-id="1d859-150">Да</span><span class="sxs-lookup"><span data-stu-id="1d859-150">Yes</span></span> |



## <a name="download-hello-agent-setup-file-from-oms"></a><span data-ttu-id="1d859-151">Загрузите файл установки hello агента с OMS</span><span class="sxs-lookup"><span data-stu-id="1d859-151">Download hello agent setup file from OMS</span></span>
1. <span data-ttu-id="1d859-152">На портале OMS hello, hello **Обзор** щелкните hello **параметры** плитки.</span><span class="sxs-lookup"><span data-stu-id="1d859-152">In hello OMS portal, on hello **Overview** page, click hello **Settings** tile.</span></span>  <span data-ttu-id="1d859-153">Нажмите кнопку hello **подключенные источники** вкладку вверху hello.</span><span class="sxs-lookup"><span data-stu-id="1d859-153">Click hello **Connected Sources** tab at hello top.</span></span>  
    <span data-ttu-id="1d859-154">![Вкладка "Подключенные источники"](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span><span class="sxs-lookup"><span data-stu-id="1d859-154">![Connected Sources tab](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span></span>
2. <span data-ttu-id="1d859-155">Нажмите кнопку **серверов Windows** и нажмите кнопку **загрузить агент Windows** применимо tooyour тип процессора компьютера toodownload файл установки hello.</span><span class="sxs-lookup"><span data-stu-id="1d859-155">Click **Windows Servers** and then click **Download Windows Agent** applicable tooyour computer processor type toodownload hello setup file.</span></span>
3. <span data-ttu-id="1d859-156">На hello справа от **идентификатор рабочей области**нажмите значок копирования hello и вставьте идентификатор hello в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="1d859-156">On hello right of **Workspace ID**, click hello copy icon and paste hello ID into Notepad.</span></span>
4. <span data-ttu-id="1d859-157">На hello справа от **первичного ключа**нажмите значок копирования hello и вставьте ключ hello в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="1d859-157">On hello right of **Primary Key**, click hello copy icon and paste hello key into Notepad.</span></span>     

## <a name="install-hello-agent-using-setup"></a><span data-ttu-id="1d859-158">Установка агента hello, с помощью программы установки</span><span class="sxs-lookup"><span data-stu-id="1d859-158">Install hello agent using setup</span></span>
1. <span data-ttu-id="1d859-159">Запустите программу установки tooinstall hello на компьютере, которые должны toomanage.</span><span class="sxs-lookup"><span data-stu-id="1d859-159">Run Setup tooinstall hello agent on a computer that you want toomanage.</span></span>
2. <span data-ttu-id="1d859-160">На начальной странице приветствия нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="1d859-160">On hello Welcome page, click **Next**.</span></span>
3. <span data-ttu-id="1d859-161">На странице приветствия условия лицензионного соглашения, прочтите hello лицензии и нажмите кнопку **принимаю**.</span><span class="sxs-lookup"><span data-stu-id="1d859-161">On hello License Terms page, read hello license and then click **I Agree**.</span></span>
4. <span data-ttu-id="1d859-162">На странице приветствия конечную папку, изменить или оставьте папку установки по умолчанию hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="1d859-162">On hello Destination Folder page, change or keep hello default installation folder and then click **Next**.</span></span>
5. <span data-ttu-id="1d859-163">На странице приветствия параметры установки агента вы можете tooconnect hello tooAzure агента анализа журналов (OMS), Operations Manager, либо hello вариантов можно оставить пустым, если требуется агент tooconfigure hello позже.</span><span class="sxs-lookup"><span data-stu-id="1d859-163">On hello Agent Setup Options page, you can choose tooconnect hello agent tooAzure Log Analytics (OMS), Operations Manager, or you can leave hello choices blank if you want tooconfigure hello agent later.</span></span> <span data-ttu-id="1d859-164">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="1d859-164">Click **Next**.</span></span>   
    - <span data-ttu-id="1d859-165">Если вы выбрали tooconnect tooAzure аналитика журналов (OMS), вставьте hello **идентификатор рабочей области** и **ключ рабочей области (первичный ключ)** , скопированные в Блокнот в предыдущей процедуре hello и нажмите кнопку  **Далее**.</span><span class="sxs-lookup"><span data-stu-id="1d859-165">If you chose tooconnect tooAzure Log Analytics (OMS), paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in hello previous procedure and then click **Next**.</span></span>  
        <span data-ttu-id="1d859-166">![Вставка идентификатора рабочей области и первичного ключа](./media/log-analytics-windows-agents/connect-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="1d859-166">![paste Workspace ID and Primary Key](./media/log-analytics-windows-agents/connect-workspace.png)</span></span>
    - <span data-ttu-id="1d859-167">Если выбрана tooconnect tooOperations Manager, введите hello **имя группы управления**, **сервера управления** имя, и **порт сервера управления**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="1d859-167">If you chose tooconnect tooOperations Manager, type hello **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span></span> <span data-ttu-id="1d859-168">На странице приветствия учетная запись действия агента выберите hello локальной системной учетной записью или учетной записью локального домена и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="1d859-168">On hello Agent Action Account page, choose either hello Local System account or a local domain account and then click **Next**.</span></span>  
        <span data-ttu-id="1d859-169">![конфигурация группы управления](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![учетная запись действия агента](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span><span class="sxs-lookup"><span data-stu-id="1d859-169">![management group configuration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span></span>

6. <span data-ttu-id="1d859-170">На странице готовности tooInstall hello, просмотрите выбранные параметры и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="1d859-170">On hello Ready tooInstall page, review your choices and then click **Install**.</span></span>
7. <span data-ttu-id="1d859-171">На hello Настройка успешно завершена и щелкните **Готово**.</span><span class="sxs-lookup"><span data-stu-id="1d859-171">On hello Configuration completed successfully page, click **Finish**.</span></span>
8. <span data-ttu-id="1d859-172">По завершении hello **Microsoft Monitoring Agent** отображается в **панели управления**.</span><span class="sxs-lookup"><span data-stu-id="1d859-172">When complete, hello **Microsoft Monitoring Agent** appears in **Control Panel**.</span></span> <span data-ttu-id="1d859-173">Можно просмотреть конфигурацию существует и убедитесь, что этот агент hello подключенных tooOperational Insights (OMS).</span><span class="sxs-lookup"><span data-stu-id="1d859-173">You can review your configuration there and verify that hello agent is connected tooOperational Insights (OMS).</span></span> <span data-ttu-id="1d859-174">При подключенном tooOMS hello агента отображается сообщение, указывающее: **hello Microsoft Monitoring Agent успешно подключен toohello службы Microsoft Operations Management Suite.**</span><span class="sxs-lookup"><span data-stu-id="1d859-174">When connected tooOMS, hello agent displays a message stating: **hello Microsoft Monitoring Agent has successfully connected toohello Microsoft Operations Management Suite service.**</span></span>

## <a name="configure-proxy-settings"></a><span data-ttu-id="1d859-175">Настройка параметров прокси</span><span class="sxs-lookup"><span data-stu-id="1d859-175">Configure proxy settings</span></span>

<span data-ttu-id="1d859-176">Можно использовать следующие параметры прокси-сервера tooconfigure процедуры для hello Microsoft Monitoring Agent с помощью панели управления hello.</span><span class="sxs-lookup"><span data-stu-id="1d859-176">You can use hello following procedure tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel.</span></span> <span data-ttu-id="1d859-177">Необходимо toouse эту процедуру для каждого сервера.</span><span class="sxs-lookup"><span data-stu-id="1d859-177">You need toouse this procedure for each server.</span></span> <span data-ttu-id="1d859-178">Если у вас есть много серверов, что вам нужно tooconfigure, может оказаться проще toouse tooautomate сценария этот процесс.</span><span class="sxs-lookup"><span data-stu-id="1d859-178">If you have many servers that you need tooconfigure, you might find it easier toouse a script tooautomate this process.</span></span> <span data-ttu-id="1d859-179">Если это так, см. далее процедуре hello [tooconfigure параметры прокси-сервера для Microsoft Monitoring Agent с помощью скрипта hello](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span><span class="sxs-lookup"><span data-stu-id="1d859-179">If so, see hello next procedure [tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span></span>

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a><span data-ttu-id="1d859-180">параметры прокси-сервера tooconfigure для hello Microsoft Monitoring Agent с помощью панели управления</span><span class="sxs-lookup"><span data-stu-id="1d859-180">tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel</span></span>
1. <span data-ttu-id="1d859-181">Откройте **Панель управления**.</span><span class="sxs-lookup"><span data-stu-id="1d859-181">Open **Control Panel**.</span></span>
2. <span data-ttu-id="1d859-182">Откройте **Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="1d859-182">Open **Microsoft Monitoring Agent**.</span></span>
3. <span data-ttu-id="1d859-183">Нажмите кнопку hello **параметры прокси-сервера** вкладки.</span><span class="sxs-lookup"><span data-stu-id="1d859-183">Click hello **Proxy Settings** tab.</span></span>  
    <span data-ttu-id="1d859-184">![вкладка параметров прокси-сервера](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span><span class="sxs-lookup"><span data-stu-id="1d859-184">![proxy settings tab](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span></span>
4. <span data-ttu-id="1d859-185">Выберите **использовать прокси-сервер** и введите hello URL-адреса и порта номер, если такой необходимости, аналогичные toohello примере показано.</span><span class="sxs-lookup"><span data-stu-id="1d859-185">Select **Use a proxy server** and type hello URL and port number, if one is needed, similar toohello example shown.</span></span> <span data-ttu-id="1d859-186">Если прокси-сервер требует проверки подлинности, введите hello имя пользователя и пароль tooaccess hello прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="1d859-186">If your proxy server requires authentication, type hello username and password tooaccess hello proxy server.</span></span>


### <a name="verify-agent-connectivity-toooms"></a><span data-ttu-id="1d859-187">Проверьте подключение tooOMS агента</span><span class="sxs-lookup"><span data-stu-id="1d859-187">Verify agent connectivity tooOMS</span></span>

<span data-ttu-id="1d859-188">Можно легко проверить, является ли агенты взаимодействуют с OMS с помощью процедуры hello:</span><span class="sxs-lookup"><span data-stu-id="1d859-188">You can easily verify whether your agents are communicating with OMS using hello following procedure:</span></span>

1.  <span data-ttu-id="1d859-189">На компьютере с агентом Windows hello hello откройте панель управления.</span><span class="sxs-lookup"><span data-stu-id="1d859-189">On hello computer with hello Windows agent, open Control Panel.</span></span>
2.  <span data-ttu-id="1d859-190">Откройте "Microsoft Monitoring Agent".</span><span class="sxs-lookup"><span data-stu-id="1d859-190">Open Microsoft Monitoring Agent.</span></span>
3.  <span data-ttu-id="1d859-191">Перейдите на вкладку hello анализа журналов Azure (OMS).</span><span class="sxs-lookup"><span data-stu-id="1d859-191">Click hello Azure Log Analytics (OMS) tab.</span></span>
4.  <span data-ttu-id="1d859-192">В столбце состояния hello вы увидите этот агент hello успешно подключения службы toohello Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="1d859-192">In hello Status column, you should see that hello agent connected successfully toohello Operations Management Suite service.</span></span>

![Агент подключен](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a><span data-ttu-id="1d859-194">параметры прокси-сервера tooconfigure для hello Microsoft Monitoring Agent с помощью скрипта</span><span class="sxs-lookup"><span data-stu-id="1d859-194">tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script</span></span>
<span data-ttu-id="1d859-195">Скопируйте hello следующие образцы, обновить его, используя сведения о конкретных tooyour среды, сохраните его с расширением PS1 и запустите скрипт hello на каждом компьютере, который подключается непосредственно toohello службой OMS.</span><span class="sxs-lookup"><span data-stu-id="1d859-195">Copy hello following sample, update it with information specific tooyour environment, save it with a PS1 file name extension, and then run hello script on each computer that connects directly toohello OMS service.</span></span>

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a><span data-ttu-id="1d859-196">Установка агента hello, с помощью командной строки hello</span><span class="sxs-lookup"><span data-stu-id="1d859-196">Install hello agent using hello command line</span></span>
- <span data-ttu-id="1d859-197">Изменения, а затем используйте следующий пример tooinstall hello агента с помощью командной строки hello hello.</span><span class="sxs-lookup"><span data-stu-id="1d859-197">Modify and then use hello following example tooinstall hello agent using hello command line.</span></span> <span data-ttu-id="1d859-198">пример Hello выполняет полностью автоматической установки.</span><span class="sxs-lookup"><span data-stu-id="1d859-198">hello example performs a fully silent installation.</span></span>

    >[!NOTE]
    <span data-ttu-id="1d859-199">Tooupgrade агент, вы должны toouse hello анализа журналов API сценариев.</span><span class="sxs-lookup"><span data-stu-id="1d859-199">If you want tooupgrade an agent, you need toouse hello Log Analytics scripting API.</span></span> <span data-ttu-id="1d859-200">В разделе tooupgrade далее разделе hello агента.</span><span class="sxs-lookup"><span data-stu-id="1d859-200">See hello next section tooupgrade an agent.</span></span>

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

<span data-ttu-id="1d859-201">Hello агент использует в качестве его самораспаковывающегося IExpress с помощью hello `/c` команды.</span><span class="sxs-lookup"><span data-stu-id="1d859-201">hello agent uses IExpress as its self-extractor using hello `/c` command.</span></span> <span data-ttu-id="1d859-202">Вы увидите hello параметры командной строки в [параметры командной строки для IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) и затем обновление hello toosuit примере вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="1d859-202">You can see hello command-line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update hello example toosuit your needs.</span></span>

|<span data-ttu-id="1d859-203">Параметры MMA</span><span class="sxs-lookup"><span data-stu-id="1d859-203">MMA-specific options</span></span>                   |<span data-ttu-id="1d859-204">Примечания</span><span class="sxs-lookup"><span data-stu-id="1d859-204">Notes</span></span>         |
|---------------------------------------|--------------|
|<span data-ttu-id="1d859-205">ADD_OPINSIGHTS_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="1d859-205">ADD_OPINSIGHTS_WORKSPACE</span></span>               | <span data-ttu-id="1d859-206">1 = Настройка hello агента tooreport tooa рабочей области</span><span class="sxs-lookup"><span data-stu-id="1d859-206">1 = Configure hello agent tooreport tooa workspace</span></span>                |
|<span data-ttu-id="1d859-207">OPINSIGHTS_WORKSPACE_ID</span><span class="sxs-lookup"><span data-stu-id="1d859-207">OPINSIGHTS_WORKSPACE_ID</span></span>                | <span data-ttu-id="1d859-208">Идентификатор рабочей области (guid) для рабочей области tooadd hello</span><span class="sxs-lookup"><span data-stu-id="1d859-208">Workspace Id (guid) for hello workspace tooadd</span></span>                    |
|<span data-ttu-id="1d859-209">OPINSIGHTS_WORKSPACE_KEY</span><span class="sxs-lookup"><span data-stu-id="1d859-209">OPINSIGHTS_WORKSPACE_KEY</span></span>               | <span data-ttu-id="1d859-210">Проверки подлинности рабочей области, ключей используется tooinitially с рабочей областью hello</span><span class="sxs-lookup"><span data-stu-id="1d859-210">Workspace key used tooinitially authenticate with hello workspace</span></span> |
|<span data-ttu-id="1d859-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span><span class="sxs-lookup"><span data-stu-id="1d859-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span></span>  | <span data-ttu-id="1d859-212">Укажите hello облачной среде, где находится hello рабочей области</span><span class="sxs-lookup"><span data-stu-id="1d859-212">Specify hello cloud environment where hello workspace is located</span></span> <br> <span data-ttu-id="1d859-213">0 — коммерческое облако Azure (по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="1d859-213">0 = Azure commercial cloud (default)</span></span> <br> <span data-ttu-id="1d859-214">1 — Azure для государственных организаций.</span><span class="sxs-lookup"><span data-stu-id="1d859-214">1 = Azure Government</span></span> |
|<span data-ttu-id="1d859-215">OPINSIGHTS_PROXY_URL</span><span class="sxs-lookup"><span data-stu-id="1d859-215">OPINSIGHTS_PROXY_URL</span></span>               | <span data-ttu-id="1d859-216">URI для hello toouse прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="1d859-216">URI for hello proxy toouse</span></span> |
|<span data-ttu-id="1d859-217">OPINSIGHTS_PROXY_USERNAME</span><span class="sxs-lookup"><span data-stu-id="1d859-217">OPINSIGHTS_PROXY_USERNAME</span></span>               | <span data-ttu-id="1d859-218">Имя пользователя tooaccess проверенный прокси-сервер</span><span class="sxs-lookup"><span data-stu-id="1d859-218">Username tooaccess an authenticated proxy</span></span> |
|<span data-ttu-id="1d859-219">OPINSIGHTS_PROXY_PASSWORD</span><span class="sxs-lookup"><span data-stu-id="1d859-219">OPINSIGHTS_PROXY_PASSWORD</span></span>               | <span data-ttu-id="1d859-220">Пароль tooaccess проверенный прокси-сервер</span><span class="sxs-lookup"><span data-stu-id="1d859-220">Password tooaccess an authenticated proxy</span></span> |

>[!NOTE]
<span data-ttu-id="1d859-221">ограничение попадание Длина командной строки hello tooavoid IExpress, установка hello агента с настроена рабочая область, а затем используйте tooset скрипт конфигурации для рабочей области hello.</span><span class="sxs-lookup"><span data-stu-id="1d859-221">tooavoid hitting hello command-line length limit of IExpress, install hello agent with no workspace configured and then use a script tooset configuration for hello workspace.</span></span>

>[!NOTE]
<span data-ttu-id="1d859-222">Если вы получаете `Command line option syntax error.` при использовании hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` параметр, можно использовать следующие инструкции по решению hello:</span><span class="sxs-lookup"><span data-stu-id="1d859-222">If you get a `Command line option syntax error.` when using hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, you can use hello following workaround:</span></span>
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a><span data-ttu-id="1d859-223">Добавление рабочей области с помощью сценария</span><span class="sxs-lookup"><span data-stu-id="1d859-223">Add a workspace using a script</span></span>
<span data-ttu-id="1d859-224">Добавление рабочей области с помощью API сценариев агента анализа журналов hello с hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="1d859-224">Add a workspace using hello Log Analytics agent scripting API with hello following example:</span></span>

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

<span data-ttu-id="1d859-225">tooadd рабочую область в Azure для правительства США, hello используйте следующий пример сценария:</span><span class="sxs-lookup"><span data-stu-id="1d859-225">tooadd a workspace in Azure for US Government, use hello following script sample:</span></span>
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
<span data-ttu-id="1d859-226">Если использовали hello командной строки или скрипта ранее tooinstall или настройки агента hello `EnableAzureOperationalInsights` была заменена `AddCloudWorkspace`.</span><span class="sxs-lookup"><span data-stu-id="1d859-226">If you've used hello command line or script previously tooinstall or configure hello agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span></span>

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a><span data-ttu-id="1d859-227">Установка агента hello, с помощью DSC службы автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="1d859-227">Install hello agent using DSC in Azure Automation</span></span>

<span data-ttu-id="1d859-228">Можно использовать следующий скрипт tooinstall пример hello агента с помощью DSC службы автоматизации Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1d859-228">You can use hello following script example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="1d859-229">пример Hello устанавливает hello 64-разрядный агент, обозначенную hello `URI` значение.</span><span class="sxs-lookup"><span data-stu-id="1d859-229">hello example installs hello 64-bit agent, identified by hello `URI` value.</span></span> <span data-ttu-id="1d859-230">Также можно использовать 32-разрядная версия hello, заменив значение URI hello.</span><span class="sxs-lookup"><span data-stu-id="1d859-230">You can also use hello 32-bit version by replacing hello URI value.</span></span> <span data-ttu-id="1d859-231">Ниже приведены Hello идентификаторы URI для обеих версий.</span><span class="sxs-lookup"><span data-stu-id="1d859-231">hello URIs for both versions are:</span></span>

- <span data-ttu-id="1d859-232">64-разрядный агент Windows: https://go.microsoft.com/fwlink/?LinkId=828603</span><span class="sxs-lookup"><span data-stu-id="1d859-232">Windows 64-bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span></span>
- <span data-ttu-id="1d859-233">32-разрядный агент Windows: https://go.microsoft.com/fwlink/?LinkId=828604</span><span class="sxs-lookup"><span data-stu-id="1d859-233">Windows 32-bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span></span>


>[!NOTE]
<span data-ttu-id="1d859-234">В этом примере процедура и сценарий не выполняют обновление существующего агента.</span><span class="sxs-lookup"><span data-stu-id="1d859-234">This procedure and script example will not upgrade an existing agent.</span></span>

1. <span data-ttu-id="1d859-235">Импорт xPSDesiredStateConfiguration hello DSC-модуль из [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) в службу автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="1d859-235">Import hello xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span></span>  
2.  <span data-ttu-id="1d859-236">Создайте в службе автоматизации Azure ресурсы-контейнеры для переменных *OPSINSIGHTS_WS_ID* и *OPSINSIGHTS_WS_KEY*.</span><span class="sxs-lookup"><span data-stu-id="1d859-236">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span></span> <span data-ttu-id="1d859-237">Задать *OPSINSIGHTS_WS_ID* tooyour идентификатор рабочей области аналитики журналов OMS и задайте *OPSINSIGHTS_WS_KEY* toohello первичный ключ рабочей области.</span><span class="sxs-lookup"><span data-stu-id="1d859-237">Set *OPSINSIGHTS_WS_ID* tooyour OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* toohello primary key of your workspace.</span></span>
3.  <span data-ttu-id="1d859-238">Использовать hello следующий скрипт и сохраните его как MMAgent.ps1</span><span class="sxs-lookup"><span data-stu-id="1d859-238">Use hello following script and save it as MMAgent.ps1</span></span>
4.  <span data-ttu-id="1d859-239">Изменения, а затем используйте следующий пример tooinstall hello агента с помощью DSC службы автоматизации Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1d859-239">Modify and then use hello following example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="1d859-240">Импорт MMAgent.ps1 автоматизации Azure с помощью интерфейса автоматизации Azure hello или командлета.</span><span class="sxs-lookup"><span data-stu-id="1d859-240">Import MMAgent.ps1 into Azure Automation by using hello Azure Automation interface or cmdlet.</span></span>
5.  <span data-ttu-id="1d859-241">Назначение toohello конфигурации узла.</span><span class="sxs-lookup"><span data-stu-id="1d859-241">Assign a node toohello configuration.</span></span> <span data-ttu-id="1d859-242">В течение 15 минут hello узел проверяет свою конфигурацию и hello MMA помещается toohello узла.</span><span class="sxs-lookup"><span data-stu-id="1d859-242">Within 15 minutes, hello node checks its configuration and hello MMA is pushed toohello node.</span></span>

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-hello-latest-productid-value"></a><span data-ttu-id="1d859-243">Получить последнее значение ProductId hello</span><span class="sxs-lookup"><span data-stu-id="1d859-243">Get hello latest ProductId value</span></span>

<span data-ttu-id="1d859-244">Hello `ProductId value` в hello MMAgent.ps1 сценария является уникальным tooeach версия агента.</span><span class="sxs-lookup"><span data-stu-id="1d859-244">hello `ProductId value` in hello MMAgent.ps1 script is unique tooeach agent version.</span></span> <span data-ttu-id="1d859-245">При публикации обновленную версию каждого агента, изменяет значение ProductId hello.</span><span class="sxs-lookup"><span data-stu-id="1d859-245">When an updated version of each agent is published, hello ProductId value changes.</span></span> <span data-ttu-id="1d859-246">Таким образом при hello ProductId изменения в будущем hello, можно найти с помощью простого скрипта версия агента hello.</span><span class="sxs-lookup"><span data-stu-id="1d859-246">So, when hello ProductId changes in hello future, you can find hello agent version using a simple script.</span></span> <span data-ttu-id="1d859-247">После того как вы hello установлен на тестовом сервере последнюю версию агента, можно использовать следующие значения ProductId hello установлен tooget сценария hello.</span><span class="sxs-lookup"><span data-stu-id="1d859-247">After you have hello latest agent version installed on a test server, you can use hello following script tooget hello installed ProductId value.</span></span> <span data-ttu-id="1d859-248">Используя последнее значение ProductId hello, можно обновить значение hello hello MMAgent.ps1 сценария.</span><span class="sxs-lookup"><span data-stu-id="1d859-248">Using hello latest ProductId value, you can update hello value in hello MMAgent.ps1 script.</span></span>

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a><span data-ttu-id="1d859-249">Настройка агента вручную или добавление дополнительных рабочих областей</span><span class="sxs-lookup"><span data-stu-id="1d859-249">Configure an agent manually or add additional workspaces</span></span>
<span data-ttu-id="1d859-250">При установке агентов, но не настроены или если требуется, чтобы агент tooreport hello toomultiple-рабочие области, можно использовать следующие сведения tooenable агента hello или перенастроить его.</span><span class="sxs-lookup"><span data-stu-id="1d859-250">If you've installed agents but did not configure them or if you want hello agent tooreport toomultiple workspaces, you can use hello following information tooenable an agent or reconfigure it.</span></span> <span data-ttu-id="1d859-251">После настройки hello агент будет зарегистрирован со службой агента hello и получите необходимые сведения о конфигурации и пакеты управления, содержащие сведения о решении.</span><span class="sxs-lookup"><span data-stu-id="1d859-251">After you've configured hello agent, it will register with hello agent service and will get necessary configuration information and management packs that contain solution information.</span></span>

1. <span data-ttu-id="1d859-252">После установки Microsoft Monitoring Agent Привет открыть **панели управления**.</span><span class="sxs-lookup"><span data-stu-id="1d859-252">After you've installed hello Microsoft Monitoring Agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="1d859-253">Откройте **Microsoft Monitoring Agent** и нажмите кнопку hello **анализа журналов Azure (OMS)** вкладки.</span><span class="sxs-lookup"><span data-stu-id="1d859-253">Open **Microsoft Monitoring Agent** and then click hello **Azure Log Analytics (OMS)** tab.</span></span>   
3. <span data-ttu-id="1d859-254">Нажмите кнопку **добавить** tooopen hello **добавьте рабочей областью аналитики журналов** поле.</span><span class="sxs-lookup"><span data-stu-id="1d859-254">Click **Add** tooopen hello **Add a Log Analytics Workspace** box.</span></span>
4. <span data-ttu-id="1d859-255">Вставить hello **идентификатор рабочей области** и **ключ рабочей области (первичный ключ)** скопированные в Блокнот в предыдущей процедуры для hello рабочей tooadd и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="1d859-255">Paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for hello workspace that you want tooadd and then click **OK**.</span></span>  
    <span data-ttu-id="1d859-256">![Настройка Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="1d859-256">![configure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span></span>

<span data-ttu-id="1d859-257">После сбора данных с компьютеров, отслеживаемых агентом hello hello число компьютеров, которые отслеживает OMS будет отображаться на портале OMS hello hello **подключенные источники** вкладке **параметры** как  **Серверы подключены**.</span><span class="sxs-lookup"><span data-stu-id="1d859-257">After data is collected from computers monitored by hello agent, hello number of computers monitored by OMS will appear in hello OMS portal on hello **Connected Sources** tab in **Settings** as **Servers Connected**.</span></span>


## <a name="toodisable-an-agent"></a><span data-ttu-id="1d859-258">toodisable агента</span><span class="sxs-lookup"><span data-stu-id="1d859-258">toodisable an agent</span></span>
1. <span data-ttu-id="1d859-259">После установки агента hello откройте **панели управления**.</span><span class="sxs-lookup"><span data-stu-id="1d859-259">After installing hello agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="1d859-260">Откройте агент Microsoft Monitoring Agent, а затем нажмите кнопку hello **анализа журналов Azure (OMS)** вкладки.</span><span class="sxs-lookup"><span data-stu-id="1d859-260">Open Microsoft Monitoring Agent and then click hello **Azure Log Analytics (OMS)** tab.</span></span>
3. <span data-ttu-id="1d859-261">Выберите рабочую область и щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="1d859-261">Select a workspace and then click **Remove**.</span></span> <span data-ttu-id="1d859-262">Повторите этот шаг для всех рабочих областей.</span><span class="sxs-lookup"><span data-stu-id="1d859-262">Repeat this step for all other workspaces.</span></span>


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="1d859-263">При необходимости настройте группы управления Operations Manager tooan tooreport агентов</span><span class="sxs-lookup"><span data-stu-id="1d859-263">Optionally, configure agents tooreport tooan Operations Manager management group</span></span>

<span data-ttu-id="1d859-264">При использовании Operations Manager в ИТ-инфраструктуре hello MMA агента может использоваться как агент Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="1d859-264">If you use Operations Manager in your IT infrastructure, you can also use hello MMA agent as an Operations Manager agent.</span></span>

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="1d859-265">tooconfigure tooreport агенты MMA tooan группы управления Operations Manager</span><span class="sxs-lookup"><span data-stu-id="1d859-265">tooconfigure MMA agents tooreport tooan Operations Manager management group</span></span>
1.  <span data-ttu-id="1d859-266">Откройте на компьютере hello, где установлен агент hello **панели управления**.</span><span class="sxs-lookup"><span data-stu-id="1d859-266">On hello computer where hello agent is installed, open **Control Panel**.</span></span>  
2.  <span data-ttu-id="1d859-267">Откройте **Microsoft Monitoring Agent** и нажмите кнопку hello **Operations Manager** вкладки.</span><span class="sxs-lookup"><span data-stu-id="1d859-267">Open **Microsoft Monitoring Agent** and then click hello **Operations Manager** tab.</span></span>  
    <span data-ttu-id="1d859-268">![Вкладка "Operations Manager в Microsoft Monitoring Agent"](./media/log-analytics-windows-agents/om-mg01.png)</span><span class="sxs-lookup"><span data-stu-id="1d859-268">![Microsoft Monitoring Agent Operations Manager tab](./media/log-analytics-windows-agents/om-mg01.png)</span></span>
3.  <span data-ttu-id="1d859-269">Если серверы Operations Manager интегрированы с Active Directory, установите флажок **Автоматически обновлять назначения групп управления из AD DS**.</span><span class="sxs-lookup"><span data-stu-id="1d859-269">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
4.  <span data-ttu-id="1d859-270">Нажмите кнопку **добавить** tooopen hello **добавить группу управления** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="1d859-270">Click **Add** tooopen hello **Add a Management Group** dialog box.</span></span>  
    <span data-ttu-id="1d859-271">![Добавление группы управления в Microsoft Monitoring Agent](./media/log-analytics-windows-agents/oms-mma-om02.png)</span><span class="sxs-lookup"><span data-stu-id="1d859-271">![Microsoft Monitoring Agent Add a Management Group](./media/log-analytics-windows-agents/oms-mma-om02.png)</span></span>
5.  <span data-ttu-id="1d859-272">В **имя группы управления** введите hello имя группы управления.</span><span class="sxs-lookup"><span data-stu-id="1d859-272">In **Management group name** box, type hello name of your management group.</span></span>
6.  <span data-ttu-id="1d859-273">В hello **основного сервера управления** введите имя компьютера hello объекта hello основного сервера управления.</span><span class="sxs-lookup"><span data-stu-id="1d859-273">In hello **Primary management server** box, type hello computer name of hello primary management server.</span></span>
7.  <span data-ttu-id="1d859-274">В hello **порт сервера управления** поле номер TCP-порта типа hello.</span><span class="sxs-lookup"><span data-stu-id="1d859-274">In hello **Management server port** box, type hello TCP port number.</span></span>
8.  <span data-ttu-id="1d859-275">В разделе **учетная запись действия агента**, выберите hello локальной системной учетной записью или учетной записью локального домена.</span><span class="sxs-lookup"><span data-stu-id="1d859-275">Under **Agent Action Account**, choose either hello Local System account or a local domain account.</span></span>
9.  <span data-ttu-id="1d859-276">Нажмите кнопку **ОК** tooclose hello **добавить группу управления** диалоговое окно и нажмите кнопку **ОК** tooclose hello **свойства Microsoft Monitoring Agent**диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="1d859-276">Click **OK** tooclose hello **Add a Management Group** dialog box and then click **OK** tooclose hello **Microsoft Monitoring Agent Properties** dialog box.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1d859-277">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1d859-277">Next steps</span></span>

- <span data-ttu-id="1d859-278">[Добавление решений анализа журналов из коллекции решений hello](log-analytics-add-solutions.md) tooadd функциональные возможности и сбора данных.</span><span class="sxs-lookup"><span data-stu-id="1d859-278">[Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md) tooadd functionality and gather data.</span></span>
