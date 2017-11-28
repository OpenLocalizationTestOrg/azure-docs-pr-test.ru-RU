---
title: "Обновление агента Linux для Azure из GitHub | Документация Майкрософт"
description: "Узнайте, как обновить агент Linux для Azure на виртуальной машине Linux до последней версии с сайта GitHub."
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
ms.openlocfilehash: c79e37976a58ae5384b5856e0f7f258a773ef0fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-update-the-azure-linux-agent-on-a-vm"></a><span data-ttu-id="a2270-103">Как обновить агент Azure Linux на виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="a2270-103">How to update the Azure Linux Agent on a VM</span></span>

<span data-ttu-id="a2270-104">Для обновления [агента Linux для Azure](https://github.com/Azure/WALinuxAgent) на виртуальной машине Linux требуется:</span><span class="sxs-lookup"><span data-stu-id="a2270-104">To update your [Azure Linux Agent](https://github.com/Azure/WALinuxAgent) on a Linux VM in Azure, you must already have:</span></span>

- <span data-ttu-id="a2270-105">работающая виртуальная машина Linux в Azure;</span><span class="sxs-lookup"><span data-stu-id="a2270-105">A running Linux VM in Azure.</span></span>
- <span data-ttu-id="a2270-106">подключение к этой виртуальной машине Linux с помощью протокола SSH.</span><span class="sxs-lookup"><span data-stu-id="a2270-106">A connection to that Linux VM using SSH.</span></span>

<span data-ttu-id="a2270-107">Пакет нужно всегда сначала проверять в репозитории дистрибутива Linux.</span><span class="sxs-lookup"><span data-stu-id="a2270-107">You should always check for a package in the Linux distro repository first.</span></span> <span data-ttu-id="a2270-108">Возможно, доступный пакет будет не последней версии. Тем не менее после включения автоматического обновления агент Linux будет всегда получать последнее обновление.</span><span class="sxs-lookup"><span data-stu-id="a2270-108">It is possible the package available may not be the latest version, however, enabling autoupdate will ensure the Linux Agent will always get the latest update.</span></span> <span data-ttu-id="a2270-109">При возникновении проблем во время установки из диспетчеров пакетов за поддержкой обратитесь к поставщику дистрибутива.</span><span class="sxs-lookup"><span data-stu-id="a2270-109">Should you have issues installing from the package managers, you should seek support from the distro vendor.</span></span>

## <a name="updating-the-azure-linux-agent"></a><span data-ttu-id="a2270-110">Обновление агента Linux для Azure</span><span class="sxs-lookup"><span data-stu-id="a2270-110">Updating the Azure Linux Agent</span></span>

## <a name="ubuntu"></a><span data-ttu-id="a2270-111">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="a2270-111">Ubuntu</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="a2270-112">Проверка текущей версии пакета</span><span class="sxs-lookup"><span data-stu-id="a2270-112">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="a2270-113">Обновление кэша пакета</span><span class="sxs-lookup"><span data-stu-id="a2270-113">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="a2270-114">Установка последней версии пакета</span><span class="sxs-lookup"><span data-stu-id="a2270-114">Install the latest package version</span></span>

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="a2270-115">Гарантия включения автоматического обновления</span><span class="sxs-lookup"><span data-stu-id="a2270-115">Ensure auto update is enabled</span></span>

<span data-ttu-id="a2270-116">Сначала проверьте, включено ли автоматическое обновление:</span><span class="sxs-lookup"><span data-stu-id="a2270-116">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="a2270-117">Найдите параметр AutoUpdate.Enabled.</span><span class="sxs-lookup"><span data-stu-id="a2270-117">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="a2270-118">Если отображаются следующие результаты, значит эта возможность включена:</span><span class="sxs-lookup"><span data-stu-id="a2270-118">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="a2270-119">Чтобы включить автоматическое обновление, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a2270-119">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="a2270-120">Перезапустите службу waagent</span><span class="sxs-lookup"><span data-stu-id="a2270-120">Restart the waagent service</span></span>

#### <a name="restart-agent-for-1404"></a><span data-ttu-id="a2270-121">Перезапуск агента для версии 14.04</span><span class="sxs-lookup"><span data-stu-id="a2270-121">Restart agent for 14.04</span></span>

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a><span data-ttu-id="a2270-122">Перезапуск агента для версии 16.04, 17.04</span><span class="sxs-lookup"><span data-stu-id="a2270-122">Restart agent for 16.04 / 17.04</span></span>

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a><span data-ttu-id="a2270-123">Debian</span><span class="sxs-lookup"><span data-stu-id="a2270-123">Debian</span></span>

### <a name="debian-7-wheezy"></a><span data-ttu-id="a2270-124">Debian 7 "Wheezy"</span><span class="sxs-lookup"><span data-stu-id="a2270-124">Debian 7 “Wheezy”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="a2270-125">Проверка текущей версии пакета</span><span class="sxs-lookup"><span data-stu-id="a2270-125">Check your current package version</span></span>

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="a2270-126">Обновление кэша пакета</span><span class="sxs-lookup"><span data-stu-id="a2270-126">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="a2270-127">Установка последней версии пакета</span><span class="sxs-lookup"><span data-stu-id="a2270-127">Install the latest package version</span></span>

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a><span data-ttu-id="a2270-128">Включение автоматического обновления агента</span><span class="sxs-lookup"><span data-stu-id="a2270-128">Enable agent auto update</span></span>
<span data-ttu-id="a2270-129">В этой версии Debian нет версии агента не ниже 2.0.16, поэтому для нее недоступно автоматическое обновление.</span><span class="sxs-lookup"><span data-stu-id="a2270-129">This version of Debian does not have a version >= 2.0.16, therefore AutoUpdate is not available for it.</span></span> <span data-ttu-id="a2270-130">Проанализировав выходные данные команды выше, можно определить, обновлен ли пакет.</span><span class="sxs-lookup"><span data-stu-id="a2270-130">The output from the above command will show you if the package is up-to-date.</span></span>

### <a name="debian-8-jessie--debian-9-stretch"></a><span data-ttu-id="a2270-131">Debian 8 "Jessie" и Debian 9 "Stretch"</span><span class="sxs-lookup"><span data-stu-id="a2270-131">Debian 8 “Jessie” / Debian 9 “Stretch”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="a2270-132">Проверка текущей версии пакета</span><span class="sxs-lookup"><span data-stu-id="a2270-132">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="a2270-133">Обновление кэша пакета</span><span class="sxs-lookup"><span data-stu-id="a2270-133">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="a2270-134">Установка последней версии пакета</span><span class="sxs-lookup"><span data-stu-id="a2270-134">Install the latest package version</span></span>

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="a2270-135">Гарантия включения автоматического обновления</span><span class="sxs-lookup"><span data-stu-id="a2270-135">Ensure auto update is enabled</span></span> 

<span data-ttu-id="a2270-136">Сначала проверьте, включено ли автоматическое обновление:</span><span class="sxs-lookup"><span data-stu-id="a2270-136">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="a2270-137">Найдите параметр AutoUpdate.Enabled.</span><span class="sxs-lookup"><span data-stu-id="a2270-137">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="a2270-138">Если отображаются следующие результаты, значит эта возможность включена:</span><span class="sxs-lookup"><span data-stu-id="a2270-138">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="a2270-139">Чтобы включить автоматическое обновление, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a2270-139">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="a2270-140">Перезапустите службу waagent</span><span class="sxs-lookup"><span data-stu-id="a2270-140">Restart the waagent service</span></span>

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a><span data-ttu-id="a2270-141">RedHat или CentOS</span><span class="sxs-lookup"><span data-stu-id="a2270-141">Redhat / CentOS</span></span>

### <a name="rhelcentos-6"></a><span data-ttu-id="a2270-142">RHEL или CentOS 6</span><span class="sxs-lookup"><span data-stu-id="a2270-142">RHEL/CentOS 6</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="a2270-143">Проверка текущей версии пакета</span><span class="sxs-lookup"><span data-stu-id="a2270-143">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="a2270-144">Проверка доступных обновлений</span><span class="sxs-lookup"><span data-stu-id="a2270-144">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="a2270-145">Установка последней версии пакета</span><span class="sxs-lookup"><span data-stu-id="a2270-145">Install the latest package version</span></span>

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="a2270-146">Гарантия включения автоматического обновления</span><span class="sxs-lookup"><span data-stu-id="a2270-146">Ensure auto update is enabled</span></span> 

<span data-ttu-id="a2270-147">Сначала проверьте, включено ли автоматическое обновление:</span><span class="sxs-lookup"><span data-stu-id="a2270-147">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="a2270-148">Найдите параметр AutoUpdate.Enabled.</span><span class="sxs-lookup"><span data-stu-id="a2270-148">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="a2270-149">Если отображаются следующие результаты, значит эта возможность включена:</span><span class="sxs-lookup"><span data-stu-id="a2270-149">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="a2270-150">Чтобы включить автоматическое обновление, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a2270-150">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="a2270-151">Перезапустите службу waagent</span><span class="sxs-lookup"><span data-stu-id="a2270-151">Restart the waagent service</span></span>

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a><span data-ttu-id="a2270-152">RHEL или CentOS 7</span><span class="sxs-lookup"><span data-stu-id="a2270-152">RHEL/CentOS 7</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="a2270-153">Проверка текущей версии пакета</span><span class="sxs-lookup"><span data-stu-id="a2270-153">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="a2270-154">Проверка доступных обновлений</span><span class="sxs-lookup"><span data-stu-id="a2270-154">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="a2270-155">Установка последней версии пакета</span><span class="sxs-lookup"><span data-stu-id="a2270-155">Install the latest package version</span></span>

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="a2270-156">Гарантия включения автоматического обновления</span><span class="sxs-lookup"><span data-stu-id="a2270-156">Ensure auto update is enabled</span></span> 

<span data-ttu-id="a2270-157">Сначала проверьте, включено ли автоматическое обновление:</span><span class="sxs-lookup"><span data-stu-id="a2270-157">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="a2270-158">Найдите параметр AutoUpdate.Enabled.</span><span class="sxs-lookup"><span data-stu-id="a2270-158">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="a2270-159">Если отображаются следующие результаты, значит эта возможность включена:</span><span class="sxs-lookup"><span data-stu-id="a2270-159">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="a2270-160">Чтобы включить автоматическое обновление, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a2270-160">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="a2270-161">Перезапустите службу waagent</span><span class="sxs-lookup"><span data-stu-id="a2270-161">Restart the waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a><span data-ttu-id="a2270-162">SUSE SLES</span><span class="sxs-lookup"><span data-stu-id="a2270-162">SUSE SLES</span></span>

### <a name="suse-sles-11-sp4"></a><span data-ttu-id="a2270-163">SUSE SLES 11 SP4</span><span class="sxs-lookup"><span data-stu-id="a2270-163">SUSE SLES 11 SP4</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="a2270-164">Проверка текущей версии пакета</span><span class="sxs-lookup"><span data-stu-id="a2270-164">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="a2270-165">Проверка доступных обновлений</span><span class="sxs-lookup"><span data-stu-id="a2270-165">Check available updates</span></span>

<span data-ttu-id="a2270-166">Проанализировав выходные данные выше, можно определить, обновлен ли пакет.</span><span class="sxs-lookup"><span data-stu-id="a2270-166">The above output will show you if the package is up to date.</span></span>

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="a2270-167">Установка последней версии пакета</span><span class="sxs-lookup"><span data-stu-id="a2270-167">Install the latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="a2270-168">Гарантия включения автоматического обновления</span><span class="sxs-lookup"><span data-stu-id="a2270-168">Ensure auto update is enabled</span></span> 

<span data-ttu-id="a2270-169">Сначала проверьте, включено ли автоматическое обновление:</span><span class="sxs-lookup"><span data-stu-id="a2270-169">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="a2270-170">Найдите параметр AutoUpdate.Enabled.</span><span class="sxs-lookup"><span data-stu-id="a2270-170">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="a2270-171">Если отображаются следующие результаты, значит эта возможность включена:</span><span class="sxs-lookup"><span data-stu-id="a2270-171">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="a2270-172">Чтобы включить автоматическое обновление, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a2270-172">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="a2270-173">Перезапустите службу waagent</span><span class="sxs-lookup"><span data-stu-id="a2270-173">Restart the waagent service</span></span>

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a><span data-ttu-id="a2270-174">SUSE SLES 12 SP2</span><span class="sxs-lookup"><span data-stu-id="a2270-174">SUSE SLES 12 SP2</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="a2270-175">Проверка текущей версии пакета</span><span class="sxs-lookup"><span data-stu-id="a2270-175">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="a2270-176">Проверка доступных обновлений</span><span class="sxs-lookup"><span data-stu-id="a2270-176">Check available updates</span></span>

<span data-ttu-id="a2270-177">Проанализировав выходные данные выше, можно определить, обновлен ли пакет.</span><span class="sxs-lookup"><span data-stu-id="a2270-177">In the output from the above, this will show you if the package is upto date.</span></span>

#### <a name="install-the-latest-package-version"></a><span data-ttu-id="a2270-178">Установка последней версии пакета</span><span class="sxs-lookup"><span data-stu-id="a2270-178">Install the latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="a2270-179">Гарантия включения автоматического обновления</span><span class="sxs-lookup"><span data-stu-id="a2270-179">Ensure auto update is enabled</span></span> 

<span data-ttu-id="a2270-180">Сначала проверьте, включено ли автоматическое обновление:</span><span class="sxs-lookup"><span data-stu-id="a2270-180">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="a2270-181">Найдите параметр AutoUpdate.Enabled.</span><span class="sxs-lookup"><span data-stu-id="a2270-181">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="a2270-182">Если отображаются следующие результаты, значит эта возможность включена:</span><span class="sxs-lookup"><span data-stu-id="a2270-182">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="a2270-183">Чтобы включить автоматическое обновление, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a2270-183">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-the-waagent-service"></a><span data-ttu-id="a2270-184">Перезапустите службу waagent</span><span class="sxs-lookup"><span data-stu-id="a2270-184">Restart the waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a><span data-ttu-id="a2270-185">Oracle 6 и 7</span><span class="sxs-lookup"><span data-stu-id="a2270-185">Oracle 6 and 7</span></span>

<span data-ttu-id="a2270-186">При работе с Oracle Linux убедитесь, что включен репозиторий `Addons` .</span><span class="sxs-lookup"><span data-stu-id="a2270-186">For Oracle Linux, make sure that the `Addons` repository is enabled.</span></span> <span data-ttu-id="a2270-187">Откройте для редактирования файл `/etc/yum.repos.d/public-yum-ol6.repo` (Oracle Linux 6) или `/etc/yum.repos.d/public-yum-ol7.repo` (Oracle Linux) и замените в нем строку `enabled=0` на строку `enabled=1` в разделе **[ol6_addons]** или **[ol7_addons]**.</span><span class="sxs-lookup"><span data-stu-id="a2270-187">Choose to edit the file `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), and change the line `enabled=0` to `enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

<span data-ttu-id="a2270-188">Затем введите следующие команды для установки последней версии агента Linux для Azure:</span><span class="sxs-lookup"><span data-stu-id="a2270-188">Then, to install the latest version of the Azure Linux Agent, type:</span></span>

```bash
sudo yum install WALinuxAgent
```

<span data-ttu-id="a2270-189">Если вы не нашли репозиторий надстроек, можно просто добавить следующие строки в конец REPO-файла в соответствии с используемой версией Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="a2270-189">If you don't find the add-on repository you can simply add these lines at the end of your .repo file according to your Oracle Linux release:</span></span>

<span data-ttu-id="a2270-190">Для виртуальных машин Oracle Linux 6.</span><span class="sxs-lookup"><span data-stu-id="a2270-190">For Oracle Linux 6 virtual machines:</span></span>

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

<span data-ttu-id="a2270-191">Для виртуальных машин Oracle Linux 7.</span><span class="sxs-lookup"><span data-stu-id="a2270-191">For Oracle Linux 7 virtual machines:</span></span>

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

<span data-ttu-id="a2270-192">Затем введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a2270-192">Then type:</span></span>

```bash
sudo yum update WALinuxAgent
```

<span data-ttu-id="a2270-193">Обычно это все, что требуется. Но если по какой-либо причине необходимо установить его с сайта https://github.com напрямую, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="a2270-193">Typically this is all you need, but if for some reason you need to install it from https://github.com directly, use the following steps.</span></span>


## <a name="update-the-linux-agent-when-no-agent-package-exists-for-distribution"></a><span data-ttu-id="a2270-194">Обновление агента Linux, если пакет агента для дистрибутива не существует</span><span class="sxs-lookup"><span data-stu-id="a2270-194">Update the Linux Agent when no agent package exists for distribution</span></span>

<span data-ttu-id="a2270-195">Установите wget (некоторые дистрибутивы не устанавливают его по умолчанию, например Redhat, CentOS и Oracle Linux версий 6.4 и 6.5), введя `sudo yum install wget` в командной строке.</span><span class="sxs-lookup"><span data-stu-id="a2270-195">Install wget (there are some distros that don't install it by default, such as Redhat, CentOS, and Oracle Linux versions 6.4 and 6.5) by typing `sudo yum install wget` on the command line.</span></span>

### <a name="1-download-the-latest-version"></a><span data-ttu-id="a2270-196">1. Скачайте последнюю версию</span><span class="sxs-lookup"><span data-stu-id="a2270-196">1. Download the latest version</span></span>
<span data-ttu-id="a2270-197">Откройте [выпуск агента Linux для Azure в GitHub](https://github.com/Azure/WALinuxAgent/releases) на веб-странице и узнайте номер последней версии.</span><span class="sxs-lookup"><span data-stu-id="a2270-197">Open [the release of Azure Linux Agent in GitHub](https://github.com/Azure/WALinuxAgent/releases) in a web page, and find out the latest version number.</span></span> <span data-ttu-id="a2270-198">(Номер текущей версии можно узнать, введя `waagent --version`.)</span><span class="sxs-lookup"><span data-stu-id="a2270-198">(You can locate your current version by typing `waagent --version`.)</span></span>

#### <a name="for-version-22x-or-later-type"></a><span data-ttu-id="a2270-199">Для версии 2.2.x или более поздней версии введите:</span><span class="sxs-lookup"><span data-stu-id="a2270-199">For version 2.2.x or later, type:</span></span>
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

<span data-ttu-id="a2270-200">В следующей строке используется версия 2.2.0 в качестве примера:</span><span class="sxs-lookup"><span data-stu-id="a2270-200">The following line uses version 2.2.0 as an example:</span></span>

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-the-azure-linux-agent"></a><span data-ttu-id="a2270-201">2) Установка агента Linux для Azure</span><span class="sxs-lookup"><span data-stu-id="a2270-201">2. Install the Azure Linux Agent</span></span>

#### <a name="for-version-22x-use"></a><span data-ttu-id="a2270-202">Для версии 2.2.x введите:</span><span class="sxs-lookup"><span data-stu-id="a2270-202">For version 2.2.x, use:</span></span>
<span data-ttu-id="a2270-203">Возможно, сначала потребуется установить пакет `setuptools`. Ознакомьтесь со сведениями, приведенными [здесь](https://pypi.python.org/pypi/setuptools).</span><span class="sxs-lookup"><span data-stu-id="a2270-203">You may need to install the package `setuptools` first--see [here](https://pypi.python.org/pypi/setuptools).</span></span> <span data-ttu-id="a2270-204">Далее выполните:</span><span class="sxs-lookup"><span data-stu-id="a2270-204">Then run:</span></span>

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="a2270-205">Гарантия включения автоматического обновления</span><span class="sxs-lookup"><span data-stu-id="a2270-205">Ensure auto update is enabled</span></span>

<span data-ttu-id="a2270-206">Сначала проверьте, включено ли автоматическое обновление:</span><span class="sxs-lookup"><span data-stu-id="a2270-206">First, check to see if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="a2270-207">Найдите параметр AutoUpdate.Enabled.</span><span class="sxs-lookup"><span data-stu-id="a2270-207">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="a2270-208">Если отображаются следующие результаты, значит эта возможность включена:</span><span class="sxs-lookup"><span data-stu-id="a2270-208">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="a2270-209">Чтобы включить автоматическое обновление, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a2270-209">To enable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-the-waagent-service"></a><span data-ttu-id="a2270-210">3. Перезапустите службу waagent</span><span class="sxs-lookup"><span data-stu-id="a2270-210">3. Restart the waagent service</span></span>
<span data-ttu-id="a2270-211">Для большинства дистрибутивов Linux:</span><span class="sxs-lookup"><span data-stu-id="a2270-211">For most of Linux distros:</span></span>

```bash
sudo service waagent restart
```

<span data-ttu-id="a2270-212">Для Ubuntu используйте:</span><span class="sxs-lookup"><span data-stu-id="a2270-212">For Ubuntu, use:</span></span>

```bash
sudo service walinuxagent restart
```

<span data-ttu-id="a2270-213">Для CoreOS используйте:</span><span class="sxs-lookup"><span data-stu-id="a2270-213">For CoreOS, use:</span></span>

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-the-azure-linux-agent-version"></a><span data-ttu-id="a2270-214">4. Подтвердите версию агента Linux для Azure</span><span class="sxs-lookup"><span data-stu-id="a2270-214">4. Confirm the Azure Linux Agent version</span></span>
    
```bash
waagent -version
```

<span data-ttu-id="a2270-215">Для CoreOS приведенная выше команда может не работать.</span><span class="sxs-lookup"><span data-stu-id="a2270-215">For CoreOS, the above command may not work.</span></span>

<span data-ttu-id="a2270-216">Вы увидите, что агент Linux для Azure обновлен до новой версии.</span><span class="sxs-lookup"><span data-stu-id="a2270-216">You will see that the Azure Linux Agent version has been updated to the new version.</span></span>

<span data-ttu-id="a2270-217">Дополнительные сведения об агенте Linux для Azure см. в [файле сведений агента Linux для Azure](https://github.com/Azure/WALinuxAgent).</span><span class="sxs-lookup"><span data-stu-id="a2270-217">For more information regarding the Azure Linux Agent, see [Azure Linux Agent README](https://github.com/Azure/WALinuxAgent).</span></span>