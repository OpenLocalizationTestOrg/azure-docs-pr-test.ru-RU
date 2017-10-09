---
title: "Пример DMZ-aaaAzure построения простой DMZ с Nsg | Документы Microsoft"
description: "Создание сети периметра с группами безопасности сети"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: f8622b1d-c07d-4ea6-b41c-4ae98d998fff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 32a40a8dc7539c4c7293988e6c36e5e32ef11045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a>Пример 1 – построение простой сети периметра с использованием групп безопасности сети и классического PowerShell
[Возвращает toohello страница лучшие рекомендации безопасности границ][HOME]

> [!div class="op_single_selector"]
> * [Шаблон Resource Manager](virtual-networks-dmz-nsg.md)
> * [Классическая модель: PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

В этой статье мы создадим простую сеть периметра с четырьмя серверами Windows Server и группами безопасности сети. В этом примере описывается каждая из команд tooprovide hello соответствующие PowerShell более глубокого понимания каждого шага. Имеется также сценарий трафика раздел tooprovide на подробные пошаговые трафик проходит через hello уровней защиты в hello DMZ. Наконец, в разделе references hello hello полный код и должна toobuild инструкция этот tootest среды и эксперимента с помощью различных сценариев. 

![Входящая сеть периметра с группой безопасности сети][1]

## <a name="environment-description"></a>Описание среды
В этом примере подписки содержит hello следующие ресурсы:

* две облачные службы: FrontEnd001 и BackEnd001;
* виртуальная сеть CorpNetwork с двумя подсетями (FrontEnd и BackEnd);
* Сетевую группу безопасности, примененных tooboth подсети
* сервер Windows Server, который представляет веб-сервер приложений (IIS01);
* два сервера Windows Server, представляющих тыловые серверы приложений (AppVM01, AppVM02);
* сервер Windows Server, который представляет DNS-сервер (DNS01).

В разделе "ссылки" hello имеется сценарий PowerShell, который создает большую часть среды hello, описанные в этом примере. Построение hello ВМ и виртуальными сетями, несмотря на то, что может быть выполнено с hello пример скрипта, не подробно описаны в этом документе. 

toobuild hello среды;

1. Сохраните hello сетевой конфигурации XML-файл включаются в раздел ссылок hello (обновлено с именами, расположение и toomatch hello заданному IP адресов сценарий)
2. Переменные пользователя hello обновления в скрипт hello среды hello toomatch hello скрипта является toobe выполняться (подписок, имена служб, и т. д.)
3. Выполните сценарий hello в PowerShell

>[!Note]
>Hello область — в hello сценарий PowerShell должен соответствовать hello область — в XML-файл конфигурации сети hello.
>
>

После hello сценарий выполняется успешно Дополнительные необязательные действия может быть переведена в, в разделе references hello двух сценариев tooset hello веб-сервер и сервер приложений с простой web tooallow приложения, тестирование с помощью этой конфигурации сети Периметра.

Hello следующих разделах подробное описание группы безопасности сети и их использовании в этом примере при рассмотрении ключей строк сценария PowerShell hello.

## <a name="network-security-groups-nsg"></a>Группы безопасности сети
В этом примере создается группа безопасности сети, после чего в нее загружаются шесть правил. 

> [!TIP]
> Вообще говоря следует сначала создать определенные правила «Разрешить», а затем последнего hello более универсальный правила «Deny». Привет, назначается приоритет, определяет, какие правила вычисляются первыми. После обнаружения tooapply tooa конкретного правила трафика вычисляются другим правилам. Правила NSG можно применить в любом в hello входящего и исходящего направления (с точки зрения hello hello подсети).
> 
> 

Создаются декларативно, hello следующие правила для входящего трафика:

1. Внутренний трафик DNS (порт 53) разрешается.
2. RDP (порт 3389) из tooany Интернет hello VM-трафика
3. Может быть HTTP-трафика (порт 80) с сервера tooweb hello Интернета (IIS01)
4. Все (все порты) из IIS01 tooAppVM1-трафика
5. Любой трафик (все порты) из Интернета toohello hello запрещен всей виртуальной сети (оба подсети)
6. Любой трафик (все порты) из hello внешней подсети toohello серверной подсети запрещен

С подсетью привязанного tooeach эти правила, если входящие данные от hello Internet toohello веб-сервера HTTP-запроса оба правила 3 (Разрешить) и 5 (запретить) будет применен, но поскольку правило 3 обладает более высоким приоритетом только он будет применен и правила 5 бы не следует учитывать. Таким образом hello HTTP-запроса допускается toohello веб-сервера. Если же трафик осуществлялось tooreach hello DNS01 server, правило 5 (Deny) бы бы hello первый tooapply и hello трафик не будет разрешен toopass toohello сервера. Правила 6 (Deny) блокирует hello внешней подсети из взаимодействии подсети серверной toohello (за исключением разрешенного трафика в правилах 1 и 4), этот набор правил защищает hello серверной сети в случае, если злоумышленник взломает hello веб-приложения на hello переднего плана, злоумышленник hello бы Серверная часть «защищен» сети (только tooresources, предоставляемые на сервере hello AppVM01) toohello доступ ограничен.

Имеется по умолчанию правило исходящего трафика, которое разрешает трафик, исходящий toohello Интернета. В этом примере мы разрешаем исходящий трафик и не меняем никаких исходящих правил. toolock трафик в обоих направлениях маршрутизации определенные пользователя не требуется и изучены в «Пример 3» на hello [страница лучшие рекомендации безопасности границ][HOME].

Каждое правило является более подробно следующим образом (**Примечание**: любой элемент в hello после списка, начиная со знака доллара (например: $NSGName) является определяемой пользователем переменной из скрипта hello в справочном разделе hello этого документа):

1. Сначала сетевую группу безопасности должны быть построены toohold hello правила:

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. Первое правило Hello в этом примере разрешает трафик DNS между всех внутренних сетей toohello DNS-сервера в подсети серверной hello. правило Hello имеет некоторые важные параметры:
   
   * Параметр Type определяет тип трафика (входящий или исходящий), к которому будет применяться правило. Направление Hello — это с точки зрения hello hello подсети или виртуальной машины (в зависимости от того, где привязан этот NSG). Таким образом Если тип — «Входящие» и трафик вводит hello подсети, hello правило будет применяться и пакетов, отправляемых hello подсети не подвержены этим правилом.
   * «Приоритет» устанавливает hello порядок, в котором вычисляется поток трафика. Hello hello номеров hello выше hello низкоприоритетные. При определенных трафику tooa применяется правило, обрабатываются другим правилам. Таким образом Если правило с приоритетом 1 разрешает трафик и правило с приоритетом 2 запрещает трафика и применяются оба правила tootraffic то трафика hello допускается tooflow (поскольку правило 1 имеет более высокий приоритет он действует и дополнительные правила не были применены).
   * Параметр Action определяет, что нужно делать с трафиком, который подпадает под действие правила, — запретить или разрешить.

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. Это правило позволяет tooflow трафик RDP из hello toohello Интернет RDP-порту на любом сервере в hello привязан подсети. В правиле используется два специальных типа адресных префиксов, VIRTUAL_NETWORK и INTERNET, Эти теги являются легко tooaddress большего категории префиксов адресов.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. Это правило разрешает входящий трафик toohit hello веб-сервер IIS. Это правило не приводит к изменению поведения маршрутизации hello. правило Hello допускает только трафик, предназначенный для IIS01 toopass. Таким образом Если трафика из Интернета hello имел hello веб-сервер в качестве места назначения, это правило будет разрешено и остановить обработку Дополнительные правила. (В hello правило с приоритетом 140 все другие этот трафик блокируется). Если только обработку HTTP-трафика, это правило может быть дальнейших ограниченных tooonly разрешить конечный порт 80.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet too$VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. Это правило позволяет toopass трафик от сервера hello IIS01 toohello AppVM01 сервера, более поздней версии правило блокирует весь остальной трафик tooBackend переднего плана. tooimprove, это правило, если порт hello известно, что должны быть добавлены. Например, если сервер IIS hello попадание SQL Server на AppVM01, диапазон портов назначения hello должен измениться с «*» (Any) too1433 (hello порт сервера SQL) таким образом позволяя меньшего размера входящего атак на AppVM01 следует hello веб-приложение будет скомпрометирован.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] too$VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. Это правило запрещает трафик от Интернет-серверы tooany hello hello сети. Правилам hello с приоритетом 110 и 120 hello эффект tooallow только входящий трафик toohello брандмауэр и порты протокола удаленного рабочего СТОЛА на серверах и блокирует все остальное. Это правило является «резервным» правило tooblock все потоки Непредвиденная.
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $VNetName VNet from hello Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. Hello окончательного правило запрещает трафик от hello внешней подсети toohello серверной подсети. Поскольку это правило является только правила входящего трафика, обратный трафик (от toohello серверной hello переднего плана).

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a>Варианты прохождения трафика
#### <a name="allowed-internet-tooweb-server"></a>(*Разрешено*) tooweb Интернет-сервера
1. Интернет-пользователь запрашивает страницу HTTP от FrontEnd001.CloudApp.Net (облачная служба, открытая для доступа из Интернета)
2. Облачные службы передает трафик через открытую конечную точку на порт 80 по направлению к IIS01 (hello веб-сервера)
3. Подсеть Frontend начинает обработку правила для входящего трафика.
   1. Не применяется правило 1 NSG (DNS), переместите toonext правило
   2. Не применяется правило 2 NSG (RDP), переместите toonext правило
   3. Применить правила NSG 3 (tooIIS01 Интернет), будет разрешен, остановите правила обработки трафика
4. Трафик достигнет внутренний IP-адрес веб-сервера hello IIS01 (10.0.1.5)
5. IIS01 прослушивание веб-трафик, получает этот запрос и начинает обработку запроса hello
6. IIS01 запрашивает hello SQL Server на AppVM01 сведения
7. В подсети Frontend нет правил для обработки исходящего трафика, поэтому трафик разрешается.
8. подсети серверной Hello начинает обработку входящее правило:
   1. Не применяется правило 1 NSG (DNS), переместите toonext правило
   2. Не применяется правило 2 NSG (RDP), переместите toonext правило
   3. Правила NSG 3 (Internet tooFirewall) не применяется, переместите toonext правило
   4. Применить правила NSG 4 (IIS01 tooAppVM01), будет разрешен, остановите правила обработки трафика
9. AppVM01 получает hello SQL-запрос и ответ
10. Поскольку имеются правила для исходящих подключений hello серверной подсети, может быть hello ответа
11. Подсеть Frontend начинает обработку правила для входящего трафика.
    1. Нет правил NSG, применяется tooInbound трафика из hello серверной подсети toohello внешней подсети, поэтому правила NSG hello не выполнены
    2. правило системы по умолчанию Hello, разрешающее трафик между подсетями позволит трафик, трафик hello.
12. Получает ответ SQL hello и завершения hello HTTP-ответ и отправляет запрашивающей стороны toohello Hello сервера IIS
13. Так как имеются правила для исходящих подключений в интерфейсной подсети hello hello ответа может быть и hello Интернета пользователь получает hello веб-страницы при запросе.

#### <a name="allowed-rdp-toobackend"></a>(*Разрешено*) toobackend протокола удаленного рабочего СТОЛА
1. Администратор сервера в Интернете запрашивает tooAppVM01 сеанс RDP в BackEnd001.CloudApp.Net:xxxxx, где xxxxx-hello случайным образом назначенный номер порта для протокола удаленного рабочего СТОЛА tooAppVM01 (hello назначенный порт можно найти на hello портал Azure или с помощью PowerShell)
2. Подсеть BackEnd начинает обработку правила для входящего трафика:
   1. Не применяется правило 1 NSG (DNS), переместите toonext правило
   2. Правило 2 группы безопасности сети (RDP) применяется — трафик разрешается, дальнейшая обработка правил прекращается.
3. Правил для исходящего трафика нет, поэтому применяются правила по умолчанию и обратный трафик разрешается.
4. Начинается сеанс RDP.
5. Запрашивает AppVM01 hello имя пользователя и пароль

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a>DNS-запрос веб-сервера к серверу DNS (*разрешено*)
1. Веб-сервера, IIS01, потребности в www.data.gov, но потребности tooresolve hello адрес канала данных.
2. Hello конфигурацию сети для виртуальной сети hello списков DNS01 (10.0.2.4 подсети hello серверной части) как hello основной DNS-сервер, IIS01 отправляет запрос tooDNS01 hello DNS
3. В подсети Frontend нет правил для обработки исходящего трафика — трафик разрешается.
4. Подсеть BackEnd начинает обработку входящего правила:
   * Правило 1 группы безопасности сети (DNS) применяется — трафик разрешается, дальнейшая обработка правил прекращается.
5. DNS-сервер получает запрос hello
6. DNS-сервер не имеет адреса hello в кэше и запрашивает у корневой сервер DNS на hello Интернета
7. В подсети BackEnd нет правил для исходящего трафика, поэтому трафик разрешается.
8. Internet DNS-сервер отвечает, поскольку этот сеанс был инициирован внутренне, допускается hello ответа
9. DNS-сервер кэширует ответ hello и реагирует назад tooIIS01 toohello исходного запроса
10. В подсети BackEnd нет правил для исходящего трафика, поэтому трафик разрешается.
11. Подсеть Frontend начинает обработку правила для входящего трафика.
    1. Нет правил NSG, применяется tooInbound трафика из hello серверной подсети toohello внешней подсети, поэтому правила NSG hello не выполнены
    2. правило системы по умолчанию Hello, разрешающее трафик между подсетями позволит трафик, трафик hello
12. IIS01 получает hello ответа от DNS01

#### <a name="allowed-web-server-access-file-on-appvm01"></a>Обращение веб-сервера к файлу на сервере AppVM01 (*разрешено*)
1. IIS01 запрашивает файл на AppVM01
2. В подсети Frontend нет правил для обработки исходящего трафика — трафик разрешается.
3. подсети серверной Hello начинает обработку входящее правило:
   1. Не применяется правило 1 NSG (DNS), переместите toonext правило
   2. Не применяется правило 2 NSG (RDP), переместите toonext правило
   3. Правила NSG 3 (Internet tooIIS01) не применяется, переместите toonext правило
   4. Применить правила NSG 4 (IIS01 tooAppVM01), будет разрешен, остановите правила обработки трафика
4. AppVM01 получает запрос hello и высылает файла (при условии, что права доступа)
5. Поскольку имеются правила для исходящих подключений hello серверной подсети, может быть hello ответа
6. Подсеть Frontend начинает обработку правила для входящего трафика.
   1. Нет правил NSG, применяется tooInbound трафика из hello серверной подсети toohello внешней подсети, поэтому правила NSG hello не выполнены
   2. правило системы по умолчанию Hello, разрешающее трафик между подсетями позволит трафик, трафик hello.
7. сервер IIS Hello получает файл hello

#### <a name="denied-web-toobackend-server"></a>(*Отказано в доступе*) toobackend веб-сервера
1. Пользователь Интернета пытается tooaccess файл на AppVM01 через hello BackEnd001.CloudApp.Net службы
2. Поскольку конечные точки не открыты для общего файлового ресурса, этот трафик не будет передан hello облачной службы и не достигают сервера hello
3. Если по некоторым причинам hello конечные точки были открыты, правило NSG 5 (Internet tooVNet) заблокирует этот трафик

#### <a name="denied-web-dns-look-up-on-dns-server"></a>DNS-запрос из Интернета к серверу DNS (*запрещено*)
1. Пользователь Интернета пытается toolook копирование внутренние DNS-запись на DNS01 через hello BackEnd001.CloudApp.Net службы
2. Поскольку конечные точки не открыты для DNS, трафик не будет передан hello облачной службы и не достигают сервера hello
3. Если по некоторым причинам hello конечные точки были открыты, правило NSG 5 (Internet tooVNet) заблокирует этот трафик (Примечание: 1 правило (DNS) не будут применяться по двум причинам, исходный адрес первого hello hello Интернета, это правило применяется только toohello также виртуальной локальной сети как hello источника Это правило является разрешающее правило, поэтому она никогда не будет запрещать трафик)

#### <a name="denied-web-toosql-access-through-firewall"></a>(*Отказано в доступе*) Web access tooSQL через брандмауэр
1. Интернет-пользователь запрашивает данные SQL из FrontEnd001.CloudApp.Net (облачная служба, открытая для доступа через Интернет)
2. Поскольку конечные точки не открыты для SQL, такой трафик не будет передан hello облачной службы и не достичь hello брандмауэра
3. Если конечные точки были открыты для какой-либо причине, hello внешней подсети начинает обработку входящее правило:
   1. Не применяется правило 1 NSG (DNS), переместите toonext правило
   2. Не применяется правило 2 NSG (RDP), переместите toonext правило
   3. Применить правила NSG 3 (tooIIS01 Интернет), будет разрешен, остановите правила обработки трафика
4. Трафик достигнет внутренний IP-адрес hello IIS01 (10.0.1.5)
5. IIS01 не прослушивает порт 1433, без запроса toohello ответа

## <a name="conclusion"></a>Заключение
В этом примере является относительно простой и простым способом изоляции hello внутренней подсети из входящего трафика.

Дополнительные примеры и общие сведения о периметре безопасности сети можно найти [здесь][HOME].

## <a name="references"></a>Ссылки
### <a name="main-script-and-network-config"></a>Основной сценарий и конфигурация сети
Сохраните hello полный скрипт в файл скрипта PowerShell. Сохранить hello сетевой конфигурации в файл с именем «NetworkConf1.xml.»
Изменение определяемых пользователем переменных hello как hello необходимые и выполнения скрипта.

#### <a name="full-script"></a>Полный сценарий
Этот скрипт будет на основе hello определяемых пользователем переменных;

1. Подключение tooan подписки Azure
2. Создайте учетную запись хранения.
3. Создание виртуальной сети и две подсети, как определено в файле конфигурации сети hello
4. Создаст четыре сервера виртуальных машин под управлением Windows.
5. Настроит группу безопасности сети:
   * Создание группы безопасности сети
   * добавит в нее правила;
   * Привязка hello NSG toohello соответствующие подсети

Этот сценарий PowerShell должен запускаться локально на ПК или сервере, подключенном к Интернету.

> [!IMPORTANT]
> При запуске этого сценария могут выдаваться предупреждения и другие информационные сообщения PowerShell. Обращать внимание следует только на сообщения об ошибках, выделенные красным цветом.
> 
>

```PowerShell
<# 
 .SYNOPSIS
  Example of Network Security Groups in an isolated network (Azure only, no hybrid connections)

 .DESCRIPTION
  This script will build out a sample DMZ setup containing:
   - A default storage account for VM disks
   - Two new cloud services
   - Two Subnets (FrontEnd and BackEnd subnets)
   - One server on hello FrontEnd Subnet
   - Three Servers on hello BackEnd Subnet
   - Network Security Groups tooallow/deny traffic patterns as declared

  Before running script, ensure hello network configuration file is created in
  hello directory referenced by $NetworkConfigFile variable (or update the
  variable tooreflect hello path and file name of hello config file being used).

 .Notes
  Security requirements are different for each use case and can be addressed in a
  myriad of ways. Please be sure that any sensitive data or applications are behind
  hello appropriate layer(s) of protection. This script serves as an example of some
  of hello techniques that can be used, but should not be used for all scenarios. You
  are responsible tooassess your security needs and hello appropriate protections
  needed, and then effectively implement those protections.

  FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
   IIS01      - 10.0.1.5

  BackEnd Service (BackEnd subnet 10.0.2.0/24)
   DNS01      - 10.0.2.4
   AppVM01    - 10.0.2.5
   AppVM02    - 10.0.2.6

#>

# Fixed Variables
    $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
    $VMName = @()
    $ServiceName = @()
    $VMFamily = @()
    $img = @()
    $size = @()
    $SubnetName = @()
    $VMIP = @()

# User-Defined Global Variables
  # These should be changes tooreflect your subscription and services
  # Invalid options will fail in hello validation section

  # Subscription Access Details
    $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

  # VM Account, Location, and Storage Details
    $LocalAdmin = "theAdmin"
    $DeploymentLocation = "Central US"
    $StorageAccountName = "vmstore02"

  # Service Details
    $FrontEndService = "FrontEnd001"
    $BackEndService = "BackEnd001"

  # Network Details
    $VNetName = "CorpNetwork"
    $FESubnet = "FrontEnd"
    $FEPrefix = "10.0.1.0/24"
    $BESubnet = "BackEnd"
    $BEPrefix = "10.0.2.0/24"
    $NetworkConfigFile = "C:\Scripts\NetworkConf1.xml"

  # VM Base Disk Image Details
    $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

  # NSG Details
    $NSGName = "MyVNetSG"

# User-Defined VM Specific Configuration
    # Note: tooensure proper NSG Rule creation later in this script:
    #       - hello Web Server must be VM 0
    #       - hello AppVM1 Server must be VM 1
    #       - hello DNS server must be VM 3
    #
    #       Otherwise hello NSG rules in hello last section of this
    #       script will need toobe changed toomatch hello modified
    #       VM array numbers ($i) so hello NSG Rule IP addresses
    #       are aligned toohello associated VM IP addresses.

    # VM 0 - hello Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - hello First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - hello Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - hello DNS Server
      $VMName += "DNS01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.4"

# ----------------------------- #
# No User-Defined Variables or  #
# Configuration past this point #
# ----------------------------- #    

  # Get your Azure accounts
    Add-AzureAccount
    Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
    Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

  # Create Storage Account
    If (Test-AzureName -Storage -Name $StorageAccountName) { 
        Write-Host "Fatal Error: This storage account name is already in use, please pick a different name." -ForegroundColor Red
        Return}
    Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
          New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

  # Update Subscription Pointer tooNew Storage Account
    Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
    Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

# Validation
$FatalError = $false

If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
     Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
     $FatalError = $true}

If (Test-AzureName -Service -Name $FrontEndService) { 
    Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

If (Test-AzureName -Service -Name $BackEndService) { 
    Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

If (-Not (Test-Path $NetworkConfigFile)) { 
    Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "hello network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation variable is correct and hello network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see hello above messages for more information." -ForegroundColor Red
    Return}
Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

# Create VNET
    Write-Host "Creating VNET" -ForegroundColor Cyan 
    Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

# Create Services
    Write-Host "Creating Services" -ForegroundColor Cyan
    New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
    New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

# Build VMs
    $i=0
    $VMName | Foreach {
        Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
        New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
            Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
            Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
            Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
            Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
            Remove-AzureEndpoint -Name "PowerShell" | `
            New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
            # Note: A Remote Desktop endpoint is automatically created when each VM is created.
        $i++
    }
    # Add HTTP Endpoint for IIS01
    Get-AzureVM -ServiceName $ServiceName[0] -Name $VMName[0] | Add-AzureEndpoint -Name HTTP -Protocol tcp -LocalPort 80 -PublicPort 80 | Update-AzureVM

# Configure NSG
    Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

  # Build hello NSG
    Write-Host "Building hello NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) too$($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
        -Protocol *

    # Assign hello NSG toohello Subnets
        Write-Host "Binding hello NSG tooboth subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

# Optional Post-script Manual Configuration
  # Install Test Web App (Run Post-Build Script on hello IIS Server)
  # Install Backend resource (Run Post-Build Script on hello AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a>Файл конфигурации сети
Сохраните этот файл xml с новое местоположение и добавьте переменной toohello $NetworkConfigFile файл toothis link hello в hello предшествующий скрипта.

```XML
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns>
      <DnsServers>
        <DnsServer name="DNS01" IPAddress="10.0.2.4" />
        <DnsServer name="Level3" IPAddress="209.244.0.3" />
      </DnsServers>
    </Dns>
    <VirtualNetworkSites>
      <VirtualNetworkSite name="CorpNetwork" Location="Central US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="FrontEnd">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="BackEnd">
            <AddressPrefix>10.0.2.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
        <DnsServersRef>
          <DnsServerRef name="DNS01" />
          <DnsServerRef name="Level3" />
        </DnsServersRef>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

#### <a name="sample-application-scripts"></a>Примеры сценариев приложения
При желании tooinstall образец приложения для этого и других примерах DMZ, оно предоставлено в hello по ссылке: [образец приложения скрипта][SampleApp]

## <a name="next-steps"></a>Дальнейшие действия
* Обновите и сохраните XML-файл
* Запустите среду hello toobuild сценария PowerShell hello
* Установите пример приложения hello
* Проверьте прохождение разных потоков трафика через эту сеть периметра.

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "Входящая сеть периметра с группой безопасности сети"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

