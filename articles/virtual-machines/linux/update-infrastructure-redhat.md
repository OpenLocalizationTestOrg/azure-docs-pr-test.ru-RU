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
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a>Red Hat Update Infrastructure для предоставляемых по запросу виртуальных машин Red Hat Enterprise Linux в Azure
Виртуальные машины, созданные из hello по требованию Red Hat Enterprise Linux (RHEL) образов, доступных в Azure Marketplace, зарегистрированных tooaccess hello Hat обновления красный инфраструктуры (RHUI) развернуты в Azure.  Hello по требованию RHEL экземпляры имеют репозиторий региональных yum tooa доступа и могут tooreceive добавочные обновления.

Список репозитория yum Hello, который находится под управлением RHUI, настраивается в вашем экземпляре RHEL во время инициализации. Toodo не требуется дополнительная настройка - запустить `yum update` после RHEL экземпляр готов tooget hello последние обновления.

> [!NOTE]
> В сентябре 2016 года были развернуты обновленные RHUI Azure и в января 2017 г. Мы запустили поэтапного shutdown hello старые RHUI Azure. Если вы использовали hello RHEL изображения (или их моментальные снимки) с сентября 2016 года или более поздней версии — скорее всего, никаких действий не требуется. Если, однако старые моментальные снимки и виртуальные машины, их конфигурации должен toobe обновлен для непрерывного доступа toohello Azure RHUI.
> 

## <a name="rhui-azure-infrastructure-update"></a>Обновление инфраструктуры Azure RHUI
Начиная с сентября 2016 г. в Azure доступен новый набор серверов Red Hat Update Infrastructure (RHUI). Эти серверы развертываются с помощью [диспетчера трафика Azure](https://azure.microsoft.com/services/traffic-manager/), чтобы конечную точку (rhui-1.microsoft.com) могла использовать любая виртуальная машина независимо от региона. Здравствуйте, новые образы RHEL Оплата по мере использования (PAYG) в новых серверов Azure RHUI hello Azure Marketplace (выпущенная в сентябре 2016 года или более поздней версии) toohello точки и не требуют дополнительных действий.

### <a name="determine-if-action-is-required"></a>Как определить, требуется ли действие
Если вы испытываете проблемы с подключением tooAzure RHUI из ВМ PAYG RHEL Azure, выполните следующие действия
1. Проверка конфигурации виртуальной машины для конечной точки Azure RHUI

    Установите флажок, если `/etc/yum.repos.d/rh-cloud.repo` файл содержит ссылку на слишком`rhui-[1-3].microsoft.com` в baseurl из `[rhui-microsoft-azure-rhel*]` раздел файла hello. Если это — вы используете hello новый RHUI Azure.

    Если указывающей место tooa с hello следующий шаблон `mirrorlist.*cds[1-4].cloudapp.net` -требуется обновление конфигурации hello.

    Если вы используете новую конфигурацию hello и по-прежнему не удается подключиться к tooAzure RHUI - файлов в службу технической поддержки Майкрософт или Red Hat.

    > [!NOTE]
    > Размещенное tooAzure RHUI доступа является ограниченной toohello ВМ в [Microsoft Azure Datacenter, IP-диапазонов](https://www.microsoft.com/download/details.aspx?id=41653).
    > 

2. Если hello старый RHUI Azure доступен по-прежнему при выполнения такой проверки и хотелось бы tooautomatically обновление hello конфигурации, выполните hello следующую команду:

    `sudo yum update RHEL6`или `sudo yum update RHEL7` в зависимости от версии семейства RHEL hello.

3. Если вы больше не можете подключиться toohello старый RHUI Azure, выполните hello вручную шаги, описанные в следующем разделе hello.

4. Убедитесь, что конфигурация hello tooupdate hello источника изображения или создания моментального снимка влияет виртуальной Машины была создана из.

### <a name="phased-shutdown-of-hello-old-azure-rhui"></a>Старый RHUI Azure hello поэтапного завершения работы
При закрытии hello hello старый RHUI Azure, мы ограничить доступ к tooit следующим образом:

1. Ограничьте tooset доступа (ACL), IP-адресов, уже подключенные tooit. Побочные эффекты: Если вы продолжите использовать hello старый RHUI Azure — новые виртуальные машины не может быть tooit может tooconnect. Виртуальные машины RHEL с динамические IP-адреса, проходят через последовательность завершения работы или освобождения/start может получить новый IP-адрес и поэтому также может начинаться сбоем tooconnect toohello старый RHUI Azure

2. Завершение работы зеркальных серверов доставки содержимого. Побочные эффекты: как мы выключить дополнительные CDSes может появиться больше `yum update` обслуживания время, дополнительные значения времени ожидания до вызова метода hello момент, когда больше не может подключиться toohello старый RHUI Azure.

### <a name="hello-ips-for-hello-new-rhui-content-delivery-servers-are"></a>Hello IP-адресов для hello новых серверов RHUI доставки содержимого
При использовании toofurther конфигурации сети ограничить доступ из виртуальных машин PAYG RHEL, убедитесь, что разрешены следующие IP-адреса hello `yum update` toowork в зависимости от того, находятся в среде hello. 

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

### <a name="manual-update-procedure-toouse-hello-new-azure-rhui-servers"></a>Ручное обновление процедуры toouse hello новых Azure RHUI серверов
Подпись открытого ключа загрузки (с помощью перелистывание) hello

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

Проверьте ключ загружаются hello

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

Проверьте выходные данные hello, проверьте `keyid` и `user ID packet`:

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

Установка hello открытого ключа

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

Загрузите, проверьте и установите RPM клиента

Загрузка для RHEL 6

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

Для RHEL 7

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

Проверка.

```bash
rpm -Kv azureclient.rpm
```

Проверьте в выходных данных этой подписью hello пакета — ОК

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

Установка hello об/мин

```bash
sudo rpm -U azureclient.rpm
```

По завершении убедитесь, что можно доступ hello Azure RHUI формы виртуальной Машины

### <a name="all-in-one-script-for-automating-hello-preceding-task"></a>В одном скрипт для автоматизации hello предшествующей задачи
Используйте следующий сценарий как задачу hello tooautomate необходимые обновления затронутые виртуальные машины toohello новых Azure RHUI серверов hello.

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

## <a name="rhui-overview"></a>Обзор RHUI
[Инфраструктура обновления Red Hat](https://access.redhat.com/products/red-hat-update-infrastructure) обеспечивает масштабируемое решение toomanage yum репозиторий контента для экземпляров облачной Red Hat Enterprise Linux, размещенные на поставщиков облачных Сертифицировано Red Hat. На основе hello вышестоящего отделение проекта, RHUI позволяет поставщиков облачных служб контента репозитория, размещенных в Red Hat зеркальной toolocally, создайте пользовательские репозитории своим содержимым и сделать эти репозиториев tooa доступных большой группе конечным пользователям через балансировкой нагрузки система содержимого доставки.

## <a name="regions-where-rhui-is-available"></a>Регионы, в которых доступна инфраструктура RHUI
Инфраструктура RHUI поддерживается во всех регионах, где доступны предоставляемые по запросу образы RHEL. В настоящее время он включает все открытые регионах, перечисленных на hello [панель мониторинга Azure status](https://azure.microsoft.com/status/) страницы области правительства США и Германии Azure. Доступ к RHUI для виртуальных машин, развернутых из предоставляемых по запросу образов RHEL, входит в стоимость образа. Дополнительные облачные региональные и национальные доступности будет обновляться планируем RHEL доступности по требованию в будущем hello.

> [!NOTE]
> Размещенное tooAzure RHUI доступа является ограниченной toohello ВМ в [Microsoft Azure Datacenter, IP-диапазонов](https://www.microsoft.com/download/details.aspx?id=41653).
> 
> 

## <a name="get-updates-from-another-update-repository"></a>Получение обновлений из другого репозитория обновлений
Если вам требуется tooget обновлений из репозитория (а не размещенной в Azure RHUI) различные обновления, сначала необходимо toounregister своих экземпляров из RHUI. Необходимо зарегистрировать toore с hello нужные обновления инфраструктуры (например, Red Hat вспомогательные или клиента портал Red Hat CDN). Кроме того, необходима подписка Red Hat для этих служб и регистрация [Red Hat Cloud Access в Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).

toounregister RHUI и инфраструктура обновления повторно зарегистрируйте tooyour выполните следующие действия.

1. Измените /etc/yum.repos.d/rh-cloud.repo, все `enabled=1` слишком`enabled=0`. Например:
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. Измените /etc/yum/pluginconf.d/rhnplugin.conf, `enabled=0` слишком`enabled=1`.
3. Затем зарегистрируйте hello требуемой инфраструктуры, например клиентский портал Red Hat. Выполните Red Hat решение руководства на [как tooregister и подписка системы toohello клиентский портал Red Hat](https://access.redhat.com/solutions/253273).

> [!NOTE]
> Доступ toohello RHUI, размещенной в Azure включается в цены изображения hello RHEL Оплата по мере использования (PAYG). При отмене регистрации виртуальную Машину RHEL PAYG hello RHUI, размещенной в Azure не выполняется преобразование hello виртуальной машины в тип перевести--владельцем-лицензии (BYOL) виртуальной Машины. При регистрации hello одной виртуальной Машины с другим источником обновления может несения двойные расходов: сначала по времени для сбора Azure RHEL программного обеспечения и hello второй раз для Red Hat подписок. 
> 
> Если необходимо постоянно toouse инфраструктуры обновления, кроме RHUI, размещенной в Azure рекомендуется создание и развертывание собственных изображений (BYOL-type), как описано в [Создание и отправка Red Hat виртуальной машины для Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) статьи.
> 

## <a name="next-steps"></a>Дальнейшие действия
Red Hat Enterprise Linux виртуальной Машины из образа Azure Marketplace Оплата по мере использования и коэффициент размещенной в Azure RHUI toocreate go слишком[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/). Можно будет toouse `yum update` в вашем экземпляре RHEL без дополнительных настроек.

