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
# <a name="inserting-ads-on-hello-client-side"></a><span data-ttu-id="a847c-103">Вставка рекламы на стороне клиента hello</span><span class="sxs-lookup"><span data-stu-id="a847c-103">Inserting ads on hello client side</span></span>
<span data-ttu-id="a847c-104">Этот раздел содержит сведения о том, как tooinsert разных типов рекламы на стороне клиента hello.</span><span class="sxs-lookup"><span data-stu-id="a847c-104">This topic contains information on how tooinsert various types of ads on hello client side.</span></span>

<span data-ttu-id="a847c-105">Сведения о поддержке субтитров и рекламы в динамических потоковых видео см. в разделе [Вставка субтитров и рекламы](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span><span class="sxs-lookup"><span data-stu-id="a847c-105">For information about closed captioning and ad support in Live streaming videos, see [Supported Closed Captioning and Ad Insertion Standards](media-services-live-streaming-with-onprem-encoders.md#cc_and_ads).</span></span>

> [!NOTE]
> <span data-ttu-id="a847c-106">Проигрыватель мультимедиа Azure на данный момент не поддерживает рекламу.</span><span class="sxs-lookup"><span data-stu-id="a847c-106">Azure Media Player does not currently support Ads.</span></span>
> 
> 

## <span data-ttu-id="a847c-107"><a id="insert_ads_into_media"></a>Вставка рекламы в мультимедиа</span><span class="sxs-lookup"><span data-stu-id="a847c-107"><a id="insert_ads_into_media"></a>Inserting Ads into your Media</span></span>
<span data-ttu-id="a847c-108">Службы мультимедиа Azure обеспечивает поддержку вставки рекламы посредством hello Windows Media Platform: платформы проигрывателя.</span><span class="sxs-lookup"><span data-stu-id="a847c-108">Azure Media Services provides support for ad insertion through hello Windows Media Platform: Player Frameworks.</span></span> <span data-ttu-id="a847c-109">Платформы проигрывателя с поддержкой рекламы доступны для устройств Windows 8, Silverlight, Windows Phone 8 и iOS.</span><span class="sxs-lookup"><span data-stu-id="a847c-109">Player frameworks with ad support are available for Windows 8, Silverlight, Windows Phone 8, and iOS devices.</span></span> <span data-ttu-id="a847c-110">Каждая платформа проигрывателя содержит образец кода, которое показывает, как tooimplement приложение проигрывателя. Существует три вида рекламы, которые можно вставить в media: список.</span><span class="sxs-lookup"><span data-stu-id="a847c-110">Each player framework contains sample code that shows you how tooimplement a player application.There are three different kinds of ads you can insert into your media:list.</span></span>

* <span data-ttu-id="a847c-111">**Линейный** — полный кадр рекламы паузы hello основного видео.</span><span class="sxs-lookup"><span data-stu-id="a847c-111">**Linear** – full frame ads that pause hello main video.</span></span>
* <span data-ttu-id="a847c-112">**Нелинейный** – реклама, которая отображается поверх основного видео hello воспроизводится, обычно это логотип или другое статическое изображение размещается в проигрывателе hello.</span><span class="sxs-lookup"><span data-stu-id="a847c-112">**Nonlinear** – overlay ads that are displayed as hello main video is playing, usually a logo or other static image placed within hello player.</span></span>
* <span data-ttu-id="a847c-113">**Помощник по поиску** – реклама, которая отображается за пределами проигрывателя hello.</span><span class="sxs-lookup"><span data-stu-id="a847c-113">**Companion** – ads that are displayed outside of hello player.</span></span>

<span data-ttu-id="a847c-114">Рекламу можно размещать в любой точке временной шкалы основного видео hello.</span><span class="sxs-lookup"><span data-stu-id="a847c-114">Ads can be placed at any point in hello main video’s time line.</span></span> <span data-ttu-id="a847c-115">Необходимо сообщить hello проигрывателя при tooplay hello ad и который tooplay рекламы.</span><span class="sxs-lookup"><span data-stu-id="a847c-115">You must tell hello player when tooplay hello ad and which ads tooplay.</span></span> <span data-ttu-id="a847c-116">Для этого используется набор стандартных XML-файлов: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST) и Digital Video Player Ad Interface Definition (VPAID).</span><span class="sxs-lookup"><span data-stu-id="a847c-116">This is done using a set of standard XML-based files: Video Ad Service Template (VAST), Digital Video Multiple Ad Playlist (VMAP), Media Abstract Sequencing Template (MAST), and Digital Video Player Ad Interface Definition (VPAID).</span></span> <span data-ttu-id="a847c-117">VAST-файлы указывают, какие toodisplay рекламы.</span><span class="sxs-lookup"><span data-stu-id="a847c-117">VAST files specify what ads toodisplay.</span></span> <span data-ttu-id="a847c-118">VMAP-файлы указывают, когда tooplay различные рекламные ролики и содержат XML-код VAST.</span><span class="sxs-lookup"><span data-stu-id="a847c-118">VMAP files specify when tooplay various ads and contain VAST XML.</span></span> <span data-ttu-id="a847c-119">MAST-файлы являются другим способом toosequence рекламы, они также содержат XML-код VAST.</span><span class="sxs-lookup"><span data-stu-id="a847c-119">MAST files are another way toosequence ads which also can contain VAST XML.</span></span> <span data-ttu-id="a847c-120">VPAID-файлы определяют интерфейс между видеопроигрывателем hello и hello ad или на сервере ad.</span><span class="sxs-lookup"><span data-stu-id="a847c-120">VPAID files define an interface between hello video player and hello ad or ad server.</span></span>

<span data-ttu-id="a847c-121">Каждая платформа проигрывателя работает по-разному, и каждой из них посвящен отдельный раздел.</span><span class="sxs-lookup"><span data-stu-id="a847c-121">Each player framework works differently and each will be covered in its own topic.</span></span> <span data-ttu-id="a847c-122">В этом разделе описано hello базовый механизм tooinsert рекламы. Видеопроигрыватель приложения запрашивают рекламу с сервера рекламы.</span><span class="sxs-lookup"><span data-stu-id="a847c-122">This topic will describe hello basic mechanisms used tooinsert ads.Video player applications request ads from an ad server.</span></span> <span data-ttu-id="a847c-123">сервер Hello рекламы может ответить несколькими способами:</span><span class="sxs-lookup"><span data-stu-id="a847c-123">hello ad server can respond in a number of ways:</span></span>

* <span data-ttu-id="a847c-124">Вернуть VAST-файл</span><span class="sxs-lookup"><span data-stu-id="a847c-124">Return a VAST file</span></span>
* <span data-ttu-id="a847c-125">Вернуть VMAP-файл (с внедренным кодом VAST)</span><span class="sxs-lookup"><span data-stu-id="a847c-125">Return a VMAP file (with embedded VAST)</span></span>
* <span data-ttu-id="a847c-126">Вернуть MAST-файл (с внедренным кодом VAST)</span><span class="sxs-lookup"><span data-stu-id="a847c-126">Return a MAST file (with embedded VAST)</span></span>
* <span data-ttu-id="a847c-127">Вернуть VAST-файл с рекламными объявлениями VPAID</span><span class="sxs-lookup"><span data-stu-id="a847c-127">Return a VAST file with VPAID ads</span></span>

### <a name="using-a-video-ad-service-template-vast-file"></a><span data-ttu-id="a847c-128">Использование файла Video Ad Service Template (VAST)</span><span class="sxs-lookup"><span data-stu-id="a847c-128">Using a Video Ad Service Template (VAST) File</span></span>
<span data-ttu-id="a847c-129">VAST-файл определяет, какие ad или toodisplay рекламы.</span><span class="sxs-lookup"><span data-stu-id="a847c-129">A VAST file specifies what ad or ads toodisplay.</span></span> <span data-ttu-id="a847c-130">Hello следующий XML-код является примером VAST-файла для линейной рекламы:</span><span class="sxs-lookup"><span data-stu-id="a847c-130">hello following XML is an example of a VAST file for a linear ad:</span></span>

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

<span data-ttu-id="a847c-131">Hello линейная реклама описывается hello <**линейное**> элемент.</span><span class="sxs-lookup"><span data-stu-id="a847c-131">hello linear ad is described by hello <**Linear**> element.</span></span> <span data-ttu-id="a847c-132">Он определяет длительность hello hello ad, события отслеживания, при щелчке, отслеживание щелчков и количество **MediaFile** элементов.</span><span class="sxs-lookup"><span data-stu-id="a847c-132">It specifies hello duration of hello ad, tracking events, click through, click tracking, and a number of **MediaFile** elements.</span></span> <span data-ttu-id="a847c-133">События отслеживания указываются в hello <**TrackingEvents**> элемент и разрешить tootrack сервера ad различные события, происходящие во время просмотра hello ad.</span><span class="sxs-lookup"><span data-stu-id="a847c-133">Tracking events are specified within hello <**TrackingEvents**> element and allow an ad server tootrack various events that occur while viewing hello ad.</span></span> <span data-ttu-id="a847c-134">В этом случае hello начала, середины, завершения и разверните отслеживаются события.</span><span class="sxs-lookup"><span data-stu-id="a847c-134">In this case hello start, midpoint, complete, and expand events are tracked.</span></span> <span data-ttu-id="a847c-135">Hello начала событие возникает при отображении hello ad.</span><span class="sxs-lookup"><span data-stu-id="a847c-135">hello start event occurs when hello ad is displayed.</span></span> <span data-ttu-id="a847c-136">событие середины Hello возникает при по крайней мере просматривал 50% hello ad временной шкалы.</span><span class="sxs-lookup"><span data-stu-id="a847c-136">hello midpoint event occurs when at least 50% of hello ad’s timeline has been viewed.</span></span> <span data-ttu-id="a847c-137">событие завершения Hello возникает, когда hello ad toohello end.</span><span class="sxs-lookup"><span data-stu-id="a847c-137">hello complete event occurs when hello ad has run toohello end.</span></span> <span data-ttu-id="a847c-138">Hello развернуть событие возникает при hello пользователь разворачивает hello видеопроигрыватель toofull экрана.</span><span class="sxs-lookup"><span data-stu-id="a847c-138">hello Expand event occurs when hello user expands hello video player toofull screen.</span></span> <span data-ttu-id="a847c-139">Действие при щелчке указывается с <**с дополнительной информацией**> элемента <**VideoClicks**> элемент и указывает toodisplay ресурсов tooa URI, когда hello пользователь выбирает hello ad.</span><span class="sxs-lookup"><span data-stu-id="a847c-139">Clickthroughs are specified with a <**ClickThrough**> element within a <**VideoClicks**> element and specifies a URI tooa resource toodisplay when hello user clicks on hello ad.</span></span> <span data-ttu-id="a847c-140">Отслеживание щелчков указывается в <**отслеживание щелчков**> элемент также в hello <**VideoClicks**> элемент и задает ресурс отслеживания toorequest hello проигрывателя при нажатии пользователем hello на hello ad.hello <**MediaFile**> элементов укажите сведения о кодировке рекламы.</span><span class="sxs-lookup"><span data-stu-id="a847c-140">ClickTracking is specified in a <**ClickTracking**> element, also within hello <**VideoClicks**> element and specifies a tracking resource for hello player toorequest when hello user clicks on hello ad.hello <**MediaFile**> elements specify information about a specific encoding of an ad.</span></span> <span data-ttu-id="a847c-141">При наличии более чем одного <**MediaFile**> элемент, hello видеопроигрыватель может выбирать лучшую кодировку hello для платформы hello.</span><span class="sxs-lookup"><span data-stu-id="a847c-141">When there is more than one <**MediaFile**> element, hello video player can choose hello best encoding for hello platform.</span></span> 

<span data-ttu-id="a847c-142">Линейную рекламу можно отображать в указанном порядке.</span><span class="sxs-lookup"><span data-stu-id="a847c-142">Linear ads can be displayed in a specified order.</span></span> <span data-ttu-id="a847c-143">toodo это, добавьте дополнительные <Ad> элементы toohello VAST файла и укажите порядок hello, с помощью атрибута последовательности hello.</span><span class="sxs-lookup"><span data-stu-id="a847c-143">toodo this, add additional <Ad> elements toohello VAST file and specify hello order using hello sequence attribute.</span></span> <span data-ttu-id="a847c-144">Привет, в следующем примере показано следующее:</span><span class="sxs-lookup"><span data-stu-id="a847c-144">hello following example illustrates this:</span></span>

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

<span data-ttu-id="a847c-145">Нелинейная реклама также задается в элементе <Creative>.</span><span class="sxs-lookup"><span data-stu-id="a847c-145">Nonlinear ads are specified in a <Creative> element as well.</span></span> <span data-ttu-id="a847c-146">Следующий пример показывает Hello <Creative> элемент, описывающий нелинейную рекламу.</span><span class="sxs-lookup"><span data-stu-id="a847c-146">hello following example shows a <Creative> element that describes a nonlinear ad.</span></span>

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


<span data-ttu-id="a847c-147">Привет <**NonLinearAds**> может содержать один или несколько <**Нелинейная**> элементов, каждый из которых можно описать нелинейную рекламу.</span><span class="sxs-lookup"><span data-stu-id="a847c-147">hello <**NonLinearAds**> element can contain one or more <**NonLinear**> elements, each of which can describe a nonlinear ad.</span></span> <span data-ttu-id="a847c-148">Привет <**Нелинейная**> элемент указывает ресурс hello для hello нелинейную рекламу.</span><span class="sxs-lookup"><span data-stu-id="a847c-148">hello <**NonLinear**> element specifies hello resource for hello nonlinear ad.</span></span> <span data-ttu-id="a847c-149">Hello ресурс может быть <**StaticResouce**>, <**IFrameResource**>, или объект <**HTMLResouce**>.</span><span class="sxs-lookup"><span data-stu-id="a847c-149">hello resource can be a <**StaticResouce**>, an <**IFrameResource**>, or an <**HTMLResouce**>.</span></span><span data-ttu-id="a847c-150"> <**StaticResource**> описывает ресурс не на основе HTML и определяет атрибут creativeType, который указывает способ отображения hello ресурсов:</span><span class="sxs-lookup"><span data-stu-id="a847c-150"> <**StaticResource**> describes a non-HTML resource and defines a creativeType attribute that specifies how hello resource is displayed:</span></span>

<span data-ttu-id="a847c-151">Изображение/gif, изображение/jpeg, image/png — ресурс hello отображается в HTML-<**img**> тег.</span><span class="sxs-lookup"><span data-stu-id="a847c-151">Image/gif, image/jpeg, image/png – hello resource is displayed in an HTML <**img**> tag.</span></span>

<span data-ttu-id="a847c-152">Приложения/x-javascript — ресурс hello отображается в HTML-<**сценарий**> тег.</span><span class="sxs-lookup"><span data-stu-id="a847c-152">Application/x-javascript – hello resource is displayed in an HTML <**script**> tag.</span></span>

<span data-ttu-id="a847c-153">Приложения/x-shockwave-flash — ресурс hello отображается в проигрывателе Flash.</span><span class="sxs-lookup"><span data-stu-id="a847c-153">Application/x-shockwave-flash – hello resource is displayed in a Flash player.</span></span>

<span data-ttu-id="a847c-154">**IFrameResource** описывает ресурс HTML, который может быть отображен в IFrame.</span><span class="sxs-lookup"><span data-stu-id="a847c-154">**IFrameResource** describes an HTML resource that can be displayed in an IFrame.</span></span> <span data-ttu-id="a847c-155">**HTMLResource** описывает фрагмент HTML-кода, который может быть вставлен в веб-страницу.</span><span class="sxs-lookup"><span data-stu-id="a847c-155">**HTMLResource** describes a piece of HTML code that can be inserted into a web page.</span></span> <span data-ttu-id="a847c-156">**TrackingEvents** укажите события отслеживания и hello URI toorequest при возникновении события hello.</span><span class="sxs-lookup"><span data-stu-id="a847c-156">**TrackingEvents** specify tracking events and hello URI toorequest when hello event occurs.</span></span> <span data-ttu-id="a847c-157">В этом образце hello отслеживаются события acceptInvitation и сворачивания.</span><span class="sxs-lookup"><span data-stu-id="a847c-157">In this sample hello acceptInvitation and collapse events are tracked.</span></span> <span data-ttu-id="a847c-158">Дополнительные сведения о hello **NonLinearAds** элемента и его дочерних элементов в разделе IAB.NET/VAST.</span><span class="sxs-lookup"><span data-stu-id="a847c-158">For more information on hello **NonLinearAds** element and its children, see IAB.NET/VAST.</span></span> <span data-ttu-id="a847c-159">Обратите внимание, что hello **TrackingEvents** элемент находится в пределах hello **NonLinearAds** элемент, а не hello **Нелинейная** элемента.</span><span class="sxs-lookup"><span data-stu-id="a847c-159">Note that hello **TrackingEvents** element is located within hello **NonLinearAds** element rather than hello **NonLinear** element.</span></span>

<span data-ttu-id="a847c-160">Сопутствующая реклама задается в элементе <CompanionAds>.</span><span class="sxs-lookup"><span data-stu-id="a847c-160">Companion ads are defined within a <CompanionAds> element.</span></span> <span data-ttu-id="a847c-161">Hello <CompanionAds> элемент может содержать один или несколько <Companion> элементов.</span><span class="sxs-lookup"><span data-stu-id="a847c-161">hello <CompanionAds> element can contain one or more <Companion> elements.</span></span> <span data-ttu-id="a847c-162">Каждый <Companion> элемент описывает сопутствующую рекламу и может содержать <StaticResource>, <IFrameResource>, или <HTMLResource> которые указываются hello же способом, как и в нелинейную рекламу.</span><span class="sxs-lookup"><span data-stu-id="a847c-162">Each <Companion> element describes a companion ad and can contain a <StaticResource>, <IFrameResource>, or <HTMLResource> which are specified in hello same way as in a nonlinear ad.</span></span> <span data-ttu-id="a847c-163">VAST-файл может содержать несколько элементов сопутствующей рекламы и приложение hello проигрывателя можно выбрать наиболее подходящий ad toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="a847c-163">A VAST file can contain multiple companion ads and hello player application can choose hello most appropriate ad toodisplay.</span></span> <span data-ttu-id="a847c-164">Дополнительные сведения о VAST см. в разделе [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="a847c-164">For more information about VAST, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span>

### <a name="using-a-digital-video-multiple-ad-playlist-vmap-file"></a><span data-ttu-id="a847c-165">Использование файла Digital Video Multiple Ad Playlist (VMAP)</span><span class="sxs-lookup"><span data-stu-id="a847c-165">Using a Digital Video Multiple Ad Playlist (VMAP) File</span></span>
<span data-ttu-id="a847c-166">VMAP-файла позволяет toospecify при возникновении рекламных пауз, — продолжительность каждого разрыва, вмещает количество рекламных роликов в паузе и типы рекламы, которые могут отображаться во время приостановки выполнения.</span><span class="sxs-lookup"><span data-stu-id="a847c-166">A VMAP file allows you toospecify when ad breaks occur, how long each break is, how many ads can be displayed within a break, and what types of ads may be displayed during a break.</span></span> <span data-ttu-id="a847c-167">Hello в пример VMAP файла, который определяет одну рекламную паузу следующих:</span><span class="sxs-lookup"><span data-stu-id="a847c-167">hello following in an example VMAP file that defines a single ad break:</span></span>

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

<span data-ttu-id="a847c-168">VMAP-файл начинается с элемента <VMAP>, в котором содержатся один или несколько элементов <AdBreak>, каждый из которых определяет рекламную паузу.</span><span class="sxs-lookup"><span data-stu-id="a847c-168">A VMAP file begins with a <VMAP> element that contains one or more <AdBreak> elements, each defining an ad break.</span></span> <span data-ttu-id="a847c-169">Каждая рекламная пауза определяется типом паузы, идентификатором и смещение времени.</span><span class="sxs-lookup"><span data-stu-id="a847c-169">Each ad break specifies a break type, break ID, and time offset.</span></span> <span data-ttu-id="a847c-170">Hello атрибут breakType указывает тип hello ad, который может воспроизводиться во время паузы hello: линейная, Нелинейная или отображение.</span><span class="sxs-lookup"><span data-stu-id="a847c-170">hello breakType attribute specifies hello type of ad that can be played during hello break: linear, nonlinear, or display.</span></span> <span data-ttu-id="a847c-171">Объявления сопоставить tooVAST сопутствующей рекламы.</span><span class="sxs-lookup"><span data-stu-id="a847c-171">Display ads map tooVAST companion ads.</span></span> <span data-ttu-id="a847c-172">Можно указать несколько типов рекламы в списке, разделенном запятыми (без пробелов).</span><span class="sxs-lookup"><span data-stu-id="a847c-172">More than one ad type can be specified in a comma (no spaces) separated list.</span></span> <span data-ttu-id="a847c-173">Hello атрибут breakID является необязательным идентификатором для hello ad.</span><span class="sxs-lookup"><span data-stu-id="a847c-173">hello breakID is an optional identifier for hello ad.</span></span> <span data-ttu-id="a847c-174">Hello timeOffset указывает, когда должна отображаться hello ad.</span><span class="sxs-lookup"><span data-stu-id="a847c-174">hello timeOffset specifies when hello ad should be displayed.</span></span> <span data-ttu-id="a847c-175">Его можно указать одним из следующих способов hello.</span><span class="sxs-lookup"><span data-stu-id="a847c-175">It can be specified in one of hello following ways:</span></span>

1. <span data-ttu-id="a847c-176">Время в формате hh:mm:ss или hh:mm:ss.mmm, где .mmm — количество миллисекунд.</span><span class="sxs-lookup"><span data-stu-id="a847c-176">Time – in hh:mm:ss or hh:mm:ss.mmm format where .mmm is milliseconds.</span></span> <span data-ttu-id="a847c-177">значение этого атрибута Hello указывает hello времени с начала hello hello шкале видео toohello начала рекламной паузы hello.</span><span class="sxs-lookup"><span data-stu-id="a847c-177">hello value of this attribute specifies hello time from hello beginning of hello video timeline toohello beginning of hello ad break.</span></span>
2. <span data-ttu-id="a847c-178">Процент в формате n %, где n — процент hello tooplay шкале видео hello перед воспроизведением hello ad</span><span class="sxs-lookup"><span data-stu-id="a847c-178">Percentage – in n% format where n is hello percentage of hello video timeline tooplay before playing hello ad</span></span>
3. <span data-ttu-id="a847c-179">Начало/конец — указывает, что реклама должна воспроизводиться до или после hello видео</span><span class="sxs-lookup"><span data-stu-id="a847c-179">Start/End – specifies that an ad should be displayed before or after hello video has been displayed</span></span>
4. <span data-ttu-id="a847c-180">Position указывает порядок рекламных пауз hello при синхронизации hello hello рекламных пауз неизвестно, например потоковой трансляции.</span><span class="sxs-lookup"><span data-stu-id="a847c-180">Position – specifies hello order of ad breaks when hello timing of hello ad breaks is unknown, such as in live streaming.</span></span> <span data-ttu-id="a847c-181">Hello порядок каждой рекламной паузы задается в формате hello #n, где n — целое число больше или равно 1.</span><span class="sxs-lookup"><span data-stu-id="a847c-181">hello order of each ad break is specified in hello #n format where n is an integer 1 or greater.</span></span> <span data-ttu-id="a847c-182">1 означает hello рекламу следует воспроизводить при первой возможности hello, 2 означает hello рекламу следует воспроизводить при второй возможности hello и т. д.</span><span class="sxs-lookup"><span data-stu-id="a847c-182">1 signifies hello ad should be played at hello first opportunity, 2 signifies hello ad should be played at hello second opportunity and so on.</span></span>

<span data-ttu-id="a847c-183">В рамках hello <**AdBreak**> элемент может быть одним <**AdSource**> элемент.</span><span class="sxs-lookup"><span data-stu-id="a847c-183">Within hello <**AdBreak**> element there can be one <**AdSource**> element.</span></span> <span data-ttu-id="a847c-184">Привет <**AdSource**> элемент содержит hello следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="a847c-184">hello <**AdSource**> element contains hello following attributes:</span></span>

1. <span data-ttu-id="a847c-185">ID указывает идентификатор источника рекламы hello</span><span class="sxs-lookup"><span data-stu-id="a847c-185">Id – specifies an identifier for hello ad source</span></span>
2. <span data-ttu-id="a847c-186">allowMultipleAds — логическое значение, указывающее отображения несколько рекламных роликов во время рекламной паузы hello</span><span class="sxs-lookup"><span data-stu-id="a847c-186">allowMultipleAds – a Boolean value that specifies whether multiple ads can be displayed during hello ad break</span></span>
3. <span data-ttu-id="a847c-187">followRedirects — необязательное логическое значение, указывающее, следует принять при hello видеопроигрыватель перенаправляет внутри реакцию на рекламу</span><span class="sxs-lookup"><span data-stu-id="a847c-187">followRedirects – an optional Boolean value that specifies if hello video player should honor redirects within an ad response</span></span>

<span data-ttu-id="a847c-188">Привет <**AdSource**> элемент предоставляет hello проигрывателю встроенную реакцию на рекламу или ссылку tooan Active Directory: ответы.</span><span class="sxs-lookup"><span data-stu-id="a847c-188">hello <**AdSource**> element provides hello player an inline ad response or a reference tooan ad response.</span></span> <span data-ttu-id="a847c-189">Имя может содержать один из следующих элементов hello:</span><span class="sxs-lookup"><span data-stu-id="a847c-189">It can contain one of hello following elements:</span></span>

* <span data-ttu-id="a847c-190"><VASTAdData>Указывает, что рекламу VAST внедрена в VMAP-файл hello</span><span class="sxs-lookup"><span data-stu-id="a847c-190"><VASTAdData> indicates a VAST ad response is embedded within hello VMAP file</span></span>
* <span data-ttu-id="a847c-191"><AdTagURI> — URI, который ссылается на отклик на рекламу из другой системы;</span><span class="sxs-lookup"><span data-stu-id="a847c-191"><AdTagURI> a URI that references an ad response from another system</span></span>
* <span data-ttu-id="a847c-192"><CustomAdData> — произвольная строка, представляющая собой отклик, не имеющий отношения к VAST.</span><span class="sxs-lookup"><span data-stu-id="a847c-192"><CustomAdData> -an arbitrary string that respresents a non-VAST response</span></span>

<span data-ttu-id="a847c-193">В этом примере указывается встроенный отклик на рекламу с элементом <VASTAdData>, содержащим отклик на рекламу VAST.</span><span class="sxs-lookup"><span data-stu-id="a847c-193">In this example an in-line ad response is specified with a <VASTAdData> element that contains a VAST ad response.</span></span> <span data-ttu-id="a847c-194">Дополнительные сведения о hello см. другие элементы [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span><span class="sxs-lookup"><span data-stu-id="a847c-194">For more information about hello other elements, see [VMAP](http://www.iab.net/guidelines/508676/digitalvideo/vsuite/vmap).</span></span>

<span data-ttu-id="a847c-195">Привет <**AdBreak**> элемент также может содержать один <**TrackingEvents**> элемент.</span><span class="sxs-lookup"><span data-stu-id="a847c-195">hello <**AdBreak**> element can also contain one <**TrackingEvents**> element.</span></span> <span data-ttu-id="a847c-196">Привет <**TrackingEvents**> элемент позволяет tootrack hello начало или конец рекламной паузы или от того, произошла ли ошибка во время рекламной паузы hello.</span><span class="sxs-lookup"><span data-stu-id="a847c-196">hello <**TrackingEvents**> element allows you tootrack hello start or end of an ad break or whether an error occurred during hello ad break.</span></span> <span data-ttu-id="a847c-197">Привет <**TrackingEvents**> элемент содержит один или несколько <**отслеживания**> элементов, каждый из которых задает события отслеживания и URI отслеживания.</span><span class="sxs-lookup"><span data-stu-id="a847c-197">hello <**TrackingEvents**> element contains one or more <**Tracking**> elements, each of which specifies a tracking event and a tracking URI.</span></span> <span data-ttu-id="a847c-198">доступны следующие события отслеживания возможных Hello.</span><span class="sxs-lookup"><span data-stu-id="a847c-198">hello possible tracking events are:</span></span>

1. <span data-ttu-id="a847c-199">breakStart отслеживает начало рекламной паузы hello</span><span class="sxs-lookup"><span data-stu-id="a847c-199">breakStart – tracks hello beginning of an ad break</span></span>
2. <span data-ttu-id="a847c-200">breakEnd завершения hello отслеживания рекламной паузы</span><span class="sxs-lookup"><span data-stu-id="a847c-200">breakEnd – track hello completion of an ad break</span></span>
3. <span data-ttu-id="a847c-201">Error отслеживает ошибки, возникшей во время рекламной паузы hello</span><span class="sxs-lookup"><span data-stu-id="a847c-201">error – tracks an error that occurred during hello ad break</span></span>

<span data-ttu-id="a847c-202">Следующий пример Hello показан VMAP-файл, который задает события отслеживания</span><span class="sxs-lookup"><span data-stu-id="a847c-202">hello following example shows a VMAP file that specifies tracking events</span></span>

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

<span data-ttu-id="a847c-203">Дополнительные сведения о hello <**TrackingEvents**> элемента и его дочерних элементов в разделе http://iab.org/VMAP.pdf</span><span class="sxs-lookup"><span data-stu-id="a847c-203">For more information on hello <**TrackingEvents**> element and its children, see http://iab.org/VMAP.pdf</span></span>

### <a name="using-a-media-abstract-sequencing-template-mast-file"></a><span data-ttu-id="a847c-204">Использование файла Media Abstract Sequencing Template (MAST)</span><span class="sxs-lookup"><span data-stu-id="a847c-204">Using a Media Abstract Sequencing Template (MAST) File</span></span>
<span data-ttu-id="a847c-205">MAST-файла позволяет toospecify триггеры, которые определяют, когда будет воспроизводиться реклама.</span><span class="sxs-lookup"><span data-stu-id="a847c-205">A MAST file allows you toospecify triggers that define when an ad is displayed.</span></span> <span data-ttu-id="a847c-206">Hello ниже приведен пример MAST-файла, содержащего триггеры для рекламы, воспроизводимой видео pre, ad воспроизводимой и рекламы, воспроизводимой после видео.</span><span class="sxs-lookup"><span data-stu-id="a847c-206">hello following is an example MAST file that contains triggers for a pre roll ad, a mid-roll ad, and a post-roll ad.</span></span>

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



<span data-ttu-id="a847c-207">MAST-файл начинается с элемента **MAST**, в котором содержится один элемент **triggers**.</span><span class="sxs-lookup"><span data-stu-id="a847c-207">A MAST file begins with a **MAST** element that contains one **triggers** element.</span></span> <span data-ttu-id="a847c-208">Hello <triggers> элемент содержит один или несколько **триггер** элементы, которые определяют, когда должна воспроизводиться реклама.</span><span class="sxs-lookup"><span data-stu-id="a847c-208">hello <triggers> element contains one or more **trigger** elements that define when an ad should be played.</span></span> 

<span data-ttu-id="a847c-209">Hello **триггер** элемент содержит **startConditions** элемент, указывающий запуска tooplay ad.</span><span class="sxs-lookup"><span data-stu-id="a847c-209">hello **trigger** element contains a **startConditions** element which specify when an ad should begin tooplay.</span></span> <span data-ttu-id="a847c-210">Hello **startConditions** элемент содержит один или несколько <condition> элементов.</span><span class="sxs-lookup"><span data-stu-id="a847c-210">hello **startConditions** element contains one or more <condition> elements.</span></span> <span data-ttu-id="a847c-211">При каждой <condition> вычисляет tootrue триггер инициируется или вызывается, в зависимости от того, является ли hello <condition> внутри **startConditions** или **endConditions** элемент соответственно.</span><span class="sxs-lookup"><span data-stu-id="a847c-211">When each <condition> evaluates tootrue a trigger is initiated or revoked depending upon whether hello <condition> is contained within a **startConditions** or **endConditions** element respectively.</span></span> <span data-ttu-id="a847c-212">Если несколько <condition> используются элементы, они обрабатываются как неявное OR, любое условие, получающее tootrue вызовет tooinitiate hello триггера.</span><span class="sxs-lookup"><span data-stu-id="a847c-212">When multiple <condition> elements are present, they are treated as an implicit OR, any condition evaluating tootrue will cause hello trigger tooinitiate.</span></span> <span data-ttu-id="a847c-213">Элементы <condition> могут быть вложенными.</span><span class="sxs-lookup"><span data-stu-id="a847c-213"><condition> elements can be nested.</span></span> <span data-ttu-id="a847c-214">Если дочерний <condition> элементы заданы, они обрабатываются как неявное and., все условия должно оцениваться tootrue для tooinitiate hello триггера.</span><span class="sxs-lookup"><span data-stu-id="a847c-214">When child <condition> elements are preset, they are treated as an implicit AND, all conditions must evaluate tootrue for hello trigger tooinitiate.</span></span> <span data-ttu-id="a847c-215">Hello <condition> элемент содержит следующие атрибуты, определяющие условия hello hello:</span><span class="sxs-lookup"><span data-stu-id="a847c-215">hello <condition> element contains hello following attributes that define hello condition:</span></span> 

1. <span data-ttu-id="a847c-216">**Тип** — указывает тип hello условие, свойства или события</span><span class="sxs-lookup"><span data-stu-id="a847c-216">**type** – specifies hello type of condition, event or property</span></span>
2. <span data-ttu-id="a847c-217">**имя** — hello имя hello свойство или событие toobe, используемые при проверке</span><span class="sxs-lookup"><span data-stu-id="a847c-217">**name** – hello name of hello property or event toobe used during evaluation</span></span>
3. <span data-ttu-id="a847c-218">**значение** – значение, которое будет вычисляться свойство hello</span><span class="sxs-lookup"><span data-stu-id="a847c-218">**value** – hello value that a property will be evaluated against</span></span>
4. <span data-ttu-id="a847c-219">**оператор** — hello toouse операции во время вычисления: EQ (равно), NEQ (не равно), GTR (больше), GEQ (больше или равно), LT (меньше), LEQ (меньше или равно), MOD (остаток от деления)</span><span class="sxs-lookup"><span data-stu-id="a847c-219">**operator** – hello operation toouse during evaluation: EQ (equal), NEQ (not equal), GTR (greater), GEQ (greater or equal), LT (Less than), LEQ (less than or equal), MOD (modulo)</span></span>

<span data-ttu-id="a847c-220">В **endConditions** также содержатся элементы <condition>.</span><span class="sxs-lookup"><span data-stu-id="a847c-220">**endConditions** also contain <condition> elements.</span></span> <span data-ttu-id="a847c-221">Если условие триггера hello tootrue — reset.hello <trigger> элемент также содержит <sources> элемент, который содержит один или несколько <source> элементов.</span><span class="sxs-lookup"><span data-stu-id="a847c-221">When a condition evaluates tootrue hello trigger is reset.hello <trigger> element also contains a <sources> element that contains one or more <source> elements.</span></span> <span data-ttu-id="a847c-222">Hello <source> элементы определяют toohello ad hello URI ответа и hello тип ответа ad.</span><span class="sxs-lookup"><span data-stu-id="a847c-222">hello <source> elements define hello URI toohello ad response and hello type of ad response.</span></span> <span data-ttu-id="a847c-223">В этом примере приведен URI tooa реакции VAST.</span><span class="sxs-lookup"><span data-stu-id="a847c-223">In this example a URI is given tooa VAST response.</span></span> 

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


### <a name="using-video-player-ad-interface-definition-vpaid"></a><span data-ttu-id="a847c-224">Использование Video Player-Ad Interface Definition (VPAID)</span><span class="sxs-lookup"><span data-stu-id="a847c-224">Using Video Player-Ad Interface Definition (VPAID)</span></span>
<span data-ttu-id="a847c-225">VPAID — это API для включения toocommunicate единицы исполняемая реклама с видеопроигрывателем.</span><span class="sxs-lookup"><span data-stu-id="a847c-225">VPAID is an API for enabling executable ad units toocommunicate with a video player.</span></span> <span data-ttu-id="a847c-226">Это позволяет создавать рекламу с высокой степенью интерактивности.</span><span class="sxs-lookup"><span data-stu-id="a847c-226">This allows highly interactive ad experiences.</span></span> <span data-ttu-id="a847c-227">Hello пользователь может взаимодействовать с hello ad и hello реклама может отвечать tooactions выполняемое просмотра hello.</span><span class="sxs-lookup"><span data-stu-id="a847c-227">hello user can interact with hello ad and hello ad can respond tooactions taken by hello viewer.</span></span> <span data-ttu-id="a847c-228">Например, в рекламе могут отображаться кнопки, позволяющие tooview пользователя hello Дополнительные сведения или более длительную версию рекламы hello.</span><span class="sxs-lookup"><span data-stu-id="a847c-228">For example an ad may display buttons that allow hello user tooview more information or a longer version of hello ad.</span></span> <span data-ttu-id="a847c-229">Hello видеопроигрыватель должен поддерживать VPAID API hello и hello исполняемая реклама должна реализовывать интерфейс API hello.</span><span class="sxs-lookup"><span data-stu-id="a847c-229">hello video player must support hello VPAID API and hello executable ad must implement hello API.</span></span> <span data-ttu-id="a847c-230">Когда проигрыватель запрашивает рекламу с сервера hello сервер рекламы может ответить реакцией VAST, которая содержит рекламу vpaid.</span><span class="sxs-lookup"><span data-stu-id="a847c-230">When a player requests an ad from an ad server hello server may respond with a VAST response that contains a VPAID ad.</span></span>

<span data-ttu-id="a847c-231">Исполняемая реклама создается в коде, который должен выполняться в среде выполнения, например Adobe Flash ™ или JavaScript, способной функционировать в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="a847c-231">An executable ad is created in code that must be executed in a runtime environment such as Adobe Flash™ or JavaScript that can be executed in a web browser.</span></span> <span data-ttu-id="a847c-232">Когда сервер рекламы возвращает реакцию VAST, содержащую РЕКЛАМУ vpaid, hello значение атрибута apiFramework hello в hello <MediaFile> элемент должен быть «VPAID».</span><span class="sxs-lookup"><span data-stu-id="a847c-232">When an ad server returns a VAST response containing a VPAID ad, hello value of hello apiFramework attribute in hello <MediaFile> element must be “VPAID”.</span></span> <span data-ttu-id="a847c-233">Этот атрибут указывает, что данного рекламного объявления hello содержится является исполняемой рекламой VPAID.</span><span class="sxs-lookup"><span data-stu-id="a847c-233">This attribute specifies that hello contained ad is a VPAID executable ad.</span></span> <span data-ttu-id="a847c-234">Hello типа атрибут должен быть задан тип MIME toohello hello исполняемый файл, например «application/x-shockwave-flash» или «application/x-javascript».</span><span class="sxs-lookup"><span data-stu-id="a847c-234">hello type attribute must be set toohello MIME type of hello executable, such as “application/x-shockwave-flash” or “application/x-javascript”.</span></span> <span data-ttu-id="a847c-235">Hello следующем фрагменте кода XML показаны hello <MediaFile> элемент из реакции VAST, содержащий исполняемое объявление vpaid.</span><span class="sxs-lookup"><span data-stu-id="a847c-235">hello following XML snippet shows hello <MediaFile> element from a VAST response containing a VPAID executable ad.</span></span> 

    <MediaFiles>
       <MediaFile id="1" delivery="progressive" type=”application/x-shockwaveflash”
                  width=”640” height=”480” apiFramework=”VPAID”>
           <!-- CDATA wrapped URI tooexecutable ad -->
       </MediaFile>
    </MediaFiles>


<span data-ttu-id="a847c-236">Исполняемую рекламу можно инициализировать с помощью hello <AdParameters> элемент в пределах hello <Linear> или <NonLinear> элементов в реакции VAST.</span><span class="sxs-lookup"><span data-stu-id="a847c-236">An executable ad can be initialized using hello <AdParameters> element within hello <Linear> or <NonLinear> elements in a VAST response.</span></span> <span data-ttu-id="a847c-237">Дополнительные сведения о hello <AdParameters> элемент, в разделе [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span><span class="sxs-lookup"><span data-stu-id="a847c-237">For more information on hello <AdParameters> element, see [VAST 3.0](http://www.iab.net/media/file/VASTv3.0.pdf).</span></span> <span data-ttu-id="a847c-238">Дополнительные сведения об VPAID API hello см. в разделе [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span><span class="sxs-lookup"><span data-stu-id="a847c-238">For more information about hello VPAID API, see [VPAID 2.0](http://www.iab.net/media/file/VPAID_2.0_Final_04-10-2012.pdf).</span></span>

## <a name="implementing-a-windows-or-windows-phone-8-player-with-ad-support"></a><span data-ttu-id="a847c-239">Реализация проигрывателя Windows или Windows Phone 8 с поддержкой рекламы</span><span class="sxs-lookup"><span data-stu-id="a847c-239">Implementing a Windows or Windows Phone 8 Player with Ad Support</span></span>
<span data-ttu-id="a847c-240">Hello Microsoft Media Platform: платформа проигрывателя для Windows 8 и Windows Phone 8 содержит набор примеров приложений, которые показывают, как приложение видеопроигрывателя с помощью tooimplement hello framework.</span><span class="sxs-lookup"><span data-stu-id="a847c-240">hello Microsoft Media Platform: Player Framework for Windows 8 and Windows Phone 8 contains a collection of sample applications that show you how tooimplement a video player application using hello framework.</span></span> <span data-ttu-id="a847c-241">Можно загрузить образцы платформа проигрывателя и hello hello из [платформа проигрывателя для Windows 8 и Windows Phone 8](https://playerframework.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="a847c-241">You can download hello Player Framework and hello samples from [Player Framework for Windows 8 and Windows Phone 8](https://playerframework.codeplex.com).</span></span>

<span data-ttu-id="a847c-242">При открытии решения Microsoft.PlayerFramework.Xaml.Samples hello вы увидите несколько папок в рамках проекта hello.</span><span class="sxs-lookup"><span data-stu-id="a847c-242">When you open hello Microsoft.PlayerFramework.Xaml.Samples solution you will see a number of folders within hello project.</span></span> <span data-ttu-id="a847c-243">Hello в папке Advertising содержится hello образец кода соответствующей toocreating видеопроигрывателя с поддержкой рекламы.</span><span class="sxs-lookup"><span data-stu-id="a847c-243">hello Advertising folder contains hello sample code relevant toocreating a video player with ad support.</span></span> <span data-ttu-id="a847c-244">В папке Advertising hello внутри имеет ряд XAML/cs файлы каждый из которых Показать как tooinsert рекламы по-разному.</span><span class="sxs-lookup"><span data-stu-id="a847c-244">Inside hello Advertising folder is a number of XAML/cs files each of which show how tooinsert ads in a different way.</span></span> <span data-ttu-id="a847c-245">После списка Hello описаны:</span><span class="sxs-lookup"><span data-stu-id="a847c-245">hello following list describes each:</span></span>

* <span data-ttu-id="a847c-246">AdPodPage.xaml показано, как toodisplay ad pod.</span><span class="sxs-lookup"><span data-stu-id="a847c-246">AdPodPage.xaml Shows how toodisplay an ad pod.</span></span>
* <span data-ttu-id="a847c-247">Показывает AdSchedulingPage.xaml как tooschedule рекламы.</span><span class="sxs-lookup"><span data-stu-id="a847c-247">AdSchedulingPage.xaml Shows how tooschedule ads.</span></span>
* <span data-ttu-id="a847c-248">FreeWheelPage.xaml показано, как toouse hello рекламы tooschedule подключаемого модуля FreeWheel.</span><span class="sxs-lookup"><span data-stu-id="a847c-248">FreeWheelPage.xaml Shows how toouse hello FreeWheel plugin tooschedule ads.</span></span>
* <span data-ttu-id="a847c-249">Показывает MastPage.xaml как tooschedule рекламы с помощью MAST-файл.</span><span class="sxs-lookup"><span data-stu-id="a847c-249">MastPage.xaml Shows how tooschedule ads with a MAST file.</span></span>
* <span data-ttu-id="a847c-250">ProgrammaticAdPage.xaml показано, как tooprogrammatically планирование рекламы в видео.</span><span class="sxs-lookup"><span data-stu-id="a847c-250">ProgrammaticAdPage.xaml Shows how tooprogrammatically schedule ads into a video.</span></span>
* <span data-ttu-id="a847c-251">Показывает ScheduleClipPage.xaml как tooschedule рекламы без VAST-файл.</span><span class="sxs-lookup"><span data-stu-id="a847c-251">ScheduleClipPage.xaml Shows how tooschedule an ad without a VAST file.</span></span>
* <span data-ttu-id="a847c-252">Показывает VastLinearCompanionPage.xaml как tooinsert линейной и сопутствующей рекламы.</span><span class="sxs-lookup"><span data-stu-id="a847c-252">VastLinearCompanionPage.xaml Shows how tooinsert a linear and companion ad.</span></span>
* <span data-ttu-id="a847c-253">Показывает VastNonLinearPage.xaml как tooinsert нелинейной рекламы.</span><span class="sxs-lookup"><span data-stu-id="a847c-253">VastNonLinearPage.xaml Shows how tooinsert a non-linear ad.</span></span>
* <span data-ttu-id="a847c-254">Показывает VmapPage.xaml как toospecify рекламы с помощью VMAP-файл.</span><span class="sxs-lookup"><span data-stu-id="a847c-254">VmapPage.xaml Shows how toospecify ads with a VMAP file.</span></span>

<span data-ttu-id="a847c-255">Каждый из этих примеров используется класс MediaPlayer hello, определенные платформой проигрывателя hello.</span><span class="sxs-lookup"><span data-stu-id="a847c-255">Each of these samples uses hello MediaPlayer class defined by hello player framework.</span></span> <span data-ttu-id="a847c-256">В большинстве образцов используются подключаемые модули, которые обеспечивают поддержку различных форматов откликов.</span><span class="sxs-lookup"><span data-stu-id="a847c-256">Most samples use plugins that add support for various ad response formats.</span></span> <span data-ttu-id="a847c-257">Образец Hello ProgrammaticAdPage программно взаимодействует с экземпляром MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="a847c-257">hello ProgrammaticAdPage sample programmatically interacts with a MediaPlayer instance.</span></span>

### <a name="adpodpage-sample"></a><span data-ttu-id="a847c-258">Образец AdPodPage</span><span class="sxs-lookup"><span data-stu-id="a847c-258">AdPodPage Sample</span></span>
<span data-ttu-id="a847c-259">В этом образце используется hello AdSchedulerPlugin toodefine при toodisplay ad.</span><span class="sxs-lookup"><span data-stu-id="a847c-259">This sample uses hello AdSchedulerPlugin toodefine when toodisplay an ad.</span></span> <span data-ttu-id="a847c-260">В этом примере объявления воспроизводимой — запланированных toobe воспроизводиться через 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="a847c-260">In this example a mid-roll advertisement is scheduled toobe played after 5 seconds.</span></span> <span data-ttu-id="a847c-261">Hello рекламы (группа toodisplay рекламы в порядке) задается в VAST-файл, возвращенный от сервера ad.</span><span class="sxs-lookup"><span data-stu-id="a847c-261">hello ad pod (a group of ads toodisplay in order) is specified in a VAST file returned from an ad server.</span></span> <span data-ttu-id="a847c-262">Hello URI toohello VAST-файл указывается в hello <RemoteAdSource> элемента.</span><span class="sxs-lookup"><span data-stu-id="a847c-262">hello URI toohello VAST file is specified in hello <RemoteAdSource> element.</span></span>

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

<span data-ttu-id="a847c-263">Дополнительные сведения о hello AdSchedulerPlugin см. в разделе [рекламу на hello платформа проигрывателя для Windows 8 и Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span><span class="sxs-lookup"><span data-stu-id="a847c-263">For more information about hello AdSchedulerPlugin, see [Advertising in hello Player Framework on Windows 8 and Windows Phone 8](http://playerframework.codeplex.com/wikipage?title=Advertising&referringTitle=Windows%208%20Player%20Documentation)</span></span>

### <a name="adschedulingpage"></a><span data-ttu-id="a847c-264">AdSchedulingPage</span><span class="sxs-lookup"><span data-stu-id="a847c-264">AdSchedulingPage</span></span>
<span data-ttu-id="a847c-265">В этом примере также используется hello AdSchedulerPlugin.</span><span class="sxs-lookup"><span data-stu-id="a847c-265">This sample also uses hello AdSchedulerPlugin.</span></span> <span data-ttu-id="a847c-266">Он планирует воспроизведение трех рекламных объявлений: до, во время и после показа видео.</span><span class="sxs-lookup"><span data-stu-id="a847c-266">It schedules three ads, a pre-roll ad, a mid-roll ad, and a post-roll ad.</span></span> <span data-ttu-id="a847c-267">Здравствуйте URI toohello vast-ФАЙЛ для каждого рекламного объявления, указанной в <RemoteAdSource> элемент.</span><span class="sxs-lookup"><span data-stu-id="a847c-267">hello URI toohello VAST for each ad is specified in a <RemoteAdSource> element.</span></span>

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


### <a name="freewheelpage"></a><span data-ttu-id="a847c-268">FreeWheelPage</span><span class="sxs-lookup"><span data-stu-id="a847c-268">FreeWheelPage</span></span>
<span data-ttu-id="a847c-269">Этот пример использует hello FreeWheelPlugin, который указывает исходный атрибут, который указывает URI, этот файл SmartXML tooa точки, определяет содержимое рекламы, а также сведения о планировании ad.</span><span class="sxs-lookup"><span data-stu-id="a847c-269">This sample uses hello FreeWheelPlugin which specifies a Source attribute that specifies a URI that points tooa SmartXML file that specifies ad content as well as ad scheduling information.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:FreeWheelPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/freewheel.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="mastpage"></a><span data-ttu-id="a847c-270">MastPage</span><span class="sxs-lookup"><span data-stu-id="a847c-270">MastPage</span></span>
<span data-ttu-id="a847c-271">Этот пример использует hello MastSchedulerPlugin, который позволяет вам toouse MAST-файл.</span><span class="sxs-lookup"><span data-stu-id="a847c-271">This sample uses hello MastSchedulerPlugin that allows you toouse a MAST file.</span></span> <span data-ttu-id="a847c-272">Исходный атрибут Hello указывает расположение hello hello MAST-файла.</span><span class="sxs-lookup"><span data-stu-id="a847c-272">hello Source attribute specifies hello location of hello MAST file.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:MastSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/mast.xml" />
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

### <a name="programmaticadpage"></a><span data-ttu-id="a847c-273">ProgrammaticAdPage</span><span class="sxs-lookup"><span data-stu-id="a847c-273">ProgrammaticAdPage</span></span>
<span data-ttu-id="a847c-274">Этот образец программно взаимодействует с hello MediaPlayer.</span><span class="sxs-lookup"><span data-stu-id="a847c-274">This sample programmatically interacts with hello MediaPlayer.</span></span> <span data-ttu-id="a847c-275">файл ProgrammaticAdPage.xaml Hello создает hello MediaPlayer:</span><span class="sxs-lookup"><span data-stu-id="a847c-275">hello ProgrammaticAdPage.xaml file instantiates hello MediaPlayer:</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>

<span data-ttu-id="a847c-276">файл ProgrammaticAdPage.xaml.cs Hello AdHandlerPlugin создает, добавляет TimelineMarker toospecify при ad должен быть отображен, а затем добавляет обработчик для события MarkerReached hello, которое загружает RemoteAdSource, указав URI tooa VAST-файл и затем играет Hello ad.</span><span class="sxs-lookup"><span data-stu-id="a847c-276">hello ProgrammaticAdPage.xaml.cs file creates an AdHandlerPlugin, adds a TimelineMarker toospecify when an ad should be displayed, and then adds a handler for hello MarkerReached event which loads a RemoteAdSource specifying a URI tooa VAST file, and then plays hello ad.</span></span>

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

### <a name="scheduleclippage"></a><span data-ttu-id="a847c-277">ScheduleClipPage</span><span class="sxs-lookup"><span data-stu-id="a847c-277">ScheduleClipPage</span></span>
<span data-ttu-id="a847c-278">Этот пример использует tooschedule AdSchedulerPlugin hello ad воспроизводимой путем указания WMV-файл, содержащий hello ad.</span><span class="sxs-lookup"><span data-stu-id="a847c-278">This sample uses hello AdSchedulerPlugin tooschedule a mid-roll ad by specifying a .wmv file that contains hello ad.</span></span>

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

### <a name="vastlinearcompanionpage"></a><span data-ttu-id="a847c-279">VastLinearCompanionPage</span><span class="sxs-lookup"><span data-stu-id="a847c-279">VastLinearCompanionPage</span></span>
<span data-ttu-id="a847c-280">В этом примере показано, как toouse hello AdSchedulerPlugin tooschedule воспроизводимой линейной рекламы с сопутствующей рекламой.</span><span class="sxs-lookup"><span data-stu-id="a847c-280">This sample illustrates how toouse hello AdSchedulerPlugin tooschedule a mid-roll linear ad with an companion ad.</span></span> <span data-ttu-id="a847c-281">Hello <RemoteAdSource> элемент определяет расположение hello hello VAST-файл.</span><span class="sxs-lookup"><span data-stu-id="a847c-281">hello <RemoteAdSource> element specifies hello location of hello VAST file.</span></span>

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

### <a name="vastlinearnonlinearpage"></a><span data-ttu-id="a847c-282">VastLinearNonLinearPage</span><span class="sxs-lookup"><span data-stu-id="a847c-282">VastLinearNonLinearPage</span></span>
<span data-ttu-id="a847c-283">Этот пример использует hello AdSchedulerPlugin tooschedule линейная и Нелинейная реклама.</span><span class="sxs-lookup"><span data-stu-id="a847c-283">This sample uses hello AdSchedulerPlugin tooschedule a linear and a non-linear ad.</span></span> <span data-ttu-id="a847c-284">Hello расположение VAST-файла, указанном с помощью hello <RemoteAdSource> элемента.</span><span class="sxs-lookup"><span data-stu-id="a847c-284">hello VAST file location is specified with hello <RemoteAdSource> element.</span></span>

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

### <a name="vmappage"></a><span data-ttu-id="a847c-285">VMAPPage</span><span class="sxs-lookup"><span data-stu-id="a847c-285">VMAPPage</span></span>
<span data-ttu-id="a847c-286">Это в примерах используется hello VmapSchedulerPlugin tooschedule рекламы посредством VMAP-файла.</span><span class="sxs-lookup"><span data-stu-id="a847c-286">This samples uses hello VmapSchedulerPlugin tooschedule ads using a VMAP file.</span></span> <span data-ttu-id="a847c-287">URI toohello Hello VMAP-файл указывается в hello исходного атрибута hello <VmapSchedulerPlugin> элемента.</span><span class="sxs-lookup"><span data-stu-id="a847c-287">hello URI toohello VMAP file is specified in hello Source attribute of hello <VmapSchedulerPlugin> element.</span></span>

    <mmppf:MediaPlayer x:Name="player" Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4">
                <mmppf:MediaPlayer.Plugins>
                    <ads:VmapSchedulerPlugin Source="http://smf.blob.core.windows.net/samples/win8/ads/vmap.xml"/>
                    <ads:AdHandlerPlugin/>
                </mmppf:MediaPlayer.Plugins>
            </mmppf:MediaPlayer>

## <a name="implementing-an-ios-video-player-with-ad-support"></a><span data-ttu-id="a847c-288">Реализация видеопроигрывателя с поддержкой рекламы для iOS</span><span class="sxs-lookup"><span data-stu-id="a847c-288">Implementing an iOS Video Player with Ad Support</span></span>
<span data-ttu-id="a847c-289">Hello Microsoft Media Platform: платформа проигрывателя для iOS содержит набор примеров приложений, которые показывают, как приложение видеопроигрывателя с помощью tooimplement hello framework.</span><span class="sxs-lookup"><span data-stu-id="a847c-289">hello Microsoft Media Platform: Player Framework for iOS contains a collection of sample applications that show you how tooimplement a video player application using hello framework.</span></span> <span data-ttu-id="a847c-290">Можно загрузить образцы платформа проигрывателя и hello hello из [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="a847c-290">You can download hello Player Framework and hello samples from [Azure Media Player Framework](https://github.com/Azure/azure-media-player-framework).</span></span> <span data-ttu-id="a847c-291">Hello странице сайта github есть ссылка tooa вики-сайт, содержащий дополнительные сведения о платформе медиапроигрывателя hello и образце проигрывателя введение toohello: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span><span class="sxs-lookup"><span data-stu-id="a847c-291">hello github page has a link tooa Wiki that contains additional information on hello player framework and an introduction toohello player sample: [Azure Media Player Wiki](https://github.com/Azure/azure-media-player-framework/wiki/How-to-use-Azure-media-player-framework).</span></span>

### <a name="scheduling-ads-with-vmap"></a><span data-ttu-id="a847c-292">Планирование рекламы с помощью VMAP</span><span class="sxs-lookup"><span data-stu-id="a847c-292">Scheduling Ads with VMAP</span></span>
<span data-ttu-id="a847c-293">Следующий пример показывает как Hello tooschedule рекламы посредством VMAP-файла.</span><span class="sxs-lookup"><span data-stu-id="a847c-293">hello following example shows how tooschedule ads using a VMAP file.</span></span>

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

### <a name="scheduling-ads-with-vast"></a><span data-ttu-id="a847c-294">Планирование рекламы с помощью VAST</span><span class="sxs-lookup"><span data-stu-id="a847c-294">Scheduling Ads with VAST</span></span>
<span data-ttu-id="a847c-295">Hello следующем образце показано, как tooschedule позднего рекламу VAST привязки.</span><span class="sxs-lookup"><span data-stu-id="a847c-295">hello following sample shows how tooschedule a late binding VAST ad.</span></span>

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

   <span data-ttu-id="a847c-296">Hello следующем образце показано, как tooschedule раннего связывания рекламу VAST.</span><span class="sxs-lookup"><span data-stu-id="a847c-296">hello following sample shows how tooschedule an early binding VAST ad.</span></span>
<span data-ttu-id="a847c-297">Пример: 4 расписание файл раннего связывания рекламу VAST //Download hello vast-ФАЙЛ, если (! [[ framework.adResolver downloadManifest: & манифеста withURL: [NSURL URLWithString: @ «http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml»]]) {[собственный logFrameworkError];} else {adLinearTime.startTime = 7; adLinearTime.duration = 0;</span><span class="sxs-lookup"><span data-stu-id="a847c-297">//Example:4 Schedule an early binding VAST ad //Download hello VAST file if (![framework.adResolver downloadManifest:&manifest withURL:[NSURL URLWithString:@"http://portalvhdsq3m25bf47d15c.blob.core.windows.net/vast/PlayerTestVAST.xml"]]) { [self logFrameworkError]; } else { adLinearTime.startTime = 7; adLinearTime.duration = 0;</span></span>

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

<span data-ttu-id="a847c-298">Hello следующем образце показано, как tooinsert рекламы посредством грубой монтажа (RCE)</span><span class="sxs-lookup"><span data-stu-id="a847c-298">hello following sample shows how tooinsert an ad using Rough Cut Editing (RCE)</span></span>

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

<span data-ttu-id="a847c-299">Hello следующем примере показано, как tooschedule ad pod.</span><span class="sxs-lookup"><span data-stu-id="a847c-299">hello following example shows how tooschedule an ad pod.</span></span>

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

<span data-ttu-id="a847c-300">Следующий пример показывает как Hello tooschedule одноразовая реклама рекламы в середине видео.</span><span class="sxs-lookup"><span data-stu-id="a847c-300">hello following example shows how tooschedule a non-sticky mid-roll ad.</span></span> <span data-ttu-id="a847c-301">Одноразовая реклама воспроизводится только после независимо от любого поиска hello выполняет средства просмотра.</span><span class="sxs-lookup"><span data-stu-id="a847c-301">A non-sticky ad is only played once regardless of any seeking hello viewer performs.</span></span>

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

<span data-ttu-id="a847c-302">Следующий пример показывает как Hello tooschedule многоразовая реклама рекламы в середине видео.</span><span class="sxs-lookup"><span data-stu-id="a847c-302">hello following example shows how tooschedule a sticky mid-roll ad.</span></span> <span data-ttu-id="a847c-303">Многоразовая реклама будет отображаться каждый раз, когда точка на временной шкале видео hello будет достигнуто заданное hello.</span><span class="sxs-lookup"><span data-stu-id="a847c-303">A sticky ad will be displayed each time hello specified point on hello video timeline is reached.</span></span>

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


<span data-ttu-id="a847c-304">Hello следующем образце показано, как tooschedule ad воспроизводимой после видео.</span><span class="sxs-lookup"><span data-stu-id="a847c-304">hello following sample shows how tooschedule a post-roll ad.</span></span>

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

<span data-ttu-id="a847c-305">Hello следующем образце показано, как tooschedule ad воспроизводимой перед видео.</span><span class="sxs-lookup"><span data-stu-id="a847c-305">hello following sample shows how tooschedule a pre-roll ad.</span></span>

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

<span data-ttu-id="a847c-306">Следующий образец Hello показано, как tooschedule воспроизводимой наложения ad.</span><span class="sxs-lookup"><span data-stu-id="a847c-306">hello following sample shows how tooschedule a mid-roll overlay ad.</span></span>

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



## <a name="media-services-learning-paths"></a><span data-ttu-id="a847c-307">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="a847c-307">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a847c-308">Отзывы</span><span class="sxs-lookup"><span data-stu-id="a847c-308">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="a847c-309">См. также</span><span class="sxs-lookup"><span data-stu-id="a847c-309">See Also</span></span>
[<span data-ttu-id="a847c-310">Разработка приложений видеопроигрывателя</span><span class="sxs-lookup"><span data-stu-id="a847c-310">Develop video player applications</span></span>](media-services-develop-video-players.md)

