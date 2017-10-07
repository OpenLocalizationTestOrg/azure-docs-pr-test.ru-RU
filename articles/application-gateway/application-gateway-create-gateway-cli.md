---
title: "aaaCreate шлюза приложения Azure - CLI Azure 2.0 | Документы Microsoft"
description: "Узнайте, как toocreate шлюза с помощью приложения hello Azure CLI 2.0 в диспетчере ресурсов"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 952065586cd87d253882438bb779b768d9fd59fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli-20"></a>Создание шлюза приложения с помощью Azure CLI 2.0 hello

> [!div class="op_single_selector"]
> * [Портал Azure](application-gateway-create-gateway-portal.md)
> * [PowerShell и диспетчер ресурсов Azure](application-gateway-create-gateway-arm.md)
> * [Классическая модель — Azure PowerShell](application-gateway-create-gateway.md)
> * [Шаблон Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI 1.0](application-gateway-create-gateway-cli.md)
> * [Azure CLI 2.0](application-gateway-create-gateway-cli.md)

Шлюз приложений — это выделенный виртуальный модуль, предоставляющий контроллер доставки приложений (ADC) как услугу, который обеспечивает для приложения множество функций балансировки нагрузки уровня 7.

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI

Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

* [Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) -нашей CLI для hello классический и ресурса управления развертывания моделей.
* [Azure CLI 2.0](application-gateway-create-gateway-cli.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления

## <a name="prerequisite-install-hello-azure-cli-20"></a>Необходимое условие: Установите hello Azure CLI 2.0

tooperform hello шаги в этой статье, вы должны слишком[Установка hello интерфейса командной строки Azure для Mac, Linux и Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

> [!NOTE]
> Если у вас нет учетной записи Azure, то вам потребуется получить ее. Зарегистрируйтесь, чтобы получить [бесплатную пробную версию](../active-directory/sign-up-organization.md).

## <a name="scenario"></a>Сценарий

В этом сценарии вы узнаете, как шлюз приложения с помощью toocreate hello портал Azure.

Вы узнаете:

* как создать средний шлюз приложений с двумя экземплярами;
* как создать виртуальную сеть AdatumAppGatewayVNET с зарезервированным блоком CIDR (10.0.0.0/16);
* как создать подсеть с именем Appgatewaysubnet и блоком CIDR (10.0.0.0/28);

> [!NOTE]
> Дополнительная настройка шлюза приложения hello, включая пользовательские работоспособности проверяет, пул адресов серверной части и дополнительные правила настраиваются после настройки шлюза приложения hello, а не во время первоначального развертывания.

## <a name="before-you-begin"></a>Перед началом работы

Шлюзу приложений Azure требуется собственная подсеть. При создании виртуальной сети, убедитесь, оставьте достаточно toohave пространства адресов несколько подсетей. После развертывания приложения шлюза tooa подсети шлюзы только дополнительное приложение можно добавить toohello подсети.

## <a name="log-in-tooazure"></a>Войдите в tooAzure

Откройте hello **командной строки пакета Microsoft Azure**и войдите в систему. 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> Можно также использовать `az login` без ключа hello для входа устройство, которое требуется ввод кода на aka.ms/devicelogin.

После ввода предшествующий пример hello предоставляется код. Перейдите toohttps://aka.ms/devicelogin в процессе входа hello toocontinue браузера.

![Команда, выводящая имя пользователя устройства][1]

В браузере hello введите полученный код hello. Все перенаправленные tooa-на страницу входа.

![Код tooenter браузера][2]

После ввода кода hello вы войдете в toocontinue hello закрыть браузер на со сценарием hello.

![Вход выполнен][3]

## <a name="create-hello-resource-group"></a>Создать группу ресурсов hello

Перед созданием шлюза приложения hello, шлюз приложения hello toocontain создания группы ресурсов. Hello ниже показана команда hello.

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-hello-application-gateway"></a>Создание шлюза приложения hello

IP-адреса Hello для внутренних hello — hello IP-адреса для сервера базы данных. Эти значения могут быть либо частных IP-адресов в виртуальной сети hello, общедоступные IP-адреса или полные доменные имена для внутренних серверов. Hello пример создает шлюза приложения с дополнительными параметрами конфигурации для настройки http, порты и правил.

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet" \
--subnet-address-prefix "10.0.0.0/28" \
--servers 10.0.0.4 10.0.0.5 \
--capacity 2 \
--sku Standard_Small \
--http-settings-cookie-based-affinity Enabled \
--http-settings-protocol Http \
--frontend-port 80 \
--routing-rule-type Basic \
--http-settings-port 80 \
--public-ip-address "pip2" \
--public-ip-address-allocation "dynamic" \

```

Hello выше примере многие свойства, которые не требуются во время создания шлюза приложения hello. Следующий пример кода Hello создает шлюза приложения hello необходимые сведения.

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet \
--subnet-address-prefix "10.0.0.0/28" \
--servers "10.0.0.5"  \
--public-ip-address pip
```
 
> [!NOTE]
> Список параметров, которые могут быть предоставлены во время создания запуска hello следующую команду: `az network application-gateway create --help`.

Этот пример создает шлюз простое приложение с параметрами по умолчанию для прослушивателя hello, внутреннего пула, параметров серверного http и правил. Вы можете изменить эти параметры toosuit развертывания после успешной подготовки hello.
Балансировка нагрузки начинается при наличии веб-приложения с внутреннего пула hello в предыдущих шагах, после ее создания, hello.

## <a name="get-application-gateway-dns-name"></a>Получение DNS-имени шлюза приложений

После создания шлюза hello hello следующим шагом является tooconfigure hello внешнего интерфейса для обмена данными. Если вы используете общедоступный IP-адрес, шлюзу приложений требуется динамически назначаемое непонятное имя DNS. tooensure конечным пользователям возможность нажать шлюза приложения hello, запись CNAME может быть используется toopoint toohello общедоступную конечную точку шлюза приложения hello. [Настройка пользовательского имени домена в Azure](../dns/dns-custom-domain.md). tooconfigure псевдоним, получить сведения о шлюза приложения hello и соответствующее IP или DNS-имя с помощью шлюза hello PublicIPAddress элемент toohello подключенных приложений. шлюз приложения Hello DNS-имя должно быть используется toocreate запись CNAME, какие точки hello двух web приложений toothis DNS-имя. Использование Hello записи A не рекомендуется, поскольку hello виртуального IP-адреса могут изменяться при перезагрузке шлюз приложений.


```azurecli-interactive
az network public-ip show --name "pip" --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="delete-all-resources"></a>Удаление всех ресурсов

toodelete все ресурсы, которые созданы в этой статье завершения hello, следующие шаги:

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как пользовательские работоспособности toocreate проверяет, посетив [пробу пользовательского состояния](application-gateway-create-probe-portal.md)

Узнайте, как tooconfigure разгрузки SSL и дешифрования SSL дорогостоящих take hello off веб-серверов, посетив [Настройка разгрузки SSL](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
