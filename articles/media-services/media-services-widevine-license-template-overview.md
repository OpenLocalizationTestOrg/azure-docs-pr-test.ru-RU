---
title: "Обзор шаблона лицензий aaaWidevine | Документы Microsoft"
description: "В этом разделе приводится обзор шаблона лицензий Widevine, использовать лицензии Widevine tooconfigure."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0e6f1f05-7ed6-4ed6-82a0-0cc2182b075a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 67a6ae38cf3d3c21e1b7282aef15f79b21776414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="widevine-license-template-overview"></a>Обзор шаблона лицензии Widevine
## <a name="overview"></a>Обзор
Службы мультимедиа Azure теперь включает лицензии Widevine tooconfigure и запроса. Когда проигрыватель hello конечный пользователь пытается tooplay Widevine защищенного содержимого запроса — службы доставки tooobtain лицензию для отправки toohello лицензии. Если hello служба лицензий утверждает запрос hello, она выдает лицензии hello отправленных toohello клиента и может быть используется toodecrypt- and -play hello указанным содержимым.

Запрос на лицензию Widevine форматируется как сообщение JSON.  

>[!NOTE]
> Вы можете toocreate пустое сообщение с нет значения просто «{}» и шаблон лицензии будет создана со всеми значениями по умолчанию. по умолчанию Hello работает в большинстве случаев. Например, для сценариев доставки лицензий на основе MS всегда используются значения по умолчанию. Если требуется hello tooset «поставщик» и «content_id» значения, поставщика должны совпадать учетными данными Widevine Google.

    {  
       “payload”:“<license challenge>”,
       “content_id”: “<content id>” 
       “provider”: ”<provider>”
       “allowed_track_types”:“<types>”,
       “content_key_specs”:[  
          {  
             “track_type”:“<track type 1>”
          },
          {  
             “track_type”:“<track type 2>”
          },
          …
       ],
       “policy_overrides”:{  
          “can_play”:<can play>,
          “can persist”:<can persist>,
          “can_renew”:<can renew>,
          “rental_duration_seconds”:<rental duration>,
          “playback_duration_seconds”:<playback duration>,
          “license_duration_seconds”:<license duration>,
          “renewal_recovery_duration_seconds”:<renewal recovery duration>,
          “renewal_server_url”:”<renewal server url>”,
          “renewal_delay_seconds”:<renewal delay>,
          “renewal_retry_interval_seconds”:<renewal retry interval>,
          “renew_with_usage”:<renew with usage>
       }
    }

## <a name="json-message"></a>Сообщение JSON
| Имя | Значение | Описание |
| --- | --- | --- |
| payload |строка в кодировке Base64 |запрос лицензии Hello, отправленные клиентом. |
| content_id |строка в кодировке Base64 |Идентификатор, используемый для каждого content_key_specs.track_type tooderive KeyId(s) и содержимого ключи. |
| provider |string |Используется toolook копирование содержимого ключи и политики. Если для доставки лицензий Widevine используется доставка ключей MS, то этот параметр пропускается. |
| policy_name |string |Имя ранее зарегистрированной политики. Необязательно |
| allowed_track_types |enum |SD_ONLY или SD_HD. Контролирует, какие ключи содержимого должны быть включены в лицензию. |
| content_key_specs |массив структур JSON, см. раздел **Спецификации ключей содержимого** ниже |Более точный контроль на какое содержимое ключей tooreturn. Более подробные сведения см. ниже в подразделе "Спецификации ключей содержимого".  Можно указать только один allowed_track_types и content_key_specs. |
| use_policy_overrides_exclusively |логическое Значение true или false |Используйте атрибуты политики, указанные в параметре policy_overrides, и пропустите все сохраненные ранее политики. |
| policy_overrides |структура JSON, см. раздел **Переопределения политики** ниже |Параметры политики для этой лицензии.  В событии hello этого актива имеет предварительно определенные политики, будут использоваться эти указанного значения. |
| session_init |структура JSON, см. раздел **Инициализация сеанса** ниже |Необязательные данные, передаваемые toolicense. |
| parse_only |логическое Значение true или false |запрос лицензии Hello анализируется, но лицензия не выдается. Однако запрос лицензии hello формы значения возвращаются в ответе hello. |

## <a name="content-key-specs"></a>Спецификации ключей содержимого
Если существует существующие политики, нет нет необходимости toospecify, любой hello значений в hello содержимого Spec ключ.  Hello существующую политику, связанную с этого содержимого будет использоваться toodetermine hello выходной защиты как HDCP и CGMS.  Если существующие политики не зарегистрирован hello Widevine сервера лицензирования, поставщик содержимого hello может вводить значения hello в запрос лицензии hello.   

Каждый content_key_specs необходимо указать для всех записей, независимо от того, параметр use_policy_overrides_exclusively hello. 

| Имя | Значение | Описание |
| --- | --- | --- |
| content_key_specs. track_type |string |Имя типа записи. Если content_key_specs указан в запросе лицензии hello, убедитесь, что toospecify, отслеживать все типы явным образом. Сбой toodo таким образом приведет к tooplayback сбоя за последние 10 секунд. |
| content_key_specs  <br/> security_level |uint32 |Определяет требования к надежности клиента для воспроизведения. <br/> 1. Требуется программное шифрование методом белого ящика. <br/> 2. Требуется шифрование ПО и скрытый декодер. <br/> 3 - hello ключа шифрования и материала операции должны выполняться в среде выполнения резервная копия доверенного оборудования. <br/> 4 - hello шифрования и декодирования содержимого должны выполняться в среде выполнения резервная копия доверенного оборудования.  <br/> 5 - hello шифрования, декодирования и все обработка hello носителя (сжатых и несжатых данных) должны быть обработаны в среде выполнения резервная копия доверенного оборудования. |
| content_key_specs <br/> required_output_protection.hdc |строка — одна из: HDCP_NONE, HDCP_V1, HDCP_V2 |Указывает, требуется ли HDCP. |
| content_key_specs <br/>key |строка в кодировке  <br/>Base64 |Toouse ключа содержимого для этой записи. Если указано, hello track_type или key_id является обязательным.  Этот параметр позволяет поставщику содержимого hello tooinject hello ключ содержимого для этой записи фиксированного сервера лицензирования Widevine создать или выполнить уточняющий запрос ключа. |
| content_key_specs.key_ID |Двоичные данные строки в кодировке Base64, 16 байт |Уникальный идентификатор для ключа hello. |

## <a name="policy-overrides"></a>Переопределения политики
| Имя | Значение | Описание |
| --- | --- | --- |
| policy_overrides. can_play |логическое Значение true или false |Указывает, что воспроизведение hello содержимое допускается. Значение по умолчанию — false. |
| policy_overrides. can_persist |логическое Значение true или false |Указывает, что этой лицензии hello может быть постоянное хранилище toonon volatile для автономного использования. Значение по умолчанию — false. |
| policy_overrides. can_renew |логическое значение: true или false |Указывает, что разрешено продление лицензии. Значение true, если длительность hello hello лицензии может быть расширена путем периодического сигнала. Значение по умолчанию — false. |
| policy_overrides. license_duration_seconds |int64 |Указывает hello интервал времени для определенной лицензии. Значение 0 указывает на длительность toohello no ограничение. Значение по умолчанию — 0. |
| policy_overrides. rental_duration_seconds |int64 |Указывает интервал времени hello во время воспроизведения разрешен. Значение 0 указывает на длительность toohello no ограничение. Значение по умолчанию — 0. |
| policy_overrides. playback_duration_seconds |int64 |Просмотр промежуток времени после запуска воспроизведения в течение интервала времени лицензии hello Hello. Значение 0 указывает на длительность toohello no ограничение. Значение по умолчанию — 0. |
| policy_overrides. renewal_server_url |string |Все запросы подтверждения (обновление) для этой лицензии должны направляться toohello указывается URL-адрес. Это поле используется только в том случае, если can_renew имеет значение "true". |
| policy_overrides. renewal_delay_seconds |int64 |Количество секунд после license_start_time перед первой попыткой продления. Это поле используется только в том случае, если can_renew имеет значение "true". Значение по умолчанию — 0. |
| policy_overrides. renewal_retry_interval_seconds |int64 |Определяет задержку hello в секундах между запросов на обновление последующих лицензий, в случае сбоя. Это поле используется только в том случае, если can_renew имеет значение "true". |
| policy_overrides. renewal_recovery_duration_seconds |int64 |Hello промежуток времени, в котором воспроизведения может быть toocontinue во время обновления попытки, пока неудачно из-за проблем toobackend с сервером лицензирования hello. Значение 0 указывает на длительность toohello no ограничение. Это поле используется только в том случае, если can_renew имеет значение "true". |
| policy_overrides. renew_with_usage |логическое значение: true или false |Указывает, что при запуске использование этой лицензии hello должны отправлять обновления. Это поле используется только в том случае, если can_renew имеет значение "true". |

## <a name="session-initialization"></a>Инициализация сеанса
| Имя | Значение | Описание |
| --- | --- | --- |
| provider_session_token |строка в кодировке Base64 |Этот маркер сеанса передается обратно в лицензии hello и будет существовать в последующих обновлений.  Помимо сеансов Hello маркер сеанса не сохраняются. |
| provider_client_token |строка в кодировке Base64 |Клиент маркера toosend обратно в ответе hello лицензии.  Если запрос лицензии hello содержит маркер клиента, это значение игнорируется. маркер клиента Hello будет сохраняется за пределами сеансы лицензии. |
| override_provider_client_token |логическое Значение true или false |Если значение false, а hello запрос лицензии содержит маркер клиента, используйте маркер hello из запроса hello даже маркера клиента был указан в этой структуре.  Значение true, если всегда используйте маркер hello, указанный в этой структуре. |

## <a name="configure-your-widevine-licenses-using-net-types"></a>Настройка лицензий Widevine с помощью типов .NET
Службы мультимедиа предоставляют API-интерфейсы .NET, которые позволяют настраивать лицензии Widevine. 

### <a name="classes-as-defined-in-hello-media-services-net-sdk"></a>Классы, как определено в hello Media Services .NET SDK
Здесь представлены Hello hello определений этих типов.

    public class WidevineMessage
    {
        public WidevineMessage();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public AllowedTrackTypes? allowed_track_types { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public ContentKeySpecs[] content_key_specs { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public object policy_overrides { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum AllowedTrackTypes
    {
        SD_ONLY = 0,
        SD_HD = 1
    }
    public class ContentKeySpecs
    {
        public ContentKeySpecs();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string key_id { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public RequiredOutputProtection required_output_protection { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public int? security_level { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string track_type { get; set; }
    }

    public class RequiredOutputProtection
    {
        public RequiredOutputProtection();

        public Hdcp hdcp { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum Hdcp
    {
        HDCP_NONE = 0,
        HDCP_V1 = 1,
        HDCP_V2 = 2
    }

### <a name="example"></a>Пример
Следующий пример показывает как Hello tooconfigure API-интерфейсы .NET toouse простой лицензии Widevine.

    private static string ConfigureWidevineLicenseTemplate()
    {
        var template = new WidevineMessage
        {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                new ContentKeySpecs
                {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                }
            },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
        };

        string configuration = JsonConvert.SerializeObject(template);
        return configuration;
    }


## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>Дополнительные материалы
[Использование общего динамического шифрования PlayReady и (или) Widevine DRM](media-services-protect-with-drm.md)

