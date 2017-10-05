---
title: "Тестирование пропускной способности сети для виртуальной машины Azure | Документация Майкрософт"
description: "Узнайте, как проверить пропускную способность сети для виртуальной машины Azure."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/21/2017
ms.author: steveesp
ms.openlocfilehash: ccebc722386a19014674d7a59757a3685bd50793
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a><span data-ttu-id="d0e87-103">Проверка пропускной способности (NTTTCP)</span><span class="sxs-lookup"><span data-stu-id="d0e87-103">Bandwidth/Throughput testing (NTTTCP)</span></span>

<span data-ttu-id="d0e87-104">При тестировании пропускной способности сети в Azure рекомендуется использовать инструмент, предназначенный для тестирования сети и сводящий к минимуму использование других ресурсов, которые могут повлиять на скорость.</span><span class="sxs-lookup"><span data-stu-id="d0e87-104">When testing network throughput performance in Azure, it's best to use a tool that targets the network for testing and minimizes the use of other resources that could impact performance.</span></span> <span data-ttu-id="d0e87-105">Рекомендуется использовать NTTTCP.</span><span class="sxs-lookup"><span data-stu-id="d0e87-105">NTTTCP is recommended.</span></span>

<span data-ttu-id="d0e87-106">Скопируйте этот инструмент на две виртуальные машины Azure одного размера.</span><span class="sxs-lookup"><span data-stu-id="d0e87-106">Copy the tool to two Azure VMs of the same size.</span></span> <span data-ttu-id="d0e87-107">Одна виртуальная машина выполняет роль отправителя, а другая — получателя.</span><span class="sxs-lookup"><span data-stu-id="d0e87-107">One VM functions as SENDER and the other as RECEIVER.</span></span>

#### <a name="deploying-vms-for-testing"></a><span data-ttu-id="d0e87-108">Развертывание виртуальных машин для тестирования</span><span class="sxs-lookup"><span data-stu-id="d0e87-108">Deploying VMs for testing</span></span>
<span data-ttu-id="d0e87-109">В целях данного теста две виртуальные машины должны находиться в одной облачной службе или одной группе доступности, чтобы мы могли использовать их внутренние IP-адреса и исключить из теста подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="d0e87-109">For the purposes of this test, the two VMs should be in either the same Cloud Service or the same Availability Set so that we can use their internal IPs and exclude the Load Balancers from the test.</span></span> <span data-ttu-id="d0e87-110">Существует возможность тестирования с помощью виртуального IP-адреса, но это выходит за рамки данного документа.</span><span class="sxs-lookup"><span data-stu-id="d0e87-110">It is possible to test with the VIP but this kind of testing is outside the scope of this document.</span></span>
 
<span data-ttu-id="d0e87-111">Запишите IP-адрес получателя.</span><span class="sxs-lookup"><span data-stu-id="d0e87-111">Make a note of the RECEIVER's IP address.</span></span> <span data-ttu-id="d0e87-112">Назовем этот IP-адрес a.b.c.r.</span><span class="sxs-lookup"><span data-stu-id="d0e87-112">Let's call that IP "a.b.c.r"</span></span>

<span data-ttu-id="d0e87-113">Запишите число ядер на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="d0e87-113">Make a note of the number of cores on the VM.</span></span> <span data-ttu-id="d0e87-114">Назовем это значение \#num\_cores.</span><span class="sxs-lookup"><span data-stu-id="d0e87-114">Let's call this "\#num\_cores"</span></span>
 
<span data-ttu-id="d0e87-115">Запустите тест NTTTCP продолжительностью 300 секунд (5 минут) на виртуальной машине-отправителе и виртуальной машине-получателе.</span><span class="sxs-lookup"><span data-stu-id="d0e87-115">Run the NTTTCP test for 300 seconds (or 5 minutes) on the sender VM and receiver VM.</span></span>

<span data-ttu-id="d0e87-116">Совет. При настройке этого теста для первого запуска можно попробовать более короткий период тестирования, чтобы быстрее получить результат.</span><span class="sxs-lookup"><span data-stu-id="d0e87-116">Tip: When setting up this test for the first time, you might try a shorter test period to get feedback sooner.</span></span> <span data-ttu-id="d0e87-117">Если инструмент будет работать ожидаемым образом, продлите период тестирования до 300 секунд, чтобы получить наиболее точные результаты.</span><span class="sxs-lookup"><span data-stu-id="d0e87-117">Once the tool is working as expected, extend the test period to 300 seconds for the most accurate results.</span></span>

> [!NOTE]
> <span data-ttu-id="d0e87-118">Для отправителя **и** получателя нужно указать **одинаковый** параметр длительности теста (-t).</span><span class="sxs-lookup"><span data-stu-id="d0e87-118">The sender **and** receiver must specify **the same** test duration parameter (-t).</span></span>

<span data-ttu-id="d0e87-119">Тестирование отдельного TCP-потока в течение 10 секунд:</span><span class="sxs-lookup"><span data-stu-id="d0e87-119">To test a single TCP stream for 10 seconds:</span></span>

<span data-ttu-id="d0e87-120">Параметры получателя: ntttcp -r -t 10 -P 1</span><span class="sxs-lookup"><span data-stu-id="d0e87-120">Receiver parameters: ntttcp -r -t 10 -P 1</span></span>

<span data-ttu-id="d0e87-121">Параметры отправителя: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span><span class="sxs-lookup"><span data-stu-id="d0e87-121">Sender parameters: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span></span>

> [!NOTE]
> <span data-ttu-id="d0e87-122">Предыдущий пример следует использовать только для подтверждения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d0e87-122">The preceding sample should only be used to confirm your configuration.</span></span> <span data-ttu-id="d0e87-123">Допустимые примеры тестирования рассматриваются далее в этом документе.</span><span class="sxs-lookup"><span data-stu-id="d0e87-123">Valid examples of testing are covered later in this document.</span></span>

## <a name="testing-vms-running-windows"></a><span data-ttu-id="d0e87-124">Тестирование виртуальных машин под управлением Windows</span><span class="sxs-lookup"><span data-stu-id="d0e87-124">Testing VMs running WINDOWS:</span></span>

#### <a name="get-ntttcp-onto-the-vms"></a><span data-ttu-id="d0e87-125">Скопируйте NTTTCP на виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="d0e87-125">Get NTTTCP onto the VMs.</span></span>

<span data-ttu-id="d0e87-126">Скачайте последнюю версию NTTTCP: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span><span class="sxs-lookup"><span data-stu-id="d0e87-126">Download the latest version: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span></span>

<span data-ttu-id="d0e87-127">Или найдите ее, если ссылка уже не работает: <https://www.bing.com/search?q=ntttcp+download>\<. Первый результат поиска должен указывать на последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="d0e87-127">Or search for it if moved: <https://www.bing.com/search?q=ntttcp+download>\< -- should be first hit</span></span>

<span data-ttu-id="d0e87-128">Рекомендуется поместить NTTTCP в отдельную папку, например c:\\tools.</span><span class="sxs-lookup"><span data-stu-id="d0e87-128">Consider putting NTTTCP in separate folder, like c:\\tools</span></span>

#### <a name="allow-ntttcp-through-the-windows-firewall"></a><span data-ttu-id="d0e87-129">Разрешение трафика NTTTCP в брандмауэре Windows</span><span class="sxs-lookup"><span data-stu-id="d0e87-129">Allow NTTTCP through the Windows firewall</span></span>
<span data-ttu-id="d0e87-130">На в брандмауэре Windows виртуальной машине-получателе создайте правило, разрешающее прием трафика NTTTCP.</span><span class="sxs-lookup"><span data-stu-id="d0e87-130">On the RECEIVER, create an Allow rule on the Windows Firewall to allow the NTTTCP traffic to arrive.</span></span> <span data-ttu-id="d0e87-131">Проще разрешить саму программу NTTTCP по имени, чем входящий трафик через определенные TCP-порты.</span><span class="sxs-lookup"><span data-stu-id="d0e87-131">It's easiest to allow the entire NTTTCP program by name rather than to allow specific TCP ports inbound.</span></span>

<span data-ttu-id="d0e87-132">Разрешите трафик NTTTCP в брандмауэре Windows следующей командой.</span><span class="sxs-lookup"><span data-stu-id="d0e87-132">Allow ntttcp through the Windows Firewall like this:</span></span>

<span data-ttu-id="d0e87-133">netsh advfirewall firewall add rule program=\<путь\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="d0e87-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

<span data-ttu-id="d0e87-134">Например, если вы скопировали ntttcp.exe в папку c:\\tools, то это будет следующая команда.</span><span class="sxs-lookup"><span data-stu-id="d0e87-134">For example, if you copied ntttcp.exe to the "c:\\tools" folder, this would be the command:</span></span> 

<span data-ttu-id="d0e87-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="d0e87-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

#### <a name="running-ntttcp-tests"></a><span data-ttu-id="d0e87-136">Выполнение тестов NTTTCP</span><span class="sxs-lookup"><span data-stu-id="d0e87-136">Running NTTTCP tests</span></span>

<span data-ttu-id="d0e87-137">Запустите NTTTCP на виртуальной машине-получателе (**в командной строке**, а не в PowerShell).</span><span class="sxs-lookup"><span data-stu-id="d0e87-137">Start NTTTCP on the RECEIVER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="d0e87-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span><span class="sxs-lookup"><span data-stu-id="d0e87-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span></span>

<span data-ttu-id="d0e87-139">Если у виртуальной машины четыре ядра и IP-адрес 10.0.0.4, то команда будет выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="d0e87-139">If the VM has four cores and an IP address of 10.0.0.4, it would look like this:</span></span>

<span data-ttu-id="d0e87-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="d0e87-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span></span>


<span data-ttu-id="d0e87-141">Запустите NTTTCP на виртуальной машине-отправителе (**в командной строке**, а не в PowerShell).</span><span class="sxs-lookup"><span data-stu-id="d0e87-141">Start NTTTCP on the SENDER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="d0e87-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="d0e87-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span></span> 

<span data-ttu-id="d0e87-143">Дождитесь результатов.</span><span class="sxs-lookup"><span data-stu-id="d0e87-143">Wait for the results.</span></span>


## <a name="testing-vms-running-linux"></a><span data-ttu-id="d0e87-144">Тестирование виртуальных машин под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="d0e87-144">Testing VMs running LINUX:</span></span>

<span data-ttu-id="d0e87-145">Используйте nttcp-for-linux.</span><span class="sxs-lookup"><span data-stu-id="d0e87-145">Use nttcp-for-linux.</span></span> <span data-ttu-id="d0e87-146">Этот инструмент доступен по адресу <https://github.com/Microsoft/ntttcp-for-linux>.</span><span class="sxs-lookup"><span data-stu-id="d0e87-146">It is available from <https://github.com/Microsoft/ntttcp-for-linux></span></span>

<span data-ttu-id="d0e87-147">Выполните приведенные ниже команды на виртуальных машинах Linux (отправителе и получателе), чтобы подготовить на них ntttcp-for-linux.</span><span class="sxs-lookup"><span data-stu-id="d0e87-147">On the Linux VMs (both SENDER and RECEIVER), run these commands to prepare ntttcp-for-linux on your VMs:</span></span>

<span data-ttu-id="d0e87-148">CentOS: установка Git.</span><span class="sxs-lookup"><span data-stu-id="d0e87-148">CentOS - Install Git:</span></span>
``` bash
  yum install gcc -y  
  yum install git -y
```
<span data-ttu-id="d0e87-149">Ubuntu: установка Git.</span><span class="sxs-lookup"><span data-stu-id="d0e87-149">Ubuntu - Install Git:</span></span>
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
<span data-ttu-id="d0e87-150">Создание и установка в обеих ОС.</span><span class="sxs-lookup"><span data-stu-id="d0e87-150">Make and Install on both:</span></span>
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

<span data-ttu-id="d0e87-151">Как и в примере для Windows, предполагается, что IP-адрес виртуальной машины-получателя Linux — 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="d0e87-151">As in the Windows example, we assume the Linux RECEIVER's IP is 10.0.0.4</span></span>

<span data-ttu-id="d0e87-152">Запустите ntttcp-for-linux на виртуальной машине-получателе.</span><span class="sxs-lookup"><span data-stu-id="d0e87-152">Start NTTTCP-for-Linux on the RECEIVER:</span></span>

``` bash
ntttcp -r -t 300
```

<span data-ttu-id="d0e87-153">На виртуальной машине-отправителе выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d0e87-153">And on the SENDER, run:</span></span>

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
<span data-ttu-id="d0e87-154">Если для теста не указан параметр времени, по умолчанию он длится 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="d0e87-154">Test length defaults to 60 seconds if no time parameter is given</span></span>

## <a name="testing-between-vms-running-windows-and-linux"></a><span data-ttu-id="d0e87-155">Тестирование подключения между виртуальными машинами под управлением Windows и Linux</span><span class="sxs-lookup"><span data-stu-id="d0e87-155">Testing between VMs running Windows and LINUX:</span></span>

<span data-ttu-id="d0e87-156">В этом сценарии нам потребуется включить режим без синхронизации, чтобы можно было запустить тест.</span><span class="sxs-lookup"><span data-stu-id="d0e87-156">On this scenarios we should enable the no-sync mode so the test can run.</span></span> <span data-ttu-id="d0e87-157">Это делается с помощью **флага -N** для Linux и **флага -ns** для Windows.</span><span class="sxs-lookup"><span data-stu-id="d0e87-157">This is done by using the **-N flag** for Linux, and **-ns flag** for Windows.</span></span>

#### <a name="from-linux-to-windows"></a><span data-ttu-id="d0e87-158">Из Linux в Windows:</span><span class="sxs-lookup"><span data-stu-id="d0e87-158">From Linux to Windows:</span></span>

<span data-ttu-id="d0e87-159">Получатель <Windows>:</span><span class="sxs-lookup"><span data-stu-id="d0e87-159">Receiver <Windows>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

<span data-ttu-id="d0e87-160">Отправитель <Linux>:</span><span class="sxs-lookup"><span data-stu-id="d0e87-160">Sender <Linux> :</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-to-linux"></a><span data-ttu-id="d0e87-161">Из Windows в Linux:</span><span class="sxs-lookup"><span data-stu-id="d0e87-161">From Windows to Linux:</span></span>

<span data-ttu-id="d0e87-162">Получатель <Linux>:</span><span class="sxs-lookup"><span data-stu-id="d0e87-162">Receiver <Linux>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

<span data-ttu-id="d0e87-163">Отправитель <Windows>:</span><span class="sxs-lookup"><span data-stu-id="d0e87-163">Sender <Windows>:</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a><span data-ttu-id="d0e87-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d0e87-164">Next steps</span></span>
* <span data-ttu-id="d0e87-165">В зависимости от полученных результатов в вашем сценарии вполне может быть возможность [оптимизировать пропускную способность сети виртуальных машин](virtual-network-optimize-network-bandwidth.md).</span><span class="sxs-lookup"><span data-stu-id="d0e87-165">Depending on results, there may be room to [Optimize network throughput machines](virtual-network-optimize-network-bandwidth.md) for your scenario.</span></span>
* <span data-ttu-id="d0e87-166">Узнайте больше из раздела [Виртуальная сеть Azure: часто задаваемые вопросы](virtual-networks-faq.md).</span><span class="sxs-lookup"><span data-stu-id="d0e87-166">Learn more wtih [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
