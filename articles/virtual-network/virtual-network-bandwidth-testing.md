---
title: "пропускная способность сети виртуальной Машины Azure aaaTesting | Документы Microsoft"
description: "Узнайте, как виртуальная машина Azure tootest сетевой пропускной способности."
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
ms.openlocfilehash: 2da85c27bc8d16a443b215891f4cd0460f41926f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a><span data-ttu-id="37fc2-103">Проверка пропускной способности (NTTTCP)</span><span class="sxs-lookup"><span data-stu-id="37fc2-103">Bandwidth/Throughput testing (NTTTCP)</span></span>

<span data-ttu-id="37fc2-104">При тестировании производительность и пропускную способность сети в Azure, это лучший toouse средство, предназначенное hello сети для тестирования и сводит к минимуму использование hello другие ресурсы, которые могут повлиять на производительность.</span><span class="sxs-lookup"><span data-stu-id="37fc2-104">When testing network throughput performance in Azure, it's best toouse a tool that targets hello network for testing and minimizes hello use of other resources that could impact performance.</span></span> <span data-ttu-id="37fc2-105">Рекомендуется использовать NTTTCP.</span><span class="sxs-lookup"><span data-stu-id="37fc2-105">NTTTCP is recommended.</span></span>

<span data-ttu-id="37fc2-106">Скопируйте средство hello tootwo виртуальных машин Azure, hello одинакового размера.</span><span class="sxs-lookup"><span data-stu-id="37fc2-106">Copy hello tool tootwo Azure VMs of hello same size.</span></span> <span data-ttu-id="37fc2-107">Одна виртуальная машина работает как ОТПРАВИТЕЛЯ, так и другие как получатель hello.</span><span class="sxs-lookup"><span data-stu-id="37fc2-107">One VM functions as SENDER and hello other as RECEIVER.</span></span>

#### <a name="deploying-vms-for-testing"></a><span data-ttu-id="37fc2-108">Развертывание виртуальных машин для тестирования</span><span class="sxs-lookup"><span data-stu-id="37fc2-108">Deploying VMs for testing</span></span>
<span data-ttu-id="37fc2-109">В целях hello этого теста hello две виртуальные машины должны находиться в hello одной облачной службе или hello же группу доступности, мы можно использовать свои внутренние IP-адреса и исключить из теста hello hello подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="37fc2-109">For hello purposes of this test, hello two VMs should be in either hello same Cloud Service or hello same Availability Set so that we can use their internal IPs and exclude hello Load Balancers from hello test.</span></span> <span data-ttu-id="37fc2-110">Это возможно tootest с hello виртуальных IP-адресов, но этот тип тестирования выходит за рамки данного документа hello.</span><span class="sxs-lookup"><span data-stu-id="37fc2-110">It is possible tootest with hello VIP but this kind of testing is outside hello scope of this document.</span></span>
 
<span data-ttu-id="37fc2-111">Запишите IP-адрес ПОЛУЧАТЕЛЯ hello.</span><span class="sxs-lookup"><span data-stu-id="37fc2-111">Make a note of hello RECEIVER's IP address.</span></span> <span data-ttu-id="37fc2-112">Назовем этот IP-адрес a.b.c.r.</span><span class="sxs-lookup"><span data-stu-id="37fc2-112">Let's call that IP "a.b.c.r"</span></span>

<span data-ttu-id="37fc2-113">Запишите hello число ядер hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="37fc2-113">Make a note of hello number of cores on hello VM.</span></span> <span data-ttu-id="37fc2-114">Назовем это значение \#num\_cores.</span><span class="sxs-lookup"><span data-stu-id="37fc2-114">Let's call this "\#num\_cores"</span></span>
 
<span data-ttu-id="37fc2-115">Проведение hello отправителя виртуальной Машины и получателя виртуальной Машины hello NTTTCP проверки на 300 секунд (или 5 минут).</span><span class="sxs-lookup"><span data-stu-id="37fc2-115">Run hello NTTTCP test for 300 seconds (or 5 minutes) on hello sender VM and receiver VM.</span></span>

<span data-ttu-id="37fc2-116">Совет: При настройке этого теста для hello первый раз, можно попробовать короткий отзыв tooget периода тестирования быстрее.</span><span class="sxs-lookup"><span data-stu-id="37fc2-116">Tip: When setting up this test for hello first time, you might try a shorter test period tooget feedback sooner.</span></span> <span data-ttu-id="37fc2-117">После hello средство работает надлежащим образом, расширьте секунд периода too300 hello теста для hello наиболее точные результаты.</span><span class="sxs-lookup"><span data-stu-id="37fc2-117">Once hello tool is working as expected, extend hello test period too300 seconds for hello most accurate results.</span></span>

> [!NOTE]
> <span data-ttu-id="37fc2-118">Отправитель Hello **и** необходимо указать получателя **hello же** параметра время проверки (-t).</span><span class="sxs-lookup"><span data-stu-id="37fc2-118">hello sender **and** receiver must specify **hello same** test duration parameter (-t).</span></span>

<span data-ttu-id="37fc2-119">tootest одного потока TCP на 10 секунд:</span><span class="sxs-lookup"><span data-stu-id="37fc2-119">tootest a single TCP stream for 10 seconds:</span></span>

<span data-ttu-id="37fc2-120">Параметры получателя: ntttcp -r -t 10 -P 1</span><span class="sxs-lookup"><span data-stu-id="37fc2-120">Receiver parameters: ntttcp -r -t 10 -P 1</span></span>

<span data-ttu-id="37fc2-121">Параметры отправителя: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span><span class="sxs-lookup"><span data-stu-id="37fc2-121">Sender parameters: ntttcp -s10.27.33.7 -t 10 -n 1 -P 1</span></span>

> [!NOTE]
> <span data-ttu-id="37fc2-122">предшествующий Образец Hello следует использовать tooconfirm конфигурации.</span><span class="sxs-lookup"><span data-stu-id="37fc2-122">hello preceding sample should only be used tooconfirm your configuration.</span></span> <span data-ttu-id="37fc2-123">Допустимые примеры тестирования рассматриваются далее в этом документе.</span><span class="sxs-lookup"><span data-stu-id="37fc2-123">Valid examples of testing are covered later in this document.</span></span>

## <a name="testing-vms-running-windows"></a><span data-ttu-id="37fc2-124">Тестирование виртуальных машин под управлением Windows</span><span class="sxs-lookup"><span data-stu-id="37fc2-124">Testing VMs running WINDOWS:</span></span>

#### <a name="get-ntttcp-onto-hello-vms"></a><span data-ttu-id="37fc2-125">Получите NTTTCP на hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="37fc2-125">Get NTTTCP onto hello VMs.</span></span>

<span data-ttu-id="37fc2-126">Загрузка последней версии hello: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span><span class="sxs-lookup"><span data-stu-id="37fc2-126">Download hello latest version: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769></span></span>

<span data-ttu-id="37fc2-127">Или найдите ее, если ссылка уже не работает: <https://www.bing.com/search?q=ntttcp+download>\<. Первый результат поиска должен указывать на последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="37fc2-127">Or search for it if moved: <https://www.bing.com/search?q=ntttcp+download>\< -- should be first hit</span></span>

<span data-ttu-id="37fc2-128">Рекомендуется поместить NTTTCP в отдельную папку, например c:\\tools.</span><span class="sxs-lookup"><span data-stu-id="37fc2-128">Consider putting NTTTCP in separate folder, like c:\\tools</span></span>

#### <a name="allow-ntttcp-through-hello-windows-firewall"></a><span data-ttu-id="37fc2-129">Разрешить NTTTCP через брандмауэр Windows hello</span><span class="sxs-lookup"><span data-stu-id="37fc2-129">Allow NTTTCP through hello Windows firewall</span></span>
<span data-ttu-id="37fc2-130">На hello ПОЛУЧАТЕЛЯ создайте разрешающее правило на tooallow брандмауэра Windows hello tooarrive трафика NTTTCP.</span><span class="sxs-lookup"><span data-stu-id="37fc2-130">On hello RECEIVER, create an Allow rule on hello Windows Firewall tooallow the NTTTCP traffic tooarrive.</span></span> <span data-ttu-id="37fc2-131">Это простой tooallow hello всей NTTTCP программы по имени, а не tooallow определенные порты TCP входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="37fc2-131">It's easiest tooallow hello entire NTTTCP program by name rather than tooallow specific TCP ports inbound.</span></span>

<span data-ttu-id="37fc2-132">Разрешить ntttcp через hello брандмауэра Windows следующим образом:</span><span class="sxs-lookup"><span data-stu-id="37fc2-132">Allow ntttcp through hello Windows Firewall like this:</span></span>

<span data-ttu-id="37fc2-133">netsh advfirewall firewall add rule program=\<путь\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="37fc2-133">netsh advfirewall firewall add rule program=\<PATH\>\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

<span data-ttu-id="37fc2-134">Например, если вы скопировали ntttcp.exe toohello «c:\\средства» папку, это было бы hello команды:</span><span class="sxs-lookup"><span data-stu-id="37fc2-134">For example, if you copied ntttcp.exe toohello "c:\\tools" folder, this would be hello command:</span></span> 

<span data-ttu-id="37fc2-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span><span class="sxs-lookup"><span data-stu-id="37fc2-135">netsh advfirewall firewall add rule program=c:\\tools\\ntttcp.exe name="ntttcp" protocol=any dir=in action=allow enable=yes profile=ANY</span></span>

#### <a name="running-ntttcp-tests"></a><span data-ttu-id="37fc2-136">Выполнение тестов NTTTCP</span><span class="sxs-lookup"><span data-stu-id="37fc2-136">Running NTTTCP tests</span></span>

<span data-ttu-id="37fc2-137">Запуск NTTTCP hello ПОЛУЧАТЕЛЯ (**запуска из CMD**, а не с PowerShell):</span><span class="sxs-lookup"><span data-stu-id="37fc2-137">Start NTTTCP on hello RECEIVER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="37fc2-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span><span class="sxs-lookup"><span data-stu-id="37fc2-138">ntttcp -r –m [2\*\#num\_cores],\*,a.b.c.r -t 300</span></span>

<span data-ttu-id="37fc2-139">Если hello виртуальной Машины имеет четыре ядра и IP-адрес 10.0.0.4, он будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="37fc2-139">If hello VM has four cores and an IP address of 10.0.0.4, it would look like this:</span></span>

<span data-ttu-id="37fc2-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="37fc2-140">ntttcp -r –m 8,\*,10.0.0.4 -t 300</span></span>


<span data-ttu-id="37fc2-141">Запуск NTTTCP hello ОТПРАВИТЕЛЯ (**запуска из CMD**, а не с PowerShell):</span><span class="sxs-lookup"><span data-stu-id="37fc2-141">Start NTTTCP on hello SENDER (**run from CMD**, not from PowerShell):</span></span>

<span data-ttu-id="37fc2-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span><span class="sxs-lookup"><span data-stu-id="37fc2-142">ntttcp -s –m 8,\*,10.0.0.4 -t 300</span></span> 

<span data-ttu-id="37fc2-143">Ожидание результатов hello.</span><span class="sxs-lookup"><span data-stu-id="37fc2-143">Wait for hello results.</span></span>


## <a name="testing-vms-running-linux"></a><span data-ttu-id="37fc2-144">Тестирование виртуальных машин под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="37fc2-144">Testing VMs running LINUX:</span></span>

<span data-ttu-id="37fc2-145">Используйте nttcp-for-linux.</span><span class="sxs-lookup"><span data-stu-id="37fc2-145">Use nttcp-for-linux.</span></span> <span data-ttu-id="37fc2-146">Этот инструмент доступен по адресу <https://github.com/Microsoft/ntttcp-for-linux>.</span><span class="sxs-lookup"><span data-stu-id="37fc2-146">It is available from <https://github.com/Microsoft/ntttcp-for-linux></span></span>

<span data-ttu-id="37fc2-147">На hello виртуальных машин Linux (ОТПРАВИТЕЛЯ и ПОЛУЧАТЕЛЯ) выполните следующие команды, чтобы подготовить ntttcp для linux на виртуальные машины:</span><span class="sxs-lookup"><span data-stu-id="37fc2-147">On hello Linux VMs (both SENDER and RECEIVER), run these commands to prepare ntttcp-for-linux on your VMs:</span></span>

<span data-ttu-id="37fc2-148">CentOS: установка Git.</span><span class="sxs-lookup"><span data-stu-id="37fc2-148">CentOS - Install Git:</span></span>
``` bash
  yum install gcc -y  
  yum install git -y
```
<span data-ttu-id="37fc2-149">Ubuntu: установка Git.</span><span class="sxs-lookup"><span data-stu-id="37fc2-149">Ubuntu - Install Git:</span></span>
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
<span data-ttu-id="37fc2-150">Создание и установка в обеих ОС.</span><span class="sxs-lookup"><span data-stu-id="37fc2-150">Make and Install on both:</span></span>
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

<span data-ttu-id="37fc2-151">Как показано в примере Windows hello предполагается, что IP-адрес ПОЛУЧАТЕЛЯ hello Linux — 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="37fc2-151">As in hello Windows example, we assume hello Linux RECEIVER's IP is 10.0.0.4</span></span>

<span data-ttu-id="37fc2-152">Начало hello ПОЛУЧАТЕЛЯ NTTTCP для Linux:</span><span class="sxs-lookup"><span data-stu-id="37fc2-152">Start NTTTCP-for-Linux on hello RECEIVER:</span></span>

``` bash
ntttcp -r -t 300
```

<span data-ttu-id="37fc2-153">И на hello ОТПРАВИТЕЛЯ, выполните:</span><span class="sxs-lookup"><span data-stu-id="37fc2-153">And on hello SENDER, run:</span></span>

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
<span data-ttu-id="37fc2-154">Получает значения по умолчанию too60 длины теста секунды, если параметр отсутствует время</span><span class="sxs-lookup"><span data-stu-id="37fc2-154">Test length defaults too60 seconds if no time parameter is given</span></span>

## <a name="testing-between-vms-running-windows-and-linux"></a><span data-ttu-id="37fc2-155">Тестирование подключения между виртуальными машинами под управлением Windows и Linux</span><span class="sxs-lookup"><span data-stu-id="37fc2-155">Testing between VMs running Windows and LINUX:</span></span>

<span data-ttu-id="37fc2-156">В этом сценарии мы следует включить режим без синхронизации hello hello теста для запуска.</span><span class="sxs-lookup"><span data-stu-id="37fc2-156">On this scenarios we should enable hello no-sync mode so hello test can run.</span></span> <span data-ttu-id="37fc2-157">Это делается с помощью hello **-N флаг** для Linux, и **-ns флаг** для Windows.</span><span class="sxs-lookup"><span data-stu-id="37fc2-157">This is done by using hello **-N flag** for Linux, and **-ns flag** for Windows.</span></span>

#### <a name="from-linux-toowindows"></a><span data-ttu-id="37fc2-158">Из Linux tooWindows:</span><span class="sxs-lookup"><span data-stu-id="37fc2-158">From Linux tooWindows:</span></span>

<span data-ttu-id="37fc2-159">Получатель <Windows>:</span><span class="sxs-lookup"><span data-stu-id="37fc2-159">Receiver <Windows>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

<span data-ttu-id="37fc2-160">Отправитель <Linux>:</span><span class="sxs-lookup"><span data-stu-id="37fc2-160">Sender <Linux> :</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-toolinux"></a><span data-ttu-id="37fc2-161">Из Windows tooLinux:</span><span class="sxs-lookup"><span data-stu-id="37fc2-161">From Windows tooLinux:</span></span>

<span data-ttu-id="37fc2-162">Получатель <Linux>:</span><span class="sxs-lookup"><span data-stu-id="37fc2-162">Receiver <Linux>:</span></span>

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

<span data-ttu-id="37fc2-163">Отправитель <Windows>:</span><span class="sxs-lookup"><span data-stu-id="37fc2-163">Sender <Windows>:</span></span>

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a><span data-ttu-id="37fc2-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="37fc2-164">Next steps</span></span>
* <span data-ttu-id="37fc2-165">В зависимости от результатов, возможно, место слишком[оптимизировать пропускную способность виртуальных машин в сети](virtual-network-optimize-network-bandwidth.md) для вашего сценария.</span><span class="sxs-lookup"><span data-stu-id="37fc2-165">Depending on results, there may be room too[Optimize network throughput machines](virtual-network-optimize-network-bandwidth.md) for your scenario.</span></span>
* <span data-ttu-id="37fc2-166">Узнайте больше из раздела [Виртуальная сеть Azure: часто задаваемые вопросы](virtual-networks-faq.md).</span><span class="sxs-lookup"><span data-stu-id="37fc2-166">Learn more wtih [Azure Virtual Network frequently asked questions (FAQ)](virtual-networks-faq.md)</span></span>
