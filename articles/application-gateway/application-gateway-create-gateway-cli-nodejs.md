---
title: "aaaCreate шлюза приложения Azure - Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как toocreate шлюза с помощью приложения hello Azure CLI 1.0 в диспетчере ресурсов"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3c0d2d96b6be404d0372d00f0deb2a32959ca419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a>Создание шлюза приложения с помощью hello Azure CLI

> [!div class="op_single_selector"]
> * [Портал Azure](application-gateway-create-gateway-portal.md)
> * [PowerShell и диспетчер ресурсов Azure](application-gateway-create-gateway-arm.md)
> * [Классическая модель — Azure PowerShell](application-gateway-create-gateway.md)
> * [Шаблон Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI 1.0](application-gateway-create-gateway-cli.md)
> * [Azure CLI 2.0](application-gateway-create-gateway-cli.md)
> 
> 

Шлюз приложений — это балансировщик нагрузки уровня 7. Он обеспечивает отработку отказа, маршрутизации производительности HTTP-запросы между различными серверами, являются ли они на hello облачной или локальной. Шлюз приложений имеет следующие возможности доставки приложения hello: HTTP загрузить пробы пользовательских работоспособности балансировки, сходство сеансов на основе файлов cookie и разгрузки Secure Sockets Layer (SSL) и поддержка нескольких сайтов.

## <a name="prerequisite-install-hello-azure-cli"></a>Необходимое условие: Установите hello Azure CLI

tooperform hello шаги в этой статье, вы должны слишком[Установка hello интерфейса командной строки Azure для Mac, Linux и Windows (Azure CLI)](../xplat-cli-install.md) и необходимо слишком[вход tooAzure](../xplat-cli-connect.md). 

> [!NOTE]
> Если у вас нет учетной записи Azure, то вам потребуется получить ее. Зарегистрируйтесь, чтобы получить [бесплатную пробную версию](../active-directory/sign-up-organization.md).

## <a name="scenario"></a>Сценарий

В этом сценарии вы узнаете, как шлюз приложения с помощью toocreate hello портал Azure.

Вы узнаете:

* как создать средний шлюз приложений с двумя экземплярами;
* как создать виртуальную сеть ContosoVNET с зарезервированным блоком CIDR (10.0.0.0/16);
* как создать подсеть subnet01 с блоком CIDR (10.0.0.0/28).

> [!NOTE]
> Дополнительная настройка шлюза приложения hello, включая пользовательские работоспособности проверяет, пул адресов серверной части и дополнительные правила настраиваются после настройки шлюза приложения hello, а не во время первоначального развертывания.

## <a name="before-you-begin"></a>Перед началом работы

Шлюзу приложений Azure требуется собственная подсеть. При создании виртуальной сети, убедитесь, оставьте достаточно toohave пространства адресов несколько подсетей. После развертывания приложения шлюза tooa подсети шлюзы только дополнительных приложений, могут toobe добавлены toohello подсети.

## <a name="log-in-tooazure"></a>Войдите в tooAzure

Откройте hello **командной строки пакета Microsoft Azure**и войдите в систему. 

```azurecli-interactive
azure login
```

После ввода предшествующий пример hello предоставляется код. Перейдите toohttps://aka.ms/devicelogin в процессе входа hello toocontinue браузера.

![Команда, выводящая имя пользователя устройства][1]

В браузере hello введите полученный код hello. Все перенаправленные tooa-на страницу входа.

![Код tooenter браузера][2]

После ввода кода hello вы войдете в toocontinue hello закрыть браузер на со сценарием hello.

![Вход выполнен][3]

## <a name="switch-tooresource-manager-mode"></a>Переключение режима диспетчера tooResource

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a>Создать группу ресурсов hello

Перед созданием шлюза приложения hello, шлюз приложения hello toocontain создания группы ресурсов. Hello ниже показана команда hello.

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a>Создать виртуальную сеть

После создания группы ресурсов hello виртуальной сети создается для шлюза приложения hello.  В следующем примере hello hello адресное пространство было как 10.0.0.0/16 как это определено в hello предшествующий сценарий заметки.

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a>Создание подсети

После создания виртуальной сети hello подсети добавляется для шлюза приложения hello.  Если планируется toouse шлюз приложения с веб-приложения размещенного в hello же виртуальной сети как шлюз приложения hello, быть достаточно места для другой подсети, что tooleave.

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a>Создание шлюза приложения hello

После создания hello виртуальную сеть и подсеть hello необходимые компоненты для шлюза приложения hello являются полными. Кроме того, ранее экспортированный PFX-файл сертификата и hello пароль для сертификата hello требуются для hello, следующий шаг: hello IP-адреса, используемые для внутреннего hello — hello IP-адреса для сервера базы данных. Эти значения могут быть либо частных IP-адресов в виртуальной сети hello, общедоступные IP-адреса или полные доменные имена для внутренних серверов.

```azurecli-interactive
azure network application-gateway create \
--name AdatumAppGateway \
--location eastus \
--resource-group ContosoRG \
--vnet-name ContosoVNET \
--subnet-name subnet01 \
--servers 134.170.185.46,134.170.188.221,134.170.185.50 \
--capacity 2 \
--sku-tier Standard \
--routing-rule-type Basic \
--frontend-port 80 \
--http-settings-cookie-based-affinity Enabled \
--http-settings-port 80 \
--http-settings-protocol http \
--frontend-port http \
--sku-name Standard_Medium
```

> [!NOTE]
> Список параметров, которые могут быть предоставлены во время создания, запуска hello следующую команду: **создать шлюз приложений сеть azure — помочь**.

Этот пример создает шлюз простое приложение с параметрами по умолчанию для прослушивателя hello, внутреннего пула, параметров серверного http и правил. Вы можете изменить эти параметры toosuit развертывания после успешной подготовки hello.
Балансировка нагрузки начинается при наличии веб-приложения с внутреннего пула hello в предыдущих шагах, после ее создания, hello.

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как пользовательские работоспособности toocreate проверяет, посетив [пробу пользовательского состояния](application-gateway-create-probe-portal.md)

Узнайте, как tooconfigure разгрузки SSL и дешифрования SSL дорогостоящих take hello off веб-серверов, посетив [Настройка разгрузки SSL](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
