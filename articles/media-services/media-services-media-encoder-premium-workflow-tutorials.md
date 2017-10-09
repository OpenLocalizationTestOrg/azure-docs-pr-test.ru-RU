---
title: "учебники по aaaAvanced расширенного рабочего процесса кодировщика мультимедиа"
description: "Этот документ содержит примеры, показывающие, как tooperform сложных задач с помощью расширенного рабочего процесса кодировщика мультимедиа и также как toocreate сложных рабочих процессов с помощью конструктора рабочих процессов."
services: media-services
documentationcenter: 
author: xstof
manager: cfowler
editor: 
ms.assetid: 1ba52865-b4a8-4ca0-ac96-920d55b9d15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: christoc;xpouyat;juliako
ms.openlocfilehash: 641bd1be3bd795b5e138fa7ffdf299ff6710904e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a>Руководства по расширенному рабочему процессу кодировщика мультимедиа
## <a name="overview"></a>Обзор
Этот документ содержит пошаговые руководства, которые показывают, как toocustomize рабочих процессов с **конструктора рабочих процессов**. Найти hello файлы фактического рабочего процесса [здесь](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).  

## <a name="toc"></a>ОГЛАВЛЕНИЕ
рассматриваются следующие вопросы Hello.

* [Кодирование MXF в файл MP4 с одной скоростью](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [Запуск нового рабочего процесса](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [С помощью hello вход файл мультимедиа](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [Проверка потоков мультимедиа](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [Добавление видеокодировщика для создания файла MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [Кодировки аудиопотока hello](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [Мультиплексирование аудио- и видеопотоков в контейнер MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [Запись файла MP4 hello](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [Создание из выходного файла hello ресурс служб мультимедиа](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [Hello тест завершения рабочего процесса локально](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [Кодирование MXF в файлы MP4 с несколькими скоростями со включенной динамической упаковкой](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [Добавление одного или нескольких дополнительных выходных файлов MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [Настройка имен вывод файлов hello](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [Добавление отдельной звуковой дорожки](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [Добавление hello. SMIL ISM-файла](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [Расширенная схема кодирования файла MXF в файл MP4 с несколькими скоростями](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [Общие сведения о tooenhance рабочего процесса](#workflow-overview-to-enhance)
  * [Соглашения об именовании файлов](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [Свойства публикации компонента на hello корневого рабочего процесса](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [Создание зависимости имен созданных выходных файлов от значений опубликованных свойств](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [Добавление выходных данных MP4 toomultibitrate эскизов](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [Для эскизов tooadd обзор рабочего процесса](#workflow-overview-to-add-thumbnails-to)
  * [Добавление кодировки JPG](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [Работа с преобразованием цветового пространства](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [Написание hello эскизов](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [Обнаружение ошибок в рабочем процессе](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [Завершенный рабочий процесс](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [Обрезка выходных файлов MP4 с несколькими скоростями по времени](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [Добавление усечение toostart обзор рабочего процесса](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [С помощью hello поток устройство обрезки](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [Завершенный рабочий процесс](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [Знакомство с hello компонента в скрипт](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [Создание сценариев в рабочем процессе: hello world](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [Обрезка выходных файлов MP4 с несколькими скоростями по кадрам](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [План toostart Общие сведения о добавлении усечение](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [С помощью hello клип списка XML](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [Изменение списка hello клип из компонента в скрипт](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [Добавление удобного свойства ClippingEnabled](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <a id="MXF_to_MP4"></a>Кодирование MXF в файл MP4 с одной скоростью
В этом разделе мы создадим из входного файла MXF аудиофайл MP4 с одной скоростью, используя кодирование AAC-HE.

### <a id="MXF_to_MP4_start_new"></a>Запуск нового рабочего процесса
Откройте конструктор рабочих процессов и последовательно щелкните "Файл" > "Создать рабочую область" > "Схема перекодирования".

Hello новый рабочий процесс будет показывать три элемента:

* основной исходный файл;
* XML-файл списка клипов;
* выходной файл и ресурс-контейнер.  

![Новый рабочий процесс кодирования](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

*Новый рабочий процесс кодирования*

### <a id="MXF_to_MP4_with_file_input"></a>С помощью hello вход файл мультимедиа
В порядке tooaccept нашей входного файла мультимедиа, один начинается с добавления компонента входного файла мультимедиа. tooadd toohello рабочего процесса компонента, искать его в поле поиска репозитория hello и перетащите hello требуемого входа на панель конструктора hello. Это необходимо сделать для входного файла мультимедиа hello и подключите hello основной исходный файл компонента toohello имя файла ввода ПИН-кода hello входного файла мультимедиа.

![Соединение области "Входные файлы мультимедиа"](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

*Соединение области "Входные файлы мультимедиа"*

Прежде чем мы еще большую мы сначала потребуется конструктора рабочих процессов toohello tooindicate какие образец файла мы хотели бы toouse toodesign с рабочим процессом. toodo таким образом, щелкните фон конструктора области hello и найдите свойство hello основной исходный файл на панели справа свойство hello. Щелкните значок папки hello и выберите hello требуемого файла tootest hello рабочий процесс. Сразу же после этого компонент hello входных данных файла мультимедиа Проверьте файл hello и заполнить его выходные данные ПИН-кодов tooreflect hello файл, который его изучить.

![Заполненная область "Входные файлы мультимедиа"](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

*Заполненная область "Входные файлы мультимедиа"*

Хотя указывает с что входе, мы хотели бы toowork с, он не сообщает еще где выходные данные в кодировке hello должен быть доставлен. Аналогичные hello toohow настроенного первичный файл источника теперь настроить hello выходной папки переменной свойства, непосредственно под.

![Указанные свойства входных и выходных данных](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

*Указанные свойства входных и выходных данных*

### <a id="MXF_to_MP4_streams"></a>Проверка потоков мультимедиа
Часто желательно, как поток hello выглядит подобно показанному tooknow проходит через hello рабочего процесса. tooinspect потока в любой момент в рабочем процессе hello, просто щелкните выходного или ввода ПИН-кода на любой из компонентов hello. В этом случае попробуйте щелкнуть на закрепление вывода видео без сжатия hello нашей входных данных в файл мультимедиа. Диалоговое окно будет открыт, позволяющий tooinspect hello исходящих видео.

![Проверка закрепление вывода hello видео без сжатия](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

*Проверка закрепление вывода hello видео без сжатия*

На рисунке выше показано, что входной видеофайл имеет разрешение 1920 x 1080, скорость 24 кадра в секунду, формат выборки 4:2:2 и продолжительность почти 2 минуты.

### <a id="MXF_to_MP4_file_generation"></a>Добавление видеокодировщика для создания файла MP4
Обратите внимание, что теперь в области "Входные файлы мультимедиа" есть несколько точек выходных соединений: одна для компонента "Видео без сжатия" и по одной для каждого компонента "Аудио без сжатия". В порядке tooencode Здравствуйте входящих видео, мы должны компонента кодирования — в этом случае для создания. MP4-файлов.

tooencode hello tooH.264 потокового видео, добавьте hello кодировщик видео AVC компонент toohello рабочую область конструктора. Этот компонент преобразовывает видеопоток без сжатия в сжатый видеопоток AVC в соответствующей выходной точке.

![Несоединенный кодировщик AVC](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

*Несоединенный кодировщик AVC*

Его свойства определяют, как именно кодирование hello происходит. Давайте посмотрим на некоторые hello более важные параметры:

* Вывод ширины и высоты выходных данных: они определяют разрешения hello hello кодирования видео. В нашем примере мы выберем 640 x 360.
* Частота кадров: когда toopassthrough набора, он будет просто внедрить частота кадров источника hello, это возможных toooverride этом хотя. Обратите внимание, что такое преобразование частоты кадров не имеет компенсации движения.
* Профиль и уровень: эти свойства определяют hello AVC профиля и уровень. tooconveniently получить дополнительные сведения о разных уровнях hello и профили, щелкните значок вопросительного знака hello компонент кодировщик видео AVC hello и страница справки hello будет отображаться более подробные сведения о каждом из уровней hello. В нашем примере выберем основного профиля на уровне 3.2 (по умолчанию hello).
* Режим управления скоростью и скорость (Кбит/с). В нашем сценарии мы хотим получить выходной файл с постоянной скоростью (CBR) 1200 Кбит/с.
* : Видео это имеет место в формате hello VUI (сведения о применимости видео), записывается в поток hello H.264 (декодирования стороне сведения, которые могут быть использованы отображения hello tooenhance декодер, но не необходимым toocorrectly):
* NTSC (формат для США и Японии, используется скорость 30 кадров/с);
* PAL (формат для Европы, используется скорость 25 кадров/с).
* Режим размера группы изображений (GOP). Для наших целей мы выберем фиксированный размер групп GOP, 2-секундный интервал опорных кадров и закрытые группы GPO. Это обеспечивает совместимость с динамической упаковки служб мультимедиа Azure предоставляет приветствия.

toofeed нашей кодировщика AVC подключение из hello входного файла мультимедиа компонент toohello видео без сжатия ввода ПИН-кода из кодировщика hello AVC закрепление вывода hello видео без сжатия.

![Соединенный кодировщик AVC](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

*Соединение основного кодировщика AVC*

### <a id="MXF_to_MP4_audio"></a>Кодировки аудиопотока hello
На этом этапе закодированные видео, но hello исходного несжатые аудиопотока по-прежнему нужна toobe сжимаются. Для этого мы обратимся AAC по hello кодирование кодировщика AAC (Dolby) компонента. Добавьте toohello рабочего процесса.

![Несоединенный кодировщик AVC](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

*Несоединенный кодировщик AAC*

Теперь несовместимы: имеется только один несжатые аудио ввода ПИН-код из hello AAC кодировщика при более одного входного файла мультимедиа вероятно hello будет иметь два разных несжатых данных поток звука: один для hello слева аудио канал и один для hello Правильно. Если речь идет об объемном звучании, каналов будет шесть. Поэтому невозможно toodirectly подключиться hello звука из источника входных данных файла мультимедиа hello в кодировщик аудио AAC hello. Hello AAC ожидается, что компонент так называемые «чередованием» аудиопотока: один поток, в котором содержатся оба hello слева и hello правого каналов, чередуются друг с другом. Когда мы знаем, что из наших исходного файла мультимедиа какие звуковые дорожки на какой позиции в источнике hello, мы можно создать такие с чередованием аудиопотока с hello правильно назначаются динамика позиции для влево и вправо.

Сначала один требуется, чтобы toogenerated поток с чередованием из аудиоканалов источника необходимые hello. Hello аудио поток Interleaver компонент будет обрабатывать это за нас. Добавьте его toohello рабочего процесса и подключите аудио выходы hello hello входных данных файла мультимедиа в него.

![Соединение компонента чередования аудиопотоков](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

*Соединение компонента чередования аудиопотоков*

Теперь, когда у нас есть с чередованием аудиопоток, мы по-прежнему не был указан где разрядов tooassign динамика hello влево или вправо. В заказывать toospecify, можно использовать hello назначено позиции говорящего.

![Добавление компонента "Назначение положения динамиков"](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

*Добавление компонента "Назначение положения динамиков"*

Настроить hello динамика позиции назначено для использования с стерео входного потока через фильтр конфигурации кодировщика для «Custom» и hello предустановку канал называется «2.0 ("L", "R")». (Это будет назначить toochannel положение левого динамика hello 1 и hello динамика правой позиции toochannel 2).

Подключите выход hello hello назначено позиции динамика toohello ввода оператора hello AAC кодировщика. Затем сообщить toowork AAC кодировщика hello» 2.0 ("L", "R")» заданы канал, чтобы он доверял toodeal с стереозвук в качестве входных данных.

### <a id="MXF_to_MP4_audio_and_fideo"></a>Мультиплексирование аудио- и видеопотоков в контейнер MP4
Видеопоток в кодировке AVC и аудиопоток в кодировке AAC можно объединить в контейнере MP4. процесс Hello смешивание разных потоков в один из них, называется «мультиплексирование» (или «muxing»). В этом случае мы чередование hello аудио- и видеопотоки hello в одном согласовано. Пакет MP4. Hello компонент, координирующий для. Контейнер MP4 называется мультиплексор ISO MPEG-4 hello. Добавьте один toohello рабочую область конструктора и подключите кодировщик видео AVC hello и входные данные tooits AAC кодировщика hello.

![Соединение мультиплексора MPEG4](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

*Соединение мультиплексора MPEG4*

### <a id="MXF_to_MP4_writing_mp4"></a>Запись файла MP4 hello
При записи в выходной файл, используется компонент hello выходной файл. Представленный вывод toohello мультиплексор ISO MPEG-4 hello можно будет подключить, чтобы toodisk возвращает запись его выходных данных. toodo этого подключения hello контейнера (MPEG-4) выходного ПИН-код toohello записи входного контакта из hello выходной файл.

![Соединение компонента "Вывод файла"](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

*Соединение компонента "Вывод файла"*

Hello имя файла, который будет использоваться определяется hello свойства файла. Это свойство может быть tooa жестко заданное значение, скорее всего один будете tooset его через выражение вместо него.

рабочий процесс toohave hello автоматически определять hello выходные данные файла имя свойства из выражения, щелкните имя файла далее toohello hello кнопки (следующий значок toohello папки). В hello раскрывающемся меню выберите команду «Выражение». Откроется редактор выражений hello. Сначала очистите содержимое hello hello редактора.

![Пустой редактор выражений](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

*Пустой редактор выражений*

Редактор выражений Hello позволяет tooenter любое литеральное значение, одновременно с одной или нескольких переменных. Переменные начинаются со знака доллара. Как клавишу hello $ hello редакторе отобразится раскрывающийся список с помощью набора доступных переменных. В нашем случае мы будем использовать сочетание hello выходной каталог переменной и hello базовый входной файл имя переменной:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![Редактор выражений с указанным значением](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

*Редактор выражений с указанным значением*

> [!NOTE]
> В порядке toosee просмотреть выходной файл задания кодирования в Azure, необходимо ввести значение в редактор выражений hello.
>
>

После подтверждения выражение hello, нажав ОК, окно свойств hello будет Предварительный просмотр toowhat значение hello файла свойство разрешает на данный момент времени.

![Полученный из выражения конечный каталог](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

*Полученный из выражения конечный каталог*

### <a id="MXF_to_MP4_asset_from_output"></a>Создание из выходного файла hello ресурс служб мультимедиа
Хотя мы написали выходной файл MP4, мы по-прежнему должны tooindicate, этот файл относится toohello выходной актив, какие службы мультимедиа создаст в результате выполнения этого рабочего процесса. используется toothis end, узел hello выходной файл или ресурс на холсте hello рабочего процесса. Все файлы, входящие в этот узел будет сделать частью hello полученный активов Azure Media Services.

Подключите hello выходной файл компонента toohello выходной файл или ресурс toofinish hello рабочий процесс компонента.

![Завершенный рабочий процесс](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

*Завершенный рабочий процесс*

### <a id="MXF_to_MP4_test"></a>Hello тест завершения рабочего процесса локально
tootest рабочего процесса hello локально, нажмите кнопку "play hello" в панели инструментов hello вверху hello. По окончании выполнения рабочего процесса hello проверьте hello выходные данные, созданные в выходную папку hello настроен. Вы увидите, что выходной файл MP4, закодированную из файла источника входных данных MXF hello завершения hello.

## <a id="MXF_to_MP4_with_dyn_packaging"></a>Кодирование файлов MXF в файлы MP4 с разными скоростями со включенной динамической упаковкой
В этом разделе мы создадим из одного входного файла MXF набор файлов MP4 с несколькими скоростями и аудиокодированием AAC.

Когда выходные данные средства с несколькими скоростями требуемого для использования в сочетании с возможностями динамической упаковки hello, предлагаемых службами мультимедиа Azure, несколькими GOP-файлами формата MP4 каждого разным битрейтом и разрешение потребуется toobe создан. Таким образом, hello toodo [MXF кодировку в односкоростной MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) Пошаговое руководство предоставляет отправную точку.

![Запуск рабочего процесса](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

*Запуск рабочего процесса*

### <a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Добавление одного или нескольких дополнительных выходных файлов MP4
Каждый файл MP4 в конечном ресурсе-контейнере служб мультимедиа Azure будет поддерживать разные скорость и разрешение. Давайте добавим один или несколько MP4 выходной файлы toohello рабочего процесса.

toomake убедиться, что у нас есть все наши видео кодировщики создан с Здравствуйте одинаковые параметры, наиболее удобным tooduplicate hello уже существующих кодировщик видео AVC и настроить другое сочетание разрешения и скорости (добавим один 960 x 540 на 25 кадров в секунду в 2,5 МБ/с). tooduplicate hello существующих кодировщиков, копировать вставьте его на поверхность конструктора hello.

Подключите hello видео без сжатия вывода ПИН-код hello входных данных файла мультимедиа в наш новый компонент AVC.

![Соединение со вторым кодировщиком AVC](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

*Соединение со вторым кодировщиком AVC*

Теперь адаптировать hello конфигурации для нашей новой AVC кодировщика toooutput 960 x 540 в 2,5 Мбит/с. Эти параметры указываются в свойствах "Ширина выходного файла", "Высота выходного файла" и "Скорость (Кбит/с)".

Учитывая мы хотим полученный активов toouse hello вместе с динамической упаковки служб мультимедиа Azure, конечной точки потоковой передачи hello должен toobe может создать из этих файлов MP4, HLS или Fragmented MP4 или ТИРЕ фрагментов, которые точно выровнены tooeach другим способом Клиенты, переключение между различными значениями скорости получение один непрерывный видео- и аудиопотоки удобства. Возможно, нам нужно, в свойства hello кодировщиков AVC hello размер GOP («группа изображений») для обоих MP4-файлов задается tooensure toomake too2 секунд, которые могут быть выполнены по:

* Установка размера GOP tooFixed режима установки размеров GOP hello и
* Hello интервал кадра ключ tootwo секунд.
* также задайте hello управления IDR GOP tooClosed GOP tooensure, все GOP основано на свои собственные без зависимостей

toomake удобный toounderstand нашей рабочего процесса, переименуйте первый AVC кодировщика hello слишком» кодировщик видео AVC 640 x 360 1200 Кбит/с» и hello второй AVC кодировщика «кодировщик видео AVC 960 x 540 2500 Кбит/с».

Теперь добавьте второй компонент "Мультиплексор ISO MPEG-4" и второй компонент "Вывод файла". Подключите hello мультиплексор toohello нового AVC кодировщика и убедитесь, что его выходные данные направляются в hello выходной файл. Также подключения hello AAC аудио кодировщика вывода toohello новый мультиплексор элемента ввода. Hello выходной файл в свою очередь после этого можно tooadd узла выходной файл или ресурс подключенных toohello его toohello актив служб мультимедиа, который будет создан.

![Соединение второго мультиплексора с компонентом "Вывод файла"](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

*Соединение второго мультиплексора с компонентом "Вывод файла"*

Для обеспечения совместимости с динамической упаковки служб мультимедиа Azure настроить число tooGOP hello мультиплексор в режиме блока или длительность и выбрать hello Gop на too1 фрагмента данных. (Должно быть по умолчанию hello.)

![Режимы фрагментирования в мультиплексоре](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

*Режимы фрагментирования в мультиплексоре*

Примечание: вы можете toorepeat этот процесс для других скоростью и выходные данные средства toohello добавлены сочетания требуется toohave разрешения.

### <a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Настройка имен вывод файлов hello
У нас есть несколько отдельных файлов добавлены toohello выходной актив. Это позволяет убедиться, что hello toomake необходимость, имена файлов для каждого hello выходные файлы отличаются друг от друга и может быть даже применяются соглашения об именах файлов, становится ясно, от имени файла hello вы имеете дело с.

Имени выходного файла можно управлять через выражениях в конструкторе hello. Откройте панель свойств hello для одного из компонентов выходной файл hello и редактор выражений hello для hello свойство файла. Наш первый выходной файл был настроен через hello, следующее выражение (см. Учебник hello для перехода из [MXF tooa односкоростной вывода MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

Это означает, что наши filename определяется две переменные: hello выходных каталогов toowrite в и hello базовое имя исходного файла. Бывшая Hello предоставляется как свойство корневого рабочего процесса hello и последнем hello определяется hello входящего файла. Обратите внимание, что выходной каталог hello используется для локального тестирования; Это свойство будет переопределено hello потоков работ при выполнении рабочего процесса hello hello процессоров носитель на основе облачных служб мультимедиа Azure.
Сначала toogive оба наши выходные данные файлы вероятен согласованный результат, hello изменение файла именования выражение для:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

и hello во-вторых, чтобы:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

Выполнение промежуточных тестового запуска toomake убедиться, что правильно формируются выходные файлы обеих MP4.

### <a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Добавление отдельной звуковой дорожки
Как мы рассмотрим позже, когда мы создаем toogo файл .ism с нашей выходных файлов MP4, мы также требуется только звук MP4-файл как hello звуковой дорожки для наших адаптивной потоковой передачи. toocreate этот файл, добавьте дополнительные muxer toohello workflow (мультиплексор ISO-MPEG-4) и соедините закрепление вывода hello AAC кодировщика с ее ввода ПИН-кода для направления 1.

![Добавление мультиплексора звука](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

*Добавление мультиплексора звука*

Создайте третий выходной файл компонента toooutput hello исходящим потоком из hello muxer и настройте hello файл именования выражения в виде:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![Мультиплексор звука создает выходной файл](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

*Мультиплексор звука создает выходной файл*

### <a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Добавление hello. SMIL ISM-файла
Hello toowork динамической упаковки в сочетании с обоих MP4 файлы (и hello только звук MP4) в нашей актив служб мультимедиа, мы также требуется файл манифеста (также называемый файлом «SMIL»: язык синхронизации для интеграции мультимедиа). Этот файл указывает tooAzure Media Services, то, какие файлы MP4 доступно для динамической упаковки и какие из этих tooconsider для потоковой передачи аудио hello. Типичный файл манифеста для набора файлов MP4 с одним звуковым потоком выглядит так:

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
        <meta name="formats" content="mp4" />
      </head>
      <body>
        <switch>
          <video src="H264_1900kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_1300kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_900kbps_AAC_und_ch2_96kbps.mp4" />
          <audio src="AAC_ch2_96kbps.mp4" title="AAC_und_ch2_96kbps" />
        </switch>
      </body>
    </smil>

Hello ISM-файле содержится в операторе switch tooeach ссылка hello отдельных MP4 видеофайлов и кроме звуковой файл toothose также один (или более) ссылается на tooan MP4, содержащую только звук hello.

Создание файла манифеста hello для наших набора MP4 можно сделать с помощью компонентом, называется «Писатель манифеста AMS» hello. toouse, перетащите его на поверхность hello и подключите hello «Записывать полный набор» закрепления вывода компонентов toohello hello три выходной файл манифеста записи AMS входных данных. Убедитесь, что tooconnect hello выходные данные hello записи манифеста AMS toohello выходной файл или ресурс.

Как и в наших других файл выходных данных компонентов, настройте hello .ism имя выходного файла с помощью выражения.

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

По завершении рабочего процесса выглядит следующим образом hello ниже.

![По завершении рабочего процесса MP4 MXF toomultibitrate](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

*По завершении рабочего процесса MP4 MXF toomultibitrate*

## <a id="MXF_to__multibitrate_MP4"></a>Расширенная схема кодирования файла MXF в файл MP4 с несколькими скоростями
В hello [предыдущем пошаговом руководстве рабочего процесса](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) мы рассмотрели, как один входной актив MXF может быть преобразован в выходной актив MP4-файлов с разными скоростями, только звук MP4-файл и файл манифеста для использования в сочетании с мультимедиа Azure Динамическая упаковка служб.

Это пошаговое руководство покажет, как некоторые аспекты hello могут быть улучшены и сделать более удобной.

### <a id="MXF_to_multibitrate_MP4_overview"></a>Общие сведения о tooenhance рабочего процесса
![Tooenhance многоскоростных MP4 рабочего процесса](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

*Tooenhance многоскоростных MP4 рабочего процесса*

### <a id="MXF_to__multibitrate_MP4_file_naming"></a>Соглашения об именовании файлов
В предыдущий рабочий процесс hello простое выражение указан как hello основания для создания имен файлов выходных данных. У нас есть некоторые дублирования хотя: все компоненты файла отдельного выхода hello hello указаны такие выражения.

Например нашей компонента выходные данные файла для первого видеофайла hello настраивается с помощью этого выражения:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

Хотя для hello второй выход видео, у нас есть выражение, подобное:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

Если бы мы могли вместо этого удалить некоторые из таких повторов, мы бы сделали настройку более гибкой, аккуратной и удобной, не так ли? Кроме того, это позволит снизить вероятность возникновения ошибок. К счастью мы можем: hello конструктор возможности выражения в сочетании с пользовательскими свойствами hello возможность toocreate на нашем корневого рабочего процесса даст нам обеспечивает дополнительный уровень удобства.

Предположим, мы будем диска имя файла конфигурации из битрейтах hello hello отдельных MP4-файлов. Эти битрейтов, мы будем стремятся tooconfigure в один центральный поместите (hello корень графа нашей), из которой будете иметь доступ к которым осуществляется tooconfigure и диск создания имени файла. toodo это, начнем с публикации свойство bitrate hello от корня toohello кодировщики AVC обоих рабочим процессом, чтобы он стал доступен с обоих корневой hello также в аспекте hello AVC кодировщиков. (Даже при отображении в двух разных местах существует только одно базовое значение.)

### <a id="MXF_to__multibitrate_MP4_publishing"></a>Свойства публикации компонента на hello корневого рабочего процесса
Откройте первый AVC кодировщика hello, перейдите свойство toohello скорость (Кбит/с) и hello раскрывающемся списке выберите публикации.

![Свойство публикации bitrate hello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

*Свойство публикации bitrate hello*

Настройка hello публикации корневой toohello toopublish диалоговое окно графа наш рабочий процесс с опубликованное название «video1bitrate» и для чтения отображаемое имя «Скоростью видео 1». Укажите для пользовательской группы имя "Streaming Bitrates" и нажмите кнопку "Опубликовать".

![Свойство публикации bitrate hello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

*Диалоговое окно публикации для свойства скорости*

Повторите hello одинаковы для свойства bitrate hello hello второй AVC кодировщика и присвойте ей имя «video2bitrate» с отображаемым именем «Скоростью видео 2», что в hello одну группа «Битрейтах потоковой передачи».

Если мы теперь проверить свойства корневого рабочего процесса hello, мы рассмотрим нашей пользовательской группе отображаются два свойства опубликованного приветствия. Оба отражения значение hello их соответствующих скоростью AVC кодировщика.

![Опубликованные свойства скорости в корне рабочего процесса](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

Каждый раз, когда мы хотим tooaccess эти свойства из кода или из выражения, мы можно сделать следующим образом:

* из встроенного кода в компоненте прямо под корневым hello: node.getPropertyAsString('.. / video1bitrate', null)
* в выражении: ${ROOT_video1bitrate}.

Давайте завершите группы «Потоковой передачи Битрейтах» hello, публикации нашей звуковой дорожки скоростью в нем также. В пределах свойства hello hello AAC кодировщика поиск приветствия скоростью и выберите публикации из следующего tooit hello раскрывающийся список. Публикация toohello корень графа hello с именем «audio1bitrate» и отображаемое имя «Битрейт аудио 1» в нашей пользовательской группы «Битрейтах потоковой передачи».

![Диалоговое окно публикации для скорости аудиопотока](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

*Диалоговое окно публикации для скорости аудиопотока*

![Итоговые свойства видео и аудио в корне](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

*Итоговые свойства видео и аудио в корне*

Обратите внимание, что при изменении любого из этих трех значений также повторно настраивает значения для соответствующих компонентов hello, они связаны с hello изменения (и, где публикуется из).

### <a id="MXF_to__multibitrate_MP4_output_files"></a>Создание зависимости имен созданных выходных файлов от значений опубликованных свойств
Вместо жесткого задания нашей имена созданный файл, мы теперь можно изменить наше выражение имя файла, на каждом toorely компоненты hello выходной файл на hello bitrate свойства, которые мы только что опубликованной в корневом каталоге graph hello. Начиная с нашей первый выходной файл, найти свойство файла hello и изменить выражение hello следующим образом:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

Hello различные параметры в этом выражении можно получить доступ к и ввести, нажав знак доллара hello на клавиатуре hello в окно приветствия выражений. Один из доступных параметров hello, наши video1bitrate свойства, которое мы ранее опубликованные.

![Доступ к параметрам в редакторе выражений](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

*Доступ к параметрам в редакторе выражений*

Здравствуйте, то же самое hello выходной файл для наших второй видео:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

и для вывода hello звукового файла:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

Если теперь мы изменили bitrate hello по одной из видео hello или звуковые файлы, соответствующие кодировщика hello будет перенастроен и hello bitrate-файл имя соглашение будет соблюдаться все автоматического.

## <a id="thumbnails_to__multibitrate_MP4"></a>Добавление выходных данных MP4 toomultibitrate эскизов
Начиная с рабочий процесс, который приводит к возникновению ошибки [многоскоростных MP4 вывод MXF ввода](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), мы теперь заинтересованы в Добавление выходных данных toohello эскизы.

### <a id="thumbnails_to__multibitrate_MP4_overview"></a>Для эскизов tooadd обзор рабочего процесса
![Toostart многоскоростных MP4 рабочего процесса из](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

*Toostart многоскоростных MP4 рабочего процесса из*

### <a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Добавление кодировки JPG
Hello суть нашей создание эскизов будет компонент hello кодировщика JPG, может toooutput JPG-файлы.

![Кодировщик JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

*Кодировщик JPG*

Мы не может подключиться напрямую, однако наши видео без сжатия потока hello входных данных файла мультимедиа в кодировщик JPG hello. Вместо этого он ожидает, что toobe передающееся отдельным кадрам. Это, мы можем сделать через компонент шлюза кадра видео hello.

![Подключение кодировщик кадра шлюза toohello JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

*Подключение кодировщик кадра шлюза toohello JPG*

шлюз кадра Hello после каждого такого большого количества секунд или кадры позволяет toopass кадров видео. Hello интервал hello время и смещение, с которой это происходит, можно изменить в свойствах hello.

![Свойства шлюза видеокадров](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

*Свойства шлюза видеокадров*

Рассмотрим Создание эскиза каждую минуту, задав режим hello tooTime (в секундах) и hello too60 интервал.

### <a id="thumbnails_to__multibitrate_MP4_color_space"></a>Работа с преобразованием цветового пространства
Хотя может показаться логических ПИН-кодов без сжатия видео шлюза кадра hello и hello входных данных файла мультимедиа теперь может быть подключен, мы бы появляется предупреждение, если мы следует делать.

![Ошибка входного цветового пространства](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

*Ошибка входного цветового пространства*

Это объясняется способ hello в какой цветной сведения представлены в наш исходный необработанный несжатые видеопотока, поступающих от наших MXF отличается от какие hello ожидается JPG кодировщика. Больше — в частности, так называемые «цветовое пространство» «RGB» или «Оттенки серого» ожидается tooflow в. Это означает, что входящий видеопоток, hello видео кадра Gate потребуется toohave преобразования, сначала применяется относительно его цветовое пространство.

Перетащите hello рабочего процесса hello цвет пространства преобразователь - Intel и подключите его tooour кадра шлюза.

![Соединение преобразователя цветового пространства](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

*Соединение преобразователя цветового пространства*

В окне свойств hello подбора hello BGR 24 входа из списка Предустановка hello.

### <a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Написание hello эскизов
Отличается от наших видео MP4, hello кодировщика JPG, компонент будет выдавать более одного файла. В порядке toodeal с этим, можно использовать компонент записи файла JPG сцены поиска: он будет принимать входящие JPG эскизы hello и записи их, имени каждого файла снабженное другой номер. (hello число обычно количеству hello секунд или единицы в потоке hello, соединяющей какие эскиз hello.)

![Общие сведения о записи файла JPG поиска сцены hello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

*Общие сведения о записи файла JPG поиска сцены hello*

Настройка hello путь к папке выходных данных свойство с выражением hello: ${ROOT_outputWriteDirectory}

и hello свойство префикса имени файла с:

    ${ROOT_sourceFileBaseName}_thumb_

префикс Hello определяют правила именования файлов эскизов hello. Они будут заканчиваться с число, указывающее hello ползунка позицию в потоке hello.

![Свойства компонента записи файлов JPG для поиска сцен](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

*Свойства компонента записи файлов JPG для поиска сцен*

Подключите hello записи файла JPG поиска сцены toohello выходной файл или ресурс узел.

### <a id="thumbnails_to__multibitrate_MP4_errors"></a>Обнаружение ошибок в рабочем процессе
Подключите ввода hello hello цвет пространства преобразователь toohello необработанные без сжатия видео выходных данных. Теперь можно выполните локального тестового запуска для рабочего процесса hello. Рабочий процесс hello высока вероятность внезапно будет останавливать выполнение и указывают красным контуром в компоненте hello, произошла ошибка:

![Ошибка преобразователя цветового пространства](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

*Ошибка преобразователя цветового пространства*

Щелкните hello немного красный значок «E» в верхнем правом углу hello toosee компонента цвета пространства преобразователь hello, какова причина hello hello кодирования попытка не удалась.

![Диалоговое окно с ошибкой преобразователя цветового пространства](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

*Диалоговое окно с ошибкой преобразователя цветового пространства*

Оказывается, как вы видите, что hello входящих цветовое пространство Стандартная hello цвет пространства преобразователя имеет rec601 toobe для наших Запрошенное преобразование YUV tooRGB. а в нашем потоке не указано, что он отвечает стандарту rec601. (Rec 601 — это стандарт кодирования чередующихся аналоговых видеосигналов в форме цифрового видео. Этот стандарт указывает активную область, охватывающую 720 отсчетов сигнала яркости и 360 цветовых отсчетов для каждой строки. цвет Hello системы кодирования называется YCbCr 4:2:2.)

toofix это, мы будет указывать на наш поток, который мы имеем дело с содержимым rec601 hello метаданных. toodo, поэтому мы будем использовать компонент видео данных тип обновления, который мы будет размещаться между нашей необработанный источник и hello цвет пространства компонент преобразования. Это средство обновления типа данных позволяет hello ручное обновление некоторых данных видео свойства типа. Настройте tooindicate цвет пространства стандарт «Rec 601». Это приведет к tootag hello hello видео данных типа обновления потока с цветовое пространство «Rec 601» hello, если не было цвет места еще не определен. (Он не переопределяет все существующие метаданные, если не был установлен флажок переопределения hello.)

![Обновление стандартный цвет пространства на hello Updater тип данных](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

*Обновление стандартный цвет пространства на hello Updater тип данных*

### <a id="thumbnails_to__multibitrate_MP4_finish"></a>Завершенный рабочий процесс
Теперь, когда наши завершения рабочего процесса, выполните другой toosee тестового запуска, передать его.

![Завершенный рабочий процесс для вывода нескольких файлов MP4 с эскизами](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

*Завершенный рабочий процесс для вывода нескольких файлов MP4 с эскизами*

## <a id="time_based_trim"></a>Обрезка выходных файлов MP4 с несколькими скоростями по времени
Начиная с рабочий процесс, который приводит к возникновению ошибки [многоскоростных MP4 вывод MXF ввода](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), мы теперь заинтересованы в обрезки hello источник видео на основе меток времени.

### <a id="time_based_trim_start"></a>Добавление усечение toostart обзор рабочего процесса
![Запуск рабочего процесса tooadd усечение](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

*Запуск рабочего процесса tooadd усечение*

### <a id="time_based_trim_use_stream_trimmer"></a>С помощью hello поток устройство обрезки
Hello устройство обрезки поток дает tootrim hello начало и конец входной поток основан на данных о времени (секунды, минуты,...). устройство обрезки Hello не поддерживает усечения, основанных на кадре.

![Компонент обрезки потока](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

*Компонент обрезки потока*

Вместо соединения непосредственно hello AVC кодировщиков и toohello назначено динамика позиции ввода файла мультимедиа, мы поместили между этими устройство обрезки поток hello. (Один для hello видеосигнала и один для hello чередуются звуковых сигналов).

![Добавление компонента обрезки потока](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

*Добавление компонента обрезки потока*

Настроим устройство обрезки hello, чтобы мы будет обрабатывать только видео и аудио от 15 до 60 секунд в видео hello.

Перейдите toohello свойства hello устройство обрезки потока видео и настройте время начала (сумм, равных 15) и свойства времени окончания (60s). toomake убедитесь, что и устройство обрезки нашей аудио и видео всегда настроенных toohello же начала и окончания для значений, мы опубликуем этих toohello корневой hello рабочего процесса.

![Публикация свойства времени начала из компонента обрезки потока](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

*Публикация свойства времени начала из компонента обрезки потока*

![Диалоговое окно публикации свойства для времени начала](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

*Диалоговое окно публикации свойства для времени начала*

![Диалоговое окно публикации свойства для времени окончания](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

*Диалоговое окно публикации свойства для времени окончания*

Если мы теперь проверить hello корнем рабочего процесса, оба свойства будет аккуратно отображаются и настраиваемые оттуда.

![Опубликованные свойства, доступные в корне](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

*Опубликованные свойства, доступные в корне*

Теперь откройте свойства усечения hello из аудио устройство обрезки hello и настроить время начала и окончания выражение со ссылкой toohello опубликованные свойства в корневом каталоге hello нашей рабочего процесса.

Время начала аудио усечения для hello:

    ${ROOT_TrimmingStartTime}

Для времени окончания обрезки аудио:

    ${ROOT_TrimmingEndTime}

### <a id="time_based_trim_finish"></a>Завершенный рабочий процесс
![Завершенный рабочий процесс](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

*Завершенный рабочий процесс*

## <a id="scripting"></a>Знакомство с hello компонента в скрипт
Скрипт компоненты могут выполняться произвольные скрипты этапах выполнения hello рабочего процесса. Существует четыре различных наборов символов, которые могут быть выполнены с определенными характеристиками и собственные место в жизненного цикла рабочего процесса hello:

* **commandScript**
* **realizeScript**
* **processInputScript**
* **lifeCycleScript**

Hello документации hello в скрипт выполняется более подробно для каждого hello выше. В [hello следующий раздел](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), hello **realizeScript** сценарий компонента — используется tooconstruct cliplist xml на лету hello при запуске рабочего процесса hello. Этот сценарий вызывается во время установки компонентов hello, который происходит один раз в его жизненного цикла.

### <a id="scripting_hello_world"></a>Создание сценариев в рабочем процессе: hello world
Перетащите компонент включен в скрипт на область конструктора hello и переименуйте его (например, «SetClipListXML»).

![Добавление компонента сценариев](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*Добавление компонента сценариев*

При проверке свойств hello hello компонента в скрипт, приветствия отображаются четыре типа различных сценариев, каждый настраиваемых tooa другой сценарий.

![Свойства компонента сценариев](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*Свойства компонента сценариев*

Отмените hello processInputScript и откройте редактор hello для hello realizeScript. Теперь мы установлено и Готово toostart сценариев.

Скрипты на языке Groovy динамически скомпилированного язык сценариев для hello Java platform, сохраняет совместимость с Java. Фактически, практически весь код Java можно использовать в качестве кода Groovy.

В контексте hello нашей realizeScript напишем сценарий хорошую простой hello world. Введите в редакторе hello hello следующие данные:

    node.log("hello world");

Теперь выполните локальный тестовый запуск. После этого запуска проверки (через вкладку система hello на hello в скрипт компонента) hello свойство журналы.

![Запись "hello world" в журнале](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

*Запись "hello world" в журнале*

Hello объекта узла, которые мы называем метод журнала hello, ссылается текущий tooour «узел» или hello компонент, который мы сценарии в рамках. Таким образом, каждый компонент имеет hello данных журналов toooutput возможности, доступные через вкладка "система" hello. В этом случае мы вывода строковый литерал hello «hello world». Здесь важно toounderstand заключается в том, что это может оказаться toobe бесценным средством отладки, предоставляя подробные сведения о делать какие сценарии hello.

Из в нашей среде скриптов, нам требуется также tooproperties доступа от других компонентов. Попробуйте выполните следующее.

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up tooother nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

Наш окно журнала будут показаны следующие hello:

![Вывод журнала для доступа к путям узла](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

*Вывод журнала для доступа к путям узла*

## <a id="frame_based_trim"></a>Обрезка выходных файлов MP4 с несколькими скоростями по кадрам
Начиная с рабочий процесс, который приводит к возникновению ошибки [многоскоростных MP4 вывод MXF ввода](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), мы теперь заинтересованы в обрезки hello исходного видео, в зависимости от числа кадров.

### <a id="frame_based_trim_start"></a>План toostart Общие сведения о добавлении усечение
![Добавление усечение toostart рабочего процесса](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

*Добавление усечение toostart рабочего процесса*

### <a id="frame_based_trim_clip_list"></a>С помощью hello клип списка XML
В всех предыдущих занятий рабочего процесса мы использовали компонент входного файла мультимедиа hello как наши видео источника входных данных. Для этого конкретного сценария, мы будем работать с hello клип списка исходный компонент вместо него. Обратите внимание, что это не должна быть hello предпочтительный способ работы; Используйте hello источника коллекции списка, только если имеется toodo особого смысла, так (как и в hello ниже вариант, где мы сделали использование возможностей фильтрации по ролям список clip hello).

tooswitch из наших toohello вход файл мультимедиа источника коллекции списка, перетащите hello клип списка исходный компонент в рабочую область конструктора hello и подключите hello XML-Clip список ПИН-код toohello клип списка XML узел hello конструктора рабочих процессов. Это необходимо заполнить hello источника коллекции списка с выходных контактов, в соответствии с tooour входное видео. Теперь подключение hello без сжатия видео и аудио несжатые ПИН-коды из toohello источника списка Clip hello hello соответствующих AVC кодировщиков и Interleaver поток аудио. Теперь можно удалите hello входных данных файла мультимедиа.

![Заменены hello источника списка Clip hello вход файл мультимедиа](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

*Заменены hello источника списка Clip hello вход файл мультимедиа*

Hello клип списка исходный компонент принимает в качестве входного «XML клип списка». При выборе hello исходный файл tootest с локально, этот XML-документ клип список автоматически заполняется автоматически.

![Автоматически заполненное свойство "XML-файл списка клипов"](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

*Автоматически заполненное свойство "XML-файл списка клипов"*

Нужна немного более подробно toohello xml, это, как оно выглядит:

![Диалоговое окно изменения списка клипов](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

*Диалоговое окно изменения списка клипов*

Однако это не отражает возможности hello hello клип списка xml. У нас есть один параметр — tooadd элемент «Обрезать» в разделе hello видео и аудио источника, следующим образом:

![Добавление списка clip toohello обрезки элемента](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

*Добавление списка clip toohello обрезки элемента*

Если изменять список XML-clip hello следующим выше и выполнения локального тестового запуска, вы увидите видео hello были правильно усекаются от 10 до 20 секунд в видео hello.

Противоположные toowhat происходит при выполнении локального запуска, хотя это то же самое cliplist xml не будет иметь тот же эффект, при применении в рабочий процесс, который выполняется в Azure Media Services hello. При запуске кодировщика Premium в Azure, hello cliplist xml создается каждый раз, чтобы еще раз, на основании кодирования hello hello входного файла был передан задания. Это означает, что любые изменения, которые мы делаем hello XML-был бы к сожалению переопределен.

toocounter hello cliplist xml стирание памяти при запуске задания кодирования, мы повторно создать его на лету hello сразу после начала hello нашей рабочего процесса. Такие действия можно выполнять с помощью компонента сценариев. Дополнительные сведения см. в разделе [введение hello в скрипт компонента](media-services-media-encoder-premium-workflow-tutorials.md#scripting).

Перетащите компонент включен в скрипт на область конструктора hello и переименуйте его слишком «SetClipListXML».

![Добавление компонента сценариев](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*Добавление компонента сценариев*

При проверке свойств hello hello компонента в скрипт, приветствия отображаются четыре типа различных сценариев, каждый настраиваемых tooa другой сценарий.

![Свойства компонента сценариев](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*Свойства компонента сценариев*

### <a id="frame_based_trim_modify_clip_list"></a>Изменение списка hello клип из компонента в скрипт
Прежде чем повторно можно написать hello cliplist xml, который создается во время запуска рабочего процесса, мы должны, toohave доступ toohello cliplist xml свойства и содержимое. Это можно сделать следующим образом.

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![Записи о входящем списке клипов в журнале](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

*Записи о входящем списке клипов в журнале*

Сначала мы должны toodetermine способом начиная с какого момента до чего мы хотим tootrim hello видео. Публикация этого пользователя-специалистами удобный toohello hello рабочего процесса, toomake два свойства toohello корень графа hello. toodo это, щелкните правой кнопкой мыши область конструктора hello и выберите «Добавить свойство»:

* Первое свойство — ClippingTimeStart. Тип — TIMECODE.
* Второе свойство — ClippingTimeEnd. Тип — TIMECODE.

![Диалоговое окно добавления свойства для времени начала обрезки](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

*Диалоговое окно добавления свойства для времени начала обрезки*

![Опубликованные свойства времени обрезки в корне рабочего процесса](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

*Опубликованные свойства времени обрезки в корне рабочего процесса*

Настройте оба свойства tooa подходящее значение.

![Настройка hello, изменение свойств начала и окончания](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

*Настройка hello, изменение свойств начала и окончания*

Теперь оба свойства можно передать в сценарий.

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![Окно журнала, показывающее начало и конец обрезки](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

*Окно журнала, показывающее начало и конец обрезки*

Давайте анализ строк hello код времени в виде toouse более удобным, с помощью простого регулярного выражения:

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![Окно журнала с преобразованными кодами времени](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

*Окно журнала с преобразованными кодами времени*

Под рукой такую информацию теперь можете изменить hello cliplist xml tooreflect hello начала и время окончания hello требуемого точные рамки обрезки hello фильма.

![Элементы trim tooadd код сценария](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

*Элементы trim tooadd код сценария*

Мы это сделали с помощью обычных операций по обработке строк. Hello результирующий xml списка измененной картинки записываются обратно свойство clipListXML toohello в корневом каталоге hello рабочего процесса с помощью метода SetProperty» —» hello. окно журнала Hello после другого теста будет показывать нам hello следующие:

![Ведение журнала hello полученный список клип](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

*Ведение журнала hello полученный список клип*

Сделайте toosee тестового запуска, как видео- и аудиопотоки hello было обрезано. Вам предстоит выполнить более одного тестового запуска с различными значениями для точки усечения hello, вы заметите, что те будет не принимать во внимание Однако! Hello причиной этого является hello конструктора, в отличие от hello среды выполнения Azure, не переопределение hello cliplist xml каждого запуска. Это означает, что только hello первом установки hello и выхода из системы точек, будет привести hello xml tootransform, все другие hello постоянно, в нашей guard предложения (если (clipListXML.indexOf («<trim>») == -1)) предотвратит добавление другого trim hello рабочего процесса элемент, если таковой уже существует.

toomake наш рабочий процесс удобный tootest локально, мы наиболее добавить хранение дома код, который проверяет, если trim элемент уже существует. Если Да, мы можем удалить перед продолжением путем изменения XML-кода hello с новыми значениями hello. Вместо использования простых операций со строками, это, возможно, более безопасные toodo этого с помощью объекта реальные xml модели синтаксического анализа.

Для такой код можно добавить Впрочем, мы потребуется tooadd нашей сценария сначала запустить несколько операторов импорта на hello.

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

После этого можно добавить необходимые очистки кода hello:

    //for local testing: delete any pre-existing trim elements from hello clip list xml by parsing hello xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
     //delete hello trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

Этот код представляет над hello точки, с которой мы добавляем toohello cliplist hello trim элементы xml.

На этом этапе мы запустить и изменить можно как почти так же, мы хотим во время изменения hello, когда-либо применены время рабочего процесса.    

### <a id="frame_based_trim_clippingenabled_prop"></a>Добавление удобного свойства ClippingEnabled
Может не всегда необходимо toohappen усечения, давайте завершить создание рабочего процесса, добавив удобный логический флаг, который указывает ли мы хотим tooenable обрезки / обрезки.

Так же как и ранее, публикации новый корневой элемент toohello свойство из наших рабочий процесс с именем «ClippingEnabled» типа «BOOLEAN».

![Публикация свойства для включения обрезки](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

*Публикация свойства для включения обрезки*

С hello ниже простое условие предложения мы установите флажок, если требуется фильтрация по ролям и решить, если наш список clip таким образом должен toobe, изменены или нет.

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <a id="code"></a>Полный код
    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: \n" + clipListXML);
    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from hello clip list xml by parsing hello xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
    //delete hello trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }

    //add trim elements toocliplist xml
    if ( clipListXML.indexOf("<trim>") == -1 )
    {
        //trim video
        clipListXML = clipListXML.replace("<videoSource>","<videoSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\"" + endframerate +"\"> " + endtimecode +
            " </outPoint>\n </trim> \n");
        //trim audio
        clipListXML = clipListXML.replace("<audioSource>","<audioSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\""+ endframerate +"\">" +
            endtimecode + "</outPoint>\n </trim>\n");
        node.log( "clip list going out: \n" +clipListXML );
        node.setProperty("../clipListXml",clipListXML);
    }


## <a name="also-see"></a>См. также:
[Знакомство со Службой кодирования категории "Премиум" в службах мультимедиа Azure](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[Как tooUse расширенной кодировки в службах мультимедиа Azure](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[Обзор и сравнение кодировщиков мультимедиа Azure по запросу](media-services-encode-asset.md#media-encoder-premium-workflow)

[Форматы и кодеки рабочего процесса Premium Media Encoder](media-services-premium-workflow-encoder-formats.md)

[Примеры файлов рабочего процесса](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[Средство Explorer для служб мультимедиа Azure](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
