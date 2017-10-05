---
title: "Установка драйвера серии N для Linux | Документация Майкрософт"
description: "Как установить драйверы NVIDIA GPU для виртуальных машин серии N под управлением Linux в Azure"
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
ms.openlocfilehash: bdeb4d5ca1d9ff4d7dfd0961690412dd7530572a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a><span data-ttu-id="eef10-103">Установка драйверов GPU NVIDIA на виртуальные машины серии N под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="eef10-103">Install NVIDIA GPU drivers on N-series VMs running Linux</span></span>

<span data-ttu-id="eef10-104">Чтобы воспользоваться преимуществами возможностей GPU виртуальных машин Azure серии N под управлением Linux, необходимо установить графические драйверы NVIDIA.</span><span class="sxs-lookup"><span data-stu-id="eef10-104">To take advantage of the GPU capabilities of Azure N-series VMs running Linux, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="eef10-105">В этой статье приводятся действия по установке драйверов после развертывания виртуальных машин серии N.</span><span class="sxs-lookup"><span data-stu-id="eef10-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="eef10-106">Сведения об установке драйверов также доступны для [виртуальных машин Windows](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eef10-106">Driver setup information is also available for [Windows VMs](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


<span data-ttu-id="eef10-107">Характеристики виртуальных машин серии N, сведения о дисках и объеме памяти см. в статье [Размеры виртуальных машин Linux, оптимизированных для GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eef10-107">For N-series VM specs, storage capacities, and disk details, see [GPU Linux VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a><span data-ttu-id="eef10-108">Установка драйверов GRID для виртуальных машин NV</span><span class="sxs-lookup"><span data-stu-id="eef10-108">Install GRID drivers for NV VMs</span></span>

<span data-ttu-id="eef10-109">Чтобы установить драйверы NVIDIA GRID на виртуальных машинах NV, подключитесь по протоколу SSH к каждой виртуальной машине и выполните действия, необходимые для дистрибутива Linux.</span><span class="sxs-lookup"><span data-stu-id="eef10-109">To install NVIDIA GRID drivers on NV VMs, make an SSH connection to each VM and follow the steps for your Linux distribution.</span></span> 

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="eef10-110">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="eef10-110">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="eef10-111">Выполните команду `lspci`.</span><span class="sxs-lookup"><span data-stu-id="eef10-111">Run the `lspci` command.</span></span> <span data-ttu-id="eef10-112">Убедитесь, что карта или карты NVIDIA M60 отображаются как устройства PCI.</span><span class="sxs-lookup"><span data-stu-id="eef10-112">Verify that the NVIDIA M60 card or cards are visible as PCI devices.</span></span>

2. <span data-ttu-id="eef10-113">Установите обновления.</span><span class="sxs-lookup"><span data-stu-id="eef10-113">Install updates.</span></span>

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. <span data-ttu-id="eef10-114">Отключите драйвер ядра Nouveau, который несовместим с драйвером NVIDIA.</span><span class="sxs-lookup"><span data-stu-id="eef10-114">Disable the Nouveau kernel driver, which is incompatible with the NVIDIA driver.</span></span> <span data-ttu-id="eef10-115">(На виртуальных машинах NV используйте только драйвер NVIDIA.) Чтобы сделать это, создайте в `/etc/modprobe.d ` файл с именем `nouveau.conf` со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="eef10-115">(Only use the NVIDIA driver on NV VMs.) To do this, create a file in `/etc/modprobe.d `named `nouveau.conf` with the following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. <span data-ttu-id="eef10-116">Перезагрузите виртуальную машину и подключитесь повторно.</span><span class="sxs-lookup"><span data-stu-id="eef10-116">Reboot the VM and reconnect.</span></span> <span data-ttu-id="eef10-117">Выйдите из X-сервера:</span><span class="sxs-lookup"><span data-stu-id="eef10-117">Exit X server:</span></span>

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. <span data-ttu-id="eef10-118">Загрузите и установите драйвер GRID.</span><span class="sxs-lookup"><span data-stu-id="eef10-118">Download and install the GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. <span data-ttu-id="eef10-119">Когда появится запрос на запуск служебной программы nvidia-xconfig для обновления файла конфигурации X, выберите **Да**.</span><span class="sxs-lookup"><span data-stu-id="eef10-119">When you're asked whether you want to run the nvidia-xconfig utility to update your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="eef10-120">После завершения установки скопируйте /etc/nvidia/gridd.conf.template в новый файл gridd.conf в расположении /etc/nvidia/.</span><span class="sxs-lookup"><span data-stu-id="eef10-120">After installation completes, copy /etc/nvidia/gridd.conf.template to a new file gridd.conf at location /etc/nvidia/</span></span>

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. <span data-ttu-id="eef10-121">Добавьте следующую строку в файл `/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="eef10-121">Add the following to `/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="eef10-122">Перезапустите виртуальную машину и приступите к проверке установки.</span><span class="sxs-lookup"><span data-stu-id="eef10-122">Reboot the VM and proceed to verify the installation.</span></span>


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="eef10-123">CentOS 7.3 или Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="eef10-123">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>


1. <span data-ttu-id="eef10-124">Обновите ядро и DKMS.</span><span class="sxs-lookup"><span data-stu-id="eef10-124">Update the kernel and DKMS.</span></span>
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. <span data-ttu-id="eef10-125">Отключите драйвер ядра Nouveau, который несовместим с драйвером NVIDIA.</span><span class="sxs-lookup"><span data-stu-id="eef10-125">Disable the Nouveau kernel driver, which is incompatible with the NVIDIA driver.</span></span> <span data-ttu-id="eef10-126">(На виртуальных машинах NV используйте только драйвер NVIDIA.) Чтобы сделать это, создайте в `/etc/modprobe.d ` файл с именем `nouveau.conf` со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="eef10-126">(Only use the NVIDIA driver on NV VMs.) To do this, create a file in `/etc/modprobe.d `named `nouveau.conf` with the following contents:</span></span>

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. <span data-ttu-id="eef10-127">Перезагрузите виртуальную машину, повторно подключитесь и установите последнюю версию служб интеграции Linux для Hyper-v.</span><span class="sxs-lookup"><span data-stu-id="eef10-127">Reboot the VM, reconnect, and install the latest Linux Integration Services for Hyper-V:</span></span>
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. <span data-ttu-id="eef10-128">Повторно подключитесь к виртуальной машине и выполните команду `lspci`.</span><span class="sxs-lookup"><span data-stu-id="eef10-128">Reconnect to the VM and run the `lspci` command.</span></span> <span data-ttu-id="eef10-129">Убедитесь, что карта или карты NVIDIA M60 отображаются как устройства PCI.</span><span class="sxs-lookup"><span data-stu-id="eef10-129">Verify that the NVIDIA M60 card or cards are visible as PCI devices.</span></span>
 
5. <span data-ttu-id="eef10-130">Загрузите и установите драйвер GRID.</span><span class="sxs-lookup"><span data-stu-id="eef10-130">Download and install the GRID driver:</span></span>

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. <span data-ttu-id="eef10-131">Когда появится запрос на запуск служебной программы nvidia-xconfig для обновления файла конфигурации X, выберите **Да**.</span><span class="sxs-lookup"><span data-stu-id="eef10-131">When you're asked whether you want to run the nvidia-xconfig utility to update your X configuration file, select **Yes**.</span></span>

7. <span data-ttu-id="eef10-132">После завершения установки скопируйте /etc/nvidia/gridd.conf.template в новый файл gridd.conf в расположении /etc/nvidia/.</span><span class="sxs-lookup"><span data-stu-id="eef10-132">After installation completes, copy /etc/nvidia/gridd.conf.template to a new file gridd.conf at location /etc/nvidia/</span></span>
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. <span data-ttu-id="eef10-133">Добавьте следующую строку в файл `/etc/nvidia/gridd.conf`:</span><span class="sxs-lookup"><span data-stu-id="eef10-133">Add the following to `/etc/nvidia/gridd.conf`:</span></span>
 
  ```
  IgnoreSP=TRUE
  ```
9. <span data-ttu-id="eef10-134">Перезапустите виртуальную машину и приступите к проверке установки.</span><span class="sxs-lookup"><span data-stu-id="eef10-134">Reboot the VM and proceed to verify the installation.</span></span>

### <a name="verify-driver-installation"></a><span data-ttu-id="eef10-135">Проверка установки драйверов</span><span class="sxs-lookup"><span data-stu-id="eef10-135">Verify driver installation</span></span>


<span data-ttu-id="eef10-136">Чтобы запросить состояние устройства GPU, установите SSH-подключение к виртуальной машине и запустите служебную программу командной строки [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface), установленную вместе с драйвером.</span><span class="sxs-lookup"><span data-stu-id="eef10-136">To query the GPU device state, SSH to the VM and run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span> 

<span data-ttu-id="eef10-137">Отобразятся выходные данные, аналогичные приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="eef10-137">Output similar to the following appears:</span></span>

![Состояние устройства NVIDIA](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a><span data-ttu-id="eef10-139">Сервер X11</span><span class="sxs-lookup"><span data-stu-id="eef10-139">X11 server</span></span>
<span data-ttu-id="eef10-140">Если вам требуется сервер X11 для удаленных подключений к виртуальной машине NV, рекомендуется использовать [x11vnc](http://www.karlrunge.com/x11vnc/), так как он поддерживает аппаратное ускорение графики.</span><span class="sxs-lookup"><span data-stu-id="eef10-140">If you need an X11 server for remote connections to an NV VM, [x11vnc](http://www.karlrunge.com/x11vnc/) is recommended because it allows hardware acceleration of graphics.</span></span> <span data-ttu-id="eef10-141">BusID устройства M60 необходимо вручную добавить в файл xconfig (`etc/X11/xorg.conf` в Ubuntu 16.04 LTS, `/etc/X11/XF86config` в CentOS 7.3 или Red Hat Enterprise Server 7.3).</span><span class="sxs-lookup"><span data-stu-id="eef10-141">The BusID of the M60 device must be manually added to the xconfig file (`etc/X11/xorg.conf` on Ubuntu 16.04 LTS, `/etc/X11/XF86config` on CentOS 7.3 or Red Hat Enterprise Server 7.3).</span></span> <span data-ttu-id="eef10-142">Добавьте раздел `"Device"`, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="eef10-142">Add a `"Device"` section similar to the following:</span></span>
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
<span data-ttu-id="eef10-143">Чтобы использовать это устройство, обновите раздел `"Screen"`.</span><span class="sxs-lookup"><span data-stu-id="eef10-143">Additionally, update your `"Screen"` section to use this device.</span></span>
 
<span data-ttu-id="eef10-144">BusID можно найти, выполнив</span><span class="sxs-lookup"><span data-stu-id="eef10-144">The BusID can be found by running</span></span>

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
<span data-ttu-id="eef10-145">BusID может измениться, если виртуальная машина будет перераспределена или перезагружена.</span><span class="sxs-lookup"><span data-stu-id="eef10-145">The BusID can change when a VM gets reallocated or rebooted.</span></span> <span data-ttu-id="eef10-146">Для обновления BusID в конфигурации X11 при перезагрузке виртуальной машины можно использовать скрипт.</span><span class="sxs-lookup"><span data-stu-id="eef10-146">Therefore, you may want to use a script to update the BusID in the X11 configuration when a VM is rebooted.</span></span> <span data-ttu-id="eef10-147">Например:</span><span class="sxs-lookup"><span data-stu-id="eef10-147">For example:</span></span>

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed to ${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

<span data-ttu-id="eef10-148">Этот файл можно вызывать с правами привилегированного пользователя во время загрузки, создав для него запись в `/etc/rc.d/rc3.d`.</span><span class="sxs-lookup"><span data-stu-id="eef10-148">This file can be invoked as root on boot by creating an entry for it in `/etc/rc.d/rc3.d`.</span></span>


## <a name="install-cuda-drivers-for-nc-vms"></a><span data-ttu-id="eef10-149">Установка драйверов CUDA для виртуальных машин серии NC</span><span class="sxs-lookup"><span data-stu-id="eef10-149">Install CUDA drivers for NC VMs</span></span>

<span data-ttu-id="eef10-150">Ниже приведены инструкции по установке драйверов NVIDIA из набора средств NVIDIA CUDA Toolkit 8.0 на виртуальные машины NC под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="eef10-150">Here are steps to install NVIDIA drivers on Linux NC VMs from the NVIDIA CUDA Toolkit 8.0.</span></span> 

<span data-ttu-id="eef10-151">Разработчики на языках C и C++ могут дополнительно установить полный набор средств для создания приложений, использующих ускорение на GPU.</span><span class="sxs-lookup"><span data-stu-id="eef10-151">C and C++ developers can optionally install the full Toolkit to build GPU-accelerated applications.</span></span> <span data-ttu-id="eef10-152">Дополнительные сведения см. в [руководстве по установке CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span><span class="sxs-lookup"><span data-stu-id="eef10-152">For more information, see the [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).</span></span>


> [!NOTE]
> <span data-ttu-id="eef10-153">Предоставленные в статье ссылки для скачивания драйверов CUDA актуальны на момент ее публикации.</span><span class="sxs-lookup"><span data-stu-id="eef10-153">CUDA driver download links provided here are current at time of publication.</span></span> <span data-ttu-id="eef10-154">Последние версии драйверов CUDA можно получить на веб-сайте [NVIDIA](http://www.nvidia.com/).</span><span class="sxs-lookup"><span data-stu-id="eef10-154">For the latest CUDA drivers, visit the [NVIDIA](http://www.nvidia.com/) website.</span></span>
>

<span data-ttu-id="eef10-155">Чтобы установить набор средств CUDA, установите SSH-подключение к каждой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="eef10-155">To install CUDA Toolkit, make an SSH connection to each VM.</span></span> <span data-ttu-id="eef10-156">Убедитесь, что в системе есть графический процессор с архитектурой CUDA, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="eef10-156">To verify that the system has a CUDA-capable GPU, run the following command:</span></span>

```bash
lspci | grep -i NVIDIA
```
<span data-ttu-id="eef10-157">Вы увидите данные, похожие на следующий пример (для адаптера NVIDIA Tesla K80):</span><span class="sxs-lookup"><span data-stu-id="eef10-157">You will see output similar to the following example (showing an NVIDIA Tesla K80 card):</span></span>

![результаты выполнения команды lspci](./media/n-series-driver-setup/lspci.png)

<span data-ttu-id="eef10-159">Затем выполните команды установки, относящиеся к используемому дистрибутиву.</span><span class="sxs-lookup"><span data-stu-id="eef10-159">Then run installation commands specific for your distribution.</span></span>

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="eef10-160">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="eef10-160">Ubuntu 16.04 LTS</span></span>

1. <span data-ttu-id="eef10-161">Скачайте и установите драйверы CUDA.</span><span class="sxs-lookup"><span data-stu-id="eef10-161">Download and install the CUDA drivers.</span></span>
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  <span data-ttu-id="eef10-162">Установка может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="eef10-162">The installation can take several minutes.</span></span>

2. <span data-ttu-id="eef10-163">Чтобы дополнительно установить полный набор средств CUDA, введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="eef10-163">To optionally install the complete CUDA toolkit, type:</span></span>

  ```bash
  sudo apt-get install cuda
  ```

3. <span data-ttu-id="eef10-164">Перезапустите виртуальную машину и приступите к проверке установки.</span><span class="sxs-lookup"><span data-stu-id="eef10-164">Reboot the VM and proceed to verify the installation.</span></span>

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="eef10-165">CentOS 7.3 или Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="eef10-165">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

1. <span data-ttu-id="eef10-166">Получите обновления.</span><span class="sxs-lookup"><span data-stu-id="eef10-166">Get updates.</span></span> 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. <span data-ttu-id="eef10-167">Подключитесь к виртуальной машине и установите последнюю версию Linux Integration Services для Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="eef10-167">Reconnect to the VM and install the latest Linux Integration Services for Hyper-V.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="eef10-168">Если вы установили на виртуальную машину NC24r образ HPC на основе CentOS, перейдите к шагу 3.</span><span class="sxs-lookup"><span data-stu-id="eef10-168">If you installed a CentOS-based HPC image on an NC24r VM, skip to Step 3.</span></span> <span data-ttu-id="eef10-169">Поскольку драйверы Azure RDMA и службы интеграции Linux предварительно установлены в образ, служба интеграции Linux не обновляется и обновления ядра отключены по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="eef10-169">Because Azure RDMA drivers and Linux Integration Services are pre-installed in the image, LIS should not be upgraded, and kernel updates are disabled by default.</span></span>
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. <span data-ttu-id="eef10-170">Повторно подключитесь к виртуальной машине и продолжите установку с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="eef10-170">Reconnect to the VM and continue installation with the following commands:</span></span>

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

  <span data-ttu-id="eef10-171">Установка может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="eef10-171">The installation can take several minutes.</span></span> 

4. <span data-ttu-id="eef10-172">Чтобы дополнительно установить полный набор средств CUDA, введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="eef10-172">To optionally install the complete CUDA toolkit, type:</span></span>

  ```bash
  sudo yum install cuda
  ```

5. <span data-ttu-id="eef10-173">Перезапустите виртуальную машину и приступите к проверке установки.</span><span class="sxs-lookup"><span data-stu-id="eef10-173">Reboot the VM and proceed to verify the installation.</span></span>


### <a name="verify-driver-installation"></a><span data-ttu-id="eef10-174">Проверка установки драйверов</span><span class="sxs-lookup"><span data-stu-id="eef10-174">Verify driver installation</span></span>


<span data-ttu-id="eef10-175">Чтобы запросить состояние устройства GPU, установите SSH-подключение к виртуальной машине и запустите служебную программу командной строки [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface), установленную вместе с драйвером.</span><span class="sxs-lookup"><span data-stu-id="eef10-175">To query the GPU device state, SSH to the VM and run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span> 

<span data-ttu-id="eef10-176">Отобразятся выходные данные, аналогичные приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="eef10-176">Output similar to the following appears:</span></span>

![Состояние устройства NVIDIA](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a><span data-ttu-id="eef10-178">Обновления драйверов CUDA</span><span class="sxs-lookup"><span data-stu-id="eef10-178">CUDA driver updates</span></span>

<span data-ttu-id="eef10-179">Рекомендуется периодически обновлять драйверы CUDA после развертывания.</span><span class="sxs-lookup"><span data-stu-id="eef10-179">We recommend that you periodically update CUDA drivers after deployment.</span></span>

#### <a name="ubuntu-1604-lts"></a><span data-ttu-id="eef10-180">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="eef10-180">Ubuntu 16.04 LTS</span></span>

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a><span data-ttu-id="eef10-181">CentOS 7.3 или Red Hat Enterprise Linux 7.3</span><span class="sxs-lookup"><span data-stu-id="eef10-181">CentOS-based 7.3 or Red Hat Enterprise Linux 7.3</span></span>

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a><span data-ttu-id="eef10-182">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="eef10-182">Troubleshooting</span></span>

* <span data-ttu-id="eef10-183">Может возникать известная проблема, связанная с работой драйверов CUDA на виртуальных машинах Azure серии N под управлением ядра Linux версии 4.4.0-75 на Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="eef10-183">There is a known issue with CUDA drivers on Azure N-series VMs running the 4.4.0-75 Linux kernel on Ubuntu 16.04 LTS.</span></span> <span data-ttu-id="eef10-184">Если вы обновляете более раннюю версию ядра, обновите ее как минимум до версии 4.4.0-77.</span><span class="sxs-lookup"><span data-stu-id="eef10-184">If you are upgrading from an earlier kernel version, upgrade to at least kernel version 4.4.0-77.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="eef10-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eef10-185">Next steps</span></span>

* <span data-ttu-id="eef10-186">Дополнительные сведения о графических процессорах NVIDIA в виртуальных машинах серии N см. в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="eef10-186">For more information about the NVIDIA GPUs on the N-series VMs, see:</span></span>
    * <span data-ttu-id="eef10-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (для виртуальных машин Azure серии NC);</span><span class="sxs-lookup"><span data-stu-id="eef10-187">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="eef10-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (для виртуальных машин Azure серии NV).</span><span class="sxs-lookup"><span data-stu-id="eef10-188">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="eef10-189">Чтобы записать образ виртуальной машины Linux с установленными драйверами NVIDIA, см. статью [Как подготовить к работе и записать образ виртуальной машины Linux](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eef10-189">To capture a Linux VM image with your installed NVIDIA drivers, see [How to generalize and capture a Linux virtual machine](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
