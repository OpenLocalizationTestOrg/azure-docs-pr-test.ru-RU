---
title: "aaaCreate, изменить или удалить интерфейс сети Azure | Документы Microsoft"
description: "Узнайте, что сетевой интерфейс и как изменить параметры toocreate и удалите одну."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: dcb6cdbd73bc0d0ca4efb9d972d370cf2d54abb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-network-interface"></a>Создание, изменение или удаление сетевых интерфейсов

Узнайте, как изменить параметры toocreate и удалить сетевой интерфейс. Сетевой интерфейс позволяет toocommunicate виртуальной машине Azure с помощью Интернета, Azure и локальными ресурсами. При создании виртуальной машины, с помощью hello портал Azure, портал hello создает один сетевой интерфейс с параметрами по умолчанию для вас. Можно вместо этого выбрать toocreate сетевых интерфейсов с пользовательскими параметрами и добавьте один или несколько сетевых интерфейсов tooa виртуальную машину при ее создании. Можно использовать параметры сетевого интерфейса toochange по умолчанию для существующего сетевого интерфейса. В этой статье объясняется, как изменить существующие параметры, такие как назначение (сетевую группу безопасности) фильтр сети, подсети назначения, параметры DNS-сервера и IP-пересылки toocreate сетевой интерфейс с пользовательскими настройками и удалить сетевой интерфейс.

Если вам требуется tooadd, измените или удалите IP-адреса для сетевого интерфейса, чтение hello [Управление IP-адреса](virtual-network-network-interface-addresses.md) статьи. Если требуется tooadd сетевых интерфейсов для или удалить сетевые интерфейсы из виртуальных машин, прочтите hello [добавления или удаления сетевых интерфейсов](virtual-network-network-interface-vm.md) статьи.


## <a name="before-you-begin"></a>Перед началом работы

Выполните следующие задачи перед выполнением любой шагов в любой части этой статьи hello.

- Просмотрите hello [Azure ограничивает](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn статьи об ограничениях для сетевых интерфейсов.
- Войдите в toohello Azure [портала](https://portal.azure.com), Azure командной строки (CLI) или Azure PowerShell с учетной записью Azure. Если у вас нет учетной записи Azure, зарегистрируйтесь для получения [бесплатной пробной учетной записи](https://azure.microsoft.com/free).
- Если с помощью PowerShell команды toocomplete задач в этой статье [Установка и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Убедитесь, что у вас есть hello самая последняя версия командлетов Azure PowerShell hello установлен. tooget справки для команд PowerShell, с примерами, введите `get-help <command> -full`.
- Если Azure командной строки (CLI) с помощью команды toocomplete задач в этой статье [Установка и настройка hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Убедитесь, что имеется hello самую последнюю версию hello Azure CLI установлен. Введите tooget справочные сведения о командах CLI, `az <command> --help`. Вместо установки hello CLI и его необходимых компонентов можно использовать hello оболочки облако Azure. Hello оболочки облако Azure — это бесплатные Bash, который выполняется непосредственно в hello портал Azure. Он имеет hello Azure CLI предварительно установить и настроить toouse с вашей учетной записью. hello toouse оболочки облака щелкните hello оболочки облака **> _** кнопку вверху hello hello [портала](https://portal.azure.com).

## <a name="create-a-network-interface"></a>Создание сетевого интерфейса

При создании виртуальной машины, с помощью hello портал Azure, портал hello создает сетевой интерфейс с параметрами по умолчанию для вас. Если бы вместо этого указать все параметры сетевого интерфейса, можно создать настраиваемые параметры сетевого интерфейса и присоединить hello сетевой интерфейс tooa виртуальной машины при создании виртуальной машины hello (с помощью PowerShell или Azure CLI hello). Можно также создать сетевой интерфейс и добавить его в существующую виртуальную машину tooan (с помощью PowerShell или Azure CLI hello). toolearn сетевой интерфейс или tooadd для toocreate с существующей виртуальной машины, или удалите сетевые интерфейсы из существующих виртуальных машин, чтение hello [добавления или удаления сетевых интерфейсов](virtual-network-network-interface-vm.md) статьи. Перед созданием сетевого интерфейса, необходимо иметь существующий [виртуальной сети](virtual-networks-create-vnet-arm-pportal.md) в hello же местоположение и подписку создать сетевому интерфейсу.

1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи, назначенные (как минимум) разрешения для роли участника сети hello для вашей подписки. Чтение hello [встроенных ролей для управления доступом на основе ролей Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) Дополнительные сведения о назначении ролей и разрешений tooaccounts toolearn статьи.
2. В поле hello, содержащее текст hello *Найдите ресурсы* вверху hello hello портал Azure, введите *сетевых интерфейсов*. Когда **сетевых интерфейсов** появится в результатах поиска hello, щелкните его.
3. В hello **сетевых интерфейсов** колонки, отображается, нажмите кнопку **+ добавить**.
4. В hello **создать сетевой интерфейс** колонки, отображается, введите, или выбрать значения для hello следующие параметры, а затем нажмите кнопку **создать**:

    |Настройка|Обязательный?|Сведения|
    |---|---|---|
    |Имя|Да|Hello имя должно быть уникальным в пределах группы ресурсов hello выбранным. Со временем в вашей подписке Azure скорее всего появится несколько сетевых интерфейсов. Чтение hello [соглашения об именовании](/azure/architecture/best-practices/naming-conventions?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-rules-and-restrictions) статью для предложения при создании именования toomake соглашение управление несколько сетевых интерфейсов проще. Hello невозможно переименовать после создания hello сетевого интерфейса.|
    |Виртуальная сеть|Да|Выберите hello виртуальной сети для сетевого интерфейса hello. Можно назначить только сетевой интерфейс tooa виртуальной сети, которая существует hello же подписке и расположении как hello сетевого интерфейса. После создания сетевого интерфейса hello виртуальной сети, когда он присваивается изменить нельзя. Hello виртуальной машины, добавьте hello сетевой интерфейс toomust также существовать в hello же местоположение и подписку как hello сетевого интерфейса.|
    |Подсеть|Да|Выберите подсеть в виртуальной сети hello выбранный. Вы можете изменить подсеть hello hello сетевого интерфейса назначается tooafter, он создается.|
    |Назначение частного IP-адреса|Да| В этот параметр, при выборе метода присваивания hello для hello IPv4-адрес. Выбрать следующие методы присваивания hello: **динамического:** при выборе этого параметра, Azure автоматически назначает доступный адрес из адресного пространства hello выбранные подсети hello. Azure может назначить другой адрес сетевого интерфейса tooa при запуске hello виртуальной машины, где находится после в hello остановлена (освобождена) состояние. адрес остается Hello hello же перезагружается hello виртуальной машины без в hello остановлена (освобождена) состояние. **Статический:** при выборе этого параметра, необходимо вручную назначить доступного IP-адреса в диапазоне адресов hello выбранные подсети hello. Статические адреса не изменяются, пока их изменении или удалении hello сетевого интерфейса. Метод hello назначения можно изменить после создания hello сетевого интерфейса. Hello Azure DHCP-сервер назначает этот адрес toohello сетевой интерфейс в операционной системе hello hello виртуальной машины.|
    |Группа безопасности сети|Нет| Оставьте значение слишком**нет**, выберите существующую [сетевой группы безопасности](virtual-networks-nsg.md), или [создайте группу безопасности сети](virtual-networks-create-nsg-arm-pportal.md). Сетевые группы безопасности позволяют toofilter сетевого трафика и из него сетевого интерфейса. Можно применить ноль или один сетевой безопасности группы tooa сетевого интерфейса. Ноль или один сетевой группы безопасности могут также применяться назначается toohello подсети hello сетевого интерфейса. При сетевой группы безопасности сетевой интерфейс примененных tooa и hello подсети hello сетевой интерфейс является назначается, возникают некоторые неожиданные результаты. группы безопасности сети tootroubleshoot, примененные toonetwork интерфейсы и подсетей, чтение hello [Устранение сетевых групп безопасности](virtual-network-nsg-troubleshoot-portal.md#nsg) статьи.|
    |Подписки|Да|Выберите одну из [подписок](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) Azure. Hello виртуальной машины, подключить сетевой интерфейс tooand hello виртуальной сети подключите его toomust существует в hello же подписки.|
    |"Private IP address (IPv6)" (Частный IP-адрес (IPv6))|Нет| Если этот флажок установлен, IPv6-адрес назначенного toohello сетевого интерфейса, кроме toohello адрес IPv4 назначен toohello сетевого интерфейса. В разделе hello [IPv6](#IPv6) этой статьи для важные сведения об использовании IPv6 с сетевыми интерфейсами. Не удается выбрать метод присваивания для hello IPv6-адрес. При выборе tooassign IPv6-адрес, назначенный с hello динамического метода.
    |Имя IPv6 (появляется, только если hello **частный IP-адрес (IPv6)** флажок) |Да, если hello **частный IP-адрес (IPv6)** установлен флажок.| Это имя назначается tooa дополнительную IP-конфигурацию сетевого интерфейса hello. Дополнительные сведения об IP-конфигурации в hello [просмотреть параметры сетевого интерфейса](#view-network-interface-settings) этой статьи.|
    |Группа ресурсов|Да|Выберите существующую [группу ресурсов](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) или создайте новую. Сетевой интерфейс может существовать в hello таким же или другой группе ресурсов, чем hello виртуальной машине можно присоединить его к, или hello виртуальной сети можно подключить к.|
    |Расположение|Да|Hello виртуальной машины, подключить сетевой интерфейс tooand hello виртуальной сети подключите его toomust существует в hello же [расположение](https://azure.microsoft.com/regions), также называется tooas область.|

портал Hello не предоставляет tooassign параметр hello общей сетевой интерфейс toohello IP адрес при ее создании, хотя портал hello создайте общедоступный IP-адрес и назначьте его tooa сетевого интерфейса, при создании виртуальной машины с помощью портала hello. toolearn tooadd открытый toohello сети IP-адресов интерфейса после создания, чтения hello [Управление IP-адреса](virtual-network-network-interface-addresses.md) статьи. Если вы хотите toocreate с общедоступный IP-адрес сетевого интерфейса, необходимо использовать hello CLI или PowerShell toocreate hello сетевого интерфейса.

>[!Note]
> Azure назначает MAC адрес toohello сетевого интерфейса только после того, hello сетевой интерфейс tooa подключенных виртуальных машин и hello виртуальной машины — hello первом запуске. Нельзя указать hello MAC-адрес, Azure назначает toohello сетевого интерфейса. Hello MAC адрес остается назначенный toohello сетевого интерфейса, пока hello сетевого интерфейса не будет удален или изменен hello частных IP-адрес toohello основной IP-конфигурации hello первичный сетевой интерфейс. Дополнительные сведения об IP-адреса и IP-конфигурации, чтение hello toolearn [Управление IP-адреса](virtual-network-network-interface-addresses.md) статьи.

**Команды**

|Средство|Команда|
|---|---|
|Интерфейс командной строки|[az network nic create](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|

## <a name="view-network-interface-settings"></a>Просмотр параметров сетевого интерфейса

Большинство параметров сетевого интерфейса можно просматривать и изменять после его создания.

1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи, назначенные (как минимум) разрешения для роли участника сети hello для вашей подписки. Чтение hello [встроенных ролей для управления доступом на основе ролей Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) Дополнительные сведения о назначении ролей и разрешений tooaccounts toolearn статьи.
2. В поле hello, содержащее текст hello *Найдите ресурсы* вверху hello hello портал Azure, введите *сетевых интерфейсов*. Когда **сетевых интерфейсов** появится в результатах поиска hello, щелкните его.
3. В hello **сетевых интерфейсов** колонки, отображается, щелкните hello сетевой интерфейс должен tooview или изменить параметры.
4. Hello следующие параметры перечислены в колонке hello, появится для hello сетевого интерфейса, выбранных.
    - **Обзор:** содержит сведения о hello сетевого интерфейса, такие как назначить tooit hello IP-адреса, назначенные hello виртуальные подсети hello сетевого интерфейса и hello виртуальной машины hello сетевой интерфейс подключается слишком (if он присоединен tooone). Hello на рисунке ниже показаны hello Обзор параметры сетевого интерфейса с именем **mywebserver256**: ![Обзор сетевой интерфейс](./media/virtual-network-network-interface/nic-overview.png) сетевой интерфейс tooa другой группе ресурсов можно переместить или подписки, нажав кнопку (**изменить**) Далее toohello **группы ресурсов** или **имя подписки**. При перемещении hello сетевого интерфейса, необходимо переместить все ресурсы сетевого интерфейса toohello связанные с ним. Если вложенное tooa виртуальной машины hello сетевого интерфейса, например, также необходимо переместить hello виртуальной машины и другие ресурсы, связанные с виртуальной машины. чтение hello toomove сетевого интерфейса, который [перемещение ресурсов tooa группы ресурсов или подписку](../azure-resource-manager/resource-group-move-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json#use-portal) статьи. Hello статье перечислены необходимые условия, порядок и toomove ресурсов с помощью портала Azure PowerShell, hello hello Azure CLI.
    - **IP-конфигурации:** общедоступных и частных адресов IPv4 и IPv6 назначенные конфигурации tooIP перечисленные здесь. Если назначено tooan IP-конфигурацию IPv6-адрес, адрес hello не отображается. Дополнительные сведения об IP-конфигурации, а также как tooadd и удалите IP-адресов в hello [настроить IP-адреса для интерфейса сети Azure](virtual-network-network-interface-addresses.md) статьи. В этом разделе также настраиваются IP-пересылка и назначение подсетей. Дополнительные сведения об этих параметров чтения hello toolearn [включить или отключить IP-пересылки](#enable-or-disable-ip-forwarding) и [изменить назначение подсети](#change-subnet-assignment) подразделах этой статьи.
    - **DNS-серверов:** можно указать DNS-сервер, сетевой интерфейс назначается hello Azure DHCP-серверов. Hello сетевой интерфейс может наследовать приветствия из hello назначается сетевой интерфейс виртуальной сети hello, или иметь пользовательского параметра, который переопределяет параметр hello для hello виртуальной сети, он не будет назначен. toomodify отображаемых, hello завершения шагов в hello [изменение DNS-серверы](#change-dns-servers) этой статьи.
    - **Группы безопасности сети (NSG):** отображает которых является NSG связанные toohello сетевого интерфейса (если таковые имеются). NSG содержит правила входящего и исходящего трафика toofilter сетевого трафика для hello сетевого интерфейса. Если NSG связанные toohello сетевого интерфейса, имя hello hello отображаются связанные NSG. toomodify отображаемых, hello завершения шагов в hello [управление связи с группами безопасности сети](virtual-network-manage-nsg-arm-portal.md#manage-associations) статьи.
    - **Свойства:** отображает ключевые параметры о hello сетевого интерфейса, включая MAC-адрес (остается пустым, если сетевой интерфейс hello не вложенные tooa виртуальной машины), а hello он существует в подписке.
    - **Правила безопасности:** правила безопасности перечислены в том случае, если hello сетевого интерфейса подключенных tooa виртуальной машины под управлением, который NSG связанные toohello сетевого интерфейса и hello подсети, он не будет назначен. toolearn Дополнительные сведения о том, что отображено чтения hello [Устранение сетевых групп безопасности](virtual-network-nsg-troubleshoot-portal.md#nsg) статьи. Дополнительные сведения о Nsg, чтение hello toolearn [сетевых групп безопасности](virtual-networks-nsg.md) статьи.
    - **Действующих маршрутах:** hello сетевой интерфейс в случае вложенных tooa виртуальной машины под управлением перечисленных маршрутов. маршруты Hello представляют собой сочетание маршруты hello Azure по умолчанию, все определяемые пользователем маршруты (UDR) и все маршруты BGP, которые могут существовать для hello подсети hello сетевого интерфейса, входящих в. toolearn Дополнительные сведения о том, что отображено чтения hello [Устранение маршруты](virtual-network-routes-troubleshoot-portal.md#view-effective-routes-for-a-network-interface) статьи. Дополнительные сведения о Azure по умолчанию и UDRs, чтение hello toolearn [определяемых пользователем маршрутов](virtual-networks-udr-overview.md) статьи.
    - **Общие параметры диспетчера ресурсов Azure:** toolearn Дополнительные сведения об общих параметров диспетчера ресурсов Azure, чтение hello [журнал действий](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#activity-logs), [(IAM) управления доступом к](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#access-control), [теги ](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags), [Блокирует](../azure-resource-manager/resource-group-lock-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json), и [сценарий автоматизации](../azure-resource-manager/resource-manager-export-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json#export-the-template-from-resource-group) статей.

**Команды**

Если IPv6-адрес назначается tooa сетевого интерфейса, hello выходные данные PowerShell возвращает фактов hello назначается адрес hello, что он не возвращает адрес, назначенный hello. Аналогичным образом hello CLI возвращает hello факт hello адрес назначается, но возвращает *null* в выходном файле для адреса hello.

|Средство|Команда|
|---|---|
|Интерфейс командной строки|[Список сетевых карт сетей AZ](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#list) tooview сетевых интерфейсов в подписке hello. [Показать сетевого адаптера сети az](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#show) tooview параметры сетевого интерфейса|
|PowerShell|[Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) tooview сетевых интерфейсов для hello подписки или просмотр параметров сетевого интерфейса|

## <a name="change-dns-servers"></a>Изменение DNS-серверов

DNS-сервер Hello назначается hello Azure DHCP toohello сетевом интерфейсе сервера в операционной системе виртуальной машины hello. Hello DNS-сервер назначен является любой приветствия сервера DNS для сетевого интерфейса. toolearn Дополнительные сведения о параметрах разрешение имени для сетевого интерфейса, в разделе [разрешение имен для виртуальных машин](virtual-networks-name-resolution-for-vms-and-role-instances.md). Hello сетевого интерфейса наследуют настройки hello hello виртуальной сети, или использовать свои собственные уникальные настройки, переопределяют параметры hello для hello виртуальной сети.

1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи, назначенные (как минимум) разрешения для роли участника сети hello для вашей подписки. Чтение hello [встроенных ролей для управления доступом на основе ролей Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) Дополнительные сведения о назначении ролей и разрешений tooaccounts toolearn статьи.
2. В поле hello, содержащее текст hello *Найдите ресурсы* вверху hello hello портал Azure, введите *сетевых интерфейсов*. Когда **сетевых интерфейсов** появится в результатах поиска hello, щелкните его.
3. В hello **сетевых интерфейсов** колонки, отображается, щелкните hello сетевой интерфейс должен tooview или изменить параметры.
4. В колонке hello hello сетевого интерфейса выбран, щелкните **DNS-серверы** под **параметры**.
5. Щелкните один из следующих параметров:
    - **Наследовать от виртуальной сети (по умолчанию)**: выберите этот параметр tooinherit hello DNS server параметр, определенный для hello виртуальной сети hello сетевого интерфейса, входящих в. На уровне виртуальной сети hello определяется hello предоставленных системой Azure DNS-сервера или пользовательского DNS-сервера. Hello предоставленных системой Azure DNS-сервер способен разрешать имена узлов для ресурсов, назначенных toohello одной виртуальной сети. Полное доменное имя должно быть используется tooresolve для ресурсов, назначенных toodifferent виртуальных сетей.
    - **Настраиваемый**: tooresolve имена сервера DNS можно настроить несколько виртуальных сетей. Введите IP-адрес hello hello сервера требуется toouse как DNS-сервер. адрес DNS-сервера Hello, указываемые назначается только toothis сетевого интерфейса и переопределений, которые назначены параметры DNS для hello виртуальной сети hello сетевого интерфейса.
6. Щелкните **Сохранить**.

**Команды**

|Средство|Команда|
|---|---|
|Интерфейс командной строки|[az network nic update](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="enable-or-disable-ip-forwarding"></a>Включение и отключение IP-пересылки

IP-пересылки позволяет виртуальной машине hello сетевой интерфейс, подключенный к:
- Получения сетевого трафика, не предназначенные для одного hello IP-адресов, назначенных tooany hello IP-конфигураций, назначенный toohello сетевого интерфейса.
- Отправка сетевого трафика с помощью другой исходный IP-адрес, чем hello одного назначенного tooone IP-конфигурации сетевого интерфейса.

для каждого сетевого интерфейса, подключенных toohello виртуальная машина, получающая трафик, hello tooforward потребностей виртуальной машины должен быть включен параметр Hello. Виртуальной машине могут пересылать трафик ли он имеет несколько сетевых интерфейсов и один сетевой интерфейс, назначенный tooit. Хотя Azure установлен IP-пересылки, hello виртуальной машины необходимо также выполнить приложение может tooforward hello трафика, например брандмауэр, ГЛОБАЛЬНОЙ оптимизации и балансировка нагрузки приложений. Если виртуальная машина работает под управлением сетевых приложений, hello виртуальной машины часто является ссылка tooas устройство виртуальной сети. Можно просмотреть список виртуальных сетевых устройств Готово toodeploy в hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances). IP-пересылка обычно используется в определяемых пользователем маршрутах. Дополнительные сведения об определяемых пользователем маршрутов, чтение hello toolearn [определяемых пользователем маршрутов](virtual-networks-udr-overview.md) статьи.

1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи, назначенные (как минимум) разрешения для роли участника сети hello для вашей подписки. Чтение hello [встроенных ролей для управления доступом на основе ролей Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) Дополнительные сведения о назначении ролей и разрешений tooaccounts toolearn статьи.
2. В поле hello, содержащее текст hello *Найдите ресурсы* вверху hello hello портал Azure, введите *сетевых интерфейсов*. Когда **сетевых интерфейсов** появится в результатах поиска hello, щелкните его.
3. В hello **сетевых интерфейсов** колонки, отображается, щелкните сетевой интерфейс hello требуется tooenable или отключить IP-пересылки для.
4. В колонке hello hello сетевого интерфейса выбран, щелкните **IP-конфигурации** в hello **параметры** раздела.
5. Нажмите кнопку **включено** или **отключено** приветствия toochange (по умолчанию).
6. Щелкните **Сохранить**.

**Команды**

|Средство|Команда|
|---|---|
|Интерфейс командной строки|[az network nic update](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet-assignment"></a>Изменение назначения подсети

Можно изменить hello подсети, но не hello виртуальной сети, назначенной для сетевого интерфейса.

1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи, назначенные (как минимум) разрешения для роли участника сети hello для вашей подписки. Чтение hello [встроенных ролей для управления доступом на основе ролей Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) Дополнительные сведения о назначении ролей и разрешений tooaccounts toolearn статьи.
2. В поле hello, содержащее текст hello *Найдите ресурсы* вверху hello hello портал Azure, введите *сетевых интерфейсов*. Когда **сетевых интерфейсов** появится в результатах поиска hello, щелкните его.
3. В hello **сетевых интерфейсов** колонки, отображается, щелкните hello сетевой интерфейс должен tooview или изменить параметры.
4. Нажмите кнопку **IP-конфигурации** под **параметры** в колонке hello для сетевого интерфейса hello выбран. Если любой частных IP-адресов для любого IP-конфигурации в списке у **(статический)** Далее toothem hello IP адрес назначения метод toodynamic необходимо изменить, выполнив hello, описанных ниже. Частные IP-адреса должны быть назначены с hello динамического назначения метод toochange hello назначение подсети для hello сетевого интерфейса. Если hello адреса назначаются с hello динамический метод, по-прежнему toostep пяти. IPv4-адреса назначаются с помощью метода назначения статических hello, выполните следующие шаги toochange hello назначения метод toodynamic hello.
    - Щелкните IP-конфигурации hello требуется hello toochange способ назначения адреса IPv4 для hello списке IP-конфигурации.
    - В hello колонки, отображается hello IP-конфигурации, щелкните **динамическое** для hello **назначения** метод. Нельзя назначить IPv6-адрес с помощью метода назначения статических hello.
    - Щелкните **Сохранить**.
5. Выберите подсеть hello требуется tooconnect hello сетевой интерфейс toofrom hello **подсети** раскрывающегося списка.
6. Щелкните **Сохранить**. Новые динамические адреса назначаются из hello диапазон адресов подсети для новой подсети hello. После назначения hello сетевой интерфейс tooa новую подсеть, можно назначить статический IPv4-адрес с hello новый диапазон адресов подсети, при выборе. Дополнительные сведения о Добавление, изменение и удаление IP-адреса для сетевого интерфейса, чтение hello toolearn [Управление IP-адреса](virtual-network-network-interface-addresses.md) статьи.

**Команды**

|Средство|Команда|
|---|---|
|Интерфейс командной строки|[az network nic ip-config update](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/set-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-a-network-interface"></a>Удаление сетевого интерфейса

Вы можете удалить сетевой интерфейс, пока не tooa подключенных виртуальных машин. Если вложенное tooa виртуальной машины, необходимо первый месте hello состояние виртуальной машины в hello остановлена (освобождена), затем отключить сетевой интерфейс hello hello виртуальной машине, прежде чем удалять сетевой интерфейс hello. toodetach сетевой интерфейс из виртуальной машины hello завершения шагов в hello [отключить сетевой интерфейс из виртуальной машины](virtual-network-network-interface-vm.md#vm-remove-nic) раздел hello [добавления или удаления сетевых интерфейсов](virtual-network-network-interface-vm.md) статьи. Удаление виртуальной машины отсоединяет все вложенные tooit интерфейсов сети, но не удаляет hello сетевых интерфейсов.

1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи, назначенные (как минимум) разрешения для роли участника сети hello для вашей подписки. Чтение hello [встроенных ролей для управления доступом на основе ролей Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) Дополнительные сведения о назначении ролей и разрешений tooaccounts toolearn статьи.
2. В поле hello, содержащее текст hello *Найдите ресурсы* вверху hello hello портал Azure, введите *сетевых интерфейсов*. Когда **сетевых интерфейсов** появится в результатах поиска hello, щелкните его.
3. Щелкните правой кнопкой мыши hello сетевой интерфейс toodelete и щелкните **удалить**.
4. Нажмите кнопку **Да** tooconfirm удаления hello сетевого интерфейса.

При удалении сетевого интерфейса, любой компьютер MAC, или назначить IP-адреса tooit освобождаются.

**Команды**

|Средство|Команда|
|---|---|
|Интерфейс командной строки|[az network nic delete](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmNetworkInterface](/powershell/module/azurerm.network/remove-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>Дальнейшие действия
toocreate виртуальную машину с несколькими сетевыми интерфейсами или IP-адреса, прочтите hello в следующих статьях:

**Команды**

|Задача|Средство|
|---|---|
|Создание виртуальной машины с несколькими сетевыми адаптерами|[Интерфейс командной строки](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Создание виртуальной машины с одним сетевым адаптером, которому назначено несколько IPv4-адресов|[Интерфейс командной строки](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Создание виртуальной машины с одним сетевым адаптером, которому назначен частный IPv6-адрес (обслуживаемый Azure Load Balancer).|[Интерфейс командной строки](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [шаблон Azure Resource Manager](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
