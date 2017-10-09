---
title: "aaaConfigure MPIO на узле StorSimple Linux | Документы Microsoft"
description: "Настройка MPIO на узел Linux tooa StorSimple подключен, под управлением CentOS 6.6"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: tysonn
ms.assetid: ca289eed-12b7-4e2e-9117-adf7e2034f2f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: alkohli
ms.openlocfilehash: d9f7e02903243494c909313fb2c33ac690764274
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a><span data-ttu-id="bad96-103">Настройка MPIO на узле StorSimple под управлением CentOS</span><span class="sxs-lookup"><span data-stu-id="bad96-103">Configure MPIO on a StorSimple host running CentOS</span></span>
<span data-ttu-id="bad96-104">В этой статье объясняется tooconfigure необходимые шаги hello несколько каналов ввода-ВЫВОДА (MPIO) на сервере узла Centos 6.6.</span><span class="sxs-lookup"><span data-stu-id="bad96-104">This article explains hello steps required tooconfigure Multipathing IO (MPIO) on your Centos 6.6 host server.</span></span> <span data-ttu-id="bad96-105">сервер узла Hello-подключенных tooyour устройство Microsoft Azure StorSimple для обеспечения высокой доступности через инициаторы iSCSI.</span><span class="sxs-lookup"><span data-stu-id="bad96-105">hello host server is connected tooyour Microsoft Azure StorSimple device for high availability via iSCSI initiators.</span></span> <span data-ttu-id="bad96-106">Описывает в автоматическое обнаружение сведений hello многоканального устройств и hello определенные настройки только для томов StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bad96-106">It describes in detail hello automatic discovery of multipath devices and hello specific setup only for StorSimple volumes.</span></span>

<span data-ttu-id="bad96-107">Эта процедура является моделей hello применимо tooall устройств серии StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="bad96-107">This procedure is applicable tooall hello models of StorSimple 8000 series devices.</span></span>

> [!NOTE]
> <span data-ttu-id="bad96-108">Эта процедура не подходит для виртуального устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bad96-108">This procedure cannot be used for a StorSimple virtual device.</span></span> <span data-ttu-id="bad96-109">Дополнительные сведения см. в разделе как tooconfigure размещения серверов для виртуального устройства.</span><span class="sxs-lookup"><span data-stu-id="bad96-109">For more information, see how tooconfigure host servers for your virtual device.</span></span>
> 
> 

## <a name="about-multipathing"></a><span data-ttu-id="bad96-110">Основные сведения о многоканальном вводе-выводе</span><span class="sxs-lookup"><span data-stu-id="bad96-110">About multipathing</span></span>
<span data-ttu-id="bad96-111">Hello несколько каналов позволяет tooconfigure несколько путей ввода-вывода между сервером узла и устройством хранения.</span><span class="sxs-lookup"><span data-stu-id="bad96-111">hello multipathing feature allows you tooconfigure multiple I/O paths between a host server and a storage device.</span></span> <span data-ttu-id="bad96-112">Эти каналы ввода-вывода являются физическими соединениями SAN, которые могут включать отдельные кабели, коммутаторы, сетевые интерфейсы и контроллеры.</span><span class="sxs-lookup"><span data-stu-id="bad96-112">These I/O paths are physical SAN connections that can include separate cables, switches, network interfaces, and controllers.</span></span> <span data-ttu-id="bad96-113">Несколько каналов объединяет пути ввода-вывода hello, tooconfigure новое устройство, связанный со всеми hello суммарный путей.</span><span class="sxs-lookup"><span data-stu-id="bad96-113">Multipathing aggregates hello I/O paths, tooconfigure a new device that is associated with all of hello aggregated paths.</span></span>

<span data-ttu-id="bad96-114">Hello несколько каналов предназначен двойную:</span><span class="sxs-lookup"><span data-stu-id="bad96-114">hello purpose of multipathing is two-fold:</span></span>

* <span data-ttu-id="bad96-115">**Высокий уровень доступности**: предоставляет альтернативный путь, если происходит сбой какой-либо элемент путь hello ввода-вывода (например, кабель, коммутатор, сетевого интерфейса или контроллера).</span><span class="sxs-lookup"><span data-stu-id="bad96-115">**High availability**: It provides an alternate path if any element of hello I/O path (such as a cable, switch, network interface, or controller) fails.</span></span>
* <span data-ttu-id="bad96-116">**Балансировка нагрузки**: в зависимости от конфигурации hello устройство хранения, он может повысить производительность hello, обнаруживая нагрузках на пути ввода-вывода hello и динамически перераспределения этих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="bad96-116">**Load balancing**: Depending on hello configuration of your storage device, it can improve hello performance by detecting loads on hello I/O paths and dynamically rebalancing those loads.</span></span>

### <a name="about-multipathing-components"></a><span data-ttu-id="bad96-117">Компоненты решения для многоканального ввода-вывода</span><span class="sxs-lookup"><span data-stu-id="bad96-117">About multipathing components</span></span>
<span data-ttu-id="bad96-118">Решение для многоканального ввода-вывода в ОС Linux состоит из компонентов ядра и компонентов пространства пользователя.</span><span class="sxs-lookup"><span data-stu-id="bad96-118">Multipathing in Linux consists of kernel components and user-space components as tabulated below.</span></span>

* <span data-ttu-id="bad96-119">**Ядра**: hello является основным компонентом hello *сопоставления устройств* , изменение пути ввода-вывода и поддерживает отработку отказа для пути и пути групп.</span><span class="sxs-lookup"><span data-stu-id="bad96-119">**Kernel**: hello main component is hello *device-mapper* that reroutes I/O and supports failover for paths and path groups.</span></span>

* <span data-ttu-id="bad96-120">**Пространство пользователя**: это *multipath средства* , управляющие многопутевых устройств, предписывая многоканального модуля сопоставления устройств hello какие toodo.</span><span class="sxs-lookup"><span data-stu-id="bad96-120">**User-space**: These are *multipath-tools* that manage multipathed devices by instructing hello device-mapper multipath module what toodo.</span></span> <span data-ttu-id="bad96-121">Hello средства включают:</span><span class="sxs-lookup"><span data-stu-id="bad96-121">hello tools consist of:</span></span>
   
   * <span data-ttu-id="bad96-122">**Multipath**. Отображает многоканальные устройства и настраивает их.</span><span class="sxs-lookup"><span data-stu-id="bad96-122">**Multipath**: lists and configures multipathed devices.</span></span>
   * <span data-ttu-id="bad96-123">**Multipathd**: управляющая программа, выполняющая пути hello multipath и мониторов.</span><span class="sxs-lookup"><span data-stu-id="bad96-123">**Multipathd**: daemon that executes multipath and monitors hello paths.</span></span>
   * <span data-ttu-id="bad96-124">**Имя Devmap**: обеспечивает devmaps значимые tooudev имя устройства.</span><span class="sxs-lookup"><span data-stu-id="bad96-124">**Devmap-name**: provides a meaningful device-name tooudev for devmaps.</span></span>
   * <span data-ttu-id="bad96-125">**Kpartx**: сопоставляет линейной devmaps toodevice секций toomake многоканального схемы секционирования.</span><span class="sxs-lookup"><span data-stu-id="bad96-125">**Kpartx**: maps linear devmaps toodevice partitions toomake multipath maps partitionable.</span></span>
   * <span data-ttu-id="bad96-126">**Multipath.conf**: файл конфигурации для многоканального управляющей программы, используемые toooverwrite hello встроенной конфигурации таблицы.</span><span class="sxs-lookup"><span data-stu-id="bad96-126">**Multipath.conf**: configuration file for multipath daemon that is used toooverwrite hello built-in configuration table.</span></span>

### <a name="about-hello-multipathconf-configuration-file"></a><span data-ttu-id="bad96-127">О файле конфигурации multipath.conf hello</span><span class="sxs-lookup"><span data-stu-id="bad96-127">About hello multipath.conf configuration file</span></span>
<span data-ttu-id="bad96-128">файл конфигурации Hello `/etc/multipath.conf` вносит много hello функции несколько каналов настраивается пользователем.</span><span class="sxs-lookup"><span data-stu-id="bad96-128">hello configuration file `/etc/multipath.conf` makes many of hello multipathing features user-configurable.</span></span> <span data-ttu-id="bad96-129">Hello `multipath` команда и hello управляющая программа ядра `multipathd` используйте сведения из этого файла.</span><span class="sxs-lookup"><span data-stu-id="bad96-129">hello `multipath` command and hello kernel daemon `multipathd` use information found in this file.</span></span> <span data-ttu-id="bad96-130">Hello файл был запрошен только во время настройки hello hello многоканального устройств.</span><span class="sxs-lookup"><span data-stu-id="bad96-130">hello file is consulted only during hello configuration of hello multipath devices.</span></span> <span data-ttu-id="bad96-131">Убедитесь, что все изменения были сделаны перед запуском hello `multipath` команды.</span><span class="sxs-lookup"><span data-stu-id="bad96-131">Make sure that all changes are made before you run hello `multipath` command.</span></span> <span data-ttu-id="bad96-132">При изменении файла hello после этого может потребоваться toostop и запустите multipathd снова для эффекта tootake изменения hello.</span><span class="sxs-lookup"><span data-stu-id="bad96-132">If you modify hello file afterwards, you will need toostop and start multipathd again for hello changes tootake effect.</span></span>

<span data-ttu-id="bad96-133">Hello multipath.conf состоит из пяти разделов.</span><span class="sxs-lookup"><span data-stu-id="bad96-133">hello multipath.conf has five sections:</span></span>

- <span data-ttu-id="bad96-134">**Параметры системного уровня, используемые по умолчанию** *(defaults)*. Здесь можно изменять стандартные системные параметры.</span><span class="sxs-lookup"><span data-stu-id="bad96-134">**System level defaults** *(defaults)*: You can override system level defaults.</span></span>
- <span data-ttu-id="bad96-135">**Остальные устройства** *(черный список)*: можно указать hello список устройств, которые не должны контролироваться путем сопоставления устройств.</span><span class="sxs-lookup"><span data-stu-id="bad96-135">**Blacklisted devices** *(blacklist)*: You can specify hello list of devices that should not be controlled by device-mapper.</span></span>
- <span data-ttu-id="bad96-136">**Защитить черным списком исключений** *(blacklist_exceptions)*: можно определить конкретные устройства toobe обрабатывается как многоканального устройства, даже если в черный список hello.</span><span class="sxs-lookup"><span data-stu-id="bad96-136">**Blacklist exceptions** *(blacklist_exceptions)*: You can identify specific devices toobe treated as multipath devices even if listed in hello blacklist.</span></span>
- <span data-ttu-id="bad96-137">**Определенные параметры хранения контроллера** *(устройства)*: можно указать параметры конфигурации, которые будут применяться toodevices у поставщика и продукта сведения.</span><span class="sxs-lookup"><span data-stu-id="bad96-137">**Storage controller specific settings** *(devices)*: You can specify configuration settings that will be applied toodevices that have Vendor and Product information.</span></span>
- <span data-ttu-id="bad96-138">**Определенные параметры устройства** *(multipaths)*: можно использовать параметры конфигурации hello этот раздел toofine настраивать для отдельных логических устройств.</span><span class="sxs-lookup"><span data-stu-id="bad96-138">**Device specific settings** *(multipaths)*: You can use this section toofine-tune hello configuration settings for individual LUNs.</span></span>

## <a name="configure-multipathing-on-storsimple-connected-toolinux-host"></a><span data-ttu-id="bad96-139">Настроить несколько каналов на узле подключенных tooLinux StorSimple</span><span class="sxs-lookup"><span data-stu-id="bad96-139">Configure multipathing on StorSimple connected tooLinux host</span></span>
<span data-ttu-id="bad96-140">Узел Linux tooa подключенное устройство StorSimple можно настроить для обеспечения высокой доступности и балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="bad96-140">A StorSimple device connected tooa Linux host can be configured for high availability and load balancing.</span></span> <span data-ttu-id="bad96-141">Например, если узел Linux hello имеет два интерфейса подключенных toohello устройство SAN и hello имеет два интерфейса подключение toohello SAN Здравствуйте, например, эти интерфейсы являются в одной подсети, а затем будут 4 пути.</span><span class="sxs-lookup"><span data-stu-id="bad96-141">For example, if hello Linux host has two interfaces connected toohello SAN and hello device has two interfaces connected toohello SAN such that these interfaces are on hello same subnet, then there will be 4 paths available.</span></span> <span data-ttu-id="bad96-142">Однако если каждый интерфейс данных в интерфейс устройства и узла hello в другой подсети IP (и не маршрутизируемый), затем только 2 пути будут доступны.</span><span class="sxs-lookup"><span data-stu-id="bad96-142">However, if each DATA interface on hello device and host interface are on a different IP subnet (and not routable), then only 2 paths will be available.</span></span> <span data-ttu-id="bad96-143">Можно настроить несколько каналов tooautomatically обнаружить все доступные пути hello, выберите алгоритм балансировки нагрузки для этих путей, применять определенные настройки для томов только для StorSimple и затем включить и проверить несколько каналов.</span><span class="sxs-lookup"><span data-stu-id="bad96-143">You can configure multipathing tooautomatically discover all hello available paths, choose a load-balancing algorithm for those paths, apply specific configuration settings for StorSimple-only volumes, and then enable and verify multipathing.</span></span>

<span data-ttu-id="bad96-144">Hello следующая процедура описывает способ tooconfigure несколько каналов, когда устройство StorSimple с двумя сетевыми интерфейсами — узел подключенных tooa с двумя сетевыми интерфейсами.</span><span class="sxs-lookup"><span data-stu-id="bad96-144">hello following procedure describes how tooconfigure multipathing when a StorSimple device with two network interfaces is connected tooa host with two network interfaces.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bad96-145">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bad96-145">Prerequisites</span></span>
<span data-ttu-id="bad96-146">В этом разделе описаны предварительные требования hello конфигурации для сервера CentOS и устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bad96-146">This section details hello configuration prerequisites for CentOS server and your StorSimple device.</span></span>

### <a name="on-centos-host"></a><span data-ttu-id="bad96-147">Узел CentOS</span><span class="sxs-lookup"><span data-stu-id="bad96-147">On CentOS host</span></span>
1. <span data-ttu-id="bad96-148">Убедитесь, что у узла CentOS есть два активных сетевых интерфейса.</span><span class="sxs-lookup"><span data-stu-id="bad96-148">Make sure that your CentOS host has 2 network interfaces enabled.</span></span> <span data-ttu-id="bad96-149">Тип:</span><span class="sxs-lookup"><span data-stu-id="bad96-149">Type:</span></span>
   
    `ifconfig`
   
    <span data-ttu-id="bad96-150">Hello примере показан вывод hello при двух сетевых интерфейсов (`eth0` и `eth1`) присутствуют на узле hello.</span><span class="sxs-lookup"><span data-stu-id="bad96-150">hello following example shows hello output when two network interfaces (`eth0` and `eth1`) are present on hello host.</span></span>
   
        [root@centosSS ~]# ifconfig
        eth0  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:41  
          inet addr:10.126.162.65  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3341/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3341/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
         RX packets:36536 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6312 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:13994127 (13.3 MiB)  TX bytes:645654 (630.5 KiB)
   
        eth1  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:42  
          inet addr:10.126.162.66  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3342/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3342/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25962 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:2597350 (2.4 MiB)  TX bytes:754 (754.0 b)
   
        loLink encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:12 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:720 (720.0 b)  TX bytes:720 (720.0 b)
2. <span data-ttu-id="bad96-151">Установите *iSCSI-initiator-utils* на сервер CentOS.</span><span class="sxs-lookup"><span data-stu-id="bad96-151">Install *iSCSI-initiator-utils* on your CentOS server.</span></span> <span data-ttu-id="bad96-152">Выполните следующие шаги tooinstall hello *iSCSI инициатора utils*.</span><span class="sxs-lookup"><span data-stu-id="bad96-152">Perform hello following steps tooinstall *iSCSI-initiator-utils*.</span></span>
   
   1. <span data-ttu-id="bad96-153">Войдите на узел CentOS как `root` .</span><span class="sxs-lookup"><span data-stu-id="bad96-153">Log on as `root` into your CentOS host.</span></span>
   2. <span data-ttu-id="bad96-154">Установка hello *iSCSI инициатора utils*.</span><span class="sxs-lookup"><span data-stu-id="bad96-154">Install hello *iSCSI-initiator-utils*.</span></span> <span data-ttu-id="bad96-155">Тип:</span><span class="sxs-lookup"><span data-stu-id="bad96-155">Type:</span></span>
      
       `yum install iscsi-initiator-utils`
   3. <span data-ttu-id="bad96-156">После hello *iSCSI инициатора utils* успешно установлен, запустить службу iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="bad96-156">After hello *iSCSI-Initiator-utils* is successfully installed, start hello iSCSI service.</span></span> <span data-ttu-id="bad96-157">Тип:</span><span class="sxs-lookup"><span data-stu-id="bad96-157">Type:</span></span>
      
       `service iscsid start`
      
       <span data-ttu-id="bad96-158">В случаях `iscsid` фактически не может начинаться и hello `--force` параметр будет требоваться</span><span class="sxs-lookup"><span data-stu-id="bad96-158">On occasions, `iscsid` may not actually start and hello `--force` option may be needed</span></span>
   4. <span data-ttu-id="bad96-159">Включение вашей инициатор iSCSI во время загрузки, используйте hello tooensure `chkconfig` команды tooenable hello службы.</span><span class="sxs-lookup"><span data-stu-id="bad96-159">tooensure that your iSCSI initiator is enabled during boot time, use hello `chkconfig` command tooenable hello service.</span></span>
      
       `chkconfig iscsi on`
   5. <span data-ttu-id="bad96-160">tooverify, что он был правильно программой установки, выполните команду hello.</span><span class="sxs-lookup"><span data-stu-id="bad96-160">tooverify that that it was properly setup, run hello command:</span></span>
      
       `chkconfig --list | grep iscsi`
      
       <span data-ttu-id="bad96-161">Результат выполнения команды показан ниже.</span><span class="sxs-lookup"><span data-stu-id="bad96-161">A sample output is shown below.</span></span>
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       <span data-ttu-id="bad96-162">Из hello выше примере видно, что среде iSCSI будет запускаться по времени загрузки на выполнения уровня 2, 3, 4 и 5.</span><span class="sxs-lookup"><span data-stu-id="bad96-162">From hello above example, you can see that your iSCSI environment will run on boot time on run levels 2, 3, 4, and 5.</span></span>
3. <span data-ttu-id="bad96-163">Установите *device-mapper-multipath*.</span><span class="sxs-lookup"><span data-stu-id="bad96-163">Install *device-mapper-multipath*.</span></span> <span data-ttu-id="bad96-164">Тип:</span><span class="sxs-lookup"><span data-stu-id="bad96-164">Type:</span></span>
   
    `yum install device-mapper-multipath`
   
    <span data-ttu-id="bad96-165">Hello Установка начнется.</span><span class="sxs-lookup"><span data-stu-id="bad96-165">hello installation will start.</span></span> <span data-ttu-id="bad96-166">Тип **Y** toocontinue запрос на подтверждение.</span><span class="sxs-lookup"><span data-stu-id="bad96-166">Type **Y** toocontinue when prompted for confirmation.</span></span>

### <a name="on-storsimple-device"></a><span data-ttu-id="bad96-167">Устройство StorSimple</span><span class="sxs-lookup"><span data-stu-id="bad96-167">On StorSimple device</span></span>
<span data-ttu-id="bad96-168">Устройство StorSimple должно удовлетворять следующим условиям.</span><span class="sxs-lookup"><span data-stu-id="bad96-168">Your StorSimple device should have:</span></span>

* <span data-ttu-id="bad96-169">Наличие как минимум двух активных интерфейсов для iSCSI.</span><span class="sxs-lookup"><span data-stu-id="bad96-169">A minimum of two interfaces enabled for iSCSI.</span></span> <span data-ttu-id="bad96-170">tooverify, что два интерфейса iSCSI включен на устройстве StorSimple, выполните следующие шаги в классический портал Azure для устройства StorSimple hello hello.</span><span class="sxs-lookup"><span data-stu-id="bad96-170">tooverify that two interfaces are iSCSI-enabled on your StorSimple device, perform hello following steps in hello Azure classic portal for your StorSimple device:</span></span>
  
  1. <span data-ttu-id="bad96-171">Войдите на классический портал hello для устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bad96-171">Log into hello classic portal for your StorSimple device.</span></span>
  2. <span data-ttu-id="bad96-172">Выберите службы диспетчера StorSimple, щелкните **устройств** и выберите hello конкретного устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bad96-172">Select your StorSimple Manager service, click **Devices** and choose hello specific StorSimple device.</span></span> <span data-ttu-id="bad96-173">Нажмите кнопку **Настройка** и проверить параметры сетевого интерфейса hello.</span><span class="sxs-lookup"><span data-stu-id="bad96-173">Click **Configure** and verify hello network interface settings.</span></span> <span data-ttu-id="bad96-174">На снимке экрана ниже показаны два сетевых интерфейса с поддержкой iSCSI.</span><span class="sxs-lookup"><span data-stu-id="bad96-174">A screenshot with two iSCSI-enabled network interfaces is shown below.</span></span> <span data-ttu-id="bad96-175">Здесь оба интерфейса 10 GbE (DATA 2 и DATA 3) поддерживают iSCSI.</span><span class="sxs-lookup"><span data-stu-id="bad96-175">Here DATA 2 and DATA 3, both 10 GbE interfaces are enabled for iSCSI.</span></span>
     
      ![Настройка MPIO на устройстве StorSimple, интерфейс DATA2](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![Настройка MPIO на устройстве StorSimple, интерфейс DATA3](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      <span data-ttu-id="bad96-178">В hello **Настройка** страницы</span><span class="sxs-lookup"><span data-stu-id="bad96-178">In hello **Configure** page</span></span>
     
     1. <span data-ttu-id="bad96-179">Убедитесь, что оба сетевых интерфейса поддерживают iSCSI.</span><span class="sxs-lookup"><span data-stu-id="bad96-179">Ensure that both network interfaces are iSCSI-enabled.</span></span> <span data-ttu-id="bad96-180">Hello **iSCSI включен** должно быть задано слишком**Да**.</span><span class="sxs-lookup"><span data-stu-id="bad96-180">hello **iSCSI enabled** field should be set too**Yes**.</span></span>
     2. <span data-ttu-id="bad96-181">Убедитесь, что сетевые интерфейсы hello hello такой же скоростью, должен иметь 1 GbE или 10 GbE.</span><span class="sxs-lookup"><span data-stu-id="bad96-181">Ensure that hello network interfaces have hello same speed, both should be 1 GbE or 10 GbE.</span></span>
     3. <span data-ttu-id="bad96-182">Обратите внимание, hello IPv4-адреса интерфейсы с включенным iSCSI hello и сохранить для последующего использования на узле hello.</span><span class="sxs-lookup"><span data-stu-id="bad96-182">Note hello IPv4 addresses of hello iSCSI-enabled interfaces and save for later use on hello host.</span></span>
* <span data-ttu-id="bad96-183">Hello iSCSI на устройстве StorSimple должны быть доступен с сервера CentOS hello.</span><span class="sxs-lookup"><span data-stu-id="bad96-183">hello iSCSI interfaces on your StorSimple device should be reachable from hello CentOS server.</span></span>
      <span data-ttu-id="bad96-184">tooverify это, необходимо tooprovide hello IP-адреса интерфейсов StorSimple сеть с поддержкой iSCSI на хост-сервере.</span><span class="sxs-lookup"><span data-stu-id="bad96-184">tooverify this, you need tooprovide hello IP addresses of your StorSimple iSCSI-enabled network interfaces on your host server.</span></span> <span data-ttu-id="bad96-185">Здравствуйте, команды, используемые и соответствующий вывод с DATA2 hello (10.126.162.25) и DATA3 (10.126.162.26) показано ниже:</span><span class="sxs-lookup"><span data-stu-id="bad96-185">hello commands used and hello corresponding output with DATA2 (10.126.162.25) and DATA3 (10.126.162.26) is shown below:</span></span>
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a><span data-ttu-id="bad96-186">Конфигурация оборудования</span><span class="sxs-lookup"><span data-stu-id="bad96-186">Hardware configuration</span></span>
<span data-ttu-id="bad96-187">Корпорация Майкрософт рекомендует подключении hello двух iSCSI сетевых интерфейсов для отдельных ветвей для обеспечения избыточности.</span><span class="sxs-lookup"><span data-stu-id="bad96-187">We recommend that you connect hello two iSCSI network interfaces on separate paths for redundancy.</span></span> <span data-ttu-id="bad96-188">на следующем рисунке Hello показывает hello рекомендуется следующая конфигурация оборудования для обеспечения высокой доступности и балансировки нагрузки несколько каналов для CentOS server и устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bad96-188">hello figure below shows hello recommended hardware configuration for high availability and load-balancing multipathing for your CentOS server and StorSimple device.</span></span>

![Конфигурация оборудования MPIO для StorSimple tooLinux узла](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

<span data-ttu-id="bad96-190">Как показано в предшествующих рисунок hello:</span><span class="sxs-lookup"><span data-stu-id="bad96-190">As shown in hello preceding figure:</span></span>

* <span data-ttu-id="bad96-191">Устройство StorSimple имеет активно-пассивную конфигурацию с двумя контроллерами.</span><span class="sxs-lookup"><span data-stu-id="bad96-191">Your StorSimple device is in an active-passive configuration with two controllers.</span></span>
* <span data-ttu-id="bad96-192">Два переключателя SAN, контроллеры tooyour подключенных устройств.</span><span class="sxs-lookup"><span data-stu-id="bad96-192">Two SAN switches are connected tooyour device controllers.</span></span>
* <span data-ttu-id="bad96-193">На устройстве StorSimple активировано два инициатора iSCSI.</span><span class="sxs-lookup"><span data-stu-id="bad96-193">Two iSCSI initiators are enabled on your StorSimple device.</span></span>
* <span data-ttu-id="bad96-194">На узле CentOS активировано два сетевых интерфейса.</span><span class="sxs-lookup"><span data-stu-id="bad96-194">Two network interfaces are enabled on your CentOS host.</span></span>

<span data-ttu-id="bad96-195">Hello выше конфигурации является 4 отдельные пути между устройством и hello узла, если интерфейсы hello узле и данных доступны для маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="bad96-195">hello above configuration will yield 4 separate paths between your device and hello host if hello host and data interfaces are routable.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="bad96-196">При реализации многоканального ввода-вывода мы рекомендуем не смешивать сетевые интерфейсы 1 GbE и 10 GbE.</span><span class="sxs-lookup"><span data-stu-id="bad96-196">We recommend that you do not mix 1 GbE and 10 GbE network interfaces for multipathing.</span></span> <span data-ttu-id="bad96-197">При использовании двух сетевых интерфейсов оба интерфейса hello должны быть идентичными типа hello.</span><span class="sxs-lookup"><span data-stu-id="bad96-197">When using two network interfaces, both hello interfaces should be hello identical type.</span></span>
> * <span data-ttu-id="bad96-198">На устройстве StorSimple интерфейсы DATA0, DATA1, DATA4 и DATA5 относятся к типу 1 GbE, а DATA2 и DATA3 — к типу 10 GbE.</span><span class="sxs-lookup"><span data-stu-id="bad96-198">On your StorSimple device, DATA0, DATA1, DATA4 and DATA5 are 1 GbE interfaces whereas DATA2 and DATA3 are 10 GbE network interfaces.|</span></span>
> 
> 

## <a name="configuration-steps"></a><span data-ttu-id="bad96-199">Этапы настройки</span><span class="sxs-lookup"><span data-stu-id="bad96-199">Configuration steps</span></span>
<span data-ttu-id="bad96-200">этапы настройки Hello несколько каналов предусматривает настройку hello доступные пути для автоматического обнаружения, указав hello балансировки нагрузки алгоритм toouse, включение несколько каналов и наконец Проверка конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="bad96-200">hello configuration steps for multipathing involve configuring hello available paths for automatic discovery, specifying hello load-balancing algorithm toouse, enabling multipathing and finally verifying hello configuration.</span></span> <span data-ttu-id="bad96-201">Каждое из этих действий подробно рассматривается в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="bad96-201">Each of these steps is discussed in detail in hello following sections.</span></span>

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a><span data-ttu-id="bad96-202">Этап 1. Настройка автоматического обнаружения доступных каналов</span><span class="sxs-lookup"><span data-stu-id="bad96-202">Step 1: Configure multipathing for automatic discovery</span></span>
<span data-ttu-id="bad96-203">устройства multipath поддерживается Hello можно автоматически обнаружить и настроить.</span><span class="sxs-lookup"><span data-stu-id="bad96-203">hello multipath-supported devices can be automatically discovered and configured.</span></span>

1. <span data-ttu-id="bad96-204">Инициализируйте файл `/etc/multipath.conf` .</span><span class="sxs-lookup"><span data-stu-id="bad96-204">Initialize `/etc/multipath.conf` file.</span></span> <span data-ttu-id="bad96-205">Тип:</span><span class="sxs-lookup"><span data-stu-id="bad96-205">Type:</span></span>
   
     `mpathconf --enable`
   
    <span data-ttu-id="bad96-206">Hello выше команда создаст `sample/etc/multipath.conf` файл.</span><span class="sxs-lookup"><span data-stu-id="bad96-206">hello above command will create a `sample/etc/multipath.conf` file.</span></span>
2. <span data-ttu-id="bad96-207">Запустите службу многоканального ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="bad96-207">Start multipath service.</span></span> <span data-ttu-id="bad96-208">Тип:</span><span class="sxs-lookup"><span data-stu-id="bad96-208">Type:</span></span>
   
    `service multipathd start`
   
    <span data-ttu-id="bad96-209">Вы увидите hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="bad96-209">You will see hello following output:</span></span>
   
    `Starting multipathd daemon:`
3. <span data-ttu-id="bad96-210">Включите автоматическое обнаружение каналов ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="bad96-210">Enable automatic discovery of multipaths.</span></span> <span data-ttu-id="bad96-211">Тип:</span><span class="sxs-lookup"><span data-stu-id="bad96-211">Type:</span></span>
   
    `mpathconf --find_multipaths y`
   
    <span data-ttu-id="bad96-212">Это будет изменен раздел значения по умолчанию hello вашей `multipath.conf` как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="bad96-212">This will modify hello defaults section of your `multipath.conf` as shown below:</span></span>
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a><span data-ttu-id="bad96-213">Этап 2. Настройка многоканального ввода-вывода для томов StorSimple</span><span class="sxs-lookup"><span data-stu-id="bad96-213">Step 2: Configure multipathing for StorSimple volumes</span></span>
<span data-ttu-id="bad96-214">По умолчанию все устройства, черный указаны в файле multipath.conf hello и не выполняется.</span><span class="sxs-lookup"><span data-stu-id="bad96-214">By default, all devices are black listed in hello multipath.conf file and will be bypassed.</span></span> <span data-ttu-id="bad96-215">Вам потребуется несколько toocreate черный список исключений tooallow каналов для томов из устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bad96-215">You will need toocreate blacklist exceptions tooallow multipathing for volumes from StorSimple devices.</span></span>

1. <span data-ttu-id="bad96-216">Изменить hello `/etc/mulitpath.conf` файла.</span><span class="sxs-lookup"><span data-stu-id="bad96-216">Edit hello `/etc/mulitpath.conf` file.</span></span> <span data-ttu-id="bad96-217">Тип:</span><span class="sxs-lookup"><span data-stu-id="bad96-217">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="bad96-218">Найдите раздел blacklist_exceptions hello в файле multipath.conf hello.</span><span class="sxs-lookup"><span data-stu-id="bad96-218">Locate hello blacklist_exceptions section in hello multipath.conf file.</span></span> <span data-ttu-id="bad96-219">Устройство StorSimple требует toobe среди черный список исключений в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="bad96-219">Your StorSimple device needs toobe listed as a blacklist exception in this section.</span></span> <span data-ttu-id="bad96-220">Вы можете Раскомментировать, что соответствующие строки в этот файл toomodify его как показано ниже (используйте только hello конкретной модели hello устройства, который вы используете):</span><span class="sxs-lookup"><span data-stu-id="bad96-220">You can uncomment relevant lines in this file toomodify it as shown below (use only hello specific model of hello device you are using):</span></span>
   
        blacklist_exceptions {
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8100*"
            }
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8600*"
            }
           }

### <a name="step-3-configure-round-robin-multipathing"></a><span data-ttu-id="bad96-221">Этап 3. Настройка циклического многоканального ввода-вывода</span><span class="sxs-lookup"><span data-stu-id="bad96-221">Step 3: Configure round-robin multipathing</span></span>
<span data-ttu-id="bad96-222">Этот алгоритм балансировки нагрузки использует все hello доступных multipaths toohello активного контроллера в сбалансированной, циклического перебора.</span><span class="sxs-lookup"><span data-stu-id="bad96-222">This load-balancing algorithm uses all hello available multipaths toohello active controller in a balanced, round-robin fashion.</span></span>

1. <span data-ttu-id="bad96-223">Изменить hello `/etc/multipath.conf` файла.</span><span class="sxs-lookup"><span data-stu-id="bad96-223">Edit hello `/etc/multipath.conf` file.</span></span> <span data-ttu-id="bad96-224">Тип:</span><span class="sxs-lookup"><span data-stu-id="bad96-224">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="bad96-225">В разделе hello `defaults` раздел, набор hello `path_grouping_policy` слишком`multibus`.</span><span class="sxs-lookup"><span data-stu-id="bad96-225">Under hello `defaults` section, set hello `path_grouping_policy` too`multibus`.</span></span> <span data-ttu-id="bad96-226">Hello `path_grouping_policy` указывает hello группирования путь по умолчанию политика multipaths toounspecified tooapply.</span><span class="sxs-lookup"><span data-stu-id="bad96-226">hello `path_grouping_policy` specifies hello default path grouping policy tooapply toounspecified multipaths.</span></span> <span data-ttu-id="bad96-227">раздел по умолчанию Hello будет выглядеть, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="bad96-227">hello defaults section will look as shown below.</span></span>
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> <span data-ttu-id="bad96-228">Здравствуйте, наиболее часто встречающихся значений из `path_grouping_policy` включают:</span><span class="sxs-lookup"><span data-stu-id="bad96-228">hello most common values of `path_grouping_policy` include:</span></span>
> 
> * <span data-ttu-id="bad96-229">failover — один канал для каждой группы приоритетов;</span><span class="sxs-lookup"><span data-stu-id="bad96-229">failover = 1 path per priority group</span></span>
> * <span data-ttu-id="bad96-230">multibus — все допустимые каналы в одной группе приоритетов.</span><span class="sxs-lookup"><span data-stu-id="bad96-230">multibus = all valid paths in 1 priority group</span></span>
> 
> 

### <a name="step-4-enable-multipathing"></a><span data-ttu-id="bad96-231">Этап 4. Активация многоканального ввода-вывода</span><span class="sxs-lookup"><span data-stu-id="bad96-231">Step 4: Enable multipathing</span></span>
1. <span data-ttu-id="bad96-232">Перезапустите hello `multipathd` управляющей программы.</span><span class="sxs-lookup"><span data-stu-id="bad96-232">Restart hello `multipathd` daemon.</span></span> <span data-ttu-id="bad96-233">Тип:</span><span class="sxs-lookup"><span data-stu-id="bad96-233">Type:</span></span>
   
    `service multipathd restart`
2. <span data-ttu-id="bad96-234">Hello выходные данные будут, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="bad96-234">hello output will be as shown below:</span></span>
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a><span data-ttu-id="bad96-235">Этап 5. Проверка работы многоканального ввода-вывода</span><span class="sxs-lookup"><span data-stu-id="bad96-235">Step 5: Verify multipathing</span></span>
1. <span data-ttu-id="bad96-236">Сначала убедитесь, что iSCSI соединения с устройством StorSimple hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="bad96-236">First make sure that iSCSI connection is established with hello StorSimple device as follows:</span></span>
   
   <span data-ttu-id="bad96-237">а.</span><span class="sxs-lookup"><span data-stu-id="bad96-237">a.</span></span> <span data-ttu-id="bad96-238">Обнаружьте устройство StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bad96-238">Discover your StorSimple device.</span></span> <span data-ttu-id="bad96-239">Тип:</span><span class="sxs-lookup"><span data-stu-id="bad96-239">Type:</span></span>
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on hello device>:<iSCSI port on StorSimple device>
    ```
    
    <span data-ttu-id="bad96-240">Hello IP-адрес DATA0 10.126.162.25 и открыть порт 3260 на устройстве StorSimple hello для трафика iSCSI исходящих при выводится как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="bad96-240">hello output when IP address for DATA0 is 10.126.162.25 and port 3260 is opened on hello StorSimple device for outbound iSCSI traffic is as shown below:</span></span>
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    <span data-ttu-id="bad96-241">Копировать hello IQN устройства StorSimple `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, из hello предшествующих выходных данных.</span><span class="sxs-lookup"><span data-stu-id="bad96-241">Copy hello IQN of your StorSimple device, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, from hello preceding output.</span></span>

   <span data-ttu-id="bad96-242">b.</span><span class="sxs-lookup"><span data-stu-id="bad96-242">b.</span></span> <span data-ttu-id="bad96-243">Подключиться с помощью целевой IQN устройства toohello.</span><span class="sxs-lookup"><span data-stu-id="bad96-243">Connect toohello device using target IQN.</span></span> <span data-ttu-id="bad96-244">устройство StorSimple Hello находится здесь hello цели iSCSI.</span><span class="sxs-lookup"><span data-stu-id="bad96-244">hello StorSimple device is hello iSCSI target here.</span></span> <span data-ttu-id="bad96-245">Тип:</span><span class="sxs-lookup"><span data-stu-id="bad96-245">Type:</span></span>

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    <span data-ttu-id="bad96-246">Hello следующем примере показаны выходные данные с целевой IQN из `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span><span class="sxs-lookup"><span data-stu-id="bad96-246">hello following example shows output with a target IQN of `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span></span> <span data-ttu-id="bad96-247">выходные данные Hello указывает, успешно подключились toohello двух интерфейсов сети с поддержкой iSCSI на устройстве.</span><span class="sxs-lookup"><span data-stu-id="bad96-247">hello output indicates that you have successfully connected toohello two iSCSI-enabled network interfaces on your device.</span></span>

    ```
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    <span data-ttu-id="bad96-248">Если вы видите только один хост-интерфейс и здесь два пути, необходимо tooenable обоих интерфейсов "hello" на узле для iSCSI.</span><span class="sxs-lookup"><span data-stu-id="bad96-248">If you see only one host interface and two paths here, then you need tooenable both hello interfaces on host for iSCSI.</span></span> <span data-ttu-id="bad96-249">Можно выполнить hello [подробные инструкции в документации Linux](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span><span class="sxs-lookup"><span data-stu-id="bad96-249">You can follow hello [detailed instructions in Linux documentation](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span></span>

2. <span data-ttu-id="bad96-250">Том является сервер CentOS предоставляется toohello из устройства StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="bad96-250">A volume is exposed toohello CentOS server from hello StorSimple device.</span></span> <span data-ttu-id="bad96-251">Дополнительные сведения см. в разделе [шаг 6: Создание тома](storsimple-deployment-walkthrough.md#step-6-create-a-volume) через hello классический портал Azure на устройстве StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bad96-251">For more information, see [Step 6: Create a volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via hello Azure classic portal on your StorSimple device.</span></span>

3. <span data-ttu-id="bad96-252">Проверьте hello доступные пути.</span><span class="sxs-lookup"><span data-stu-id="bad96-252">Verify hello available paths.</span></span> <span data-ttu-id="bad96-253">Тип:</span><span class="sxs-lookup"><span data-stu-id="bad96-253">Type:</span></span>

      ```
      multipath –l
      ```

      <span data-ttu-id="bad96-254">Привет, в следующем примере показаны выходные данные hello для двух сетевых интерфейсов на интерфейсе StorSimple устройство подключенных tooa один узел сети с двумя доступные пути.</span><span class="sxs-lookup"><span data-stu-id="bad96-254">hello following example shows hello output for two network interfaces on a StorSimple device connected tooa single host network interface with two available paths.</span></span>

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        hello following example shows hello output for two network interfaces on a StorSimple device connected tootwo host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After hello paths are configured, refer toohello specific instructions on your host operating system (Centos 6.6) toomount and format this volume.

## <a name="troubleshoot-multipathing"></a><span data-ttu-id="bad96-255">Устранение неполадок многоканального ввода-вывода</span><span class="sxs-lookup"><span data-stu-id="bad96-255">Troubleshoot multipathing</span></span>
<span data-ttu-id="bad96-256">В этом разделе приведены некоторые полезные советы, которые помогут вам при возникновении проблем во время настройки многоканального ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="bad96-256">This section provides some helpful tips if you run into any issues during multipathing configuration.</span></span>

<span data-ttu-id="bad96-257">В.</span><span class="sxs-lookup"><span data-stu-id="bad96-257">Q.</span></span> <span data-ttu-id="bad96-258">Я не вижу hello изменения в `multipath.conf` файл вступают в силу.</span><span class="sxs-lookup"><span data-stu-id="bad96-258">I do not see hello changes in `multipath.conf` file taking effect.</span></span>

<span data-ttu-id="bad96-259">О.</span><span class="sxs-lookup"><span data-stu-id="bad96-259">A.</span></span> <span data-ttu-id="bad96-260">При внесении любого изменения toohello `multipath.conf` файл, необходимо будет toorestart hello несколько каналов службы.</span><span class="sxs-lookup"><span data-stu-id="bad96-260">If you have made any changes toohello `multipath.conf` file, you will need toorestart hello multipathing service.</span></span> <span data-ttu-id="bad96-261">Введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="bad96-261">Type hello following command:</span></span>

    service multipathd restart

<span data-ttu-id="bad96-262">В.</span><span class="sxs-lookup"><span data-stu-id="bad96-262">Q.</span></span> <span data-ttu-id="bad96-263">Включена, две сетевые интерфейсы на устройстве StorSimple hello и двух сетевых интерфейсов на узле hello.</span><span class="sxs-lookup"><span data-stu-id="bad96-263">I have enabled two network interfaces on hello StorSimple device and two network interfaces on hello host.</span></span> <span data-ttu-id="bad96-264">Перечень доступных путей hello, виден только двух ветвей.</span><span class="sxs-lookup"><span data-stu-id="bad96-264">When I list hello available paths, I see only two paths.</span></span> <span data-ttu-id="bad96-265">Ожидалось toosee четыре доступные пути.</span><span class="sxs-lookup"><span data-stu-id="bad96-265">I expected toosee four available paths.</span></span>

<span data-ttu-id="bad96-266">О.</span><span class="sxs-lookup"><span data-stu-id="bad96-266">A.</span></span> <span data-ttu-id="bad96-267">Убедитесь, что на hello hello два пути одной подсети, поддерживают маршрутизацию.</span><span class="sxs-lookup"><span data-stu-id="bad96-267">Make sure that hello two paths are on hello same subnet and routable.</span></span> <span data-ttu-id="bad96-268">Если сетевые интерфейсы hello находятся на разных виртуальных локальных сетей, не поддерживают маршрутизацию, вы увидите только двух ветвей.</span><span class="sxs-lookup"><span data-stu-id="bad96-268">If hello network interfaces are on different vLANs and not routable, you will see only two paths.</span></span> <span data-ttu-id="bad96-269">Одним из способов tooverify это toomake том, что можно получить доступ к оба интерфейса hello узла из сетевого интерфейса на устройстве StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="bad96-269">One way tooverify this is toomake sure that you can reach both hello host interfaces from a network interface on hello StorSimple device.</span></span> <span data-ttu-id="bad96-270">Необходимо будет слишком[обратитесь в службу поддержки корпорации Майкрософт](storsimple-contact-microsoft-support.md) как такая проверка может выполняться только через сеанса поддержки.</span><span class="sxs-lookup"><span data-stu-id="bad96-270">You will need too[contact Microsoft Support](storsimple-contact-microsoft-support.md) as this verification can only be done via a support session.</span></span>

<span data-ttu-id="bad96-271">В.</span><span class="sxs-lookup"><span data-stu-id="bad96-271">Q.</span></span> <span data-ttu-id="bad96-272">Когда я пытаюсь вывести список доступных каналов, ничего не происходит.</span><span class="sxs-lookup"><span data-stu-id="bad96-272">When I list available paths, I do not see any output.</span></span>

<span data-ttu-id="bad96-273">О.</span><span class="sxs-lookup"><span data-stu-id="bad96-273">A.</span></span> <span data-ttu-id="bad96-274">Как правило, не отображаются все пути многопутевых предлагает проблема с управляющей программы hello несколько каналов, и это скорее всего, здесь все проблемы заключается в hello `multipath.conf` файла.</span><span class="sxs-lookup"><span data-stu-id="bad96-274">Typically, not seeing any multipathed paths suggests a problem with hello multipathing daemon, and it’s most likely that any problem here lies in hello `multipath.conf` file.</span></span>

<span data-ttu-id="bad96-275">Было бы также стоит проверки, что можно увидеть некоторые диски после подключения целевой toohello как нет ответа из списков многоканального hello может также означать, что у вас нет все диски.</span><span class="sxs-lookup"><span data-stu-id="bad96-275">It would also be worth checking that you can actually see some disks after connecting toohello target, as no response from hello multipath listings could also mean you don’t have any disks.</span></span>

* <span data-ttu-id="bad96-276">Используйте следующие шины SCSI hello toorescan команда hello.</span><span class="sxs-lookup"><span data-stu-id="bad96-276">Use hello following command toorescan hello SCSI bus:</span></span>
  
    <span data-ttu-id="bad96-277">`$ rescan-scsi-bus.sh `(часть пакета sg3_utils)</span><span class="sxs-lookup"><span data-stu-id="bad96-277">`$ rescan-scsi-bus.sh `(part of sg3_utils package)</span></span>
* <span data-ttu-id="bad96-278">Введите следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="bad96-278">Type hello following commands:</span></span>
  
    `$ dmesg | grep sd*`
     
     <span data-ttu-id="bad96-279">Или</span><span class="sxs-lookup"><span data-stu-id="bad96-279">Or</span></span>
  
    `$ fdisk –l`
  
    <span data-ttu-id="bad96-280">В результате будут возвращены сведения о недавно добавленных дисках.</span><span class="sxs-lookup"><span data-stu-id="bad96-280">These will return details of recently added disks.</span></span>
* <span data-ttu-id="bad96-281">toodetermine ли это StorSimple диск, используйте hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="bad96-281">toodetermine whether it is a StorSimple disk, use hello following commands:</span></span>
  
    `cat /sys/block/<DISK>/device/model`
  
    <span data-ttu-id="bad96-282">В результате будет возвращена строка, которая определит, принадлежит ли диск устройству StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bad96-282">This will return a string, which will determine if it’s a StorSimple disk.</span></span>

<span data-ttu-id="bad96-283">Менее вероятной, но также возможной причиной может быть устаревший идентификатор процесса iscsid.</span><span class="sxs-lookup"><span data-stu-id="bad96-283">A less likely but possible cause could also be stale iscsid pid.</span></span> <span data-ttu-id="bad96-284">Используйте следующую команду toolog off из сеансов iSCSI hello hello.</span><span class="sxs-lookup"><span data-stu-id="bad96-284">Use hello following command toolog off from hello iSCSI sessions:</span></span>

    iscsiadm -m node --logout -p <Target_IP>

<span data-ttu-id="bad96-285">Повторите эту команду для всех сетевых интерфейсов hello подключен на цели iSCSI hello, который является устройства StorSimple.</span><span class="sxs-lookup"><span data-stu-id="bad96-285">Repeat this command for all hello connected network interfaces on hello iSCSI target, which is your StorSimple device.</span></span> <span data-ttu-id="bad96-286">После входа от всех сеансов iSCSI hello, используйте hello цели iSCSI IQN, tooreestablish hello сеанса iSCSI.</span><span class="sxs-lookup"><span data-stu-id="bad96-286">Once you have logged off from all hello iSCSI sessions, use hello iSCSI target IQN tooreestablish hello iSCSI session.</span></span> <span data-ttu-id="bad96-287">Введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="bad96-287">Type hello following command:</span></span>

    iscsiadm -m node --login -T <TARGET_IQN>


<span data-ttu-id="bad96-288">В.</span><span class="sxs-lookup"><span data-stu-id="bad96-288">Q.</span></span> <span data-ttu-id="bad96-289">Я не уверен, включено ли мое устройство в список разрешенных устройств.</span><span class="sxs-lookup"><span data-stu-id="bad96-289">I am not sure if my device is whitelisted.</span></span>

<span data-ttu-id="bad96-290">О.</span><span class="sxs-lookup"><span data-stu-id="bad96-290">A.</span></span> <span data-ttu-id="bad96-291">tooverify ли устройство не входят, используйте следующую команду по устранению неполадок интерактивных hello:</span><span class="sxs-lookup"><span data-stu-id="bad96-291">tooverify whether your device is whitelisted, use hello following troubleshooting interactive command:</span></span>

    multipathd –k
    multipathd> show devices
    available block devices:
    ram0 devnode blacklisted, unmonitored
    ram1 devnode blacklisted, unmonitored
    ram2 devnode blacklisted, unmonitored
    ram3 devnode blacklisted, unmonitored
    ram4 devnode blacklisted, unmonitored
    ram5 devnode blacklisted, unmonitored
    ram6 devnode blacklisted, unmonitored
    ram7 devnode blacklisted, unmonitored
    ram8 devnode blacklisted, unmonitored
    ram9 devnode blacklisted, unmonitored
    ram10 devnode blacklisted, unmonitored
    ram11 devnode blacklisted, unmonitored
    ram12 devnode blacklisted, unmonitored
    ram13 devnode blacklisted, unmonitored
    ram14 devnode blacklisted, unmonitored
    ram15 devnode blacklisted, unmonitored
    loop0 devnode blacklisted, unmonitored
    loop1 devnode blacklisted, unmonitored
    loop2 devnode blacklisted, unmonitored
    loop3 devnode blacklisted, unmonitored
    loop4 devnode blacklisted, unmonitored
    loop5 devnode blacklisted, unmonitored
    loop6 devnode blacklisted, unmonitored
    loop7 devnode blacklisted, unmonitored
    sr0 devnode blacklisted, unmonitored
    sda devnode whitelisted, monitored
    dm-0 devnode blacklisted, unmonitored
    dm-1 devnode blacklisted, unmonitored
    dm-2 devnode blacklisted, unmonitored
    sdb devnode whitelisted, monitored
    sdc devnode whitelisted, monitored
    dm-3 devnode blacklisted, unmonitored


<span data-ttu-id="bad96-292">Дополнительные сведения см. слишком[воспользуйтесь неполадок интерактивную команду для несколько каналов](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span><span class="sxs-lookup"><span data-stu-id="bad96-292">For more information, go too[use troubleshooting interactive command for multipathing](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span></span>

## <a name="list-of-useful-commands"></a><span data-ttu-id="bad96-293">Список полезных команд</span><span class="sxs-lookup"><span data-stu-id="bad96-293">List of useful commands</span></span>
| <span data-ttu-id="bad96-294">При появлении запроса на подтверждение нажмите клавишу </span><span class="sxs-lookup"><span data-stu-id="bad96-294">Type</span></span> | <span data-ttu-id="bad96-295">Команда</span><span class="sxs-lookup"><span data-stu-id="bad96-295">Command</span></span> | <span data-ttu-id="bad96-296">Описание</span><span class="sxs-lookup"><span data-stu-id="bad96-296">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bad96-297">**iSCSI**</span><span class="sxs-lookup"><span data-stu-id="bad96-297">**iSCSI**</span></span> |`service iscsid start` |<span data-ttu-id="bad96-298">Запуск службы iSCSI</span><span class="sxs-lookup"><span data-stu-id="bad96-298">Start iSCSI service</span></span> |
| &nbsp; |`service iscsid stop` |<span data-ttu-id="bad96-299">Остановка службы iSCSI</span><span class="sxs-lookup"><span data-stu-id="bad96-299">Stop iSCSI service</span></span> |
| &nbsp; |`service iscsid restart` |<span data-ttu-id="bad96-300">Перезапуск службы iSCSI</span><span class="sxs-lookup"><span data-stu-id="bad96-300">Restart iSCSI service</span></span> |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |<span data-ttu-id="bad96-301">Обнаружение доступных целевых объектов на hello указан адрес</span><span class="sxs-lookup"><span data-stu-id="bad96-301">Discover available targets on hello specified address</span></span> |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |<span data-ttu-id="bad96-302">Войдите в toohello цели iSCSI</span><span class="sxs-lookup"><span data-stu-id="bad96-302">Log in toohello iSCSI target</span></span> |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |<span data-ttu-id="bad96-303">Выйдите из цели iSCSI hello</span><span class="sxs-lookup"><span data-stu-id="bad96-303">Log out from hello iSCSI target</span></span> |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |<span data-ttu-id="bad96-304">Вывод имени инициатора iSCSI</span><span class="sxs-lookup"><span data-stu-id="bad96-304">Print iSCSI initiator name</span></span> |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |<span data-ttu-id="bad96-305">Проверьте состояние hello сеанса iSCSI hello и тома, обнаруженные на узле hello</span><span class="sxs-lookup"><span data-stu-id="bad96-305">Check hello state of hello iSCSI session and volume discovered on hello host</span></span> |
| &nbsp; |`iscsi –m session` |<span data-ttu-id="bad96-306">Показывает все сеансы iSCSI hello, установленных между hello узле и устройстве StorSimple hello</span><span class="sxs-lookup"><span data-stu-id="bad96-306">Shows all hello iSCSI sessions established between hello host and hello StorSimple device</span></span> |
|  | | |
| <span data-ttu-id="bad96-307">**Поддержка нескольких каналов ввода-вывода**</span><span class="sxs-lookup"><span data-stu-id="bad96-307">**Multipathing**</span></span> |`service multipathd start` |<span data-ttu-id="bad96-308">Запуск управляющей программы многоканального ввода-вывода</span><span class="sxs-lookup"><span data-stu-id="bad96-308">Start multipath daemon</span></span> |
| &nbsp; |`service multipathd stop` |<span data-ttu-id="bad96-309">Остановка управляющей программы многоканального ввода-вывода</span><span class="sxs-lookup"><span data-stu-id="bad96-309">Stop multipath daemon</span></span> |
| &nbsp; |`service multipathd restart` |<span data-ttu-id="bad96-310">Перезапуск управляющей программы многоканального ввода-вывода</span><span class="sxs-lookup"><span data-stu-id="bad96-310">Restart multipath daemon</span></span> |
| &nbsp; |`chkconfig multipathd on` </br> <span data-ttu-id="bad96-311">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="bad96-311">OR</span></span> </br> `mpathconf –with_chkconfig y` |<span data-ttu-id="bad96-312">Включить toostart многоканального управляющей программы во время загрузки</span><span class="sxs-lookup"><span data-stu-id="bad96-312">Enable multipath daemon toostart at boot time</span></span> |
| &nbsp; |`multipathd –k` |<span data-ttu-id="bad96-313">Запуск интерактивной консоли hello для устранения неполадок</span><span class="sxs-lookup"><span data-stu-id="bad96-313">Start hello interactive console for troubleshooting</span></span> |
| &nbsp; |`multipath –l` |<span data-ttu-id="bad96-314">Вывод списка подключений и устройств с многоканальным вводом-выводом</span><span class="sxs-lookup"><span data-stu-id="bad96-314">List multipath connections and devices</span></span> |
| &nbsp; |`mpathconf --enable` |<span data-ttu-id="bad96-315">Создание примера файла mulitpath.conf в `/etc/mulitpath.conf`</span><span class="sxs-lookup"><span data-stu-id="bad96-315">Create a sample mulitpath.conf file in `/etc/mulitpath.conf`</span></span> |
|  | | |

## <a name="next-steps"></a><span data-ttu-id="bad96-316">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bad96-316">Next steps</span></span>
<span data-ttu-id="bad96-317">При настройке MPIO на узле Linux, может также потребоваться следующие документы CentoS 6.6 toohello toorefer:</span><span class="sxs-lookup"><span data-stu-id="bad96-317">As you are configuring MPIO on Linux host, you may also need toorefer toohello following CentoS 6.6 documents:</span></span>

* [<span data-ttu-id="bad96-318">Настройка MPIO на CentOS</span><span class="sxs-lookup"><span data-stu-id="bad96-318">Setting up MPIO on CentOS</span></span>](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [<span data-ttu-id="bad96-319">Учебное руководство Linux</span><span class="sxs-lookup"><span data-stu-id="bad96-319">Linux Training Guide</span></span>](http://linux-training.be/files/books/LinuxAdm.pdf)

