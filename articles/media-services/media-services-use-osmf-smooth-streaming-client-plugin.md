---
title: "aaaSmooth подключаемого модуля потоковой передачи для hello открытую платформу исходного носителя"
description: "Узнайте, как toouse hello Azure Media Services Smooth Streaming подключаемый модуль для hello Adobe открытую платформу исходного носителя."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6068151f-b6b0-4507-9346-f03416d3d572
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: 3cf8e4679279344cf79c3f0e5b28f63adf88179d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-microsoft-smooth-streaming-plugin-for-hello-adobe-open-source-media-framework"></a><span data-ttu-id="508b2-103">Как tooUse hello Microsoft Smooth Streaming подключаемого модуля для hello Adobe открытую платформу исходного носителя</span><span class="sxs-lookup"><span data-stu-id="508b2-103">How tooUse hello Microsoft Smooth Streaming Plugin for hello Adobe Open Source Media Framework</span></span>
## <a name="overview"></a><span data-ttu-id="508b2-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="508b2-104">Overview</span></span>
<span data-ttu-id="508b2-105">Здравствуйте подключаемый модуль Microsoft Smooth Streaming для Open Source Media Framework 2.0 (SS для OSMF) расширяет возможности по умолчанию hello OSMF и добавляет toonew воспроизведения содержимого Microsoft Smooth Streaming и OSMF существующие проигрыватели.</span><span class="sxs-lookup"><span data-stu-id="508b2-105">hello Microsoft Smooth Streaming plugin for Open Source Media Framework 2.0 (SS for OSMF) extends hello default capabilities of OSMF and adds Microsoft Smooth Streaming content playback toonew and existing OSMF players.</span></span> <span data-ttu-id="508b2-106">Подключаемый модуль Hello также добавляет Smooth Streaming воспроизведения возможности tooStrobe Media Playback (SMP).</span><span class="sxs-lookup"><span data-stu-id="508b2-106">hello plugin also adds Smooth Streaming playback capabilities tooStrobe Media Playback (SMP).</span></span>

<span data-ttu-id="508b2-107">SS для OSMF включает в себя две версии подключаемого модуля:</span><span class="sxs-lookup"><span data-stu-id="508b2-107">SS for OSMF includes two versions of plugin:</span></span>

* <span data-ttu-id="508b2-108">статический подключаемый модуль Smooth Streaming для OSMF (.swc);</span><span class="sxs-lookup"><span data-stu-id="508b2-108">Static Smooth Streaming plugin for OSMF (.swc)</span></span>
* <span data-ttu-id="508b2-109">динамический подключаемый модуль Smooth Streaming для OSMF (.swf).</span><span class="sxs-lookup"><span data-stu-id="508b2-109">Dynamic Smooth Streaming plugin for OSMF (.swf)</span></span>

<span data-ttu-id="508b2-110">Данный документ предполагает, что модуль чтения hello имеет общие опыт работы с OSMF и OSMF подключаемых модулей. Дополнительные сведения о OSMF, см. в разделе документации hello на hello [официальный сайт OSMF](http://osmf.org/).</span><span class="sxs-lookup"><span data-stu-id="508b2-110">This document assumes that hello reader has a general working knowledge of OSMF and OSMF plug-ins. For more information about OSMF, please see hello documentation on hello [official OSMF site](http://osmf.org/).</span></span>

### <a name="smooth-streaming-plugin-for-osmf-20"></a><span data-ttu-id="508b2-111">Подключаемый модуль Smooth Streaming для OSMF 2.0</span><span class="sxs-lookup"><span data-stu-id="508b2-111">Smooth Streaming plugin for OSMF 2.0</span></span>
<span data-ttu-id="508b2-112">Подключаемый модуль Hello поддерживает загрузки и воспроизведения Smooth Streaming содержимого по запросу с hello следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="508b2-112">hello plugin supports loading and playback of on-demand Smooth Streaming content with hello following features:</span></span>

* <span data-ttu-id="508b2-113">воспроизведение Smooth Streaming по запросу (воспроизведение, пауза, поиск, остановка);</span><span class="sxs-lookup"><span data-stu-id="508b2-113">On-demand Smooth Streaming playback (Play, Pause, Seek, Stop)</span></span>
* <span data-ttu-id="508b2-114">воспроизведение Smooth Streaming в реальном времени (воспроизведение);</span><span class="sxs-lookup"><span data-stu-id="508b2-114">Live Smooth Streaming playback (Play)</span></span>
* <span data-ttu-id="508b2-115">функции DVR в реальном времени (пауза, поиск, воспроизведение DVR, Go-to-Live);</span><span class="sxs-lookup"><span data-stu-id="508b2-115">Live DVR functions (Pause, Seek, DVR Playback, Go-to-Live)</span></span>
* <span data-ttu-id="508b2-116">поддержка видеокодеков H.264;</span><span class="sxs-lookup"><span data-stu-id="508b2-116">Support for video codecs - H.264</span></span>
* <span data-ttu-id="508b2-117">поддержка аудиокодеков AAC;</span><span class="sxs-lookup"><span data-stu-id="508b2-117">Support for Audio codecs - AAC</span></span>
* <span data-ttu-id="508b2-118">поддержка нескольких языков аудио с помощью встроенных API-интерфейсов OSMF;</span><span class="sxs-lookup"><span data-stu-id="508b2-118">Multiple audio language switching with OSMF built-in APIs</span></span>
* <span data-ttu-id="508b2-119">выбор качества воспроизведения с помощью встроенных API-интерфейсов OSMF;</span><span class="sxs-lookup"><span data-stu-id="508b2-119">Max playback quality selection with OSMF built-in APIs</span></span>
* <span data-ttu-id="508b2-120">боковые субтитры с использованием подключаемого модуля субтитров OSMF;</span><span class="sxs-lookup"><span data-stu-id="508b2-120">Sidecar closed captions with OSMF captions plugin</span></span>
* <span data-ttu-id="508b2-121">Adobe&reg; Flash&reg; Player 11.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="508b2-121">Adobe&reg; Flash&reg; Player 11.4 or higher.</span></span>
* <span data-ttu-id="508b2-122">Эта версия поддерживает только OSMF 2.0.</span><span class="sxs-lookup"><span data-stu-id="508b2-122">This version only supports OSMF 2.0.</span></span>

## <a name="supported-features-and-known-issues"></a><span data-ttu-id="508b2-123">Поддерживаемые функции и известные проблемы</span><span class="sxs-lookup"><span data-stu-id="508b2-123">Supported features and known issues</span></span>
<span data-ttu-id="508b2-124">Полный список поддерживаемых функций, неподдерживаемых функций и известных проблемах см. в разделе слишком[в этом документе](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span><span class="sxs-lookup"><span data-stu-id="508b2-124">For a full list of supported features, unsupported features and known issues, refer too[this document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span></span>

## <a name="loading-hello-plugin"></a><span data-ttu-id="508b2-125">Загрузка hello подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="508b2-125">Loading hello Plugin</span></span>
<span data-ttu-id="508b2-126">Подключаемые модули OSMF можно загружать статически (во время компиляции) или динамически (во время выполнения).</span><span class="sxs-lookup"><span data-stu-id="508b2-126">OSMF plugins can be loaded statically (at compile time) or dynamically (at run-time).</span></span> <span data-ttu-id="508b2-127">Hello подключаемый модуль Smooth Streaming для OSMF загрузки включает динамических и статических версии.</span><span class="sxs-lookup"><span data-stu-id="508b2-127">hello Smooth Streaming plugin for OSMF download includes both dynamic and static versions.</span></span>

* <span data-ttu-id="508b2-128">Статические загрузки: tooload статически, статическая библиотека (SWC) является обязательным.</span><span class="sxs-lookup"><span data-stu-id="508b2-128">Static loading: tooload statically, a static library (SWC) file is required.</span></span> <span data-ttu-id="508b2-129">Статические подключаемые модули будут добавлены как ссылка toohello проекты и объединение внутри hello выходных файлов во время компиляции hello.</span><span class="sxs-lookup"><span data-stu-id="508b2-129">Static plugins are added as a reference toohello projects and merge inside hello final output file at hello compile time.</span></span>
* <span data-ttu-id="508b2-130">Динамическая загрузка: tooload динамически, предварительно скомпилированный файл (SWF) является обязательным.</span><span class="sxs-lookup"><span data-stu-id="508b2-130">Dynamic loading: tooload dynamically, a precompiled (SWF) file is required.</span></span> <span data-ttu-id="508b2-131">Динамические подключаемые модули загружаются в hello выполнения и не включены в выходные данные проекта hello.</span><span class="sxs-lookup"><span data-stu-id="508b2-131">Dynamic plugins are loaded in hello runtime and not included in hello project output.</span></span> <span data-ttu-id="508b2-132">(Выходные данные компиляции) Динамические подключаемые модули можно загрузить с использованием протоколов HTTP и FILE.</span><span class="sxs-lookup"><span data-stu-id="508b2-132">(Compiled output) Dynamic plugins can be loaded using HTTP and FILE protocols.</span></span>

<span data-ttu-id="508b2-133">Дополнительные сведения о статических и динамических загрузки. в разделе официальные hello [страница подключаемого модуля OSMF](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span><span class="sxs-lookup"><span data-stu-id="508b2-133">For more information on static and dynamic loading, see hello official [OSMF plugin page](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span></span>

### <a name="ss-for-osmf-static-loading"></a><span data-ttu-id="508b2-134">Динамическая загрузка SS для OSMF</span><span class="sxs-lookup"><span data-stu-id="508b2-134">SS for OSMF Static Loading</span></span>
<span data-ttu-id="508b2-135">Приведенный далее фрагмент кода Hello показано, как tooload hello SS подключаемого модуля для OSMF статически и воспроизведения видео basic с помощью класса OSMF MediaFactory.</span><span class="sxs-lookup"><span data-stu-id="508b2-135">hello code snippet below shows how tooload hello SS plugin for OSMF statically and play a basic video using OSMF MediaFactory class.</span></span> <span data-ttu-id="508b2-136">Перед включением hello SS для OSMF кода, убедитесь, что hello ссылку на проект включает статических подключаемого модуля «MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swc» hello.</span><span class="sxs-lookup"><span data-stu-id="508b2-136">Before including hello SS for OSMF code, please ensure that hello project reference includes hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" static plugin.</span></span>

```
package 
{

    import com.microsoft.azure.media.AdaptiveStreamingPluginInfo;

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;



    [SWF(width="1024", height="768", backgroundColor='#405050', frameRate="25")]
    public class TestPlayer extends Sprite
    {        
        public var _container:MediaContainer;
        public var _mediaFactory:DefaultMediaFactory;
        private var _mediaPlayerSprite:MediaPlayerSprite;


        public function TestPlayer( )
        {
            stage.quality = StageQuality.HIGH;

            initMediaPlayer();

        }

        private function initMediaPlayer():void
        {

            // Create hello container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);
            _mediaPlayerSprite.scaleMode = ScaleMode.NONE;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            //Adds hello container toohello stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add hello listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load hello plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;

            pluginResource = new PluginInfoResource(new AdaptiveStreamingPluginInfo( )); 
            _mediaFactory.loadPlugin( pluginResource ); 
        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // hello plugin is loaded successfully.
            // Your web server needs toohost a valid crossdomain.xml file tooallow plugin toodownload Smooth Streaming files.
        loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")

        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // hello plugin is failed tooload ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started tooload.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code toodeal with Player Ready when it is hit hello first load after a source is loaded. 

                    break;

                case MediaPlayerState.BUFFERING :

                    break;

                case  MediaPlayerState.PAUSED :
                    break;      
                // other states ...          
            }
        }

        private function onPlayerFailed(event:MediaErrorEvent) : void
        {
            // Media Player is failed .           
        }

        private function loadMediaSource(sourceURL : String):void 
        {
            // Take an URL of SmoothStreamingSource's manifest and add it toohello page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;

            // Add hello media element
            _mediaPlayerSprite.media = element;
        }     

    }
}
```


### <a name="ss-for-osmf-dynamic-loading"></a><span data-ttu-id="508b2-137">Динамическая загрузка SS для OSMF</span><span class="sxs-lookup"><span data-stu-id="508b2-137">SS for OSMF Dynamic Loading</span></span>
<span data-ttu-id="508b2-138">Приведенный далее фрагмент кода Hello показано, как tooload hello SS подключаемого модуля для OSMF динамически и воспроизведения видео basic с помощью класса OSMF MediaFactory hello.</span><span class="sxs-lookup"><span data-stu-id="508b2-138">hello code snippet below shows how tooload hello SS plugin for OSMF dynamically and play a basic video using hello OSMF MediaFactory class.</span></span> <span data-ttu-id="508b2-139">Перед включением hello SS для OSMF кода, скопируйте папку проекта toohello динамического подключаемого модуля «MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swf» hello, при tooload протоколу ФАЙЛ или скопировать в веб-сервер для загрузки HTTP.</span><span class="sxs-lookup"><span data-stu-id="508b2-139">Before including hello SS for OSMF code, copy hello "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" dynamic plugin toohello project folder if you want tooload using FILE protocol, or copy under a web server for HTTP load.</span></span> <span data-ttu-id="508b2-140">Нет необходимости tooinclude «MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swc», в ссылках проекта hello не существует.</span><span class="sxs-lookup"><span data-stu-id="508b2-140">There is no need tooinclude "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" in hello project references.</span></span>

<span data-ttu-id="508b2-141">пакет {</span><span class="sxs-lookup"><span data-stu-id="508b2-141">package {</span></span>

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;
    import flash.events.Event;
    import flash.system.Capabilities;


    //Sets hello size of hello SWF

    [SWF(width="1024", height="768", backgroundColor='#405050', frameRate="25")]
    public class TestPlayer extends Sprite
    {        
        public var _container:MediaContainer;
        public var _mediaFactory:DefaultMediaFactory;
        private var _mediaPlayerSprite:MediaPlayerSprite;


        public function TestPlayer( )
        {
            stage.quality = StageQuality.HIGH;
            initMediaPlayer();
        }

        private function initMediaPlayer():void
        {

            // Create hello container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);

            //Adds hello container toohello stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add hello listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load hello plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;
            var adaptiveStreamingPluginUrl:String;

            // Your dynamic plugin web server needs toohost a valid crossdomain.xml file tooallow loading plugins.

            adaptiveStreamingPluginUrl = "http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf";
            pluginResource = new URLResource(adaptiveStreamingPluginUrl);
            _mediaFactory.loadPlugin( pluginResource ); 

        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // hello plugin is loaded successfully.

            // Your web server needs toohost a valid crossdomain.xml file tooallow plugin toodownload Smooth Streaming files.

    loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")
        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // hello plugin is failed tooload ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started tooload.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code toodeal with Player Ready when it is hit hello first load after a source is loaded. 

                    break;

                case MediaPlayerState.BUFFERING :

                    break;

                case  MediaPlayerState.PAUSED :
                    break;      
                // other states ...          
            }
        }

        private function onPlayerFailed(event:MediaErrorEvent) : void
        {
            // Media Player is failed .           
        }

        private function loadMediaSource(sourceURL : String):void 
        {
            // Take an URL of SmoothStreamingSource's manifest and add it toohello page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            // Add hello media element
            _mediaPlayerSprite.media = element;
        }     

    }
<span data-ttu-id="508b2-142">}</span><span class="sxs-lookup"><span data-stu-id="508b2-142">}</span></span>

## <a name="strobe-media--playback-with-hello-ss-odmf-dynamic-plugin"></a><span data-ttu-id="508b2-143">Воспроизведение мультимедиа strobe hello SS динамического ODMF подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="508b2-143">Strobe Media  Playback with hello SS ODMF Dynamic Plugin</span></span>
<span data-ttu-id="508b2-144">Hello Smooth Streaming для динамической подключаемого модуля OSMF совместима с [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span><span class="sxs-lookup"><span data-stu-id="508b2-144">hello Smooth Streaming for OSMF dynamic plugin is compatible with [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span></span> <span data-ttu-id="508b2-145">Hello SS можно использовать для OSMF подключаемый модуль tooadd Smooth Streaming воспроизведения содержимого tooSMP.</span><span class="sxs-lookup"><span data-stu-id="508b2-145">You can use hello SS for OSMF plugin tooadd Smooth Streaming content playback tooSMP.</span></span> <span data-ttu-id="508b2-146">toodo, копия «MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf» в веб-сервер для нагрузки HTTP с помощью hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="508b2-146">toodo this, copy "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" under a web server for HTTP load using hello following steps:</span></span>

1. <span data-ttu-id="508b2-147">Обзор hello [страница установки Strobe Media Playback](http://osmf.org/dev/2.0gm/setup.html).</span><span class="sxs-lookup"><span data-stu-id="508b2-147">Browse hello [Strobe Media Playback setup page](http://osmf.org/dev/2.0gm/setup.html).</span></span> 
2. <span data-ttu-id="508b2-148">Задать источник hello src tooa Smooth Streaming (например http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span><span class="sxs-lookup"><span data-stu-id="508b2-148">Set hello src tooa Smooth Streaming source, (e.g. http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span></span> 
3. <span data-ttu-id="508b2-149">Вносить изменения в конфигурацию требуемого hello и нажмите кнопку просмотра и обновления.</span><span class="sxs-lookup"><span data-stu-id="508b2-149">Make hello desired configuration changes and click Preview and Update.</span></span>
   
   <span data-ttu-id="508b2-150">**Примечание.** На веб-сервере должен размещаться допустимый файл crossdomain.xml.</span><span class="sxs-lookup"><span data-stu-id="508b2-150">**Note** Your content web server needs a valid crossdomain.xml.</span></span> 
4. <span data-ttu-id="508b2-151">Скопируйте и вставьте hello кода tooa простой HTML-страницу с помощью предпочитаемого текстового редактора, например, в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="508b2-151">Copy and paste hello code tooa simple HTML page using your favorite text editor, such as in hello following example:</span></span>

        <html>
        <body>
        <object width="920" height="640"> 
        <param name="movie" value="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf"></param>
        <param name="flashvars" value="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest &autoPlay=true"></param>
        <param name="allowFullScreen" value="true"></param>
        <param name="allowscriptaccess" value="always"></param>
        <param name="wmode" value="direct"></param>
        <embed src="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf" 
            type="application/x-shockwave-flash" 
            allowscriptaccess="always" 
            allowfullscreen="true" 
            wmode="direct" 
            width="920" 
            height="640" 
            flashvars=" src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true">
        </embed>
        </object>
        </body>
        </html>



1. <span data-ttu-id="508b2-152">Добавить подключаемый модуль toohello Smooth Streaming OSMF код внедрения и сохранить.</span><span class="sxs-lookup"><span data-stu-id="508b2-152">Add Smooth Streaming OSMF plugin toohello embed code and save.</span></span>
   
        <html>
        <object width="920" height="640"> 
        <param name="movie" value="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf"></param>
        <param name="flashvars" value="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true&plugin_AdaptiveStreamingPlugin=http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf&AdaptiveStreamingPlugin_retryLive=true&AdaptiveStreamingPlugin_retryInterval=10"></param>
        <param name="allowFullScreen" value="true"></param>
        <param name="allowscriptaccess" value="always"></param>
        <param name="wmode" value="direct"></param>
        <embed src="http://osmf.org/dev/2.0gm/StrobeMediaPlayback.swf" 
            type="application/x-shockwave-flash" 
            allowscriptaccess="always" 
            allowfullscreen="true" 
            wmode="direct" 
            width="920" 
            height="640" 
            flashvars="src=http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest&autoPlay=true&plugin_AdaptiveStreamingPlugin=http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf&AdaptiveStreamingPlugin_retryLive=true&AdaptiveStreamingPlugin_retryInterval=10">
        </embed>
        </object>
        </html>
2. <span data-ttu-id="508b2-153">Сохраните страницу HTML и публикации tooa веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="508b2-153">Save your HTML page and publish tooa web server.</span></span> <span data-ttu-id="508b2-154">Обзор toohello опубликованных веб-страницы с помощью вашего любимого Flash&reg; проигрывателя включено интернет-браузере (Internet Explorer, Chrome, Firefox, т. д).</span><span class="sxs-lookup"><span data-stu-id="508b2-154">Browse toohello published web page using your favorite Flash&reg; Player enabled Internet browser (Internet Explorer, Chrome, Firefox, so on).</span></span>
3. <span data-ttu-id="508b2-155">Наслаждайтесь просмотром содержимого Smooth Streaming в проигрывателе Adobe&reg; Flash&reg; Player.</span><span class="sxs-lookup"><span data-stu-id="508b2-155">Enjoy Smooth Streaming content inside Adobe&reg; Flash&reg; Player.</span></span>

<span data-ttu-id="508b2-156">Дополнительные сведения о общей разработки OSMF, см. в разделе официальные hello [страница разработки OSMF](http://osmf.org/resources.html).</span><span class="sxs-lookup"><span data-stu-id="508b2-156">For more information on general OSMF development, please see hello official [OSMF development page](http://osmf.org/resources.html).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="508b2-157">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="508b2-157">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="508b2-158">Отзывы</span><span class="sxs-lookup"><span data-stu-id="508b2-158">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="508b2-159">См. также</span><span class="sxs-lookup"><span data-stu-id="508b2-159">See Also</span></span>
[<span data-ttu-id="508b2-160">Адаптивный подключаемый модуль Майкрософт для потоковой передачи для обновления OSMF</span><span class="sxs-lookup"><span data-stu-id="508b2-160">Microsoft Adaptive Streaming Plugin for OSMF Update</span></span>](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

