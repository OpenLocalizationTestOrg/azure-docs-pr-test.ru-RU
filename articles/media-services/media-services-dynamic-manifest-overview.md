---
title: "aaaFilters и динамические манифесты | Документы Microsoft"
description: "Описывается, как фильтры toocreate, поэтому клиент может их использовать toostream определенных разделов потока. Службы мультимедиа создает динамические манифесты tooarchive Выборочный streaming."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: ff102765-8cee-4c08-a6da-b603db9e2054
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 06/29/2017
ms.author: cenkd;juliako
ms.openlocfilehash: 9527a011438c11da07a363d701ea736414412ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="filters-and-dynamic-manifests"></a>Фильтры и динамические манифесты
Начиная с выпуска 2.11, службы мультимедиа позволяют фильтры toodefine средств. Эти фильтры являются правила стороне сервера, позволяющие клиентам toochoose toodo таких вещей, как: воспроизведения только части видео (вместо воспроизведение hello всего видео), или укажите только набор представлений аудио и видео обработки (устройства клиента вместо всех hello представлений, которые связаны с активом hello). Такая фильтрация средств архивируется через **динамического манифеста**, созданных после toostream запрос клиента видео на основе указанного фильтров.

Приведенные здесь статьи рассматриваются распространенные сценарии, в котором с помощью фильтров будет очень полезными tooyour клиентов и ссылки tootopics, показывающими, как программным образом фильтрует toocreate (в настоящее время можно создать фильтры с API REST только).

## <a name="overview"></a>Обзор
При доставке поставленной вашего содержимого toocustomers (потоковой передачи событий в реальном времени или видео по запросу) является toodeliver к устройствам высокое качество видео toovarious условиях другую сеть. Эта цель hello следующие tooachieve:

* поток toomulti-bitrate кодирования ([с адаптивной скоростью](http://en.wikipedia.org/wiki/Adaptive_bitrate_streaming)) видеопоток (это берет на себя условия качества и сети) и 
* Использование служб мультимедиа [динамической упаковки](media-services-dynamic-packaging-overview.md) toodynamically повторно упаковать потока в различных протоколов (это берет на себя потоковой передачи на разных устройствах). Службы мультимедиа поддерживают доставку hello следующие технологии потоковой передачи с адаптивной скоростью: HTTP Live Streaming (HLS), Smooth Streaming и MPEG DASH. 

### <a name="manifest-files"></a>Файлы манифестов
При кодировании актива для потоковой передачи с адаптивной скоростью **манифеста** (воспроизведения) создается (файл hello текста или XML). Hello **манифеста** файл, содержащий, например потоковой передачи метаданных: отслеживайте тип (аудио, видео или текст), отслеживать имя, время начала и окончания, скоростью (качества), отслеживания языков, окно презентации (скользящее окно фиксированной длительности), видео кодек (FourCC). Оно также указывает следующий фрагмент tooretrieve проигрывателя hello hello, предоставляя информацию о hello Далее пригодный для воспроизведения видео фрагменты доступны и их расположение. Фрагментов (или сегменты) представляют собой hello фактическое «хранилища» видео-контента.

Ниже приведен пример файла манифеста: 

    <?xml version="1.0" encoding="UTF-8"?>    
    <SmoothStreamingMedia MajorVersion="2" MinorVersion="0" Duration="330187755" TimeScale="10000000">

    <StreamIndex Chunks="17" Type="video" Url="QualityLevels({bitrate})/Fragments(video={start time})" QualityLevels="8">
    <QualityLevel Index="0" Bitrate="5860941" FourCC="H264" MaxWidth="1920" MaxHeight="1080" CodecPrivateData="0000000167640028AC2CA501E0089F97015202020280000003008000001931300016E360000E4E1FF8C7076850A4580000000168E9093525" />
    <QualityLevel Index="1" Bitrate="4602724" FourCC="H264" MaxWidth="1920" MaxHeight="1080" CodecPrivateData="0000000167640028AC2CA501E0089F97015202020280000003008000001931100011EDC00002CD29FF8C7076850A45800000000168E9093525" />
    <QualityLevel Index="2" Bitrate="3319311" FourCC="H264" MaxWidth="1280" MaxHeight="720" CodecPrivateData="000000016764001FAC2CA5014016EC054808080A00000300020000030064C0800067C28000103667F8C7076850A4580000000168E9093525" />
    <QualityLevel Index="3" Bitrate="2195119" FourCC="H264" MaxWidth="960" MaxHeight="540" CodecPrivateData="000000016764001FAC2CA503C045FBC054808080A000000300200000064C1000044AA0000ABA9FE31C1DA14291600000000168E9093525" />
    <QualityLevel Index="4" Bitrate="1469881" FourCC="H264" MaxWidth="960" MaxHeight="540" CodecPrivateData="000000016764001FAC2CA503C045FBC054808080A000000300200000064C04000B71A0000E4E1FF8C7076850A4580000000168E9093525" />
    <QualityLevel Index="5" Bitrate="978815" FourCC="H264" MaxWidth="640" MaxHeight="360" CodecPrivateData="000000016764001EAC2CA50280BFE5C0548303032000000300200000064C08001E8480004C4B7F8C7076850A45800000000168E9093525" />
    <QualityLevel Index="6" Bitrate="638374" FourCC="H264" MaxWidth="640" MaxHeight="360" CodecPrivateData="000000016764001EAC2CA50280BFE5C0548303032000000300200000064C080013D60000C65DFE31C1DA1429160000000168E9093525" />
    <QualityLevel Index="7" Bitrate="388851" FourCC="H264" MaxWidth="320" MaxHeight="180" CodecPrivateData="000000016764000DAC2CA505067E7C054830303200000300020000030064C040030D40003D093F8C7076850A45800000000168E9093525" />

    <c t="0" d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="20000000" /><c d="9600000"/>
    </StreamIndex>


    <StreamIndex Chunks="17" Type="audio" Url="QualityLevels({bitrate})/Fragments(AAC_und_ch2_128kbps={start time})" QualityLevels="1" Name="AAC_und_ch2_128kbps">
    <QualityLevel AudioTag="255" Index="0" BitsPerSample="16" Bitrate="125658" FourCC="AACL" CodecPrivateData="1210" Channels="2" PacketSize="4" SamplingRate="44100" />

    <c t="0" d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="6965987" /></StreamIndex>


    <StreamIndex Chunks="17" Type="audio" Url="QualityLevels({bitrate})/Fragments(AAC_und_ch2_56kbps={start time})" QualityLevels="1" Name="AAC_und_ch2_56kbps">
    <QualityLevel AudioTag="255" Index="0" BitsPerSample="16" Bitrate="53655" FourCC="AACL" CodecPrivateData="1210" Channels="2" PacketSize="4" SamplingRate="44100" />

    <c t="0" d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201361" /><c d="20201360" /><c d="20201361" /><c d="20201360" /><c d="6965987" /></StreamIndex>

    </SmoothStreamingMedia>

### <a name="dynamic-manifests"></a>Динамические манифесты
Существуют [сценариев](media-services-dynamic-manifest-overview.md#scenarios) клиентом, когда потребуется большую гибкость, чем описанных в файле манифеста ресурса по умолчанию hello. Например:

* Устройства определенного: доставки hello указано представлений и (или) указан только отслеживает языков, поддерживаемых hello устройства, используемые tooplayback hello фильтрацию («представления»). 
* Уменьшите hello манифеста tooshow суб-клип динамической события («суб-клип фильтрация»).
* Начало Trim hello видео («обрезки видео»).
* Настройка окна представления (DVR) в порядке tooprovide ограниченной длины окна DVR hello в проигрывателе hello («Настройка презентации окно»).

tooachieve этот гибкость, Media Services имеют **динамического манифесты** зависимости на предварительно определенные [фильтры](media-services-dynamic-manifest-overview.md#filters).  После определения фильтров hello клиентам использовать их toostream другое представление или суб-клипы видео. Их следует указать фильтры в URL-адрес потоковой передачи hello. Фильтры могут быть потоковой передачи протоколы, поддерживаемые скоростью примененных tooadaptive [динамической упаковки](media-services-dynamic-packaging-overview.md): HLS, MPEG-DASH и Smooth Streaming. Например:

URL-адрес MPEG DASH с фильтром

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf,filter=MyLocalFilter)

URL-адрес Smooth Streaming с фильтром

    http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(filter=MyLocalFilter)


Дополнительные сведения о том, как toodeliver содержимого и построения потоковой передачи в URL-адреса, в разделе [доставки содержимого Обзор](media-services-deliver-content-overview.md).

> [!NOTE]
> Обратите внимание, что динамические манифесты не изменяйте активов hello и hello манифест по умолчанию для этого ресурса. Ваш клиент можно выбрать toorequest потока с или без них. 
> 
> 

### <a id="filters"></a>Фильтры
Существуют два типа фильтров активов. 

* Глобальные фильтры (можно быть применен tooany средства в hello учетная запись служб мультимедиа Azure, время существования hello учетной записи) и 
* Локальных фильтров (можно только примененные tooan активов, с какой hello фильтра была связана после их создания, время существования средства hello). 

Типы фильтров глобальная и локальная, гарантия в точности hello и те же свойства. Hello основное различие между двумя hello является для сценариев, какой тип фильтр более подходящим. Глобальные фильтры обычно подходят для профилей устройств (Фильтрация представления) где локальных фильтров может быть используется tootrim определенного актива.

## <a id="scenarios"></a>Распространенные сценарии
Как упоминалось ранее, при доставки вашего содержимого toocustomers (потоковой передачи событий в реальном времени или видео по запросу) ваша цель — toodeliver высокое качество видео toovarious устройства в другой сети условия. Кроме этого, возможны и другие требования, задействующие фильтрацию активов и использование **динамических манифестов**. Привет, в следующих разделах дать краткий обзор различных сценариев фильтрации.

* Укажите только набор представлений аудио и видео, которые может обрабатывать определенные устройства (а не всех hello представлений, связанные с активом hello). 
* Воспроизведение только часть видео (а не выполняет hello всего видео).
* Настройка окна представления DVR.

## <a name="rendition-filtering"></a>Фильтрация представлений
Вы можете tooencode активов toomultiple кодирования профили (H.264 базовый, высокий уровень H.264, AACL, AACH, Dolby Digital Plus) и несколько битрейтов качества. Однако не все клиентские устройства будут поддерживать все профили и скорости потока вашего актива. Например, старые устройства Android поддерживают только H.264 Baseline+AACL. Отправка выше устройство tooa битрейтов, который не удается получить преимущества hello, много вычисления пропускной способности и устройства. Такие устройства необходимо расшифровать все Здравствуйте, учитывая сведения только tooscale его вниз для отображения.

С динамической манифеста можно создать профили устройств мобильных устройств, например, консоли, HD/SD, т. д. и включать отслеживает hello и качеств, которые следует включить toobe часть каждого профиля.

![Пример фильтрации представлений][renditions2]

В следующем примере hello кодировщик был tooencode используется для расширения средства в семь представлений видео MP4-файлов ISO (от too1080p 180p). Hello кодированный актив могут быть динамически упакованы в любой из hello следующие протоколы потоковых: HLS, Smooth и MPEG DASH.  Вверху hello hello диаграммы отображается hello HLS манифеста для ресурса hello без фильтров (содержит все семь представлений).  В нижнем левом углу hello hello HLS манифеста toowhich, который был применен фильтр с именем «ott» отображается. Фильтр «ott» Hello указывает tooremove все битрейтах ниже 1 Мбит/с, что привело к hello нижней два уровня качества отброшены в ответ hello.  Hello нижнем правом углу, hello HLS показан toowhich манифеста, который был применен фильтр с именем «мобильных устройств». Фильтр «мобильных устройств» Hello указывает tooremove представлений, где hello разрешение больше, чем 720p, что привело к hello отброшены два представления 1080p.

![Фильтрация представлений][renditions1]

## <a name="removing-language-tracks"></a>Удаление языковых дорожек
Активы могут содержать аудиодорожки на нескольких языках, например английском, испанском, французском и т. д. Обычно диспетчеры hello этого ПАКЕТА по умолчанию выбор звуковой дорожки и отслеживает доступные звука на выбор пользователя. Он является довольно сложной toodevelop такие пакеты SDK проигрывателя, необходимо различных реализаций через платформы проигрывателя конкретного устройства. Кроме того на некоторых платформах API проигрывателя ограничены и не включают функции аудио выбора, где пользователи не могут выбрать или изменить звуковой дорожки по умолчанию hello. С помощью фильтров активов можно управлять поведением hello с помощью фильтров, включать только нужные языки аудио.

![Фильтрация языковых дорожек][language_filter]

## <a name="trimming-start-of-an-asset"></a>Обрезка начала актива
В большинстве динамической потоковой передачи событий операторы выполнять некоторые тесты до фактического события hello. Например, они могут включать Сланец следующим образом, перед запуском hello hello события: «Программа начнет свою работу незамедлительно». Если программа hello архивирования, hello тестирования и содержания данных также архивируются и будут включены в презентации hello. Тем не менее эти сведения не должен отображаться toohello клиентов. С помощью динамического манифеста можно создать фильтр времени начала и удалить hello нежелательных данных из манифеста hello.

![Начало обрезки][trim_filter]

## <a name="creating-sub-clips-views-from-a-live-archive"></a>Создание субклипов (представлений) из текущего архива
Многие текущие события являются длительными, и их текущий архив может включать в себя несколько событий. После hello интерактивного события окончания источников может потребоваться toobreak копирование hello live архива в логической программы для запуска и остановки последовательности. Затем опубликуйте эти виртуальные программы отдельно без post обработки динамического архива hello и не создавая отдельные активы (которые не будут пользоваться преимуществами существующих кэшированные фрагменты hello в hello CDN). Примерами таких виртуальных программ (суб-клипы): hello кварталы футбольной или Баскетбольная игры, иннингов hello в бейсбольные или отдельные события f # программы Олимпийские игры.

С помощью динамического манифеста можно создавать фильтры, с помощью времени начала и окончания и создавать виртуального представления поверх hello динамического архива. 

![Фильтр субклипа][subclip_filter]

Фильтрованный архив:

![Лыжный спорт][skiing]

## <a name="adjusting-presentation-window-dvr"></a>Настройка окна презентации (DVR)
В настоящее время службы мультимедиа Azure предлагает циклические архива, где можно настроить длительность hello от 5 минут — 25 часов. Манифеста можно использовать фильтрацию используется toocreate скользящего окна DVR поверх hello архива hello, не удаляя носителя. Существует множество сценариев, где источников добавить tooprovide ограниченный окна DVR, который перемещается вместе с hello live границы и на hello то же время сохранить увеличить архивирования окно. Вещателем может потребоваться данных toouse hello, выходящее за пределы окна toohighlight hello DVR клипы или he\she может потребоваться tooprovide различные окна DVR для различных устройств. Например большинство hello мобильных устройств не обрабатывают большие windows DVR (для настольных клиентов могут иметь окна DVR 2 минуты для мобильных устройств и 1 час).

![Окно DVR][dvr_filter]

## <a name="adjusting-livebackoff-live-position"></a>Настройка LiveBackoff (динамической позиции)
Манифеста можно использовать фильтрацию tooremove используется несколько секунд от края динамической hello динамической программы. Это позволяет источников toowatch hello презентации на предварительный просмотр публикации hello точки и создать объявление точки вставки, прежде чем средств просмотра hello получить поток hello (обычно резервные выключение до 30 секунд). Источников можно передать эти объявления tootheir клиентских платформ времени для них сведения hello tooreceived и процесс перед возможности объявления hello.

Кроме поддержки toohello объявления, LiveBackoff можно использовать для корректировки положение динамической загрузки клиента так, чтобы когда клиенты смещения и попадания динамической edge hello они могут по-прежнему получить фрагментов сервера, а не происходят ошибки HTTP 404 или 412.

![livebackoff_filter][livebackoff_filter]

## <a name="combining-multiple-rules-in-a-single-filter"></a>Объединение нескольких правил в одном фильтре
В одном фильтре можно объединить несколько правил фильтрации. В качестве примера можно определить правило для диапазона tooremove материала из динамического архива и фильтровать доступные битрейтов. Для нескольких фильтрации end hello правила результат — hello комбинацию (пересечение) из этих правил.

![multiple-rules][multiple-rules]

## <a name="create-filters-programmatically"></a>Программное создание фильтров
Hello разделе обсуждаются сущностей служб мультимедиа, которые являются связанные toofilters. Hello разделе также показано, как tooprogrammatically создать фильтры.  

[Создание фильтров с помощью интерфейсов REST API](media-services-rest-dynamic-manifest.md).

## <a name="combining-multiple-filters-filter-composition"></a>Объединение нескольких фильтров (сложение фильтров)
Кроме того, вы можете объединять несколько фильтров в одном URL-адресе. 

Hello следующем сценарии демонстрируется, которым toocombine фильтры:

1. Требуется toofilter вашей качества видео для мобильных устройств, например Android или iPAD (в качества видео toolimit порядке). tooremove Здравствуйте нежелательных качеств, необходимо создать как глобальный фильтр, который подходит для профилей устройств. Как упоминалось выше, глобальные фильтры можно использовать для всех ресурсов в группе hello и те же носители учетная запись службы не все дополнительные связи. 
2. Также требуется tootrim hello начала и время актива окончания. tooachieve это, вам потребуется создать локальный фильтр и задать начальное и конечное время hello. 
3. Вы хотите toocombine оба эти фильтры (без сочетания потребовалось бы tooadd качества фильтрации toohello усечения фильтр, который будет трудно использование фильтра).

фильтры toocombine необходимо tooset hello фильтр имен toohello манифеста или список воспроизведения URL-адрес с запятой. Предположим, что у вас есть фильтр под названием *MyMobileDevice* , фильтрует качества и у вас есть другое свойство с именем *MyStartTime* tooset конкретного времени начала. Их можно объединить следующим образом:

    http://teststreaming.streaming.mediaservices.windows.net/3d56a4d-b71d-489b-854f-1d67c0596966/64ff1f89-b430-43f8-87dd-56c87b7bd9e2.ism/Manifest(filter=MyMobileDevice;MyStartTime)

Можно объединять too3 фильтров. 

Дополнительную информацию см. в [этом](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) блоге.

## <a name="know-issues-and-limitations"></a>Известные проблемы и ограничения
* Динамический манифест работает в пределах GOP (по ключевым кадрам), поэтому обрезка производится с точностью GOP. 
* Одно и то же имя фильтра можно использовать для локальных и глобальных фильтров. Обратите внимание, что локальный фильтр имеет более высокий приоритет и переопределяет глобальные фильтры.
* При обновлении фильтра может занять too2 минут для потоковой передачи конечной точки toorefresh hello правила. Если содержимое hello был обработан с помощью некоторых фильтров (и кэширования в прокси-серверы и CDN кэши), обновление этих фильтров можно привести к сбою проигрывателя. Рекомендуется tooclear hello кэша после обновления hello фильтра. Если такой вариант невозможен, рассмотрите возможность использования другого фильтра.

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>См. также
[Доставка содержимого tooCustomers Обзор](media-services-deliver-content-overview.md)

[renditions1]: ./media/media-services-dynamic-manifest-overview/media-services-rendition-filter.png
[renditions2]: ./media/media-services-dynamic-manifest-overview/media-services-rendition-filter2.png

[rendered_subclip]: ./media/media-services-dynamic-manifests/media-services-rendered-subclip.png
[timeline_trim_event]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-event.png
[timeline_trim_subclip]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-subclip.png

[multiple-rules]:./media/media-services-dynamic-manifest-overview/media-services-multiple-rules-filters.png

[subclip_filter]: ./media/media-services-dynamic-manifest-overview/media-services-subclips-filter.png
[trim_event]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-event.png
[trim_subclip]: ./media/media-services-dynamic-manifests/media-services-timeline-trim-subclip.png
[trim_filter]: ./media/media-services-dynamic-manifest-overview/media-services-trim-filter.png
[redered_subclip]: ./media/media-services-dynamic-manifests/media-services-rendered-subclip.png
[livebackoff_filter]: ./media/media-services-dynamic-manifest-overview/media-services-livebackoff-filter.png
[language_filter]: ./media/media-services-dynamic-manifest-overview/media-services-language-filter.png
[dvr_filter]: ./media/media-services-dynamic-manifest-overview/media-services-dvr-filter.png
[skiing]: ./media/media-services-dynamic-manifest-overview/media-services-skiing.png
