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
# <a name="how-tooupdate-hello-azure-linux-agent-on-a-vm"></a><span data-ttu-id="9e379-103">Как tooupdate hello агент Azure Linux на виртуальной Машине</span><span class="sxs-lookup"><span data-stu-id="9e379-103">How tooupdate hello Azure Linux Agent on a VM</span></span>

<span data-ttu-id="9e379-104">tooupdate вашей [агент Azure Linux](https://github.com/Azure/WALinuxAgent) на виртуальной Машине Linux в Azure, необходимо иметь:</span><span class="sxs-lookup"><span data-stu-id="9e379-104">tooupdate your [Azure Linux Agent](https://github.com/Azure/WALinuxAgent) on a Linux VM in Azure, you must already have:</span></span>

- <span data-ttu-id="9e379-105">работающая виртуальная машина Linux в Azure;</span><span class="sxs-lookup"><span data-stu-id="9e379-105">A running Linux VM in Azure.</span></span>
- <span data-ttu-id="9e379-106">Toothat подключение виртуальных Машин Linux с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="9e379-106">A connection toothat Linux VM using SSH.</span></span>

<span data-ttu-id="9e379-107">Всегда следует выполнять проверку для пакета в репозитории дистрибутив Linux hello сначала.</span><span class="sxs-lookup"><span data-stu-id="9e379-107">You should always check for a package in hello Linux distro repository first.</span></span> <span data-ttu-id="9e379-108">Возможно доступен пакет hello не может быть hello последнюю версию, однако разрешение автоматическое обновление гарантирует hello агент Linux, всегда получают hello последнее обновление.</span><span class="sxs-lookup"><span data-stu-id="9e379-108">It is possible hello package available may not be hello latest version, however, enabling autoupdate will ensure hello Linux Agent will always get hello latest update.</span></span> <span data-ttu-id="9e379-109">При возникновении проблем при установке из hello диспетчеров пакетов, необходимо найти поддержки поставщика дистрибутив hello.</span><span class="sxs-lookup"><span data-stu-id="9e379-109">Should you have issues installing from hello package managers, you should seek support from hello distro vendor.</span></span>

## <a name="updating-hello-azure-linux-agent"></a><span data-ttu-id="9e379-110">Обновление hello Azure Linux Agent</span><span class="sxs-lookup"><span data-stu-id="9e379-110">Updating hello Azure Linux Agent</span></span>

## <a name="ubuntu"></a><span data-ttu-id="9e379-111">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="9e379-111">Ubuntu</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="9e379-112">Проверка текущей версии пакета</span><span class="sxs-lookup"><span data-stu-id="9e379-112">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="9e379-113">Обновление кэша пакета</span><span class="sxs-lookup"><span data-stu-id="9e379-113">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="9e379-114">Установите последнюю версию пакета hello</span><span class="sxs-lookup"><span data-stu-id="9e379-114">Install hello latest package version</span></span>

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="9e379-115">Гарантия включения автоматического обновления</span><span class="sxs-lookup"><span data-stu-id="9e379-115">Ensure auto update is enabled</span></span>

<span data-ttu-id="9e379-116">Во-первых проверьте toosee, если он включен:</span><span class="sxs-lookup"><span data-stu-id="9e379-116">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="9e379-117">Найдите параметр AutoUpdate.Enabled.</span><span class="sxs-lookup"><span data-stu-id="9e379-117">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="9e379-118">Если отображаются следующие результаты, значит эта возможность включена:</span><span class="sxs-lookup"><span data-stu-id="9e379-118">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="9e379-119">tooenable запуска:</span><span class="sxs-lookup"><span data-stu-id="9e379-119">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="9e379-120">Перезапустите службу waagent hello</span><span class="sxs-lookup"><span data-stu-id="9e379-120">Restart hello waagent service</span></span>

#### <a name="restart-agent-for-1404"></a><span data-ttu-id="9e379-121">Перезапуск агента для версии 14.04</span><span class="sxs-lookup"><span data-stu-id="9e379-121">Restart agent for 14.04</span></span>

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a><span data-ttu-id="9e379-122">Перезапуск агента для версии 16.04, 17.04</span><span class="sxs-lookup"><span data-stu-id="9e379-122">Restart agent for 16.04 / 17.04</span></span>

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a><span data-ttu-id="9e379-123">Debian</span><span class="sxs-lookup"><span data-stu-id="9e379-123">Debian</span></span>

### <a name="debian-7-wheezy"></a><span data-ttu-id="9e379-124">Debian 7 "Wheezy"</span><span class="sxs-lookup"><span data-stu-id="9e379-124">Debian 7 “Wheezy”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="9e379-125">Проверка текущей версии пакета</span><span class="sxs-lookup"><span data-stu-id="9e379-125">Check your current package version</span></span>

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="9e379-126">Обновление кэша пакета</span><span class="sxs-lookup"><span data-stu-id="9e379-126">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="9e379-127">Установите последнюю версию пакета hello</span><span class="sxs-lookup"><span data-stu-id="9e379-127">Install hello latest package version</span></span>

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a><span data-ttu-id="9e379-128">Включение автоматического обновления агента</span><span class="sxs-lookup"><span data-stu-id="9e379-128">Enable agent auto update</span></span>
<span data-ttu-id="9e379-129">В этой версии Debian нет версии агента не ниже 2.0.16, поэтому для нее недоступно автоматическое обновление.</span><span class="sxs-lookup"><span data-stu-id="9e379-129">This version of Debian does not have a version >= 2.0.16, therefore AutoUpdate is not available for it.</span></span> <span data-ttu-id="9e379-130">Hello вывод hello выше команду Показать, если пакет hello актуален.</span><span class="sxs-lookup"><span data-stu-id="9e379-130">hello output from hello above command will show you if hello package is up-to-date.</span></span>

### <a name="debian-8-jessie--debian-9-stretch"></a><span data-ttu-id="9e379-131">Debian 8 "Jessie" и Debian 9 "Stretch"</span><span class="sxs-lookup"><span data-stu-id="9e379-131">Debian 8 “Jessie” / Debian 9 “Stretch”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="9e379-132">Проверка текущей версии пакета</span><span class="sxs-lookup"><span data-stu-id="9e379-132">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="9e379-133">Обновление кэша пакета</span><span class="sxs-lookup"><span data-stu-id="9e379-133">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="9e379-134">Установите последнюю версию пакета hello</span><span class="sxs-lookup"><span data-stu-id="9e379-134">Install hello latest package version</span></span>

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="9e379-135">Гарантия включения автоматического обновления</span><span class="sxs-lookup"><span data-stu-id="9e379-135">Ensure auto update is enabled</span></span> 

<span data-ttu-id="9e379-136">Во-первых проверьте toosee, если он включен:</span><span class="sxs-lookup"><span data-stu-id="9e379-136">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="9e379-137">Найдите параметр AutoUpdate.Enabled.</span><span class="sxs-lookup"><span data-stu-id="9e379-137">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="9e379-138">Если отображаются следующие результаты, значит эта возможность включена:</span><span class="sxs-lookup"><span data-stu-id="9e379-138">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="9e379-139">tooenable запуска:</span><span class="sxs-lookup"><span data-stu-id="9e379-139">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="9e379-140">Перезапустите службу waagent hello</span><span class="sxs-lookup"><span data-stu-id="9e379-140">Restart hello waagent service</span></span>

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a><span data-ttu-id="9e379-141">RedHat или CentOS</span><span class="sxs-lookup"><span data-stu-id="9e379-141">Redhat / CentOS</span></span>

### <a name="rhelcentos-6"></a><span data-ttu-id="9e379-142">RHEL или CentOS 6</span><span class="sxs-lookup"><span data-stu-id="9e379-142">RHEL/CentOS 6</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="9e379-143">Проверка текущей версии пакета</span><span class="sxs-lookup"><span data-stu-id="9e379-143">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="9e379-144">Проверка доступных обновлений</span><span class="sxs-lookup"><span data-stu-id="9e379-144">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="9e379-145">Установите последнюю версию пакета hello</span><span class="sxs-lookup"><span data-stu-id="9e379-145">Install hello latest package version</span></span>

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="9e379-146">Гарантия включения автоматического обновления</span><span class="sxs-lookup"><span data-stu-id="9e379-146">Ensure auto update is enabled</span></span> 

<span data-ttu-id="9e379-147">Во-первых проверьте toosee, если он включен:</span><span class="sxs-lookup"><span data-stu-id="9e379-147">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="9e379-148">Найдите параметр AutoUpdate.Enabled.</span><span class="sxs-lookup"><span data-stu-id="9e379-148">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="9e379-149">Если отображаются следующие результаты, значит эта возможность включена:</span><span class="sxs-lookup"><span data-stu-id="9e379-149">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="9e379-150">tooenable запуска:</span><span class="sxs-lookup"><span data-stu-id="9e379-150">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="9e379-151">Перезапустите службу waagent hello</span><span class="sxs-lookup"><span data-stu-id="9e379-151">Restart hello waagent service</span></span>

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a><span data-ttu-id="9e379-152">RHEL или CentOS 7</span><span class="sxs-lookup"><span data-stu-id="9e379-152">RHEL/CentOS 7</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="9e379-153">Проверка текущей версии пакета</span><span class="sxs-lookup"><span data-stu-id="9e379-153">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="9e379-154">Проверка доступных обновлений</span><span class="sxs-lookup"><span data-stu-id="9e379-154">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="9e379-155">Установите последнюю версию пакета hello</span><span class="sxs-lookup"><span data-stu-id="9e379-155">Install hello latest package version</span></span>

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="9e379-156">Гарантия включения автоматического обновления</span><span class="sxs-lookup"><span data-stu-id="9e379-156">Ensure auto update is enabled</span></span> 

<span data-ttu-id="9e379-157">Во-первых проверьте toosee, если он включен:</span><span class="sxs-lookup"><span data-stu-id="9e379-157">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="9e379-158">Найдите параметр AutoUpdate.Enabled.</span><span class="sxs-lookup"><span data-stu-id="9e379-158">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="9e379-159">Если отображаются следующие результаты, значит эта возможность включена:</span><span class="sxs-lookup"><span data-stu-id="9e379-159">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="9e379-160">tooenable запуска:</span><span class="sxs-lookup"><span data-stu-id="9e379-160">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="9e379-161">Перезапустите службу waagent hello</span><span class="sxs-lookup"><span data-stu-id="9e379-161">Restart hello waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a><span data-ttu-id="9e379-162">SUSE SLES</span><span class="sxs-lookup"><span data-stu-id="9e379-162">SUSE SLES</span></span>

### <a name="suse-sles-11-sp4"></a><span data-ttu-id="9e379-163">SUSE SLES 11 SP4</span><span class="sxs-lookup"><span data-stu-id="9e379-163">SUSE SLES 11 SP4</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="9e379-164">Проверка текущей версии пакета</span><span class="sxs-lookup"><span data-stu-id="9e379-164">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="9e379-165">Проверка доступных обновлений</span><span class="sxs-lookup"><span data-stu-id="9e379-165">Check available updates</span></span>

<span data-ttu-id="9e379-166">Hello выше выходных данных будет показано, если пакет hello работает toodate.</span><span class="sxs-lookup"><span data-stu-id="9e379-166">hello above output will show you if hello package is up toodate.</span></span>

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="9e379-167">Установите последнюю версию пакета hello</span><span class="sxs-lookup"><span data-stu-id="9e379-167">Install hello latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="9e379-168">Гарантия включения автоматического обновления</span><span class="sxs-lookup"><span data-stu-id="9e379-168">Ensure auto update is enabled</span></span> 

<span data-ttu-id="9e379-169">Во-первых проверьте toosee, если он включен:</span><span class="sxs-lookup"><span data-stu-id="9e379-169">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="9e379-170">Найдите параметр AutoUpdate.Enabled.</span><span class="sxs-lookup"><span data-stu-id="9e379-170">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="9e379-171">Если отображаются следующие результаты, значит эта возможность включена:</span><span class="sxs-lookup"><span data-stu-id="9e379-171">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="9e379-172">tooenable запуска:</span><span class="sxs-lookup"><span data-stu-id="9e379-172">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="9e379-173">Перезапустите службу waagent hello</span><span class="sxs-lookup"><span data-stu-id="9e379-173">Restart hello waagent service</span></span>

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a><span data-ttu-id="9e379-174">SUSE SLES 12 SP2</span><span class="sxs-lookup"><span data-stu-id="9e379-174">SUSE SLES 12 SP2</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="9e379-175">Проверка текущей версии пакета</span><span class="sxs-lookup"><span data-stu-id="9e379-175">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="9e379-176">Проверка доступных обновлений</span><span class="sxs-lookup"><span data-stu-id="9e379-176">Check available updates</span></span>

<span data-ttu-id="9e379-177">В выходных данных hello hello выше здесь вы найдете Если пакет hello не требует обновления.</span><span class="sxs-lookup"><span data-stu-id="9e379-177">In hello output from hello above, this will show you if hello package is upto date.</span></span>

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="9e379-178">Установите последнюю версию пакета hello</span><span class="sxs-lookup"><span data-stu-id="9e379-178">Install hello latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="9e379-179">Гарантия включения автоматического обновления</span><span class="sxs-lookup"><span data-stu-id="9e379-179">Ensure auto update is enabled</span></span> 

<span data-ttu-id="9e379-180">Во-первых проверьте toosee, если он включен:</span><span class="sxs-lookup"><span data-stu-id="9e379-180">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="9e379-181">Найдите параметр AutoUpdate.Enabled.</span><span class="sxs-lookup"><span data-stu-id="9e379-181">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="9e379-182">Если отображаются следующие результаты, значит эта возможность включена:</span><span class="sxs-lookup"><span data-stu-id="9e379-182">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="9e379-183">tooenable запуска:</span><span class="sxs-lookup"><span data-stu-id="9e379-183">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="9e379-184">Перезапустите службу waagent hello</span><span class="sxs-lookup"><span data-stu-id="9e379-184">Restart hello waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a><span data-ttu-id="9e379-185">Oracle 6 и 7</span><span class="sxs-lookup"><span data-stu-id="9e379-185">Oracle 6 and 7</span></span>

<span data-ttu-id="9e379-186">Oracle Linux, убедитесь, что hello `Addons` репозитория включена.</span><span class="sxs-lookup"><span data-stu-id="9e379-186">For Oracle Linux, make sure that hello `Addons` repository is enabled.</span></span> <span data-ttu-id="9e379-187">Выберите файл hello tooedit `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) или `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux) и измените строку hello `enabled=0` слишком`enabled=1` под **[ol6_addons]** или **[ol7_addons]** в этом файле.</span><span class="sxs-lookup"><span data-stu-id="9e379-187">Choose tooedit hello file `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), and change hello line `enabled=0` too`enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

<span data-ttu-id="9e379-188">Затем tooinstall hello последнюю версию hello Azure Linux Agent типа:</span><span class="sxs-lookup"><span data-stu-id="9e379-188">Then, tooinstall hello latest version of hello Azure Linux Agent, type:</span></span>

```bash
sudo yum install WALinuxAgent
```

<span data-ttu-id="9e379-189">Если вы не нашли репозитория hello надстройку можно просто добавить эти строки в конце hello файла .repo tooyour Oracle Linux выпуск в соответствии с:</span><span class="sxs-lookup"><span data-stu-id="9e379-189">If you don't find hello add-on repository you can simply add these lines at hello end of your .repo file according tooyour Oracle Linux release:</span></span>

<span data-ttu-id="9e379-190">Для виртуальных машин Oracle Linux 6.</span><span class="sxs-lookup"><span data-stu-id="9e379-190">For Oracle Linux 6 virtual machines:</span></span>

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

<span data-ttu-id="9e379-191">Для виртуальных машин Oracle Linux 7.</span><span class="sxs-lookup"><span data-stu-id="9e379-191">For Oracle Linux 7 virtual machines:</span></span>

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

<span data-ttu-id="9e379-192">Затем введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9e379-192">Then type:</span></span>

```bash
sudo yum update WALinuxAgent
```

<span data-ttu-id="9e379-193">Обычно это все, что требуется, но если для какой-либо причине требуется tooinstall из https://github.com напрямую, hello используйте следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="9e379-193">Typically this is all you need, but if for some reason you need tooinstall it from https://github.com directly, use hello following steps.</span></span>


## <a name="update-hello-linux-agent-when-no-agent-package-exists-for-distribution"></a><span data-ttu-id="9e379-194">Обновить агент Linux hello существование без агента пакета для распространения</span><span class="sxs-lookup"><span data-stu-id="9e379-194">Update hello Linux Agent when no agent package exists for distribution</span></span>

<span data-ttu-id="9e379-195">Для установки wget (отсутствуют некоторые дистрибутивы, не устанавливайте значение по умолчанию, например Redhat CentOS и Oracle Linux версии 6.4 и 6.5) введите `sudo yum install wget` hello в командной строке.</span><span class="sxs-lookup"><span data-stu-id="9e379-195">Install wget (there are some distros that don't install it by default, such as Redhat, CentOS, and Oracle Linux versions 6.4 and 6.5) by typing `sudo yum install wget` on hello command line.</span></span>

### <a name="1-download-hello-latest-version"></a><span data-ttu-id="9e379-196">1. Загрузка последней версии hello</span><span class="sxs-lookup"><span data-stu-id="9e379-196">1. Download hello latest version</span></span>
<span data-ttu-id="9e379-197">Откройте [hello выпуска Azure Linux Agent в GitHub](https://github.com/Azure/WALinuxAgent/releases) в веб-страницы, а также узнать номер последней версии hello.</span><span class="sxs-lookup"><span data-stu-id="9e379-197">Open [hello release of Azure Linux Agent in GitHub](https://github.com/Azure/WALinuxAgent/releases) in a web page, and find out hello latest version number.</span></span> <span data-ttu-id="9e379-198">(Номер текущей версии можно узнать, введя `waagent --version`.)</span><span class="sxs-lookup"><span data-stu-id="9e379-198">(You can locate your current version by typing `waagent --version`.)</span></span>

#### <a name="for-version-22x-or-later-type"></a><span data-ttu-id="9e379-199">Для версии 2.2.x или более поздней версии введите:</span><span class="sxs-lookup"><span data-stu-id="9e379-199">For version 2.2.x or later, type:</span></span>
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

<span data-ttu-id="9e379-200">Hello следующую строку версии 2.2.0 в качестве примера используется:</span><span class="sxs-lookup"><span data-stu-id="9e379-200">hello following line uses version 2.2.0 as an example:</span></span>

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-hello-azure-linux-agent"></a><span data-ttu-id="9e379-201">2. Установите агент Azure Linux hello</span><span class="sxs-lookup"><span data-stu-id="9e379-201">2. Install hello Azure Linux Agent</span></span>

#### <a name="for-version-22x-use"></a><span data-ttu-id="9e379-202">Для версии 2.2.x введите:</span><span class="sxs-lookup"><span data-stu-id="9e379-202">For version 2.2.x, use:</span></span>
<span data-ttu-id="9e379-203">Может потребоваться пакет hello tooinstall `setuptools` сначала — в разделе [здесь](https://pypi.python.org/pypi/setuptools).</span><span class="sxs-lookup"><span data-stu-id="9e379-203">You may need tooinstall hello package `setuptools` first--see [here](https://pypi.python.org/pypi/setuptools).</span></span> <span data-ttu-id="9e379-204">Далее выполните:</span><span class="sxs-lookup"><span data-stu-id="9e379-204">Then run:</span></span>

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="9e379-205">Гарантия включения автоматического обновления</span><span class="sxs-lookup"><span data-stu-id="9e379-205">Ensure auto update is enabled</span></span>

<span data-ttu-id="9e379-206">Во-первых проверьте toosee, если он включен:</span><span class="sxs-lookup"><span data-stu-id="9e379-206">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="9e379-207">Найдите параметр AutoUpdate.Enabled.</span><span class="sxs-lookup"><span data-stu-id="9e379-207">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="9e379-208">Если отображаются следующие результаты, значит эта возможность включена:</span><span class="sxs-lookup"><span data-stu-id="9e379-208">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="9e379-209">tooenable запуска:</span><span class="sxs-lookup"><span data-stu-id="9e379-209">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-hello-waagent-service"></a><span data-ttu-id="9e379-210">3. Перезапустите службу waagent hello</span><span class="sxs-lookup"><span data-stu-id="9e379-210">3. Restart hello waagent service</span></span>
<span data-ttu-id="9e379-211">Для большинства дистрибутивов Linux:</span><span class="sxs-lookup"><span data-stu-id="9e379-211">For most of Linux distros:</span></span>

```bash
sudo service waagent restart
```

<span data-ttu-id="9e379-212">Для Ubuntu используйте:</span><span class="sxs-lookup"><span data-stu-id="9e379-212">For Ubuntu, use:</span></span>

```bash
sudo service walinuxagent restart
```

<span data-ttu-id="9e379-213">Для CoreOS используйте:</span><span class="sxs-lookup"><span data-stu-id="9e379-213">For CoreOS, use:</span></span>

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-hello-azure-linux-agent-version"></a><span data-ttu-id="9e379-214">4. Проверить версию агента Azure Linux hello</span><span class="sxs-lookup"><span data-stu-id="9e379-214">4. Confirm hello Azure Linux Agent version</span></span>
    
```bash
waagent -version
```

<span data-ttu-id="9e379-215">Для CoreOS hello выше команды может не работать.</span><span class="sxs-lookup"><span data-stu-id="9e379-215">For CoreOS, hello above command may not work.</span></span>

<span data-ttu-id="9e379-216">Вы увидите, что hello Azure Linux Agent версия была обновленных toohello новой версии.</span><span class="sxs-lookup"><span data-stu-id="9e379-216">You will see that hello Azure Linux Agent version has been updated toohello new version.</span></span>

<span data-ttu-id="9e379-217">Дополнительные сведения о hello агент Azure Linux см. в разделе [README агента Azure Linux](https://github.com/Azure/WALinuxAgent).</span><span class="sxs-lookup"><span data-stu-id="9e379-217">For more information regarding hello Azure Linux Agent, see [Azure Linux Agent README](https://github.com/Azure/WALinuxAgent).</span></span>
