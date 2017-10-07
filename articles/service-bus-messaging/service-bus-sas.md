---
title: "Проверка подлинности Service Bus aaaAzure с подписями коллективного доступа | Документы Microsoft"
description: "Обзор аутентификации служебной шины с помощью подписанных URL-адресов, а также сведения об аутентификации SAS с помощью служебной шины Azure."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 773bb11720384d7245820b56dc25b8e064ffa746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-authentication-with-shared-access-signatures"></a>Аутентификация служебной шины с помощью подписанных URL-адресов

*Подписи коллективного доступа* (SAS), hello безопасности основной механизм для обмена сообщениями Service Bus. В этой статье рассматриваются SAS, как они работают и как toouse их в виде зависящий от платформы.

Проверка подлинности SAS позволяет tooService tooauthenticate приложений шины с помощью клавиши доступа, настроенной на приветствия имен или hello сущности (очереди или раздела) обмена сообщениями с связаны определенные права. Затем можно использовать этот ключа toogenerate маркер SAS, которая tooauthenticate tooService шины в свою очередь может использоваться клиентами.

Поддержка проверки подлинности SAS включается в hello Azure SDK версии 2.0 и более поздней версии.

## <a name="overview-of-sas"></a>Общие сведения о SAS

Подписи общего доступа представляют собой механизм проверки подлинности на основе безопасных хэшей SHA-256 или URI. Это очень мощный механизм, который используется всеми службами служебной шины. На практике SAS состоит из двух компонентов: *политики общего доступа* и *подписанного URL-адреса* (который часто называется *маркером*).

Проверка подлинности SAS в Service Bus включается конфигурация hello криптографического ключа со связанными правами для ресурса Service Bus. Клиенты утверждения доступа tooService шины ресурсов путем предъявления маркера SAS. Этот маркер состоит из hello ресурса (URI) для вызываемой и срока действия подписана hello настроить ключ.

Правила авторизации подписанного URL-адреса можно настроить в [ретрансляторах](service-bus-fundamentals-hybrid-solutions.md#relays), [очередях](service-bus-fundamentals-hybrid-solutions.md#queues) и [разделах](service-bus-fundamentals-hybrid-solutions.md#topics) служебной шины.

Проверка подлинности SAS использует hello следующие элементы:

* [Правило авторизации общего доступа](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule): 256-битный основной криптографический ключ в кодировке Base64, необязательный дополнительный ключ, имя ключа и соответствующие права (набор прав на *прослушивание*, *отправку* и *управление*).
* [Подписанный URL-](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) маркера: создан с помощью hello HMAC-SHA256 строки ресурса, состоящий из URI ресурса hello, к которому осуществляется hello и срока действия с криптографическим ключом hello. подпись Hello и другие элементы, описанные в следующих разделах hello форматируются в строку tooform hello маркер SAS.

## <a name="shared-access-policy"></a>Политика общего доступа

Главное toounderstand о SAS — что он начинается с политикой. Для каждой политики необходимо выбрать три элемента информации: **имя**, **область** и **разрешения**. Hello **имя** , является; уникальное имя в пределах данной области. Hello области достаточно просто: его hello URI ресурса hello в вопросе. Для пространства имен Service Bus, hello относится hello полное доменное имя (FQDN), такие как `https://<yournamespace>.servicebus.windows.net/`.

во многом очевидны Hello доступные разрешения для политики:

* Отправка
* Прослушивание
* Управление

После создания политики hello, ей назначается *первичного ключа* и *вторичный ключ*. Это криптографически строгие ключи. Не потеряны и их утечка — они всегда будут доступны в hello [портал Azure][Azure portal]. Можно использовать любой из созданных hello ключи и повторно создать их в любое время. Тем не менее если повторно создать или изменить первичный ключ hello в политике hello, станут недействительными все подписанные URL-адреса созданные из нее.

При создании пространства имен Service Bus политики создается автоматически для всего пространства имен hello вызывается **RootManageSharedAccessKey**, и эта политика имеет все разрешения. Так как вы не входите в систему как **привилегированный пользователь**, не используйте эту политику без действительно веской причины. Можно создать дополнительные политики в hello **Настройка** вкладки для пространства имен hello hello портала. Это важные toonote, уровень одно дерево в Service Bus (пространство имен, очереди, т. д.) может иметь только копирование tooit too12 присоединенного политики.

## <a name="configuration-for-shared-access-signature-authentication"></a>Настройка проверки подлинности подписанного URL-адреса
Можно настроить hello [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) правило на пространства имен служебной шины, очереди или разделы. Настройка [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) на Service Bus подписка в настоящее время не поддерживается, но можно использовать правила, настроенные на пространство имен или разделе toosubscriptions toosecure доступа. Рабочий образец иллюстрирует эту процедуру см. в разделе hello [проверки подлинности с помощью общего подписи доступа (SAS) с подписками Service Bus](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c) образца.

В пространстве имен, очереди или разделе служебной шины можно настроить до 12 таких правил. Правила, которые можно настроить на пространство имен служебной шины применяются tooall сущностей в этом пространстве имен.

![SAS](./media/service-bus-sas/service-bus-namespace.png)

На этом рисунке hello *manageRuleNS*, *sendRuleNS*, и *listenRuleNS* применяются правила авторизации, tooboth очередь Q1 и к разделу T1, пока *listenRuleQ*  и *sendRuleQ* применяются только tooqueue Q1 и *sendRuleT* применяется только tootopic T1.

Здравствуйте, важнейшие параметры [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) , как показано ниже:

| Параметр | Описание |
| --- | --- |
| *KeyName* |Строка, описывающая hello правила авторизации. |
| *PrimaryKey* |Base64-кодированном 256-разрядный первичный ключ для подписания и проверки маркера SAS hello. |
| *SecondaryKey* |Base64-кодированном 256-разрядный вторичный ключ для подписания и проверки маркера SAS hello. |
| *AccessRights* |Список прав доступа, предоставляемых правилом авторизации hello. Эти права могут быть любым набором прав на прослушивание, отправку и управление. |

При подготовке пространства имен Service Bus [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), с [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) значение слишком**RootManageSharedAccessKey**, создается по умолчанию.

## <a name="generate-a-shared-access-signature-token"></a>Создание подписанного URL-адреса (маркера)

сама политика Hello не hello маркер доступа для Service Bus. — Это объект hello, из которого hello создается маркер доступа - с помощью либо hello первичный или вторичный ключ. Любой клиент, имеющий доступ toohello подписи ключи, указанные в правиле авторизации общего доступа hello можно создать токен SAS hello. токен Hello создается тщательно разработать строку в кодировке hello:

```
SharedAccessSignature sig=<signature-string>&se=<expiry>&skn=<keyName>&sr=<URL-encoded-resourceURI>
```

Где `signature-string` область hello маркера hello хэш hello SHA-256 (**область** как описано в предыдущем разделе hello) с добавляется код CRLF и время истечения срока действия (в секундах с начала эпохи hello: `00:00:00 UTC` 1 января 1970 года). 

> [!NOTE]
> tooavoid короткий срок действия токена, рекомендуется кодировать hello значение времени истечения срока действия, как по крайней мере 32-разрядное целое число без знака или предпочтительно целое long (64-разрядная версия).  
> 
> 

хэш Hello выглядит примерно toohello следующий псевдокод и возвращает 32 байта.

```
SHA-256('https://<yournamespace>.servicebus.windows.net/'+'\n'+ 1438205742)
```

Hello нехэшированные значения находятся в hello **SharedAccessSignature** строки, hello получателя можно вычислить hello хэш-код с hello такими же параметрами, убедиться, что он возвращает toobe hello того же результата. Hello URI указывает область hello и имя ключа hello идентифицирует хэш hello toocompute toobe использовать политики hello. Это требуется для обеспечения безопасности. Если подпись hello не соответствует значению hello получателей (Service Bus) вычисляет, доступ запрещен. На этом этапе можно быть уверенным, что отправителя hello имел toohello ключ доступа и должны быть предоставлены права hello, указанным в политике hello.

Обратите внимание, что необходимо использовать hello кодировке ресурса (URI) для этой операции. Hello ресурса (URI) — hello, который запрашивается полный URI hello доступа toowhich ресурсов служебной шины. Например, `http://<namespace>.servicebus.windows.net/<entityPath>` или `sb://<namespace>.servicebus.windows.net/<entityPath>`. Вся строка будет выглядеть так: `http://contoso.servicebus.windows.net/contosoTopics/T1/Subscriptions/S3`.

правила авторизации общего доступа Hello, используемого для подписи должен быть настроен, этот URI, либо один из его родителей иерархических сущности hello. Например `http://contoso.servicebus.windows.net/contosoTopics/T1` или `http://contoso.servicebus.windows.net` в предыдущем примере hello.

Маркер SAS действителен для всех ресурсов в группе hello `<resourceURI>` используется в hello `signature-string`.

Hello [KeyName](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_KeyName) в hello SAS токен относится toohello **keyName** элемента hello правила авторизации общего доступа используется токен toogenerate hello.

Hello *URL-encoded-resourceURI* необходимо hello так же, как hello URI, используемый в строку hello-входа во время вычисления подписи hello hello. Значение должно быть [закодировано с помощью знака процента](https://msdn.microsoft.com/library/4fkewx0t.aspx).

Рекомендуется периодически заново формировать ключи hello, используемые в hello [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) объекта. Приложения обычно должны использовать hello [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) toogenerate маркер SAS. При повторном создании ключей hello, следует заменить hello [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) с старая первичная hello ключом и сформировать новый ключ в качестве hello новый первичный ключ. Это позволяет toocontinue использование токенов для авторизации, созданные hello старому первичному ключу, и который еще не истек.

Если ключ становится известен посторонним и у вас есть toorevoke hello ключи, можно повторно создать оба hello [PrimaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_PrimaryKey) и hello [SecondaryKey](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule#Microsoft_ServiceBus_Messaging_SharedAccessAuthorizationRule_SecondaryKey) из [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule), заменить их с использованием новых ключей. Эта процедура делает недействительными все маркеры, подписанные hello старые ключи.

## <a name="how-toouse-shared-access-signature-authentication-with-service-bus"></a>Способ проверки подлинности подписи общего доступа toouse со служебной шиной

Привет, следующие сценарии включают Настройка правил авторизации, Создание маркеров SAS и авторизация клиента.

Полный рабочий образец приложения служебной шины, который иллюстрирует hello конфигурации и используется авторизация SAS, в разделе [проверки подлинности подписи общего доступа с Service Bus](http://code.msdn.microsoft.com/Shared-Access-Signature-0a88adf8). Подходящий пример, иллюстрирующий использование правил авторизации SAS, настроенных в пространствах имен или разделах подписках Service Bus toosecure hello доступен здесь: [проверки подлинности с помощью общего подписи доступа (SAS) с подписками Service Bus ](http://code.msdn.microsoft.com/Using-Shared-Access-e605b37c).

## <a name="access-shared-access-authorization-rules-on-a-namespace"></a>Доступ к правилам авторизации общего доступа в пространстве имен

Операции на корень пространства имен Service Bus hello требуют проверки подлинности сертификата. Необходимо передать сертификат управления для вашей подписки Azure. tooupload сертификата управления, выполните действия hello [здесь](../cloud-services/cloud-services-configure-ssl-certificate-portal.md#step-3-upload-a-certificate), с помощью hello [портал Azure][Azure portal]. Дополнительные сведения о сертификатах управления Azure см. в разделе hello [Общие сведения о сертификатах Azure](../cloud-services/cloud-services-certs-create.md#what-are-management-certificates).

Конечная точка Hello для доступа к правил авторизации общего доступа на пространство имен служебной шины выглядит следующим образом:

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/
```

toocreate [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) объектов на пространство имен служебной шины, выполните операцию POST для этой конечной точки с hello сериализацией сведений о формате JSON или XML. Например:

```csharp
// Base address for accessing authorization rules on a namespace
string baseAddress = @"https://management.core.windows.net/<subscriptionId>/services/ServiceBus/namespaces/<namespace>/AuthorizationRules/";

// Configure authorization rule with base64-encoded 256-bit key and Send rights
var sendRule = new SharedAccessAuthorizationRule("contosoSendAll",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send });

// Operations on hello Service Bus namespace root require certificate authentication.
WebRequestHandler handler = new WebRequestHandler
{
    ClientCertificateOptions = ClientCertificateOption.Manual
};
// Access hello management certificate by subject name
handler.ClientCertificates.Add(GetCertificate(<certificateSN>));

HttpClient httpClient = new HttpClient(handler)
{
    BaseAddress = new Uri(baseAddress)
};
httpClient.DefaultRequestHeaders.Accept.Add(
    new MediaTypeWithQualityHeaderValue("application/json"));
httpClient.DefaultRequestHeaders.Add("x-ms-version", "2015-01-01");

// Execute a POST operation on hello baseAddress above toocreate an auth rule
var postResult = httpClient.PostAsJsonAsync("", sendRule).Result;
```

Аналогичным образом можно используйте операцию GET на правила hello конечной точки tooread hello авторизации, настроенные в пространстве имен hello.

tooupdate или удалить определенное правило авторизации, используйте hello, следующая конечная точка:

```http
https://management.core.windows.net/{subscriptionId}/services/ServiceBus/namespaces/{namespace}/AuthorizationRules/{KeyName}
```

## <a name="access-shared-access-authorization-rules-on-an-entity"></a>Доступ к правилам авторизации общего доступа в сущности

Вы можете получить доступ к [Microsoft.ServiceBus.Messaging.SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) настраивается на очередь служебной шины или разделе через hello объекта [AuthorizationRules](/dotnet/api/microsoft.servicebus.messaging.authorizationrules) коллекции в hello соответствующий [QueueDescription](/dotnet/api/microsoft.servicebus.messaging.queuedescription) или [TopicDescription](/dotnet/api/microsoft.servicebus.messaging.topicdescription).

Hello, следующий код показывает, как правила авторизации tooadd для очереди.

```csharp
// Create an instance of NamespaceManager for hello operation
NamespaceManager nsm = NamespaceManager.CreateFromConnectionString(
    <connectionString> );
QueueDescription qd = new QueueDescription( <qPath> );

// Create a rule with send rights with keyName as "contosoQSendKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoSendKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Send }));

// Create a rule with listen rights with keyName as "contosoQListenKey"
// and add it toohello queue description.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQListenKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] { AccessRights.Listen }));

// Create a rule with manage rights with keyName as "contosoQManageKey"
// and add it toohello queue description.
// A rule with manage rights must also have send and receive rights.
qd.Authorization.Add(new SharedAccessAuthorizationRule("contosoQManageKey",
    SharedAccessAuthorizationRule.GenerateRandomKey(),
    new[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send }));

// Create hello queue.
nsm.CreateQueue(qd);
```

## <a name="use-shared-access-signature-authorization"></a>Использование авторизации подписанного URL-адреса

Приложения, использующие hello Azure .NET SDK с библиотеками .NET служебной шины hello можно использовать авторизации SAS с помощью hello [SharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.sharedaccesssignaturetokenprovider) класса. Hello следующий код иллюстрирует использование hello tooa hello поставщик маркеров toosend сообщений очереди Service Bus.

```csharp
Uri runtimeUri = ServiceBusEnvironment.CreateServiceUri("sb",
    <yourServiceNamespace>, string.Empty);
MessagingFactory mf = MessagingFactory.Create(runtimeUri,
    TokenProvider.CreateSharedAccessSignatureTokenProvider(keyName, key));
QueueClient sendClient = mf.CreateQueueClient(qPath);

//Sending hello message tooqueue.
BrokeredMessage helloMessage = new BrokeredMessage("Hello, Service Bus!");
helloMessage.MessageId = "SAS-Sample-Message";
sendClient.Send(helloMessage);
```

Приложения также могут использовать SAS для проверки подлинности с помощью строки подключения SAS в методах, которые принимают строки подключения в качестве параметров.

Обратите внимание, что авторизации SAS toouse с ретранслятор Service Bus, можно использовать ключи SAS, настроенные на пространство имен Service Bus hello. Если вы явно создаете ретрансляцию в пространстве имен hello ([NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) с [RelayDescription](/dotnet/api/microsoft.servicebus.messaging.relaydescription)) объекта, можно задать правила SAS hello только для ретрансляции. toouse авторизации SAS с подписками Service Bus, можно использовать ключи SAS, настроенные в пространстве имен служебной шины или разделе.

## <a name="use-hello-shared-access-signature-at-http-level"></a>Использовать hello подпись общего доступа (на уровне HTTP)

Теперь, когда известно, как toocreate подписей общего доступа для всех сущностей в Service Bus, вы готовы tooperform HTTP POST:

```http
POST https://<yournamespace>.servicebus.windows.net/<yourentity>/messages
Content-Type: application/json
Authorization: SharedAccessSignature sr=https%3A%2F%2F<yournamespace>.servicebus.windows.net%2F<yourentity>&sig=<yoursignature from code above>&se=1438205742&skn=KeyName
ContentType: application/atom+xml;type=entry;charset=utf-8
``` 

Этот способ работает всегда. SAS можно создать для очереди, раздела или подписки. 

Если вы предоставляете отправителя или клиента маркер SAS, они не имеют hello ключ непосредственно, и нельзя изменить обратно tooobtain хэширования Привет его. Это позволяет контролировать, к чему вы предоставляете доступ и на какое время. Tooremember главное — что при изменении hello первичного ключа в политике hello все подписанные URL-адреса созданные из этого станут недействительными.

## <a name="use-hello-shared-access-signature-at-amqp-level"></a>Использовать hello подпись общего доступа (на уровне AMQP)

В предыдущем разделе hello вы увидели, как toouse hello маркер SAS с помощью запроса HTTP POST для отправки данных toohello Service Bus. Как известно, можно получить доступ к Service Bus с помощью hello Advanced Message Queuing Protocol (AMQP), toouse hello предпочитаемый протокол для повышения производительности во многих сценариях. описывается использование токенов SAS с помощью AMQP Hello в документе hello [AMQP Claim-Based безопасности версии 1.0](https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc) именно в рабочем проекте с момента выпуска 2013 но хорошо поддерживается Azure сегодня.

Перед началом tooService toosend данных шины, hello издатель должен отослать передачи маркера SAS hello внутри AMQP сообщение tooa четко определенных AMQP узел с именем **$cbs** (вы можете просмотреть его как «специальный» очередь используется tooacquire службы hello и проверить все маркеры SAS Hello). Hello издателя необходимо указать hello **ReplyTo** поле внутри сообщения hello AMQP — это узел hello, в какие hello службы отвечает издатель toohello с результатом проверки токенов hello (простой запрос ответ шаблон между hello Издатель и службы). Этот узел ответ создается на «hello ходу, «говоря о динамических» Создание «удаленного узла, как описано в спецификации hello AMQP 1.0. После проверки допустимости этот маркер SAS hello, hello издателя может продолжаться и запустить службу toohello toosend данных.

Hello следующие шаги показывают, как toosend hello маркер SAS с протоколом AMQP, с помощью hello [AMQP.Net Lite](https://github.com/Azure/amqpnetlite) библиотеки. Это полезно, если не удается использовать официальные hello пакет SDK служебной шины (например на WinRT, .net Compact Framework, платформа .net Micro Framework и Mono) разработке на языке C\#. Конечно, эта библиотека является полезным toohelp понять систему безопасности на основе утверждений работает на уровне AMQP hello, как было показано, как работает на уровне hello HTTP (с HTTP POST запроса и hello SAS маркера отправленных внутри hello» «заголовок авторизации). Если не требуется такой глубоких знаний о AMQP, можно использовать официальные hello пакет SDK служебной шины с помощью .net Framework приложения, которые будет выполнять ее автоматически.

### <a name="c35"></a>C&#35;

```csharp
/// <summary>
/// Send claim-based security (CBS) token
/// </summary>
/// <param name="shareAccessSignature">Shared access signature (token) toosend</param>
private bool PutCbsToken(Connection connection, string sasToken)
{
    bool result = true;
    Session session = new Session(connection);

    string cbsClientAddress = "cbs-client-reply-to";
    var cbsSender = new SenderLink(session, "cbs-sender", "$cbs");
    var cbsReceiver = new ReceiverLink(session, cbsClientAddress, "$cbs");

    // construct hello put-token message
    var request = new Message(sasToken);
    request.Properties = new Properties();
    request.Properties.MessageId = Guid.NewGuid().ToString();
    request.Properties.ReplyTo = cbsClientAddress;
    request.ApplicationProperties = new ApplicationProperties();
    request.ApplicationProperties["operation"] = "put-token";
    request.ApplicationProperties["type"] = "servicebus.windows.net:sastoken";
    request.ApplicationProperties["name"] = Fx.Format("amqp://{0}/{1}", sbNamespace, entity);
    cbsSender.Send(request);

    // receive hello response
    var response = cbsReceiver.Receive();
    if (response == null || response.Properties == null || response.ApplicationProperties == null)
    {
        result = false;
    }
    else
    {
        int statusCode = (int)response.ApplicationProperties["status-code"];
        if (statusCode != (int)HttpStatusCode.Accepted && statusCode != (int)HttpStatusCode.OK)
        {
            result = false;
        }
    }

    // hello sender/receiver may be kept open for refreshing tokens
    cbsSender.Close();
    cbsReceiver.Close();
    session.Close();

    return result;
}
```

Hello `PutCbsToken()` метод получает hello *подключения* (экземпляр класса подключение AMQP в соответствии со hello [AMQP .NET Lite библиотеки](https://github.com/Azure/amqpnetlite)), представляющий службу toohello подключения TCP hello и hello *sasToken* параметр toosend маркера SAS hello. 

> [!NOTE]
> Очень важно, что соединения hello создается с **механизма SASL проверки подлинности значение tooEXTERNAL** (и не hello обычного по умолчанию с именем пользователя и пароль, используемый, когда нет необходимости использовать маркер SAS toosend hello).
> 
> 

Далее издателю hello создает две связи AMQP для отправки маркера SAS hello и получения ответа hello (результат проверки токенов hello) из службы hello.

приветственное сообщение AMQP содержит набор свойств и больше сведений, чем простое сообщение. маркер SAS Hello — hello тело сообщения hello (использование конструктора). Hello **«ReplyTo»** свойству toohello имя узла для получения hello результат проверки связи приемника hello (если необходимо, и она будет создана динамически службой hello, можно изменить его имя). Hello последние три приложения и пользовательские свойства используются службы tooindicate hello какие операции имеет tooexecute. Описанный hello спецификация CBS, они должны быть hello **имя операции** hello («put-token»), **тип маркера** (в данном случае «servicebus.windows.net:sastoken») и hello **» Имя «hello аудитории** toowhich hello токен применяется (hello всей сущности).

После отправки hello маркера SAS на ссылку отправителя hello, hello издателя должна чтение hello ответа на ссылку приемника hello. Hello ответа имеет простое сообщение AMQP с свойства приложения с именем **«код состояния»** , может содержать hello же значений в виде кода состояния HTTP.

## <a name="rights-required-for-service-bus-operations"></a>Права, необходимые для операций служебной шины

Hello следующей таблице показаны hello права доступа, необходимые для выполнения различных операций на ресурсах Service Bus.

| Операция | Требуемое утверждение | Область утверждения |
| --- | --- | --- |
| **Пространство имен** | | |
| Настройка правила авторизации для пространства имен |управление |Любой адрес пространства имен |
| **Регистр служб** | | |
| Перечисление частных политик |управление |Любой адрес пространства имен |
| Начало прослушивания в пространстве имен |Прослушивание |Любой адрес пространства имен |
| Отправка сообщений tooa прослушивателя в пространстве имен |Отправка |Любой адрес пространства имен |
| **Очередь** | | |
| Создание очереди |управление |Любой адрес пространства имен |
| Удаление очереди |управление |Любой допустимый адрес очереди |
| Перечисление очередей |управление |/$Resources/Queues |
| Получение описания очереди hello |Управление |Любой допустимый адрес очереди |
| Настройка правила авторизации для очереди |управление |Любой допустимый адрес очереди |
| Отправка в очередь toohello |Отправка |Любой допустимый адрес очереди |
| Получение сообщений из очереди |Прослушивание |Любой допустимый адрес очереди |
| Прервать или завершить сообщения после получения сообщения hello в режиме пиковой блокировки |Прослушивание |Любой допустимый адрес очереди |
| Откладывание сообщения для последующего получения |Прослушивание |Любой допустимый адрес очереди |
| Назначение сообщению статуса недоставленного |Прослушивание |Любой допустимый адрес очереди |
| Получение состояния hello, связанного с сеансом очереди сообщений |Прослушивание |Любой допустимый адрес очереди |
| Задание состояния hello, связанный с сеансом очереди сообщений |Прослушивание |Любой допустимый адрес очереди |
| **Раздел** | | |
| Создание раздела |управление |Любой адрес пространства имен |
| Удаление раздела |управление |Любой допустимый адрес раздела |
| Перечисление разделов |управление |/$Resources/Topics |
| Получите описание раздела hello |Управление |Любой допустимый адрес раздела |
| Настройка правила авторизации для раздела |управление |Любой допустимый адрес раздела |
| Отправить toohello раздела |Отправка |Любой допустимый адрес раздела |
| **Подписка** | | |
| Создание подписки |управление |Любой адрес пространства имен |
| Удаление подписки |управление |../myTopic/Subscriptions/mySubscription |
| Перечисление подписок |управление |../myTopic/Subscriptions |
| Получение описания подписки |Управление |../myTopic/Subscriptions/mySubscription |
| Прервать или завершить сообщения после получения сообщения hello в режиме пиковой блокировки |Прослушивание |../myTopic/Subscriptions/mySubscription |
| Откладывание сообщения для последующего получения |Прослушивание |../myTopic/Subscriptions/mySubscription |
| Назначение сообщению статуса недоставленного |Прослушивание |../myTopic/Subscriptions/mySubscription |
| Получение состояния hello, связанного с сеансом раздела |Прослушивание |../myTopic/Subscriptions/mySubscription |
| Задание состояния hello, связанный с сеансом раздела |Прослушивание |../myTopic/Subscriptions/mySubscription |
| **Правила** | | |
| Создание правила |управление |../myTopic/Subscriptions/mySubscription |
| Удаление правила |управление |../myTopic/Subscriptions/mySubscription |
| Перечисление правил |Управление или прослушивание |../myTopic/Subscriptions/mySubscription/Rules 

## <a name="next-steps"></a>Дальнейшие действия

toolearn Дополнительные сведения о Service Bus обмена сообщениями, см. следующие разделы hello.

* [Базовая информация о служебной шине](service-bus-fundamentals-hybrid-solutions.md)
* [Очереди, разделы и подписки служебной шины](service-bus-queues-topics-subscriptions.md)
* [Как toouse очереди шины обслуживания](service-bus-dotnet-get-started-with-queues.md)
* [Как toouse Service Bus разделы и подписки](service-bus-dotnet-how-to-use-topics-subscriptions.md)

[Azure portal]: https://portal.azure.com