---
title: "aaaRed Hat обновления инфраструктуры (RHUI) | Документы Microsoft"
description: "Узнайте об инфраструктуре обновления Red Hat Update Infrastructure для предоставляемых по запросу экземпляров Red Hat Enterprise Linux по запросу в Microsoft Azure"
services: virtual-machines-linux
documentationcenter: 
author: BorisB2015
manager: timlt
editor: 
ms.assetid: f495f1b4-ae24-46b9-8d26-c617ce3daf3a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: borisb
ms.openlocfilehash: cc244857104b25e4e61862c518db77e915e137ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a><span data-ttu-id="dfeb0-103">Red Hat Update Infrastructure для предоставляемых по запросу виртуальных машин Red Hat Enterprise Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="dfeb0-103">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>
<span data-ttu-id="dfeb0-104">Виртуальные машины, созданные из hello по требованию Red Hat Enterprise Linux (RHEL) образов, доступных в Azure Marketplace, зарегистрированных tooaccess hello Hat обновления красный инфраструктуры (RHUI) развернуты в Azure.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-104">Virtual machines created from hello on-demand Red Hat Enterprise Linux (RHEL) images available in Azure Marketplace are registered tooaccess hello Red Hat Update Infrastructure (RHUI) deployed in Azure.</span></span>  <span data-ttu-id="dfeb0-105">Hello по требованию RHEL экземпляры имеют репозиторий региональных yum tooa доступа и могут tooreceive добавочные обновления.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-105">hello on-demand RHEL instances have access tooa regional yum repository and able tooreceive incremental updates.</span></span>

<span data-ttu-id="dfeb0-106">Список репозитория yum Hello, который находится под управлением RHUI, настраивается в вашем экземпляре RHEL во время инициализации.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-106">hello yum repository list, which is managed by RHUI, is configured in your RHEL instance during provisioning.</span></span> <span data-ttu-id="dfeb0-107">Toodo не требуется дополнительная настройка - запустить `yum update` после RHEL экземпляр готов tooget hello последние обновления.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-107">You don't need toodo any additional configuration - run `yum update` after your RHEL instance is ready tooget hello latest updates.</span></span>

> [!NOTE]
> <span data-ttu-id="dfeb0-108">В сентябре 2016 года были развернуты обновленные RHUI Azure и в января 2017 г. Мы запустили поэтапного shutdown hello старые RHUI Azure.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-108">In September 2016 we deployed an updated Azure RHUI and in January 2017 we started phased shutdown of hello older Azure RHUI.</span></span> <span data-ttu-id="dfeb0-109">Если вы использовали hello RHEL изображения (или их моментальные снимки) с сентября 2016 года или более поздней версии — скорее всего, никаких действий не требуется.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-109">If you have been using hello RHEL images (or their snapshots) from September 2016 or later - likely no action is required.</span></span> <span data-ttu-id="dfeb0-110">Если, однако старые моментальные снимки и виртуальные машины, их конфигурации должен toobe обновлен для непрерывного доступа toohello Azure RHUI.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-110">If, however, you have older snapshots/VMs, their configuration needs toobe updated for uninterrupted access toohello Azure RHUI.</span></span>
> 

## <a name="rhui-azure-infrastructure-update"></a><span data-ttu-id="dfeb0-111">Обновление инфраструктуры Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="dfeb0-111">RHUI Azure Infrastructure Update</span></span>
<span data-ttu-id="dfeb0-112">Начиная с сентября 2016 г. в Azure доступен новый набор серверов Red Hat Update Infrastructure (RHUI).</span><span class="sxs-lookup"><span data-stu-id="dfeb0-112">As of September 2016, Azure has a new set of Red Hat Update Infrastructure (RHUI) servers.</span></span> <span data-ttu-id="dfeb0-113">Эти серверы развертываются с помощью [диспетчера трафика Azure](https://azure.microsoft.com/services/traffic-manager/), чтобы конечную точку (rhui-1.microsoft.com) могла использовать любая виртуальная машина независимо от региона.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-113">These servers are deployed with [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) so that a single endpoint (rhui-1.microsoft.com) can be used by any VM regardless of region.</span></span> <span data-ttu-id="dfeb0-114">Здравствуйте, новые образы RHEL Оплата по мере использования (PAYG) в новых серверов Azure RHUI hello Azure Marketplace (выпущенная в сентябре 2016 года или более поздней версии) toohello точки и не требуют дополнительных действий.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-114">hello new RHEL Pay-As-You-Go (PAYG) images in hello Azure Marketplace (versions dated September 2016 or later) point toohello new Azure RHUI servers and do not require any additional action.</span></span>

### <a name="determine-if-action-is-required"></a><span data-ttu-id="dfeb0-115">Как определить, требуется ли действие</span><span class="sxs-lookup"><span data-stu-id="dfeb0-115">Determine if action is required</span></span>
<span data-ttu-id="dfeb0-116">Если вы испытываете проблемы с подключением tooAzure RHUI из ВМ PAYG RHEL Azure, выполните следующие действия</span><span class="sxs-lookup"><span data-stu-id="dfeb0-116">If you are experiencing problems connecting tooAzure RHUI from your Azure RHEL PAYG VM, follow these steps</span></span>
1. <span data-ttu-id="dfeb0-117">Проверка конфигурации виртуальной машины для конечной точки Azure RHUI</span><span class="sxs-lookup"><span data-stu-id="dfeb0-117">Inspect VM configuration for Azure RHUI endpoint</span></span>

    <span data-ttu-id="dfeb0-118">Установите флажок, если `/etc/yum.repos.d/rh-cloud.repo` файл содержит ссылку на слишком`rhui-[1-3].microsoft.com` в baseurl из `[rhui-microsoft-azure-rhel*]` раздел файла hello.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-118">Check if `/etc/yum.repos.d/rh-cloud.repo` file contains reference too`rhui-[1-3].microsoft.com` in baseurl of `[rhui-microsoft-azure-rhel*]` section of hello file.</span></span> <span data-ttu-id="dfeb0-119">Если это — вы используете hello новый RHUI Azure.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-119">If it is - you are using hello new Azure RHUI.</span></span>

    <span data-ttu-id="dfeb0-120">Если указывающей место tooa с hello следующий шаблон `mirrorlist.*cds[1-4].cloudapp.net` -требуется обновление конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-120">If it pointing tooa location with hello following pattern `mirrorlist.*cds[1-4].cloudapp.net` - hello configuration update is required.</span></span>

    <span data-ttu-id="dfeb0-121">Если вы используете новую конфигурацию hello и по-прежнему не удается подключиться к tooAzure RHUI - файлов в службу технической поддержки Майкрософт или Red Hat.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-121">If you are using hello new configuration and still cannot connect tooAzure RHUI - file a support case with Microsoft or Red Hat.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dfeb0-122">Размещенное tooAzure RHUI доступа является ограниченной toohello ВМ в [Microsoft Azure Datacenter, IP-диапазонов](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="dfeb0-122">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
    > 

2. <span data-ttu-id="dfeb0-123">Если hello старый RHUI Azure доступен по-прежнему при выполнения такой проверки и хотелось бы tooautomatically обновление hello конфигурации, выполните hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="dfeb0-123">If hello old Azure RHUI is still available when you do this check and you would like tooautomatically update hello configuration, execute hello following command:</span></span>

    <span data-ttu-id="dfeb0-124">`sudo yum update RHEL6`или `sudo yum update RHEL7` в зависимости от версии семейства RHEL hello.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-124">`sudo yum update RHEL6` or `sudo yum update RHEL7` depending on hello RHEL family version.</span></span>

3. <span data-ttu-id="dfeb0-125">Если вы больше не можете подключиться toohello старый RHUI Azure, выполните hello вручную шаги, описанные в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-125">If you can no longer connect toohello old Azure RHUI, follow hello manual steps described in hello next section.</span></span>

4. <span data-ttu-id="dfeb0-126">Убедитесь, что конфигурация hello tooupdate hello источника изображения или создания моментального снимка влияет виртуальной Машины была создана из.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-126">Make sure tooupdate hello configuration on hello source image/snapshot affected VM was provisioned from.</span></span>

### <a name="phased-shutdown-of-hello-old-azure-rhui"></a><span data-ttu-id="dfeb0-127">Старый RHUI Azure hello поэтапного завершения работы</span><span class="sxs-lookup"><span data-stu-id="dfeb0-127">Phased shutdown of hello old Azure RHUI</span></span>
<span data-ttu-id="dfeb0-128">При закрытии hello hello старый RHUI Azure, мы ограничить доступ к tooit следующим образом:</span><span class="sxs-lookup"><span data-stu-id="dfeb0-128">During hello shutdown of hello old Azure RHUI we restrict access tooit as follows:</span></span>

1. <span data-ttu-id="dfeb0-129">Ограничьте tooset доступа (ACL), IP-адресов, уже подключенные tooit.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-129">Further restrict access (ACL) tooset of IP addresses that are already connecting tooit.</span></span> <span data-ttu-id="dfeb0-130">Побочные эффекты: Если вы продолжите использовать hello старый RHUI Azure — новые виртуальные машины не может быть tooit может tooconnect.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-130">Possible side-effects: if you continue using hello old Azure RHUI - your new VMs may not be able tooconnect tooit.</span></span> <span data-ttu-id="dfeb0-131">Виртуальные машины RHEL с динамические IP-адреса, проходят через последовательность завершения работы или освобождения/start может получить новый IP-адрес и поэтому также может начинаться сбоем tooconnect toohello старый RHUI Azure</span><span class="sxs-lookup"><span data-stu-id="dfeb0-131">RHEL VMs with dynamic IPs that go through shutdown/deallocate/start sequence may receive new IP and hence also could start failing tooconnect toohello old Azure RHUI</span></span>

2. <span data-ttu-id="dfeb0-132">Завершение работы зеркальных серверов доставки содержимого.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-132">Shutdown of mirror content delivery servers.</span></span> <span data-ttu-id="dfeb0-133">Побочные эффекты: как мы выключить дополнительные CDSes может появиться больше `yum update` обслуживания время, дополнительные значения времени ожидания до вызова метода hello момент, когда больше не может подключиться toohello старый RHUI Azure.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-133">Possible side-effects: as we shut down more CDSes you may see longer `yum update` servicing time, more timeouts up until hello point when you can no longer connect toohello old Azure RHUI.</span></span>

### <a name="hello-ips-for-hello-new-rhui-content-delivery-servers-are"></a><span data-ttu-id="dfeb0-134">Hello IP-адресов для hello новых серверов RHUI доставки содержимого</span><span class="sxs-lookup"><span data-stu-id="dfeb0-134">hello IPs for hello new RHUI content delivery servers are</span></span>
<span data-ttu-id="dfeb0-135">При использовании toofurther конфигурации сети ограничить доступ из виртуальных машин PAYG RHEL, убедитесь, что разрешены следующие IP-адреса hello `yum update` toowork в зависимости от того, находятся в среде hello.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-135">If you are using network configuration toofurther restrict access from RHEL PAYG VMs, make sure hello following IPs are allowed for `yum update` toowork depending on hello environment you are in.</span></span> 

```
# Azure Global
13.91.47.76
40.85.190.91
52.187.75.218
52.174.163.213

# Azure US Government
13.72.186.193

# Azure Germany
51.5.243.77
51.4.228.145
```

### <a name="manual-update-procedure-toouse-hello-new-azure-rhui-servers"></a><span data-ttu-id="dfeb0-136">Ручное обновление процедуры toouse hello новых Azure RHUI серверов</span><span class="sxs-lookup"><span data-stu-id="dfeb0-136">Manual update procedure toouse hello new Azure RHUI servers</span></span>
<span data-ttu-id="dfeb0-137">Подпись открытого ключа загрузки (с помощью перелистывание) hello</span><span class="sxs-lookup"><span data-stu-id="dfeb0-137">Download (via curl) hello public key signature</span></span>

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

<span data-ttu-id="dfeb0-138">Проверьте ключ загружаются hello</span><span class="sxs-lookup"><span data-stu-id="dfeb0-138">Verify hello downloaded key</span></span>

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="dfeb0-139">Проверьте выходные данные hello, проверьте `keyid` и `user ID packet`:</span><span class="sxs-lookup"><span data-stu-id="dfeb0-139">Check hello output, verify `keyid` and `user ID packet`:</span></span>

```bash
Version: GnuPG v1.4.7 (GNU/Linux)
:public key packet:
        version 4, algo 1, created 1446074508, expires 0
        pkey[0]: [2048 bits]
        pkey[1]: [17 bits]
        keyid: EB3E94ADBE1229CF
:user ID packet: "Microsoft (Release signing) <gpgsecurity@microsoft.com>"
:signature packet: algo 1, keyid EB3E94ADBE1229CF
        version 4, created 1446074508, md5len 0, sigclass 0x13
        digest algo 2, begin of digest 1a 9b
        hashed subpkt 2 len 4 (sig created 2015-10-28)
        hashed subpkt 27 len 1 (key flags: 03)
        hashed subpkt 11 len 5 (pref-sym-algos: 9 8 7 3 2)
        hashed subpkt 21 len 3 (pref-hash-algos: 2 8 3)
        hashed subpkt 22 len 2 (pref-zip-algos: 2 1)
        hashed subpkt 30 len 1 (features: 01)
        hashed subpkt 23 len 1 (key server preferences: 80)
        subpkt 16 len 8 (issuer key ID EB3E94ADBE1229CF)
        data: [2047 bits]
```

<span data-ttu-id="dfeb0-140">Установка hello открытого ключа</span><span class="sxs-lookup"><span data-stu-id="dfeb0-140">Install hello public key</span></span>

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="dfeb0-141">Загрузите, проверьте и установите RPM клиента</span><span class="sxs-lookup"><span data-stu-id="dfeb0-141">Download, Verify, and Install Client RPM</span></span>

<span data-ttu-id="dfeb0-142">Загрузка для RHEL 6</span><span class="sxs-lookup"><span data-stu-id="dfeb0-142">Download: For RHEL 6</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

<span data-ttu-id="dfeb0-143">Для RHEL 7</span><span class="sxs-lookup"><span data-stu-id="dfeb0-143">For RHEL 7</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

<span data-ttu-id="dfeb0-144">Проверка.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-144">Verify:</span></span>

```bash
rpm -Kv azureclient.rpm
```

<span data-ttu-id="dfeb0-145">Проверьте в выходных данных этой подписью hello пакета — ОК</span><span class="sxs-lookup"><span data-stu-id="dfeb0-145">Check in output that signature of hello package is OK</span></span>

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

<span data-ttu-id="dfeb0-146">Установка hello об/мин</span><span class="sxs-lookup"><span data-stu-id="dfeb0-146">Install hello RPM</span></span>

```bash
sudo rpm -U azureclient.rpm
```

<span data-ttu-id="dfeb0-147">По завершении убедитесь, что можно доступ hello Azure RHUI формы виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="dfeb0-147">Upon completion, verify that you can access Azure RHUI form hello VM</span></span>

### <a name="all-in-one-script-for-automating-hello-preceding-task"></a><span data-ttu-id="dfeb0-148">В одном скрипт для автоматизации hello предшествующей задачи</span><span class="sxs-lookup"><span data-stu-id="dfeb0-148">All-in-one script for automating hello preceding task</span></span>
<span data-ttu-id="dfeb0-149">Используйте следующий сценарий как задачу hello tooautomate необходимые обновления затронутые виртуальные машины toohello новых Azure RHUI серверов hello.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-149">Use hello following script as needed tooautomate hello task of updating affected VMs toohello new Azure RHUI servers.</span></span>

```sh
# Download key
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 

# Validate key
if ! gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release | grep -q "keyid: EB3E94ADBE1229CF"; then
    echo "Keyfile azure.asc NOT valid. Exiting."
    exit 1
fi

# Install Key
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release

# Download RPM package
if grep -q "release 7" /etc/redhat-release; then
    ver=7
elif  grep -q "release 6" /etc/redhat-release; then
    ver=6
else
    echo "Version not supported, exiting"
    exit 1
fi

url=https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel$ver/rhui-azure-rhel$ver-2.0-2.noarch.rpm
curl -o azureclient.rpm "$url"

# Verify package
if ! rpm -Kv azureclient.rpm | grep -q "key ID be1229cf: OK"; then
    echo "RPM failed validation ($url)"
    exit 1
fi

# Install package
sudo rpm -U azureclient.rpm
```

## <a name="rhui-overview"></a><span data-ttu-id="dfeb0-150">Обзор RHUI</span><span class="sxs-lookup"><span data-stu-id="dfeb0-150">RHUI overview</span></span>
<span data-ttu-id="dfeb0-151">[Инфраструктура обновления Red Hat](https://access.redhat.com/products/red-hat-update-infrastructure) обеспечивает масштабируемое решение toomanage yum репозиторий контента для экземпляров облачной Red Hat Enterprise Linux, размещенные на поставщиков облачных Сертифицировано Red Hat.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-151">[Red Hat Update Infrastructure](https://access.redhat.com/products/red-hat-update-infrastructure) offers a highly scalable solution toomanage yum repository content for Red Hat Enterprise Linux cloud instances that are hosted by Red Hat-certified cloud providers.</span></span> <span data-ttu-id="dfeb0-152">На основе hello вышестоящего отделение проекта, RHUI позволяет поставщиков облачных служб контента репозитория, размещенных в Red Hat зеркальной toolocally, создайте пользовательские репозитории своим содержимым и сделать эти репозиториев tooa доступных большой группе конечным пользователям через балансировкой нагрузки система содержимого доставки.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-152">Based on hello upstream Pulp project, RHUI allows cloud providers toolocally mirror Red Hat-hosted repository content, create custom repositories with their own content, and make those repositories available tooa large group of end users through a load-balanced content delivery system.</span></span>

## <a name="regions-where-rhui-is-available"></a><span data-ttu-id="dfeb0-153">Регионы, в которых доступна инфраструктура RHUI</span><span class="sxs-lookup"><span data-stu-id="dfeb0-153">Regions where RHUI is available</span></span>
<span data-ttu-id="dfeb0-154">Инфраструктура RHUI поддерживается во всех регионах, где доступны предоставляемые по запросу образы RHEL.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-154">RHUI is available in all regions where RHEL on-demand images are available.</span></span> <span data-ttu-id="dfeb0-155">В настоящее время он включает все открытые регионах, перечисленных на hello [панель мониторинга Azure status](https://azure.microsoft.com/status/) страницы области правительства США и Германии Azure.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-155">It currently includes all public regions listed on hello [Azure status dashboard](https://azure.microsoft.com/status/) page, Azure US Government and Azure Germany regions.</span></span> <span data-ttu-id="dfeb0-156">Доступ к RHUI для виртуальных машин, развернутых из предоставляемых по запросу образов RHEL, входит в стоимость образа.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-156">RHUI access for VMs provisioned from RHEL on-demand images is included in their price.</span></span> <span data-ttu-id="dfeb0-157">Дополнительные облачные региональные и национальные доступности будет обновляться планируем RHEL доступности по требованию в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-157">Additional regional/national cloud availability will be updated as we expand RHEL on-demand availability in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="dfeb0-158">Размещенное tooAzure RHUI доступа является ограниченной toohello ВМ в [Microsoft Azure Datacenter, IP-диапазонов](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="dfeb0-158">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
> 
> 

## <a name="get-updates-from-another-update-repository"></a><span data-ttu-id="dfeb0-159">Получение обновлений из другого репозитория обновлений</span><span class="sxs-lookup"><span data-stu-id="dfeb0-159">Get updates from another update repository</span></span>
<span data-ttu-id="dfeb0-160">Если вам требуется tooget обновлений из репозитория (а не размещенной в Azure RHUI) различные обновления, сначала необходимо toounregister своих экземпляров из RHUI.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-160">If you need tooget updates from a different update repository (instead of Azure-hosted RHUI), first you need toounregister your instances from RHUI.</span></span> <span data-ttu-id="dfeb0-161">Необходимо зарегистрировать toore с hello нужные обновления инфраструктуры (например, Red Hat вспомогательные или клиента портал Red Hat CDN).</span><span class="sxs-lookup"><span data-stu-id="dfeb0-161">Then you need toore-register them with hello desired update infrastructure (such as Red Hat Satellite or Red Hat Customer Portal CDN).</span></span> <span data-ttu-id="dfeb0-162">Кроме того, необходима подписка Red Hat для этих служб и регистрация [Red Hat Cloud Access в Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="dfeb0-162">You will need appropriate Red Hat subscriptions for these services and registration for [Red Hat Cloud Access in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span></span>

<span data-ttu-id="dfeb0-163">toounregister RHUI и инфраструктура обновления повторно зарегистрируйте tooyour выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-163">toounregister RHUI and reregister tooyour update infrastructure follow these steps:</span></span>

1. <span data-ttu-id="dfeb0-164">Измените /etc/yum.repos.d/rh-cloud.repo, все `enabled=1` слишком`enabled=0`.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-164">Edit /etc/yum.repos.d/rh-cloud.repo and change all `enabled=1` too`enabled=0`.</span></span> <span data-ttu-id="dfeb0-165">Например:</span><span class="sxs-lookup"><span data-stu-id="dfeb0-165">For example:</span></span>
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. <span data-ttu-id="dfeb0-166">Измените /etc/yum/pluginconf.d/rhnplugin.conf, `enabled=0` слишком`enabled=1`.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-166">Edit /etc/yum/pluginconf.d/rhnplugin.conf and change `enabled=0` too`enabled=1`.</span></span>
3. <span data-ttu-id="dfeb0-167">Затем зарегистрируйте hello требуемой инфраструктуры, например клиентский портал Red Hat.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-167">Then register with hello desired infrastructure, such as Red Hat Customer Portal.</span></span> <span data-ttu-id="dfeb0-168">Выполните Red Hat решение руководства на [как tooregister и подписка системы toohello клиентский портал Red Hat](https://access.redhat.com/solutions/253273).</span><span class="sxs-lookup"><span data-stu-id="dfeb0-168">Follow Red Hat solution guide on [how tooregister and subscribe a system toohello Red Hat Customer Portal](https://access.redhat.com/solutions/253273).</span></span>

> [!NOTE]
> <span data-ttu-id="dfeb0-169">Доступ toohello RHUI, размещенной в Azure включается в цены изображения hello RHEL Оплата по мере использования (PAYG).</span><span class="sxs-lookup"><span data-stu-id="dfeb0-169">Access toohello Azure-hosted RHUI is included in hello RHEL Pay-As-You-Go (PAYG) image price.</span></span> <span data-ttu-id="dfeb0-170">При отмене регистрации виртуальную Машину RHEL PAYG hello RHUI, размещенной в Azure не выполняется преобразование hello виртуальной машины в тип перевести--владельцем-лицензии (BYOL) виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-170">Unregistering a PAYG RHEL VM from hello Azure-hosted RHUI does not convert hello virtual machine into Bring-Your-Own-License (BYOL) type VM.</span></span> <span data-ttu-id="dfeb0-171">При регистрации hello одной виртуальной Машины с другим источником обновления может несения двойные расходов: сначала по времени для сбора Azure RHEL программного обеспечения и hello второй раз для Red Hat подписок.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-171">If you register hello same VM with another source of updates you may be incurring double charges: first time for Azure RHEL software fee, and hello second time for Red Hat subscription(s).</span></span> 
> 
> <span data-ttu-id="dfeb0-172">Если необходимо постоянно toouse инфраструктуры обновления, кроме RHUI, размещенной в Azure рекомендуется создание и развертывание собственных изображений (BYOL-type), как описано в [Создание и отправка Red Hat виртуальной машины для Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) статьи.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-172">If you consistently need toouse an update infrastructure other than Azure-hosted RHUI consider creating and deploying your own (BYOL-type) images as described in [Create and Upload Red Hat-based virtual machine for Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article.</span></span>
> 

## <a name="next-steps"></a><span data-ttu-id="dfeb0-173">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="dfeb0-173">Next steps</span></span>
<span data-ttu-id="dfeb0-174">Red Hat Enterprise Linux виртуальной Машины из образа Azure Marketplace Оплата по мере использования и коэффициент размещенной в Azure RHUI toocreate go слишком[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span><span class="sxs-lookup"><span data-stu-id="dfeb0-174">toocreate a Red Hat Enterprise Linux VM from Azure Marketplace Pay-As-You-Go image and leverage Azure-hosted RHUI go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span></span> <span data-ttu-id="dfeb0-175">Можно будет toouse `yum update` в вашем экземпляре RHEL без дополнительных настроек.</span><span class="sxs-lookup"><span data-stu-id="dfeb0-175">You will be able toouse `yum update` in your RHEL instance without any additional setup.</span></span>

