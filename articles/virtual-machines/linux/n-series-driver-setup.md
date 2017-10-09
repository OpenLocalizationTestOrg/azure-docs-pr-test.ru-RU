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
# <a name="install-nvidia-gpu-drivers-on-n-series-vms-running-linux"></a>Установка драйверов GPU NVIDIA на виртуальные машины серии N под управлением Linux

преимущества tootake работы GPU hello Azure N-й серии виртуальных машин под управлением Linux, установите поддерживаемые NVIDIA графические драйверы. В этой статье приводятся действия по установке драйверов после развертывания виртуальных машин серии N. Сведения об установке драйверов также доступны для [виртуальных машин Windows](../windows/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


Характеристики виртуальных машин серии N, сведения о дисках и объеме памяти см. в статье [Размеры виртуальных машин Linux, оптимизированных для GPU](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 



[!INCLUDE [virtual-machines-n-series-linux-support](../../../includes/virtual-machines-n-series-linux-support.md)]

## <a name="install-grid-drivers-for-nv-vms"></a>Установка драйверов GRID для виртуальных машин NV

драйверы tooinstall NVIDIA СЕТКИ на виртуальных машинах NV, сделать tooeach подключения SSH виртуальной Машины и выполните действия hello для дистрибутива Linux. 

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

1. Запустите hello `lspci` команды. Убедитесь, что hello NVIDIA M60 карты или карты отображаются как устройства PCI.

2. Установите обновления.

  ```bash
  sudo apt-get update

  sudo apt-get upgrade -y

  sudo apt-get dist-upgrade -y

  sudo apt-get install build-essential ubuntu-desktop -y
  ```
3. Отключение драйвера ядра Nouveau hello, которая несовместима с драйвером NVIDIA hello. (Только используйте драйвер NVIDIA hello на виртуальных машинах NV). toodo это, создайте файл в `/etc/modprobe.d `с именем `nouveau.conf` с hello после содержимого:

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```


4. Перезагрузите компьютер hello виртуальной Машины и повторного подключения. Выйдите из X-сервера:

  ```bash
  sudo systemctl stop lightdm.service
  ```

5. Загрузите и установите драйвер hello СЕТКИ.

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 

6. В ответ на запрос, следует ли toorun hello nvidia xconfig программа tooupdate X файла конфигурации, выберите **Да**.

7. После завершения установки, скопируйте gridd.conf tooa новый /etc/nvidia/gridd.conf.template файл в расположение/etc/nvidia /

  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```

8. Добавьте hello слишком следующие`/etc/nvidia/gridd.conf`:
 
  ```
  IgnoreSP=TRUE
  ```
9. Перезагрузите компьютер hello виртуальной Машины и продолжить установку tooverify hello.


### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>CentOS 7.3 или Red Hat Enterprise Linux 7.3


1. Обновление ядра hello и DKMS.
 
  ```bash  
  sudo yum update
 
  sudo yum install kernel-devel
 
  sudo rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
 
  sudo yum install dkms
  ```

2. Отключение драйвера ядра Nouveau hello, которая несовместима с драйвером NVIDIA hello. (Только используйте драйвер NVIDIA hello на виртуальных машинах NV). toodo это, создайте файл в `/etc/modprobe.d `с именем `nouveau.conf` с hello после содержимого:

  ```
  blacklist nouveau

  blacklist lbm-nouveau
  ```
 
3. Перезагрузите hello ВМ, повторно подключиться и установите последнюю версию служб интеграции Linux для Hyper-V: hello
 
  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
 
  tar xvzf lis-rpms-4.2.2-2.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
4. Подключите toohello виртуальной Машины и выполнить hello `lspci` команды. Убедитесь, что hello NVIDIA M60 карты или карты отображаются как устройства PCI.
 
5. Загрузите и установите драйвер hello СЕТКИ.

  ```bash
  wget -O NVIDIA-Linux-x86_64-367.106-grid.run https://go.microsoft.com/fwlink/?linkid=849941  

  chmod +x NVIDIA-Linux-x86_64-367.106-grid.run

  sudo ./NVIDIA-Linux-x86_64-367.106-grid.run
  ``` 
6. В ответ на запрос, следует ли toorun hello nvidia xconfig программа tooupdate X файла конфигурации, выберите **Да**.

7. После завершения установки, скопируйте gridd.conf tooa новый /etc/nvidia/gridd.conf.template файл в расположение/etc/nvidia /
  
  ```bash
  sudo cp /etc/nvidia/gridd.conf.template /etc/nvidia/gridd.conf
  ```
  
8. Добавьте hello слишком следующие`/etc/nvidia/gridd.conf`:
 
  ```
  IgnoreSP=TRUE
  ```
9. Перезагрузите компьютер hello виртуальной Машины и продолжить установку tooverify hello.

### <a name="verify-driver-installation"></a>Проверка установки драйверов


tooquery hello состояния устройств GPU, SSH toohello ВМ и выполнения hello [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) программа устанавливается вместе с драйвером hello. 

Появится примерно toohello следующие выходные данные:

![Состояние устройства NVIDIA](./media/n-series-driver-setup/smi-nv.png)
 

### <a name="x11-server"></a>Сервер X11
Если вам требуется X11 сервера для удаленных подключений tooan ВМ NV [x11vnc](http://www.karlrunge.com/x11vnc/) рекомендуется, так как она допускает аппаратное ускорение графики. Hello BusID hello M60 устройства необходимо вручную добавить файл xconfig toohello (`etc/X11/xorg.conf` на Ubuntu 16.04 LTS, `/etc/X11/XF86config` на CentOS 7.3 или Red Hat Enterprise Server 7.3). Добавить `"Device"` статьи аналогичные toohello следующее:
 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "Tesla M60"
    BusID          "your-BusID:0:0:0"
EndSection
```
 
Кроме того, обновить ваш `"Screen"` статьи toouse это устройство.
 
Hello BusID можно найти, выполнив

```bash
/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1
```
 
Hello BusID можно изменить, если виртуальная машина получает перераспределить или перезагрузки. Таким образом вы можете toouse hello tooupdate сценарий BusID в конфигурации hello X11 при перезагрузке виртуальной Машины. Например:

```bash 
#!/bin/bash
BUSID=$((16#`/usr/bin/nvidia-smi --query-gpu=pci.bus_id --format=csv | tail -1 | cut -d ':' -f 1`))

if grep -Fxq "${BUSID}" /etc/X11/XF86Config; then     echo "BUSID is matching"; else   echo "BUSID changed too${BUSID}" && sed -i '/BusID/c\    BusID          \"PCI:0@'${BUSID}':0:0:0\"' /etc/X11/XF86Config; fi
```

Этот файл можно вызывать с правами привилегированного пользователя во время загрузки, создав для него запись в `/etc/rc.d/rc3.d`.


## <a name="install-cuda-drivers-for-nc-vms"></a>Установка драйверов CUDA для виртуальных машин серии NC

Вот драйверы NVIDIA tooinstall действия на виртуальных машинах Linux NC из hello NVIDIA CUDA Toolkit 8.0. 

Разработчикам C и C++ можно также установить hello полный набор средств toobuild ускорением GPU приложений. Дополнительные сведения см. в разделе hello [руководство по установке CUDA](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html).


> [!NOTE]
> Предоставленные в статье ссылки для скачивания драйверов CUDA актуальны на момент ее публикации. Последние версии драйверов CUDA hello, на сайте hello [NVIDIA](http://www.nvidia.com/) веб-сайта.
>

tooinstall CUDA Toolkit сделать tooeach подключения SSH виртуальной Машины. tooverify, hello система имеет поддержкой CUDA GPU, запустите следующую команду hello.

```bash
lspci | grep -i NVIDIA
```
Вы увидите примерно toohello вывода следующий пример (показывающее плату NVIDIA Tesla K80):

![результаты выполнения команды lspci](./media/n-series-driver-setup/lspci.png)

Затем выполните команды установки, относящиеся к используемому дистрибутиву.

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

1. Загрузите и установите драйвер CUDA hello.
  ```bash
  CUDA_REPO_PKG=cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

  wget -O /tmp/${CUDA_REPO_PKG} http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/${CUDA_REPO_PKG} 

  sudo dpkg -i /tmp/${CUDA_REPO_PKG}

  rm -f /tmp/${CUDA_REPO_PKG}

  sudo apt-get update

  sudo apt-get install cuda-drivers

  ```

  Hello установка может занять несколько минут.

2. toooptionally установки hello завершения CUDA набор средств, тип:

  ```bash
  sudo apt-get install cuda
  ```

3. Перезагрузите компьютер hello виртуальной Машины и продолжить установку tooverify hello.

### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>CentOS 7.3 или Red Hat Enterprise Linux 7.3

1. Получите обновления. 

  ```bash
  sudo yum update

  sudo reboot
  ```
2. Подключите toohello ВМ и установить hello последнюю версию служб интеграции Linux для Hyper-V.

  > [!IMPORTANT]
  > При установке образа на основе CentOS HPC на Виртуальной машине NC24r пропустите tooStep 3. Поскольку драйверы Azure RDMA и службы интеграции Linux предварительно установлен в образе hello, LIS не обновляются и обновлений ядра отключены по умолчанию.
  >

  ```bash
  wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.1.tar.gz
 
  tar xvzf lis-rpms-4.2.1.tar.gz
 
  cd LISISO
 
  sudo ./install.sh
 
  sudo reboot
  ```
 
3. Переподключение toohello ВМ и продолжите установку hello, следующие команды:

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

  Hello установка может занять несколько минут. 

4. toooptionally установки hello завершения CUDA набор средств, тип:

  ```bash
  sudo yum install cuda
  ```

5. Перезагрузите компьютер hello виртуальной Машины и продолжить установку tooverify hello.


### <a name="verify-driver-installation"></a>Проверка установки драйверов


tooquery hello состояния устройств GPU, SSH toohello ВМ и выполнения hello [nvidia smi](https://developer.nvidia.com/nvidia-system-management-interface) программа устанавливается вместе с драйвером hello. 

Появится примерно toohello следующие выходные данные:

![Состояние устройства NVIDIA](./media/n-series-driver-setup/smi.png)


### <a name="cuda-driver-updates"></a>Обновления драйверов CUDA

Рекомендуется периодически обновлять драйверы CUDA после развертывания.

#### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS

```bash
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get dist-upgrade -y

sudo apt-get install cuda-drivers

sudo reboot
```


#### <a name="centos-based-73-or-red-hat-enterprise-linux-73"></a>CentOS 7.3 или Red Hat Enterprise Linux 7.3

```bash
sudo yum update

sudo reboot
```



## <a name="troubleshooting"></a>Устранение неполадок

* Имеется известная проблема с драйверами CUDA на ОС Linux ядра hello 4.4.0-75 Ubuntu 16.04 LTS виртуальных машинах Azure N-й серии. При обновлении с более ранней версии ядра обновление tooat наименьших 4.4.0-77 версию ядра. 



## <a name="next-steps"></a>Дальнейшие действия

* Дополнительные сведения о графических процессоров NVIDIA hello hello N-й серии виртуальных машин см.:
    * [NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (для виртуальных машин Azure серии NC);
    * [NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (для виртуальных машин Azure серии NV).

* образ ВМ Linux с вашей установленные драйверы NVIDIA toocapture. в разделе [как toogeneralize и записать виртуальную машину Linux](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
