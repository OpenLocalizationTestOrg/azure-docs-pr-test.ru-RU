---
title: "aaaUsing внутренние DNS для виртуальной Машины имен в Azure | Документы Microsoft"
description: "Использование внутренней службы DNS для разрешения имен виртуальных машин в Azure."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: 94fd6577aa51ce5db4dc26649b415ddeeb410eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a>Использование внутренней службы DNS для разрешения имен виртуальных машин в Azure

В этой статье показано, как tooset статические внутренние DNS имена виртуальных машин Linux с использованием карт виртуального сетевого Адаптера (VNic) и метка DNS-имена. Статические имена DNS используются для постоянных инфраструктурных служб, таких как сервер сборки Jenkins, который используется для этого поддержания документа, или сервер Git.

Существуют следующие требования Hello.

* [учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/);
* [файлы открытого и закрытого ключа SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI
Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

- [Azure CLI 1.0](#quick-commands) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления


## <a name="quick-commands"></a>Быстрые команды

Если вам требуется tooquickly выполнения задачи hello, hello в следующем разделе подробно описываются hello команд, которые необходимы. Более подробные сведения и контекста, для каждого шага можно найти hello остальной части документа hello [начиная здесь](#detailed-walkthrough).  

Предварительные требования: группа ресурсов, виртуальная сеть, группа безопасности сети с входящим трафиком SSH, подсеть.

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a>Создание виртуального сетевого адаптера со статическим внутренним именем DNS

Hello `-r` cli флаг предназначен для параметра hello DNS метку, которую предоставляет hello статических DNS-имя для hello виртуального сетевого адаптера.

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-hello-vm-into-hello-vnet-nsg-and-connect-hello-vnic"></a>Развертывание hello виртуальной Машины в hello виртуальной сети, NSG и подключения hello виртуального сетевого адаптера

Hello `-N` подключается hello виртуального сетевого адаптера toohello новой виртуальной Машины во время развертывания tooAzure hello.

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a>Подробное пошаговое руководство

Полная непрерывной интеграции и непрерывного развертывания (CiCd) инфраструктуру в Azure требует определенных серверов toobe статической или долгоживущие серверов.  Рекомендуется, активов Azure как hello виртуальных сетей (Vnet) и группы безопасности сети (Nsg), должен быть статическим и долго ресурсы, которые развертываются редко.  После развертывания виртуальной сети, он может быть использован в новые развертывания без инфраструктуры toohello любой негативно влияет на.  Добавление статического сети toothis Git репозитория сервер и сервер автоматизации Jenkins доставляет CiCd tooyour средах разработки и тестирования.  

Внутренние имена DNS можно сопоставлять только внутри виртуальной сети Azure.  Так как hello DNS-имена являются внутренними, они не удается разрешить toohello за пределами Интернет, обеспечивая дополнительную безопасность инфраструктуры toohello.

_Замените все примеры своими именами._

## <a name="create-hello-resource-group"></a>Создать группу ресурсов hello

Группа ресурсов находится необходимые tooorganize все, что мы создадим в этом пошаговом руководстве.  Дополнительные сведения о группах ресурсов см. в статье [Общие сведения об Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-hello-vnet"></a>Создать hello виртуальной сети

Hello первым шагом является toobuild виртуальных машин в hello toolaunch виртуальной сети.  Hello виртуальная сеть содержит одну подсеть для этого пошагового руководства.  Дополнительные сведения о виртуальных сетях Azure см. в разделе [Создание виртуальной сети с помощью hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-hello-nsg"></a>Создать hello NSG

Hello подсети создана за существующей сетевой группы безопасности, поэтому мы создаем hello NSG перед hello подсети.  Nsg Azure — это эквивалент tooa брандмауэра на уровне сети hello.  Дополнительные сведения о Nsg Azure см. в разделе [как Nsg toocreate в hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Добавление правила, разрешающего входящий трафик по протоколу SSH

Hello ВМ Linux требуется доступ из hello необходима Интернета, переданной правило, разрешающее трафик 22 toobe входящий порт на виртуальной Машине Linux hello tooport сети hello 22.

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a>Добавить toohello подсети виртуальной сети

Виртуальные машины в виртуальной сети hello должна находиться в подсети.  Каждая виртуальная сеть может содержать несколько подсетей.  Создать подсеть hello и свяжите с tooadd NSG hello подсети toohello брандмауэра hello подсеть.

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

Теперь Hello подсети добавляется внутри hello виртуальной сети и связанные с hello NSG и правила NSG hello.

## <a name="creating-static-dns-names"></a>Создание статических DNS-имен

Azure является более гибким, но toouse DNS-имен для разрешения имен виртуальных машин, необходимо их как виртуальные сетевые карты (VNics) с помощью DNS пометки toocreate.  VNics являются важными, как можно повторно использовать их, подключив их toodifferent ВМ, поддерживающий hello виртуального сетевого адаптера как статический ресурс hello виртуальных машин может быть временной.  С помощью DNS, метки на hello виртуального сетевого адаптера, не может tooenable простое имя разрешения из других виртуальных машин в виртуальной сети hello.  С помощью разрешения имен включает другие виртуальные машины сервера автоматизации hello tooaccess hello DNS-именем `Jenkins` или сервера hello Git в качестве `gitrepo`.  Создание виртуального сетевого адаптера и связать его с hello подсети, созданного в предыдущем шаге hello.

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Развертывание hello виртуальной Машины в виртуальной сети hello и NSG

Теперь у нас есть виртуальной сети, подсети в этой виртуальной сети и NSG выступает в роли tooprotect брандмауэра нашей подсети, блокируя весь входящий трафик, за исключением порт 22 для SSH.  Теперь может быть развернут Hello виртуальной Машины внутри этой существующей сетевой инфраструктуре.

С помощью Azure CLI hello и hello `azure vm create` команды hello виртуальных Машин Linux — развернутой toohello существующие группы ресурсов Azure, виртуальной сети, подсети и виртуального сетевого адаптера.  Дополнительные сведения об использовании toodeploy CLI hello завершения виртуальной Машины в разделе [создать полную среду Linux с помощью hello Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

С помощью hello CLI флаги toocall существующие ресурсы мы поручить Azure toodeploy hello виртуальных Машин в существующей сети hello.  tooreiterate, после развертывания виртуальной сети и подсети они могут остаться статические или постоянным ресурсов в ваш регион Azure.  

## <a name="next-steps"></a>Дальнейшие действия
* [Создание полной среды Linux с помощью интерфейса командной строки Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Создание виртуальной машины Linux с помощью шаблона Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
