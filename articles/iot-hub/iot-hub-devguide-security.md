---
title: "Центр IoT Azure безопасности aaaUnderstand | Документы Microsoft"
description: "Руководство разработчика - как toocontrol доступ к tooIoT концентратора для приложений устройств и серверной части. Содержит сведения о маркерах безопасности и поддержке сертификатов X.509."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 45631e70-865b-4e06-bb1d-aae1175a52ba
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 717726328a6bb5c5c334a123d0abfed711b2c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="control-access-tooiot-hub"></a>Элемент управления доступом tooIoT концентратора

В этой статье описываются hello механизмы защиты вашего центра IoT. Центр IoT использует *разрешений* конечной точки центра IoT tooeach toogrant доступа. Разрешения ограничивают hello доступа tooan IoT hub на основе функциональности.

Содержание статьи

* Hello различные разрешения, можно предоставить tooaccess серверной части приложения или устройства tooa ваш центр IoT.
* Здравствуйте, токены проверки подлинности процесса и hello используется tooverify разрешения.
* Как tooscope учетные данные toolimit доступ к ресурсам toospecific.
* Поддержка сертификатов X.509 в Центре Интернета вещей.
* Механизмы настраиваемой аутентификации устройства, использующие существующие реестры удостоверений устройств или схемы аутентификации.

### <a name="when-toouse"></a>Когда toouse

Необходимо иметь соответствующие разрешения tooaccess все конечные точки центра IoT hello. Например устройство необходимо включить токен, содержащий учетные данные безопасности вместе с каждое сообщение, что он отправляет tooIoT концентратора.

## <a name="access-control-and-permissions"></a>Контроль доступа и разрешений

Вы можете предоставить [разрешений](#iot-hub-permissions) в hello следующих способов:

* **Политики общего доступа на уровне Центра Интернета вещей**. Политики общего доступа могут предоставлять любое сочетание [разрешений](#iot-hub-permissions). Политики можно определить в hello [портал Azure][lnk-management-portal], или программно с помощью hello [API REST поставщика ресурсов центра IoT][lnk-resource-provider-apis]. Вновь созданный центр IoT состоит из следующих политик по умолчанию hello.

  * **iothubowner**: политика со всеми разрешениями;
  * **service**: политика с разрешением **ServiceConnect**;
  * **device**: политика с разрешением **DeviceConnect**;
  * **registryRead**: политика с разрешением **RegistryRead**;
  * **registryReadWrite**: политика с разрешениями **RegistryRead** и RegistryWrite.
  * **Учетные данные безопасности на уровне отдельного устройства**. Каждый Центр Интернета вещей содержит [реестр удостоверений][lnk-identity-registry]. Для каждого устройства в данном реестре удостоверений можно настроить учетные данные безопасности, которые предоставляют **DeviceConnect** разрешения области toohello соответствующие конечные точки устройства.

Например, в стандартном решении IoT:

* компонент управления Hello устройство использует hello *registryReadWrite* политики.
* компонент обработчика событий Hello использует hello *службы* политики.
* бизнес-логики Hello устройства во время выполнения компонент использует hello *службы* политики.
* Отдельные устройства подключения, используя учетные данные, хранящиеся в реестре удостоверений центра IoT hello.

> [!NOTE]
> Дополнительные сведения см. в статье о [разрешениях](#iot-hub-permissions).

## <a name="authentication"></a>Аутентификация

Центр IoT Azure предоставляет tooendpoints доступ, проверяя токен от hello общей политики доступа и учетные данные безопасности реестра удостоверений.

Учетные данные безопасности, такие как симметричные ключи никогда не отправляются по сети hello.

> [!NOTE]
> Hello поставщика ресурсов Azure IoT Hub защищена с помощью подписки Azure как всех поставщиков в hello [диспетчера ресурсов Azure][lnk-azure-resource-manager].

Дополнительные сведения о том, как tooconstruct и используйте маркеры безопасности, в разделе [маркеры безопасности центра IoT][lnk-sas-tokens].

### <a name="protocol-specifics"></a>Особенности протокола

Каждый поддерживаемый протокол, например MQTT, AMQP и HTTP, передает маркеры разными способами.

При использовании MQTT, пакет приветствия соединение имеет hello deviceId как hello ClientId, {iothubhostname} / {deviceId} в поле имени пользователя hello и маркер SAS в поле пароля hello. {iothubhostname} должно hello полный CName hello центр IoT (например, contoso.azure-devices.net).

При использовании [AMQP][lnk-amqp] Центр Интернета вещей поддерживает механизм [SASL PLAIN][lnk-sasl-plain] и стандарт [защиты AMQP на основе утверждений][lnk-cbs].

При использовании AMQP утверждений на основе безопасности, стандартные hello указывает как tootransmit эти токены.

ОБЫЧНЫЙ SASL hello **username** может быть:

* `{policyName}@sas.root.{iothubName}` — при использовании маркеров уровня Центра Интернета вещей;
* `{deviceId}@sas.{iothubname}` — при использовании маркеров уровня устройства.

В обоих случаях поле пароль hello содержит токен hello, как описано в [маркеры безопасности центра IoT][lnk-sas-tokens].

HTTP реализует проверку подлинности, включая действительный маркер в hello **авторизации** заголовка запроса.

#### <a name="example"></a>Пример

Имя пользователя (значение DeviceId следует вводить с учетом регистра): `iothubname.azure-devices.net/DeviceId`

Пароль (маркер создания SAS с hello [обозреватель устройств] [ lnk-device-explorer] средство):`SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`

> [!NOTE]
> Hello [пакеты SDK Azure IoT] [ lnk-sdks] автоматически создавать маркеры при подключении toohello службы. В некоторых случаях hello пакеты SDK Azure IoT не поддерживают все протоколы hello или все методы проверки подлинности hello.

### <a name="special-considerations-for-sasl-plain"></a>Специальные рекомендации для SASL PLAIN

При использовании обычного SASL с AMQP, клиент, подключающийся tooan центра IoT можно использовать один токен для каждого соединения TCP. По истечении срока действия маркера hello hello TCP-соединение отключается от службы hello и запускает переподключения. Такое поведение, пока не проблематично для серверной части приложения разорвал для приложения устройства для hello следующих причин:

* Шлюзы обычно подключаются от имени многих устройств. При использовании обычного SASL, они имеют toocreate distinct подключения TCP для каждого устройства, подключающегося tooan центр IoT. Этот сценарий значительно увеличивает hello потребление мощности и сетевых ресурсов и увеличивает задержку hello каждого подключения устройства.
* После каждого срока действия маркера hello увеличено использование ресурсов tooreconnect нарушена устройств с ограниченными ресурсами.

## <a name="scope-iot-hub-level-credentials"></a>Определение области действия учетных данных на уровне Центра Интернета вещей

Чтобы определить область действия для политик безопасности на уровне Центра Интернета вещей, создайте маркеры с помощью универсального кода (URI) ограниченного ресурса. Например, сообщения из устройства в облако toosend hello конечной точки с устройства — **/devices/ {deviceId} / сообщений и событий**. Можно также использовать политику общего доступа на уровне концентратора IoT с **DeviceConnect** toosign разрешения маркер равен которого resourceURI **/devices/ {deviceId}**. Этот подход создает маркер, который может использоваться toosend сообщения от имени устройства является только **deviceId**.

Этот механизм — примерно toohello [политики издателя концентраторов событий][lnk-event-hubs-publisher-policy]и появится возможность tooimplement настраиваемые методы проверки подлинности.

## <a name="security-tokens"></a>Маркеры безопасности Центра Интернета вещей

Центр IoT используется безопасность маркеры tooauthenticate устройств и служб tooavoid отправку ключей hello сети. Кроме того, маркеры безопасности ограничены по времени и области действия. [Пакеты SDK для Azure IoT][lnk-sdks] автоматически создают маркеры без специальной настройки. Некоторые сценарии требуют toogenerate и использование маркеров безопасности напрямую. Ниже приведены соответствующие сценарии.

* Hello прямое использование рабочих областей hello MQTT, AMQP или HTTP.
* Здравствуйте реализацию шаблона службы маркеров hello, как описано в статье [нестандартной проверки подлинности устройства][lnk-custom-auth].

Центр IoT также допускает tooauthenticate устройства с центром IoT [сертификаты X.509][lnk-x509].

### <a name="security-token-structure"></a>Структура маркера безопасности

Использовать безопасности маркеры toogrant привязанных ко времени доступа toodevices toospecific функциональных возможностей и служб в центр IoT. tooIoT tooconnect tooget авторизации концентратора, устройств и служб необходимо отправить безопасности маркеров, подписанных с общего доступа или симметричный ключ. Эти ключи хранятся в реестре удостоверений hello удостоверение устройства.

Токен, подписанным с функциями общего доступа ключ предоставляет доступ tooall hello, связанные с помощью политики hello общего доступа. Токен, подписанным с hello симметричный ключ только предоставляет удостоверение устройства **DeviceConnect** разрешение для hello связанного удостоверения устройства.

Hello маркер безопасности имеет hello следующий формат:

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

Ниже приведены hello ожидаемые значения.

| Значение | Описание |
| --- | --- |
| {signature} |Строки подписи HMAC-SHA256 hello формы: `{URL-encoded-resourceURI} + "\n" + expiry`. **Важные**: hello ключ декодирование из base64 и использовать в качестве ключа tooperform hello HMAC-SHA256 вычисления. |
| {resourceURI} |Префикс URI (с помощью сегмента) hello конечных точек, доступных с данным маркером, начиная с имени узла центра IoT hello (не protocol). Например, `myHub.azure-devices.net/devices/device1` |
| {expiry} |Строки UTF-8 для числа секунд, прошедших с начала эпохи hello: 00:00:00 UTC 1 января 1970 года. |
| {URL-encoded-resourceURI} |Чем меньше случае кодирование URL-адресов-hello нижнего регистра ресурса (URI) |
| {policyName} |Имя Hello hello общего toowhich политики доступа ссылается этот токен. Отсутствует, если токен hello ссылается реестра toodevice учетные данные. |

**Обратите внимание на префикс**: префикс URI hello вычисляется с помощью сегмента, а не символ. Например, `/a/b` — это префикс для `/a/b/c`, а не для `/a/bc`.

Hello следующие Node.js фрагмент показывает, функция, вызываемая **generateSasToken** Здравствуйте, вычисляет токен из входных данных hello `resourceUri, signingKey, policyName, expiresInMins`. Hello далее разделах описано, как варианты использования tooinitialize hello различных входных данных для другой токен hello.

```nodejs
var generateSasToken = function(resourceUri, signingKey, policyName, expiresInMins) {
    resourceUri = encodeURIComponent(resourceUri);

    // Set expiration in seconds
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    expires = Math.ceil(expires);
    var toSign = resourceUri + '\n' + expires;

    // Use crypto
    var hmac = crypto.createHmac('sha256', new Buffer(signingKey, 'base64'));
    hmac.update(toSign);
    var base64UriEncoded = encodeURIComponent(hmac.digest('base64'));

    // Construct autorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
};
```

Для сравнения hello эквивалентные toogenerate кода Python, маркер безопасности является:

```python
from base64 import b64encode, b64decode
from hashlib import sha256
from time import time
from urllib import quote_plus, urlencode
from hmac import HMAC

def generate_sas_token(uri, key, policy_name, expiry=3600):
    ttl = time() + expiry
    sign_key = "%s\n%d" % ((quote_plus(uri)), int(ttl))
    print sign_key
    signature = b64encode(HMAC(b64decode(key), sign_key, sha256).digest())

    rawtoken = {
        'sr' :  uri,
        'sig': signature,
        'se' : str(int(ttl))
    }

    if policy_name is not None:
        rawtoken['skn'] = policy_name

    return 'SharedAccessSignature ' + urlencode(rawtoken)
```

> [!NOTE]
> Так как срок действия маркера hello hello проверяется на компьютерах центра IoT, hello смещение на часах hello hello машины, который создает токен hello должен быть минимальным.

### <a name="use-sas-tokens-in-a-device-app"></a>Использование маркеров SAS в приложении для устройства

Существует два способа tooobtain **DeviceConnect** разрешений с центром IoT с маркерами безопасности: используйте [ключ симметричного устройства из реестра удостоверений hello](#use-a-symmetric-key-in-the-identity-registry), или используйте [общий ключ доступа](#use-a-shared-access-policy).

Помните, что все функциональные возможности, доступные с устройств, намеренно предоставляются в конечных точках с префиксом `/devices/{deviceId}`.

> [!IMPORTANT]
> Hello только что центр IoT проверяет подлинность определенного устройства при использовании симметричным ключом удостоверения устройства hello. В случаях если политика общего доступа используется tooaccess функциональные возможности устройства, hello решения необходимо учитывать компонент hello выдачи маркера безопасности hello доверенного компонента.

конечные точки с выходом устройства Hello являются (вне зависимости от протокола hello):

| Конечная точка | Функции |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |Отправка сообщений с устройства в облако. |
| `{iot hub host name}/devices/{deviceId}/devicebound` |Получение сообщений из облака на устройство. |

### <a name="use-a-symmetric-key-in-hello-identity-registry"></a>Использовать симметричный ключ в реестре удостоверений hello

При использовании симметричного ключа удостоверения устройства toogenerate маркер, hello Имя_политики (`skn`) элемент маркера hello пропускается.

Например маркер создания tooaccess hello все функциональные возможности устройства должны иметь следующие параметры:

* универсальный код ресурса (URI): `{IoT hub name}.azure-devices.net/devices/{device id}`;
* ключ подписи: любого симметричного ключа для hello `{device id}` удостоверения
* имя политики не требуется;
* время окончания срока действия.

Пример использования hello, предшествующий Node.js функция будет следующим:

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

Hello результат, который предоставляет функциональные возможности tooall доступа для устройстве 1, будет следующим:

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> Он является маркер SAS, с помощью hello .NET возможных toogenerate [обозреватель устройств] [ lnk-device-explorer] инструмент либо hello кросс платформенных, основанные на узлах [explorer центром IOT] [ lnk-iothub-explorer] программы командной строки.

### <a name="use-a-shared-access-policy"></a>Использование политики общего доступа

При создании маркера из политики общего доступа установлен hello `skn` toohello имя поля hello политики. Эта политика необходимо предоставить hello **DeviceConnect** разрешение.

приведены Hello два основных сценария использования функциональные возможности устройства tooaccess политики общего доступа.

* [облачные шлюзы протоколов][lnk-endpoints];
* [службы маркеров] [ lnk-custom-auth] используется tooimplement пользовательских схем проверки подлинности.

С момента hello политики общего доступа могут потенциально предоставлять доступ tooconnect любое устройство является важным toouse hello правильный URI ресурса, при создании маркеров безопасности. Этот параметр особенно важен для служб маркеров, которые имеют tooscope hello маркера tooa определенному устройству с помощью hello ресурса (URI). Он менее критичен для шлюзов протоколов, так как они уже обрабатывают трафик для всех устройств.

Например, маркер службы с помощью предварительно созданного hello общих политика доступа **устройства** создать токен hello следующие параметры:

* универсальный код ресурса (URI): `{IoT hub name}.azure-devices.net/devices/{device id}`;
* ключ подписи: один из ключей hello hello `device` политики,
* имя политики: `device`;
* время окончания срока действия.

Пример использования hello, предшествующий Node.js функция будет следующим:

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

Hello результат, который предоставляет функциональные возможности tooall доступа для устройстве 1, будет следующим:

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

Использовать шлюз протокола hello же маркера для всех устройств, которые просто параметр hello ресурса (URI), слишком`myhub.azure-devices.net/devices`.

### <a name="use-security-tokens-from-service-components"></a>Использование маркеров безопасности из компонентов службы

Компоненты службы можно создавать только маркеры безопасности, с помощью политики общего доступа, предоставление hello соответствующие разрешения, как описано выше.

Вот hello функции службы, предоставляемые hello конечных точек.

| Конечная точка | Функции |
| --- | --- |
| `{iot hub host name}/devices` |Создание, обновление, извлечение и удаление удостоверений устройств. |
| `{iot hub host name}/messages/events` |Получение сообщений с устройства в облако. |
| `{iot hub host name}/servicebound/feedback` |Получение ответа на сообщения, отправляемые из облака на устройство. |
| `{iot hub host name}/devicebound` |Отправка сообщений из облака на устройство. |

Например, службы, создание с помощью предварительно созданного hello общих политика доступа **registryRead** создать токен hello следующие параметры:

* универсальный код ресурса (URI): `{IoT hub name}.azure-devices.net/devices`;
* ключ подписи: один из ключей hello hello `registryRead` политики,
* имя политики: `registryRead`;
* время окончания срока действия.

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

результат Hello, которой предоставляется доступ tooread все удостоверения на устройстве, будет следующим:

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a>Поддерживаемые сертификаты X.509

Можно использовать любой tooauthenticate сертификат X.509 устройства с центром IoT. Сертификаты включают в себя:

* **Существующий сертификат X.509**. Возможно, устройство уже имеет связанный сертификат X.509. Hello устройство может использовать этот сертификат tooauthenticate с центром IoT.
* **Самостоятельно сформированный и самозаверяющий сертификат X-509**. Изготовителя устройства или собственных разработчик может создать эти сертификаты и сохранить hello соответствующий закрытый ключ (и сертификата) на устройстве hello. Для этого вы можете использовать такие инструменты, как [OpenSSL][lnk-openssl] и служебная программа [Windows SelfSignedCertificate][lnk-selfsigned].
* **Сертификат X.509, подписанный центром сертификации**. tooidentify устройства и выполнять его проверку подлинности с центром IoT, можно использовать сертификат X.509 созданный и подписанный с центром сертификации (ЦС). Центр IoT только проверяет, что отпечаток hello представлены соответствует отпечатку hello настроен. Центром IOT не проверяет цепочку сертификатов hello.

Для аутентификации устройство может использовать только один из вариантов: либо сертификат X.509, либо маркер безопасности.

### <a name="register-an-x509-certificate-for-a-device"></a>Регистрация сертификата X.509 для устройства

Hello [пакет SDK службы Azure IoT для C#] [ lnk-service-sdk] (версия 1.0.8+) поддерживает регистрации устройства, использующего сертификат X.509 для проверки подлинности. Другие интерфейсы API (например, импорт и экспорт устройств) также поддерживают сертификаты X.509.

### <a name="c-support"></a>Поддержка C\#

Hello **RegistryManager** класс предоставляет tooregister программный способ устройства. В частности, hello **AddDeviceAsync** и **UpdateDeviceAsync** методы позволяют tooregister и обновить устройство в hello реестра удостоверений центр IoT. Эти два метода используют экземпляр **устройства** в качестве входных данных. Hello **устройства** класс включает **проверки подлинности** свойство, которое позволяет вам toospecify первичного и вторичного X.509 отпечатки сертификата. отпечаток Hello представляет хэш SHA-1 сертификата X.509 hello (хранимая с помощью двоичной кодировке DER). Предусмотрена возможность hello указания первичного отпечаток или получателей отпечаток или оба. Отпечатки основного и дополнительного, поддерживаемых toohandle сценариев смены сертификата.

> [!NOTE]
> Центр IoT не требует или сохранить hello весь сертификат X.509, только отпечаток hello.

Ниже приведен пример C\# кода устройства с помощью сертификата X.509 tooregister фрагмент кода:

```csharp
var device = new Device(deviceId)
{
  Authentication = new AuthenticationMechanism()
  {
    X509Thumbprint = new X509Thumbprint()
    {
      PrimaryThumbprint = "921BC9694ADEB8929D4F7FE4B9A3A6DE58B0790B"
    }
  }
};
RegistryManager registryManager = RegistryManager.CreateFromConnectionString(deviceGatewayConnectionString);
await registryManager.AddDeviceAsync(device);
```

### <a name="use-an-x509-certificate-during-run-time-operations"></a>Использование сертификата X.509 во время выполнения операций среды выполнения

Hello [устройств Azure IoT SDK для .NET] [ lnk-client-sdk] (версия 1.0.11+) поддерживает использование hello сертификатов X.509.

### <a name="c-support"></a>Поддержка C\#

Здравствуйте, класс **DeviceAuthenticationWithX509Certificate** поддерживает hello создание **DeviceClient** экземпляров с помощью сертификата X.509. сертификат X.509 Hello должен быть в формате PFX (также называемый PKCS #12) hello, который содержит закрытый ключ hello.

Ниже приведен образец фрагмента кода:

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a>Настраиваемая проверка подлинности устройства

Можно использовать центр IoT hello [реестра удостоверений] [ lnk-identity-registry] с помощью управление доступом и учетные данные безопасности на устройство tooconfigure [маркеры] [ lnk-sas-tokens] . Если решения IoT уже имеет схему пользовательское удостоверение реестра или проверку подлинности, рассмотрите возможность создания *токена службы* toointegrate эта инфраструктура с центром IoT. Таким образом можно использовать и другие функции IoT в решении.

Служба маркеров — это пользовательская облачная служба. Она использует Центр IoT *общей политики доступа* с **DeviceConnect** toocreate разрешений *уровня устройства* маркеры. Эти маркеры позволяют центра IoT tooyour tooconnect устройства.

![Действия службы маркеров шаблона hello][img-tokenservice]

Ниже приведены основные этапы hello hello шаблона службы маркеров.

1. Создание политики общего доступа Центра Интернета вещей с разрешениями **DeviceConnect** для вашего Центра Интернета вещей. Эту политику можно создать в hello [портал Azure] [ lnk-management-portal] или программными средствами. Hello маркера служба использует этот токены hello toosign политики, созданные им.
1. Когда устройство должно tooaccess концентратор IoT, подписанный маркер запросов из токена службы. Hello устройства могут проходить проверку подлинности с удостоверением пользовательское удостоверение hello toodetermine проверки подлинности реестру схемы устройства, hello маркера служба использует маркер toocreate hello.
1. Служба маркеров Hello возвращает маркер. Hello токен создается с помощью `/devices/{deviceId}` как `resourceURI`, с `deviceId` как устройство hello, проходящего проверку подлинности. Служба маркеров Hello использует hello общей политики tooconstruct hello токен доступа.
1. Hello устройства с помощью токена hello непосредственно с центром IoT hello.

> [!NOTE]
> Можно использовать класс .NET hello [SharedAccessSignatureBuilder] [ lnk-dotnet-sas] или hello класс Java [IotHubServiceSasToken] [ lnk-java-sas] toocreate маркер в службе маркеров.

Hello службы маркеров можно задать срок действия токена hello в случае необходимости. По истечении срока действия маркера hello центра IoT hello разрывает подключение устройства hello. Затем устройство hello должен запросить новый маркер от службы маркеров hello. Короткий срок увеличивает нагрузку hello на устройстве hello и службой маркеров hello.

Концентратора tooyour tooconnect устройства, необходимо добавить его toohello реестра удостоверений центр IoT — несмотря на то, что устройство hello использует токен и не tooconnect ключа устройства. Таким образом, вы можете продолжить toouse контроля доступа на устройство, включение или отключение устройства удостоверений в hello [реестра удостоверений][lnk-identity-registry]. Этот подход снижает риски hello использования маркеров со временем long истечения срока действия.

### <a name="comparison-with-a-custom-gateway"></a>Сравнение с настраиваемым шлюзом

шаблон службы маркеров Hello является hello рекомендуется tooimplement способом схему проверки подлинности реестру пользовательское удостоверение с центром IoT. Рекомендуется использовать такую схему, поскольку центр IoT будет toohandle большая часть трафика hello решения. Однако если hello пользовательской схемы проверки подлинности Итак находящаяся между протокола hello, может потребоваться *пользовательского шлюза* tooprocess все hello трафика. В качестве примера сценария можно привести использование [протокола TLS и общих ключей][lnk-tls-psk]. Дополнительные сведения см. в разделе hello [шлюз протокола] [ lnk-protocols] раздела.

## <a name="reference-topics"></a>Справочные материалы

Hello следующие справочные разделы предоставляют дополнительные сведения о центра IoT tooyour управления доступом.

## <a name="iot-hub-permissions"></a>Разрешения Центра Интернета вещей

Hello следующей таблице перечислены разрешения hello, можно использовать центр IoT tooyour toocontrol доступа.

| Разрешение | Примечания |
| --- | --- |
| **RegistryRead** |Предоставляет доступ на чтение toohello удостоверение реестра. Дополнительные сведения см. в разделе о [реестре удостоверений][lnk-identity-registry]. <br/>Это разрешение используется серверными облачными службами. |
| **RegistryReadWrite** |Предоставление доступа чтения и записи toohello реестра удостоверений. Дополнительные сведения см. в разделе о [реестре удостоверений][lnk-identity-registry]. <br/>Это разрешение используется серверными облачными службами. |
| **ServiceConnect** |Предоставляет доступ к связи с выходом службы toocloud и мониторинг конечных точек. <br/>Предоставляет разрешение tooreceive устройства в облако сообщений, отправки сообщений облака на устройство и получить hello соответствующего подтверждения доставки. <br/>Отправка подтверждения доставки tooretrieve предоставляет разрешения для файла. <br/>Предоставляет разрешение tooaccess устройства близнецы tooupdate теги нужными свойствами получить свойства отчета и выполнения запросов. <br/>Это разрешение используется серверными облачными службами. |
| **DeviceConnect** |Предоставляет доступ к стороне toodevice конечных точек. <br/>Предоставляет разрешение toosend устройства в облако сообщения и получать сообщения облака на устройство. <br/>Предоставляет разрешение tooperform отправки файла на устройстве. <br/>Предоставляет разрешение tooreceive устройства двойных требуемого свойства уведомления и обновления устройств двойных отчета свойства. <br/>Передает файл tooperform предоставляет разрешение. <br/>Это разрешение используют устройства. |

## <a name="additional-reference-material"></a>Дополнительные справочные материалы

Другие разделы ссылку в hello центра IoT руководстве для разработчиков:

* [Конечные точки центра IoT] [ lnk-endpoints] описывает hello различные конечные точки, предоставляемые каждый центр IoT для операций времени выполнения и управления.
* [Регулирование и квоты] [ lnk-quotas] описывает hello квот и регулирования, применяющимся toohello службы центра IoT.
* [Пакеты SDK устройств и служб Azure IoT] [ lnk-sdks] списки hello языка различных пакетов SDK, которые можно использовать при разработке приложений, устройств и служб, которые взаимодействуют с центром IoT.
* [Язык запросов центра IoT] [ lnk-query] описывает hello язык запросов, можно использовать tooretrieve сведения из центра IoT близнецы устройства и заданий.
* [Поддержка MQTT концентратора IoT] [ lnk-devguide-mqtt] приведены более подробные сведения о поддержке центра IoT протокола MQTT hello.

## <a name="next-steps"></a>Дальнейшие действия

Теперь вы узнали, как toocontrol доступа центра IoT, можно получить в следующие разделы руководства разработчика центра IoT hello:

* [Конфигурации и состояния toosynchronize близнецы устройства][lnk-devguide-device-twins]
* [Вызов прямого метода на устройстве (предварительная версия)][lnk-devguide-directmethods]
* [Schedule jobs on multiple devices][lnk-devguide-jobs] (Планирование заданий на нескольких устройствах)

При желании tootry некоторые основные понятия hello, описанных в этой статье, могут быть интересны следующие учебники центра IoT hello параметры:

* [Приступая к работе с Центром Интернета вещей Azure][lnk-getstarted-tutorial]
* [Способ сообщений toosend облака на устройство с центром IoT][lnk-c2d-tutorial]
* [Как tooprocess сообщения из устройства в облако центра IoT][lnk-d2c-tutorial]

<!-- links and images -->

[img-tokenservice]: ./media/iot-hub-devguide-security/tokenservice.png
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-openssl]: https://www.openssl.org/
[lnk-selfsigned]: https://technet.microsoft.com/library/hh848633

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-sas-tokens]: iot-hub-devguide-security.md#security-tokens
[lnk-amqp]: https://www.amqp.org/
[lnk-azure-resource-manager]: ../azure-resource-manager/resource-group-overview.md
[lnk-cbs]: https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc
[lnk-event-hubs-publisher-policy]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab
[lnk-management-portal]: https://portal.azure.com
[lnk-sasl-plain]: http://tools.ietf.org/html/rfc4616
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-dotnet-sas]: https://msdn.microsoft.com/library/microsoft.azure.devices.common.security.sharedaccesssignaturebuilder.aspx
[lnk-java-sas]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth._iot_hub_service_sas_token
[lnk-tls-psk]: https://tools.ietf.org/html/rfc4279
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-custom-auth]: iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: iot-hub-devguide-security.md#supported-x509-certificates
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-client-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
