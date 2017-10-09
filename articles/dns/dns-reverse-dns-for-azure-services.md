---
title: "aaaReverse DNS для служб Azure | Документы Microsoft"
description: "Узнайте, как tooconfigure обратный просмотр DNS для служб, размещенных в Azure"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: c6fe1d80232f124be86dd7fc57abc20699be7eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a>Настройка обратного просмотра DNS для размещенных в Azure служб

В этой статье объясняется, как tooconfigure обратный просмотр DNS для служб, размещенных в Azure.

Службы в Azure используют IP-адреса, присвоенные им службой Azure и являющиеся собственностью Майкрософт. Эти обратной записи DNS (PTR-записей) должны создаваться в hello соответствующего корпорации Майкрософт зоны обратного просмотра DNS уточняющего запроса. В этой статье объясняется, как toodo это.

Этот сценарий не следует путать с возможностью hello слишком[размещения hello зоны обратного просмотра DNS подстановки для назначенных диапазонов IP-в Azure DNS](dns-reverse-dns-hosting.md). В этом случае hello диапазоны IP-адресов, представленный зоны обратного просмотра hello должны быть назначены организации tooyour обычно поставщиком услуг Интернета.

Перед прочтением этой статьи ознакомьтесь со статьей [Основные сведения об обратной зоне DNS и ее поддержке в Azure](dns-reverse-dns-overview.md).

В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).
* В модели развертывания диспетчера ресурсов hello вычислительных ресурсов (например, виртуальные машины, наборы масштабирования виртуальных машин или кластеров Service Fabric) предоставляются через ресурсов PublicIpAddress. Обратный поиск DNS настраиваются с помощью свойства «ReverseFqdn» hello hello PublicIpAddress.
* В hello классической модели развертывания вычислительные ресурсы предоставляются с помощью облачных служб. Обратный поиск DNS настраиваются с помощью свойства «ReverseDnsFqdn» hello hello облачной службы.

Обратного DNS для hello службе приложений Azure в настоящее время не поддерживается.

## <a name="validation-of-reverse-dns-records"></a>Проверка записей обратной зоны DNS

Сторонних производителей не должно быть возможности toocreate обратного DNS-записи для их доменов DNS tooyour сопоставления службы Azure. tooprevent, Azure позволяет только создание hello обратную запись DNS, где — имя домена, указанное в записи DNS обратного hello hello таким же, как или автоматически преобразуется в hello DNS-имя или IP-адрес PublicIpAddress или облачной службы в hello же подписки Azure.

Эта проверка выполняется только при установке или изменить hello обратную запись DNS. Периодическая повторная проверка не выполняется.

Пример: предположим, что hello PublicIpAddress ресурсов имеет имя contosoapp1.northus.cloudapp.azure.com hello DNS и IP-адрес 23.96.52.53. Hello ReverseFqdn hello PublicIpAddress могут быть указаны как:
* имя DNS Hello hello PublicIpAddress, contosoapp1.northus.cloudapp.azure.com
* Hello DNS-имен для разных PublicIpAddress в hello же подписку, такую как contosoapp2.westus.cloudapp.azure.com
* Именного DNS-имен, например app1.contoso.com, при условии, что это имя является *первый* настроен в качестве CNAME toocontosoapp1.northus.cloudapp.azure.com или tooa другой PublicIpAddress в hello одной подписке.
* Именного DNS-имен, например app1.contoso.com, при условии, что это имя является *первый* настроен в качестве значения записи toohello IP-адрес 23.96.52.53 или toohello IP-адрес другой PublicIpAddress в hello одной подписке.

Hello и те же ограничения применяются tooreverse DNS для облачных служб.


## <a name="reverse-dns-for-publicipaddress-resources"></a>Обратная зона DNS для ресурсов PublicIpAddress

В этом разделе приведены подробные инструкции как tooconfigure обратный поиск DNS для ресурсов PublicIpAddress в модели развертывания диспетчера ресурсов hello, с помощью Azure PowerShell, CLI Azure 1.0 или Azure CLI 2.0. Настройка обратного DNS для ресурсов PublicIpAddress не поддерживается в настоящее время через портал Azure hello.

Сейчас Azure поддерживает обратную зону DNS только для IPv4-ресурсов PublicIpAddress. Для IPv6 эта возможность не поддерживается.

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a>Добавление обратного tooan DNS существующих общедоступных

#### <a name="powershell"></a>PowerShell

tooadd существующие PublicIpAddress обратного tooan DNS:

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

tooadd обратную DNS tooan существующие PublicIpAddress, в котором еще нет DNS-имя, необходимо также указать DNS-имя:

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

tooadd существующие PublicIpAddress обратного tooan DNS:

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

tooadd обратную DNS tooan существующие PublicIpAddress, в котором еще нет DNS-имя, необходимо также указать DNS-имя:

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

tooadd существующие PublicIpAddress обратного tooan DNS:

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

tooadd обратную DNS tooan существующие PublicIpAddress, в котором еще нет DNS-имя, необходимо также указать DNS-имя:

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a>Создание общедоступного IP-адреса с обратной зоной DNS

toocreate новый PublicIpAddress с hello свойство обратного DNS уже задан:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a>Просмотр обратной зоны DNS в существующем ресурсе PublicIpAddress

tooview hello значение, настроенное для существующего PublicIpAddress:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a>Удаление обратной зоны DNS из существующих общедоступных IP-адресов

tooremove обратного DNS свойство из существующего PublicIpAddress:

#### <a name="powershell"></a>PowerShell

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a>Настройка обратной зоны DNS для облачных служб

В этом разделе приведены подробные инструкции как tooconfigure обратный поиск DNS для облачных служб в hello классической модели развертывания с помощью Azure PowerShell. Настройка обратного DNS для облачных служб не поддерживается через hello портал Azure, Azure CLI 1.0 или Azure CLI 2.0.

### <a name="add-reverse-dns-tooexisting-cloud-services"></a>Добавление обратного DNS tooexisting облачные службы

tooadd обратного DNS записи tooan существующей облачной службы:

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a>Создание облачной службы с обратной зоной DNS

toocreate новую облачную службу с hello свойство обратного DNS уже задан:

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a>Просмотр обратной зоны DNS в существующих облачных службах

tooview hello обратного DNS свойство для существующей облачной службы:

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a>Удаление обратной зоны DNS из существующих облачных служб

tooremove обратного DNS свойства из существующей облачной службы:

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a>Часто задаваемые вопросы

### <a name="how-much-do-reverse-dns-records-cost"></a>Сколько стоит обратная зона DNS?

Она бесплатна!  Никакие дополнительные затраты на записи или запросы обратной зоны DNS не требуются.

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a>Будет Мой обратной записи разрешения DNS из hello Интернет?

Да. После свойство hello обратного DNS для службы Azure, Azure управляет всем делегирования DNS hello и зон DNS требуемые разрешает tooensure, обратная запись DNS для всех пользователей.

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a>Создаются ли для моих служб Azure какие-то стандартные записи обратной зоны DNS?

Нет. Обратная зона DNS — это подключаемая возможность. По умолчанию создаются обратной записи DNS, при выборе не tooconfigure их.

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a>Что такое формат hello hello полное доменное имя (FQDN)

Полные доменные имена указываются в прямом порядке и должны завершаться точкой (например, app1.contoso.com.).

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a>Что произойдет, если проверка hello для hello обратный поиск DNS, я указал завершается ошибкой?

Где hello обратного DNS неудачной проверки hello операции tooconfigure hello обратную запись DNS не выполняется. Исправьте значение обратного DNS hello при необходимости и повторите попытку.

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a>Можно ли настроить обратную зону DNS для службы приложений Azure?

Нет. Обратного DNS не поддерживается для hello службе приложений Azure.

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a>Можно ли настроить несколько записей обратной зоны DNS для моей службы Azure?

Нет. В Azure поддерживается только одна запись обратной зоны DNS для каждой облачной службы Azure или каждого ресурса PublicIpAddress.

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a>Можно ли настроить обратную зону DNS для IPv6-ресурсов PublicIpAddress?

Нет. Сейчас Azure поддерживает обратную зону DNS только для облачных служб и IPv4-ресурсов PublicIpAddress.

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a>Можно отправлять сообщения электронной почты tooexternal домены из службы вычислений Azure?

Нет. [Службы вычислений Azure не поддерживают отправку сообщений электронной почты tooexternal доменов](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения см. [в статье Википедии об обратном просмотре DNS](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Узнайте, каким образом слишком[зоны обратного просмотра hello узла для диапазона IP, назначенной поставщика услуг Интернета в Azure DNS](dns-reverse-dns-for-azure-services.md).

