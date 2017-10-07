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
# <a name="understanding-and-using-hello-azure-linux-agent"></a><span data-ttu-id="299f5-103">Понимание и использование hello Azure Linux Agent</span><span class="sxs-lookup"><span data-stu-id="299f5-103">Understanding and using hello Azure Linux Agent</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a><span data-ttu-id="299f5-104">Введение</span><span class="sxs-lookup"><span data-stu-id="299f5-104">Introduction</span></span>
<span data-ttu-id="299f5-105">Hello Microsoft Azure Linux Agent (waagent) управляет Linux и FreeBSD подготовки и взаимодействие виртуальной Машины с hello Azure Fabric Controller.</span><span class="sxs-lookup"><span data-stu-id="299f5-105">hello Microsoft Azure Linux Agent (waagent) manages Linux & FreeBSD provisioning, and VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="299f5-106">Он предоставляет следующие функциональные возможности для развертывания ОС Linux и FreeBSD IaaS hello:</span><span class="sxs-lookup"><span data-stu-id="299f5-106">It provides hello following functionality for Linux and FreeBSD IaaS deployments:</span></span>

> [!NOTE]
> <span data-ttu-id="299f5-107">Разделе hello Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="299f5-107">See hello Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) for additional details.</span></span>
> 
> 

* <span data-ttu-id="299f5-108">**Подготовка образа**</span><span class="sxs-lookup"><span data-stu-id="299f5-108">**Image Provisioning**</span></span>
  
  * <span data-ttu-id="299f5-109">Создание учетной записи пользователя</span><span class="sxs-lookup"><span data-stu-id="299f5-109">Creation of a user account</span></span>
  * <span data-ttu-id="299f5-110">Настройка типов аутентификации SSH</span><span class="sxs-lookup"><span data-stu-id="299f5-110">Configuring SSH authentication types</span></span>
  * <span data-ttu-id="299f5-111">Развертывание открытых ключей SSH и пар ключей</span><span class="sxs-lookup"><span data-stu-id="299f5-111">Deployment of SSH public keys and key pairs</span></span>
  * <span data-ttu-id="299f5-112">Параметр имени узла hello</span><span class="sxs-lookup"><span data-stu-id="299f5-112">Setting hello host name</span></span>
  * <span data-ttu-id="299f5-113">Имя узла публикации hello – платформа toohello DNS</span><span class="sxs-lookup"><span data-stu-id="299f5-113">Publishing hello host name toohello platform DNS</span></span>
  * <span data-ttu-id="299f5-114">Reporting платформа toohello отпечаток ключа SSH узла</span><span class="sxs-lookup"><span data-stu-id="299f5-114">Reporting SSH host key fingerprint toohello platform</span></span>
  * <span data-ttu-id="299f5-115">Управление диском ресурсов</span><span class="sxs-lookup"><span data-stu-id="299f5-115">Resource Disk Management</span></span>
  * <span data-ttu-id="299f5-116">Форматирование и подключении диска ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="299f5-116">Formatting and mounting hello resource disk</span></span>
  * <span data-ttu-id="299f5-117">Настройка пространства подкачки</span><span class="sxs-lookup"><span data-stu-id="299f5-117">Configuring swap space</span></span>
* <span data-ttu-id="299f5-118">**Сеть**</span><span class="sxs-lookup"><span data-stu-id="299f5-118">**Networking**</span></span>
  
  * <span data-ttu-id="299f5-119">Управляет маршруты tooimprove совместимости с платформой DHCP-серверами</span><span class="sxs-lookup"><span data-stu-id="299f5-119">Manages routes tooimprove compatibility with platform DHCP servers</span></span>
  * <span data-ttu-id="299f5-120">Обеспечивает стабильность hello hello имя сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="299f5-120">Ensures hello stability of hello network interface name</span></span>
* <span data-ttu-id="299f5-121">**Ядро**</span><span class="sxs-lookup"><span data-stu-id="299f5-121">**Kernel**</span></span>
  
  * <span data-ttu-id="299f5-122">Настраивает виртуальную архитектуру NUMA (отключить для ядра версий ранее 2.6.37).</span><span class="sxs-lookup"><span data-stu-id="299f5-122">Configures virtual NUMA (disable for kernel <2.6.37)</span></span>
  * <span data-ttu-id="299f5-123">Использование энтропии Hyper-V для /dev/random</span><span class="sxs-lookup"><span data-stu-id="299f5-123">Consumes Hyper-V entropy for /dev/random</span></span>
  * <span data-ttu-id="299f5-124">Настраивает время ожидания SCSI для hello Корневое устройство (это может быть удаленный)</span><span class="sxs-lookup"><span data-stu-id="299f5-124">Configures SCSI timeouts for hello root device (which could be remote)</span></span>
* <span data-ttu-id="299f5-125">**Диагностика**</span><span class="sxs-lookup"><span data-stu-id="299f5-125">**Diagnostics**</span></span>
  
  * <span data-ttu-id="299f5-126">Консоль перенаправления toohello последовательного порта</span><span class="sxs-lookup"><span data-stu-id="299f5-126">Console redirection toohello serial port</span></span>
* <span data-ttu-id="299f5-127">**Развернутые приложения SCVMM**</span><span class="sxs-lookup"><span data-stu-id="299f5-127">**SCVMM Deployments**</span></span>
  
  * <span data-ttu-id="299f5-128">Обнаруживает и загружает hello агент VMM для Linux при выполнении в среде System Center Virtual Machine Manager 2012 R2</span><span class="sxs-lookup"><span data-stu-id="299f5-128">Detects and bootstraps hello VMM agent for Linux when running in a System Center Virtual Machine Manager 2012 R2 environment</span></span>
* <span data-ttu-id="299f5-129">**Расширение виртуальной машины**</span><span class="sxs-lookup"><span data-stu-id="299f5-129">**VM Extension**</span></span>
  
  * <span data-ttu-id="299f5-130">Вставить компонент, написанный корпорацией Майкрософт и партнерами в автоматизации tooenable программному обеспечению и конфигурации ВМ Linux (IaaS)</span><span class="sxs-lookup"><span data-stu-id="299f5-130">Inject component authored by Microsoft and Partners into Linux VM (IaaS) tooenable software and configuration automation</span></span>
  * <span data-ttu-id="299f5-131">Эталонная реализация расширения виртуальной машины на сайте [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span><span class="sxs-lookup"><span data-stu-id="299f5-131">VM Extension reference implementation on [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span></span>

## <a name="communication"></a><span data-ttu-id="299f5-132">Обмен данными</span><span class="sxs-lookup"><span data-stu-id="299f5-132">Communication</span></span>
<span data-ttu-id="299f5-133">Hello потоком данных, передаваемых из агента toohello hello выполняется с помощью двух каналов:</span><span class="sxs-lookup"><span data-stu-id="299f5-133">hello information flow from hello platform toohello agent occurs via two channels:</span></span>

* <span data-ttu-id="299f5-134">Прилагаемый DVD, используемый во время загрузки, для развернутых приложений IaaS.</span><span class="sxs-lookup"><span data-stu-id="299f5-134">A boot-time attached DVD for IaaS deployments.</span></span> <span data-ttu-id="299f5-135">Этот DVD-ДИСК содержит OVF-совместимый файл конфигурации, который включает все сведения об инициализации, кроме hello, фактический пары ключей SSH.</span><span class="sxs-lookup"><span data-stu-id="299f5-135">This DVD includes an OVF-compliant configuration file that includes all provisioning information other than hello actual SSH keypairs.</span></span>
* <span data-ttu-id="299f5-136">Предоставление доступа к REST API конечной точке TCP используется tooobtain развертывания и настройки топологии.</span><span class="sxs-lookup"><span data-stu-id="299f5-136">A TCP endpoint exposing a REST API used tooobtain deployment and topology configuration.</span></span>

## <a name="requirements"></a><span data-ttu-id="299f5-137">Требования</span><span class="sxs-lookup"><span data-stu-id="299f5-137">Requirements</span></span>
<span data-ttu-id="299f5-138">Hello следующих систем были протестированы и известны toowork с hello агент Azure Linux:</span><span class="sxs-lookup"><span data-stu-id="299f5-138">hello following systems have been tested and are known toowork with hello Azure Linux Agent:</span></span>

> [!NOTE]
> <span data-ttu-id="299f5-139">Этот список может отличаться от hello официальный список поддерживаемых систем на платформе Microsoft Azure hello, как описано здесь: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span><span class="sxs-lookup"><span data-stu-id="299f5-139">This list may differ from hello official list of supported systems on hello Microsoft Azure Platform, as described here: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span></span>
> 
> 

* <span data-ttu-id="299f5-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="299f5-140">CoreOS</span></span>
* <span data-ttu-id="299f5-141">CentOS 6.3+</span><span class="sxs-lookup"><span data-stu-id="299f5-141">CentOS 6.3+</span></span>
* <span data-ttu-id="299f5-142">Red Hat Enterprise Linux 6.7 и более поздней версии</span><span class="sxs-lookup"><span data-stu-id="299f5-142">Red Hat Enterprise Linux 6.7+</span></span>
* <span data-ttu-id="299f5-143">Debian 7.0+</span><span class="sxs-lookup"><span data-stu-id="299f5-143">Debian 7.0+</span></span>
* <span data-ttu-id="299f5-144">Ubuntu 12.04+</span><span class="sxs-lookup"><span data-stu-id="299f5-144">Ubuntu 12.04+</span></span>
* <span data-ttu-id="299f5-145">openSUSE 12.3+</span><span class="sxs-lookup"><span data-stu-id="299f5-145">openSUSE 12.3+</span></span>
* <span data-ttu-id="299f5-146">SLES 11 SP3+</span><span class="sxs-lookup"><span data-stu-id="299f5-146">SLES 11 SP3+</span></span>
* <span data-ttu-id="299f5-147">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="299f5-147">Oracle Linux 6.4+</span></span>

<span data-ttu-id="299f5-148">Другие поддерживаемые системы:</span><span class="sxs-lookup"><span data-stu-id="299f5-148">Other Supported Systems:</span></span>

* <span data-ttu-id="299f5-149">FreeBSD 10 и более поздней версии (агент Linux для Azure 2.0.10 и более поздней версии)</span><span class="sxs-lookup"><span data-stu-id="299f5-149">FreeBSD 10+ (Azure Linux Agent v2.0.10+)</span></span>

<span data-ttu-id="299f5-150">Некоторые пакеты системы в порядке toofunction зависит агент Linux Hello должным образом.</span><span class="sxs-lookup"><span data-stu-id="299f5-150">hello Linux agent depends on some system packages in order toofunction properly:</span></span>

* <span data-ttu-id="299f5-151">Python 2.6+</span><span class="sxs-lookup"><span data-stu-id="299f5-151">Python 2.6+</span></span>
* <span data-ttu-id="299f5-152">OpenSSL 1.0 и более поздней версии</span><span class="sxs-lookup"><span data-stu-id="299f5-152">OpenSSL 1.0+</span></span>
* <span data-ttu-id="299f5-153">OpenSSH 5.3 и более поздней версии</span><span class="sxs-lookup"><span data-stu-id="299f5-153">OpenSSH 5.3+</span></span>
* <span data-ttu-id="299f5-154">Служебные программы файловой системы: sfdisk, fdisk, mkfs, parted</span><span class="sxs-lookup"><span data-stu-id="299f5-154">Filesystem utilities: sfdisk, fdisk, mkfs, parted</span></span>
* <span data-ttu-id="299f5-155">Инструменты работы с паролями: chpasswd, sudo</span><span class="sxs-lookup"><span data-stu-id="299f5-155">Password tools: chpasswd, sudo</span></span>
* <span data-ttu-id="299f5-156">Инструменты обработки текста: sed, grep</span><span class="sxs-lookup"><span data-stu-id="299f5-156">Text processing tools: sed, grep</span></span>
* <span data-ttu-id="299f5-157">Сетевые инструменты: ip-route</span><span class="sxs-lookup"><span data-stu-id="299f5-157">Network tools: ip-route</span></span>
* <span data-ttu-id="299f5-158">Поддержка ядра для монтирования файловых систем UDF.</span><span class="sxs-lookup"><span data-stu-id="299f5-158">Kernel support for mounting UDF filesystems.</span></span>

## <a name="installation"></a><span data-ttu-id="299f5-159">Установка</span><span class="sxs-lookup"><span data-stu-id="299f5-159">Installation</span></span>
<span data-ttu-id="299f5-160">Установку, используя RPM или DEB пакета из репозитория пакетов на распределение — hello предпочитаемый метод установки и обновления hello Azure Linux Agent.</span><span class="sxs-lookup"><span data-stu-id="299f5-160">Installation using an RPM or a DEB package from your distribution's package repository is hello preferred method of installing and upgrading hello Azure Linux Agent.</span></span> <span data-ttu-id="299f5-161">Все hello [одобренных поставщиков распространения](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) интегрировать пакет агента Azure Linux hello в их репозиториев и изображения.</span><span class="sxs-lookup"><span data-stu-id="299f5-161">All hello [endorsed distribution providers](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrate hello Azure Linux agent package into their images and repositories.</span></span>

<span data-ttu-id="299f5-162">См. документацию toohello в hello [репозитория агент Azure Linux на GitHub](https://github.com/Azure/WALinuxAgent) для установки дополнительных параметров, например Установка из источника или toocustom расположений или префиксов.</span><span class="sxs-lookup"><span data-stu-id="299f5-162">Refer toohello documentation in hello [Azure Linux Agent repo on GitHub](https://github.com/Azure/WALinuxAgent) for advanced installation options, such as installing from source or toocustom locations or prefixes.</span></span>

## <a name="command-line-options"></a><span data-ttu-id="299f5-163">Параметры командной строки</span><span class="sxs-lookup"><span data-stu-id="299f5-163">Command Line Options</span></span>
### <a name="flags"></a><span data-ttu-id="299f5-164">Флаги</span><span class="sxs-lookup"><span data-stu-id="299f5-164">Flags</span></span>
* <span data-ttu-id="299f5-165">verbose: расширить указанную команду</span><span class="sxs-lookup"><span data-stu-id="299f5-165">verbose: Increase verbosity of specified command</span></span>
* <span data-ttu-id="299f5-166">force: пропустить интерактивные подтверждения для некоторых команд</span><span class="sxs-lookup"><span data-stu-id="299f5-166">force: Skip interactive confirmation for some commands</span></span>

### <a name="commands"></a><span data-ttu-id="299f5-167">Команды</span><span class="sxs-lookup"><span data-stu-id="299f5-167">Commands</span></span>
* <span data-ttu-id="299f5-168">Справка: список команд hello поддерживается и флаги.</span><span class="sxs-lookup"><span data-stu-id="299f5-168">help: Lists hello supported commands and flags.</span></span>
* <span data-ttu-id="299f5-169">отзыв: попытка tooclean hello системы и соответствующих повторно подготовки.</span><span class="sxs-lookup"><span data-stu-id="299f5-169">deprovision: Attempt tooclean hello system and make it suitable for re-provisioning.</span></span> <span data-ttu-id="299f5-170">Эта операция удалены hello следующее:</span><span class="sxs-lookup"><span data-stu-id="299f5-170">This operation deleted hello following:</span></span>
  
  * <span data-ttu-id="299f5-171">Все ключи SSH узла (если Provisioning.RegenerateSshHostKeyPair «y» в файле конфигурации hello)</span><span class="sxs-lookup"><span data-stu-id="299f5-171">All SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="299f5-172">Настройка имени сервера в /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="299f5-172">Nameserver configuration in /etc/resolv.conf</span></span>
  * <span data-ttu-id="299f5-173">Пароль учетной записи root в/etc/shadow (если Provisioning.DeleteRootPassword «y» в файле конфигурации hello)</span><span class="sxs-lookup"><span data-stu-id="299f5-173">Root password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="299f5-174">Кэшированные аренды DHCP-клиентов</span><span class="sxs-lookup"><span data-stu-id="299f5-174">Cached DHCP client leases</span></span>
  * <span data-ttu-id="299f5-175">Сброс размещения toolocalhost.localdomain имя</span><span class="sxs-lookup"><span data-stu-id="299f5-175">Resets host name toolocalhost.localdomain</span></span>

> [!WARNING]
> <span data-ttu-id="299f5-176">Отзыв не гарантирует, что это изображение hello очищаются все конфиденциальные данные и подходит для распространения.</span><span class="sxs-lookup"><span data-stu-id="299f5-176">Deprovisioning does not guarantee that hello image is cleared of all sensitive information and suitable for redistribution.</span></span>
> 
> 

* <span data-ttu-id="299f5-177">отзыв + пользователь: выполняет все данные - deprovision (выше) и также удаляет hello последнего подготовленных учетную запись пользователя (полученные от /var/lib/waagent) и связанные данные.</span><span class="sxs-lookup"><span data-stu-id="299f5-177">deprovision+user: Performs everything under -deprovision (above) and also deletes hello last provisioned user account (obtained from /var/lib/waagent) and associated data.</span></span> <span data-ttu-id="299f5-178">Этот параметр используется для отмены подготовки ранее подготовленного образа в Azure с целью его записи и повторного использования.</span><span class="sxs-lookup"><span data-stu-id="299f5-178">This parameter is when de-provisioning an image that was previously provisioning on Azure so it may be captured and re-used.</span></span>
* <span data-ttu-id="299f5-179">версия: версия waagent отображает hello</span><span class="sxs-lookup"><span data-stu-id="299f5-179">version: Displays hello version of waagent</span></span>
* <span data-ttu-id="299f5-180">serialconsole: настраивает GRUB toomark ttyS0 (hello используют порт) как консоль загрузки hello.</span><span class="sxs-lookup"><span data-stu-id="299f5-180">serialconsole: Configures GRUB toomark ttyS0 (hello first serial port) as hello boot console.</span></span> <span data-ttu-id="299f5-181">Это гарантирует, что журналы загрузки ядра отправляются toothe последовательного порта и становятся доступными для отладки.</span><span class="sxs-lookup"><span data-stu-id="299f5-181">This ensures that kernel bootup logs are sent toothe serial port and made available for debugging.</span></span>
* <span data-ttu-id="299f5-182">управляющая программа: запустите waagent как взаимодействие toomanage управляющей программы с платформой hello.</span><span class="sxs-lookup"><span data-stu-id="299f5-182">daemon: Run waagent as a daemon toomanage interaction with hello platform.</span></span> <span data-ttu-id="299f5-183">Этот аргумент является указанным toowaagent в скрипте init waagent hello.</span><span class="sxs-lookup"><span data-stu-id="299f5-183">This argument is specified toowaagent in hello waagent init script.</span></span>
* <span data-ttu-id="299f5-184">start: запуск waagent как фонового процесса</span><span class="sxs-lookup"><span data-stu-id="299f5-184">start: Run waagent as a background process</span></span>

## <a name="configuration"></a><span data-ttu-id="299f5-185">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="299f5-185">Configuration</span></span>
<span data-ttu-id="299f5-186">Файл конфигурации (/ etc/waagent.conf) действия waagent hello элементов управления.</span><span class="sxs-lookup"><span data-stu-id="299f5-186">A configuration file (/etc/waagent.conf) controls hello actions of waagent.</span></span> <span data-ttu-id="299f5-187">Ниже приводится пример файла конфигурации:</span><span class="sxs-lookup"><span data-stu-id="299f5-187">A sample configuration file is shown below:</span></span>

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

<span data-ttu-id="299f5-188">Здравствуйте, ниже подробно описываются различные параметры конфигурации.</span><span class="sxs-lookup"><span data-stu-id="299f5-188">hello various configuration options are described in detail below.</span></span> <span data-ttu-id="299f5-189">Параметры конфигурации относятся к одному из трех типов: логическое значение, строка или целое число.</span><span class="sxs-lookup"><span data-stu-id="299f5-189">Configuration options are of three types; Boolean, String or Integer.</span></span> <span data-ttu-id="299f5-190">параметры конфигурации логическое Hello можно указать как «y» или «n».</span><span class="sxs-lookup"><span data-stu-id="299f5-190">hello Boolean configuration options can be specified as "y" or "n".</span></span> <span data-ttu-id="299f5-191">Здравствуйте, специальное слово «None» могут использоваться некоторые строки типа конфигурации записи, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="299f5-191">hello special keyword "None" may be used for some string type configuration entries as detailed below.</span></span>

<span data-ttu-id="299f5-192">**Provisioning.Enabled:**</span><span class="sxs-lookup"><span data-stu-id="299f5-192">**Provisioning.Enabled:**</span></span>  
<span data-ttu-id="299f5-193">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="299f5-193">Type: Boolean</span></span>  
<span data-ttu-id="299f5-194">По умолчанию: y</span><span class="sxs-lookup"><span data-stu-id="299f5-194">Default: y</span></span>

<span data-ttu-id="299f5-195">Это позволяет tooenable hello пользователя или отключить hello подготовки функциональные возможности агента hello.</span><span class="sxs-lookup"><span data-stu-id="299f5-195">This allows hello user tooenable or disable hello provisioning functionality in hello agent.</span></span> <span data-ttu-id="299f5-196">Допустимые значения: "y" или "n".</span><span class="sxs-lookup"><span data-stu-id="299f5-196">Valid values are "y" or "n".</span></span> <span data-ttu-id="299f5-197">При отключении подготовки ключей SSH узла и пользователя в образе hello сохраняются и какой-либо настройки, указанные в Azure API подготовки hello учитывается.</span><span class="sxs-lookup"><span data-stu-id="299f5-197">If provisioning is disabled, SSH host and user keys in hello image are preserved and any configuration specified in hello Azure provisioning API is ignored.</span></span>

> [!NOTE]
> <span data-ttu-id="299f5-198">Hello `Provisioning.Enabled` слишком «n» на изображениях Ubuntu облака, используйте облачные init для подготовки параметров по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="299f5-198">hello `Provisioning.Enabled` parameter defaults too"n" on Ubuntu Cloud Images that use cloud-init for provisioning.</span></span>
> 
> 

<span data-ttu-id="299f5-199">**Provisioning.DeleteRootPassword:**</span><span class="sxs-lookup"><span data-stu-id="299f5-199">**Provisioning.DeleteRootPassword:**</span></span>  
<span data-ttu-id="299f5-200">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="299f5-200">Type: Boolean</span></span>  
<span data-ttu-id="299f5-201">По умолчанию: n</span><span class="sxs-lookup"><span data-stu-id="299f5-201">Default: n</span></span>

<span data-ttu-id="299f5-202">Здравствуйте, если набор, пароль пользователя root hello в файл теневой hello/etc/будут удалены во время процесса подготовки.</span><span class="sxs-lookup"><span data-stu-id="299f5-202">If set, hello root password in hello /etc/shadow file is erased during hello provisioning process.</span></span>

<span data-ttu-id="299f5-203">**Provisioning.RegenerateSshHostKeyPair:**</span><span class="sxs-lookup"><span data-stu-id="299f5-203">**Provisioning.RegenerateSshHostKeyPair:**</span></span>  
<span data-ttu-id="299f5-204">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="299f5-204">Type: Boolean</span></span>  
<span data-ttu-id="299f5-205">По умолчанию: y</span><span class="sxs-lookup"><span data-stu-id="299f5-205">Default: y</span></span>

<span data-ttu-id="299f5-206">Если набор всех SSH узла пары ключей (ecdsa, dsa и rsa) будут удалены в процессе подготовки процесса из/etc/ssh/hello.</span><span class="sxs-lookup"><span data-stu-id="299f5-206">If set, all SSH host key pairs (ecdsa, dsa and rsa) are deleted during hello provisioning process from /etc/ssh/.</span></span> <span data-ttu-id="299f5-207">При этом генерируется одна новая пара ключей.</span><span class="sxs-lookup"><span data-stu-id="299f5-207">And a single fresh key pair is generated.</span></span>

<span data-ttu-id="299f5-208">Тип шифрования Hello для hello новую пару ключей, которая может настроить hello Provisioning.SshHostKeyPairType входа.</span><span class="sxs-lookup"><span data-stu-id="299f5-208">hello encryption type for hello fresh key pair is configurable by hello Provisioning.SshHostKeyPairType entry.</span></span> <span data-ttu-id="299f5-209">Обратите внимание на то, что некоторых дистрибутивов повторно создаст пары ключей SSH для любые виды шифрования, отсутствует при перезапуске hello управляющая программа SSH (например, после перезагрузки).</span><span class="sxs-lookup"><span data-stu-id="299f5-209">Please note that some distributions will re-create SSH key pairs for any missing encryption types when hello SSH daemon is restarted (for example, upon a reboot).</span></span>

<span data-ttu-id="299f5-210">**Provisioning.SshHostKeyPairType:**</span><span class="sxs-lookup"><span data-stu-id="299f5-210">**Provisioning.SshHostKeyPairType:**</span></span>  
<span data-ttu-id="299f5-211">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="299f5-211">Type: String</span></span>  
<span data-ttu-id="299f5-212">По умолчанию: rsa</span><span class="sxs-lookup"><span data-stu-id="299f5-212">Default: rsa</span></span>

<span data-ttu-id="299f5-213">Это можно задать тип алгоритма шифрования tooan, поддерживаемый hello управляющая программа SSH на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="299f5-213">This can be set tooan encryption algorithm type that is supported by hello SSH daemon on hello virtual machine.</span></span> <span data-ttu-id="299f5-214">Hello обычно поддерживаемые значения: «rsa», «dsa» и «ecdsa».</span><span class="sxs-lookup"><span data-stu-id="299f5-214">hello typically supported values are "rsa", "dsa" and "ecdsa".</span></span> <span data-ttu-id="299f5-215">Обратите внимание, что "putty.exe" в Windows не поддерживает "ecdsa".</span><span class="sxs-lookup"><span data-stu-id="299f5-215">Note that "putty.exe" on Windows does not support "ecdsa".</span></span> <span data-ttu-id="299f5-216">Таким образом Если вы хотите toouse putty.exe tooa tooconnect Windows развертывания Linux, используйте «rsa» или «dsa».</span><span class="sxs-lookup"><span data-stu-id="299f5-216">So, if you intend toouse putty.exe on Windows tooconnect tooa Linux deployment, please use "rsa" or "dsa".</span></span>

<span data-ttu-id="299f5-217">**Provisioning.MonitorHostName:**</span><span class="sxs-lookup"><span data-stu-id="299f5-217">**Provisioning.MonitorHostName:**</span></span>  
<span data-ttu-id="299f5-218">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="299f5-218">Type: Boolean</span></span>  
<span data-ttu-id="299f5-219">По умолчанию: y</span><span class="sxs-lookup"><span data-stu-id="299f5-219">Default: y</span></span>

<span data-ttu-id="299f5-220">Если задано, команда waagent будет отслеживать hello виртуальной машины Linux для изменения имени узла (как возвращается командой «hostname» hello ") и автоматически обновить конфигурацию сети hello в tooreflect hello hello изображения изменяется.</span><span class="sxs-lookup"><span data-stu-id="299f5-220">If set, waagent will monitor hello Linux virtual machine for hostname changes (as returned by hello "hostname" command) and automatically update hello networking configuration in hello image tooreflect hello change.</span></span> <span data-ttu-id="299f5-221">В имени hello toopush порядок можно изменить toohello DNS-серверы, сеть будет перезапущена в hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="299f5-221">In order toopush hello name change toohello DNS servers, networking will be restarted in hello virtual machine.</span></span> <span data-ttu-id="299f5-222">Это приведет к кратковременной потере подключения к Интернету.</span><span class="sxs-lookup"><span data-stu-id="299f5-222">This will result in brief loss of Internet connectivity.</span></span>

<span data-ttu-id="299f5-223">**Provisioning.DecodeCustomData**</span><span class="sxs-lookup"><span data-stu-id="299f5-223">**Provisioning.DecodeCustomData**</span></span>  
<span data-ttu-id="299f5-224">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="299f5-224">Type: Boolean</span></span>  
<span data-ttu-id="299f5-225">По умолчанию: n</span><span class="sxs-lookup"><span data-stu-id="299f5-225">Default: n</span></span>

<span data-ttu-id="299f5-226">Если установлен, waagent будет декодировать пользовательские данные CustomData из кодировки Base64.</span><span class="sxs-lookup"><span data-stu-id="299f5-226">If set, waagent will decode CustomData from Base64.</span></span>

<span data-ttu-id="299f5-227">**Provisioning.ExecuteCustomData**</span><span class="sxs-lookup"><span data-stu-id="299f5-227">**Provisioning.ExecuteCustomData**</span></span>  
<span data-ttu-id="299f5-228">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="299f5-228">Type: Boolean</span></span>  
<span data-ttu-id="299f5-229">По умолчанию: n</span><span class="sxs-lookup"><span data-stu-id="299f5-229">Default: n</span></span>

<span data-ttu-id="299f5-230">Если установлен, waagent выполнит пользовательские данные CustomData после подготовки.</span><span class="sxs-lookup"><span data-stu-id="299f5-230">If set, waagent will execute CustomData after provisioning.</span></span>

<span data-ttu-id="299f5-231">**Provisioning.PasswordCryptId**</span><span class="sxs-lookup"><span data-stu-id="299f5-231">**Provisioning.PasswordCryptId**</span></span>  
<span data-ttu-id="299f5-232">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="299f5-232">Type:String</span></span>  
<span data-ttu-id="299f5-233">По умолчанию: 6</span><span class="sxs-lookup"><span data-stu-id="299f5-233">Default:6</span></span>

<span data-ttu-id="299f5-234">Алгоритм, используемый crypt при создании хеша пароля.</span><span class="sxs-lookup"><span data-stu-id="299f5-234">Algorithm used by crypt when generating password hash.</span></span>  
 <span data-ttu-id="299f5-235">1 — MD5</span><span class="sxs-lookup"><span data-stu-id="299f5-235">1 - MD5</span></span>  
 <span data-ttu-id="299f5-236">2a — Blowfish</span><span class="sxs-lookup"><span data-stu-id="299f5-236">2a - Blowfish</span></span>  
 <span data-ttu-id="299f5-237">5 — SHA-256</span><span class="sxs-lookup"><span data-stu-id="299f5-237">5 - SHA-256</span></span>  
 <span data-ttu-id="299f5-238">6 — SHA-512</span><span class="sxs-lookup"><span data-stu-id="299f5-238">6 - SHA-512</span></span>  

<span data-ttu-id="299f5-239">**Provisioning.PasswordCryptSaltLength**</span><span class="sxs-lookup"><span data-stu-id="299f5-239">**Provisioning.PasswordCryptSaltLength**</span></span>  
<span data-ttu-id="299f5-240">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="299f5-240">Type:String</span></span>  
<span data-ttu-id="299f5-241">По умолчанию: 10</span><span class="sxs-lookup"><span data-stu-id="299f5-241">Default:10</span></span>

<span data-ttu-id="299f5-242">Длина случайной соли, используемой при создании хеша пароля.</span><span class="sxs-lookup"><span data-stu-id="299f5-242">Length of random salt used when generating password hash.</span></span>

<span data-ttu-id="299f5-243">**ResourceDisk.Format:**</span><span class="sxs-lookup"><span data-stu-id="299f5-243">**ResourceDisk.Format:**</span></span>  
<span data-ttu-id="299f5-244">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="299f5-244">Type: Boolean</span></span>  
<span data-ttu-id="299f5-245">По умолчанию: y</span><span class="sxs-lookup"><span data-stu-id="299f5-245">Default: y</span></span>

<span data-ttu-id="299f5-246">Если задано, hello диска ресурсов, предоставляемых платформой hello будет отформатирован и подключенным сервером waagent, если тип файловой системы hello запросу пользователя hello в «ResourceDisk.Filesystem» ничего, кроме «файловая система ntfs».</span><span class="sxs-lookup"><span data-stu-id="299f5-246">If set, hello resource disk provided by hello platform will be formatted and mounted by waagent if hello filesystem type requested by hello user in "ResourceDisk.Filesystem" is anything other than "ntfs".</span></span> <span data-ttu-id="299f5-247">Один раздел типа Linux (83) будет предоставляться на диске hello.</span><span class="sxs-lookup"><span data-stu-id="299f5-247">A single partition of type Linux (83) will be made available on hello disk.</span></span> <span data-ttu-id="299f5-248">Обратите внимание, что этот раздел не будет отформатирован, если он может быть успешно подключен.</span><span class="sxs-lookup"><span data-stu-id="299f5-248">Note that this partition will not be formatted if it can be successfully mounted.</span></span>

<span data-ttu-id="299f5-249">**ResourceDisk.Filesystem:**</span><span class="sxs-lookup"><span data-stu-id="299f5-249">**ResourceDisk.Filesystem:**</span></span>  
<span data-ttu-id="299f5-250">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="299f5-250">Type: String</span></span>  
<span data-ttu-id="299f5-251">По умолчанию: ext4</span><span class="sxs-lookup"><span data-stu-id="299f5-251">Default: ext4</span></span>

<span data-ttu-id="299f5-252">Указывает тип hello файловой системы для диска ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="299f5-252">This specifies hello filesystem type for hello resource disk.</span></span> <span data-ttu-id="299f5-253">Допустимые значения зависят от дистрибутива Linux.</span><span class="sxs-lookup"><span data-stu-id="299f5-253">Supported values vary by Linux distribution.</span></span> <span data-ttu-id="299f5-254">Если строка hello X, а затем mkfs. X должен присутствовать на hello образа Linux.</span><span class="sxs-lookup"><span data-stu-id="299f5-254">If hello string is X, then mkfs.X should be present on hello Linux image.</span></span> <span data-ttu-id="299f5-255">Для образов SLES 11 обычно используется значение "ext3".</span><span class="sxs-lookup"><span data-stu-id="299f5-255">SLES 11 images should typically use 'ext3'.</span></span> <span data-ttu-id="299f5-256">Для образов FreeBSD здесь следует использовать "ufs2".</span><span class="sxs-lookup"><span data-stu-id="299f5-256">FreeBSD images should use 'ufs2' here.</span></span>

<span data-ttu-id="299f5-257">**ResourceDisk.MountPoint:**</span><span class="sxs-lookup"><span data-stu-id="299f5-257">**ResourceDisk.MountPoint:**</span></span>  
<span data-ttu-id="299f5-258">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="299f5-258">Type: String</span></span>  
<span data-ttu-id="299f5-259">По умолчанию: /mnt/resource</span><span class="sxs-lookup"><span data-stu-id="299f5-259">Default: /mnt/resource</span></span> 

<span data-ttu-id="299f5-260">Указывает путь hello, с которой подключен диск ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="299f5-260">This specifies hello path at which hello resource disk is mounted.</span></span> <span data-ttu-id="299f5-261">Обратите внимание, этот диск ресурсов hello *временные* диск, а также может очищаться при отмененной подготовкой hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="299f5-261">Note that hello resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span>

<span data-ttu-id="299f5-262">**ResourceDisk.MountOptions**</span><span class="sxs-lookup"><span data-stu-id="299f5-262">**ResourceDisk.MountOptions**</span></span>  
<span data-ttu-id="299f5-263">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="299f5-263">Type: String</span></span>  
<span data-ttu-id="299f5-264">По умолчанию: нет</span><span class="sxs-lookup"><span data-stu-id="299f5-264">Default: None</span></span>

<span data-ttu-id="299f5-265">Команда диска подключения параметры toobe передан toohello mount -o.</span><span class="sxs-lookup"><span data-stu-id="299f5-265">Specifies disk mount options toobe passed toohello mount -o command.</span></span> <span data-ttu-id="299f5-266">Это список значений, разделенный запятыми, например</span><span class="sxs-lookup"><span data-stu-id="299f5-266">This is a comma separated list of values, ex.</span></span> <span data-ttu-id="299f5-267">'nodev,nosuid'.</span><span class="sxs-lookup"><span data-stu-id="299f5-267">'nodev,nosuid'.</span></span> <span data-ttu-id="299f5-268">Подробные сведения см. в разделе mount(8).</span><span class="sxs-lookup"><span data-stu-id="299f5-268">See mount(8) for details.</span></span>

<span data-ttu-id="299f5-269">**ResourceDisk.EnableSwap:**</span><span class="sxs-lookup"><span data-stu-id="299f5-269">**ResourceDisk.EnableSwap:**</span></span>  
<span data-ttu-id="299f5-270">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="299f5-270">Type: Boolean</span></span>  
<span data-ttu-id="299f5-271">По умолчанию: n</span><span class="sxs-lookup"><span data-stu-id="299f5-271">Default: n</span></span>

<span data-ttu-id="299f5-272">Если задать файл подкачки (/ swapfile) создается на диске ресурсов hello и добавлены toohello пространства подкачки в системе.</span><span class="sxs-lookup"><span data-stu-id="299f5-272">If set, a swap file (/swapfile) is created on hello resource disk and added toohello system swap space.</span></span>

<span data-ttu-id="299f5-273">**ResourceDisk.SwapSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="299f5-273">**ResourceDisk.SwapSizeMB:**</span></span>  
<span data-ttu-id="299f5-274">Тип: целое число</span><span class="sxs-lookup"><span data-stu-id="299f5-274">Type: Integer</span></span>  
<span data-ttu-id="299f5-275">По умолчанию: 0</span><span class="sxs-lookup"><span data-stu-id="299f5-275">Default: 0</span></span>

<span data-ttu-id="299f5-276">размер Hello hello файла подкачки в мегабайтах.</span><span class="sxs-lookup"><span data-stu-id="299f5-276">hello size of hello swap file in megabytes.</span></span>

<span data-ttu-id="299f5-277">**Logs.Verbose:**</span><span class="sxs-lookup"><span data-stu-id="299f5-277">**Logs.Verbose:**</span></span>  
<span data-ttu-id="299f5-278">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="299f5-278">Type: Boolean</span></span>  
<span data-ttu-id="299f5-279">По умолчанию: n</span><span class="sxs-lookup"><span data-stu-id="299f5-279">Default: n</span></span>

<span data-ttu-id="299f5-280">Если задано, то файл журнала расширяется.</span><span class="sxs-lookup"><span data-stu-id="299f5-280">If set, log verbosity is boosted.</span></span> <span data-ttu-id="299f5-281">Команда Waagent регистрирует too/var/log/waagent.log, а также использует журналы toorotate функциональность logrotate системы hello.</span><span class="sxs-lookup"><span data-stu-id="299f5-281">Waagent logs too/var/log/waagent.log and leverages hello system logrotate functionality toorotate logs.</span></span>

<span data-ttu-id="299f5-282">**OS.EnableRDMA**</span><span class="sxs-lookup"><span data-stu-id="299f5-282">**OS.EnableRDMA**</span></span>  
<span data-ttu-id="299f5-283">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="299f5-283">Type: Boolean</span></span>  
<span data-ttu-id="299f5-284">По умолчанию: n</span><span class="sxs-lookup"><span data-stu-id="299f5-284">Default: n</span></span>

<span data-ttu-id="299f5-285">Если задано, hello агент будет попытка tooinstall и затем загрузить драйвер ядра RDMA, который совпадает с версией hello hello встроенное по hello базового оборудования.</span><span class="sxs-lookup"><span data-stu-id="299f5-285">If set, hello agent will attempt tooinstall and then load an RDMA kernel driver that matches hello version of hello firmware on hello underlying hardware.</span></span>

<span data-ttu-id="299f5-286">**OS.RootDeviceScsiTimeout:**</span><span class="sxs-lookup"><span data-stu-id="299f5-286">**OS.RootDeviceScsiTimeout:**</span></span>  
<span data-ttu-id="299f5-287">Тип: целое число</span><span class="sxs-lookup"><span data-stu-id="299f5-287">Type: Integer</span></span>  
<span data-ttu-id="299f5-288">По умолчанию: 300</span><span class="sxs-lookup"><span data-stu-id="299f5-288">Default: 300</span></span>

<span data-ttu-id="299f5-289">Это настраивает hello SCSI ожидания в секундах на дисках hello ОС диска и данные.</span><span class="sxs-lookup"><span data-stu-id="299f5-289">This configures hello SCSI timeout in seconds on hello OS disk and data drives.</span></span> <span data-ttu-id="299f5-290">Если свойство не задано, используются значения по умолчанию hello системы.</span><span class="sxs-lookup"><span data-stu-id="299f5-290">If not set, hello system defaults are used.</span></span>

<span data-ttu-id="299f5-291">**OS.OpensslPath:**</span><span class="sxs-lookup"><span data-stu-id="299f5-291">**OS.OpensslPath:**</span></span>  
<span data-ttu-id="299f5-292">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="299f5-292">Type: String</span></span>  
<span data-ttu-id="299f5-293">По умолчанию: нет</span><span class="sxs-lookup"><span data-stu-id="299f5-293">Default: None</span></span>

<span data-ttu-id="299f5-294">Это может быть toospecify используется альтернативный путь для двоичного toouse hello openssl для криптографических операций.</span><span class="sxs-lookup"><span data-stu-id="299f5-294">This can be used toospecify an alternate path for hello openssl binary toouse for cryptographic operations.</span></span>

<span data-ttu-id="299f5-295">**HttpProxy.Host, HttpProxy.Port**</span><span class="sxs-lookup"><span data-stu-id="299f5-295">**HttpProxy.Host, HttpProxy.Port**</span></span>  
<span data-ttu-id="299f5-296">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="299f5-296">Type: String</span></span>  
<span data-ttu-id="299f5-297">По умолчанию: нет</span><span class="sxs-lookup"><span data-stu-id="299f5-297">Default: None</span></span>

<span data-ttu-id="299f5-298">Если задано, hello агент будет использовать этот прокси-сервера tooaccess hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="299f5-298">If set, hello agent will use this proxy server tooaccess hello internet.</span></span> 

## <a name="ubuntu-cloud-images"></a><span data-ttu-id="299f5-299">Образы облаков Ubuntu</span><span class="sxs-lookup"><span data-stu-id="299f5-299">Ubuntu Cloud Images</span></span>
<span data-ttu-id="299f5-300">Обратите внимание, что образы облака Ubuntu используют [облака init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform многих задач настройки, которые в противном случае будет управляться hello агент Azure Linux.</span><span class="sxs-lookup"><span data-stu-id="299f5-300">Note that Ubuntu Cloud Images utilize [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform many configuration tasks that would otherwise be managed by hello Azure Linux Agent.</span></span>  <span data-ttu-id="299f5-301">Имейте в виду hello следующие различия:</span><span class="sxs-lookup"><span data-stu-id="299f5-301">Please note hello following differences:</span></span>

* <span data-ttu-id="299f5-302">**Provisioning.Enabled** слишком «n» на изображениях Ubuntu облака, использовать tooperform init облачные задачи управления по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="299f5-302">**Provisioning.Enabled** defaults too"n" on Ubuntu Cloud Images that use cloud-init tooperform provisioning tasks.</span></span>
* <span data-ttu-id="299f5-303">следующие параметры конфигурации Hello не оказывают влияния на Ubuntu облака изображений, использовать облако init toomanage hello ресурсов диска и замены пространства:</span><span class="sxs-lookup"><span data-stu-id="299f5-303">hello following configuration parameters have no effect on Ubuntu Cloud Images that use cloud-init toomanage hello resource disk and swap space:</span></span>
  
  * <span data-ttu-id="299f5-304">**ResourceDisk.Format;**</span><span class="sxs-lookup"><span data-stu-id="299f5-304">**ResourceDisk.Format**</span></span>
  * <span data-ttu-id="299f5-305">**ResourceDisk.Filesystem;**</span><span class="sxs-lookup"><span data-stu-id="299f5-305">**ResourceDisk.Filesystem**</span></span>
  * <span data-ttu-id="299f5-306">**ResourceDisk.MountPoint;**</span><span class="sxs-lookup"><span data-stu-id="299f5-306">**ResourceDisk.MountPoint**</span></span>
  * <span data-ttu-id="299f5-307">**ResourceDisk.EnableSwap;**</span><span class="sxs-lookup"><span data-stu-id="299f5-307">**ResourceDisk.EnableSwap**</span></span>
  * <span data-ttu-id="299f5-308">**ResourceDisk.SwapSizeMB.**</span><span class="sxs-lookup"><span data-stu-id="299f5-308">**ResourceDisk.SwapSizeMB**</span></span>
* <span data-ttu-id="299f5-309">См. следующие ресурсы tooconfigure hello ресурса диска точки подключения hello и пространство на изображениях облака Ubuntu подкачки во время подготовки:</span><span class="sxs-lookup"><span data-stu-id="299f5-309">Please see hello following resources tooconfigure hello resource disk mount point and swap space on Ubuntu Cloud Images during provisioning:</span></span>
  
  * [<span data-ttu-id="299f5-310">Вики-сайт по Ubuntu: настройка разделов подкачки</span><span class="sxs-lookup"><span data-stu-id="299f5-310">Ubuntu Wiki: Configure Swap Partitions</span></span>](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [<span data-ttu-id="299f5-311">Включение пользовательских данных в виртуальную машину Azure</span><span class="sxs-lookup"><span data-stu-id="299f5-311">Injecting Custom Data into an Azure Virtual Machine</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

