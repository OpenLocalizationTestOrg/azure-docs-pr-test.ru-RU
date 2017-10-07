---
title: "Кодировщик стандартной схеме aaaMedia | Документы Microsoft"
description: "Hello разделе приводится обзор hello Media Encoder стандартной схемы."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 4c060062-8ef2-41d9-834e-e81e8eafcf2e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 82bad27b9546f75557ac691ff148b46990647632
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="media-encoder-standard-schema"></a>Схема Media Encoder Standard
В этом разделе описываются некоторые элементы hello и типы XML-схемы hello на котором [Media Encoder стандартные стили](media-services-mes-presets-overview.md) основаны. Hello разделе приводится описание элементов и их допустимые значения. Hello полной схемы будут опубликованы в будущем.  

## <a name="Preset"></a> Предустановка (корневой элемент)
Определяет предустановку кодирования.  

### <a name="elements"></a>Элементы
| Имя | Тип | Описание |
| --- | --- | --- |
| **Кодирование** |[Кодирование](media-services-mes-schema.md#Encoding) |Корневой элемент указывает источников входных данных hello toobe кодировке. |
| **Outputs** |[Outputs](media-services-mes-schema.md#Output) |Коллекция требуемых выходных файлов. |

### <a name="attributes"></a>Атрибуты
| Имя | Тип | Описание |
| --- | --- | --- |
| **Версия**<br/><br/> Обязательно |**xs:decimal** |Hello предварительно версии. Hello применяются следующие ограничения: значение xs:fractionDigits = значение «1» и xs:minInclusive = «1», например, **версия = «1.0»**. |

## <a name="Encoding"></a> Кодирование
Содержит последовательность hello следующие элементы.  

### <a name="elements"></a>Элементы
| Имя | Тип | Описание |
| --- | --- | --- |
| **H264Video** |[H264Video](media-services-mes-schema.md#H264Video) |Параметры кодирования видео в формате H.264. |
| **AACAudio** |[AACAudio](media-services-mes-schema.md#AACAudio) |Параметры кодирования аудио в формате AAC. |
| **BmpImage** |[BmpImage](media-services-mes-schema.md#BmpImage) |Параметры изображения в формате BMP. |
| **PngImage** |[PngImage](media-services-mes-schema.md#PngImage) |Параметры изображения в формате PNG. |
| **JpgImage** |[JpgImage](media-services-mes-schema.md#JpgImage) |Параметры изображения в формате JPG. |

## <a name="H264Video"></a> H264Video
### <a name="elements"></a>Элементы
| Имя | Тип | Описание |
| --- | --- | --- |
| **TwoPass**<br/><br/> minOccurs="0" |**xs:boolean** |Сейчас поддерживается только однопроходное кодирование. |
| **KeyFrameInterval**<br/><br/> minOccurs="0"<br/><br/> **default="00:00:02"** |**xs:time** |Определяет hello фиксированной интервалы между кадрами IDR в секундах. Также называется длительность GOP tooas hello. В разделе **SceneChangeDetection** (см. ниже) для управления ли hello кодировщик может отличаться от этого значения. |
| **SceneChangeDetection**<br/><br/> minOccurs="0"<br/><br/> default=”false” |**xs:boolean** |Если набор tootrue, кодировщик попыток сцены toodetect изменением в видео hello и вставка IDR рамки. |
| **Complexity**<br/><br/> minOccurs="0"<br/><br/> default="Balanced" |**xs:string** |Элементы управления hello компромисса между кодирования качества скорость и видео. Может принимать одно из последующих значений hello: **скорость**, **Сбалансированный**, или **качества**<br/><br/> Значение по умолчанию: **Balanced**. |
| **SyncMode**<br/><br/> minOccurs="0" | |Функция будет доступна в будущих выпусках. |
| **H264Layers**<br/><br/> minOccurs="0" |[H264Layers](media-services-mes-schema.md#H264Layers) |Коллекция уровней выходных видео. |

### <a name="attributes"></a>Атрибуты
| Имя | Тип | Описание |
| --- | --- | --- |
| **Condition** |**xs:string** | После ввода hello нет изображения можно tooforce hello кодировщика tooinsert монохромный видеодорожки. toodo, использовать условие = «InsertBlackIfNoVideoBottomLayerOnly» (tooinsert видео битрейтом hello наименьшее) или условие = «InsertBlackIfNoVideo» (tooinsert видео на всех битрейтах в выходных данных). Чтобы узнать больше, ознакомьтесь с [этим](media-services-advanced-encoding-with-mes.md#no_video) разделом.|

## <a name="H264Layers"></a> H264Layers

По умолчанию при отправке входных toohello кодировщик, содержит только аудио и видео не, hello выходного актива будет содержать файлы аудио только с данными. Некоторые проигрыватели не удается toohandle такого потока вывода. Можно использовать hello H264Video **InsertBlackIfNoVideo** задания tooadd кодировщика hello tooforce видеодорожки toohello вывода в этом случае атрибут. Чтобы узнать больше, ознакомьтесь с [этим](media-services-advanced-encoding-with-mes.md#no_video) разделом.
              
### <a name="elements"></a>Элементы
| Имя | Тип | Описание |
| --- | --- | --- |
| **H264Layer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[H264Layer](media-services-mes-schema.md#H264Layer) |Коллекция уровней H264. |

## <a name="H264Layer"></a> H264Layer
> [!NOTE]
> Видео ограничения основаны на значениях hello, описанные в hello [H264 уровни](https://en.wikipedia.org/wiki/H.264/MPEG-4_AVC#Levels) таблицы.  
> 
> 

### <a name="elements"></a>Элементы
| Имя | Тип | Описание |
| --- | --- | --- |
| **Профиль**<br/><br/> minOccurs="0"<br/><br/> default=”Auto” |**xs:string** |Может иметь одно из следующих hello **xs: String** значения: **автоматически**, **базового**, **Main**, **высокой**. |
| **Level**<br/><br/> minOccurs="0"<br/><br/> default=”Auto” |**xs:string** | |
| **Bitrate**<br/><br/> minOccurs="0" |**xs:int** |Hello скорость, использующаяся для этого слоя видео, указанный в Кбит/с. |
| **MaxBitrate**<br/><br/> minOccurs="0" |**xs:int** |Hello Максимальная скорость, использующаяся для этого слоя видео, указанный в Кбит/с. |
| **BufferWindow**<br/><br/> minOccurs="0"<br/><br/> default="00:00:05" |**xs:time** |Длина буфера hello. |
| **Width**<br/><br/> minOccurs="0" |**xs:int** |Ширина hello вывода кадра видео, в пикселях.<br/><br/> Обратите внимание, что сейчас необходимо указывать и ширину, и высоту. Hello ширина и высота должны toobe четные числа. |
| **Height**<br/><br/> minOccurs="0" |**xs:int** |Высота hello вывода кадра видео, в пикселях.<br/><br/> Обратите внимание, что сейчас необходимо указывать и ширину, и высоту. Hello ширина и высота должны toobe четные числа.|
| **BFrames**<br/><br/> minOccurs="0" |**xs:int** |Число кадров B между опорными кадрами. |
| **ReferenceFrames**<br/><br/> minOccurs="0"<br/><br/> default=”3” |**xs:int** |Число опорных кадров в GOP. |
| **EntropyMode**<br/><br/> minOccurs="0"<br/><br/> default=”Cabac” |**xs:string** |Может принимать одно из последующих значений hello: **Cabac** и **Cavlc**. |
| **FrameRate**<br/><br/> minOccurs="0" |Рациональное число |Определяет частоту кадров hello hello вывода видео. Используйте значение по умолчанию «0 или 1» toolet hello кодировщика используйте hello одного кадра интенсивность как hello ввода видео. Допустимые значения: ожидаемое toobe Общие видео частоту обновления, как показано ниже. Но допустимо любое рациональное число. Например, значение 1/1 — это 1 кадр/с. Оно является допустимым.<br/><br/> - 12/1 (12 кадров/с)<br/><br/> - 15/1 (15 кадров/с)<br/><br/> - 24/1 (24 кадра/с)<br/><br/> - 24 000/1001 (23,976 кадра/с)<br/><br/> - 25/1 (25 кадров/с)<br/><br/>  - 30/1 (30 кадров/с)<br/><br/> - 30 000/1001 (29,97 кадра/с) <br/> <br/>**Примечание** при создании пользовательской предустановки для кодирования несколькими скоростями, затем все слои hello предустановленный набор **должен** используйте hello же значение частоты кадров.|
| **AdaptiveBFrame**<br/><br/> minOccurs="0" |**xs:boolean** |Копия из кодировщика мультимедиа Azure |
| **Slices**<br/><br/> minOccurs="0"<br/><br/> default="0" |**xs:int** |Определяет число фрагментов для разделенного кадра. Рекомендуется использовать значение по умолчанию. |

## <a name="AACAudio"></a> AACAudio
 Содержит последовательность hello следующие элементы и группы.  

 См. дополнительные сведения о стандарте [AAC](https://en.wikipedia.org/wiki/Advanced_Audio_Coding).  

### <a name="elements"></a>Элементы
| Имя | Тип | Описание |
| --- | --- | --- |
| **Профиль**<br/><br/> minOccurs="0 "<br/><br/> default="AACLC" |**xs:string** |Может принимать одно из последующих значений hello: **AACLC**, **HEAACV1**, или **HEAACV2**. |

### <a name="attributes"></a>Атрибуты
| Имя | Тип | Описание |
| --- | --- | --- |
| **Condition** |**xs:string** |tooforce hello кодировщика tooproduce актив, содержащий автоматической звуковой дорожки, когда входные данные не содержит звука, укажите значение «InsertSilenceIfNoAudio» hello.<br/><br/> По умолчанию при отправке входных toohello кодировщик, содержит только видео и без звука нажмите hello выходного актива будет содержать файлы, содержащие только видео данные. Некоторые проигрыватели не удается toohandle такого потока вывода. В этом сценарии можно использовать этот параметр tooforce hello кодировщика tooadd является выходом toohello автоматической звуковой дорожки. |

### <a name="groups"></a>Группы
| Справочные материалы | Описание |
| --- | --- |
| [AudioGroup](media-services-mes-schema.md#AudioGroup)<br/><br/> minOccurs="0" |См. описание [AudioGroup](media-services-mes-schema.md#AudioGroup) tooknow hello соответствующее количество каналов, частоту выборки и скорость потока, который может задаваться для каждого профиля. |

## <a name="AudioGroup"></a> AudioGroup
Сведения о какие значения допустимы для каждого профиля см. в следующей таблице «Сведения кодека аудио» hello.  

### <a name="elements"></a>Элементы
| Имя | Тип | Описание |
| --- | --- | --- |
| **Channels**<br/><br/> minOccurs="0" |**xs:int** |число кодированных аудиоканалов Hello. Hello ниже приведены допустимые значения: 1, 2, 5, 6, 8.<br/><br/> Значение по умолчанию: 2. |
| **SamplingRate**<br/><br/> minOccurs="0" |**xs:int** |Hello частоту выборки звука, указанного в Гц. |
| **Bitrate**<br/><br/> minOccurs="0" |**xs:int** |Hello скорость, использующаяся при использовании кодирования аудио hello в Кбит/с. |

### <a name="audio-codec-details"></a>Сведения об аудиокодеке
Аудиокодек|Сведения  
-----------------|---  
**AACLC**|1:<br/><br/> - 11 025 : 8 &lt;= скорость &lt; 16<br/><br/> - 12 000 : 8 &lt;= скорость &lt; 16<br/><br/> - 16 000 : 8 &lt;= скорость &lt;32<br/><br/>- 22 050 : 24 &lt;= скорость &lt; 32<br/><br/> - 24 000 : 24 &lt;= скорость &lt; 32<br/><br/> - 32 000 : 32 &lt;= скорость &lt; 192<br/><br/> - 44 100 : 56 &lt;= скорость &lt; 288<br/><br/> - 48 000 : 56 &lt;= скорость &lt;288<br/><br/> - 88 200 : 128 &lt;= скорость &lt; 288<br/><br/> - 96 000 : 128 &lt;= скорость &lt; 288<br/><br/> 2.<br/><br/> - 11 025 : 16 &lt;= скорость &lt; 24<br/><br/> - 12 000 : 16 &lt;= скорость &lt; 24<br/><br/> - 16 000 : 16 &lt;= скорость &lt; 40<br/><br/> - 22 050 : 32 &lt;= скорость &lt; 40<br/><br/> - 24 000 : 32 &lt;= скорость &lt; 40<br/><br/> - 32 000 : 40 &lt;= скорость &lt; 384<br/><br/> - 44 100 : 96 &lt;= скорость &lt; 576<br/><br/> - 48 000 : 96 &lt;= скорость &lt; 576<br/><br/> - 88 200 : 256 &lt;= скорость &lt; 576<br/><br/> - 96 000 : 256 &lt;= скорость &lt; 576<br/><br/> 5/6:<br/><br/> - 32 000 : 160 &lt;= скорость &lt; 896<br/><br/> - 44 100 : 240 &lt;= скорость &lt; 1024<br/><br/> - 48 000 : 240 &lt;= скорость &lt; 1024<br/><br/> - 88 200 : 640 &lt;= скорость &lt; 1024<br/><br/> - 96 000 : 640 &lt;= скорость &lt; 1024<br/><br/> 8:<br/><br/> - 32 000 : 224 &lt;= скорость &lt; 1024<br/><br/> - 44 100 : 384 &lt;= скорость &lt; 1024<br/><br/> - 48 000 : 384 &lt;= скорость &lt; 1024<br/><br/> - 88 200 : 896 &lt;= скорость &lt; 1024<br/><br/> - 96 000 : 896 &lt;= скорость &lt; 1024  
**HEAACV1**|1:<br/><br/> - 22 050 : скорость = 8<br/><br/> - 24 000 : 8 &lt;= скорость &lt; 10<br/><br/> - 32 000 : 12 &lt;= скорость &lt; 64<br/><br/> - 44 100 : 20 &lt;= скорость &lt; 64<br/><br/> - 48 000 : 20 &lt;= скорость &lt; 64<br/><br/> - 88 200 : скорость = 64<br/><br/> 2.<br/><br/> - 32 000 : 16 &lt;= скорость &lt;= 128<br/><br/> - 44 100 : 16 &lt;= скорость &lt;= 128<br/><br/> - 48 000 : 16 &lt;= скорость &lt;= 128<br/><br/> - 88 200 : 96 &lt;= скорость &lt;= 128<br/><br/> - 96 000 : 96 &lt;= скорость &lt;= 128<br/><br/> 5/6:<br/><br/> - 32 000 : 64 &lt;= скорость &lt;= 320<br/><br/> - 44 100 : 64 &lt;= скорость &lt;= 320<br/><br/> - 48 000 : 64 &lt;= скорость &lt;= 320<br/><br/> - 88 200 : 256 &lt;= скорость &lt;= 320<br/><br/> - 96 000 : 256 &lt;= скорость &lt;= 320<br/><br/> 8:<br/><br/> - 32 000 : 96 &lt;= скорость &lt;= 448<br/><br/> - 44 100 : 96 &lt;= скорость &lt;= 448<br/><br/> - 48 000 : 96 &lt;= скорость &lt;= 448<br/><br/> - 88 200 : 384 &lt;= скорость &lt;= 448<br/><br/> - 96 000 : 384 &lt;= скорость &lt;= 448  
**HEAACV2**|2.<br/><br/> - 22 050 : 8 &lt;= скорость &lt;= 10<br/><br/> - 24 000 : 8 &lt;= скорость &lt; 10<br/><br/> - 32 000 : 12 &lt;= скорость &lt; 64<br/><br/> - 44 100 : 20 &lt;= скорость &lt; 64<br/><br/> - 48 000 : 20 &lt;= скорость &lt; 64<br/><br/> - 88 200 : 64 &lt;= скорость &lt;= 64  
  

## <a name="Clip"></a> Клип
### <a name="attributes"></a>Атрибуты
| Имя | Тип | Описание |
| --- | --- | --- |
| **StartTime** |**xs:duration** |Указывает время начала hello презентации. Hello значение StartTime должно toomatch hello абсолютный отметки времени hello входное видео. Например, если hello первый кадр hello входное видео имеет отметку времени, 12:00:10.000, то время начала должно быть по крайней мере 12:00:10.000 или выше. |
| **Duration** |**xs:duration** |Задает длительность hello представления (например, внешний вид наложение видео hello). |

## <a name="Output"></a> Выходные данные
### <a name="attributes"></a>Атрибуты
| Имя | Тип | Описание |
| --- | --- | --- |
| **FileName** |**xs:string** |Имя Hello hello выходного файла.<br/><br/> Можно использовать макросы, описанные в hello следующие имена таблиц toobuild hello выходного файла. Например:<br/><br/> **"Outputs": [      {       "FileName": "{Basename}*{Resolution}*{Bitrate}.mp4",       "Format": {         "Type": "MP4Format"       }     }   ]** |

### <a name="macros"></a>Макросы
| Макрос | Описание |
| --- | --- |
| **{Basename}** |При выполнении кодирования VoD hello {базовое имя} hello первые 32 символа свойство AssetFile.Name hello hello первичного файла в hello входного актива.<br/><br/> Если входной актив hello динамического архива, затем hello {базовое имя} является производным от атрибутов trackName hello в манифесте сервера hello. При отправке задания subclip с помощью hello TopBitrate, как в: «< VideoStream\>TopBitrate < / VideoStream\>» и hello выходной файл будет содержать видео, а затем hello {базовое имя} hello первые 32 символа trackName hello объекта hello слой видео с наивысшим битрейтом hello.<br/><br/> Вместо этого при подтверждении subclip задания, используя входной битрейтах hello, такие как «< VideoStream\>* < / VideoStream\>» и hello выходной файл будет содержать видео, а затем {базовое имя} — hello первые 32 символа trackName hello объекта Hello соответствующего слоя видео. |
| **{Codec}** |Сопоставляет слишком «H264» для видео и «AAC» для аудио. |
| **{Bitrate}** |Hello целевой скорость видео hello выходной файл будет содержать видео и аудио или скорость аудио целевой Если hello выходной файл содержит только звук. используется значение Hello — bitrate hello Кбит/с. |
| **{Channel}** |Счетчик аудио каналов, если файл hello содержит аудио. |
| **{Width}** |Ширина видео в пикселях в hello выходной файл, если файл hello содержит видео hello. |
| **{Height}** |Высота hello видео в пикселях в hello выходной файл, если файл hello содержит видео. |
| **{Extension}** |Наследует от hello свойство «Тип» для hello выходного файла. Имя выходного файла Hello будет иметь расширение, которое является одним из: «mp4», «служб терминалов», «jpg», «png» или «bmp». |
| **{Index}** |Обязателен для эскиза. Должен быть представлен только один раз. |

## <a name="Video"></a> Видео (сложный тип, который наследуется из кодека)
### <a name="attributes"></a>Атрибуты
| Имя | Тип | Описание |
| --- | --- | --- |
| **Начало** |**xs:string** | |
| **Step** |**xs:string** | |
| **Range** |**xs:string** | |
| **PreserveResolutionAfterRotation** |**xs:boolean** |Подробное описание см. в разделе hello в следующем разделе: [PreserveResolutionAfterRotation](media-services-mes-schema.md#PreserveResolutionAfterRotation) |

### <a name="PreserveResolutionAfterRotation"></a> PreserveResolutionAfterRotation
Рекомендуется флаг PreserveResolutionAfterRotation toouse hello в сочетании со значениями разрешения, выраженное в процентах (Ширина = Высота «100%» = «100%»).  

По умолчанию hello кодировать параметры разрешения (ширину, высоту) в hello, нацеленных на видео с поворот 0 градусов предустановок Media Encoder стандартных (MES). Например, если входной видео 1280 x 720 с нуля поворот градусов, затем стили по умолчанию hello обеспечить hello выходные данные hello одинакового разрешения. См. рисунок ниже.  

![MESRoation1](./media/media-services-shemas/media-services-mes-roation1.png) 

Тем не менее это означает, что если входное видео hello захваченное ненулевое значение поворота (например) смартфоне или планшете удерживаются по вертикали), а затем MES по умолчанию будет применяться hello кодирования разрешение ввода видео toohello параметров (ширина, высота) и затем компенсировать hello поворота. Например см. приведенный Далее рисунок hello. Hello Предустановка используются параметры ширины = высота «100%» = «100%», которая интерпретирует MES как требующее hello вывода toobe 1280 пикселей и высотой 720 пикселей. После смены hello видео, затем уменьшается toofit рисунок hello в этом окне начальные toopillar полях областей на hello влево и вправо.  

![MESRoation2](./media/media-services-shemas/media-services-mes-roation2.png) 

Если hello выше не hello требуемого поведения, то чтобы использовать флаг PreserveResolutionAfterRotation hello и задать для него слишком «true» (по умолчанию — «false»). Поэтому если вашей предустановки имеет ширину = «100%», высота = «100%» и задайте слишком «true», входное видео, который находится в 1280 пикселей в ширину и 720 пикселей с поворот на 90 градусов вывод с нуля поворот градусов, но 720 пикселей 1280 PreserveResolutionAfterRotation пикселей в высоту. См. приведенный Далее рисунок hello.  

![MESRoation3](./media/media-services-shemas/media-services-mes-roation3.png) 

## <a name="FormatGroup"></a> FormatGroup (группа)
### <a name="elements"></a>Элементы
| Имя | Тип | Описание |
| --- | --- | --- |
| **BmpFormat** |**BmpFormat** | |
| **PngFormat** |**PngFormat** | |
| **JpgFormat** |**JpgFormat** | |

## <a name="BmpLayer"></a> BmpLayer
### <a name="element"></a>Элемент
| Имя | Тип | Описание |
| --- | --- | --- |
| **Width**<br/><br/> minOccurs="0" |**xs:int** | |
| **Height**<br/><br/> minOccurs="0" |**xs:int** | |

### <a name="attributes"></a>Атрибуты
| Имя | Тип | Описание |
| --- | --- | --- |
| **Condition** |**xs:string** | |

## <a name="PngLayer"></a> PngLayer
### <a name="element"></a>Элемент
| Имя | Тип | Описание |
| --- | --- | --- |
| **Width**<br/><br/> minOccurs="0" |**xs:int** | |
| **Height**<br/><br/> minOccurs="0" |**xs:int** | |

### <a name="attributes"></a>Атрибуты
| Имя | Тип | Описание |
| --- | --- | --- |
| **Condition** |**xs:string** | |

## <a name="JpgLayer"></a> JpgLayer
### <a name="element"></a>Элемент
| Имя | Тип | Описание |
| --- | --- | --- |
| **Width**<br/><br/> minOccurs="0" |**xs:int** | |
| **Height**<br/><br/> minOccurs="0" |**xs:int** | |
| **Quality**<br/><br/> minOccurs="0" |**xs:int** |Допустимые значения: 1–100 (от худшего качества до наилучшего) |

### <a name="attributes"></a>Атрибуты
| Имя | Тип | Описание |
| --- | --- | --- |
| **Condition** |**xs:string** | |

## <a name="PngLayers"></a> PngLayers
### <a name="elements"></a>Элементы
| Имя | Тип | Описание |
| --- | --- | --- |
| **PngLayer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[PngLayer](media-services-mes-schema.md#PngLayer) | |

## <a name="BmpLayers"></a> BmpLayers
### <a name="elements"></a>Элементы
| Имя | Тип | Описание |
| --- | --- | --- |
| **BmpLayer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[BmpLayer](media-services-mes-schema.md#BmpLayer) | |

## <a name="JpgLayers"></a> JpgLayers
### <a name="elements"></a>Элементы
| Имя | Тип | Описание |
| --- | --- | --- |
| **JpgLayer**<br/><br/> minOccurs="0" maxOccurs="unbounded" |[JpgLayer](media-services-mes-schema.md#JpgLayer) | |

## <a name="BmpImage"></a> BmpImage (сложный тип, который наследуется из видео)
### <a name="elements"></a>Элементы
| Имя | Тип | Описание |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs="0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Уровни PNG |

## <a name="JpgImage"></a> JpgImage (сложный тип, который наследуется из видео)
### <a name="elements"></a>Элементы
| Имя | Тип | Описание |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs="0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Уровни PNG |

## <a name="PngImage"></a> PngImage (сложный тип, который наследуется из видео)
### <a name="elements"></a>Элементы
| Имя | Тип | Описание |
| --- | --- | --- |
| **PngLayers**<br/><br/> minOccurs="0" |[PngLayers](media-services-mes-schema.md#PngLayers) |Уровни PNG |

## <a name="examples"></a>Примеры
Примеры предустановок XML, созданных на основе этой схемы, см. в документации по [предустановкам задач для MES (Media Encoder Standard)](media-services-mes-presets-overview.md).

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

