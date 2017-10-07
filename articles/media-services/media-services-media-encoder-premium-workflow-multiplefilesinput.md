---
title: "aaaMultiple входных файлов и свойства компонента с помощью кодировщика Premium - Azure | Документы Microsoft"
description: "В этом разделе объясняется, как toouse setRuntimeProperties toouse несколько входных данных файлов и передать обработчик мультимедиа расширенного рабочего процесса кодировщика мультимедиа toohello пользовательские данные."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: 7fb35bdd-9891-4401-a65b-ef3cc8190e8a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: xpouyat;anilmur;juliako
ms.openlocfilehash: e14d10fbf9669e0b88e5ba1c519f1ba5e0bafdd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a>Использование нескольких входных файлов и свойств компонентов в кодировщике Premium
## <a name="overview"></a>Обзор
Существуют сценарии, в которых может потребоваться toocustomize свойства компонента, укажите XML-список Clip содержимое или отправить несколько входных файлов, при отправке задачи с помощью hello **расширенного рабочего процесса кодировщика мультимедиа** обработчика мультимедиа. Ниже приведены некоторые примеры.

* Наложения текста на видео и задание hello текстовое значение (например, hello текущая дата) во время выполнения для каждого входного видео.
* Настройка hello клип списка XML (toospecify одно или несколько исходных файлов, с или без обрезки и т. д.).
* Перекрытия изображение эмблемы на входное видео hello, пока hello видео кодируется.
* Кодирование нескольких аудиодорожек на разных языках.

toolet hello **расширенного рабочего процесса кодировщика мультимедиа** знать, что некоторые свойства в рабочем процессе hello изменяется при создании задачи hello или отправить несколько входных файлов, имеют toouse строку конфигурации, содержащий  **setRuntimeProperties** и/или **transcodeSource**. В этом разделе объясняется, каким образом toouse их.

## <a name="configuration-string-syntax"></a>Синтаксис строки конфигурации
tooset строка конфигурации Hello в hello кодирования задач использует XML-документ, который выглядит следующим образом:

```xml
<?xml version="1.0" encoding="utf-8"?>
<transcodeRequest>
  <transcodeSource>
  </transcodeSource>
  <setRuntimeProperties>
    <property propertyPath="Media File Input/filename" value="VideoFileName.mp4" />
  </setRuntimeProperties>
</transcodeRequest>
```

Hello ниже приведен код hello C#, который считывает из файла конфигурации XML hello, обновите его с hello право видео имя файла и передает его toohello задач в задании:

```c#
string premiumConfiguration = ReadAllText(@"D:\home\site\wwwroot\Presets\SetRuntime.xml").Replace("VideoFileName", myVideoFileName);

// Declare a new job.
IJob job = _context.Jobs.Create("Premium Workflow encoding job");

// Get a media processor reference, and pass tooit hello name of hello 
// processor toouse for hello specific task.
IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

// Create a task with hello encoding details, using a string preset.
ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                              processor,
                              premiumConfiguration,
                              TaskOptions.None);

// Specify hello input assets
task.InputAssets.Add(workflow); // workflow asset
task.InputAssets.Add(video); // video asset with multiple files

// Add an output asset toocontain hello results of hello job. 
// This output is specified as AssetCreationOptions.None, which 
// means hello output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);
```

## <a name="customizing-component-properties"></a>Настройка свойств компонентов
### <a name="property-with-a-simple-value"></a>Свойство с простым значением
В некоторых случаях бывает полезно toocustomize свойство компонента вместе с файлом hello рабочего процесса, который будет выполнен задачей расширенного рабочего процесса кодировщика мультимедиа toobe.

Предположим, что разработано рабочего процесса, наложений текста на видео текста hello (например, hello текущая дата) должен toobe набора во время выполнения. Это можно сделать путем отправки toobe текст hello задайте hello кодирования задач как hello новое значение для свойства текста hello hello наложения компонента. Этот механизм toochange других свойств компонента можно использовать в рабочем процессе hello (например, «hello положение или цвет наложения hello, скоростью hello hello AVC кодировщика и т. д.).

**setRuntimeProperties** — это свойство в компоненты hello hello рабочего процесса используется toooverride.

Пример:

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="MyInputVideo.mp4" />
      <property propertyPath="/primarySourceFile" value="MyInputVideo.mp4" />
      <property propertyPath="Optional Text Overlay/Text tooImage Converter/text" value="Today is Friday hello 13th of May, 2016"/>
  </setRuntimeProperties>
</transcodeRequest>
```

### <a name="property-with-an-xml-value"></a>Свойство со значением XML
Инкапсуляция tooset свойство, которое ожидает значение XML, с помощью `<![CDATA[ and ]]>`.

Пример:

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

> [!NOTE]
> Убедитесь, что сразу после возврата tooput каретки `<![CDATA[`.

### <a name="propertypath-value"></a>Значение propertyPath
В предыдущих примерах hello был hello propertyPath «/ мультимедийных файлов входных данных и имя файла» или «/ inactiveTimeout» или «clipListXml».
Это, как правило, имя hello hello компонента, а затем имя hello hello свойства. Hello путь может содержать большее или меньшее число уровней, например «/ primarySourceFile» (так как свойство hello в корне hello hello рабочего процесса) или «/ видео обработки и график наложения и непрозрачности» (так как наложение hello в группе).    

toocheck hello путь и имя свойства, используйте hello кнопка, немедленно расположенный возле каждого свойства. Вы можете нажать эту управляющую кнопку и выбрать команду **Изменить**. При этом будут отображены вы hello фактическое имя свойства hello и непосредственно над ним, hello пространства имен.

![Действие/Изменить](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![Свойство](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a>Несколько входных файлов
Каждая задача отправки toohello **расширенного рабочего процесса кодировщика мультимедиа** требует два средства:

* Hello сначала он *активов рабочего процесса* , содержащий файл рабочего процесса. Файлы рабочего процесса можно создать с помощью hello [конструктора рабочих процессов](media-services-workflow-designer.md).
* Hello второй раз — *актив мультимедиа* , содержащий hello файлов мультимедиа, которое следует tooencode.

При отправке нескольких toohello файлов мультимедиа **расширенного рабочего процесса кодировщика мультимедиа** кодировщика, применяются следующие ограничения hello:

* Все носители hello, файлы должны находиться в hello же *актив мультимедиа*. Использование нескольких ресурсов мультимедиа не поддерживается.
* Необходимо задать hello первичный файл в этот актив мультимедиа (в идеальном случае это hello основной файл видео, hello кодировщика запрашивается tooprocess).
* Это toopass необходимые данные конфигурации, включающий hello **setRuntimeProperties** и/или **transcodeSource** элемент toohello процессора.
  * **setRuntimeProperties** toooverride используется свойство filename hello или другому свойству в компонентах hello hello рабочего процесса.
  * **transcodeSource** — используется toospecify hello XML-Clip список содержимого.

Подключения в рабочем процессе hello:

* Если используется один или несколько компонентов входных данных файла мультимедиа и планирование toouse **setRuntimeProperties** toospecify Здравствуйте, имя файла, а затем компонент ПИН-кода hello первичный файл toothem не подключаются. Убедитесь, что соединение между объектом первичный файл hello и hello входными данными файла носителя отсутствует.
* Если вы предпочитаете toouse клип списка XML и один компонент источник мультимедиа, затем можно соединить оба.

![Нет соединения с tooMedia первичный файл источника входных данных файла](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

*Если свойство setRuntimeProperties tooset hello filename отсутствует подключение из tooMedia hello первичный файл входных данных файла компонентов.*

![Подключение из коллекции списка XML tooClip источника списка](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

*Можно подключиться tooMedia-Clip списка XML источника и использовать transcodeSource.*

### <a name="clip-list-xml-customization"></a>Настройка XML-файла со списком клипов
Можно указать hello клип списка XML в рабочем процессе hello во время выполнения с помощью **transcodeSource** в конфигурации hello строки XML. Это требуется hello клип списка XML ПИН-код toobe подключен toohello источник мультимедиа компонент в рабочем процессе hello.

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <transcodeSource>
      <clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
      </clipList>
    </transcodeSource>
    <setRuntimeProperties>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

Если вы хотите toouse /primarySourceFile toospecify этих выходных данных свойство tooname hello файлов при помощи «Expressions», то рекомендуется передача hello клип списка XML как свойство *после* свойство /primarySourceFile hello, tooavoid наличие hello картинки переопределяться /primarySourceFile приветствия.

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="c:\temp\start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

Ниже приведен код с дополнительной точной обрезкой кадров.

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

## <a name="example-1--overlay-an-image-on-top-of-hello-video"></a>Пример 1: Наложение изображение поверх видео hello

### <a name="presentation"></a>Уровень представления
Рассмотрим пример, в котором нужно toooverlay изображение эмблемы на входное видео hello во время кодирования видео hello. В этом примере hello входное видео с именем «Microsoft_HoloLens_Possibilities_816p24.mp4» и эмблема hello называется «logo.png». Необходимо выполнить следующие шаги hello:

* Создание активов рабочего процесса с файлом hello рабочих процессов (см. следующий пример hello).
* Создать актив мультимедиа, который содержит два файла: MyInputVideo.mp4 как hello первичный файл и MyLogo.png.
* Отправка toohello задача расширенного рабочего процесса кодировщика мультимедиа media ресурсы процессора с hello выше входных данных и укажите hello, следующая строка конфигурации.

Конфигурация:

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

В приведенном выше примере hello имя hello hello видеофайл отправляется toohello вход файл мультимедиа компонента и hello primarySourceFile свойство. Имя файла логотипа hello Hello отправляется tooanother входных данных файла мультимедиа, являющийся компонентом графические наложения подключенных toohello.

> [!NOTE]
> Имя файла видео Hello отправляется toohello primarySourceFile свойство. Здравствуйте, причиной этого является toouse это свойство в рабочем процессе hello для построения с помощью выражений, например имя hello правильный выходного файла.

### <a name="step-by-step-workflow-creation"></a>Пошаговое создание рабочего процесса
Ниже приведены шаги toocreate hello рабочий процесс, который принимает в качестве входных данных два файла: видео и изображения. Он отправляет сообщение hello изображение поверх видео hello.

Откройте **конструктор рабочих процессов** и последовательно щелкните **Файл** > **Создать рабочую область** > **Схема перекодирования**.

новый рабочий процесс Hello показано три элемента:

* основной исходный файл;
* XML-файл списка клипов;
* выходной файл и ресурс-контейнер.  

![Новый рабочий процесс кодирования](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

*Новый рабочий процесс кодирования*

В порядке tooaccept hello входного файла мультимедиа начните с добавления компонент входного файла мультимедиа. tooadd toohello рабочего процесса компонента, искать его в поле поиска репозитория hello и перетащите hello требуемого входа на панель конструктора hello.

Затем добавьте toobe hello видеофайлов, используемых при разработке рабочего процесса. toodo таким образом, нажмите кнопку область фона hello в конструкторе рабочих процессов и найдите свойство hello основной исходный файл на панели справа свойство hello. Щелкните значок папки hello и выберите соответствующий файл видео hello.

![Основной источник файла](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

*Основной источник файла*

Затем укажите видеофайл hello в компоненте hello входных данных файла мультимедиа.   

![Источник входного файла мультимедиа](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

*Источник входного файла мультимедиа*

Сразу же после этого компонент hello входных данных файла мультимедиа Проверьте файл hello и заполнения его выходной ПИН-кодов tooreflect hello файл, который его изучить.

Hello следующим шагом является tooadd tooRec.709 пространства toospecify hello «Видео данных тип обновления» цвета. Добавить «Видео формата преобразователь», заданный тип макета и макета tooData = плоские можно настроить. Это преобразует hello видеопотока tooa формат, который может считаться исходного компонента наложения hello.

![Компоненты "Обновление типа видеоданных" и "Конвертер форматов видео"](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

*Компоненты "Обновление типа видеоданных" и "Конвертер форматов видео"*

![Тип макета — Configurable Planar (Настраиваемый переключатель)](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

*Тип макета — "Configurable Planar"*

Затем добавьте компонент наложения видео и подключения hello (без сжатия) видео ПИН-код toohello (без сжатия) видео контакта входного файла мультимедиа hello.

Добавления другой входного файла мультимедиа (файл эмблемы hello tooload), щелкните этот компонент и переименуйте его слишком «Logo входных данных файла мультимедиа», а затем выберите образ (PNG-файл для примера) свойство файла hello. Подключения контакта hello без сжатия изображения ПИН-код toohello без сжатия изображения hello наложения.

![Компонент наложения и источник файла изображения](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

*Компонент наложения и источник файла изображения*

Если следует toomodify положение hello hello эмблемы на видео hello (например, может потребоваться tooposition на 10 процентов от верхней hello левом углу hello видео), снимите флажок «Ручной ввод» hello. Это можно сделать, так как вы используете входных данных файла мультимедиа tooprovide hello логотип файл toohello наложения компонента.

![Положение наложения](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

*Положение наложения*

tooencode hello tooH.264 потокового видео, добавьте hello кодировщик видео AVC и AAC кодировщика компонентов toohello рабочую область конструктора. Подключите hello ПИН-кодов.
Настройка кодировщика AAC hello и выберите преобразование формата аудио/стиль: 2.0 ("L", "R").

![Кодировщики аудио и видео](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

*Кодировщики аудио и видео*

Теперь добавьте hello **ISO Mpeg-4 мультиплексор** и **выходной файл** компоненты и подключите hello ПИН-коды, как показано.

![Мультиплексор MP4 и вывод файла](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

*Мультиплексор MP4 и вывод файла*

Требуется имя hello tooset для hello выходного файла. Нажмите кнопку hello **выходной файл** компонента и измените выражение hello hello файла:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![Имя вывода файла](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

*Имя вывода файла*

Можно запустить рабочий процесс hello локально toocheck, на котором работает правильно.

После завершения его можно запустить в службах мультимедиа Azure.

Во-первых, Подготовка актива в службах мультимедиа Azure с двумя файлами в нем: hello видеофайлов и эмблема hello. Это можно сделать с помощью hello .NET или REST API. Также это можно сделать с помощью портала Azure hello или [обозреватель служб мультимедиа Azure](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).

В этом учебнике показано как активы toomanage с AMSE. Существует два способа tooadd файлы tooan активов.

* Создать локальную папку, скопируйте файлы hello двумя и перетащите toohello папку hello **активов** вкладки.
* Передача hello видеофайл как основное средство, отобразить сведения об активе hello, перейдите на вкладку файлы toohello и передать дополнительный файл (эмблема).

> [!NOTE]
> Сделать tooset убедиться, что первичный файл в ресурсе hello (hello основного видео-файл).

![Файлы ресурсов в AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

*Файлы ресурсов в AMSE*

Выберите средство hello и выберите tooencode с помощью кодировщика Premium. Отправить рабочий процесс hello и выберите его.

Щелкните hello кнопка toopass данных toohello процессора и добавьте следующие свойства среды выполнения hello tooset XML hello.

![Кодировщик Premium в AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

*Кодировщик Premium в AMSE*

Вставьте hello следующие XML-данных. Требуется имя hello toospecify hello видеофайла hello входных данных файла мультимедиа и primarySourceFile. Укажите имя hello hello имя файла для логотипа hello слишком.

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

![setRuntimeProperties](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture20_amsexmldata.png)

*setRuntimeProperties*

Если вы используете .NET SDK toocreate hello и запуска задачи «hello», этот XML-данных имеет toobe передаются как строка hello конфигурации.

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

После завершения задания hello hello MP4-файл в hello выходные данные средства, которое отображает hello наложения!

![Наложение на hello видео](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

*Наложение на hello видео*

Вы можете загрузить пример hello рабочего процесса из [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).

## <a name="example-2--multiple-audio-language-encoding"></a>Пример 2. Кодирование нескольких аудиодорожек на разных языках

Пример рабочего процесса кодирования нескольких аудиодорожек на разных языках доступен в [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).

Эта папка содержит образец рабочего процесса, который можно использовать tooencode ресурс MXF файл tooa несколькими MP4 файлы с нескольких звуковых дорожек.

Этот рабочий процесс предполагает, что этот файл MXF hello содержит один звуковой дорожки; Hello дополнительных звуковые дорожки должны передаваться как отдельные файлы звука (WAV или MP4...).

tooencode, выполните следующие действия:

* Создайте актив служб мультимедиа с помощью файла MXF hello и hello звуковые файлы (0 too18 аудио).
* Убедитесь, что этот файл MXF hello задан как первичный файл.
* Создание заданий и задач, с помощью обработчика рабочего процесса кодировщика Premium hello. Используйте рабочий процесс hello, предоставляемые (MultiMP4-1080p-19audio-v1.workflow).
* Передайте задачу toohello hello setruntime.xml данных (если используется обозреватель служб мультимедиа Azure, кнопка «передать рабочего процесса toohello данных xml» hello ").
  * Обновите hello XML данных toospecify hello правильный файл языки и имена тегов.
  * Hello рабочий процесс состоит из аудио компонентов с именем tooAudio аудио 1 18.
  * RFC5646 поддерживается для тега языка hello.

```xml
<?xml version="1.0" encoding="utf-16"?>
<transcodeRequest>
  <setRuntimeProperties>
    <property propertyPath="Media File Input Video/filename" value="MainVideo.mxf" />
    <property propertyPath="Language/language_code" value="en" />
    <property propertyPath="/primarySourceFile" value="MainVideo.mxf" />
    <property propertyPath="Audio 1/Media File Input/filename" value="french-audio.wav" />
    <property propertyPath="Audio 1/Language/language_code" value="fr" />
    <property propertyPath="Audio 2/Media File Input/filename" value="german-audio.wav" />
    <property propertyPath="Audio 2/Language/language_code" value="de" />
    <property propertyPath="Audio 3/Media File Input/filename" value="japanese-audio.wav" />
    <property propertyPath="Audio 3/Language/language_code" value="ja" />
  </setRuntimeProperties>
</transcodeRequest>
```

* Hello кодировке активов будет содержать звуковые дорожки нескольких языков и эти записи должно быть доступным для выбора в Azure Media Player.

## <a name="see-also"></a>См. также
* [Знакомство со Службой кодирования категории "Премиум" в службах мультимедиа Azure](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [Как toouse расширенной кодировки в службах мультимедиа Azure](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [Обзор и сравнение кодировщиков мультимедиа Azure по запросу](media-services-encode-asset.md#media-encoder-premium-workflow)
* [Форматы и кодеки рабочего процесса Premium Media Encoder](media-services-premium-workflow-encoder-formats.md)
* [Примеры файлов рабочего процесса](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [Средство Explorer для служб мультимедиа Azure](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
