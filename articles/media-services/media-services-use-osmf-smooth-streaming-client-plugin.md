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
# <a name="how-toouse-hello-microsoft-smooth-streaming-plugin-for-hello-adobe-open-source-media-framework"></a>Как tooUse hello Microsoft Smooth Streaming подключаемого модуля для hello Adobe открытую платформу исходного носителя
## <a name="overview"></a>Обзор
Здравствуйте подключаемый модуль Microsoft Smooth Streaming для Open Source Media Framework 2.0 (SS для OSMF) расширяет возможности по умолчанию hello OSMF и добавляет toonew воспроизведения содержимого Microsoft Smooth Streaming и OSMF существующие проигрыватели. Подключаемый модуль Hello также добавляет Smooth Streaming воспроизведения возможности tooStrobe Media Playback (SMP).

SS для OSMF включает в себя две версии подключаемого модуля:

* статический подключаемый модуль Smooth Streaming для OSMF (.swc);
* динамический подключаемый модуль Smooth Streaming для OSMF (.swf).

Данный документ предполагает, что модуль чтения hello имеет общие опыт работы с OSMF и OSMF подключаемых модулей. Дополнительные сведения о OSMF, см. в разделе документации hello на hello [официальный сайт OSMF](http://osmf.org/).

### <a name="smooth-streaming-plugin-for-osmf-20"></a>Подключаемый модуль Smooth Streaming для OSMF 2.0
Подключаемый модуль Hello поддерживает загрузки и воспроизведения Smooth Streaming содержимого по запросу с hello следующие атрибуты:

* воспроизведение Smooth Streaming по запросу (воспроизведение, пауза, поиск, остановка);
* воспроизведение Smooth Streaming в реальном времени (воспроизведение);
* функции DVR в реальном времени (пауза, поиск, воспроизведение DVR, Go-to-Live);
* поддержка видеокодеков H.264;
* поддержка аудиокодеков AAC;
* поддержка нескольких языков аудио с помощью встроенных API-интерфейсов OSMF;
* выбор качества воспроизведения с помощью встроенных API-интерфейсов OSMF;
* боковые субтитры с использованием подключаемого модуля субтитров OSMF;
* Adobe&reg; Flash&reg; Player 11.4 или более поздней версии.
* Эта версия поддерживает только OSMF 2.0.

## <a name="supported-features-and-known-issues"></a>Поддерживаемые функции и известные проблемы
Полный список поддерживаемых функций, неподдерживаемых функций и известных проблемах см. в разделе слишком[в этом документе](http://download.microsoft.com/download/3/1/B/31B63D97-574E-4A8D-BF8D-170744181724/Smooth_Streaming_Plugin_for_OSMF.pdf).

## <a name="loading-hello-plugin"></a>Загрузка hello подключаемого модуля
Подключаемые модули OSMF можно загружать статически (во время компиляции) или динамически (во время выполнения). Hello подключаемый модуль Smooth Streaming для OSMF загрузки включает динамических и статических версии.

* Статические загрузки: tooload статически, статическая библиотека (SWC) является обязательным. Статические подключаемые модули будут добавлены как ссылка toohello проекты и объединение внутри hello выходных файлов во время компиляции hello.
* Динамическая загрузка: tooload динамически, предварительно скомпилированный файл (SWF) является обязательным. Динамические подключаемые модули загружаются в hello выполнения и не включены в выходные данные проекта hello. (Выходные данные компиляции) Динамические подключаемые модули можно загрузить с использованием протоколов HTTP и FILE.

Дополнительные сведения о статических и динамических загрузки. в разделе официальные hello [страница подключаемого модуля OSMF](http://osmf.org/dev/osmf/OtherPDFs/osmf_plugin_dev_guide.pdf).

### <a name="ss-for-osmf-static-loading"></a>Динамическая загрузка SS для OSMF
Приведенный далее фрагмент кода Hello показано, как tooload hello SS подключаемого модуля для OSMF статически и воспроизведения видео basic с помощью класса OSMF MediaFactory. Перед включением hello SS для OSMF кода, убедитесь, что hello ссылку на проект включает статических подключаемого модуля «MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swc» hello.

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


### <a name="ss-for-osmf-dynamic-loading"></a>Динамическая загрузка SS для OSMF
Приведенный далее фрагмент кода Hello показано, как tooload hello SS подключаемого модуля для OSMF динамически и воспроизведения видео basic с помощью класса OSMF MediaFactory hello. Перед включением hello SS для OSMF кода, скопируйте папку проекта toohello динамического подключаемого модуля «MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swf» hello, при tooload протоколу ФАЙЛ или скопировать в веб-сервер для загрузки HTTP. Нет необходимости tooinclude «MSAdaptiveStreamingPlugin v1.0.3 osmf2.0.swc», в ссылках проекта hello не существует.

пакет {

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
}

## <a name="strobe-media--playback-with-hello-ss-odmf-dynamic-plugin"></a>Воспроизведение мультимедиа strobe hello SS динамического ODMF подключаемого модуля.
Hello Smooth Streaming для динамической подключаемого модуля OSMF совместима с [Strobe Media Playback (SMP)](http://osmf.org/strobe_mediaplayback.html). Hello SS можно использовать для OSMF подключаемый модуль tooadd Smooth Streaming воспроизведения содержимого tooSMP. toodo, копия «MSAdaptiveStreamingPlugin-v1.0.3-osmf2.0.swf» в веб-сервер для нагрузки HTTP с помощью hello следующие шаги:

1. Обзор hello [страница установки Strobe Media Playback](http://osmf.org/dev/2.0gm/setup.html). 
2. Задать источник hello src tooa Smooth Streaming (например http://devplatem.vo.msecnd.net/Sintel/Sintel_H264.ism/manifest) 
3. Вносить изменения в конфигурацию требуемого hello и нажмите кнопку просмотра и обновления.
   
   **Примечание.** На веб-сервере должен размещаться допустимый файл crossdomain.xml. 
4. Скопируйте и вставьте hello кода tooa простой HTML-страницу с помощью предпочитаемого текстового редактора, например, в следующий пример hello:

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



1. Добавить подключаемый модуль toohello Smooth Streaming OSMF код внедрения и сохранить.
   
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
2. Сохраните страницу HTML и публикации tooa веб-сервера. Обзор toohello опубликованных веб-страницы с помощью вашего любимого Flash&reg; проигрывателя включено интернет-браузере (Internet Explorer, Chrome, Firefox, т. д).
3. Наслаждайтесь просмотром содержимого Smooth Streaming в проигрывателе Adobe&reg; Flash&reg; Player.

Дополнительные сведения о общей разработки OSMF, см. в разделе официальные hello [страница разработки OSMF](http://osmf.org/resources.html).

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>См. также
[Адаптивный подключаемый модуль Майкрософт для потоковой передачи для обновления OSMF](https://azure.microsoft.com/blog/2014/10/27/microsoft-adaptive-streaming-plugin-for-osmf-update/) 

