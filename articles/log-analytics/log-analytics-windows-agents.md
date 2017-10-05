---
title: "Подключение компьютеров Windows к Azure Log Analytics | Документация Майкрософт"
description: "В этой статье приведена процедура подключения компьютеров Windows в локальной инфраструктуре к службе Log Analytics с помощью настраиваемой версии Microsoft Monitoring Agent (MMA)."
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
ms.openlocfilehash: 48a0eaeb10d406d551c9e5870edde06809bd7544
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="connect-windows-computers-to-the-log-analytics-service-in-azure"></a><span data-ttu-id="3f052-103">Подключение компьютеров Windows к службе Log Analytics в Azure</span><span class="sxs-lookup"><span data-stu-id="3f052-103">Connect Windows computers to the Log Analytics service in Azure</span></span>

<span data-ttu-id="3f052-104">В этой статье приведена процедура подключения компьютеров Windows в локальной инфраструктуре к рабочим областям OMS с помощью настраиваемой версии Microsoft Monitoring Agent (MMA).</span><span class="sxs-lookup"><span data-stu-id="3f052-104">This article shows the steps to connect Windows computers in your on-premises infrastructure to OMS workspaces by using a customized version of the Microsoft Monitoring Agent (MMA).</span></span> <span data-ttu-id="3f052-105">Необходимо установить и подключить агенты для всех компьютеров, которые должны быть присоединены, чтобы те могли отправлять данные в службу Log Analytics, просматривать эти данные и выполнять с ними операции.</span><span class="sxs-lookup"><span data-stu-id="3f052-105">You need to install and connect agents for all of the computers that you want to onboard in order for them to send data to the Log Analytics service and to view and act on that data.</span></span> <span data-ttu-id="3f052-106">Каждый агент может передавать данные в несколько рабочих областей.</span><span class="sxs-lookup"><span data-stu-id="3f052-106">Each agent can report to multiple workspaces.</span></span>

<span data-ttu-id="3f052-107">Установить агенты можно с помощью программы установки, командной строки или DSC (настройки требуемого состояния) в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="3f052-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span></span>  

>[!NOTE]
<span data-ttu-id="3f052-108">Для виртуальных машин, запущенных в Azure, установку можно упростить с помощью [расширения виртуальной машины](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="3f052-108">For virtual machines running in Azure, you can simplify installation by using the [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="3f052-109">На компьютерах, подключенных к Интернету, агент использует это подключение для отправки данных в OMS.</span><span class="sxs-lookup"><span data-stu-id="3f052-109">On computers with Internet connectivity, the agent uses the connection to the Internet to send data to OMS.</span></span> <span data-ttu-id="3f052-110">Для компьютеров, не подключенных к Интернету, можно использовать прокси-сервер или [шлюз OMS](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="3f052-110">For computers that do not have Internet connectivity, you can use a proxy or the [OMS Gateway](log-analytics-oms-gateway.md).</span></span>

<span data-ttu-id="3f052-111">Подключение компьютеров Windows к OMS выполняется в три простых этапа.</span><span class="sxs-lookup"><span data-stu-id="3f052-111">Connecting your Windows computers to OMS is straightforward using three simple steps:</span></span>

1. <span data-ttu-id="3f052-112">Скачайте файл установки агента на портале OMS.</span><span class="sxs-lookup"><span data-stu-id="3f052-112">Download the agent setup file from the OMS portal</span></span>
2. <span data-ttu-id="3f052-113">Установка агента выбранным способом</span><span class="sxs-lookup"><span data-stu-id="3f052-113">Install the agent using the method you choose</span></span>
3. <span data-ttu-id="3f052-114">Настройка агента или добавление дополнительных рабочих областей (при необходимости)</span><span class="sxs-lookup"><span data-stu-id="3f052-114">Configure the agent or add additional workspaces, if necessary</span></span>

<span data-ttu-id="3f052-115">На следующей схеме показана связь между компьютерами Windows и OMS после установки и настройки агентов.</span><span class="sxs-lookup"><span data-stu-id="3f052-115">The following diagram shows the relationship between your Windows computers and OMS after you’ve installed and configured agents.</span></span>

![oms-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

<span data-ttu-id="3f052-117">Если установленные политики безопасности ИТ не разрешают компьютерам в вашей сети подключаться к Интернету, можно настроить эти компьютеры для подключения к шлюзу OMS.</span><span class="sxs-lookup"><span data-stu-id="3f052-117">If your IT security policies do not allow computers on your network to connect to the Internet, you can configure your computers to connect to the OMS Gateway.</span></span> <span data-ttu-id="3f052-118">Дополнительные сведения и инструкции по настройке серверов для обмена данными со службой OMS через шлюз OMS см. в статье [Подключения компьютеров к OMS с помощью шлюза OMS без доступа к Интернету](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="3f052-118">For more information and steps on how to configure your servers to communicate through an OMS Gateway to the OMS service, see [Connect computers to OMS using the OMS Gateway](log-analytics-oms-gateway.md).</span></span>

## <a name="system-requirements-and-required-configuration"></a><span data-ttu-id="3f052-119">Системные требования и необходимая конфигурация</span><span class="sxs-lookup"><span data-stu-id="3f052-119">System requirements and required configuration</span></span>
<span data-ttu-id="3f052-120">Перед установкой или развертыванием агентов просмотрите следующие сведения и убедитесь в том, что требования выполнены.</span><span class="sxs-lookup"><span data-stu-id="3f052-120">Before you install or deploy agents, review the following details to ensure you meet the requirements.</span></span>

- <span data-ttu-id="3f052-121">MMA OMS можно устанавливать на компьютеры под управлением Windows Server 2008 SP 1 или более поздней версии либо Windows 7 SP1 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="3f052-121">You can only install the OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span></span>
- <span data-ttu-id="3f052-122">Вам понадобится подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="3f052-122">You need an Azure subscription.</span></span>  <span data-ttu-id="3f052-123">Дополнительные сведения см. в статье [Начало работы с Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3f052-123">For more information, see [Get started with Log Analytics](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="3f052-124">Каждый компьютер Windows должен иметь доступ к Интернету по протоколу HTTPS или к шлюзу OMS.</span><span class="sxs-lookup"><span data-stu-id="3f052-124">Each Windows computer must be able to connect to the Internet using HTTPS or to the OMS Gateway.</span></span> <span data-ttu-id="3f052-125">Подключение может быть установлено напрямую, через прокси-сервер или через шлюз OMS.</span><span class="sxs-lookup"><span data-stu-id="3f052-125">This connection can be direct, via a proxy, or through the OMS Gateway.</span></span>
- <span data-ttu-id="3f052-126">MMA OMS можно устанавливать на автономные компьютеры, серверы и виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="3f052-126">You can install the OMS MMA on stand-alone computers, servers, and virtual machines.</span></span> <span data-ttu-id="3f052-127">Если вы хотите подключить к OMS виртуальные машины, размещенные в Azure, см. статью [Подключение виртуальных машин Azure к службе Log Analytics](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="3f052-127">If you want to connect Azure-hosted virtual machines to OMS, see [Connect Azure virtual machines to Log Analytics](log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="3f052-128">Агенту необходимо использовать TCP-порт 443 для различных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3f052-128">The agent needs to use TCP port 443 for various resources.</span></span>

### <a name="network"></a><span data-ttu-id="3f052-129">Сеть</span><span class="sxs-lookup"><span data-stu-id="3f052-129">Network</span></span>

<span data-ttu-id="3f052-130">Чтобы агенты Windows могли подключиться к службе OMS и зарегистрироваться в ней, им нужен доступ к сетевым ресурсам, включая номера портов и URL-адреса доменов.</span><span class="sxs-lookup"><span data-stu-id="3f052-130">For Windows agents to connect to and register with the OMS service, they must have access to network resources, including the port numbers and domain URLs.</span></span>

- <span data-ttu-id="3f052-131">Для прокси-серверов необходимо убедиться, что в параметрах агента настроены соответствующие ресурсы прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="3f052-131">For proxy servers, you need to ensure that the appropriate proxy server resources are configured in agent settings.</span></span>
- <span data-ttu-id="3f052-132">Если используются брандмауэры, ограничивающие доступ к Интернету, вам или вашим сетевым инженерам следует настроить их таким образом, чтобы разрешить доступ к OMS.</span><span class="sxs-lookup"><span data-stu-id="3f052-132">For firewalls that restrict access to the Internet, you or your networking engineers need to configure your firewall to permit access to OMS.</span></span> <span data-ttu-id="3f052-133">Настройка параметров агента не требуется.</span><span class="sxs-lookup"><span data-stu-id="3f052-133">No action is needed in agent settings.</span></span>

<span data-ttu-id="3f052-134">В следующей таблице показаны ресурсы, необходимые для обмена данными.</span><span class="sxs-lookup"><span data-stu-id="3f052-134">The following table shows resources needed for communication.</span></span>

>[!NOTE]
><span data-ttu-id="3f052-135">В некоторых из ресурсов упоминается Operational Insights — предыдущее название Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3f052-135">Some of the following resources mention Operational Insights, which was a previous name for Log Analytics.</span></span>

| <span data-ttu-id="3f052-136">Ресурс агента</span><span class="sxs-lookup"><span data-stu-id="3f052-136">Agent Resource</span></span> | <span data-ttu-id="3f052-137">порты;</span><span class="sxs-lookup"><span data-stu-id="3f052-137">Ports</span></span> | <span data-ttu-id="3f052-138">Обход проверки HTTPS</span><span class="sxs-lookup"><span data-stu-id="3f052-138">Bypass HTTPS inspection</span></span> |
|---|---|---|
| <span data-ttu-id="3f052-139">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="3f052-139">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="3f052-140">443</span><span class="sxs-lookup"><span data-stu-id="3f052-140">443</span></span> | <span data-ttu-id="3f052-141">Да</span><span class="sxs-lookup"><span data-stu-id="3f052-141">Yes</span></span> |
| <span data-ttu-id="3f052-142">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="3f052-142">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="3f052-143">443</span><span class="sxs-lookup"><span data-stu-id="3f052-143">443</span></span> | <span data-ttu-id="3f052-144">Да</span><span class="sxs-lookup"><span data-stu-id="3f052-144">Yes</span></span> |
| <span data-ttu-id="3f052-145">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="3f052-145">*.blob.core.windows.net</span></span> | <span data-ttu-id="3f052-146">443</span><span class="sxs-lookup"><span data-stu-id="3f052-146">443</span></span> | <span data-ttu-id="3f052-147">Да</span><span class="sxs-lookup"><span data-stu-id="3f052-147">Yes</span></span> |
| <span data-ttu-id="3f052-148">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="3f052-148">*.azure-automation.net</span></span> | <span data-ttu-id="3f052-149">443</span><span class="sxs-lookup"><span data-stu-id="3f052-149">443</span></span> | <span data-ttu-id="3f052-150">Да</span><span class="sxs-lookup"><span data-stu-id="3f052-150">Yes</span></span> |



## <a name="download-the-agent-setup-file-from-oms"></a><span data-ttu-id="3f052-151">Загрузка файла установки агента из OMS</span><span class="sxs-lookup"><span data-stu-id="3f052-151">Download the agent setup file from OMS</span></span>
1. <span data-ttu-id="3f052-152">На портале OMS на странице **Обзор** щелкните плитку **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="3f052-152">In the OMS portal, on the **Overview** page, click the **Settings** tile.</span></span>  <span data-ttu-id="3f052-153">Откройте расположенную сверху вкладку **Подключенные источники**.</span><span class="sxs-lookup"><span data-stu-id="3f052-153">Click the **Connected Sources** tab at the top.</span></span>  
    <span data-ttu-id="3f052-154">![Вкладка "Подключенные источники"](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span><span class="sxs-lookup"><span data-stu-id="3f052-154">![Connected Sources tab](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span></span>
2. <span data-ttu-id="3f052-155">Чтобы скачать файл установки, щелкните **Серверы с Windows** и нажмите кнопку **Скачать агент для Windows**, соответствующую типу процессора на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="3f052-155">Click **Windows Servers** and then click **Download Windows Agent** applicable to your computer processor type to download the setup file.</span></span>
3. <span data-ttu-id="3f052-156">Справа от **идентификатора рабочей области**нажмите значок копирования и вставьте идентификатор в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="3f052-156">On the right of **Workspace ID**, click the copy icon and paste the ID into Notepad.</span></span>
4. <span data-ttu-id="3f052-157">Справа от **первичного ключа**нажмите значок копирования и вставьте ключ в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="3f052-157">On the right of **Primary Key**, click the copy icon and paste the key into Notepad.</span></span>     

## <a name="install-the-agent-using-setup"></a><span data-ttu-id="3f052-158">Установка агента с помощью программы установки</span><span class="sxs-lookup"><span data-stu-id="3f052-158">Install the agent using setup</span></span>
1. <span data-ttu-id="3f052-159">Запустите программу установки, чтобы установить агент на компьютер, которым требуется управлять.</span><span class="sxs-lookup"><span data-stu-id="3f052-159">Run Setup to install the agent on a computer that you want to manage.</span></span>
2. <span data-ttu-id="3f052-160">На странице приветствия нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3f052-160">On the Welcome page, click **Next**.</span></span>
3. <span data-ttu-id="3f052-161">На странице "Условия лицензии" прочтите лицензию и нажмите кнопку **Принимаю**.</span><span class="sxs-lookup"><span data-stu-id="3f052-161">On the License Terms page, read the license and then click **I Agree**.</span></span>
4. <span data-ttu-id="3f052-162">На странице "Папка назначения" измените или оставьте папку установки по умолчанию и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3f052-162">On the Destination Folder page, change or keep the default installation folder and then click **Next**.</span></span>
5. <span data-ttu-id="3f052-163">На странице "Параметры установки агента" можно подключить агент к Azure Log Analytics (OMS) или Operations Manager либо оставить поле пустым, чтобы настроить агент позднее.</span><span class="sxs-lookup"><span data-stu-id="3f052-163">On the Agent Setup Options page, you can choose to connect the agent to Azure Log Analytics (OMS), Operations Manager, or you can leave the choices blank if you want to configure the agent later.</span></span> <span data-ttu-id="3f052-164">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3f052-164">Click **Next**.</span></span>   
    - <span data-ttu-id="3f052-165">Если выбрано подключение к Azure Log Analytics (OMS), вставьте **идентификатор рабочей области** и **ключ рабочей области (первичный ключ)**, скопированные в Блокнот на предыдущих шагах, и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3f052-165">If you chose to connect to Azure Log Analytics (OMS), paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in the previous procedure and then click **Next**.</span></span>  
        <span data-ttu-id="3f052-166">![Вставка идентификатора рабочей области и первичного ключа](./media/log-analytics-windows-agents/connect-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="3f052-166">![paste Workspace ID and Primary Key](./media/log-analytics-windows-agents/connect-workspace.png)</span></span>
    - <span data-ttu-id="3f052-167">Если выбрано подключение к Operations Manager, введите **имя группы управления**, имя **сервера управления** и **порт сервера управления**, затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3f052-167">If you chose to connect to Operations Manager, type the **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span></span> <span data-ttu-id="3f052-168">На странице "Учетная запись действия агента" выберите учетную запись Local System или учетную запись локального домена и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3f052-168">On the Agent Action Account page, choose either the Local System account or a local domain account and then click **Next**.</span></span>  
        <span data-ttu-id="3f052-169">![конфигурация группы управления](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![учетная запись действия агента](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span><span class="sxs-lookup"><span data-stu-id="3f052-169">![management group configuration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span></span>

6. <span data-ttu-id="3f052-170">На странице "Готовность к установке" просмотрите выбранные параметры и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="3f052-170">On the Ready to Install page, review your choices and then click **Install**.</span></span>
7. <span data-ttu-id="3f052-171">На странице "Настройка успешно завершена" нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="3f052-171">On the Configuration completed successfully page, click **Finish**.</span></span>
8. <span data-ttu-id="3f052-172">После завершения установки на **панели управления** появится **Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="3f052-172">When complete, the **Microsoft Monitoring Agent** appears in **Control Panel**.</span></span> <span data-ttu-id="3f052-173">Здесь можно просмотреть конфигурацию и проверить, подключен ли агент к Operational Insights (OMS).</span><span class="sxs-lookup"><span data-stu-id="3f052-173">You can review your configuration there and verify that the agent is connected to Operational Insights (OMS).</span></span> <span data-ttu-id="3f052-174">При подключении к OMS агент выдает следующее сообщение: **Microsoft Monitoring Agent успешно подключен к службе Microsoft Operations Management Suite.**</span><span class="sxs-lookup"><span data-stu-id="3f052-174">When connected to OMS, the agent displays a message stating: **The Microsoft Monitoring Agent has successfully connected to the Microsoft Operations Management Suite service.**</span></span>

## <a name="configure-proxy-settings"></a><span data-ttu-id="3f052-175">Настройка параметров прокси</span><span class="sxs-lookup"><span data-stu-id="3f052-175">Configure proxy settings</span></span>

<span data-ttu-id="3f052-176">Далее описано, как настроить параметры прокси-сервера для Microsoft Monitoring Agent с помощью панели управления.</span><span class="sxs-lookup"><span data-stu-id="3f052-176">You can use the following procedure to configure proxy settings for the Microsoft Monitoring Agent using Control Panel.</span></span> <span data-ttu-id="3f052-177">Эту процедуру необходимо использовать для каждого сервера.</span><span class="sxs-lookup"><span data-stu-id="3f052-177">You need to use this procedure for each server.</span></span> <span data-ttu-id="3f052-178">Если вам нужно настроить несколько серверов, возможно, проще использовать скрипт для автоматизации этого процесса.</span><span class="sxs-lookup"><span data-stu-id="3f052-178">If you have many servers that you need to configure, you might find it easier to use a script to automate this process.</span></span> <span data-ttu-id="3f052-179">Далее описано, [как настроить параметры прокси-сервера для Microsoft Monitoring Agent с помощью скрипта](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span><span class="sxs-lookup"><span data-stu-id="3f052-179">If so, see the next procedure [To configure proxy settings for the Microsoft Monitoring Agent using a script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span></span>

### <a name="to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-control-panel"></a><span data-ttu-id="3f052-180">Настройка параметров прокси-сервера для Microsoft Monitoring Agent с помощью панели управления</span><span class="sxs-lookup"><span data-stu-id="3f052-180">To configure proxy settings for the Microsoft Monitoring Agent using Control Panel</span></span>
1. <span data-ttu-id="3f052-181">Откройте **Панель управления**.</span><span class="sxs-lookup"><span data-stu-id="3f052-181">Open **Control Panel**.</span></span>
2. <span data-ttu-id="3f052-182">Откройте **Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="3f052-182">Open **Microsoft Monitoring Agent**.</span></span>
3. <span data-ttu-id="3f052-183">Перейдите на вкладку **Параметры прокси-сервера**.</span><span class="sxs-lookup"><span data-stu-id="3f052-183">Click the **Proxy Settings** tab.</span></span>  
    <span data-ttu-id="3f052-184">![вкладка параметров прокси-сервера](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span><span class="sxs-lookup"><span data-stu-id="3f052-184">![proxy settings tab](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span></span>
4. <span data-ttu-id="3f052-185">Выберите **Использовать прокси-сервер** и введите URL-адрес и номер порта (если он нужен), как показано в примере.</span><span class="sxs-lookup"><span data-stu-id="3f052-185">Select **Use a proxy server** and type the URL and port number, if one is needed, similar to the example shown.</span></span> <span data-ttu-id="3f052-186">Если для доступа к прокси-серверу требуется проверка подлинности, введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="3f052-186">If your proxy server requires authentication, type the username and password to access the proxy server.</span></span>


### <a name="verify-agent-connectivity-to-oms"></a><span data-ttu-id="3f052-187">Проверка подключения к агенту OMS</span><span class="sxs-lookup"><span data-stu-id="3f052-187">Verify agent connectivity to OMS</span></span>

<span data-ttu-id="3f052-188">Можно легко проверить, могут ли агенты обмениваться данными с OMS, воспользовавшись следующей процедурой.</span><span class="sxs-lookup"><span data-stu-id="3f052-188">You can easily verify whether your agents are communicating with OMS using the following procedure:</span></span>

1.  <span data-ttu-id="3f052-189">На компьютере, на котором установлен агент Windows, откройте панель управления.</span><span class="sxs-lookup"><span data-stu-id="3f052-189">On the computer with the Windows agent, open Control Panel.</span></span>
2.  <span data-ttu-id="3f052-190">Откройте "Microsoft Monitoring Agent".</span><span class="sxs-lookup"><span data-stu-id="3f052-190">Open Microsoft Monitoring Agent.</span></span>
3.  <span data-ttu-id="3f052-191">Перейдите на вкладку "Azure Log Analytics (OMS)".</span><span class="sxs-lookup"><span data-stu-id="3f052-191">Click the Azure Log Analytics (OMS) tab.</span></span>
4.  <span data-ttu-id="3f052-192">В столбце "Состояние" вы увидите, что агент успешно подключен к службе Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="3f052-192">In the Status column, you should see that the agent connected successfully to the Operations Management Suite service.</span></span>

![Агент подключен](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script"></a><span data-ttu-id="3f052-194">как настроить параметры прокси-сервера для Microsoft Monitoring Agent с помощью скрипта</span><span class="sxs-lookup"><span data-stu-id="3f052-194">To configure proxy settings for the Microsoft Monitoring Agent using a script</span></span>
<span data-ttu-id="3f052-195">Скопируйте следующий пример, измените его, указав данные своей среды, сохраните его в файл с расширением PS1, затем выполните сценарий на каждом компьютере, который подключается непосредственно к службе OMS.</span><span class="sxs-lookup"><span data-stu-id="3f052-195">Copy the following sample, update it with information specific to your environment, save it with a PS1 file name extension, and then run the script on each computer that connects directly to the OMS service.</span></span>

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get the Health Service configuration object.  We need to determine if we
    #have the right update rollup with the API we need.  If not, no need to run the rest of the script.
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

    Write-Output "Setting proxy to $ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-the-agent-using-the-command-line"></a><span data-ttu-id="3f052-196">Установка агента с помощью командной строки</span><span class="sxs-lookup"><span data-stu-id="3f052-196">Install the agent using the command line</span></span>
- <span data-ttu-id="3f052-197">Измените, а затем используйте следующий пример для установки агента с помощью командной строки.</span><span class="sxs-lookup"><span data-stu-id="3f052-197">Modify and then use the following example to install the agent using the command line.</span></span> <span data-ttu-id="3f052-198">В примере выполняется полностью автоматическая установка.</span><span class="sxs-lookup"><span data-stu-id="3f052-198">The example performs a fully silent installation.</span></span>

    >[!NOTE]
    <span data-ttu-id="3f052-199">Для обновления агента необходимо использовать API сценариев службы Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3f052-199">If you want to upgrade an agent, you need to use the Log Analytics scripting API.</span></span> <span data-ttu-id="3f052-200">Сведения об обновлении агента см. в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="3f052-200">See the next section to upgrade an agent.</span></span>

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

<span data-ttu-id="3f052-201">Агент использует IExpress в качестве самоизвлечения с помощью команды `/c`.</span><span class="sxs-lookup"><span data-stu-id="3f052-201">The agent uses IExpress as its self-extractor using the `/c` command.</span></span> <span data-ttu-id="3f052-202">Воспользуйтесь параметрами командной строки в разделе [Параметры командной строки для IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) и затем измените пример в соответствии со своими потребностями.</span><span class="sxs-lookup"><span data-stu-id="3f052-202">You can see the command-line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update the example to suit your needs.</span></span>

|<span data-ttu-id="3f052-203">Параметры MMA</span><span class="sxs-lookup"><span data-stu-id="3f052-203">MMA-specific options</span></span>                   |<span data-ttu-id="3f052-204">Примечания</span><span class="sxs-lookup"><span data-stu-id="3f052-204">Notes</span></span>         |
|---------------------------------------|--------------|
|<span data-ttu-id="3f052-205">ADD_OPINSIGHTS_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="3f052-205">ADD_OPINSIGHTS_WORKSPACE</span></span>               | <span data-ttu-id="3f052-206">1 — настройка агента для передачи отчетов в рабочую область.</span><span class="sxs-lookup"><span data-stu-id="3f052-206">1 = Configure the agent to report to a workspace</span></span>                |
|<span data-ttu-id="3f052-207">OPINSIGHTS_WORKSPACE_ID</span><span class="sxs-lookup"><span data-stu-id="3f052-207">OPINSIGHTS_WORKSPACE_ID</span></span>                | <span data-ttu-id="3f052-208">Идентификатор добавляемой рабочей области (GUID).</span><span class="sxs-lookup"><span data-stu-id="3f052-208">Workspace Id (guid) for the workspace to add</span></span>                    |
|<span data-ttu-id="3f052-209">OPINSIGHTS_WORKSPACE_KEY</span><span class="sxs-lookup"><span data-stu-id="3f052-209">OPINSIGHTS_WORKSPACE_KEY</span></span>               | <span data-ttu-id="3f052-210">Ключ рабочей области, используемый для первоначальной аутентификации в рабочей области.</span><span class="sxs-lookup"><span data-stu-id="3f052-210">Workspace key used to initially authenticate with the workspace</span></span> |
|<span data-ttu-id="3f052-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span><span class="sxs-lookup"><span data-stu-id="3f052-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span></span>  | <span data-ttu-id="3f052-212">Укажите облачную среду, в которой находится рабочая область.</span><span class="sxs-lookup"><span data-stu-id="3f052-212">Specify the cloud environment where the workspace is located</span></span> <br> <span data-ttu-id="3f052-213">0 — коммерческое облако Azure (по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="3f052-213">0 = Azure commercial cloud (default)</span></span> <br> <span data-ttu-id="3f052-214">1 — Azure для государственных организаций.</span><span class="sxs-lookup"><span data-stu-id="3f052-214">1 = Azure Government</span></span> |
|<span data-ttu-id="3f052-215">OPINSIGHTS_PROXY_URL</span><span class="sxs-lookup"><span data-stu-id="3f052-215">OPINSIGHTS_PROXY_URL</span></span>               | <span data-ttu-id="3f052-216">Универсальный код ресурса (URI) для прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="3f052-216">URI for the proxy to use</span></span> |
|<span data-ttu-id="3f052-217">OPINSIGHTS_PROXY_USERNAME</span><span class="sxs-lookup"><span data-stu-id="3f052-217">OPINSIGHTS_PROXY_USERNAME</span></span>               | <span data-ttu-id="3f052-218">Имя пользователя для доступа к прокси-серверу после аутентификации.</span><span class="sxs-lookup"><span data-stu-id="3f052-218">Username to access an authenticated proxy</span></span> |
|<span data-ttu-id="3f052-219">OPINSIGHTS_PROXY_PASSWORD</span><span class="sxs-lookup"><span data-stu-id="3f052-219">OPINSIGHTS_PROXY_PASSWORD</span></span>               | <span data-ttu-id="3f052-220">Пароль для доступа к прокси-серверу после аутентификации.</span><span class="sxs-lookup"><span data-stu-id="3f052-220">Password to access an authenticated proxy</span></span> |

>[!NOTE]
<span data-ttu-id="3f052-221">Чтобы избежать достижения ограничения длины командной строки IExpress, установите агента, не настраивая рабочую область, и затем с помощью сценария настройте конфигурацию рабочей области.</span><span class="sxs-lookup"><span data-stu-id="3f052-221">To avoid hitting the command-line length limit of IExpress, install the agent with no workspace configured and then use a script to set configuration for the workspace.</span></span>

>[!NOTE]
<span data-ttu-id="3f052-222">Если при использовании параметра `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` появляется сообщение `Command line option syntax error.`, можно выполнить приведенный ниже способ обхода.</span><span class="sxs-lookup"><span data-stu-id="3f052-222">If you get a `Command line option syntax error.` when using the `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, you can use the following workaround:</span></span>
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a><span data-ttu-id="3f052-223">Добавление рабочей области с помощью сценария</span><span class="sxs-lookup"><span data-stu-id="3f052-223">Add a workspace using a script</span></span>
<span data-ttu-id="3f052-224">Добавьте рабочую область с помощью API сценариев службы Log Analytics, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="3f052-224">Add a workspace using the Log Analytics agent scripting API with the following example:</span></span>

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

<span data-ttu-id="3f052-225">Чтобы добавить рабочую область в Azure для государственных организаций США, используйте следующий сценарий.</span><span class="sxs-lookup"><span data-stu-id="3f052-225">To add a workspace in Azure for US Government, use the following script sample:</span></span>
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
<span data-ttu-id="3f052-226">Если ранее вы использовали командную строку или сценарий для установки или настройки агента, теперь вместо `EnableAzureOperationalInsights` используется `AddCloudWorkspace`.</span><span class="sxs-lookup"><span data-stu-id="3f052-226">If you've used the command line or script previously to install or configure the agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span></span>

## <a name="install-the-agent-using-dsc-in-azure-automation"></a><span data-ttu-id="3f052-227">Установка агента с помощью DSC в службе автоматизации Azure</span><span class="sxs-lookup"><span data-stu-id="3f052-227">Install the agent using DSC in Azure Automation</span></span>

<span data-ttu-id="3f052-228">Вы можете использовать следующий пример сценария для установки агента с помощью DSC в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="3f052-228">You can use the following script example to install the agent using DSC in Azure Automation.</span></span> <span data-ttu-id="3f052-229">В примере выполняется установка 64-разрядного агента, идентифицируемого значением `URI`.</span><span class="sxs-lookup"><span data-stu-id="3f052-229">The example installs the 64-bit agent, identified by the `URI` value.</span></span> <span data-ttu-id="3f052-230">Вы также можете использовать 32-разрядную версию, заменив значение универсального кода ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="3f052-230">You can also use the 32-bit version by replacing the URI value.</span></span> <span data-ttu-id="3f052-231">URI для обеих версий:</span><span class="sxs-lookup"><span data-stu-id="3f052-231">The URIs for both versions are:</span></span>

- <span data-ttu-id="3f052-232">64-разрядный агент Windows: https://go.microsoft.com/fwlink/?LinkId=828603</span><span class="sxs-lookup"><span data-stu-id="3f052-232">Windows 64-bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span></span>
- <span data-ttu-id="3f052-233">32-разрядный агент Windows: https://go.microsoft.com/fwlink/?LinkId=828604</span><span class="sxs-lookup"><span data-stu-id="3f052-233">Windows 32-bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span></span>


>[!NOTE]
<span data-ttu-id="3f052-234">В этом примере процедура и сценарий не выполняют обновление существующего агента.</span><span class="sxs-lookup"><span data-stu-id="3f052-234">This procedure and script example will not upgrade an existing agent.</span></span>

1. <span data-ttu-id="3f052-235">Импортируйте модуль DSC xPSDesiredStateConfiguration со страницы [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) в службу автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="3f052-235">Import the xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span></span>  
2.  <span data-ttu-id="3f052-236">Создайте в службе автоматизации Azure ресурсы-контейнеры для переменных *OPSINSIGHTS_WS_ID* и *OPSINSIGHTS_WS_KEY*.</span><span class="sxs-lookup"><span data-stu-id="3f052-236">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span></span> <span data-ttu-id="3f052-237">В качестве значения параметра *OPSINSIGHTS_WS_ID* укажите идентификатор рабочей области Log Analytics в OMS, а для параметра *OPSINSIGHTS_WS_KEY* — первичный ключ рабочей области.</span><span class="sxs-lookup"><span data-stu-id="3f052-237">Set *OPSINSIGHTS_WS_ID* to your OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* to the primary key of your workspace.</span></span>
3.  <span data-ttu-id="3f052-238">Скопируйте приведенный ниже сценарий и сохраните его как файл MMAgent.ps1.</span><span class="sxs-lookup"><span data-stu-id="3f052-238">Use the following script and save it as MMAgent.ps1</span></span>
4.  <span data-ttu-id="3f052-239">Измените, а затем используйте следующий пример для установки агента с помощью DSC в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="3f052-239">Modify and then use the following example to install the agent using DSC in Azure Automation.</span></span> <span data-ttu-id="3f052-240">Импортируйте MMAgent.ps1 в службу автоматизации Azure с помощью интерфейса службы или командлета.</span><span class="sxs-lookup"><span data-stu-id="3f052-240">Import MMAgent.ps1 into Azure Automation by using the Azure Automation interface or cmdlet.</span></span>
5.  <span data-ttu-id="3f052-241">Назначьте узел конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3f052-241">Assign a node to the configuration.</span></span> <span data-ttu-id="3f052-242">В течение 15 минут узел проверит свою конфигурацию, а MMA будет помещен в узел.</span><span class="sxs-lookup"><span data-stu-id="3f052-242">Within 15 minutes, the node checks its configuration and the MMA is pushed to the node.</span></span>

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

### <a name="get-the-latest-productid-value"></a><span data-ttu-id="3f052-243">Получение последнего значения ProductId</span><span class="sxs-lookup"><span data-stu-id="3f052-243">Get the latest ProductId value</span></span>

<span data-ttu-id="3f052-244">`ProductId value` в сценарии MMAgent.ps1 уникален для каждой версии агента.</span><span class="sxs-lookup"><span data-stu-id="3f052-244">The `ProductId value` in the MMAgent.ps1 script is unique to each agent version.</span></span> <span data-ttu-id="3f052-245">При публикации обновленной версии каждого агента значение ProductId изменяется.</span><span class="sxs-lookup"><span data-stu-id="3f052-245">When an updated version of each agent is published, the ProductId value changes.</span></span> <span data-ttu-id="3f052-246">Таким образом, когда ProductId изменится в будущем, версию агента можно найти с помощью простого сценария.</span><span class="sxs-lookup"><span data-stu-id="3f052-246">So, when the ProductId changes in the future, you can find the agent version using a simple script.</span></span> <span data-ttu-id="3f052-247">Установив последнюю версию агента на тестовом сервере, получите установленное значение ProductId, выполнив следующий сценарий.</span><span class="sxs-lookup"><span data-stu-id="3f052-247">After you have the latest agent version installed on a test server, you can use the following script to get the installed ProductId value.</span></span> <span data-ttu-id="3f052-248">Используя последнее значение ProductId, можно обновить значение в сценарии MMAgent.ps1.</span><span class="sxs-lookup"><span data-stu-id="3f052-248">Using the latest ProductId value, you can update the value in the MMAgent.ps1 script.</span></span>

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

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a><span data-ttu-id="3f052-249">Настройка агента вручную или добавление дополнительных рабочих областей</span><span class="sxs-lookup"><span data-stu-id="3f052-249">Configure an agent manually or add additional workspaces</span></span>
<span data-ttu-id="3f052-250">Если вы установили, но не настроили агенты, или хотите, чтобы агенты передавали данные в несколько рабочих областей, вы можете использовать указанные ниже сведения для включения или перенастройки агентов.</span><span class="sxs-lookup"><span data-stu-id="3f052-250">If you've installed agents but did not configure them or if you want the agent to report to multiple workspaces, you can use the following information to enable an agent or reconfigure it.</span></span> <span data-ttu-id="3f052-251">После настройки агент будет зарегистрирован в службе агента и получит необходимые данные конфигурации и пакеты управления, содержащие сведения о решении.</span><span class="sxs-lookup"><span data-stu-id="3f052-251">After you've configured the agent, it will register with the agent service and will get necessary configuration information and management packs that contain solution information.</span></span>

1. <span data-ttu-id="3f052-252">После установки Microsoft Monitoring Agent откройте **панель управления**.</span><span class="sxs-lookup"><span data-stu-id="3f052-252">After you've installed the Microsoft Monitoring Agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="3f052-253">Откройте агент **Microsoft Monitoring Agent** и перейдите на вкладку **Azure Log Analytics (OMS)**.</span><span class="sxs-lookup"><span data-stu-id="3f052-253">Open **Microsoft Monitoring Agent** and then click the **Azure Log Analytics (OMS)** tab.</span></span>   
3. <span data-ttu-id="3f052-254">Щелкните **Добавить**, чтобы открыть диалоговое окно **Добавление рабочей области Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="3f052-254">Click **Add** to open the **Add a Log Analytics Workspace** box.</span></span>
4. <span data-ttu-id="3f052-255">Вставьте **идентификатор рабочей области** и **ключ рабочей области (первичный ключ)** для добавляемой рабочей области, скопированные в Блокнот в предыдущей процедуре, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3f052-255">Paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for the workspace that you want to add and then click **OK**.</span></span>  
    <span data-ttu-id="3f052-256">![Настройка Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="3f052-256">![configure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span></span>

<span data-ttu-id="3f052-257">После сбора данных с компьютеров, отслеживаемых агентом, количество компьютеров, отслеживаемых OMS, отобразится на портале OMS на вкладке **Подключенные источники** в разделе **Параметры** как **Подключенные серверы**.</span><span class="sxs-lookup"><span data-stu-id="3f052-257">After data is collected from computers monitored by the agent, the number of computers monitored by OMS will appear in the OMS portal on the **Connected Sources** tab in **Settings** as **Servers Connected**.</span></span>


## <a name="to-disable-an-agent"></a><span data-ttu-id="3f052-258">Отключение агента</span><span class="sxs-lookup"><span data-stu-id="3f052-258">To disable an agent</span></span>
1. <span data-ttu-id="3f052-259">После установки агента откройте **панель управления**.</span><span class="sxs-lookup"><span data-stu-id="3f052-259">After installing the agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="3f052-260">Откройте агент Microsoft Monitoring Agent и перейдите на вкладку **Azure Log Analytics (OMS)** .</span><span class="sxs-lookup"><span data-stu-id="3f052-260">Open Microsoft Monitoring Agent and then click the **Azure Log Analytics (OMS)** tab.</span></span>
3. <span data-ttu-id="3f052-261">Выберите рабочую область и щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="3f052-261">Select a workspace and then click **Remove**.</span></span> <span data-ttu-id="3f052-262">Повторите этот шаг для всех рабочих областей.</span><span class="sxs-lookup"><span data-stu-id="3f052-262">Repeat this step for all other workspaces.</span></span>


## <a name="optionally-configure-agents-to-report-to-an-operations-manager-management-group"></a><span data-ttu-id="3f052-263">Также можно настроить агенты таким образом, чтобы они отчитывались перед группой управления Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="3f052-263">Optionally, configure agents to report to an Operations Manager management group</span></span>

<span data-ttu-id="3f052-264">Если в ИТ-инфраструктуре используется Operations Manager, в качестве агента Operations Manager можно также использовать агент MMA.</span><span class="sxs-lookup"><span data-stu-id="3f052-264">If you use Operations Manager in your IT infrastructure, you can also use the MMA agent as an Operations Manager agent.</span></span>

### <a name="to-configure-mma-agents-to-report-to-an-operations-manager-management-group"></a><span data-ttu-id="3f052-265">Настройка агентов MMA для отчетности перед группой управления Operations Manager</span><span class="sxs-lookup"><span data-stu-id="3f052-265">To configure MMA agents to report to an Operations Manager management group</span></span>
1.  <span data-ttu-id="3f052-266">На компьютере, где установлен агент, откройте **панель управления**.</span><span class="sxs-lookup"><span data-stu-id="3f052-266">On the computer where the agent is installed, open **Control Panel**.</span></span>  
2.  <span data-ttu-id="3f052-267">Откройте **Microsoft Monitoring Agent** и перейдите на вкладку **Operations Manager**.</span><span class="sxs-lookup"><span data-stu-id="3f052-267">Open **Microsoft Monitoring Agent** and then click the **Operations Manager** tab.</span></span>  
    <span data-ttu-id="3f052-268">![Вкладка "Operations Manager в Microsoft Monitoring Agent"](./media/log-analytics-windows-agents/om-mg01.png)</span><span class="sxs-lookup"><span data-stu-id="3f052-268">![Microsoft Monitoring Agent Operations Manager tab](./media/log-analytics-windows-agents/om-mg01.png)</span></span>
3.  <span data-ttu-id="3f052-269">Если серверы Operations Manager интегрированы с Active Directory, установите флажок **Автоматически обновлять назначения групп управления из AD DS**.</span><span class="sxs-lookup"><span data-stu-id="3f052-269">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
4.  <span data-ttu-id="3f052-270">Нажмите кнопку **Добавить**, чтобы открыть диалоговое окно **Добавление группы управления**.</span><span class="sxs-lookup"><span data-stu-id="3f052-270">Click **Add** to open the **Add a Management Group** dialog box.</span></span>  
    <span data-ttu-id="3f052-271">![Добавление группы управления в Microsoft Monitoring Agent](./media/log-analytics-windows-agents/oms-mma-om02.png)</span><span class="sxs-lookup"><span data-stu-id="3f052-271">![Microsoft Monitoring Agent Add a Management Group](./media/log-analytics-windows-agents/oms-mma-om02.png)</span></span>
5.  <span data-ttu-id="3f052-272">В поле **Имя группы управления** введите имя группы управления.</span><span class="sxs-lookup"><span data-stu-id="3f052-272">In **Management group name** box, type the name of your management group.</span></span>
6.  <span data-ttu-id="3f052-273">В поле **Основной сервер управления** введите имя компьютера основного сервера управления.</span><span class="sxs-lookup"><span data-stu-id="3f052-273">In the **Primary management server** box, type the computer name of the primary management server.</span></span>
7.  <span data-ttu-id="3f052-274">В поле **Порт сервера управления** введите номер порта TCP.</span><span class="sxs-lookup"><span data-stu-id="3f052-274">In the **Management server port** box, type the TCP port number.</span></span>
8.  <span data-ttu-id="3f052-275">На странице **Учетная запись действия агента**выберите учетную запись Local System или учетную запись локального домена.</span><span class="sxs-lookup"><span data-stu-id="3f052-275">Under **Agent Action Account**, choose either the Local System account or a local domain account.</span></span>
9.  <span data-ttu-id="3f052-276">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Добавление группы управления**, и еще раз нажмите **ОК**, чтобы закрыть диалоговое окно **Свойства Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="3f052-276">Click **OK** to close the **Add a Management Group** dialog box and then click **OK** to close the **Microsoft Monitoring Agent Properties** dialog box.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3f052-277">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3f052-277">Next steps</span></span>

- <span data-ttu-id="3f052-278">[добавьте решения Log Analytics из коллекции решений](log-analytics-add-solutions.md) .</span><span class="sxs-lookup"><span data-stu-id="3f052-278">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span></span>
