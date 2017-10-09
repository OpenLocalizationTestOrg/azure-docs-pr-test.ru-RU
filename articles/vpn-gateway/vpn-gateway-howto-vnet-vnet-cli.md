---
title: "Подключение виртуальной сети tooanother виртуальной сети: Azure CLI | Документы Microsoft"
description: "В этой статье описаны этапы настройки подключения между виртуальными сетями с помощью Azure Resource Manager и Azure CLI."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a>Настройка подключения VPN-шлюза между виртуальными сетями с помощью Azure CLI

В этой статье показано, как toocreate шлюза VPN-подключение между виртуальными сетями. Hello виртуальные сети могут находиться в Здравствуйте, или же в разных регионах, и из hello таким же или разных подписках. При подключении виртуальных сетей из разных подписок, подписки hello не обязательно toobe, связанный с hello того же клиента Active Directory. 

в этой статье инструкциям Hello применить toohello модели развертывания диспетчера ресурсов и использовать Azure CLI. Можно также создать этой конфигурации с помощью средства развертывания или модель развертывания, выбрав другой вариант из hello после списка.

> [!div class="op_single_selector"]
> * [Портал Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Интерфейс командной строки Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Портал Azure (классический)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Подключение с использованием разных моделей развертывания — портал Azure](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Подключение с использованием разных моделей развертывания — PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

Подключение виртуальной сети tooanother виртуальной сети (VNet-VNet) — примерно tooconnecting локального сайта виртуальной сети tooan расположения. Оба типа подключения используйте tooprovide шлюза VPN защищенный туннель, с помощью IPsec/IKE. Если ваш виртуальных сетей в hello совпадают, вы можете tooconsider подключаются с помощью Пиринг виртуальной сети. При пиринговой связи между виртуальными сетями VPN-шлюз не используется. Дополнительную информацию см. в статье [Пиринговая связь между виртуальными сетями](../virtual-network/virtual-network-peering-overview.md).

Подключение типа "виртуальная сеть — виртуальная сеть" можно комбинировать с многосайтовыми конфигурациями. Это дает возможность установления сетевых топологий, которые объединяют подключения между организациями с подключением между виртуальными сетями, как показано в hello, следующая схема:

![Сведения о подключениях](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <a name="why"></a>Зачем нужна связь между виртуальными сетями?

Вы можете tooconnect виртуальных сетей для hello следующих причин:

* **Межрегиональная географическая избыточность и географическое присутствие**

  * Вы можете настроить собственную георепликацию или синхронизацию с безопасной связью без прохождения трафика через конечные точки с выходом в Интернет.
  * С помощью Azure Load Balancer и диспетчера трафика можно настроить высокодоступную рабочую нагрузку с геоизбыточностью в нескольких регионах Azure. Важный пример — tooset копии SQL Always On с группами доступности, распределение по нескольким регионам Azure.
* **Региональные многоуровневые приложения с изоляцией или административной границей**

  * В пределах hello же регионе, можно настроить многоуровневые приложения с несколькими виртуальными сетями, которые соединены друг с другом, из-за tooisolation или требований администрирования.

Дополнительные сведения о подключениях к виртуальной сети для виртуальной сети см. в разделе hello [часто задаваемые вопросы о виртуальной сети для виртуальной сети](#faq) конце hello в этой статье.

### <a name="which-set-of-steps-should-i-use"></a>Каким инструкциям следовать?

В этой статье приведены два разных набора действий. Один набор шагов для [Здравствуйте, виртуальных сетей, которые находятся в одной подписке](#samesub), а другой — [виртуальных сетей, которые находятся в разных подписках](#difsub).

## <a name="samesub"></a>Подключение виртуальных сетей, которые в hello одной подписке

![Схема подключения между виртуальными сетями](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a>Перед началом работы

Прежде чем начать, установите последнюю версию hello hello команды CLI (2.0 или более поздней версии). Сведения об установке hello командах CLI см. в разделе [установить CLI Azure 2.0](/cli/azure/install-azure-cli).

### <a name="Plan"></a>Планирование диапазонов IP-адресов

В hello, выполнив действия мы создадим два виртуальных сетей вместе с их соответствующими шлюза подсетях и конфигурациях. Затем создадим VPN-подключение между hello двух виртуальных сетей. Это важные tooplan hello IP-адресов для настройки сети. Имейте в виду, необходимо убедиться в том, что ни один из диапазонов виртуальных сетей или диапазонов локальных сетей никак не перекрываются. В этих примерах мы не включаем DNS-сервер. Сведения о разрешении имен виртуальных машин см. в [этой статье](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Мы используем следующие значения в примерах hello hello:

**Значения для TestVNet1:**

* Имя виртуальной сети: TestVNet1
* Группа ресурсов: TestRG1
* Расположение: восточная часть США
* TestVNet1: 10.11.0.0/16 и 10.12.0.0/16
* FrontEnd: 10.11.0.0/24
* BackEnd: 10.12.0.0/24
* GatewaySubnet: 10.12.255.0/27
* Имя шлюза: VNet1GW
* Общедоступный IP-адрес: VNet1GWIP
* Тип VPN: RouteBased
* Подключение (1–4): VNet1toVNet4
* Подключение (1–5): VNet1toVNet5
* Тип подключения: VNet2VNet

**Значения для TestVNet4:**

* Имя виртуальной сети: TestVNet4
* TestVNet2: 10.41.0.0/16 и 10.42.0.0/16
* FrontEnd: 10.41.0.0/24
* BackEnd: 10.42.0.0/24
* GatewaySubnet: 10.42.255.0/27
* Группа ресурсов: TestRG4
* Расположение: Запад США
* Имя шлюза: VNet4GW
* Общедоступный IP-адрес: VNet4GWIP
* Тип VPN: RouteBased
* Подключение: VNet4toVNet1
* Тип подключения: VNet2VNet


### <a name="Connect"></a>Шаг 1 — подключить tooyour подписки

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <a name="TestVNet1"></a>Шаг 2. Создание и настройка TestVNet1

1. Создайте группу ресурсов.

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. Создание подсети TestVNet1 и hello для TestVNet1. Пример ниже создает виртуальная сеть TestVNet1 и подсеть FrontEnd.

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. Создание дополнительных адресного пространства для подсети hello серверной части. Обратите внимание, что на этом шаге мы задать оба hello адресное пространство, которая была создана ранее, дополнительное адресное пространство, что мы хотим tooadd hello. Это обусловлено hello [обновления виртуальной сети сети az](https://docs.microsoft.com/cli/azure/network/vnet#update) команда перезаписывает предыдущие параметры hello. Убедитесь, что toospecify все префиксов адресов hello при использовании этой команды.

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. Создайте подсеть hello серверной части.
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. Создайте подсеть шлюза hello. Обратите внимание, что в этой подсети шлюза hello с именем «GatewaySubnet». Это обязательное имя. В этом примере hello подсеть шлюза используется /27. Хотя возможных toocreate как /29 подсеть шлюза, рекомендуется создать подсеть большего размера, включающий несколько адресов, выбрав по крайней мере /28 или /27. Это позволит достаточно адреса tooaccommodate возможные дополнительные настройки, вы можете в hello будущих.

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. Запрос открытый IP-адрес toobe toohello выделенный шлюз, создаваемых для виртуальной сети. Обратите внимание, что hello AllocationMethod является динамической. Нельзя указать hello IP-адреса, которые должны toouse. Он служит шлюзом динамически выделяемый tooyour.

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. Создание шлюза виртуальной сети hello для TestVNet1. Для подключений типа VNet-to-VNet необходимо использовать тип VPN RouteBased. При выполнении этой команды, с помощью hello параметр «--no - wait», вы не видите любой отзыв или выходных данных. Hello параметр «--no - wait» позволяет toocreate шлюза hello в фоновом режиме hello. Это не означает шлюза VPN hello завершает создание немедленно. Создание шлюза часто занимает 45 минут или более, в зависимости от шлюза hello SKU, вы используете.

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="TestVNet4"></a>Шаг 3. Создание и настройка TestVNet4

1. Создайте группу ресурсов.

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. Создайте TestVNet4.

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. Создайте дополнительную подсеть для TestVNet4.

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. Создайте подсеть шлюза hello.

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. Запросите общедоступный IP-адрес.

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. Создание шлюза виртуальной сети TestVNet4 hello.

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="createconnect"></a>Шаг 4 — Создание подключений hello

Теперь у вас есть две виртуальные сети с VPN-шлюзами. Hello следующим шагом является toocreate подключения через шлюз VPN между шлюзами виртуальной сети hello. При использовании выше примерах hello шлюзов виртуальной сети находятся в разных группах ресурсов. Когда шлюзы находятся в разных группах ресурсов, требуется tooidentify и укажите hello идентификаторы ресурсов для всех шлюзов, при установке соединения. Если ваш виртуальных сетей в hello же группу ресурсов можно использовать hello [второй набор инструкций](#samerg) так, как идентификаторы ресурсов hello toospecify не требуется.

### <a name="diffrg"></a>tooconnect виртуальных сетей, которые находятся в разных группах ресурсов

1. Получите идентификатор ресурса из VNet1GW hello из вывода hello hello следующую команду:

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  В выходных данных hello найти hello «идентификатор:» строки. Hello значения внутри кавычек hello, необходимые toocreate hello соединения в следующем разделе hello. Скопируйте эти значения tooa текстовый редактор, например «Блокнот», чтобы их можно вставлять их при создании подключения.

  Выходные данные примера:

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  Скопируйте значения hello после **«id»:** в кавычки hello.

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. Получение hello VNet4GW из идентификатора ресурса и скопируйте hello значения tooa текстовый редактор.

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. Создание подключения tooTestVNet4 TestVNet1 hello. На этом этапе можно создать подключение hello TestVNet1 tooTestVNet4. Нет общего ключа, на который ссылается примеры hello. Можно использовать собственные значения для hello общего ключа. Важно, что это общий ключ, hello Hello оба соединения должны совпадать. Создание подключения занимает некоторое время toocomplete.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. Создание подключения tooTestVNet1 TestVNet4 hello. Этот шаг является аналогичные toohello показано выше, за исключением того, вы создаете подключение hello из TestVNet4 tooTestVNet1. Убедитесь, что hello общие ключи совпадают. Подключение hello tooestablish он занимает несколько минут.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. Проверьте подключения. Дополнительные сведения см. в разделе [Проверка подключений](#verify).

### <a name="samerg"></a>tooconnect виртуальных сетей, в котором hello же группу ресурсов

1. Создание подключения tooTestVNet4 TestVNet1 hello. На этом этапе можно создать подключение hello TestVNet1 tooTestVNet4. Группы ресурсов hello уведомления являются hello же в примерах hello. Появиться общий ключ, на который ссылается примеры hello. Однако hello общий ключ должен совпадать для обоих подключений, можно использовать собственные значения для hello общего ключа. Создание подключения занимает некоторое время toocomplete.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. Создание подключения tooTestVNet1 TestVNet4 hello. Этот шаг является аналогичные toohello показано выше, за исключением того, вы создаете подключение hello из TestVNet4 tooTestVNet1. Убедитесь, что hello общие ключи совпадают. Подключение hello tooestablish он занимает несколько минут.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. Проверьте подключения. Дополнительные сведения см. в разделе [Проверка подключений](#verify).

## <a name="difsub"></a>Подключение виртуальных сетей из разных подписок

![Схема подключения между виртуальными сетями](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

В этом сценарии мы создадим подключение между TestVNet1 и TestVNet5. Hello виртуальных сетей находятся в разных подписках. Hello подписки не обязательно toobe, связанный с hello того же клиента Active Directory. Hello этапах данной конфигурации добавьте дополнительное подключение виртуальной сети для виртуальной сети в порядке tooconnect TestVNet1 tooTestVNet5.

### <a name="TestVNet1diff"></a>Шаг 5. Создание и настройка TestVNet1

Эти инструкции по-прежнему из шагов hello в предыдущих разделах hello. Необходимо выполнить [шаг 1](#Connect) и [шаг 2](#TestVNet1) toocreate hello VPN-шлюза для TestVNet1 и настроите TestVNet1. Для этой конфигурации не требуется toocreate TestVNet4 hello в предыдущем разделе, несмотря на то, что при ее создании, оно не будет конфликтовать с следующие действия. Выполнив шаг 1 и 2, перейдите к шагу 6.

### <a name="verifyranges"></a>Шаг 6 - проверка hello диапазоны IP-адресов

При создании дополнительных подключений, это важно tooverify, пространство IP-адресов hello hello новой виртуальной сети не пересекается с любым из других диапазонов сети VNet или диапазоны шлюза локальной сети. Для этого упражнения можно использовать следующие значения для hello TestVNet5 hello.

**Значения для TestVNet5:**

* Имя виртуальной сети: TestVNet5
* Группа ресурсов: TestRG5
* Расположение: восточная часть Японии
* TestVNet5: 10.51.0.0/16 и 10.52.0.0/16
* FrontEnd: 10.51.0.0/24
* BackEnd: 10.52.0.0/24
* GatewaySubnet: 10.52.255.0.0/27
* Имя шлюза: VNet5GW
* Общедоступный IP-адрес: VNet5GWIP
* Тип VPN: RouteBased
* Подключение: VNet5toVNet1
* Тип подключения: VNet2VNet

### <a name="TestVNet5"></a>Шаг 7. Создание и настройка TestVNet5

Этот шаг необходимо выполнить в контексте hello hello новую подписку, 5 подписки. Эта часть может выполняться Здравствуйте, администратор в другой организации, которой принадлежит подписка hello. tooswitch между подписками пользуются "az список учетных записей — все" toolist hello учетной записи tooyour доступные подписки, а затем "az учетная запись набора--подписки <subscriptionID>" tooswitch toohello подписки, которые должны toouse.

1. Убедитесь, что вы подключенных tooSubscription 5, а затем создайте группу ресурсов.

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. Создайте TestVNet5.

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. Добавьте подсети.

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. Добавьте подсеть шлюза hello.

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. Запросите общедоступный IP-адрес.

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. Создание шлюза TestVNet5 hello

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="connections5"></a>Шаг 8 — Создание подключений hello

Мы разбить этот шаг в двух сеансах CLI, помеченные как **[подписки 1]**, и **[подписки 5]** так, как шлюзы hello находятся в разных подписках hello. tooswitch между подписками пользуются "az список учетных записей — все" toolist hello учетной записи tooyour доступные подписки, а затем "az учетная запись набора--подписки <subscriptionID>" tooswitch toohello подписки, которые должны toouse.

1. **[Подписки 1]**  Вход и подключиться tooSubscription 1. Выполнения hello следующая команда tooget hello имя и идентификатор hello шлюза hello в выходных данных:

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  Копировать выходные данные hello для «идентификатор:». Отправьте hello идентификатор и имя hello hello виртуальной сети (VNet1GW) toohello администратор шлюза 5 подписки по электронной почте или другим методом.

  Выходные данные примера:

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. **[Подписки 5]**  Вход и подключиться tooSubscription 5. Выполнения hello следующая команда tooget hello имя и идентификатор hello шлюза hello в выходных данных:

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  Копировать выходные данные hello для «идентификатор:». Отправьте hello идентификатор и имя hello hello виртуальной сети (VNet5GW) toohello администратор шлюза 1 подписки по электронной почте или другим методом.

3. **[Подписки 1]**  На этом шаге создания hello подключения из TestVNet1 tooTestVNet5. Однако hello общий ключ должен совпадать для обоих подключений, можно использовать собственные значения для hello общего ключа. Создание соединения может занять некоторое время toocomplete. Убедитесь, что подключение tooSubscription 1.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. **[Подписки 5]**  Этот шаг является аналогичные toohello показано выше, за исключением того, вы создаете подключение hello из TestVNet5 tooTestVNet1. Убедитесь, что hello общие ключи совпадают, а также подключение tooSubscription 5.

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <a name="verify"></a>Проверка подключений hello
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <a name="faq"></a>Часто задаваемые вопросы о подключениях типа "виртуальная сеть — виртуальная сеть"
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Дальнейшие действия

* После завершения подключения можно добавить виртуальные машины tooyour виртуальных сетей. Дополнительные сведения см. в разделе hello [документация по виртуальным машинам](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Сведения о BGP см. в разделе hello [Обзор BGP](vpn-gateway-bgp-overview.md) и [как tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
