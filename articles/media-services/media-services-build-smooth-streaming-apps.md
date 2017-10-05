---
title: "Руководство по приложениям Магазина Windows с потоковой передачей Smooth Streaming | Документация Майкрософт"
description: "Сведения об использовании служб мультимедиа Azure для создания приложения для магазина Windows на C# с управляющим элементом XML MediaElement для воспроизведения контента Smooth Stream"
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
ms.openlocfilehash: c9bb3b1915543fea3561cb309f55c4e8a74ded6d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-build-a-smooth-streaming-windows-store-application"></a><span data-ttu-id="29f32-103">Создание приложения для магазина Windows с бесперебойной потоковой передачей</span><span class="sxs-lookup"><span data-stu-id="29f32-103">How to Build a Smooth Streaming Windows Store Application</span></span>

<span data-ttu-id="29f32-104">Клиентский пакет SDK для бесперебойной потоковой передачи для Windows 8 позволяет разработчикам создавать приложения для магазина Windows, способные воспроизводить контент по требованию и в режиме реального времени с бесперебойной потоковой передачей.</span><span class="sxs-lookup"><span data-stu-id="29f32-104">The Smooth Streaming Client SDK for Windows 8 enables developers to build Windows Store applications that can play on-demand and live Smooth Streaming content.</span></span> <span data-ttu-id="29f32-105">Помимо основных функций воспроизведения контента с бесперебойной потоковой передачей этот пакет SDK также предоставляет богатые возможности, такие как защита Microsoft PlayReady, ограничение уровня качества, Live DVR, переключение потока аудио, прослушивание событий ошибок и обновления состояния (например, изменения уровня качества) и т. д.</span><span class="sxs-lookup"><span data-stu-id="29f32-105">In addition to the basic playback of Smooth Streaming content, the SDK also provides rich features like Microsoft PlayReady protection, quality level restriction, Live DVR, audio stream switching, listening for status updates (such as quality level changes) and error events, and so on.</span></span> <span data-ttu-id="29f32-106">Дополнительные сведения о поддерживаемых возможностях см. в [заметках к выпуску](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span><span class="sxs-lookup"><span data-stu-id="29f32-106">For more information of the supported features, see the [release notes](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span></span> <span data-ttu-id="29f32-107">Дополнительные сведения см. на странице, посвященной [Player Framework для Windows 8](http://playerframework.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="29f32-107">For more information, see [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span></span> 

<span data-ttu-id="29f32-108">Этот учебный курс состоит из четырех занятий:</span><span class="sxs-lookup"><span data-stu-id="29f32-108">This tutorial contains four lessons:</span></span>

1. <span data-ttu-id="29f32-109">Создание базового приложения магазина с бесперебойной потоковой передачей</span><span class="sxs-lookup"><span data-stu-id="29f32-109">Create a Basic Smooth Streaming Store Application</span></span>
2. <span data-ttu-id="29f32-110">Добавление ползунка для управления ходом воспроизведения мультимедиа</span><span class="sxs-lookup"><span data-stu-id="29f32-110">Add a Slider Bar to Control the Media Progress</span></span>
3. <span data-ttu-id="29f32-111">Выбор потоков для бесперебойной потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="29f32-111">Select Smooth Streaming Streams</span></span>
4. <span data-ttu-id="29f32-112">Выбор дорожек для бесперебойной потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="29f32-112">Select Smooth Streaming Tracks</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29f32-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="29f32-113">Prerequisites</span></span>
* <span data-ttu-id="29f32-114">Windows 8 (32-разрядная или 64-разрядная).</span><span class="sxs-lookup"><span data-stu-id="29f32-114">Windows 8 32-bit or 64-bit.</span></span> <span data-ttu-id="29f32-115">Можно получить [оценку Windows 8 Enterprise](http://msdn.microsoft.com/evalcenter/jj554510.aspx) из MSDN.</span><span class="sxs-lookup"><span data-stu-id="29f32-115">You can get [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) from MSDN.</span></span>
* <span data-ttu-id="29f32-116">Visual Studio 2012 или Visual Studio Express 2012 (либо более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="29f32-116">Visual Studio 2012 or Visual Studio Express 2012 (or a later version).</span></span> <span data-ttu-id="29f32-117">Пробную версию можно получить [здесь](http://www.microsoft.com/visualstudio/11/downloads).</span><span class="sxs-lookup"><span data-stu-id="29f32-117">You can get the trial version from [here](http://www.microsoft.com/visualstudio/11/downloads).</span></span>
* <span data-ttu-id="29f32-118">[Клиентский пакет SDK для бесперебойной потоковой передачи Microsoft для Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home)</span><span class="sxs-lookup"><span data-stu-id="29f32-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span></span>

<span data-ttu-id="29f32-119">Готовое решение для каждого урока можно загрузить из раздела образцов кода для разработчиков MSDN (коллекция кодов):</span><span class="sxs-lookup"><span data-stu-id="29f32-119">The completed solution for each lesson can be downloaded from MSDN Developer Code Samples (Code Gallery):</span></span> 

* <span data-ttu-id="29f32-120">[Урок 1.](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) Простой мультимедиапроигрыватель для Windows 8 с потоковой передачей Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="29f32-120">[Lesson 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - A Simple Windows 8 Smooth Streaming Media Player,</span></span> 
* <span data-ttu-id="29f32-121">[Урок 2.](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) Простой мультимедиапроигрыватель для Windows 8 с потоковой передачей Smooth Streaming и элементом управления «Ползунок».</span><span class="sxs-lookup"><span data-stu-id="29f32-121">[Lesson 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - A Simple Windows 8 Smooth Streaming Media Player with a Slider Bar Control,</span></span> 
* <span data-ttu-id="29f32-122">[Урок 3.](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) Простой мультимедиапроигрыватель для Windows 8 с потоковой передачей Smooth Streaming и выбором потока.</span><span class="sxs-lookup"><span data-stu-id="29f32-122">[Lesson 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - A Windows 8 Smooth Streaming Media Player with Stream Selection,</span></span>  
* <span data-ttu-id="29f32-123">[Урок 4.](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) Мультимедиапроигрыватель для Windows 8 с потоковой передачей Smooth Streaming и выбором дорожки.</span><span class="sxs-lookup"><span data-stu-id="29f32-123">[Lesson 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907)  - A Windows 8 Smooth Streaming Media Player with Track Selection.</span></span>

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a><span data-ttu-id="29f32-124">Урок 1. Создание базового приложения для магазина с бесперебойной потоковой передачей</span><span class="sxs-lookup"><span data-stu-id="29f32-124">Lesson 1: Create a Basic Smooth Streaming Store Application</span></span>

<span data-ttu-id="29f32-125">На этом занятии предстоит создать приложение для магазина Windows с элементом управления MediaElement для воспроизведения контента с бесперебойной потоковой передачей.</span><span class="sxs-lookup"><span data-stu-id="29f32-125">In this lesson, you will create a Windows Store application with a MediaElement control to play Smooth Stream content.</span></span>  <span data-ttu-id="29f32-126">Работающее приложение имеет следующий вид:</span><span class="sxs-lookup"><span data-stu-id="29f32-126">The running application looks like:</span></span>

![Пример приложения для магазина Windows с бесперебойной потоковой передачей][PlayerApplication]

<span data-ttu-id="29f32-128">Дополнительные сведения о разработке приложений Магазина Windows см. в разделе, посвященном [разработке потрясающих приложений для Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span><span class="sxs-lookup"><span data-stu-id="29f32-128">For more information on developing Windows Store application, see [Develop Great Apps for Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span></span> <span data-ttu-id="29f32-129">Это занятие содержит следующие процедуры:</span><span class="sxs-lookup"><span data-stu-id="29f32-129">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="29f32-130">Создание проекта для магазина Windows</span><span class="sxs-lookup"><span data-stu-id="29f32-130">Create a Windows Store project</span></span>
2. <span data-ttu-id="29f32-131">Проектирование пользовательского интерфейса (XAML)</span><span class="sxs-lookup"><span data-stu-id="29f32-131">Design the user interface (XAML)</span></span>
3. <span data-ttu-id="29f32-132">Изменение кода в файле</span><span class="sxs-lookup"><span data-stu-id="29f32-132">Modify the code behind file</span></span>
4. <span data-ttu-id="29f32-133">Компиляция и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="29f32-133">Compile and test the application</span></span>

<span data-ttu-id="29f32-134">**Создание проекта приложения Магазина Windows**</span><span class="sxs-lookup"><span data-stu-id="29f32-134">**To create a Windows Store project**</span></span>

1. <span data-ttu-id="29f32-135">Запустите Visual Studio 2012 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="29f32-135">Run Visual Studio 2012 or later.</span></span>
2. <span data-ttu-id="29f32-136">В меню **Файл** выберите команду **Создать**, а затем — **Проект**.</span><span class="sxs-lookup"><span data-stu-id="29f32-136">From the **FILE** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="29f32-137">В диалоговом окне "Новый проект" введите или выберите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="29f32-137">From the New Project dialog, type or select  the following values:</span></span>

| <span data-ttu-id="29f32-138">Имя</span><span class="sxs-lookup"><span data-stu-id="29f32-138">Name</span></span> | <span data-ttu-id="29f32-139">Значение</span><span class="sxs-lookup"><span data-stu-id="29f32-139">Value</span></span> |
| --- | --- |
| <span data-ttu-id="29f32-140">Группа шаблонов</span><span class="sxs-lookup"><span data-stu-id="29f32-140">Template group</span></span> |<span data-ttu-id="29f32-141">Installed/Templates/Visual C#/Windows Store</span><span class="sxs-lookup"><span data-stu-id="29f32-141">Installed/Templates/Visual C#/Windows Store</span></span> |
| <span data-ttu-id="29f32-142">Шаблон</span><span class="sxs-lookup"><span data-stu-id="29f32-142">Template</span></span> |<span data-ttu-id="29f32-143">Пустое приложение (XAML)</span><span class="sxs-lookup"><span data-stu-id="29f32-143">Blank App (XAML)</span></span> |
| <span data-ttu-id="29f32-144">Имя</span><span class="sxs-lookup"><span data-stu-id="29f32-144">Name</span></span> |<span data-ttu-id="29f32-145">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="29f32-145">SSPlayer</span></span> |
| <span data-ttu-id="29f32-146">Расположение</span><span class="sxs-lookup"><span data-stu-id="29f32-146">Location</span></span> |<span data-ttu-id="29f32-147">C:\SSTutorials</span><span class="sxs-lookup"><span data-stu-id="29f32-147">C:\SSTutorials</span></span> |
| <span data-ttu-id="29f32-148">Имя решения</span><span class="sxs-lookup"><span data-stu-id="29f32-148">Solution Name</span></span> |<span data-ttu-id="29f32-149">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="29f32-149">SSPlayer</span></span> |
| <span data-ttu-id="29f32-150">Создать каталог для решения</span><span class="sxs-lookup"><span data-stu-id="29f32-150">Create directory for solution</span></span> |<span data-ttu-id="29f32-151">(выбрано)</span><span class="sxs-lookup"><span data-stu-id="29f32-151">(selected)</span></span> |

1. <span data-ttu-id="29f32-152">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="29f32-152">Click **OK**.</span></span>

<span data-ttu-id="29f32-153">**Добавление ссылки на пакет SDK клиента Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="29f32-153">**To add a reference to the Smooth Streaming Client SDK**</span></span>

1. <span data-ttu-id="29f32-154">В обозревателе решений щелкните правой кнопкой мыши **SSPlayer**, а затем выберите команду **Добавить ссылку**.</span><span class="sxs-lookup"><span data-stu-id="29f32-154">From Solution Explorer, right-click **SSPlayer**, and then click **Add Reference**.</span></span>
2. <span data-ttu-id="29f32-155">Введите или выберите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="29f32-155">Type or select the following values:</span></span>

| <span data-ttu-id="29f32-156">Имя</span><span class="sxs-lookup"><span data-stu-id="29f32-156">Name</span></span> | <span data-ttu-id="29f32-157">Значение</span><span class="sxs-lookup"><span data-stu-id="29f32-157">Value</span></span> |
| --- | --- |
| <span data-ttu-id="29f32-158">Ссылочная группа</span><span class="sxs-lookup"><span data-stu-id="29f32-158">Reference group</span></span> |<span data-ttu-id="29f32-159">Windows/Расширения</span><span class="sxs-lookup"><span data-stu-id="29f32-159">Windows/Extensions</span></span> |
| <span data-ttu-id="29f32-160">Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="29f32-160">Reference</span></span> |<span data-ttu-id="29f32-161">Выберите клиентский пакет SDK бесперебойной потоковой передачи Microsoft для Windows 8 и пакет среды выполнения Microsoft Visual C++</span><span class="sxs-lookup"><span data-stu-id="29f32-161">Select Microsoft Smooth Streaming Client SDK for Windows 8 and Microsoft Visual C++ Runtime Package</span></span> |

1. <span data-ttu-id="29f32-162">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="29f32-162">Click **OK**.</span></span> 

<span data-ttu-id="29f32-163">После добавления ссылок необходимо выбрать целевую платформу (x64 x86), добавление ссылок будет действовать не для всех конфигураций платформы ЦП.</span><span class="sxs-lookup"><span data-stu-id="29f32-163">After adding the references, you must select the targeted platform (x64 or x86), adding references will not work for Any CPU platform configuration.</span></span>  <span data-ttu-id="29f32-164">Для таких добавленных ссылок в обозревателе решений будет выведен желтый значок предупреждения.</span><span class="sxs-lookup"><span data-stu-id="29f32-164">In solution explorer, you will see yellow warning mark for these added references.</span></span>

<span data-ttu-id="29f32-165">**Создание пользовательского интерфейса проигрывателя**</span><span class="sxs-lookup"><span data-stu-id="29f32-165">**To design the player user interface**</span></span>

1. <span data-ttu-id="29f32-166">В обозревателе решений дважды щелкните **MainPage.xaml** , чтобы открыть его в режиме конструктора.</span><span class="sxs-lookup"><span data-stu-id="29f32-166">From Solution Explorer, double click **MainPage.xaml** to open it in the design view.</span></span>
2. <span data-ttu-id="29f32-167">Найдите теги **&lt;Grid&gt;** и **&lt;/Grid&gt;** в XAML-файле и вставьте между ними код ниже:</span><span class="sxs-lookup"><span data-stu-id="29f32-167">Locate the **&lt;Grid&gt;** and **&lt;/Grid&gt;**  tags the XAML file, and paste the following code between the two tags:</span></span>

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
   
   <span data-ttu-id="29f32-168">Элемент управления MediaElement используется для воспроизведения мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="29f32-168">The MediaElement control is used to playback media.</span></span> <span data-ttu-id="29f32-169">Для управления мультимедиа в следующем уроке будет использоваться ползунок с именем sliderProgress.</span><span class="sxs-lookup"><span data-stu-id="29f32-169">The slider control named sliderProgress will be used in the next lesson to control the media progress.</span></span>
3. <span data-ttu-id="29f32-170">Нажмите клавиши **CTRL+S** , чтобы сохранить файл.</span><span class="sxs-lookup"><span data-stu-id="29f32-170">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="29f32-171">Элемент управления MediaElement поддерживает бесперебойную потоковую передачу контента без дополнительной настройки.</span><span class="sxs-lookup"><span data-stu-id="29f32-171">The MediaElement control does not support Smooth Streaming content out-of-box.</span></span> <span data-ttu-id="29f32-172">Чтобы включить поддержку бесперебойной потоковой передачи, необходимо зарегистрировать обработчик потока байтов для бесперебойной потоковой передачи по расширению файла и MIME-типу.</span><span class="sxs-lookup"><span data-stu-id="29f32-172">To enable the Smooth Streaming support, you must register the Smooth Streaming byte-stream handler by file name extension and MIME type.</span></span>  <span data-ttu-id="29f32-173">Для регистрации используется метод MediaExtensionManager.RegisterByteStremHandler в пространстве имен Windows.Media.</span><span class="sxs-lookup"><span data-stu-id="29f32-173">To register, you use the MediaExtensionManager.RegisterByteStremHandler method of the Windows.Media namespace.</span></span>

<span data-ttu-id="29f32-174">В этом XAML-файле некоторые обработчики событий связаны с элементами управления.</span><span class="sxs-lookup"><span data-stu-id="29f32-174">In this XAML file, some event handlers are associated with the controls.</span></span>  <span data-ttu-id="29f32-175">Такие обработчики событий необходимо определить.</span><span class="sxs-lookup"><span data-stu-id="29f32-175">You must define those event handlers.</span></span>

<span data-ttu-id="29f32-176">**Изменение файла кода программной части**</span><span class="sxs-lookup"><span data-stu-id="29f32-176">**To modify the code behind file**</span></span>

1. <span data-ttu-id="29f32-177">В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.</span><span class="sxs-lookup"><span data-stu-id="29f32-177">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="29f32-178">Добавьте следующую инструкцию using в начало файла:</span><span class="sxs-lookup"><span data-stu-id="29f32-178">At the top of the file, add the following using statement:</span></span>
   
        using Windows.Media;
3. <span data-ttu-id="29f32-179">В начале класса **MainPage** добавьте следующие члены данных:</span><span class="sxs-lookup"><span data-stu-id="29f32-179">At the beginning of the **MainPage** class, add the following data member:</span></span>
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. <span data-ttu-id="29f32-180">В конце конструктора **MainPage** добавьте следующие две строки:</span><span class="sxs-lookup"><span data-stu-id="29f32-180">At the end of the **MainPage** constructor, add the following two lines:</span></span>
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. <span data-ttu-id="29f32-181">Добавьте в конце класса **MainPage** следующий код:</span><span class="sxs-lookup"><span data-stu-id="29f32-181">At the end of the **MainPage** class, paste the following code:</span></span>
   
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
             txtStatus.Text = "Click the Play button to play the media source.";
         }
         }
         private void btnStop_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Stop();
         txtStatus.Text = "MediaElement is stopped";
         }
         private void sliderProgress_PointerPressed(object sender, PointerRoutedEventArgs e)
         {

         txtStatus.Text = "Seek to position " + sliderProgress.Value;
         mediaElement.Position = new TimeSpan(0, 0, (int)(sliderProgress.Value));
         }
         # endregion

<span data-ttu-id="29f32-182">Здесь определяется обработчик события sliderProgress_PointerPressed.</span><span class="sxs-lookup"><span data-stu-id="29f32-182">The sliderProgress_PointerPressed event handler is defined here.</span></span>  <span data-ttu-id="29f32-183">Для его запуска требуется выполнить ряд дополнительных действий, которые будут рассматриваться на следующем уроке этого учебного курса.</span><span class="sxs-lookup"><span data-stu-id="29f32-183">There are more works to do to get it working, which will be covered in the next lesson of this tutorial.</span></span>
6. <span data-ttu-id="29f32-184">Нажмите клавиши **CTRL+S** , чтобы сохранить файл.</span><span class="sxs-lookup"><span data-stu-id="29f32-184">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="29f32-185">Готовый код файла должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="29f32-185">The finished the code behind file shall look like this:</span></span>

![Просмотр кода в Visual Studio для приложения для магазина Windows с бесперебойной потоковой передачей][CodeViewPic]

<span data-ttu-id="29f32-187">**Компиляция и тестирование приложения**</span><span class="sxs-lookup"><span data-stu-id="29f32-187">**To compile and test the application**</span></span>

1. <span data-ttu-id="29f32-188">В меню **СБОРКА** выберите **Диспетчер конфигураций**.</span><span class="sxs-lookup"><span data-stu-id="29f32-188">From the **BUILD** menu, click **Configuration Manager**.</span></span>
2. <span data-ttu-id="29f32-189">Измените параметр **Платформа активного решения** в соответствии с вашей платформой разработки.</span><span class="sxs-lookup"><span data-stu-id="29f32-189">Change **Active solution platform** to match your development platform.</span></span>
3. <span data-ttu-id="29f32-190">Нажмите клавишу **F6** для компиляции проекта.</span><span class="sxs-lookup"><span data-stu-id="29f32-190">Press **F6** to compile the project.</span></span> 
4. <span data-ttu-id="29f32-191">Нажмите клавишу **F5** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="29f32-191">Press **F5** to run the application.</span></span>
5. <span data-ttu-id="29f32-192">В верхней части приложения можно выбрать URL-адрес бесперебойной потоковой передачи по умолчанию или ввести другой.</span><span class="sxs-lookup"><span data-stu-id="29f32-192">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
6. <span data-ttu-id="29f32-193">Щелкните **Задать источник**.</span><span class="sxs-lookup"><span data-stu-id="29f32-193">Click **Set Source**.</span></span> <span data-ttu-id="29f32-194">Так как по умолчанию включен параметр **Автовоспроизведение** , мультимедиа должно воспроизводиться автоматически.</span><span class="sxs-lookup"><span data-stu-id="29f32-194">Because **Auto Play** is enabled by default, the media shall play automatically.</span></span>  <span data-ttu-id="29f32-195">Управление мультимедиа ведется с помощью кнопок **Воспроизвести**, **Пауза** и **Остановить**.</span><span class="sxs-lookup"><span data-stu-id="29f32-195">You can control the media using the **Play**, **Pause** and **Stop** buttons.</span></span>  <span data-ttu-id="29f32-196">Громкость звука выбирается вертикальным ползунком.</span><span class="sxs-lookup"><span data-stu-id="29f32-196">You can control the media volume using the vertical slider.</span></span>  <span data-ttu-id="29f32-197">Однако горизонтальный ползунок для управления воспроизведением мультимедиа пока не реализован полностью.</span><span class="sxs-lookup"><span data-stu-id="29f32-197">However the horizontal slider for controlling the media progress is not fully implemented yet.</span></span> 

<span data-ttu-id="29f32-198">Вы завершили урок 1.</span><span class="sxs-lookup"><span data-stu-id="29f32-198">You have completed lesson1.</span></span>  <span data-ttu-id="29f32-199">В этом уроке с помощью элемента управления MediaElement воспроизводится контент с бесперебойной потоковой передачей.</span><span class="sxs-lookup"><span data-stu-id="29f32-199">In this lesson, you use a MediaElement control to playback Smooth Streaming content.</span></span>  <span data-ttu-id="29f32-200">На следующем занятии будет добавлен ползунок, который позволит управлять воспроизведением такого контента.</span><span class="sxs-lookup"><span data-stu-id="29f32-200">In the next lesson, you will add a slider to control the progress of the Smooth Streaming content.</span></span>

## <a name="lesson-2-add-a-slider-bar-to-control-the-media-progress"></a><span data-ttu-id="29f32-201">Урок 2. Добавление ползунка для управления ходом воспроизведения мультимедиа</span><span class="sxs-lookup"><span data-stu-id="29f32-201">Lesson 2: Add a Slider Bar to Control the Media Progress</span></span>

<span data-ttu-id="29f32-202">На занятии 1 было создано приложение для магазина Windows с элементом управления XAML MediaElement для воспроизведения контента мультимедиа с бесперебойной потоковой передачей.</span><span class="sxs-lookup"><span data-stu-id="29f32-202">In lesson 1, you created a Windows Store application with a MediaElement XAML control to playback Smooth Streaming media content.</span></span>  <span data-ttu-id="29f32-203">Этот элемент изначально имеет такие функции, как начало, останов и приостановка воспроизведения.</span><span class="sxs-lookup"><span data-stu-id="29f32-203">It comes some basic media functions like start, stop and pause.</span></span>  <span data-ttu-id="29f32-204">На этом занятии в приложение будет добавлен еще один элемент управления — ползунок.</span><span class="sxs-lookup"><span data-stu-id="29f32-204">In this lesson, you will add a slider bar control to the application.</span></span>

<span data-ttu-id="29f32-205">В этом учебном курсе для обновления положения ползунка на основе текущего положения элемента управления MediaElement будет использоваться таймер.</span><span class="sxs-lookup"><span data-stu-id="29f32-205">In this tutorial, we will use a timer to update the slider position based on the current position of the MediaElement control.</span></span>  <span data-ttu-id="29f32-206">При воспроизведении контента в режиме реального времени также требуется обновлять время начала и окончания ползунка.</span><span class="sxs-lookup"><span data-stu-id="29f32-206">The slider start and end time also need to be updated in case of live content.</span></span>  <span data-ttu-id="29f32-207">Для обработки лучше использовать событие обновления адаптивного источника.</span><span class="sxs-lookup"><span data-stu-id="29f32-207">This can be better handled in the adaptive source update event.</span></span>

<span data-ttu-id="29f32-208">Источники мультимедиа — это объекты, которые создают данные мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="29f32-208">Media sources are objects that generate media data.</span></span>  <span data-ttu-id="29f32-209">Средство выбора источника принимает URL-адрес или поток байтов и создает соответствующий источник мультимедиа для этого контента.</span><span class="sxs-lookup"><span data-stu-id="29f32-209">The source resolver takes a URL or byte stream and creates the appropriate media source for that content.</span></span>  <span data-ttu-id="29f32-210">Средство выбора источника является стандартным способом для создания источников мультимедиа в приложениях.</span><span class="sxs-lookup"><span data-stu-id="29f32-210">The source resolver is the standard way for the applications to create media sources.</span></span> 

<span data-ttu-id="29f32-211">Это занятие содержит следующие процедуры:</span><span class="sxs-lookup"><span data-stu-id="29f32-211">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="29f32-212">Регистрация обработчика бесперебойной потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="29f32-212">Register the Smooth Streaming handler</span></span> 
2. <span data-ttu-id="29f32-213">Добавление обработчиков событий уровня диспетчера адаптивных источников.</span><span class="sxs-lookup"><span data-stu-id="29f32-213">Add the adaptive source manager level event handlers</span></span>
3. <span data-ttu-id="29f32-214">Добавление обработчиков событий уровня адаптивного источника.</span><span class="sxs-lookup"><span data-stu-id="29f32-214">Add the adaptive source level event handlers</span></span>
4. <span data-ttu-id="29f32-215">Добавление обработчиков событий MediaElement</span><span class="sxs-lookup"><span data-stu-id="29f32-215">Add MediaElement event handlers</span></span>
5. <span data-ttu-id="29f32-216">Добавление кода, связанного с ползунком</span><span class="sxs-lookup"><span data-stu-id="29f32-216">Add slider bar related code</span></span>
6. <span data-ttu-id="29f32-217">Компиляция и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="29f32-217">Compile and test the application</span></span>

<span data-ttu-id="29f32-218">**Регистрация обработчика байтового потока Smooth Streaming и передача набора свойств propertyset**</span><span class="sxs-lookup"><span data-stu-id="29f32-218">**To register the Smooth Streaming byte-stream handler and pass the propertyset**</span></span>

1. <span data-ttu-id="29f32-219">В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.</span><span class="sxs-lookup"><span data-stu-id="29f32-219">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="29f32-220">Добавьте следующую инструкцию using в начало файла:</span><span class="sxs-lookup"><span data-stu-id="29f32-220">At the beginning of the file, add the following using statement:</span></span>

        using Microsoft.Media.AdaptiveStreaming;
3. <span data-ttu-id="29f32-221">В начале класса MainPage добавьте следующие члены данных:</span><span class="sxs-lookup"><span data-stu-id="29f32-221">At the beginning of the MainPage class, add the following data members:</span></span>

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. <span data-ttu-id="29f32-222">В конструкторе **MainPage** добавьте следующий код после строки **this.Initialize Components();** и строк кода регистрации, добавленных на предыдущем занятии:</span><span class="sxs-lookup"><span data-stu-id="29f32-222">Inside the **MainPage** constructor, add the following code after the **this.Initialize Components();** line and the registration code lines written in the previous lesson:</span></span>

        // Gets the default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value to AdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. <span data-ttu-id="29f32-223">В конструкторе **MainPage** измените два метода RegisterByteStreamHandler для добавления следующих параметров:</span><span class="sxs-lookup"><span data-stu-id="29f32-223">Inside the **MainPage** constructor, modify the two RegisterByteStreamHandler methods to add the forth parameters:</span></span>

         // Registers Smooth Streaming byte-stream handler for ".ism" extension and, 
         // "text/xml" and "application/vnd.ms-ss" mime-types and pass the propertyset. 
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
6. <span data-ttu-id="29f32-224">Нажмите клавиши **CTRL+S** , чтобы сохранить файл.</span><span class="sxs-lookup"><span data-stu-id="29f32-224">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="29f32-225">**Добавление обработчиков событий уровня диспетчера адаптивных источников**</span><span class="sxs-lookup"><span data-stu-id="29f32-225">**To add the adaptive source manager level event handler**</span></span>

1. <span data-ttu-id="29f32-226">В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.</span><span class="sxs-lookup"><span data-stu-id="29f32-226">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="29f32-227">В классе **MainPage** добавьте следующий член данных:</span><span class="sxs-lookup"><span data-stu-id="29f32-227">Inside the **MainPage** class, add the following data member:</span></span>
   
     <span data-ttu-id="29f32-228">private AdaptiveSource adaptiveSource = null;</span><span class="sxs-lookup"><span data-stu-id="29f32-228">private AdaptiveSource adaptiveSource = null;</span></span>
3. <span data-ttu-id="29f32-229">В конце класса **MainPage** добавьте следующий обработчик событий:</span><span class="sxs-lookup"><span data-stu-id="29f32-229">At the end of the **MainPage** class, add the following event handler:</span></span>
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. <span data-ttu-id="29f32-230">В конце конструктора **MainPage** добавьте следующую строку для подписки на событие открытия адаптивного источника:</span><span class="sxs-lookup"><span data-stu-id="29f32-230">At the end of the **MainPage** constructor, add the following line to subscribe to the adaptive source open event:</span></span>
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. <span data-ttu-id="29f32-231">Нажмите клавиши **CTRL+S** , чтобы сохранить файл.</span><span class="sxs-lookup"><span data-stu-id="29f32-231">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="29f32-232">**Добавление обработчиков событий уровня адаптивного источника**</span><span class="sxs-lookup"><span data-stu-id="29f32-232">**To add adaptive source level event handlers**</span></span>

1. <span data-ttu-id="29f32-233">В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.</span><span class="sxs-lookup"><span data-stu-id="29f32-233">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="29f32-234">В классе **MainPage** добавьте следующий член данных:</span><span class="sxs-lookup"><span data-stu-id="29f32-234">Inside the **MainPage** class, add the following data member:</span></span>
   
     <span data-ttu-id="29f32-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span><span class="sxs-lookup"><span data-stu-id="29f32-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span></span>
3. <span data-ttu-id="29f32-236">В конце класса **MainPage** добавьте следующие обработчики событий:</span><span class="sxs-lookup"><span data-stu-id="29f32-236">At the end of the **MainPage** class, add the following event handlers:</span></span>

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
4. <span data-ttu-id="29f32-237">В конце метода **mediaElement AdaptiveSourceOpened** добавьте следующий код, чтобы подписаться на события:</span><span class="sxs-lookup"><span data-stu-id="29f32-237">At the end of the **mediaElement AdaptiveSourceOpened** method, add the following code to subscribe to the events:</span></span>
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. <span data-ttu-id="29f32-238">Нажмите клавиши **CTRL+S** , чтобы сохранить файл.</span><span class="sxs-lookup"><span data-stu-id="29f32-238">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="29f32-239">Эти же события доступны на уровне диспетчера адаптивных источников, который может использоваться для обработки функций, общих для всех элементов мультимедиа в приложении.</span><span class="sxs-lookup"><span data-stu-id="29f32-239">The same events are available on Adaptive Source manger level as well, which can be used for handling functionality common to all media elements in the app.</span></span> <span data-ttu-id="29f32-240">Каждый адаптивный источник имеет свои собственные события, и все события AdaptiveSource будут передаваться каскадом в диспетчер AdaptiveSourceManager.</span><span class="sxs-lookup"><span data-stu-id="29f32-240">Each AdaptiveSource includes its own events and all AdaptiveSource events will be cascaded under AdaptiveSourceManager.</span></span>

<span data-ttu-id="29f32-241">**Добавление обработчиков событий MediaElement**</span><span class="sxs-lookup"><span data-stu-id="29f32-241">**To add Media Element event handlers**</span></span>

1. <span data-ttu-id="29f32-242">В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.</span><span class="sxs-lookup"><span data-stu-id="29f32-242">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="29f32-243">В конце класса **MainPage** добавьте следующие обработчики событий:</span><span class="sxs-lookup"><span data-stu-id="29f32-243">At the end of the **MainPage** class, add the following event handlers:</span></span>

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
3. <span data-ttu-id="29f32-244">В конце конструктора **MainPage** добавьте следующий код для подписки на события:</span><span class="sxs-lookup"><span data-stu-id="29f32-244">At the end of the **MainPage** constructor, add the following code to subscript to the events:</span></span>

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. <span data-ttu-id="29f32-245">Нажмите клавиши **CTRL+S** , чтобы сохранить файл.</span><span class="sxs-lookup"><span data-stu-id="29f32-245">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="29f32-246">**Добавление кода, связанного с ползунком**</span><span class="sxs-lookup"><span data-stu-id="29f32-246">**To add slider bar related code**</span></span>

1. <span data-ttu-id="29f32-247">В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.</span><span class="sxs-lookup"><span data-stu-id="29f32-247">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="29f32-248">Добавьте следующую инструкцию using в начало файла:</span><span class="sxs-lookup"><span data-stu-id="29f32-248">At the beginning of the file, add the following using statement:</span></span>
      
        using Windows.UI.Core;
3. <span data-ttu-id="29f32-249">В классе **MainPage** добавьте следующий член данных:</span><span class="sxs-lookup"><span data-stu-id="29f32-249">Inside the **MainPage** class, add the following data members:</span></span>
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. <span data-ttu-id="29f32-250">В конце конструктора **MainPage** добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="29f32-250">At the end of the **MainPage** constructor, add the following code:</span></span>
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. <span data-ttu-id="29f32-251">Добавьте в конце класса **MainPage** следующий код:</span><span class="sxs-lookup"><span data-stu-id="29f32-251">At the end of the **MainPage** class, add the following code:</span></span>

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
><span data-ttu-id="29f32-252">CoreDispatcher используется для внесения изменений в поток пользовательского интерфейса из других потоков.</span><span class="sxs-lookup"><span data-stu-id="29f32-252">CoreDispatcher is used to make changes to the UI thread from non UI Thread.</span></span> <span data-ttu-id="29f32-253">В случае возникновения узких мест в потоке-отправителе разработчик может использовать отправитель, предоставленный элементом пользовательского интерфейса, который планируется обновить.</span><span class="sxs-lookup"><span data-stu-id="29f32-253">In case of bottleneck on dispatcher thread, developer can choose to use dispatcher provided by UI-element he/she intends to update.</span></span>  <span data-ttu-id="29f32-254">Например:</span><span class="sxs-lookup"><span data-stu-id="29f32-254">For example:</span></span>
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. <span data-ttu-id="29f32-255">В конце метода **mediaElement_AdaptiveSourceStatusUpdated** добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="29f32-255">At the end of the **mediaElement_AdaptiveSourceStatusUpdated** method, add the following code:</span></span>

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. <span data-ttu-id="29f32-256">В конце метода **MediaOpened** добавьте следующий код:</span><span class="sxs-lookup"><span data-stu-id="29f32-256">At the end of the **MediaOpened** method, add the following code:</span></span>

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. <span data-ttu-id="29f32-257">Нажмите клавиши **CTRL+S** , чтобы сохранить файл.</span><span class="sxs-lookup"><span data-stu-id="29f32-257">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="29f32-258">**Компиляция и тестирование приложения**</span><span class="sxs-lookup"><span data-stu-id="29f32-258">**To compile and test the application**</span></span>

1. <span data-ttu-id="29f32-259">Нажмите клавишу **F6** для компиляции проекта.</span><span class="sxs-lookup"><span data-stu-id="29f32-259">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="29f32-260">Нажмите клавишу **F5** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="29f32-260">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="29f32-261">В верхней части приложения можно выбрать URL-адрес бесперебойной потоковой передачи по умолчанию или ввести другой.</span><span class="sxs-lookup"><span data-stu-id="29f32-261">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="29f32-262">Щелкните **Задать источник**.</span><span class="sxs-lookup"><span data-stu-id="29f32-262">Click **Set Source**.</span></span> 
5. <span data-ttu-id="29f32-263">Протестируйте работу ползунка.</span><span class="sxs-lookup"><span data-stu-id="29f32-263">Test the slider bar.</span></span>

<span data-ttu-id="29f32-264">Вы завершили урок 2.</span><span class="sxs-lookup"><span data-stu-id="29f32-264">You have completed lesson 2.</span></span>  <span data-ttu-id="29f32-265">В этом уроке в приложение был добавлен ползунок.</span><span class="sxs-lookup"><span data-stu-id="29f32-265">In this lesson you added a slider to application.</span></span> 

## <a name="lesson-3-select-smooth-streaming-streams"></a><span data-ttu-id="29f32-266">Урок 3. Выбор потоков для бесперебойной потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="29f32-266">Lesson 3: Select Smooth Streaming Streams</span></span>
<span data-ttu-id="29f32-267">Бесперебойная потоковая передача способна передавать контент с аудиодорожками на нескольких языках, которые могут быть выбраны просматривающими.</span><span class="sxs-lookup"><span data-stu-id="29f32-267">Smooth Streaming is capable to stream content with multiple language audio tracks that are selectable by the viewers.</span></span>  <span data-ttu-id="29f32-268">На этом занятии предстоит включить средства просмотра для выбора потоков.</span><span class="sxs-lookup"><span data-stu-id="29f32-268">In this lesson, you will enable viewers to select streams.</span></span> <span data-ttu-id="29f32-269">Это занятие содержит следующие процедуры:</span><span class="sxs-lookup"><span data-stu-id="29f32-269">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="29f32-270">Изменение XAML-файла</span><span class="sxs-lookup"><span data-stu-id="29f32-270">Modify the XAML file</span></span>
2. <span data-ttu-id="29f32-271">Изменение кода файла behand</span><span class="sxs-lookup"><span data-stu-id="29f32-271">Modify the code behand file</span></span>
3. <span data-ttu-id="29f32-272">Компиляция и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="29f32-272">Compile and test the application</span></span>

<span data-ttu-id="29f32-273">**Изменение XAML-файла**</span><span class="sxs-lookup"><span data-stu-id="29f32-273">**To modify the XAML file**</span></span>

1. <span data-ttu-id="29f32-274">В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Конструктор представлений**.</span><span class="sxs-lookup"><span data-stu-id="29f32-274">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="29f32-275">Найдите &lt;Grid.RowDefinitions&gt; и измените RowDefinitions следующим образом:</span><span class="sxs-lookup"><span data-stu-id="29f32-275">Locate &lt;Grid.RowDefinitions&gt;, and modify the RowDefinitions so they looks like:</span></span>
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. <span data-ttu-id="29f32-276">Внутри тегов &lt;Grid&gt;&lt;/Grid&gt; добавьте следующий код, чтобы определить элемент управления типа "поле со списком", который позволит пользователям просматривать список доступных потоков и выбирать нужные:</span><span class="sxs-lookup"><span data-stu-id="29f32-276">Inside the &lt;Grid&gt;&lt;/Grid&gt; tags, add the following code to define a listbox control, so users can see the list of available streams, and select streams:</span></span>

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
4. <span data-ttu-id="29f32-277">Нажмите клавишу **CTRL+S** , чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="29f32-277">Press **CTRL+S** to save the changes.</span></span>

<span data-ttu-id="29f32-278">**Изменение файла кода программной части**</span><span class="sxs-lookup"><span data-stu-id="29f32-278">**To modify the code behind file**</span></span>

1. <span data-ttu-id="29f32-279">В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.</span><span class="sxs-lookup"><span data-stu-id="29f32-279">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="29f32-280">В пространстве имен SSPlayer добавьте следующий новый класс:</span><span class="sxs-lookup"><span data-stu-id="29f32-280">Inside the SSPlayer namespace, add a new class:</span></span>
   
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
                    // mMke the video stream always checked.
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
3. <span data-ttu-id="29f32-281">В начале класса MainPage добавьте следующие определения переменных:</span><span class="sxs-lookup"><span data-stu-id="29f32-281">At the beginning of the MainPage class, add the following variable definitions:</span></span>
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. <span data-ttu-id="29f32-282">Добавьте в класс MainPage следующую область:</span><span class="sxs-lookup"><span data-stu-id="29f32-282">Inside the MainPage class, add the following region:</span></span>
   
        #region stream selection
        ///<summary>
        ///Functionality to select streams from IManifestStream available streams
        /// </summary>
   
        // This function is called from the mediaElement_ManifestReady event handler 
        // to retrieve the streams and populate them to the local data members.
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
   
                    //populate the stream lists based on the types
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
   
                    // Select the default selected streams from the manifest.
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
   
        // This function set the list box ItemSource
        private async void refreshAvailableStreamsListBoxItemSource()
        {
            try
            {
                //update the stream check box list on the UI
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
   
            // Select the frist video stream from the list if no video stream is selected
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
                    txtStatus.Text = "The audio stream is changed to " + availableAudioStreams[j].ManifestStream.Name;
                }
            }
   
            // Select the frist audio stream from the list if no audio steam is selected.
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
5. <span data-ttu-id="29f32-283">Найдите метод mediaElement_ManifestReady, измените следующий код в конце функции:</span><span class="sxs-lookup"><span data-stu-id="29f32-283">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span></span>
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    <span data-ttu-id="29f32-284">Таким образом, если манифест MediaElement готов, код получает список доступных потоков и заполняет поле со списком пользовательского интерфейса этими значениями.</span><span class="sxs-lookup"><span data-stu-id="29f32-284">So when MediaElement manifest is ready, the code gets a list of the available streams, and populates the UI list box with the list.</span></span>
6. <span data-ttu-id="29f32-285">В классе MainPage найдите область событий щелчка кнопок пользовательского интерфейса и добавьте следующее определение функции:</span><span class="sxs-lookup"><span data-stu-id="29f32-285">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span></span>
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of the selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on the presentation
            changeStreams(selectedStreams);
        }

<span data-ttu-id="29f32-286">**Компиляция и тестирование приложения**</span><span class="sxs-lookup"><span data-stu-id="29f32-286">**To compile and test the application**</span></span>

1. <span data-ttu-id="29f32-287">Нажмите клавишу **F6** для компиляции проекта.</span><span class="sxs-lookup"><span data-stu-id="29f32-287">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="29f32-288">Нажмите клавишу **F5** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="29f32-288">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="29f32-289">В верхней части приложения можно выбрать URL-адрес бесперебойной потоковой передачи по умолчанию или ввести другой.</span><span class="sxs-lookup"><span data-stu-id="29f32-289">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="29f32-290">Щелкните **Задать источник**.</span><span class="sxs-lookup"><span data-stu-id="29f32-290">Click **Set Source**.</span></span> 
5. <span data-ttu-id="29f32-291">Язык по умолчанию — audio_eng.</span><span class="sxs-lookup"><span data-stu-id="29f32-291">The default language is audio_eng.</span></span> <span data-ttu-id="29f32-292">Попробуйте переключиться между audio_eng и audio_es.</span><span class="sxs-lookup"><span data-stu-id="29f32-292">Try to switch between audio_eng and audio_es.</span></span> <span data-ttu-id="29f32-293">Каждый раз при выборе нового потока необходимо нажать кнопку "Отправить".</span><span class="sxs-lookup"><span data-stu-id="29f32-293">Everytime, you select a new stream, you must click the Submit button.</span></span>

<span data-ttu-id="29f32-294">Вы завершили урок 3.</span><span class="sxs-lookup"><span data-stu-id="29f32-294">You have completed lesson 3.</span></span>  <span data-ttu-id="29f32-295">В этом уроке были добавлены функциональные возможности для выбора потоков.</span><span class="sxs-lookup"><span data-stu-id="29f32-295">In this lesson, you add the functionality to choose streams.</span></span>

## <a name="lesson-4-select-smooth-streaming-tracks"></a><span data-ttu-id="29f32-296">Урок 4. Выбор дорожек для бесперебойной потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="29f32-296">Lesson 4: Select Smooth Streaming Tracks</span></span>
<span data-ttu-id="29f32-297">Представление бесперебойной потоковой передачи может содержать несколько видеофайлов, зашифрованных с разными уровнями качества (скоростью) и разрешениями.</span><span class="sxs-lookup"><span data-stu-id="29f32-297">A Smooth Streaming presentation can contain multiple video files encoded with different quality levels (bit rates) and resolutions.</span></span> <span data-ttu-id="29f32-298">На этом занятии предстоит включить возможность выбора потоков для пользователей.</span><span class="sxs-lookup"><span data-stu-id="29f32-298">In this lesson, you will enable users to select tracks.</span></span> <span data-ttu-id="29f32-299">Это занятие содержит следующие процедуры:</span><span class="sxs-lookup"><span data-stu-id="29f32-299">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="29f32-300">Изменение XAML-файла</span><span class="sxs-lookup"><span data-stu-id="29f32-300">Modify the XAML file</span></span>
2. <span data-ttu-id="29f32-301">Изменение кода файла behand</span><span class="sxs-lookup"><span data-stu-id="29f32-301">Modify the code behand file</span></span>
3. <span data-ttu-id="29f32-302">Компиляция и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="29f32-302">Compile and test the application</span></span>

<span data-ttu-id="29f32-303">**Изменение XAML-файла**</span><span class="sxs-lookup"><span data-stu-id="29f32-303">**To modify the XAML file**</span></span>

1. <span data-ttu-id="29f32-304">В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Конструктор представлений**.</span><span class="sxs-lookup"><span data-stu-id="29f32-304">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="29f32-305">Найдите тег &lt;Grid&gt; с именем **gridStreamAndBitrateSelection** и добавьте следующий код в конце этого тега:</span><span class="sxs-lookup"><span data-stu-id="29f32-305">Locate the &lt;Grid&gt; tag with the name **gridStreamAndBitrateSelection**, append the following code at the end of the tag:</span></span>
   
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
3. <span data-ttu-id="29f32-306">Нажмите клавиши **CTRL+S** , чтобы сохранить изменения</span><span class="sxs-lookup"><span data-stu-id="29f32-306">Press **CTRL+S** to save he changes</span></span>

<span data-ttu-id="29f32-307">**Изменение файла кода программной части**</span><span class="sxs-lookup"><span data-stu-id="29f32-307">**To modify the code behind file**</span></span>

1. <span data-ttu-id="29f32-308">В обозревателе решений щелкните правой кнопкой мыши файл **MainPage.xaml** и выберите команду **Просмотреть код**.</span><span class="sxs-lookup"><span data-stu-id="29f32-308">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="29f32-309">В пространстве имен SSPlayer добавьте следующий новый класс:</span><span class="sxs-lookup"><span data-stu-id="29f32-309">Inside the SSPlayer namespace, add a new class:</span></span>
   
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
3. <span data-ttu-id="29f32-310">В начале класса MainPage добавьте следующие определения переменных:</span><span class="sxs-lookup"><span data-stu-id="29f32-310">At the beginning of the MainPage class, add the following variable definitions:</span></span>
   
        private List<Track> availableTracks;
4. <span data-ttu-id="29f32-311">Добавьте в класс MainPage следующую область:</span><span class="sxs-lookup"><span data-stu-id="29f32-311">Inside the MainPage class, add the following region:</span></span>
   
        #region track selection
        /// <summary>
        /// Functionality to select video streams
        /// </summary>
   
        /// This Function gets the tracks for the selected video stream
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
   
        // This function gets the video stream that is playing
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
   
        // This function set the UI list box control ItemSource
        private async void refreshAvailableTracksListBoxItemSource()
        {
            try
            {
                // Update the track check box list on the UI 
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableVideoTracks.ItemsSource = availableTracks; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }        
        }
   
        // This function creates a list of the selected tracks.
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
   
        // This function selects the tracks based on user selection 
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
5. <span data-ttu-id="29f32-312">Найдите метод mediaElement_ManifestReady, измените следующий код в конце функции:</span><span class="sxs-lookup"><span data-stu-id="29f32-312">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span></span>
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. <span data-ttu-id="29f32-313">В классе MainPage найдите область событий щелчка кнопок пользовательского интерфейса и добавьте следующее определение функции:</span><span class="sxs-lookup"><span data-stu-id="29f32-313">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span></span>
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of the selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on the presentation
            changeStreams(selectedStreams);
         }

<span data-ttu-id="29f32-314">**Компиляция и тестирование приложения**</span><span class="sxs-lookup"><span data-stu-id="29f32-314">**To compile and test the application**</span></span>

1. <span data-ttu-id="29f32-315">Нажмите клавишу **F6** для компиляции проекта.</span><span class="sxs-lookup"><span data-stu-id="29f32-315">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="29f32-316">Нажмите клавишу **F5** для запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="29f32-316">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="29f32-317">В верхней части приложения можно выбрать URL-адрес бесперебойной потоковой передачи по умолчанию или ввести другой.</span><span class="sxs-lookup"><span data-stu-id="29f32-317">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="29f32-318">Щелкните **Задать источник**.</span><span class="sxs-lookup"><span data-stu-id="29f32-318">Click **Set Source**.</span></span> 
5. <span data-ttu-id="29f32-319">По умолчанию выбраны все дорожки потока видеоданных.</span><span class="sxs-lookup"><span data-stu-id="29f32-319">By default, all of the tracks of the video stream are selected.</span></span> <span data-ttu-id="29f32-320">Чтобы поэкспериментировать со скоростью, выберите минимально возможную скорость, а затем — максимально возможную.</span><span class="sxs-lookup"><span data-stu-id="29f32-320">To experiment the bit rate changes, you can select the lowest bit rate available, and then select the highest bit rate available.</span></span> <span data-ttu-id="29f32-321">После каждого изменения необходимо нажать кнопку "Отправить".</span><span class="sxs-lookup"><span data-stu-id="29f32-321">You must click Submit after each change.</span></span>  <span data-ttu-id="29f32-322">Вы увидите, как изменилось качество видеоизображения.</span><span class="sxs-lookup"><span data-stu-id="29f32-322">You can see the video quality changes.</span></span>

<span data-ttu-id="29f32-323">Вы завершили урок 4.</span><span class="sxs-lookup"><span data-stu-id="29f32-323">You have completed lesson 4.</span></span>  <span data-ttu-id="29f32-324">В этом уроке были добавлены функциональные возможности для выбора дорожек.</span><span class="sxs-lookup"><span data-stu-id="29f32-324">In this lesson, you add the functionality to choose tracks.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="29f32-325">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="29f32-325">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="29f32-326">Отзывы</span><span class="sxs-lookup"><span data-stu-id="29f32-326">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a><span data-ttu-id="29f32-327">Другие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="29f32-327">Other Resources:</span></span>
* [<span data-ttu-id="29f32-328">Создание приложения для Windows 8 с потоковой передачей Smooth Streaming на JavaScript с расширенными возможностями</span><span class="sxs-lookup"><span data-stu-id="29f32-328">How to build a Smooth Streaming Windows 8 JavaScript application with advanced features</span></span>](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [<span data-ttu-id="29f32-329">Технический обзор Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="29f32-329">Smooth Streaming Technical Overview</span></span>](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

