---
title: "Пример: aaaDMZ создавать DMZ tooprotect приложения с брандмауэром, Nsg | Документы Microsoft"
description: "Построение сети периметра с брандмауэром и группами безопасности сети"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: c78491c7-54ac-4469-851c-b35bfed0f528
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: 18f116dc3897567bff14a509ae8c13f449182bfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="example-2--build-a-dmz-tooprotect-applications-with-a-firewall-and-nsgs"></a>Пример 2 — создавать DMZ tooprotect приложения с брандмауэром, Nsg
[Возвращает toohello страница лучшие рекомендации безопасности границ][HOME]

В этом примере будет создана сеть периметра с брандмауэром, четырьмя серверами Windows Server и группами безопасности сети. Он также поможет выполнить каждого из соответствующих команд tooprovide hello более глубокого понимания каждого шага. Имеется также сценарий трафика раздел tooprovide на подробные пошаговые трафик проходит через hello уровней защиты в hello DMZ. Наконец, в разделе references hello hello полный код и должна toobuild инструкция этот tootest среды и эксперимента с помощью различных сценариев. 

![Входящий DMZ с Уязвимости и NSG][1]

## <a name="environment-description"></a>Описание среды
В этом примере имеется подписка, содержащий hello следующее:

* две облачные службы: FrontEnd001 и BackEnd001;
* виртуальная сеть CorpNetwork с двумя подсетями (FrontEnd и BackEnd);
* Одну группу безопасности сети, будет применен tooboth подсети
* Устройство виртуальной сети, в этом примере брандмауэр Barracuda NextGen, подключен toohello внешней подсети
* сервер Windows Server, который представляет веб-сервер приложений (IIS01);
* два сервера Windows Server, представляющих тыловые серверы приложений (AppVM01, AppVM02);
* сервер Windows Server, который представляет DNS-сервер (DNS01).

> [!NOTE]
> Несмотря на то, что в этом примере используется брандмауэр Barracuda NextGen, многие из разных виртуальных сетевых устройств, которые могут использоваться в этом примере приветствия.
> 
> 

В разделе references hello ниже имеется сценарий PowerShell, построит большая часть среды hello, описанных выше. Построение hello ВМ и виртуальными сетями, несмотря на то, что может быть выполнено с hello пример скрипта, не подробно описаны в этом документе.

Среда toobuild hello.

1. Сохраните hello сетевой конфигурации XML-файл включаются в раздел ссылок hello (обновлено с именами, расположение и toomatch hello заданному IP адресов сценарий)
2. Переменные пользователя hello обновления в скрипт hello среды hello toomatch hello скрипта является toobe выполняться (подписок, имена служб, и т. д.)
3. Выполните сценарий hello в PowerShell

**Примечание**: hello область — в hello сценарий PowerShell должен соответствовать hello область — в XML-файл конфигурации сети hello.

После успешного выполнения сценария hello может быть переведена hello следующие шаги после сценария:

1. Настройка правил брандмауэра hello, это рассматривается в hello ниже раздел: правила брандмауэра.
2. При необходимости в разделе references hello являются двумя tooset сценарии hello веб-сервер и сервер приложений с простой web tooallow приложения, тестирование с помощью этой конфигурации сети Периметра.

Hello следующем разделе показано большинство hello сценарии операторы относительных tooNetwork групп безопасности.

## <a name="network-security-groups-nsg"></a>Группы безопасности сети
В этом примере создается группа безопасности сети, после чего в нее загружаются шесть правил. 

> [!TIP]
> Вообще говоря следует сначала создать определенные правила «Разрешить», а затем последнего hello более универсальный правила «Deny». Привет, назначается приоритет, определяет, какие правила вычисляются первыми. После обнаружения tooapply tooa конкретного правила трафика вычисляются другим правилам. Правила NSG можно применить в любом в hello входящего и исходящего направления (с точки зрения hello hello подсети).
> 
> 

Создаются декларативно, hello следующие правила для входящего трафика:

1. Внутренний трафик DNS (порт 53) разрешается.
2. RDP (порт 3389) из tooany Интернет hello VM-трафика
3. Может быть HTTP-трафика (порт 80) из Интернета hello toohello NVA (брандмауэром)
4. Все (все порты) из IIS01 tooAppVM1-трафика
5. Любой трафик (все порты) из Интернета toohello hello запрещен всей виртуальной сети (оба подсети)
6. Любой трафик (все порты) из hello внешней подсети toohello серверной подсети запрещен

С подсетью привязанного tooeach эти правила, если входящие данные от hello Internet toohello веб-сервера HTTP-запроса оба правила 3 (Разрешить) и 5 (запретить) будет применен, но поскольку правило 3 обладает более высоким приоритетом только он будет применен и правила 5 бы не следует учитывать. Таким образом запрос hello HTTP допустимы toohello брандмауэра. Если же трафик осуществлялось tooreach hello DNS01 server, правило 5 (Deny) бы бы hello первый tooapply и hello трафик не будет разрешен toopass toohello сервера. Правила 6 внешней подсети hello (Deny) блоки из взаимодействии подсети серверной toohello (за исключением разрешенного трафика в правилах 1 и 4), это позволяет защитить hello серверной сети, если злоумышленник взломает hello веб-приложения на hello переднего плана, hello злоумышленник ограниченный доступ toohello серверной» защищенной» (только tooresources, предоставляемые на сервере AppVM01 hello).

Имеется по умолчанию правило исходящего трафика, которое разрешает трафик, исходящий toohello Интернета. В этом примере мы разрешаем исходящий трафик и не меняем никаких исходящих правил. toolock трафик в обоих направлениях маршрутизации определенные пользователя не требуется, это изучена в другой пример, в котором можно найти в hello [документа границ безопасности основного][HOME].

описанные выше Hello правила NSG являются очень схожие правила NSG toohello в [пример 1 - построение простого DMZ с Nsg][Example1]. Просмотрите hello NSG описание в этом документе для подробное описание каждого правила NSG и его атрибуты.

## <a name="firewall-rules"></a>Правила брандмауэра
Клиент управления будет требуется toobe установлен брандмауэр hello toomanage ПК и создавать hello конфигурациях. См. документации из брандмауэр (или другие Уязвимости) поставщика hello как toomanage hello устройства. Hello оставшейся части данного раздела описывается hello конфигурации брандмауэра hello, через hello клиент управления поставщиков (т. е. не hello портал Azure или PowerShell).

Инструкции по загрузки клиента и подключении toohello Barracuda используется в этом примере можно найти здесь: [Barracuda NG администратора](https://techlib.barracuda.com/NG61/NGAdmin)

На брандмауэре hello правила перенаправления потребуется создать toobe. Так как в этом примере только направляет трафик входящих toohello при использовании брандмауэра, а затем toohello веб-сервера, пересылки только одно правило NAT необходим. На hello брандмауэр Barracuda NextGen, используемых в этом примере hello правило будет NAT назначения правила toopass («Dst NAT») этого трафика.

toocreate hello следующих правил (или проверить существующие правила по умолчанию), начиная с панели мониторинга клиент Barracuda NG Admin hello, перейдите на вкладку Конфигурация toohello, в hello рабочей конфигурации нажмите кнопку набора правил. Вызывается сетку, «Main правила» будет отображаться hello существующие активные и неактивные правила брандмауэра hello. Верхний правый угол hello сетки является небольшой, зеленый «+», выберите элемент этого toocreate новое правило (Примечание: брандмауэра «заблокирована» для изменения, если помечены кнопки «Блокировка» и, не удается toocreate или изменение правил, нажмите кнопку эта кнопка слишком «разблокировать» hello набор правил и разрешить изменение). При желании tooedit существующее правило, выберите это правило, щелкните правой кнопкой мыши и выберите команду Изменить правило.

Создайте новое правило и укажите имя правила, например WebTraffic. 

значок правила NAT назначения Hello выглядит следующим образом: ![NAT значок назначения][2]

само правило Hello будет выглядеть примерно следующим образом:

![Правила брандмауэра][3]

Здесь адреса входящего трафика, что попаданий hello брандмауэра попытки tooreach HTTP (порт 80 или 443 для HTTPS) будут отправлены Здравствуйте, «Локальные DHCP1 IP-адрес» интерфейс и перенаправленный toohello веб-сервер с IP-адрес 10.0.1.5 hello брандмауэра. Поскольку hello трафик поступает порт 80 и постоянной toohello веб-сервера на порт 80 без изменений порт не требовались. Тем не менее целевой список были бы 10.0.1.5:8080 Если веб-сервере прослушивал порт 8080 таким образом выполнении приветствия hello входящий порт 80 hello брандмауэра tooinbound порт 8080 hello веб-сервера.

Метод подключения должны также быть обозначать, для hello правила назначения из Интернета, hello «Динамического SNAT» лучше всего подходит. 

Несмотря на то что было создано только одно правило, важно правильно задать его приоритет. Если в сетке hello всех правил в брандмауэре hello это новое правило нижней hello (см. ниже правило «BLOCKALL» hello) никогда не перейдет в игру. Убедитесь, что выше правила BLOCKALL hello hello вновь созданные правила для веб-трафика.

После создания правила hello, он должен быть принудительно отправлены toohello брандмауэра и затем активируется, если этого не сделать hello правило, изменения не вступят в силу. Hello принудительной отправки и активации процесс описан в следующем разделе hello.

## <a name="rule-activation"></a>Активация правил
С hello ruleset изменен tooadd это правило, hello ruleset должен быть отправлен toohello брандмауэра и активации.

![Активация правила брандмауэра][4]

В правом верхнем углу hello клиент управления hello являются кластера кнопок. Щелкните toohello «Изменения отправить «hello кнопка toosend hello изменены правила брандмауэра, а затем нажмите кнопку «Активировать» hello.

Hello активации из набора правил брандмауэра hello с этой сборкой среды пример завершена. При необходимости скрипты сборки hello post в hello ссылки на раздел может быть запустите tooadd среды tootest приложения toothis hello ниже сценарии трафика.

> [!IMPORTANT]
> Это критическое toorealize, что вы не столкнутся hello веб-сервер напрямую. Когда браузер запрашивает страницу HTTP из FrontEnd001.CloudApp.Net, hello HTTP (порт 80) конечная точка передает этот брандмауэр toohello трафик не hello веб-сервер. Здравствуйте брандмауэра, затем toohello правила в соответствии с созданным ранее, NAT, запрашивающих toohello веб-сервера.
> 
> 

## <a name="traffic-scenarios"></a>Варианты прохождения трафика
#### <a name="allowed-web-tooweb-server-through-firewall"></a>(Разрешено) TooWeb Web Server через брандмауэр
1. Интернет-пользователь запрашивает страницу HTTP из FrontEnd001.CloudApp.Net (облачная служба, открытая для доступа через Интернет)
2. Облачные службы передает трафик через открытую конечную точку в локальном интерфейсе toofirewall порт 80 на 10.0.1.4:80
3. Подсеть Frontend начинает обработку правила для входящего трафика.
   1. Не применяется правило 1 NSG (DNS), переместите toonext правило
   2. Не применяется правило 2 NSG (RDP), переместите toonext правило
   3. Применить правила NSG 3 (tooFirewall Интернет), будет разрешен, остановите правила обработки трафика
4. Трафик достигнет внутренний IP-адрес брандмауэра hello (10.0.1.4)
5. Правило пересылки брандмауэра см. это трафик на порт 80, происходит его перенаправление веб-сервере toohello IIS01
6. IIS01 прослушивание веб-трафик, получает этот запрос и начинает обработку запроса hello
7. IIS01 запрашивает hello SQL Server на AppVM01 сведения
8. В подсети Frontend нет правил для обработки исходящего трафика — трафик разрешается.
9. подсети серверной Hello начинает обработку входящее правило:
   1. Не применяется правило 1 NSG (DNS), переместите toonext правило
   2. Не применяется правило 2 NSG (RDP), переместите toonext правило
   3. Правила NSG 3 (Internet tooFirewall) не применяется, переместите toonext правило
   4. Применить правила NSG 4 (IIS01 tooAppVM01), будет разрешен, остановите правила обработки трафика
10. AppVM01 получает hello SQL-запрос и ответ
11. Так как имеются может быть не правила для исходящих подключений на hello ответа hello подсети серверной части
12. Подсеть Frontend начинает обработку правила для входящего трафика.
    1. Нет правил NSG, применяется tooInbound трафика из hello серверной подсети toohello внешней подсети, поэтому правила NSG hello не выполнены
    2. правило системы по умолчанию Hello, разрешающее трафик между подсетями позволит трафик, трафик hello.
13. Получает ответ SQL hello и завершения hello HTTP-ответ и отправляет запрашивающей стороны toohello Hello сервера IIS
14. Поскольку это сеанс NAT из брандмауэра hello, назначение ответа hello (первоначально) — для hello брандмауэра
15. брандмауэр Hello получает hello ответа от hello веб-сервера и пересылает задней toohello пользователя Интернета
16. Так как имеются исходящего правила на hello интерфейсной подсети hello ответа не допускается, и hello пользователя Интернета получает hello веб-страницы, в запросе.

#### <a name="allowed-rdp-toobackend"></a>(Разрешено) TooBackend протокола удаленного рабочего СТОЛА
1. Администратор сервера в Интернете запрашивает tooAppVM01 сеанс RDP в BackEnd001.CloudApp.Net:xxxxx, где xxxxx-hello случайным образом назначенный номер порта для протокола удаленного рабочего СТОЛА tooAppVM01 (hello назначенный порт можно найти на портале Azure hello или с помощью PowerShell)
2. С момента hello, брандмауэр только прослушивание hello FrontEnd001.CloudApp.Net адрес он не участвует в этот поток трафика
3. Подсеть BackEnd начинает обработку правила для входящего трафика:
   1. Не применяется правило 1 NSG (DNS), переместите toonext правило
   2. Правило 2 группы безопасности сети (RDP) применяется — трафик разрешается, дальнейшая обработка правил прекращается.
4. Правил для исходящего трафика нет, поэтому применяются правила по умолчанию и обратный трафик разрешается.
5. Начинается сеанс RDP.
6. Сервер AppVM01 запрашивает имя пользователя и пароль.

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a>DNS-запрос веб-сервера к серверу DNS (разрешено) 
1. Веб-сервера, IIS01, потребности в www.data.gov, но потребности tooresolve hello адрес канала данных.
2. Hello конфигурацию сети для виртуальной сети hello списков DNS01 (10.0.2.4 подсети hello серверной части) как hello основной DNS-сервер, IIS01 отправляет запрос tooDNS01 hello DNS
3. В подсети Frontend нет правил для обработки исходящего трафика — трафик разрешается.
4. Подсеть BackEnd начинает обработку входящего правила:
   1. Правило 1 группы безопасности сети (DNS) применяется — трафик разрешается, дальнейшая обработка правил прекращается.
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

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(Разрешено) Веб-сервер обращается к файлу на AppVM01
1. IIS01 запрашивает файл на AppVM01
2. В подсети Frontend нет правил для обработки исходящего трафика — трафик разрешается.
3. подсети серверной Hello начинает обработку входящее правило:
   1. Не применяется правило 1 NSG (DNS), переместите toonext правило
   2. Не применяется правило 2 NSG (RDP), переместите toonext правило
   3. Правила NSG 3 (Internet tooFirewall) не применяется, переместите toonext правило
   4. Применить правила NSG 4 (IIS01 tooAppVM01), будет разрешен, остановите правила обработки трафика
4. AppVM01 получает запрос hello и высылает файла (при условии, что права доступа)
5. Так как имеются может быть не правила для исходящих подключений на hello ответа hello подсети серверной части
6. Подсеть Frontend начинает обработку правила для входящего трафика.
   1. Нет правил NSG, применяется tooInbound трафика из hello серверной подсети toohello внешней подсети, поэтому правила NSG hello не выполнены
   2. правило системы по умолчанию Hello, разрешающее трафик между подсетями позволит трафик, трафик hello.
7. сервер IIS Hello получает файл hello

#### <a name="denied-web-direct-tooweb-server"></a>(Запрещено) Прямой tooWeb Web Server
С момента hello веб-сервера, IIS01 и hello брандмауэра в hello одной облачной службе, они совместно используют hello же открытый IP-адреса. Таким образом будет направляться трафик HTTP toohello брандмауэра. Хотя бы успешно предоставил hello запроса, не может ссылаться непосредственно toohello веб-сервера, он прошел, как было задумано, сначала через hello брандмауэра. В разделе hello первый сценарий в этом разделе для потока трафика hello.

#### <a name="denied-web-toobackend-server"></a>(Запрещено) Веб-сервера tooBackend
1. Пользователь Интернета пытается tooaccess файл на AppVM01 через hello BackEnd001.CloudApp.Net службы
2. Поскольку конечные точки не открыты для общего файлового ресурса, это не будет передан hello облачной службы и не достигают сервера hello
3. Если по некоторым причинам hello конечные точки были открыты, правило NSG 5 (Internet tooVNet) заблокирует этот трафик

#### <a name="denied-web-dns-lookup-on-dns-server"></a>(Запрещено) DNS-запрос из Интернета к серверу DNS
1. Пользователь Интернета пытается toolookup внутренние DNS-запись на DNS01 через hello BackEnd001.CloudApp.Net службы
2. Поскольку конечные точки не открыты для DNS, это не будет передан hello облачной службы и не достигают сервера hello
3. Если по некоторым причинам hello конечные точки были открыты, правило NSG 5 (Internet tooVNet) заблокирует этот трафик (Примечание: 1 правило (DNS) не будут применяться по двум причинам, исходный адрес первого hello hello Интернета, это правило применяется только toohello также виртуальной локальной сети как hello источника Это правило разрешить, поэтому она никогда не будет запрещать трафик)

#### <a name="denied-web-toosql-access-through-firewall"></a>(Запрещено) Веб-tooSQL доступ через брандмауэр
1. Интернет-пользователь данные SQL из FrontEnd001.CloudApp.Net (облачная служба, открытая для доступа через Интернет)
2. Поскольку конечные точки не открыты для SQL, это не будет передан hello облачной службы и не будет достигнут hello брандмауэра
3. Если конечные точки были открыты для какой-либо причине, hello внешней подсети начинает обработку входящее правило:
   1. Не применяется правило 1 NSG (DNS), переместите toonext правило
   2. Не применяется правило 2 NSG (RDP), переместите toonext правило
   3. Применить правило NSG 2 (Internet tooFirewall), будет разрешен, остановите правила обработки трафика
4. Трафик достигнет внутренний IP-адрес брандмауэра hello (10.0.1.4)
5. Нет правила перенаправления имеет брандмауэр для SQL и удаляет hello трафика

## <a name="conclusion"></a>Заключение
Этот способ относительно прост для защиты приложения с брандмауэром и изоляции hello серверной части подсети из входящего трафика.

Дополнительные примеры и общие сведения о периметре безопасности сети можно найти [здесь][HOME].

## <a name="references"></a>Ссылки
### <a name="main-script-and-network-config"></a>Основной сценарий и конфигурация сети
Сохраните hello полный скрипт в файл скрипта PowerShell. Сохраните hello сетевой конфигурации в файл с именем «NetworkConf2.xml».
При необходимости измените hello определенные пользователем переменные. Запустите сценарий hello, а затем выполните hello брандмауэра правила установки инструкции выше.

#### <a name="full-script"></a>Полный сценарий
Этот скрипт будет, на основе hello определяемых пользователем переменных:

1. Подключение tooan подписки Azure
2. Создание новой учетной записи хранения
3. Создайте новую виртуальную сеть и две подсети, как определено в файле конфигурации сети hello
4. Создаст четыре виртуальные машины под управлением Windows Server.
5. Настроит группу безопасности сети:
   * создаст группу безопасности сети;
   * добавит в нее правила;
   * Привязка hello NSG toohello соответствующие подсети

Этот сценарий PowerShell должен запускаться локально на ПК или сервере, подключенном к Интернету.

> [!IMPORTANT]
> При запуске этого сценария могут выдаваться предупреждения и другие информационные сообщения PowerShell. Обращать внимание следует только на сообщения об ошибках, выделенные красным цветом.
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and Network Security Groups in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Two new cloud services
       - Two Subnets (FrontEnd and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet (plus hello NVA on hello FrontEnd subnet)
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
       myFirewall - 10.0.1.4
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

    # User Defined Global Variables
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
        $NetworkConfigFile = "C:\Scripts\NetworkConf2.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure proper NSG Rule creation later in this script:
        #       - hello Web Server must be VM 1
        #       - hello AppVM1 Server must be VM 2
        #       - hello DNS server must be VM 4
        #
        #       Otherwise hello NSG rules in hello last section of this
        #       script will need toobe changed toomatch hello modified
        #       VM array numbers ($i) so hello NSG Rule IP addresses
        #       are aligned toohello associated VM IP addresses.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
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
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
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
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: Web traffic goes through hello firewall, so we'll need tooset up a HTTP endpoint.
                #       Also, hello firewall will be redirecting web traffic tooa new IP and Port in a
                #       forwarding rule, so hello HTTP endpoint here will have hello same public and local
                #       port and hello firewall will do hello NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                    # Note: A Remote Desktop endpoint is automatically created when each VM is created.
                }
            $i++
        }

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) too$($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
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
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a>Файл конфигурации сети
Сохраните этот файл xml с новое местоположение и добавьте ссылку toothis hello файл toohello $NetworkConfigFile переменной в представленном выше сценарии hello.

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

#### <a name="sample-application-scripts"></a>Сценарии примера приложения
При желании tooinstall образец приложения для этого и других примерах DMZ, оно предоставлено в hello по ссылке: [образец приложения скрипта][SampleApp]

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "Входящая сеть периметра с группой безопасности сети"
[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Значок NAT назначения"
[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Правило брандмауэра"
[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Активация правила брандмауэра"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
