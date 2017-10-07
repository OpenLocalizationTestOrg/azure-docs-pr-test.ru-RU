---
title: "заметки о выпуске служб aaaMedia | Документы Microsoft"
description: "Заметки о выпуске служб мультимедиа"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ca2d7af-1cf0-45fa-9585-3b73f3ee057d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: media
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: c365b1133987267173ec858298c4c6de62744946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-release-notes"></a>Заметки о выпуске служб мультимедиа Azure
В этих заметках описаны изменения по сравнению с предыдущими выпусками, а также известные проблемы.

> [!NOTE]
> Мы toohear из наших клиентов и сосредоточиться на исправлении проблем, влияющих на вас. tooreport проблема или задать вопросы, опубликуйте hello [форум MSDN по службам мультимедиа Azure].
> 
> 

## <a id="issues"></a>Известные проблемы
### <a id="general_issues"></a>Общие проблемы служб мультимедиа
| Проблема | Описание |
| --- | --- |
| Несколько общих заголовков HTTP в API-интерфейса REST hello не предоставляются. |При разработке приложений служб мультимедиа с помощью API-интерфейса REST hello выяснится, что полей общих заголовков HTTP (включая CLIENT-REQUEST-ID REQUEST-ID и RETURN-CLIENT-REQUEST-ID) не поддерживаются. в дальнейшем будут добавлены заголовки Hello. |
| URL-кодирование содержимого не допускается. |Службы мультимедиа используют значение hello hello свойство IAssetFile.Name при построении URL-адреса для hello, потоковая передача содержимого (например, http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) По этой причине кодирование с помощью знака процента не допускается. Здравствуйте, значение hello **имя** свойство не может иметь любой из следующих hello [процентов зарезервированные символы](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! * "();: @& = + $, /? % # []». Кроме того, может использоваться только один знак ".". для расширения имени файла hello. |
| Здравствуйте, ListBlobs метод, который входит в состав hello пакет SDK хранилища Azure версии 3.x завершается ошибкой. |Службы мультимедиа создают URL-адреса SAS основании hello [2012-02-12](https://docs.microsoft.com/rest/api/storageservices/Version-2012-02-12) версии. Toouse пакет SDK хранилища Azure toolist BLOB-объектов в контейнере больших двоичных объектов, используйте hello [CloudBlobContainer.ListBlobs](http://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.listblobs.aspx) метод, который входит в пакет SDK хранилища Azure версии 2.x. Здравствуйте, ListBlobs метод, который входит в состав hello пакет SDK хранилища Azure версии 3.x, выдает ошибку. |
| Механизм регулирования служб мультимедиа ограничивает использование ресурсов hello приложениями, отправляющими Чрезмерное число запросов toohello службы. Hello служба может возвратить код состояния HTTP служба недоступна (503) hello. |Дополнительные сведения см. в описании hello кода состояния HTTP hello 503 в hello [коды ошибок Azure Media Services](media-services-encoding-error-codes.md) раздела. |
| При запросе сущности, имеется ограничение в 1000 сущностей, возвращаемых одновременно, так как открытые v2 REST ограничивает результаты too1000 результаты запроса. |Требуется toouse **пропустить** и **принимать** (.NET) и **верхней** (REST), как описано в [в этом примере .NET](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) и [этот интерфейс API REST Пример](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities). |
| Некоторые клиенты могут попадаться с проблемой тег повтора манифеста Smooth Streaming hello. |Дополнительные сведения см. в [этом разделе](media-services-deliver-content-overview.md#known-issues). |
| Объекты в пакете SDK .NET для служб мультимедиа Azure не могут быть сериализованы и поэтому не работают со службой кэша Azure. |Если при попытке tooadd объект SDK AssetCollection hello tooserialize его tooAzure кэширование, исключение создается исключение. |
| Задание кодирования завершается ошибкой с таким сообщением: "Stage: DownloadFile. Code: System.NullReferenceException". |Hello типичный рабочий процесс в кодировки — tooan tooupload входные файлы видео входных активов и отправки один, или несколько заданий кодирования, для входных активов, без дальнейшего изменения входных активов. Однако при изменении hello мультимедиа (например, добавление или удаление или переименование файлов в пределах hello активов) ввода, а затем последующие задания может завершиться с ошибкой DownloadFile. решение Hello — toodelete мультимедиа ввода hello и повторно отправить входные файлы tooa новый актив. |

## <a id="rest_version_history"></a>Журнал версий интерфейса API REST
Сведения о hello журнал версий API REST служб мультимедиа см. в разделе [Справочник API REST служб мультимедиа Azure].

## <a name="june-2017-release"></a>Выпуск: июнь 2017 г.

Службы мультимедиа теперь поддерживают [аутентификацию на основе Azure Active Directory (Azure AD)](media-services-use-aad-auth-to-access-ams-api.md).

> [!IMPORTANT]
> В настоящее время службы мультимедиа поддерживают модель проверки подлинности службы контроля доступа Azure hello. Тем не менее авторизация посредством службы контроля доступа будет объявлена устаревшей 1 июня 2018 года. Рекомендуется как можно быстрее перейти модель проверки подлинности toohello Azure AD.

## <a name="march-2017-release"></a>Выпуск от марта 2017 г.

Теперь можно использовать стандартные мультимедиа Azure слишком[автоматическое создание лестницу скоростью](media-services-autogen-bitrate-ladder-with-mes.md) , указав «Адаптивной потоковой передачи» hello предустановленной строки при создании задания кодирования. «Адаптивной потоковой передачи» будет hello рекомендуемые конфигурации, если вы хотите tooencode видео для потоковой передачи с помощью служб мультимедиа. Если требуется toocustomize кодировку конфигурации для конкретного сценария можно начать с [эти](media-services-mes-presets-overview.md) стили.

Теперь можно использовать Azure Media стандартного или расширенного рабочего процесса кодировщика мультимедиа слишком[создать задачу кодирования, которая приводит к возникновению ошибки блоки fMP4](media-services-generate-fmp4-chunks.md). 


## <a name="febuary-2017-release"></a>Выпуск: февраль 2017 г.

Начиная с 1 апреля 2017 г., записи любого задания в вашей учетной записи старше 90 дней автоматически удаляется, а также связанные с ней записи задачи, даже если hello общее количество записей ниже максимальная квота hello. Если вам нужна информация задания или задачи hello tooarchive, можно использовать код hello описано [здесь](media-services-dotnet-manage-entities.md).

## <a name="january-2017-release"></a>Выпуск: январь 2017 г.

В Microsoft Azure Media Services (AMS) **конечной точки потоковой передачи** представляет собой службу потоковой передачи, способную доставить содержимое напрямую tooa приложение проигрывателя клиента или tooa сеть доставки содержимого (CDN) для дальнейшего распределения. Службы мультимедиа также обеспечивают прозрачную интеграцию с Azure CDN. Hello исходящим потоком из службы StreamingEndpoint может быть обновляющегося потока, видео по запросу или последовательную загрузку актива в учетной записи служб мультимедиа. Каждая учетная запись служб мультимедиа Azure включает конечную точку потоковой передачи по умолчанию. Можно создать дополнительные конечные точки потоковой передачи под учетной записью hello. Доступны две версии конечных точек потоковой передачи: 1.0 и 2.0. Начиная с 10 января 2017 г. все новые учетные записи AMS будут включать конечную точку потоковой передачи версии 2.0 **по умолчанию**. Дополнительные добавления учетной записи toothis конечные точки потоковой передачи также будет версии 2.0. Это изменение не повлияет на существующие учетные записи hello; существующих конечных точек потоковой передачи будет версии 1.0, а также может быть обновленного tooversion 2.0. Это изменение повлечет изменения в поведении, выставлении счетов и функциях (дополнительные сведения см. [здесь](media-services-streaming-endpoints-overview.md)).

Кроме того, службы мультимедиа Azure начиная с версии hello 2,15, добавлены следующие свойства toohello конечной точки потоковой передачи сущности hello: **CdnProvider**, **CdnProfile**,  **FreeTrialEndTime**, **StreamingEndpointVersion**. Подробный обзор этих свойств см. [здесь](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint). 

## <a name="december-2016-release"></a>Выпуск: декабрь 2016 г.

Службы мультимедиа Azure теперь включает tooaccess данные телеметрии и показатели для служб. Текущая версия Hello AMS позволяет собирать данные телеметрии для динамического канала конечной точки потоковой передачи, и архив сущностей в реальном времени. Чтобы узнать больше, ознакомьтесь с [этим](media-services-telemetry-overview.md) разделом.

## <a id="july_changes16"></a>Выпуск: июль 2016 г.
### <a name="updates-toomanifest-file-ism-generated-by-encoding-tasks"></a>Файл toomanifest обновления (*. Созданные задач кодирования ISM)
После кодирования задачи отправленной tooMedia стандартного кодировщика или Azure Media Encoder, создает задачу кодирования hello [файла манифеста потоковой передачи](media-services-deliver-content-overview.md) (* .ism) файл в hello выходных активов. С последнего выпуска службы hello был обновлен синтаксис hello этого файла манифеста потоковой передачи.

> [!NOTE]
> синтаксис Hello hello потоковой передачи файла манифеста (.ism) зарезервирован для внутреннего использования и является toochange субъекта в будущих выпусках. Не изменять и управлять hello содержимое этого файла.
> 
> 

### <a name="a-new-client-manifest-ismc-file-is-generated-in-hello-output-asset-when-an-encoding-task-outputs-one-or-more-mp4-files"></a>Новый манифест клиента (*. Файл ISMC) создается в hello вывода активов, если задачу кодирования выводит один или несколько MP4-файлов
Начиная с последнего выпуска службы hello, после завершения hello задачи кодирования, создает один дополнительные MP4-файлов, hello выходных данных средства также будет содержать файл манифеста (*.ismc) для потоковой передачи клиента. файл .ismc Hello позволяет повысить производительность hello динамической потоковой передачи. 

> [!NOTE]
> синтаксис Hello hello пользовательского файла манифеста (.ismc) зарезервирован для внутреннего использования и является toochange субъекта в будущих выпусках. Не изменять и управлять hello содержимое этого файла.
> 
> 

Дополнительную информацию см. в [этом](https://blogs.msdn.microsoft.com/randomnumber/2016/07/08/encoder-changes-within-azure-media-services-now-create-ismc-file/) блоге.

### <a name="known-issues"></a>Известные проблемы
Некоторые клиенты могут попадаться с проблемой тег повтора манифеста Smooth Streaming hello. Дополнительные сведения см. в [этом разделе](media-services-deliver-content-overview.md#known-issues).

## <a id="apr_changes16"></a>Выпуск: апрель 2016 г.
### <a name="azure-media-analytics"></a>Аналитика мультимедиа Azure
В службах мультимедиа Azure появилась возможность аналитики мультимедиа для интеллектуальной работы с видео. Подробные сведения см. в статье [Общие сведения об аналитике служб мультимедиа Azure](media-services-analytics-overview.md).

### <a name="apple-fairplay-preview"></a>Apple FairPlay (предварительная версия)
Теперь вы toodynamically шифрования вашей HTTP Live Streaming (HLS) включает содержимого с помощью Apple FairPlay служб мультимедиа Azure. Можно также использовать AMS службы доставки лицензий toodeliver tooclients лицензии FairPlay. Дополнительные сведения см. в разделе [tooStream служб мультимедиа Azure используйте свой контент HLS защищена Apple FairPlay ](media-services-protect-hls-with-fairplay.md).

## <a id="feb_changes16"></a>Выпуск: февраль 2016 г.
Hello последнюю версию пакета SDK служб мультимедиа Azure для .NET (3.5.3) содержит Widevine связанные исправления ошибки. Hello проблема вызвана: AssetDeliveryPolicy не удалось повторно для нескольких средств, зашифрованных с Widevine. Как часть этого исправления ошибки hello следующие свойства добавлен toohello SDK: **WidevineBaseLicenseAcquisitionUrl**.

    Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
        new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
    {
        {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl,"http://testurl"},

    };

## <a id="jan_changes_16"></a>Выпуск: январь 2016 г.
Зарезервированные элементы кодирования переименовать tooreduce путаницы с именами кодировщика.

Hello Basic, Standard и Premium зарезервированные элементы кодирования являются переименованный tooS1, S2, и S3 зарезервированные единицы, соответственно.  Сегодня с помощью основных RUs кодирования клиенты видят S1 как hello метки на портале Azure (/ hello счета), при Standard и Premium увидите метки hello S2 и S3 соответственно. 

## <a id="dec_changes_15"></a>Выпуск: декабрь 2015 г.

### <a name="azure-media-encoder-deprecation-announcement"></a>Объявление о нерекомендуемой версии Azure Media Encoder

Начиная с примерно 12 месяцев после выпуска hello стандартный кодировщик мультимедиа будет считаться устаревшей Azure Media Encoder.

### <a name="azure-sdk-for-php"></a>Пакет SDK для Azure для PHP
Команда Hello Azure SDK публикации нового выпуска hello [пакет Azure SDK для PHP](http://github.com/Azure/azure-sdk-for-php) пакет, содержащий обновления и новые компоненты для службы мультимедиа Microsoft Azure. В частности, hello Azure Media Services SDK для PHP теперь поддерживает последние hello [Защита контента](media-services-content-protection-overview.md) функции: динамическое шифрование AES и управления цифровыми правами (PlayReady и Widevine) с и без ограничения токена. Кроме того, он поддерживает масштабирование [единиц кодирования](media-services-dotnet-encoding-units.md).

Дополнительные сведения можно найти в разделе 

* Hello [Microsoft Azure Media Services SDK для PHP](http://southworks.com/blog/2015/12/09/new-microsoft-azure-media-services-sdk-for-php-release-available-with-new-features-and-samples/) блога.
* следующие Hello [примеры кода](http://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices) toohelp приступить к работе:
  * **vodworkflow_aes.PHP**: это PHP-файла, который показывает, как toouse динамическое шифрование AES-128 и службы доставки ключей. Он основан на образце hello .NET, подробно описан [это](media-services-protect-with-aes128.md) статьи.
  * **vodworkflow_aes.PHP**: это PHP-файла, который показывает, как toouse динамическое шифрование PlayReady и службы доставки лицензий. Он основан на образце hello .NET, подробно описан [это](media-services-protect-with-drm.md) статьи.
  * **scale_encoding_units.PHP**: это файл PHP, показывающий, как кодирование tooscale зарезервированные единицы.

## <a id="nov_changes_15"></a>Выпуск: ноябрь 2015 г.
Службы мультимедиа Azure теперь предоставляет службы доставки лицензий Google Widevine в облаке hello. Дополнительные сведения см. в разделе слишком[этот блог объявления](https://azure.microsoft.com/blog/announcing-google-widevine-license-delivery-services-public-preview-in-azure-media-services/). См. также [это руководство](media-services-protect-with-drm.md) и [репозиторий GitHub](http://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm). 

Обратите внимание, что службами мультимедиа Azure предоставляется предварительная версия служб доставки лицензий Widevine. Дополнительные сведения см. в [этом блоге](https://azure.microsoft.com/blog/announcing-google-widevine-license-delivery-services-public-preview-in-azure-media-services/).

## <a id="oct_changes_15"></a>Выпуск: октябрь 2015 г.
Службы мультимедиа Azure (AMS) теперь в активном состоянии в hello, следуя центрах обработки данных: Южной Бразилии, Западная Индия, Южной Индии и центральной Индии. Теперь вы можете использовать портал Azure hello слишком[создавать учетные записи службы мультимедиа](media-services-portal-create-account.md) и выполнять различные задачи, описанные [здесь](https://azure.microsoft.com/documentation/services/media-services/). Но в этих центрах обработки данных не поддерживается Сервис Кодирования в реальном времени. Кроме того, в этих центрах обработки данных доступны не все типы зарезервированных единиц кодирования.

* Южная Бразилия: доступны зарезервированные единицы кодирования только категории "Стандартный" и "Базовый".
* Западная Индия, южная Индия и Центральная Индия: доступны зарезервированные единицы кодирования только категории "Базовый".

## <a id="september_changes_15"></a>Выпуск: сентябрь 2015 г.
* AMS теперь предлагает hello tooprotect возможности видео по запросу (VOD) и обновляющиеся потоки с технологией Widevine модульной DRM. Можно использовать следующие доставки служб партнеров toohelp доставки лицензии Widevine hello: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/). Дополнительную информацию см. в [этом блоге](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/).
  
    Можно использовать [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (начиная с версии hello 3.5.1) или REST API tooconfigure вашей AssetDeliveryConfiguration toouse Widevine.  
* AMS поддерживает видео в формате Apple ProRes. Теперь вы можете отправлять исходные видеофайлы в формате QuickTime, использующие Apple ProRes или другие кодеки. Дополнительную информацию см. в [этом блоге](https://azure.microsoft.com/blog/announcing-support-for-apple-prores-videos-in-azure-media-services/).
* Теперь можно использовать стандартный кодировщик мультимедиа toodo подзапроса Обрезка и динамическая извлечения архива. Дополнительную информацию см. в [этом блоге](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).
* были сделаны после фильтрации обновлений Hello: 
  
  * Теперь можно использовать формат Apple HTTP Live Streaming (HLS) с фильтром "только аудио". Это обновление позволяет отслеживать только tooremove, указав (только со звуком = false) в URL-АДРЕСЕ hello.
  * При определении фильтров для активов, теперь у вас есть возможность toocombine нескольких (вверх too3) фильтров в URL-адрес единого.
    
    Дополнительную информацию см. в [этом](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) блоге.
* AMS теперь поддерживает I-Frames в HLS версии 4. Поддержка I-Frames оптимизирует операции перемотки вперед и назад. По умолчанию все выходные каналы HLS версии 4 включают список воспроизведения I-Frames (EXT-X-I-FRAME-STREAM-INF).
  
    Дополнительную информацию см. в [этом](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) блоге.

## <a id="august_changes_15"></a>Выпуск от августа 2015 г.
* В настоящее время доступны пакет SDK служб мультимедиа Azure для выпуска Java версии 0.8.0 и новые примеры. Дополнительные сведения можно найти в разделе 
  
  * [Запись блога](http://southworks.com/blog/2015/08/25/microsoft-azure-media-services-sdk-for-java-v0-8-0-released-and-new-samples-available/)
  * [Репозиторий примеров для Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
* Обновление Проигрывателя мультимедиа Azure с поддержкой нескольких аудиопотоков. Дополнительные сведения можно найти в разделе 
  * [Запись блога](https://azure.microsoft.com/blog/2015/08/13/azure-media-player-update-with-multi-audio-stream-support/)

## <a id="july_changes_15"></a>Выпуск: июль 2015 г.
* Объявляет о hello выпуска Standard кодировщика мультимедиа. Дополнительные сведения см. в [этой записи блога](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/).
  
    В Media Encoder Standard используются предустановки, описанные в [этой](http://go.microsoft.com/fwlink/?LinkId=618336) статье. Обратите внимание, что при использовании стиля кодирует 4 КБ, вы должны получить hello **Premium** зарезервировано тип единицы измерения. Дополнительные сведения см. в разделе [как tooScale кодировка](media-services-scale-media-processing-overview.md).
* Интерактивные субтитры в режиме реального времени в службах мультимедиа Azure и проигрывателе. Дополнительные сведения см. в [этой записи блога](https://azure.microsoft.com/blog/2015/07/08/live-real-time-captions-with-azure-media-services-and-player/).

### <a name="media-services-net-sdk-updates"></a>Обновления пакета SDK служб мультимедиа для .NET
Пакет SDK служб мультимедиа Azure для .NET обновлен до версии 3.4.0.0. в этом выпуске были добавлены следующие функциональные возможности Hello:  

* Реализована поддержка динамического архива. При этом загружать ресурсы, содержащие динамические архивы, нельзя.
* Реализована поддержка динамических фильтров.
* Реализованные функциональные возможности, позволяющие контейнер хранилища tookeep пользователей при удалении активов.
* Исправления ошибок, связанные с политиками tooretry в каналах.
* Включен **рабочий процесс Media Encoder Premium**.

## <a id="june_changes_15"></a>Выпуск: июнь 2015 г.
### <a name="media-services-net-sdk-updates"></a>Обновления пакета SDK служб мультимедиа для .NET
Пакет SDK служб мультимедиа Azure для .NET обновлен до версии 3.3.0.0. в этом выпуске были добавлены следующие функциональные возможности Hello:  

* поддержка спецификации OpenId подключения обнаружения,
* поддержка обработки смены ключей на стороне поставщика удостоверений. 

При использовании поставщика удостоверений, который предоставляет документ обнаружения OpenID Connect (как hello выполните следующие поставщики: Azure Active Directory, Google, Salesforce), можно настроить ключи для проверки маркера JWT из подписи tooobtain служб мультимедиа Azure OpenID подключения spec обнаружения. 

Дополнительные сведения см. в разделе [с помощью Json Web ключей из характеристик обнаружения toowork OpenID Connect с помощью JWT токена проверки подлинности в службах мультимедиа Azure](http://gtrifonov.com/2015/06/07/using-json-web-keys-from-openid-connect-discovery-spec-to-work-with-jwt-token-authentication-in-azure-media-services/).

## <a id="may_changes_15"></a>Выпуск: май 2015 г.
Объявляет о hello следующие новые функции:

* [Предварительный просмотр кодирования в реальном времени с помощью служб мультимедиа](media-services-manage-live-encoder-enabled-channels.md)
* [Динамические манифесты](media-services-dynamic-manifest-overview.md)
* [Предварительный просмотр обработчика мультимедиа Azure Media Hyperlapse](https://azure.microsoft.com/blog/?p=286281&preview=1&_ppp=61e1a0b3db)

## <a id="april_changes_15"></a>Выпуск: апрель 2015 г.
### <a name="general-media-services-updates"></a>Общие обновления служб мультимедиа
* [Выход Проигрывателя мультимедиа Azure](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/).
* Начиная с 2.10 REST служб мультимедиа, каналы, настроенные tooingest протокола RTMP создаются с основной и дополнительный URL-адреса приема. Дополнительные сведения см. в разделе [Конфигурации входа (приема) канала](media-services-live-streaming-with-onprem-encoders.md#channel_input).
* Обновления индексатора мультимедийных данных Azure
* Поддержка испанского языка
* Формат xml новой конфигурации

Дополнительные сведения см. в [этом блоге](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/).

### <a name="media-services-net-sdk-updates"></a>Обновления пакета SDK служб мультимедиа для .NET
Пакет SDK служб мультимедиа Azure для .NET обновлен до версии 3.2.0.0.

Hello ниже приведены некоторые из клиентов hello обновлений:

* **Критическое изменение**: изменить **TokenRestrictionTemplate.Issuer** и **TokenRestrictionTemplate.Audience** toobe относится к типу string.
* Обновления, связанные с toocreating собственных политик повторов.
* Исправления ошибок, связанных с toouploading или загрузке файлов.
* Hello **MediaServicesCredentials** класс теперь принимает tooauthenticate конечной точки управления первичного и вторичного доступа к.

## <a id="march_changes_15"></a>Выпуск: март 2015 г.
### <a name="general-media-services-updates"></a>Общие обновления служб мультимедиа
* Теперь службы мультимедиа обеспечивают интеграцию Azure CDN. toosupport hello интеграции, hello **CdnEnabled** свойство было добавлено слишком**конечной точки потоковой передачи**.  **CdnEnabled** можно использовать с REST API, начиная с версии 2.9 (дополнительные сведения см. в статье [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)).  **CdnEnabled** можно использовать с пакетом SDK для .NET, начиная с версии 3.1.0.2 (дополнительные сведения см. в статье [StreamingEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.istreamingendpoint\(v=azure.10\).aspx)).
* Объявление о **рабочем процессе Premium обработчика мультимедиа**. Дополнительные сведения см. в статье [Знакомство со Службой кодирования категории "Премиум" в службах мультимедиа Azure](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/).

## <a id="february_changes_15"></a>Выпуск: февраль 2015 года.
### <a name="general-media-services-updates"></a>Общие обновления служб мультимедиа
API REST служб мультимедиа обновлены до версии 2.9. Начиная с этой версии можно включить hello интеграцию сети доставки Содержимого Azure с помощью конечных точек потоковой передачи. Дополнительные сведения см. в статье [StreamingEndpoint](https://msdn.microsoft.com/library/dn783468.aspx).

## <a id="january_changes_15"></a>Выпуск: январь 2015 г.
### <a name="general-media-services-updates"></a>Общие обновления служб мультимедиа
Объявления о поддержке защиты содержимого с помощью динамического шифрования в общедоступной версии. Дополнительные сведения см. в статье [Azure Media Services enhances streaming security with General Availability of DRM technology](https://azure.microsoft.com/blog/2015/01/29/azure-media-services-enhances-streaming-security-with-general-availability-of-drm-technology/) (Потоковая передача в службах мультимедиа Azure стала еще безопаснее благодаря поддержке технологии DRM в общедоступной версии).

### <a name="media-services-net-sdk-updates"></a>Обновления пакета SDK служб мультимедиа для .NET
Вышла версия 3.1.0.1 пакета SDK служб мультимедиа Azure для .NET.

Этот выпуск помечен как конструктор Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization.TokenRestrictionTemplate по умолчанию hello как устаревшие. новый конструктор Hello TokenType принимает в качестве аргумента.

    TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);


## <a id="december_changes_14"></a>Выпуск: декабрь 2014 г.
### <a name="general-media-services-updates"></a>Общие обновления служб мультимедиа
* Обработчик мультимедиа индексатора Azure toohello добавлены некоторые обновления и новые компоненты. Дополнительные сведения см. в разделе [Azure Media Indexer Version 1.1.6.7 Release Notes](https://azure.microsoft.com/blog/2014/12/03/azure-media-indexer-version-1-1-6-7-release-notes/) (Заметки о выпуске Azure Media Indexer версии 1.1.6.7).
* Добавлен новый API REST, обеспечивающий tooupdate зарезервированные единицы кодирования: [EncodingReservedUnitType с ОСТАЛЬНОЙ](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype).
* Добавлена поддержка CORS для службы доставки ключей.
* Повышена производительность параметров политики запроса авторизации.
* В китайском центре обработки данных, hello [URL-адрес доставки ключей](https://docs.microsoft.com/rest/api/media/operations/contentkey#get_delivery_service_url) теперь выдается каждому клиенту (как в других центрах обработки данных).
* Добавлено автоматическое назначение длительности HLS. При динамической потоковой передаче HLS всегда упаковывается динамически. По умолчанию службы мультимедиа автоматически вычисляют коэффициент упаковки сегментов HLS (FragmentsPerSegment) в зависимости от hello опорный кадр tooas интервал (KeyFrameInterval), называются группой изображений — GOP, получаемой из динамического кодировщика hello. Дополнительные сведения см. в статье [Общие сведения о динамической потоковой передаче с использованием служб мультимедиа Azure].

### <a name="media-services-net-sdk-updates"></a>Обновления пакета SDK служб мультимедиа для .NET
* [Пакет SDK служб мультимедиа Azure для .NET](http://www.nuget.org/packages/windowsazure.mediaservices/) обновлен до версии 3.1.0.0.
* Обновлены hello .net SDK too.NET зависимостей 4.5 Framework.
* Добавлен новый API, позволяющий tooupdate зарезервированные единицы кодирования. Дополнительные сведения см. в статье [Масштабирование кодирования с помощью пакета SDK для .NET](media-services-dotnet-encoding-units.md).
* Добавлена поддержка токена JWT (веб-токена JSON) для проверки подлинности токенов. Дополнительные сведения см. в статье [JWT token Authentication in Azure Media Services and Dynamic Encryption](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/) (Проверка подлинности токена JWT в службах мультимедиа Azure и динамическое шифрование).
* Добавлены относительные смещения для BeginDate и ExpirationDate в шаблон лицензии PlayReady hello.

## <a id="november_changes_14"></a>Выпуск: ноябрь 2014 г.
* Службы мультимедиа теперь позволяют tooingest динамической содержимое Smooth Streaming (FMP4) через SSL-подключение. tooingest по протоколу SSL, убедитесь, что hello tooupdate приема tooHTTPS URL-адрес.  Обратите внимание, что в настоящее время AMS не поддерживает SSL для личных доменов.  Дополнительные сведения о потоковой передаче в реальном времени см. в статье [Общие сведения о динамической потоковой передаче с использованием служб мультимедиа Azure].
* В настоящее время невозможно принять потоковую передачу RTMP по SSL-подключению.
* Может только передавать по протоколу SSL, если конечной точки, из которого доставки контента потоковой передачи hello была создана после 10 сентября 2014 г. Если URL-адресов потоковой передачи основаны на конечные точки, созданные после 10 сентября потоковой передачи hello, hello URL-адрес содержит «streaming.mediaservices.windows.net» (hello новый формат). Потоковой передачи URL-адреса, которые содержат «origin.mediaservices.windows.net» (hello старый формат) не поддерживают протокол SSL. Если URL-адрес находится в старом формате hello и по протоколу SSL, необходимо будет toostream toobe [создать новую конечную точку потоковой передачи](media-services-portal-manage-streaming-endpoints.md). Используйте URL-адреса создаются на основании hello новые потоковая передача конечной точки toostream контента по протоколу SSL.

## <a id="october_changes_14"></a>Выпуск: октябрь 2014 г.
### <a id="new_encoder_release"></a>Выпуск кодировщика служб мультимедиа
Объявляет о hello новым выпуском служб Media Services Azure Media Encoder. С hello последнюю Azure Media Encoder выставляется только за количество гигабайт выходных данных, но в противном случае нового кодировщика hello — компонент, совместимый с предыдущего кодировщика hello. Дополнительные сведения см. на странице [цен на службы мультимедиа].

### <a id="oct_sdk"></a>Пакет SDK служб мультимедиа для .NET
Пакет SDK служб мультимедиа для расширений .NET теперь имеет версию 2.0.0.3.

Пакет SDK служб мультимедиа для .NET теперь имеет версию 3.0.0.8.

были внесены следующие изменения Hello:

* Рефакторинг в классах политики повторов.
* Добавление заголовков запроса toohttp строку агента пользователя.
* Добавление шага восстановления сборки NuGet.
* Исправление cert toouse x509 сценарии тестов из репозитория.
* Проверка параметров при обновлении канала и точки потоковой передачи.

### <a name="new-github-repository-toohost-media-services-samples"></a>Новые образцы служб мультимедиа toohost репозитория GitHub
Примеры расположены в [репозитории примеров GitHub служб мультимедиа Azure](https://github.com/Azure/Azure-Media-Services-Samples).

## <a id="september_changes_14"></a>Выпуск: сентябрь 2014 г.
Метаданные REST служб мультимедиа теперь имеют версию 2.7. Дополнительные сведения о последних обновлениях REST hello см. в разделе [Справочник API REST служб мультимедиа Azure].

Пакет SDK служб мультимедиа для .NET теперь имеет версию 3.0.0.7.

### <a id="sept_14_breaking_changes"></a>Критические изменения
* **Источник** был переименован слишком[конечной точки потоковой передачи].
* Изменение в поведении по умолчанию hello при использовании hello **портал Azure** tooencode и публикации MP4-файлов.

Ранее, при использовании классического портала Azure toopublish hello ресурс видео MP4 однофайловых URL-адрес SAS будут создаваться (URL-адреса SAS позволяют toodownload hello видео из хранилища больших двоичных объектов). В настоящее время при использовании tooencode hello классический портал Azure и затем опубликовать ресурс один файл видео MP4, hello созданный URL-адрес точки tooan служб мультимедиа Azure конечной точки потоковой передачи.  Это изменение не влияет на видео MP4, которые непосредственно отправленного tooMedia служб и публикуются без кодирования службами мультимедиа Azure.

В настоящее время у вас hello следующая проблема hello toosolve двух параметров.

* Включить единицы потоковой передачи и использовать динамическую упаковку toostream hello .mp4 активов smooth потоковой передачи презентации.
* Создайте toodownload URL-адрес SAS (или постепенно воспроизвести) hello .mp4. Дополнительные сведения о том, как toocreate указатель SAS в разделе [доставки содержимого].

### <a id="sept_14_GA_changes"></a>Новые функции и сценарии, включенные в общедоступный выпуск
* **Indexer Media Processor.** Дополнительные сведения см. в статье [Индексирование файлов мультимедиа с помощью Azure Media Indexer].
* Hello [конечной точки потоковой передачи] сущности теперь позволяет tooadd имена пользовательских доменов (узла).
  
    Toobe имя пользовательского домена, используется в качестве имени конечной точки потоковой передачи служб мультимедиа hello необходимо tooadd пользовательское основное приложение имена tooyour конечной точки потоковой передачи. Используйте hello API REST служб мультимедиа или пакет SDK для .NET tooadd пользовательских имен узлов.
  
    применить Hello следующие вопросы:
  
  * Необходимо быть владельцем hello hello пользовательское имя домена.
  * службы мультимедиа Azure должны быть проверены Hello владения hello доменное имя. toovalidate hello домена, создайте запись CName, которая сопоставляет <MediaServicesAccountId>.<parent domain> tooverifydns. < mediaservices-dns-zone >. 
  * Необходимо создать другой CName, которая сопоставляет имя узла hello пользовательское основное приложение имя (например, sports.contoso.com) tooyour Media Services StreamingEndpont элемента (например, amstest.streaming.mediaservices.windows.net).

    Дополнительные сведения см. в разделе hello **CustomHostNames** свойство в hello [конечной точки потоковой передачи] раздела.

### <a id="sept_14_preview_changes"></a>Новые функции и сценарии, являющихся частью выпуска общедоступной предварительной версии hello
* Предварительный просмотр потоковой передачи в реальном времени. Дополнительные сведения см. в статье [Общие сведения о динамической потоковой передаче с использованием служб мультимедиа Azure].
* Служба доставки ключей. Дополнительные сведения см. в статье [Использование динамического шифрования AES-128 и службы доставки ключей].
* Динамическое шифрование на основе AES. Дополнительные сведения см. в статье [Использование динамического шифрования AES-128 и службы доставки ключей].
* Служба доставки лицензий PlayReady. Дополнительные сведения см. в статье [Использование общего динамического шифрования PlayReady и (или) Widevine DRM].
* Динамическое шифрование на основе PlayReady. Дополнительные сведения см. в статье [Использование общего динамического шифрования PlayReady и (или) Widevine DRM].
* Шаблон лицензии PlayReady для служб мультимедиа. Дополнительные сведения см. в статье [Обзор шаблонов лицензий PlayReady служб мультимедиа].
* Потоковая передача зашифрованных активов хранилища. Дополнительные сведения см. в статье [Настройка политик доставки ресурсов-контейнеров с помощью пакета SDK для .NET].

## <a id="august_changes_14"></a>Выпуск: август 2014 г.
При кодировании актива выходной актив производится после завершения задания кодирования hello. До этого выпуска кодировщик служб мультимедиа Azure создавал метаданные о выходных активах. Начиная с этого выпуска hello кодировщика также формирует метаданные о входных ресурсах. Дополнительные сведения см. в разделе hello [метаданные входных данных] и [выходные метаданные] разделы.

## <a id="july_changes_14"></a>Выпуск: июль 2014 г.
После исправления ошибок Hello были внесены для hello Azure Media Services Packager и шифратора:

* Только звук воспроизводится при мультиплексирование tooHTTP активов динамического архива Live Streaming — эта проблема была исправлена, и теперь воспроизводить аудио и видео.
* При упаковке tooHTTP активов Live Streaming и AES 128-разрядное шифрование конверта, hello упакованные потоки воспроизводятся на устройствах Android — это ошибка исправлена и hello упакованные потоки воспроизводятся на устройствах, поддерживающих HTTP Live Streaming.

## <a id="may_changes_14"></a>Выпуск: май 2014 г.
### <a id="may_14_changes"></a>Общие обновления служб мультимедиа
Теперь вы можете использовать [динамической упаковки] toostream HTTP Live Streaming (HLS) v3. toostream HLS v3, добавить следующий путь указателя источника toohello формат hello: * .ism/manifest(format=m3u8-aapl-v3). Дополнительные сведения см. в [блоге Ника Дроуина (Nick Drouin)].

Динамическая упаковка теперь также поддерживает доставку потоков HLS (v3 и v4), зашифрованных с помощью PlayReady на основе Smooth Streaming со статическим шифрованием с использованием PlayReady. Дополнительные сведения о разделе Smooth Streaming с PlayReady, tooencrypt [защита потоков Smooth Stream с помощью PlayReady].

### <a name="may_14_donnet_changes"></a>Обновления пакета SDK служб мультимедиа для .NET
hello выпуска пакета SDK .NET служб мультимедиа 3.0.0.5 содержит включает Hello следующие усовершенствования:

* Увеличена скорость и отказоустойчивость передачи и загрузки активов мультимедиа.
* Улучшена логика повторных попыток и обработка временных исключений. 
  
  * Улучшены обнаружение временных ошибок и логика повторных попыток для исключений при отправке запросов, сохранении изменений, отправке и загрузке файлов. 
  * При получении исключений веб-приложений (например, во время запроса маркера ACS) неустранимые ошибки теперь обрабатываются быстрее.

Дополнительные сведения см. в разделе [логика повторных попыток в hello пакета SDK служб мультимедиа для .NET].

## <a id="april_changes_14"></a>Выпуск кодировщика: апрель 2014 г.
### <a name="april_14_enocer_changes"></a>Обновления кодировщика служб мультимедиа
* Добавлена поддержка приема AVI-файлов создаются с использованием редактора нелинейный Grass Valley EDIUS hello, где hello видео в незначительной степени сжимаются с использованием кодека Grass Valley HQ/HQX. Дополнительные сведения см. в разделе [Grass Valley объявляет о выпуске EDIUS 7 Streaming через hello облака].
* Добавлена возможность задать соглашение об именовании hello hello файлы, созданные hello Media Encoder. Дополнительные сведения см. в статье [Управление именами выходных файлов кодировщика служб мультимедиа].
* Добавлена поддержка наложения видео- и/или аудиоданных. Дополнительные сведения см. в статье [Создание наложений].
* Добавлена поддержка стыковки нескольких сегментов видео. Дополнительные сведения см. в статье [Стыковка сегментов видео].
* Исправлена ошибка, связанная tootranscoding из MP4-файлов, где hello звук был закодирован с MPEG-1 Audio layer 3 (также называемого MP3).

## <a id="jan_feb_changes_14"></a>Выпуски: январь — февраль 2014 г.
### <a name="jan_fab_14_donnet_changes"></a>Пакет SDK служб мультимедиа Azure для .NET 3.0.0.1, 3.0.0.2 и 3.0.0.3
изменения Hello в версиях 3.0.0.1 и 3.0.0.2 включают:

* Исправлены проблемы, связанные с toousage запросов LINQ с операторами OrderBy.
* Тестовые решения в [GitHub] разделены на тесты на основе единиц и тесты на основе сценариев.

Дополнительные сведения об изменениях hello см. в разделе: [освобождает Azure Media Services SDK для .NET 3.0.0.1 и 3.0.0.2].

в выпуске 3.0.0.3 произошли Hello следующие изменения:

* Обновить версию toouse зависимости хранилища Azure 3.0.3.0. 
* Исправлена проблема совместимости с предыдущими выпусками 3.0.*.* . 

## <a id="december_changes_13"></a>Выпуск: декабрь 2013 г.
### <a name="dec_13_donnet_changes"></a>Выпуск 3.0.0.0 пакета SDK служб мультимедиа Azure для .NET
> [!NOTE]
> Версии 3.0.x.x несовместимы с версиями 2.4.x.x.
> 
> 

последнюю версию пакета SDK служб мультимедиа hello Hello сейчас 3.0.0.0. Можно загрузить последнюю версию пакета hello Nuget или получить hello биты в [GitHub].

Начиная с пакета SDK служб мультимедиа версии 3.0.0.0 hello, можно повторно использовать hello [Azure Active Directory Access управления Service (ACS)] маркеры. Дополнительные сведения см. в разделе hello «повторное использование токенов службы контроля доступа» раздела hello [подключения служб tooMedia с hello пакета SDK служб мультимедиа для .NET] раздела.

### <a name="dec_13_donnet_ext_changes"></a>Расширения версии 2.0.0.0 пакета SDK служб мультимедиа Azure для .NET
Hello расширения SDK .NET служб мультимедиа Azure — это набор методов и вспомогательных функций, которые позволяют упростить код и сделать проще toodevelop со службами мультимедиа Azure. Вы можете получить последнюю биты hello из [расширения SDK .NET служб мультимедиа Azure].

## <a id="november_changes_13"></a>Выпуск: ноябрь 2013 г.
### <a name="nov_13_donnet_changes"></a>Изменения в пакете SDK служб мультимедиа Azure для .NET
Начиная с этой версией hello пакета SDK служб мультимедиа для .NET обрабатывает временные сбои, которые могут возникнуть при выполнении вызовов toohello API REST служб мультимедиа слоя.

## <a id="august_changes_13"></a>Выпуск: август 2013 г.
### <a name="aug_13_powershell_changes"></a>Командлеты PowerShell служб мультимедиа включены в инструменты SDK Azure
Привет, следующие командлеты PowerShell для служб мультимедиа теперь включены в [azure-sdk-tools].

* Get-AzureMediaServices 
  
    Пример: `Get-AzureMediaServicesAccount`.
* New-AzureMediaServicesAccount 
  
    Пример: `New-AzureMediaServicesAccount -Name “MediaAccountName” -Location “Region” -StorageAccountName “StorageAccountName”`.
* New-AzureMediaServicesKey 
  
    Пример: `New-AzureMediaServicesKey -Name “MediaAccountName” -KeyType Secondary -Force`.
* Remove-AzureMediaServicesAccount 
  
    Пример: `Remove-AzureMediaServicesAccount -Name “MediaAccountName” -Force`.

## <a id="june_changes_13"></a>Выпуск: июнь 2013 г.
### <a name="june_13_general_changes"></a>Изменения в службах мультимедиа Azure
изменения Hello, упомянутые в этом разделе, обновления, включенные в приветствия освобождает служб мультимедиа июня 2013 г.

* Возможность toolink несколько учетных записей хранения tooa учетную запись служб мультимедиа. 
  
    StorageAccount
  
    Asset.StorageAccountName и Asset.StorageAccount
* Возможность tooupdate Job.Priority. 
* Сущности и свойства, связанные с уведомлением: 
  
    JobNotificationSubscription
  
    NotificationEndPoint
  
    Задание
* Asset.Uri 
* Locator.Name 

### <a name="june_13_dotnet_changes"></a>Изменения в пакете SDK служб мультимедиа Azure для .NET
Hello включены следующие изменения в июне 2013 г. выпусках пакета SDK служб мультимедиа. Hello последнюю пакета SDK служб мультимедиа можно найти в GitHub.

* Начиная с версии hello 2.3.0.0, пакет SDK служб мультимедиа поддерживает связывание нескольких tooa учетных записей хранилища учетной записи служб мультимедиа hello. Hello следующие API-интерфейсы поддерживают эту функцию:
  
    Здравствуйте, IStorageAccount типа.
  
    Здравствуйте, свойство Microsoft.WindowsAzure.MediaServices.Client.CloudMediaContext.StorageAccounts.
  
    Здравствуйте, свойство StorageAccount.
  
    Здравствуйте, StorageAccountName свойство.
  
    Дополнительные сведения см. в статье [Управление активами служб мультимедиа в нескольких учетных записях хранения].
* API-интерфейсы, связанные с уведомлениями. Начиная с версии hello 2.2.0.0, у вас есть хранилища hello возможности toolisten tooAzure очереди уведомлений. Дополнительные сведения см. в статье [Обработка уведомлений из заданий служб мультимедиа].
  
    Здравствуйте, свойство Microsoft.WindowsAzure.MediaServices.Client.IJob.JobNotificationSubscriptions.
  
    Здравствуйте, Microsoft.WindowsAzure.MediaServices.Client.INotificationEndPoint типа.
  
    Здравствуйте, Microsoft.WindowsAzure.MediaServices.Client.IJobNotificationSubscription типа.
  
    Здравствуйте, Microsoft.WindowsAzure.MediaServices.Client.NotificationEndPointCollection типа.
  
    Здравствуйте, Microsoft.WindowsAzure.MediaServices.Client.NotificationEndPointType типа.
  
    Здравствуйте, Microsoft.WindowsAzure.MediaServices.Client.NotificationJobState типа.
* Зависимость от hello хранилища клиента Azure SDK 2.0 (Microsoft.WindowsAzure.StorageClient.dll).
* Зависимость от OData 5.5 (Microsoft.Data.OData.dll).

## <a id="december_changes_12"></a>Выпуск: декабрь 2012 г.
### <a name="dec_12_dotnet_changes"></a>Изменения в пакете SDK служб мультимедиа Azure для .NET
* Intellisense. Добавлена отсутствующая документация Intellisense по многим типам.
* Microsoft.Practices.TransientFaultHandling.Core: Исправлена проблема, где hello SDK по-прежнему зависел tooan зависимостей, старую версию этой сборки. Hello SDK теперь ссылки с версией 5.1.1209.1 этой сборки.

Исправления для проблем, обнаруженных в hello ноябрь 2012 г. пакета SDK:

* IAsset.Locators.Count. Теперь этот счетчик правильно показывает данные по новым интерфейсам IAsset после удаления всех локаторов.
* IAssetFile.ContentFileSize. Теперь это значение устанавливается правильно после отправки из IAssetFile.Upload(путь к файлу).
* IAssetFile.ContentFileSize. Теперь это свойство можно задать при создании файла актива. Ранее оно было доступно только для чтения.
* IAssetFile.Upload(filepath): Исправлена проблема, где данный метод асинхронной передачи порождал hello следующая ошибка при передаче нескольких активов toohello файлов. Ошибка Hello: «серверу не удалось tooauthenticate hello запроса. Убедитесь, что значение заголовка авторизации hello имеет правильный формат, включая подпись hello.»
* IAssetFile.UploadAsync. Исправлена проблема, при которой не удавалось одновременно отправить более 5 файлов.
* IAssetFile.UploadProgressChanged: Это событие теперь предоставляется посредством hello SDK.
* IAssetFile.DownloadAsync(string, BlobTransferClient, ILocator, CancellationToken). Теперь предоставляется перезагрузка этого метода.
* IAssetFile.UploadAsync. Исправлена проблема, при которой не удавалось одновременно загрузить более 5 файлов.
* IAssetFile.Delete(): Исправлена проблема, где вызове метода delete может привести к исключению, если файл не был загружен для hello IAssetFile.
* Задания: Устранена проблема, где цепочки «MP4 tooSmooth потоки задача» с «PlayReady Protection Task» с помощью шаблона задания не создаст все задачи вообще.
* EncryptionUtils.GetCertificateFromStore(): Этот метод больше не вызывает исключения NullReferenceException из-за ошибок tooa при поиске сертификата hello, основанного на конфигурации проблемы с сертификатом.

## <a id="november_changes_12"></a>Выпуск: ноябрь 2012 г
Hello изменения, описанные в этом разделе были обновления, включенные в hello ноябрь 2012 г. (версия 2.0.0.0) SDK. Эти изменения могут потребовать любой код, написанный для hello июнь 2012 г. Предварительная версия пакета SDK для выпуска toobe изменен или переписать.

* Активы
  
    IAsset.Create(assetName) является функции создания активов только hello. IAsset.Create больше не передает файлы в процессе вызова метода hello. Для отправки используйте функцию IAssetFile.
  
    метод IAsset.Publish Hello и значение перечисления AssetState.Publish hello были удалены из пакета SDK служб hello. Необходимо переработать код, связанный с этим значением.
* FileInfo
  
    Этот класс удален и заменен классом IAssetFile.
  
    IAssetFiles
  
    IAssetFile заменяет класс FileInfo и используется иначе. toouse, создать экземпляр объекта IAssetFiles hello, а затем передать файл либо с помощью hello пакета SDK служб мультимедиа или hello пакет SDK хранилища Azure. можно использовать следующие перегрузки IAssetFile.Upload Hello.
  
  * IAssetFile.Upload(filePath): Синхронный метод, который блокирует поток hello и рекомендуется только при передаче одного файла.
  * IAssetFile.UploadAsync(filePath, blobTransferClient, locator, cancellationToken). Асинхронный метод. Это hello предпочтительный механизм передачи. 
    
    Известная ошибка: с помощью hello cancellationToken действительно отменит hello передачи; Тем не менее состояние отмены hello hello задач может быть любое число состояний. Необходимо правильно перехватывать и обрабатывать исключения.
* Локаторы
  
    Hello исходной версии были удалены. Hello SAS определенного контекста. Locators.CreateSasLocator (asset, accessPolicy) будет помечена устаревший или удален с общедоступной. Указатели hello в разделе "раздела" новые функциональные возможности для обновленного действия.

## <a id="june_changes_12"></a>Предварительный выпуск: июнь 2012 г.
следующие функции Hello впервые появился в ноябрьском выпуске пакета SDK для hello hello.

* Удаление сущностей
  
    Объекты IAsset, IAssetFile, ILocator, IAccessPolicy и IContentKey объекты теперь удаляются на уровне объекта hello, т. е. с помощью IObject.Delete(), а не требуют удаления hello коллекция, в которой находится с помощью cloudMediaContext.ObjCollection.Delete(objInstance).
* Локаторы
  
    Указатели, должен быть создан с помощью метода CreateLocator hello и использовать значения перечисления LocatorType.SAS или LocatorType.OnDemandOrigin hello в качестве аргумента для определенного типа указателя hello требуется toocreate.
  
    Были добавлены новые свойства tooLocators toomake его проще tooobtain пригодных URI для содержимого. Изменение указателей был предназначен tooprovide большую гибкость для будущего расширения сторонних разработчиков и повышения удобства использования мультимедийных клиентских приложений.
* Поддержка асинхронных методов
  
    Асинхронные была добавлена поддержка tooall методы.

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

<!-- Anchors. -->

<!-- Images. -->

<!--- URLs. --->
[форум MSDN по службам мультимедиа Azure]: http://social.msdn.microsoft.com/forums/azure/home?forum=MediaServices
[Справочник API REST служб мультимедиа Azure]: https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference
[цен на службы мультимедиа]: http://azure.microsoft.com/pricing/details/media-services/
[метаданные входных данных]: http://msdn.microsoft.com/library/azure/dn783120.aspx
[выходные метаданные]: http://msdn.microsoft.com/library/azure/dn783217.aspx
[доставки содержимого]: http://msdn.microsoft.com/library/azure/hh973618.aspx
[Индексирование файлов мультимедиа с помощью Azure Media Indexer]: http://msdn.microsoft.com/library/azure/dn783455.aspx
[конечной точки потоковой передачи]: http://msdn.microsoft.com/library/azure/dn783468.aspx
[Общие сведения о динамической потоковой передаче с использованием служб мультимедиа Azure]: http://msdn.microsoft.com/library/azure/dn783466.aspx
[Использование динамического шифрования AES-128 и службы доставки ключей]: http://msdn.microsoft.com/library/azure/dn783457.aspx
[Использование общего динамического шифрования PlayReady и (или) Widevine DRM]: http://msdn.microsoft.com/library/azure/dn783467.aspx
[Preview features]: http://azure.microsoft.com/services/preview/
[Обзор шаблонов лицензий PlayReady служб мультимедиа]: http://msdn.microsoft.com/library/azure/dn783459.aspx
[Настройка политик доставки ресурсов-контейнеров с помощью пакета SDK для .NET]: http://msdn.microsoft.com/library/azure/dn783451.aspx
[Azure portal]: https://manage.windowsazure.com
[динамической упаковки]: http://msdn.microsoft.com/library/azure/jj889436.aspx
[блоге Ника Дроуина (Nick Drouin)]: http://blog-ndrouin.azurewebsites.net/hls-v3-new-old-thing/
[защита потоков Smooth Stream с помощью PlayReady]: http://msdn.microsoft.com/library/azure/dn189154.aspx
[логика повторных попыток в hello пакета SDK служб мультимедиа для .NET]: http://msdn.microsoft.com/library/azure/dn745650.aspx
[Grass Valley объявляет о выпуске EDIUS 7 Streaming через hello облака]: http://www.streamingmedia.com/Producer/Articles/ReadArticle.aspx?ArticleID=96351&utm_source=dlvr.it&utm_medium=twitter
[Управление именами выходных файлов кодировщика служб мультимедиа]: http://msdn.microsoft.com/library/azure/dn303341.aspx
[Создание наложений]: http://msdn.microsoft.com/library/azure/dn640496.aspx
[Стыковка сегментов видео]: http://msdn.microsoft.com/library/azure/dn640504.aspx
[освобождает Azure Media Services SDK для .NET 3.0.0.1 и 3.0.0.2]: http://www.gtrifonov.com/2014/02/07/windows-azure-media-services-.net-sdk-3.0.0.2-release/
[Azure Active Directory Access управления Service (ACS)]: http://msdn.microsoft.com/library/hh147631.aspx
[подключения служб tooMedia с hello пакета SDK служб мультимедиа для .NET]: http://msdn.microsoft.com/library/azure/jj129571.aspx
[расширения SDK .NET служб мультимедиа Azure]: https://github.com/Azure/azure-sdk-for-media-services-extensions/tree/dev
[azure-sdk-tools]: https://github.com/Azure/azure-sdk-tools
[GitHub]: https://github.com/Azure/azure-sdk-for-media-services
[Управление активами служб мультимедиа в нескольких учетных записях хранения]: http://msdn.microsoft.com/library/azure/dn271889.aspx
[Обработка уведомлений из заданий служб мультимедиа]: http://msdn.microsoft.com/library/azure/dn261241.aspx

