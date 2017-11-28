---
title: "Проверка пропускной способности VPN для виртуальной сети Microsoft Azure | Документы Майкрософт"
description: "Этот документ помогает пользователю проверить пропускную способность сети от своих локальных ресурсов до виртуальной машины Azure."
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
ms.openlocfilehash: 2e0347854b5d30c955a50a01d6f7ba08e24f94b6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-validate-vpn-throughput-to-a-virtual-network"></a><span data-ttu-id="2af04-103">Порядок проверки пропускной способности VPN для виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="2af04-103">How to validate VPN throughput to a virtual network</span></span>

<span data-ttu-id="2af04-104">Подключение к VPN-шлюзу позволяет установить защищенное распределенное соединение между виртуальной сетью в Azure и локальной ИТ-инфраструктурой.</span><span class="sxs-lookup"><span data-stu-id="2af04-104">A VPN gateway connection enables you to establish secure, cross-premises connectivity between your Virtual Network within Azure and your on-premises IT infrastructure.</span></span>

<span data-ttu-id="2af04-105">В этой статье описано, как проверить пропускную способность сети от локальных ресурсов до виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="2af04-105">This article shows how to validate network throughput from the on-premises resources to an Azure virtual machine.</span></span> <span data-ttu-id="2af04-106">Кроме того, в ней приведены рекомендации по устранению неполадок.</span><span class="sxs-lookup"><span data-stu-id="2af04-106">It also provides troubleshooting guidance.</span></span>

>[!NOTE]
><span data-ttu-id="2af04-107">Эта статья помогает диагностировать и устранить распространенные проблемы.</span><span class="sxs-lookup"><span data-stu-id="2af04-107">This article is intended to help diagnose and fix common issues.</span></span> <span data-ttu-id="2af04-108">Если вам не удается решить проблему с помощью приведенных ниже сведений, [обратитесь в службу поддержки](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="2af04-108">If you're unable to solve the issue by using the following information, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
>
>

## <a name="overview"></a><span data-ttu-id="2af04-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="2af04-109">Overview</span></span>

<span data-ttu-id="2af04-110">Подключение к VPN-шлюзу состоит из следующих компонентов:</span><span class="sxs-lookup"><span data-stu-id="2af04-110">The VPN gateway connection involves the following components:</span></span>

- <span data-ttu-id="2af04-111">Локальное VPN-устройство (см. список [проверенных VPN-устройств](vpn-gateway-about-vpn-devices.md#devicetable)).</span><span class="sxs-lookup"><span data-stu-id="2af04-111">On-premises VPN device (view a list of [validated VPN devices)](vpn-gateway-about-vpn-devices.md#devicetable).</span></span>
- <span data-ttu-id="2af04-112">Общедоступный Интернет</span><span class="sxs-lookup"><span data-stu-id="2af04-112">Public Internet</span></span>
- <span data-ttu-id="2af04-113">VPN-шлюз Azure</span><span class="sxs-lookup"><span data-stu-id="2af04-113">Azure VPN gateway</span></span>
- <span data-ttu-id="2af04-114">Виртуальная машина Azure</span><span class="sxs-lookup"><span data-stu-id="2af04-114">Azure virtual machine</span></span>

<span data-ttu-id="2af04-115">На следующей схеме показано логическое подключение между локальной сетью и виртуальной сетью Azure через VPN.</span><span class="sxs-lookup"><span data-stu-id="2af04-115">The following diagram shows the logical connectivity of an on-premises network to an Azure virtual network through VPN.</span></span>

![Логическое подключение сети клиента к сети MSFT с помощью VPN](./media/vpn-gateway-validate-throughput-to-vnet/VPNPerf.png)

## <a name="calculate-the-maximum-expected-ingressegress"></a><span data-ttu-id="2af04-117">Расчет максимального ожидаемого исходящего и входящего трафика</span><span class="sxs-lookup"><span data-stu-id="2af04-117">Calculate the maximum expected ingress/egress</span></span>

1.  <span data-ttu-id="2af04-118">Определите базовые требования приложения к пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="2af04-118">Determine your application's baseline throughput requirements.</span></span>
2.  <span data-ttu-id="2af04-119">Определите предел пропускной способности для VPN-шлюза Azure.</span><span class="sxs-lookup"><span data-stu-id="2af04-119">Determine your Azure VPN gateway throughput limits.</span></span> <span data-ttu-id="2af04-120">Дополнительные сведения см. в разделе "Суммарная пропускная способность в зависимости от SKU и типа VPN" статьи [Планирование и проектирование VPN-шлюза](vpn-gateway-plan-design.md).</span><span class="sxs-lookup"><span data-stu-id="2af04-120">For help, see the "Aggregate throughput by SKU and VPN type" section of [Planning and design for VPN Gateway](vpn-gateway-plan-design.md).</span></span>
3.  <span data-ttu-id="2af04-121">Определите [рекомендованную пропускную способность](../virtual-machines/virtual-machines-windows-sizes.md) для используемого размера виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="2af04-121">Determine the [Azure VM throughput guidance](../virtual-machines/virtual-machines-windows-sizes.md) for your VM size.</span></span>
4.  <span data-ttu-id="2af04-122">Определите пропускную способность поставщика услуг Интернета (ISP).</span><span class="sxs-lookup"><span data-stu-id="2af04-122">Determine your Internet Service Provider (ISP) bandwidth.</span></span>
5.  <span data-ttu-id="2af04-123">Вычислите ожидаемую пропускную способность — наименьшая пропускная способность (виртуальной машины, шлюза, поставщика услуг Интернета) * 0,8.</span><span class="sxs-lookup"><span data-stu-id="2af04-123">Calculate your expected throughput - Least bandwidth of (VM, Gateway, ISP) * 0.8.</span></span>

<span data-ttu-id="2af04-124">Если расчетная пропускная способность не удовлетворяет базовым потребностям приложения, нужно увеличить пропускную способность ресурса, определенного как узкое место.</span><span class="sxs-lookup"><span data-stu-id="2af04-124">If your calculated throughput does not meet your application's baseline throughput requirements, you need to increase the bandwidth of the resource that you identified as the bottleneck.</span></span> <span data-ttu-id="2af04-125">Чтобы изменить размер VPN-шлюза Azure, см. статью [Изменение SKU шлюза](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="2af04-125">To resize an Azure VPN Gateway, see [Changing a gateway SKU](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="2af04-126">Чтобы изменить размер виртуальной машины, см. статью [Изменение размера виртуальной машины](../virtual-machines/virtual-machines-windows-resize-vm.md).</span><span class="sxs-lookup"><span data-stu-id="2af04-126">To resize a virtual machine, see [Resize a VM](../virtual-machines/virtual-machines-windows-resize-vm.md).</span></span> <span data-ttu-id="2af04-127">Если ожидаемая пропускная способность Интернета не обеспечивается, рекомендуем обратиться к поставщику услуг Интернета.</span><span class="sxs-lookup"><span data-stu-id="2af04-127">If you are not experiencing expected Internet bandwidth, you may also want to contact your ISP.</span></span>

## <a name="validate-network-throughput-by-using-performance-tools"></a><span data-ttu-id="2af04-128">Проверка пропускной способности сети с помощью средств повышения производительности</span><span class="sxs-lookup"><span data-stu-id="2af04-128">Validate network throughput by using performance tools</span></span>

<span data-ttu-id="2af04-129">Эту проверку следует выполнять в часы пониженной нагрузки, так как насыщенность пропускной способности туннеля VPN при тестировании не позволяет получить точные результаты.</span><span class="sxs-lookup"><span data-stu-id="2af04-129">This validation should be performed during non-peak hours, as VPN tunnel throughput saturation during testing does not give accurate results.</span></span>

<span data-ttu-id="2af04-130">Для этого теста мы используем средство iPerf, которое работает в Windows и Linux, а также имеет режимы клиента и сервера.</span><span class="sxs-lookup"><span data-stu-id="2af04-130">The tool we use for this test is iPerf, which works on both Windows and Linux and has both client and server modes.</span></span> <span data-ttu-id="2af04-131">Для виртуальных машин Windows его пропускная способность ограничена значением 3 Гбит/с.</span><span class="sxs-lookup"><span data-stu-id="2af04-131">It is limited to 3 Gbps for Windows VMs.</span></span>

<span data-ttu-id="2af04-132">Это средство не выполняет операции чтения и записи на диск.</span><span class="sxs-lookup"><span data-stu-id="2af04-132">This tool does not perform any read/write operations to disk.</span></span> <span data-ttu-id="2af04-133">Оно лишь создает самостоятельно сформированный TCP-трафик с одного конца на другой.</span><span class="sxs-lookup"><span data-stu-id="2af04-133">It solely produces self-generated TCP traffic from one end to the other.</span></span> <span data-ttu-id="2af04-134">По результатам эксперимента, измеряющего пропускную способность между узлами клиента и сервера, средство формирует статистику.</span><span class="sxs-lookup"><span data-stu-id="2af04-134">It generated statistics based on experimentation that measures the bandwidth available between client and server nodes.</span></span> <span data-ttu-id="2af04-135">При тестировании между двумя узлами один выступает в качестве сервера, а другой — клиента.</span><span class="sxs-lookup"><span data-stu-id="2af04-135">When testing between two nodes, one acts as the server and the other as a client.</span></span> <span data-ttu-id="2af04-136">После завершения теста рекомендуется поменять роли местами, чтобы проверить пропускную способность как при отправке, так и при скачивании на обоих узлах.</span><span class="sxs-lookup"><span data-stu-id="2af04-136">Once this test is completed, we recommend that you reverse the roles to test both upload and download throughput on both nodes.</span></span>

### <a name="download-iperf"></a><span data-ttu-id="2af04-137">Скачивание iPerf</span><span class="sxs-lookup"><span data-stu-id="2af04-137">Download iPerf</span></span>
<span data-ttu-id="2af04-138">Скачайте [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span><span class="sxs-lookup"><span data-stu-id="2af04-138">Download [iPerf](https://iperf.fr/download/iperf_3.1/iperf-3.1.2-win64.zip).</span></span> <span data-ttu-id="2af04-139">Дополнительные сведения см. в [документации по iPerf](https://iperf.fr/iperf-doc.php).</span><span class="sxs-lookup"><span data-stu-id="2af04-139">For details, see [iPerf documentation](https://iperf.fr/iperf-doc.php).</span></span>

 >[!NOTE]
 ><span data-ttu-id="2af04-140">Продукты сторонних производителей, обсуждаемые в этой статье, разрабатываются компаниями, независимыми от корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="2af04-140">The third-party products that this article discusses are manufactured by companies that are independent of Microsoft.</span></span> <span data-ttu-id="2af04-141">Корпорация Майкрософт не дает никаких гарантий, явных или подразумеваемых, относительно производительности или надежности таких продуктов.</span><span class="sxs-lookup"><span data-stu-id="2af04-141">Microsoft makes no warranty, implied or otherwise, about the performance or reliability of these products.</span></span>
 >
 >

### <a name="run-iperf-iperf3exe"></a><span data-ttu-id="2af04-142">Запуск iPerf (iperf3.exe)</span><span class="sxs-lookup"><span data-stu-id="2af04-142">Run iPerf (iperf3.exe)</span></span>
1. <span data-ttu-id="2af04-143">Включите правило NSG/ACL, разрешающее такой трафик (для тестирования общедоступного IP-адреса на виртуальной машине Azure).</span><span class="sxs-lookup"><span data-stu-id="2af04-143">Enable an NSG/ACL rule allowing the traffic (for public IP address testing on Azure VM).</span></span>

2. <span data-ttu-id="2af04-144">На обоих узлах включите исключение брандмауэра для порта 5001.</span><span class="sxs-lookup"><span data-stu-id="2af04-144">On both nodes, enable a firewall exception for port 5001.</span></span>

    <span data-ttu-id="2af04-145">**Windows.** Выполните следующую команду от имени администратора:</span><span class="sxs-lookup"><span data-stu-id="2af04-145">**Windows:** Run the following command as an administrator:</span></span>

    ```CMD
    netsh advfirewall firewall add rule name="Open Port 5001" dir=in action=allow protocol=TCP localport=5001
    ```

    <span data-ttu-id="2af04-146">Чтобы удалить правило после окончания тестирования, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2af04-146">To remove the rule when testing is complete, run this command:</span></span>

    ```CMD
    netsh advfirewall firewall delete rule name="Open Port 5001" protocol=TCP localport=5001
    ```
    </br>
    <span data-ttu-id="2af04-147">**Linux в Azure.** Образы Linux в Azure имеют нестрогие брандмауэры.</span><span class="sxs-lookup"><span data-stu-id="2af04-147">**Azure Linux:**  Azure Linux images have permissive firewalls.</span></span> <span data-ttu-id="2af04-148">Когда приложение прослушивает порт, прохождение трафика разрешается.</span><span class="sxs-lookup"><span data-stu-id="2af04-148">If there is an application listening on a port, the traffic is allowed through.</span></span> <span data-ttu-id="2af04-149">Для защищенных пользовательских образов может потребоваться явно открыть нужные порты.</span><span class="sxs-lookup"><span data-stu-id="2af04-149">Custom images that are secured may need ports opened explicitly.</span></span> <span data-ttu-id="2af04-150">В число распространенных брандмауэров уровня ОС для Linux входят `iptables`, `ufw` и `firewalld`.</span><span class="sxs-lookup"><span data-stu-id="2af04-150">Common Linux OS-layer firewalls include `iptables`, `ufw`, or `firewalld`.</span></span>

3. <span data-ttu-id="2af04-151">На узле сервера перейдите в каталог, куда извлекается iperf3.exe.</span><span class="sxs-lookup"><span data-stu-id="2af04-151">On the server node, change to the directory where iperf3.exe is extracted.</span></span> <span data-ttu-id="2af04-152">Затем запустите iPerf в режиме сервера и настройте его для прослушивания порта 5001, как показано в следующих командах:</span><span class="sxs-lookup"><span data-stu-id="2af04-152">Then run iPerf in server mode and set it to listen on port 5001 as the following commands:</span></span>

     ```CMD
     cd c:\iperf-3.1.2-win65

     iperf3.exe -s -p 5001
     ```

4. <span data-ttu-id="2af04-153">На узле клиента перейдите в каталог, куда извлекается средство iperf, и выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2af04-153">On the client node, change to the directory where iperf tool is extracted and then run the following command:</span></span>

    ```CMD
    iperf3.exe -c <IP of the iperf Server> -t 30 -p 5001 -P 32
    ```

    <span data-ttu-id="2af04-154">Клиент передает трафик на сервер через порт 5001 в течение на 30 секунд.</span><span class="sxs-lookup"><span data-stu-id="2af04-154">The client is inducing traffic on port 5001 to the server for 30 seconds.</span></span> <span data-ttu-id="2af04-155">Флаг "-P", указывающий, что мы используем 32 одновременных подключения к узлу сервера.</span><span class="sxs-lookup"><span data-stu-id="2af04-155">The flag '-P ' that indicates we are using 32 simultaneous connections to the server node.</span></span>

    <span data-ttu-id="2af04-156">Ниже представлены выходные данные для этого примера:</span><span class="sxs-lookup"><span data-stu-id="2af04-156">The following screen shows the output from this example:</span></span>

    ![Выходные данные](./media/vpn-gateway-validate-throughput-to-vnet/06theoutput.png)

5. <span data-ttu-id="2af04-158">(НЕОБЯЗАТЕЛЬНО) Чтобы сохранить результаты тестирования, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2af04-158">(OPTIONAL) To preserve the testing results, run this command:</span></span>

    ```CMD
    iperf3.exe -c IPofTheServerToReach -t 30 -p 5001 -P 32  >> output.txt
    ```

6. <span data-ttu-id="2af04-159">После завершения предыдущих шагов выполните те же действия, изменив роли на противоположные, чтобы узел сервера стал клиентом, и наоборот.</span><span class="sxs-lookup"><span data-stu-id="2af04-159">After completing the previous steps, execute the same steps with the roles reversed, so that the server node will now be the client and vice-versa.</span></span>

## <a name="address-slow-file-copy-issues"></a><span data-ttu-id="2af04-160">Решение проблем с низкой скоростью при копировании файлов</span><span class="sxs-lookup"><span data-stu-id="2af04-160">Address slow file copy issues</span></span>
<span data-ttu-id="2af04-161">При использовании проводника или перетаскивании объектов во время сеанса RDP может наблюдаться снижение скорости копирования файлов.</span><span class="sxs-lookup"><span data-stu-id="2af04-161">You may experience slow file coping when using Windows Explorer or dragging and dropping through an RDP session.</span></span> <span data-ttu-id="2af04-162">Обычно эта проблема вызвана одним или обоими следующими факторами:</span><span class="sxs-lookup"><span data-stu-id="2af04-162">This problem is normally due to one or both of the following factors:</span></span>

- <span data-ttu-id="2af04-163">Приложения для копирования файлов, такие как проводник и RDP, не используют несколько потоков при копировании.</span><span class="sxs-lookup"><span data-stu-id="2af04-163">File copy applications, such as Windows Explorer and RDP, do not use multiple threads when copying files.</span></span> <span data-ttu-id="2af04-164">Для повышения производительности используйте многопоточное приложение, например [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx), которое копирует файлы с помощью 16 или 32 потоков.</span><span class="sxs-lookup"><span data-stu-id="2af04-164">For better performance, use a multi-threaded file copy application such as [Richcopy](https://technet.microsoft.com/en-us/magazine/2009.04.utilityspotlight.aspx) to copy files by using 16 or 32 threads.</span></span> <span data-ttu-id="2af04-165">Чтобы изменить число используемых потоков в Richcopy, выберите **Action** (Действие) > **Copy options** (Параметры копирования) > **File copy** (Копирование файлов).</span><span class="sxs-lookup"><span data-stu-id="2af04-165">To change the thread number for file copy in Richcopy, click **Action** > **Copy options** > **File copy**.</span></span><br><br><span data-ttu-id="2af04-166">
![Проблемы с низкой скоростью при копировании файлов](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span><span class="sxs-lookup"><span data-stu-id="2af04-166">
![Slow file copy issues](./media/vpn-gateway-validate-throughput-to-vnet/Richcopy.png)</span></span><br>
- <span data-ttu-id="2af04-167">Недостаточная скорость чтения и записи виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2af04-167">Insufficient VM disk read/write speed.</span></span> <span data-ttu-id="2af04-168">Дополнительные сведения см. в статье [Устранение неполадок службы хранилища Azure](../storage/common/storage-e2e-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="2af04-168">For more information, see [Azure Storage Troubleshooting](../storage/common/storage-e2e-troubleshooting.md).</span></span>

## <a name="on-premises-device-external-facing-interface"></a><span data-ttu-id="2af04-169">Внешний интерфейс для локального устройства</span><span class="sxs-lookup"><span data-stu-id="2af04-169">On-premises device external facing interface</span></span>
<span data-ttu-id="2af04-170">Если IP-адрес для Интернета локального VPN-устройства включен в определение [локальной сети](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) в Azure, вы можете столкнуться с невозможностью запуска VPN, нерегулярными отключениями либо снижением производительности.</span><span class="sxs-lookup"><span data-stu-id="2af04-170">If the on-premises VPN device Internet-facing IP address is included in the [local network](vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) definition in Azure, you may experience inability to bring up the VPN, sporadic disconnects, or performance issues.</span></span>

## <a name="checking-latency"></a><span data-ttu-id="2af04-171">Проверка задержки</span><span class="sxs-lookup"><span data-stu-id="2af04-171">Checking latency</span></span>
<span data-ttu-id="2af04-172">Используйте команду tracert для трассировки до устройства Microsoft Azure, чтобы определить наличие задержки более 100 мс между прыжками.</span><span class="sxs-lookup"><span data-stu-id="2af04-172">Use tracert to trace to Microsoft Azure Edge device to determine if there are any delays exceeding 100 ms between hops.</span></span>

<span data-ttu-id="2af04-173">Из локальной сети запустите *tracert* для виртуального IP-адреса шлюза или виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="2af04-173">From the on-premises network, run *tracert* to the VIP of the Azure Gateway or VM.</span></span> <span data-ttu-id="2af04-174">Если возвращается лишь знак *, значит вы достигли края Azure.</span><span class="sxs-lookup"><span data-stu-id="2af04-174">Once you see only * returned, you know you have reached the Azure edge.</span></span> <span data-ttu-id="2af04-175">Когда возвращаются DNS-имена, содержащие "MSN", значит вы достигли магистрали Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="2af04-175">When you see DNS names that include "MSN" returned, you know you have reached the Microsoft backbone.</span></span><br><br><span data-ttu-id="2af04-176">
![Проверка задержки](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span><span class="sxs-lookup"><span data-stu-id="2af04-176">
![Checking Latency](./media/vpn-gateway-validate-throughput-to-vnet/08checkinglatency.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="2af04-177">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2af04-177">Next steps</span></span>
<span data-ttu-id="2af04-178">Дополнительные сведения доступны в следующих источниках:</span><span class="sxs-lookup"><span data-stu-id="2af04-178">For more information or help, check out the following links:</span></span>

- [<span data-ttu-id="2af04-179">Оптимизации пропускной способности сети для виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="2af04-179">Optimize network throughput for Azure virtual machines</span></span>](../virtual-network/virtual-network-optimize-network-bandwidth.md)
- [<span data-ttu-id="2af04-180">Служба технической поддержки Майкрософт</span><span class="sxs-lookup"><span data-stu-id="2af04-180">Microsoft Support</span></span>](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)
