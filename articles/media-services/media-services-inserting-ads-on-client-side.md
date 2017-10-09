---
title: "aaaInserting рекламы на стороне клиента hello | Документы Microsoft"
description: "В этом разделе показано, как tooinsert рекламы на hello на стороне клиента."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 65c9c747-128e-497e-afe0-3f92d2bf7972
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: e6eab4aa92918ad734db8ac3a4e7818d02ed7fe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="inserting-ads-on-hello-client-side"></a>Вставка рекламы на стороне клиента hello
Этот раздел содержит сведения о том, как tooinsert разных типов рекламы на стороне клиента hello.

Сведения о поддержке субтитров и рекламы в динамических потоковых видео см. в разделе [Вставка субтитров и рекламы](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).

> [!NOTE]
> Проигрыватель мультимедиа Azure на данный момент не поддерживает рекламу.
> 
> 

## <a id="insert_ads_into_media"></a>Вставка рекламы в мультимедиа
Службы мультимедиа Azure обеспечивает поддержку вставки рекламы посредством hello Windows Media Platform: платформы проигрывателя. Платформы проигрывателя с поддержкой рекламы доступны для устройств Windows 8, Silverlight, Windows Phone 8 и iOS. Каждая платформа проигрывателя содержит образец кода, которое показывает, как tooimplement приложение проигрывателя. Существует три вида рекламы, которые можно вставить в media: список.

* **Линейный** — полный кадр рекламы паузы hello основного видео.
* **Нелинейный** – реклама, которая отображается поверх основного видео hello воспроизводится, обычно это логотип или другое статическое изображение размещается в проигрывателе hello.
* **Помощник по поиску** – реклама, которая отображается за пределами проигрывателя hello.

Рекламу можно размещать в любой точке временной шкалы основного видео hello. Необходимо сообщить hello проигрывателя при tooplay hello ad и который tooplay рекламы. Для этого используется набор стандартных XML-файлов: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST) и Digital Video Player Ad Interface Definition (VPAID). VAST-файлы указывают, какие toodisplay рекламы. VMAP-файлы указывают, когда tooplay различные рекламные ролики и содержат XML-код VAST. MAST-файлы являются другим способом toosequence рекламы, они также содержат XML-код VAST. VPAID-файлы определяют интерфейс между видеопроигрывателем hello и hello ad или на сервере ad.

Каждая платформа проигрывателя работает по-разному, и каждой из них посвящен отдельный раздел. В этом разделе описано hello базовый механизм tooinsert рекламы. Видеопроигрыватель приложения запрашивают рекламу с сервера рекламы. сервер Hello рекламы может ответить несколькими способами:

* Вернуть VAST-файл
* Вернуть VMAP-файл (с внедренным кодом VAST)
* Вернуть MAST-файл (с внедренным кодом VAST)
* Вернуть VAST-файл с рекламными объявлениями VPAID

### <a name="using-a-video-ad-service-template-vast-file"></a>Использование файла Video Ad Service Template (VAST)
VAST-файл определяет, какие ad или toodisplay рекламы. Hello следующий XML-код является примером VAST-файла для линейной рекламы:

    <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
      <Ad id="115571748">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://www.myserver.com/tracking-resource]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:32</Duration>
                <TrackingEvents>
                  <Tracking event="start"><![CDATA[http://www.myserver.com/start-tracking-resource]]></Tracking>
                  <Tracking event="midpoint"><![CDATA[http://www.myserver.com/midpoint-tracking-resource]]></Tracking>
                  <Tracking event="complete"><![CDATA http://www.myserver.com/complete-tracking-resource]]></Tracking>
                  <Tracking event="expand"><![CDATA[http://www.myserver.com/expand-tracking-resource]]></Tracking>
                </TrackingEvents>
                <VideoClicks>
                  <ClickThrough id="Atlas Redirect"><![CDATA[http://www.myserver.com/click-resource]]></ClickThrough>
                  <ClickTracking id="Spare"></ClickTracking>
                </VideoClicks>
                <MediaFiles>
                  <MediaFile apiFramework="Windows Media" id="windows_progressive_200" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="200" width="400" height="300" type="video/x-ms-wmv">
                    <![CDATA[http://www.myserver.com/media/myad_200_4x3.wmv]]>
                  </MediaFile>
                  <MediaFile apiFramework="Windows Media" id="windows_progressive_300" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="300" width="400" height="300" type="video/x-ms-wmv">
                    <![CDATA[http://www.myserver.com/media/myad_300_4x3.wmv]]>
                  </MediaFile>
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
          <Extensions>
            <Extension type="Atlas">
            </Extension>
          </Extensions>
        </InLine>
      </Ad>
    </VAST>

Hello линейная реклама описывается hello <**линейное**> элемент. Он определяет длительность hello hello ad, события отслеживания, при щелчке, отслеживание щелчков и количество **MediaFile** элементов. События отслеживания указываются в hello <**TrackingEvents**> элемент и разрешить tootrack сервера ad различные события, происходящие во время просмотра hello ad. В этом случае hello начала, середины, завершения и разверните отслеживаются события. Hello начала событие возникает при отображении hello ad. событие середины Hello возникает при по крайней мере просматривал 50% hello ad временной шкалы. событие завершения Hello возникает, когда hello ad toohello end. Hello развернуть событие возникает при hello пользователь разворачивает hello видеопроигрыватель toofull экрана. Действие при щелчке указывается с <**с дополнительной информацией**> элемента <**VideoClicks**> элемент и указывает toodisplay ресурсов tooa URI, когда hello пользователь выбирает hello ad. Отслеживание щелчков указывается в <**отслеживание щелчков**> элемент также в hello <**VideoClicks**> элемент и задает ресурс отслеживания toorequest hello проигрывателя при нажатии пользователем hello на hello ad.hello <**MediaFile**> элементов укажите сведения о кодировке рекламы. При наличии более чем одного <**MediaFile**> элемент, hello видеопроигрыватель может выбирать лучшую кодировку hello для платформы hello. 

Линейную рекламу можно отображать в указанном порядке. toodo это, добавьте дополнительные <Ad> элементы toohello VAST файла и укажите порядок hello, с помощью атрибута последовательности hello. Привет, в следующем примере показано следующее:

    <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
      <Ad id="1" sequence="0">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://myserver.com/Impression/Ad1trackingResouce]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:32</Duration>
                <MediaFiles>
                  <!-- ... -->
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
        </InLine>
      </Ad>
      <Ad id="2" sequence="1">
        <InLine>
          <AdSystem version="2.0 alpha">Atlas</AdSystem>
          <AdTitle>Unknown</AdTitle>
          <Description>Unknown</Description>
          <Survey></Survey>
          <Error></Error>
          <Impression id="Atlas"><![CDATA[http://myserver.com/Impression/Ad2trackingResouce]]></Impression>
          <Creatives>
            <Creative id="video" sequence="0" AdID="">
              <Linear>
                <Duration>00:00:30</Duration>
                <MediaFiles>
                  <!-- ... -->
                </MediaFiles>
              </Linear>
            </Creative>
          </Creatives>
        </InLine>
      </Ad>
    </VAST>

Нелинейная реклама также задается в элементе <Creative>. Следующий пример показывает Hello <Creative> элемент, описывающий нелинейную рекламу.

    <Creative id="video" sequence="1" AdID="">
      <NonLinearAds>
        <NonLinear width="216" height="121" minSuggestedDuration="00:00:15">
          <StaticResource creativeType="image/png"><![CDATA[http://myserver/images/image.png]]></StaticResource>
          <StaticResource creativeType="image/jpg"><![CDATA[http://myserver/images/image.jpg]]></StaticResource>
        </NonLinear>
        <TrackingEvents>
             <Tracking event="acceptInvitation"><![CDATA[http://myserver/tracking/trackingID]></Tracking>
             <Tracking event="collapse"><![CDATA[http://myserver/tracking/trackingID2]]></Tracking>
         </TrackingEvents>
       </NonLinearAds>
    </Creative>


Привет <**NonLinearAds**> может содержать один или несколько <**Нелинейная**> элементов, каждый из которых можно описать нелинейную рекламу. Привет <**Нелинейная**> элемент указывает ресурс hello для hello нелинейную рекламу. Hello ресурс может быть <**StaticResouce**>, <**IFrameResource**>, или объект <**HTMLResouce**>. <**StaticResource**> описывает ресурс не на основе HTML и определяет атрибут creativeType, который указывает способ отображения hello ресурсов:

Изображение/gif, изображение/jpeg, image/png — ресурс hello отображается в HTML-<**img**> тег.

Приложения/x-javascript — ресурс hello отображается в HTML-<**сценарий**> тег.

Приложения/x-shockwave-flash — ресурс hello отображается в проигрывателе Flash.

**IFrameResource** описывает ресурс HTML, который может быть отображен в IFrame. **HTMLResource** описывает фрагмент HTML-кода, который может быть вставлен в веб-страницу. **TrackingEvents** укажите события отслеживания и hello URI toorequest при возникновении события hello. В этом образце hello отслеживаются события acceptInvitation и сворачивания. Дополнительные сведения о hello **NonLinearAds** элемента и его дочерних элементов в разделе IAB.NET/VAST. Обратите внимание, что hello **TrackingEvents** элемент находится в пределах hello **NonLinearAds** элемент, а не hello **Нелинейная** элемента.

Сопутствующая реклама задается в элементе <CompanionAds>. Hello <CompanionAds> элемент может содержать один или несколько <Companion> элементов. Каждый <Companion> элемент описывает сопутствующую рекламу и может содержать <StaticResource>, <IFrameResource>, или <HTMLResource> которые указываются hello же способом, как и в нелинейную рекламу. VAST-файл может содержать несколько элементов сопутствующей рекламы и приложение hello проигрывателя можно выбрать наиболее подходящий ad toodisplay hello. Дополнительные сведения о VAST см. в разделе [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a>Использование файла Digital Video Multiple Ad Playlist (VMAP)
VMAP-файла позволяет toospecify при возникновении рекламных пауз, — продолжительность каждого разрыва, вмещает количество рекламных роликов в паузе и типы рекламы, которые могут отображаться во время приостановки выполнения. Hello в пример VMAP файла, который определяет одну рекламную паузу следующих:

    <vmap:VMAP xmlns:vmap="http://www.iab.net/vmap-1.0" version="1.0">
      <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start">
        <vmap:AdSource allowMultipleAds="true" followRedirects="true" id="1">
          <vmap:VASTData>
            <VAST version="2.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="oxml.xsd">
              <Ad id="115571748">
                <InLine>
                  <AdSystem version="2.0 alpha">Atlas</AdSystem>
                  <AdTitle>Unknown</AdTitle>
                  <Description>Unknown</Description>
                  <Survey></Survey>
                  <Error></Error>
                  <Impression id="Atlas"><![CDATA[http://view.atdmt.com/000/sview/115571748/direct;ai.201582527;vt.2/01/634364885739970673]]></Impression>
                  <Creatives>
                    <Creative id="video" sequence="0" AdID="">
                      <Linear>
                        <Duration>00:00:32</Duration>
                        <MediaFiles>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_200" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="200" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_1_000_200_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_300" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="300" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_300_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_500" maintainAspectRatio="true" scaleable="true"  delivery="progressive" bitrate="500" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_1_000_500_4x3.wmv]]>
                          </MediaFile>
                          <MediaFile apiFramework="Windows Media" id="windows_progressive_700" maintainAspectRatio="true" scaleable="true" delivery="progressive" bitrate="700" width="400" height="300" type="video/x-ms-wmv">
                            <![CDATA[http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_700_4x3.wmv]]>
                          </MediaFile>
                        </MediaFiles>
                      </Linear>
                    </Creative>
                  </Creatives>
                </InLine>
              </Ad>
            </VAST>
          </vmap:VASTData>
        </vmap:AdSource>
        <vmap:TrackingEvents>
          <vmap:Tracking event="breakStart">
            http://MyServer.com/breakstart.gif
          </vmap:Tracking>
        </vmap:TrackingEvents>
      </vmap:AdBreak>
    </vmap:VMAP>

VMAP-файл начинается с элемента <VMAP>, в котором содержатся один или несколько элементов <AdBreak>, каждый из которых определяет рекламную паузу. Каждая рекламная пауза определяется типом паузы, идентификатором и смещение времени. Hello атрибут breakType указывает тип hello ad, который может воспроизводиться во время паузы hello: линейная, Нелинейная или отображение. Объявления сопоставить tooVAST сопутствующей рекламы. Можно указать несколько типов рекламы в списке, разделенном запятыми (без пробелов). Hello атрибут breakID является необязательным идентификатором для hello ad. Hello timeOffset указывает, когда должна отображаться hello ad. Его можно указать одним из следующих способов hello.

1. Время в формате hh:mm:ss или hh:mm:ss.mmm, где .mmm — количество миллисекунд. значение этого атрибута Hello указывает hello времени с начала hello hello шкале видео toohello начала рекламной паузы hello.
2. Процент в формате n %, где n — процент hello tooplay шкале видео hello перед воспроизведением hello ad
3. Начало/конец — указывает, что реклама должна воспроизводиться до или после hello видео
4. Position указывает порядок рекламных пауз hello при синхронизации hello hello рекламных пауз неизвестно, например потоковой трансляции. Hello порядок каждой рекламной паузы задается в формате hello #n, где n — целое число больше или равно 1. 1 означает hello рекламу следует воспроизводить при первой возможности hello, 2 означает hello рекламу следует воспроизводить при второй возможности hello и т. д.

В рамках hello <**AdBreak**> элемент может быть одним <**AdSource**> элемент. Привет <**AdSource**> элемент содержит hello следующие атрибуты:

1. ID указывает идентификатор источника рекламы hello
2. allowMultipleAds — логическое значение, указывающее отображения несколько рекламных роликов во время рекламной паузы hello
3. followRedirects — необязательное логическое значение, указывающее, следует принять при hello видеопроигрыватель перенаправляет внутри реакцию на рекламу

Привет <**AdSource**> элемент предоставляет hello проигрывателю встроенную реакцию на рекламу или ссылку tooan Active Directory: ответы. Имя может содержать один из следующих элементов hello:

* <VASTAdData>Указывает, что рекламу VAST внедрена в VMAP-файл hello
* <AdTagURI> — URI, который ссылается на отклик на рекламу из другой системы;
* <CustomAdData> — произвольная строка, представляющая собой отклик, не имеющий отношения к VAST.

В этом примере указывается встроенный отклик на рекламу с элементом <VASTAdData>, содержащим отклик на рекламу VAST. Дополнительные сведения о hello см. другие элементы [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).

Привет <**AdBreak**> элемент также может содержать один <**TrackingEvents**> элемент. Привет <**TrackingEvents**> элемент позволяет tootrack hello начало или конец рекламной паузы или от того, произошла ли ошибка во время рекламной паузы hello. Привет <**TrackingEvents**> элемент содержит один или несколько <**отслеживания**> элементов, каждый из которых задает события отслеживания и URI отслеживания. доступны следующие события отслеживания возможных Hello.

1. breakStart отслеживает начало рекламной паузы hello
2. breakEnd завершения hello отслеживания рекламной паузы
3. Error отслеживает ошибки, возникшей во время рекламной паузы hello

Следующий пример Hello показан VMAP-файл, который задает события отслеживания

    <vmap:VMAP xmlns:vmap="http://www.iab.net/vmap-1.0" version="1.0">
      <vmap:AdBreak breakType="linear" breakId="mypre" timeOffset="start">
        <vmap:AdSource allowMultipleAds="true" followRedirects="true" id="1">
          <vmap:VASTData>
            <!--Inline VAST -->
          </vmap:VASTData>
        </vmap:AdSource>
        <vmap:TrackingEvents>
          <vmap:Tracking event="breakStart">
            http://MyServer.com/breakstart.gif
          </vmap:Tracking>
          <vmap:Tracking event="breakend">
            http://MyServer.com/breakend.gif
          </vmap:Tracking>
          <vmap:Tracking event="error">
            http://MyServer.com/error.gif
          </vmap:Tracking>
        </vmap:TrackingEvents>
      </vmap:AdBreak>
    </vmap:VMAP>

Дополнительные сведения о hello <**TrackingEvents**> элемента и его дочерних элементов в разделе http://iab.org/VMAP.pdf

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a>Использование файла Media Abstract Sequencing Template (MAST)
MAST-файла позволяет toospecify триггеры, которые определяют, когда будет воспроизводиться реклама. Hello ниже приведен пример MAST-файла, содержащего триггеры для рекламы, воспроизводимой видео pre, ad воспроизводимой и рекламы, воспроизводимой после видео.

    <MAST xsi:schemaLocation="http://openvideoplayer.sf.net/mast http://openvideoplayer.sf.net/mast/mast.xsd" xmlns="http://openvideoplayer.sf.net/mast" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <triggers>
        <trigger id="preroll" description="preroll every item"  >
          <startConditions>
            <condition type="event" name="OnItemStart" />
          </startConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>

        <trigger id="midroll" description="midroll at 15 sec."  >
          <startConditions>
            <condition type="property" name="Position" value="00:00:15.0" operator="GEQ" />
          </startConditions>
          <endConditions>
            <condition type="event" name="OnItemEnd"/>
            <!--This 'resets' hello trigger for hello next clip-->
          </endConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>

        <trigger id="postroll" description="postroll"  >
          <startConditions>
            <condition type="event" name="OnItemEnd"/>
          </startConditions>
          <sources>
            <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
              <sources />
            </source>
          </sources>
        </trigger>
      </triggers>
    </MAST>



MAST-файл начинается с элемента **MAST**, в котором содержится один элемент **triggers**. Hello <triggers> элемент содержит один или несколько **триггер** элементы, которые определяют, когда должна воспроизводиться реклама. 

Hello **триггер** элемент содержит **startConditions** элемент, указывающий запуска tooplay ad. Hello **startConditions** элемент содержит один или несколько <condition> элементов. При каждой <condition> вычисляет tootrue триггер инициируется или вызывается, в зависимости от того, является ли hello <condition> внутри **startConditions** или **endConditions** элемент соответственно. Если несколько <condition> используются элементы, они обрабатываются как неявное OR, любое условие, получающее tootrue вызовет tooinitiate hello триггера. Элементы <condition> могут быть вложенными. Если дочерний <condition> элементы заданы, они обрабатываются как неявное and., все условия должно оцениваться tootrue для tooinitiate hello триггера. Hello <condition> элемент содержит следующие атрибуты, определяющие условия hello hello: 

1. **Тип** — указывает тип hello условие, свойства или события
2. **имя** — hello имя hello свойство или событие toobe, используемые при проверке
3. **значение** – значение, которое будет вычисляться свойство hello
4. **оператор** — hello toouse операции во время вычисления: EQ (равно), NEQ (не равно), GTR (больше), GEQ (больше или равно), LT (меньше), LEQ (меньше или равно), MOD (остаток от деления)

В **endConditions** также содержатся элементы <condition>. Если условие триггера hello tootrue — reset.hello <trigger> элемент также содержит <sources> элемент, который содержит один или несколько <source> элементов. Hello <source> элементы определяют toohello ad hello URI ответа и hello тип ответа ad. В этом примере приведен URI tooa реакции VAST. 

    <trigger id="postroll" description="postroll"  >
      <startConditions>
        <condition/>
      </startConditions>
      <sources>
        <source uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" format="vast">
          <sources />
        </source>
      </sources>
    </trigger>


### <a name="using-video-player-ad-interface-definition-vpaid"></a>Использование Video Player-Ad Interface Definition (VPAID)
VPAID — это API для включения toocommunicate единицы исполняемая реклама с видеопроигрывателем. Это позволяет создавать рекламу с высокой степенью интерактивности. Hello пользователь может взаимодействовать с hello ad и hello реклама может отвечать tooactions выполняемое просмотра hello. Например, в рекламе могут отображаться кнопки, позволяющие tooview пользователя hello Дополнительные сведения или более длительную версию рекламы hello. Hello видеопроигрыватель должен поддерживать VPAID API hello и hello исполняемая реклама должна реализовывать интерфейс API hello. Когда проигрыватель запрашивает рекламу с сервера hello сервер рекламы может ответить реакцией VAST, которая содержит рекламу vpaid.

Исполняемая реклама создается в коде, который должен выполняться в среде выполнения, например Adobe Flash ™ или JavaScript, способной функционировать в веб-браузере. Когда сервер рекламы возвращает реакцию VAST, содержащую РЕКЛАМУ vpaid, hello значение атрибута apiFramework hello в hello <MediaFile> элемент должен быть «VPAID». Этот атрибут указывает, что данного рекламного объявления hello содержится является исполняемой рекламой VPAID. Hello типа атрибут должен быть задан тип MIME toohello hello исполняемый файл, например «application/x-shockwave-flash» или «application/x-javascript». Hello следующем фрагменте кода XML показаны hello <MediaFile> элемент из реакции VAST, содержащий исполняемое объявление vpaid. 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI tooexecutable ad -->
       </MediaFile>
    </MediaFiles>


Исполняемую рекламу можно инициализировать с помощью hello <AdParameters> элемент в пределах hello <Linear> или <NonLinear> элементов в реакции VAST. Дополнительные сведения о hello <AdParameters> элемент, в разделе [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf). Дополнительные сведения об VPAID API hello см. в разделе [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a>Реализация проигрывателя Windows или Windows Phone 8 с поддержкой рекламы
Hello Microsoft Media Platform: платформа проигрывателя для Windows 8 и Windows Phone 8 содержит набор примеров приложений, которые показывают, как приложение видеопроигрывателя с помощью tooimplement hello framework. Можно загрузить образцы платформа проигрывателя и hello hello из [платформа проигрывателя для Windows 8 и Windows Phone 8](https://playerframework.codeplex.com).

При открытии решения Microsoft.PlayerFramework.Xaml.Samples hello вы увидите несколько папок в рамках проекта hello. Hello в папке Advertising содержится hello образец кода соответствующей toocreating видеопроигрывателя с поддержкой рекламы. В папке Advertising hello внутри имеет ряд XAML/cs файлы каждый из которых Показать как tooinsert рекламы по-разному. После списка Hello описаны:

* AdPodPage.xaml показано, как toodisplay ad pod.
* Показывает AdSchedulingPage.xaml как tooschedule рекламы.
* FreeWheelPage.xaml показано, как toouse hello рекламы tooschedule подключаемого модуля FreeWheel.
* Показывает MastPage.xaml как tooschedule рекламы с помощью MAST-файл.
* ProgrammaticAdPage.xaml показано, как tooprogrammatically планирование рекламы в видео.
* Показывает ScheduleClipPage.xaml как tooschedule рекламы без VAST-файл.
* Показывает VastLinearCompanionPage.xaml как tooinsert линейной и сопутствующей рекламы.
* Показывает VastNonLinearPage.xaml как tooinsert нелинейной рекламы.
* Показывает VmapPage.xaml как toospecify рекламы с помощью VMAP-файл.

Каждый из этих примеров используется класс MediaPlayer hello, определенные платформой проигрывателя hello. В большинстве образцов используются подключаемые модули, которые обеспечивают поддержку различных форматов откликов. Образец Hello ProgrammaticAdPage программно взаимодействует с экземпляром MediaPlayer.

### <a name="adpodpage-sample"></a>Образец AdPodPage
В этом образце используется hello AdSchedulerPlugin toodefine при toodisplay ad. В этом примере объявления воспроизводимой — запланированных toobe воспроизводиться через 5 секунд. Hello рекламы (группа toodisplay рекламы в порядке) задается в VAST-файл, возвращенный от сервера ad. Hello URI toohello VAST-файл указывается в hello <RemoteAdSource> элемента.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">

        <mmppf:MediaPlayer.Plugins>
            <ads:AdSchedulerPlugin>
                <ads:AdSchedulerPlugin.Advertisements>

                    <ads:MidrollAdvertisement Time="00:00:05">
                        <ads:MidrollAdvertisement.Source>
                            <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_adpod.xml" Type="vast"/>
                        </ads:MidrollAdvertisement.Source>
                    </ads:MidrollAdvertisement>

                </ads:AdSchedulerPlugin.Advertisements>
            </ads:AdSchedulerPlugin>
            <ads:AdHandlerPlugin/>
        </mmppf:MediaPlayer.Plugins>
    </mmppf:MediaPlayer>

Дополнительные сведения о hello AdSchedulerPlugin см. в разделе [рекламу на hello платформа проигрывателя для Windows 8 и Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)

### <a name="adschedulingpage"></a>AdSchedulingPage
В этом примере также используется hello AdSchedulerPlugin. Он планирует воспроизведение трех рекламных объявлений: до, во время и после показа видео. Здравствуйте URI toohello vast-ФАЙЛ для каждого рекламного объявления, указанной в <RemoteAdSource> элемент.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:PrerollAdvertisement>
                                <ads:PrerollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:PrerollAdvertisement.Source>
                            </ads:PrerollAdvertisement>

                            <ads:MidrollAdvertisement Time="00:00:15">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                            <ads:PostrollAdvertisement>
                                <ads:PostrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml" Type="vast"/>
                                </ads:PostrollAdvertisement.Source>
                            </ads:PostrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>


### <a name="freewheelpage"></a>FreeWheelPage
Этот пример использует hello FreeWheelPlugin, который указывает исходный атрибут, который указывает URI, этот файл SmartXML tooa точки, определяет содержимое рекламы, а также сведения о планировании ad.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a>MastPage
Этот пример использует hello MastSchedulerPlugin, который позволяет вам toouse MAST-файл. Исходный атрибут Hello указывает расположение hello hello MAST-файла.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a>ProgrammaticAdPage
Этот образец программно взаимодействует с hello MediaPlayer. файл ProgrammaticAdPage.xaml Hello создает hello MediaPlayer:

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

файл ProgrammaticAdPage.xaml.cs Hello AdHandlerPlugin создает, добавляет TimelineMarker toospecify при ad должен быть отображен, а затем добавляет обработчик для события MarkerReached hello, которое загружает RemoteAdSource, указав URI tooa VAST-файл и затем играет Hello ad.

    public sealed partial class ProgrammaticAdPage : Microsoft.PlayerFramework.Samples.Common.LayoutAwarePage
        {
            AdHandlerPlugin adHandler;

            public ProgrammaticAdPage()
            {
                this.InitializeComponent();
                adHandler = new AdHandlerPlugin();
                player.Plugins.Add(new AdHandlerPlugin());
                player.Markers.Add(new TimelineMarker() { Time = TimeSpan.FromSeconds(5), Type = "myAd" });
                player.MarkerReached += pf_MarkerReached;
            }

            async void pf_MarkerReached(object sender, TimelineMarkerRoutedEventArgs e)
            {
                if (e.Marker.Type == "myAd")
                {
                    var adSource = new RemoteAdSource() { Type = VastAdPayloadHandler.AdType, Uri = new Uri("http://smf.blob.core.windows.net/samples/win8/ads/vast_linear.xml") };
                    //var adSource = new AdSource() { Type = DocumentAdPayloadHandler.AdType, Payload = SampleAdDocument };
                    var progress = new Progress<AdStatus>();
                    try
                    {
                        await player.PlayAd(adSource, progress, CancellationToken.None);
                    }
                    catch { /* ignore */ }
                }
            }

### <a name="scheduleclippage"></a>ScheduleClipPage
Этот пример использует tooschedule AdSchedulerPlugin hello ad воспроизводимой путем указания WMV-файл, содержащий hello ad.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.cloudapp.net/html5/media/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:AdSource Type="clip">
                                        <ads:AdSource.Payload>
                                            <ads:ClipAdPayload MediaSource="http://smf.blob.core.windows.net/samples/ads/media/XBOX_HD_DEMO_700_2_000_700_4x3.wmv" MimeType="video/x-ms-wmv" />
                                        </ads:AdSource.Payload>
                                    </ads:AdSource>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vastlinearcompanionpage"></a>VastLinearCompanionPage
В этом примере показано, как toouse hello AdSchedulerPlugin tooschedule воспроизводимой линейной рекламы с сопутствующей рекламой. Hello <RemoteAdSource> элемент определяет расположение hello hello VAST-файл.

    <mmppf:MediaPlayer Grid.Row="1"  x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear_companions.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vastlinearnonlinearpage"></a>VastLinearNonLinearPage
Этот пример использует hello AdSchedulerPlugin tooschedule линейная и Нелинейная реклама. Hello расположение VAST-файла, указанном с помощью hello <RemoteAdSource> элемента.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:AdSchedulerPlugin>
                        <ads:AdSchedulerPlugin.Advertisements>

                            <ads:MidrollAdvertisement Time="00:00:05">
                                <ads:MidrollAdvertisement.Source>
                                    <ads:RemoteAdSource Uri="http://smf.blob.core.windows.net/samples/win8/ads/vast_linear_nonlinear.xml" Type="vast"/>
                                </ads:MidrollAdvertisement.Source>
                            </ads:MidrollAdvertisement>

                        </ads:AdSchedulerPlugin.Advertisements>
                    </ads:AdSchedulerPlugin>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="vmappage"></a>VMAPPage
Это в примерах используется hello VmapSchedulerPlugin tooschedule рекламы посредством VMAP-файла. URI toohello Hello VMAP-файл указывается в hello исходного атрибута hello <VmapSchedulerPlugin> элемента.

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a>Реализация видеопроигрывателя с поддержкой рекламы для iOS
Hello Microsoft Media Platform: платформа проигрывателя для iOS содержит набор примеров приложений, которые показывают, как приложение видеопроигрывателя с помощью tooimplement hello framework. Можно загрузить образцы платформа проигрывателя и hello hello из [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework). Hello странице сайта github есть ссылка tooa вики-сайт, содержащий дополнительные сведения о платформе медиапроигрывателя hello и образце проигрывателя введение toohello: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).

### <a name="scheduling-ads-with-vmap"></a>Планирование рекламы с помощью VMAP
Следующий пример показывает как Hello tooschedule рекламы посредством VMAP-файла.

    // How tooschedule an Ad using VMAP.
    //First download hello VMAP manifest

    if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVMAP.xml"]])
            {
                [self logFrameworkError];
            }
            else
            {
                // Schedule a list of ads using hello downloaded VMAP manifest
                if (![framework scheduleVMAPWithManifest:manifest])
                {
                    [self logFrameworkError];
                }          
            }

### <a name="scheduling-ads-with-vast"></a>Планирование рекламы с помощью VAST
Hello следующем образце показано, как tooschedule позднего рекламу VAST привязки.

    //Example:3 How tooschedule a late binding VAST ad.
    // set hello start time for hello ad
    adLinearTime.startTime = 13;
    adLinearTime.duration = 0;
    // Specify hello URI of hello VAST file
    NSString *vastAd1=@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml";
    // Create an AdInfo object
     AdInfo *vastAdInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URL tooVAST file
    vastAdInfo1.clipURL = [NSURL URLWithString:vastAd1];
    // set running time of ad
    vastAdInfo1.mediaTime = [[[MediaTime alloc] init] autorelease];
    vastAdInfo1.mediaTime.clipBeginMediaTime = 0;
    vastAdInfo1.mediaTime.clipEndMediaTime = 10;
    vastAdInfo1.policy = @"policy for late binding VAST";
    // specify ad type
    vastAdInfo1.type = AdType_Midroll;
    vastAdInfo1.appendTo=-1;
    adIndex = 0;
    // schedule ad
    if (![framework scheduleClip:vastAdInfo1 atTime:adLinearTime forType:PlaylistEntryType_VAST andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

   Hello следующем образце показано, как tooschedule раннего связывания рекламу VAST.
Пример: 4 расписание файл раннего связывания рекламу VAST //Download hello vast-ФАЙЛ, если (! [[ framework.adResolver downloadManifest: & манифеста withURL: [NSURL URLWithString: @ «http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml»]]) {[собственный logFrameworkError];} else {adLinearTime.startTime = 7; adLinearTime.duration = 0;

        // Create AdInfo instance
        AdInfo *vastAdInfo2 = [[[AdInfo alloc] init] autorelease];
        vastAdInfo2.mediaTime = [[[MediaTime alloc] init] autorelease];
        vastAdInfo2.policy = @"policy for early binding VAST";
        // specify ad type
        vastAdInfo2.type = AdType_Midroll;
        vastAdInfo2.appendTo=-1;
        // schedule ad
        if (![framework scheduleVASTClip:vastAdInfo2 withManifest:manifest atTime:adLinearTime andGetClipId:&adIndex])
        {
            [self logFrameworkError];
        }
    }

Hello следующем образце показано, как tooinsert рекламы посредством грубой монтажа (RCE)

    //Example:1 How toouse RCE.
    // specify manifest for ad content
    NSString *secondContent=@"http://wamsblureg001orig-hs.cloudapp.net/6651424c-a9d1-419b-895c-6993f0f48a26/The%20making%20of%20Microsoft%20Surface-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";

    // specify ad length
    mediaTime.currentPlaybackPosition = 0;
    mediaTime.clipBeginMediaTime = 0;
    mediaTime.clipEndMediaTime = 80;
    // append ad content
    if (![framework appendContentClip:[NSURL URLWithString:secondContent] withMediaTime:mediaTime andGetClipId:&clipId])
    {
        [self logFrameworkError];
    }

Hello следующем примере показано, как tooschedule ad pod.

    //Example:5 Schedule an ad Pod.
    // Set start time for ad
    adLinearTime.startTime = 23;
    adLinearTime.duration = 0;

    // Specify URL toocontent
    NSString *adpodSt1=@"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    // Create an AdInfo instance
    AdInfo *adpodInfo1 = [[[AdInfo alloc] init] autorelease];
    // set URI tooad content
    adpodInfo1.clipURL = [NSURL URLWithString:adpodSt1];
    // Set ad running time
    adpodInfo1.mediaTime = [[[MediaTime alloc] init] autorelease];
    adpodInfo1.mediaTime.clipBeginMediaTime = 0;
    adpodInfo1.mediaTime.clipEndMediaTime = 17;
    adpodInfo1.policy = @"policy for ad pod 1";
    // Set ad type
    adpodInfo1.type = AdType_Midroll;
    adpodInfo1.appendTo=-1;
    adIndex = 0;
    // Schedule ad
    if (![framework scheduleClip:adpodInfo1 atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

Следующий пример показывает как Hello tooschedule одноразовая реклама рекламы в середине видео. Одноразовая реклама воспроизводится только после независимо от любого поиска hello выполняет средства просмотра.

    //Example:6 Schedule a single non sticky mid roll Ad
    // specify URL toocontent
    NSString *oneTimeAd=@"http://wamsblureg001orig-hs.cloudapp.net/5389c0c5-340f-48d7-90bc-0aab664e5f02/Windows%208_%20You%20and%20Me%20Together-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";

    // create an AdInfo instance
    AdInfo *oneTimeInfo = [[[AdInfo alloc] init] autorelease];
    // set URL of ad
    oneTimeInfo.clipURL = [NSURL URLWithString:oneTimeAd];
    oneTimeInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    oneTimeInfo.mediaTime.clipBeginMediaTime = 0;
    oneTimeInfo.mediaTime.clipEndMediaTime = -1;
    oneTimeInfo.policy = @"policy for one-time ad";
    // set ad start time
    adLinearTime.startTime = 43;
    adLinearTime.duration = 0;
    // set ad type
    oneTimeInfo.type = AdType_Midroll;
    // non sticky ad
    oneTimeInfo.deleteAfterPlayed = YES;
    // schedule ad
    if (![framework scheduleClip:oneTimeInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

Следующий пример показывает как Hello tooschedule многоразовая реклама рекламы в середине видео. Многоразовая реклама будет отображаться каждый раз, когда точка на временной шкале видео hello будет достигнуто заданное hello.

    //Example:7 Schedule a single sticky mid roll Ad
    NSString *stickyAd=@"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *stickyAdInfo = [[[AdInfo alloc] init] autorelease];
    // set URI tooad
    stickyAdInfo.clipURL = [NSURL URLWithString:stickyAd];
    stickyAdInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    stickyAdInfo.mediaTime.clipBeginMediaTime = 0;
    stickyAdInfo.mediaTime.clipEndMediaTime = 15;
    stickyAdInfo.policy = @"policy for sticky mid-roll ad";
    // set ad start time
    adLinearTime.startTime = 64;
    adLinearTime.duration = 0;
    // set ad type
    stickyAdInfo.type = AdType_Midroll;
    stickyAdInfo.deleteAfterPlayed = NO;
    // schedule ad
    if (![framework scheduleClip:stickyAdInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }


Hello следующем образце показано, как tooschedule ad воспроизводимой после видео.

    //Example:8 Schedule Post Roll Ad
    NSString *postAdURLString=@"http://wamsblureg001orig-hs.cloudapp.net/aa152d7f-3c54-487b-ba07-a58e0e33280b/wp-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    // create AdInfo instance
    AdInfo *postAdInfo = [[[AdInfo alloc] init] autorelease];
    postAdInfo.clipURL = [NSURL URLWithString:postAdURLString];
    postAdInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    postAdInfo.mediaTime.clipBeginMediaTime = 0;
    // set ad length
    postAdInfo.mediaTime.clipEndMediaTime = 45;
    postAdInfo.policy = @"policy for post-roll ad";
    // set ad type
    postAdInfo.type = AdType_Postroll;
    adLinearTime.duration = 0;
    if (![framework scheduleClip:postAdInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

Hello следующем образце показано, как tooschedule ad воспроизводимой перед видео.

    //Example:9 Schedule Pre Roll Ad
    NSString *adURLString = @"http://wamsblureg001orig-hs.cloudapp.net/2e4e7d1f-b72a-4994-a406-810c796fc4fc/The%20Surface%20Movement-m3u8-aapl.ism/Manifest(format=m3u8-aapl)";
    AdInfo *adInfo = [[[AdInfo alloc] init] autorelease];
    adInfo.clipURL = [NSURL URLWithString:adURLString];
    adInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    adInfo.mediaTime.currentPlaybackPosition = 0;
    adInfo.mediaTime.clipBeginMediaTime = 40; //You could play a portion of an Ad. Yeh!
    adInfo.mediaTime.clipEndMediaTime = 59;
    adInfo.policy = @"policy for pre-roll ad";
    adInfo.appendTo = -1;
    adInfo.type = AdType_Preroll;
    adLinearTime.duration = 0;
    // schedule ad
    if (![framework scheduleClip:adInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }

Следующий образец Hello показано, как tooschedule воспроизводимой наложения ad.

    // Example10: Schedule a Mid Roll overlay Ad
    NSString *adURLString = @"https://portalvhdsq3m25bf47d15c.blob.core.windows.net/asset-e47b43fd-05dc-4587-ac87-5916439ad07f/Windows%208_%20Cliffjumpers.mp4?st=2012-11-28T16%3A31%3A57Z&se=2014-11-28T16%3A31%3A57Z&sr=c&si=2a6dbb1e-f906-4187-a3d3-7e517192cbd0&sig=qrXYZBekqlbbYKqwovxzaVZNLv9cgyINgMazSCbdrfU%3D";
    //Create AdInfo instance
    AdInfo *adInfo = [[[AdInfo alloc] init] autorelease];
    adInfo.clipURL = [NSURL URLWithString:adURLString];
    adInfo.mediaTime = [[[MediaTime alloc] init] autorelease];
    adInfo.mediaTime.currentPlaybackPosition = 0;
    adInfo.mediaTime.clipBeginMediaTime = 0;
    // specify ad length
    adInfo.mediaTime.clipEndMediaTime = 20;
    adInfo.policy = @"policy for mid-roll overlay ad";
    adInfo.appendTo = -1;
    // specify ad type
    adInfo.type = AdType_Midroll;
    // specify ad start time & duration
    adLinearTime.startTime = 300;
    adLinearTime.duration = 20;
    // schedule ad            if (![framework scheduleClip:adInfo atTime:adLinearTime forType:PlaylistEntryType_Media andGetClipId:&adIndex])
    {
        [self logFrameworkError];
    }



## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>См. также
[Разработка приложений видеопроигрывателя](media-services-develop-video-players.md)

