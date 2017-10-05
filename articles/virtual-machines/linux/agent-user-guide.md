---
title: "Обзор агента виртуальной машины Linux в Azure | Документация Майкрософт"
description: "Узнайте, как установить и настроить агент Linux (waagent) для управления взаимодействием виртуальной машины с Azure Fabric Controller."
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
ms.openlocfilehash: 486ad6bb148583a957fb82b7954ff94f853b12cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="understanding-and-using-the-azure-linux-agent"></a><span data-ttu-id="cef2c-103">Что такое агент Linux для Azure и как его использовать</span><span class="sxs-lookup"><span data-stu-id="cef2c-103">Understanding and using the Azure Linux Agent</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a><span data-ttu-id="cef2c-104">Введение</span><span class="sxs-lookup"><span data-stu-id="cef2c-104">Introduction</span></span>
<span data-ttu-id="cef2c-105">Агент Linux для Microsoft Azure (waagent) управляет подготовкой Linux и FreeBSD и взаимодействием виртуальной машины с контроллером структуры Azure.</span><span class="sxs-lookup"><span data-stu-id="cef2c-105">The Microsoft Azure Linux Agent (waagent) manages Linux & FreeBSD provisioning, and VM interaction with the Azure Fabric Controller.</span></span> <span data-ttu-id="cef2c-106">Он предоставляет следующие функциональные возможности для развернутых приложений IaaS в Linux и FreeBSD:</span><span class="sxs-lookup"><span data-stu-id="cef2c-106">It provides the following functionality for Linux and FreeBSD IaaS deployments:</span></span>

> [!NOTE]
> <span data-ttu-id="cef2c-107">Для получения дополнительных сведений см. файл [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) агента Linux для Azure.</span><span class="sxs-lookup"><span data-stu-id="cef2c-107">See the Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) for additional details.</span></span>
> 
> 

* <span data-ttu-id="cef2c-108">**Подготовка образа**</span><span class="sxs-lookup"><span data-stu-id="cef2c-108">**Image Provisioning**</span></span>
  
  * <span data-ttu-id="cef2c-109">Создание учетной записи пользователя</span><span class="sxs-lookup"><span data-stu-id="cef2c-109">Creation of a user account</span></span>
  * <span data-ttu-id="cef2c-110">Настройка типов аутентификации SSH</span><span class="sxs-lookup"><span data-stu-id="cef2c-110">Configuring SSH authentication types</span></span>
  * <span data-ttu-id="cef2c-111">Развертывание открытых ключей SSH и пар ключей</span><span class="sxs-lookup"><span data-stu-id="cef2c-111">Deployment of SSH public keys and key pairs</span></span>
  * <span data-ttu-id="cef2c-112">Настройка имени узла</span><span class="sxs-lookup"><span data-stu-id="cef2c-112">Setting the host name</span></span>
  * <span data-ttu-id="cef2c-113">Публикация имени узла DNS платформы</span><span class="sxs-lookup"><span data-stu-id="cef2c-113">Publishing the host name to the platform DNS</span></span>
  * <span data-ttu-id="cef2c-114">Отчет с отпечатком ключа узла SSH для платформы</span><span class="sxs-lookup"><span data-stu-id="cef2c-114">Reporting SSH host key fingerprint to the platform</span></span>
  * <span data-ttu-id="cef2c-115">Управление диском ресурсов</span><span class="sxs-lookup"><span data-stu-id="cef2c-115">Resource Disk Management</span></span>
  * <span data-ttu-id="cef2c-116">Форматирование и подключение диска ресурсов</span><span class="sxs-lookup"><span data-stu-id="cef2c-116">Formatting and mounting the resource disk</span></span>
  * <span data-ttu-id="cef2c-117">Настройка пространства подкачки</span><span class="sxs-lookup"><span data-stu-id="cef2c-117">Configuring swap space</span></span>
* <span data-ttu-id="cef2c-118">**Сеть**</span><span class="sxs-lookup"><span data-stu-id="cef2c-118">**Networking**</span></span>
  
  * <span data-ttu-id="cef2c-119">Управляет маршрутами для улучшения совместимости с DHCP-серверами платформы</span><span class="sxs-lookup"><span data-stu-id="cef2c-119">Manages routes to improve compatibility with platform DHCP servers</span></span>
  * <span data-ttu-id="cef2c-120">Обеспечивает стабильность имени сетевого интерфейса</span><span class="sxs-lookup"><span data-stu-id="cef2c-120">Ensures the stability of the network interface name</span></span>
* <span data-ttu-id="cef2c-121">**Ядро**</span><span class="sxs-lookup"><span data-stu-id="cef2c-121">**Kernel**</span></span>
  
  * <span data-ttu-id="cef2c-122">Настраивает виртуальную архитектуру NUMA (отключить для ядра версий ранее 2.6.37).</span><span class="sxs-lookup"><span data-stu-id="cef2c-122">Configures virtual NUMA (disable for kernel <2.6.37)</span></span>
  * <span data-ttu-id="cef2c-123">Использование энтропии Hyper-V для /dev/random</span><span class="sxs-lookup"><span data-stu-id="cef2c-123">Consumes Hyper-V entropy for /dev/random</span></span>
  * <span data-ttu-id="cef2c-124">Настройка времени ожидания SCSI для корневого устройства (может быть удаленным)</span><span class="sxs-lookup"><span data-stu-id="cef2c-124">Configures SCSI timeouts for the root device (which could be remote)</span></span>
* <span data-ttu-id="cef2c-125">**Диагностика**</span><span class="sxs-lookup"><span data-stu-id="cef2c-125">**Diagnostics**</span></span>
  
  * <span data-ttu-id="cef2c-126">Перенаправление консоли на последовательный порт</span><span class="sxs-lookup"><span data-stu-id="cef2c-126">Console redirection to the serial port</span></span>
* <span data-ttu-id="cef2c-127">**Развернутые приложения SCVMM**</span><span class="sxs-lookup"><span data-stu-id="cef2c-127">**SCVMM Deployments**</span></span>
  
  * <span data-ttu-id="cef2c-128">Обнаружение и начальная загрузка агента VMM для Linux при работе в среде System Center Virtual Machine Manager 2012 R2</span><span class="sxs-lookup"><span data-stu-id="cef2c-128">Detects and bootstraps the VMM agent for Linux when running in a System Center Virtual Machine Manager 2012 R2 environment</span></span>
* <span data-ttu-id="cef2c-129">**Расширение виртуальной машины**</span><span class="sxs-lookup"><span data-stu-id="cef2c-129">**VM Extension**</span></span>
  
  * <span data-ttu-id="cef2c-130">Вставка компонента, созданного корпорацией Майкрософт и ее партнерами, в виртуальную машину Linux (IaaS) для включения программного обеспечения и автоматизации настройки</span><span class="sxs-lookup"><span data-stu-id="cef2c-130">Inject component authored by Microsoft and Partners into Linux VM (IaaS) to enable software and configuration automation</span></span>
  * <span data-ttu-id="cef2c-131">Эталонная реализация расширения виртуальной машины на сайте [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span><span class="sxs-lookup"><span data-stu-id="cef2c-131">VM Extension reference implementation on [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span></span>

## <a name="communication"></a><span data-ttu-id="cef2c-132">Обмен данными</span><span class="sxs-lookup"><span data-stu-id="cef2c-132">Communication</span></span>
<span data-ttu-id="cef2c-133">Поток информации от платформы к агенту передается по двум каналам:</span><span class="sxs-lookup"><span data-stu-id="cef2c-133">The information flow from the platform to the agent occurs via two channels:</span></span>

* <span data-ttu-id="cef2c-134">Прилагаемый DVD, используемый во время загрузки, для развернутых приложений IaaS.</span><span class="sxs-lookup"><span data-stu-id="cef2c-134">A boot-time attached DVD for IaaS deployments.</span></span> <span data-ttu-id="cef2c-135">На этом DVD содержится OVF-совместимый файл конфигурации, включающий всю информацию для подготовки кроме самих пар ключей SSH.</span><span class="sxs-lookup"><span data-stu-id="cef2c-135">This DVD includes an OVF-compliant configuration file that includes all provisioning information other than the actual SSH keypairs.</span></span>
* <span data-ttu-id="cef2c-136">Чтобы получить развертывание и настройку топологии, используется конечная точка TCP с REST API.</span><span class="sxs-lookup"><span data-stu-id="cef2c-136">A TCP endpoint exposing a REST API used to obtain deployment and topology configuration.</span></span>

## <a name="requirements"></a><span data-ttu-id="cef2c-137">Требования</span><span class="sxs-lookup"><span data-stu-id="cef2c-137">Requirements</span></span>
<span data-ttu-id="cef2c-138">Следующие системы протестированы и гарантированно поддерживают работу с агентом Linux для Azure:</span><span class="sxs-lookup"><span data-stu-id="cef2c-138">The following systems have been tested and are known to work with the Azure Linux Agent:</span></span>

> [!NOTE]
> <span data-ttu-id="cef2c-139">Этот список может отличаться от официального списка систем, поддерживаемых платформой Microsoft Azure, который доступен на странице: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216).</span><span class="sxs-lookup"><span data-stu-id="cef2c-139">This list may differ from the official list of supported systems on the Microsoft Azure Platform, as described here: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span></span>
> 
> 

* <span data-ttu-id="cef2c-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="cef2c-140">CoreOS</span></span>
* <span data-ttu-id="cef2c-141">CentOS 6.3+</span><span class="sxs-lookup"><span data-stu-id="cef2c-141">CentOS 6.3+</span></span>
* <span data-ttu-id="cef2c-142">Red Hat Enterprise Linux 6.7 и более поздней версии</span><span class="sxs-lookup"><span data-stu-id="cef2c-142">Red Hat Enterprise Linux 6.7+</span></span>
* <span data-ttu-id="cef2c-143">Debian 7.0+</span><span class="sxs-lookup"><span data-stu-id="cef2c-143">Debian 7.0+</span></span>
* <span data-ttu-id="cef2c-144">Ubuntu 12.04+</span><span class="sxs-lookup"><span data-stu-id="cef2c-144">Ubuntu 12.04+</span></span>
* <span data-ttu-id="cef2c-145">openSUSE 12.3+</span><span class="sxs-lookup"><span data-stu-id="cef2c-145">openSUSE 12.3+</span></span>
* <span data-ttu-id="cef2c-146">SLES 11 SP3+</span><span class="sxs-lookup"><span data-stu-id="cef2c-146">SLES 11 SP3+</span></span>
* <span data-ttu-id="cef2c-147">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="cef2c-147">Oracle Linux 6.4+</span></span>

<span data-ttu-id="cef2c-148">Другие поддерживаемые системы:</span><span class="sxs-lookup"><span data-stu-id="cef2c-148">Other Supported Systems:</span></span>

* <span data-ttu-id="cef2c-149">FreeBSD 10 и более поздней версии (агент Linux для Azure 2.0.10 и более поздней версии)</span><span class="sxs-lookup"><span data-stu-id="cef2c-149">FreeBSD 10+ (Azure Linux Agent v2.0.10+)</span></span>

<span data-ttu-id="cef2c-150">Для правильного функционирования агента Linux требуются определенные пакеты системы:</span><span class="sxs-lookup"><span data-stu-id="cef2c-150">The Linux agent depends on some system packages in order to function properly:</span></span>

* <span data-ttu-id="cef2c-151">Python 2.6+</span><span class="sxs-lookup"><span data-stu-id="cef2c-151">Python 2.6+</span></span>
* <span data-ttu-id="cef2c-152">OpenSSL 1.0 и более поздней версии</span><span class="sxs-lookup"><span data-stu-id="cef2c-152">OpenSSL 1.0+</span></span>
* <span data-ttu-id="cef2c-153">OpenSSH 5.3 и более поздней версии</span><span class="sxs-lookup"><span data-stu-id="cef2c-153">OpenSSH 5.3+</span></span>
* <span data-ttu-id="cef2c-154">Служебные программы файловой системы: sfdisk, fdisk, mkfs, parted</span><span class="sxs-lookup"><span data-stu-id="cef2c-154">Filesystem utilities: sfdisk, fdisk, mkfs, parted</span></span>
* <span data-ttu-id="cef2c-155">Инструменты работы с паролями: chpasswd, sudo</span><span class="sxs-lookup"><span data-stu-id="cef2c-155">Password tools: chpasswd, sudo</span></span>
* <span data-ttu-id="cef2c-156">Инструменты обработки текста: sed, grep</span><span class="sxs-lookup"><span data-stu-id="cef2c-156">Text processing tools: sed, grep</span></span>
* <span data-ttu-id="cef2c-157">Сетевые инструменты: ip-route</span><span class="sxs-lookup"><span data-stu-id="cef2c-157">Network tools: ip-route</span></span>
* <span data-ttu-id="cef2c-158">Поддержка ядра для монтирования файловых систем UDF.</span><span class="sxs-lookup"><span data-stu-id="cef2c-158">Kernel support for mounting UDF filesystems.</span></span>

## <a name="installation"></a><span data-ttu-id="cef2c-159">Установка</span><span class="sxs-lookup"><span data-stu-id="cef2c-159">Installation</span></span>
<span data-ttu-id="cef2c-160">Установка с помощью пакета RPM или DEB из репозитория пакета дистрибутива является предпочтительным способом установки и обновления агента Linux для Azure.</span><span class="sxs-lookup"><span data-stu-id="cef2c-160">Installation using an RPM or a DEB package from your distribution's package repository is the preferred method of installing and upgrading the Azure Linux Agent.</span></span> <span data-ttu-id="cef2c-161">Все [поставщики поддерживаемых дистрибутивов](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) встраивают пакет агента Linux для Azure в свои образы и репозитории.</span><span class="sxs-lookup"><span data-stu-id="cef2c-161">All the [endorsed distribution providers](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrate the Azure Linux agent package into their images and repositories.</span></span>

<span data-ttu-id="cef2c-162">Дополнительные варианты установки, например установка из источника, установка в пользовательские расположения или префиксы, описаны в документации в [репозитории агента Linux для Azure на сайте GitHub](https://github.com/Azure/WALinuxAgent).</span><span class="sxs-lookup"><span data-stu-id="cef2c-162">Refer to the documentation in the [Azure Linux Agent repo on GitHub](https://github.com/Azure/WALinuxAgent) for advanced installation options, such as installing from source or to custom locations or prefixes.</span></span>

## <a name="command-line-options"></a><span data-ttu-id="cef2c-163">Параметры командной строки</span><span class="sxs-lookup"><span data-stu-id="cef2c-163">Command Line Options</span></span>
### <a name="flags"></a><span data-ttu-id="cef2c-164">Флаги</span><span class="sxs-lookup"><span data-stu-id="cef2c-164">Flags</span></span>
* <span data-ttu-id="cef2c-165">verbose: расширить указанную команду</span><span class="sxs-lookup"><span data-stu-id="cef2c-165">verbose: Increase verbosity of specified command</span></span>
* <span data-ttu-id="cef2c-166">force: пропустить интерактивные подтверждения для некоторых команд</span><span class="sxs-lookup"><span data-stu-id="cef2c-166">force: Skip interactive confirmation for some commands</span></span>

### <a name="commands"></a><span data-ttu-id="cef2c-167">Команды</span><span class="sxs-lookup"><span data-stu-id="cef2c-167">Commands</span></span>
* <span data-ttu-id="cef2c-168">help: список поддерживаемых команд и флагов.</span><span class="sxs-lookup"><span data-stu-id="cef2c-168">help: Lists the supported commands and flags.</span></span>
* <span data-ttu-id="cef2c-169">deprovision: попытка очистки системы и выполнение действий для ее повторной подготовки.</span><span class="sxs-lookup"><span data-stu-id="cef2c-169">deprovision: Attempt to clean the system and make it suitable for re-provisioning.</span></span> <span data-ttu-id="cef2c-170">При выполнении этой операции были удалены следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="cef2c-170">This operation deleted the following:</span></span>
  
  * <span data-ttu-id="cef2c-171">Все ключи узла SSH (если в файле конфигурации для Provisioning.RegenerateSshHostKeyPair указано значение «y»)</span><span class="sxs-lookup"><span data-stu-id="cef2c-171">All SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in the configuration file)</span></span>
  * <span data-ttu-id="cef2c-172">Настройка имени сервера в /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="cef2c-172">Nameserver configuration in /etc/resolv.conf</span></span>
  * <span data-ttu-id="cef2c-173">Корневой пароль из /etc/shadow (если в файле конфигурации для Provisioning.DeleteRootPassword указано значение «y»)</span><span class="sxs-lookup"><span data-stu-id="cef2c-173">Root password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in the configuration file)</span></span>
  * <span data-ttu-id="cef2c-174">Кэшированные аренды DHCP-клиентов</span><span class="sxs-lookup"><span data-stu-id="cef2c-174">Cached DHCP client leases</span></span>
  * <span data-ttu-id="cef2c-175">возвращается имя узла localhost.localdomain;</span><span class="sxs-lookup"><span data-stu-id="cef2c-175">Resets host name to localhost.localdomain</span></span>

> [!WARNING]
> <span data-ttu-id="cef2c-176">Отмена подготовки не гарантирует, что из образа будет удалена вся конфиденциальная информация и что он будет готов к повторному распространению.</span><span class="sxs-lookup"><span data-stu-id="cef2c-176">Deprovisioning does not guarantee that the image is cleared of all sensitive information and suitable for redistribution.</span></span>
> 
> 

* <span data-ttu-id="cef2c-177">deprovision+user: выполняет все действия, указанные для команды -deprovision (см. выше), а также удаляет последнюю подготовленную учетную запись пользователя (полученную в /var/lib/waagent) и связанные с ней данные.</span><span class="sxs-lookup"><span data-stu-id="cef2c-177">deprovision+user: Performs everything under -deprovision (above) and also deletes the last provisioned user account (obtained from /var/lib/waagent) and associated data.</span></span> <span data-ttu-id="cef2c-178">Этот параметр используется для отмены подготовки ранее подготовленного образа в Azure с целью его записи и повторного использования.</span><span class="sxs-lookup"><span data-stu-id="cef2c-178">This parameter is when de-provisioning an image that was previously provisioning on Azure so it may be captured and re-used.</span></span>
* <span data-ttu-id="cef2c-179">version: отображает версию waagent</span><span class="sxs-lookup"><span data-stu-id="cef2c-179">version: Displays the version of waagent</span></span>
* <span data-ttu-id="cef2c-180">serialconsole: настройка GRUB для маркировки ttyS0 (первый последовательный порт) в качестве консоли загрузки.</span><span class="sxs-lookup"><span data-stu-id="cef2c-180">serialconsole: Configures GRUB to mark ttyS0 (the first serial port) as the boot console.</span></span> <span data-ttu-id="cef2c-181">Это гарантирует, что журналы загрузки ядра отправляются на последовательный порт и становятся доступными для отладки.</span><span class="sxs-lookup"><span data-stu-id="cef2c-181">This ensures that kernel bootup logs are sent to the serial port and made available for debugging.</span></span>
* <span data-ttu-id="cef2c-182">daemon: запуск waagent в качестве управляющей программы для контроля взаимодействия с платформой.</span><span class="sxs-lookup"><span data-stu-id="cef2c-182">daemon: Run waagent as a daemon to manage interaction with the platform.</span></span> <span data-ttu-id="cef2c-183">Этот аргумент указывается для waagent в сценарии инициализации waagent.</span><span class="sxs-lookup"><span data-stu-id="cef2c-183">This argument is specified to waagent in the waagent init script.</span></span>
* <span data-ttu-id="cef2c-184">start: запуск waagent как фонового процесса</span><span class="sxs-lookup"><span data-stu-id="cef2c-184">start: Run waagent as a background process</span></span>

## <a name="configuration"></a><span data-ttu-id="cef2c-185">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="cef2c-185">Configuration</span></span>
<span data-ttu-id="cef2c-186">Файл конфигурации (/ etc/waagent.conf) определяет действия waagent.</span><span class="sxs-lookup"><span data-stu-id="cef2c-186">A configuration file (/etc/waagent.conf) controls the actions of waagent.</span></span> <span data-ttu-id="cef2c-187">Ниже приводится пример файла конфигурации:</span><span class="sxs-lookup"><span data-stu-id="cef2c-187">A sample configuration file is shown below:</span></span>

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

<span data-ttu-id="cef2c-188">Ниже подробно описаны различные параметры конфигурации.</span><span class="sxs-lookup"><span data-stu-id="cef2c-188">The various configuration options are described in detail below.</span></span> <span data-ttu-id="cef2c-189">Параметры конфигурации относятся к одному из трех типов: логическое значение, строка или целое число.</span><span class="sxs-lookup"><span data-stu-id="cef2c-189">Configuration options are of three types; Boolean, String or Integer.</span></span> <span data-ttu-id="cef2c-190">Логические параметры конфигурации могут принимать значение "y" или "n".</span><span class="sxs-lookup"><span data-stu-id="cef2c-190">The Boolean configuration options can be specified as "y" or "n".</span></span> <span data-ttu-id="cef2c-191">Для некоторых записей конфигурации типа "строка", описанных ниже, может использоваться специальное ключевое слово "None".</span><span class="sxs-lookup"><span data-stu-id="cef2c-191">The special keyword "None" may be used for some string type configuration entries as detailed below.</span></span>

<span data-ttu-id="cef2c-192">**Provisioning.Enabled:**</span><span class="sxs-lookup"><span data-stu-id="cef2c-192">**Provisioning.Enabled:**</span></span>  
<span data-ttu-id="cef2c-193">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="cef2c-193">Type: Boolean</span></span>  
<span data-ttu-id="cef2c-194">По умолчанию: y</span><span class="sxs-lookup"><span data-stu-id="cef2c-194">Default: y</span></span>

<span data-ttu-id="cef2c-195">Он позволяет пользователю включить или отключить функцию подготовки в агенте.</span><span class="sxs-lookup"><span data-stu-id="cef2c-195">This allows the user to enable or disable the provisioning functionality in the agent.</span></span> <span data-ttu-id="cef2c-196">Допустимые значения: "y" или "n".</span><span class="sxs-lookup"><span data-stu-id="cef2c-196">Valid values are "y" or "n".</span></span> <span data-ttu-id="cef2c-197">Если подготовка отключена, узел SSH и пользовательские ключи в образе сохраняются, а любые настройки, указанные в API для подготовки Azure, игнорируются.</span><span class="sxs-lookup"><span data-stu-id="cef2c-197">If provisioning is disabled, SSH host and user keys in the image are preserved and any configuration specified in the Azure provisioning API is ignored.</span></span>

> [!NOTE]
> <span data-ttu-id="cef2c-198">В образах облаков Ubuntu, использующих для подготовки пакет cloud-init, для параметра `Provisioning.Enabled` по умолчанию устанавливается значение n.</span><span class="sxs-lookup"><span data-stu-id="cef2c-198">The `Provisioning.Enabled` parameter defaults to "n" on Ubuntu Cloud Images that use cloud-init for provisioning.</span></span>
> 
> 

<span data-ttu-id="cef2c-199">**Provisioning.DeleteRootPassword:**</span><span class="sxs-lookup"><span data-stu-id="cef2c-199">**Provisioning.DeleteRootPassword:**</span></span>  
<span data-ttu-id="cef2c-200">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="cef2c-200">Type: Boolean</span></span>  
<span data-ttu-id="cef2c-201">По умолчанию: n</span><span class="sxs-lookup"><span data-stu-id="cef2c-201">Default: n</span></span>

<span data-ttu-id="cef2c-202">Удаляет корневой пароль в файле /etc/shadow в процессе подготовки.</span><span class="sxs-lookup"><span data-stu-id="cef2c-202">If set, the root password in the /etc/shadow file is erased during the provisioning process.</span></span>

<span data-ttu-id="cef2c-203">**Provisioning.RegenerateSshHostKeyPair:**</span><span class="sxs-lookup"><span data-stu-id="cef2c-203">**Provisioning.RegenerateSshHostKeyPair:**</span></span>  
<span data-ttu-id="cef2c-204">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="cef2c-204">Type: Boolean</span></span>  
<span data-ttu-id="cef2c-205">По умолчанию: y</span><span class="sxs-lookup"><span data-stu-id="cef2c-205">Default: y</span></span>

<span data-ttu-id="cef2c-206">Удаляет все пары ключей узла SSH (ecdsa, dsa и rsa) из /etc/ssh/ в процессе подготовки.</span><span class="sxs-lookup"><span data-stu-id="cef2c-206">If set, all SSH host key pairs (ecdsa, dsa and rsa) are deleted during the provisioning process from /etc/ssh/.</span></span> <span data-ttu-id="cef2c-207">При этом генерируется одна новая пара ключей.</span><span class="sxs-lookup"><span data-stu-id="cef2c-207">And a single fresh key pair is generated.</span></span>

<span data-ttu-id="cef2c-208">Тип шифрования для новой пары ключей настраивается с помощью операции Provisioning.SshHostKeyPairType.</span><span class="sxs-lookup"><span data-stu-id="cef2c-208">The encryption type for the fresh key pair is configurable by the Provisioning.SshHostKeyPairType entry.</span></span> <span data-ttu-id="cef2c-209">Обратите внимание, что некоторые дистрибутивы повторно создают пары ключей SSH для любых недостающих типов шифрования при перезапуске управляющей программы SSH (например, после перезагрузки).</span><span class="sxs-lookup"><span data-stu-id="cef2c-209">Please note that some distributions will re-create SSH key pairs for any missing encryption types when the SSH daemon is restarted (for example, upon a reboot).</span></span>

<span data-ttu-id="cef2c-210">**Provisioning.SshHostKeyPairType:**</span><span class="sxs-lookup"><span data-stu-id="cef2c-210">**Provisioning.SshHostKeyPairType:**</span></span>  
<span data-ttu-id="cef2c-211">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="cef2c-211">Type: String</span></span>  
<span data-ttu-id="cef2c-212">По умолчанию: rsa</span><span class="sxs-lookup"><span data-stu-id="cef2c-212">Default: rsa</span></span>

<span data-ttu-id="cef2c-213">Задается тип алгоритма шифрования, поддерживаемый управляющей программой SSH на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="cef2c-213">This can be set to an encryption algorithm type that is supported by the SSH daemon on the virtual machine.</span></span> <span data-ttu-id="cef2c-214">Обычно поддерживаются значения "rsa", "dsa" и "ecdsa".</span><span class="sxs-lookup"><span data-stu-id="cef2c-214">The typically supported values are "rsa", "dsa" and "ecdsa".</span></span> <span data-ttu-id="cef2c-215">Обратите внимание, что "putty.exe" в Windows не поддерживает "ecdsa".</span><span class="sxs-lookup"><span data-stu-id="cef2c-215">Note that "putty.exe" on Windows does not support "ecdsa".</span></span> <span data-ttu-id="cef2c-216">Таким образом, если вы планируете использовать putty.exe в Windows для подключения к развертыванию Linux, используйте "rsa" или "dsa".</span><span class="sxs-lookup"><span data-stu-id="cef2c-216">So, if you intend to use putty.exe on Windows to connect to a Linux deployment, please use "rsa" or "dsa".</span></span>

<span data-ttu-id="cef2c-217">**Provisioning.MonitorHostName:**</span><span class="sxs-lookup"><span data-stu-id="cef2c-217">**Provisioning.MonitorHostName:**</span></span>  
<span data-ttu-id="cef2c-218">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="cef2c-218">Type: Boolean</span></span>  
<span data-ttu-id="cef2c-219">По умолчанию: y</span><span class="sxs-lookup"><span data-stu-id="cef2c-219">Default: y</span></span>

<span data-ttu-id="cef2c-220">Если задано, waagent будет отслеживать виртуальную машину Linux на предмет изменений имени узла (как значение, возвращаемое командой "hostname") и автоматически обновлять сетевую конфигурацию образа в соответствии с изменениями.</span><span class="sxs-lookup"><span data-stu-id="cef2c-220">If set, waagent will monitor the Linux virtual machine for hostname changes (as returned by the "hostname" command) and automatically update the networking configuration in the image to reflect the change.</span></span> <span data-ttu-id="cef2c-221">Для передачи изменения имени на DNS-серверы сеть на виртуальной машине будет перезапущена.</span><span class="sxs-lookup"><span data-stu-id="cef2c-221">In order to push the name change to the DNS servers, networking will be restarted in the virtual machine.</span></span> <span data-ttu-id="cef2c-222">Это приведет к кратковременной потере подключения к Интернету.</span><span class="sxs-lookup"><span data-stu-id="cef2c-222">This will result in brief loss of Internet connectivity.</span></span>

<span data-ttu-id="cef2c-223">**Provisioning.DecodeCustomData**</span><span class="sxs-lookup"><span data-stu-id="cef2c-223">**Provisioning.DecodeCustomData**</span></span>  
<span data-ttu-id="cef2c-224">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="cef2c-224">Type: Boolean</span></span>  
<span data-ttu-id="cef2c-225">По умолчанию: n</span><span class="sxs-lookup"><span data-stu-id="cef2c-225">Default: n</span></span>

<span data-ttu-id="cef2c-226">Если установлен, waagent будет декодировать пользовательские данные CustomData из кодировки Base64.</span><span class="sxs-lookup"><span data-stu-id="cef2c-226">If set, waagent will decode CustomData from Base64.</span></span>

<span data-ttu-id="cef2c-227">**Provisioning.ExecuteCustomData**</span><span class="sxs-lookup"><span data-stu-id="cef2c-227">**Provisioning.ExecuteCustomData**</span></span>  
<span data-ttu-id="cef2c-228">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="cef2c-228">Type: Boolean</span></span>  
<span data-ttu-id="cef2c-229">По умолчанию: n</span><span class="sxs-lookup"><span data-stu-id="cef2c-229">Default: n</span></span>

<span data-ttu-id="cef2c-230">Если установлен, waagent выполнит пользовательские данные CustomData после подготовки.</span><span class="sxs-lookup"><span data-stu-id="cef2c-230">If set, waagent will execute CustomData after provisioning.</span></span>

<span data-ttu-id="cef2c-231">**Provisioning.PasswordCryptId**</span><span class="sxs-lookup"><span data-stu-id="cef2c-231">**Provisioning.PasswordCryptId**</span></span>  
<span data-ttu-id="cef2c-232">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="cef2c-232">Type:String</span></span>  
<span data-ttu-id="cef2c-233">По умолчанию: 6</span><span class="sxs-lookup"><span data-stu-id="cef2c-233">Default:6</span></span>

<span data-ttu-id="cef2c-234">Алгоритм, используемый crypt при создании хеша пароля.</span><span class="sxs-lookup"><span data-stu-id="cef2c-234">Algorithm used by crypt when generating password hash.</span></span>  
 <span data-ttu-id="cef2c-235">1 — MD5</span><span class="sxs-lookup"><span data-stu-id="cef2c-235">1 - MD5</span></span>  
 <span data-ttu-id="cef2c-236">2a — Blowfish</span><span class="sxs-lookup"><span data-stu-id="cef2c-236">2a - Blowfish</span></span>  
 <span data-ttu-id="cef2c-237">5 — SHA-256</span><span class="sxs-lookup"><span data-stu-id="cef2c-237">5 - SHA-256</span></span>  
 <span data-ttu-id="cef2c-238">6 — SHA-512</span><span class="sxs-lookup"><span data-stu-id="cef2c-238">6 - SHA-512</span></span>  

<span data-ttu-id="cef2c-239">**Provisioning.PasswordCryptSaltLength**</span><span class="sxs-lookup"><span data-stu-id="cef2c-239">**Provisioning.PasswordCryptSaltLength**</span></span>  
<span data-ttu-id="cef2c-240">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="cef2c-240">Type:String</span></span>  
<span data-ttu-id="cef2c-241">По умолчанию: 10</span><span class="sxs-lookup"><span data-stu-id="cef2c-241">Default:10</span></span>

<span data-ttu-id="cef2c-242">Длина случайной соли, используемой при создании хеша пароля.</span><span class="sxs-lookup"><span data-stu-id="cef2c-242">Length of random salt used when generating password hash.</span></span>

<span data-ttu-id="cef2c-243">**ResourceDisk.Format:**</span><span class="sxs-lookup"><span data-stu-id="cef2c-243">**ResourceDisk.Format:**</span></span>  
<span data-ttu-id="cef2c-244">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="cef2c-244">Type: Boolean</span></span>  
<span data-ttu-id="cef2c-245">По умолчанию: y</span><span class="sxs-lookup"><span data-stu-id="cef2c-245">Default: y</span></span>

<span data-ttu-id="cef2c-246">Если задано, диск ресурсов, предоставленный платформой, будет отформатирован и смонтирован с использованием waagent, если тип файловой системы, запрошенный пользователем в "ResourceDisk.Filesystem", отличается от "ntfs".</span><span class="sxs-lookup"><span data-stu-id="cef2c-246">If set, the resource disk provided by the platform will be formatted and mounted by waagent if the filesystem type requested by the user in "ResourceDisk.Filesystem" is anything other than "ntfs".</span></span> <span data-ttu-id="cef2c-247">На диске будет доступен один раздел типа Linux (83).</span><span class="sxs-lookup"><span data-stu-id="cef2c-247">A single partition of type Linux (83) will be made available on the disk.</span></span> <span data-ttu-id="cef2c-248">Обратите внимание, что этот раздел не будет отформатирован, если он может быть успешно подключен.</span><span class="sxs-lookup"><span data-stu-id="cef2c-248">Note that this partition will not be formatted if it can be successfully mounted.</span></span>

<span data-ttu-id="cef2c-249">**ResourceDisk.Filesystem:**</span><span class="sxs-lookup"><span data-stu-id="cef2c-249">**ResourceDisk.Filesystem:**</span></span>  
<span data-ttu-id="cef2c-250">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="cef2c-250">Type: String</span></span>  
<span data-ttu-id="cef2c-251">По умолчанию: ext4</span><span class="sxs-lookup"><span data-stu-id="cef2c-251">Default: ext4</span></span>

<span data-ttu-id="cef2c-252">Указывает тип файловой системы для диска ресурса.</span><span class="sxs-lookup"><span data-stu-id="cef2c-252">This specifies the filesystem type for the resource disk.</span></span> <span data-ttu-id="cef2c-253">Допустимые значения зависят от дистрибутива Linux.</span><span class="sxs-lookup"><span data-stu-id="cef2c-253">Supported values vary by Linux distribution.</span></span> <span data-ttu-id="cef2c-254">Если используется строка X, в образе Linux должна присутствовать строка mkfs.X.</span><span class="sxs-lookup"><span data-stu-id="cef2c-254">If the string is X, then mkfs.X should be present on the Linux image.</span></span> <span data-ttu-id="cef2c-255">Для образов SLES 11 обычно используется значение "ext3".</span><span class="sxs-lookup"><span data-stu-id="cef2c-255">SLES 11 images should typically use 'ext3'.</span></span> <span data-ttu-id="cef2c-256">Для образов FreeBSD здесь следует использовать "ufs2".</span><span class="sxs-lookup"><span data-stu-id="cef2c-256">FreeBSD images should use 'ufs2' here.</span></span>

<span data-ttu-id="cef2c-257">**ResourceDisk.MountPoint:**</span><span class="sxs-lookup"><span data-stu-id="cef2c-257">**ResourceDisk.MountPoint:**</span></span>  
<span data-ttu-id="cef2c-258">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="cef2c-258">Type: String</span></span>  
<span data-ttu-id="cef2c-259">По умолчанию: /mnt/resource</span><span class="sxs-lookup"><span data-stu-id="cef2c-259">Default: /mnt/resource</span></span> 

<span data-ttu-id="cef2c-260">Указывает путь, по которому подключен диск ресурсов.</span><span class="sxs-lookup"><span data-stu-id="cef2c-260">This specifies the path at which the resource disk is mounted.</span></span> <span data-ttu-id="cef2c-261">Следует отметить, что диск ресурсов является *временным* диском и должен быть очищен при отмене подготовки ВМ.</span><span class="sxs-lookup"><span data-stu-id="cef2c-261">Note that the resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span>

<span data-ttu-id="cef2c-262">**ResourceDisk.MountOptions**</span><span class="sxs-lookup"><span data-stu-id="cef2c-262">**ResourceDisk.MountOptions**</span></span>  
<span data-ttu-id="cef2c-263">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="cef2c-263">Type: String</span></span>  
<span data-ttu-id="cef2c-264">По умолчанию: нет</span><span class="sxs-lookup"><span data-stu-id="cef2c-264">Default: None</span></span>

<span data-ttu-id="cef2c-265">Задает параметры монтирования диска, которые должны быть переданы команде mount -o.</span><span class="sxs-lookup"><span data-stu-id="cef2c-265">Specifies disk mount options to be passed to the mount -o command.</span></span> <span data-ttu-id="cef2c-266">Это список значений, разделенный запятыми, например</span><span class="sxs-lookup"><span data-stu-id="cef2c-266">This is a comma separated list of values, ex.</span></span> <span data-ttu-id="cef2c-267">'nodev,nosuid'.</span><span class="sxs-lookup"><span data-stu-id="cef2c-267">'nodev,nosuid'.</span></span> <span data-ttu-id="cef2c-268">Подробные сведения см. в разделе mount(8).</span><span class="sxs-lookup"><span data-stu-id="cef2c-268">See mount(8) for details.</span></span>

<span data-ttu-id="cef2c-269">**ResourceDisk.EnableSwap:**</span><span class="sxs-lookup"><span data-stu-id="cef2c-269">**ResourceDisk.EnableSwap:**</span></span>  
<span data-ttu-id="cef2c-270">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="cef2c-270">Type: Boolean</span></span>  
<span data-ttu-id="cef2c-271">По умолчанию: n</span><span class="sxs-lookup"><span data-stu-id="cef2c-271">Default: n</span></span>

<span data-ttu-id="cef2c-272">Если задано, на диске ресурсов создается файл подкачки (/swapfile), который добавляется к пространству подкачки в системе.</span><span class="sxs-lookup"><span data-stu-id="cef2c-272">If set, a swap file (/swapfile) is created on the resource disk and added to the system swap space.</span></span>

<span data-ttu-id="cef2c-273">**ResourceDisk.SwapSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="cef2c-273">**ResourceDisk.SwapSizeMB:**</span></span>  
<span data-ttu-id="cef2c-274">Тип: целое число</span><span class="sxs-lookup"><span data-stu-id="cef2c-274">Type: Integer</span></span>  
<span data-ttu-id="cef2c-275">По умолчанию: 0</span><span class="sxs-lookup"><span data-stu-id="cef2c-275">Default: 0</span></span>

<span data-ttu-id="cef2c-276">Размер файла подкачки в мегабайтах.</span><span class="sxs-lookup"><span data-stu-id="cef2c-276">The size of the swap file in megabytes.</span></span>

<span data-ttu-id="cef2c-277">**Logs.Verbose:**</span><span class="sxs-lookup"><span data-stu-id="cef2c-277">**Logs.Verbose:**</span></span>  
<span data-ttu-id="cef2c-278">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="cef2c-278">Type: Boolean</span></span>  
<span data-ttu-id="cef2c-279">По умолчанию: n</span><span class="sxs-lookup"><span data-stu-id="cef2c-279">Default: n</span></span>

<span data-ttu-id="cef2c-280">Если задано, то файл журнала расширяется.</span><span class="sxs-lookup"><span data-stu-id="cef2c-280">If set, log verbosity is boosted.</span></span> <span data-ttu-id="cef2c-281">Waagent записывает данные в /var/log/waagent.log, а также использует системную функцию logrotate для ротации журналов.</span><span class="sxs-lookup"><span data-stu-id="cef2c-281">Waagent logs to /var/log/waagent.log and leverages the system logrotate functionality to rotate logs.</span></span>

<span data-ttu-id="cef2c-282">**OS.EnableRDMA**</span><span class="sxs-lookup"><span data-stu-id="cef2c-282">**OS.EnableRDMA**</span></span>  
<span data-ttu-id="cef2c-283">Тип: логический</span><span class="sxs-lookup"><span data-stu-id="cef2c-283">Type: Boolean</span></span>  
<span data-ttu-id="cef2c-284">По умолчанию: n</span><span class="sxs-lookup"><span data-stu-id="cef2c-284">Default: n</span></span>

<span data-ttu-id="cef2c-285">Если установлен, агент попытается установить, а затем загрузить драйвер ядра RDMA, соответствующий версии встроенного ПО базового оборудования.</span><span class="sxs-lookup"><span data-stu-id="cef2c-285">If set, the agent will attempt to install and then load an RDMA kernel driver that matches the version of the firmware on the underlying hardware.</span></span>

<span data-ttu-id="cef2c-286">**OS.RootDeviceScsiTimeout:**</span><span class="sxs-lookup"><span data-stu-id="cef2c-286">**OS.RootDeviceScsiTimeout:**</span></span>  
<span data-ttu-id="cef2c-287">Тип: целое число</span><span class="sxs-lookup"><span data-stu-id="cef2c-287">Type: Integer</span></span>  
<span data-ttu-id="cef2c-288">По умолчанию: 300</span><span class="sxs-lookup"><span data-stu-id="cef2c-288">Default: 300</span></span>

<span data-ttu-id="cef2c-289">Настраивает время ожидания SCSI в секундах на дисках операционной системы и на дисках с данными.</span><span class="sxs-lookup"><span data-stu-id="cef2c-289">This configures the SCSI timeout in seconds on the OS disk and data drives.</span></span> <span data-ttu-id="cef2c-290">Если не установлено, будут использоваться системные значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cef2c-290">If not set, the system defaults are used.</span></span>

<span data-ttu-id="cef2c-291">**OS.OpensslPath:**</span><span class="sxs-lookup"><span data-stu-id="cef2c-291">**OS.OpensslPath:**</span></span>  
<span data-ttu-id="cef2c-292">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="cef2c-292">Type: String</span></span>  
<span data-ttu-id="cef2c-293">По умолчанию: нет</span><span class="sxs-lookup"><span data-stu-id="cef2c-293">Default: None</span></span>

<span data-ttu-id="cef2c-294">Можно указать альтернативный путь для двоичного файла openssl, используемого при выполнении шифрования.</span><span class="sxs-lookup"><span data-stu-id="cef2c-294">This can be used to specify an alternate path for the openssl binary to use for cryptographic operations.</span></span>

<span data-ttu-id="cef2c-295">**HttpProxy.Host, HttpProxy.Port**</span><span class="sxs-lookup"><span data-stu-id="cef2c-295">**HttpProxy.Host, HttpProxy.Port**</span></span>  
<span data-ttu-id="cef2c-296">Тип: строка</span><span class="sxs-lookup"><span data-stu-id="cef2c-296">Type: String</span></span>  
<span data-ttu-id="cef2c-297">По умолчанию: нет</span><span class="sxs-lookup"><span data-stu-id="cef2c-297">Default: None</span></span>

<span data-ttu-id="cef2c-298">Если установлен, агент будет использовать этот прокси-сервер для доступа в Интернет.</span><span class="sxs-lookup"><span data-stu-id="cef2c-298">If set, the agent will use this proxy server to access the internet.</span></span> 

## <a name="ubuntu-cloud-images"></a><span data-ttu-id="cef2c-299">Образы облаков Ubuntu</span><span class="sxs-lookup"><span data-stu-id="cef2c-299">Ubuntu Cloud Images</span></span>
<span data-ttu-id="cef2c-300">Обратите внимание, что в образах облаков Ubuntu пакет [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) используется для выполнения ряда задач настройки, которыми в противном случае управлял бы агент Linux для Azure.</span><span class="sxs-lookup"><span data-stu-id="cef2c-300">Note that Ubuntu Cloud Images utilize [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) to perform many configuration tasks that would otherwise be managed by the Azure Linux Agent.</span></span>  <span data-ttu-id="cef2c-301">Обратите внимание на следующие отличия.</span><span class="sxs-lookup"><span data-stu-id="cef2c-301">Please note the following differences:</span></span>

* <span data-ttu-id="cef2c-302">**Provisioning.Enabled** по умолчанию устанавливается значение "n" в образах облаков Ubuntu, использующих пакет cloud-init для выполнения задач по подготовке.</span><span class="sxs-lookup"><span data-stu-id="cef2c-302">**Provisioning.Enabled** defaults to "n" on Ubuntu Cloud Images that use cloud-init to perform provisioning tasks.</span></span>
* <span data-ttu-id="cef2c-303">Следующие параметры конфигурации не влияют на образы облаков Ubuntu, использующие пакеты cloud-init для управления диском ресурсов и пространством подкачки:</span><span class="sxs-lookup"><span data-stu-id="cef2c-303">The following configuration parameters have no effect on Ubuntu Cloud Images that use cloud-init to manage the resource disk and swap space:</span></span>
  
  * <span data-ttu-id="cef2c-304">**ResourceDisk.Format;**</span><span class="sxs-lookup"><span data-stu-id="cef2c-304">**ResourceDisk.Format**</span></span>
  * <span data-ttu-id="cef2c-305">**ResourceDisk.Filesystem;**</span><span class="sxs-lookup"><span data-stu-id="cef2c-305">**ResourceDisk.Filesystem**</span></span>
  * <span data-ttu-id="cef2c-306">**ResourceDisk.MountPoint;**</span><span class="sxs-lookup"><span data-stu-id="cef2c-306">**ResourceDisk.MountPoint**</span></span>
  * <span data-ttu-id="cef2c-307">**ResourceDisk.EnableSwap;**</span><span class="sxs-lookup"><span data-stu-id="cef2c-307">**ResourceDisk.EnableSwap**</span></span>
  * <span data-ttu-id="cef2c-308">**ResourceDisk.SwapSizeMB.**</span><span class="sxs-lookup"><span data-stu-id="cef2c-308">**ResourceDisk.SwapSizeMB**</span></span>
* <span data-ttu-id="cef2c-309">См. следующие ресурсы, если вам нужно настроить точку подключения диска ресурсов и пространство подкачки в образах облаков Ubuntu во время подготовки.</span><span class="sxs-lookup"><span data-stu-id="cef2c-309">Please see the following resources to configure the resource disk mount point and swap space on Ubuntu Cloud Images during provisioning:</span></span>
  
  * [<span data-ttu-id="cef2c-310">Вики-сайт по Ubuntu: настройка разделов подкачки</span><span class="sxs-lookup"><span data-stu-id="cef2c-310">Ubuntu Wiki: Configure Swap Partitions</span></span>](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [<span data-ttu-id="cef2c-311">Включение пользовательских данных в виртуальную машину Azure</span><span class="sxs-lookup"><span data-stu-id="cef2c-311">Injecting Custom Data into an Azure Virtual Machine</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

