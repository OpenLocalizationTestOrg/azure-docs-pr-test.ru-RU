---
title: "Учебник приложения магазина Windows потоковой передачи aaaSmooth | Документы Microsoft"
description: "Узнайте, как toocreate toouse служб мультимедиа Azure приложения для магазина Windows на C# с XML MediaElement tooplayback Smooth Stream содержимого элемента управления."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0fa5d8c5-3d5f-4886-ae55-fb6de4f5256d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: juliako
ms.openlocfilehash: b02aa2c7f68fe22a23ea846d72fdd23bfba2b19c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobuild-a-smooth-streaming-windows-store-application"></a>Как tooBuild приложения Smooth Streaming Windows Store

Hello Smooth Streaming клиента SDK для Windows 8 позволяет приложениям магазина Windows toobuild разработчики, которые могут играть по требованию и динамического содержимого Smooth Streaming. В дополнение к этому toohello основные воспроизведения Smooth Streaming содержимое hello SDK также предоставляет богатые возможности, как Microsoft PlayReady protection, ограничение на уровни качества, Live DVR аудиопотока переключения, Ожидание обновления состояния (например, изменения уровня качества ) и событий ошибок и т. д. Функции hello поддерживается Дополнительные сведения см. в разделе hello [заметки о выпуске](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes). Дополнительные сведения см. на странице, посвященной [Player Framework для Windows 8](http://playerframework.codeplex.com/). 

Этот учебный курс состоит из четырех занятий:

1. Создание базового приложения магазина с бесперебойной потоковой передачей
2. Добавить ползунок hello tooControl Media хода выполнения
3. Выбор потоков для бесперебойной потоковой передачи
4. Выбор дорожек для бесперебойной потоковой передачи

## <a name="prerequisites"></a>Предварительные требования
* Windows 8 (32-разрядная или 64-разрядная). Можно получить [оценку Windows 8 Enterprise](http://msdn.microsoft.com/evalcenter/jj554510.aspx) из MSDN.
* Visual Studio 2012 или Visual Studio Express 2012 (либо более поздней версии). Можно получить пробную версию hello из [здесь](http://www.microsoft.com/visualstudio/11/downloads).
* [Клиентский пакет SDK для бесперебойной потоковой передачи Microsoft для Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home)

решение Hello завершена для всех занятий можно загрузить из примеров кода MSDN для разработчиков (Галерея кода): 

* [Урок 1.](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) Простой мультимедиапроигрыватель для Windows 8 с потоковой передачей Smooth Streaming. 
* [Урок 2.](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) Простой мультимедиапроигрыватель для Windows 8 с потоковой передачей Smooth Streaming и элементом управления «Ползунок». 
* [Урок 3.](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) Простой мультимедиапроигрыватель для Windows 8 с потоковой передачей Smooth Streaming и выбором потока.  
* [Урок 4.](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) Мультимедиапроигрыватель для Windows 8 с потоковой передачей Smooth Streaming и выбором дорожки.

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a>Урок 1. Создание базового приложения для магазина с бесперебойной потоковой передачей

На этом занятии вы создадите приложения для магазина Windows с помощью элемента управления MediaElement tooplay Smooth потока содержимого.  запущенное приложение Hello выглядит следующим образом.

![Пример приложения для магазина Windows с бесперебойной потоковой передачей][PlayerApplication]

Дополнительные сведения о разработке приложений Магазина Windows см. в разделе, посвященном [разработке потрясающих приложений для Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx). Это занятие содержит hello следующих процедур.

1. Создание проекта для магазина Windows
2. Разработка пользовательского интерфейса hello (XAML)
3. Измените файл с выделенным кодом hello
4. Компиляции и тестирования приложения hello

**toocreate проекта магазина Windows**

1. Запустите Visual Studio 2012 или более поздней версии.
2. Из hello **ФАЙЛ** меню, нажмите кнопку **New**, а затем нажмите кнопку **проекта**.
3. В диалоговом окне нового проекта hello типа или выберите hello следующие значения:

| Имя | Значение |
| --- | --- |
| Группа шаблонов |Installed/Templates/Visual C#/Windows Store |
| Шаблон |Пустое приложение (XAML) |
| Имя |SSPlayer |
| Расположение |C:\SSTutorials |
| Имя решения |SSPlayer |
| Создать каталог для решения |(выбрано) |

1. Нажмите кнопку **ОК**.

**tooadd ссылки toohello Smooth Streaming Client SDK**

1. В обозревателе решений щелкните правой кнопкой мыши **SSPlayer**, а затем выберите команду **Добавить ссылку**.
2. Введите или выберите hello следующие значения:

| Имя | Значение |
| --- | --- |
| Ссылочная группа |Windows/Расширения |
| Справочные материалы |Выберите клиентский пакет SDK бесперебойной потоковой передачи Microsoft для Windows 8 и пакет среды выполнения Microsoft Visual C++ |

1. Нажмите кнопку **ОК**. 

После добавления ссылки на hello, необходимо выбрать hello целевой платформы (x64 или x86), добавления ссылок не будет работать для конфигурации платформы любой ЦП.  Для таких добавленных ссылок в обозревателе решений будет выведен желтый значок предупреждения.

**toodesign hello проигрывателя пользовательского интерфейса**

1. В обозревателе решений дважды щелкните **MainPage.xaml** tooopen его в конструктор hello просмотра.
2. Найдите hello  **&lt;сетки&gt;**  и  **&lt;/Grid&gt;**  теги hello XAML-файл, и следующие hello вставить код между тегами hello двух:

         <Grid.RowDefinitions>

            <RowDefinition Height="20"/>    <!-- spacer -->
            <RowDefinition Height="50"/>    <!-- media controls -->
            <RowDefinition Height="100*"/>  <!-- media element -->
            <RowDefinition Height="80*"/>   <!-- media stream and track selection -->
            <RowDefinition Height="50"/>    <!-- status bar -->
         </Grid.RowDefinitions>

         <StackPanel Name="spMediaControl" Grid.Row="1" Orientation="Horizontal">
            <TextBlock x:Name="tbSource" Text="Source :  " FontSize="16" FontWeight="Bold" VerticalAlignment="Center" />
            <TextBox x:Name="txtMediaSource" Text="http://ecn.channel9.msdn.com/o9/content/smf/smoothcontent/elephantsdream/Elephants_Dream_1024-h264-st-aac.ism/manifest" FontSize="10" Width="700" Margin="0,4,0,10" />
            <Button x:Name="btnSetSource" Content="Set Source" Width="111" Height="43" Click="btnSetSource_Click"/>
            <Button x:Name="btnPlay" Content="Play" Width="111" Height="43" Click="btnPlay_Click"/>
            <Button x:Name="btnPause" Content="Pause"  Width="111" Height="43" Click="btnPause_Click"/>
            <Button x:Name="btnStop" Content="Stop"  Width="111" Height="43" Click="btnStop_Click"/>
            <CheckBox x:Name="chkAutoPlay" Content="Auto Play" Height="55" Width="Auto" IsChecked="{Binding AutoPlay, ElementName=mediaElement, Mode=TwoWay}"/>
            <CheckBox x:Name="chkMute" Content="Mute" Height="55" Width="67" IsChecked="{Binding IsMuted, ElementName=mediaElement, Mode=TwoWay}"/>
         </StackPanel>

         <StackPanel Name="spMediaElement" Grid.Row="2" Height="435" Width="1072"
                    HorizontalAlignment="Center" VerticalAlignment="Center">
            <MediaElement x:Name="mediaElement" Height="356" Width="924" MinHeight="225"
                          HorizontalAlignment="Center" VerticalAlignment="Center" 
                          AudioCategory="BackgroundCapableMedia" />
            <StackPanel Orientation="Horizontal">
                <Slider x:Name="sliderProgress" Width="924" Height="44"
                        HorizontalAlignment="Center" VerticalAlignment="Center"
                        PointerPressed="sliderProgress_PointerPressed"/>
                <Slider x:Name="sliderVolume" 
                        HorizontalAlignment="Right" VerticalAlignment="Center" Orientation="Vertical" 
                        Height="79" Width="148" Minimum="0" Maximum="1" StepFrequency="0.1" 
                        Value="{Binding Volume, ElementName=mediaElement, Mode=TwoWay}" 
                        ToolTipService.ToolTip="{Binding Value, RelativeSource={RelativeSource Mode=Self}}"/>
            </StackPanel>
         </StackPanel>

         <StackPanel Name="spStatus" Grid.Row="4" Orientation="Horizontal">
            <TextBlock x:Name="tbStatus" Text="Status :  " 
               FontSize="16" FontWeight="Bold" VerticalAlignment="Center" HorizontalAlignment="Center" />
            <TextBox x:Name="txtStatus" FontSize="10" Width="700" VerticalAlignment="Center"/>
         </StackPanel>
   
   Hello управления MediaElement — используется tooplayback мультимедиа. элемент управления "ползунок" Hello, с именем sliderProgress будет использоваться идет hello Далее занятия toocontrol hello носителя.
3. Нажмите клавишу **CTRL + S** toosave hello файла.

Hello управления MediaElement не поддерживает Smooth Streaming содержимого out-of-box. Поддержка Smooth Streaming tooenable hello, необходимо зарегистрировать обработчик hello потока байтов в Smooth Streaming, расширение имени файла и тип MIME.  tooregister, используйте метод MediaExtensionManager.RegisterByteStremHandler hello пространства имен Windows.Media hello.

В этом файле XAML некоторые обработчики событий связаны с элементами управления hello.  Такие обработчики событий необходимо определить.

**файл с выделенным кодом toomodify hello**

1. В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.
2. В начале hello hello файла, добавьте следующее hello с помощью инструкции:
   
        using Windows.Media;
3. В начале hello hello **MainPage** добавьте hello после элемента данных:
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. В конце hello hello **MainPage** конструктор, добавить hello, следующие две строки:
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. В конце hello hello **MainPage** класса, вставьте hello, следующий код:
   
         # region UI Button Click Events
         private void btnPlay_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Play();
         txtStatus.Text = "MediaElement is playing ...";
         }
         private void btnPause_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Pause();
         txtStatus.Text = "MediaElement is paused";
         }
         private void btnSetSource_Click(object sender, RoutedEventArgs e)
         {

         sliderProgress.Value = 0;
         mediaElement.Source = new Uri(txtMediaSource.Text);

         if (chkAutoPlay.IsChecked == true)
         {
             txtStatus.Text = "MediaElement is playing ...";
         }
         else
         {
             txtStatus.Text = "Click hello Play button tooplay hello media source.";
         }
         }
         private void btnStop_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Stop();
         txtStatus.Text = "MediaElement is stopped";
         }
         private void sliderProgress_PointerPressed(object sender, PointerRoutedEventArgs e)
         {

         txtStatus.Text = "Seek tooposition " + sliderProgress.Value;
         mediaElement.Position = new TimeSpan(0, 0, (int)(sliderProgress.Value));
         }
         # endregion

Здесь определяется обработчик события sliderProgress_PointerPressed Hello.  Существуют дополнительные tooget toodo works его работы, который будет рассматриваться в hello следующем занятии этого учебника.
6. Нажмите клавишу **CTRL + S** toosave hello файла.

Hello готовой hello файл кода программной части должен выглядеть следующим образом:

![Просмотр кода в Visual Studio для приложения для магазина Windows с бесперебойной потоковой передачей][CodeViewPic]

**toocompile и тестирования приложения hello**

1. Из hello **ПОСТРОЕНИЯ** меню, нажмите кнопку **Configuration Manager**.
2. Изменение **Активная платформа решения** toomatch платформу разработки.
3. Нажмите клавишу **F6** toocompile hello проекта. 
4. Нажмите клавишу **F5** toorun приложения hello.
5. Вверху hello приложения hello можно использовать значение по умолчанию hello Smooth Streaming URL-адрес или введите его. 
6. Щелкните **Задать источник**. Поскольку **автовоспроизведения** включена по умолчанию hello должны автоматического воспроизведения мультимедиа.  Можно управлять hello мультимедиа с помощью hello **воспроизведение**, **Пауза** и **остановить** кнопки.  Можно управлять с помощью ползунка вертикальной hello том носителя hello.  Однако hello горизонтальный ползунок для управления media выполняется еще не реализован полностью приветствия. 

Вы завершили урок 1.  На этом занятии используйте tooplayback управления MediaElement содержимое Smooth Streaming.  Hello следующем занятии вы добавите элемент ползунок toocontrol hello ход выполнения hello содержимое Smooth Streaming.

## <a name="lesson-2-add-a-slider-bar-toocontrol-hello-media-progress"></a>Занятие 2: Добавление ползунок hello tooControl Media хода выполнения

На занятии 1 вы создали приложения для магазина Windows с tooplayback управления MediaElement XAML контента Smooth Streaming.  Этот элемент изначально имеет такие функции, как начало, останов и приостановка воспроизведения.  На этом занятии вы добавите приложение toohello панель элемента управления "ползунок".

В этом учебнике мы будем использовать таймер tooupdate hello положение ползунка на основе текущего положения hello hello управления MediaElement.  ползунок Hello время начала и окончания также необходимость toobe обновляется в случае содержимого в реальном времени.  Это можно лучше обрабатывать в событии обновления hello адаптивной источника.

Источники мультимедиа — это объекты, которые создают данные мультимедиа.  Hello источника принимает поток URL-адрес или байт и создает соответствующий носитель hello источником этого содержимого.  Сопоставитель Hello источника — hello стандартный способ источников мультимедиа toocreate приложения hello. 

Это занятие содержит hello следующих процедур.

1. Зарегистрируйте обработчик Smooth Streaming hello 
2. Добавьте обработчики событий уровня manager адаптивной источника hello
3. Добавление обработчиков событий уровня адаптивной источника hello
4. Добавление обработчиков событий MediaElement
5. Добавление кода, связанного с ползунком
6. Компиляции и тестирования приложения hello

**tooregister hello потока байтов в Smooth Streaming обработчика и передайте hello propertyset**

1. В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.
2. В начале файла hello hello, добавьте следующее hello с помощью инструкции:

        using Microsoft.Media.AdaptiveStreaming;
3. В начале hello hello класса MainPage, добавьте hello следующие элементы данных:

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. Внутри hello **MainPage** конструктора, добавьте следующий код после hello hello **это. Инициализация Components();**  строки и строки кода регистрации hello, написанных на предыдущем занятии hello:

        // Gets hello default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value tooAdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. Внутри hello **MainPage** конструктор, д изменение hello tooadd методы RegisterByteStreamHandler hello двух параметров:

         // Registers Smooth Streaming byte-stream handler for ".ism" extension and, 
         // "text/xml" and "application/vnd.ms-ss" mime-types and pass hello propertyset. 
         // http://*.ism/manifest URI resources will be resolved by Byte-stream handler.
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "text/xml", 
            propertySet );
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "application/vnd.ms-sstr+xml", 
         propertySet);
6. Нажмите клавишу **CTRL + S** toosave hello файла.

**tooadd hello адаптивной источника диспетчера событий уровня обработчика**

1. В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.
2. Внутри hello **MainPage** добавьте hello после элемента данных:
   
     private AdaptiveSource adaptiveSource = null;
3. В конце hello hello **MainPage** добавьте следующий обработчик событий hello:
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. В конце hello hello **MainPage** конструктор, добавить следующие строки toosubscribe toohello адаптивной исходного открытые события hello:
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. Нажмите клавишу **CTRL + S** toosave hello файла.

**обработчики событий уровня tooadd адаптивной источника**

1. В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.
2. Внутри hello **MainPage** добавьте hello после элемента данных:
   
     private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;
3. В конце hello hello **MainPage** добавьте следующие обработчики событий hello:

         # region Adaptive Source Level Events
         private void mediaElement_ManifestReady(AdaptiveSource sender, ManifestReadyEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
            manifestObject = args.AdaptiveSource.Manifest;
         }

         private void mediaElement_AdaptiveSourceStatusUpdated(AdaptiveSource sender, AdaptiveSourceStatusUpdatedEventArgs args)
         {

            adaptiveSourceStatusUpdate = args;
         }

         private void mediaElement_AdaptiveSourceFailed(AdaptiveSource sender, AdaptiveSourceFailedEventArgs args)
         {

            txtStatus.Text = "Error: " + args.HttpResponse;
         }

         # endregion Adaptive Source Level Events
4. В конце hello hello **mediaElement AdaptiveSourceOpened** метод, добавьте следующий код для событий toohello toosubscribe hello:
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. Нажмите клавишу **CTRL + S** toosave hello файла.

Здравствуйте, того же события, доступные на адаптивной диспетчера уровень источника, который может использоваться для обработки Общие элементы мультимедиа tooall функциональности в приложение hello. Каждый адаптивный источник имеет свои собственные события, и все события AdaptiveSource будут передаваться каскадом в диспетчер AdaptiveSourceManager.

**обработчики событий для элемента мультимедиа tooadd**

1. В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.
2. В конце hello hello **MainPage** добавьте следующие обработчики событий hello:

         # region Media Element Event Handlers
         private void MediaOpened(object sender, RoutedEventArgs e)
         {

            txtStatus.Text = "MediaElement opened";
         }

         private void MediaFailed(object sender, ExceptionRoutedEventArgs e)
         {

            txtStatus.Text= "MediaElement failed: " + e.ErrorMessage;
         }

         private void MediaEnded(object sender, RoutedEventArgs e)
         {

            txtStatus.Text ="MediaElement ended.";
         }

         # endregion Media Element Event Handlers
3. В конце hello hello **MainPage** конструктора, добавьте следующий код для событий toohello toosubscript hello:

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. Нажмите клавишу **CTRL + S** toosave hello файла.

**ползунок tooadd связанный код**

1. В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.
2. В начале файла hello hello, добавьте следующее hello с помощью инструкции:
      
        using Windows.UI.Core;
3. Внутри hello **MainPage** добавьте следующие члены данных hello:
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. В конце hello hello **MainPage** конструктор, добавить hello, следующий код:
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. В конце hello hello **MainPage** добавьте hello, следующий код:

         # region sliderMediaPlayer
         private double SliderFrequency(TimeSpan timevalue)
         {

            long absvalue = 0;
            double stepfrequency = -1;

            if (manifestObject != null)
            {
                absvalue = manifestObject.Duration - (long)manifestObject.StartTime;
            }
            else
            {
                absvalue = mediaElement.NaturalDuration.TimeSpan.Ticks;
            }

            TimeSpan totalDVRDuration = new TimeSpan(absvalue);

            if (totalDVRDuration.TotalMinutes >= 10 && totalDVRDuration.TotalMinutes < 30)
            {
               stepfrequency = 10;
            }
            else if (totalDVRDuration.TotalMinutes >= 30 
                     && totalDVRDuration.TotalMinutes < 60)
            {
                stepfrequency = 30;
            }
            else if (totalDVRDuration.TotalHours >= 1)
            {
                stepfrequency = 60;
            }

            return stepfrequency;
         }

         void updateSliderPositionoNTicks(object sender, object e)
         {

            sliderProgress.Value = mediaElement.Position.TotalSeconds;
         }

         public void setupTimer()
         {

            sliderPositionUpdateDispatcher = new DispatcherTimer();
            sliderPositionUpdateDispatcher.Interval = new TimeSpan(0, 0, 0, 0, 300);
            startTimer();
         }

         public void startTimer()
         {

            sliderPositionUpdateDispatcher.Tick += updateSliderPositionoNTicks;
            sliderPositionUpdateDispatcher.Start();
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderStartTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.StartTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Minimum = absvalue;
            });
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderEndTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Maximum = absvalue;
            });
         }

         # endregion sliderMediaPlayer
      
>[!NOTE]
>CoreDispatcher — используется toomake изменения потока toohello пользовательского интерфейса из потока без пользовательского интерфейса. В случае узкое место в поток dispatcher разработчика можно выбрать диспетчер toouse элементом пользовательского интерфейса при условии, что он планирует tooupdate.  Например:
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. В конце hello hello **mediaElement_AdaptiveSourceStatusUpdated** метод, добавить hello, следующий код:

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. В конце hello hello **MediaOpened** метод, добавить hello, следующий код:

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. Нажмите клавишу **CTRL + S** toosave hello файла.

**toocompile и тестирования приложения hello**

1. Нажмите клавишу **F6** toocompile hello проекта. 
2. Нажмите клавишу **F5** toorun приложения hello.
3. Вверху hello приложения hello можно использовать значение по умолчанию hello Smooth Streaming URL-адрес или введите его. 
4. Щелкните **Задать источник**. 
5. Ползунок hello теста.

Вы завершили урок 2.  На этом занятии вы добавили tooapplication ползунок. 

## <a name="lesson-3-select-smooth-streaming-streams"></a>Урок 3. Выбор потоков для бесперебойной потоковой передачи
Smooth Streaming — поддержкой toostream содержимого с помощью нескольких языков звуковые файлы, доступны для выбора путем просмотра hello.  На этом занятии вы включите потоки tooselect средства просмотра. Это занятие содержит hello следующих процедур.

1. Измените файл XAML hello
2. Измените файл behand кода hello
3. Компиляции и тестирования приложения hello

**toomodify hello XAML-файла**

1. В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Конструктор представлений**.
2. Найдите &lt;Grid.RowDefinitions&gt;и изменение hello RowDefinitions, поэтому они выглядит следующим образом:
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. Внутри hello &lt;сетки&gt;&lt;/Grid&gt; тегов, добавьте следующий hello кода toodefine элемент управления listbox, чтобы пользователи могли видеть список доступных потоков hello и выберите потоки:

         <Grid Name="gridStreamAndBitrateSelection" Grid.Row="3">
            <Grid.RowDefinitions>
                <RowDefinition Height="300"/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="250*"/>
                <ColumnDefinition Width="250*"/>
            </Grid.ColumnDefinitions>
            <StackPanel Name="spStreamSelection" Grid.Row="1" Grid.Column="0">
                <StackPanel Orientation="Horizontal">
                    <TextBlock Name="tbAvailableStreams" Text="Available Streams:" FontSize="16" VerticalAlignment="Center"></TextBlock>
                    <Button Name="btnChangeStreams" Content="Submit" Click="btnChangeStream_Click"/>
                </StackPanel>
                <ListBox x:Name="lbAvailableStreams" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                    ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
                    <ListBox.ItemTemplate>
                        <DataTemplate>
                            <CheckBox Content="{Binding Name}" IsChecked="{Binding isChecked, Mode=TwoWay}" />
                        </DataTemplate>
                    </ListBox.ItemTemplate>
                </ListBox>
            </StackPanel>
         </Grid>
4. Нажмите клавишу **CTRL + S** toosave hello изменения.

**файл с выделенным кодом toomodify hello**

1. В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.
2. В пределах пространства имен SSPlayer hello добавьте новый класс:
   
        #region class Stream
   
        public class Stream
        {
            private IManifestStream stream;
            public bool isCheckedValue;
            public string name;
   
            public string Name
            {
                get { return name; }
                set { name = value; }
            }
   
            public IManifestStream ManifestStream
            {
                get { return stream; }
                set { stream = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    // mMke hello video stream always checked.
                    if (stream.Type == MediaStreamType.Video)
                    {
                        isCheckedValue = true;
                    }
                    else
                    {
                        isCheckedValue = value;
                    }
                }
            }
   
            public Stream(IManifestStream streamIn)
            {
                stream = streamIn;
                name = stream.Name;
            }
        }
        #endregion class Stream
3. В начале hello hello класса MainPage, добавьте hello после определения переменной:
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. В пределах hello класса MainPage добавьте hello следующие области:
   
        #region stream selection
        ///<summary>
        ///Functionality tooselect streams from IManifestStream available streams
        /// </summary>
   
        // This function is called from hello mediaElement_ManifestReady event handler 
        // tooretrieve hello streams and populate them toohello local data members.
        public void getStreams(Manifest manifestObject)
        {
            availableStreams = new List<Stream>();
            availableVideoStreams = new List<Stream>();
            availableAudioStreams = new List<Stream>();
            availableTextStreams = new List<Stream>();
   
            try
            {
                for (int i = 0; i<manifestObject.AvailableStreams.Count; i++)
                {
                    Stream newStream = new Stream(manifestObject.AvailableStreams[i]);
                    newStream.isChecked = false;
   
                    //populate hello stream lists based on hello types
                    availableStreams.Add(newStream);
   
                    switch (newStream.ManifestStream.Type)
                    {
                        case MediaStreamType.Video:
                            availableVideoStreams.Add(newStream);
                            break;
                        case MediaStreamType.Audio:
                            availableAudioStreams.Add(newStream);
                            break;
                        case MediaStreamType.Text:
                            availableTextStreams.Add(newStream);
                            break;
                    }
   
                    // Select hello default selected streams from hello manifest.
                    for (int j = 0; j<manifestObject.SelectedStreams.Count; j++)
                    {
                        string selectedStreamName = manifestObject.SelectedStreams[j].Name;
                        if (selectedStreamName.Equals(newStream.Name))
                        {
                            newStream.isChecked = true;
                            break;
                        }
                    }
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function set hello list box ItemSource
        private async void refreshAvailableStreamsListBoxItemSource()
        {
            try
            {
                //update hello stream check box list on hello UI
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableStreams.ItemsSource = availableStreams; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function creates a selected streams list
        private void createSelectedStreamsList(List<IManifestStream> selectedStreams)
        {
            bool isOneVideoSelected = false;
            bool isOneAudioSelected = false;
   
            // Only one video stream can be selected
            for (int j = 0; j<availableVideoStreams.Count; j++)
            {
                if (availableVideoStreams[j].isChecked && (!isOneVideoSelected))
                {
                    selectedStreams.Add(availableVideoStreams[j].ManifestStream);
                    isOneVideoSelected = true;
                }
            }
   
            // Select hello frist video stream from hello list if no video stream is selected
            if (!isOneVideoSelected)
            {
                availableVideoStreams[0].isChecked = true;
                selectedStreams.Add(availableVideoStreams[0].ManifestStream);
            }
   
            // Only one audio stream can be selected
            for (int j = 0; j<availableAudioStreams.Count; j++)
            {
                if (availableAudioStreams[j].isChecked && (!isOneAudioSelected))
                {
                    selectedStreams.Add(availableAudioStreams[j].ManifestStream);
                    isOneAudioSelected = true;
                    txtStatus.Text = "hello audio stream is changed too" + availableAudioStreams[j].ManifestStream.Name;
                }
            }
   
            // Select hello frist audio stream from hello list if no audio steam is selected.
            if (!isOneAudioSelected)
            {
                availableAudioStreams[0].isChecked = true;
                selectedStreams.Add(availableAudioStreams[0].ManifestStream);
            }
   
            // Multiple text streams are supported.
            for (int j = 0; j < availableTextStreams.Count; j++)
            {
                if (availableTextStreams[j].isChecked)
                {
                    selectedStreams.Add(availableTextStreams[j].ManifestStream);
                }
            }
        }
   
        // Change streams on a smooth streaming presentation with multiple video streams.
        private async void changeStreams(List<IManifestStream> selectStreams)
        {
            try
            {
                IReadOnlyList<IStreamChangedResult> returnArgs =
                    await manifestObject.SelectStreamsAsync(selectStreams);
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
        #endregion stream selection
5. Найдите метод mediaElement_ManifestReady hello, добавьте следующий код в конце hello функции hello hello:
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    Поэтому при готовности манифест MediaElement кода hello Получает список доступных потоков hello и заполняет hello пользовательского интерфейса списка со списком hello.
6. Внутри hello класса MainPage, найдите кнопками ИП hello выберите регион события, а затем добавьте следующие определения функции hello:
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on hello presentation
            changeStreams(selectedStreams);
        }

**toocompile и тестирования приложения hello**

1. Нажмите клавишу **F6** toocompile hello проекта. 
2. Нажмите клавишу **F5** toorun приложения hello.
3. Вверху hello приложения hello можно использовать значение по умолчанию hello Smooth Streaming URL-адрес или введите его. 
4. Щелкните **Задать источник**. 
5. язык по умолчанию Hello — audio_eng. Попробуйте tooswitch между audio_eng и audio_es. При каждом, выберите новый поток, необходимо нажать кнопку Submit hello.

Вы завершили урок 3.  На этом занятии добавьте потоки toochoose функции hello.

## <a name="lesson-4-select-smooth-streaming-tracks"></a>Урок 4. Выбор дорожек для бесперебойной потоковой передачи
Представление бесперебойной потоковой передачи может содержать несколько видеофайлов, зашифрованных с разными уровнями качества (скоростью) и разрешениями. На этом занятии вы включите отслеживает tooselect пользователей. Это занятие содержит hello следующих процедур.

1. Измените файл XAML hello
2. Измените файл behand кода hello
3. Компиляции и тестирования приложения hello

**toomodify hello XAML-файла**

1. В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Конструктор представлений**.
2. Найдите hello &lt;сетки&gt; тег с именем hello **gridStreamAndBitrateSelection**, добавьте следующий код в конце hello тег hello hello:
   
         <StackPanel Name="spBitRateSelection" Grid.Row="1" Grid.Column="1">
         <StackPanel Orientation="Horizontal">
             <TextBlock Name="tbBitRate" Text="Available Bitrates:" FontSize="16" VerticalAlignment="Center"/>
             <Button Name="btnChangeTracks" Content="Submit" Click="btnChangeTrack_Click" />
         </StackPanel>
         <ListBox x:Name="lbAvailableVideoTracks" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                  ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
             <ListBox.ItemTemplate>
                 <DataTemplate>
                     <CheckBox Content="{Binding Bitrate}" IsChecked="{Binding isChecked, Mode=TwoWay}"/>
                 </DataTemplate>
             </ListBox.ItemTemplate>
         </ListBox>
         </StackPanel>
3. Нажмите клавишу **CTRL + S** toosave, он изменяет

**файл с выделенным кодом toomodify hello**

1. В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.
2. В пределах пространства имен SSPlayer hello добавьте новый класс:
   
        #region class Track
        public class Track
        {
            private IManifestTrack trackInfo;
            public string _bitrate;
            public bool isCheckedValue;
   
            public IManifestTrack TrackInfo
            {
                get { return trackInfo; }
                set { trackInfo = value; }
            }
   
            public string Bitrate
            {
                get { return _bitrate; }
                set { _bitrate = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    isCheckedValue = value;
                }
            }
   
            public Track(IManifestTrack trackInfoIn)
            {
                trackInfo = trackInfoIn;
                _bitrate = trackInfoIn.Bitrate.ToString();
            }
            //public Track() { }
        }
        #endregion class Track
3. В начале hello hello класса MainPage, добавьте hello после определения переменной:
   
        private List<Track> availableTracks;
4. В пределах hello класса MainPage добавьте hello следующие области:
   
        #region track selection
        /// <summary>
        /// Functionality tooselect video streams
        /// </summary>
   
        /// This Function gets hello tracks for hello selected video stream
        public void getTracks(Manifest manifestObject)
        {
            availableTracks = new List<Track>();
   
            IManifestStream videoStream = getVideoStream();
            IReadOnlyList<IManifestTrack> availableTracksLocal = videoStream.AvailableTracks;
            IReadOnlyList<IManifestTrack> selectedTracksLocal = videoStream.SelectedTracks;
   
            try
            {
                for (int i = 0; i < availableTracksLocal.Count; i++)
                {
                    Track thisTrack = new Track(availableTracksLocal[i]);
                    thisTrack.isChecked = true;
   
                    for (int j = 0; j < selectedTracksLocal.Count; j++)
                    {
                        string selectedTrackName = selectedTracksLocal[j].Bitrate.ToString();
                        if (selectedTrackName.Equals(thisTrack.Bitrate))
                        {
                            thisTrack.isChecked = true;
                            break;
                        }
                    }
                    availableTracks.Add(thisTrack);
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = e.Message;
            }
        }
   
        // This function gets hello video stream that is playing
        private IManifestStream getVideoStream()
        {
            IManifestStream videoStream = null;
            for (int i = 0; i < manifestObject.SelectedStreams.Count; i++)
            {
                if (manifestObject.SelectedStreams[i].Type == MediaStreamType.Video)
                {
                    videoStream = manifestObject.SelectedStreams[i];
                    break;
                }
            }
            return videoStream;
        }
   
        // This function set hello UI list box control ItemSource
        private async void refreshAvailableTracksListBoxItemSource()
        {
            try
            {
                // Update hello track check box list on hello UI 
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableVideoTracks.ItemsSource = availableTracks; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }        
        }
   
        // This function creates a list of hello selected tracks.
        private void createSelectedTracksList(List<IManifestTrack> selectedTracks)
        {
            // Create a list of selected tracks
            for (int j = 0; j < availableTracks.Count; j++)
            {
                if (availableTracks[j].isCheckedValue == true)
                {
                    selectedTracks.Add(availableTracks[j].TrackInfo);
                }
            }
        }
   
        // This function selects hello tracks based on user selection 
        private void changeTracks(List<IManifestTrack> selectedTracks)
        {
            IManifestStream videoStream = getVideoStream();
            try
            {
                videoStream.SelectTracks(selectedTracks);
            }
            catch (Exception ex)
            {
                txtStatus.Text = ex.Message;
            }
        }
        #endregion track selection
5. Найдите метод mediaElement_ManifestReady hello, добавьте следующий код в конце hello функции hello hello:
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. Внутри hello класса MainPage, найдите кнопками ИП hello выберите регион события, а затем добавьте следующие определения функции hello:
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on hello presentation
            changeStreams(selectedStreams);
         }

**toocompile и тестирования приложения hello**

1. Нажмите клавишу **F6** toocompile hello проекта. 
2. Нажмите клавишу **F5** toorun приложения hello.
3. Вверху hello приложения hello можно использовать значение по умолчанию hello Smooth Streaming URL-адрес или введите его. 
4. Щелкните **Задать источник**. 
5. По умолчанию выбираются все записи hello hello видеопотока. tooexperiment hello бит скорость изменения, можно выберите hello низкий битрейт доступны, а затем выберите hello наибольший скорость доступны. После каждого изменения необходимо нажать кнопку "Отправить".  Можно заметить изменения качества видео hello.

Вы завершили урок 4.  На этом занятии добавьте отслеживает toochoose функции hello.

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a>Другие ресурсы:
* [Как toobuild приложении Smooth Streaming Windows 8 на языке JavaScript с помощью дополнительных возможностей](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [Технический обзор Smooth Streaming](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

