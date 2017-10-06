---
title: "aaaTroubleshoot защиты от сбоев VMware или физическими tooAzure | Документы Microsoft"
description: "В этой статье описываются распространенные ошибки при репликации VMware машины hello и как tootroubleshoot их"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/26/2017
ms.author: asgang
ms.openlocfilehash: b821e9aa2610482ba1900645fb75e75744dc442f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a><span data-ttu-id="737e1-103">Устранение неполадок репликации виртуальной машины VMware или физического сервера в локальной среде</span><span class="sxs-lookup"><span data-stu-id="737e1-103">Troubleshoot on-premises VMware/Physical server replication issues</span></span>
<span data-ttu-id="737e1-104">Вы можете получить определенные сообщения об ошибках при защите виртуальных машин VMware или физических серверов с помощью Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="737e1-104">You may receive a specific error message when protecting your VMware virtual machines or physical servers using Azure Site Recovery.</span></span> <span data-ttu-id="737e1-105">Этой статьи описаны некоторые из наиболее распространенных сообщений об ошибках, обнаружения, а также устранение неполадок tooresolve действия Здравствуйте, их.</span><span class="sxs-lookup"><span data-stu-id="737e1-105">This article details some of hello more common error messages encountered, along with troubleshooting steps tooresolve them.</span></span>


## <a name="initial-replication-is-stuck-at-0"></a><span data-ttu-id="737e1-106">Начальная репликация зависла на 0 %</span><span class="sxs-lookup"><span data-stu-id="737e1-106">Initial replication is stuck at 0%</span></span>
<span data-ttu-id="737e1-107">Большинство сбоев hello начальной репликации, которые мы сталкиваемся с поддержкой, из-за проблем с tooconnectivity между исходного сервера к процессу сервера или сервера процесса-Azure.</span><span class="sxs-lookup"><span data-stu-id="737e1-107">Most of hello initial replication failures that we encounter at support are due tooconnectivity issues between source server-to-process server or process server-to-Azure.</span></span>
<span data-ttu-id="737e1-108">В большинстве случаев вы можете самостоятельно устранять эти проблемы, выполните указанные ниже действия hello.</span><span class="sxs-lookup"><span data-stu-id="737e1-108">For most cases, you can self troubleshoot these issues by following hello steps listed below.</span></span>

###<a name="check-hello-following-on-source-machine"></a><span data-ttu-id="737e1-109">Установите флажок, hello на ИСХОДНОМ КОМПЬЮТЕРЕ</span><span class="sxs-lookup"><span data-stu-id="737e1-109">Check hello following on SOURCE MACHINE</span></span>
* <span data-ttu-id="737e1-110">Из командной строки для компьютера исходного сервера используйте Telnet tooping hello сервера обработки с https-порт (по умолчанию 9443), как показано ниже toosee, если существуют проблемы с сетевым подключением или порт брандмауэра, критические препятствия.</span><span class="sxs-lookup"><span data-stu-id="737e1-110">From Source Server machine command line, use Telnet tooping hello Process Server with https port (default 9443) as shown below toosee if there are any network connectivity issues or firewall port blocking issues.</span></span>
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > <span data-ttu-id="737e1-111">Использовать Telnet, не использует подключение tootest PING.</span><span class="sxs-lookup"><span data-stu-id="737e1-111">Use Telnet, don’t use PING tootest connectivity.</span></span>  <span data-ttu-id="737e1-112">Если Telnet не установлена, выполните список шагов hello [здесь](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="737e1-112">If Telnet is not installed, follow hello steps list [here](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span></span>

<span data-ttu-id="737e1-113">Если не удается tooconnect Разрешить входящий порт 9443 на приветствия сервера обработки и установите флажок, если hello проблема по-прежнему завершает работу.</span><span class="sxs-lookup"><span data-stu-id="737e1-113">If unable tooconnect, allow inbound port 9443 on hello Process Server and check if hello problem still exits.</span></span> <span data-ttu-id="737e1-114">В некоторых случаях, когда сервер обработки находился за промежуточной подсетью, именно это вызывало такую проблему.</span><span class="sxs-lookup"><span data-stu-id="737e1-114">There has been some cases where process server was behind DMZ, which was causing this problem.</span></span>

* <span data-ttu-id="737e1-115">Проверьте состояние службы hello `InMage Scout VX Agent – Sentinel/OutpostStart` если он не выполняется» и «проверка hello проблема все еще существует.</span><span class="sxs-lookup"><span data-stu-id="737e1-115">Check hello status of service `InMage Scout VX Agent – Sentinel/OutpostStart` if it is not running and check if hello problem still exists.</span></span>   
 
###<a name="check-hello-following-on-process-server"></a><span data-ttu-id="737e1-116">Установите флажок, hello на сервер ОБРАБОТКИ</span><span class="sxs-lookup"><span data-stu-id="737e1-116">Check hello following on PROCESS SERVER</span></span>

* <span data-ttu-id="737e1-117">**Проверьте, если сервер обработки активно внедряет tooAzure данных**</span><span class="sxs-lookup"><span data-stu-id="737e1-117">**Check if process server is actively pushing data tooAzure**</span></span> 

<span data-ttu-id="737e1-118">С сервера обработки машины откройте диспетчер задач (нажмите сочетание клавиш Ctrl-Shift-Esc) hello.</span><span class="sxs-lookup"><span data-stu-id="737e1-118">From Process Server machine, open hello Task Manager (press Ctrl-Shift-Esc ).</span></span> <span data-ttu-id="737e1-119">Перейдите на вкладку "Быстродействие" toohello и щелкните ссылку «Открыть монитор ресурсов».</span><span class="sxs-lookup"><span data-stu-id="737e1-119">Go toohello Performance tab and click ‘Open Resource Monitor’ link.</span></span> <span data-ttu-id="737e1-120">Из диспетчера ресурсов перейдите tooNetwork вкладки. Проверьте, отправляет ли файл cbengine.exe на вкладке "Процессы с сетевой активностью" большие объемы данных (в МБ).</span><span class="sxs-lookup"><span data-stu-id="737e1-120">From Resource Manager, go tooNetwork tab. Check if cbengine.exe in ‘Processes with Network Activity’ is actively sending large volume (in Mbs) of data.</span></span>

![Включение репликации](./media/site-recovery-protection-common-errors/cbengine.png)

<span data-ttu-id="737e1-122">Если нет, выполните указанные ниже действия hello.</span><span class="sxs-lookup"><span data-stu-id="737e1-122">If not follow hello steps listed below:</span></span>

* <span data-ttu-id="737e1-123">**Проверьте, является ли процесс сервера может tooconnect больших двоичных объектов Azure**: выберите и установите hello «TCP-подключений» cbengine.exe tooview toosee, если отсутствует связь с URL-адреса процесса сервера tooAzure хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="737e1-123">**Check if Process server is able tooconnect Azure Blob**: Select and check cbengine.exe tooview hello ‘TCP Connections’ toosee if there is connectivity from Process server tooAzure Storage blob URL.</span></span>

![Включение репликации](./media/site-recovery-protection-common-errors/rmonitor.png)

<span data-ttu-id="737e1-125">Если нет, перейдите на панель tooControl > Проверьте службы, если hello следующие службы запущены и работают:</span><span class="sxs-lookup"><span data-stu-id="737e1-125">If not then go tooControl Panel > Services, check if hello following services are up and running:</span></span>

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
<span data-ttu-id="737e1-126">(Re) Запустите любой службе, не выполняется и проверьте, существует ли проблема hello.</span><span class="sxs-lookup"><span data-stu-id="737e1-126">(Re)Start any service which is not running and check if hello problem still exists.</span></span>

* <span data-ttu-id="737e1-127">**Проверьте, является ли процесс сервера может tooconnect tooAzure общедоступный IP-адрес через порт 443**</span><span class="sxs-lookup"><span data-stu-id="737e1-127">**Check if Process server is able tooconnect tooAzure Public IP address using port 443**</span></span>

<span data-ttu-id="737e1-128">Откройте hello последнюю CBEngineCurr.errlog из `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` и выполните поиск: 443 и подключения не удалась.</span><span class="sxs-lookup"><span data-stu-id="737e1-128">Open hello latest CBEngineCurr.errlog from `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` and search for :443  and connection attempt failed.</span></span>

![Включение репликации](./media/site-recovery-protection-common-errors/logdetails1.png)

<span data-ttu-id="737e1-130">Если возникли проблемы, с сервера обработки командной строки, используйте telnet tooping к Azure общедоступный IP-адрес (маскироваться в над изображением) в hello CBEngineCurr.currLog через порт 443.</span><span class="sxs-lookup"><span data-stu-id="737e1-130">If there are issues, then from Process Server command line, use telnet tooping your Azure Public IP address (masked in above image) found in hello CBEngineCurr.currLog using port 443.</span></span>

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
<span data-ttu-id="737e1-131">Если не удается tooconnect, проверьте проблемы доступа hello в случае из-за toofirewall или прокси-сервера, как описано в следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="737e1-131">If you are unable tooconnect, then check if hello access issue is due toofirewall or Proxy as described in next step.</span></span>


* <span data-ttu-id="737e1-132">**Проверьте, если IP-адресом брандмауэр на сервер обработки не блокируют доступ**: при использовании правила IP-адресом брандмауэра на сервере hello Загрузите полный список hello Microsoft Azure Datacenter диапазоны IP-адресов из [здесь ](https://www.microsoft.com/download/details.aspx?id=41653) и добавить их конфигурации tooensure tooyour брандмауэр, делают возможным обмен данными tooAzure (и hello порта HTTPS (443)).</span><span class="sxs-lookup"><span data-stu-id="737e1-132">**Check if IP address-based firewall on Process server are not blocking access**: If you are using an IP address-based firewall rules on hello server, then download hello complete list of Microsoft Azure Datacenter IP Ranges from [here](https://www.microsoft.com/download/details.aspx?id=41653) and add them tooyour firewall configuration tooensure they allow communication tooAzure (and hello HTTPS (443) port).</span></span>  <span data-ttu-id="737e1-133">Разрешить диапазоны IP-адресов для hello регион Azure, подписки и Запад США (используется для контроля доступа и удостоверений).</span><span class="sxs-lookup"><span data-stu-id="737e1-133">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

* <span data-ttu-id="737e1-134">**Проверьте, если брандмауэр на основе URL-адреса на сервер обработки не блокирует доступ**: при использовании URL-адрес на основе правила брандмауэра на сервере hello убедитесь hello следующие URL-адреса будут добавлены toofirewall конфигурации.</span><span class="sxs-lookup"><span data-stu-id="737e1-134">**Check if URL-based firewall on Process server is not blocking access**:  If you are using a URL based firewall rules on hello server, ensure hello following URLs are added toofirewall configuration.</span></span> 
     
  <span data-ttu-id="737e1-135">`*.accesscontrol.windows.net:`: используется для контроля доступа и управления удостоверениями;</span><span class="sxs-lookup"><span data-stu-id="737e1-135">`*.accesscontrol.windows.net:` Used for access control and identity management</span></span>

  <span data-ttu-id="737e1-136">`*.backup.windowsazure.com:`: используется для передачи данных репликации и оркестрации;</span><span class="sxs-lookup"><span data-stu-id="737e1-136">`*.backup.windowsazure.com:` Used for replication data transfer and orchestration</span></span>

  <span data-ttu-id="737e1-137">`*.blob.core.windows.net:`Используется для доступа к toohello учетной записи хранилища, в котором хранятся данные репликации</span><span class="sxs-lookup"><span data-stu-id="737e1-137">`*.blob.core.windows.net:` Used for access toohello storage account that stores replicated data</span></span>

  <span data-ttu-id="737e1-138">`*.hypervrecoverymanager.windowsazure.com:`: используется для операций управления репликацией и оркестрации;</span><span class="sxs-lookup"><span data-stu-id="737e1-138">`*.hypervrecoverymanager.windowsazure.com:` Used for replication management operations and orchestration</span></span>

  <span data-ttu-id="737e1-139">`time.nist.gov`и `time.windows.com`: использовать toocheck синхронизации времени между системой и глобальное время.</span><span class="sxs-lookup"><span data-stu-id="737e1-139">`time.nist.gov` and `time.windows.com`: Used toocheck time synchronization between system and global time.</span></span>

<span data-ttu-id="737e1-140">URL-адреса для **облака Azure для государственных организаций**:</span><span class="sxs-lookup"><span data-stu-id="737e1-140">URLs for **Azure Government Cloud**:</span></span>

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* <span data-ttu-id="737e1-141">**Проверьте, не блокируют ли доступ параметры прокси-сервера на сервере обработки.**</span><span class="sxs-lookup"><span data-stu-id="737e1-141">**Check if Proxy Settings on Process server are not blocking access**.</span></span>  <span data-ttu-id="737e1-142">При использовании прокси-сервер, убедитесь, что разрешает имя прокси-сервера hello hello DNS-сервером.</span><span class="sxs-lookup"><span data-stu-id="737e1-142">If you are using a Proxy Server, ensure hello proxy server name is resolving by hello DNS server.</span></span>
<span data-ttu-id="737e1-143">toocheck указано во время установки сервера конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="737e1-143">toocheck what you have provided at hello time of Configuration Server setup.</span></span> <span data-ttu-id="737e1-144">Перейдите в раздел tooregistry</span><span class="sxs-lookup"><span data-stu-id="737e1-144">Go tooregistry key</span></span>

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

<span data-ttu-id="737e1-145">Теперь убедитесь, что hello одинаковые параметры используются по данным toosend агента Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="737e1-145">Now ensure that hello same settings are being used by Azure Site Recovery agent toosend data.</span></span>
<span data-ttu-id="737e1-146">Поиск Microsoft Azure Backup</span><span class="sxs-lookup"><span data-stu-id="737e1-146">Search Microsoft Azure  Backup</span></span> 

![Включение репликации](./media/site-recovery-protection-common-errors/mab.png)

<span data-ttu-id="737e1-148">Откройте службу и щелкните "Действие > Изменить свойства".</span><span class="sxs-lookup"><span data-stu-id="737e1-148">Open it and click on Action > Change Properties.</span></span> <span data-ttu-id="737e1-149">На вкладке настройки прокси-сервера вы увидите адрес hello прокси-сервера, в который должны быть такими же, как показано hello реестра.</span><span class="sxs-lookup"><span data-stu-id="737e1-149">Under Proxy Configuration tab, you should see hello proxy address, which should be same as shown by hello registry settings.</span></span> <span data-ttu-id="737e1-150">Если нет, измените его toohello того же адреса.</span><span class="sxs-lookup"><span data-stu-id="737e1-150">If not, please change it toohello same address.</span></span>

![Включение репликации](./media/site-recovery-protection-common-errors/mabproxy.png)

* <span data-ttu-id="737e1-152">**Проверьте, если на сервер обработки не ограничен регулирования пропускной способности**: увеличить пропускную способность hello и проверьте, существует ли проблема hello.</span><span class="sxs-lookup"><span data-stu-id="737e1-152">**Check if Throttle bandwidth is not constrained on Process server**:  Increase hello bandwidth  and check if hello problem still exists.</span></span>

##<a name="next-steps"></a><span data-ttu-id="737e1-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="737e1-153">Next steps</span></span>
<span data-ttu-id="737e1-154">Если вам нужна дополнительная помощь, разнесите запроса слишком[форум ASR](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="737e1-154">If you need more help, then post your query too[ASR forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span></span> <span data-ttu-id="737e1-155">У нас есть сообщество активно и один из наших инженеров будет может tooassist вы.</span><span class="sxs-lookup"><span data-stu-id="737e1-155">We have an active community and one of our engineers will be able tooassist you.</span></span>
