---
title: "Обзор шаблона лицензии Widevine | Документация Майкрософт"
description: "В этом разделе описан шаблон лицензии Widevine, который используется для настройки лицензий Widevine."
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
ms.openlocfilehash: 85de5765975b0c55fafe9bb4c14a1c1f435a6d5c
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/10/2018
---
# <a name="widevine-license-template-overview"></a>Обзор шаблона лицензии Widevine
С помощью служб мультимедиа Azure можно настраивать и запрашивать лицензии Google Widevine. Когда проигрыватель пытается воспроизвести содержимое, защищенное с помощью Widevine, в службу доставки лицензий отправляется запрос на получение лицензии. Если служба лицензий утвердит запрос, служба выдаст лицензию. Лицензия отправляется клиенту и используется для расшифровки и воспроизведения указанного содержимого.

Запрос на лицензию Widevine форматируется как сообщение JSON.  

>[!NOTE]
> Можно создать пустое сообщение без значений — просто {}. Затем будет создан шаблон лицензии со значениями по умолчанию. Значения по умолчанию подходят для большинства случаев. В сценариях доставки лицензий на основе технологий Майкрософт следует всегда использовать значения по умолчанию. Если необходимо задать значения параметров provider (поставщик) и content_id (идентификатор содержимого), то поставщик должен совпадать с учетными данными Widevine.

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
| ИМЯ | Значение | ОПИСАНИЕ |
| --- | --- | --- |
| payload |Строка в кодировке base64 |Запрос на лицензию, отправленный клиентом. |
| content_id |Строка в кодировке base64 |Идентификатор, используемый для получения идентификатора ключа и ключа содержимого для каждого content_key_specs.track_type. |
| provider |строка |Используется для поиска ключей и политик содержимого. Если для доставки лицензий Widevine используется доставка ключей Майкрософт, этот параметр пропускается. |
| policy_name |строка |Имя ранее зарегистрированной политики. Необязательный элемент. |
| allowed_track_types |enum |SD_ONLY или SD_HD. Контролирует, какие ключи содержимого включаются в лицензию. |
| content_key_specs |Массив структур JSON, см. раздел "Спецификации ключей содержимого".  |Более точный контроль возвращаемых ключей содержимого. Дополнительные сведения см. в разделе "Спецификации ключей содержимого". Указать можно только одно из значений allowed_track_types и content_key_specs. |
| use_policy_overrides_exclusively |Логическое значение: true или false |Используйте атрибуты политики, указанные в параметре policy_overrides, и пропустите все сохраненные ранее политики. |
| policy_overrides |Структура JSON, см. раздел "Переопределения политики". |Параметры политики для этой лицензии.  Если у этого ресурса есть предопределенная политика, будут использоваться указанные значения. |
| session_init |Структура JSON, см. раздел "Инициализация сеанса". |Необязательные данные передаются в лицензию. |
| parse_only |Логическое значение: true или false |Запрос на лицензию проанализирован, но лицензия не выдана. Но в ответе возвращаются значения из запроса на лицензию. |

## <a name="content-key-specs"></a>Спецификации ключей содержимого
Если политика существует, указывать какие-либо значения в спецификации ключа содержимого не требуется. Существующая политика, связанная с этим содержимым, используется для определения защиты выходных данных, например защиты цифрового содержимого с высокой пропускной способностью (HDCP) и Copy General Management System (CGMS). Если существующая политика не зарегистрирована на сервере лицензирования Widevine, поставщик содержимого может внедрить значения в запрос на лицензию.   

Каждое значение content_key_specs должно быть указано для всех записей независимо от параметра use_policy_overrides_exclusively. 

| ИМЯ | Значение | ОПИСАНИЕ |
| --- | --- | --- |
| content_key_specs. track_type |строка |Имя типа записи. Если content_key_specs указан в запросе лицензии, убедитесь, что все типы записей указаны явным образом. Невыполнение этого требования приведет к сбою воспроизведения последних 10 секунд. |
| content_key_specs  <br/> security_level |uint32 |Определяет требования к надежности клиента для воспроизведения. <br/> — Требуется программное шифрование методом белого ящика. <br/> — Требуются шифрование ПО и скрытый декодер. <br/> — Материал ключа и операции шифрования должны быть выполнены в резервной доверенной аппаратной среде выполнения. <br/> — Операции шифрования и расшифровки содержимого должны быть выполнены в резервной доверенной аппаратной среде выполнения.  <br/> — Шифрование, расшифровка и обработка всех носителей (сжатых и несжатых) должны быть выполнены в резервной доверенной аппаратной среде выполнения. |
| content_key_specs <br/> required_output_protection.hdc |Строка, одна из: HDCP_NONE, HDCP_V1, HDCP_V2 |Указывает, требуется ли HDCP. |
| content_key_specs <br/>key |Base64-<br/>Base64 |Ключ содержимого для этой записи. Если указано, требуется track_type или key_id. Поставщик содержимого с помощью этого параметра может вставить ключ содержимого для этой дорожки вместо того, чтобы сервер лицензирования Widevine создал или нашел ключ. |
| content_key_specs.key_ID |Двоичные данные строки в кодировке base64, 16 байт |Уникальный идентификатор ключа. |

## <a name="policy-overrides"></a>Переопределения политики
| ИМЯ | Значение | ОПИСАНИЕ |
| --- | --- | --- |
| policy_overrides. can_play |Логическое значение: true или false |Указывает, допускается ли воспроизведение содержимого. Значение по умолчанию — false. |
| policy_overrides. can_persist |Логическое значение: true или false |Указывает, что лицензия может быть сохранена в энергонезависимом хранилище для автономного использования. Значение по умолчанию — false. |
| policy_overrides. can_renew |Логическое значение: true или false |Указывает, что разрешено продление лицензии. Если указано значение "true", лицензию можно расширить с помощью периодического сигнала. Значение по умолчанию — false. |
| policy_overrides. license_duration_seconds |int64 |Указывает интервал времени для данной конкретной лицензии. Значение 0 указывает на неограниченное время. Значение по умолчанию — 0. |
| policy_overrides. rental_duration_seconds |int64 |Указывает интервал времени, в течение которого разрешено воспроизведение. Значение 0 указывает на неограниченное время. Значение по умолчанию — 0. |
| policy_overrides. playback_duration_seconds |int64 |Окно просмотра времени после начала воспроизведения в течение срока действия лицензии. Значение 0 указывает на неограниченное время. Значение по умолчанию — 0. |
| policy_overrides. renewal_server_url |строка |Все запросы на продление для этой лицензии направляются на указанный URL-адрес. Это поле используется, только если can_renew имеет значение true. |
| policy_overrides. renewal_delay_seconds |int64 |Число секунд после license_start_time перед первой попыткой продления. Это поле используется, только если can_renew имеет значение true. Значение по умолчанию — 0. |
| policy_overrides. renewal_retry_interval_seconds |int64 |Определяет задержку в секундах между последующими запросами на продление лицензии (в случае сбоя). Это поле используется, только если can_renew имеет значение true. |
| policy_overrides. renewal_recovery_duration_seconds |int64 |Интервал времени, в течение которого разрешено продолжать воспроизведение при неудачной попытке продления лицензии из-за внутренних проблем с сервером лицензирования. Значение 0 указывает на неограниченное время. Это поле используется, только если can_renew имеет значение true. |
| policy_overrides. renew_with_usage |Логическое значение: true или false |Указывает, что лицензия отправлена на продление в начале использования. Это поле используется, только если can_renew имеет значение true. |

## <a name="session-initialization"></a>Инициализация сеанса
| ИМЯ | Значение | ОПИСАНИЕ |
| --- | --- | --- |
| provider_session_token |Строка в кодировке base64 |Этот маркер сеанса передается обратно в лицензию и существует в рамках последующих операций продления. Маркер сеанса не сохраняется вне сеансов. |
| provider_client_token |Строка в кодировке base64 |Маркер клиента для отправки обратно в ответе лицензии. Если запрос лицензии содержит маркер клиента, это значение игнорируется. Маркер клиента сохраняется вне сеансов лицензии. |
| override_provider_client_token |Логическое значение: true или false |Если задано значение "false" и запрос лицензии содержит маркер клиента, используйте маркер из запроса, даже если в этой структуре был указан маркер клиента. Если задано значение "true", всегда используйте маркер, заданный в этой структуре. |

## <a name="configure-your-widevine-licenses-by-using-net-types"></a>Настройка лицензий Widevine с помощью типов .NET
Службы мультимедиа предоставляют API-интерфейсы .NET, которые позволяют настраивать лицензии Widevine. 

### <a name="classes-as-defined-in-the-media-services-net-sdk"></a>Классы, как определено в пакете SDK .NET для служб мультимедиа
Следующие классы являются определениями этих типов:

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
В следующем примере показано, как использовать API-интерфейсы .NET для настройки простой лицензии Widevine:

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

## <a name="see-also"></a>См. также
[Использование общего динамического шифрования PlayReady и (или) Widevine DRM](media-services-protect-with-playready-widevine.md)

