---
title: "aaaCreating и использовании внутренней подсистемы балансировки нагрузки с помощью среды службы приложений | Документы Microsoft"
description: "Создание и использование ASE с внутренним балансировщиком нагрузки."
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: ad9a1e00-d5e5-413e-be47-e21e5b285dbf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 20799f260993d6e81499408e5b547a2e21430174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-an-internal-load-balancer-with-an-app-service-environment"></a>Использование внутреннего балансировщика нагрузки в среде службы приложений

> [!NOTE] 
> Эта статья является о hello v1 среды службы приложений. Имеется более новая версия hello среды службы приложений, удобнее toouse и выполняется на более мощный инфраструктуры. Дополнительные сведения о новой версии hello начинаться с hello toolearn [toohello введение среды службы приложений](../app-service/app-service-environment/intro.md).
>

функция Hello среды службы приложений (ASE) — это параметр службы Premium службы приложения Azure, которая обеспечивает возможность расширенной настройки, недоступные в hello отметки нескольких клиентов. функция ASE Hello фактически развертывает hello службе приложений Azure в вашей виртуальной Network(VNet) Azure. toogain предлагаемых лучшего понимания возможностей hello по среды службы приложения чтения hello [возможности среды службы приложений] [ WhatisASE] документации. Если вы не знаете, преимущества hello в виртуальной сети чтения hello [Azure виртуальные сети часто задаваемые вопросы о][virtualnetwork]. 

## <a name="overview"></a>Обзор
ASE может развертываться с конечной точкой, доступной из Интернета, или IP-адресом в вашей виртуальной сети. В порядке tooset hello IP адрес tooa адрес виртуальной сети необходимо toodeploy вашей ASE с внутренней Balancer(ILB) нагрузки. Настройка среды ASE с внутренним балансировщиком нагрузки обеспечивает следующие возможности.

* Ваш собственный домен или поддомен. toomake легким, данный документ предполагает дочерний домен, но его можно настроить в любом случае. 
* Hello сертификат, используемый для HTTPS
* Управление DNS для поддомена. 

Это дает следующие возможности:

* хост-приложения интрасети, как бизнес-приложения, безопасно хранятся на hello облако какой доступ через сайт tooSite или ExpressRoute VPN
* узел приложения в облаке hello, не перечисленных в общедоступные DNS-серверы
* создание изолированных от Интернета внутренних приложений, с которыми можно безопасно интегрировать свои внешние приложения.

#### <a name="disabled-functionality"></a>Отключенные функциональные возможности
Существуют некоторые функции, недоступные при использовании ASE с внутренним балансировщиком нагрузки. К ним относятся:

* использование SSL на основе IP;
* Назначение IP-адресов toospecific приложений
* приобретение и использование сертификатов при приложения через портал hello. Конечно по-прежнему можно получить сертификаты непосредственно с центром сертификации и использовать его в приложениях не только через портал Azure hello.

## <a name="creating-an-ilb-ase"></a>Создание ASE с внутренним балансировщиком нагрузки
Создание ASE с внутренним балансировщиком нагрузки не сильно отличается от создания ASE обычным образом. Подробное обсуждение создания ASE чтения [как tooCreate среды службы приложений][HowtoCreateASE]. toocreate процесс Hello — ILB ASE hello совпадают создания виртуальной сети во время создания ASE или выбора существующей виртуальной сети. toocreate ILB ASE: 

1. В hello Azure портала выберите **New -> Web + Mobile -> среды службы приложений**
2. Выберите свою подписку.
3. Выберите или создайте группу ресурсов.
4. Выберите или создайте виртуальную сеть.
5. Создайте подсеть, если была выбрана виртуальная сеть.
6. Выберите **виртуальной сети "->" Конфигурация виртуальной сети** и набор hello tooInternal тип виртуального IP-адреса
7. Введите имя дочернего домена (это будет hello дочерний домен, используемый для приложений, созданных в этом ASE)
8. Нажмите кнопку "ОК", а затем — "Создать".

![][1]

В колонке hello виртуальной сети есть параметр конфигурации виртуальной сети. Он позволяет выбрать внешний или внутренний виртуальный IP-адрес. по умолчанию Hello — External. Если эти параметры настроены tooExternal вашей ASE будет использовать Интернет доступных виртуальных IP-адресов. Если выбрать внутренний виртуальный IP-адрес, то для ASE будет настроен внутренний балансировщик нагрузки с IP-адресом в виртуальной сети. 

После выбора для внутреннего использования, hello возможность tooadd несколько IP-адресов tooyour ASE удаляется и вместо этого потребуется поддомен hello tooprovide hello ASE. В ASE с hello внешних виртуальных IP-адресов имя hello ASE для приложений, созданных в этом ASE используется в поддомен hello. Если ваш ASE вызывался ***contosotest*** и приложения в этом ASE был вызван ***mytest*** то hello дочернего домена будет hello формата ***contosotest.p.azurewebsites.net*** и Hello URL-адрес для этого приложения будет ***mytest.contosotest.p.azurewebsites.net***. Если задать hello tooInternal тип виртуального IP-адреса, ваше имя ASE не используется в поддомен hello для hello ASE. Явно укажите поддомен hello. Если был дочернего домена ***contoso.corp.net*** и сделать приложение в том, что с именем ASE ***timereporting*** Здравствуйте URL-адрес, для этого приложения будет ***timereporting.contoso.corp.net***.

## <a name="apps-in-an-ilb-ase"></a>Приложения в ASE с внутренним балансировщиком нагрузки
Создание приложения в ILB ASE hello такой же, как создание приложения в ASE обычным образом. 

1. В hello Azure портала выберите **New -> Web + Mobile -> Web** или **Mobile** или **приложения API**
2. Введите имя приложения.
3. Выберите подписку.
4. Выберите или создайте группу ресурсов.
5. Выберите или создайте план службы приложений. Создание нового ASP затем выберите ваш ASE как расположение hello и выберите hello рабочего пула следует ли ваш toobe ASP, созданные в. При создании hello ASP указать вашей ASE в качестве расположения hello hello рабочего пула. При указании имени hello приложения hello, вы увидите hello поддомен в списке имя вашего приложения заменяется hello дочерний домен для вашей ASE. 
6. Нажмите кнопку Создать. Следует выбрать hello **toodashboard ПИН-код** флажок, если необходимо tooshow приложения hello на информационной панели. 

![][2]

В приложение hello имя поддомена hello имя получает обновленные tooreflect поддомен hello вашей ASE. 

## <a name="post-ilb-ase-creation-validation"></a>Проверка после создания ASE с внутренним балансировщиком нагрузки
ILB ASE немного отличается от hello не - ILB ASE. Как уже отмечалось, необходимо toomanage собственный DNS-сервера, а также tooprovide собственный сертификат для подключения по протоколу HTTPS. 

После создания вашей ASE можно заметить поддомен hello показывает поддомен hello указанного, и новый элемент в hello **параметр** меню с именем **ILB сертификата**. Hello ASE создается самозаверяющий сертификат, который позволяет упростить tootest HTTPS. Hello портал сообщит, что необходимо tooprovide собственный сертификат для использования протокола HTTPS, но это toodrive toohave сертификат, который начинается с дочернего домена. 

![][3]

Если просто пытаетесь вещей и не знаете, как toocreate сертификат можно использовать hello IIS MMC toocreate консольного приложения a self подписи сертификата. После создания можно экспортировать его как PFX-файл и затем передать его в пользовательский Интерфейс сертификатов ILB hello. При доступа сайт защищен с помощью самозаверяющего сертификата, браузер выводит предупреждение, hello сайта, к которому выполняется подключение не является безопасным, из-за toohello невозможности toovalidate hello сертификата. Если вы хотите tooavoid этого предупреждения необходимо должным образом подписанный сертификат, который соответствует дочернего домена и имеет цепочку доверия, распознаются в браузере.

![][6]

Если требуется tootry hello потока с помощью собственных сертификатов и проверки HTTP и HTTPS ASE tooyour доступа:

1. Go tooASE пользовательского интерфейса после создания ASE **ASE -> Параметры -> сертификаты ILB**
2. Задайте сертификат ILB, выбрав PFX-файл сертификата, и введите пароль. Это требует немного при tooprocess и будет выведено сообщение hello, выполняется операция масштабирования.
3. Получить адрес ILB hello для вашего ASE (**ASE "->" Свойства "->" виртуальный IP-адрес**)
4. Создайте веб-приложение в среде ASE после ее создания. 
5. Создайте виртуальную Машину, если у вас его нет в этой виртуальной сети (не в hello же подсети, что hello ASE или прерывание выполнения действия)
6. Задайте DNS для поддомена. Можно использовать подстановочные знаки с дочернего домена в DNS или toodo несколько простых тестов, измените файл hosts hello на вашей виртуальной Машины tooset web app имя tooVIP IP-адрес. Если ваш ASE имя поддомена hello. ilbase.com и внесены hello web app mytestapp так, чтобы он бы адресу mytestapp.ilbase.com затем набор, в файл hosts. (В Windows hello узлов находится в файле C:\Windows\System32\drivers\etc\)
7. Использовать браузер на этой виртуальной Машине и перейдите toohttp://mytestapp.ilbase.com (или что там имя вашего веб-приложения с дочернего домена)
8. Использовать браузер на этой виртуальной Машине и перейдите toohttps://mytestapp.ilbase.com имеется отсутствие hello tooaccept безопасности при использовании самозаверяющего сертификата. 

в свойствах Hello IP-адрес для вашего ILB указано как hello виртуальный IP-адрес

![][4]

## <a name="using-an-ilb-ase"></a>Использование ASE с внутренним балансировщиком нагрузки
#### <a name="network-security-groups"></a>группы сетевой безопасности;
ILB ASE включает сетевая изоляция для приложений приложения hello не доступны или даже известных по hello Интернета. Это прекрасно подходит для размещения сайтов интрасети, например бизнес-приложений. Если вам нужен доступ toorestrict даже дальнейшей можно по-прежнему использовать доступа toocontrol Groups(NSGs) безопасности сети на уровне сети hello. 

При желании toofurther Nsg toouse ограничить доступ, то вы должны убедиться, что не приводит к нарушению связи hello toomake, ASE hello необходим toooperate заказа. Несмотря на то, что hello доступа HTTP/HTTPS — только через hello ILB используется hello ASE приветствия ASE по-прежнему зависит от ресурса за пределами hello виртуальной сети. toosee, какой доступ к сети будет по-прежнему требуются просмотрите hello сведения в документе hello на [tooan управление входящий трафик среды службы приложений] [ ControlInbound] и hello документ на [сети Сведения о конфигурации для среды службы приложений с ExpressRoute][ExpressRoute]. 

tooconfigure, Nsg требуется tooknow hello IP адрес, который указывается используемый Azure toomanage вашей ASE. Этот IP-адрес также является hello исходящий IP-адрес из вашего ASE, если он делает Интернет-запросы. Hello исходящий IP-адрес для вашего ASE останется статический объект для hello жизненного цикла вашего ASE. Если вы удалите и повторно создадите ASE, будет получен новый IP-адрес. Этот IP-адрес перехода слишком toofind**параметры -> свойства** и найти hello **исходящий IP-адрес**. 

![][5]

#### <a name="general-ilb-ase-management"></a>Общее управление ASE с внутренним балансировщиком нагрузки
Управление ILB ASE является главным образом hello такой же, как управление ASE обычным образом. Требуется tooscale копирование вашего toohost рабочих пулов несколько экземпляров ASP и вертикальное масштабирование toohandle увеличить объемы серверы переднего плана вашей трафик HTTP/HTTPS. Общие сведения об управлении hello конфигурацию ASE чтения документа hello на [Настройка среды службы приложений][ASEConfig]. 

элементы управления Hello — управления сертификатами и управления DNS. Требуется tooobtain и hello сертификат используется для протокола HTTPS после создания ILB ASE и замените его до истечения срока его действия. Так как Azure, которому принадлежит базовый домен hello мы предоставляем сертификаты для ASEs с помощью внешнего виртуального IP-адреса. Так как hello дочерний домен, используемый ILB ASE может быть любым, необходимы tooprovide собственный сертификат для использования протокола HTTPS. 

#### <a name="dns-configuration"></a>Настройка DNS
Если с помощью внешнего виртуального IP-адреса hello DNS управляется Azure. Любое приложение, созданных в вашей ASE автоматически добавляется tooAzure DNS, который является общедоступном DNS-Сервере. В ILB ASE имеются toomanage собственный DNS-сервера. Для заданного дочернего домена, например contoso.corp.net необходимые toocreate, этот адрес tooyour точки ILB для записей DNS типа.

    * 
    *.scm ftp publish 


## <a name="getting-started"></a>Приступая к работе
Все статьи и как-для пользователя для среды службы приложений теперь доступны в hello [файл README для среды службы приложения](../app-service/app-service-app-service-environments-readme.md).

tooget к работе с среды службы приложения, в разделе [tooApp введение среды службы][WhatisASE]

Дополнительные сведения о платформе hello службе приложений Azure см. в разделе [службе приложений Azure][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createilbase.png
[2]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createapp.png
[3]: ./media/app-service-environment-with-internal-load-balancer/ilbase-newase.png
[4]: ./media/app-service-environment-with-internal-load-balancer/ilbase-vip.png
[5]: ./media/app-service-environment-with-internal-load-balancer/ilbase-externalvip.png
[6]: ./media/app-service-environment-with-internal-load-balancer/ilbase-ilbcertificate.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[ControlInbound]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ExpressRoute]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[vnetnsgs]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
