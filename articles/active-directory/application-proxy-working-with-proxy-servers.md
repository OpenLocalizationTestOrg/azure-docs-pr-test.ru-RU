---
title: "aaaWork с существующими локальными прокси-серверами и Azure AD | Документы Microsoft"
description: "Рассматриваются как toowork с существующими локальными прокси-серверов."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7f8cec4f676f99bead5211bcbcf23056bd7f211f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>Работа с имеющимися локальными прокси-серверами

В этой статье объясняется, как tooconfigure toowork соединителей прокси приложения Azure Active Directory (Azure AD) с исходящий прокси-серверами. Она предназначена для клиентов, использующих сетевые среды с имеющимися прокси.

Рассмотрим основные сценарии развертывания:
* Настройте соединители toobypass вашей локальной исходящих прокси-серверов.
* Настройте соединители toouse исходящего прокси-сервера tooaccess прокси приложения Azure AD.

Дополнительные сведения о соединителях см. в статье [Сведения о соединителях прокси приложения Azure AD](application-proxy-understand-connectors.md).

## <a name="configure-hello-outbound-proxy"></a>Настройка прокси-сервера на исходящие hello

Если имеется исходящий прокси-сервер в вашей среде, необходимо используйте учетную запись с соответствующими разрешениями tooconfigure hello исходящего прокси-сервера. Поскольку hello установщик запускается в контексте hello hello пользователя, который выполняет установку hello, проверьте конфигурацию hello с помощью Microsoft Edge или другой браузер Интернета.

параметры прокси-сервера tooconfigure hello в Microsoft Edge.

1. Go слишком**параметры** > **Дополнительные параметры представления** > **откройте параметры прокси-сервера** > **ручной настройки прокси-сервера** .
2. Задать **использовать прокси-сервер** слишком**на**выберите hello **не используйте hello прокси-сервер для локальных адресов (интрасеть)** флажок, а затем tooreflect изменение hello адрес и порт ваш локальный прокси-сервер.
3. Заполните параметры hello необходимые прокси-сервера.

   ![Диалоговое окно для настройки прокси-сервера](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a>Обход исходящих прокси-серверов

Соединители имеют базовые компоненты ОС, выполняющие исходящие запросы. Эти компоненты автоматически предпринимает toolocate прокси-сервера в сети hello. Они используют автоматическое обнаружение прокси-сервера веб-(WPAD), если он включен в среде hello.

компоненты операционной системы Hello попытку toolocate прокси-сервер, выполняющий поиск в DNS для wpad.domainsuffix. Если это разрешается в DNS, HTTP-запроса затем выполняется toohello IP-адрес для wpad.dat. Этот запрос становится hello сценарий настройки прокси-сервера в вашей среде. Соединитель Hello использует этот сценарий tooselect исходящий прокси-сервера. Тем не менее, соединитель трафик может по-прежнему не проходит через, из-за дополнительных параметров настройки для hello прокси-сервера.

Можно настроить toobypass соединитель hello вашей tooensure прокси-сервера в локальной среде, она использует прямое подключение toohello Azure службы. Это рекомендуемый подход (если сетевой политики разрешает для него), так как он означает, что один меньше toomaintain конфигурации.

Использование toodisable исходящего прокси-сервера для соединителя hello, измените файл C:\Program Files\Microsoft AAD приложения прокси Connector\ApplicationProxyConnectorService.exe.config hello и добавьте hello *system.net* раздела показано в этом примере кода :

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>
    <defaultProxy enabled="false"></defaultProxy>
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```
tooensure, средство обновления соединителя службы hello в обход прокси-сервера hello, внести аналогичные изменения toohello ApplicationProxyConnectorUpdaterService.exe.config файл, расположенный в средство обновления соединителя прокси приложения в AAD Files\Microsoft C:\Program.

Следует убедиться, что toomake копии hello исходные файлы, необходимые файлы .config toorevert toohello по умолчанию.

## <a name="use-hello-outbound-proxy-server"></a>Использовать hello исходящий прокси-сервер

Некоторые среды требуют все toogo исходящего трафика через исходящий прокси-сервер без исключений. В результате обход прокси-сервера hello являются обязательными.

Hello соединителя трафика toogo через прокси-сервер hello Исходящие, можно настроить, как показано в hello, следующая схема:

 ![Настройка соединителя toogo трафика через tooAzure исходящего прокси-сервера AD прокси приложения](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

В результате возникают только исходящий трафик, выделяется tooconfigure не требуется входящий доступ через межсетевой экран.

### <a name="step-1-configure-hello-connector-and-related-services-toogo-through-hello-outbound-proxy"></a>Шаг 1: Настройте соединитель hello и связанных служб toogo через hello исходящего прокси-сервера

Как описано ранее, если включен в среде hello и надлежащим образом настраивается WPAD, соединитель hello автоматически обнаруживать hello toouse исходящего прокси-сервера сервера и попытка ее. Тем не менее можно настроить явно toogo соединитель hello через исходящего прокси-сервера.

toodo таким образом, измените файл C:\Program Files\Microsoft AAD приложения прокси Connector\ApplicationProxyConnectorService.exe.config hello и добавьте hello *system.net* раздела показано в этом примере кода. Изменение *proxyserver:8080* tooreflect ваш локальный прокси-сервер имя сервера или IP-адрес и hello порта, что он прослушивает.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>  
    <defaultProxy>   
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True"/>   
    </defaultProxy>  
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```

Настройте прокси-сервер hello средство обновления соединителя службы toouse hello, делая аналогичные изменения toohello, находящемся в C:\Program Files\Microsoft AAD приложения прокси-сервера соединителя Updater\ApplicationProxyConnectorUpdaterService.exe.config.

### <a name="step-2-configure-hello-proxy-tooallow-traffic-from-hello-connector-and-related-services-tooflow-through"></a>Шаг 2: Настройка hello прокси tooallow трафик от соединителя hello и связанных служб tooflow через

Существует четыре tooconsider аспекты в hello исходящего прокси-сервера:
* правила для исходящих подключений прокси-сервера;
* проверка подлинности прокси-сервера;
* порты прокси-сервера;
* проверка SSL.

#### <a name="proxy-outbound-rules"></a>правила для исходящих подключений прокси-сервера;
Разрешить доступ toohello следующие конечные точки для доступа к службе соединителя:

* *.msappproxy.net;
* *.servicebus.windows.net

Для первоначальной регистрации разрешите доступ toohello следующие конечные точки:

* login.windows.net
* login.microsoftonline.com

Если вы не сможете разрешить подключения по полному доменному ИМЕНИ и необходимые диапазоны IP-адресов toospecify используйте эти параметры:

* Разрешите исходящий доступ соединитель hello tooall назначения.
* Разрешить исходящий доступ соединитель hello слишком[диапазоны IP-адресов центра обработки данных Azure](https://www.microsoft.com/en-gb/download/details.aspx?id=41653). проблема Hello использования hello список диапазонов IP-адресов центра обработки данных Azure — еженедельно обновляется. Необходимо tooput процесса в месте tooensure соответствующим образом обновлены правила доступа.

#### <a name="proxy-authentication"></a>проверка подлинности прокси-сервера;

Проверка подлинности прокси в настоящее время не поддерживается. Мы рекомендуем — tooallow hello соединителя анонимный доступ toohello пунктам назначения в Интернете.

#### <a name="proxy-ports"></a>порты прокси-сервера;

Соединитель Hello делает исходящих соединений на основе протокола SSL с помощью метода CONNECT hello. Этот метод фактически устанавливает туннель через hello исходящего прокси-сервера. Настройте hello прокси сервера tooallow туннелирование tooports 443 и 80.

>[!NOTE]
>При запуске служебной шины по протоколу HTTPS используется порт 443. Тем не менее по умолчанию Service Bus пытается прямые подключения TCP и возвращается tooHTTPS только в том случае, если прямое подключение завершается ошибкой.

tooensure, Здравствуйте Service Bus, он также отправляется hello исходящий прокси-сервер, убедитесь, что для этого соединителя hello не может напрямую подключиться toohello службы Azure для порты 9350, 9352 и 5671.

#### <a name="ssl-inspection"></a>проверка SSL.
Не используйте проверку SSL для трафика соединителя hello, так как это вызывает проблемы, для трафика соединителя hello.

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a>Устранение неполадок в работе соединителя через прокси-сервера и с подключением к службе
Теперь вы увидите все трафик через прокси-сервер hello. Если возникают проблемы, поможет hello следующие сведения об устранении неполадок.

Здравствуйте, лучшим способом tooidentify и устранения неполадок подключения соединитель проблемы является tootake сети записываться hello соединитель службы во время запуска службы соединителя hello. Это может оказаться непростой задачей, так что давайте рассмотрим советы по сбору и фильтрации данных трассировки сети.

Можно использовать средство по вашему выбору наблюдения за hello. В целях hello данной статьи мы использовали Microsoft Network Monitor 3.4. Эту версию можно загрузить [здесь](https://www.microsoft.com/download/details.aspx?id=4865).

Примеры Hello и фильтры, используемые в следующих разделах hello конкретных tooNetwork монитора, но принципы hello могут быть применен tooany средство анализа.

### <a name="take-a-capture-by-using-network-monitor"></a>Выполнение записи с помощью сетевого монитора

toostart записи:

1. Откройте сетевой монитор и щелкните **New Capture** (Новая запись).
2. Нажмите кнопку hello **запустить** кнопки.

   ![Окно сетевого монитора](./media/application-proxy-working-with-proxy-servers/network-capture.png)

После завершения записи нажмите кнопку hello **остановить** кнопку tooend его.

### <a name="take-a-capture-of-connector-traffic"></a>Сбор трафика соединителя

Изначальная Диагностика выполните hello следующие шаги:

1. Из services.msc остановите службу hello соединитель прокси приложения Azure AD.
2. Начать запись сети hello.
3. Запустите службу hello соединитель прокси приложения Azure AD.
4. Остановка записи hello сетевого трафика.

   ![Служба соединителя прокси приложения Azure AD в services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-hello-requests-from-hello-connector-toohello-proxy-server"></a>Рассмотрим hello запросы от hello соединитель toohello прокси-сервера

Теперь, когда у вас есть записи сетевого трафика, вы будете готовы toofilter его. Hello ключа toolooking в трассировке hello понимания того, как записать toofilter hello.

Один фильтр составляет (где 8080 — порт службы hello прокси-сервера):

**(http.Request or http.Response) and tcp.port==8080**

Если указать этот фильтр в hello **фильтр отображения** и выберите **применить**, фильтрует hello захвачен трафика на основе фильтра hello.

Hello выше отображаются лишь hello запросов и ответов HTTP из hello порт прокси-сервера. Для запуска соединителя, где hello соединителя — toouse настроенный прокси-сервер hello фильтра будут показаны примерно следующим образом:

 ![Пример списка отфильтрованных запросов и ответов HTTP](./media/application-proxy-working-with-proxy-servers/http-requests.png)

Теперь специально Запрашиваемая hello ПОДКЛЮЧЕНИЕ запросов, показывающие связь с прокси-сервера hello. В случае успеха вы получите ответ OK с HTTP-кодом 200.

Если другие коды ответа, например 407 или 502, hello прокси требование проверки подлинности или не позволяет hello трафика по другой причине. На этом этапе следует обратиться в службу поддержки прокси-сервера.

### <a name="identify-failed-tcp-connection-attempts"></a>Выявление неудачных попыток подключения TCP

Hello другим распространенным сценарием, могут быть интересны является hello соединителя пытается tooconnect напрямую, когда происходит сбой.

— Другой фильтр сетевой монитор, который помогает tooeasily идентификации проблемы:

**property.TCPSynRetransmit**

Пакет SYN — первый пакет приветствия отправки tooestablish TCP-подключение. Если этот пакет не возвращает ответ, hello SYN повторяется. Можно использовать любой повторно SYN hello предшествующий toosee фильтра. Затем можно проверить, соответствуют ли эти SYN tooany трафика соединителя.

Hello ниже приведен пример попытки неудачного подключения порт шины tooService 9352.

 ![Пример ответа для ошибки подключения](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

При появлении примерно hello предшествующий ответа соединителя hello пытается toocommunicate непосредственно с hello службы Azure Service Bus. Если предполагается, что прямые подключения toomake toohello Azure для hello соединителя служб, этот ответ является четкое представление о том, что имеются проблемы с сетью или брандмауэром.

>[!NOTE]
>Если toouse настроенный прокси-сервер, этот ответ может означать, что Service Bus пытается прямое подключение TCP перед переключением tooattempting соединение по протоколу HTTPS.
>

Анализ трассировки сети — не идеальное решение. Но это может быть полезным средством tooget краткие сведения о том, что сети.

В случае продолжения toostruggle с проблемами подключения соединитель создайте билет с нашей группой поддержки. Команда Hello может помочь устранить неполадки.

Сведения об устранении ошибок соединителя прокси приложения см. в [этой статье](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).

## <a name="next-steps"></a>Дальнейшие действия

[Сведения о соединителях прокси приложения Azure AD](application-proxy-understand-connectors.md)<br>
[Как toosilently установку hello соединитель прокси приложения Azure AD](active-directory-application-proxy-silent-installation.md)
