---
title: "Подключаемый модуль Smooth Streaming для платформы Open Source Media Framework"
description: "Узнайте, как использовать подключаемый модуль Smooth Streaming служб мультимедиа Azure для платформы Open Source Media Framework."
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
ms.openlocfilehash: 9c764f176ae75085320882de3fb26d8e7d52daaf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-the-microsoft-smooth-streaming-plugin-for-the-adobe-open-source-media-framework"></a><span data-ttu-id="66106-103">Использование подключаемого модуля Smooth Streaming Майкрософт для платформы Adobe Open Source Media Framework</span><span class="sxs-lookup"><span data-stu-id="66106-103">How to Use the Microsoft Smooth Streaming Plugin for the Adobe Open Source Media Framework</span></span>
## <a name="overview"></a><span data-ttu-id="66106-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="66106-104">Overview</span></span>
<span data-ttu-id="66106-105">Подключаемый модуль Smooth Streaming для платформы Open Source Media Framework 2.0 (SS для OSMF) расширяет возможности OSMF по умолчанию и добавляет возможности воспроизведения контента Smooth Streaming для новых и существующих проигрывателей OSMF.</span><span class="sxs-lookup"><span data-stu-id="66106-105">The Microsoft Smooth Streaming plugin for Open Source Media Framework 2.0 (SS for OSMF) extends the default capabilities of OSMF and adds Microsoft Smooth Streaming content playback to new and existing OSMF players.</span></span> <span data-ttu-id="66106-106">Подключаемый модуль также добавляет возможность воспроизведения Smooth Streaming в SMP.</span><span class="sxs-lookup"><span data-stu-id="66106-106">The plugin also adds Smooth Streaming playback capabilities to Strobe Media Playback (SMP).</span></span>

<span data-ttu-id="66106-107">SS для OSMF включает в себя две версии подключаемого модуля:</span><span class="sxs-lookup"><span data-stu-id="66106-107">SS for OSMF includes two versions of plugin:</span></span>

* <span data-ttu-id="66106-108">статический подключаемый модуль Smooth Streaming для OSMF (.swc);</span><span class="sxs-lookup"><span data-stu-id="66106-108">Static Smooth Streaming plugin for OSMF (.swc)</span></span>
* <span data-ttu-id="66106-109">динамический подключаемый модуль Smooth Streaming для OSMF (.swf).</span><span class="sxs-lookup"><span data-stu-id="66106-109">Dynamic Smooth Streaming plugin for OSMF (.swf)</span></span>

<span data-ttu-id="66106-110">В настоящем документе предполагается, что читатель имеет общие знания о работе с OSMF и подключаемыми модулями OSMF. Дополнительные сведения об OSMF см. в документации на [официальном сайте OSMF](http://osmf.org/).</span><span class="sxs-lookup"><span data-stu-id="66106-110">This document assumes that the reader has a general working knowledge of OSMF and OSMF plug-ins. For more information about OSMF, please see the documentation on the [official OSMF site](http://osmf.org/).</span></span>

### <a name="smooth-streaming-plugin-for-osmf-20"></a><span data-ttu-id="66106-111">Подключаемый модуль Smooth Streaming для OSMF 2.0</span><span class="sxs-lookup"><span data-stu-id="66106-111">Smooth Streaming plugin for OSMF 2.0</span></span>
<span data-ttu-id="66106-112">Подключаемый модуль поддерживает загрузку и воспроизведение контента Smooth Streaming по запросу со следующими возможностями:</span><span class="sxs-lookup"><span data-stu-id="66106-112">The plugin supports loading and playback of on-demand Smooth Streaming content with the following features:</span></span>

* <span data-ttu-id="66106-113">воспроизведение Smooth Streaming по запросу (воспроизведение, пауза, поиск, остановка);</span><span class="sxs-lookup"><span data-stu-id="66106-113">On-demand Smooth Streaming playback (Play, Pause, Seek, Stop)</span></span>
* <span data-ttu-id="66106-114">воспроизведение Smooth Streaming в реальном времени (воспроизведение);</span><span class="sxs-lookup"><span data-stu-id="66106-114">Live Smooth Streaming playback (Play)</span></span>
* <span data-ttu-id="66106-115">функции DVR в реальном времени (пауза, поиск, воспроизведение DVR, Go-to-Live);</span><span class="sxs-lookup"><span data-stu-id="66106-115">Live DVR functions (Pause, Seek, DVR Playback, Go-to-Live)</span></span>
* <span data-ttu-id="66106-116">поддержка видеокодеков H.264;</span><span class="sxs-lookup"><span data-stu-id="66106-116">Support for video codecs - H.264</span></span>
* <span data-ttu-id="66106-117">поддержка аудиокодеков AAC;</span><span class="sxs-lookup"><span data-stu-id="66106-117">Support for Audio codecs - AAC</span></span>
* <span data-ttu-id="66106-118">поддержка нескольких языков аудио с помощью встроенных API-интерфейсов OSMF;</span><span class="sxs-lookup"><span data-stu-id="66106-118">Multiple audio language switching with OSMF built-in APIs</span></span>
* <span data-ttu-id="66106-119">выбор качества воспроизведения с помощью встроенных API-интерфейсов OSMF;</span><span class="sxs-lookup"><span data-stu-id="66106-119">Max playback quality selection with OSMF built-in APIs</span></span>
* <span data-ttu-id="66106-120">боковые субтитры с использованием подключаемого модуля субтитров OSMF;</span><span class="sxs-lookup"><span data-stu-id="66106-120">Sidecar closed captions with OSMF captions plugin</span></span>
* <span data-ttu-id="66106-121">Adobe&reg; Flash&reg; Player 11.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="66106-121">Adobe&reg; Flash&reg; Player 11.4 or higher.</span></span>
* <span data-ttu-id="66106-122">Эта версия поддерживает только OSMF 2.0.</span><span class="sxs-lookup"><span data-stu-id="66106-122">This version only supports OSMF 2.0.</span></span>

## <a name="supported-features-and-known-issues"></a><span data-ttu-id="66106-123">Поддерживаемые функции и известные проблемы</span><span class="sxs-lookup"><span data-stu-id="66106-123">Supported features and known issues</span></span>
<span data-ttu-id="66106-124">Полный список поддерживаемых и неподдерживаемых функций, а также известных проблем см. в [этом документе](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span><span class="sxs-lookup"><span data-stu-id="66106-124">For a full list of supported features, unsupported features and known issues, refer to [this document](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).</span></span>

## <a name="loading-the-plugin"></a><span data-ttu-id="66106-125">Загрузка подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="66106-125">Loading the Plugin</span></span>
<span data-ttu-id="66106-126">Подключаемые модули OSMF можно загружать статически (во время компиляции) или динамически (во время выполнения).</span><span class="sxs-lookup"><span data-stu-id="66106-126">OSMF plugins can be loaded statically (at compile time) or dynamically (at run-time).</span></span> <span data-ttu-id="66106-127">Подключаемый модуль Smooth Streaming для OSMF содержит динамическую и статическую версию.</span><span class="sxs-lookup"><span data-stu-id="66106-127">The Smooth Streaming plugin for OSMF download includes both dynamic and static versions.</span></span>

* <span data-ttu-id="66106-128">Статическая загрузка: для статической загрузки требуется файл статической библиотеки (SWC).</span><span class="sxs-lookup"><span data-stu-id="66106-128">Static loading: To load statically, a static library (SWC) file is required.</span></span> <span data-ttu-id="66106-129">Статические подключаемые модули добавляются как ссылки на проекты и объединяются с окончательным выходным файлом во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="66106-129">Static plugins are added as a reference to the projects and merge inside the final output file at the compile time.</span></span>
* <span data-ttu-id="66106-130">Динамическая загрузка: для динамической загрузки требуется предварительно скомпилированный файл (SWF).</span><span class="sxs-lookup"><span data-stu-id="66106-130">Dynamic loading: To load dynamically, a precompiled (SWF) file is required.</span></span> <span data-ttu-id="66106-131">Динамические подключаемые модули загружаются во время выполнения и не включаются в выходные данные проекта.</span><span class="sxs-lookup"><span data-stu-id="66106-131">Dynamic plugins are loaded in the runtime and not included in the project output.</span></span> <span data-ttu-id="66106-132">(Выходные данные компиляции) Динамические подключаемые модули можно загрузить с использованием протоколов HTTP и FILE.</span><span class="sxs-lookup"><span data-stu-id="66106-132">(Compiled output) Dynamic plugins can be loaded using HTTP and FILE protocols.</span></span>

<span data-ttu-id="66106-133">Дополнительные сведения о статической и динамической загрузке см. на официальной [странице подключаемого модуля OSMF](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span><span class="sxs-lookup"><span data-stu-id="66106-133">For more information on static and dynamic loading, see the official [OSMF plugin page](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).</span></span>

### <a name="ss-for-osmf-static-loading"></a><span data-ttu-id="66106-134">Динамическая загрузка SS для OSMF</span><span class="sxs-lookup"><span data-stu-id="66106-134">SS for OSMF Static Loading</span></span>
<span data-ttu-id="66106-135">В следующем фрагменте кода показано, как загрузить подключаемый модуль SS для OSMF статически и воспроизвести простое видео с помощью класса MediaFactory OSMF.</span><span class="sxs-lookup"><span data-stu-id="66106-135">The code snippet below shows how to load the SS plugin for OSMF statically and play a basic video using OSMF MediaFactory class.</span></span> <span data-ttu-id="66106-136">Перед добавлением кода SS для OSMF убедитесь, что ссылка на проект включает статический подключаемый модуль "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc".</span><span class="sxs-lookup"><span data-stu-id="66106-136">Before including the SS for OSMF code, please ensure that the project reference includes the "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" static plugin.</span></span>

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

            // Create the container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);
            _mediaPlayerSprite.scaleMode = ScaleMode.NONE;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            //Adds the container to the stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add the listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load the plugin class 
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
            // The plugin is loaded successfully.
            // Your web server needs to host a valid crossdomain.xml file to allow plugin to download Smooth Streaming files.
        loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")

        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // The plugin is failed to load ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started to load.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code to deal with Player Ready when it is hit the first load after a source is loaded. 

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
            // Take an URL of SmoothStreamingSource's manifest and add it to the page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;

            // Add the media element
            _mediaPlayerSprite.media = element;
        }     

    }
}
```


### <a name="ss-for-osmf-dynamic-loading"></a><span data-ttu-id="66106-137">Динамическая загрузка SS для OSMF</span><span class="sxs-lookup"><span data-stu-id="66106-137">SS for OSMF Dynamic Loading</span></span>
<span data-ttu-id="66106-138">В следующем фрагменте кода показано, как загрузить подключаемый модуль SS для OSMF динамически и воспроизвести простое видео с помощью класса MediaFactory OSMF.</span><span class="sxs-lookup"><span data-stu-id="66106-138">The code snippet below shows how to load the SS plugin for OSMF dynamically and play a basic video using the OSMF MediaFactory class.</span></span> <span data-ttu-id="66106-139">Перед включением кода SS для OSMF скопируйте динамический модуль "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" в папку проекта, если загрузка будет выполняться с помощью протокола FILE, или скопируйте его на веб-сервер для загрузки с помощью протокола HTTP.</span><span class="sxs-lookup"><span data-stu-id="66106-139">Before including the SS for OSMF code, copy the "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" dynamic plugin to the project folder if you want to load using FILE protocol, or copy under a web server for HTTP load.</span></span> <span data-ttu-id="66106-140">Нет необходимости включать "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" в ссылки проекта.</span><span class="sxs-lookup"><span data-stu-id="66106-140">There is no need to include "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swc" in the project references.</span></span>

<span data-ttu-id="66106-141">пакет {</span><span class="sxs-lookup"><span data-stu-id="66106-141">package {</span></span>

    import flash.display.*;
    import org.osmf.media.*;
    import org.osmf.containers.MediaContainer;
    import org.osmf.events.MediaErrorEvent;
    import org.osmf.events.MediaFactoryEvent;
    import org.osmf.events.MediaPlayerStateChangeEvent;
    import org.osmf.layout.*;
    import flash.events.Event;
    import flash.system.Capabilities;


    //Sets the size of the SWF

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

            // Create the container (sprite) for managing display and layout
            _mediaPlayerSprite = new MediaPlayerSprite();    
            _mediaPlayerSprite.addEventListener(MediaErrorEvent.MEDIA_ERROR, onPlayerFailed);
            _mediaPlayerSprite.addEventListener(MediaPlayerStateChangeEvent.MEDIA_PLAYER_STATE_CHANGE, onPlayerStateChange);

            //Adds the container to the stage
            addChild(_mediaPlayerSprite);

            // Create a mediafactory instance
            _mediaFactory = new DefaultMediaFactory();

            // Add the listeners for PLUGIN_LOADING
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD,onPluginLoaded);
            _mediaFactory.addEventListener(MediaFactoryEvent.PLUGIN_LOAD_ERROR, onPluginLoadFailed );

            // Load the plugin class 
            loadAdaptiveStreamingPlugin( );  

        }

        private function loadAdaptiveStreamingPlugin( ):void
        {
            var pluginResource:MediaResourceBase;
            var adaptiveStreamingPluginUrl:String;

            // Your dynamic plugin web server needs to host a valid crossdomain.xml file to allow loading plugins.

            adaptiveStreamingPluginUrl = "http://yourdomain/MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf";
            pluginResource = new URLResource(adaptiveStreamingPluginUrl);
            _mediaFactory.loadPlugin( pluginResource ); 

        }

        private function onPluginLoaded( event:MediaFactoryEvent ):void
        {
            // The plugin is loaded successfully.

            // Your web server needs to host a valid crossdomain.xml file to allow plugin to download Smooth Streaming files.

    loadMediaSource("http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest")
        }

        private function onPluginLoadFailed( event:MediaFactoryEvent ):void
        {
            // The plugin is failed to load ...
        }


        private function onPlayerStateChange(event:MediaPlayerStateChangeEvent) : void
        {
            var state:String;

            state =  event.state;

            switch (state)
            {
                case MediaPlayerState.LOADING: 

                    // A new source is started to load.

                    break;

                case  MediaPlayerState.READY :   
                    // Add code to deal with Player Ready when it is hit the first load after a source is loaded. 

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
            // Take an URL of SmoothStreamingSource's manifest and add it to the page.

            var resource:URLResource= new URLResource( sourceURL );

            var element:MediaElement = _mediaFactory.createMediaElement( resource );
            _mediaPlayerSprite.scaleMode = ScaleMode.LETTERBOX;
            _mediaPlayerSprite.width = stage.stageWidth;
            _mediaPlayerSprite.height = stage.stageHeight;
            // Add the media element
            _mediaPlayerSprite.media = element;
        }     

    }
<span data-ttu-id="66106-142">}</span><span class="sxs-lookup"><span data-stu-id="66106-142">}</span></span>

## <a name="strobe-media--playback-with-the-ss-odmf-dynamic-plugin"></a><span data-ttu-id="66106-143">Воспроизведение Strobe Media с помощью динамического подключаемого модуля SS ODMF</span><span class="sxs-lookup"><span data-stu-id="66106-143">Strobe Media  Playback with the SS ODMF Dynamic Plugin</span></span>
<span data-ttu-id="66106-144">Динамический подключаемый модуль Smooth Streaming для OSMF совместим с проигрывателем [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span><span class="sxs-lookup"><span data-stu-id="66106-144">The Smooth Streaming for OSMF dynamic plugin is compatible with [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html).</span></span> <span data-ttu-id="66106-145">Подключаемый модуль SS для OSMF можно использовать для поддержки воспроизведения контента в SMP.</span><span class="sxs-lookup"><span data-stu-id="66106-145">You can use the SS for OSMF plugin to add Smooth Streaming content playback to SMP.</span></span> <span data-ttu-id="66106-146">Для этого скопируйте "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" на веб-сервер, чтобы выполнять загрузку по протоколу HTTP, и выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="66106-146">To do this, copy "MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf" under a web server for HTTP load using the following steps:</span></span>

1. <span data-ttu-id="66106-147">Откройте [страницу настройки Strobe Media Playback](http://osmf.org/dev/2.0gm/setup.html).</span><span class="sxs-lookup"><span data-stu-id="66106-147">Browse the [Strobe Media Playback setup page](http://osmf.org/dev/2.0gm/setup.html).</span></span> 
2. <span data-ttu-id="66106-148">Задайте src в качестве значения для источника Smooth Streaming, (например, http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span><span class="sxs-lookup"><span data-stu-id="66106-148">Set the src to a Smooth Streaming source, (e.g. http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest)</span></span> 
3. <span data-ttu-id="66106-149">Внесите требуемые изменения и нажмите кнопку "Предварительный просмотр и обновление".</span><span class="sxs-lookup"><span data-stu-id="66106-149">Make the desired configuration changes and click Preview and Update.</span></span>
   
   <span data-ttu-id="66106-150">**Примечание.** На веб-сервере должен размещаться допустимый файл crossdomain.xml.</span><span class="sxs-lookup"><span data-stu-id="66106-150">**Note** Your content web server needs a valid crossdomain.xml.</span></span> 
4. <span data-ttu-id="66106-151">Скопируйте и вставьте код на простую HTML-страницу, используя предпочитаемый текстовый редактор, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="66106-151">Copy and paste the code to a simple HTML page using your favorite text editor, such as in the following example:</span></span>

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



1. <span data-ttu-id="66106-152">Добавьте подключаемый модуль Smooth Streaming OSMF в код внедрения и сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="66106-152">Add Smooth Streaming OSMF plugin to the embed code and save.</span></span>
   
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
2. <span data-ttu-id="66106-153">Сохраните HTML-страницу и опубликуйте ее на веб-сервере.</span><span class="sxs-lookup"><span data-stu-id="66106-153">Save your HTML page and publish to a web server.</span></span> <span data-ttu-id="66106-154">Перейдите к опубликованной веб-странице в предпочитаемом браузере с поддержкой проигрывателя Flash&reg; Player (Internet Explorer, Chrome, Firefox и т. п.).</span><span class="sxs-lookup"><span data-stu-id="66106-154">Browse to the published web page using your favorite Flash&reg; Player enabled Internet browser (Internet Explorer, Chrome, Firefox, so on).</span></span>
3. <span data-ttu-id="66106-155">Наслаждайтесь просмотром содержимого Smooth Streaming в проигрывателе Adobe&reg; Flash&reg; Player.</span><span class="sxs-lookup"><span data-stu-id="66106-155">Enjoy Smooth Streaming content inside Adobe&reg; Flash&reg; Player.</span></span>

<span data-ttu-id="66106-156">Дополнительные сведения об общей процедуре разработки для OSMF см. на официальной [странице разработки OSMF](http://osmf.org/resources.html).</span><span class="sxs-lookup"><span data-stu-id="66106-156">For more information on general OSMF development, please see the official [OSMF development page](http://osmf.org/resources.html).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="66106-157">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="66106-157">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="66106-158">Отзывы</span><span class="sxs-lookup"><span data-stu-id="66106-158">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="66106-159">См. также</span><span class="sxs-lookup"><span data-stu-id="66106-159">See Also</span></span>
[<span data-ttu-id="66106-160">Адаптивный подключаемый модуль Майкрософт для потоковой передачи для обновления OSMF</span><span class="sxs-lookup"><span data-stu-id="66106-160">Microsoft Adaptive Streaming Plugin for OSMF Update</span></span>](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

