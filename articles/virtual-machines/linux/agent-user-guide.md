---
title: "Общие сведения об агенте виртуальной Машины Linux aaaAzure | Документы Microsoft"
description: "Узнайте, как tooinstall и настроить агент для Linux (waagent) toomanage взаимодействие виртуальной машины с Azure Fabric Controller."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: e41de979-6d56-40b0-8916-895bf215ded6
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: szark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4e08c84d9205f4db7aae6fd1568ec1f15fba395c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-and-using-hello-azure-linux-agent"></a>Понимание и использование hello Azure Linux Agent
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a>Введение
Hello Microsoft Azure Linux Agent (waagent) управляет Linux и FreeBSD подготовки и взаимодействие виртуальной Машины с hello Azure Fabric Controller. Он предоставляет следующие функциональные возможности для развертывания ОС Linux и FreeBSD IaaS hello:

> [!NOTE]
> Разделе hello Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) для получения дополнительных сведений.
> 
> 

* **Подготовка образа**
  
  * Создание учетной записи пользователя
  * Настройка типов аутентификации SSH
  * Развертывание открытых ключей SSH и пар ключей
  * Параметр имени узла hello
  * Имя узла публикации hello – платформа toohello DNS
  * Reporting платформа toohello отпечаток ключа SSH узла
  * Управление диском ресурсов
  * Форматирование и подключении диска ресурсов hello
  * Настройка пространства подкачки
* **Сеть**
  
  * Управляет маршруты tooimprove совместимости с платформой DHCP-серверами
  * Обеспечивает стабильность hello hello имя сетевого интерфейса
* **Ядро**
  
  * Настраивает виртуальную архитектуру NUMA (отключить для ядра версий ранее 2.6.37).
  * Использование энтропии Hyper-V для /dev/random
  * Настраивает время ожидания SCSI для hello Корневое устройство (это может быть удаленный)
* **Диагностика**
  
  * Консоль перенаправления toohello последовательного порта
* **Развернутые приложения SCVMM**
  
  * Обнаруживает и загружает hello агент VMM для Linux при выполнении в среде System Center Virtual Machine Manager 2012 R2
* **Расширение виртуальной машины**
  
  * Вставить компонент, написанный корпорацией Майкрософт и партнерами в автоматизации tooenable программному обеспечению и конфигурации ВМ Linux (IaaS)
  * Эталонная реализация расширения виртуальной машины на сайте [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)

## <a name="communication"></a>Обмен данными
Hello потоком данных, передаваемых из агента toohello hello выполняется с помощью двух каналов:

* Прилагаемый DVD, используемый во время загрузки, для развернутых приложений IaaS. Этот DVD-ДИСК содержит OVF-совместимый файл конфигурации, который включает все сведения об инициализации, кроме hello, фактический пары ключей SSH.
* Предоставление доступа к REST API конечной точке TCP используется tooobtain развертывания и настройки топологии.

## <a name="requirements"></a>Требования
Hello следующих систем были протестированы и известны toowork с hello агент Azure Linux:

> [!NOTE]
> Этот список может отличаться от hello официальный список поддерживаемых систем на платформе Microsoft Azure hello, как описано здесь: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)
> 
> 

* CoreOS
* CentOS 6.3+
* Red Hat Enterprise Linux 6.7 и более поздней версии
* Debian 7.0+
* Ubuntu 12.04+
* openSUSE 12.3+
* SLES 11 SP3+
* Oracle Linux 6.4+

Другие поддерживаемые системы:

* FreeBSD 10 и более поздней версии (агент Linux для Azure 2.0.10 и более поздней версии)

Некоторые пакеты системы в порядке toofunction зависит агент Linux Hello должным образом.

* Python 2.6+
* OpenSSL 1.0 и более поздней версии
* OpenSSH 5.3 и более поздней версии
* Служебные программы файловой системы: sfdisk, fdisk, mkfs, parted
* Инструменты работы с паролями: chpasswd, sudo
* Инструменты обработки текста: sed, grep
* Сетевые инструменты: ip-route
* Поддержка ядра для монтирования файловых систем UDF.

## <a name="installation"></a>Установка
Установку, используя RPM или DEB пакета из репозитория пакетов на распределение — hello предпочитаемый метод установки и обновления hello Azure Linux Agent. Все hello [одобренных поставщиков распространения](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) интегрировать пакет агента Azure Linux hello в их репозиториев и изображения.

См. документацию toohello в hello [репозитория агент Azure Linux на GitHub](https://github.com/Azure/WALinuxAgent) для установки дополнительных параметров, например Установка из источника или toocustom расположений или префиксов.

## <a name="command-line-options"></a>Параметры командной строки
### <a name="flags"></a>Флаги
* verbose: расширить указанную команду
* force: пропустить интерактивные подтверждения для некоторых команд

### <a name="commands"></a>Команды
* Справка: список команд hello поддерживается и флаги.
* отзыв: попытка tooclean hello системы и соответствующих повторно подготовки. Эта операция удалены hello следующее:
  
  * Все ключи SSH узла (если Provisioning.RegenerateSshHostKeyPair «y» в файле конфигурации hello)
  * Настройка имени сервера в /etc/resolv.conf
  * Пароль учетной записи root в/etc/shadow (если Provisioning.DeleteRootPassword «y» в файле конфигурации hello)
  * Кэшированные аренды DHCP-клиентов
  * Сброс размещения toolocalhost.localdomain имя

> [!WARNING]
> Отзыв не гарантирует, что это изображение hello очищаются все конфиденциальные данные и подходит для распространения.
> 
> 

* отзыв + пользователь: выполняет все данные - deprovision (выше) и также удаляет hello последнего подготовленных учетную запись пользователя (полученные от /var/lib/waagent) и связанные данные. Этот параметр используется для отмены подготовки ранее подготовленного образа в Azure с целью его записи и повторного использования.
* версия: версия waagent отображает hello
* serialconsole: настраивает GRUB toomark ttyS0 (hello используют порт) как консоль загрузки hello. Это гарантирует, что журналы загрузки ядра отправляются toothe последовательного порта и становятся доступными для отладки.
* управляющая программа: запустите waagent как взаимодействие toomanage управляющей программы с платформой hello. Этот аргумент является указанным toowaagent в скрипте init waagent hello.
* start: запуск waagent как фонового процесса

## <a name="configuration"></a>Конфигурация
Файл конфигурации (/ etc/waagent.conf) действия waagent hello элементов управления. Ниже приводится пример файла конфигурации:

    Provisioning.Enabled=y
    Provisioning.DeleteRootPassword=n
    Provisioning.RegenerateSshHostKeyPair=y
    Provisioning.SshHostKeyPairType=rsa
    Provisioning.MonitorHostName=y
    Provisioning.DecodeCustomData=n
    Provisioning.ExecuteCustomData=n
    Provisioning.PasswordCryptId=6
    Provisioning.PasswordCryptSaltLength=10
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.MountOptions=None
    ResourceDisk.EnableSwap=n
    ResourceDisk.SwapSizeMB=0
    LBProbeResponder=y
    Logs.Verbose=n
    OS.RootDeviceScsiTimeout=300
    OS.OpensslPath=None
    HttpProxy.Host=None
    HttpProxy.Port=None

Здравствуйте, ниже подробно описываются различные параметры конфигурации. Параметры конфигурации относятся к одному из трех типов: логическое значение, строка или целое число. параметры конфигурации логическое Hello можно указать как «y» или «n». Здравствуйте, специальное слово «None» могут использоваться некоторые строки типа конфигурации записи, как описано ниже.

**Provisioning.Enabled:**  
Тип: логический  
По умолчанию: y

Это позволяет tooenable hello пользователя или отключить hello подготовки функциональные возможности агента hello. Допустимые значения: "y" или "n". При отключении подготовки ключей SSH узла и пользователя в образе hello сохраняются и какой-либо настройки, указанные в Azure API подготовки hello учитывается.

> [!NOTE]
> Hello `Provisioning.Enabled` слишком «n» на изображениях Ubuntu облака, используйте облачные init для подготовки параметров по умолчанию.
> 
> 

**Provisioning.DeleteRootPassword:**  
Тип: логический  
По умолчанию: n

Здравствуйте, если набор, пароль пользователя root hello в файл теневой hello/etc/будут удалены во время процесса подготовки.

**Provisioning.RegenerateSshHostKeyPair:**  
Тип: логический  
По умолчанию: y

Если набор всех SSH узла пары ключей (ecdsa, dsa и rsa) будут удалены в процессе подготовки процесса из/etc/ssh/hello. При этом генерируется одна новая пара ключей.

Тип шифрования Hello для hello новую пару ключей, которая может настроить hello Provisioning.SshHostKeyPairType входа. Обратите внимание на то, что некоторых дистрибутивов повторно создаст пары ключей SSH для любые виды шифрования, отсутствует при перезапуске hello управляющая программа SSH (например, после перезагрузки).

**Provisioning.SshHostKeyPairType:**  
Тип: строка  
По умолчанию: rsa

Это можно задать тип алгоритма шифрования tooan, поддерживаемый hello управляющая программа SSH на виртуальной машине hello. Hello обычно поддерживаемые значения: «rsa», «dsa» и «ecdsa». Обратите внимание, что "putty.exe" в Windows не поддерживает "ecdsa". Таким образом Если вы хотите toouse putty.exe tooa tooconnect Windows развертывания Linux, используйте «rsa» или «dsa».

**Provisioning.MonitorHostName:**  
Тип: логический  
По умолчанию: y

Если задано, команда waagent будет отслеживать hello виртуальной машины Linux для изменения имени узла (как возвращается командой «hostname» hello ") и автоматически обновить конфигурацию сети hello в tooreflect hello hello изображения изменяется. В имени hello toopush порядок можно изменить toohello DNS-серверы, сеть будет перезапущена в hello виртуальной машины. Это приведет к кратковременной потере подключения к Интернету.

**Provisioning.DecodeCustomData**  
Тип: логический  
По умолчанию: n

Если установлен, waagent будет декодировать пользовательские данные CustomData из кодировки Base64.

**Provisioning.ExecuteCustomData**  
Тип: логический  
По умолчанию: n

Если установлен, waagent выполнит пользовательские данные CustomData после подготовки.

**Provisioning.PasswordCryptId**  
Тип: строка  
По умолчанию: 6

Алгоритм, используемый crypt при создании хеша пароля.  
 1 — MD5  
 2a — Blowfish  
 5 — SHA-256  
 6 — SHA-512  

**Provisioning.PasswordCryptSaltLength**  
Тип: строка  
По умолчанию: 10

Длина случайной соли, используемой при создании хеша пароля.

**ResourceDisk.Format:**  
Тип: логический  
По умолчанию: y

Если задано, hello диска ресурсов, предоставляемых платформой hello будет отформатирован и подключенным сервером waagent, если тип файловой системы hello запросу пользователя hello в «ResourceDisk.Filesystem» ничего, кроме «файловая система ntfs». Один раздел типа Linux (83) будет предоставляться на диске hello. Обратите внимание, что этот раздел не будет отформатирован, если он может быть успешно подключен.

**ResourceDisk.Filesystem:**  
Тип: строка  
По умолчанию: ext4

Указывает тип hello файловой системы для диска ресурсов hello. Допустимые значения зависят от дистрибутива Linux. Если строка hello X, а затем mkfs. X должен присутствовать на hello образа Linux. Для образов SLES 11 обычно используется значение "ext3". Для образов FreeBSD здесь следует использовать "ufs2".

**ResourceDisk.MountPoint:**  
Тип: строка  
По умолчанию: /mnt/resource 

Указывает путь hello, с которой подключен диск ресурсов hello. Обратите внимание, этот диск ресурсов hello *временные* диск, а также может очищаться при отмененной подготовкой hello виртуальной Машины.

**ResourceDisk.MountOptions**  
Тип: строка  
По умолчанию: нет

Команда диска подключения параметры toobe передан toohello mount -o. Это список значений, разделенный запятыми, например 'nodev,nosuid'. Подробные сведения см. в разделе mount(8).

**ResourceDisk.EnableSwap:**  
Тип: логический  
По умолчанию: n

Если задать файл подкачки (/ swapfile) создается на диске ресурсов hello и добавлены toohello пространства подкачки в системе.

**ResourceDisk.SwapSizeMB:**  
Тип: целое число  
По умолчанию: 0

размер Hello hello файла подкачки в мегабайтах.

**Logs.Verbose:**  
Тип: логический  
По умолчанию: n

Если задано, то файл журнала расширяется. Команда Waagent регистрирует too/var/log/waagent.log, а также использует журналы toorotate функциональность logrotate системы hello.

**OS.EnableRDMA**  
Тип: логический  
По умолчанию: n

Если задано, hello агент будет попытка tooinstall и затем загрузить драйвер ядра RDMA, который совпадает с версией hello hello встроенное по hello базового оборудования.

**OS.RootDeviceScsiTimeout:**  
Тип: целое число  
По умолчанию: 300

Это настраивает hello SCSI ожидания в секундах на дисках hello ОС диска и данные. Если свойство не задано, используются значения по умолчанию hello системы.

**OS.OpensslPath:**  
Тип: строка  
По умолчанию: нет

Это может быть toospecify используется альтернативный путь для двоичного toouse hello openssl для криптографических операций.

**HttpProxy.Host, HttpProxy.Port**  
Тип: строка  
По умолчанию: нет

Если задано, hello агент будет использовать этот прокси-сервера tooaccess hello Интернета. 

## <a name="ubuntu-cloud-images"></a>Образы облаков Ubuntu
Обратите внимание, что образы облака Ubuntu используют [облака init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform многих задач настройки, которые в противном случае будет управляться hello агент Azure Linux.  Имейте в виду hello следующие различия:

* **Provisioning.Enabled** слишком «n» на изображениях Ubuntu облака, использовать tooperform init облачные задачи управления по умолчанию.
* следующие параметры конфигурации Hello не оказывают влияния на Ubuntu облака изображений, использовать облако init toomanage hello ресурсов диска и замены пространства:
  
  * **ResourceDisk.Format;**
  * **ResourceDisk.Filesystem;**
  * **ResourceDisk.MountPoint;**
  * **ResourceDisk.EnableSwap;**
  * **ResourceDisk.SwapSizeMB.**
* См. следующие ресурсы tooconfigure hello ресурса диска точки подключения hello и пространство на изображениях облака Ubuntu подкачки во время подготовки:
  
  * [Вики-сайт по Ubuntu: настройка разделов подкачки](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [Включение пользовательских данных в виртуальную машину Azure](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

