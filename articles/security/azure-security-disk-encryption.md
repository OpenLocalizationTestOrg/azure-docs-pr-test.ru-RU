---
title: "Шифрование дисков для Windows и Linux ВМ IaaS aaaAzure | Документы Microsoft"
description: "В этой статье приведен обзор шифрования дисков Microsoft Azure для виртуальных машин IaaS под управлением Windows и Linux."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a><span data-ttu-id="0272f-103">Дисковое шифрование Azure для виртуальных машин IaaS под управлением Windows и Linux</span><span class="sxs-lookup"><span data-stu-id="0272f-103">Azure Disk Encryption for Windows and Linux IaaS VMs</span></span>
<span data-ttu-id="0272f-104">Microsoft Azure прилагает все усилия tooensuring конфиденциальность данных независимости данных и позволяет toocontrol, размещенной в Azure данные в диапазоне tooencrypt перспективных технологий для управления ключами шифрования, управления и аудита доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="0272f-104">Microsoft Azure is strongly committed tooensuring your data privacy, data sovereignty and enables you toocontrol your Azure hosted data through a range of advanced technologies tooencrypt, control and manage encryption keys, control & audit access of data.</span></span> <span data-ttu-id="0272f-105">Это обеспечивает клиентам Azure hello гибкость toochoose hello решение, которое наилучшим образом соответствует потребностям бизнеса.</span><span class="sxs-lookup"><span data-stu-id="0272f-105">This provides Azure customers hello flexibility toochoose hello solution that best meets their business needs.</span></span> <span data-ttu-id="0272f-106">В этом документе вы ознакомитесь tooa новое технологическое решение «Шифрование диска Azure для Windows и ВМ IaaS Linux» toohelp защиты и защиты вашего toomeet данных организации свои обязательства по безопасности и соответствия требованиям.</span><span class="sxs-lookup"><span data-stu-id="0272f-106">In this paper, we will introduce you tooa new technology solution “Azure Disk Encryption for Windows and Linux IaaS VM’s” toohelp protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="0272f-107">Подробное руководство по способ шифрования toouse hello диска Azure функции в том числе hello поддерживается сценарии и взаимодействия с пользователем hello Hello бумаги.</span><span class="sxs-lookup"><span data-stu-id="0272f-107">hello paper provides detailed guidance on how toouse hello Azure disk encryption features including hello supported scenarios and hello user experiences.</span></span>

> [!NOTE]
> <span data-ttu-id="0272f-108">Выполнение некоторых приведенных рекомендаций может привести к более интенсивному использованию данных, сети или вычислительных ресурсов, а следовательно к дополнительным затратам на лицензии или подписки.</span><span class="sxs-lookup"><span data-stu-id="0272f-108">Certain recommendations might increase data, network, or compute resource usage, resulting in additional license or subscription costs.</span></span>

## <a name="overview"></a><span data-ttu-id="0272f-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="0272f-109">Overview</span></span>
<span data-ttu-id="0272f-110">Шифрование дисков Azure — это новая функция, которая помогает зашифровать диски виртуальных машин IaaS под управлением Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="0272f-110">Azure Disk Encryption is a new capability that helps you encrypt your Windows and Linux IaaS virtual machine disks.</span></span> <span data-ttu-id="0272f-111">Azure шифрование диска использует отраслевой стандарт hello [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) компонента Windows, а также hello [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) функции шифрования тома tooprovide Linux для hello ОС и дисков данных hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-111">Azure Disk Encryption leverages hello industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux tooprovide volume encryption for hello OS and hello data disks.</span></span> <span data-ttu-id="0272f-112">решение Hello интегрировано с [хранилище ключей Azure](https://azure.microsoft.com/documentation/services/key-vault/) toohelp управления и управление ключами шифрования диска hello и секретные данные в вашей подписке хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="0272f-112">hello solution is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp you control and manage hello disk-encryption keys and secrets in your key vault subscription.</span></span> <span data-ttu-id="0272f-113">Hello решение также обеспечивает шифрование всех данных на диски виртуальной машины hello хранятся в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="0272f-113">hello solution also ensures that all data on hello virtual machine disks are encrypted at rest in your Azure storage.</span></span>

<span data-ttu-id="0272f-114">Теперь **общедоступная версия** шифрования дисков Azure представлена во всех общедоступных регионах Azure и регионах AzureGov для виртуальных машин IaaS с ОС Windows и Linux уровня "Стандартный" или c хранилищем класса "Премиум".</span><span class="sxs-lookup"><span data-stu-id="0272f-114">Azure disk encryption for Windows and Linux IaaS VMs is now in **General Availability** in all Azure public regions and AzureGov regions for Standard  VMs and VMs with premium storage.</span></span>

### <a name="encryption-scenarios"></a><span data-ttu-id="0272f-115">Сценарии шифрования</span><span class="sxs-lookup"><span data-stu-id="0272f-115">Encryption scenarios</span></span>
<span data-ttu-id="0272f-116">Hello решения по шифрованию диска Azure поддерживает следующие сценарии клиента hello:</span><span class="sxs-lookup"><span data-stu-id="0272f-116">hello Azure Disk Encryption solution supports hello following customer scenarios:</span></span>

* <span data-ttu-id="0272f-117">включение шифрования для новых виртуальных машин IaaS, для создания которых используются предварительно зашифрованные виртуальные жесткие диски и ключи шифрования;</span><span class="sxs-lookup"><span data-stu-id="0272f-117">Enable encryption on new IaaS VMs created from pre-encrypted VHD and encryption keys</span></span>
* <span data-ttu-id="0272f-118">Включить шифрование на новые виртуальные машины IaaS, созданных из образов коллекции Azure поддерживается hello</span><span class="sxs-lookup"><span data-stu-id="0272f-118">Enable encryption on new IaaS VMs created from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="0272f-119">включение шифрования в имеющихся виртуальных машинах IaaS, запущенных в Azure;</span><span class="sxs-lookup"><span data-stu-id="0272f-119">Enable encryption on existing IaaS VMs running in Azure</span></span>
* <span data-ttu-id="0272f-120">отключение шифрования на виртуальных машинах IaaS под управлением Windows;</span><span class="sxs-lookup"><span data-stu-id="0272f-120">Disable encryption on Windows IaaS VMs</span></span>
* <span data-ttu-id="0272f-121">отключение шифрования на дисках данных виртуальных машин IaaS под управлением Linux;</span><span class="sxs-lookup"><span data-stu-id="0272f-121">Disable encryption on data drives for Linux IaaS VMs</span></span>
* <span data-ttu-id="0272f-122">включение шифрования виртуальных машин с управляемыми дисками;</span><span class="sxs-lookup"><span data-stu-id="0272f-122">Enable encryption of managed disk VMs</span></span>
* <span data-ttu-id="0272f-123">изменение параметров шифрования существующей зашифрованной виртуальной машины с хранилищем не класса "Премиум";</span><span class="sxs-lookup"><span data-stu-id="0272f-123">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="0272f-124">резервное копирование и восстановление виртуальных машин, зашифрованных с помощью ключа шифрования.</span><span class="sxs-lookup"><span data-stu-id="0272f-124">Backup and restore of encrypted VMs, encrypted with key encryption key</span></span>

<span data-ttu-id="0272f-125">решение Hello поддерживает следующие сценарии для ВМ IaaS, если они включены в Microsoft Azure hello:</span><span class="sxs-lookup"><span data-stu-id="0272f-125">hello solution supports hello following scenarios for IaaS VMs when they are enabled in Microsoft Azure:</span></span>

* <span data-ttu-id="0272f-126">интеграция с хранилищем ключей Azure;</span><span class="sxs-lookup"><span data-stu-id="0272f-126">Integration with Azure Key Vault</span></span>
* <span data-ttu-id="0272f-127">виртуальные машины IaaS серий [A, D, DS, G, GS, F и т. д.](https://azure.microsoft.com/pricing/details/virtual-machines/) уровня "Стандартный";</span><span class="sxs-lookup"><span data-stu-id="0272f-127">Standard tier VMs: [A, D, DS, G, GS, F, and so forth series IaaS VMs](https://azure.microsoft.com/pricing/details/virtual-machines/)</span></span>
* <span data-ttu-id="0272f-128">Включить шифрование в Windows и Linux ВМ IaaS и управляемого диска виртуальных машин из hello поддерживается образов коллекции Azure</span><span class="sxs-lookup"><span data-stu-id="0272f-128">Enable encryption on Windows and Linux IaaS VMs and managed disk VMs from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="0272f-129">отключение шифрования на дисках данных и в операционной системе виртуальных машин IaaS с ОС Windows и виртуальных машин с управляемыми дисками;</span><span class="sxs-lookup"><span data-stu-id="0272f-129">Disable encryption on OS and data drives for Windows IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="0272f-130">отключение шифрования на дисках данных виртуальных машин IaaS с ОС Windows и виртуальных машин с управляемыми дисками;</span><span class="sxs-lookup"><span data-stu-id="0272f-130">Disable encryption on data drives for Linux IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="0272f-131">включение шифрования на виртуальных машинах IaaS под управлением клиентской ОС Windows;</span><span class="sxs-lookup"><span data-stu-id="0272f-131">Enable encryption on IaaS VMs running Windows Client OS</span></span>
* <span data-ttu-id="0272f-132">включение шифрования для томов с путями подключения.</span><span class="sxs-lookup"><span data-stu-id="0272f-132">Enable encryption on volumes with mount paths</span></span>
* <span data-ttu-id="0272f-133">включение шифрования на виртуальных машинах Linux с чередованием дисков RAID с помощью программы mdadm;</span><span class="sxs-lookup"><span data-stu-id="0272f-133">Enable encryption on Linux VMs configured with disk striping (RAID) using mdadm</span></span>
* <span data-ttu-id="0272f-134">включение шифрования на виртуальных машинах Linux с использованием диспетчера логических томов для дисков данных;</span><span class="sxs-lookup"><span data-stu-id="0272f-134">Enable encryption on Linux VMs using LVM for data disks</span></span>
* <span data-ttu-id="0272f-135">включение шифрования на виртуальных машинах Windows с дисковыми пространствами;</span><span class="sxs-lookup"><span data-stu-id="0272f-135">Enable encryption on Windows VMs configured with Storage Spaces</span></span>
* <span data-ttu-id="0272f-136">изменение параметров шифрования существующей зашифрованной виртуальной машины с хранилищем не класса "Премиум";</span><span class="sxs-lookup"><span data-stu-id="0272f-136">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="0272f-137">поддерживаются все общедоступные регионы Azure и регионы AzureGov.</span><span class="sxs-lookup"><span data-stu-id="0272f-137">All Azure Public and AzureGov regions are supported</span></span>

<span data-ttu-id="0272f-138">решение Hello не поддерживает следующие сценарии, функции и технологии hello:</span><span class="sxs-lookup"><span data-stu-id="0272f-138">hello solution does not support hello following scenarios, features, and technology:</span></span>

* <span data-ttu-id="0272f-139">виртуальные машины уровня "Базовый";</span><span class="sxs-lookup"><span data-stu-id="0272f-139">Basic tier IaaS VMs</span></span>
* <span data-ttu-id="0272f-140">отключение шифрования диска ОС виртуальных машин IaaS под управлением Linux;</span><span class="sxs-lookup"><span data-stu-id="0272f-140">Disabling encryption on an OS drive for Linux IaaS VMs</span></span>
* <span data-ttu-id="0272f-141">Отключение шифрования на диске с данными при шифровании hello диска ОС ВМ Iaas Linux</span><span class="sxs-lookup"><span data-stu-id="0272f-141">Disabling encryption on a data drive if hello OS drive is encrypted for Linux Iaas VMs</span></span>
* <span data-ttu-id="0272f-142">Виртуальные машины IaaS, созданных с помощью метода создания виртуальной Машины классический hello</span><span class="sxs-lookup"><span data-stu-id="0272f-142">IaaS VMs that are created by using hello classic VM creation method</span></span>
* <span data-ttu-id="0272f-143">включение шифрования для виртуальных машин IaaS под управлением Windows и Linux, созданных из пользовательских образов НЕ поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0272f-143">Enable encryption on Windows and Linux IaaS VMs customer custom images is NOT supported.</span></span> <span data-ttu-id="0272f-144">Включение шифрования для диска ОС в операционной системе Linux LVM в настоящее время не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0272f-144">Enable enccryption on Linux LVM OS disk is not supported currently.</span></span> <span data-ttu-id="0272f-145">Поддержка будет обеспечена в ближайшее время.</span><span class="sxs-lookup"><span data-stu-id="0272f-145">This support will come soon.</span></span>
* <span data-ttu-id="0272f-146">интеграция с локальной службой управления ключами;</span><span class="sxs-lookup"><span data-stu-id="0272f-146">Integration with your on-premises Key Management Service</span></span>
* <span data-ttu-id="0272f-147">служба файлов Azure (общая файловая система), NFS, динамические тома, виртуальные машины Windows с программными системами RAID.</span><span class="sxs-lookup"><span data-stu-id="0272f-147">Azure Files (shared file system), Network File System (NFS), dynamic volumes, and Windows VMs that are configured with software-based RAID systems</span></span>
* <span data-ttu-id="0272f-148">резервное копирование и восстановление виртуальных машин, зашифрованных без использования ключа шифрования;</span><span class="sxs-lookup"><span data-stu-id="0272f-148">Backup and restore of encrypted VMs, encrypted without key encryption key.</span></span>
* <span data-ttu-id="0272f-149">изменение параметров шифрования существующей зашифрованной виртуальной машины с хранилищем класса "Премиум".</span><span class="sxs-lookup"><span data-stu-id="0272f-149">Update encryption settings of an existing encrypted premium storage VM.</span></span>

> [!NOTE]
> <span data-ttu-id="0272f-150">Резервное копирование и восстановление виртуальных машин, зашифрованные поддерживается только для виртуальных машин, которые шифруются с помощью ключа обмена Ключами конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-150">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="0272f-151">Виртуальные машины, зашифрованные без ключа шифрования ключей, не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="0272f-151">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="0272f-152">KEK — это необязательный параметр для включения шифрования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="0272f-152">KEK is an optional parameter that enables VM encryption.</span></span> <span data-ttu-id="0272f-153">Поддержка ожидается в ближайшем будущем.</span><span class="sxs-lookup"><span data-stu-id="0272f-153">This support is coming soon.</span></span>
> <span data-ttu-id="0272f-154">Изменение параметров шифрования существующей зашифрованной виртуальной машины с хранилищем класса "Премиум" не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0272f-154">Update encryption settings of an existing encrypted premium storage VM are not supported.</span></span> <span data-ttu-id="0272f-155">Поддержка ожидается в ближайшем будущем.</span><span class="sxs-lookup"><span data-stu-id="0272f-155">This support is coming soon.</span></span>

### <a name="encryption-features"></a><span data-ttu-id="0272f-156">Функции шифрования</span><span class="sxs-lookup"><span data-stu-id="0272f-156">Encryption features</span></span>
<span data-ttu-id="0272f-157">При включении и развернуть шифрование диска Azure ВМ IaaS Azure hello следующие возможности включены, в зависимости от конфигурации hello:</span><span class="sxs-lookup"><span data-stu-id="0272f-157">When you enable and deploy Azure Disk Encryption for Azure IaaS VMs, hello following capabilities are enabled, depending on hello configuration provided:</span></span>

* <span data-ttu-id="0272f-158">Шифрование тома hello ОС тома tooprotect hello загрузки хранятся в хранилище</span><span class="sxs-lookup"><span data-stu-id="0272f-158">Encryption of hello OS volume tooprotect hello boot volume at rest in your storage</span></span>
* <span data-ttu-id="0272f-159">Шифрование тома данных hello tooprotect тома данных хранятся в хранилище</span><span class="sxs-lookup"><span data-stu-id="0272f-159">Encryption of data volumes tooprotect hello data volumes at rest in your storage</span></span>
* <span data-ttu-id="0272f-160">Отключение шифрования на hello операционной системы и данных дисков ВМ IaaS Windows</span><span class="sxs-lookup"><span data-stu-id="0272f-160">Disabling encryption on hello OS and data drives for Windows IaaS VMs</span></span>
* <span data-ttu-id="0272f-161">Отключение шифрования для данных hello дисков для виртуальных машин Linux IaaS (если ОС диск является не шифруются)</span><span class="sxs-lookup"><span data-stu-id="0272f-161">Disabling encryption on hello data drives for Linux IaaS VMs (only if OS drive IS NOT encrypted)</span></span>
* <span data-ttu-id="0272f-162">Защита ключей шифрования hello и секретные данные в вашей подписке хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="0272f-162">Safeguarding hello encryption keys and secrets in your key vault subscription</span></span>
* <span data-ttu-id="0272f-163">Отчеты о состоянии шифрования hello объекта hello зашифрованные ВМ IaaS</span><span class="sxs-lookup"><span data-stu-id="0272f-163">Reporting hello encryption status of hello encrypted IaaS VM</span></span>
* <span data-ttu-id="0272f-164">Удаление параметров конфигурации шифрование диска от виртуальной машины IaaS hello</span><span class="sxs-lookup"><span data-stu-id="0272f-164">Removal of disk-encryption configuration settings from hello IaaS virtual machine</span></span>
* <span data-ttu-id="0272f-165">Резервное копирование и восстановление виртуальных машин, зашифрованные с помощью службы архивации Azure hello</span><span class="sxs-lookup"><span data-stu-id="0272f-165">Backup and restore of encrypted VMs by using hello Azure Backup service</span></span>

> [!NOTE]
> <span data-ttu-id="0272f-166">Резервное копирование и восстановление виртуальных машин, зашифрованные поддерживается только для виртуальных машин, которые шифруются с помощью ключа обмена Ключами конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-166">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="0272f-167">Виртуальные машины, зашифрованные без ключа шифрования ключей, не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="0272f-167">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="0272f-168">KEK — это необязательный параметр для включения шифрования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="0272f-168">KEK is an optional parameter that enables VM encryption.</span></span>

<span data-ttu-id="0272f-169">Решения для шифрования дисков Azure для виртуальных машин IaaS под управлением Windows и Linux включает в себя следующее:</span><span class="sxs-lookup"><span data-stu-id="0272f-169">Azure Disk Encryption for IaaS VMS for Windows and Linux solution includes:</span></span>

* <span data-ttu-id="0272f-170">расширение шифрование диска Windows Hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-170">hello disk-encryption extension for Windows.</span></span>
* <span data-ttu-id="0272f-171">Hello шифрование диска расширения для Linux.</span><span class="sxs-lookup"><span data-stu-id="0272f-171">hello disk-encryption extension for Linux.</span></span>
* <span data-ttu-id="0272f-172">командлеты PowerShell Hello шифрование диска.</span><span class="sxs-lookup"><span data-stu-id="0272f-172">hello disk-encryption PowerShell cmdlets.</span></span>
* <span data-ttu-id="0272f-173">Здравствуйте шифрования диска командлеты Azure командной строки (CLI).</span><span class="sxs-lookup"><span data-stu-id="0272f-173">hello disk-encryption Azure command-line interface (CLI) cmdlets.</span></span>
* <span data-ttu-id="0272f-174">шаблоны Azure Resource Manager Hello шифрование диска.</span><span class="sxs-lookup"><span data-stu-id="0272f-174">hello disk-encryption Azure Resource Manager templates.</span></span>

<span data-ttu-id="0272f-175">Hello решения по шифрованию диска Azure поддерживается на виртуальных машинах IaaS, работающих под управлением ОС Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="0272f-175">hello Azure Disk Encryption solution is supported on IaaS VMs that are running Windows or Linux OS.</span></span> <span data-ttu-id="0272f-176">Дополнительные сведения о hello поддерживаемых операционных системах см. в разделе hello «необходимые условия» раздела.</span><span class="sxs-lookup"><span data-stu-id="0272f-176">For more information about hello supported operating systems, see hello "Prerequisites" section.</span></span>

> [!NOTE]
> <span data-ttu-id="0272f-177">Дополнительная плата за шифрование дисков Azure для виртуальных машин не взимается.</span><span class="sxs-lookup"><span data-stu-id="0272f-177">There is no additional charge for encrypting VM disks with Azure Disk Encryption.</span></span>

### <a name="value-proposition"></a><span data-ttu-id="0272f-178">Предлагаемые преимущества</span><span class="sxs-lookup"><span data-stu-id="0272f-178">Value proposition</span></span>
<span data-ttu-id="0272f-179">При применении решения hello Управление шифрованием диска Azure может удовлетворять hello следующие бизнес-требований:</span><span class="sxs-lookup"><span data-stu-id="0272f-179">When you apply hello Azure Disk Encryption-management solution, you can satisfy hello following business needs:</span></span>

* <span data-ttu-id="0272f-180">Виртуальные машины IaaS, защищены неактивные, поскольку можно использовать стандартные технологии tooaddress организации безопасности и соответствия требованиям требования к шифрованию.</span><span class="sxs-lookup"><span data-stu-id="0272f-180">IaaS VMs are secured at rest, because you can use industry-standard encryption technology tooaddress organizational security and compliance requirements.</span></span>
* <span data-ttu-id="0272f-181">Загрузка виртуальных машин IaaS выполняется в соответствии с ключами и политиками, которыми управляет клиент. Можно также проводить аудит их использования в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="0272f-181">IaaS VMs boot under customer-controlled keys and policies, and you can audit their usage in your key vault.</span></span>

### <a name="encryption-workflow"></a><span data-ttu-id="0272f-182">Рабочий процесс шифрования</span><span class="sxs-lookup"><span data-stu-id="0272f-182">Encryption workflow</span></span>
<span data-ttu-id="0272f-183">Шифрование диска tooenable для Windows и виртуальных машин Linux hello следующие:</span><span class="sxs-lookup"><span data-stu-id="0272f-183">tooenable disk encryption for Windows and Linux VMs, do hello following:</span></span>

1. <span data-ttu-id="0272f-184">Выберите сценарии шифрования на один из предыдущих сценариев шифрования hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-184">Choose an encryption scenario from among hello preceding encryption scenarios.</span></span>
2. <span data-ttu-id="0272f-185">Включить шифрование диска tooenabling посредством шаблона диспетчера ресурсов шифрования диска Azure hello, командлеты PowerShell или интерфейса командной и укажите конфигурацию шифрования hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-185">Opt in tooenabling disk encryption via hello Azure Disk Encryption Resource Manager template, PowerShell cmdlets, or CLI command, and specify hello encryption configuration.</span></span>

   * <span data-ttu-id="0272f-186">Для шифрования клиента сценария виртуального жесткого диска: hello передачи учетной записи хранилища tooyour виртуальный жесткий ДИСК зашифрован hello и hello шифрования ключа tooyour материала ключа хранилища.</span><span class="sxs-lookup"><span data-stu-id="0272f-186">For hello customer-encrypted VHD scenario, upload hello encrypted VHD tooyour storage account and hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="0272f-187">Укажите конфигурации tooenable hello шифрование на новую виртуальную Машину IaaS.</span><span class="sxs-lookup"><span data-stu-id="0272f-187">Then, provide hello encryption configuration tooenable encryption on a new IaaS VM.</span></span>
   * <span data-ttu-id="0272f-188">Для новых виртуальных машин, созданными на hello Marketplace и существующих виртуальных машин, которые уже запущены в Azure предоставляют tooenable конфигурации hello шифрование на hello ВМ IaaS.</span><span class="sxs-lookup"><span data-stu-id="0272f-188">For new VMs that are created from hello Marketplace and existing VMs that are already running in Azure, provide hello encryption configuration tooenable encryption on hello IaaS VM.</span></span>

3. <span data-ttu-id="0272f-189">Предоставление доступа к toohello платформы Azure tooread hello ключ шифрования материалы (ключи шифрования BitLocker для систем Windows) и парольную фразу для Linux из вашего хранилища ключей шифрования tooenable hello ВМ IaaS.</span><span class="sxs-lookup"><span data-stu-id="0272f-189">Grant access toohello Azure platform tooread hello encryption-key material (BitLocker encryption keys for Windows systems and Passphrase for Linux) from your key vault tooenable encryption on hello IaaS VM.</span></span>

4. <span data-ttu-id="0272f-190">Укажите hello Azure Active Directory (Azure AD) приложения удостоверение toowrite hello шифрования ключа материала tooyour хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="0272f-190">Provide hello Azure Active Directory (Azure AD) application identity toowrite hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="0272f-191">Это позволяет включить шифрование на hello ВМ IaaS для сценариев hello, упомянутых в шаге 2.</span><span class="sxs-lookup"><span data-stu-id="0272f-191">Doing so enables encryption on hello IaaS VM for hello scenarios mentioned in step 2.</span></span>

5. <span data-ttu-id="0272f-192">Azure обновляет модель службы hello виртуальной Машины с помощью шифрования и настройки хранилища ключей hello и устанавливает зашифрованные ВМ.</span><span class="sxs-lookup"><span data-stu-id="0272f-192">Azure updates hello VM service model with encryption and hello key vault configuration, and sets up your encrypted VM.</span></span>

 ![Антивредоносное ПО Майкрософт в Azure](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a><span data-ttu-id="0272f-194">Рабочий процесс расшифровки</span><span class="sxs-lookup"><span data-stu-id="0272f-194">Decryption workflow</span></span>
<span data-ttu-id="0272f-195">Шифрование диска toodisable ВМ IaaS, полный hello следующие общие действия:</span><span class="sxs-lookup"><span data-stu-id="0272f-195">toodisable disk encryption for IaaS VMs, complete hello following high-level steps:</span></span>

1. <span data-ttu-id="0272f-196">Выберите toodisable шифрования (расшифровки) на работающей ВМ в Azure IaaS через hello шаблона диспетчера ресурсов шифрования диска Azure или командлеты PowerShell и указать конфигурацию расшифровки hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-196">Choose toodisable encryption (decryption) on a running IaaS VM in Azure via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets, and specify hello decryption configuration.</span></span>

 <span data-ttu-id="0272f-197">Этот шаг отключает шифрование тома данных ОС или hello hello, или на запуск виртуальной Машины IaaS Windows hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-197">This step disables encryption of hello OS or hello data volume or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="0272f-198">Тем не менее как упоминалось в предыдущем разделе hello, отключение шифрования диска операционной системы для Linux не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0272f-198">However, as mentioned in hello previous section, disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="0272f-199">этап расшифровки Hello допустим только для дисков с данными на виртуальных машинах Linux, при условии, что диск ОС hello не шифруются.</span><span class="sxs-lookup"><span data-stu-id="0272f-199">hello decryption step is allowed only for data drives on Linux VMs as long as hello OS disk is not encrypted.</span></span>
2. <span data-ttu-id="0272f-200">Обновления Azure hello модели службы виртуальной Машины, а hello ВМ IaaS помечается расшифрованы.</span><span class="sxs-lookup"><span data-stu-id="0272f-200">Azure updates hello VM service model, and hello IaaS VM is marked decrypted.</span></span> <span data-ttu-id="0272f-201">содержимое Hello hello ВМ больше не шифруются при хранении.</span><span class="sxs-lookup"><span data-stu-id="0272f-201">hello contents of hello VM are no longer encrypted at rest.</span></span>

> [!NOTE]
> <span data-ttu-id="0272f-202">Операция отключения шифрования Hello не удаляет вашего ключа хранилища и hello основы ключа шифрования (ключи шифрования BitLocker для систем Windows) или парольную фразу для Linux.</span><span class="sxs-lookup"><span data-stu-id="0272f-202">hello disable-encryption operation does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows systems or Passphrase for Linux).</span></span>
 > <span data-ttu-id="0272f-203">Отключение шифрования диска операционной системы для Linux не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0272f-203">Disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="0272f-204">этап расшифровки Hello допустим только для дисков с данными на виртуальных машинах Linux.</span><span class="sxs-lookup"><span data-stu-id="0272f-204">hello decryption step is allowed only for data drives on Linux VMs.</span></span>
<span data-ttu-id="0272f-205">Отключение шифрования диска данных для Linux не поддерживается, если шифрование hello диска операционной системы.</span><span class="sxs-lookup"><span data-stu-id="0272f-205">Disabling data disk encryption for Linux is not supported if hello OS drive is encrypted.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0272f-206">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0272f-206">Prerequisites</span></span>
<span data-ttu-id="0272f-207">Прежде чем включить шифрование диска Azure на виртуальные машины IaaS Azure для hello поддерживается сценариев, которые были описаны в разделе «Обзор» hello, см. следующие необходимые условия hello:</span><span class="sxs-lookup"><span data-stu-id="0272f-207">Before you enable Azure Disk Encryption on Azure IaaS VMs for hello supported scenarios that were discussed in hello "Overview" section, see hello following prerequisites:</span></span>

* <span data-ttu-id="0272f-208">Необходимо иметь действующая Активная подписка Azure toocreate ресурсы в Azure в регионах hello поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0272f-208">You must have a valid active Azure subscription toocreate resources in Azure in hello supported regions.</span></span>
* <span data-ttu-id="0272f-209">Azure диска шифрование поддерживается для следующих версий Windows Server hello: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 и Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="0272f-209">Azure Disk Encryption is supported on hello following Windows Server versions: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>
* <span data-ttu-id="0272f-210">В следующих клиентских версий Windows hello поддерживается Azure шифрование диска: клиента Windows 8 и Windows 10.</span><span class="sxs-lookup"><span data-stu-id="0272f-210">Azure Disk Encryption is supported on hello following Windows client versions: Windows 8 client and Windows 10 client.</span></span>

> [!NOTE]
> <span data-ttu-id="0272f-211">Для Windows Server 2008 R2 перед включением шифрования в Azure требуется установить .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="0272f-211">For Windows Server 2008 R2, you must have .NET Framework 4.5 installed before you enable encryption in Azure.</span></span> <span data-ttu-id="0272f-212">Можно установить его из центра обновления Windows, установив необязательное обновление hello Microsoft .NET Framework 4.5.2 для x64-разрядных систем Windows Server 2008 R2 ([KB2901983](https://support.microsoft.com/kb/2901983)).</span><span class="sxs-lookup"><span data-stu-id="0272f-212">You can install it from Windows Update by installing hello optional update Microsoft .NET Framework 4.5.2 for Windows Server 2008 R2 x64-based systems ([KB2901983](https://support.microsoft.com/kb/2901983)).</span></span>

* <span data-ttu-id="0272f-213">Поддерживается Azure шифрование диска на hello следующие коллекции Azure на основе сервера дистрибутивах Linux и версиях:</span><span class="sxs-lookup"><span data-stu-id="0272f-213">Azure Disk Encryption is supported on hello following Azure Gallery based Linux server distributions and versions:</span></span>

| <span data-ttu-id="0272f-214">Дистрибутив Linux</span><span class="sxs-lookup"><span data-stu-id="0272f-214">Linux Distribution</span></span> | <span data-ttu-id="0272f-215">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="0272f-215">Version</span></span> | <span data-ttu-id="0272f-216">Тип тома, для которого поддерживается шифрование</span><span class="sxs-lookup"><span data-stu-id="0272f-216">Volume Type Supported for Encryption</span></span>|
| --- | --- |--- |
| <span data-ttu-id="0272f-217">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="0272f-217">Ubuntu</span></span> | <span data-ttu-id="0272f-218">16.04-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="0272f-218">16.04-DAILY-LTS</span></span> | <span data-ttu-id="0272f-219">Диск операционной системы и данных</span><span class="sxs-lookup"><span data-stu-id="0272f-219">OS and Data disk</span></span> |
| <span data-ttu-id="0272f-220">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="0272f-220">Ubuntu</span></span> | <span data-ttu-id="0272f-221">14.04.5-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="0272f-221">14.04.5-DAILY-LTS</span></span> | <span data-ttu-id="0272f-222">Диск операционной системы и данных</span><span class="sxs-lookup"><span data-stu-id="0272f-222">OS and Data disk</span></span> |
| <span data-ttu-id="0272f-223">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="0272f-223">Ubuntu</span></span> | <span data-ttu-id="0272f-224">12.10</span><span class="sxs-lookup"><span data-stu-id="0272f-224">12.10</span></span> | <span data-ttu-id="0272f-225">Диск данных</span><span class="sxs-lookup"><span data-stu-id="0272f-225">Data disk</span></span> |
| <span data-ttu-id="0272f-226">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="0272f-226">Ubuntu</span></span> | <span data-ttu-id="0272f-227">12.04</span><span class="sxs-lookup"><span data-stu-id="0272f-227">12.04</span></span> | <span data-ttu-id="0272f-228">Диск данных</span><span class="sxs-lookup"><span data-stu-id="0272f-228">Data disk</span></span> |
| <span data-ttu-id="0272f-229">RHEL</span><span class="sxs-lookup"><span data-stu-id="0272f-229">RHEL</span></span> | <span data-ttu-id="0272f-230">7.3</span><span class="sxs-lookup"><span data-stu-id="0272f-230">7.3</span></span> | <span data-ttu-id="0272f-231">Диск операционной системы и данных</span><span class="sxs-lookup"><span data-stu-id="0272f-231">OS and Data disk</span></span> |
| <span data-ttu-id="0272f-232">RHEL</span><span class="sxs-lookup"><span data-stu-id="0272f-232">RHEL</span></span> | <span data-ttu-id="0272f-233">7,2</span><span class="sxs-lookup"><span data-stu-id="0272f-233">7.2</span></span> | <span data-ttu-id="0272f-234">Диск операционной системы и данных</span><span class="sxs-lookup"><span data-stu-id="0272f-234">OS and Data disk</span></span> |
| <span data-ttu-id="0272f-235">RHEL</span><span class="sxs-lookup"><span data-stu-id="0272f-235">RHEL</span></span> | <span data-ttu-id="0272f-236">6,8</span><span class="sxs-lookup"><span data-stu-id="0272f-236">6.8</span></span> | <span data-ttu-id="0272f-237">Диск операционной системы и данных</span><span class="sxs-lookup"><span data-stu-id="0272f-237">OS and Data disk</span></span> |
| <span data-ttu-id="0272f-238">RHEL</span><span class="sxs-lookup"><span data-stu-id="0272f-238">RHEL</span></span> | <span data-ttu-id="0272f-239">6.7</span><span class="sxs-lookup"><span data-stu-id="0272f-239">6.7</span></span> | <span data-ttu-id="0272f-240">Диск данных</span><span class="sxs-lookup"><span data-stu-id="0272f-240">Data disk</span></span> |
| <span data-ttu-id="0272f-241">CentOS</span><span class="sxs-lookup"><span data-stu-id="0272f-241">CentOS</span></span> | <span data-ttu-id="0272f-242">7.3</span><span class="sxs-lookup"><span data-stu-id="0272f-242">7.3</span></span> | <span data-ttu-id="0272f-243">Диск операционной системы и данных</span><span class="sxs-lookup"><span data-stu-id="0272f-243">OS and Data disk</span></span> |
| <span data-ttu-id="0272f-244">CentOS</span><span class="sxs-lookup"><span data-stu-id="0272f-244">CentOS</span></span> | <span data-ttu-id="0272f-245">7.2n</span><span class="sxs-lookup"><span data-stu-id="0272f-245">7.2n</span></span> | <span data-ttu-id="0272f-246">Диск операционной системы и данных</span><span class="sxs-lookup"><span data-stu-id="0272f-246">OS and Data disk</span></span> |
| <span data-ttu-id="0272f-247">CentOS</span><span class="sxs-lookup"><span data-stu-id="0272f-247">CentOS</span></span> | <span data-ttu-id="0272f-248">6,8</span><span class="sxs-lookup"><span data-stu-id="0272f-248">6.8</span></span> | <span data-ttu-id="0272f-249">Диск операционной системы и данных</span><span class="sxs-lookup"><span data-stu-id="0272f-249">OS and Data disk</span></span> |
| <span data-ttu-id="0272f-250">CentOS</span><span class="sxs-lookup"><span data-stu-id="0272f-250">CentOS</span></span> | <span data-ttu-id="0272f-251">7.1.</span><span class="sxs-lookup"><span data-stu-id="0272f-251">7.1</span></span> | <span data-ttu-id="0272f-252">Диск данных</span><span class="sxs-lookup"><span data-stu-id="0272f-252">Data disk</span></span> |
| <span data-ttu-id="0272f-253">CentOS</span><span class="sxs-lookup"><span data-stu-id="0272f-253">CentOS</span></span> | <span data-ttu-id="0272f-254">7.0</span><span class="sxs-lookup"><span data-stu-id="0272f-254">7.0</span></span> | <span data-ttu-id="0272f-255">Диск данных</span><span class="sxs-lookup"><span data-stu-id="0272f-255">Data disk</span></span> |
| <span data-ttu-id="0272f-256">CentOS</span><span class="sxs-lookup"><span data-stu-id="0272f-256">CentOS</span></span> | <span data-ttu-id="0272f-257">6.7</span><span class="sxs-lookup"><span data-stu-id="0272f-257">6.7</span></span> | <span data-ttu-id="0272f-258">Диск данных</span><span class="sxs-lookup"><span data-stu-id="0272f-258">Data disk</span></span> |
| <span data-ttu-id="0272f-259">CentOS</span><span class="sxs-lookup"><span data-stu-id="0272f-259">CentOS</span></span> | <span data-ttu-id="0272f-260">6.6</span><span class="sxs-lookup"><span data-stu-id="0272f-260">6.6</span></span> | <span data-ttu-id="0272f-261">Диск данных</span><span class="sxs-lookup"><span data-stu-id="0272f-261">Data disk</span></span> |
| <span data-ttu-id="0272f-262">CentOS</span><span class="sxs-lookup"><span data-stu-id="0272f-262">CentOS</span></span> | <span data-ttu-id="0272f-263">6,5</span><span class="sxs-lookup"><span data-stu-id="0272f-263">6.5</span></span> | <span data-ttu-id="0272f-264">Диск данных</span><span class="sxs-lookup"><span data-stu-id="0272f-264">Data disk</span></span> |
| <span data-ttu-id="0272f-265">openSUSE</span><span class="sxs-lookup"><span data-stu-id="0272f-265">openSUSE</span></span> | <span data-ttu-id="0272f-266">13.2</span><span class="sxs-lookup"><span data-stu-id="0272f-266">13.2</span></span> | <span data-ttu-id="0272f-267">Диск данных</span><span class="sxs-lookup"><span data-stu-id="0272f-267">Data disk</span></span> |
| <span data-ttu-id="0272f-268">SLES</span><span class="sxs-lookup"><span data-stu-id="0272f-268">SLES</span></span> | <span data-ttu-id="0272f-269">12 с пакетом обновления 1 (SP1)</span><span class="sxs-lookup"><span data-stu-id="0272f-269">12 SP1</span></span> | <span data-ttu-id="0272f-270">Диск данных</span><span class="sxs-lookup"><span data-stu-id="0272f-270">Data disk</span></span> |
| <span data-ttu-id="0272f-271">SLES</span><span class="sxs-lookup"><span data-stu-id="0272f-271">SLES</span></span> | <span data-ttu-id="0272f-272">12-SP1 (Премиум)</span><span class="sxs-lookup"><span data-stu-id="0272f-272">12-SP1 (Premium)</span></span> | <span data-ttu-id="0272f-273">Диск данных</span><span class="sxs-lookup"><span data-stu-id="0272f-273">Data disk</span></span> |
| <span data-ttu-id="0272f-274">SLES</span><span class="sxs-lookup"><span data-stu-id="0272f-274">SLES</span></span> | <span data-ttu-id="0272f-275">HPC 12</span><span class="sxs-lookup"><span data-stu-id="0272f-275">HPC 12</span></span> | <span data-ttu-id="0272f-276">Диск данных</span><span class="sxs-lookup"><span data-stu-id="0272f-276">Data disk</span></span> |
| <span data-ttu-id="0272f-277">SLES</span><span class="sxs-lookup"><span data-stu-id="0272f-277">SLES</span></span> | <span data-ttu-id="0272f-278">11-SP4 (Премиум)</span><span class="sxs-lookup"><span data-stu-id="0272f-278">11-SP4 (Premium)</span></span> | <span data-ttu-id="0272f-279">Диск данных</span><span class="sxs-lookup"><span data-stu-id="0272f-279">Data disk</span></span> |
| <span data-ttu-id="0272f-280">SLES</span><span class="sxs-lookup"><span data-stu-id="0272f-280">SLES</span></span> | <span data-ttu-id="0272f-281">11 SP4</span><span class="sxs-lookup"><span data-stu-id="0272f-281">11 SP4</span></span> | <span data-ttu-id="0272f-282">Диск данных</span><span class="sxs-lookup"><span data-stu-id="0272f-282">Data disk</span></span> |

* <span data-ttu-id="0272f-283">Требуется Azure шифрование данных на диске, хранилище ключей и виртуальные машины находились в hello же регионе Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="0272f-283">Azure Disk Encryption requires that your key vault and VMs reside in hello same Azure region and subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="0272f-284">Настройка ресурсов hello в отдельные области вызывает сбой включить функцию шифрования диска Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-284">Configuring hello resources in separate regions causes a failure in enabling hello Azure Disk Encryption feature.</span></span>

* <span data-ttu-id="0272f-285">tooset и Настройка хранилища ключей для шифрования диска Azure, см. раздел **задать и Настройка хранилища ключей для шифрования диска Azure** в hello *необходимые компоненты* этой статьи.</span><span class="sxs-lookup"><span data-stu-id="0272f-285">tooset up and configure your key vault for Azure Disk Encryption, see section **Set up and configure your key vault for Azure Disk Encryption** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="0272f-286">tooset и настройка приложения Azure AD в Azure Active directory для шифрования диска Azure, см. раздел **настройки приложения hello Azure AD в Azure Active Directory** в hello *необходимых компонентов* части этой статьи.</span><span class="sxs-lookup"><span data-stu-id="0272f-286">tooset up and configure Azure AD application in Azure Active directory for Azure Disk Encryption, see section **Set up hello Azure AD application in Azure Active Directory** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="0272f-287">tooset и настройка политики доступа hello хранилища ключей для приложения hello Azure AD, см. раздел **настроить политику доступа hello хранилища ключей для приложения hello Azure AD** в hello *необходимые компоненты* раздела в этой статье.</span><span class="sxs-lookup"><span data-stu-id="0272f-287">tooset up and configure hello key vault access policy for hello Azure AD application, see section **Set up hello key vault access policy for hello Azure AD application** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="0272f-288">tooprepare предварительно зашифрованный VHD Windows, см. раздел **подготовить предварительно зашифрованный ФАЙЛ Windows** в hello *приложение*.</span><span class="sxs-lookup"><span data-stu-id="0272f-288">tooprepare a pre-encrypted Windows VHD, see section **Prepare a pre-encrypted Windows VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="0272f-289">tooprepare предварительно зашифрованный VHD Linux, см. раздел **подготовить предварительно зашифрованный ФАЙЛ Linux** в hello *приложение*.</span><span class="sxs-lookup"><span data-stu-id="0272f-289">tooprepare a pre-encrypted Linux VHD, see section **Prepare a pre-encrypted Linux VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="0272f-290">Hello платформы Azure требует ключи шифрования toohello доступа или секреты в хранилище ключей toomake их доступных toohello виртуальной машины при его загрузке и расшифровывает hello тома ОС виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0272f-290">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello virtual machine when it boots and decrypts hello virtual machine OS volume.</span></span> <span data-ttu-id="0272f-291">разрешения tooAzure toogrant платформы, набор hello **EnabledForDiskEncryption** свойство в хранилище ключей hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-291">toogrant permissions tooAzure platform, set hello **EnabledForDiskEncryption** property in hello key vault.</span></span> <span data-ttu-id="0272f-292">Дополнительные сведения см. в разделе **задать и Настройка хранилища ключей для шифрования диска Azure** в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-292">For more information, see **Set up and configure your key vault for Azure Disk Encryption** in hello Appendix.</span></span>
* <span data-ttu-id="0272f-293">Для URL-адресов секрета и ключа шифрования ключей (KEK) хранилища ключей необходимо включить управление версиями.</span><span class="sxs-lookup"><span data-stu-id="0272f-293">Your key vault secret and KEK URLs must be versioned.</span></span> <span data-ttu-id="0272f-294">Это требование Azure.</span><span class="sxs-lookup"><span data-stu-id="0272f-294">Azure enforces this restriction of versioning.</span></span> <span data-ttu-id="0272f-295">Действительный секретный и KEK URL-адреса см. следующие примеры hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-295">For valid secret and KEK URLs, see hello following examples:</span></span>

  * <span data-ttu-id="0272f-296">Пример допустимого URL-адреса секрета: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*.</span><span class="sxs-lookup"><span data-stu-id="0272f-296">Example of a valid secret URL:   *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="0272f-297">Пример допустимого ключа шифрования ключей: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*.</span><span class="sxs-lookup"><span data-stu-id="0272f-297">Example of a valid KEK URL:   *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="0272f-298">Шифрование дисков Azure не поддерживает указание номеров портов в URL-адресах секрета и ключа шифрования ключей для хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="0272f-298">Azure Disk Encryption does not support specifying port numbers as part of key vault secrets and KEK URLs.</span></span> <span data-ttu-id="0272f-299">Примеры URL-адреса не поддерживается и поддерживаемых хранилища ключей см. в следующем hello:</span><span class="sxs-lookup"><span data-stu-id="0272f-299">For examples of non-supported and supported key vault URLs, see hello following:</span></span>

  * <span data-ttu-id="0272f-300">Недопустимый URL-адрес хранилища ключей: *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*.</span><span class="sxs-lookup"><span data-stu-id="0272f-300">Unacceptable key vault URL  *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="0272f-301">Допустимый URL-адрес хранилища ключей: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*.</span><span class="sxs-lookup"><span data-stu-id="0272f-301">Acceptable key vault URL:   *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="0272f-302">функция шифрования диска Azure tooenable hello, hello ВМ IaaS должен удовлетворять hello следующие требования к конфигурации конечной точки сети.</span><span class="sxs-lookup"><span data-stu-id="0272f-302">tooenable hello Azure Disk Encryption feature, hello IaaS VMs must meet hello following network endpoint configuration requirements:</span></span>
  * <span data-ttu-id="0272f-303">tooget маркеров tooconnect tooyour хранилища ключей, hello ВМ IaaS должна быть конечной точкой Azure Active Directory может tooconnect tooan, \[login.microsoftonline.com\].</span><span class="sxs-lookup"><span data-stu-id="0272f-303">tooget a token tooconnect tooyour key vault, hello IaaS VM must be able tooconnect tooan Azure Active Directory endpoint, \[login.microsoftonline.com\].</span></span>
  * <span data-ttu-id="0272f-304">toowrite hello шифрования ключей tooyour хранилища ключей, hello ВМ IaaS должна быть конечной точкой хранилища ключей toohello может tooconnect.</span><span class="sxs-lookup"><span data-stu-id="0272f-304">toowrite hello encryption keys tooyour key vault, hello IaaS VM must be able tooconnect toohello key vault endpoint.</span></span>
  * <span data-ttu-id="0272f-305">Hello ВМ IaaS должно быть конечной точки может tooconnect tooan хранилища Azure, узлы hello репозиторий расширений Azure и учетной записью хранения Azure, что узлы hello VHD-файлы.</span><span class="sxs-lookup"><span data-stu-id="0272f-305">hello IaaS VM must be able tooconnect tooan Azure storage endpoint that hosts hello Azure extension repository and an Azure storage account that hosts hello VHD files.</span></span>

  > [!NOTE]
  > <span data-ttu-id="0272f-306">Если политика безопасности ограничивает доступ из виртуальных машин Azure toohello Интернета, можно решить hello, предшествующий URI и настроить toohello исходящие подключения tooallow конкретного правила IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="0272f-306">If your security policy limits access from Azure VMs toohello Internet, you can resolve hello preceding URI and configure a specific rule tooallow outbound connectivity toohello IPs.</span></span>
  >
  ><span data-ttu-id="0272f-307">tooconfigure и доступа к хранилищу ключей Azure за брандмауэром (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span><span class="sxs-lookup"><span data-stu-id="0272f-307">tooconfigure and access Azure Key Vault behind a firewall(https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span></span>

* <span data-ttu-id="0272f-308">Используйте последнюю версию пакета SDK для Azure PowerShell версии tooconfigure шифрование диска Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-308">Use hello latest version of Azure PowerShell SDK version tooconfigure Azure Disk Encryption.</span></span> <span data-ttu-id="0272f-309">Загрузка последней версии hello объекта [выпуска Azure PowerShell](https://github.com/Azure/azure-powershell/releases)</span><span class="sxs-lookup"><span data-stu-id="0272f-309">Download hello latest version of [Azure PowerShell release](https://github.com/Azure/azure-powershell/releases)</span></span>

 > [!NOTE]
  > <span data-ttu-id="0272f-310">Шифрование дисков Azure не поддерживается в [пакете SDK для Azure PowerShell версии 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span><span class="sxs-lookup"><span data-stu-id="0272f-310">Azure Disk Encryption is not supported on [Azure PowerShell SDK version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span></span> <span data-ttu-id="0272f-311">Если вы получили ошибку toousing Azure PowerShell 1.1.0, связанные с. в разделе [tooAzure связанные ошибки шифрования диска Azure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span><span class="sxs-lookup"><span data-stu-id="0272f-311">If you are receiving an error related toousing Azure PowerShell 1.1.0, see [Azure Disk Encryption Error Related tooAzure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span></span>

* <span data-ttu-id="0272f-312">toorun любую команду Azure CLI и связать ее с подпиской Azure, необходимо сначала установить Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="0272f-312">toorun any Azure CLI command and associate it with your Azure subscription, you must first install Azure CLI:</span></span>
  * <span data-ttu-id="0272f-313">tooinstall Azure CLI и связать ее с подпиской Azure см. в разделе [как tooinstall и настройка Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="0272f-313">tooinstall Azure CLI and associate it with your Azure subscription, see [How tooinstall and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="0272f-314">toouse Azure CLI для Mac, Linux и Windows с помощью диспетчера ресурсов Azure в разделе [команды Azure CLI в режим диспетчера ресурсов](../virtual-machines/azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="0272f-314">toouse Azure CLI for Mac, Linux, and Windows with Azure Resource Manager, see [Azure CLI commands in Resource Manager mode](../virtual-machines/azure-cli-arm-commands.md).</span></span>

* <span data-ttu-id="0272f-315">При шифровании управляемого диска, он является обязательной к установке tootake моментальный снимок hello управляемого диска или из резервной копии диска hello за пределами предыдущего tooenabling шифрования шифрование диска Azure.</span><span class="sxs-lookup"><span data-stu-id="0272f-315">When encrypting a managed disk, it is mandatory prerequisite tootake a snapshot of hello managed disk or a backup of hello disk outside of Azure Disk Encryption prior tooenabling encryption.</span></span>  <span data-ttu-id="0272f-316">Без резервной копии в месте любой непредвиденный сбой во время шифрования может сделать hello диск и виртуальная машина недоступными без параметра восстановления.</span><span class="sxs-lookup"><span data-stu-id="0272f-316">Without a backup in place, any unexpected failure during encryption may render hello disk and VM inaccessible without a recovery option.</span></span>  <span data-ttu-id="0272f-317">Набор AzureRmVMDiskEncryptionExtension в настоящее время не резервное копирование управляемых дисков и появится сообщение об ошибке, если используется для управляемого диска, если не был указан параметр - skipVmBackup hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-317">Set-AzureRmVMDiskEncryptionExtension does not currently back up managed disks and will error if used against a managed disk unless hello -skipVmBackup parameter has been specified.</span></span>  <span data-ttu-id="0272f-318">Этот параметр является небезопасным toouse, если резервной копии уже были внесены за пределами Azure шифрование диска.</span><span class="sxs-lookup"><span data-stu-id="0272f-318">This parameter is unsafe toouse unless a backup has already been made outside of Azure Disk Encryption.</span></span>   <span data-ttu-id="0272f-319">Если указан параметр - skipVmBackup hello, командлет hello не сделает резервную копию предыдущего tooencryption hello управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="0272f-319">When hello -skipVmBackup parameter is specified, hello cmdlet will not make a backup of hello managed disk prior tooencryption.</span></span>  <span data-ttu-id="0272f-320">По этой причине считается обязательным к установке toomake, убедиться, что требуется резервная копия hello управляемого диска, который виртуальная машина находится в месте предыдущих tooenabling шифрование диска Azure, в случае восстановления является более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="0272f-320">For this reason, it is considered a mandatory prerequisite toomake sure a backup of hello managed disk VM is in place prior tooenabling Azure Disk Encryption in case recovery is later needed.</span></span>  
> [!NOTE]
 > <span data-ttu-id="0272f-321">никогда не следует использовать Hello - skipVmBackup параметр, если моментальный снимок или резервная копия уже выполнен за пределами Azure шифрование диска.</span><span class="sxs-lookup"><span data-stu-id="0272f-321">hello -skipVmBackup parameter should never be used unless a snapshot or backup has already been made outside of Azure Disk Encryption.</span></span> 

* <span data-ttu-id="0272f-322">Hello решения по шифрованию диска Azure использует предохранитель внешнего ключа BitLocker hello ВМ IaaS Windows.</span><span class="sxs-lookup"><span data-stu-id="0272f-322">hello Azure Disk Encryption solution uses hello BitLocker external key protector for Windows IaaS VMs.</span></span> <span data-ttu-id="0272f-323">Если виртуальные машины присоединены к домену, не применяйте групповые политики, требующие использования предохранителей TPM.</span><span class="sxs-lookup"><span data-stu-id="0272f-323">For domain joined VMs, DO NOT push any group policies that enforce TPM protectors.</span></span> <span data-ttu-id="0272f-324">Сведения о групповой политике hello «Разрешить использование BitLocker без совместимого TPM» в разделе [Справочник по групповой политики BitLocker](https://technet.microsoft.com/library/ee706521).</span><span class="sxs-lookup"><span data-stu-id="0272f-324">For information about hello group policy for “Allow BitLocker without a compatible TPM,” see [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span></span>
* <span data-ttu-id="0272f-325">Политики BitLocker на виртуальных машинах, присоединенных к домену с помощью пользовательской групповой политики необходимо включить следующий параметр hello: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` шифрование диска Azure не сможет пользовательские параметры политики для Bitlocker несовместимы.</span><span class="sxs-lookup"><span data-stu-id="0272f-325">Bitlocker policy on domain joined virtual machines with custom group policy must include hello following setting: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key`  Azure Disk Encryption will fail when custom group policy settings for Bitlocker are incompatible.</span></span> <span data-ttu-id="0272f-326">На компьютерах, не имеющие hello может потребоваться правильный параметр политики, применение hello новой политики, принудительное hello tooupdate новой политики (gpupdate.exe/force) и повторный запуск.</span><span class="sxs-lookup"><span data-stu-id="0272f-326">On machines that did not have hello correct policy setting, applying hello new policy, forcing hello new policy tooupdate (gpupdate.exe /force), and then restarting may be required.</span></span>  
* <span data-ttu-id="0272f-327">toocreate приложения Azure AD, Создание хранилища ключей, или настроить существующие хранилища ключей и включения шифрования см. в разделе hello [шифрование диска Azure готовности сценарий PowerShell](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span><span class="sxs-lookup"><span data-stu-id="0272f-327">toocreate an Azure AD application, create a key vault, or set up an existing key vault and enable encryption, see hello [Azure Disk Encryption prerequisite PowerShell script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span></span>
* <span data-ttu-id="0272f-328">tooconfigure необходимых компонентов шифрование диска с помощью Azure CLI hello. в разделе [этот скрипт Bash](https://github.com/ejarvi/ade-cli-getting-started).</span><span class="sxs-lookup"><span data-stu-id="0272f-328">tooconfigure disk-encryption prerequisites using hello Azure CLI, see [this Bash script](https://github.com/ejarvi/ade-cli-getting-started).</span></span>
* <span data-ttu-id="0272f-329">tooback службы toouse hello резервное копирование и восстановление шифрование виртуальных машин, при включении шифрования с помощью шифрования диска Azure, зашифровать виртуальные машины с помощью настройки ключей шифрования диска Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-329">toouse hello Azure Backup service tooback up and restore encrypted VMs, when encryption is enabled with Azure Disk Encryption, encrypt your VMs by using hello Azure Disk Encryption key configuration.</span></span> <span data-ttu-id="0272f-330">Hello службы резервного копирования поддерживает виртуальные машины, которые зашифрованы с помощью ключа обмена Ключами конфигурации только.</span><span class="sxs-lookup"><span data-stu-id="0272f-330">hello Backup service supports VMs that are encrypted using KEK configuration only.</span></span> <span data-ttu-id="0272f-331">В разделе [способ tooback копирования и восстановления шифрования виртуальных машин с помощью шифрования резервной копии Azure](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span><span class="sxs-lookup"><span data-stu-id="0272f-331">See [How tooback up and restore encrypted virtual machines with Azure Backup  encryption](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span></span>

* <span data-ttu-id="0272f-332">При шифровании тома операционной системы Linux, обратите внимание, что перезагрузка виртуальной Машины требуются в данный момент в конце hello hello процесса.</span><span class="sxs-lookup"><span data-stu-id="0272f-332">When encrypting a Linux OS volume, note that a VM restart is currently required at hello end of hello process.</span></span> <span data-ttu-id="0272f-333">Это можно сделать через портал hello, powershell или интерфейс командной строки.</span><span class="sxs-lookup"><span data-stu-id="0272f-333">This can be done via hello portal, powershell, or CLI.</span></span>   <span data-ttu-id="0272f-334">Ход hello tootrack шифрования, периодически опрашивать hello возвращаемый Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus сообщение о состоянии.</span><span class="sxs-lookup"><span data-stu-id="0272f-334">tootrack hello progress of encryption, periodically poll hello status message returned by Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span></span>  <span data-ttu-id="0272f-335">После завершения шифрования возвращенный этой командой сообщение о состоянии hello hello сообщит об этом.</span><span class="sxs-lookup"><span data-stu-id="0272f-335">Once encryption is complete, hello hello status message returned by this command will indicate this.</span></span>  <span data-ttu-id="0272f-336">Например «ProgressMessage: успешно шифрование диска операционной системы, выполните перезагрузку hello виртуальной Машины» в этой точке hello ВМ можно перезапустить и использовать.</span><span class="sxs-lookup"><span data-stu-id="0272f-336">For example, "ProgressMessage: OS disk successfully encrypted, please reboot hello VM"  At this point hello VM can be restarted and used.</span></span>  

* <span data-ttu-id="0272f-337">Azure шифрование диска для Linux требует toohave диски данных подключенная файловая система в предыдущих tooencryption Linux</span><span class="sxs-lookup"><span data-stu-id="0272f-337">Azure Disk Encryption for Linux requires data disks toohave a mounted file system in Linux prior tooencryption</span></span>

* <span data-ttu-id="0272f-338">Рекурсивно подключенных данных не поддерживает диски hello шифрование диска Azure для Linux.</span><span class="sxs-lookup"><span data-stu-id="0272f-338">Recursively mounted data disks are not supported by hello Azure Disk Encryption for Linux.</span></span> <span data-ttu-id="0272f-339">Например если hello целевой системе монтирования диска на /foo/bar и затем еще одну на /foo/bar/baz шифрования hello /foo/bar/baz будет успешным, но шифрования/foo/полосы завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="0272f-339">For example, if hello target system has mounted a disk on /foo/bar and then another on /foo/bar/baz, hello encryption of /foo/bar/baz will succeed, but encryption of /foo/bar will fail.</span></span> 

* <span data-ttu-id="0272f-340">Azure шифрование диска поддерживается только в коллекции Azure поддерживается изображения, соответствующие требованиям упомянутой выше hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-340">Azure Disk Encryption is only supported on Azure gallery supported images that meet hello aforementioned prerequisites.</span></span> <span data-ttu-id="0272f-341">Клиент пользовательских образов из-за toocustom схемы секционирования и процесс поведения, которые могут существовать в эти образы не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="0272f-341">Customer custom images are not supported due toocustom partition schemes and process behaviors that may exist on these images.</span></span> <span data-ttu-id="0272f-342">Кроме того, даже виртуальные машины, созданные по образу из коллекции, который изначально соответствовал предварительным требованиям, но был изменен во время создания, могут быть несовместимы.</span><span class="sxs-lookup"><span data-stu-id="0272f-342">Further, even gallery image based VM's that initially met prerequisites but have been modified after creation may be incompatible.</span></span>  <span data-ttu-id="0272f-343">Для причине hello предлагаемые процедуры для шифрования ВМ Linux — toostart из чистой коллекции образов, зашифровать hello виртуальной Машины и программного обеспечения или toohello данных виртуальной Машины, при необходимости добавить.</span><span class="sxs-lookup"><span data-stu-id="0272f-343">For that reason, hello suggested procedure for encrypting a Linux VM is toostart from a clean gallery image, encrypt hello VM, and then add custom software or data toohello VM as needed.</span></span>  

> [!NOTE]
> <span data-ttu-id="0272f-344">Резервное копирование и восстановление виртуальных машин, зашифрованные поддерживается только для виртуальных машин, которые шифруются с помощью ключа обмена Ключами конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-344">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="0272f-345">Виртуальные машины, зашифрованные без ключа шифрования ключей, не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="0272f-345">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="0272f-346">KEK — это необязательный параметр для включения виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="0272f-346">KEK is an optional parameter that enables VM.</span></span>

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a><span data-ttu-id="0272f-347">Настройка hello приложения Azure AD в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0272f-347">Set up hello Azure AD application in Azure Active Directory</span></span>
<span data-ttu-id="0272f-348">Если вам требуется toobe шифрование включено на работающей ВМ в Azure, шифрование диска Azure создает и записывает хранилища ключей tooyour ключей шифрования hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-348">When you need encryption toobe enabled on a running VM in Azure, Azure Disk Encryption generates and writes hello encryption keys tooyour key vault.</span></span> <span data-ttu-id="0272f-349">Для управления ключами шифрования в хранилище ключей требуется аутентификация Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0272f-349">Managing encryption keys in your key vault requires Azure AD authentication.</span></span>

<span data-ttu-id="0272f-350">Для этой цели создайте приложение Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0272f-350">For this purpose, create an Azure AD application.</span></span> <span data-ttu-id="0272f-351">Можно найти подробные инструкции по регистрации приложения в разделе «Получение удостоверения приложения hello» hello hello блога [хранилище ключей Azure — шаг за шагом](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="0272f-351">You can find detailed steps for registering an application in hello “Get an Identity for hello Application” section of hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="0272f-352">В этой записи вы также найдете несколько полезных примеров подготовки и настройки хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="0272f-352">This post also contains a number of helpful examples for setting up and configuring your key vault.</span></span> <span data-ttu-id="0272f-353">Можно использовать аутентификацию на основе секрета клиента или на основе сертификата клиента в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0272f-353">For authentication purposes, you can use either client secret-based authentication or client certificate-based Azure AD authentication.</span></span>

#### <a name="client-secret-based-authentication-for-azure-ad"></a><span data-ttu-id="0272f-354">Аутентификация в Azure AD на основе секрета клиента</span><span class="sxs-lookup"><span data-stu-id="0272f-354">Client secret-based authentication for Azure AD</span></span>
<span data-ttu-id="0272f-355">Hello разделах, помогут настроить на основе секрет проверки подлинности клиента для Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0272f-355">hello sections that follow can help you configure a client secret-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a><span data-ttu-id="0272f-356">Создание приложения Azure AD с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0272f-356">Create an Azure AD application by using Azure PowerShell</span></span>
<span data-ttu-id="0272f-357">Используйте следующий командлет PowerShell toocreate приложения Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-357">Use hello following PowerShell cmdlet toocreate an Azure AD application:</span></span>

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> <span data-ttu-id="0272f-358">$azureAdApplication.ApplicationId — hello Azure AD ClientID, $aadClientSecret hello секрет клиента, что необходимо использовать более поздней версии tooenable шифрование диска Azure.</span><span class="sxs-lookup"><span data-stu-id="0272f-358">$azureAdApplication.ApplicationId is hello Azure AD ClientID and $aadClientSecret is hello client secret that you should use later tooenable Azure Disk Encryption.</span></span> <span data-ttu-id="0272f-359">Защита секрет клиента Azure AD hello соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="0272f-359">Safeguard hello Azure AD client secret appropriately.</span></span>

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a><span data-ttu-id="0272f-360">Настройка hello Azure AD идентификатор клиента и секрет из hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="0272f-360">Setting up hello Azure AD client ID and secret from hello Azure classic portal</span></span>
<span data-ttu-id="0272f-361">Также можно выполнить настройку идентификатор клиента Azure AD и секрет с помощью hello [классический портал Azure]( https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="0272f-361">You can also set up your Azure AD client ID and secret by using hello [Azure classic portal]( https://manage.windowsazure.com).</span></span> <span data-ttu-id="0272f-362">tooperform это задача, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="0272f-362">tooperform this task, do hello following:</span></span>

1. <span data-ttu-id="0272f-363">Нажмите кнопку hello **Active Directory** вкладки.</span><span class="sxs-lookup"><span data-stu-id="0272f-363">Click hello **Active Directory** tab.</span></span>

 ![Дисковое шифрование Azure](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. <span data-ttu-id="0272f-365">Нажмите кнопку **добавить приложение**и выберите имя приложения hello типа.</span><span class="sxs-lookup"><span data-stu-id="0272f-365">Click **Add Application**, and then type hello application name.</span></span>

 ![Дисковое шифрование Azure](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. <span data-ttu-id="0272f-367">Нажмите кнопку со стрелкой hello, а затем настройте свойства приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-367">Click hello arrow button, and then configure hello application properties.</span></span>

 ![Дисковое шифрование Azure](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. <span data-ttu-id="0272f-369">Щелкните флажок hello в нижнем левом углу toofinish hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-369">Click hello check mark in hello lower left corner toofinish.</span></span> <span data-ttu-id="0272f-370">Откроется страница настройки приложения Hello и идентификатор клиента Azure AD hello отображается внизу hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="0272f-370">hello application configuration page appears, and hello Azure AD client ID is displayed at hello bottom of hello page.</span></span>

 ![Дисковое шифрование Azure](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. <span data-ttu-id="0272f-372">Сохранить секрет клиента hello Azure AD, установив hello **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="0272f-372">Save hello Azure AD client secret by clicking hello **Save** button.</span></span> <span data-ttu-id="0272f-373">Обратите внимание, секрет клиента hello Azure AD в текстовом поле hello ключей.</span><span class="sxs-lookup"><span data-stu-id="0272f-373">Note hello Azure AD client secret in hello keys text box.</span></span> <span data-ttu-id="0272f-374">Храните его с соблюдением мер предосторожности.</span><span class="sxs-lookup"><span data-stu-id="0272f-374">Safeguard it appropriately.</span></span>

 ![Дисковое шифрование Azure](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > <span data-ttu-id="0272f-376">Hello предшествующий потока не поддерживается на hello классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0272f-376">hello preceding flow is not supported on hello Azure classic portal.</span></span>

##### <a name="use-an-existing-application"></a><span data-ttu-id="0272f-377">Использование существующего приложения</span><span class="sxs-lookup"><span data-stu-id="0272f-377">Use an existing application</span></span>
<span data-ttu-id="0272f-378">tooexecute hello, следующие команды, получения и использования hello [модуля Azure AD PowerShell](https://technet.microsoft.com/library/jj151815.aspx).</span><span class="sxs-lookup"><span data-stu-id="0272f-378">tooexecute hello following commands, obtain and use hello [Azure AD PowerShell module](https://technet.microsoft.com/library/jj151815.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="0272f-379">Hello следующие команды должен выполняться из нового окна PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0272f-379">hello following commands must be executed from a new PowerShell window.</span></span> <span data-ttu-id="0272f-380">Не использовать Azure PowerShell или команды hello tooexecute окно диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-380">Do not use Azure PowerShell or hello Azure Resource Manager window tooexecute hello commands.</span></span> <span data-ttu-id="0272f-381">Такой подход рекомендуется из-за этих командлетов в модуле MSOnline hello или Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0272f-381">We recommend this approach because these cmdlets are in hello MSOnline module or Azure AD PowerShell.</span></span>

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a><span data-ttu-id="0272f-382">Аутентификация на основе сертификата в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0272f-382">Certificate-based authentication for Azure AD</span></span>
> [!NOTE]
> <span data-ttu-id="0272f-383">В настоящее время аутентификация на основе сертификата Azure AD на виртуальных машинах Linux не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="0272f-383">Azure AD certificate-based authentication is currently not supported on Linux VMs.</span></span>

<span data-ttu-id="0272f-384">Здравствуйте разделах Показать как tooconfigure проверку подлинности на основе сертификатов для Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0272f-384">hello sections that follow show how tooconfigure a certificate-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application"></a><span data-ttu-id="0272f-385">Создание приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="0272f-385">Create an Azure AD application</span></span>
<span data-ttu-id="0272f-386">toocreate приложения Azure AD, выполните следующие командлеты PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="0272f-386">toocreate an Azure AD application, execute hello following PowerShell cmdlets:</span></span>

> [!NOTE]
> <span data-ttu-id="0272f-387">Замените следующую hello `yourpassword` строка, в которой безопасного пароля и защиты паролем hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-387">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

<span data-ttu-id="0272f-388">После завершения этого этапа Отправка хранилища ключей tooyour файл PFX и включить toodeploy политики, необходимый для доступа к hello, сертификат tooa виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0272f-388">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy needed toodeploy that certificate tooa VM.</span></span>

##### <a name="use-an-existing-azure-ad-application"></a><span data-ttu-id="0272f-389">Использование существующего приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="0272f-389">Use an existing Azure AD application</span></span>
<span data-ttu-id="0272f-390">При настройке проверки подлинности на основе сертификатов для существующего приложения, используйте командлеты PowerShell hello, показано ниже.</span><span class="sxs-lookup"><span data-stu-id="0272f-390">If you are configuring certificate-based authentication for an existing application, use hello PowerShell cmdlets shown here.</span></span> <span data-ttu-id="0272f-391">Быть tooexecute убедиться, что с помощью нового окна PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0272f-391">Be sure tooexecute them from a new PowerShell window.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

<span data-ttu-id="0272f-392">После завершения этого этапа, передайте хранилища ключей tooyour файл PFX и включить политику доступа hello достаточно toodeploy hello сертификат tooa виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0272f-392">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy that's needed toodeploy hello certificate tooa VM.</span></span>

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a><span data-ttu-id="0272f-393">Отправка хранилища ключей tooyour файла PFX</span><span class="sxs-lookup"><span data-stu-id="0272f-393">Upload a PFX file tooyour key vault</span></span>
<span data-ttu-id="0272f-394">Подробное описание этого процесса см. в разделе [hello официальный блог группы хранилища Azure ключ](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span><span class="sxs-lookup"><span data-stu-id="0272f-394">For a detailed explanation of this process, see [hello Official Azure Key Vault Team Blog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span></span> <span data-ttu-id="0272f-395">Однако следующие командлеты PowerShell hello, все, что требуется для задачи «hello».</span><span class="sxs-lookup"><span data-stu-id="0272f-395">However, hello following PowerShell cmdlets are all you need for hello task.</span></span> <span data-ttu-id="0272f-396">Быть tooexecute убедиться, что их из консоли Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0272f-396">Be sure tooexecute them from Azure PowerShell console.</span></span>

> [!NOTE]
> <span data-ttu-id="0272f-397">Замените следующую hello `yourpassword` строка, в которой безопасного пароля и защиты паролем hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-397">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a><span data-ttu-id="0272f-398">Развертывание сертификата в вашей tooan хранилища ключей существующей виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="0272f-398">Deploy a certificate in your key vault tooan existing VM</span></span>
<span data-ttu-id="0272f-399">После завершения передачи hello PFX, разверните сертификат в существующей виртуальной Машины с hello следующих tooan хранилища ключей hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-399">After you finish uploading hello PFX, deploy a certificate in hello key vault tooan existing VM with hello following:</span></span>
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a><span data-ttu-id="0272f-400">Настройте политику доступа hello хранилища ключей для приложения hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0272f-400">Set up hello key vault access policy for hello Azure AD application</span></span>
<span data-ttu-id="0272f-401">Azure AD приложению права tooaccess hello ключей или секреты в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-401">Your Azure AD application needs rights tooaccess hello keys or secrets in hello vault.</span></span> <span data-ttu-id="0272f-402">Используйте hello [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) командлет toogrant разрешения toohello приложение, используя идентификатор клиента hello (который был создан при регистрации приложения hello) как hello _ServicePrincipalName —_ значение параметра.</span><span class="sxs-lookup"><span data-stu-id="0272f-402">Use hello [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant permissions toohello application, using hello client ID (which was generated when hello application was registered) as hello _–ServicePrincipalName_ parameter value.</span></span> <span data-ttu-id="0272f-403">hello записи блога, см. toolearn [хранилище ключей Azure — шаг за шагом](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="0272f-403">toolearn more, see hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="0272f-404">Ниже приведен пример как tooperform это задачи через PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0272f-404">Here is an example of how tooperform this task via PowerShell:</span></span>

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> <span data-ttu-id="0272f-405">Azure шифрование диска требуются следующие доступ политики tooyour Azure AD клиентское приложение hello tooconfigure: _WrapKey_ и _задать_ разрешения.</span><span class="sxs-lookup"><span data-stu-id="0272f-405">Azure Disk Encryption requires you tooconfigure hello following access policies tooyour Azure AD client application: _WrapKey_ and _Set_ permissions.</span></span>

## <a name="terminology"></a><span data-ttu-id="0272f-406">Терминология</span><span class="sxs-lookup"><span data-stu-id="0272f-406">Terminology</span></span>
<span data-ttu-id="0272f-407">Некоторые из основных терминах hello используется эта технология используется hello в следующей таблице терминология toounderstand:</span><span class="sxs-lookup"><span data-stu-id="0272f-407">toounderstand some of hello common terms used by this technology, use hello following terminology table:</span></span>

| <span data-ttu-id="0272f-408">Терминология</span><span class="sxs-lookup"><span data-stu-id="0272f-408">Terminology</span></span> | <span data-ttu-id="0272f-409">Определение</span><span class="sxs-lookup"><span data-stu-id="0272f-409">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="0272f-410">Azure AD</span><span class="sxs-lookup"><span data-stu-id="0272f-410">Azure AD</span></span> | <span data-ttu-id="0272f-411">Azure AD — это сокращенное обозначение [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="0272f-411">Azure AD is [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span></span> <span data-ttu-id="0272f-412">Учетная запись Azure AD необходима для аутентификации, хранения секретов в хранилище ключей и извлечения их из него.</span><span class="sxs-lookup"><span data-stu-id="0272f-412">An Azure AD account is a prerequisite for authenticating, storing, and retrieving secrets from a key vault.</span></span> |
| <span data-ttu-id="0272f-413">Хранилище ключей Azure</span><span class="sxs-lookup"><span data-stu-id="0272f-413">Azure Key Vault</span></span> | <span data-ttu-id="0272f-414">Key Vault представляет собой службу управления криптографическими ключами. Она основана на аппаратных модулях безопасности, соответствующих Федеральному стандарту обработки информации (FIPS), и позволяет надежно хранить криптографические ключи и конфиденциальные данные.</span><span class="sxs-lookup"><span data-stu-id="0272f-414">Key Vault is a cryptographic, key management service that's based on Federal Information Processing Standards (FIPS)-validated hardware security modules, which help safeguard your cryptographic keys and sensitive secrets.</span></span> <span data-ttu-id="0272f-415">Дополнительные сведения см. в документации по [Key Vault](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="0272f-415">For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="0272f-416">ARM</span><span class="sxs-lookup"><span data-stu-id="0272f-416">ARM</span></span> | <span data-ttu-id="0272f-417">Диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="0272f-417">Azure Resource Manager</span></span> |
| <span data-ttu-id="0272f-418">BitLocker</span><span class="sxs-lookup"><span data-stu-id="0272f-418">BitLocker</span></span> |<span data-ttu-id="0272f-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) является отрасли Windows тома технологии шифрования, использовал шифрование диска tooenable на виртуальных машинах IaaS Windows.</span><span class="sxs-lookup"><span data-stu-id="0272f-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is an industry-recognized Windows volume encryption technology that's used tooenable disk encryption on Windows IaaS VMs.</span></span> |
| <span data-ttu-id="0272f-420">BEK</span><span class="sxs-lookup"><span data-stu-id="0272f-420">BEK</span></span> | <span data-ttu-id="0272f-421">Ключи шифрования BitLocker, используемые tooencrypt hello ОС загрузочного тома и тома данных.</span><span class="sxs-lookup"><span data-stu-id="0272f-421">BitLocker encryption keys are used tooencrypt hello OS boot volume and data volumes.</span></span> <span data-ttu-id="0272f-422">в хранилище ключей в виде секретов об ключи BitLocker Hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-422">hello BitLocker keys are safeguarded in a key vault as secrets.</span></span> |
| <span data-ttu-id="0272f-423">Интерфейс командной строки</span><span class="sxs-lookup"><span data-stu-id="0272f-423">CLI</span></span> | <span data-ttu-id="0272f-424">Ознакомьтесь с разделом [Интерфейс командной строки Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="0272f-424">See [Azure command-line interface](../cli-install-nodejs.md).</span></span> |
| <span data-ttu-id="0272f-425">DM-Crypt</span><span class="sxs-lookup"><span data-stu-id="0272f-425">DM-Crypt</span></span> |<span data-ttu-id="0272f-426">[Интеллектуальный анализ данных Crypt](https://en.wikipedia.org/wiki/Dm-crypt) — подсистема диска шифрования на основе Linux, прозрачный hello использовал шифрование диска tooenable на виртуальных машинах IaaS Linux.</span><span class="sxs-lookup"><span data-stu-id="0272f-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is hello Linux-based, transparent disk-encryption subsystem that's used tooenable disk encryption on Linux IaaS VMs.</span></span> |
| <span data-ttu-id="0272f-427">KEK</span><span class="sxs-lookup"><span data-stu-id="0272f-427">KEK</span></span> | <span data-ttu-id="0272f-428">Ключ шифрования ключа — hello асимметричного ключа (RSA 2048) можно использовать tooprotect или перенос секрет hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-428">Key encryption key is hello asymmetric key (RSA 2048) that you can use tooprotect or wrap hello secret.</span></span> <span data-ttu-id="0272f-429">Вы можете использовать защищенный HSM-ключ или ключ с программной защитой.</span><span class="sxs-lookup"><span data-stu-id="0272f-429">You can provide a hardware security modules (HSM)-protected key or software-protected key.</span></span> <span data-ttu-id="0272f-430">Дополнительные сведения см. в документации по [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="0272f-430">For more details, see [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="0272f-431">Командлеты PS</span><span class="sxs-lookup"><span data-stu-id="0272f-431">PS cmdlets</span></span> | <span data-ttu-id="0272f-432">Ознакомьтесь с [командлетами Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0272f-432">See [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span> |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a><span data-ttu-id="0272f-433">Установка и настройка хранилища ключей для шифрования дисков Azure</span><span class="sxs-lookup"><span data-stu-id="0272f-433">Set up and configure your key vault for Azure Disk Encryption</span></span>
<span data-ttu-id="0272f-434">Azure шифрование диска помогает защитить hello шифрование диска ключи и секретные данные в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="0272f-434">Azure Disk Encryption helps safeguard hello disk-encryption keys and secrets in your key vault.</span></span> <span data-ttu-id="0272f-435">tooset копирование хранилища ключей для шифрования диска Azure hello завершения действия в каждом hello в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="0272f-435">tooset up your key vault for Azure Disk Encryption, complete hello steps in each of hello following sections.</span></span>

#### <a name="create-a-key-vault"></a><span data-ttu-id="0272f-436">Создайте хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="0272f-436">Create a key vault</span></span>
<span data-ttu-id="0272f-437">toocreate хранилища ключей, используйте один из следующих вариантов hello:</span><span class="sxs-lookup"><span data-stu-id="0272f-437">toocreate a key vault, use one of hello following options:</span></span>

* [<span data-ttu-id="0272f-438">Шаблон Resource Manager 101-Key-Vault-Create</span><span class="sxs-lookup"><span data-stu-id="0272f-438">"101-Key-Vault-Create" Resource Manager template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* <span data-ttu-id="0272f-439">[командлеты Azure PowerShell для хранилища ключей](/powershell/module/azurerm.keyvault/#key_vault);</span><span class="sxs-lookup"><span data-stu-id="0272f-439">[Azure PowerShell key vault cmdlets](/powershell/module/azurerm.keyvault/#key_vault)</span></span>
* <span data-ttu-id="0272f-440">Диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="0272f-440">Azure Resource Manager</span></span>
* <span data-ttu-id="0272f-441">Как слишком[безопасного хранилища ключей](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span><span class="sxs-lookup"><span data-stu-id="0272f-441">How too[Secure your key vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span></span>

> [!NOTE]
> <span data-ttu-id="0272f-442">Если вы уже настроили хранилища ключей для вашей подписки, пропустите следующий раздел toohello.</span><span class="sxs-lookup"><span data-stu-id="0272f-442">If you have already set up a key vault for your subscription, skip toohello next section.</span></span>

![Хранилище ключей Azure](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a><span data-ttu-id="0272f-444">Настройка ключа шифрования ключей (необязательно)</span><span class="sxs-lookup"><span data-stu-id="0272f-444">Set up a key encryption key (optional)</span></span>
<span data-ttu-id="0272f-445">Если требуется дополнительный уровень безопасности для ключей шифрования BitLocker hello toouse ключа обмена Ключами, добавьте хранилище ключей tooyour ключа обмена Ключами.</span><span class="sxs-lookup"><span data-stu-id="0272f-445">If you want toouse a KEK for an additional layer of security for hello BitLocker encryption keys, add a KEK tooyour key vault.</span></span> <span data-ttu-id="0272f-446">Используйте hello [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) toocreate командлет ключа шифрования ключа в хранилище ключей hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-446">Use hello [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet toocreate a key encryption key in hello key vault.</span></span> <span data-ttu-id="0272f-447">Кроме того, KEK можно импортировать из своего локального модуля HSM службы управления ключами.</span><span class="sxs-lookup"><span data-stu-id="0272f-447">You can also import a KEK from your on-premises key management HSM.</span></span> <span data-ttu-id="0272f-448">Дополнительные сведения см. в [документации по Key Vault](https://azure.microsoft.com/documentation/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="0272f-448">For more details, see [Key Vault Documentation](https://azure.microsoft.com/documentation/services/key-vault/).</span></span>

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

<span data-ttu-id="0272f-449">Можно добавить hello ключа обмена Ключами, перейдя tooAzure диспетчера ресурсов, либо с помощью интерфейса хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="0272f-449">You can add hello KEK by going tooAzure Resource Manager or by using your key vault interface.</span></span>

![Хранилище ключей Azure](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a><span data-ttu-id="0272f-451">Задание разрешений хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="0272f-451">Set key vault permissions</span></span>
<span data-ttu-id="0272f-452">Hello платформы Azure требует ключи шифрования toohello доступа или секреты в хранилище ключей toomake их доступных toohello ВМ для загрузки и расшифровки hello тома.</span><span class="sxs-lookup"><span data-stu-id="0272f-452">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello VM for booting and decrypting hello volumes.</span></span> <span data-ttu-id="0272f-453">разрешения toogrant toohello платформы Azure, набор hello **EnabledForDiskEncryption** свойство hello ключа в хранилище с помощью командлета PowerShell hello хранилища ключей:</span><span class="sxs-lookup"><span data-stu-id="0272f-453">toogrant permissions toohello Azure platform, set hello **EnabledForDiskEncryption** property in hello key vault by using hello key vault PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

<span data-ttu-id="0272f-454">Можно также задать hello **EnabledForDiskEncryption** свойства, перейдя по адресу hello [обозревателя ресурсов Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0272f-454">You can also set hello **EnabledForDiskEncryption** property by visiting hello [Azure Resource Explorer](https://resources.azure.com).</span></span>

<span data-ttu-id="0272f-455">Как упоминалось ранее, необходимо задать hello **EnabledForDiskEncryption** свойства в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="0272f-455">As mentioned earlier, you must set hello **EnabledForDiskEncryption** property on your key vault.</span></span> <span data-ttu-id="0272f-456">В противном случае произойдет сбой развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-456">Otherwise, hello deployment will fail.</span></span>

<span data-ttu-id="0272f-457">Можно настроить политики доступа для приложения Azure AD из интерфейса hello хранилища ключей, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="0272f-457">You can set up access policies for your Azure AD application from hello key vault interface, as shown here:</span></span>

![Хранилище ключей Azure](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Хранилище ключей Azure](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

<span data-ttu-id="0272f-460">На hello **политики расширенного доступа** , убедитесь, что хранилище ключей включено шифрование диска Azure:</span><span class="sxs-lookup"><span data-stu-id="0272f-460">On hello **Advanced access policies** tab, make sure that your key vault is enabled for Azure Disk Encryption:</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a><span data-ttu-id="0272f-462">Сценарии развертывания шифрования дисков и взаимодействие с пользователем</span><span class="sxs-lookup"><span data-stu-id="0272f-462">Disk-encryption deployment scenarios and user experiences</span></span>
<span data-ttu-id="0272f-463">Можно включить множество сценариев шифрования диска и hello шаги могут различаться соответствующим toohello сценария.</span><span class="sxs-lookup"><span data-stu-id="0272f-463">You can enable many disk-encryption scenarios, and hello steps may vary according toohello scenario.</span></span> <span data-ttu-id="0272f-464">Hello следующих разделах описаны сценарии hello более подробно.</span><span class="sxs-lookup"><span data-stu-id="0272f-464">hello following sections cover hello scenarios in greater detail.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a><span data-ttu-id="0272f-465">Включить шифрование на новые виртуальные машины IaaS, созданными на Marketplace hello</span><span class="sxs-lookup"><span data-stu-id="0272f-465">Enable encryption on new IaaS VMs that are created from hello Marketplace</span></span>
<span data-ttu-id="0272f-466">Можно включить шифрование диска на новой виртуальной Машины IaaS Windows из hello Marketplace в Azure с помощью hello [шаблона диспетчера ресурсов](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span><span class="sxs-lookup"><span data-stu-id="0272f-466">You can enable disk encryption on new IaaS Windows VM from hello Marketplace in Azure by using hello  [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span></span>

1. <span data-ttu-id="0272f-467">Hello Azure краткое шаблон, нажмите кнопку **развертывание tooAzure**, введите конфигурацию шифрования hello на hello **параметры** и, при необходимости нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0272f-467">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="0272f-468">Выберите подписку hello, группы ресурсов, расположение группы ресурсов, условия и соглашения и нажмите кнопку **создать** tooenable шифрование на новую виртуальную Машину IaaS.</span><span class="sxs-lookup"><span data-stu-id="0272f-468">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="0272f-469">Этот шаблон создает новое зашифрованное виртуальной Машине Windows, использующего коллекции образ Windows Server 2012 hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-469">This template creates a new encrypted Windows VM that uses hello Windows Server 2012 gallery image.</span></span>

<span data-ttu-id="0272f-470">Шифрование дисков на новой виртуальной машине IaaS под управлением RedHat Linux 7.2 с 200 ГБ массивом RAID-0 можно включить с помощью этого [шаблона Resource Manager](https://aka.ms/fde-rhel).</span><span class="sxs-lookup"><span data-stu-id="0272f-470">You can enable disk encryption on a new IaaS RedHat Linux 7.2 VM with a 200-GB RAID-0 array by using this [Resource Manager template](https://aka.ms/fde-rhel).</span></span> <span data-ttu-id="0272f-471">После развертывания шаблона hello, проверьте состояние шифрования hello виртуальной Машины с помощью hello `Get-AzureRmVmDiskEncryptionStatus` командлет, как описано в [диска шифрования ОС на работающей ВМ Linux](#encrypting-os-drive-on-a-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="0272f-471">After you deploy hello template, verify hello VM encryption status by using hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet, as described in [Encrypting OS drive on a running Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span></span> <span data-ttu-id="0272f-472">Если машины hello возвращается в состояние _VMRestartPending_, перезапустите hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0272f-472">When hello machine returns a status of _VMRestartPending_, restart hello VM.</span></span>

<span data-ttu-id="0272f-473">Hello следующей таблице перечислены параметры шаблона диспетчера ресурсов hello для новых виртуальных машин из Marketplace сценарий hello, с помощью идентификатора клиента Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0272f-473">hello following table lists hello Resource Manager template parameters for new VMs from hello Marketplace scenario using Azure AD client ID:</span></span>

| <span data-ttu-id="0272f-474">Параметр</span><span class="sxs-lookup"><span data-stu-id="0272f-474">Parameter</span></span> | <span data-ttu-id="0272f-475">Описание</span><span class="sxs-lookup"><span data-stu-id="0272f-475">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0272f-476">adminUserName</span><span class="sxs-lookup"><span data-stu-id="0272f-476">adminUserName</span></span> | <span data-ttu-id="0272f-477">Имя пользователя администратора для виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-477">Admin user name for hello virtual machine.</span></span> |
| <span data-ttu-id="0272f-478">adminPassword</span><span class="sxs-lookup"><span data-stu-id="0272f-478">adminPassword</span></span> | <span data-ttu-id="0272f-479">Пароль пользователя администратора для виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-479">Admin user password for hello virtual machine.</span></span> |
| <span data-ttu-id="0272f-480">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="0272f-480">newStorageAccountName</span></span> | <span data-ttu-id="0272f-481">Имя toostore учетной записи хранилища hello ОС и виртуальных жестких дисков данных.</span><span class="sxs-lookup"><span data-stu-id="0272f-481">Name of hello storage account toostore OS and data VHDs.</span></span> |
| <span data-ttu-id="0272f-482">vmSize</span><span class="sxs-lookup"><span data-stu-id="0272f-482">vmSize</span></span> | <span data-ttu-id="0272f-483">Размер hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0272f-483">Size of hello VM.</span></span> <span data-ttu-id="0272f-484">Сейчас поддерживаются только серии A, D и G уровня "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="0272f-484">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="0272f-485">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="0272f-485">virtualNetworkName</span></span> | <span data-ttu-id="0272f-486">Имя виртуальной сети, сетевой Адаптер виртуальной Машины hello hello должны принадлежать.</span><span class="sxs-lookup"><span data-stu-id="0272f-486">Name of hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="0272f-487">subnetName</span><span class="sxs-lookup"><span data-stu-id="0272f-487">subnetName</span></span> | <span data-ttu-id="0272f-488">Имя подсети hello в hello виртуальной сети, hello сетевого Адаптера виртуальной Машины должны принадлежать.</span><span class="sxs-lookup"><span data-stu-id="0272f-488">Name of hello subnet in hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="0272f-489">AADClientID</span><span class="sxs-lookup"><span data-stu-id="0272f-489">AADClientID</span></span> | <span data-ttu-id="0272f-490">Идентификатор клиента приложения hello Azure AD с хранилище ключей tooyour секреты toowrite разрешения.</span><span class="sxs-lookup"><span data-stu-id="0272f-490">Client ID of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="0272f-491">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="0272f-491">AADClientSecret</span></span> | <span data-ttu-id="0272f-492">Секрет клиента приложения Azure AD hello хранилища ключей tooyour секреты toowrite разрешения.</span><span class="sxs-lookup"><span data-stu-id="0272f-492">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="0272f-493">keyVaultURL</span><span class="sxs-lookup"><span data-stu-id="0272f-493">keyVaultURL</span></span> | <span data-ttu-id="0272f-494">URL-адрес hello ключ хранилища, должна быть передана ключ BitLocker hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-494">URL of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="0272f-495">Его можно получить с помощью командлета hello `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span><span class="sxs-lookup"><span data-stu-id="0272f-495">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span></span> |
| <span data-ttu-id="0272f-496">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="0272f-496">keyEncryptionKeyURL</span></span> | <span data-ttu-id="0272f-497">URL-адрес ключа шифрования ключа hello, используемые tooencrypt hello созданный ключ BitLocker (необязательно).</span><span class="sxs-lookup"><span data-stu-id="0272f-497">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key (optional).</span></span> |
| <span data-ttu-id="0272f-498">keyVaultResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0272f-498">keyVaultResourceGroup</span></span> | <span data-ttu-id="0272f-499">Группа ресурсов хранилища ключей hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-499">Resource group of hello key vault.</span></span> |
| <span data-ttu-id="0272f-500">vmName</span><span class="sxs-lookup"><span data-stu-id="0272f-500">vmName</span></span> | <span data-ttu-id="0272f-501">Hello виртуальной Машины, операция шифрования hello называется toobe блокировкой.</span><span class="sxs-lookup"><span data-stu-id="0272f-501">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="0272f-502">_KeyEncryptionKeyURL_ является необязательным параметром.</span><span class="sxs-lookup"><span data-stu-id="0272f-502">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="0272f-503">Собственные KEK toofurther защиты hello ключ шифрования данных (секрет парольную фразу) можно импортировать в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="0272f-503">You can bring your own KEK toofurther safeguard hello data encryption key (Passphrase secret) in your key vault.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a><span data-ttu-id="0272f-504">Включение шифрования для новых виртуальных машин IaaS, при создании которых используются пользовательские зашифрованные виртуальные жесткие диски и ключи шифрования</span><span class="sxs-lookup"><span data-stu-id="0272f-504">Enable encryption on new IaaS VMs that are created from customer-encrypted VHD and encryption keys</span></span>
<span data-ttu-id="0272f-505">В этом сценарии можно включить шифрование с помощью шаблона диспетчера ресурсов hello, командлеты PowerShell или команды CLI.</span><span class="sxs-lookup"><span data-stu-id="0272f-505">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="0272f-506">Hello следующих разделах объясняется в шаблона диспетчера ресурсов hello больше сведений и командах CLI.</span><span class="sxs-lookup"><span data-stu-id="0272f-506">hello following sections explain in greater detail hello Resource Manager template and CLI commands.</span></span>

<span data-ttu-id="0272f-507">Следуйте инструкциям Привет одному из этих разделов Подготовка предварительно зашифрованный образов, которые могут использоваться в Azure.</span><span class="sxs-lookup"><span data-stu-id="0272f-507">Follow hello instructions from one of these sections for preparing pre-encrypted images that can be used in Azure.</span></span> <span data-ttu-id="0272f-508">После создания образа hello hello действия можно использовать в toocreate далее разделе hello зашифрованные ВМ Azure.</span><span class="sxs-lookup"><span data-stu-id="0272f-508">After hello image is created, you can use hello steps in hello next section toocreate an encrypted Azure VM.</span></span>

* [<span data-ttu-id="0272f-509">Подготовка предварительно зашифрованного виртуального жесткого диска Windows</span><span class="sxs-lookup"><span data-stu-id="0272f-509">Prepare a pre-encrypted Windows VHD</span></span>](#preparing-a-pre-encrypted-windows-vhd)
* [<span data-ttu-id="0272f-510">Подготовка предварительно зашифрованного виртуального жесткого диска Linux</span><span class="sxs-lookup"><span data-stu-id="0272f-510">Prepare a pre-encrypted Linux VHD</span></span>](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="0272f-511">С помощью шаблона диспетчера ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="0272f-511">Using hello Resource Manager template</span></span>
<span data-ttu-id="0272f-512">Можно включить шифрование диска на зашифрованные им с помощью hello [шаблона диспетчера ресурсов](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span><span class="sxs-lookup"><span data-stu-id="0272f-512">You can enable disk encryption on your encrypted VHD by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span></span>

1. <span data-ttu-id="0272f-513">Hello Azure краткое шаблон, нажмите кнопку **развертывание tooAzure**, введите конфигурацию шифрования hello на hello **параметры** и, при необходимости нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0272f-513">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="0272f-514">Выберите подписку hello, группы ресурсов, расположение группы ресурсов, условия и соглашения и нажмите кнопку **создать** tooenable шифрование на hello новой виртуальной Машины IaaS.</span><span class="sxs-lookup"><span data-stu-id="0272f-514">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello new IaaS VM.</span></span>

<span data-ttu-id="0272f-515">Hello следующей таблице перечислены параметры шаблона диспетчера ресурсов hello для вашего зашифрованные виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="0272f-515">hello following table lists hello Resource Manager template parameters for your encrypted VHD:</span></span>

| <span data-ttu-id="0272f-516">Параметр</span><span class="sxs-lookup"><span data-stu-id="0272f-516">Parameter</span></span> | <span data-ttu-id="0272f-517">Описание</span><span class="sxs-lookup"><span data-stu-id="0272f-517">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0272f-518">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="0272f-518">newStorageAccountName</span></span> | <span data-ttu-id="0272f-519">Имя hello toostore учетной записи хранилища hello шифруются виртуального жесткого диска операционной системы.</span><span class="sxs-lookup"><span data-stu-id="0272f-519">Name of hello storage account toostore hello encrypted OS VHD.</span></span> <span data-ttu-id="0272f-520">Эта учетная запись должна уже были созданы в hello же группу ресурсов и местоположения hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0272f-520">This storage account should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="0272f-521">osVhdUri</span><span class="sxs-lookup"><span data-stu-id="0272f-521">osVhdUri</span></span> | <span data-ttu-id="0272f-522">URI hello виртуального жесткого диска операционной системы из учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-522">URI of hello OS VHD from hello storage account.</span></span> |
| <span data-ttu-id="0272f-523">osType</span><span class="sxs-lookup"><span data-stu-id="0272f-523">osType</span></span> | <span data-ttu-id="0272f-524">Тип продукта ОС (Windows, Linux).</span><span class="sxs-lookup"><span data-stu-id="0272f-524">OS product type (Windows/Linux).</span></span> |
| <span data-ttu-id="0272f-525">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="0272f-525">virtualNetworkName</span></span> | <span data-ttu-id="0272f-526">Имя виртуальной сети, сетевой Адаптер виртуальной Машины hello hello должны принадлежать.</span><span class="sxs-lookup"><span data-stu-id="0272f-526">Name of hello VNet that hello VM NIC should belong to.</span></span> <span data-ttu-id="0272f-527">Hello имя должна уже быть создана в hello же группу ресурсов и местоположения hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0272f-527">hello name should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="0272f-528">subnetName</span><span class="sxs-lookup"><span data-stu-id="0272f-528">subnetName</span></span> | <span data-ttu-id="0272f-529">Имя подсети hello на hello виртуальной сети, hello сетевого Адаптера виртуальной Машины должны принадлежать.</span><span class="sxs-lookup"><span data-stu-id="0272f-529">Name of hello subnet on hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="0272f-530">vmSize</span><span class="sxs-lookup"><span data-stu-id="0272f-530">vmSize</span></span> | <span data-ttu-id="0272f-531">Размер hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0272f-531">Size of hello VM.</span></span> <span data-ttu-id="0272f-532">Сейчас поддерживаются только серии A, D и G уровня "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="0272f-532">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="0272f-533">keyVaultResourceID</span><span class="sxs-lookup"><span data-stu-id="0272f-533">keyVaultResourceID</span></span> | <span data-ttu-id="0272f-534">Hello ResourceID, который определяет ресурсы хранилища ключей hello в диспетчере ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="0272f-534">hello ResourceID that identifies hello key vault resource in Azure Resource Manager.</span></span> <span data-ttu-id="0272f-535">Его можно получить с помощью командлета PowerShell hello `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span><span class="sxs-lookup"><span data-stu-id="0272f-535">You can get it by using hello PowerShell cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span></span> |
| <span data-ttu-id="0272f-536">keyVaultSecretUrl</span><span class="sxs-lookup"><span data-stu-id="0272f-536">keyVaultSecretUrl</span></span> | <span data-ttu-id="0272f-537">URL-адрес ключа шифрования диска hello, установлены в хранилище ключей hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-537">URL of hello disk-encryption key that's set up in hello key vault.</span></span> |
| <span data-ttu-id="0272f-538">keyVaultKekUrl</span><span class="sxs-lookup"><span data-stu-id="0272f-538">keyVaultKekUrl</span></span> | <span data-ttu-id="0272f-539">URL-адрес ключа hello ключа шифрования для шифрования hello создается ключ шифрования диска.</span><span class="sxs-lookup"><span data-stu-id="0272f-539">URL of hello key encryption key for encrypting hello generated disk-encryption key.</span></span> |
| <span data-ttu-id="0272f-540">vmName</span><span class="sxs-lookup"><span data-stu-id="0272f-540">vmName</span></span> | <span data-ttu-id="0272f-541">Имя ВМ IaaS hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-541">Name of hello IaaS VM.</span></span> |

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="0272f-542">Использование командлетов PowerShell</span><span class="sxs-lookup"><span data-stu-id="0272f-542">Using PowerShell cmdlets</span></span>
<span data-ttu-id="0272f-543">Можно включить шифрование диска на зашифрованные им с помощью командлета PowerShell hello [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="0272f-543">You can enable disk encryption on your encrypted VHD by using hello PowerShell cmdlet [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span>  

#### <a name="using-cli-commands"></a><span data-ttu-id="0272f-544">Использование команд интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="0272f-544">Using CLI commands</span></span>
<span data-ttu-id="0272f-545">Шифрование диска tooenable для этого сценария с помощью команды CLI hello следующие:</span><span class="sxs-lookup"><span data-stu-id="0272f-545">tooenable disk encryption for this scenario by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="0272f-546">Задайте политики доступа в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="0272f-546">Set access policies in your key vault:</span></span>

   * <span data-ttu-id="0272f-547">Набор hello **EnabledForDiskEncryption** флаг:</span><span class="sxs-lookup"><span data-stu-id="0272f-547">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="0272f-548">Набор разрешений tooAzure AD приложения toowrite секреты tooyour хранилища ключей:</span><span class="sxs-lookup"><span data-stu-id="0272f-548">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="0272f-549">шифрование tooenable на виртуальной Машине существующий или не запущены, тип:</span><span class="sxs-lookup"><span data-stu-id="0272f-549">tooenable encryption on an existing or running VM, type:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="0272f-550">Получите состояние шифрования, введя следующую команду.</span><span class="sxs-lookup"><span data-stu-id="0272f-550">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="0272f-551">шифрование tooenable на новой виртуальной Машины с зашифрованного диска, hello используйте следующие параметры с hello `azure vm create` команды:</span><span class="sxs-lookup"><span data-stu-id="0272f-551">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a><span data-ttu-id="0272f-552">Включение шифрования на виртуальной машине IaaS Windows, которая уже существует или работает в Azure</span><span class="sxs-lookup"><span data-stu-id="0272f-552">Enable encryption on existing or running IaaS Windows VM in Azure</span></span>
<span data-ttu-id="0272f-553">В этом сценарии можно включить шифрование с помощью шаблона диспетчера ресурсов hello, командлеты PowerShell или команды CLI.</span><span class="sxs-lookup"><span data-stu-id="0272f-553">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="0272f-554">Hello ниже описаны более подробно как tooenable его с помощью hello шаблона диспетчера ресурсов и команд CLI.</span><span class="sxs-lookup"><span data-stu-id="0272f-554">hello following sections explain in greater detail how tooenable it by using hello Resource Manager template and CLI commands.</span></span>

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="0272f-555">С помощью шаблона диспетчера ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="0272f-555">Using hello Resource Manager template</span></span>
<span data-ttu-id="0272f-556">Можно включить шифрование диска на существующие или виртуальным машинам IaaS Windows в Azure с помощью hello [шаблона диспетчера ресурсов](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="0272f-556">You can enable disk encryption on existing or running IaaS Windows VMs in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="0272f-557">Hello Azure краткое шаблон, нажмите кнопку **развертывание tooAzure**, введите конфигурацию шифрования hello на hello **параметры** и, при необходимости нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0272f-557">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="0272f-558">Выберите подписку hello, группы ресурсов, расположение группы ресурсов, условия и соглашения и нажмите кнопку **создать** tooenable шифрование на hello существующий или под управлением ВМ IaaS.</span><span class="sxs-lookup"><span data-stu-id="0272f-558">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="0272f-559">Hello следующей таблице перечислены параметры шаблона диспетчера ресурсов hello для существующих или работающих виртуальных машин, использующих идентификатор клиента Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0272f-559">hello following table lists hello Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="0272f-560">Параметр</span><span class="sxs-lookup"><span data-stu-id="0272f-560">Parameter</span></span> | <span data-ttu-id="0272f-561">Описание</span><span class="sxs-lookup"><span data-stu-id="0272f-561">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0272f-562">AADClientID</span><span class="sxs-lookup"><span data-stu-id="0272f-562">AADClientID</span></span> | <span data-ttu-id="0272f-563">Идентификатор клиента приложения hello Azure AD с хранилище ключей toohello секреты toowrite разрешения.</span><span class="sxs-lookup"><span data-stu-id="0272f-563">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="0272f-564">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="0272f-564">AADClientSecret</span></span> | <span data-ttu-id="0272f-565">Секрет клиента приложения Azure AD hello хранилища ключей toohello секреты toowrite разрешения.</span><span class="sxs-lookup"><span data-stu-id="0272f-565">Client secret of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="0272f-566">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="0272f-566">keyVaultName</span></span> | <span data-ttu-id="0272f-567">Имя ключа hello хранилища, должна быть передана ключ BitLocker hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-567">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="0272f-568">Его можно получить с помощью командлета hello `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="0272f-568">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="0272f-569">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="0272f-569">keyEncryptionKeyURL</span></span> | <span data-ttu-id="0272f-570">URL-адрес ключа шифрования ключа hello, используемые tooencrypt hello созданный ключ BitLocker.</span><span class="sxs-lookup"><span data-stu-id="0272f-570">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="0272f-571">Этот параметр является необязательным, если выбрать **nokek** hello UseExistingKek раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="0272f-571">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="0272f-572">При выборе **kek** hello UseExistingKek раскрывающегося списка, необходимо ввести hello _keyEncryptionKeyURL_ значение.</span><span class="sxs-lookup"><span data-stu-id="0272f-572">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="0272f-573">volumeType</span><span class="sxs-lookup"><span data-stu-id="0272f-573">volumeType</span></span> | <span data-ttu-id="0272f-574">Тип тома, для которого выполняется операция шифрования hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-574">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="0272f-575">Допустимые значения: _OS_, _Data_ и _All_.</span><span class="sxs-lookup"><span data-stu-id="0272f-575">Valid values are _OS_, _Data_, and _All_.</span></span> |
| <span data-ttu-id="0272f-576">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="0272f-576">sequenceVersion</span></span> | <span data-ttu-id="0272f-577">Версия последовательности hello операции BitLocker.</span><span class="sxs-lookup"><span data-stu-id="0272f-577">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="0272f-578">Этот номер версии увеличивается, каждый раз, шифрование диска операции на hello одной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0272f-578">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="0272f-579">vmName</span><span class="sxs-lookup"><span data-stu-id="0272f-579">vmName</span></span> | <span data-ttu-id="0272f-580">Hello виртуальной Машины, операция шифрования hello называется toobe блокировкой.</span><span class="sxs-lookup"><span data-stu-id="0272f-580">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="0272f-581">_KeyEncryptionKeyURL_ является необязательным параметром.</span><span class="sxs-lookup"><span data-stu-id="0272f-581">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="0272f-582">Вы можете воплощать свои собственные KEK toofurther защиты hello ключ шифрования данных (секрета шифрования BitLocker) в хранилище ключей hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-582">You can bring your own KEK toofurther safeguard hello data encryption key (BitLocker encryption secret) in hello key vault.</span></span>

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="0272f-583">Использование командлетов PowerShell</span><span class="sxs-lookup"><span data-stu-id="0272f-583">Using PowerShell cmdlets</span></span>
<span data-ttu-id="0272f-584">Сведения о включении шифрования с помощью шифрования диска Azure с помощью командлетов PowerShell см. в блогах hello [исследовать шифрование диска Azure с использованием Azure PowerShell, часть 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) и [исследовать шифрование диска Azure с помощью Azure PowerShell — часть 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="0272f-584">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

#### <a name="using-cli-commands"></a><span data-ttu-id="0272f-585">Использование команд интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="0272f-585">Using CLI commands</span></span>
<span data-ttu-id="0272f-586">шифрование tooenable на существующие или ВМ IaaS Windows в Azure с помощью команды CLI hello следующие:</span><span class="sxs-lookup"><span data-stu-id="0272f-586">tooenable encryption on existing or running IaaS Windows VM in Azure using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="0272f-587">tooset политики доступа в хранилище ключей hello:</span><span class="sxs-lookup"><span data-stu-id="0272f-587">tooset access policies in hello key vault:</span></span>
   * <span data-ttu-id="0272f-588">Набор hello **EnabledForDiskEncryption** флаг:</span><span class="sxs-lookup"><span data-stu-id="0272f-588">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="0272f-589">Набор разрешений tooAzure AD приложения toowrite секреты tooyour хранилища ключей:</span><span class="sxs-lookup"><span data-stu-id="0272f-589">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. <span data-ttu-id="0272f-590">шифрование tooenable на Виртуальной машине существующий или не запущены:</span><span class="sxs-lookup"><span data-stu-id="0272f-590">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. <span data-ttu-id="0272f-591">состояние шифрования tooget:</span><span class="sxs-lookup"><span data-stu-id="0272f-591">tooget encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. <span data-ttu-id="0272f-592">шифрование tooenable на новой виртуальной Машины с зашифрованного диска, hello используйте следующие параметры с hello `azure vm create` команды:</span><span class="sxs-lookup"><span data-stu-id="0272f-592">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a><span data-ttu-id="0272f-593">Включение шифрования на виртуальной машине IaaS под управлением Linux, которая уже существует или работает в Azure</span><span class="sxs-lookup"><span data-stu-id="0272f-593">Enable encryption on an existing or running IaaS Linux VM in Azure</span></span>
<span data-ttu-id="0272f-594">Можно включить шифрование диска на виртуальной Машине Linux IaaS существующих или работает в Azure с помощью hello [шаблона диспетчера ресурсов](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="0272f-594">You can enable disk encryption on an existing or running IaaS Linux VM in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span></span>

1. <span data-ttu-id="0272f-595">Нажмите кнопку **развертывание tooAzure** на шаблоне hello Azure краткое введите конфигурацию шифрования hello на hello **параметры** и, при необходимости нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0272f-595">Click **Deploy tooAzure** on hello Azure quick-start template, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="0272f-596">Выберите подписку hello, группы ресурсов, расположение группы ресурсов, условия и соглашения и нажмите кнопку **создать** tooenable шифрование на hello существующий или под управлением ВМ IaaS.</span><span class="sxs-lookup"><span data-stu-id="0272f-596">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="0272f-597">Привет, в следующей таблице перечислены параметры шаблона диспетчера ресурсов для существующих или работающих виртуальных машин, использующих идентификатор клиента Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0272f-597">hello following table lists Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="0272f-598">Параметр</span><span class="sxs-lookup"><span data-stu-id="0272f-598">Parameter</span></span> | <span data-ttu-id="0272f-599">Описание</span><span class="sxs-lookup"><span data-stu-id="0272f-599">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0272f-600">AADClientID</span><span class="sxs-lookup"><span data-stu-id="0272f-600">AADClientID</span></span> | <span data-ttu-id="0272f-601">Идентификатор клиента приложения hello Azure AD с хранилище ключей toohello секреты toowrite разрешения.</span><span class="sxs-lookup"><span data-stu-id="0272f-601">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="0272f-602">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="0272f-602">AADClientSecret</span></span> | <span data-ttu-id="0272f-603">Секрет клиента приложения Azure AD hello хранилища ключей tooyour секреты toowrite разрешения.</span><span class="sxs-lookup"><span data-stu-id="0272f-603">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="0272f-604">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="0272f-604">keyVaultName</span></span> | <span data-ttu-id="0272f-605">Имя ключа hello хранилища, должна быть передана ключ BitLocker hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-605">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="0272f-606">Его можно получить с помощью командлета hello `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="0272f-606">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="0272f-607">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="0272f-607">keyEncryptionKeyURL</span></span> | <span data-ttu-id="0272f-608">URL-адрес ключа шифрования ключа hello, используемые tooencrypt hello созданный ключ BitLocker.</span><span class="sxs-lookup"><span data-stu-id="0272f-608">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="0272f-609">Этот параметр является необязательным, если выбрать **nokek** hello UseExistingKek раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="0272f-609">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="0272f-610">При выборе **kek** hello UseExistingKek раскрывающегося списка, необходимо ввести hello _keyEncryptionKeyURL_ значение.</span><span class="sxs-lookup"><span data-stu-id="0272f-610">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="0272f-611">volumeType</span><span class="sxs-lookup"><span data-stu-id="0272f-611">volumeType</span></span> | <span data-ttu-id="0272f-612">Тип тома, для которого выполняется операция шифрования hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-612">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="0272f-613">Поддерживаемые допустимые значения: _OS_ или _All_ (для RHEL 7.2, CentOS 7.2 и Ubuntu 16.04) и _Data_ (для всех остальных дистрибутивов).</span><span class="sxs-lookup"><span data-stu-id="0272f-613">Valid supported values are _OS_ or _All_ (for RHEL 7.2, CentOS 7.2, and Ubuntu 16.04), and _Data_ (for all other distributions).</span></span> |
| <span data-ttu-id="0272f-614">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="0272f-614">sequenceVersion</span></span> | <span data-ttu-id="0272f-615">Версия последовательности hello операции BitLocker.</span><span class="sxs-lookup"><span data-stu-id="0272f-615">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="0272f-616">Этот номер версии увеличивается, каждый раз, шифрование диска операции на hello одной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0272f-616">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="0272f-617">vmName</span><span class="sxs-lookup"><span data-stu-id="0272f-617">vmName</span></span> | <span data-ttu-id="0272f-618">Hello виртуальной Машины, операция шифрования hello называется toobe блокировкой.</span><span class="sxs-lookup"><span data-stu-id="0272f-618">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |
| <span data-ttu-id="0272f-619">passPhrase</span><span class="sxs-lookup"><span data-stu-id="0272f-619">passPhrase</span></span> | <span data-ttu-id="0272f-620">Введите ключ шифрования данных hello надежную парольную фразу.</span><span class="sxs-lookup"><span data-stu-id="0272f-620">Type a strong passphrase as hello data encryption key.</span></span> |

> [!NOTE]
> <span data-ttu-id="0272f-621">_KeyEncryptionKeyURL_ является необязательным параметром.</span><span class="sxs-lookup"><span data-stu-id="0272f-621">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="0272f-622">Собственные KEK toofurther защиты hello ключ шифрования данных (секрет парольную фразу) можно импортировать в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="0272f-622">You can bring your own KEK toofurther safeguard hello data encryption key (passphrase secret) in your key vault.</span></span>

#### <a name="cli-commands"></a><span data-ttu-id="0272f-623">Команды интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="0272f-623">CLI commands</span></span>
<span data-ttu-id="0272f-624">Можно включить шифрование диска на зашифрованные им при установке и использовании hello [команду CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="0272f-624">You can enable disk encryption on your encrypted VHD by installing and using hello [CLI command](../cli-install-nodejs.md).</span></span> <span data-ttu-id="0272f-625">шифрование tooenable на существующие или виртуальным машинам IaaS Linux в Azure с помощью команд CLI hello следующие:</span><span class="sxs-lookup"><span data-stu-id="0272f-625">tooenable encryption on existing or running IaaS Linux VMs in Azure by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="0272f-626">Задать политику доступа в хранилище ключей hello:</span><span class="sxs-lookup"><span data-stu-id="0272f-626">Set access policies in hello key vault:</span></span>

 * <span data-ttu-id="0272f-627">Набор hello **EnabledForDiskEncryption** флаг:</span><span class="sxs-lookup"><span data-stu-id="0272f-627">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * <span data-ttu-id="0272f-628">Набор разрешений tooAzure AD приложения toowrite секреты tooyour хранилища ключей:</span><span class="sxs-lookup"><span data-stu-id="0272f-628">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="0272f-629">шифрование tooenable на Виртуальной машине существующий или не запущены:</span><span class="sxs-lookup"><span data-stu-id="0272f-629">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="0272f-630">Получите состояние шифрования, введя следующую команду.</span><span class="sxs-lookup"><span data-stu-id="0272f-630">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="0272f-631">шифрование tooenable на новой виртуальной Машины с зашифрованного диска, hello используйте следующие параметры с hello `azure vm create` команды:</span><span class="sxs-lookup"><span data-stu-id="0272f-631">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a><span data-ttu-id="0272f-632">Получить состояние шифрования зашифрованных ВМ IaaS hello</span><span class="sxs-lookup"><span data-stu-id="0272f-632">Get hello encryption status of an encrypted IaaS VM</span></span>
<span data-ttu-id="0272f-633">Состояние шифрования hello можно получить с помощью диспетчера ресурсов Azure, [командлеты PowerShell](/powershell/azure/overview), или команды CLI.</span><span class="sxs-lookup"><span data-stu-id="0272f-633">You can get hello encryption status by using Azure Resource Manager, [PowerShell cmdlets](/powershell/azure/overview), or CLI commands.</span></span> <span data-ttu-id="0272f-634">Hello в следующих разделах объясняется, как toouse hello классический портал Azure и tooget команд CLI hello состояние шифрования.</span><span class="sxs-lookup"><span data-stu-id="0272f-634">hello following sections explain how toouse hello Azure classic portal and CLI commands tooget hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a><span data-ttu-id="0272f-635">Получить состояние шифрования hello зашифрованные виртуальной машины Windows с помощью диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="0272f-635">Get hello encryption status of an encrypted Windows VM by using Azure Resource Manager</span></span>
<span data-ttu-id="0272f-636">Состояние шифрования hello hello ВМ IaaS из диспетчера ресурсов Azure можно получить, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="0272f-636">You can get hello encryption status of hello IaaS VM from Azure Resource Manager by doing hello following:</span></span>

1. <span data-ttu-id="0272f-637">Вход toohello [классический портал Azure](https://portal.azure.com/), а затем нажмите кнопку **виртуальные машины** в левой области hello toosee сводное представление hello виртуальных машин в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="0272f-637">Sign in toohello [Azure classic portal](https://portal.azure.com/), and then click **Virtual machines** in hello left pane toosee a summary view of hello virtual machines in your subscription.</span></span> <span data-ttu-id="0272f-638">Вы можете фильтровать представление виртуальных машин hello, выбрав имя подписки hello в hello **подписки** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="0272f-638">You can filter hello virtual machines view by selecting hello subscription name in hello **Subscription** drop-down list.</span></span>

2. <span data-ttu-id="0272f-639">Вверху hello hello **виртуальные машины** щелкните **столбцы**.</span><span class="sxs-lookup"><span data-stu-id="0272f-639">At hello top of hello **Virtual machines** page, click **Columns**.</span></span>

3. <span data-ttu-id="0272f-640">На hello **Выбор столбца** колонке выберите **шифрование диска**и нажмите кнопку **обновление**.</span><span class="sxs-lookup"><span data-stu-id="0272f-640">On hello **Choose column** blade, select **Disk Encryption**, and then click **Update**.</span></span> <span data-ttu-id="0272f-641">Вы увидите состояние шифрования для столбца отображение hello шифрование диска hello _включено_ или _не включена_ для каждой виртуальной Машины, как показано в следующий рисунок hello:</span><span class="sxs-lookup"><span data-stu-id="0272f-641">You should see hello disk-encryption column showing hello encryption state _Enabled_ or _Not Enabled_ for each VM, as shown in hello following figure:</span></span>

 ![Антивредоносное ПО Майкрософт в Azure](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a><span data-ttu-id="0272f-643">Состояние шифрования hello зашифрованные ВМ IaaS (Windows или Linux) можно получить с помощью командлета PowerShell hello шифрование диска</span><span class="sxs-lookup"><span data-stu-id="0272f-643">Get hello encryption status of an encrypted (Windows/Linux) IaaS VM by using hello disk-encryption PowerShell cmdlet</span></span>
<span data-ttu-id="0272f-644">Состояние шифрования hello hello ВМ IaaS можно получить из командлета PowerShell шифрование диска hello `Get-AzureRmVMDiskEncryptionStatus`.</span><span class="sxs-lookup"><span data-stu-id="0272f-644">You can get hello encryption status of hello IaaS VM from hello disk-encryption PowerShell cmdlet `Get-AzureRmVMDiskEncryptionStatus`.</span></span> <span data-ttu-id="0272f-645">параметры шифрования hello tooget для виртуальной Машины, введите hello следующие данные:</span><span class="sxs-lookup"><span data-stu-id="0272f-645">tooget hello encryption settings for your VM, enter hello following:</span></span>

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

<span data-ttu-id="0272f-646">Можно просмотреть выходные данные hello _Get AzureRmVMDiskEncryptionStatus_ для шифрования ключа URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="0272f-646">You can inspect hello output of _Get-AzureRmVMDiskEncryptionStatus_ for encryption key URLs.</span></span>

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

<span data-ttu-id="0272f-647">Hello OSVolumeEncrypted и значения параметров DataVolumesEncrypted задаются too_Encrypted_, показывающий, что обоих томов, шифруются с помощью шифрования диска Azure.</span><span class="sxs-lookup"><span data-stu-id="0272f-647">hello OSVolumeEncrypted and DataVolumesEncrypted settings values are set too_Encrypted_, which shows that both volumes are encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="0272f-648">Сведения о включении шифрования с помощью шифрования диска Azure с помощью командлетов PowerShell см. в блогах hello [исследовать шифрование диска Azure с использованием Azure PowerShell, часть 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) и [исследовать шифрование диска Azure с помощью Azure PowerShell — часть 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="0272f-648">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="0272f-649">На виртуальных машинах Linux, он принимает три минуты toofour для hello `Get-AzureRmVMDiskEncryptionStatus` состояние шифрования hello tooreport командлета.</span><span class="sxs-lookup"><span data-stu-id="0272f-649">On Linux VMs, it takes three toofour minutes for hello `Get-AzureRmVMDiskEncryptionStatus` cmdlet tooreport hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a><span data-ttu-id="0272f-650">Получить состояние шифрования hello hello ВМ IaaS из команду CLI hello шифрование диска</span><span class="sxs-lookup"><span data-stu-id="0272f-650">Get hello encryption status of hello IaaS VM from hello disk-encryption CLI command</span></span>
<span data-ttu-id="0272f-651">Состояние шифрования hello hello ВМ IaaS можно получить с помощью команды CLI шифрование диска hello `azure vm show-disk-encryption-status`.</span><span class="sxs-lookup"><span data-stu-id="0272f-651">You can get hello encryption status of hello IaaS VM by using hello disk-encryption CLI command `azure vm show-disk-encryption-status`.</span></span> <span data-ttu-id="0272f-652">параметры шифрования hello tooget для виртуальной Машины, введите ваш сеанс Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="0272f-652">tooget hello encryption settings for your VM, enter your Azure CLI session:</span></span>

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a><span data-ttu-id="0272f-653">Отключение шифрования на работающей виртуальной машине IaaS под управлением Windows</span><span class="sxs-lookup"><span data-stu-id="0272f-653">Disable encryption on running Windows IaaS VM</span></span>
<span data-ttu-id="0272f-654">Можно отключить шифрование на запуск Windows или Linux ВМ IaaS через hello шаблона диспетчера ресурсов шифрования диска Azure или командлеты PowerShell и указать конфигурацию расшифровки hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-654">You can disable encryption on a running Windows or Linux IaaS VM via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets and specify hello decryption configuration.</span></span>

##### <a name="windows-vm"></a><span data-ttu-id="0272f-655">Виртуальная машина Windows</span><span class="sxs-lookup"><span data-stu-id="0272f-655">Windows VM</span></span>
<span data-ttu-id="0272f-656">Hello отключение шифрования шаг отключает шифрование hello ОС hello объем данных, и на выполнение ВМ IaaS Windows hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-656">hello disable-encryption step disables encryption of hello OS, hello data volume, or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="0272f-657">Невозможно отключить hello тома операционной системы и оставьте шифрованием hello данных тома.</span><span class="sxs-lookup"><span data-stu-id="0272f-657">You cannot disable hello OS volume and leave hello data volume encrypted.</span></span> <span data-ttu-id="0272f-658">При выполнении шага hello disable шифрования hello Azure классической модели развертывания обновляет hello модели службы ВМ и ВМ IaaS Windows hello помечен расшифрованные.</span><span class="sxs-lookup"><span data-stu-id="0272f-658">When hello disable-encryption step is performed, hello Azure classic deployment model updates hello VM service model, and hello Windows IaaS VM is marked decrypted.</span></span> <span data-ttu-id="0272f-659">содержимое Hello hello ВМ больше не шифруются при хранении.</span><span class="sxs-lookup"><span data-stu-id="0272f-659">hello contents of hello VM are no longer encrypted at rest.</span></span> <span data-ttu-id="0272f-660">Расшифровка Hello не удаляет вашего ключа хранилища и hello основы ключа шифрования (ключи шифрования BitLocker для Windows и парольную фразу для Linux).</span><span class="sxs-lookup"><span data-stu-id="0272f-660">hello decryption does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows and Passphrase for Linux).</span></span>

##### <a name="linux-vm"></a><span data-ttu-id="0272f-661">Виртуальная машина Linux</span><span class="sxs-lookup"><span data-stu-id="0272f-661">Linux VM</span></span>
<span data-ttu-id="0272f-662">Hello отключение шифрования шаг отключает шифрование тома данных hello hello под управлением Linux ВМ IaaS.</span><span class="sxs-lookup"><span data-stu-id="0272f-662">hello disable-encryption step disables encryption of hello data volume on hello running Linux IaaS VM.</span></span> <span data-ttu-id="0272f-663">Этот шаг работает только в том случае, если диск ОС hello не шифруются.</span><span class="sxs-lookup"><span data-stu-id="0272f-663">This step only works if hello OS disk is not encrypted.</span></span>

> [!NOTE]
> <span data-ttu-id="0272f-664">Отключение шифрования на диске ОС hello не допускается на виртуальных машинах Linux.</span><span class="sxs-lookup"><span data-stu-id="0272f-664">Disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span>

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="0272f-665">Отключение шифрования на существующей или запущенной виртуальной машине IaaS</span><span class="sxs-lookup"><span data-stu-id="0272f-665">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="0272f-666">Можно отключить шифрование диска на работающих виртуальных машин IaaS Windows с помощью hello [шаблона диспетчера ресурсов](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="0272f-666">You can disable disk encryption on running Windows IaaS VMs by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="0272f-667">Hello Azure краткое шаблон, нажмите кнопку **развертывание tooAzure**, введите hello расшифровки конфигурации на hello **параметры** и, при необходимости нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0272f-667">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello decryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="0272f-668">Выберите подписку hello, группы ресурсов, расположение группы ресурсов, условия и соглашения и нажмите кнопку **создать** tooenable шифрование на новую виртуальную Машину IaaS.</span><span class="sxs-lookup"><span data-stu-id="0272f-668">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

<span data-ttu-id="0272f-669">Для виртуальных машин Linux, можно отключить шифрование с помощью hello [отключить шифрование на работающей ВМ Linux](https://aka.ms/decrypt-linuxvm) шаблона.</span><span class="sxs-lookup"><span data-stu-id="0272f-669">For Linux VMs, you can disable encryption by using hello [Disable encryption on a running Linux VM](https://aka.ms/decrypt-linuxvm) template.</span></span>

<span data-ttu-id="0272f-670">Hello следующей таблице перечислены параметры шаблона диспетчера ресурсов для отключения шифрования на работающей ВМ IaaS.</span><span class="sxs-lookup"><span data-stu-id="0272f-670">hello following table lists Resource Manager template parameters for disabling encryption on a running IaaS VM:</span></span>

| <span data-ttu-id="0272f-671">Параметр</span><span class="sxs-lookup"><span data-stu-id="0272f-671">Parameter</span></span> | <span data-ttu-id="0272f-672">Описание</span><span class="sxs-lookup"><span data-stu-id="0272f-672">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0272f-673">vmName</span><span class="sxs-lookup"><span data-stu-id="0272f-673">vmName</span></span> | <span data-ttu-id="0272f-674">Hello виртуальной Машины, операция шифрования hello называется toobe блокировкой.</span><span class="sxs-lookup"><span data-stu-id="0272f-674">Name of hello VM that hello encryption operation is toobe performed on.</span></span>
| <span data-ttu-id="0272f-675">volumeType</span><span class="sxs-lookup"><span data-stu-id="0272f-675">volumeType</span></span> | <span data-ttu-id="0272f-676">Тип тома, для которого будет выполняться расшифровка.</span><span class="sxs-lookup"><span data-stu-id="0272f-676">Type of volume that a decryption operation is performed on.</span></span> <span data-ttu-id="0272f-677">Допустимые значения: _OS_, _Data_ и _All_.</span><span class="sxs-lookup"><span data-stu-id="0272f-677">Valid values are _OS_, _Data_, and _All_.</span></span> <span data-ttu-id="0272f-678">Невозможно отключить шифрование на под управлением ОС ВМ IaaS Windows или загрузочного тома без отключения шифрования hello _данные_ тома.</span><span class="sxs-lookup"><span data-stu-id="0272f-678">You cannot disable encryption on running Windows IaaS VM OS/boot volume without disabling encryption on hello _Data_ volume.</span></span> <span data-ttu-id="0272f-679">Также Обратите внимание, что отключение шифрования на диске ОС hello не разрешен на виртуальных машинах Linux.</span><span class="sxs-lookup"><span data-stu-id="0272f-679">Also note that disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span> |
| <span data-ttu-id="0272f-680">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="0272f-680">sequenceVersion</span></span> | <span data-ttu-id="0272f-681">Версия последовательности hello операции BitLocker.</span><span class="sxs-lookup"><span data-stu-id="0272f-681">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="0272f-682">Этот номер версии увеличивается, каждый раз операции расшифровки диска выполняется на hello одной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0272f-682">Increment this version number every time a disk decryption operation is performed on hello same VM.</span></span> |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="0272f-683">Отключение шифрования на существующей или запущенной виртуальной машине IaaS</span><span class="sxs-lookup"><span data-stu-id="0272f-683">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="0272f-684">toodisable шифрования на виртуальной Машине IaaS существующих или не запущены с помощью командлета PowerShell hello, в разделе [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span><span class="sxs-lookup"><span data-stu-id="0272f-684">toodisable encryption on an existing or running IaaS VM by using hello PowerShell cmdlet, see [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span></span> <span data-ttu-id="0272f-685">Этот командлет поддерживает виртуальные машины Linux и Windows.</span><span class="sxs-lookup"><span data-stu-id="0272f-685">This cmdlet supports both Windows and Linux VMs.</span></span> <span data-ttu-id="0272f-686">шифрование toodisable устанавливаются расширения на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-686">toodisable encryption, it installs an extension on hello virtual machine.</span></span> <span data-ttu-id="0272f-687">Если hello _имя_ параметр не указан, расширения с именем по умолчанию hello _AzureDiskEncryption ВМ_ создается.</span><span class="sxs-lookup"><span data-stu-id="0272f-687">If hello _Name_ parameter is not specified, an extension with hello default name _AzureDiskEncryption for Windows VMs_ is created.</span></span>

<span data-ttu-id="0272f-688">На виртуальных машинах Linux используется hello AzureDiskEncryptionForLinux расширения.</span><span class="sxs-lookup"><span data-stu-id="0272f-688">On Linux VMs, hello AzureDiskEncryptionForLinux extension is used.</span></span>

> [!NOTE]
> <span data-ttu-id="0272f-689">Этот командлет перезагружает hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0272f-689">This cmdlet reboots hello virtual machine.</span></span>

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="0272f-690">Включение шифрования для предварительно зашифрованной виртуальной машины IaaS с управляемым диском Azure</span><span class="sxs-lookup"><span data-stu-id="0272f-690">Enable encryption on pre-encrypted IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="0272f-691">Используйте hello ARM диска управляемых Azure шаблона toocreate зашифрованные виртуальной Машины на основе предварительно зашифрованный VHD с помощью шаблона hello ARM, расположенный в</span><span class="sxs-lookup"><span data-stu-id="0272f-691">Use hello Azure Managed Disk ARM template toocreate a encrypted VM from a pre-encrypted VHD using hello ARM template located at</span></span>   
<span data-ttu-id="0272f-692">[Создание зашифрованного управляемого диска на основе предварительно зашифрованного виртуального жесткого диска или BLOB-объекта] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span><span class="sxs-lookup"><span data-stu-id="0272f-692">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span></span>

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="0272f-693">Включение шифрования для новой виртуальной машины IaaS с ОС Linux и управляемым диском Azure</span><span class="sxs-lookup"><span data-stu-id="0272f-693">Enable encryption on a new Linux IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="0272f-694">Используйте hello ARM диска управляемых Azure шаблона toocreate новое зашифрованное ВМ IaaS Linux с помощью шаблона hello ARM, расположенный в</span><span class="sxs-lookup"><span data-stu-id="0272f-694">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
<span data-ttu-id="0272f-695">[Развертывание RHEL 7.2 с полным шифрованием дисков] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span><span class="sxs-lookup"><span data-stu-id="0272f-695">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span></span>

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="0272f-696">Включение шифрования для новой виртуальной машины IaaS с ОС Windows и управляемым диском Azure</span><span class="sxs-lookup"><span data-stu-id="0272f-696">Enable encryption on a new Windows IaaS VM with Azure Managed Disk</span></span>
 <span data-ttu-id="0272f-697">Используйте hello ARM диска управляемых Azure шаблона toocreate новое зашифрованное ВМ IaaS Linux с помощью шаблона hello ARM, расположенный в</span><span class="sxs-lookup"><span data-stu-id="0272f-697">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
 <span data-ttu-id="0272f-698">[Создание зашифрованной виртуальной машины IaaS с ОС Windows и управляемым диском на основе образа из коллекции] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span><span class="sxs-lookup"><span data-stu-id="0272f-698">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span></span>

  > [!NOTE]
  ><span data-ttu-id="0272f-699">Это обязательный toosnapshot и/или резервного копирования управляемого диска на основе экземпляра виртуальной Машины за пределами и предыдущих tooenabling шифрование диска Azure.</span><span class="sxs-lookup"><span data-stu-id="0272f-699">It is mandatory toosnapshot and/or backup a managed disk based VM instance outside of and prior tooenabling Azure Disk Encryption.</span></span>  <span data-ttu-id="0272f-700">Моментальный снимок hello управляемого диска могут браться из портала hello или Azure Backup может использоваться.</span><span class="sxs-lookup"><span data-stu-id="0272f-700">A snapshot of hello managed disk can be taken from hello portal, or Azure Backup can be used.</span></span>  <span data-ttu-id="0272f-701">Резервные копии убедитесь, что параметр восстановления возможно в случае, когда hello любой непредвиденный сбой во время шифрования.</span><span class="sxs-lookup"><span data-stu-id="0272f-701">Backups ensure that a recovery option is possible in hello case of any unexpected failure during encryption.</span></span>  <span data-ttu-id="0272f-702">После выполнения резервной копии командлет hello AzureRmVMDiskEncryptionExtension набор может быть дисков используется tooencrypt управляемых с помощью параметра - skipVmBackup hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-702">Once a backup is made, hello Set-AzureRmVMDiskEncryptionExtension cmdlet can be used tooencrypt managed disks by specifying hello -skipVmBackup parameter.</span></span>  <span data-ttu-id="0272f-703">Эта команда будет завершаться ошибкой при использовании с виртуальными машинами на основе управляемых дисков, пока не будет сделана резервная копия и указан определенный параметр.</span><span class="sxs-lookup"><span data-stu-id="0272f-703">This command will fail against managed disk based VM's until a backup has been made and this parameter has been specified.</span></span>    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a><span data-ttu-id="0272f-704">Изменение параметров шифрования существующей зашифрованной виртуальной машины не класса "Премиум"</span><span class="sxs-lookup"><span data-stu-id="0272f-704">Update encryption settings of an existing encrypted non-premium VM</span></span>
  <span data-ttu-id="0272f-705">Используйте hello существующие диск Azure поддерживает шифрование интерфейсы для запуска виртуальной Машины [командлеты PS, CLI или ARM шаблонов] tooupdate hello параметры шифрования, например клиента AAD ID и секретный ключ шифрования ключа [KEK], ключ шифрования BitLocker для виртуальной Машины Windows или парольную фразу для Виртуальная машина Linux т. д. hello обновления шифрования параметр поддерживается только для виртуальных машин, поддерживаемый хранения Premium-класса.</span><span class="sxs-lookup"><span data-stu-id="0272f-705">Use hello existing Azure disk encryption supported interfaces for running VM [PS cmdlets, CLI or ARM templates] tooupdate hello encryption settings like AAD client ID/secret, Key encryption key [KEK], BitLocker encryption key for Windows VM or Passphrase for Linux VM etc. hello update encryption setting is supported only for VMs backed by non-premium storage.</span></span> <span data-ttu-id="0272f-706">Оно не поддерживается для виртуальных машин на основе хранилища класса "Премиум".</span><span class="sxs-lookup"><span data-stu-id="0272f-706">It is NNOT supported for VMs backed by premium storage.</span></span>

## <a name="appendix"></a><span data-ttu-id="0272f-707">Приложение</span><span class="sxs-lookup"><span data-stu-id="0272f-707">Appendix</span></span>
### <a name="connect-tooyour-subscription"></a><span data-ttu-id="0272f-708">Подключение tooyour подписки</span><span class="sxs-lookup"><span data-stu-id="0272f-708">Connect tooyour subscription</span></span>
<span data-ttu-id="0272f-709">Прежде чем продолжить, просмотрите hello *необходимые компоненты* этой статьи.</span><span class="sxs-lookup"><span data-stu-id="0272f-709">Before you proceed, review hello *Prerequisites* section in this article.</span></span> <span data-ttu-id="0272f-710">Убедившись, что выполнены все необходимые компоненты, подключите tooyour подписки, выполнив следующие hello:</span><span class="sxs-lookup"><span data-stu-id="0272f-710">After you ensure that all prerequisites have been met, connect tooyour subscription by doing hello following:</span></span>

1. <span data-ttu-id="0272f-711">Запустите сеанс Azure PowerShell и войдите в учетную запись Azure tooyour с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0272f-711">Start an Azure PowerShell session, and sign in tooyour Azure account with hello following command:</span></span>

    `Login-AzureRmAccount`

2. <span data-ttu-id="0272f-712">Если есть несколько подписок и требуется один toouse toospecify, введите hello, следуя toosee hello подписки для учетной записи:</span><span class="sxs-lookup"><span data-stu-id="0272f-712">If you have multiple subscriptions and want toospecify one toouse, type hello following toosee hello subscriptions for your account:</span></span>

    `Get-AzureRmSubscription`

3. <span data-ttu-id="0272f-713">toospecify hello подписку toouse, тип:</span><span class="sxs-lookup"><span data-stu-id="0272f-713">toospecify hello subscription you want toouse, type:</span></span>

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. <span data-ttu-id="0272f-714">правильность настройки подписки hello tooverify, введите:</span><span class="sxs-lookup"><span data-stu-id="0272f-714">tooverify that hello subscription configured is correct, type:</span></span>

    `Get-AzureRmSubscription`

5. <span data-ttu-id="0272f-715">hello tooconfirm установлены командлеты, шифрование диска Azure типа:</span><span class="sxs-lookup"><span data-stu-id="0272f-715">tooconfirm hello Azure Disk Encryption cmdlets are installed, type:</span></span>

    `Get-command *diskencryption*`

6. <span data-ttu-id="0272f-716">После вывода Hello подтверждает hello Azure PowerShell шифрования диска установки:</span><span class="sxs-lookup"><span data-stu-id="0272f-716">hello following output confirms hello Azure Disk Encryption PowerShell installation:</span></span>

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a><span data-ttu-id="0272f-717">Подготовка предварительно зашифрованного виртуального жесткого диска Windows</span><span class="sxs-lookup"><span data-stu-id="0272f-717">Prepare a pre-encrypted Windows VHD</span></span>
<span data-ttu-id="0272f-718">Hello разделах являются необходимые tooprepare предварительно зашифрованный виртуального жесткого диска Windows для развертывания в виде зашифрованного виртуального жесткого диска в Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="0272f-718">hello sections that follow are necessary tooprepare a pre-encrypted Windows VHD for deployment as an encrypted VHD in Azure IaaS.</span></span> <span data-ttu-id="0272f-719">Использовать сведения tooprepare hello и загрузите новую Windows виртуальной Машины (VHD) на Azure или Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0272f-719">Use hello information tooprepare and boot a fresh Windows VM (VHD) on Azure Site Recovery or Azure.</span></span>

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a><span data-ttu-id="0272f-720">Обновление групповой политики tooallow без НЕГО для защиты операционной системы</span><span class="sxs-lookup"><span data-stu-id="0272f-720">Update group policy tooallow non-TPM for OS protection</span></span>
<span data-ttu-id="0272f-721">Настройте параметр групповой политики BitLocker hello **шифрования диска BitLocker**, его можно найти в разделе **политика локального компьютера** > **Конфигурация компьютера**  >  **Административные шаблоны** > **компоненты Windows**.</span><span class="sxs-lookup"><span data-stu-id="0272f-721">Configure hello BitLocker Group Policy setting **BitLocker Drive Encryption**, which you'll find under **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **Windows Components**.</span></span> <span data-ttu-id="0272f-722">Изменить этот параметр слишком**диски операционной системы** > **требуется дополнительная проверка подлинности при запуске** > **разрешить использование BitLocker без совместимого TPM**, как показано в следующий рисунок hello:</span><span class="sxs-lookup"><span data-stu-id="0272f-722">Change this setting too**Operating System Drives** > **Require additional authentication at startup** > **Allow BitLocker without a compatible TPM**, as shown in hello following figure:</span></span>

![Антивредоносное ПО Майкрософт в Azure](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a><span data-ttu-id="0272f-724">Установка компонентов BitLocker</span><span class="sxs-lookup"><span data-stu-id="0272f-724">Install BitLocker feature components</span></span>
<span data-ttu-id="0272f-725">Windows Server 2012 и более поздних версий используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0272f-725">For Windows Server 2012 and later, use hello following command:</span></span>

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

<span data-ttu-id="0272f-726">Для Windows Server 2008 R2 используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0272f-726">For Windows Server 2008 R2, use hello following command:</span></span>

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a><span data-ttu-id="0272f-727">Подготовьте hello тома операционной системы с помощью BitLocker`bdehdcfg`</span><span class="sxs-lookup"><span data-stu-id="0272f-727">Prepare hello OS volume for BitLocker by using `bdehdcfg`</span></span>
<span data-ttu-id="0272f-728">toocompress hello раздела операционной системы и подготовка машины hello для BitLocker, выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-728">toocompress hello OS partition and prepare hello machine for BitLocker, execute hello following command:</span></span>

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a><span data-ttu-id="0272f-729">Защита hello тома операционной системы с помощью BitLocker</span><span class="sxs-lookup"><span data-stu-id="0272f-729">Protect hello OS volume by using BitLocker</span></span>
<span data-ttu-id="0272f-730">Используйте hello [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) шифрование tooenable команды на hello загрузочного тома с помощью внешнего средства защиты ключа.</span><span class="sxs-lookup"><span data-stu-id="0272f-730">Use hello [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) command tooenable encryption on hello boot volume using an external key protector.</span></span> <span data-ttu-id="0272f-731">Также можно поместите hello внешнего ключа (.bek-файл) на hello внешний диск или том.</span><span class="sxs-lookup"><span data-stu-id="0272f-731">Also place hello external key (.bek file) on hello external drive or volume.</span></span> <span data-ttu-id="0272f-732">После следующей перезагрузки hello включено шифрование для hello системный или загрузочный том.</span><span class="sxs-lookup"><span data-stu-id="0272f-732">Encryption is enabled on hello system/boot volume after hello next reboot.</span></span>

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> <span data-ttu-id="0272f-733">Подготовьте hello виртуальной Машины с отдельной или ресурса данных виртуального жесткого диска для получения hello внешнего ключа с помощью BitLocker.</span><span class="sxs-lookup"><span data-stu-id="0272f-733">Prepare hello VM with a separate data/resource VHD for getting hello external key by using BitLocker.</span></span>

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a><span data-ttu-id="0272f-734">Шифрование диска ОС на работающей виртуальной машине Linux</span><span class="sxs-lookup"><span data-stu-id="0272f-734">Encrypting an OS drive on a running Linux VM</span></span>
<span data-ttu-id="0272f-735">После распределения hello поддерживается шифрования диска операционной системы на работающей виртуальной Машины Linux:</span><span class="sxs-lookup"><span data-stu-id="0272f-735">Encryption of an OS drive on a running Linux VM is supported on hello following distributions:</span></span>

* <span data-ttu-id="0272f-736">RHEL 7.2;</span><span class="sxs-lookup"><span data-stu-id="0272f-736">RHEL 7.2</span></span>
* <span data-ttu-id="0272f-737">CentOS 7.2;</span><span class="sxs-lookup"><span data-stu-id="0272f-737">CentOS 7.2</span></span>
* <span data-ttu-id="0272f-738">Ubuntu 16.04.</span><span class="sxs-lookup"><span data-stu-id="0272f-738">Ubuntu 16.04</span></span>

##### <a name="prerequisites-for-os-disk-encryption"></a><span data-ttu-id="0272f-739">Предварительные требования для шифрования диска ОС</span><span class="sxs-lookup"><span data-stu-id="0272f-739">Prerequisites for OS disk encryption</span></span>

* <span data-ttu-id="0272f-740">Hello ВМ должны быть созданы из образа Marketplace hello в диспетчере ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="0272f-740">hello VM must be created from hello Marketplace image in Azure Resource Manager.</span></span>
* <span data-ttu-id="0272f-741">Виртуальная машина Azure по крайней мере с 4 ГБ ОЗУ (рекомендуемый размер — 7 ГБ).</span><span class="sxs-lookup"><span data-stu-id="0272f-741">Azure VM with at least 4 GB of RAM (recommended size is 7 GB).</span></span>
* <span data-ttu-id="0272f-742">(Для RHEL и CentOS.) Отключите SELinux.</span><span class="sxs-lookup"><span data-stu-id="0272f-742">(For RHEL and CentOS) Disable SELinux.</span></span> <span data-ttu-id="0272f-743">toodisable SELinux, в разделе «4.4.2.</span><span class="sxs-lookup"><span data-stu-id="0272f-743">toodisable SELinux, see "4.4.2.</span></span> <span data-ttu-id="0272f-744">Отключение SELinux» в hello [руководство администратора и пользователя SELinux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0272f-744">Disabling SELinux" in hello [SELinux User's and Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) on hello VM.</span></span>
* <span data-ttu-id="0272f-745">После отключения SELinux перезагрузите hello ВМ по крайней мере один раз.</span><span class="sxs-lookup"><span data-stu-id="0272f-745">After you disable SELinux, reboot hello VM at least once.</span></span>

##### <a name="steps"></a><span data-ttu-id="0272f-746">Действия</span><span class="sxs-lookup"><span data-stu-id="0272f-746">Steps</span></span>
1. <span data-ttu-id="0272f-747">Создайте виртуальную Машину с помощью одного из распределения hello, указанном ранее.</span><span class="sxs-lookup"><span data-stu-id="0272f-747">Create a VM by using one of hello distributions specified previously.</span></span>

 <span data-ttu-id="0272f-748">Для CentOS 7.2 шифрование диска операционной системы можно включить через специальный образ.</span><span class="sxs-lookup"><span data-stu-id="0272f-748">For CentOS 7.2, OS disk encryption is supported via a special image.</span></span> <span data-ttu-id="0272f-749">toouse это изображения, укажите «7.2n» как hello SKU при создании hello виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="0272f-749">toouse this image, specify "7.2n" as hello SKU when you create hello VM:</span></span>
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. <span data-ttu-id="0272f-750">Настройте соответствующим требованиям tooyour hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0272f-750">Configure hello VM according tooyour needs.</span></span> <span data-ttu-id="0272f-751">Если вы собираетесь tooencrypt все диски hello (ОС + данные), диски с данными hello должны toobe указанного и подключить из/etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="0272f-751">If you are going tooencrypt all hello (OS + data) drives, hello data drives need toobe specified and mountable from /etc/fstab.</span></span>

 > [!NOTE]
 > <span data-ttu-id="0272f-752">Используйте UUID =... toospecify дисках с данными в/etc/fstab вместо указания имени устройства hello блока (например, / dev/sdb1).</span><span class="sxs-lookup"><span data-stu-id="0272f-752">Use UUID=... toospecify data drives in /etc/fstab instead of specifying hello block device name (for example, /dev/sdb1).</span></span> <span data-ttu-id="0272f-753">Во время шифрования hello порядок изменений дисков на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0272f-753">During encryption, hello order of drives changes on hello VM.</span></span> <span data-ttu-id="0272f-754">Если ВМ зависит от определенного порядка блочные устройства, то возникнет ошибка toomount их после шифрования.</span><span class="sxs-lookup"><span data-stu-id="0272f-754">If your VM relies on a specific order of block devices, it will fail toomount them after encryption.</span></span>

3. <span data-ttu-id="0272f-755">Выйдите из сеансов SSH hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-755">Sign out of hello SSH sessions.</span></span>

4. <span data-ttu-id="0272f-756">hello tooencrypt операционной системы, укажите volumeType как **все** или **ОС** при вы [включить шифрование](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span><span class="sxs-lookup"><span data-stu-id="0272f-756">tooencrypt hello OS, specify volumeType as **All** or **OS** when you [enable encryption](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span></span>

 > [!NOTE]
 > <span data-ttu-id="0272f-757">Все пользовательские процессы, не запущенные как службы `systemd`, необходимо завершить с помощью `SIGKILL`.</span><span class="sxs-lookup"><span data-stu-id="0272f-757">All user-space processes that are not running as `systemd` services should be killed with a `SIGKILL`.</span></span> <span data-ttu-id="0272f-758">Перезагрузите hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0272f-758">Reboot hello VM.</span></span> <span data-ttu-id="0272f-759">В случае включения шифрования диска ОС на работающей виртуальной запланируйте период простоя.</span><span class="sxs-lookup"><span data-stu-id="0272f-759">When you enable OS disk encryption on a running VM, plan on VM downtime.</span></span>

5. <span data-ttu-id="0272f-760">Периодически отслеживать ход hello шифрования с помощью инструкции hello в hello [разделу](#monitoring-os-encryption-progress).</span><span class="sxs-lookup"><span data-stu-id="0272f-760">Periodically monitor hello progress of encryption by using hello instructions in hello [next section](#monitoring-os-encryption-progress).</span></span>

6. <span data-ttu-id="0272f-761">После Get AzureRmVmDiskEncryptionStatus показывает «VMRestartPending», перезапуск виртуальной Машины при входе в tooit или с помощью портала hello, PowerShell или интерфейс командной строки.</span><span class="sxs-lookup"><span data-stu-id="0272f-761">After Get-AzureRmVmDiskEncryptionStatus shows "VMRestartPending," restart your VM either by signing in tooit or by using hello portal, PowerShell, or CLI.</span></span>
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
<span data-ttu-id="0272f-762">До перезагрузки, рекомендуется сохранить [загрузки диагностики](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) из hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0272f-762">Before you reboot, we recommend that you save [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) of hello VM.</span></span>

#### <a name="monitoring-os-encryption-progress"></a><span data-ttu-id="0272f-763">Мониторинг хода выполнения шифрования операционной системы</span><span class="sxs-lookup"><span data-stu-id="0272f-763">Monitoring OS encryption progress</span></span>
<span data-ttu-id="0272f-764">Мониторинг хода выполнения шифрования ОС можно выполнять тремя способами.</span><span class="sxs-lookup"><span data-stu-id="0272f-764">You can monitor OS encryption progress in three ways:</span></span>

* <span data-ttu-id="0272f-765">Используйте hello `Get-AzureRmVmDiskEncryptionStatus` командлета и проверьте поля ProgressMessage hello:</span><span class="sxs-lookup"><span data-stu-id="0272f-765">Use hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet and inspect hello ProgressMessage field:</span></span>
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 <span data-ttu-id="0272f-766">После hello виртуальной Машины достигает «На диске ОС шифрования к работе», занимает около 40 минут too50 хранилища Premium резервного виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0272f-766">After hello VM reaches "OS disk encryption started," it takes about 40 too50 minutes on a Premium-storage backed VM.</span></span>

 <span data-ttu-id="0272f-767">В связи с [ошибкой № 388](https://github.com/Azure/WALinuxAgent/issues/388) в WALinuxAgent в некоторых дистрибутивах `OsVolumeEncrypted` и `DataVolumesEncrypted` отображаются как `Unknown`.</span><span class="sxs-lookup"><span data-stu-id="0272f-767">Because of [issue #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` and `DataVolumesEncrypted` show up as `Unknown` in some distributions.</span></span> <span data-ttu-id="0272f-768">В WALinuxAgent 2.1.5 и более поздних версиях эта проблема исправляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="0272f-768">With WALinuxAgent version 2.1.5 and later, this issue is fixed automatically.</span></span> <span data-ttu-id="0272f-769">Если вы видите `Unknown` в выходных данных hello, можно проверить состояние шифрования диска с помощью hello обозревателя ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="0272f-769">If you see `Unknown` in hello output, you can verify disk-encryption status by using hello Azure Resource Explorer.</span></span>

 <span data-ttu-id="0272f-770">Go слишком[обозревателя ресурсов Azure](https://resources.azure.com/), а затем разверните эту иерархию в область выбора hello слева:</span><span class="sxs-lookup"><span data-stu-id="0272f-770">Go too[Azure Resource Explorer](https://resources.azure.com/), and then expand this hierarchy in hello selection panel on left:</span></span>

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 <span data-ttu-id="0272f-771">Hello InstanceView прокрутите вниз toosee hello состояние шифрования дисков.</span><span class="sxs-lookup"><span data-stu-id="0272f-771">In hello InstanceView, scroll down toosee hello encryption status of your drives.</span></span>

 ![Представление экземпляра виртуальной машины](./media/azure-security-disk-encryption/vm-instanceview.png)

* <span data-ttu-id="0272f-773">Просмотрите [диагностические данные загрузки](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span><span class="sxs-lookup"><span data-stu-id="0272f-773">Look at [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span> <span data-ttu-id="0272f-774">Сообщения от hello ADE расширение должно начинаться с `[AzureDiskEncryption]`.</span><span class="sxs-lookup"><span data-stu-id="0272f-774">Messages from hello ADE extension should be prefixed with `[AzureDiskEncryption]`.</span></span>

* <span data-ttu-id="0272f-775">Войдите в toohello виртуальной Машины по протоколу SSH и получить журнал hello расширения из:</span><span class="sxs-lookup"><span data-stu-id="0272f-775">Sign in toohello VM via SSH, and get hello extension log from:</span></span>

    <span data-ttu-id="0272f-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span><span class="sxs-lookup"><span data-stu-id="0272f-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span></span>

 <span data-ttu-id="0272f-777">Мы рекомендуем, что вы не выполняют вход в toohello виртуальной Машины во время шифрования операционной системы.</span><span class="sxs-lookup"><span data-stu-id="0272f-777">We recommend that you do not sign in toohello VM while OS encryption is in progress.</span></span> <span data-ttu-id="0272f-778">Копировать журналы hello, только когда hello других двух методов завершились ошибкой.</span><span class="sxs-lookup"><span data-stu-id="0272f-778">Copy hello logs only when hello other two methods have failed.</span></span>

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a><span data-ttu-id="0272f-779">Подготовка предварительно зашифрованного виртуального жесткого диска Linux</span><span class="sxs-lookup"><span data-stu-id="0272f-779">Prepare a pre-encrypted Linux VHD</span></span>
##### <a name="ubuntu-16"></a><span data-ttu-id="0272f-780">Ubuntu 16</span><span class="sxs-lookup"><span data-stu-id="0272f-780">Ubuntu 16</span></span>
<span data-ttu-id="0272f-781">Настройка шифрования во время установки распространения hello, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="0272f-781">Configure encryption during hello distribution installation by doing hello following:</span></span>

1. <span data-ttu-id="0272f-782">Выберите **Настройка зашифрованных томов** при секционировании hello дисков.</span><span class="sxs-lookup"><span data-stu-id="0272f-782">Select **Configure encrypted volumes** when you partition hello disks.</span></span>

 ![Настройка Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. <span data-ttu-id="0272f-784">Создайте отдельный загрузочный диск (незашифрованный).</span><span class="sxs-lookup"><span data-stu-id="0272f-784">Create a separate boot drive, which must not be encrypted.</span></span> <span data-ttu-id="0272f-785">Зашифруйте корневой диск.</span><span class="sxs-lookup"><span data-stu-id="0272f-785">Encrypt your root drive.</span></span>

 ![Настройка Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. <span data-ttu-id="0272f-787">Укажите парольную фразу.</span><span class="sxs-lookup"><span data-stu-id="0272f-787">Provide a passphrase.</span></span> <span data-ttu-id="0272f-788">Это hello парольную фразу, передаче toohello хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="0272f-788">This is hello passphrase that you upload toohello key vault.</span></span>

 ![Настройка Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. <span data-ttu-id="0272f-790">Завершите настройку разделов.</span><span class="sxs-lookup"><span data-stu-id="0272f-790">Finish partitioning.</span></span>

 ![Настройка Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. <span data-ttu-id="0272f-792">При загрузке hello виртуальной Машины и требуется указать парольную фразу, используйте hello парольную фразу, что на шаге 3.</span><span class="sxs-lookup"><span data-stu-id="0272f-792">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![Настройка Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. <span data-ttu-id="0272f-794">Подготовка виртуальной Машины hello для передачи в Azure с помощью [эти инструкции](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="0272f-794">Prepare hello VM for uploading into Azure using [these instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span></span> <span data-ttu-id="0272f-795">Еще не запущены на последнем шаге hello (hello списания виртуальной Машины).</span><span class="sxs-lookup"><span data-stu-id="0272f-795">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="0272f-796">Настройка шифрования toowork с Azure, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="0272f-796">Configure encryption toowork with Azure by doing hello following:</span></span>

1. <span data-ttu-id="0272f-797">Создайте файл /usr/local/sbin/azure_crypt_key.sh, с содержимым hello в hello, выполнив сценарий.</span><span class="sxs-lookup"><span data-stu-id="0272f-797">Create a file under /usr/local/sbin/azure_crypt_key.sh, with hello content in hello following script.</span></span> <span data-ttu-id="0272f-798">Обратите внимание toohello имя файла, так как это имя файла hello парольную фразу, используемые в Azure.</span><span class="sxs-lookup"><span data-stu-id="0272f-798">Pay attention toohello KeyFileName, because it is hello passphrase file name used by Azure.</span></span>

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. <span data-ttu-id="0272f-799">Изменение конфигурации crypt hello в *crypttab/etc/*.</span><span class="sxs-lookup"><span data-stu-id="0272f-799">Change hello crypt config in */etc/crypttab*.</span></span> <span data-ttu-id="0272f-800">Результат будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="0272f-800">It should look like this:</span></span>
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. <span data-ttu-id="0272f-801">Если вы изменяете *azure_crypt_key.sh* в Windows и скопировать его tooLinux, запустите `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span><span class="sxs-lookup"><span data-stu-id="0272f-801">If you are editing *azure_crypt_key.sh* in Windows and you copied it tooLinux, run `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span></span>

4. <span data-ttu-id="0272f-802">Добавьте скрипт toohello исполняемый файл разрешений:</span><span class="sxs-lookup"><span data-stu-id="0272f-802">Add executable permissions toohello script:</span></span>
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. <span data-ttu-id="0272f-803">Измените */etc/initramfs-tools/modules*, добавив приведенные ниже строки.</span><span class="sxs-lookup"><span data-stu-id="0272f-803">Edit */etc/initramfs-tools/modules* by appending lines:</span></span>
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. <span data-ttu-id="0272f-804">Запустите `update-initramfs -u -k all` initramfs toomake tooupdate hello hello `keyscript` вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="0272f-804">Run `update-initramfs -u -k all` tooupdate hello initramfs toomake hello `keyscript` take effect.</span></span>

7. <span data-ttu-id="0272f-805">Теперь можно сделать hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0272f-805">Now you can deprovision hello VM.</span></span>

 ![Настройка Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. <span data-ttu-id="0272f-807">Продолжить toohello следующий шаг и [отправить им](#upload-encrypted-vhd-to-an-azure-storage-account) в Azure.</span><span class="sxs-lookup"><span data-stu-id="0272f-807">Continue toohello next step and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="opensuse-132"></a><span data-ttu-id="0272f-808">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="0272f-808">openSUSE 13.2</span></span>
<span data-ttu-id="0272f-809">шифрование tooconfigure во время установки распространения hello hello следующие:</span><span class="sxs-lookup"><span data-stu-id="0272f-809">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="0272f-810">При секционировании hello дисков выберите **шифрования группы томов**, а затем введите пароль.</span><span class="sxs-lookup"><span data-stu-id="0272f-810">When you partition hello disks, select **Encrypt Volume Group**, and then enter a password.</span></span> <span data-ttu-id="0272f-811">Это hello пароль, который будет передан tooyour хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="0272f-811">This is hello password that you will upload tooyour key vault.</span></span>

 ![Настройка openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. <span data-ttu-id="0272f-813">Загрузите hello виртуальную Машину с помощью пароля.</span><span class="sxs-lookup"><span data-stu-id="0272f-813">Boot hello VM using your password.</span></span>

 ![Настройка openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. <span data-ttu-id="0272f-815">Подготовка hello виртуальной Машины для передачи в соответствии с инструкциями hello в tooAzure [Подготовка виртуальной машины SLES или openSUSE для Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span><span class="sxs-lookup"><span data-stu-id="0272f-815">Prepare hello VM for uploading tooAzure by following hello instructions in [Prepare a SLES or openSUSE virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span></span> <span data-ttu-id="0272f-816">Еще не запущены на последнем шаге hello (hello списания виртуальной Машины).</span><span class="sxs-lookup"><span data-stu-id="0272f-816">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="0272f-817">tooconfigure toowork шифрования с помощью Azure hello следующие:</span><span class="sxs-lookup"><span data-stu-id="0272f-817">tooconfigure encryption toowork with Azure, do hello following:</span></span>
1. <span data-ttu-id="0272f-818">Измените hello /etc/dracut.conf и добавьте hello, следующей строкой:</span><span class="sxs-lookup"><span data-stu-id="0272f-818">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. <span data-ttu-id="0272f-819">Закомментируйте эти строки концу hello hello файла /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span><span class="sxs-lookup"><span data-stu-id="0272f-819">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. <span data-ttu-id="0272f-820">Добавьте hello, следующей строкой в начале hello hello /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh файла:</span><span class="sxs-lookup"><span data-stu-id="0272f-820">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
 ```
    DRACUT_SYSTEMD=0
 ```
<span data-ttu-id="0272f-821">Затем измените все вхождения</span><span class="sxs-lookup"><span data-stu-id="0272f-821">And change all occurrences of:</span></span>
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
<span data-ttu-id="0272f-822">на:</span><span class="sxs-lookup"><span data-stu-id="0272f-822">to:</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="0272f-823">Изменить /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh и добавьте к нему слишком «# откройте LUKS устройства»:</span><span class="sxs-lookup"><span data-stu-id="0272f-823">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append it too“# Open LUKS device”:</span></span>

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. <span data-ttu-id="0272f-824">Запустите `/usr/sbin/dracut -f -v` tooupdate hello initrd.</span><span class="sxs-lookup"><span data-stu-id="0272f-824">Run `/usr/sbin/dracut -f -v` tooupdate hello initrd.</span></span>

6. <span data-ttu-id="0272f-825">Теперь можно hello виртуальной Машины и [отправить им](#upload-encrypted-vhd-to-an-azure-storage-account) в Azure.</span><span class="sxs-lookup"><span data-stu-id="0272f-825">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="centos-7"></a><span data-ttu-id="0272f-826">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="0272f-826">CentOS 7</span></span>
<span data-ttu-id="0272f-827">шифрование tooconfigure во время установки распространения hello hello следующие:</span><span class="sxs-lookup"><span data-stu-id="0272f-827">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="0272f-828">Во время настройки разделов дисков выберите **Encrypt my data** (Шифрование личных данных).</span><span class="sxs-lookup"><span data-stu-id="0272f-828">Select **Encrypt my data** when you partition disks.</span></span>

 ![Настройка CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. <span data-ttu-id="0272f-830">Включите шифрование для корневого раздела (параметр **Encrypt**).</span><span class="sxs-lookup"><span data-stu-id="0272f-830">Make sure **Encrypt** is selected for root partition.</span></span>

 ![Настройка CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. <span data-ttu-id="0272f-832">Укажите парольную фразу.</span><span class="sxs-lookup"><span data-stu-id="0272f-832">Provide a passphrase.</span></span> <span data-ttu-id="0272f-833">Это hello парольная фраза будет отправлять tooyour хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="0272f-833">This is hello passphrase that you will upload tooyour key vault.</span></span>

 ![Настройка CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. <span data-ttu-id="0272f-835">При загрузке hello виртуальной Машины и требуется указать парольную фразу, используйте hello парольную фразу, что на шаге 3.</span><span class="sxs-lookup"><span data-stu-id="0272f-835">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![Настройка CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. <span data-ttu-id="0272f-837">Hello подготовки виртуальной Машины для передачи в Azure с помощью инструкции «CentOS 7.0 +» hello в [Подготовка виртуальной машины на основе CentOS для Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span><span class="sxs-lookup"><span data-stu-id="0272f-837">Prepare hello VM for uploading into Azure by using hello "CentOS 7.0+" instructions in [Prepare a CentOS-based virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span></span> <span data-ttu-id="0272f-838">Еще не запущены на последнем шаге hello (hello списания виртуальной Машины).</span><span class="sxs-lookup"><span data-stu-id="0272f-838">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

6. <span data-ttu-id="0272f-839">Теперь можно hello виртуальной Машины и [отправить им](#upload-encrypted-vhd-to-an-azure-storage-account) в Azure.</span><span class="sxs-lookup"><span data-stu-id="0272f-839">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

<span data-ttu-id="0272f-840">tooconfigure toowork шифрования с помощью Azure hello следующие:</span><span class="sxs-lookup"><span data-stu-id="0272f-840">tooconfigure encryption toowork with Azure, do hello following:</span></span>

1. <span data-ttu-id="0272f-841">Измените hello /etc/dracut.conf и добавьте hello, следующей строкой:</span><span class="sxs-lookup"><span data-stu-id="0272f-841">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. <span data-ttu-id="0272f-842">Закомментируйте эти строки концу hello hello файла /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span><span class="sxs-lookup"><span data-stu-id="0272f-842">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. <span data-ttu-id="0272f-843">Добавьте hello, следующей строкой в начале hello hello /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh файла:</span><span class="sxs-lookup"><span data-stu-id="0272f-843">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
```
    DRACUT_SYSTEMD=0
```
<span data-ttu-id="0272f-844">Затем измените все вхождения</span><span class="sxs-lookup"><span data-stu-id="0272f-844">And change all occurrences of:</span></span>
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
<span data-ttu-id="0272f-845">значение</span><span class="sxs-lookup"><span data-stu-id="0272f-845">to</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="0272f-846">Измените /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh и добавить это после «# откройте LUKS device» hello:</span><span class="sxs-lookup"><span data-stu-id="0272f-846">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append this after hello “# Open LUKS device”:</span></span>
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. <span data-ttu-id="0272f-847">Запустите hello «/ usr/sbin/dracut - f - v» tooupdate hello initrd.</span><span class="sxs-lookup"><span data-stu-id="0272f-847">Run hello “/usr/sbin/dracut -f -v” tooupdate hello initrd.</span></span>

![Настройка CentOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a><span data-ttu-id="0272f-849">Отправка зашифрованного учетной записи хранилища Azure tooan виртуального жесткого диска</span><span class="sxs-lookup"><span data-stu-id="0272f-849">Upload encrypted VHD tooan Azure storage account</span></span>
<span data-ttu-id="0272f-850">После включения шифрования BitLocker или Crypt интеллектуальный анализ данных для шифрования локальных hello шифруются учетной записи хранилища tooyour toobe отправлен потребностей виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="0272f-850">After BitLocker encryption or DM-Crypt encryption is enabled, hello local encrypted VHD needs toobe uploaded tooyour storage account.</span></span>

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a><span data-ttu-id="0272f-851">Отправка hello секрет шифрование диска для hello предварительно зашифрованный ВМ tooyour хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="0272f-851">Upload hello disk-encryption secret for hello pre-encrypted VM tooyour key vault</span></span>
<span data-ttu-id="0272f-852">секрет Hello шифрование диска, полученный ранее должен быть передан как секрет в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="0272f-852">hello disk-encryption secret that you obtained previously must be uploaded as a secret in your key vault.</span></span> <span data-ttu-id="0272f-853">хранилище ключей Hello должен toohave шифрования диска и разрешениями, назначенными для вашего клиента Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0272f-853">hello key vault needs toohave disk encryption and permissions enabled for your Azure AD client.</span></span>

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a><span data-ttu-id="0272f-854">Секрет дискового шифрования не шифруется с помощью KEK</span><span class="sxs-lookup"><span data-stu-id="0272f-854">Disk encryption secret not encrypted with a KEK</span></span>
<span data-ttu-id="0272f-855">tooset копирование hello секрет в хранилище ключей, используйте [AzureKeyVaultSecret набор](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="0272f-855">tooset up hello secret in your key vault, use [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span></span> <span data-ttu-id="0272f-856">При наличии виртуальной машины Windows hello bek файл кодируется в виде строки base64, а затем загружается tooyour хранилища ключей с помощью hello `Set-AzureKeyVaultSecret` командлета.</span><span class="sxs-lookup"><span data-stu-id="0272f-856">If you have a Windows virtual machine, hello bek file is encoded as a base64 string and then uploaded tooyour key vault using hello `Set-AzureKeyVaultSecret` cmdlet.</span></span> <span data-ttu-id="0272f-857">Для Linux парольную фразу hello кодируется в виде строки base64 и затем загружается toohello хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="0272f-857">For Linux, hello passphrase is encoded as a base64 string and then uploaded toohello key vault.</span></span> <span data-ttu-id="0272f-858">Кроме того убедитесь, что этот hello следующие теги задаются при создании hello секрет в хранилище ключей hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-858">In addition, make sure that hello following tags are set when you create hello secret in hello key vault.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

<span data-ttu-id="0272f-859">Используйте hello `$secretUrl` hello на следующем шаге для [присоединение диска hello ОС без использования KEK](#without-using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="0272f-859">Use hello `$secretUrl` in hello next step for [attaching hello OS disk without using KEK](#without-using-a-kek).</span></span>

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a><span data-ttu-id="0272f-860">Секрет дискового шифрования, зашифрованный с помощью KEK</span><span class="sxs-lookup"><span data-stu-id="0272f-860">Disk encryption secret encrypted with a KEK</span></span>
<span data-ttu-id="0272f-861">Перед отправкой хранилища ключей секретный toohello hello, вы можете зашифровать с помощью ключа шифрования.</span><span class="sxs-lookup"><span data-stu-id="0272f-861">Before you upload hello secret toohello key vault, you can optionally encrypt it by using a key encryption key.</span></span> <span data-ttu-id="0272f-862">Используйте hello wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst шифрования с помощью ключа шифрования ключа hello секрет hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-862">Use hello wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst encrypt hello secret using hello key encryption key.</span></span> <span data-ttu-id="0272f-863">Hello этой операции wrap выводится строка URL-адреса в кодировке base64 можно затем передать как секрета с помощью hello [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) командлета.</span><span class="sxs-lookup"><span data-stu-id="0272f-863">hello output of this wrap operation is a base64 URL encoded string, which you can then upload as a secret by using hello [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

<span data-ttu-id="0272f-864">Используйте `$KeyEncryptionKey` и `$secretUrl` hello на следующем шаге для [присоединение диска hello операционной системы с помощью ключа обмена Ключами](#using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="0272f-864">Use `$KeyEncryptionKey` and `$secretUrl` in hello next step for [attaching hello OS disk using KEK](#using-a-kek).</span></span>

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a><span data-ttu-id="0272f-865">Указание URL-адреса секрета при подключении диска ОС</span><span class="sxs-lookup"><span data-stu-id="0272f-865">Specify a secret URL when you attach an OS disk</span></span>
#### <a name="without-using-a-kek"></a><span data-ttu-id="0272f-866">Без использования ключа шифрования ключа</span><span class="sxs-lookup"><span data-stu-id="0272f-866">Without using a KEK</span></span>
<span data-ttu-id="0272f-867">Во время присоединения диска hello ОС, необходимо toopass `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="0272f-867">While you are attaching hello OS disk, you need toopass `$secretUrl`.</span></span> <span data-ttu-id="0272f-868">Hello URL-адрес был создан в разделе «Шифрование диска не зашифрован с помощью ключа обмена Ключами секрет» hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-868">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a><span data-ttu-id="0272f-869">С использованием ключа шифрования ключа</span><span class="sxs-lookup"><span data-stu-id="0272f-869">Using a KEK</span></span>
<span data-ttu-id="0272f-870">При подключении диска hello ОС, передайте `$KeyEncryptionKey` и `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="0272f-870">When you attach hello OS disk, pass `$KeyEncryptionKey` and `$secretUrl`.</span></span> <span data-ttu-id="0272f-871">Hello URL-адрес был создан в разделе «Шифрование диска не зашифрован с помощью ключа обмена Ключами секрет» hello.</span><span class="sxs-lookup"><span data-stu-id="0272f-871">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a><span data-ttu-id="0272f-872">Загрузка руководства</span><span class="sxs-lookup"><span data-stu-id="0272f-872">Download this guide</span></span>
<span data-ttu-id="0272f-873">Это руководство можно загрузить из hello [коллекции TechNet](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span><span class="sxs-lookup"><span data-stu-id="0272f-873">You can download this guide from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span></span>

## <a name="for-more-information"></a><span data-ttu-id="0272f-874">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="0272f-874">For more information</span></span>
<span data-ttu-id="0272f-875">[Explore Azure Disk Encryption with Azure PowerShell](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0) (Изучение возможностей шифрования дисков Azure с помощью PowerShell)</span><span class="sxs-lookup"><span data-stu-id="0272f-875">[Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)</span></span>  
[<span data-ttu-id="0272f-876">Изучение возможностей дискового шифрования Azure с помощью Azure PowerShell — часть 2</span><span class="sxs-lookup"><span data-stu-id="0272f-876">Explore Azure Disk Encryption with Azure PowerShell - Part 2</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
