---
title: "aaaDelivering содержимого toocustomers | Документы Microsoft"
description: "В этой статье представлен обзор доставки содержимого с помощью служб мультимедиа Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 89ede54a-6a9c-4814-9858-dcfbb5f4fed5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 0570bd62d9d42633df0132f9449b357e2abb4086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deliver-content-toocustomers"></a>Доставка содержимого toocustomers
Когда доставка потоковой передачи или видео по запросу содержимого toocustomers, ваша цель состоит в toodeliver устройств toovarious видео высокого качества условиях другую сеть.

tooachieve этой цели вы можете:

* Кодирование поток tooa потокового видео многоскоростной (адаптивный битрейт). Это позволит соблюдать различные уровни качества и условия сети.
* Использование служб мультимедиа Microsoft Azure [динамической упаковки](media-services-dynamic-packaging-overview.md) toodynamically повторно упаковать потока в различных протоколов. Это позволит транслировать поток на разных устройствах. Службы мультимедиа поддерживают доставку hello следующие технологии потоковой передачи с адаптивной скоростью: HTTP Live Streaming (HLS), Smooth Streaming и MPEG-DASH.

>[!NOTE]
>При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния. Потоковая передача вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования toostart hello конечной точки потоковой передачи, из которого нужно имеет содержимое toostream toobe в hello **под управлением** состояния. 

В этой статье приводится обзор важных понятий, связанных с доставкой содержимого.

Известные проблемы, toocheck в разделе [известные проблемы](media-services-deliver-content-overview.md#known-issues).

## <a name="dynamic-packaging"></a>Динамическая упаковка
При использовании динамической упаковки hello, Media Services предоставляет, можно доставлять контент MP4 или Smooth Streaming закодированный с адаптивной скоростью в потоковом форматы, поддерживаемые службами мультимедиа (MPEG-DASH, HLS, Smooth Streaming) без необходимости toore пакета в Эти форматы потоковой передачи. Мы рекомендуем доставлять содержимое с помощью динамической упаковки.

tootake преимущества динамической упаковки необходимо tooencode мезонинный (источник) в набор файлов MP4 с адаптивной скоростью или файлов Smooth Streaming с адаптивной скоростью.

При использовании динамической упаковки можно хранить и платить за файлы hello в едином формате хранения. Службы мультимедиа будут создавать и обслуживать соответствующий ответ hello на ваших запросов на основе.

Динамическая упаковка доступна для конечных точек потоковой передачи уровня "Стандартный" и "Премиум". 

Чтобы узнать больше, ознакомьтесь со [Dynamic packaging](media-services-dynamic-packaging-overview.md).

## <a name="filters-and-dynamic-manifests"></a>Фильтры и динамические манифесты
Службы мультимедиа позволяют определять фильтры для ресурсов-контейнеров. Эти фильтры являются серверных правил, которые помогут вашим клиентам, например, воспроизведение видео определенного раздела или указать подмножество аудио и видео представлений, которые могут обрабатывать устройства клиента (а не всех hello представлений, связанные с активом hello ). Такая фильтрация достигается за счет *динамического манифесты* создаются, когда клиент запрашивает toostream видео на основе одного или нескольких указанных фильтров.

Чтобы узнать больше, ознакомьтесь со [Фильтры и динамические манифесты](media-services-dynamic-manifest-overview.md).

## <a name="locators"></a>Локаторы
tooprovide пользователя с URL-адресом, который можно использовать toostream или загрузить содержимое, необходимо сначала toopublish актива путем создания локатора. Указатель предоставляет hello tooaccess точки входа файлам, содержащимся в активе. Службы мультимедиа поддерживают два типа указателей:

* Указатели OnDemandOrigin. Это используется toostream мультимедиа (например, MPEG-DASH, HLS или Smooth Streaming), или постепенно загружать файлы.
* Указатели подписанного URL-адреса (SAS). Это используется toodownload файлы мультимедиа tooyour локального компьютера.

*Доступ к политике* — используется toodefine hello разрешения (например, чтение, запись и список) и длительность, для которой клиент имеет доступ для конкретного средства. Обратите внимание, что разрешение hello списка (AccessPermissions.List) не должен использоваться при создании указателя OrDemandOrigin.

Указатели имеют срок действия. портал Azure Hello задает дату окончания срока действия 100 лет в hello будущих для указателей.

> [!NOTE]
> При использовании hello Azure портала toocreate указатели до марта 2015 этих указателей заданы tooexpire после двух лет.
> 
> 

tooupdate дату окончания срока действия на указатель, используйте [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) или [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API-интерфейсы. Обратите внимание, что при обновлении срок действия локатора SAS hello hello URL-адрес изменяется.

Указатели не предназначены для управления доступом на уровне пользователя toomanage. Пользователи с правами tooindividual различный уровень доступа можно предоставить с помощью решения управления цифровыми правами (DRM). Дополнительные сведения см. в разделе [Службы мультимедиа — потоковая передача по запросу](http://msdn.microsoft.com/library/azure/dn282272.aspx).

При создании указателя может быть 30-секундная задержка из-за toorequired хранения и распространения процессов в хранилище Azure.

## <a name="adaptive-streaming"></a>Адаптивная потоковая передача
Адаптивные технологии битрейта позволяют приложениям видеопроигрыватель toodetermine состояния сети и выберите из нескольких битрейтов. Когда снизилась сетевого взаимодействия, hello клиент может выбрать более низкий битрейт, чтобы воспроизведение можно продолжить работу с более низкое качество видео. Как повысить условий сети, hello клиент может переключиться tooa высокий битрейт с высоким качеством видео. Службы мультимедиа Azure поддерживают hello следующие адаптивные технологии битрейта: HTTP Live Streaming (HLS), Smooth Streaming и MPEG-DASH.

tooprovide пользователей с потоковой передачи URL-адреса, сначала необходимо создать указатель OnDemandOrigin. Создание локатора дает hello активов toohello базовый путь, содержащий содержимое hello hello требуется toostream. Тем не менее могут toostream toobe этот контент, необходимо toomodify этот путь. полный URL-адрес toohello файла манифеста потоковой передачи, необходимо СЦЕПИТЬ путь локатора hello tooconstruct значение и hello манифеста (filename.ism) имя файла. Затем добавьте **/Manifest** и путь локатора toohello соответствующий формат (при необходимости).

> [!NOTE]
> Также по SSL-подключению можно выполнять потоковую передачу содержимого. toodo это, убедитесь, что потоковой передачи запуска URL-адреса с помощью протокола HTTPS. Обратите внимание, что в настоящее время AMS не поддерживает SSL для личных доменов.  
> 


Может только передавать по протоколу SSL, если конечной точки, из которого доставки контента потоковой передачи hello была создана после 10 сентября 2014 г. Если URL-адресов потоковой передачи основаны на конечные точки, созданные после десятой сентябрь 2014 г., потоковой передачи hello hello URL-адрес содержит «streaming.mediaservices.windows.net». Потоковой передачи URL-адреса, которые содержат «origin.mediaservices.windows.net» (hello старый формат) не поддерживают протокол SSL. Если URL-адрес находится в старом формате hello и необходимо будет toostream toobe по протоколу SSL, создайте новую конечную точку потоковой передачи. Использование URL-адреса на основе новых потоковой передачи конечной точки toostream hello контента по протоколу SSL.

## <a name="streaming-url-formats"></a>Форматы URL-адресов потоковой передачи
### <a name="mpeg-dash-format"></a>Формат MPEG-DASH
{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest(format=mpd-time-csf)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf)

### <a name="apple-http-live-streaming-hls-v4-format"></a>Формат Apple HTTP Live Streaming (HLS) V4
{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest(format=m3u8-aapl)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl)

### <a name="apple-http-live-streaming-hls-v3-format"></a>Формат Apple HTTP Live Streaming (HLS) V3
{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest(format=m3u8-aapl-v3)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3)

### <a name="apple-http-live-streaming-hls-format-with-audio-only-filter"></a>Формат Apple HTTP Live Streaming (HLS) с фильтром "только аудио"
По умолчанию только со звуком отслеживает включаются в манифест HLS приветствия. Это требуется для сертификации магазина Apple для сетей мобильной связи. Таким образом Если клиент не имеет достаточную пропускную способность или подключен через подключение 2G, воспроизведение переключает только для tooaudio. Это помогает tookeep содержимого потоковой передачи без буферизации, но отсутствует изображение отсутствует. В некоторых сценариях буферизация проигрывателя может быть предпочтительнее воспроизведения лишь аудио дорожки. Отслеживание только со звуком hello tooremove добавить **только со звуком = false** toohello URL-адрес.

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3,audio-only=false)

Дополнительные сведения см. в записи блога [Azure Media Services – Dynamic Manifest Composition support and HLS output additional features](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) (Службы мультимедиа Azure — поддержка динамического создания манифестов и дополнительные функции вывода HLS).

### <a name="smooth-streaming-format"></a>Формат Smooth Streaming
{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest

Пример:

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest

### <a id="fmp4_v20"></a>Манифест Smooth Streaming 2.0 (манифест прежних версий)
По умолчанию формат манифеста Smooth Streaming содержит тег повтора hello (r-tag). Однако некоторые проигрыватели не поддерживают hello r-tag. Клиенты с этими пользователями могут использовать формат, который отключает hello r-tag:

{имя конечной точки потоковой передачи - имя учетной записи служб мультимедиа}.streaming.mediaservices.windows.net/{идентификатор указателя}/{имя файла}.ism/Manifest(format=fmp4-v20)

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=fmp4-v20)

## <a name="progressive-download"></a>Прогрессивное скачивание
Последовательная загрузка позволяет запускать воспроизведение мультимедиа до загрузки всего файла hello. ISMV-, ISMA-, ISMT- и ISMC-файлы не могут быть загружены поэтапно.

tooprogressively загрузки содержимого, используйте тип локатора OnDemandOrigin hello. Hello ниже приведен пример hello URL-адрес, основанный на hello тип локатора OnDemandOrigin.

    http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

Необходимо расшифровать все хранилище зашифровано ОС, которые должны toostream из службы origin hello для последовательной загрузки.

## <a name="download"></a>Загрузить
toodownload содержимого tooa устройства клиента, необходимо создать указатель SAS. указатель SAS Hello предоставляет доступ к toohello контейнер хранилища Azure, где расположен файл. toobuild hello URL-адрес загрузки, имеют имя файла tooembed hello между hello узлом и подписью SAS.

Hello ниже приведен пример hello URL-адрес, основанный на указателя SAS hello.

    https://test001.blob.core.windows.net/asset-ca7a4c3f-9eb5-4fd8-a898-459cb17761bd/BigBuckBunny.mp4?sv=2012-02-12&se=2014-05-03T01%3A23%3A50Z&sr=c&si=7c093e7c-7dab-45b4-beb4-2bfdff764bb5&sig=msEHP90c6JHXEOtTyIWqD7xio91GtVg0UIzjdpFscHk%3D

применить Hello следующие вопросы:

* Необходимо расшифровать все хранилище зашифровано ОС, которые должны toostream из службы origin hello для последовательной загрузки.
* Процесс скачивания, не завершенный в течение 12 часов, завершается ошибкой.

## <a name="streaming-endpoints"></a>Конечные точки потоковой передачи

Конечную точку потоковой передачи представляет собой службу потоковой передачи, способную доставить содержимое напрямую tooa клиента проигрывателя приложения или tooa сети доставки содержимого (CDN) для дальнейшего распространения. Hello исходящим потоком из потоковой передачи конечной точки службы может быть потоком трансляции или актив видео по запросу в учетную запись служб мультимедиа. Существует два типа конечных точек потоковой передачи: **стандартные** и **Премиум**. Дополнительные сведения см. в статье [Общие сведения о конечных точках потоковой передачи](media-services-streaming-endpoints-overview.md).

>[!NOTE]
>При создании учетной записи AMS **по умолчанию** конечной точки потоковой передачи в hello добавлена учетная запись tooyour **остановлена** состояния. Потоковая передача вашего содержимого и примите преимуществами динамической упаковки и динамического шифрования toostart hello конечной точки потоковой передачи, из которого нужно имеет содержимое toostream toobe в hello **под управлением** состояния. 

## <a name="known-issues"></a>Известные проблемы
### <a name="changes-toosmooth-streaming-manifest-version"></a>Версия манифеста потоковой передачи tooSmooth изменения
Перед возвращением hello выпуск обновления июль 2016 г. — при активы стандартный кодировщик мультимедиа, расширенного рабочего процесса кодировщика мультимедиа, или hello потоковую передачу предыдущих Azure Media Encoder были включены с помощью динамической упаковки--hello Smooth Streaming манифеста будет соответствовать tooversion 2.0. В версии 2.0 длительности фрагмент hello не следует использовать теги hello так называемые повтора (r). Например:

<?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" n="0" />
            <c d="2000" />
            <c d="2000" />
            <c d="2000" />
        </StreamIndex>
    </SmoothStreamingMedia>

В hello июля 2016 г. службы созданный hello манифеста Smooth Streaming соответствует tooversion 2.2, с длительностью фрагмента с помощью тегов повторов. Например:

    <?xml version="1.0" encoding="UTF-8"?>
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="2" Duration="8000" TimeScale="1000">
        <StreamIndex Chunks="4" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="3" Subtype="" Name="video" TimeScale="1000">
            <QualityLevel Index="0" Bitrate="1000000" FourCC="AVC1" MaxWidth="640" MaxHeight="360" CodecPrivateData="00000001674D4029965201405FF2E02A100000030010000003032E0A000F42400040167F18E3050007A12000200B3F8C70ED0B16890000000168EB7352" />
            <c t="0" d="2000" r="4" />
        </StreamIndex>
    </SmoothStreamingMedia>

Некоторые устаревшие клиенты hello Smooth Streaming могут не поддерживать hello повторов теги, сможет tooload hello манифест. toomitigate эту проблему, можно использовать параметр устаревший формат манифеста hello **(формат = fmp4 v20)** или обновить ваш клиент toohello последней версии, поддерживает повторов тегов. Чтобы узнать больше, ознакомьтесь со [Smooth Streaming 2.0](media-services-deliver-content-overview.md#fmp4_v20).

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-topics"></a>Связанные разделы
[Обновление указателей служб мультимедиа после отката ключей хранилища](media-services-roll-storage-access-keys.md)

