---
title: "aaaCreate и использование внутренней подсистемы балансировки нагрузки с среду службы приложений Azure"
description: "Сведения о том, как toocreate и использование изолированной от Интернета среды службы приложений Azure"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 0f4c1fa4-e344-46e7-8d24-a25e247ae138
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: d019ca6f231c3acfdab4cd380db375a076802f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a>Создание и использование внутреннего балансировщика нагрузки со средой службы приложений #

 Среда службы приложений — это развернутая служба приложений Azure в подсети виртуальной сети Azure. Существует два способа toodeploy среду службы приложений (ASE): 

- с виртуальным IP-адресом на основе внешнего IP-адреса, что часто называют внешней средой ASE;
- VIP-адрес, на внутренний IP-адрес часто называют ILB ASE, поскольку внутренняя Подсистема балансировки нагрузки (ILB) hello внутренней конечной точки. 

В этой статье показано, как toocreate ILB ASE. Обзор на hello ASE см. в разделе [введение среды службы tooApp][Intro]. статье toocreate внешних ASE toolearn [Создание внешних ASE][MakeExternalASE].

## <a name="overview"></a>Обзор ##

Вы можете развернуть ASE с конечной точкой, доступной из Интернета, или IP-адресом в вашей виртуальной сети. tooset в hello IP-адресов tooa адрес виртуальной сети, приветствия ASE должны быть развернуты вместе с ILB. При развертывании среды службы приложений с внутренним балансировщиком нагрузки необходимо наличие следующих компонентов:

-   Ваш собственный домен, в котором создаются приложения.
-   Hello сертификат, используемый для HTTPS.
-   Управление службой DNS для домена.

Это дает следующие возможности:

-   Узел приложения интрасети безопасно в облаке hello, доступ к которому осуществляется через сайт сайт или Azure ExpressRoute VPN.
-   Приложения узлов в облаке hello, не перечисленным в общедоступные DNS-серверы.
-   Создание изолированных от Интернета внутренних приложений, с которыми можно безопасно интегрировать свои внешние приложения.

### <a name="disabled-functionality"></a>Отключенные функциональные возможности ###

Существуют некоторые функции, недоступные при использовании ASE с внутренним балансировщиком нагрузки.

-   Использование SSL на основе IP-адреса.
-   Назначьте IP-адреса toospecific приложений.
-   Приобретение и использование сертификата с помощью приложения через портал Azure hello. Вы можете получить сертификаты непосредственно в центре сертификации и использовать их вместе со своими приложениями. Не удается получить их через портал Azure hello.

## <a name="create-an-ilb-ase"></a>Создание среды службы приложений с внутренней подсистемой балансировки нагрузки ##

toocreate ILB ASE:

1. В hello портал Azure, выберите **New** > **Интернет + мобильные устройства** > **среды службы приложений**.

2. Выберите свою подписку.

3. Выберите или создайте группу ресурсов.

4. Выберите или создайте виртуальную сеть.

5. При выборе существующей виртуальной сети необходимо toocreate hello toohold подсети ASE. Убедитесь, что tooset подсети размер достаточно большой tooaccommodate к дальнейшему росту Вашего ASE. Рекомендуемый размер — `/25`. Такая подсеть содержит 128 адресов и может обслуживать среду службы приложений максимального размера. можно выбрать минимальный размер Hello — `/28`. После должен инфраструктуры, этот размер может быть более масштабированный tooa 11 экземпляров.

    * Выходят за рамки максимум 100 экземпляров по умолчанию hello в планах службы приложений.

    * Можно выполнить масштабирование примерно до 100 экземпляров, но путем более быстрого масштабирования внешнего интерфейса.

6. Выберите **Виртуальная сеть/расположение** > **Конфигурация виртуальной сети**. Набор hello **тип виртуального IP-адреса** слишком**внутренний**.

7. Введите имя домена. Привет, другая — для приложений, созданных в этом ASE является этот домен. Существуют некоторые ограничения. Нельзя использовать такие имена:

    * net;   

    * azurewebsites.net;

    * p.azurewebsites.net;

    * &lt;имя_ASE&gt;.p.azurewebsites.net.

   Hello пользовательское доменное имя, используемое для приложений и имя домена hello, используемых вашей ASE не могут перекрываться. Для ILB ASE доменным именем hello _contoso.com_, нельзя использовать пользовательские доменные имена для приложений, как:

    * www.contoso.com;

    * abcd.def.contoso.com;

    * abcd.contoso.com.

   Если вы знаете hello пользовательских доменных имен для приложений, выберите домен для hello ASE ILB, не имеется конфликт с именами соответствующих пользовательского домена. В этом примере можно использовать нечто похожее на *contoso internal.com* для домена вашей ASE hello, так как не противоречит пользовательские доменные имена, заканчивающиеся на *. contoso.com*.

8. Щелкните **ОК**, а затем выберите **Создать**.

    ![создание ASE][1]

На hello **виртуальной сети** колонке имеется **конфигурации виртуальной сети** параметр. Его можно использовать tooselect букве виртуального IP-адреса внешних или внутренних виртуальных IP-адресов. по умолчанию Hello — **внешних**. Если выбрать значение **Внешний**, для среды службы приложений будет использоваться виртуальный IP-адрес, доступный из Интернета. Если выбрать **внутренний** виртуальный IP-адрес, то для ASE будет настроена внутренний балансировщик нагрузки с IP-адресом в виртуальной сети.

После выбора **внутренний**, tooadd возможность hello несколько IP-адресов tooyour ASE удаляется. Вместо этого необходим домен hello tooprovide hello ASE. В ASE с внешнего виртуального IP-адреса hello hello ASE имя используется в домене hello для приложений, созданных в этом ASE.

Если задать **тип виртуального IP-адреса** слишком**внутренний**, название ASE не используется в домене hello для hello ASE. Укажите домен hello явным образом. Если ваш домен называется *contoso.corp.net* и создать приложение, в том, что с именем ASE *timereporting*, hello URL-адрес для этого приложения является timereporting.contoso.corp.net.


## <a name="create-an-app-in-an-ilb-ase"></a>Создание приложения в ASE с внутренним балансировщиком нагрузки ##

Создайте приложение в ASE ILB в hello так же, что создается приложение, в ASE обычно.

1. В hello портал Azure, выберите **New** > **Интернет + мобильные устройства** > **Web** или **Mobile** или  **Приложения API**.

2. Введите имя hello приложение hello.

3. Выберите подписку hello.

4. Выберите или создайте группу ресурсов.

5. Выбор или создание плана службы приложений Toocreate новый план служб приложений, выберите ваш ASE как расположение hello. Выберите место создания плана toobe вашей службы приложений система пул рабочих hello. При создании hello план служб приложений, выберите ваш ASE как расположение hello и hello рабочего пула. При указании имени hello приложение hello hello домена в списке имя вашего приложения заменяется hello домена для вашей ASE.

6. Нажмите кнопку **Создать**. Tooappear приложения hello на панели мониторинга, установите **toodashboard ПИН-код** флажок.

    ![Создание плана служб приложений][2]

    В разделе **имя приложения**, hello доменное имя — домен вашей ASE обновленные tooreflect hello.

## <a name="post-ilb-ase-creation-validation"></a>Проверка после создания ASE с внутренним балансировщиком нагрузки ##

ILB ASE немного отличается от hello не - ILB ASE. Как уже отмечалось необходимо toomanage собственный DNS-сервера. Также имеется tooprovide собственный сертификат для подключения по протоколу HTTPS.

После создания вашей ASE hello доменное имя показывает hello указанного домена. В меню **Параметры** появился новый пункт **Сертификат ILB**. Hello ASE создается сертификатом, который не указывает hello ILB ASE домена. Если hello ASE использовать с этим сертификатом, браузер показывает, что не допускается. Этот сертификат позволяет проще tootest HTTPS, но требуется tooupload собственный сертификат равноценных tooyour ILB ASE доменом. Этот шаг является обязательным независимо от типа сертификата: самозаверяющий или получен из ЦС.

![Имя домена ASE с ILB][3]

Для ASE с внутренним балансировщиком нагрузки требуется допустимый сертификат SSL. Можно получить сертификат от внутреннего центра сертификации, приобрести его у внешнего поставщика и использовать самозаверяющий сертификат. Вне зависимости от источника hello hello SSL-сертификат hello следующие атрибуты сертификатов, необходимые toobe настроен должным образом.

* **Тема**: этот атрибут должен быть задан too*.your корневого домена здесь.
* **Subject Alternative Name** — этот атрибут должен содержать два значения: **.имя_корневого_домена* и **.scm.имя_корневого_домена*. SCM/Kudu сайта, связанные с каждой приложением toohello подключений SSL использует адрес формы hello *your-app-name.scm.your-root-domain-here*.

Преобразования и сохранения hello SSL-сертификата в PFX-файл. Hello PFX-файл должен включать все промежуточные и корневые сертификаты. Защитите его паролем.

Если вы хотите toocreate самозаверяющий сертификат, можно использовать команды PowerShell hello здесь. Быть toouse убедиться, что имя домена ILB ASE вместо *internal.contoso.com*: 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

сертификат Hello, создания этих команд PowerShell помечается в браузерах, так как сертификат hello не была создана, в браузере цепочка доверия центром сертификации. сертификат, который доверяет браузер, tooget получения ключа из коммерческого центра сертификации в цепи доверия в браузере. 

![Задание сертификата ILB][4]

tooupload сертификаты и доступа теста:

1. После создания hello ASE перейдите toohello ASE пользовательского интерфейса. Выберите **ASE** > **Параметры** > **Сертификат ILB**.

2. tooset hello ILB сертификат, выберите PFX-файл сертификата hello и введите пароль hello. Этот шаг займет некоторое время tooprocess. Появится сообщение о том, что выполняется отправка.

3. Получите адрес ILB hello для вашего ASE. Выберите **ASE** > **Свойства** > **Виртуальный IP-адрес**.

4. Создание веб-приложения в вашей ASE после создания hello ASE.

5. Создайте виртуальную машину в этой виртуальной сети (если вы этого еще не сделали).

    > [!NOTE] 
    > Старайтесь не toocreate эту виртуальную Машину в hello одной подсети как hello ASE, так как он будут завершаться ошибкой или вызвать проблемы.
    >
    >

6. Задайте hello DNS для домена ASE. Можно указать в DNS подстановочные знаки с именем домена. toodo несколько простых тестов, измените файл hosts hello на вашей виртуальной Машины tooset hello web app имя toohello виртуального IP-адреса IP-адрес:

    а. Если ваш ASE hello доменных имен _. ilbase.com_ и создать hello веб-приложения с именем _mytestapp_, она описана в _mytestapp.ilbase.com_. Затем установите _mytestapp.ilbase.com_ tooresolve toohello ILB адрес. (В Windows hello файл hosts находится в _C:\Windows\System32\drivers\etc\_.)

    b. tootest web развертывания публикации или доступа toohello дополнительные консоли, создайте запись для _mytestapp.scm.ilbase.com_.

7. Откройте браузер на этой виртуальной машине и перейдите по адресу http://mytestapp.ilbase.com. (Или перейти toowhatever — имя вашего веб-приложения с вашим доменом).

8. Откройте браузер на этой виртуальной машине и перейдите по адресу https://mytestapp.ilbase.com. Если вы используете самозаверяющий сертификат, примите hello отсутствие безопасности.

    Hello IP-адрес для вашего ILB находится в списке **IP-адреса**. Этот список также содержит hello IP-адреса, используемые для hello внешних виртуальных IP-адресов для входящего трафика управления трафиком.

    ![IP-адрес ILB][5]

### <a name="web-jobs-functions-and-hello-ilb-ase"></a>Веб-задания, функции и hello ILB ASE

Функции и веб-задания поддерживаются в ILB ASE, но для hello портала toowork с ними, необходимо иметь сетевой доступ toohello SCM сайт.  Это означает, что браузер должен быть на узле, либо подключены toohello виртуальной сети.  

При использовании функции Azure на ILB ASE может появиться сообщение об ошибке «не может tooretrieve функций в данный момент. Повторите попытку позже". Эта ошибка возникает, поскольку hello функций пользовательского интерфейса использует hello SCM сайта по протоколу HTTPS и hello корневой сертификат не hello браузера цепочки сертификатов. Веб-задания могут вызывать подобную проблему. tooavoid эту проблему, можно выполнить одно из следующих hello:

- Добавьте хранилище доверенных сертификатов tooyour hello сертификата. Это позволит разблокировать Edge и Internet Explorer.
- Используйте Chrome и сначала перейдите toohello SCM сайт, примите hello ненадежный сертификат, а затем перейдите toohello портала.
- Используйте коммерческий сертификат, который находится в цепочке сертификатов браузера.  Это лучший вариант hello.  

## <a name="dns-configuration"></a>Настройка DNS ##

При использовании внешних виртуальных IP-адресов, hello DNS управляется Azure. Любое приложение, созданных в вашей ASE автоматически добавляется tooAzure DNS, передаваемый в общедоступном DNS-Сервере. В ASE с ILB необходимо управлять собственной службой DNS. Для данного домена, такие как _contoso.net_, требуется toocreate DNS типа записей в DNS этот адрес tooyour точки ILB для:

- *.contoso.net;
- *.scm.contoso.net.

Если домен ILB ASE используется для нескольких операций за пределами этого ASE, может потребоваться toomanage DNS на основе имени приложения. Этот метод весьма сложно, поскольку требуется tooadd каждого нового имени приложения в DNS-сервера при ее создании. По этой причине рекомендуется использовать выделенный домен.

## <a name="publish-with-an-ilb-ase"></a>Публикация с использованием ASE с внутренним балансировщиком нагрузки ##

Для каждого создаваемого приложения предоставляются две конечные точки. В ASE с ILB это *&lt;имя_приложения>.&lt;домен_ASE_с_ILB>* и *&lt;имя_приложения>.scm.&lt;домен_ASE_с_ILB>*. 

Имя сайта SCM Hello принимает toohello Kudu консоли называется hello **Дополнительно портала**внутри hello портал Azure. консоль Kudu Hello позволяет просмотреть переменные среды, исследовать hello диска, используйте консоль и многое другое. Дополнительные сведения см. на странице, посвященной [консоли Kudu для службы приложений Azure][Kudu]. 

Мультитенантный hello службы приложений и внешних ASE нет единого входа между hello портал Azure и консоли Kudu hello. Для hello ILB ASE Однако необходимо toouse вашей публикации toosign учетные данные в консоль Kudu hello.

Интернет-CI системах, таких как GitHub и Visual Studio Team Services, не работают с ILB ASE, так как конечную точку публикации hello Интернет доступен. Вместо этого необходим toouse элементов конфигурации системы, где используется запросу модели, например Dropbox.

Публикация конечных точек для приложений в ILB ASE Hello использовать домен hello, hello ILB ASE была создана с. Этот домен отображается в приложение hello профиль публикации и в колонке портала приложение hello (**Обзор** > **Essentials** , а также **свойства**). При наличии ASE ILB с поддомена hello *contoso.net* и приложения с именем *mytest*, используйте *mytest.contoso.net* для FTP-сервера и *mytest.scm.contoso.net*  для развертывания веб-приложения.

## <a name="couple-an-ilb-ase-with-a-waf-device"></a>Взаимозависимость среды ASE с внутренним балансировщиком нагрузки и устройства WAF ##

Служба приложений Azure предоставляет множество мер безопасности, защитить систему hello. Они также помогут toodetermine ли приложение было вредоносной атаки. Лучший способ защиты Hello для веб-приложения — toocouple размещения платформы, такие как службы приложений Azure, с брандмауэр веб-приложения (WAF). Так как hello ILB ASE конечную точку приложения с сетевой изоляцией, подходит для такого использования.

Дополнительные сведения о tooconfigure вашей ASE ILB с устройством WAF статье toolearn [настроить брандмауэр веб-приложения со средой службы приложений][ASEWAF]. В этой статье показано, как toouse Barracuda с вашей ASE виртуального устройства. Другой вариант — toouse шлюза приложения Azure. Шлюз приложения использует hello OWASP основных правил toosecure любых приложений, расположенных позади его. Дополнительные сведения о шлюзе приложений см. в разделе [брандмауэр введение toohello Azure веб-приложения][AppGW].

## <a name="get-started"></a>Начало работы ##

Все статьи и как tooinstructions для ASEs доступны в [файл README для среды службы приложений][ASEReadme].

* tooget к работе с ASEs, в разделе [введение среды службы tooApp][Intro].
* Дополнительные сведения о платформе hello службе приложений Azure см. в разделе [службе приложений Azure](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).
 
<!--Image references-->
[1]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-network.png
[2]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-webapp.png
[3]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate.png
[4]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate2.png
[5]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-ipaddresses.png

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
