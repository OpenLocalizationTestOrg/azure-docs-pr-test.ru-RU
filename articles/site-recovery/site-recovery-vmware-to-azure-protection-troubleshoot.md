---
title: "Устранение ошибок защиты на виртуальных машинах VMware или физических компьютерах в Azure | Документация Майкрософт"
description: "В этой статье описаны распространенные ошибки репликации компьютера VMware и способы их устранения"
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
ms.openlocfilehash: 6ebec2e06566b1e2d6834fdd81c0d8b2801b80b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a><span data-ttu-id="b4807-103">Устранение неполадок репликации виртуальной машины VMware или физического сервера в локальной среде</span><span class="sxs-lookup"><span data-stu-id="b4807-103">Troubleshoot on-premises VMware/Physical server replication issues</span></span>
<span data-ttu-id="b4807-104">Вы можете получить определенные сообщения об ошибках при защите виртуальных машин VMware или физических серверов с помощью Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b4807-104">You may receive a specific error message when protecting your VMware virtual machines or physical servers using Azure Site Recovery.</span></span> <span data-ttu-id="b4807-105">В этой статье описаны некоторые наиболее распространенные сообщения об ошибках, а также действия по их устранению.</span><span class="sxs-lookup"><span data-stu-id="b4807-105">This article details some of the more common error messages encountered, along with troubleshooting steps to resolve them.</span></span>


## <a name="initial-replication-is-stuck-at-0"></a><span data-ttu-id="b4807-106">Начальная репликация зависла на 0 %</span><span class="sxs-lookup"><span data-stu-id="b4807-106">Initial replication is stuck at 0%</span></span>
<span data-ttu-id="b4807-107">Большинство ошибок начальной репликации, с которой сталкивается служба поддержки, происходят из-за проблем с подключением между исходным сервером для передачи данных, между сервером и процессом или при передаче данных с сервера обработки в Azure.</span><span class="sxs-lookup"><span data-stu-id="b4807-107">Most of the initial replication failures that we encounter at support are due to connectivity issues between source server-to-process server or process server-to-Azure.</span></span>
<span data-ttu-id="b4807-108">В большинстве случаев вы можете самостоятельно устранить эти проблемы, выполнив приведенные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="b4807-108">For most cases, you can self troubleshoot these issues by following the steps listed below.</span></span>

###<a name="check-the-following-on-source-machine"></a><span data-ttu-id="b4807-109">Проверка на исходном компьютере</span><span class="sxs-lookup"><span data-stu-id="b4807-109">Check the following on SOURCE MACHINE</span></span>
* <span data-ttu-id="b4807-110">В командной строке компьютера исходного сервера используйте Telnet, чтобы проверить связь сервера обработки с HTTPS-портом (по умолчанию 9443), как показано ниже, чтобы узнать, существуют ли проблемы с сетевым подключением или с блокировкой порта брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="b4807-110">From Source Server machine command line, use Telnet to ping the Process Server with https port (default 9443) as shown below to see if there are any network connectivity issues or firewall port blocking issues.</span></span>
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > <span data-ttu-id="b4807-111">Используйте Telnet, а не команду PING для проверки соединения.</span><span class="sxs-lookup"><span data-stu-id="b4807-111">Use Telnet, don’t use PING to test connectivity.</span></span>  <span data-ttu-id="b4807-112">Если Telnet не установлен, выполните шаги, указанные [здесь](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx).</span><span class="sxs-lookup"><span data-stu-id="b4807-112">If Telnet is not installed, follow the steps list [here](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span></span>

<span data-ttu-id="b4807-113">Если не удается подключиться, разрешите входящий порт 9443 на сервере обработки и проверьте, не исчезла ли проблема.</span><span class="sxs-lookup"><span data-stu-id="b4807-113">If unable to connect, allow inbound port 9443 on the Process Server and check if the problem still exits.</span></span> <span data-ttu-id="b4807-114">В некоторых случаях, когда сервер обработки находился за промежуточной подсетью, именно это вызывало такую проблему.</span><span class="sxs-lookup"><span data-stu-id="b4807-114">There has been some cases where process server was behind DMZ, which was causing this problem.</span></span>

* <span data-ttu-id="b4807-115">Проверьте состояние службы `InMage Scout VX Agent – Sentinel/OutpostStart`, если она не выполняется, и проверьте, не исчезла ли проблема.</span><span class="sxs-lookup"><span data-stu-id="b4807-115">Check the status of service `InMage Scout VX Agent – Sentinel/OutpostStart` if it is not running and check if the problem still exists.</span></span>   
 
###<a name="check-the-following-on-process-server"></a><span data-ttu-id="b4807-116">Проверка сервера обработки</span><span class="sxs-lookup"><span data-stu-id="b4807-116">Check the following on PROCESS SERVER</span></span>

* <span data-ttu-id="b4807-117">**Проверьте, отправляет ли принудительно сервер обработки данные в Azure.**</span><span class="sxs-lookup"><span data-stu-id="b4807-117">**Check if process server is actively pushing data to Azure**</span></span> 

<span data-ttu-id="b4807-118">Откройте диспетчер задач с компьютера сервера обработки (нажмите сочетание клавиш CTRL+SHIFT+ESC).</span><span class="sxs-lookup"><span data-stu-id="b4807-118">From Process Server machine, open the Task Manager (press Ctrl-Shift-Esc ).</span></span> <span data-ttu-id="b4807-119">Перейдите на вкладку "Производительность" и щелкните ссылку "Открыть монитор ресурсов".</span><span class="sxs-lookup"><span data-stu-id="b4807-119">Go to the Performance tab and click ‘Open Resource Monitor’ link.</span></span> <span data-ttu-id="b4807-120">Из диспетчера ресурсов перейдите на вкладку "Сеть".</span><span class="sxs-lookup"><span data-stu-id="b4807-120">From Resource Manager, go to Network tab.</span></span> <span data-ttu-id="b4807-121">Проверьте, отправляет ли файл cbengine.exe на вкладке "Процессы с сетевой активностью" большие объемы данных (в МБ).</span><span class="sxs-lookup"><span data-stu-id="b4807-121">Check if cbengine.exe in ‘Processes with Network Activity’ is actively sending large volume (in Mbs) of data.</span></span>

![Включение репликации](./media/site-recovery-protection-common-errors/cbengine.png)

<span data-ttu-id="b4807-123">Если нет, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="b4807-123">If not follow the steps listed below:</span></span>

* <span data-ttu-id="b4807-124">**Проверьте, может ли сервер обработки подключится к большому двоичному объекту Azure.** Щелкните cbengine.exe, проверьте его и просмотрите область "Подключения TCP", чтобы определить, есть ли подключение с сервера обработки к URL-адресу большого двоичного объекта хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b4807-124">**Check if Process server is able to connect Azure Blob**: Select and check cbengine.exe to view the ‘TCP Connections’ to see if there is connectivity from Process server to Azure Storage blob URL.</span></span>

![Включение репликации](./media/site-recovery-protection-common-errors/rmonitor.png)

<span data-ttu-id="b4807-126">Если нет, тогда выберите "Панель управления > Службы" и проверьте, работают ли следующие службы:</span><span class="sxs-lookup"><span data-stu-id="b4807-126">If not then go to Control Panel > Services, check if the following services are up and running:</span></span>

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
<span data-ttu-id="b4807-127">Запустите все службы, которые не выполняются, и проверьте, не исчезла ли проблема.</span><span class="sxs-lookup"><span data-stu-id="b4807-127">(Re)Start any service which is not running and check if the problem still exists.</span></span>

* <span data-ttu-id="b4807-128">**Проверьте возможность подключения сервера обработки по общедоступному IP-адресу Azure с помощью порта 443**</span><span class="sxs-lookup"><span data-stu-id="b4807-128">**Check if Process server is able to connect to Azure Public IP address using port 443**</span></span>

<span data-ttu-id="b4807-129">Откройте последний журнал CBEngineCurr.errlog в расположении `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` и найдите строку : 443 и connection attempt failed.</span><span class="sxs-lookup"><span data-stu-id="b4807-129">Open the latest CBEngineCurr.errlog from `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` and search for :443  and connection attempt failed.</span></span>

![Включение репликации](./media/site-recovery-protection-common-errors/logdetails1.png)

<span data-ttu-id="b4807-131">Если возникли проблемы, тогда из командной строки сервера обработки используйте Telnet, чтобы проверить связь своего общедоступного IP-адреса Azure (замаскирован на изображении выше), найденного в CBEngineCurr.currLog, с помощью порта 443.</span><span class="sxs-lookup"><span data-stu-id="b4807-131">If there are issues, then from Process Server command line, use telnet to ping your Azure Public IP address (masked in above image) found in the CBEngineCurr.currLog using port 443.</span></span>

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
<span data-ttu-id="b4807-132">Если вы не можете подключиться, тогда проверьте, произошли ли проблемы доступа из-за брандмауэра или прокси-сервера, как описано в следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="b4807-132">If you are unable to connect, then check if the access issue is due to firewall or Proxy as described in next step.</span></span>


* <span data-ttu-id="b4807-133">**Проверьте, не блокирует ли доступ брандмауэр на основе IP-адресов на сервере обработки.** При использовании правил брандмауэра на основе IP-адресов на сервере скачайте список диапазонов IP-адресов центра обработки данных Microsoft Azure [здесь](https://www.microsoft.com/download/details.aspx?id=41653) и добавьте их в свою конфигурацию брандмауэра, чтобы убедиться, что они позволяют подключение к Azure (и HTTPS-порт 443).</span><span class="sxs-lookup"><span data-stu-id="b4807-133">**Check if IP address-based firewall on Process server are not blocking access**: If you are using an IP address-based firewall rules on the server, then download the complete list of Microsoft Azure Datacenter IP Ranges from [here](https://www.microsoft.com/download/details.aspx?id=41653) and add them to your firewall configuration to ensure they allow communication to Azure (and the HTTPS (443) port).</span></span>  <span data-ttu-id="b4807-134">Необходимо разрешить доступ для диапазонов IP-адресов региона Azure, в котором располагается ваша подписка, и региона "Западная часть США" (используется для контроля доступа и управления удостоверениями).</span><span class="sxs-lookup"><span data-stu-id="b4807-134">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

* <span data-ttu-id="b4807-135">**Проверьте, блокирует ли доступ брандмауэр на основе URL-адреса на сервере обработки.** При использовании брандмауэра на основе URL-адреса на сервере убедитесь, что в конфигурацию брандмауэра добавлены следующие URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="b4807-135">**Check if URL-based firewall on Process server is not blocking access**:  If you are using a URL based firewall rules on the server, ensure the following URLs are added to firewall configuration.</span></span> 
     
  <span data-ttu-id="b4807-136">`*.accesscontrol.windows.net:`: используется для контроля доступа и управления удостоверениями;</span><span class="sxs-lookup"><span data-stu-id="b4807-136">`*.accesscontrol.windows.net:` Used for access control and identity management</span></span>

  <span data-ttu-id="b4807-137">`*.backup.windowsazure.com:`: используется для передачи данных репликации и оркестрации;</span><span class="sxs-lookup"><span data-stu-id="b4807-137">`*.backup.windowsazure.com:` Used for replication data transfer and orchestration</span></span>

  <span data-ttu-id="b4807-138">`*.blob.core.windows.net:`: используется для доступа к учетной записи хранения, в которой хранятся реплицируемые данные;</span><span class="sxs-lookup"><span data-stu-id="b4807-138">`*.blob.core.windows.net:` Used for access to the storage account that stores replicated data</span></span>

  <span data-ttu-id="b4807-139">`*.hypervrecoverymanager.windowsazure.com:`: используется для операций управления репликацией и оркестрации;</span><span class="sxs-lookup"><span data-stu-id="b4807-139">`*.hypervrecoverymanager.windowsazure.com:` Used for replication management operations and orchestration</span></span>

  <span data-ttu-id="b4807-140">`time.nist.gov` и `time.windows.com`: используются для проверки синхронизации времени системы с глобальным временем.</span><span class="sxs-lookup"><span data-stu-id="b4807-140">`time.nist.gov` and `time.windows.com`: Used to check time synchronization between system and global time.</span></span>

<span data-ttu-id="b4807-141">URL-адреса для **облака Azure для государственных организаций**:</span><span class="sxs-lookup"><span data-stu-id="b4807-141">URLs for **Azure Government Cloud**:</span></span>

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* <span data-ttu-id="b4807-142">**Проверьте, не блокируют ли доступ параметры прокси-сервера на сервере обработки.**</span><span class="sxs-lookup"><span data-stu-id="b4807-142">**Check if Proxy Settings on Process server are not blocking access**.</span></span>  <span data-ttu-id="b4807-143">При использовании прокси-сервера убедитесь, что его имя преобразуется DNS-сервером.</span><span class="sxs-lookup"><span data-stu-id="b4807-143">If you are using a Proxy Server, ensure the proxy server name is resolving by the DNS server.</span></span>
<span data-ttu-id="b4807-144">Чтобы проверить параметры, указанные во время настройки сервера конфигурации,</span><span class="sxs-lookup"><span data-stu-id="b4807-144">To check what you have provided at the time of Configuration Server setup.</span></span> <span data-ttu-id="b4807-145">перейдите в раздел реестра</span><span class="sxs-lookup"><span data-stu-id="b4807-145">Go to registry key</span></span>

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

<span data-ttu-id="b4807-146">Теперь убедитесь, что те же параметры используются агентом Azure Site Recovery для отправки данных.</span><span class="sxs-lookup"><span data-stu-id="b4807-146">Now ensure that the same settings are being used by Azure Site Recovery agent to send data.</span></span>
<span data-ttu-id="b4807-147">Поиск Microsoft Azure Backup</span><span class="sxs-lookup"><span data-stu-id="b4807-147">Search Microsoft Azure  Backup</span></span> 

![Включение репликации](./media/site-recovery-protection-common-errors/mab.png)

<span data-ttu-id="b4807-149">Откройте службу и щелкните "Действие > Изменить свойства".</span><span class="sxs-lookup"><span data-stu-id="b4807-149">Open it and click on Action > Change Properties.</span></span> <span data-ttu-id="b4807-150">На вкладке настройки прокси-сервера вы увидите адрес прокси-сервера, который должен соответствовать указанному в параметрах реестра.</span><span class="sxs-lookup"><span data-stu-id="b4807-150">Under Proxy Configuration tab, you should see the proxy address, which should be same as shown by the registry settings.</span></span> <span data-ttu-id="b4807-151">Если нет, измените его на тот же адрес.</span><span class="sxs-lookup"><span data-stu-id="b4807-151">If not, please change it to the same address.</span></span>

![Включение репликации](./media/site-recovery-protection-common-errors/mabproxy.png)

* <span data-ttu-id="b4807-153">**Проверьте, не ограничено ли регулирование пропускной способности на сервере обработки**. Увеличьте пропускную способность и проверьте, не исчезла ли проблема.</span><span class="sxs-lookup"><span data-stu-id="b4807-153">**Check if Throttle bandwidth is not constrained on Process server**:  Increase the bandwidth  and check if the problem still exists.</span></span>

##<a name="next-steps"></a><span data-ttu-id="b4807-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b4807-154">Next steps</span></span>
<span data-ttu-id="b4807-155">Если вам нужна дополнительная помощь, отправьте свой запрос на [форум ASR](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="b4807-155">If you need more help, then post your query to [ASR forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span></span> <span data-ttu-id="b4807-156">У нас есть активное сообщество и один из наших инженеров сможет помочь вам.</span><span class="sxs-lookup"><span data-stu-id="b4807-156">We have an active community and one of our engineers will be able to assist you.</span></span>