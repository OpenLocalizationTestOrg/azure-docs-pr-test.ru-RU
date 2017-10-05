---
title: "Средство диагностики для устранения неполадок устройства StorSimple 8000 | Документация Майкрософт"
description: "В статье описываются режимы устройства StorSimple и объясняется, как изменить режим устройства StorSimple с помощью Windows PowerShell."
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
ms.openlocfilehash: 8fae7bb357f8e5e8eff249edfe3a2aaafe04283c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-storsimple-diagnostics-tool-to-troubleshoot-8000-series-device-issues"></a><span data-ttu-id="2cb5b-103">Устранение неполадок устройства серии 8000 с помощью средства диагностики StorSimple</span><span class="sxs-lookup"><span data-stu-id="2cb5b-103">Use the StorSimple Diagnostics Tool to troubleshoot 8000 series device issues</span></span>

## <a name="overview"></a><span data-ttu-id="2cb5b-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="2cb5b-104">Overview</span></span>

<span data-ttu-id="2cb5b-105">Средство диагностики StorSimple диагностирует проблемы, связанные с системой, производительностью, сетью и работоспособностью компонентов оборудования устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-105">The StorSimple Diagnostics tool diagnoses issues related to system, performance, network, and hardware component health for a StorSimple device.</span></span> <span data-ttu-id="2cb5b-106">Средство диагностики можно использовать в различных сценариях,</span><span class="sxs-lookup"><span data-stu-id="2cb5b-106">The diagnostics tool can be used in various scenarios.</span></span> <span data-ttu-id="2cb5b-107">таких как планирование рабочей нагрузки, развертывание устройства StorSimple, оценка сетевой среды и определение производительности работающего устройства.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-107">These scenarios include workload planning, deploying a StorSimple device, assessing the network environment, and determining the performance of an operational device.</span></span> <span data-ttu-id="2cb5b-108">В этой статье представлен обзор средства диагностики и описание его использования с устройством StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-108">This article provides an overview of the diagnostics tool and describes how the tool can be used with a StorSimple device.</span></span>

<span data-ttu-id="2cb5b-109">Средство диагностики в основном предназначено для локальных устройств StorSimple серии 8000 (8100 и 8600).</span><span class="sxs-lookup"><span data-stu-id="2cb5b-109">The diagnostics tool is primarily intended for StorSimple 8000 series on-premises devices (8100 and 8600).</span></span>

## <a name="run-diagnostics-tool"></a><span data-ttu-id="2cb5b-110">Запуск средства диагностики</span><span class="sxs-lookup"><span data-stu-id="2cb5b-110">Run diagnostics tool</span></span>

<span data-ttu-id="2cb5b-111">Это средство можно запустить из интерфейса Windows PowerShell устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-111">This tool can be run via the Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="2cb5b-112">Доступ к локальному интерфейсу устройства можно получить двумя способами:</span><span class="sxs-lookup"><span data-stu-id="2cb5b-112">There are two ways to access the local interface of your device:</span></span>

* <span data-ttu-id="2cb5b-113">[подключение к последовательной консоли устройства с помощью PuTTY](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console);</span><span class="sxs-lookup"><span data-stu-id="2cb5b-113">[Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
* <span data-ttu-id="2cb5b-114">[удаленное подключение к устройству через Windows PowerShell для StorSimple](storsimple-remote-connect.md).</span><span class="sxs-lookup"><span data-stu-id="2cb5b-114">[Remotely access the tool via the Windows PowerShell for StorSimple](storsimple-remote-connect.md).</span></span>

<span data-ttu-id="2cb5b-115">В этой статье предполагается, что вы подключились к последовательной консоли устройства с помощью PuTTY.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-115">In this article, we assume that you have connected to the device serial console via PuTTY.</span></span>

#### <a name="to-run-the-diagnostics-tool"></a><span data-ttu-id="2cb5b-116">Запуск средства диагностики</span><span class="sxs-lookup"><span data-stu-id="2cb5b-116">To run the diagnostics tool</span></span>

<span data-ttu-id="2cb5b-117">Подключившись к интерфейсу Windows PowerShell устройства, выполните командлет, сделав следующее.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-117">Once you have connected to the Windows PowerShell interface of the device, perform the following steps to run the cmdlet.</span></span>
1. <span data-ttu-id="2cb5b-118">Войдите в последовательную консоль устройства, выполнив действия, описанные в разделе [Использование PuTTY для подключения к последовательной консоли устройства](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="2cb5b-118">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>

2. <span data-ttu-id="2cb5b-119">Введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2cb5b-119">Type the following command:</span></span>

    `Invoke-HcsDiagnostics`

    <span data-ttu-id="2cb5b-120">Если параметр области не указан, командлет выполняет все диагностические тесты</span><span class="sxs-lookup"><span data-stu-id="2cb5b-120">If the scope parameter is not specified, the cmdlet executes all the diagnostic tests.</span></span> <span data-ttu-id="2cb5b-121">(проверка системы, работоспособности компонента оборудования, сети и производительности).</span><span class="sxs-lookup"><span data-stu-id="2cb5b-121">These tests include system, hardware component health, network, and performance.</span></span> 
    
    <span data-ttu-id="2cb5b-122">Чтобы выполнить определенный тест, укажите параметр области.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-122">To run only a specific test, specify the scope parameter.</span></span> <span data-ttu-id="2cb5b-123">Например, чтобы проверить только сеть, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="2cb5b-123">For instance, to run only the network test, type</span></span>

    `Invoke-HcsDiagnostics -Scope Network`

3. <span data-ttu-id="2cb5b-124">Выберите и скопируйте выходные данные из окна PuTTY в текстовый файл для дальнейшего анализа.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-124">Select and copy the output from the PuTTY window into a text file for further analysis.</span></span>

## <a name="scenarios-to-use-the-diagnostics-tool"></a><span data-ttu-id="2cb5b-125">Сценарии использования средства диагностики</span><span class="sxs-lookup"><span data-stu-id="2cb5b-125">Scenarios to use the diagnostics tool</span></span>

<span data-ttu-id="2cb5b-126">Средство диагностики позволяет устранять неполадки сети, производительности, системы и работоспособности системного оборудования.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-126">Use the diagnostics tool to troubleshoot the network, performance, system, and hardware health of the system.</span></span> <span data-ttu-id="2cb5b-127">Ниже приведено несколько сценариев.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-127">Here are some possible scenarios:</span></span>

* <span data-ttu-id="2cb5b-128">**Устройство не в сети.** Устройство StorSimple серии 8000 находится в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-128">**Device offline** - Your StorSimple 8000 series device is offline.</span></span> <span data-ttu-id="2cb5b-129">Однако в интерфейсе Windows PowerShell видно, что оба контроллера запущены и работают.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-129">However, from the Windows PowerShell interface, it seems that both the controllers are up and running.</span></span>
    * <span data-ttu-id="2cb5b-130">Это средство можно использовать для определения состояния сети.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-130">You can use this tool to then determine the network state.</span></span>
         
         > [!NOTE]
         > <span data-ttu-id="2cb5b-131">Не используйте это средство для оценки параметров производительности и сетевых параметров на устройстве перед регистрацией (или настройкой с помощью мастера установки).</span><span class="sxs-lookup"><span data-stu-id="2cb5b-131">Do not use this tool to assess performance and network settings on a device before the registration (or configuring via setup wizard).</span></span> <span data-ttu-id="2cb5b-132">Во время регистрации и работы с мастером настройки устройству назначается допустимый IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-132">A valid IP is assigned to the device during setup wizard and registration.</span></span> <span data-ttu-id="2cb5b-133">Этот командлет можно выполнить на незарегистрированном устройстве для проверки работоспособности оборудования и системы.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-133">You can run this cmdlet, on a device that is not registered, for hardware health and system.</span></span> <span data-ttu-id="2cb5b-134">Используйте параметр области в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="2cb5b-134">Use the scope parameter, for example:</span></span>
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* <span data-ttu-id="2cb5b-135">**Постоянные проблемы с устройством.** Вы столкнулись с проблемами устройства, которые невозможно устранить.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-135">**Persistent device issues** - You are experiencing device issues that seem to persist.</span></span> <span data-ttu-id="2cb5b-136">Например, сбой регистрации.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-136">For instance, registration is failing.</span></span> <span data-ttu-id="2cb5b-137">Кроме того, проблемы с устройством могут возникнуть после того, как оно будет зарегистрировано и поработает некоторое время.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-137">You could also be experiencing device issues after the device is successfully registered and operational for a while.</span></span>
    * <span data-ttu-id="2cb5b-138">В этом случае используйте это средство для предварительного устранения неполадок, прежде чем отправлять запрос на поддержку Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-138">In this case, use this tool for preliminary troubleshooting before you log a service request with Microsoft Support.</span></span> <span data-ttu-id="2cb5b-139">Мы рекомендуем запустить это средство и сохранить его выходные данные.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-139">We recommend that you run this tool and capture the output of this tool.</span></span> <span data-ttu-id="2cb5b-140">Затем их можно предоставить в службу поддержки, чтобы ускорить процесс устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-140">You can then provide this output to Support to expedite troubleshooting.</span></span>
    * <span data-ttu-id="2cb5b-141">В случае сбоев компонентов оборудования или кластера необходимо отправить запрос на поддержку.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-141">If there are any hardware component or cluster failures, you should log in a Support request.</span></span>

* <span data-ttu-id="2cb5b-142">**Низкий уровень производительности устройства.** Устройство Your StorSimple медленно работает.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-142">**Low device performance** - Your StorSimple device is slow.</span></span>
    * <span data-ttu-id="2cb5b-143">В этом случае выполните командлет с параметром области производительности.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-143">In this case, run this cmdlet with scope parameter set to performance.</span></span> <span data-ttu-id="2cb5b-144">Проанализируйте выходные данные.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-144">Analyze the output.</span></span> <span data-ttu-id="2cb5b-145">Вы получите сведения о задержке при выполнении операций чтения и записи в облаке.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-145">You get the cloud read-write latencies.</span></span> <span data-ttu-id="2cb5b-146">Используйте полученные значения задержки в качестве максимально достижимого целевого показателя, учтите запас на внутреннюю обработку данных и разверните рабочие нагрузки в системе.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-146">Use the reported latencies as maximum achievable target, factor in some overhead for the internal data processing, and then deploy the workloads on the system.</span></span> <span data-ttu-id="2cb5b-147">Дополнительные сведения см. в разделе [Проверка сети](#network-test).</span><span class="sxs-lookup"><span data-stu-id="2cb5b-147">For more information, go to [Use the network test to troubleshoot device performance](#network-test).</span></span>


## <a name="diagnostics-test-and-sample-outputs"></a><span data-ttu-id="2cb5b-148">Диагностическая проверка и пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="2cb5b-148">Diagnostics test and sample outputs</span></span>

### <a name="hardware-test"></a><span data-ttu-id="2cb5b-149">Проверка оборудования</span><span class="sxs-lookup"><span data-stu-id="2cb5b-149">Hardware test</span></span>

<span data-ttu-id="2cb5b-150">В ходе этой проверки определяется состояние компонентов оборудования, встроенного ПО USM и встроенного ПО дисков в системе.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-150">This test determines the status of the hardware components, the USM firmware, and the disk firmware running on your system.</span></span>

* <span data-ttu-id="2cb5b-151">Указываются компоненты оборудования, которые не прошли проверку или которых нет в системе.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-151">The hardware components reported are those components that failed the test or are not present in the system.</span></span>
* <span data-ttu-id="2cb5b-152">Определяются версии встроенного ПО USM и диска для контроллера 0 и 1 и общих компонентов в системе.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-152">The USM firmware and disk firmware versions are reported for the Controller 0, Controller 1, and shared components in your system.</span></span> <span data-ttu-id="2cb5b-153">Полный список компонентов оборудования см. в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="2cb5b-153">For a complete list of hardware components, go to:</span></span>

    * [<span data-ttu-id="2cb5b-154">Список компонентов для основного корпуса устройства StorSimple</span><span class="sxs-lookup"><span data-stu-id="2cb5b-154">Components in primary enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [<span data-ttu-id="2cb5b-155">Список компонентов для корпуса EBOD устройства StorSimple</span><span class="sxs-lookup"><span data-stu-id="2cb5b-155">Components in EBOD enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> <span data-ttu-id="2cb5b-156">Если в ходе проверки оборудования обнаружены неисправные компоненты, [отправьте запрос на поддержку Майкрософт](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="2cb5b-156">If the hardware test reports failed components, [log in a service request with Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a><span data-ttu-id="2cb5b-157">Пример выходных данных проверки оборудования устройства серии 8100</span><span class="sxs-lookup"><span data-stu-id="2cb5b-157">Sample output of hardware test run on an 8100 device</span></span>

<span data-ttu-id="2cb5b-158">Ниже приведен пример выходных данных устройства StorSimple 8100.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-158">Here is a sample output from a StorSimple 8100 device.</span></span> <span data-ttu-id="2cb5b-159">В модели устройства серии 8100 корпус EBOD не используется.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-159">In the 8100 model device, the EBOD enclosure is not present.</span></span> <span data-ttu-id="2cb5b-160">Следовательно, компоненты контроллера EBOD не указываются.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-160">Hence, the EBOD controller components are not reported.</span></span>

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

### <a name="system-test"></a><span data-ttu-id="2cb5b-161">Системная проверка</span><span class="sxs-lookup"><span data-stu-id="2cb5b-161">System test</span></span>

<span data-ttu-id="2cb5b-162">В ходе этой проверки предоставляются сведения о системе, доступных обновлениях, о кластере и служебные данные об устройстве.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-162">This test reports the system information, the updates available, the cluster information, and the service information for your device.</span></span>

* <span data-ttu-id="2cb5b-163">Сведения о системе включают модель, серийный номер устройства, часовой пояс, состояние контроллера и точную версию программного обеспечения, работающего в системе.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-163">The system information includes the model, device serial number, time zone, controller status, and the detailed software version running on the system.</span></span> <span data-ttu-id="2cb5b-164">Объяснение различных параметров системы, выводимых в качестве выходных данных, представлено в разделе [Интерпретация системных сведений](#appendix-interpreting-system-information).</span><span class="sxs-lookup"><span data-stu-id="2cb5b-164">To understand the various system parameters reported as the output, go to [Interpreting system information](#appendix-interpreting-system-information).</span></span>

* <span data-ttu-id="2cb5b-165">Из сведений о доступности обновлений можно узнать, доступен ли режим стандартного обновления и обновления для обслуживания, а также имена связанных пакетов.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-165">The update availability reports whether the regular and maintenance modes are available and their associated package names.</span></span> <span data-ttu-id="2cb5b-166">Если параметры `RegularUpdates` и `MaintenanceModeUpdates` имеют значение `false`, это означает, что обновления недоступны.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-166">If `RegularUpdates` and `MaintenanceModeUpdates` are `false`, this indicates that the updates are not available.</span></span> <span data-ttu-id="2cb5b-167">Устройство находится в актуальном состоянии.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-167">Your device is up-to-date.</span></span>
* <span data-ttu-id="2cb5b-168">Сведения о кластере содержат данные о различных логических компонентах всех групп кластеров HCS и их соответствующих состояниях.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-168">The cluster information contains the information on various logical components of all the HCS cluster groups and their respective statuses.</span></span> <span data-ttu-id="2cb5b-169">Если в этой части отчета указана группа кластеров в автономном состоянии, [обратитесь в службу поддержки Майкрософт](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="2cb5b-169">If you see an offline cluster group in this section of the report, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="2cb5b-170">Сведения о службе включают имена и состояния всех служб HCS и CIS, работающих на устройстве.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-170">The service information includes the names and statuses of all the HCS and CiS services running on your device.</span></span> <span data-ttu-id="2cb5b-171">Они полезны для службы поддержки Майкрософт при устранении неполадок устройства.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-171">This information is helpful for the Microsoft Support in troubleshooting the device issue.</span></span>

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a><span data-ttu-id="2cb5b-172">Пример выходных данных системной проверки устройства серии 8100</span><span class="sxs-lookup"><span data-stu-id="2cb5b-172">Sample output of system test run on an 8100 device</span></span>

<span data-ttu-id="2cb5b-173">Ниже представлен пример выходных данных системной проверки устройства серии 8100.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-173">Here is a sample output of the system test run on an 8100 device.</span></span>

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

### <a name="network-test"></a><span data-ttu-id="2cb5b-174">Проверка сети</span><span class="sxs-lookup"><span data-stu-id="2cb5b-174">Network test</span></span>

<span data-ttu-id="2cb5b-175">В ходе этой проверки определяются состояние сетевых интерфейсов, порты, возможность подключения к DNS- и NTP-серверам, SSL-сертификаты, учетные данные учетных записей хранения, возможность подключения к серверам обновления и к веб-прокси на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-175">This test validates the status of the network interfaces, ports, DNS and NTP server connectivity, SSL certificate, storage account credentials, connectivity to the Update servers, and web proxy connectivity on your StorSimple device.</span></span>

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a><span data-ttu-id="2cb5b-176">Пример выходных данных проверки сети при включении только DATA0</span><span class="sxs-lookup"><span data-stu-id="2cb5b-176">Sample output of network test when only DATA0 is enabled</span></span>

<span data-ttu-id="2cb5b-177">Ниже приведен пример выходных данных устройства серии 8100,</span><span class="sxs-lookup"><span data-stu-id="2cb5b-177">Here is a sample output of the 8100 device.</span></span> <span data-ttu-id="2cb5b-178">по которому можно определить следующее:</span><span class="sxs-lookup"><span data-stu-id="2cb5b-178">You can see in the output that:</span></span>
* <span data-ttu-id="2cb5b-179">Включены и настроены только сетевые интерфейсы DATA0 и DATA1.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-179">Only DATA 0 and DATA 1 network interfaces are enabled and configured.</span></span>
* <span data-ttu-id="2cb5b-180">Сетевые интерфейсы DATA2–5 не включены на портале.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-180">DATA 2 - 5 are not enabled in the portal.</span></span>
* <span data-ttu-id="2cb5b-181">Конфигурация DNS-сервера допустимая, и устройство может подключаться через DNS-сервер.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-181">The DNS server configuration is valid and the device can connect via the DNS server.</span></span>
* <span data-ttu-id="2cb5b-182">Вы также можете подключиться через NTP-сервер.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-182">The NTP server connectivity is also fine.</span></span>
* <span data-ttu-id="2cb5b-183">Открыты порты 80 и 443.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-183">Ports 80 and 443 are open.</span></span> <span data-ttu-id="2cb5b-184">Тем не менее порт 9354 заблокирован.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-184">However, port 9354 is blocked.</span></span> <span data-ttu-id="2cb5b-185">В соответствии с [требованиями системы к сети](storsimple-system-requirements.md) необходимо открыть этот порт для взаимодействия служебной шины.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-185">Based on the [system network requirements](storsimple-system-requirements.md), you need to open this port for the service bus communication.</span></span>
* <span data-ttu-id="2cb5b-186">SSL-сертификат является допустимым.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-186">The SSL certification is valid.</span></span>
* <span data-ttu-id="2cb5b-187">Устройство может подключиться к учетной записи хранения _myss8000storageacct_.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-187">The device can connect to the storage account: _myss8000storageacct_.</span></span>
* <span data-ttu-id="2cb5b-188">Вы можете подключиться к серверам обновления.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-188">The connectivity to Update servers is valid.</span></span>
* <span data-ttu-id="2cb5b-189">Веб-прокси не настроен на этом устройстве.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-189">The web proxy is not configured on this device.</span></span>

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a><span data-ttu-id="2cb5b-190">Пример выходных данных проверки сети при включении DATA0 и DATA1</span><span class="sxs-lookup"><span data-stu-id="2cb5b-190">Sample output of network test when DATA0 and DATA1 are enabled</span></span>

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

### <a name="performance-test"></a><span data-ttu-id="2cb5b-191">тест производительности;</span><span class="sxs-lookup"><span data-stu-id="2cb5b-191">Performance test</span></span>

<span data-ttu-id="2cb5b-192">В ходе этой проверки определяется производительность облака по значениям задержки операций чтения и записи в облаке для устройства.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-192">This test reports the cloud performance via the cloud read-write latencies for your device.</span></span> <span data-ttu-id="2cb5b-193">С помощью этого средства можно задать базовые показатели производительности облака, которых можно достичь на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-193">This tool can be used to establish a baseline of the cloud performance that you can achieve with StorSimple.</span></span> <span data-ttu-id="2cb5b-194">Средство указывает максимальную производительность (самые низкие показатели задержки операций чтения и записи), которую можно получить для подключения.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-194">The tool reports the maximum performance (best case scenario for read-write latencies) that you can get for your connection.</span></span>

<span data-ttu-id="2cb5b-195">Так как средство сообщает о максимально возможной достижимой производительности, полученные значения задержки операций чтения и записи можно использовать в качестве целевых при развертывании рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-195">As the tool reports the maximum achievable performance, we can use the reported read-write latencies as targets when deploying the workloads.</span></span>

<span data-ttu-id="2cb5b-196">В ходе теста моделируются размеры больших двоичных объектов, связанные с разными типами томов на устройстве.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-196">The test simulates the blob sizes associated with the different volume types on the device.</span></span> <span data-ttu-id="2cb5b-197">Обычные многоуровневые тома и их резервные копии, закрепленные локально, используют большие двоичные объекты на 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-197">Regular tiered and backups of locally pinned volumes use a 64 KB blob size.</span></span> <span data-ttu-id="2cb5b-198">Многоуровневые тома с архивацией используют большие двоичные объекты объемом 512 КБ.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-198">Tiered volumes with archive option checked use 512 KB blob data size.</span></span> <span data-ttu-id="2cb5b-199">Если на устройстве настроены многоуровневые и локально закрепленные тома, выполняется проверка для больших двоичных объектов на 64 КБ.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-199">If your device has tiered and locally pinned volumes configured, only the test corresponding to 64 KB blob data size is run.</span></span>

<span data-ttu-id="2cb5b-200">Чтобы воспользоваться средством, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="2cb5b-200">To use this tool, perform the following steps:</span></span>

1.  <span data-ttu-id="2cb5b-201">Сначала создайте сочетание многоуровневых томов и многоуровневых томов с архивацией.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-201">First, create a mix of tiered volumes and tiered volumes with archived option checked.</span></span> <span data-ttu-id="2cb5b-202">Таким образом, средство выполнит тесты для больших двоичных объектов на 64 КБ и 512 КБ.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-202">This action ensures that the tool runs the tests for both 64 KB and 512 KB blob sizes.</span></span>

2. <span data-ttu-id="2cb5b-203">Создав и настроив тома, выполните командлет.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-203">Run the cmdlet after you have created and configured the volumes.</span></span> <span data-ttu-id="2cb5b-204">Введите:</span><span class="sxs-lookup"><span data-stu-id="2cb5b-204">Type:</span></span>

    `Invoke-HcsDiagnostics -Scope Performance`

3. <span data-ttu-id="2cb5b-205">Запишите значения задержек операций чтения и записи, указанных средством.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-205">Make a note of the read-write latencies reported by the tool.</span></span> <span data-ttu-id="2cb5b-206">Результаты проверки будут получены через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-206">This test can take several minutes to run before it reports the results.</span></span>

4. <span data-ttu-id="2cb5b-207">Если значения задержки подключения, сообщаемые средством, находятся в пределах ожидаемого диапазона значений, их можно использовать в качестве максимально достижимых целевых значений при развертывании рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-207">If the connection latencies are all under the expected range, then the latencies reported by the tool can be used as maximum achievable target when deploying the workloads.</span></span> <span data-ttu-id="2cb5b-208">Учитывайте некоторый запас на внутреннюю обработку данных.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-208">Factor in some overhead for internal data processing.</span></span>

    <span data-ttu-id="2cb5b-209">Если средство диагностики указало высокую задержку операций чтения и записи, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="2cb5b-209">If the read-write latencies reported by the diagnostics tool are high:</span></span>

    1. <span data-ttu-id="2cb5b-210">Настройте аналитику хранилища для служб BLOB-объектов и проанализируйте выходные данные, чтобы определить задержки для учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-210">Configure Storage Analytics for blob services and analyze the output to understand the latencies for the Azure storage account.</span></span> <span data-ttu-id="2cb5b-211">Подробные инструкции см. в статье [Включение метрик хранилища и просмотр данных метрик](../storage/common/storage-enable-and-view-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="2cb5b-211">For detailed instructions, go to [enable and configure Storage Analytics](../storage/common/storage-enable-and-view-metrics.md).</span></span> <span data-ttu-id="2cb5b-212">Если эти значения задержки так же высоки, как и значения, полученные от средства диагностики StorSimple, необходимо отправить запрос на поддержку в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-212">If those latencies are also high and comparable to the numbers you received from the StorSimple Diagnostics tool, then you need to log a service request with Azure storage.</span></span>

    2. <span data-ttu-id="2cb5b-213">Если значения задержки в учетной записи хранения низкие, обратитесь к администратору сети, чтобы изучить любые проблемы с задержкой в сети.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-213">If the storage account latencies are low, contact your network administrator to investigate any latency issues in your network.</span></span>

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a><span data-ttu-id="2cb5b-214">Пример выходных данных проверки производительности устройства серии 8100</span><span class="sxs-lookup"><span data-stu-id="2cb5b-214">Sample output of performance test run on an 8100 device</span></span>

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

## <a name="appendix-interpreting-system-information"></a><span data-ttu-id="2cb5b-215">Приложение: интерпретация системных сведений</span><span class="sxs-lookup"><span data-stu-id="2cb5b-215">Appendix: interpreting system information</span></span>

<span data-ttu-id="2cb5b-216">Ниже представлена таблица со сведениями о сопоставлении различных параметров Windows PowerShell в сведениях о системе.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-216">Here is a table describing what the various Windows PowerShell parameters in the system information map to.</span></span> 

| <span data-ttu-id="2cb5b-217">Параметр PowerShell</span><span class="sxs-lookup"><span data-stu-id="2cb5b-217">PowerShell Parameter</span></span>    | <span data-ttu-id="2cb5b-218">Описание</span><span class="sxs-lookup"><span data-stu-id="2cb5b-218">Description</span></span>  |
|-------------------------|------------------|
| <span data-ttu-id="2cb5b-219">Идентификатор экземпляра</span><span class="sxs-lookup"><span data-stu-id="2cb5b-219">Instance ID</span></span>             | <span data-ttu-id="2cb5b-220">С каждым контроллером связан уникальный идентификатор или GUID.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-220">Every controller has a unique identifier or a GUID associated with it.</span></span>|
| <span data-ttu-id="2cb5b-221">Имя</span><span class="sxs-lookup"><span data-stu-id="2cb5b-221">Name</span></span>                    | <span data-ttu-id="2cb5b-222">Понятное имя устройства, настроенное на портале Azure во время развертывания устройства.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-222">The friendly name of the device as configured through the Azure portal during device deployment.</span></span> <span data-ttu-id="2cb5b-223">В качестве понятного имени по умолчанию используется серийный номер устройства.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-223">The default friendly name is the device serial number.</span></span> |
| <span data-ttu-id="2cb5b-224">Модель</span><span class="sxs-lookup"><span data-stu-id="2cb5b-224">Model</span></span>                   | <span data-ttu-id="2cb5b-225">Модель устройства StorSimple серии 8000</span><span class="sxs-lookup"><span data-stu-id="2cb5b-225">The model of your StorSimple 8000 series device.</span></span> <span data-ttu-id="2cb5b-226">(8100 или 8600).</span><span class="sxs-lookup"><span data-stu-id="2cb5b-226">The model can be 8100 or 8600.</span></span>|
| <span data-ttu-id="2cb5b-227">SerialNumber</span><span class="sxs-lookup"><span data-stu-id="2cb5b-227">SerialNumber</span></span>            | <span data-ttu-id="2cb5b-228">Серийный номер устройства назначается на заводе и состоит из 15 знаков.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-228">The device serial number is assigned at the factory and is 15 characters long.</span></span> <span data-ttu-id="2cb5b-229">Например, 8600-SHX0991003G44HT:</span><span class="sxs-lookup"><span data-stu-id="2cb5b-229">For instance, 8600-SHX0991003G44HT indicates:</span></span><br> <span data-ttu-id="2cb5b-230">8600 — это модель устройства;</span><span class="sxs-lookup"><span data-stu-id="2cb5b-230">8600 – Is the device model.</span></span><br><span data-ttu-id="2cb5b-231">SHX — это регион производства;</span><span class="sxs-lookup"><span data-stu-id="2cb5b-231">SHX – Is the manufacturing site.</span></span><br> <span data-ttu-id="2cb5b-232">0991003 — определенный продукт;</span><span class="sxs-lookup"><span data-stu-id="2cb5b-232">0991003 - Is a specific product.</span></span> <br> <span data-ttu-id="2cb5b-233">G44HT — последние 5 цифр увеличиваются для получения уникального серийного номера.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-233">G44HT- the last 5 digits are incremented to create unique serial numbers.</span></span> <span data-ttu-id="2cb5b-234">Набор может быть неупорядоченным.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-234">This may not be a sequential set.</span></span>|
| <span data-ttu-id="2cb5b-235">TimeZone</span><span class="sxs-lookup"><span data-stu-id="2cb5b-235">TimeZone</span></span>                | <span data-ttu-id="2cb5b-236">Часовой пояс устройства, настроенный на портале Azure во время развертывания устройства.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-236">The device time zone as configured in the Azure portal during device deployment.</span></span>|
| <span data-ttu-id="2cb5b-237">CurrentController</span><span class="sxs-lookup"><span data-stu-id="2cb5b-237">CurrentController</span></span>       | <span data-ttu-id="2cb5b-238">Контроллер, к которому подключена система через интерфейс Windows PowerShell устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-238">The controller that you are connected to through the Windows PowerShell interface of your StorSimple device.</span></span>|
| <span data-ttu-id="2cb5b-239">ActiveController</span><span class="sxs-lookup"><span data-stu-id="2cb5b-239">ActiveController</span></span>        | <span data-ttu-id="2cb5b-240">Активный контроллер на устройстве, управляющий всеми сетевыми и дисковыми операциями.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-240">The controller that is active on your device and is controlling all the network and disk operations.</span></span> <span data-ttu-id="2cb5b-241">Это может быть контроллер 0 или 1.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-241">This can be Controller 0 or Controller 1.</span></span>  |
| <span data-ttu-id="2cb5b-242">Controller0Status</span><span class="sxs-lookup"><span data-stu-id="2cb5b-242">Controller0Status</span></span>       | <span data-ttu-id="2cb5b-243">Состояние контроллера 0 на устройстве</span><span class="sxs-lookup"><span data-stu-id="2cb5b-243">The status of Controller 0 on your device.</span></span> <span data-ttu-id="2cb5b-244">("Обычное", "В режиме восстановления" или "Недоступно").</span><span class="sxs-lookup"><span data-stu-id="2cb5b-244">The controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="2cb5b-245">Controller1Status</span><span class="sxs-lookup"><span data-stu-id="2cb5b-245">Controller1Status</span></span>       | <span data-ttu-id="2cb5b-246">Состояние контроллера 1 на устройстве</span><span class="sxs-lookup"><span data-stu-id="2cb5b-246">The status of Controller 1 on your device.</span></span>  <span data-ttu-id="2cb5b-247">("Обычное", "В режиме восстановления" или "Недоступно").</span><span class="sxs-lookup"><span data-stu-id="2cb5b-247">The controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="2cb5b-248">SystemMode</span><span class="sxs-lookup"><span data-stu-id="2cb5b-248">SystemMode</span></span>              | <span data-ttu-id="2cb5b-249">Общее состояние устройства StorSimple</span><span class="sxs-lookup"><span data-stu-id="2cb5b-249">The overall status of your StorSimple device.</span></span> <span data-ttu-id="2cb5b-250">("Обычное", "Обслуживание" или "Списан") (соответствует отключению на портале Azure).</span><span class="sxs-lookup"><span data-stu-id="2cb5b-250">The device status can be normal, maintenance, or decommissioned (corresponds to deactivated in the Azure portal).</span></span>|
| <span data-ttu-id="2cb5b-251">FriendlySoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="2cb5b-251">FriendlySoftwareVersion</span></span> | <span data-ttu-id="2cb5b-252">Понятная строка, соответствующая версии программного обеспечения устройства.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-252">The friendly string that corresponds to the device software version.</span></span> <span data-ttu-id="2cb5b-253">Для системы с обновлением 4 будет использоваться понятная версия программного обеспечения StorSimple серии 8000 с обновлением 4.0.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-253">For a system running Update 4, the friendly software version would be StorSimple 8000 Series Update 4.0.</span></span>|
| <span data-ttu-id="2cb5b-254">HcsSoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="2cb5b-254">HcsSoftwareVersion</span></span>      | <span data-ttu-id="2cb5b-255">Версия программного обеспечения HCS, работающего на устройстве.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-255">The HCS software version running on your device.</span></span> <span data-ttu-id="2cb5b-256">Например, устройству StorSimple серии 8000 с обновлением 4.0 соответствует версия программного обеспечения HCS 6.3.9600.17820.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-256">For instance, the HCS software version corresponding to StorSimple 8000 Series Update 4.0 is 6.3.9600.17820.</span></span> |
| <span data-ttu-id="2cb5b-257">ApiVersion</span><span class="sxs-lookup"><span data-stu-id="2cb5b-257">ApiVersion</span></span>              | <span data-ttu-id="2cb5b-258">Версия программного обеспечения API Windows PowerShell устройства HCS.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-258">The software version of the Windows PowerShell API of the HCS device.</span></span>|
| <span data-ttu-id="2cb5b-259">VhdVersion</span><span class="sxs-lookup"><span data-stu-id="2cb5b-259">VhdVersion</span></span>              | <span data-ttu-id="2cb5b-260">Версия программного обеспечения заводского образа, поставляемого с устройством.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-260">The software version of the factory image that the device was shipped with.</span></span> <span data-ttu-id="2cb5b-261">При сбросе устройства к заводским настройкам оно запустится с этой версией программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-261">If you reset your device to factory defaults, then it runs this software version.</span></span>|
| <span data-ttu-id="2cb5b-262">OSVersion</span><span class="sxs-lookup"><span data-stu-id="2cb5b-262">OSVersion</span></span>               | <span data-ttu-id="2cb5b-263">Версия программного обеспечения операционной системы Windows Server, запущенной на устройстве.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-263">The software version of the Windows Server operating system running on the device.</span></span> <span data-ttu-id="2cb5b-264">Устройство StorSimple работает на базе Windows Server 2012 R2, что соответствует версии 6.3.9600.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-264">The StorSimple device is based off the Windows Server 2012 R2 that corresponds to 6.3.9600.</span></span>|
| <span data-ttu-id="2cb5b-265">CisAgentVersion</span><span class="sxs-lookup"><span data-stu-id="2cb5b-265">CisAgentVersion</span></span>         | <span data-ttu-id="2cb5b-266">Версия агента CIS, запущенного на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-266">The version for your Cis agent running on your StorSimple device.</span></span> <span data-ttu-id="2cb5b-267">Этот агент позволяет взаимодействовать со службой диспетчера StorSimple, запущенной в Azure.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-267">This agent helps communicate with the StorSimple Manager service running in Azure.</span></span>|
| <span data-ttu-id="2cb5b-268">MdsAgentVersion</span><span class="sxs-lookup"><span data-stu-id="2cb5b-268">MdsAgentVersion</span></span>         | <span data-ttu-id="2cb5b-269">Версия агента MDS, запущенного на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-269">The version corresponding to the Mds agent running on your StorSimple device.</span></span> <span data-ttu-id="2cb5b-270">Этот агент перемещает данные в службу MDS.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-270">This agent moves data to the Monitoring and Diagnostics Service (MDS).</span></span>|
| <span data-ttu-id="2cb5b-271">Lsisas2Version</span><span class="sxs-lookup"><span data-stu-id="2cb5b-271">Lsisas2Version</span></span>          | <span data-ttu-id="2cb5b-272">Версия драйверов LSI на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-272">The version corresponding to the LSI drivers on your StorSimple device.</span></span>|
| <span data-ttu-id="2cb5b-273">Емкость</span><span class="sxs-lookup"><span data-stu-id="2cb5b-273">Capacity</span></span>                | <span data-ttu-id="2cb5b-274">Общая емкость устройства в байтах.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-274">The total capacity of the device in bytes.</span></span>|
| <span data-ttu-id="2cb5b-275">RemoteManagementMode</span><span class="sxs-lookup"><span data-stu-id="2cb5b-275">RemoteManagementMode</span></span>    | <span data-ttu-id="2cb5b-276">Указывает на то, можно ли управлять устройством удаленно через интерфейс Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-276">Indicates whether the device can be remotely managed via its Windows PowerShell interface.</span></span> |
| <span data-ttu-id="2cb5b-277">FipsMode</span><span class="sxs-lookup"><span data-stu-id="2cb5b-277">FipsMode</span></span>                | <span data-ttu-id="2cb5b-278">Указывает, включен ли на устройстве режим FIPS (федеральный стандарт обработки информации США).</span><span class="sxs-lookup"><span data-stu-id="2cb5b-278">Indicates whether the United States Federal Information Processing Standard (FIPS) mode is enabled on your device.</span></span> <span data-ttu-id="2cb5b-279">Стандарт FIPS 140 определяет криптографические алгоритмы, утвержденные для использования в компьютерных системах федеральной власти США для защиты конфиденциальных данных.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-279">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span></span> <span data-ttu-id="2cb5b-280">Для устройств с обновлением версии 4 или более поздней режим FIPS включен по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-280">For devices running Update 4 or later, FIPS mode is enabled by default.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2cb5b-281">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2cb5b-281">Next steps</span></span>

* <span data-ttu-id="2cb5b-282">Узнайте о [синтаксисе командлета Invoke-HcsDiagnostics](https://technet.microsoft.com/library/mt795371.aspx).</span><span class="sxs-lookup"><span data-stu-id="2cb5b-282">Learn the [syntax of the Invoke-HcsDiagnostics cmdlet](https://technet.microsoft.com/library/mt795371.aspx).</span></span>

* <span data-ttu-id="2cb5b-283">Дополнительные сведения об [устранении неполадок развертывания](storsimple-troubleshoot-deployment.md) на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2cb5b-283">Learn more about how to [troubleshoot deployment issues](storsimple-troubleshoot-deployment.md) on your StorSimple device.</span></span>
