---
title: "Проверка пропускной способности VPN tooa виртуальная сеть Microsoft Azure | Документы Microsoft"
description: "Hello цель данного документа — toohelp пользователя проверить пропускную способность сети hello из их tooan ресурсы локальной виртуальной машине Azure."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: jasmc
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/10/2017
ms.author: radwiv;chadmat;genli
ms.openlocfilehash: 9cf0b67145645a3c2a9556b0cc910066cc62a9ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toovalidate-vpn-throughput-tooa-virtual-network"></a><span data-ttu-id="3694a-103">Как toovalidate VPN пропускной способности tooa виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="3694a-103">How toovalidate VPN throughput tooa virtual network</span></span>

<span data-ttu-id="3694a-104">Шлюз VPN-подключение позволяет tooestablish безопасность, подключения между организациями между виртуальной сети в Azure и локальной ИТ-инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="3694a-104">A VPN gateway connection enables you tooestablish secure, cross-premises connectivity between your Virtual Network within Azure and your on-premises IT infrastructure.</span></span>

<span data-ttu-id="3694a-105">В этой статье показано, как toovalidate пропускную способность сети из hello локальной tooan ресурсы виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="3694a-105">This article shows how toovalidate network throughput from hello on-premises resources tooan Azure virtual machine.</span></span> <span data-ttu-id="3694a-106">Кроме того, в ней приведены рекомендации по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="3694a-106">It also provides troubleshooting guidance.</span></span>

>[!NOTE]
><span data-ttu-id="3694a-107">Эта статья посвящена toohelp диагностики и устранения распространенных проблем.</span><span class="sxs-lookup"><span data-stu-id="3694a-107">This article is intended toohelp diagnose and fix common issues.</span></span> <span data-ttu-id="3694a-108">Если вы не удается toosolve hello проблема, используя следующую информацию, hello [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="3694a-108">If you're unable toosolve hello issue by using hello following information, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="3694a-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="3694a-109">Overview</span></span>

<span data-ttu-id="3694a-110">Hello шлюза VPN-подключения включает в себя hello следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="3694a-110">hello VPN gateway connection involves hello following components:</span></span>

- <span data-ttu-id="3694a-111">Локальное VPN-устройство (см. список [проверенных VPN-устройств](vpn-gateway-about-vpn-devices.md#devicetable)).</span><span class="sxs-lookup"><span data-stu-id="3694a-111">On-premises VPN device (view a list of [validated VPN devices)](vpn-gateway-about-vpn-devices.md#devicetable).</span></span>
- <span data-ttu-id="3694a-112">Общедоступный Интернет</span><span class="sxs-lookup"><span data-stu-id="3694a-112">Public Internet</span></span>
- <span data-ttu-id="3694a-113">VPN-шлюз Azure</span><span class="sxs-lookup"><span data-stu-id="3694a-113">Azure VPN gateway</span></span>
- <span data-ttu-id="3694a-114">Виртуальная машина Azure</span><span class="sxs-lookup"><span data-stu-id="3694a-114">Azure virtual machine</span></span>

<span data-ttu-id="3694a-115">Hello, следующая диаграмма показывает hello логические подключения локальной сети tooan виртуальной сети Azure через виртуальную частную сеть.</span><span class="sxs-lookup"><span data-stu-id="3694a-115">hello following diagram shows hello logical connectivity of an on-premises network tooan Azure virtual network through VPN.</span></span>

![TooMSFT логические сети клиента подключения к сети с помощью VPN](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-hello-maximum-expected-ingressegress"></a><span data-ttu-id="3694a-117">Вычислить hello максимальный ожидаемый Исходящие и входящие данные</span><span class="sxs-lookup"><span data-stu-id="3694a-117">Calculate hello maximum expected ingress/egress</span></span>

1.  <span data-ttu-id="3694a-118">Определите базовые требования приложения к пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="3694a-118">Determine your application's baseline throughput requirements.</span></span>
2.  <span data-ttu-id="3694a-119">Определите предел пропускной способности для VPN-шлюза Azure.</span><span class="sxs-lookup"><span data-stu-id="3694a-119">Determine your Azure VPN gateway throughput limits.</span></span> <span data-ttu-id="3694a-120">Для получения справки, в разделе hello» суммарную пропускную способность, SKU и VPN типа» [планирования и проектирования для шлюза VPN](vpn-gateway-plan-design.md).</span><span class="sxs-lookup"><span data-stu-id="3694a-120">For help, see hello "Aggregate throughput by SKU and VPN type" section of [Planning and design for VPN Gateway](vpn-gateway-plan-design.md).</span></span>
3.  <span data-ttu-id="3694a-121">Определить hello [виртуальной Машины Azure пропускная способность рекомендации](../virtual-machines/virtual-machines-windows-sizes.md) для размер виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="3694a-121">Determine hello [Azure VM throughput guidance](../virtual-machines/virtual-machines-windows-sizes.md) for your VM size.</span></span>
4.  <span data-ttu-id="3694a-122">Определите пропускную способность поставщика услуг Интернета (ISP).</span><span class="sxs-lookup"><span data-stu-id="3694a-122">Determine your Internet Service Provider (ISP) bandwidth.</span></span>
5.  <span data-ttu-id="3694a-123">Вычислите ожидаемую пропускную способность — наименьшая пропускная способность (виртуальной машины, шлюза, поставщика услуг Интернета) * 0,8.</span><span class="sxs-lookup"><span data-stu-id="3694a-123">Calculate your expected throughput - Least bandwidth of (VM, Gateway, ISP) * 0.8.</span></span>

<span data-ttu-id="3694a-124">Если вычисляемый пропускная способность не соответствует требованиям приложения базовые пропускной способности, необходимо пропускной способности hello tooincrease hello ресурса, который считается hello узким местом.</span><span class="sxs-lookup"><span data-stu-id="3694a-124">If your calculated throughput does not meet your application's baseline throughput requirements, you need tooincrease hello bandwidth of hello resource that you identified as hello bottleneck.</span></span> <span data-ttu-id="3694a-125">tooresize шлюз VPN Azure в разделе [изменение номер SKU шлюза](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="3694a-125">tooresize an Azure VPN Gateway, see [Changing a gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="3694a-126">tooresize виртуальной машины в разделе [изменить размер виртуальной Машины](../virtual-machines/virtual-machines-windows-resize-vm.md).</span><span class="sxs-lookup"><span data-stu-id="3694a-126">tooresize a virtual machine, see [Resize a VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span></span> <span data-ttu-id="3694a-127">Если вы не столкнетесь с ожидаемой пропускной способности Интернета, можно также toocontact поставщика услуг Интернета.</span><span class="sxs-lookup"><span data-stu-id="3694a-127">If you are not experiencing expected Internet bandwidth, you may also want toocontact your ISP.</span></span>

## <a name="validate-network-throughput-by-using-performance-tools"></a><span data-ttu-id="3694a-128">Проверка пропускной способности сети с помощью средств повышения производительности</span><span class="sxs-lookup"><span data-stu-id="3694a-128">Validate network throughput by using performance tools</span></span>

<span data-ttu-id="3694a-129">Эту проверку следует выполнять в часы пониженной нагрузки, так как насыщенность пропускной способности туннеля VPN при тестировании не позволяет получить точные результаты.</span><span class="sxs-lookup"><span data-stu-id="3694a-129">This validation should be performed during non-peak hours, as VPN tunnel throughput saturation during testing does not give accurate results.</span></span>

<span data-ttu-id="3694a-130">Средство Hello, мы используем для этого теста является iPerf, который работает в Windows и Linux и имеет режима сервера и клиента.</span><span class="sxs-lookup"><span data-stu-id="3694a-130">hello tool we use for this test is iPerf, which works on both Windows and Linux and has both client and server modes.</span></span> <span data-ttu-id="3694a-131">Это ограниченное too3 Гбит/с для виртуальных машин Windows.</span><span class="sxs-lookup"><span data-stu-id="3694a-131">It is limited too3 Gbps for Windows VMs.</span></span>

<span data-ttu-id="3694a-132">Это средство не выполняет любой toodisk операций чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="3694a-132">This tool does not perform any read/write operations toodisk.</span></span> <span data-ttu-id="3694a-133">Самостоятельно сформированный трафик TCP от одного конечного toohello других исключительно создается.</span><span class="sxs-lookup"><span data-stu-id="3694a-133">It solely produces self-generated TCP traffic from one end toohello other.</span></span> <span data-ttu-id="3694a-134">Статистику на основании экспериментов, что меры hello пропускную способность между клиентом и сервером узлами, оно создано.</span><span class="sxs-lookup"><span data-stu-id="3694a-134">It generated statistics based on experimentation that measures hello bandwidth available between client and server nodes.</span></span> <span data-ttu-id="3694a-135">При тестировании между двумя узлами, один действует как сервер hello и hello других в качестве клиента.</span><span class="sxs-lookup"><span data-stu-id="3694a-135">When testing between two nodes, one acts as hello server and hello other as a client.</span></span> <span data-ttu-id="3694a-136">После завершения этого теста, рекомендуется, выполняется обратная tootest ролей hello и отправка и загрузка пропускной способности на обоих узлах.</span><span class="sxs-lookup"><span data-stu-id="3694a-136">Once this test is completed, we recommend that you reverse hello roles tootest both upload and download throughput on both nodes.</span></span>

### <a name="download-iperf"></a><span data-ttu-id="3694a-137">Скачивание iPerf</span><span class="sxs-lookup"><span data-stu-id="3694a-137">Download iPerf</span></span>
<span data-ttu-id="3694a-138">Скачайте [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span><span class="sxs-lookup"><span data-stu-id="3694a-138">Download [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span></span> <span data-ttu-id="3694a-139">Дополнительные сведения см. в [документации по iPerf](https://iperf.fr/iperf-doc.php).</span><span class="sxs-lookup"><span data-stu-id="3694a-139">For details, see [iPerf documentation](https://iperf.fr/iperf-doc.php).</span></span>

 >[!NOTE]
 ><span data-ttu-id="3694a-140">Hello сторонние продукты, которые описаны в этой статье, созданы компаниями, не зависимыми от Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3694a-140">hello third-party products that this article discusses are manufactured by companies that are independent of Microsoft.</span></span> <span data-ttu-id="3694a-141">Корпорация Майкрософт не дает никаких гарантий, явных или подразумеваемых гарантий, о hello производительности и надежности этих продуктов.</span><span class="sxs-lookup"><span data-stu-id="3694a-141">Microsoft makes no warranty, implied or otherwise, about hello performance or reliability of these products.</span></span>
 >
 >

### <a name="run-iperf-iperf3exe"></a><span data-ttu-id="3694a-142">Запуск iPerf (iperf3.exe)</span><span class="sxs-lookup"><span data-stu-id="3694a-142">Run iPerf (iperf3.exe)</span></span>
1. <span data-ttu-id="3694a-143">Включите правило NSG и ACL, разрешающее трафик hello (для тестирования на виртуальной Машине Azure общедоступный IP-адрес).</span><span class="sxs-lookup"><span data-stu-id="3694a-143">Enable an NSG/ACL rule allowing hello traffic (for public IP address testing on Azure VM).</span></span>

2. <span data-ttu-id="3694a-144">На обоих узлах включите исключение брандмауэра для порта 5001.</span><span class="sxs-lookup"><span data-stu-id="3694a-144">On both nodes, enable a firewall exception for port 5001.</span></span>

    <span data-ttu-id="3694a-145">**Windows:** выполнения hello следующую команду с правами администратора:</span><span class="sxs-lookup"><span data-stu-id="3694a-145">**Windows:** Run hello following command as an administrator:</span></span>

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    <span data-ttu-id="3694a-146">правило hello tooremove при тестировании завершена, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3694a-146">tooremove hello rule when testing is complete, run this command:</span></span>

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    <span data-ttu-id="3694a-147">**Linux в Azure.** Образы Linux в Azure имеют нестрогие брандмауэры.</span><span class="sxs-lookup"><span data-stu-id="3694a-147">**Azure Linux:**  Azure Linux images have permissive firewalls.</span></span> <span data-ttu-id="3694a-148">В случае прослушивание порта приложения hello-трафика через.</span><span class="sxs-lookup"><span data-stu-id="3694a-148">If there is an application listening on a port, hello traffic is allowed through.</span></span> <span data-ttu-id="3694a-149">Для защищенных пользовательских образов может потребоваться явно открыть нужные порты.</span><span class="sxs-lookup"><span data-stu-id="3694a-149">Custom images that are secured may need ports opened explicitly.</span></span> <span data-ttu-id="3694a-150">В число распространенных брандмауэров уровня ОС для Linux входят `iptables`, `ufw` и `firewalld`.</span><span class="sxs-lookup"><span data-stu-id="3694a-150">Common Linux OS-layer firewalls include `iptables`, `ufw`, or `firewalld`.</span></span>

3. <span data-ttu-id="3694a-151">На узле сервера hello измените toohello каталог, где извлекается iperf3.exe.</span><span class="sxs-lookup"><span data-stu-id="3694a-151">On hello server node, change toohello directory where iperf3.exe is extracted.</span></span> <span data-ttu-id="3694a-152">Затем запустите iPerf в режиме сервера и сделать его toolisten через порт 5001 hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="3694a-152">Then run iPerf in server mode and set it toolisten on port 5001 as hello following commands:</span></span>

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. <span data-ttu-id="3694a-153">На узле клиента hello измените toohello каталог, где средство iperf извлечены и затем выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="3694a-153">On hello client node, change toohello directory where iperf tool is extracted and then run hello following command:</span></span>

    ```CMD
    iperf3.exe -c <IP of hello iperf Server> -t 30 -p 5001 -P 32
    ```

    <span data-ttu-id="3694a-154">Hello клиент инициирует трафик через порт 5001 toohello сервера на 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="3694a-154">hello client is inducing traffic on port 5001 toohello server for 30 seconds.</span></span> <span data-ttu-id="3694a-155">Здравствуйте, флаг "-P", указывающее, мы используем 32 узла сервера toohello одновременных подключений.</span><span class="sxs-lookup"><span data-stu-id="3694a-155">hello flag '-P ' that indicates we are using 32 simultaneous connections toohello server node.</span></span>

    <span data-ttu-id="3694a-156">Hello следующий экран показывает hello выходные данные в этом примере:</span><span class="sxs-lookup"><span data-stu-id="3694a-156">hello following screen shows hello output from this example:</span></span>

    ![Выходные данные](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. <span data-ttu-id="3694a-158">(Необязательно) toopreserve hello тестирование результатов, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="3694a-158">(OPTIONAL) toopreserve hello testing results, run this command:</span></span>

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. <span data-ttu-id="3694a-159">После выполнения предыдущих шагов hello, выполните hello отменить же действия с ролями hello, таким образом, hello узел сервера теперь будет hello клиента и наоборот.</span><span class="sxs-lookup"><span data-stu-id="3694a-159">After completing hello previous steps, execute hello same steps with hello roles reversed, so that hello server node will now be hello client and vice-versa.</span></span>

## <a name="address-slow-file-copy-issues"></a><span data-ttu-id="3694a-160">Решение проблем с низкой скоростью при копировании файлов</span><span class="sxs-lookup"><span data-stu-id="3694a-160">Address slow file copy issues</span></span>
<span data-ttu-id="3694a-161">При использовании проводника или перетаскивании объектов во время сеанса RDP может наблюдаться снижение скорости копирования файлов.</span><span class="sxs-lookup"><span data-stu-id="3694a-161">You may experience slow file coping when using Windows Explorer or dragging and dropping through an RDP session.</span></span> <span data-ttu-id="3694a-162">Эта проблема обычно является из-за tooone или оба hello следующие факторы:</span><span class="sxs-lookup"><span data-stu-id="3694a-162">This problem is normally due tooone or both of hello following factors:</span></span>

- <span data-ttu-id="3694a-163">Приложения для копирования файлов, такие как проводник и RDP, не используют несколько потоков при копировании.</span><span class="sxs-lookup"><span data-stu-id="3694a-163">File copy applications, such as Windows Explorer and RDP, do not use multiple threads when copying files.</span></span> <span data-ttu-id="3694a-164">Для повышения производительности используйте многопоточные копирования файлов, например [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy файлы с помощью потоков 16 или 32.</span><span class="sxs-lookup"><span data-stu-id="3694a-164">For better performance, use a multi-threaded file copy application such as [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) toocopy files by using 16 or 32 threads.</span></span> <span data-ttu-id="3694a-165">Щелкните номер потока hello toochange для копирования файлов в Richcopy, **действия** > **параметры копирования** > **копирование файла**.</span><span class="sxs-lookup"><span data-stu-id="3694a-165">toochange hello thread number for file copy in Richcopy, click **Action** > **Copy options** > **File copy**.</span></span><br><br><span data-ttu-id="3694a-166">
![Проблемы с низкой скоростью при копировании файлов](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span><span class="sxs-lookup"><span data-stu-id="3694a-166">
![Slow file copy issues](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span></span><br>
- <span data-ttu-id="3694a-167">Недостаточная скорость чтения и записи виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="3694a-167">Insufficient VM disk read/write speed.</span></span> <span data-ttu-id="3694a-168">Дополнительные сведения см. в статье [Устранение неполадок службы хранилища Azure](../storage/common/storage-e2e-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="3694a-168">For more information, see [Azure Storage Troubleshooting](../storage/common/storage-e2e-troubleshooting.md).</span></span>

## <a name="on-premises-device-external-facing-interface"></a><span data-ttu-id="3694a-169">Внешний интерфейс для локального устройства</span><span class="sxs-lookup"><span data-stu-id="3694a-169">On-premises device external facing interface</span></span>
<span data-ttu-id="3694a-170">Если hello локального VPN-устройства из Интернета IP-адрес включается в hello [локальной сети](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) определение в Azure, могут возникнуть toobring невозможности hello отключает VPN, случайные или проблем с производительностью.</span><span class="sxs-lookup"><span data-stu-id="3694a-170">If hello on-premises VPN device Internet-facing IP address is included in hello [local network](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definition in Azure, you may experience inability toobring up hello VPN, sporadic disconnects, or performance issues.</span></span>

## <a name="checking-latency"></a><span data-ttu-id="3694a-171">Проверка задержки</span><span class="sxs-lookup"><span data-stu-id="3694a-171">Checking latency</span></span>
<span data-ttu-id="3694a-172">Используйте tracert tootrace tooMicrosoft Azure Edge устройства toodetermine при наличии задержки превышает 100 мс между прыжков.</span><span class="sxs-lookup"><span data-stu-id="3694a-172">Use tracert tootrace tooMicrosoft Azure Edge device toodetermine if there are any delays exceeding 100 ms between hops.</span></span>

<span data-ttu-id="3694a-173">Запустите из локальной сети hello, *tracert* toohello VIP hello шлюза Azure или виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="3694a-173">From hello on-premises network, run *tracert* toohello VIP of hello Azure Gateway or VM.</span></span> <span data-ttu-id="3694a-174">Как только вы увидите только * возвращен, вы знаете, достигнуто hello Azure edge.</span><span class="sxs-lookup"><span data-stu-id="3694a-174">Once you see only * returned, you know you have reached hello Azure edge.</span></span> <span data-ttu-id="3694a-175">При появлении DNS-имена, включающие «MSN» вернул известно, что достигнуто магистрали Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="3694a-175">When you see DNS names that include "MSN" returned, you know you have reached hello Microsoft backbone.</span></span><br><br><span data-ttu-id="3694a-176">
![Проверка задержки](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span><span class="sxs-lookup"><span data-stu-id="3694a-176">
![Checking Latency](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3694a-177">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3694a-177">Next steps</span></span>
<span data-ttu-id="3694a-178">Для получения дополнительных сведений справки ознакомьтесь с hello ссылкам:</span><span class="sxs-lookup"><span data-stu-id="3694a-178">For more information or help, check out hello following links:</span></span>

- [<span data-ttu-id="3694a-179">Оптимизации пропускной способности сети для виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="3694a-179">Optimize network throughput for Azure virtual machines</span></span>](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [<span data-ttu-id="3694a-180">Служба технической поддержки Майкрософт</span><span class="sxs-lookup"><span data-stu-id="3694a-180">Microsoft Support</span></span>](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
