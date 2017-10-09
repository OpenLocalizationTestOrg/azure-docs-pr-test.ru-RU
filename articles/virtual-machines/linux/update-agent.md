---
title: "aaaUpdate hello Azure Linux Agent из GitHub | Документы Microsoft"
description: "Узнайте, как tooupdate агент Azure Linux для ВМ Linux в последней версии Azure toohello из GitHub"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: f1f19300-987d-4f29-9393-9aba866f049c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: mingzhan
ms.openlocfilehash: 4ce7c56efc1e6563e6415f7687573f9fb9e7b4c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-hello-azure-linux-agent-on-a-vm"></a>Как tooupdate hello агент Azure Linux на виртуальной Машине

tooupdate вашей [агент Azure Linux](https://github.com/Azure/WALinuxAgent) на виртуальной Машине Linux в Azure, необходимо иметь:

- работающая виртуальная машина Linux в Azure;
- Toothat подключение виртуальных Машин Linux с помощью SSH.

Всегда следует выполнять проверку для пакета в репозитории дистрибутив Linux hello сначала. Возможно доступен пакет hello не может быть hello последнюю версию, однако разрешение автоматическое обновление гарантирует hello агент Linux, всегда получают hello последнее обновление. При возникновении проблем при установке из hello диспетчеров пакетов, необходимо найти поддержки поставщика дистрибутив hello.

## <a name="updating-hello-azure-linux-agent"></a>Обновление hello Azure Linux Agent

## <a name="ubuntu"></a>Ubuntu

#### <a name="check-your-current-package-version"></a>Проверка текущей версии пакета

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a>Обновление кэша пакета

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Установите последнюю версию пакета hello

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a>Гарантия включения автоматического обновления

Во-первых проверьте toosee, если он включен:

```bash
cat /etc/waagent.conf
```

Найдите параметр AutoUpdate.Enabled. Если отображаются следующие результаты, значит эта возможность включена:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable запуска:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Перезапустите службу waagent hello

#### <a name="restart-agent-for-1404"></a>Перезапуск агента для версии 14.04

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a>Перезапуск агента для версии 16.04, 17.04

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a>Debian

### <a name="debian-7-wheezy"></a>Debian 7 "Wheezy"

#### <a name="check-your-current-package-version"></a>Проверка текущей версии пакета

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a>Обновление кэша пакета

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Установите последнюю версию пакета hello

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a>Включение автоматического обновления агента
В этой версии Debian нет версии агента не ниже 2.0.16, поэтому для нее недоступно автоматическое обновление. Hello вывод hello выше команду Показать, если пакет hello актуален.

### <a name="debian-8-jessie--debian-9-stretch"></a>Debian 8 "Jessie" и Debian 9 "Stretch"

#### <a name="check-your-current-package-version"></a>Проверка текущей версии пакета

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a>Обновление кэша пакета

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a>Установите последнюю версию пакета hello

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a>Гарантия включения автоматического обновления 

Во-первых проверьте toosee, если он включен:

```bash
cat /etc/waagent.conf
```

Найдите параметр AutoUpdate.Enabled. Если отображаются следующие результаты, значит эта возможность включена:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable запуска:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Перезапустите службу waagent hello

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a>RedHat или CentOS

### <a name="rhelcentos-6"></a>RHEL или CentOS 6

#### <a name="check-your-current-package-version"></a>Проверка текущей версии пакета

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a>Проверка доступных обновлений

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a>Установите последнюю версию пакета hello

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a>Гарантия включения автоматического обновления 

Во-первых проверьте toosee, если он включен:

```bash
cat /etc/waagent.conf
```

Найдите параметр AutoUpdate.Enabled. Если отображаются следующие результаты, значит эта возможность включена:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable запуска:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Перезапустите службу waagent hello

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a>RHEL или CentOS 7

#### <a name="check-your-current-package-version"></a>Проверка текущей версии пакета

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a>Проверка доступных обновлений

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a>Установите последнюю версию пакета hello

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a>Гарантия включения автоматического обновления 

Во-первых проверьте toosee, если он включен:

```bash
cat /etc/waagent.conf
```

Найдите параметр AutoUpdate.Enabled. Если отображаются следующие результаты, значит эта возможность включена:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable запуска:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Перезапустите службу waagent hello

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a>SUSE SLES

### <a name="suse-sles-11-sp4"></a>SUSE SLES 11 SP4

#### <a name="check-your-current-package-version"></a>Проверка текущей версии пакета

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a>Проверка доступных обновлений

Hello выше выходных данных будет показано, если пакет hello работает toodate.

#### <a name="install-hello-latest-package-version"></a>Установите последнюю версию пакета hello

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a>Гарантия включения автоматического обновления 

Во-первых проверьте toosee, если он включен:

```bash
cat /etc/waagent.conf
```

Найдите параметр AutoUpdate.Enabled. Если отображаются следующие результаты, значит эта возможность включена:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable запуска:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Перезапустите службу waagent hello

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a>SUSE SLES 12 SP2

#### <a name="check-your-current-package-version"></a>Проверка текущей версии пакета

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a>Проверка доступных обновлений

В выходных данных hello hello выше здесь вы найдете Если пакет hello не требует обновления.

#### <a name="install-hello-latest-package-version"></a>Установите последнюю версию пакета hello

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a>Гарантия включения автоматического обновления 

Во-первых проверьте toosee, если он включен:

```bash
cat /etc/waagent.conf
```

Найдите параметр AutoUpdate.Enabled. Если отображаются следующие результаты, значит эта возможность включена:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable запуска:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a>Перезапустите службу waagent hello

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a>Oracle 6 и 7

Oracle Linux, убедитесь, что hello `Addons` репозитория включена. Выберите файл hello tooedit `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) или `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux) и измените строку hello `enabled=0` слишком`enabled=1` под **[ol6_addons]** или **[ol7_addons]** в этом файле.

Затем tooinstall hello последнюю версию hello Azure Linux Agent типа:

```bash
sudo yum install WALinuxAgent
```

Если вы не нашли репозитория hello надстройку можно просто добавить эти строки в конце hello файла .repo tooyour Oracle Linux выпуск в соответствии с:

Для виртуальных машин Oracle Linux 6.

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

Для виртуальных машин Oracle Linux 7.

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

Затем введите следующую команду:

```bash
sudo yum update WALinuxAgent
```

Обычно это все, что требуется, но если для какой-либо причине требуется tooinstall из https://github.com напрямую, hello используйте следующие шаги.


## <a name="update-hello-linux-agent-when-no-agent-package-exists-for-distribution"></a>Обновить агент Linux hello существование без агента пакета для распространения

Для установки wget (отсутствуют некоторые дистрибутивы, не устанавливайте значение по умолчанию, например Redhat CentOS и Oracle Linux версии 6.4 и 6.5) введите `sudo yum install wget` hello в командной строке.

### <a name="1-download-hello-latest-version"></a>1. Загрузка последней версии hello
Откройте [hello выпуска Azure Linux Agent в GitHub](https://github.com/Azure/WALinuxAgent/releases) в веб-страницы, а также узнать номер последней версии hello. (Номер текущей версии можно узнать, введя `waagent --version`.)

#### <a name="for-version-22x-or-later-type"></a>Для версии 2.2.x или более поздней версии введите:
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

Hello следующую строку версии 2.2.0 в качестве примера используется:

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-hello-azure-linux-agent"></a>2. Установите агент Azure Linux hello

#### <a name="for-version-22x-use"></a>Для версии 2.2.x введите:
Может потребоваться пакет hello tooinstall `setuptools` сначала — в разделе [здесь](https://pypi.python.org/pypi/setuptools). Далее выполните:

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a>Гарантия включения автоматического обновления

Во-первых проверьте toosee, если он включен:

```bash
cat /etc/waagent.conf
```

Найдите параметр AutoUpdate.Enabled. Если отображаются следующие результаты, значит эта возможность включена:

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

tooenable запуска:

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-hello-waagent-service"></a>3. Перезапустите службу waagent hello
Для большинства дистрибутивов Linux:

```bash
sudo service waagent restart
```

Для Ubuntu используйте:

```bash
sudo service walinuxagent restart
```

Для CoreOS используйте:

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-hello-azure-linux-agent-version"></a>4. Проверить версию агента Azure Linux hello
    
```bash
waagent -version
```

Для CoreOS hello выше команды может не работать.

Вы увидите, что hello Azure Linux Agent версия была обновленных toohello новой версии.

Дополнительные сведения о hello агент Azure Linux см. в разделе [README агента Azure Linux](https://github.com/Azure/WALinuxAgent).
