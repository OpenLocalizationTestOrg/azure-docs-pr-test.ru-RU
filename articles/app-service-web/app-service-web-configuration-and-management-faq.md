---
title: "aaaConfiguration вопросы и ответы для веб-приложениях Azure | Документы Microsoft"
description: "Получите ответы toofrequently вопросы и ответы о проблемы настройки и управления для веб-приложения hello функции службы приложений Azure."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 5aa405582813291a4aaf144d2f821ecb20a5edcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-and-management-faqs-for-web-apps-in-azure"></a>Часто задаваемые вопросы о настройке и управлении для функции "Веб-приложения" в Azure

Данная статья содержит ответы toofrequently, задаваемые вопросы (FAQ) о проблемах настройки и управления для hello [веб-приложений функции службы приложений Azure](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="are-there-limitations-i-should-be-aware-of-if-i-want-toomove-app-service-resources"></a>Существуют ограничения, о которых мне следует иметь в виду Если я хочу toomove ресурсы службы приложений?

Если планируется toomove службы приложений ресурсы tooa новую группу ресурсов или подписки, существует несколько ограничений toobe учитывать. Дополнительные сведения см. в разделе [Ограничения службы приложений](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations).

## <a name="how-do-i-use-a-custom-domain-name-for-my-web-app"></a>Как использовать имя пользовательского домена для веб-приложения?

Ответы toocommon вопросы об использовании пользовательского имени домена в Azure веб-приложении, см. в наших семь минута видео [добавить собственное доменное имя](https://channel9.msdn.com/blogs/Azure-App-Service-Self-Help/Add-a-Custom-Domain-Name). Hello видео предлагает Пошаговое руководство по tooadd пользовательского имени домена. Описывает способ toouse собственный URL-адрес вместо hello *. azurewebsites.net URL-адрес веб-приложения служб приложений. Вы также увидите Подробное пошаговое руководство по [как toomap пользовательское доменное имя](web-sites-custom-domain-name.md).


## <a name="how-do-i-purchase-a-new-custom-domain-for-my-web-app"></a>Как приобрести новый пользовательский домен для веб-приложения?

toolearn toopurchase и настройки пользовательского домена для веб-приложения служб приложений. в статье [приобрести и настроить пользовательское доменное имя в службе приложений](custom-dns-web-site-buydomains-web-app.md).


## <a name="how-do-i-upload-and-configure-an-existing-ssl-certificate-for-my-web-app"></a>Как загрузить и настроить существующий сертификат SSL для веб-приложения?

toolearn tooupload и настройте существующий пользовательский сертификат SSL, в статье [привязать существующие пользовательские SSL сертификат tooan Azure веб-приложение](app-service-web-tutorial-custom-ssl.md#upload).


## <a name="how-do-i-purchase-and-configure-a-new-ssl-certificate-in-azure-for-my-web-app"></a>Как приобрести и настроить новый сертификат SSL в Azure для веб-приложения?

toolearn toopurchase и Настройка SSL-сертификат для веб-приложения служб приложений. в статье [добавить tooyour сертификат SSL приложение служб приложений](web-sites-purchase-ssl-web-site.md).


## <a name="how-do-i-move-application-insights-resources"></a>Как перемещать ресурсы Application Insights?

В настоящее время Azure Application Insights не поддерживает операции перемещения hello. Если исходная группа ресурсов содержит ресурс Application Insights, этот ресурс переместить нельзя. При включении ресурса Application Insights hello при попытке toomove приложение службы приложений hello всей сбоя операции перемещения. Тем не менее Application Insights и hello не обязательно toobe в плане служб приложений hello же группе ресурсов, что приложение hello для toofunction приложения hello правильно.

Дополнительные сведения см. в разделе [Ограничения службы приложений](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations).

## <a name="where-can-i-find-a-guidance-checklist-and-learn-more-about-resource-move-operations"></a>Где найти контрольный список с инструкциями и дополнительные сведения о перемещении ресурсов?

[Ограничения службы приложений](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations) показано, как ресурсы toomove tooeither подписки или tooa новый ресурс в группы hello же подписки. Можно получить сведения о контрольный список для перемещения ресурсов hello, узнайте, какие службы поддерживают операции перемещения hello и Дополнительные сведения об ограничениях службы приложений и другие разделы.

## <a name="how-do-i-set-hello-server-time-zone-for-my-web-app"></a>Как задать часовой пояс сервера hello для веб-приложение?

tooset hello часовым поясом сервера для веб-приложения:

1. В hello в вашу подписку на службы приложений портале Azure перейдите toohello **параметры приложения** меню.
2. В разделе **Параметры приложения** добавьте параметр:
    * Ключ = WEBSITE_TIME_ZONE
    * Значение = *hello часового пояса требуется*
3. Щелкните **Сохранить**.

## <a name="why-do-my-continuous-webjobs-sometimes-fail"></a>Почему при выполнении непрерывных веб-заданий иногда происходят сбои?

По умолчанию в случае простоя в течение заданного периода времени веб-приложения выгружаются. Это позволяет сэкономить ресурсы системы hello. В планах Basic и Standard, можно включить hello **Always On** Установка веб-приложения hello tookeep загружены все hello. Если веб-приложения выполняется непрерывные веб-задания, следует включить **Always On**, или hello веб-задания может не запуститься надежно. Дополнительные сведения см. в разделе [Создание непрерывно выполняющегося веб-задания](web-sites-create-web-jobs.md#CreateContinuous).

## <a name="how-do-i-get-hello-outbound-ip-address-for-my-web-app"></a>Получение hello исходящий IP-адрес для веб-приложения

Список hello tooget исходящий IP-адреса для веб-приложения:

1. В hello портал Azure, на вашей панели приложения web перейдите toohello **свойства** меню.
2. Введите в поле поиска **исходящий IP-адрес**.

Появится список Hello исходящий IP-адресов.

Если веб-сайт размещается в среде службы приложений для работы с PowerApps toolearn как tooget исходящий IP-адрес, в разделе [исходящих сетевых адресов](app-service-app-service-environment-network-architecture-overview.md#outbound-network-addresses).

## <a name="how-do-i-get-a-reserved-or-dedicated-inbound-ip-address-for-my-web-app"></a>Как получить зарезервированный или выделенный входящий IP-адрес для веб-приложения?

tooset выделенный или зарезервированный IP-адрес для входящих вызовов веб-сайт tooyour приложения Azure, установить и настроить сертификат SSL на основе IP-адресов.

Обратите внимание, что выделенную toouse или зарезервированный IP-адрес для входящих вызовов плана служб приложений должен быть в план обслуживания, Basic или более поздней версии.

## <a name="can-i-export-my-app-service-certificate-toouse-outside-azure-such-as-for-a-website-hosted-elsewhere"></a>Можно ли экспортировать Мой toouse сертификата службы приложений за пределами Azure, такие как для веб-сайта, размещенной в другом месте 

Сертификаты службы приложений считаются ресурсами Azure. Они не являются предполагаемого toouse за пределами служб Azure. Нельзя экспортировать их toouse за пределами Azure. Дополнительные сведения см. в статье [FAQs for App Service certificates and custom domains](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview) (Вопросы и ответы по сертификатам службы приложений и личным доменам).

## <a name="can-i-export-my-app-service-certificate-toouse-with-other-azure-cloud-services"></a>Можно экспортировать Мои toouse сертификата службы приложений с другим облачным службам Azure

Hello портал предоставляет эффективные возможности развертывания сертификат службы приложения по приложениям службы tooApp хранилища ключей Azure. Тем не менее мы получены запросы от клиентов toouse эти сертификаты за пределами hello платформы службы приложений, например, с виртуальными машинами Azure. toolearn как сертификат toocreate PFX локальную копию приложения службы, поэтому hello сертификат можно использовать с другими ресурсами Azure. в разделе [создать локальную копию PFX сертификата службы приложений](https://blogs.msdn.microsoft.com/appserviceteam/2017/02/24/creating-a-local-pfx-copy-of-app-service-certificate/).

Дополнительные сведения см. в статье [FAQs for App Service certificates and custom domains](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview) (Вопросы и ответы по сертификатам службы приложений и личным доменам).


## <a name="why-do-i-see-hello-message-partially-succeeded-when-i-try-tooback-up-my-web-app"></a>Почему я вижу приветственное сообщение «Выполнено частично» при попытке tooback копирование Мое веб-приложение?

Наиболее распространенной причиной сбоя резервного копирования — что некоторые файлы используются приложением hello. Файлы, которые используются блокируются во время выполнения резервного копирования hello. Это препятствуют их резервному копированию и может привести к появлению сообщения "Выполнено частично". Вы можете потенциально предотвратить возникновение такой исключить файлы из процесса резервного копирования hello. Вы можете tooback копирование только необходимое. Дополнительные сведения см. в разделе [резервное копирование только hello важные части узла с помощью веб-приложениях Azure](http://www.zainrizvi.io/2015/06/05/creating-partial-backups-of-your-site-with-azure-web-apps/).

## <a name="how-do-i-remove-a-header-from-hello-http-response"></a>Удаление заголовка из hello HTTP-ответа

tooremove hello заголовки из HTTP-ответа hello обновление файла web.config веб-узла. Дополнительные сведения см. в статье [Remove standard server headers on your Azure websites](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/) (Удаление стандартных заголовков сервера на веб-сайтах Azure).

## <a name="is-app-service-compliant-with-pci-standard-30-and-31"></a>Соответствует ли служба приложений стандарту PCI версий 3.0 и 3.1?

В настоящее время функция веб-приложения hello службе приложений Azure — в соответствии с версией PCI данных безопасности стандартной (DSS) 3.0 уровень 1. Поддержка PCI DSS версии 3.1 запланирована в нашей стратегии. Планирование, уже осуществляется для способ внедрения стандарта последнюю hello продолжится.

Для сертификации PCI DSS версии 3.1 требуется отключить протокол TLS 1.0. В настоящее время для большинства планов службы приложений отключение TLS 1.0 выполнить нельзя. Однако при использовании среды службы приложений или являются пойти toomigrate вашей рабочей нагрузки tooApp среды службы, можно получить больший контроль среды. Например, можно отключить TLS 1.0, обратившись в службу поддержки Azure. В hello рядом будущем мы планируем toomake доступен toousers эти параметры.

Дополнительные сведения см. в статье [Microsoft Azure App Service web app compliance with PCI Standard 3.0 and 3.1](https://support.microsoft.com/help/3124528) (Соответствие веб-приложений службы приложений Microsoft Azure стандарту PCI версии 3.0 и 3.1).

## <a name="how-do-i-use-hello-staging-environment-and-deployment-slots"></a>Как использовать hello в промежуточной среде и слоты развертывания?

При развертывании вашей tooApp app web Service, в планах Standard и Premium службы приложений, можно развернуть tooa отдельный слот развертывания вместо производственный слот по умолчанию toohello. Слоты развертывания являются динамическими веб-приложениями с собственными именами узлов. Приложение веб-содержимого и конфигурации элементов можно переключать между двумя слотами развертывания, включая производственный слот hello.

Дополнительные сведения об использовании слотов развертывания см. в статье [Настройка промежуточных сред в службе приложений Azure](web-sites-staged-publishing.md).

## <a name="how-do-i-access-and-review-webjob-logs"></a>Как получить доступ к веб-заданиям и просмотреть их журналы?

журналы веб-задания tooreview:

1. Войдите в tooyour [Kudu веб-сайт](https://*yourwebsitename*.scm.azurewebsites.net).
2. Выберите hello веб-задания.
3. Выберите hello **переключить вывод** кнопки.
4. toodownload hello выходной файл, выберите hello **загрузки** ссылку.
5. Для отдельного запуска выберите **Отдельный вызов**.
6. Выберите hello **переключить вывод** кнопки.
7. Ссылка для загрузки выберите hello.

## <a name="im-trying-toouse-hybrid-connections-with-sql-server-why-do-i-see-hello-message-systemoverflowexception-arithmetic-operation-resulted-in-an-overflow"></a>Удается toouse гибридные подключения с SQL Server. Почему я вижу приветственное сообщение «System.OverflowException: переполнение в результате выполнения арифметической операции»?

При использовании tooaccess гибридные подключения SQL Server, обновление Microsoft .NET 10 мая 2016 г., может привести к toofail подключений. Может появиться это сообщение:

```
Exception: System.Data.Entity.Core.EntityException: hello underlying provider failed on Open. —> System.OverflowException: Arithmetic operation resulted in an overflow. or (64 bit Web app) System.OverflowException: Array dimensions exceeded supported range, at System.Data.SqlClient.TdsParser.ConsumePreLoginHandshake
```

### <a name="resolution"></a>Способы устранения:

Мы активно работаем над tooupdate toofix диспетчер гибридного подключения этой проблемы. Способы решения см. в записи блога [Hybrid Connections error with SQL Server: System.OverflowException: Arithmetic operation resulted in an overflow](https://blogs.msdn.microsoft.com/waws/2016/05/17/hybrid-connection-error-with-sql-server-system-overflowexception-arithmetic-operation-resulted-in-an-overflow/) (Ошибка гибридных подключений к SQL Server — System.OverflowException: переполнение в результате арифметической операции).

## <a name="how-do-i-add-or-edit-a-url-rewrite-rule"></a>Как добавить или изменить правило переопределения URL-адреса?

tooadd или изменить правило подстановки URL:

1. Настройка диспетчера Internet Information Services (IIS), подключенный tooyour службы приложений веб-приложения. tooconnect службы tooApp диспетчера служб IIS. в статье toolearn [удаленного администрирования веб-сайтов Azure с помощью диспетчера IIS](https://azure.microsoft.com/blog/remote-administration-of-windows-azure-websites-using-iis-manager/).
2. В диспетчере IIS добавьте или измените правило переопределения URL-адреса. toolearn, как правило tooadd или изменить переопределения URL-адресов, в разделе [создать правила подстановки URL-адреса hello перепишите модуль](https://www.iis.net/learn/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module).

## <a name="how-do-i-control-inbound-traffic-tooapp-service"></a>Как контролировать tooApp входящий трафик службы?

На уровне узла hello у вас есть два варианта управления tooApp входящий трафик службы:

* Включите динамическое ограничение IP-адресов. toolearn tooturn на динамические ограничения IP-адресов, в статье [ограничения IP-адресов и доменов для веб-сайтов Azure](https://azure.microsoft.com/blog/ip-and-domain-restrictions-for-windows-azure-web-sites/).
* Включите Module Security. toolearn tooturn на модуль безопасности, в статье [ModSecurity брандмауэр веб-приложения на веб-сайты Azure](https://azure.microsoft.com/blog/modsecurity-for-azure-websites/).

В среде службы приложений можно использовать [брандмауэр Barracuda](https://azure.microsoft.com/blog/configuring-barracuda-web-application-firewall-for-azure-app-service-environment/).

## <a name="how-do-i-block-ports-in-an-app-service-web-app"></a>Как блокировать порты в веб-приложении службы приложений?

В hello службы приложения совместно используется в среде клиента, он не возможные tooblock определенные порты из-за характера hello hello инфраструктуры. TCP-порты 4016, 4018 и 4020 также могут быть открыты для удаленной отладки Visual Studio.

В среде службы приложений можно полностью контролировать входящий и исходящий трафик. Можно использовать группы безопасности сети toorestrict или блок определенные порты. Дополнительные сведения о среде службы приложений см. в записи блога [Introducing App Service Environment](https://azure.microsoft.com/blog/introducing-app-service-environment/) (Введение в среду службы приложения).

## <a name="how-do-i-capture-an-f12-trace"></a>Как отслеживать трассировку F12?

Трассировку F12 можно отслеживать двумя способами.

* HTTP-трассировка F12
* Вывод F12 на консоль

### <a name="f12-http-trace"></a>HTTP-трассировка F12

1. В Internet Explorer перейдите на веб-сайт tooyour. Важные toosign находится в перед hello дальнейшие действия. В противном случае hello F12 трассировки записываются конфиденциальные данные.
2. Нажмите клавишу F12.
3. Убедитесь, что hello **сети** вкладка и выберите hello зеленый **воспроизведение** кнопки.
4. Здравствуйте, действия, которые воспроизводят проблему hello.
5. Выберите hello красным **остановить** кнопки.
6. Выберите hello **Сохранить** кнопку (значок диска) и сохраните файл HAR hello (в Internet Explorer и границей) *или* щелкните правой кнопкой мыши hello HAR-файл, а затем выберите **Сохранить как HAR с содержимым** () в браузере Chrome).

### <a name="f12-console-output"></a>Вывод F12 на консоль

1. Выберите hello **консоли** вкладки.
2. Для каждой вкладки, содержащей элементы больше нуля, перейдите на вкладку hello (**ошибка**, **предупреждение**, или **сведения**). Если не выбрана вкладка «hello», значок hello вкладки — черный или серый при перемещении курсора hello вне его.
3. Щелкните правой кнопкой мыши в сообщение hello hello области, а затем выберите **Копировать все**.
4. Вставить hello скопировать текст в файле, а затем сохраните файл hello.

tooview HAR-файл, можно использовать hello [HAR просмотра](http://www.softwareishard.com/har/viewer/).

## <a name="why-do-i-get-an-error-when-i-try-tooconnect-an-app-service-web-app-tooa-virtual-network-that-is-connected-tooexpressroute"></a>Почему получить ошибку при попытке tooconnect службы приложения web app tooa виртуальную сеть, подключенных tooExpressRoute?

При попытке tooconnect Azure web app tooa виртуальной сетью подключенный tooAzure ExpressRoute, происходит сбой. Hello появится следующее сообщение: «Шлюз не VPN-шлюза.»

В настоящее время не может иметь точка сеть VPN подключения tooa виртуальной сети, подключенной tooExpressRoute. Точка сеть VPN и ExpressRoute не может использоваться совместно для hello же виртуальной сети. Дополнительные сведения см. в разделе о [квотах и ограничениях для ExpressRoute и VPN-подключений типа "сеть — сеть"](../expressroute/expressroute-howto-coexist-classic.md#limits-and-limitations).

## <a name="how-do-i-connect-an-app-service-web-app-tooa-virtual-network-that-has-a-static-routing-policy-based-gateway"></a>Как подключить приложение службы web app tooa виртуальную сеть, имеющую шлюз статической маршрутизации (на основе политики)

В настоящее время подключение приложения службы web app tooa виртуальную сеть, имеющую шлюз статической маршрутизации (на основе политики) не поддерживается. Целевой виртуальной сети уже существует, должно иметь точка сеть VPN включено, шлюз динамической маршрутизации перед tooan подключенных приложений. Если шлюз toostatic маршрутизации, невозможно включить VPN-Подключение точка сеть. 

Дополнительные сведения см. в разделе [Приступая к работе](web-sites-integrate-with-vnet.md#getting-started).

## <a name="in-my-app-service-environment-why-can-i-create-only-one-app-service-plan-even-though-i-have-two-workers-available"></a>Почему в среде службы приложений можно создать только один план службы приложений, даже если доступны две рабочие роли?

tooprovide отказоустойчивость, среды службы приложений требует, что каждый пул рабочих требуется по крайней мере один дополнительных вычислительных ресурсов. Hello дополнительных вычислительных ресурсов нельзя задать рабочую нагрузку.

Дополнительные сведения см. в разделе [как toocreate среды службы приложений](app-service-web-how-to-create-an-app-service-environment.md).

## <a name="why-do-i-see-timeouts-when-i-try-toocreate-an-app-service-environment"></a>Почему я вижу тайм-ауты при попытке toocreate среды службы приложений?

Иногда при создании среды службы приложений происходят сбои. В этом случае появится следующая ошибка в журналах действий приветствия hello:
```
ResourceID: /subscriptions/{SubscriptionID}/resourceGroups/Default-Networking/providers/Microsoft.Web/hostingEnvironments/{ASEname}
Error:{"error":{"code":"ResourceDeploymentFailure","message":"hello resource provision operation did not complete within hello allowed timeout period.”}}
```

tooresolve это, убедитесь, что ни один из следующих условий hello выполняются:
* подсети Hello слишком мал.
* Hello подсети не является пустым.
* ExpressRoute предотвращает hello требования сетевого подключения из среды службы приложений.
* Неправильный группы безопасности сети предотвращает hello требования сетевого подключения из среды службы приложений.
* Включено принудительное туннелирование.

Дополнительные сведения см. в записи блога [Most frequent issues when deploying (creating) a new Azure App Service Environment](https://blogs.msdn.microsoft.com/waws/2016/05/13/most-frequent-issues-when-deploying-creating-a-new-azure-app-service-environment-ase/) (Частые проблемы при развертывании (создании) новой среды службы приложений Azure).

## <a name="why-cant-i-delete-my-app-service-plan"></a>Почему не удается удалить план службы приложений?

Невозможно удалить план служб приложений, если все приложения службы приложений связаны с hello план служб приложений. Прежде чем удалить план служб приложений, удалите все связанные приложения служб приложений из hello план служб приложений.

## <a name="how-do-i-schedule-a-webjob"></a>Как запланировать веб-задание?

Создать запланированное веб-задание можно при помощи выражений Cron:

1. Создайте файл settings.job.
2. Включите в этом файле JSON свойство расписания при помощи выражения Cron: 
    ```
    { "schedule": "{second}
    {minute} {hour} {day}
    {month} {day of hello week}" }
    ```

Дополнительные сведения о запланированных веб-заданиях см. в разделе [Создание запланированного веб-задания с использованием выражения CRON](web-sites-create-web-jobs.md#CreateScheduledCRON).

## <a name="how-do-i-perform-penetration-testing-for-my-app-service-app"></a>Как выполнить тест безопасности для приложения службы приложений?

Тестирование уязвимости tooperform, [отправить запрос на](https://security-forms.azure.com/penetration-testing/terms).

## <a name="how-do-i-configure-a-custom-domain-name-for-an-app-service-web-app-that-uses-traffic-manager"></a>Как настроить имя пользовательского домена для веб-приложения службы приложений, использующего диспетчер трафика?

toouse пользовательского имени домена в приложении службы приложений, использует диспетчер трафика Azure для балансировки нагрузки, в статье toolearn [настроить пользовательское доменное имя для веб-приложение Azure с помощью диспетчера трафика](web-sites-traffic-manager-custom-domain-name.md).

## <a name="my-app-service-certificate-is-flagged-for-fraud-how-do-i-resolve-this"></a>Мой сертификат службы приложений помечен как мошеннический. Как решить эту проблему?

Во время проверки домена hello приобретения сертификата службы приложений может появиться следующие сообщения hello:

"Сертификат помечен как возможно мошеннический. Hello запроса находится на рассмотрении. Если сертификат hello не становится может использоваться в течение 24 часов, обратитесь в службу поддержки Azure.»

Как сообщение hello указывает, процесс проверки мошенничество может занимать toocomplete too24 часов. В течение этого времени вы перейдете toosee приветственное сообщение.

Если сертификат службы приложений по-прежнему tooshow это сообщение через 24 часа, запустите следующий сценарий PowerShell hello. Hello скрипт контакты hello [поставщик certificate](https://www.godaddy.com/) непосредственно tooresolve hello проблему.

```
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId <subId>
$actionProperties = @{
    "Name"= "<Customer Email Address>"
    };
Invoke-AzureRmResourceAction -ResourceGroupName "<App Service Certificate Resource Group Name>" -ResourceType Microsoft.CertificateRegistration/certificateOrders -ResourceName "<App Service Certificate Resource Name>" -Action resendRequestEmails -Parameters $actionProperties -ApiVersion 2015-08-01 -Force   
```

## <a name="how-do-authentication-and-authorization-work-in-app-service"></a>Как в службе приложений выполняется проверка подлинности и авторизация?

Подробную документацию по проверке подлинности и авторизации в службе приложений см. в статье [Безопасность службы приложений Azure](../app-service/app-service-security-readme.md). Hello документация также содержит сведения о настройке службы приложений toouse различные определения поставщика входа в систему:
* [Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)
* [Facebook](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md)
* [Google](../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md)
* [Учетная запись Майкрософт](../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md)
* [Twitter](../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md)

## <a name="how-do-i-redirect-hello-default-azurewebsitesnet-domain-toomy-azure-web-apps-custom-domain"></a>Как перенаправление по умолчанию hello *. пользовательский домен toomy Azure web azurewebsites.net домена приложения?

При создании нового веб-сайта с помощью веб-приложения в Azure, значение по умолчанию *sitename*. azurewebsites.net домена назначен сайту tooyour. При добавлении пользовательских tooyour имя узла и не хотите может tooaccess toobe пользователей по умолчанию *. домене azurewebsites.net можно перенаправить URL-адрес по умолчанию hello. toolearn tooredirect все трафик с веб-сайта по умолчанию домена tooyour пользовательского домена разделе [hello по умолчанию домена tooyour пользовательский домен перенаправления в веб-приложениях Azure](http://www.zainrizvi.io/2016/04/07/block-default-azure-websites-domain/).

## <a name="how-do-i-determine-which-version-of-net-version-is-installed-in-app-service"></a>Как определить, какая версия платформы .NET установлена в службе приложений?

Hello быстрым способом toofind hello версию Microsoft .NET, установленного в службе приложений можно с помощью консоли Kudu hello. Hello портале или с помощью URL-адрес hello приложение службы приложений можно получить доступ к консоли Kudu hello. Подробные инструкции см. в разделе [определите версию .NET hello установлен в службе приложений](https://blogs.msdn.microsoft.com/waws/2016/11/02/how-to-determine-the-installed-net-version-in-azure-app-services/).

## <a name="why-isnt-autoscale-working-as-expected"></a>Почему автомасштабирование не работает правильно?

Если Автомасштабирование Azure еще не масштабируется по или масштабировать экземпляр приложения hello web, как указано, возможно, вы используете в сценарии, в котором мы намеренно выберите не tooscale tooavoid бесконечный цикл из-за слишком «неустойчивый». Обычно это происходит, когда не между пороговыми значениями hello масштабирования и масштабирования в соответствующие поля. tooavoid «неустойчивый» и tooread других автомасштабирования советы и рекомендации, в статье toolearn [автомасштабирования рекомендации](../monitoring-and-diagnostics/insights-autoscale-best-practices.md#autoscale-best-practices).

## <a name="why-does-autoscale-sometimes-scale-only-partially"></a>Почему автомасштабирование иногда выполняется только частично?

Автомасштабирование активируется, если метрики превышают предварительно настроенные границы. В некоторых случаях могут появиться емкости hello лишь частично заполняется сравниваемых toowhat отличаются от ожидаемых. Это может произойти, если hello количество экземпляров, которые нужно недоступны. В этом случае автомасштабирования частично отображается hello количество доступных экземпляров. Автомасштабирование запустит логику tooget hello измените баланс дополнительной емкости. Он выделяет память для оставшихся экземпляров hello. Это может занять несколько минут.

Если вы не видите hello ожидаемого числа экземпляров через несколько минут, возможно, из-за частичного пополнения hello метрики hello достаточно toobring в пределах границ hello. Или автомасштабирования может уменьшен так как он достиг hello нижнюю границу метрики.

Если эти условия не выполнены и повторения hello, отправьте запрос на техническую поддержку.

## <a name="how-do-i-turn-on-http-compression-for-my-content"></a>Как включить сжатие HTTP для содержимого?

tooturn сжатия в обоих статические и динамические типы содержимого, добавьте следующие файл web.config уровня приложения toohello кода hello:

```
<system.webServer>
<urlCompression doStaticCompression="true" doDynamicCompression="true" />
< /system.webServer>
```

Также можно указать определенные динамической hello и типы, которые должны toocompress статических MIME. Дополнительные сведения см. в разделе наш вопрос на форуме tooa ответа в [httpCompression параметры на веб-сайте простой Azure](https://social.msdn.microsoft.com/Forums/azure/890b6d25-f7dd-4272-8970-da7798bcf25d/httpcompression-settings-on-a-simple-azure-website?forum=windowsazurewebsitespreview).

## <a name="how-do-i-migrate-from-an-on-premises-environment-tooapp-service"></a>Как перенести из локальной среды tooApp службы?

сайты toomigrate из Windows и Linux tooApp серверы web Service, могут использовать помощник по миграции Azure приложения службы. Средство миграции Hello создает веб-приложений и баз данных в Azure, при необходимости и затем публикует содержимое hello. Дополнительные сведения см. на странице [Azure App Service Migration Assistant](https://www.movemetothecloud.net/) (Средство Migration Assistant службы приложений Azure).
