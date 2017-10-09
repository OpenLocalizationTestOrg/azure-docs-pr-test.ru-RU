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
# <a name="how-toobuild-a-smooth-streaming-windows-store-application"></a><span data-ttu-id="b2369-103">Как tooBuild приложения Smooth Streaming Windows Store</span><span class="sxs-lookup"><span data-stu-id="b2369-103">How tooBuild a Smooth Streaming Windows Store Application</span></span>

<span data-ttu-id="b2369-104">Hello Smooth Streaming клиента SDK для Windows 8 позволяет приложениям магазина Windows toobuild разработчики, которые могут играть по требованию и динамического содержимого Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="b2369-104">hello Smooth Streaming Client SDK for Windows 8 enables developers toobuild Windows Store applications that can play on-demand and live Smooth Streaming content.</span></span> <span data-ttu-id="b2369-105">В дополнение к этому toohello основные воспроизведения Smooth Streaming содержимое hello SDK также предоставляет богатые возможности, как Microsoft PlayReady protection, ограничение на уровни качества, Live DVR аудиопотока переключения, Ожидание обновления состояния (например, изменения уровня качества ) и событий ошибок и т. д.</span><span class="sxs-lookup"><span data-stu-id="b2369-105">In addition toohello basic playback of Smooth Streaming content, hello SDK also provides rich features like Microsoft PlayReady protection, quality level restriction, Live DVR, audio stream switching, listening for status updates (such as quality level changes) and error events, and so on.</span></span> <span data-ttu-id="b2369-106">Функции hello поддерживается Дополнительные сведения см. в разделе hello [заметки о выпуске](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span><span class="sxs-lookup"><span data-stu-id="b2369-106">For more information of hello supported features, see hello [release notes](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span></span> <span data-ttu-id="b2369-107">Дополнительные сведения см. на странице, посвященной [Player Framework для Windows 8](http://playerframework.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="b2369-107">For more information, see [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span></span> 

<span data-ttu-id="b2369-108">Этот учебный курс состоит из четырех занятий:</span><span class="sxs-lookup"><span data-stu-id="b2369-108">This tutorial contains four lessons:</span></span>

1. <span data-ttu-id="b2369-109">Создание базового приложения магазина с бесперебойной потоковой передачей</span><span class="sxs-lookup"><span data-stu-id="b2369-109">Create a Basic Smooth Streaming Store Application</span></span>
2. <span data-ttu-id="b2369-110">Добавить ползунок hello tooControl Media хода выполнения</span><span class="sxs-lookup"><span data-stu-id="b2369-110">Add a Slider Bar tooControl hello Media Progress</span></span>
3. <span data-ttu-id="b2369-111">Выбор потоков для бесперебойной потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="b2369-111">Select Smooth Streaming Streams</span></span>
4. <span data-ttu-id="b2369-112">Выбор дорожек для бесперебойной потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="b2369-112">Select Smooth Streaming Tracks</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2369-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b2369-113">Prerequisites</span></span>
* <span data-ttu-id="b2369-114">Windows 8 (32-разрядная или 64-разрядная).</span><span class="sxs-lookup"><span data-stu-id="b2369-114">Windows 8 32-bit or 64-bit.</span></span> <span data-ttu-id="b2369-115">Можно получить [оценку Windows 8 Enterprise](http://msdn.microsoft.com/evalcenter/jj554510.aspx) из MSDN.</span><span class="sxs-lookup"><span data-stu-id="b2369-115">You can get [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) from MSDN.</span></span>
* <span data-ttu-id="b2369-116">Visual Studio 2012 или Visual Studio Express 2012 (либо более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="b2369-116">Visual Studio 2012 or Visual Studio Express 2012 (or a later version).</span></span> <span data-ttu-id="b2369-117">Можно получить пробную версию hello из [здесь](http://www.microsoft.com/visualstudio/11/downloads).</span><span class="sxs-lookup"><span data-stu-id="b2369-117">You can get hello trial version from [here](http://www.microsoft.com/visualstudio/11/downloads).</span></span>
* <span data-ttu-id="b2369-118">[Клиентский пакет SDK для бесперебойной потоковой передачи Microsoft для Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home)</span><span class="sxs-lookup"><span data-stu-id="b2369-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span></span>

<span data-ttu-id="b2369-119">решение Hello завершена для всех занятий можно загрузить из примеров кода MSDN для разработчиков (Галерея кода):</span><span class="sxs-lookup"><span data-stu-id="b2369-119">hello completed solution for each lesson can be downloaded from MSDN Developer Code Samples (Code Gallery):</span></span> 

* <span data-ttu-id="b2369-120">[Урок 1.](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) Простой мультимедиапроигрыватель для Windows 8 с потоковой передачей Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="b2369-120">[Lesson 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - A Simple Windows 8 Smooth Streaming Media Player,</span></span> 
* <span data-ttu-id="b2369-121">[Урок 2.](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) Простой мультимедиапроигрыватель для Windows 8 с потоковой передачей Smooth Streaming и элементом управления «Ползунок».</span><span class="sxs-lookup"><span data-stu-id="b2369-121">[Lesson 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - A Simple Windows 8 Smooth Streaming Media Player with a Slider Bar Control,</span></span> 
* <span data-ttu-id="b2369-122">[Урок 3.](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) Простой мультимедиапроигрыватель для Windows 8 с потоковой передачей Smooth Streaming и выбором потока.</span><span class="sxs-lookup"><span data-stu-id="b2369-122">[Lesson 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - A Windows 8 Smooth Streaming Media Player with Stream Selection,</span></span>  
* <span data-ttu-id="b2369-123">[Урок 4.](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) Мультимедиапроигрыватель для Windows 8 с потоковой передачей Smooth Streaming и выбором дорожки.</span><span class="sxs-lookup"><span data-stu-id="b2369-123">[Lesson 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907)  - A Windows 8 Smooth Streaming Media Player with Track Selection.</span></span>

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a><span data-ttu-id="b2369-124">Урок 1. Создание базового приложения для магазина с бесперебойной потоковой передачей</span><span class="sxs-lookup"><span data-stu-id="b2369-124">Lesson 1: Create a Basic Smooth Streaming Store Application</span></span>

<span data-ttu-id="b2369-125">На этом занятии вы создадите приложения для магазина Windows с помощью элемента управления MediaElement tooplay Smooth потока содержимого.</span><span class="sxs-lookup"><span data-stu-id="b2369-125">In this lesson, you will create a Windows Store application with a MediaElement control tooplay Smooth Stream content.</span></span>  <span data-ttu-id="b2369-126">запущенное приложение Hello выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="b2369-126">hello running application looks like:</span></span>

![Пример приложения для магазина Windows с бесперебойной потоковой передачей][PlayerApplication]

<span data-ttu-id="b2369-128">Дополнительные сведения о разработке приложений Магазина Windows см. в разделе, посвященном [разработке потрясающих приложений для Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2369-128">For more information on developing Windows Store application, see [Develop Great Apps for Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span></span> <span data-ttu-id="b2369-129">Это занятие содержит hello следующих процедур.</span><span class="sxs-lookup"><span data-stu-id="b2369-129">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="b2369-130">Создание проекта для магазина Windows</span><span class="sxs-lookup"><span data-stu-id="b2369-130">Create a Windows Store project</span></span>
2. <span data-ttu-id="b2369-131">Разработка пользовательского интерфейса hello (XAML)</span><span class="sxs-lookup"><span data-stu-id="b2369-131">Design hello user interface (XAML)</span></span>
3. <span data-ttu-id="b2369-132">Измените файл с выделенным кодом hello</span><span class="sxs-lookup"><span data-stu-id="b2369-132">Modify hello code behind file</span></span>
4. <span data-ttu-id="b2369-133">Компиляции и тестирования приложения hello</span><span class="sxs-lookup"><span data-stu-id="b2369-133">Compile and test hello application</span></span>

<span data-ttu-id="b2369-134">**toocreate проекта магазина Windows**</span><span class="sxs-lookup"><span data-stu-id="b2369-134">**toocreate a Windows Store project**</span></span>

1. <span data-ttu-id="b2369-135">Запустите Visual Studio 2012 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="b2369-135">Run Visual Studio 2012 or later.</span></span>
2. <span data-ttu-id="b2369-136">Из hello **ФАЙЛ** меню, нажмите кнопку **New**, а затем нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="b2369-136">From hello **FILE** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="b2369-137">В диалоговом окне нового проекта hello типа или выберите hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="b2369-137">From hello New Project dialog, type or select  hello following values:</span></span>

| <span data-ttu-id="b2369-138">Имя</span><span class="sxs-lookup"><span data-stu-id="b2369-138">Name</span></span> | <span data-ttu-id="b2369-139">Значение</span><span class="sxs-lookup"><span data-stu-id="b2369-139">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b2369-140">Группа шаблонов</span><span class="sxs-lookup"><span data-stu-id="b2369-140">Template group</span></span> |<span data-ttu-id="b2369-141">Installed/Templates/Visual C#/Windows Store</span><span class="sxs-lookup"><span data-stu-id="b2369-141">Installed/Templates/Visual C#/Windows Store</span></span> |
| <span data-ttu-id="b2369-142">Шаблон</span><span class="sxs-lookup"><span data-stu-id="b2369-142">Template</span></span> |<span data-ttu-id="b2369-143">Пустое приложение (XAML)</span><span class="sxs-lookup"><span data-stu-id="b2369-143">Blank App (XAML)</span></span> |
| <span data-ttu-id="b2369-144">Имя</span><span class="sxs-lookup"><span data-stu-id="b2369-144">Name</span></span> |<span data-ttu-id="b2369-145">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="b2369-145">SSPlayer</span></span> |
| <span data-ttu-id="b2369-146">Расположение</span><span class="sxs-lookup"><span data-stu-id="b2369-146">Location</span></span> |<span data-ttu-id="b2369-147">C:\SSTutorials</span><span class="sxs-lookup"><span data-stu-id="b2369-147">C:\SSTutorials</span></span> |
| <span data-ttu-id="b2369-148">Имя решения</span><span class="sxs-lookup"><span data-stu-id="b2369-148">Solution Name</span></span> |<span data-ttu-id="b2369-149">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="b2369-149">SSPlayer</span></span> |
| <span data-ttu-id="b2369-150">Создать каталог для решения</span><span class="sxs-lookup"><span data-stu-id="b2369-150">Create directory for solution</span></span> |<span data-ttu-id="b2369-151">(выбрано)</span><span class="sxs-lookup"><span data-stu-id="b2369-151">(selected)</span></span> |

1. <span data-ttu-id="b2369-152">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b2369-152">Click **OK**.</span></span>

<span data-ttu-id="b2369-153">**tooadd ссылки toohello Smooth Streaming Client SDK**</span><span class="sxs-lookup"><span data-stu-id="b2369-153">**tooadd a reference toohello Smooth Streaming Client SDK**</span></span>

1. <span data-ttu-id="b2369-154">В обозревателе решений щелкните правой кнопкой мыши **SSPlayer**, а затем выберите команду **Добавить ссылку**.</span><span class="sxs-lookup"><span data-stu-id="b2369-154">From Solution Explorer, right-click **SSPlayer**, and then click **Add Reference**.</span></span>
2. <span data-ttu-id="b2369-155">Введите или выберите hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="b2369-155">Type or select hello following values:</span></span>

| <span data-ttu-id="b2369-156">Имя</span><span class="sxs-lookup"><span data-stu-id="b2369-156">Name</span></span> | <span data-ttu-id="b2369-157">Значение</span><span class="sxs-lookup"><span data-stu-id="b2369-157">Value</span></span> |
| --- | --- |
| <span data-ttu-id="b2369-158">Ссылочная группа</span><span class="sxs-lookup"><span data-stu-id="b2369-158">Reference group</span></span> |<span data-ttu-id="b2369-159">Windows/Расширения</span><span class="sxs-lookup"><span data-stu-id="b2369-159">Windows/Extensions</span></span> |
| <span data-ttu-id="b2369-160">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="b2369-160">Reference</span></span> |<span data-ttu-id="b2369-161">Выберите клиентский пакет SDK бесперебойной потоковой передачи Microsoft для Windows 8 и пакет среды выполнения Microsoft Visual C++</span><span class="sxs-lookup"><span data-stu-id="b2369-161">Select Microsoft Smooth Streaming Client SDK for Windows 8 and Microsoft Visual C++ Runtime Package</span></span> |

1. <span data-ttu-id="b2369-162">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b2369-162">Click **OK**.</span></span> 

<span data-ttu-id="b2369-163">После добавления ссылки на hello, необходимо выбрать hello целевой платформы (x64 или x86), добавления ссылок не будет работать для конфигурации платформы любой ЦП.</span><span class="sxs-lookup"><span data-stu-id="b2369-163">After adding hello references, you must select hello targeted platform (x64 or x86), adding references will not work for Any CPU platform configuration.</span></span>  <span data-ttu-id="b2369-164">Для таких добавленных ссылок в обозревателе решений будет выведен желтый значок предупреждения.</span><span class="sxs-lookup"><span data-stu-id="b2369-164">In solution explorer, you will see yellow warning mark for these added references.</span></span>

<span data-ttu-id="b2369-165">**toodesign hello проигрывателя пользовательского интерфейса**</span><span class="sxs-lookup"><span data-stu-id="b2369-165">**toodesign hello player user interface**</span></span>

1. <span data-ttu-id="b2369-166">В обозревателе решений дважды щелкните **MainPage.xaml** tooopen его в конструктор hello просмотра.</span><span class="sxs-lookup"><span data-stu-id="b2369-166">From Solution Explorer, double click **MainPage.xaml** tooopen it in hello design view.</span></span>
2. <span data-ttu-id="b2369-167">Найдите hello  **&lt;сетки&gt;**  и  **&lt;/Grid&gt;**  теги hello XAML-файл, и следующие hello вставить код между тегами hello двух:</span><span class="sxs-lookup"><span data-stu-id="b2369-167">Locate hello **&lt;Grid&gt;** and **&lt;/Grid&gt;**  tags hello XAML file, and paste hello following code between hello two tags:</span></span>

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
   
   <span data-ttu-id="b2369-168">Hello управления MediaElement — используется tooplayback мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b2369-168">hello MediaElement control is used tooplayback media.</span></span> <span data-ttu-id="b2369-169">элемент управления "ползунок" Hello, с именем sliderProgress будет использоваться идет hello Далее занятия toocontrol hello носителя.</span><span class="sxs-lookup"><span data-stu-id="b2369-169">hello slider control named sliderProgress will be used in hello next lesson toocontrol hello media progress.</span></span>
3. <span data-ttu-id="b2369-170">Нажмите клавишу **CTRL + S** toosave hello файла.</span><span class="sxs-lookup"><span data-stu-id="b2369-170">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="b2369-171">Hello управления MediaElement не поддерживает Smooth Streaming содержимого out-of-box.</span><span class="sxs-lookup"><span data-stu-id="b2369-171">hello MediaElement control does not support Smooth Streaming content out-of-box.</span></span> <span data-ttu-id="b2369-172">Поддержка Smooth Streaming tooenable hello, необходимо зарегистрировать обработчик hello потока байтов в Smooth Streaming, расширение имени файла и тип MIME.</span><span class="sxs-lookup"><span data-stu-id="b2369-172">tooenable hello Smooth Streaming support, you must register hello Smooth Streaming byte-stream handler by file name extension and MIME type.</span></span>  <span data-ttu-id="b2369-173">tooregister, используйте метод MediaExtensionManager.RegisterByteStremHandler hello пространства имен Windows.Media hello.</span><span class="sxs-lookup"><span data-stu-id="b2369-173">tooregister, you use hello MediaExtensionManager.RegisterByteStremHandler method of hello Windows.Media namespace.</span></span>

<span data-ttu-id="b2369-174">В этом файле XAML некоторые обработчики событий связаны с элементами управления hello.</span><span class="sxs-lookup"><span data-stu-id="b2369-174">In this XAML file, some event handlers are associated with hello controls.</span></span>  <span data-ttu-id="b2369-175">Такие обработчики событий необходимо определить.</span><span class="sxs-lookup"><span data-stu-id="b2369-175">You must define those event handlers.</span></span>

<span data-ttu-id="b2369-176">**файл с выделенным кодом toomodify hello**</span><span class="sxs-lookup"><span data-stu-id="b2369-176">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="b2369-177">В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.</span><span class="sxs-lookup"><span data-stu-id="b2369-177">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="b2369-178">В начале hello hello файла, добавьте следующее hello с помощью инструкции:</span><span class="sxs-lookup"><span data-stu-id="b2369-178">At hello top of hello file, add hello following using statement:</span></span>
   
        using Windows.Media;
3. <span data-ttu-id="b2369-179">В начале hello hello **MainPage** добавьте hello после элемента данных:</span><span class="sxs-lookup"><span data-stu-id="b2369-179">At hello beginning of hello **MainPage** class, add hello following data member:</span></span>
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. <span data-ttu-id="b2369-180">В конце hello hello **MainPage** конструктор, добавить hello, следующие две строки:</span><span class="sxs-lookup"><span data-stu-id="b2369-180">At hello end of hello **MainPage** constructor, add hello following two lines:</span></span>
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. <span data-ttu-id="b2369-181">В конце hello hello **MainPage** класса, вставьте hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="b2369-181">At hello end of hello **MainPage** class, paste hello following code:</span></span>
   
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

<span data-ttu-id="b2369-182">Здесь определяется обработчик события sliderProgress_PointerPressed Hello.</span><span class="sxs-lookup"><span data-stu-id="b2369-182">hello sliderProgress_PointerPressed event handler is defined here.</span></span>  <span data-ttu-id="b2369-183">Существуют дополнительные tooget toodo works его работы, который будет рассматриваться в hello следующем занятии этого учебника.</span><span class="sxs-lookup"><span data-stu-id="b2369-183">There are more works toodo tooget it working, which will be covered in hello next lesson of this tutorial.</span></span>
6. <span data-ttu-id="b2369-184">Нажмите клавишу **CTRL + S** toosave hello файла.</span><span class="sxs-lookup"><span data-stu-id="b2369-184">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="b2369-185">Hello готовой hello файл кода программной части должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b2369-185">hello finished hello code behind file shall look like this:</span></span>

![Просмотр кода в Visual Studio для приложения для магазина Windows с бесперебойной потоковой передачей][CodeViewPic]

<span data-ttu-id="b2369-187">**toocompile и тестирования приложения hello**</span><span class="sxs-lookup"><span data-stu-id="b2369-187">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="b2369-188">Из hello **ПОСТРОЕНИЯ** меню, нажмите кнопку **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="b2369-188">From hello **BUILD** menu, click **Configuration Manager**.</span></span>
2. <span data-ttu-id="b2369-189">Изменение **Активная платформа решения** toomatch платформу разработки.</span><span class="sxs-lookup"><span data-stu-id="b2369-189">Change **Active solution platform** toomatch your development platform.</span></span>
3. <span data-ttu-id="b2369-190">Нажмите клавишу **F6** toocompile hello проекта.</span><span class="sxs-lookup"><span data-stu-id="b2369-190">Press **F6** toocompile hello project.</span></span> 
4. <span data-ttu-id="b2369-191">Нажмите клавишу **F5** toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b2369-191">Press **F5** toorun hello application.</span></span>
5. <span data-ttu-id="b2369-192">Вверху hello приложения hello можно использовать значение по умолчанию hello Smooth Streaming URL-адрес или введите его.</span><span class="sxs-lookup"><span data-stu-id="b2369-192">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
6. <span data-ttu-id="b2369-193">Щелкните **Задать источник**.</span><span class="sxs-lookup"><span data-stu-id="b2369-193">Click **Set Source**.</span></span> <span data-ttu-id="b2369-194">Поскольку **автовоспроизведения** включена по умолчанию hello должны автоматического воспроизведения мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b2369-194">Because **Auto Play** is enabled by default, hello media shall play automatically.</span></span>  <span data-ttu-id="b2369-195">Можно управлять hello мультимедиа с помощью hello **воспроизведение**, **Пауза** и **остановить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="b2369-195">You can control hello media using hello **Play**, **Pause** and **Stop** buttons.</span></span>  <span data-ttu-id="b2369-196">Можно управлять с помощью ползунка вертикальной hello том носителя hello.</span><span class="sxs-lookup"><span data-stu-id="b2369-196">You can control hello media volume using hello vertical slider.</span></span>  <span data-ttu-id="b2369-197">Однако hello горизонтальный ползунок для управления media выполняется еще не реализован полностью приветствия.</span><span class="sxs-lookup"><span data-stu-id="b2369-197">However hello horizontal slider for controlling hello media progress is not fully implemented yet.</span></span> 

<span data-ttu-id="b2369-198">Вы завершили урок 1.</span><span class="sxs-lookup"><span data-stu-id="b2369-198">You have completed lesson1.</span></span>  <span data-ttu-id="b2369-199">На этом занятии используйте tooplayback управления MediaElement содержимое Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="b2369-199">In this lesson, you use a MediaElement control tooplayback Smooth Streaming content.</span></span>  <span data-ttu-id="b2369-200">Hello следующем занятии вы добавите элемент ползунок toocontrol hello ход выполнения hello содержимое Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="b2369-200">In hello next lesson, you will add a slider toocontrol hello progress of hello Smooth Streaming content.</span></span>

## <a name="lesson-2-add-a-slider-bar-toocontrol-hello-media-progress"></a><span data-ttu-id="b2369-201">Занятие 2: Добавление ползунок hello tooControl Media хода выполнения</span><span class="sxs-lookup"><span data-stu-id="b2369-201">Lesson 2: Add a Slider Bar tooControl hello Media Progress</span></span>

<span data-ttu-id="b2369-202">На занятии 1 вы создали приложения для магазина Windows с tooplayback управления MediaElement XAML контента Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="b2369-202">In lesson 1, you created a Windows Store application with a MediaElement XAML control tooplayback Smooth Streaming media content.</span></span>  <span data-ttu-id="b2369-203">Этот элемент изначально имеет такие функции, как начало, останов и приостановка воспроизведения.</span><span class="sxs-lookup"><span data-stu-id="b2369-203">It comes some basic media functions like start, stop and pause.</span></span>  <span data-ttu-id="b2369-204">На этом занятии вы добавите приложение toohello панель элемента управления "ползунок".</span><span class="sxs-lookup"><span data-stu-id="b2369-204">In this lesson, you will add a slider bar control toohello application.</span></span>

<span data-ttu-id="b2369-205">В этом учебнике мы будем использовать таймер tooupdate hello положение ползунка на основе текущего положения hello hello управления MediaElement.</span><span class="sxs-lookup"><span data-stu-id="b2369-205">In this tutorial, we will use a timer tooupdate hello slider position based on hello current position of hello MediaElement control.</span></span>  <span data-ttu-id="b2369-206">ползунок Hello время начала и окончания также необходимость toobe обновляется в случае содержимого в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="b2369-206">hello slider start and end time also need toobe updated in case of live content.</span></span>  <span data-ttu-id="b2369-207">Это можно лучше обрабатывать в событии обновления hello адаптивной источника.</span><span class="sxs-lookup"><span data-stu-id="b2369-207">This can be better handled in hello adaptive source update event.</span></span>

<span data-ttu-id="b2369-208">Источники мультимедиа — это объекты, которые создают данные мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b2369-208">Media sources are objects that generate media data.</span></span>  <span data-ttu-id="b2369-209">Hello источника принимает поток URL-адрес или байт и создает соответствующий носитель hello источником этого содержимого.</span><span class="sxs-lookup"><span data-stu-id="b2369-209">hello source resolver takes a URL or byte stream and creates hello appropriate media source for that content.</span></span>  <span data-ttu-id="b2369-210">Сопоставитель Hello источника — hello стандартный способ источников мультимедиа toocreate приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b2369-210">hello source resolver is hello standard way for hello applications toocreate media sources.</span></span> 

<span data-ttu-id="b2369-211">Это занятие содержит hello следующих процедур.</span><span class="sxs-lookup"><span data-stu-id="b2369-211">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="b2369-212">Зарегистрируйте обработчик Smooth Streaming hello</span><span class="sxs-lookup"><span data-stu-id="b2369-212">Register hello Smooth Streaming handler</span></span> 
2. <span data-ttu-id="b2369-213">Добавьте обработчики событий уровня manager адаптивной источника hello</span><span class="sxs-lookup"><span data-stu-id="b2369-213">Add hello adaptive source manager level event handlers</span></span>
3. <span data-ttu-id="b2369-214">Добавление обработчиков событий уровня адаптивной источника hello</span><span class="sxs-lookup"><span data-stu-id="b2369-214">Add hello adaptive source level event handlers</span></span>
4. <span data-ttu-id="b2369-215">Добавление обработчиков событий MediaElement</span><span class="sxs-lookup"><span data-stu-id="b2369-215">Add MediaElement event handlers</span></span>
5. <span data-ttu-id="b2369-216">Добавление кода, связанного с ползунком</span><span class="sxs-lookup"><span data-stu-id="b2369-216">Add slider bar related code</span></span>
6. <span data-ttu-id="b2369-217">Компиляции и тестирования приложения hello</span><span class="sxs-lookup"><span data-stu-id="b2369-217">Compile and test hello application</span></span>

<span data-ttu-id="b2369-218">**tooregister hello потока байтов в Smooth Streaming обработчика и передайте hello propertyset**</span><span class="sxs-lookup"><span data-stu-id="b2369-218">**tooregister hello Smooth Streaming byte-stream handler and pass hello propertyset**</span></span>

1. <span data-ttu-id="b2369-219">В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.</span><span class="sxs-lookup"><span data-stu-id="b2369-219">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="b2369-220">В начале файла hello hello, добавьте следующее hello с помощью инструкции:</span><span class="sxs-lookup"><span data-stu-id="b2369-220">At hello beginning of hello file, add hello following using statement:</span></span>

        using Microsoft.Media.AdaptiveStreaming;
3. <span data-ttu-id="b2369-221">В начале hello hello класса MainPage, добавьте hello следующие элементы данных:</span><span class="sxs-lookup"><span data-stu-id="b2369-221">At hello beginning of hello MainPage class, add hello following data members:</span></span>

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. <span data-ttu-id="b2369-222">Внутри hello **MainPage** конструктора, добавьте следующий код после hello hello **это. Инициализация Components();**  строки и строки кода регистрации hello, написанных на предыдущем занятии hello:</span><span class="sxs-lookup"><span data-stu-id="b2369-222">Inside hello **MainPage** constructor, add hello following code after hello **this.Initialize Components();** line and hello registration code lines written in hello previous lesson:</span></span>

        // Gets hello default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value tooAdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. <span data-ttu-id="b2369-223">Внутри hello **MainPage** конструктор, д изменение hello tooadd методы RegisterByteStreamHandler hello двух параметров:</span><span class="sxs-lookup"><span data-stu-id="b2369-223">Inside hello **MainPage** constructor, modify hello two RegisterByteStreamHandler methods tooadd hello forth parameters:</span></span>

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
6. <span data-ttu-id="b2369-224">Нажмите клавишу **CTRL + S** toosave hello файла.</span><span class="sxs-lookup"><span data-stu-id="b2369-224">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="b2369-225">**tooadd hello адаптивной источника диспетчера событий уровня обработчика**</span><span class="sxs-lookup"><span data-stu-id="b2369-225">**tooadd hello adaptive source manager level event handler**</span></span>

1. <span data-ttu-id="b2369-226">В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.</span><span class="sxs-lookup"><span data-stu-id="b2369-226">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="b2369-227">Внутри hello **MainPage** добавьте hello после элемента данных:</span><span class="sxs-lookup"><span data-stu-id="b2369-227">Inside hello **MainPage** class, add hello following data member:</span></span>
   
     <span data-ttu-id="b2369-228">private AdaptiveSource adaptiveSource = null;</span><span class="sxs-lookup"><span data-stu-id="b2369-228">private AdaptiveSource adaptiveSource = null;</span></span>
3. <span data-ttu-id="b2369-229">В конце hello hello **MainPage** добавьте следующий обработчик событий hello:</span><span class="sxs-lookup"><span data-stu-id="b2369-229">At hello end of hello **MainPage** class, add hello following event handler:</span></span>
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. <span data-ttu-id="b2369-230">В конце hello hello **MainPage** конструктор, добавить следующие строки toosubscribe toohello адаптивной исходного открытые события hello:</span><span class="sxs-lookup"><span data-stu-id="b2369-230">At hello end of hello **MainPage** constructor, add hello following line toosubscribe toohello adaptive source open event:</span></span>
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. <span data-ttu-id="b2369-231">Нажмите клавишу **CTRL + S** toosave hello файла.</span><span class="sxs-lookup"><span data-stu-id="b2369-231">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="b2369-232">**обработчики событий уровня tooadd адаптивной источника**</span><span class="sxs-lookup"><span data-stu-id="b2369-232">**tooadd adaptive source level event handlers**</span></span>

1. <span data-ttu-id="b2369-233">В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.</span><span class="sxs-lookup"><span data-stu-id="b2369-233">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="b2369-234">Внутри hello **MainPage** добавьте hello после элемента данных:</span><span class="sxs-lookup"><span data-stu-id="b2369-234">Inside hello **MainPage** class, add hello following data member:</span></span>
   
     <span data-ttu-id="b2369-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span><span class="sxs-lookup"><span data-stu-id="b2369-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span></span>
3. <span data-ttu-id="b2369-236">В конце hello hello **MainPage** добавьте следующие обработчики событий hello:</span><span class="sxs-lookup"><span data-stu-id="b2369-236">At hello end of hello **MainPage** class, add hello following event handlers:</span></span>

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
4. <span data-ttu-id="b2369-237">В конце hello hello **mediaElement AdaptiveSourceOpened** метод, добавьте следующий код для событий toohello toosubscribe hello:</span><span class="sxs-lookup"><span data-stu-id="b2369-237">At hello end of hello **mediaElement AdaptiveSourceOpened** method, add hello following code toosubscribe toohello events:</span></span>
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. <span data-ttu-id="b2369-238">Нажмите клавишу **CTRL + S** toosave hello файла.</span><span class="sxs-lookup"><span data-stu-id="b2369-238">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="b2369-239">Здравствуйте, того же события, доступные на адаптивной диспетчера уровень источника, который может использоваться для обработки Общие элементы мультимедиа tooall функциональности в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="b2369-239">hello same events are available on Adaptive Source manger level as well, which can be used for handling functionality common tooall media elements in hello app.</span></span> <span data-ttu-id="b2369-240">Каждый адаптивный источник имеет свои собственные события, и все события AdaptiveSource будут передаваться каскадом в диспетчер AdaptiveSourceManager.</span><span class="sxs-lookup"><span data-stu-id="b2369-240">Each AdaptiveSource includes its own events and all AdaptiveSource events will be cascaded under AdaptiveSourceManager.</span></span>

<span data-ttu-id="b2369-241">**обработчики событий для элемента мультимедиа tooadd**</span><span class="sxs-lookup"><span data-stu-id="b2369-241">**tooadd Media Element event handlers**</span></span>

1. <span data-ttu-id="b2369-242">В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.</span><span class="sxs-lookup"><span data-stu-id="b2369-242">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="b2369-243">В конце hello hello **MainPage** добавьте следующие обработчики событий hello:</span><span class="sxs-lookup"><span data-stu-id="b2369-243">At hello end of hello **MainPage** class, add hello following event handlers:</span></span>

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
3. <span data-ttu-id="b2369-244">В конце hello hello **MainPage** конструктора, добавьте следующий код для событий toohello toosubscript hello:</span><span class="sxs-lookup"><span data-stu-id="b2369-244">At hello end of hello **MainPage** constructor, add hello following code toosubscript toohello events:</span></span>

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. <span data-ttu-id="b2369-245">Нажмите клавишу **CTRL + S** toosave hello файла.</span><span class="sxs-lookup"><span data-stu-id="b2369-245">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="b2369-246">**ползунок tooadd связанный код**</span><span class="sxs-lookup"><span data-stu-id="b2369-246">**tooadd slider bar related code**</span></span>

1. <span data-ttu-id="b2369-247">В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.</span><span class="sxs-lookup"><span data-stu-id="b2369-247">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="b2369-248">В начале файла hello hello, добавьте следующее hello с помощью инструкции:</span><span class="sxs-lookup"><span data-stu-id="b2369-248">At hello beginning of hello file, add hello following using statement:</span></span>
      
        using Windows.UI.Core;
3. <span data-ttu-id="b2369-249">Внутри hello **MainPage** добавьте следующие члены данных hello:</span><span class="sxs-lookup"><span data-stu-id="b2369-249">Inside hello **MainPage** class, add hello following data members:</span></span>
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. <span data-ttu-id="b2369-250">В конце hello hello **MainPage** конструктор, добавить hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="b2369-250">At hello end of hello **MainPage** constructor, add hello following code:</span></span>
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. <span data-ttu-id="b2369-251">В конце hello hello **MainPage** добавьте hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="b2369-251">At hello end of hello **MainPage** class, add hello following code:</span></span>

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
><span data-ttu-id="b2369-252">CoreDispatcher — используется toomake изменения потока toohello пользовательского интерфейса из потока без пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b2369-252">CoreDispatcher is used toomake changes toohello UI thread from non UI Thread.</span></span> <span data-ttu-id="b2369-253">В случае узкое место в поток dispatcher разработчика можно выбрать диспетчер toouse элементом пользовательского интерфейса при условии, что он планирует tooupdate.</span><span class="sxs-lookup"><span data-stu-id="b2369-253">In case of bottleneck on dispatcher thread, developer can choose toouse dispatcher provided by UI-element he/she intends tooupdate.</span></span>  <span data-ttu-id="b2369-254">Например:</span><span class="sxs-lookup"><span data-stu-id="b2369-254">For example:</span></span>
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. <span data-ttu-id="b2369-255">В конце hello hello **mediaElement_AdaptiveSourceStatusUpdated** метод, добавить hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="b2369-255">At hello end of hello **mediaElement_AdaptiveSourceStatusUpdated** method, add hello following code:</span></span>

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. <span data-ttu-id="b2369-256">В конце hello hello **MediaOpened** метод, добавить hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="b2369-256">At hello end of hello **MediaOpened** method, add hello following code:</span></span>

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. <span data-ttu-id="b2369-257">Нажмите клавишу **CTRL + S** toosave hello файла.</span><span class="sxs-lookup"><span data-stu-id="b2369-257">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="b2369-258">**toocompile и тестирования приложения hello**</span><span class="sxs-lookup"><span data-stu-id="b2369-258">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="b2369-259">Нажмите клавишу **F6** toocompile hello проекта.</span><span class="sxs-lookup"><span data-stu-id="b2369-259">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="b2369-260">Нажмите клавишу **F5** toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b2369-260">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="b2369-261">Вверху hello приложения hello можно использовать значение по умолчанию hello Smooth Streaming URL-адрес или введите его.</span><span class="sxs-lookup"><span data-stu-id="b2369-261">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="b2369-262">Щелкните **Задать источник**.</span><span class="sxs-lookup"><span data-stu-id="b2369-262">Click **Set Source**.</span></span> 
5. <span data-ttu-id="b2369-263">Ползунок hello теста.</span><span class="sxs-lookup"><span data-stu-id="b2369-263">Test hello slider bar.</span></span>

<span data-ttu-id="b2369-264">Вы завершили урок 2.</span><span class="sxs-lookup"><span data-stu-id="b2369-264">You have completed lesson 2.</span></span>  <span data-ttu-id="b2369-265">На этом занятии вы добавили tooapplication ползунок.</span><span class="sxs-lookup"><span data-stu-id="b2369-265">In this lesson you added a slider tooapplication.</span></span> 

## <a name="lesson-3-select-smooth-streaming-streams"></a><span data-ttu-id="b2369-266">Урок 3. Выбор потоков для бесперебойной потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="b2369-266">Lesson 3: Select Smooth Streaming Streams</span></span>
<span data-ttu-id="b2369-267">Smooth Streaming — поддержкой toostream содержимого с помощью нескольких языков звуковые файлы, доступны для выбора путем просмотра hello.</span><span class="sxs-lookup"><span data-stu-id="b2369-267">Smooth Streaming is capable toostream content with multiple language audio tracks that are selectable by hello viewers.</span></span>  <span data-ttu-id="b2369-268">На этом занятии вы включите потоки tooselect средства просмотра.</span><span class="sxs-lookup"><span data-stu-id="b2369-268">In this lesson, you will enable viewers tooselect streams.</span></span> <span data-ttu-id="b2369-269">Это занятие содержит hello следующих процедур.</span><span class="sxs-lookup"><span data-stu-id="b2369-269">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="b2369-270">Измените файл XAML hello</span><span class="sxs-lookup"><span data-stu-id="b2369-270">Modify hello XAML file</span></span>
2. <span data-ttu-id="b2369-271">Измените файл behand кода hello</span><span class="sxs-lookup"><span data-stu-id="b2369-271">Modify hello code behand file</span></span>
3. <span data-ttu-id="b2369-272">Компиляции и тестирования приложения hello</span><span class="sxs-lookup"><span data-stu-id="b2369-272">Compile and test hello application</span></span>

<span data-ttu-id="b2369-273">**toomodify hello XAML-файла**</span><span class="sxs-lookup"><span data-stu-id="b2369-273">**toomodify hello XAML file**</span></span>

1. <span data-ttu-id="b2369-274">В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Конструктор представлений**.</span><span class="sxs-lookup"><span data-stu-id="b2369-274">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="b2369-275">Найдите &lt;Grid.RowDefinitions&gt;и изменение hello RowDefinitions, поэтому они выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b2369-275">Locate &lt;Grid.RowDefinitions&gt;, and modify hello RowDefinitions so they looks like:</span></span>
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. <span data-ttu-id="b2369-276">Внутри hello &lt;сетки&gt;&lt;/Grid&gt; тегов, добавьте следующий hello кода toodefine элемент управления listbox, чтобы пользователи могли видеть список доступных потоков hello и выберите потоки:</span><span class="sxs-lookup"><span data-stu-id="b2369-276">Inside hello &lt;Grid&gt;&lt;/Grid&gt; tags, add hello following code toodefine a listbox control, so users can see hello list of available streams, and select streams:</span></span>

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
4. <span data-ttu-id="b2369-277">Нажмите клавишу **CTRL + S** toosave hello изменения.</span><span class="sxs-lookup"><span data-stu-id="b2369-277">Press **CTRL+S** toosave hello changes.</span></span>

<span data-ttu-id="b2369-278">**файл с выделенным кодом toomodify hello**</span><span class="sxs-lookup"><span data-stu-id="b2369-278">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="b2369-279">В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.</span><span class="sxs-lookup"><span data-stu-id="b2369-279">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="b2369-280">В пределах пространства имен SSPlayer hello добавьте новый класс:</span><span class="sxs-lookup"><span data-stu-id="b2369-280">Inside hello SSPlayer namespace, add a new class:</span></span>
   
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
3. <span data-ttu-id="b2369-281">В начале hello hello класса MainPage, добавьте hello после определения переменной:</span><span class="sxs-lookup"><span data-stu-id="b2369-281">At hello beginning of hello MainPage class, add hello following variable definitions:</span></span>
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. <span data-ttu-id="b2369-282">В пределах hello класса MainPage добавьте hello следующие области:</span><span class="sxs-lookup"><span data-stu-id="b2369-282">Inside hello MainPage class, add hello following region:</span></span>
   
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
5. <span data-ttu-id="b2369-283">Найдите метод mediaElement_ManifestReady hello, добавьте следующий код в конце hello функции hello hello:</span><span class="sxs-lookup"><span data-stu-id="b2369-283">Locate hello mediaElement_ManifestReady method, append hello following code at hello end of hello function:</span></span>
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    <span data-ttu-id="b2369-284">Поэтому при готовности манифест MediaElement кода hello Получает список доступных потоков hello и заполняет hello пользовательского интерфейса списка со списком hello.</span><span class="sxs-lookup"><span data-stu-id="b2369-284">So when MediaElement manifest is ready, hello code gets a list of hello available streams, and populates hello UI list box with hello list.</span></span>
6. <span data-ttu-id="b2369-285">Внутри hello класса MainPage, найдите кнопками ИП hello выберите регион события, а затем добавьте следующие определения функции hello:</span><span class="sxs-lookup"><span data-stu-id="b2369-285">Inside hello MainPage class, locate hello UI buttons click events region, and then add hello following function definition:</span></span>
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on hello presentation
            changeStreams(selectedStreams);
        }

<span data-ttu-id="b2369-286">**toocompile и тестирования приложения hello**</span><span class="sxs-lookup"><span data-stu-id="b2369-286">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="b2369-287">Нажмите клавишу **F6** toocompile hello проекта.</span><span class="sxs-lookup"><span data-stu-id="b2369-287">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="b2369-288">Нажмите клавишу **F5** toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b2369-288">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="b2369-289">Вверху hello приложения hello можно использовать значение по умолчанию hello Smooth Streaming URL-адрес или введите его.</span><span class="sxs-lookup"><span data-stu-id="b2369-289">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="b2369-290">Щелкните **Задать источник**.</span><span class="sxs-lookup"><span data-stu-id="b2369-290">Click **Set Source**.</span></span> 
5. <span data-ttu-id="b2369-291">язык по умолчанию Hello — audio_eng.</span><span class="sxs-lookup"><span data-stu-id="b2369-291">hello default language is audio_eng.</span></span> <span data-ttu-id="b2369-292">Попробуйте tooswitch между audio_eng и audio_es.</span><span class="sxs-lookup"><span data-stu-id="b2369-292">Try tooswitch between audio_eng and audio_es.</span></span> <span data-ttu-id="b2369-293">При каждом, выберите новый поток, необходимо нажать кнопку Submit hello.</span><span class="sxs-lookup"><span data-stu-id="b2369-293">Everytime, you select a new stream, you must click hello Submit button.</span></span>

<span data-ttu-id="b2369-294">Вы завершили урок 3.</span><span class="sxs-lookup"><span data-stu-id="b2369-294">You have completed lesson 3.</span></span>  <span data-ttu-id="b2369-295">На этом занятии добавьте потоки toochoose функции hello.</span><span class="sxs-lookup"><span data-stu-id="b2369-295">In this lesson, you add hello functionality toochoose streams.</span></span>

## <a name="lesson-4-select-smooth-streaming-tracks"></a><span data-ttu-id="b2369-296">Урок 4. Выбор дорожек для бесперебойной потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="b2369-296">Lesson 4: Select Smooth Streaming Tracks</span></span>
<span data-ttu-id="b2369-297">Представление бесперебойной потоковой передачи может содержать несколько видеофайлов, зашифрованных с разными уровнями качества (скоростью) и разрешениями.</span><span class="sxs-lookup"><span data-stu-id="b2369-297">A Smooth Streaming presentation can contain multiple video files encoded with different quality levels (bit rates) and resolutions.</span></span> <span data-ttu-id="b2369-298">На этом занятии вы включите отслеживает tooselect пользователей.</span><span class="sxs-lookup"><span data-stu-id="b2369-298">In this lesson, you will enable users tooselect tracks.</span></span> <span data-ttu-id="b2369-299">Это занятие содержит hello следующих процедур.</span><span class="sxs-lookup"><span data-stu-id="b2369-299">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="b2369-300">Измените файл XAML hello</span><span class="sxs-lookup"><span data-stu-id="b2369-300">Modify hello XAML file</span></span>
2. <span data-ttu-id="b2369-301">Измените файл behand кода hello</span><span class="sxs-lookup"><span data-stu-id="b2369-301">Modify hello code behand file</span></span>
3. <span data-ttu-id="b2369-302">Компиляции и тестирования приложения hello</span><span class="sxs-lookup"><span data-stu-id="b2369-302">Compile and test hello application</span></span>

<span data-ttu-id="b2369-303">**toomodify hello XAML-файла**</span><span class="sxs-lookup"><span data-stu-id="b2369-303">**toomodify hello XAML file**</span></span>

1. <span data-ttu-id="b2369-304">В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Конструктор представлений**.</span><span class="sxs-lookup"><span data-stu-id="b2369-304">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="b2369-305">Найдите hello &lt;сетки&gt; тег с именем hello **gridStreamAndBitrateSelection**, добавьте следующий код в конце hello тег hello hello:</span><span class="sxs-lookup"><span data-stu-id="b2369-305">Locate hello &lt;Grid&gt; tag with hello name **gridStreamAndBitrateSelection**, append hello following code at hello end of hello tag:</span></span>
   
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
3. <span data-ttu-id="b2369-306">Нажмите клавишу **CTRL + S** toosave, он изменяет</span><span class="sxs-lookup"><span data-stu-id="b2369-306">Press **CTRL+S** toosave he changes</span></span>

<span data-ttu-id="b2369-307">**файл с выделенным кодом toomodify hello**</span><span class="sxs-lookup"><span data-stu-id="b2369-307">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="b2369-308">В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.</span><span class="sxs-lookup"><span data-stu-id="b2369-308">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="b2369-309">В пределах пространства имен SSPlayer hello добавьте новый класс:</span><span class="sxs-lookup"><span data-stu-id="b2369-309">Inside hello SSPlayer namespace, add a new class:</span></span>
   
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
3. <span data-ttu-id="b2369-310">В начале hello hello класса MainPage, добавьте hello после определения переменной:</span><span class="sxs-lookup"><span data-stu-id="b2369-310">At hello beginning of hello MainPage class, add hello following variable definitions:</span></span>
   
        private List<Track> availableTracks;
4. <span data-ttu-id="b2369-311">В пределах hello класса MainPage добавьте hello следующие области:</span><span class="sxs-lookup"><span data-stu-id="b2369-311">Inside hello MainPage class, add hello following region:</span></span>
   
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
5. <span data-ttu-id="b2369-312">Найдите метод mediaElement_ManifestReady hello, добавьте следующий код в конце hello функции hello hello:</span><span class="sxs-lookup"><span data-stu-id="b2369-312">Locate hello mediaElement_ManifestReady method, append hello following code at hello end of hello function:</span></span>
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. <span data-ttu-id="b2369-313">Внутри hello класса MainPage, найдите кнопками ИП hello выберите регион события, а затем добавьте следующие определения функции hello:</span><span class="sxs-lookup"><span data-stu-id="b2369-313">Inside hello MainPage class, locate hello UI buttons click events region, and then add hello following function definition:</span></span>
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on hello presentation
            changeStreams(selectedStreams);
         }

<span data-ttu-id="b2369-314">**toocompile и тестирования приложения hello**</span><span class="sxs-lookup"><span data-stu-id="b2369-314">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="b2369-315">Нажмите клавишу **F6** toocompile hello проекта.</span><span class="sxs-lookup"><span data-stu-id="b2369-315">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="b2369-316">Нажмите клавишу **F5** toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b2369-316">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="b2369-317">Вверху hello приложения hello можно использовать значение по умолчанию hello Smooth Streaming URL-адрес или введите его.</span><span class="sxs-lookup"><span data-stu-id="b2369-317">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="b2369-318">Щелкните **Задать источник**.</span><span class="sxs-lookup"><span data-stu-id="b2369-318">Click **Set Source**.</span></span> 
5. <span data-ttu-id="b2369-319">По умолчанию выбираются все записи hello hello видеопотока.</span><span class="sxs-lookup"><span data-stu-id="b2369-319">By default, all of hello tracks of hello video stream are selected.</span></span> <span data-ttu-id="b2369-320">tooexperiment hello бит скорость изменения, можно выберите hello низкий битрейт доступны, а затем выберите hello наибольший скорость доступны.</span><span class="sxs-lookup"><span data-stu-id="b2369-320">tooexperiment hello bit rate changes, you can select hello lowest bit rate available, and then select hello highest bit rate available.</span></span> <span data-ttu-id="b2369-321">После каждого изменения необходимо нажать кнопку "Отправить".</span><span class="sxs-lookup"><span data-stu-id="b2369-321">You must click Submit after each change.</span></span>  <span data-ttu-id="b2369-322">Можно заметить изменения качества видео hello.</span><span class="sxs-lookup"><span data-stu-id="b2369-322">You can see hello video quality changes.</span></span>

<span data-ttu-id="b2369-323">Вы завершили урок 4.</span><span class="sxs-lookup"><span data-stu-id="b2369-323">You have completed lesson 4.</span></span>  <span data-ttu-id="b2369-324">На этом занятии добавьте отслеживает toochoose функции hello.</span><span class="sxs-lookup"><span data-stu-id="b2369-324">In this lesson, you add hello functionality toochoose tracks.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="b2369-325">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="b2369-325">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b2369-326">Отзывы</span><span class="sxs-lookup"><span data-stu-id="b2369-326">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a><span data-ttu-id="b2369-327">Другие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="b2369-327">Other Resources:</span></span>
* [<span data-ttu-id="b2369-328">Как toobuild приложении Smooth Streaming Windows 8 на языке JavaScript с помощью дополнительных возможностей</span><span class="sxs-lookup"><span data-stu-id="b2369-328">How toobuild a Smooth Streaming Windows 8 JavaScript application with advanced features</span></span>](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [<span data-ttu-id="b2369-329">Технический обзор Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="b2369-329">Smooth Streaming Technical Overview</span></span>](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

