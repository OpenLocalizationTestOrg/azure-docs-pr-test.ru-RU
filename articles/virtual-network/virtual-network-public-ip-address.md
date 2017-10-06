---
title: "aaaCreate, изменять и удалять Azure общедоступный IP-адрес | Документы Microsoft"
description: "Узнайте, как toocreate, изменить или удалить общедоступный IP-адрес."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bb71abaf-b2d9-4147-b607-38067a10caf6
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: 0f2578e8661c8f33419b896debcfa0ba1b41fc5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-public-ip-address"></a>Создание, изменение и удаление общедоступного IP-адреса

Дополнительные сведения о общедоступный IP-адрес, адрес и как toocreate, изменять и удалять одну. Общедоступный IP-адрес — это ресурс с собственными настраиваемыми параметрами. Назначение общих tooother адрес IP ресурсы Azure обеспечивает:
- Входящий tooresources подключения к Интернету виртуальных машин (ВМ) Azure, наборы масштабирования виртуальных машин Azure, Azure VPN-шлюз, шлюзы приложений и подсистемы балансировки нагрузки Azure с выходом в Интернет. Ресурсы Azure не может получать входящий трафик от hello Интернет без назначенного общедоступный IP-адрес. Хотя некоторые ресурсы Azure по своей природе доступны через общие IP-адреса, другие ресурсы должны иметь общих IP-адресов, назначенных toothem toobe доступен из Интернета hello.
- Toohello исходящие подключения к Интернету с использованием предсказуемого IP-адреса. Например виртуальной машины могут взаимодействовать исходящих toohello Интернет без открытого tooit адрес, назначенный IP, но его адрес сетевой адрес преобразовываются Azure tooan непредсказуемым общедоступный адрес. Назначение открытого ресурса IP-адреса tooa обеспечивает tooknow IP адрес, используемый для исходящего подключения hello. На то, что прогнозируемый, можно изменить адрес hello в зависимости от выбранного метода присваивания hello. Дополнительные сведения см. в разделе [Создание общедоступного IP-адреса](#create-a-public-ip-address). Дополнительные сведения о исходящие подключения из ресурсы Azure, чтение hello toolearn [понять исходящих соединений](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) статьи.

## <a name="before-you-begin"></a>Перед началом работы

Выполните следующие задачи перед выполнением любой шагов в любой части этой статьи hello.

- Просмотрите hello [Azure ограничивает](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn статьи об ограничениях для общедоступных IP-адресов.
- Войдите в toohello Azure [портала](https://portal.azure.com), Azure командной строки (CLI) или Azure PowerShell с учетной записью Azure. Если у вас нет учетной записи Azure, зарегистрируйтесь для получения [бесплатной пробной учетной записи](https://azure.microsoft.com/free).
- Если с помощью PowerShell команды toocomplete задач в этой статье [Установка и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Убедитесь, что у вас есть hello самая последняя версия командлетов Azure PowerShell hello установлен. tooget справки для команд PowerShell, с примерами, введите `get-help <command> -full`.
- Если Azure командной строки (CLI) с помощью команды toocomplete задач в этой статье [Установка и настройка hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Убедитесь, что имеется hello самую последнюю версию hello Azure CLI установлен. Введите tooget справочные сведения о командах CLI, `az <command> --help`. Вместо установки hello CLI и его необходимых компонентов можно использовать hello оболочки облако Azure. Hello оболочки облако Azure — это бесплатные Bash, который выполняется непосредственно в hello портал Azure. Он имеет hello Azure CLI предварительно установить и настроить toouse с вашей учетной записью. hello toouse оболочки облака щелкните hello оболочки облака **> _** кнопку вверху hello hello [портала](https://portal.azure.com).

За использование общедоступных IP-адресов взимается номинальная плата. tooview hello цен, чтение hello [цены IP адрес](https://azure.microsoft.com/pricing/details/ip-addresses) страницы. 

## <a name="create-a-public-ip-address"></a>Создание общедоступного IP-адреса

1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи, назначенные (как минимум) разрешения для роли участника сети hello для вашей подписки. Чтение hello [встроенных ролей для управления доступом на основе ролей Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) Дополнительные сведения о назначении ролей и разрешений tooaccounts toolearn статьи.
2. В поле hello, содержащее текст hello *Найдите ресурсы* вверху hello hello портал Azure, введите *общедоступный IP-адрес*. Когда **открытый IP-адреса** появится в результатах поиска hello, щелкните его.
3. Нажмите кнопку **+ добавить** в hello **общедоступный IP-адрес** колонки, отображается.
4. Введите или выберите значения для следующих параметров в hello hello **создать общедоступный IP-адрес** колонки, отображается, нажмите кнопку **создать**:

    |Настройка|Обязательный?|Сведения|
    |---|---|---|
    |Имя|Да|Hello имя должно быть уникальным в пределах группы ресурсов hello выбранным.|
    |Версия IP-адреса|Да| Выберите IPv4 или IPv6. Пока открытый IPv4 адреса могут быть назначены tooseveral ресурсы Azure, общедоступный IP-адрес IPv6 можно назначить только балансировки нагрузки tooan с выходом в Интернет. Подсистема балансировки нагрузки Hello можно балансировку нагрузки IPv6 трафика tooAzure виртуальных машин. Дополнительные сведения о [машины toovirtual трафик IPv6 с балансировкой нагрузки](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
    |Назначение IP-адресов|Да|**Динамический:** динамические адреса назначаются только после связывания hello общедоступный IP-адрес tooa сетевой Адаптер подключен tooa ВМ и hello виртуальная машина запускается hello первый раз. Динамические адреса можно изменить, если hello ВМ hello Сетевых вложенного toois остановлена (освобождена). адрес остается Hello hello же если hello ВМ перезагрузки или остановлена (но не освобождается). **Статический:** при создании hello общедоступный IP-адрес назначения статических адресов. Статические адреса сделать это не изменение, даже если hello виртуальная машина переводится в hello остановлена (освобождена) состояние. Hello адрес освобождается только при удалении hello сетевого Адаптера. Метод hello назначения можно изменить после создания hello сетевого Адаптера. При выборе IPv6 для hello **IP версии**, метод доступен только назначения hello **динамическое**.|
    |Время ожидания простоя (в минутах)|Нет|Сколько времени в минутах tookeep открыть соединение TCP или HTTP не полагаться на toosend сообщения проверки активности клиентов. При выборе IPv6 в качестве **версии IP** это значение невозможно изменить. |
    |Метка имени DNS|Нет|Должно быть уникальным в пределах hello расположение Azure, можно создать имя hello в (по всем подпискам и для всех клиентов). Hello Azure общей службы DNS автоматически регистрирует имя hello и IP-адрес для подключения tooa ресурсов с именем hello. Добавляет Azure *location.cloudapp.azure.com* (где расположение является выбрать расположение hello) toohello именем toocreate hello полностью полное имя DNS. Если выбрать обе версии адрес toocreate hello же DNS-имя назначается tooboth hello IPv4 и IPv6-адресов. Hello служба Azure DNS содержит записи IPv4 A и IPv6 AAAA имен и реакцию с обеих записей, выполняется поиск hello DNS-имя. какой адрес (IPv4 или IPv6) toocommunicate с выбираемый клиентом Hello.|
    |"Create an IPv6 (or IPv4) address" (Создание IPv6- или IPv4-адреса)|Нет| То, какой из адресов отображается (IPv6 и IPv4) зависит от выбора **версии IP**. Например, при выборе **IPv4** в качестве **версии IP** здесь отображается **IPv6**.
    |Имя (отображается, только если установлен флажок hello **создать адрес IPv6 (или IPv4)** флажок)|Да, если выбрать hello **создать IPv6** (или IPv4) флажок.|Hello имя должно отличаться от имени hello для hello сначала введите **имя** в этом списке. При выборе toocreate IPv4 и IPv6-адрес портала hello создает два отдельных открытые ресурсы IP-адресов, одно с каждой версией IP адрес, назначенный tooit.|
    |Назначение IP-адресов (отображается, только если установлен флажок hello **создать адрес IPv6 (или IPv4)** флажок)|Да, если выбрать hello **создать IPv6** (или IPv4) флажок.|Если флажок hello говорит **создать адрес IPv4**, можно выбрать метод присваивания. Если флажок hello говорит **создать IPv6-адрес**, нельзя выбрать метод присваивания, как она должна быть **динамического**.|
    |Подписки|Да|Должен существовать в hello же [подписки](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) как ресурс hello требуется tooassociate hello общий IP-адрес.|
    |Группа ресурсов|Да|Может существовать в hello в одном или разных, [группы ресурсов](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) как ресурс hello требуется tooassociate hello общий IP-адрес.|
    |Расположение|Да|Должен существовать в hello же [расположение](https://azure.microsoft.com/regions), также называется области tooas hello ресурс, tooassociate hello общий IP-адрес.|

**Команды**

Хотя hello портал предоставляет toocreate параметр hello два открытых ресурсы IP-адресов (один адрес IPv4 и IPv6 на один), следующие команды PowerShell и CLI hello создать один ресурс с адресом для одной версии IP или hello других. Если требуется два открытых ресурсы IP-адресов, один для каждой версии IP следует вызвать команду hello дважды, указав разные имена и версии hello открытые ресурсы IP-адресов. 

|Средство|Команда|
|---|---|
|Интерфейс командной строки|[az network public-ip create](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)|

## <a name="view-change-settings-for-or-delete-a-public-ip-address"></a>Просмотр, изменение параметров или удаление общедоступного IP-адреса

1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи, назначенные (как минимум) разрешения для роли участника сети hello для вашей подписки. Чтение hello [встроенных ролей для управления доступом на основе ролей Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) Дополнительные сведения о назначении ролей и разрешений tooaccounts toolearn статьи.
2. В поле hello, содержащее текст hello *Найдите ресурсы* вверху hello hello портал Azure, введите *общедоступный IP-адрес*. Когда **открытый IP-адреса** появится в результатах поиска hello, щелкните его.
3. В hello **открытый IP-адреса** колонки, отображается, щелкните имя hello hello общедоступного IP-адреса должны tooview, изменение параметров или удалить.
4. В колонке hello, которое отображается для hello общедоступный IP-адрес, выполнение одного из следующих вариантов в зависимости от того, нужно ли tooview, hello, удаление или изменение hello общедоступный IP-адрес.
    - **Представление**: hello **Обзор** части колонки hello показаны ключевые параметры для hello общедоступный IP-адрес, например hello сетевого интерфейса оно связано слишком (если hello адрес связанного tooa сетевой интерфейс). портал Hello не отображает hello версии hello адреса (IPv4 или IPv6). tooview hello сведений о версии, hello используйте PowerShell или интерфейс командной строки команду tooview hello общедоступный IP-адрес. Если версия hello IP-адреса IPv6, назначен адрес hello портала hello, PowerShell или hello CLI не отображается. 
    - **Удалить**: toodelete hello общедоступный IP-адрес, нажмите кнопку **удаление** в hello **Обзор** части колонки hello. Если адрес hello в настоящее время связаны tooan IP-конфигурации, его нельзя удалить. Если адрес hello в настоящее время связан с конфигурацией, нажмите кнопку **отмените связь** toodissociate hello адрес из hello IP-конфигурации.
    - **Изменение**. Щелкните **Конфигурация**. Изменение параметров с помощью hello сведения на шаге 4 hello [создать общедоступный IP-адрес](#create-a-public-ip-address) этой статьи. toochange hello назначения для IPv4-адреса из статического toodynamic, необходимо сначала разорвать связь hello общедоступный IPv4-адрес из hello IP-конфигурации, которыми он связан для. Затем можно изменить метод toodynamic hello назначения и нажмите кнопку **связать** tooassociate hello IP адрес toohello же IP конфигурации, другой конфигурации или оставить его отдельно. общедоступный IP-адрес в hello toodissociate **Обзор** щелкните **отмените связь**.

>[!WARNING]
>При переключении метод присваивания hello из статических toodynamic утере hello IP-адрес, назначенный toohello общедоступный IP-адрес. Пока hello Azure общедоступные DNS-серверы сохранить сопоставление адресов статической или динамической и любые метка DNS-имени (если он был определен), динамический IP-адрес может измениться при запуске hello виртуальной Машины после в hello остановлена (освобождена) состояние. адрес hello tooprevent изменять, назначьте статический IP-адрес.

**Команды**

|Средство|Команда|
|---|---|
|Интерфейс командной строки|[Список public-ip-сети AZ](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#list) toolist общих IP-адресов, [az сети public-ip Показать](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#show) tooshow параметры; [обновления открытого ip-сети az](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#update) tooupdate; [удалить az сетевого public-IP-адреса](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#delete) toodelete|
|PowerShell|[Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) tooretrieve общедоступный IP-адрес, адрес объекта и просмотреть ее параметры [AzureRmPublicIpAddress набор](/powershell/resourcemanager/azurerm.network/set-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) tooupdate параметры; [AzureRmPublicIpAddress удаление](/powershell/module/azurerm.network/remove-azurermpublicipaddress) toodelete|

## <a name="next-steps"></a>Дальнейшие действия
Назначение общих IP-адресов, при создании hello следующие ресурсы Azure:

- виртуальных машин [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) или [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json);
- [Azure Load Balancer с доступом к Интернету](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json);
- [Шлюз приложений Azure](../application-gateway/application-gateway-create-gateway-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [подключения типа "сеть — сеть" с помощью VPN-шлюза Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json);
- [масштабируемого набора виртуальных машин Azure](../virtual-machine-scale-sets/virtual-machine-scale-sets-portal-create.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
