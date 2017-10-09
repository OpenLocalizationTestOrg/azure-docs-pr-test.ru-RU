---
title: "Фильтр пакетов aaaUse FreeBSD toocreate брандмауэра в Azure | Документы Microsoft"
description: "Узнайте, как toodeploy NAT брандмауэра с помощью элемента FreeBSD PF в Azure."
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/20/2017
ms.author: kyliel
ms.openlocfilehash: 3d3a5dde2ca03ba6fc384581c786f5eb746e6d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-freebsds-packet-filter-toocreate-a-secure-firewall-in-azure"></a>Как фильтр пакетов toouse FreeBSD toocreate безопасный брандмауэр в Azure
В этой статье описаны как toodeploy брандмауэра NAT с помощью фильтра FreeBSD Packer через шаблона Azure Resource Manager для общих веб-сервере сценарий.

## <a name="what-is-pf"></a>Что такое PF?
PF — это лицензированный (по лицензии BSD) фильтр пакетов с отслеживанием состояния, а также основной элемент программного обеспечения для брандмауэра. Фильтр пакетов получил широкое распространение, так как он обладает рядом преимуществ по сравнению с другими доступными брандмауэрами. Преобразование сетевых адресов (NAT) находится в общей папки с момента первого дня, а затем планировщик пакетов и активной очереди управления были включены в PF, благодаря интеграции hello ALTQ и сделав его можно настроить через PF элемента конфигурации. Функции, например pfsync и CARP для перехода на другой ресурс и избыточности, authpf для сеанса проверки подлинности и ftp прокси tooease полезных hello сложно протокол FTP, также расширена PF. Короче говоря, PF — это брандмауэр с расширенными возможностями. 

## <a name="get-started"></a>Начало работы
Если вы заинтересованы в настройке безопасный брандмауэр в облаке hello для веб-серверов, а затем давайте начнем. Можно также применить hello скриптов, используемых в этой tooset шаблона диспетчера ресурсов Azure копирование топологии сети.
Настройка виртуальной машины FreeBSD шаблона Azure Resource Manager Hello, выполняющего /redirection NAT с помощью PF и две виртуальные машины FreeBSD с веб-сервер Nginx hello установлен и настроен. В дополнение к этому tooperforming NAT для двух веб-серверов hello входящего трафика, hello NAT или перенаправление виртуальной машины перехватывает HTTP-запросы и перенаправлять их toohello два веб-сервера в режиме циклического перебора. Hello виртуальной сети использует hello закрытый немаршрутизируемый IP адрес места 10.0.0.2/24 и можно изменить параметры hello hello шаблона. шаблон диспетчера ресурсов Azure Hello также определяет таблицы маршрутов для всей виртуальной сети, которая представляет собой набор отдельных маршрутов используется toooverride Azure по умолчанию маршрутов, зависимости IP-адрес назначения hello hello. 

![pf_topology](./media/freebsd-pf-nat/pf_topology.jpg)
    
### <a name="deploy-through-azure-cli"></a>Развертывание с помощью Azure CLI
Hello требуется последняя версия [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login). Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create). Hello следующий пример создает имя группы ресурсов `myResourceGroup` в hello `West US` расположение.

```azurecli
az group create --name myResourceGroup --location westus
```

Затем разверните шаблон hello [pf freebsd программа установки](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup) с [создания развертывания группы az](/cli/azure/group/deployment#create). Загрузить [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/pf-freebsd-setup/azuredeploy.parameters.json) в разделе hello же пути и определять собственные значения ресурсов, такие как `adminPassword`, `networkPrefix`, и `domainNamePrefix`. 

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeploymentName \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/pf-freebsd-setup/azuredeploy.json \
    --parameters '@azuredeploy.parameters.json' --verbose
```

После около пяти минут, вы получите сведения hello `"provisioningState": "Succeeded"`. Затем вы можете ssh переднего плана toohello виртуальной Машины (NAT) или получить доступ к веб-сервер Nginx в браузере, используя hello общедоступный IP-адрес или полное доменное имя сервера переднего плана hello виртуальной Машины (NAT). Hello следующий пример выводит полное доменное имя и общедоступный IP-адрес, назначенный переднего плана toohello виртуальной Машины (NAT) в hello `myResourceGroup` группы ресурсов. 

```azurecli
az network public-ip list --resource-group myResourceGroup
```
    
## <a name="next-steps"></a>Дальнейшие действия
Вы хотите tooset копирование NAT в Azure? используя бесплатное и эффективное средство с открытым кодом, PF отлично подходит для этого. С помощью шаблона hello [pf freebsd программа установки](https://github.com/Azure/azure-quickstart-templates/tree/master/pf-freebsd-setup), достаточно tooset пять минут брандмауэра NAT с циклическим балансировки с помощью элемента FreeBSD PF в Azure для общих веб-сервере сценарий. 

Если требуется поддержка hello toolearn FreeBSD в Azure, см. слишком[tooFreeBSD введение в Azure](freebsd-intro-on-azure.md).

Дополнительные сведения о PF tooknow следует ссылаться слишком[по Intel FreeBSD](https://www.freebsd.org/doc/handbook/firewalls-pf.html) или [PF-руководство пользователя](https://www.freebsd.org/doc/handbook/firewalls-pf.html).
