---
title: "N-й серии aaaAzure установки драйвера для Linux | Документы Microsoft"
description: "Как tooset драйверы GPU, NVIDIA для N-й серии виртуальных машин под управлением Linux в Azure"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d91695d0-64b9-4e6b-84bd-18401eaecdde
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7db1b3859f9075c6d9f0319f39418946ea08743f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a><span data-ttu-id="36c19-103">Установка драйверов GPU NVIDIA на виртуальные машины серии N под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="36c19-103">Install NVIDIA GPU drivers on N-series VMs running Linux</span></span>

<span data-ttu-id="36c19-104">преимущества tootake работы GPU hello Azure N-й серии виртуальных машин под управлением Linux, установите поддерживаемые NVIDIA графические драйверы.</span><span class="sxs-lookup"><span data-stu-id="36c19-104">tootake advantage of hello GPU capabilities of Azure N-series VMs running Linux, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="36c19-105">В этой статье приводятся действия по установке драйверов после развертывания виртуальных машин серии N.</span><span class="sxs-lookup"><span data-stu-id="36c19-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="36c19-106">Сведения об установке драйверов также доступны для [виртуальных машин Windows](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="36c19-106">Driver setup information is also available for [Windows VMs](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


<span data-ttu-id="36c19-107">Характеристики виртуальных машин серии N, сведения о дисках и объеме памяти см. в статье [Размеры виртуальных машин Linux, оптимизированных для GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="36c19-107">For N-series VM specs, storage capacities, and disk details, see [GPU Linux VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a><span data-ttu-id="36c19-108">Установка драйверов GRID для виртуальных машин NV</span><span class="sxs-lookup"><span data-stu-id="36c19-108">Install GRID drivers for NV VMs</span></span>

<span data-ttu-id="36c19-109">драйверы tooinstall NVIDIA СЕТКИ на виртуальных машинах NV, сделать tooeach подключения SSH виртуальной Машины и выполните действия hello для дистрибутива Linux.</span><span class="sxs-lookup"><span data-stu-id="36c19-109">tooinstall NVIDIA GRID drivers on NV VMs, make an SSH connection tooeach VM and follow hello steps for your Linux distribution.</span></span> 

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="36c19-110">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="36c19-110">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="36c19-111">Запустите hello `lspci` команды.</span><span class="sxs-lookup"><span data-stu-id="36c19-111">Run hello `lspci` command.</span></span> <span data-ttu-id="36c19-112">Убедитесь, что hello NVIDIA M60 карты или карты отображаются как устройства PCI.</span><span class="sxs-lookup"><span data-stu-id="36c19-112">Verify that hello NVIDIA M60 card or cards are visible as PCI devices.</span></span>

2. <span data-ttu-id="36c19-113">Установите обновления.</span><span class="sxs-lookup"><span data-stu-id="36c19-113">Install updates.</span></span>

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. <span data-ttu-id="36c19-114">Отключение драйвера ядра Nouveau hello, которая несовместима с драйвером NVIDIA hello.</span><span class="sxs-lookup"><span data-stu-id="36c19-114">Disable hello Nouveau kernel driver, which is incompatible with hello NVIDIA driver.</span></span> <span data-ttu-id="36c19-115">(Только используйте драйвер NVIDIA hello на виртуальных машинах NV). toodo это, создайте файл в `/etc/modprobe.d `с именем `nouveau.conf` с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="36c19-115">(Only use hello NVIDIA driver on NV VMs.) toodo this, create a file in `/etc/modprobe.d `named `nouveau.conf` with hello following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. <span data-ttu-id="36c19-116">Перезагрузите компьютер hello виртуальной Машины и повторного подключения.</span><span class="sxs-lookup"><span data-stu-id="36c19-116">Reboot hello VM and reconnect.</span></span> <span data-ttu-id="36c19-117">Выйдите из X-сервера:</span><span class="sxs-lookup"><span data-stu-id="36c19-117">Exit X server:</span></span>

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. <span data-ttu-id="36c19-118">Загрузите и установите драйвер hello СЕТКИ.</span><span class="sxs-lookup"><span data-stu-id="36c19-118">Download and install hello GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. <span data-ttu-id="36c19-119">В ответ на запрос, следует ли toorun hello nvidia xconfig программа tooupdate X файла конфигурации, выберите **Да**.</span><span class="sxs-lookup"><span data-stu-id="36c19-119">When you're asked whether you want toorun hello nvidia-xconfig utility tooupdate your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="36c19-120">После завершения установки, скопируйте gridd.conf tooa новый /etc/nvidia/gridd.conf.template файл в расположение/etc/nvidia /</span><span class="sxs-lookup"><span data-stu-id="36c19-120">After installation completes, copy /etc/nvidia/gridd.conf.template tooa new file gridd.conf at location /etc/nvidia/</span></span>

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. <span data-ttu-id="36c19-121">Добавьте hello слишком следующие`/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="36c19-121">Add hello following too`/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="36c19-122">Перезагрузите компьютер hello виртуальной Машины и продолжить установку tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="36c19-122">Reboot hello VM and proceed tooverify hello installation.</span></span>


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="36c19-123">CentOS 7.3 или Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="36c19-123">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>


1. <span data-ttu-id="36c19-124">Обновление ядра hello и DKMS.</span><span class="sxs-lookup"><span data-stu-id="36c19-124">Update hello kernel and DKMS.</span></span>
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. <span data-ttu-id="36c19-125">Отключение драйвера ядра Nouveau hello, которая несовместима с драйвером NVIDIA hello.</span><span class="sxs-lookup"><span data-stu-id="36c19-125">Disable hello Nouveau kernel driver, which is incompatible with hello NVIDIA driver.</span></span> <span data-ttu-id="36c19-126">(Только используйте драйвер NVIDIA hello на виртуальных машинах NV). toodo это, создайте файл в `/etc/modprobe.d `с именем `nouveau.conf` с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="36c19-126">(Only use hello NVIDIA driver on NV VMs.) toodo this, create a file in `/etc/modprobe.d `named `nouveau.conf` with hello following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. <span data-ttu-id="36c19-127">Перезагрузите hello ВМ, повторно подключиться и установите последнюю версию служб интеграции Linux для Hyper-V: hello</span><span class="sxs-lookup"><span data-stu-id="36c19-127">Reboot hello VM, reconnect, and install hello latest Linux Integration Services for Hyper-V:</span></span>
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. <span data-ttu-id="36c19-128">Подключите toohello виртуальной Машины и выполнить hello `lspci` команды.</span><span class="sxs-lookup"><span data-stu-id="36c19-128">Reconnect toohello VM and run hello `lspci` command.</span></span> <span data-ttu-id="36c19-129">Убедитесь, что hello NVIDIA M60 карты или карты отображаются как устройства PCI.</span><span class="sxs-lookup"><span data-stu-id="36c19-129">Verify that hello NVIDIA M60 card or cards are visible as PCI devices.</span></span>
 
5. <span data-ttu-id="36c19-130">Загрузите и установите драйвер hello СЕТКИ.</span><span class="sxs-lookup"><span data-stu-id="36c19-130">Download and install hello GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. <span data-ttu-id="36c19-131">В ответ на запрос, следует ли toorun hello nvidia xconfig программа tooupdate X файла конфигурации, выберите **Да**.</span><span class="sxs-lookup"><span data-stu-id="36c19-131">When you're asked whether you want toorun hello nvidia-xconfig utility tooupdate your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="36c19-132">После завершения установки, скопируйте gridd.conf tooa новый /etc/nvidia/gridd.conf.template файл в расположение/etc/nvidia /</span><span class="sxs-lookup"><span data-stu-id="36c19-132">After installation completes, copy /etc/nvidia/gridd.conf.template tooa new file gridd.conf at location /etc/nvidia/</span></span>
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. <span data-ttu-id="36c19-133">Добавьте hello слишком следующие`/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="36c19-133">Add hello following too`/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="36c19-134">Перезагрузите компьютер hello виртуальной Машины и продолжить установку tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="36c19-134">Reboot hello VM and proceed tooverify hello installation.</span></span>

### <a name="verify-driver-installation"></a><span data-ttu-id="36c19-135">Проверка установки драйверов</span><span class="sxs-lookup"><span data-stu-id="36c19-135">Verify driver installation</span></span>


<span data-ttu-id="36c19-136">tooquery hello состояния устройств GPU, SSH toohello ВМ и выполнения hello [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) программа устанавливается вместе с драйвером hello.</span><span class="sxs-lookup"><span data-stu-id="36c19-136">tooquery hello GPU device state, SSH toohello VM and run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span> 

<span data-ttu-id="36c19-137">Появится примерно toohello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="36c19-137">Output similar toohello following appears:</span></span>

![Состояние устройства NVIDIA](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a><span data-ttu-id="36c19-139">Сервер X11</span><span class="sxs-lookup"><span data-stu-id="36c19-139">X11 server</span></span>
<span data-ttu-id="36c19-140">Если вам требуется X11 сервера для удаленных подключений tooan ВМ NV [x11vnc](http://www.karlrunge.com/x11vnc/) рекомендуется, так как она допускает аппаратное ускорение графики.</span><span class="sxs-lookup"><span data-stu-id="36c19-140">If you need an X11 server for remote connections tooan NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) is recommended because it allows hardware acceleration of graphics.</span></span> <span data-ttu-id="36c19-141">Hello BusID hello M60 устройства необходимо вручную добавить файл xconfig toohello (`etc/X11/xorg.conf` на Ubuntu 16.04 LTS, `/etc/X11/XF86config` на CentOS 7.3 или Red Hat Enterprise Server 7.3).</span><span class="sxs-lookup"><span data-stu-id="36c19-141">hello BusID of hello M60 device must be manually added toohello xconfig file (`etc/X11/xorg.conf` on Ubuntu 16.04 LTS, `/etc/X11/XF86config` on CentOS 7.3 or Red Hat Enterprise Server 7.3).</span></span> <span data-ttu-id="36c19-142">Добавить `"Device"` статьи аналогичные toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="36c19-142">Add a `"Device"` section similar toohello following:</span></span>
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
<span data-ttu-id="36c19-143">Кроме того, обновить ваш `"Screen"` статьи toouse это устройство.</span><span class="sxs-lookup"><span data-stu-id="36c19-143">Additionally, update your `"Screen"` section toouse this device.</span></span>
 
<span data-ttu-id="36c19-144">Hello BusID можно найти, выполнив</span><span class="sxs-lookup"><span data-stu-id="36c19-144">hello BusID can be found by running</span></span>

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
<span data-ttu-id="36c19-145">Hello BusID можно изменить, если виртуальная машина получает перераспределить или перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="36c19-145">hello BusID can change when a VM gets reallocated or rebooted.</span></span> <span data-ttu-id="36c19-146">Таким образом вы можете toouse hello tooupdate сценарий BusID в конфигурации hello X11 при перезагрузке виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="36c19-146">Therefore, you may want toouse a script tooupdate hello BusID in hello X11 configuration when a VM is rebooted.</span></span> <span data-ttu-id="36c19-147">Например:</span><span class="sxs-lookup"><span data-stu-id="36c19-147">For example:</span></span>

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed too${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

<span data-ttu-id="36c19-148">Этот файл можно вызывать с правами привилегированного пользователя во время загрузки, создав для него запись в `/etc/rc.d/rc3.d`.</span><span class="sxs-lookup"><span data-stu-id="36c19-148">This file can be invoked as root on boot by creating an entry for it in `/etc/rc.d/rc3.d`.</span></span>


## <a name="install-cuda-drivers-for-nc-vms"></a><span data-ttu-id="36c19-149">Установка драйверов CUDA для виртуальных машин серии NC</span><span class="sxs-lookup"><span data-stu-id="36c19-149">Install CUDA drivers for NC VMs</span></span>

<span data-ttu-id="36c19-150">Вот драйверы NVIDIA tooinstall действия на виртуальных машинах Linux NC из hello NVIDIA CUDA Toolkit 8.0.</span><span class="sxs-lookup"><span data-stu-id="36c19-150">Here are steps tooinstall NVIDIA drivers on Linux NC VMs from hello NVIDIA CUDA Toolkit 8.0.</span></span> 

<span data-ttu-id="36c19-151">Разработчикам C и C++ можно также установить hello полный набор средств toobuild ускорением GPU приложений.</span><span class="sxs-lookup"><span data-stu-id="36c19-151">C and C++ developers can optionally install hello full Toolkit toobuild GPU-accelerated applications.</span></span> <span data-ttu-id="36c19-152">Дополнительные сведения см. в разделе hello [руководство по установке CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span><span class="sxs-lookup"><span data-stu-id="36c19-152">For more information, see hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span></span>


> [!NOTE]
> <span data-ttu-id="36c19-153">Предоставленные в статье ссылки для скачивания драйверов CUDA актуальны на момент ее публикации.</span><span class="sxs-lookup"><span data-stu-id="36c19-153">CUDA driver download links provided here are current at time of publication.</span></span> <span data-ttu-id="36c19-154">Последние версии драйверов CUDA hello, на сайте hello [NVIDIA](http://www.nvidia.com/) веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="36c19-154">For hello latest CUDA drivers, visit hello [NVIDIA](http://www.nvidia.com/) website.</span></span>
>

<span data-ttu-id="36c19-155">tooinstall CUDA Toolkit сделать tooeach подключения SSH виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="36c19-155">tooinstall CUDA Toolkit, make an SSH connection tooeach VM.</span></span> <span data-ttu-id="36c19-156">tooverify, hello система имеет поддержкой CUDA GPU, запустите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="36c19-156">tooverify that hello system has a CUDA-capable GPU, run hello following command:</span></span>

```bash
lspci | grep -i NVIDIA
```
<span data-ttu-id="36c19-157">Вы увидите примерно toohello вывода следующий пример (показывающее плату NVIDIA Tesla K80):</span><span class="sxs-lookup"><span data-stu-id="36c19-157">You will see output similar toohello following example (showing an NVIDIA Tesla K80 card):</span></span>

![результаты выполнения команды lspci](./media/n-series-driver-setup/lspci.png)

<span data-ttu-id="36c19-159">Затем выполните команды установки, относящиеся к используемому дистрибутиву.</span><span class="sxs-lookup"><span data-stu-id="36c19-159">Then run installation commands specific for your distribution.</span></span>

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="36c19-160">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="36c19-160">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="36c19-161">Загрузите и установите драйвер CUDA hello.</span><span class="sxs-lookup"><span data-stu-id="36c19-161">Download and install hello CUDA drivers.</span></span>
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  <span data-ttu-id="36c19-162">Hello установка может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="36c19-162">hello installation can take several minutes.</span></span>

2. <span data-ttu-id="36c19-163">toooptionally установки hello завершения CUDA набор средств, тип:</span><span class="sxs-lookup"><span data-stu-id="36c19-163">toooptionally install hello complete CUDA toolkit, type:</span></span>

  ```bash
  sudo apt-get install cuda
  ```

3. <span data-ttu-id="36c19-164">Перезагрузите компьютер hello виртуальной Машины и продолжить установку tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="36c19-164">Reboot hello VM and proceed tooverify hello installation.</span></span>

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="36c19-165">CentOS 7.3 или Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="36c19-165">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

1. <span data-ttu-id="36c19-166">Получите обновления.</span><span class="sxs-lookup"><span data-stu-id="36c19-166">Get updates.</span></span> 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. <span data-ttu-id="36c19-167">Подключите toohello ВМ и установить hello последнюю версию служб интеграции Linux для Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="36c19-167">Reconnect toohello VM and install hello latest Linux Integration Services for Hyper-V.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="36c19-168">При установке образа на основе CentOS HPC на Виртуальной машине NC24r пропустите tooStep 3.</span><span class="sxs-lookup"><span data-stu-id="36c19-168">If you installed a CentOS-based HPC image on an NC24r VM, skip tooStep 3.</span></span> <span data-ttu-id="36c19-169">Поскольку драйверы Azure RDMA и службы интеграции Linux предварительно установлен в образе hello, LIS не обновляются и обновлений ядра отключены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="36c19-169">Because Azure RDMA drivers and Linux Integration Services are pre-installed in hello image, LIS should not be upgraded, and kernel updates are disabled by default.</span></span>
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. <span data-ttu-id="36c19-170">Переподключение toohello ВМ и продолжите установку hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="36c19-170">Reconnect toohello VM and continue installation with hello following commands:</span></span>

  ```bash
  sudo yum install kernel-devel

  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

  sudo yum install dkms

  CUDA_REPO_PKG=cuda-repo-rhel7-8.0.61-1.x86_64.rpm

  wget http://developer.download.nvidia.com/compute/cuda/repos/rhel7/x86_64/${CUDA_REPO_PKG} -O /tmp/${CUDA_REPO_PKG}

  sudo rpm -ivh /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo yum install cuda-drivers
  ```

  <span data-ttu-id="36c19-171">Hello установка может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="36c19-171">hello installation can take several minutes.</span></span> 

4. <span data-ttu-id="36c19-172">toooptionally установки hello завершения CUDA набор средств, тип:</span><span class="sxs-lookup"><span data-stu-id="36c19-172">toooptionally install hello complete CUDA toolkit, type:</span></span>

  ```bash
  sudo yum install cuda
  ```

5. <span data-ttu-id="36c19-173">Перезагрузите компьютер hello виртуальной Машины и продолжить установку tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="36c19-173">Reboot hello VM and proceed tooverify hello installation.</span></span>


### <a name="verify-driver-installation"></a><span data-ttu-id="36c19-174">Проверка установки драйверов</span><span class="sxs-lookup"><span data-stu-id="36c19-174">Verify driver installation</span></span>


<span data-ttu-id="36c19-175">tooquery hello состояния устройств GPU, SSH toohello ВМ и выполнения hello [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) программа устанавливается вместе с драйвером hello.</span><span class="sxs-lookup"><span data-stu-id="36c19-175">tooquery hello GPU device state, SSH toohello VM and run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span> 

<span data-ttu-id="36c19-176">Появится примерно toohello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="36c19-176">Output similar toohello following appears:</span></span>

![Состояние устройства NVIDIA](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a><span data-ttu-id="36c19-178">Обновления драйверов CUDA</span><span class="sxs-lookup"><span data-stu-id="36c19-178">CUDA driver updates</span></span>

<span data-ttu-id="36c19-179">Рекомендуется периодически обновлять драйверы CUDA после развертывания.</span><span class="sxs-lookup"><span data-stu-id="36c19-179">We recommend that you periodically update CUDA drivers after deployment.</span></span>

#### <a name="ubuntu-1604-lts"></a><span data-ttu-id="36c19-180">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="36c19-180">Ubuntu 16.04 LTS</span></span>

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="36c19-181">CentOS 7.3 или Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="36c19-181">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a><span data-ttu-id="36c19-182">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="36c19-182">Troubleshooting</span></span>

* <span data-ttu-id="36c19-183">Имеется известная проблема с драйверами CUDA на ОС Linux ядра hello 4.4.0-75 Ubuntu 16.04 LTS виртуальных машинах Azure N-й серии.</span><span class="sxs-lookup"><span data-stu-id="36c19-183">There is a known issue with CUDA drivers on Azure N-series VMs running hello 4.4.0-75 Linux kernel on Ubuntu 16.04 LTS.</span></span> <span data-ttu-id="36c19-184">При обновлении с более ранней версии ядра обновление tooat наименьших 4.4.0-77 версию ядра.</span><span class="sxs-lookup"><span data-stu-id="36c19-184">If you are upgrading from an earlier kernel version, upgrade tooat least kernel version 4.4.0-77.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="36c19-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="36c19-185">Next steps</span></span>

* <span data-ttu-id="36c19-186">Дополнительные сведения о графических процессоров NVIDIA hello hello N-й серии виртуальных машин см.:</span><span class="sxs-lookup"><span data-stu-id="36c19-186">For more information about hello NVIDIA GPUs on hello N-series VMs, see:</span></span>
    * <span data-ttu-id="36c19-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (для виртуальных машин Azure серии NC);</span><span class="sxs-lookup"><span data-stu-id="36c19-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="36c19-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (для виртуальных машин Azure серии NV).</span><span class="sxs-lookup"><span data-stu-id="36c19-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="36c19-189">образ ВМ Linux с вашей установленные драйверы NVIDIA toocapture. в разделе [как toogeneralize и записать виртуальную машину Linux](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="36c19-189">toocapture a Linux VM image with your installed NVIDIA drivers, see [How toogeneralize and capture a Linux virtual machine](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
