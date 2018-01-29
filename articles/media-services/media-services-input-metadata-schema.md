---
title: "Схема входных метаданных служб мультимедиа Azure | Документация Майкрософт"
description: "Эта статья содержит обзор схемы входных метаданных служб мультимедиа Azure."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d72848e2-4b65-4c84-94bc-e2a90a6e7f47
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 85a3662fec08cfc081095ef252842a30fde7dd27
ms.sourcegitcommit: 9a8b9a24d67ba7b779fa34e67d7f2b45c941785e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2018
---
# <a name="input-metadata"></a>Входные метаданные
Задание кодирования связано с входным ресурсом-контейнером (или ресурсами-контейнерами), в котором нужно выполнить эти задачи.  После выполнения задачи создается выходной ресурс-контейнер.  Выходной ресурс-контейнер содержит видео- и аудиофайлы, эскизы, манифест и т. д. Выходной актив также содержит файл с метаданными входного актива. Имя XML-файла метаданных имеет следующий формат: &lt;ИД_ресурса-контейнера&gt;_metadata.xml (например, 41114ad3-eb5e-4c57-8d92-5354e2b7d4a4_metadata.xml), где &lt;ИД_ресурса-контейнера&gt; — это значение AssetId для входного ресурса-контейнера.  

Если вы хотите просмотреть файл метаданных, создайте указатель **SAS** и скачайте файл на локальный компьютер. Пример создания указателя SAS и скачивания файла см. в статье [Приступая к работе с доставкой содержимого по запросу с помощью пакета SDK для .NET](media-services-dotnet-get-started.md).  

В этой статье рассматриваются элементы и типы XML-схемы, на основе которой создаются входные метаданные (&lt;ид_ресурса&gt;_metadata.xml).  Сведения о файле, который содержит метаданные выходного контейнера-ресурса, см. в статье [Output Metadata](media-services-output-metadata-schema.md) (Выходные метаданные).  

> [!NOTE]
> В конце этой статьи вы найдете [код схемы](media-services-input-metadata-schema.md#code) и [пример XML-файла](media-services-input-metadata-schema.md#xml).  
> 
> 

## <a name="AssetFiles"></a> Элемент AssetFiles (корневой элемент)
Содержит коллекцию [элементов AssetFile](media-services-input-metadata-schema.md#AssetFile) для задания кодирования.  

Пример XML-файла см. в разделе [Пример XML-файла](media-services-input-metadata-schema.md#xml) в конце статьи.  

| ИМЯ | ОПИСАНИЕ |
| --- | --- |
| **AssetFile**<br /><br /> minOccurs="1" maxOccurs="unbounded" |Один дочерний элемент. Дополнительные сведения см. в разделе [Элемент AssetFile](media-services-input-metadata-schema.md#AssetFile). |

## <a name="AssetFile"></a> Элемент AssetFile
 Содержит атрибуты и элементы, описывающие файл ресурса-контейнера.  

 Пример XML-файла см. в разделе [Пример XML-файла](media-services-input-metadata-schema.md#xml) в конце статьи.  

### <a name="attributes"></a>Атрибуты
| ИМЯ | type | ОПИСАНИЕ |
| --- | --- | --- |
| **Имя**<br /><br /> Обязательное значение |**xs:string** |Имя файла ресурса-контейнера. |
| **Размер**<br /><br /> Обязательное значение |**xs:long** |Размер файла ресурса-контейнера в байтах. |
| **Duration**<br /><br /> Обязательное значение |**xs:duration** |Длительность воспроизведения содержимого. Пример: Duration="PT25M37.757S". |
| **NumberOfStreams**<br /><br /> Обязательное значение |**xs:int** |Количество потоков в файле ресурса-контейнера. |
| **FormatNames**<br /><br /> Обязательное значение |**xs: string** |Имена форматов. |
| **FormatVerboseNames**<br /><br /> Обязательное значение |**xs: string** |Подробные имена форматов. |
| **StartTime** |**xs:duration** |Время начала содержимого. Пример: StartTime="PT2.669S". |
| **OverallBitRate** |**xs: int** |Средняя скорость файла ресурса-контейнера (Кбит/с). |

> [!NOTE]
> Следующие четыре дочерних элемента должны появляться последовательно.  
> 
> 

### <a name="child-elements"></a>Дочерние элементы
| ИМЯ | type | ОПИСАНИЕ |
| --- | --- | --- |
| **Programs**<br /><br /> minOccurs="0" | |Коллекция всех [элементов Programs](media-services-input-metadata-schema.md#Programs), если файл ресурса-контейнера имеет формат MPEG-TS. |
| **VideoTracks**<br /><br /> minOccurs="0" | |Каждый физический файл ресурса может содержать ноль или более видеодорожек, чередуемых в соответствующем формате ресурса. Этот элемент содержит коллекцию всех [элементов VideoTracks](media-services-input-metadata-schema.md#VideoTracks), которые являются частью файла ресурса. |
| **AudioTracks**<br /><br /> minOccurs="0" | |Каждый физический файл ресурса-контейнера может содержать ноль или более звуковых дорожек, чередуемых в соответствующем формате ресурса-контейнера. Этот элемент содержит коллекцию всех [элементов AudioTracks](media-services-input-metadata-schema.md#AudioTracks), которые являются частью файла ресурса. |
| **Metadata**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[MetadataType](media-services-input-metadata-schema.md#MetadataType) |Метаданные файла ресурса-контейнера, представленные в виде строки "ключ —значение". Например: <br /><br /> **&lt;Metadata key="language" value="eng" /&gt;** |

## <a name="TrackType"></a> TrackType
Пример XML-файла см. в разделе [Пример XML-файла](media-services-input-metadata-schema.md#xml) в конце статьи.  

### <a name="attributes"></a>Атрибуты
| ИМЯ | type | ОПИСАНИЕ |
| --- | --- | --- |
| **Id**<br /><br /> Обязательное значение |**xs:int** |Отсчитываемый от нуля индекс аудио- или видеодорожки.<br /><br /> MP4-файл не обязательно должен содержать идентификатор дорожки. |
| **Codec** |**xs:string** |Строка кодека видеодорожки. |
| **CodecLongName** |**xs: string** |Полное имя кодека звуковой или видеодорожки. |
| **TimeBase**<br /><br /> Обязательное значение |**xs:string** |Базовый счетчик времени. Пример: TimeBase="1/48000" |
| **NumberOfFrames** |**xs:int** |Количество кадров (для видеодорожек). |
| **StartTime** |**xs: duration** |Время начала дорожки. Пример: StartTime="PT2.669S" |
| **Duration** |**xs:duration** |Продолжительность дорожки. Пример: Duration="PTSampleFormat M37.757S". |

> [!NOTE]
> Следующие два дочерних элемента должны появляться последовательно.  
> 
> 

### <a name="child-elements"></a>Дочерние элементы
| ИМЯ | type | ОПИСАНИЕ |
| --- | --- | --- |
| **Disposition**<br /><br /> minOccurs="0" maxOccurs="1" |[StreamDispositionType](media-services-input-metadata-schema.md#StreamDispositionType) |Содержит сведения о презентации (например, указывает, предназначена ли конкретная звуковая дорожка для людей с нарушениями зрения). |
| **Metadata**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[MetadataType](media-services-input-metadata-schema.md#MetadataType) |Общие строки "ключ —значение", которые можно использовать для хранения различных сведений. Например, key="language" и value="eng". |

## <a name="AudioTrackType"></a> AudioTrackType (наследуется из TrackType)
 **AudioTrackType** — это глобальный сложный тип, который наследуется из [TrackType](media-services-input-metadata-schema.md#TrackType).  

 Этот тип представляет конкретную звуковую дорожку в файле ресурса-контейнера.  

 Пример XML-файла см. в разделе [Пример XML-файла](media-services-input-metadata-schema.md#xml) в конце статьи.  

### <a name="attributes"></a>Атрибуты
| ИМЯ | type | ОПИСАНИЕ |
| --- | --- | --- |
| **SampleFormat** |**xs:string** |Формат выборки. |
| **ChannelLayout** |**xs: string** |Структура канала. |
| **Channels**<br /><br /> Обязательное значение |**xs:int** |Количество (0 или более) аудиоканалов. |
| **SamplingRate**<br /><br /> Обязательное значение |**xs:int** |Частота аудиовыборки: выборок/с или Гц. |
| **Bitrate** |**xs:int** |Средняя скорость аудиопотока в битах в секунду, вычисленная на основе файла ресурса-контейнера. Подсчитываются только полезные данные элементарного потока, издержки на упаковку не включаются. |
| **BitsPerSample** |**xs:int** |Битов на выборку для формата wFormatTag. |

## <a name="VideoTrackType"></a> VideoTrackType (наследуется из TrackType)
**VideoTrackType** — это глобальный сложный тип, который наследуется из [TrackType](media-services-input-metadata-schema.md#TrackType).  

Этот тип представляет конкретную видеодорожку в файле ресурса-контейнера.  

Пример XML-файла см. в разделе [Пример XML-файла](media-services-input-metadata-schema.md#xml) в конце статьи.  

### <a name="attributes"></a>Атрибуты
| ИМЯ | type | ОПИСАНИЕ |
| --- | --- | --- |
| **FourCC**<br /><br /> Обязательное значение |**xs:string** |Код FourCC видеокодека. |
| **Профиль** |**xs: string** |Профиль видеодорожки. |
| **Level** |**xs: string** |Уровень видеодорожки. |
| **PixelFormat** |**xs: string** |Формат пикселей видеодорожки. |
| **Width**<br /><br /> Обязательное значение |**xs:int** |Ширина закодированного видео в пикселях. |
| **Height**<br /><br /> Обязательное значение |**xs:int** |Высота закодированного видео в пикселях. |
| **DisplayAspectRatioNumerator**<br /><br /> Обязательное значение |**xs: double** |Числитель пропорции отображения видео. |
| **DisplayAspectRatioDenominator**<br /><br /> Обязательное значение |**xs:double** |Знаменатель пропорции отображения видео. |
| **DisplayAspectRatioDenominator**<br /><br /> Обязательное значение |**xs: double** |Числитель пропорции выборки видео. |
| **SampleAspectRatioNumerator** |**xs: double** |Числитель пропорции выборки видео. |
| **SampleAspectRatioNumerator** |**xs:double** |Знаменатель пропорции выборки видео. |
| **FrameRate**<br /><br /> Обязательное значение |**xs:decimal** |Измеренная частота видеокадров в формате 3F. |
| **Bitrate** |**xs:int** |Средняя скорость аудиопотока в килобитах в секунду, вычисленная на основе файла ресурса-контейнера. Подсчитываются только полезные данные элементарного потока, издержки на упаковку не включаются. |
| **MaxGOPBitrate** |**xs: int** |Максимальная средняя скорость группы изображений (GOP) для данной видеодорожки в килобитах в секунду. |
| **HasBFrames** |**xs:int** |Количество видеодорожек с кадрами B. |

## <a name="MetadataType"></a> MetadataType
**MetadataType** — глобальный сложный тип, описывающий метаданные файла ресурса-контейнера в виде строк "ключ —значение". Например, key="language" и value="eng".  

Пример XML-файла см. в разделе [Пример XML-файла](media-services-input-metadata-schema.md#xml) в конце статьи.  

### <a name="attributes"></a>Атрибуты
| ИМЯ | type | ОПИСАНИЕ |
| --- | --- | --- |
| **key**<br /><br /> Обязательное значение |**xs:string** |Ключ в паре "ключ — значение". |
| **значение**<br /><br /> Обязательное значение |**xs:string** |Значение в паре "ключ — значение". |

## <a name="ProgramType"></a> ProgramType
**ProgramType** — глобальный сложный тип, описывающий программу.  

### <a name="attributes"></a>Атрибуты
| ИМЯ | type | ОПИСАНИЕ |
| --- | --- | --- |
| **ProgramId**<br /><br /> Обязательное значение |**xs:int** |Идентификатор программы |
| **NumberOfPrograms**<br /><br /> Обязательное значение |**xs:int** |Количество программ. |
| **PmtPid**<br /><br /> Обязательное значение |**xs:int** |Таблицы сопоставления программ (PMT) содержат сведения о программах.  Дополнительные сведения см. в разделе [PMT](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT). |
| **PcrPid**<br /><br /> Обязательное значение |**xs: int** |Используется декодером. Дополнительные сведения см. в разделе [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR). |
| **StartPTS** |**xs: long** |Метка времени начала презентации. |
| **EndPTS** |**xs: long** |Метка времени окончания презентации. |

## <a name="StreamDispositionType"></a> StreamDispositionType
**StreamDispositionType** — глобальный сложный тип, описывающий поток.  

Пример XML-файла см. в разделе [Пример XML-файла](media-services-input-metadata-schema.md#xml) в конце статьи.  

### <a name="attributes"></a>Атрибуты
| ИМЯ | type | ОПИСАНИЕ |
| --- | --- | --- |
| **По умолчанию**<br /><br /> Обязательное значение |**xs: int** |Установите значение 1, чтобы указать, что это презентация по умолчанию. |
| **Dub**<br /><br /> Обязательное значение |**xs:int** |Установите значение 1, чтобы указать, что это дубликат презентации. |
| **Original**<br /><br /> Обязательное значение |**xs: int** |Установите значение 1, чтобы указать, что это оригинал презентации. |
| **Comment**<br /><br /> Обязательное значение |**xs:int** |Установите значение 1, чтобы указать, что эта дорожка содержит дикторский текст. |
| **Lyrics**<br /><br /> Обязательное значение |**xs:int** |Установите значение 1, чтобы указать, что эта дорожка содержит слова композиции. |
| **Karaoke**<br /><br /> Обязательное значение |**xs:int** |Установите значение 1, чтобы указать, что это караоке-дорожка (фонограмма без вокала). |
| **Forced**<br /><br /> Обязательное значение |**xs:int** |Установите значение 1, чтобы указать, что это принудительная презентация. |
| **HearingImpaired**<br /><br /> Обязательное значение |**xs:int** |Установите значение 1, чтобы указать, что эта дорожка предназначена для пользователей с нарушениями слуха. |
| **VisualImpaired**<br /><br /> Обязательное значение |**xs:int** |Установите значение 1, чтобы указать, что эта дорожка предназначена для пользователей с нарушениями зрения. |
| **CleanEffects**<br /><br /> Обязательное значение |**xs: int** |Установите значение 1, чтобы указать, что эта дорожка содержит чистые эффекты. |
| **AttachedPic**<br /><br /> Обязательное значение |**xs: int** |Установите значение 1, чтобы указать, что эта дорожка содержит изображения. |

## <a name="Programs"></a> Элемент Programs
Оболочечный элемент, содержащий несколько элементов **Program**.  

### <a name="child-elements"></a>Дочерние элементы
| ИМЯ | type | ОПИСАНИЕ |
| --- | --- | --- |
| **Program**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[ProgramType](media-services-input-metadata-schema.md#ProgramType) |Содержит сведения о программах в файле ресурса-контейнера (в формате MPEG-TS). |

## <a name="VideoTracks"></a> Элемент VideoTracks
 Оболочечный элемент, содержащий несколько элементов **VideoTrack**.  

 Пример XML-файла см. в разделе [Пример XML-файла](media-services-input-metadata-schema.md#xml) в конце статьи.  

### <a name="child-elements"></a>Дочерние элементы
| ИМЯ | type | ОПИСАНИЕ |
| --- | --- | --- |
| **VideoTrack**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[VideoTrackType (наследуется из TrackType)](media-services-input-metadata-schema.md#VideoTrackType) |Содержит сведения о видеодорожках в файле ресурса-контейнера. |

## <a name="AudioTracks"></a> Элемент AudioTracks
 Оболочечный элемент, содержащий несколько элементов **AudioTrack**.  

 Пример XML-файла см. в разделе [Пример XML-файла](media-services-input-metadata-schema.md#xml) в конце статьи.  

### <a name="elements"></a>элементы
| ИМЯ | type | ОПИСАНИЕ |
| --- | --- | --- |
| **AudioTrack**<br /><br /> minOccurs="0" maxOccurs="unbounded" |[AudioTrackType (наследуется из TrackType)](media-services-input-metadata-schema.md#AudioTrackType) |Содержит сведения о звуковых дорожках в файле ресурса-контейнера. |

## <a name="code"></a> Код схемы
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.0"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               elementFormDefault="qualified">  

      <xs:complexType name="MetadataType">  
        <xs:attribute name="key"   type="xs:string" use="required"/>  
        <xs:attribute name="value" type="xs:string" use="required"/>  
      </xs:complexType>  

      <xs:complexType name="ProgramType">  
        <xs:attribute name="ProgramId" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Program Id</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfPrograms" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Number of programs</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PmtPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pmt pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PcrPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pcr pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="StartPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>start pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="EndPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>end pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="StreamDispositionType">  
        <xs:attribute name="Default"          type="xs:int" use="required" />  
        <xs:attribute name="Dub"              type="xs:int" use="required" />  
        <xs:attribute name="Original"         type="xs:int" use="required" />  
        <xs:attribute name="Comment"          type="xs:int" use="required" />  
        <xs:attribute name="Lyrics"           type="xs:int" use="required" />  
        <xs:attribute name="Karaoke"          type="xs:int" use="required" />  
        <xs:attribute name="Forced"           type="xs:int" use="required" />  
        <xs:attribute name="HearingImpaired"  type="xs:int" use="required" />  
        <xs:attribute name="VisualImpaired"   type="xs:int" use="required" />  
        <xs:attribute name="CleanEffects"     type="xs:int" use="required" />  
        <xs:attribute name="AttachedPic"      type="xs:int" use="required" />  
      </xs:complexType>  

      <xs:complexType name="TrackType" abstract="true">  
        <xs:sequence>  
          <xs:element name="Disposition" type="StreamDispositionType" minOccurs="0" maxOccurs="1"/>  
          <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded"/>  
        </xs:sequence>  
        <xs:attribute name="Id" use="required">  
          <xs:annotation>  
            <xs:documentation>zero-based index of this video track. Note: this is not necessarily the TrackID as used in an MP4 file</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="Codec" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec string</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="CodecLongName" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec long name</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="TimeBase"  type="xs:string" use="required">  
          <xs:annotation>  
            <xs:documentation>Time base. Example: TimeBase="1/48000"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfFrames">  
          <xs:annotation>  
            <xs:documentation>number of frames</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="StartTime" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track start time. Example: StartTime="PT2.669S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="Duration" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track duration. Example: Duration="PT25M37.757S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="VideoTrackType">  
        <xs:annotation>  
          <xs:documentation>A specific video track in the parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="FourCC" type="xs:string" use="required">  
              <xs:annotation>  
                <xs:documentation>video codec FourCC code</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Profile" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>profile</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Level" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>level</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="PixelFormat" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>Video track's pixel format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Width" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video width in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Height" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video height in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioNumerator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioDenominator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioNumerator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioDenominator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="FrameRate" use="required">  
              <xs:annotation>  
                <xs:documentation>measured video frame rate in .3f format</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:decimal">  
                  <xs:minInclusive value="0"/>  
                  <xs:fractionDigits value="3"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average video bit rate in kilobits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="MaxGOPBitrate">  
              <xs:annotation>  
                <xs:documentation>Max GOP average bitrate for this video track, in kilobits per second</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="HasBFrames" type="xs:int">  
              <xs:annotation>  
                <xs:documentation>video track number of B frames</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:complexType name="AudioTrackType">  
        <xs:annotation>  
          <xs:documentation>a specific audio track in the parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="SampleFormat"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>sample format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="ChannelLayout"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>channel layout</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Channels" use="required">  
              <xs:annotation>  
                <xs:documentation>number of audio channels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SamplingRate" use="required">  
              <xs:annotation>  
                <xs:documentation>audio sampling rate in samples/sec or Hz</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average audio bit rate in bits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for the wFormatTag format type</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for the encoding job</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="AssetFile" minOccurs="1" maxOccurs="unbounded">  
              <xs:annotation>  
                <xs:documentation>asset file</xs:documentation>  
              </xs:annotation>  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="Programs" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>This is the collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is the collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is the collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" type="AudioTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded" />  
                </xs:sequence>  
                <xs:attribute name="Name" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>the media asset file name</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Size" use="required">  
                  <xs:annotation>  
                    <xs:documentation>size of file in bytes</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:long">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
                <xs:attribute name="Duration" type="xs:duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration. Example: Duration="PT25M37.757S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="NumberOfStreams" type="xs:int" use="required">  
                  <xs:annotation>  
                    <xs:documentation>number of streams in asset file</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatNames" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatVerboseName" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format verbose names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="StartTime" type="xs:duration">  
                  <xs:annotation>  
                    <xs:documentation>content start time. Example: StartTime="PT2.669S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="OverallBitRate">  
                  <xs:annotation>  
                    <xs:documentation>average bitrate of the asset file in kbps</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:int">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  


## <a name="xml"></a> Пример XML-файла
Ниже приведен пример файла входных метаданных.  

    <?xml version="1.0" encoding="utf-8"?>  
    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata">  
      <AssetFile Name="bear.mp4" Size="1973733" Duration="PT12.678S" NumberOfStreams="2" FormatNames="mov,mp4,m4a,3gp,3g2,mj2" FormatVerboseName="QuickTime / MOV" StartTime="PT0S" OverallBitRate="1245">  
        <VideoTracks>  
          <VideoTrack Id="1" Codec="h264" CodecLongName="H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10" TimeBase="1/29970" NumberOfFrames="375" StartTime="PT0.034S" Duration="PT12.645S" FourCC="avc1" Profile="High" Level="4.1" PixelFormat="yuv420p" Width="512" Height="384" DisplayAspectRatioNumerator="4" DisplayAspectRatioDenominator="3" SampleAspectRatioNumerator="1" SampleAspectRatioDenominator="1" FrameRate="29.656" Bitrate="1043" HasBFrames="1">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Video Media Handler" />  
          </VideoTrack>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="aac" CodecLongName="AAC (Advanced Audio Coding)" TimeBase="1/44100" NumberOfFrames="546" StartTime="PT0S" Duration="PT12.678S" SampleFormat="fltp" ChannelLayout="stereo" Channels="2" SamplingRate="44100" Bitrate="156" BitsPerSample="0">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Sound Media Handler" />  
          </AudioTrack>  
        </AudioTracks>  
        <Metadata key="major_brand" value="mp42" />  
        <Metadata key="minor_version" value="0" />  
        <Metadata key="compatible_brands" value="mp42mp41" />  
        <Metadata key="creation_time" value="2010-03-10 16:11:53" />  
        <Metadata key="comment" value="Courtesy of National Geographic.  Used by Permission." />  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a>Дополнительная информация
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

