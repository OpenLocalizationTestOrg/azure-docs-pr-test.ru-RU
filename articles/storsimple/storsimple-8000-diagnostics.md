---
title: "устройство StorSimple 8000 tootroubleshoot средство aaaDiagnostics | Документы Microsoft"
description: "Описание режимов устройства StorSimple hello и как toouse Windows PowerShell для StorSimple toochange hello режим устройства."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: e8b7fdbc44d2533973b63da841335ba73ba0014b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-diagnostics-tool-tootroubleshoot-8000-series-device-issues"></a><span data-ttu-id="698c2-103">Используйте hello средство диагностики StorSimple tootroubleshoot 8000 ряда проблем устройствами</span><span class="sxs-lookup"><span data-stu-id="698c2-103">Use hello StorSimple Diagnostics Tool tootroubleshoot 8000 series device issues</span></span>

## <a name="overview"></a><span data-ttu-id="698c2-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="698c2-104">Overview</span></span>

<span data-ttu-id="698c2-105">Средство диагностики StorSimple Hello Диагностика toosystem связанных проблем, производительности, сети и работоспособность компонента оборудования для устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="698c2-105">hello StorSimple Diagnostics tool diagnoses issues related toosystem, performance, network, and hardware component health for a StorSimple device.</span></span> <span data-ttu-id="698c2-106">Средство диагностики Hello может использоваться в различных сценариях.</span><span class="sxs-lookup"><span data-stu-id="698c2-106">hello diagnostics tool can be used in various scenarios.</span></span> <span data-ttu-id="698c2-107">К таким сценариям относятся рабочей нагрузки планирование, развертывание устройства StorSimple, оценки hello сетевой среды и определение hello производительность рабочего устройства.</span><span class="sxs-lookup"><span data-stu-id="698c2-107">These scenarios include workload planning, deploying a StorSimple device, assessing hello network environment, and determining hello performance of an operational device.</span></span> <span data-ttu-id="698c2-108">В этой статье содержится обзор средства диагностики hello и описано использование средства hello с устройством StorSimple.</span><span class="sxs-lookup"><span data-stu-id="698c2-108">This article provides an overview of hello diagnostics tool and describes how hello tool can be used with a StorSimple device.</span></span>

<span data-ttu-id="698c2-109">Средство диагностики Hello в основном предназначен для локальных устройств серии StorSimple 8000 (8100 и 8600).</span><span class="sxs-lookup"><span data-stu-id="698c2-109">hello diagnostics tool is primarily intended for StorSimple 8000 series on-premises devices (8100 and 8600).</span></span>

## <a name="run-diagnostics-tool"></a><span data-ttu-id="698c2-110">Запуск средства диагностики</span><span class="sxs-lookup"><span data-stu-id="698c2-110">Run diagnostics tool</span></span>

<span data-ttu-id="698c2-111">Это средство можно запускать при помощи hello в интерфейсе Windows PowerShell устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="698c2-111">This tool can be run via hello Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="698c2-112">Tooaccess hello локальный интерфейс устройства двумя способами:</span><span class="sxs-lookup"><span data-stu-id="698c2-112">There are two ways tooaccess hello local interface of your device:</span></span>

* <span data-ttu-id="698c2-113">[Последовательной консоли устройства toohello использование PuTTY tooconnect](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="698c2-113">[Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
* <span data-ttu-id="698c2-114">[Удаленный доступ к hello средство через hello Windows PowerShell для StorSimple](storsimple-remote-connect.md).</span><span class="sxs-lookup"><span data-stu-id="698c2-114">[Remotely access hello tool via hello Windows PowerShell for StorSimple](storsimple-remote-connect.md).</span></span>

<span data-ttu-id="698c2-115">В этой статье предполагается, что вы подключились последовательной консоли устройства toohello через PuTTY.</span><span class="sxs-lookup"><span data-stu-id="698c2-115">In this article, we assume that you have connected toohello device serial console via PuTTY.</span></span>

#### <a name="toorun-hello-diagnostics-tool"></a><span data-ttu-id="698c2-116">Средство диагностики toorun hello</span><span class="sxs-lookup"><span data-stu-id="698c2-116">toorun hello diagnostics tool</span></span>

<span data-ttu-id="698c2-117">После подключения toohello интерфейс Windows PowerShell устройства hello выполните следующие шаги toorun hello командлет hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-117">Once you have connected toohello Windows PowerShell interface of hello device, perform hello following steps toorun hello cmdlet.</span></span>
1. <span data-ttu-id="698c2-118">Войдите на последовательную консоль устройства toohello, следуя указаниям hello [последовательной консоли устройства toohello использование PuTTY tooconnect](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="698c2-118">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>

2. <span data-ttu-id="698c2-119">Введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="698c2-119">Type hello following command:</span></span>

    `Invoke-HcsDiagnostics`

    <span data-ttu-id="698c2-120">Если параметр области hello не указан, командлет hello выполняет все диагностические тесты hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-120">If hello scope parameter is not specified, hello cmdlet executes all hello diagnostic tests.</span></span> <span data-ttu-id="698c2-121">(проверка системы, работоспособности компонента оборудования, сети и производительности).</span><span class="sxs-lookup"><span data-stu-id="698c2-121">These tests include system, hardware component health, network, and performance.</span></span> 
    
    <span data-ttu-id="698c2-122">toorun только конкретного теста, укажите параметр области hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-122">toorun only a specific test, specify hello scope parameter.</span></span> <span data-ttu-id="698c2-123">Например toorun только hello тестирование сети, тип</span><span class="sxs-lookup"><span data-stu-id="698c2-123">For instance, toorun only hello network test, type</span></span>

    `Invoke-HcsDiagnostics -Scope Network`

3. <span data-ttu-id="698c2-124">Выделите и скопируйте выходной hello из hello PuTTY окна в текстовый файл для дальнейшего анализа.</span><span class="sxs-lookup"><span data-stu-id="698c2-124">Select and copy hello output from hello PuTTY window into a text file for further analysis.</span></span>

## <a name="scenarios-toouse-hello-diagnostics-tool"></a><span data-ttu-id="698c2-125">Средство диагностики hello toouse сценариев</span><span class="sxs-lookup"><span data-stu-id="698c2-125">Scenarios toouse hello diagnostics tool</span></span>

<span data-ttu-id="698c2-126">Используйте hello диагностики средство tootroubleshoot hello сети, производительности, система и оборудование работоспособности системы hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-126">Use hello diagnostics tool tootroubleshoot hello network, performance, system, and hardware health of hello system.</span></span> <span data-ttu-id="698c2-127">Ниже приведено несколько сценариев.</span><span class="sxs-lookup"><span data-stu-id="698c2-127">Here are some possible scenarios:</span></span>

* <span data-ttu-id="698c2-128">**Устройство не в сети.** Устройство StorSimple серии 8000 находится в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="698c2-128">**Device offline** - Your StorSimple 8000 series device is offline.</span></span> <span data-ttu-id="698c2-129">Однако из интерфейса Windows PowerShell hello, кажется, что оба контроллера hello доступны и запущены.</span><span class="sxs-lookup"><span data-stu-id="698c2-129">However, from hello Windows PowerShell interface, it seems that both hello controllers are up and running.</span></span>
    * <span data-ttu-id="698c2-130">Это средство можно использовать toothen определить состояние сетевого hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-130">You can use this tool toothen determine hello network state.</span></span>
         
         > [!NOTE]
         > <span data-ttu-id="698c2-131">Не используйте это средство tooassess производительности и сетевые параметры на устройстве перед регистрации hello (или настройка с помощью мастера установки).</span><span class="sxs-lookup"><span data-stu-id="698c2-131">Do not use this tool tooassess performance and network settings on a device before hello registration (or configuring via setup wizard).</span></span> <span data-ttu-id="698c2-132">Имеет допустимый IP-адрес назначается toohello устройства во время установки и регистрации.</span><span class="sxs-lookup"><span data-stu-id="698c2-132">A valid IP is assigned toohello device during setup wizard and registration.</span></span> <span data-ttu-id="698c2-133">Этот командлет можно выполнить на незарегистрированном устройстве для проверки работоспособности оборудования и системы.</span><span class="sxs-lookup"><span data-stu-id="698c2-133">You can run this cmdlet, on a device that is not registered, for hardware health and system.</span></span> <span data-ttu-id="698c2-134">Используйте параметр области hello, например:</span><span class="sxs-lookup"><span data-stu-id="698c2-134">Use hello scope parameter, for example:</span></span>
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* <span data-ttu-id="698c2-135">**Проблемы постоянного устройства** -вы испытываете проблемы устройства, которые кажутся toopersist.</span><span class="sxs-lookup"><span data-stu-id="698c2-135">**Persistent device issues** - You are experiencing device issues that seem toopersist.</span></span> <span data-ttu-id="698c2-136">Например, сбой регистрации.</span><span class="sxs-lookup"><span data-stu-id="698c2-136">For instance, registration is failing.</span></span> <span data-ttu-id="698c2-137">Вы может также сталкивается устройства после hello устройство не будет успешно зарегистрирован и оперативной некоторое время.</span><span class="sxs-lookup"><span data-stu-id="698c2-137">You could also be experiencing device issues after hello device is successfully registered and operational for a while.</span></span>
    * <span data-ttu-id="698c2-138">В этом случае используйте это средство для предварительного устранения неполадок, прежде чем отправлять запрос на поддержку Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="698c2-138">In this case, use this tool for preliminary troubleshooting before you log a service request with Microsoft Support.</span></span> <span data-ttu-id="698c2-139">Рекомендуется запустить этот инструмент и отслеживания hello выходные данные этого средства.</span><span class="sxs-lookup"><span data-stu-id="698c2-139">We recommend that you run this tool and capture hello output of this tool.</span></span> <span data-ttu-id="698c2-140">Затем можно предоставить этот tooexpedite tooSupport вывода устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="698c2-140">You can then provide this output tooSupport tooexpedite troubleshooting.</span></span>
    * <span data-ttu-id="698c2-141">В случае сбоев компонентов оборудования или кластера необходимо отправить запрос на поддержку.</span><span class="sxs-lookup"><span data-stu-id="698c2-141">If there are any hardware component or cluster failures, you should log in a Support request.</span></span>

* <span data-ttu-id="698c2-142">**Низкий уровень производительности устройства.** Устройство Your StorSimple медленно работает.</span><span class="sxs-lookup"><span data-stu-id="698c2-142">**Low device performance** - Your StorSimple device is slow.</span></span>
    * <span data-ttu-id="698c2-143">В этом случае используйте этот командлет с tooperformance набор параметров области.</span><span class="sxs-lookup"><span data-stu-id="698c2-143">In this case, run this cmdlet with scope parameter set tooperformance.</span></span> <span data-ttu-id="698c2-144">Анализ вывода hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-144">Analyze hello output.</span></span> <span data-ttu-id="698c2-145">Облако hello получение задержки чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="698c2-145">You get hello cloud read-write latencies.</span></span> <span data-ttu-id="698c2-146">Используйте hello сообщил задержки в качестве максимального достичь целевого объекта, учитывайте некоторые издержки hello внутренней обработки данных, а затем развернуть hello рабочих нагрузок в системе hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-146">Use hello reported latencies as maximum achievable target, factor in some overhead for hello internal data processing, and then deploy hello workloads on hello system.</span></span> <span data-ttu-id="698c2-147">Дополнительные сведения см. слишком[использовать hello сети тестирование tootroubleshoot устройства производительности](#network-test).</span><span class="sxs-lookup"><span data-stu-id="698c2-147">For more information, go too[Use hello network test tootroubleshoot device performance](#network-test).</span></span>


## <a name="diagnostics-test-and-sample-outputs"></a><span data-ttu-id="698c2-148">Диагностическая проверка и пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="698c2-148">Diagnostics test and sample outputs</span></span>

### <a name="hardware-test"></a><span data-ttu-id="698c2-149">Проверка оборудования</span><span class="sxs-lookup"><span data-stu-id="698c2-149">Hardware test</span></span>

<span data-ttu-id="698c2-150">Этот тест определяет состояние hello hello компоненты оборудования, встроенного по USM hello и встроенного по диска hello, выполняемых в системе.</span><span class="sxs-lookup"><span data-stu-id="698c2-150">This test determines hello status of hello hardware components, hello USM firmware, and hello disk firmware running on your system.</span></span>

* <span data-ttu-id="698c2-151">Hello оборудования отчет — эти компоненты этого теста не удалось hello или не присутствуют в системе hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-151">hello hardware components reported are those components that failed hello test or are not present in hello system.</span></span>
* <span data-ttu-id="698c2-152">Hello USM встроенного по диска встроенного по версии и передаются для контроллера 0 контроллер 1 hello и общих компонентов в системе.</span><span class="sxs-lookup"><span data-stu-id="698c2-152">hello USM firmware and disk firmware versions are reported for hello Controller 0, Controller 1, and shared components in your system.</span></span> <span data-ttu-id="698c2-153">Полный список компонентов оборудования см. в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="698c2-153">For a complete list of hardware components, go to:</span></span>

    * [<span data-ttu-id="698c2-154">Список компонентов для основного корпуса устройства StorSimple</span><span class="sxs-lookup"><span data-stu-id="698c2-154">Components in primary enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [<span data-ttu-id="698c2-155">Список компонентов для корпуса EBOD устройства StorSimple</span><span class="sxs-lookup"><span data-stu-id="698c2-155">Components in EBOD enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> <span data-ttu-id="698c2-156">Если проверки оборудования hello сообщает неисправных компонентов [входа в запрос на обслуживание в службу технической поддержки Майкрософт](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="698c2-156">If hello hardware test reports failed components, [log in a service request with Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a><span data-ttu-id="698c2-157">Пример выходных данных проверки оборудования устройства серии 8100</span><span class="sxs-lookup"><span data-stu-id="698c2-157">Sample output of hardware test run on an 8100 device</span></span>

<span data-ttu-id="698c2-158">Ниже приведен пример выходных данных устройства StorSimple 8100.</span><span class="sxs-lookup"><span data-stu-id="698c2-158">Here is a sample output from a StorSimple 8100 device.</span></span> <span data-ttu-id="698c2-159">В модели устройства 8100 hello hello корпусе отсутствует.</span><span class="sxs-lookup"><span data-stu-id="698c2-159">In hello 8100 model device, hello EBOD enclosure is not present.</span></span> <span data-ttu-id="698c2-160">Таким образом компоненты контроллера EBOD hello не фиксируются.</span><span class="sxs-lookup"><span data-stu-id="698c2-160">Hence, hello EBOD controller components are not reported.</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Hardware
Running hardware diagnostics ...
--------------------------------------------------
Hardware components failed or not present
----------------------

           Type           State      Controller           Index     EnclosureId
           ----           -----      ----------           -----     -----------
...rVipResource      NotPresent            None               1            None
...rVipResource      NotPresent            None               2            None
...rVipResource      NotPresent            None               3            None
...rVipResource      NotPresent            None               4            None
...rVipResource      NotPresent            None               5            None
...rVipResource      NotPresent            None               6            None
...rVipResource      NotPresent            None               7            None
...rVipResource      NotPresent            None               8            None
...rVipResource      NotPresent            None               9            None
...rVipResource      NotPresent            None              10            None
...rVipResource      NotPresent            None              11            None

Firmware information
----------------------
TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

--------------------------------------------------
```

### <a name="system-test"></a><span data-ttu-id="698c2-161">Системная проверка</span><span class="sxs-lookup"><span data-stu-id="698c2-161">System test</span></span>

<span data-ttu-id="698c2-162">Этот тест сообщает сведения о системе hello, доступных обновлений hello, сведения о кластере hello и hello службы сведения для вашего устройства.</span><span class="sxs-lookup"><span data-stu-id="698c2-162">This test reports hello system information, hello updates available, hello cluster information, and hello service information for your device.</span></span>

* <span data-ttu-id="698c2-163">сведения о системе Hello включает hello модель, серийный номер устройства, часовой пояс, состояние контроллера и для версии программного обеспечения hello в системе hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-163">hello system information includes hello model, device serial number, time zone, controller status, and hello detailed software version running on hello system.</span></span> <span data-ttu-id="698c2-164">hello toounderstand различных системных параметров сообщила о выходе hello go слишком[интерпретации сведений о системе](#appendix-interpreting-system-information).</span><span class="sxs-lookup"><span data-stu-id="698c2-164">toounderstand hello various system parameters reported as hello output, go too[Interpreting system information](#appendix-interpreting-system-information).</span></span>

* <span data-ttu-id="698c2-165">доступности обновлений Hello отчеты, доступны ли hello обычных и обслуживания режима и их имена связанных пакетов.</span><span class="sxs-lookup"><span data-stu-id="698c2-165">hello update availability reports whether hello regular and maintenance modes are available and their associated package names.</span></span> <span data-ttu-id="698c2-166">Если `RegularUpdates` и `MaintenanceModeUpdates` , `false`, это означает, что hello обновления недоступны.</span><span class="sxs-lookup"><span data-stu-id="698c2-166">If `RegularUpdates` and `MaintenanceModeUpdates` are `false`, this indicates that hello updates are not available.</span></span> <span data-ttu-id="698c2-167">Устройство находится в актуальном состоянии.</span><span class="sxs-lookup"><span data-stu-id="698c2-167">Your device is up-to-date.</span></span>
* <span data-ttu-id="698c2-168">сведения о кластере Hello сведения hello на различных логических компонентов всех групп кластера HCS hello и их соответствующие состояния.</span><span class="sxs-lookup"><span data-stu-id="698c2-168">hello cluster information contains hello information on various logical components of all hello HCS cluster groups and their respective statuses.</span></span> <span data-ttu-id="698c2-169">Если вы видите группы вне сети кластера в этом разделе отчета hello [обратитесь в службу поддержки корпорации Майкрософт](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="698c2-169">If you see an offline cluster group in this section of hello report, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="698c2-170">сведения о службе Hello включает имена hello и состояния всех hello HCS и элементы конфигурации службы, работающие на вашем устройстве.</span><span class="sxs-lookup"><span data-stu-id="698c2-170">hello service information includes hello names and statuses of all hello HCS and CiS services running on your device.</span></span> <span data-ttu-id="698c2-171">Эта информация полезна для hello технической поддержки корпорации Майкрософт в устранении проблемы устройства hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-171">This information is helpful for hello Microsoft Support in troubleshooting hello device issue.</span></span>

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a><span data-ttu-id="698c2-172">Пример выходных данных системной проверки устройства серии 8100</span><span class="sxs-lookup"><span data-stu-id="698c2-172">Sample output of system test run on an 8100 device</span></span>

<span data-ttu-id="698c2-173">Ниже приведен пример выходных данных теста системы hello запускается на устройстве с 8100.</span><span class="sxs-lookup"><span data-stu-id="698c2-173">Here is a sample output of hello system test run on an 8100 device.</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope System
Running system diagnostics ...
--------------------------------------------------

System information
----------------------
Controller0:

InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                : (UTC-08:00) Pacific Time (US & Canada)
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : Disabled
FipsMode                : Enabled

Controller1:
InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                :
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : HttpsAndHttpEnabled
FipsMode                : Enabled

Update availability
----------------------
RegularUpdates              : False
MaintenanceModeUpdates      : False
RegularUpdatesTitle         : {}
MaintenanceModeUpdatesTitle : {}

Cluster information
----------------------
Name                          State OwnerGroup
----                          ----- ----------
ApplicationHostRLUA           Online HCS Cluster Group
Data0v4                       Online HCS Cluster Group
HCS Vnic Resource             Online HCS Cluster Group
hcs_cloud_connectivity_...    Online HCS Cluster Group
hcs_controller_replacement    Online HCS Cluster Group
hcs_datapath_service          Online HCS Cluster Group
hcs_management_servic         Online HCS Cluster Group
hcs_nvram_service             Online HCS Cluster Group
hcs_passive_datapath          Online HCS Passive Cluster Group
hcs_platform_service          Online HCS Cluster Group
hcs_saas_agent_service        Online HCS Cluster Group
HddDataClusterDisk            Online HCS Cluster Group
HddMgmtClusterDisk            Online HCS Cluster Group
HddReplClusterDisk            Online HCS Cluster Group
iSCSI Target Server           Online HCS Cluster Group
NvramClusterDisk              Online HCS Cluster Group
SSAdminRLUA                   Online HCS Cluster Group
SsdDataClusterDisk            Online HCS Cluster Group
SsdNvramClusterDisk           Online HCS Cluster Group

Service information
----------------------
Name                                          Status DisplayName
----                                          ------ -----------
CiSAgentSvc                                   Stopped CiS Service Agent
hcs_cloud_connectivity_...                    Running hcs_cloud_connectivity...
hcs_controller_replacement                    Running HCS Controller Replace...
hcs_datapath_service                          Running HCS Datapath Service
hcs_management_service                        Running HCS Management Service
hcs_minishell                                 Running hcs_minishell
HCS_NVRAM_Service                             Running HCS NVRAM Service
hcs_passive_datapath                          Stopped HCS Passive Datapath S...
hcs_platform_service                          Running HCS Platform Monitor S...
hcs_saas_agent_service                        Running hcs_saas_agent_service
hcs_startup                                   Stopped hcs_startup
--------------------------------------------------
```

### <a name="network-test"></a><span data-ttu-id="698c2-174">Проверка сети</span><span class="sxs-lookup"><span data-stu-id="698c2-174">Network test</span></span>

<span data-ttu-id="698c2-175">Этот тест проверяет hello состояния hello сетевых интерфейсов, порты, DNS и NTP подключения к серверу, SSL сертификат, учетные данные хранилища, серверы обновления toohello подключения и подключения прокси на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="698c2-175">This test validates hello status of hello network interfaces, ports, DNS and NTP server connectivity, SSL certificate, storage account credentials, connectivity toohello Update servers, and web proxy connectivity on your StorSimple device.</span></span>

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a><span data-ttu-id="698c2-176">Пример выходных данных проверки сети при включении только DATA0</span><span class="sxs-lookup"><span data-stu-id="698c2-176">Sample output of network test when only DATA0 is enabled</span></span>

<span data-ttu-id="698c2-177">Ниже приведен пример выходных данных устройства 8100 hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-177">Here is a sample output of hello 8100 device.</span></span> <span data-ttu-id="698c2-178">Вы увидите в выходных данных hello:</span><span class="sxs-lookup"><span data-stu-id="698c2-178">You can see in hello output that:</span></span>
* <span data-ttu-id="698c2-179">Включены и настроены только сетевые интерфейсы DATA0 и DATA1.</span><span class="sxs-lookup"><span data-stu-id="698c2-179">Only DATA 0 and DATA 1 network interfaces are enabled and configured.</span></span>
* <span data-ttu-id="698c2-180">ДАННЫЕ 2 – 5 не включены на портале hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-180">DATA 2 - 5 are not enabled in hello portal.</span></span>
* <span data-ttu-id="698c2-181">Конфигурация DNS-сервера Hello является допустимым и hello устройства могут подключаться с помощью hello DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="698c2-181">hello DNS server configuration is valid and hello device can connect via hello DNS server.</span></span>
* <span data-ttu-id="698c2-182">также подходит Hello соединение с сервером NTP.</span><span class="sxs-lookup"><span data-stu-id="698c2-182">hello NTP server connectivity is also fine.</span></span>
* <span data-ttu-id="698c2-183">Открыты порты 80 и 443.</span><span class="sxs-lookup"><span data-stu-id="698c2-183">Ports 80 and 443 are open.</span></span> <span data-ttu-id="698c2-184">Тем не менее порт 9354 заблокирован.</span><span class="sxs-lookup"><span data-stu-id="698c2-184">However, port 9354 is blocked.</span></span> <span data-ttu-id="698c2-185">В зависимости от hello [требования к системе для сети](storsimple-system-requirements.md), требуется tooopen этот порт для связи шины службы hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-185">Based on hello [system network requirements](storsimple-system-requirements.md), you need tooopen this port for hello service bus communication.</span></span>
* <span data-ttu-id="698c2-186">Hello сертификации SSL является допустимым.</span><span class="sxs-lookup"><span data-stu-id="698c2-186">hello SSL certification is valid.</span></span>
* <span data-ttu-id="698c2-187">Hello устройство может подключиться toohello учетной записи хранилища: _myss8000storageacct_.</span><span class="sxs-lookup"><span data-stu-id="698c2-187">hello device can connect toohello storage account: _myss8000storageacct_.</span></span>
* <span data-ttu-id="698c2-188">серверы tooUpdate Hello подключение является допустимым.</span><span class="sxs-lookup"><span data-stu-id="698c2-188">hello connectivity tooUpdate servers is valid.</span></span>
* <span data-ttu-id="698c2-189">Hello веб-прокси не настроен на этом устройстве.</span><span class="sxs-lookup"><span data-stu-id="698c2-189">hello web proxy is not configured on this device.</span></span>

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a><span data-ttu-id="698c2-190">Пример выходных данных проверки сети при включении DATA0 и DATA1</span><span class="sxs-lookup"><span data-stu-id="698c2-190">Sample output of network test when DATA0 and DATA1 are enabled</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Network
Running network diagnostics ....
--------------------------------------------------
Validating networks .....
Name                Entity              Result              Details
----                ------              ------              -------
Network interface   Data0               Valid
Network interface   Data1               Valid
Network interface   Data2               Not enabled
Network interface   Data3               Not enabled
Network interface   Data4               Not enabled
Network interface   Data5               Not enabled
DNS                 10.222.118.154      Valid
NTP                 time.windows.com    Valid
Port                80                  Open
Port                443                 Open
Port                9354                Blocked
SSL certificate     https://myss8000... Valid
Storage account ... myss8000storageacct Valid
URL                 http://download.... Valid
URL                 http://download.... Valid
Web proxy                               Not enabled         Web proxy is not...
--------------------------------------------------
```

### <a name="performance-test"></a><span data-ttu-id="698c2-191">тест производительности;</span><span class="sxs-lookup"><span data-stu-id="698c2-191">Performance test</span></span>

<span data-ttu-id="698c2-192">Этот тест сообщает производительность cloud hello через задержки чтения и записи hello облака для устройства.</span><span class="sxs-lookup"><span data-stu-id="698c2-192">This test reports hello cloud performance via hello cloud read-write latencies for your device.</span></span> <span data-ttu-id="698c2-193">Это средство можно использовать tooestablish базовых показателей производительности hello облака, можно добиться с помощью StorSimple.</span><span class="sxs-lookup"><span data-stu-id="698c2-193">This tool can be used tooestablish a baseline of hello cloud performance that you can achieve with StorSimple.</span></span> <span data-ttu-id="698c2-194">Hello средство отчетов hello максимальной производительности (наилучший сценарий для чтения и записи задержки), которые можно получить для соединения.</span><span class="sxs-lookup"><span data-stu-id="698c2-194">hello tool reports hello maximum performance (best case scenario for read-write latencies) that you can get for your connection.</span></span>

<span data-ttu-id="698c2-195">Как средство hello сообщает максимальной производительности достижимая hello, мы используем hello сообщила о задержки чтения и записи цели при развертывании hello рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="698c2-195">As hello tool reports hello maximum achievable performance, we can use hello reported read-write latencies as targets when deploying hello workloads.</span></span>

<span data-ttu-id="698c2-196">Hello тест моделирует hello размеры больших двоичных объектов, связанные с типами hello другой том на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-196">hello test simulates hello blob sizes associated with hello different volume types on hello device.</span></span> <span data-ttu-id="698c2-197">Обычные многоуровневые тома и их резервные копии, закрепленные локально, используют большие двоичные объекты на 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="698c2-197">Regular tiered and backups of locally pinned volumes use a 64 KB blob size.</span></span> <span data-ttu-id="698c2-198">Многоуровневые тома с архивацией используют большие двоичные объекты объемом 512 КБ.</span><span class="sxs-lookup"><span data-stu-id="698c2-198">Tiered volumes with archive option checked use 512 KB blob data size.</span></span> <span data-ttu-id="698c2-199">Если устройство имеет многоуровневого и локально закрепленного тома настраиваются только hello теста соответствующей too64 КБ большой двоичный объект будет выполняться размер данных.</span><span class="sxs-lookup"><span data-stu-id="698c2-199">If your device has tiered and locally pinned volumes configured, only hello test corresponding too64 KB blob data size is run.</span></span>

<span data-ttu-id="698c2-200">toouse это средство, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="698c2-200">toouse this tool, perform hello following steps:</span></span>

1.  <span data-ttu-id="698c2-201">Сначала создайте сочетание многоуровневых томов и многоуровневых томов с архивацией.</span><span class="sxs-lookup"><span data-stu-id="698c2-201">First, create a mix of tiered volumes and tiered volumes with archived option checked.</span></span> <span data-ttu-id="698c2-202">Это действие гарантирует, что средство hello выполняет тесты hello 64 КБ и 512 КБ размер большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="698c2-202">This action ensures that hello tool runs hello tests for both 64 KB and 512 KB blob sizes.</span></span>

2. <span data-ttu-id="698c2-203">Используйте командлет hello, после создания и настройки hello тома.</span><span class="sxs-lookup"><span data-stu-id="698c2-203">Run hello cmdlet after you have created and configured hello volumes.</span></span> <span data-ttu-id="698c2-204">Тип:</span><span class="sxs-lookup"><span data-stu-id="698c2-204">Type:</span></span>

    `Invoke-HcsDiagnostics -Scope Performance`

3. <span data-ttu-id="698c2-205">Запишите hello задержки чтения и записи, о которых сообщает анализатор hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-205">Make a note of hello read-write latencies reported by hello tool.</span></span> <span data-ttu-id="698c2-206">Этот тест может занять несколько минут toorun до того, как результаты hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-206">This test can take several minutes toorun before it reports hello results.</span></span>

4. <span data-ttu-id="698c2-207">Если значения задержек подключения hello в категории hello ожидаемого диапазона, то hello задержки, о которых сообщает анализатор hello можно использовать в качестве максимального достичь цели при развертывании hello рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="698c2-207">If hello connection latencies are all under hello expected range, then hello latencies reported by hello tool can be used as maximum achievable target when deploying hello workloads.</span></span> <span data-ttu-id="698c2-208">Учитывайте некоторый запас на внутреннюю обработку данных.</span><span class="sxs-lookup"><span data-stu-id="698c2-208">Factor in some overhead for internal data processing.</span></span>

    <span data-ttu-id="698c2-209">Средство диагностики hello высоки, сообщила hello задержки чтения и записи:</span><span class="sxs-lookup"><span data-stu-id="698c2-209">If hello read-write latencies reported by hello diagnostics tool are high:</span></span>

    1. <span data-ttu-id="698c2-210">Настройки аналитики хранилища для службы BLOB-объектов и анализ hello вывода toounderstand hello задержки для hello учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="698c2-210">Configure Storage Analytics for blob services and analyze hello output toounderstand hello latencies for hello Azure storage account.</span></span> <span data-ttu-id="698c2-211">Подробные инструкции см. слишком[Включение и Настройка аналитики хранилища](../storage/common/storage-enable-and-view-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="698c2-211">For detailed instructions, go too[enable and configure Storage Analytics](../storage/common/storage-enable-and-view-metrics.md).</span></span> <span data-ttu-id="698c2-212">Если эти задержки также высокого уровня и сравним toohello чисел, полученный от hello средство диагностики StorSimple, должны toolog запрос на обслуживание в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="698c2-212">If those latencies are also high and comparable toohello numbers you received from hello StorSimple Diagnostics tool, then you need toolog a service request with Azure storage.</span></span>

    2. <span data-ttu-id="698c2-213">При низкой задержки учетной записи хранилища hello, обратитесь в службу tooinvestigate администратор вашей сети, выдает задержек в сети.</span><span class="sxs-lookup"><span data-stu-id="698c2-213">If hello storage account latencies are low, contact your network administrator tooinvestigate any latency issues in your network.</span></span>

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a><span data-ttu-id="698c2-214">Пример выходных данных проверки производительности устройства серии 8100</span><span class="sxs-lookup"><span data-stu-id="698c2-214">Sample output of performance test run on an 8100 device</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Performance
Running performance diagnostics...
--------------------------------------------------
Cloud performance: writing blobs
Cloud write latency: 194 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: reading blobs..
Cloud read latency: 544 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: writing blobs.
Cloud write latency: 369 ms using credential 'myss8000storageacct', blob size '512KB'
Cloud performance: reading blobs...
Cloud read latency: 4924 ms using credential 'myss8000storageacct', blob size '512KB'
--------------------------------------------------
Controller0>
```

## <a name="appendix-interpreting-system-information"></a><span data-ttu-id="698c2-215">Приложение: интерпретация системных сведений</span><span class="sxs-lookup"><span data-stu-id="698c2-215">Appendix: interpreting system information</span></span>

<span data-ttu-id="698c2-216">Вот таблица какие hello сопоставить различные параметры Windows PowerShell, сведения о системе hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-216">Here is a table describing what hello various Windows PowerShell parameters in hello system information map to.</span></span> 

| <span data-ttu-id="698c2-217">Параметр PowerShell</span><span class="sxs-lookup"><span data-stu-id="698c2-217">PowerShell Parameter</span></span>    | <span data-ttu-id="698c2-218">Описание</span><span class="sxs-lookup"><span data-stu-id="698c2-218">Description</span></span>  |
|-------------------------|------------------|
| <span data-ttu-id="698c2-219">Идентификатор экземпляра</span><span class="sxs-lookup"><span data-stu-id="698c2-219">Instance ID</span></span>             | <span data-ttu-id="698c2-220">С каждым контроллером связан уникальный идентификатор или GUID.</span><span class="sxs-lookup"><span data-stu-id="698c2-220">Every controller has a unique identifier or a GUID associated with it.</span></span>|
| <span data-ttu-id="698c2-221">Имя</span><span class="sxs-lookup"><span data-stu-id="698c2-221">Name</span></span>                    | <span data-ttu-id="698c2-222">Hello понятное имя устройства hello, как настроить с помощью портала Azure hello во время развертывания устройства.</span><span class="sxs-lookup"><span data-stu-id="698c2-222">hello friendly name of hello device as configured through hello Azure portal during device deployment.</span></span> <span data-ttu-id="698c2-223">Понятное имя по умолчанию Hello — серийный номер устройства hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-223">hello default friendly name is hello device serial number.</span></span> |
| <span data-ttu-id="698c2-224">Модель</span><span class="sxs-lookup"><span data-stu-id="698c2-224">Model</span></span>                   | <span data-ttu-id="698c2-225">модель Hello вашего устройства серии StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="698c2-225">hello model of your StorSimple 8000 series device.</span></span> <span data-ttu-id="698c2-226">Hello модели может быть 8100 или 8600.</span><span class="sxs-lookup"><span data-stu-id="698c2-226">hello model can be 8100 or 8600.</span></span>|
| <span data-ttu-id="698c2-227">SerialNumber</span><span class="sxs-lookup"><span data-stu-id="698c2-227">SerialNumber</span></span>            | <span data-ttu-id="698c2-228">серийный номер устройства Hello назначается на заводе hello, а не 15 символов.</span><span class="sxs-lookup"><span data-stu-id="698c2-228">hello device serial number is assigned at hello factory and is 15 characters long.</span></span> <span data-ttu-id="698c2-229">Например, 8600-SHX0991003G44HT:</span><span class="sxs-lookup"><span data-stu-id="698c2-229">For instance, 8600-SHX0991003G44HT indicates:</span></span><br> <span data-ttu-id="698c2-230">8600 — это модель устройства hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-230">8600 – Is hello device model.</span></span><br><span data-ttu-id="698c2-231">SHX — является hello производства узла.</span><span class="sxs-lookup"><span data-stu-id="698c2-231">SHX – Is hello manufacturing site.</span></span><br> <span data-ttu-id="698c2-232">0991003 — определенный продукт;</span><span class="sxs-lookup"><span data-stu-id="698c2-232">0991003 - Is a specific product.</span></span> <br> <span data-ttu-id="698c2-233">G44HT hello, последние 5 цифр, увеличивается на единицу toocreate уникальные серийные номера.</span><span class="sxs-lookup"><span data-stu-id="698c2-233">G44HT- hello last 5 digits are incremented toocreate unique serial numbers.</span></span> <span data-ttu-id="698c2-234">Набор может быть неупорядоченным.</span><span class="sxs-lookup"><span data-stu-id="698c2-234">This may not be a sequential set.</span></span>|
| <span data-ttu-id="698c2-235">TimeZone</span><span class="sxs-lookup"><span data-stu-id="698c2-235">TimeZone</span></span>                | <span data-ttu-id="698c2-236">Hello часовой пояс устройства, настроенным в hello портал Azure во время развертывания устройства.</span><span class="sxs-lookup"><span data-stu-id="698c2-236">hello device time zone as configured in hello Azure portal during device deployment.</span></span>|
| <span data-ttu-id="698c2-237">CurrentController</span><span class="sxs-lookup"><span data-stu-id="698c2-237">CurrentController</span></span>       | <span data-ttu-id="698c2-238">Hello контроллер, подключенных toothrough hello интерфейс Windows PowerShell устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="698c2-238">hello controller that you are connected toothrough hello Windows PowerShell interface of your StorSimple device.</span></span>|
| <span data-ttu-id="698c2-239">ActiveController</span><span class="sxs-lookup"><span data-stu-id="698c2-239">ActiveController</span></span>        | <span data-ttu-id="698c2-240">контроллер Hello, активна на устройстве и управляет все операции сетевого и дискового hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-240">hello controller that is active on your device and is controlling all hello network and disk operations.</span></span> <span data-ttu-id="698c2-241">Это может быть контроллер 0 или 1.</span><span class="sxs-lookup"><span data-stu-id="698c2-241">This can be Controller 0 or Controller 1.</span></span>  |
| <span data-ttu-id="698c2-242">Controller0Status</span><span class="sxs-lookup"><span data-stu-id="698c2-242">Controller0Status</span></span>       | <span data-ttu-id="698c2-243">состояние Hello контроллер 0 на вашем устройстве.</span><span class="sxs-lookup"><span data-stu-id="698c2-243">hello status of Controller 0 on your device.</span></span> <span data-ttu-id="698c2-244">состояние контроллера Hello может быть обычный режим восстановления или недоступен.</span><span class="sxs-lookup"><span data-stu-id="698c2-244">hello controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="698c2-245">Controller1Status</span><span class="sxs-lookup"><span data-stu-id="698c2-245">Controller1Status</span></span>       | <span data-ttu-id="698c2-246">Hello состояние контроллера 1 на вашем устройстве.</span><span class="sxs-lookup"><span data-stu-id="698c2-246">hello status of Controller 1 on your device.</span></span>  <span data-ttu-id="698c2-247">состояние контроллера Hello может быть обычный режим восстановления или недоступен.</span><span class="sxs-lookup"><span data-stu-id="698c2-247">hello controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="698c2-248">SystemMode</span><span class="sxs-lookup"><span data-stu-id="698c2-248">SystemMode</span></span>              | <span data-ttu-id="698c2-249">Здравствуйте, общее состояние устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="698c2-249">hello overall status of your StorSimple device.</span></span> <span data-ttu-id="698c2-250">Состояние устройства Hello может быть обычный, обслуживания, или списания (соответствует toodeactivated в hello портал Azure).</span><span class="sxs-lookup"><span data-stu-id="698c2-250">hello device status can be normal, maintenance, or decommissioned (corresponds toodeactivated in hello Azure portal).</span></span>|
| <span data-ttu-id="698c2-251">FriendlySoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="698c2-251">FriendlySoftwareVersion</span></span> | <span data-ttu-id="698c2-252">Hello понятное строка, соответствующая toohello версию программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="698c2-252">hello friendly string that corresponds toohello device software version.</span></span> <span data-ttu-id="698c2-253">Системы с обновлением 4 hello понятное программное обеспечение версии будет ряда обновления StorSimple 8000 4.0.</span><span class="sxs-lookup"><span data-stu-id="698c2-253">For a system running Update 4, hello friendly software version would be StorSimple 8000 Series Update 4.0.</span></span>|
| <span data-ttu-id="698c2-254">HcsSoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="698c2-254">HcsSoftwareVersion</span></span>      | <span data-ttu-id="698c2-255">версия программного обеспечения HCS Hello запущена на устройстве.</span><span class="sxs-lookup"><span data-stu-id="698c2-255">hello HCS software version running on your device.</span></span> <span data-ttu-id="698c2-256">Для экземпляра hello HCS программного обеспечения версии соответствующего tooStorSimple 8000 ряда обновления 4.0 является 6.3.9600.17820.</span><span class="sxs-lookup"><span data-stu-id="698c2-256">For instance, hello HCS software version corresponding tooStorSimple 8000 Series Update 4.0 is 6.3.9600.17820.</span></span> |
| <span data-ttu-id="698c2-257">ApiVersion</span><span class="sxs-lookup"><span data-stu-id="698c2-257">ApiVersion</span></span>              | <span data-ttu-id="698c2-258">версия программного обеспечения Hello hello API Windows PowerShell устройства HCS hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-258">hello software version of hello Windows PowerShell API of hello HCS device.</span></span>|
| <span data-ttu-id="698c2-259">VhdVersion</span><span class="sxs-lookup"><span data-stu-id="698c2-259">VhdVersion</span></span>              | <span data-ttu-id="698c2-260">версия программного обеспечения Hello hello заводского образа, hello устройства поставлялась вместе с.</span><span class="sxs-lookup"><span data-stu-id="698c2-260">hello software version of hello factory image that hello device was shipped with.</span></span> <span data-ttu-id="698c2-261">При сбросе значения по умолчанию устройств toofactory выполняется версии программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="698c2-261">If you reset your device toofactory defaults, then it runs this software version.</span></span>|
| <span data-ttu-id="698c2-262">OSVersion</span><span class="sxs-lookup"><span data-stu-id="698c2-262">OSVersion</span></span>               | <span data-ttu-id="698c2-263">версия программного обеспечения операционной системы Windows Server hello, запущенного на устройстве hello Hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-263">hello software version of hello Windows Server operating system running on hello device.</span></span> <span data-ttu-id="698c2-264">устройство StorSimple Hello основывается на Windows Server 2012 R2, соответствующий too6.3.9600 hello.</span><span class="sxs-lookup"><span data-stu-id="698c2-264">hello StorSimple device is based off hello Windows Server 2012 R2 that corresponds too6.3.9600.</span></span>|
| <span data-ttu-id="698c2-265">CisAgentVersion</span><span class="sxs-lookup"><span data-stu-id="698c2-265">CisAgentVersion</span></span>         | <span data-ttu-id="698c2-266">версия Hello вашей конфигурации агента на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="698c2-266">hello version for your Cis agent running on your StorSimple device.</span></span> <span data-ttu-id="698c2-267">Этот агент позволяет взаимодействовать со службой StorSimple Manager hello, запущенных в Azure.</span><span class="sxs-lookup"><span data-stu-id="698c2-267">This agent helps communicate with hello StorSimple Manager service running in Azure.</span></span>|
| <span data-ttu-id="698c2-268">MdsAgentVersion</span><span class="sxs-lookup"><span data-stu-id="698c2-268">MdsAgentVersion</span></span>         | <span data-ttu-id="698c2-269">Hello версии соответствующего toohello Mds агент, работающий на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="698c2-269">hello version corresponding toohello Mds agent running on your StorSimple device.</span></span> <span data-ttu-id="698c2-270">Этот агент перемещает toohello данных наблюдения и диагностики службы (MDS).</span><span class="sxs-lookup"><span data-stu-id="698c2-270">This agent moves data toohello Monitoring and Diagnostics Service (MDS).</span></span>|
| <span data-ttu-id="698c2-271">Lsisas2Version</span><span class="sxs-lookup"><span data-stu-id="698c2-271">Lsisas2Version</span></span>          | <span data-ttu-id="698c2-272">Здравствуйте, соответствующие драйверы toohello LSI версии на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="698c2-272">hello version corresponding toohello LSI drivers on your StorSimple device.</span></span>|
| <span data-ttu-id="698c2-273">Capacity</span><span class="sxs-lookup"><span data-stu-id="698c2-273">Capacity</span></span>                | <span data-ttu-id="698c2-274">Hello общая емкость устройства hello в байтах.</span><span class="sxs-lookup"><span data-stu-id="698c2-274">hello total capacity of hello device in bytes.</span></span>|
| <span data-ttu-id="698c2-275">RemoteManagementMode</span><span class="sxs-lookup"><span data-stu-id="698c2-275">RemoteManagementMode</span></span>    | <span data-ttu-id="698c2-276">Указывает, могут ли устройство hello удаленное управление через его интерфейс Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="698c2-276">Indicates whether hello device can be remotely managed via its Windows PowerShell interface.</span></span> |
| <span data-ttu-id="698c2-277">FipsMode</span><span class="sxs-lookup"><span data-stu-id="698c2-277">FipsMode</span></span>                | <span data-ttu-id="698c2-278">Указывает, включен ли режим США федеральным сведения обработки Standard (FIPS) hello на вашем устройстве.</span><span class="sxs-lookup"><span data-stu-id="698c2-278">Indicates whether hello United States Federal Information Processing Standard (FIPS) mode is enabled on your device.</span></span> <span data-ttu-id="698c2-279">стандарт Hello FIPS 140 определяет утвержденные для использования системами нам федеральным правительством компьютера для защиты конфиденциальных данных hello алгоритмов шифрования.</span><span class="sxs-lookup"><span data-stu-id="698c2-279">hello FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for hello protection of sensitive data.</span></span> <span data-ttu-id="698c2-280">Для устройств с обновлением версии 4 или более поздней режим FIPS включен по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="698c2-280">For devices running Update 4 or later, FIPS mode is enabled by default.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="698c2-281">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="698c2-281">Next steps</span></span>

* <span data-ttu-id="698c2-282">Дополнительные сведения hello [синтаксис командлета Invoke-HcsDiagnostics hello](https://technet.microsoft.com/library/mt795371.aspx).</span><span class="sxs-lookup"><span data-stu-id="698c2-282">Learn hello [syntax of hello Invoke-HcsDiagnostics cmdlet](https://technet.microsoft.com/library/mt795371.aspx).</span></span>

* <span data-ttu-id="698c2-283">Дополнительные сведения о том, как слишком[устранения проблем развертывания](storsimple-troubleshoot-deployment.md) на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="698c2-283">Learn more about how too[troubleshoot deployment issues](storsimple-troubleshoot-deployment.md) on your StorSimple device.</span></span>
