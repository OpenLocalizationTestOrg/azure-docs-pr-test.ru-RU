---
title: "пропускная способность сети виртуальной Машины aaaOptimize | Документы Microsoft"
description: "Узнайте, как виртуальная машина Azure toooptimize сетевой пропускной способности."
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
ms.date: 07/24/2017
ms.author: steveesp
ms.openlocfilehash: a5cff2d0ab6e3553c3f90d99629521a431477de0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a>Оптимизации пропускной способности сети для виртуальной машины Azure

Виртуальные машины Azure имеют сетевые параметры по умолчанию, с помощью которых можно дополнительно оптимизировать пропускную способность сети. В этой статье описывается, как toooptimize сетевой пропускной способности для Microsoft Azure Windows и виртуальных машин Linux, включая основные распределения, например Ubuntu, CentOS и Red Hat.

## <a name="windows-vm"></a>Виртуальная машина Windows

Если ВМ Windows поддерживается с [Accelerated сети](virtual-network-create-vm-accelerated-networking.md), включение этой функции будет hello оптимальную конфигурацию для пропускной способности. Остальные виртуальные машины Windows, использующие масштабирование размера приема (RSS), могут иметь большую максимальную пропускную способность, чем виртуальная машина без RSS. По умолчанию функция RSS может быть отключена на виртуальной машине Windows. Выполните следующие шаги toodetermine RSS, включен ли hello и tooenable его, если она отключена.

1. Введите hello `Get-NetAdapterRss` toosee команду PowerShell, если для сетевого адаптера включена технология RSS. В hello следующий пример выходных данных, возвращенные hello `Get-NetAdapterRss`, не включена технология RSS.

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. Введите следующие команды tooenable RSS hello:

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    Предыдущая команда Hello не имеет выходных данных. Команда Hello изменить параметры сетевого Адаптера, вызывая потери подключения временных около одной минуты. Диалоговое окно Reconnecting отображается во время потери подключения hello. Обычно восстановление подключения после попытки третий hello.
3. Убедитесь, что RSS включена в hello виртуальной Машины, введя hello `Get-NetAdapterRss` еще раз. В случае успешного выполнения возвращается hello следующий пример выходных данных:

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a>Виртуальная машина Linux

Функция RSS по умолчанию всегда включена на виртуальной машине Azure по управлением Linux. Ядро Linux, выпущенные после января 2017 г. включает новые параметры оптимизации сети, позволяющие виртуальной Машине Linux tooachieve выше пропускную способность сети.

### <a name="ubuntu"></a>Ubuntu

В порядке tooget hello оптимизации необходимо сначала обновите версию toohello последней поддерживается, начиная с июня 2017 г., который является:
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
После завершения обновления hello, введите следующие команды tooget hello последнюю ядра hello:

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

Необязательная команда:

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a>Ядро предварительной версии Azure Ubuntu
> [!WARNING]
> Эта предварительная версия Linux Azure ядра не может иметь hello того же уровня доступности и надежности Marketplace образов и ядра, в целом доступности выпуска. функция Hello не поддерживается, могут ограничены возможности и не может быть как можно надежней ядра по умолчанию hello. Не используйте это ядро для производственных задач.

Значительно пропускную способность производительности достигается путем установки hello предложенные ядра Azure Linux. tootry этот ядра, добавьте этот too/etc/apt/sources.list строки

```bash
#add this toohello end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

Затем выполните следующие команды (требуется доступ с правами root):
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a>CentOS

В порядке tooget hello оптимизации необходимо сначала обновите версию toohello последней поддерживается, начиная с июля 2017 г., который является:
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
После завершения обновления hello установки hello последние службы интеграции Linux (LIS).
оптимизации пропускной способности Hello находится в LIS, начиная с 4.2.2-2. Введите следующие команды tooinstall LIS hello:

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a>Red Hat

В порядке tooget hello оптимизации необходимо сначала обновите версию toohello последней поддерживается, начиная с июля 2017 г., который является:
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
После завершения обновления hello установки hello последние службы интеграции Linux (LIS).
оптимизации пропускной способности Hello находится в LIS, начиная с 4.2. Введите следующие команды toodownload hello и устанавливать LIS:

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

Дополнительные сведения о 4.2 версию служб интеграции Linux для Hyper-V, просмотрев hello [страница загрузки](https://www.microsoft.com/download/details.aspx?id=55106).

## <a name="next-steps"></a>Дальнейшие действия
* Hello ВМ оптимизирован, см. статью hello результат с [пропускной способности и пропускной способности тестирования виртуальной Машины Azure](virtual-network-bandwidth-testing.md) для вашего сценария.
* Дополнительные сведения см. в статье [Виртуальная сеть Azure: часто задаваемые вопросы](virtual-networks-faq.md).
