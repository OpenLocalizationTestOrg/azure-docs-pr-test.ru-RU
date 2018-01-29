---
title: "Схема выходных метаданных служб мультимедиа Azure | Документация Майкрософт"
description: "Эта статья содержит обзор схемы выходных метаданных служб мультимедиа Azure."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 1ed84c88-eea5-4a24-9c4f-f2428157d08a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: c8792535eeeb71e7233c42bd9ea2a446a1c4d43c
ms.sourcegitcommit: 9a8b9a24d67ba7b779fa34e67d7f2b45c941785e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/08/2018
---
# <a name="output-metadata"></a>Выходные метаданные
## <a name="overview"></a>Обзор
Задание кодирования связано с входным ресурсом-контейнером (или ресурсами-контейнерами), в котором нужно выполнить эти задачи. Например, преобразуйте MP4-файл в набор мультискоростных MP4-файлов в формате H.264. Создайте эскиз и наложения. После выполнения задачи создается выходной ресурс-контейнер.  Он содержит видео- и аудиофайлы, эскизы и т. д. Выходной актив также содержит файл с метаданными выходного актива. Имя XML-файла метаданных имеет следующий формат: &lt;имя_исходного_файла&gt;_manifest.xml (например, BigBuckBunny_manifest.xml).  

Если вы хотите просмотреть файл метаданных, создайте указатель **SAS** и скачайте файл на локальный компьютер.  

В этой статье рассматриваются элементы и типы XML-схемы, на основе которой создаются выходные метаданные (&lt;имя_исходного_файла&gt;_metadata.xml). Сведения о файле, который содержит метаданные входного контейнера-ресурса, см. в статье [Input Metadata](media-services-input-metadata-schema.md) (Входные метаданные).  

> [!NOTE]
> В конце этой статьи вы найдете код полной схемы и пример XML-файла.  
>
>

## <a name="AssetFiles "></a> Корневой элемент AssetFiles
Коллекция записей AssetFile для задания кодирования.  

### <a name="child-elements"></a>Дочерние элементы
| ИМЯ | ОПИСАНИЕ |
| --- | --- |
| **AssetFile**<br/><br/> minOccurs="0" maxOccurs="1" |[Элемент AssetFile](media-services-output-metadata-schema.md), который является частью коллекции AssetFiles. |

## <a name="AssetFile "></a> Элемент AssetFile
Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).  

### <a name="attributes"></a>Атрибуты
| ИМЯ | type | ОПИСАНИЕ |
| --- | --- | --- |
| **Имя**<br/><br/> Обязательное значение |**xs:string** |Имя файла ресурса мультимедиа. |
| **Размер**<br/><br/> minInclusive ="0"<br/><br/> Обязательное значение |**xs:long** |Размер файла ресурса-контейнера в байтах. |
| **Duration**<br/><br/> Обязательное значение |**xs:duration** |Длительность воспроизведения содержимого. |

### <a name="child-elements"></a>Дочерние элементы
| ИМЯ | ОПИСАНИЕ |
| --- | --- |
| **Источники** |Коллекция входных и исходных файлов мультимедиа, которая обрабатывалась для создания AssetFile. Дополнительные сведения см. в разделе [Элемент Source](media-services-output-metadata-schema.md). |
| **VideoTracks**<br/><br/> minOccurs="0" maxOccurs="1" |Каждый физический файл ресурса может содержать ноль или более видеодорожек, чередуемых в соответствующем формате ресурса-контейнера. Дополнительные сведения см. в разделе [Элемент VideoTracks](media-services-output-metadata-schema.md). |
| **AudioTracks**<br/><br/> minOccurs="0" maxOccurs="1" |Каждый физический файл ресурса-контейнера может содержать ноль или более звуковых дорожек, чередуемых в соответствующем формате ресурса-контейнера. Это коллекция всех звуковых дорожек. Дополнительные сведения см. в разделе [Элемент AudioTracks](media-services-output-metadata-schema.md). |

## <a name="Sources "></a> Элемент Sources
Коллекция входных и исходных файлов мультимедиа, которая обрабатывалась для создания AssetFile.  

Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).  

### <a name="child-elements"></a>Дочерние элементы
| ИМЯ | ОПИСАНИЕ |
| --- | --- |
| **Источник**<br/><br/> minOccurs="1" maxOccurs="unbounded" |Входной или исходный файл, используемый при создании этого ресурса. Дополнительные сведения см. в разделе [Элемент Source](media-services-output-metadata-schema.md). |

## <a name="Source "></a> Элемент Source
Входной или исходный файл, используемый при создании этого ресурса.  

Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).  

### <a name="attributes"></a>Атрибуты
| ИМЯ | type | ОПИСАНИЕ |
| --- | --- | --- |
| **Имя**<br/><br/> Обязательное значение |**xs:string** |Имя входного исходного файла. |

## <a name="VideoTracks "></a> Элемент VideoTracks
Каждый физический файл ресурса может содержать ноль или более видеодорожек, чередуемых в соответствующем формате ресурса-контейнера. Элемент **VideoTracks** — это коллекция всех видеодорожек.  

Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).  

### <a name="child-elements"></a>Дочерние элементы
| ИМЯ | ОПИСАНИЕ |
| --- | --- |
| **VideoTrack**<br/><br/> minOccurs="1" maxOccurs="unbounded" |Конкретная видеодорожка в родительском элементе AssetFile. Дополнительные сведения см. в разделе [Элемент VideoTrack](media-services-output-metadata-schema.md#VideoTrack). |

## <a name="VideoTrack"></a> Элемент VideoTrack
Конкретная видеодорожка в родительском элементе AssetFile.  

Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).  

### <a name="attributes"></a>Атрибуты
| ИМЯ | type | ОПИСАНИЕ |
| --- | --- | --- |
| **Id**<br/><br/> minInclusive ="0"<br/><br/> Обязательное значение |**xs:int** |Отсчитываемый от нуля индекс видеодорожки. **Примечание.** Этот **идентификатор** не обязательно является TrackID, как используемый в файле MP4. |
| **FourCC**<br/><br/> Обязательное значение |**xs:string** |Код FourCC видеокодека. |
| **Профиль** |**xs:string** |Профиль H264 (применим только для кодека H264). |
| **Level** |**xs:string** |Уровень H264 (применим только для кодека H264). |
| **Width**<br/><br/> minInclusive ="0"<br/><br/> Обязательное значение |**xs:int** |Ширина закодированного видео в пикселях. |
| **Height**<br/><br/> minInclusive ="0"<br/><br/> Обязательное значение |**xs:int** |Высота закодированного видео в пикселях. |
| **DisplayAspectRatioNumerator**<br/><br/> minInclusive ="0"<br/><br/> Обязательное значение |**xs:double** |Числитель пропорции отображения видео. |
| **DisplayAspectRatioDenominator**<br/><br/> minInclusive ="0"<br/><br/> Обязательное значение |**xs:double** |Знаменатель пропорции отображения видео. |
| **Framerate**<br/><br/> minInclusive ="0"<br/><br/> Обязательное значение |**xs:decimal** |Измеренная частота видеокадров в формате 3F. |
| **TargetFramerate**<br/><br/> minInclusive ="0"<br/><br/> Обязательное значение |**xs:decimal** |Предустановленная частота кадров целевого видео в формате 3F. |
| **Bitrate**<br/><br/> minInclusive ="0"<br/><br/> Обязательное значение |**xs:int** |Средняя скорость аудиопотока в килобитах в секунду, вычисленная на основе файла ресурса-контейнера. Подсчитываются только полезные данные элементарного потока, издержки на упаковку не включаются. |
| **TargetBitrate**<br/><br/> minInclusive ="0"<br/><br/> Обязательное значение |**xs:int** |Целевая средняя скорость для данной видеодорожки в килобитах в секунду, запрошенная на основе предустановки кодирования. |
| **MaxGOPBitrate**<br/><br/> minInclusive ="0" |**xs:int** |Максимальная средняя скорость группы изображений (GOP) для данной видеодорожки в килобитах в секунду. |

## <a name="AudioTracks "></a> Элемент AudioTracks
Каждый физический файл ресурса-контейнера может содержать ноль или более звуковых дорожек, чередуемых в соответствующем формате ресурса-контейнера. Элемент **AudioTracks** — это коллекция всех аудиодорожек.  

Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).  

### <a name="child-elements"></a>Дочерние элементы
| ИМЯ | ОПИСАНИЕ |
| --- | --- |
| **AudioTrack**<br/><br/> minOccurs="1" maxOccurs="unbounded" |Конкретная звуковая дорожка в родительском элементе AssetFile. Дополнительные сведения см. в разделе [Элемент AudioTrack](media-services-output-metadata-schema.md). |

## <a name="AudioTrack "></a> Элемент AudioTrack
Конкретная звуковая дорожка в родительском элементе AssetFile.  

Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).  

### <a name="attributes"></a>Атрибуты
| ИМЯ | type | ОПИСАНИЕ |
| --- | --- | --- |
| **Id**<br/><br/> minInclusive ="0"<br/><br/> Обязательное значение |**xs:int** |Отсчитываемый от нуля индекс звуковой дорожки. **Примечание.** MP4-файл необязательно должен содержать идентификатор дорожки. |
| **Codec** |**xs:string** |Строка кодека звуковой дорожки. |
| **EncoderVersion** |**xs:string** |Дополнительная строка версии кодировщика, требуемая для EAC3. |
| **Channels**<br/><br/> minInclusive ="0"<br/><br/> Обязательное значение |**xs:int** |Число аудиоканалов. |
| **SamplingRate**<br/><br/> minInclusive ="0"<br/><br/> Обязательное значение |**xs:int** |Частота аудиовыборки: выборок/с или Гц. |
| **Bitrate**<br/><br/> minInclusive ="0"<br/><br/> Обязательное значение |**xs:int** |Средняя скорость аудиопотока в битах в секунду, вычисленная на основе файла ресурса-контейнера. Подсчитываются только полезные данные элементарного потока, издержки на упаковку не включаются. |
| **BitsPerSample**<br/><br/> minInclusive ="0"<br/><br/> Обязательное значение |**xs:int** |Битов на выборку для формата wFormatTag. |

### <a name="child-elements"></a>Дочерние элементы
| ИМЯ | ОПИСАНИЕ |
| --- | --- |
| **LoudnessMeteringResultParameters**<br/><br/> minOccurs="0" maxOccurs="1" |Параметры результата измерения громкости. Дополнительные сведения см. в разделе [Элемент LoudnessMeteringResultParameter](media-services-output-metadata-schema.md). |

## <a name="LoudnessMeteringResultParameters "></a> Элемент LoudnessMeteringResultParameters
Параметры результата измерения громкости.  

Пример XML-файла см. в [соответствующем разделе](media-services-output-metadata-schema.md#xml).  

### <a name="attributes"></a>Атрибуты
| ИМЯ | type | ОПИСАНИЕ |
| --- | --- | --- |
| **DPLMVersionInformation** |**xs:string** |Версия комплекта разработчика **Dolby** Professional Loudness Metering (DPLM). |
| **DialogNormalization**<br/><br/> minInclusive="-31" maxInclusive="-1"<br/><br/> Обязательное значение |**xs:int** |DialogNormalization, созданный с помощью DPLM, необходим при установке LoudnessMetering. |
| **IntegratedLoudness**<br/><br/> minInclusive="-70" maxInclusive="10"<br/><br/> Обязательное значение |**xs: float** |Интегрированная громкость |
| **IntegratedLoudnessUnit**<br/><br/> Обязательное значение |**xs:string** |Единица измерения интегрированной громкости. |
| **IntegratedLoudnessGatingMethod**<br/><br/> Обязательное значение |**xs:string** |Идентификатор стробирования |
| **IntegratedLoudnessSpeechPercentage**<br/><br/> minInclusive ="0" maxInclusive="100" |**xs: float** |Речевое содержимое в программе в процентах. |
| **SamplePeak**<br/><br/> Обязательное значение |**xs: float** |Пиковое абсолютное опорное значение в канале после сброса или последней очистки.  Единицы измерения — dBFS. |
| **SamplePeakUnit**<br/><br/> fixed="dBFS"<br/><br/> Обязательное значение |**xs:anySimpleType** |Единица измерения пикового опорного значения. |
| **TruePeak**<br/><br/> Обязательное значение |**xs: float** |Наибольшее абсолютное пиковое значение в канале, соответствующее ITU-R BS.1770-2, после сброса или последней очистки. Единицы измерения — dBTP. |
| **TruePeakUnit**<br/><br/> fixed="dBTP"<br/><br/> Обязательное значение |**xs:anySimpleType** |Единица измерения наибольшего абсолютного опорного значения. |

## <a name="schema-code"></a>Код схемы
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.2"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata"  
               elementFormDefault="qualified">  
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
                  <xs:element name="Sources">  
                    <xs:annotation>  
                      <xs:documentation>Collection of input/source media files, that was processed in order to produce this AssetFile</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Source" minOccurs="1" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>An input/source file used when generating this asset</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:attribute name="Name" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>input source file name</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is the collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>A specific video track in the parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
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
                            <xs:attribute name="FourCC" type="xs:string" use="required">  
                              <xs:annotation>  
                                <xs:documentation>video codec FourCC code</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Profile" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 profile (only appliable for H264 codec)</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="Level" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>H264 level (only appliable for H264 codec)</xs:documentation>  
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
                            <xs:attribute name="Framerate" use="required">  
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
                            <xs:attribute name="TargetFramerate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>preset target video frame rate in .3f format</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:decimal">  
                                  <xs:minInclusive value="0"/>  
                                  <xs:fractionDigits value="3"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average video bit rate in kilobits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="TargetBitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>target average bitrate for this video track, as requested via the encoding preset, in kilobits per second</xs:documentation>  
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
                          </xs:complexType>  
                        </xs:element>  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is the collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" maxOccurs="unbounded">  
                          <xs:annotation>  
                            <xs:documentation>a specific audio track in the parent AssetFile</xs:documentation>  
                          </xs:annotation>  
                          <xs:complexType>  
                            <xs:sequence>  
                              <xs:element name="LoudnessMeteringResultParameters" minOccurs="0" maxOccurs="1">  
                                <xs:annotation>  
                                  <xs:documentation>Loudness Metering Result Parameters</xs:documentation>  
                                </xs:annotation>  
                                <xs:complexType>  
                                  <xs:attribute name="DPLMVersionInformation" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Dolby Professional Loudness Metering Development Kit Version</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="DialogNormalization" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation> DialogNormalization generated through DPLM, required when LoudnessMetering is set</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:int">  
                                        <xs:minInclusive value="-31"/>  
                                        <xs:maxInclusive value="-1"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudness" use="required">  
                                    <xs:annotation>  
                                      <xs:documentation>Integrated loudness</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="-70"/>  
                                        <xs:maxInclusive value="10"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessUnit" use="required" type="xs:string">  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessGatingMethod" use="required" type="xs:string">  
                                    <xs:annotation>  
                                      <xs:documentation>Gating identifier</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="IntegratedLoudnessSpeechPercentage">  
                                    <xs:annotation>  
                                      <xs:documentation>Speech content over the program, as a percentage.</xs:documentation>  
                                    </xs:annotation>  
                                    <xs:simpleType>  
                                      <xs:restriction base="xs:float">  
                                        <xs:minInclusive value="0"/>  
                                        <xs:maxInclusive value="100"/>  
                                      </xs:restriction>  
                                    </xs:simpleType>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Peak absolute sample value, since reset or since it was last cleared, per channel.  Units are dBFS.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="SamplePeakUnit" use="required" fixed="dBFS">  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeak" use="required" type="xs:float">  
                                    <xs:annotation>  
                                      <xs:documentation>Maximum True Peak value, as per ITU-R BS.1770-2, since reset or since it was last cleared, per channel.  Units are dBTP.</xs:documentation>  
                                    </xs:annotation>  
                                  </xs:attribute>  
                                  <xs:attribute name="TruePeakUnit" use="required" fixed="dBTP">  
                                  </xs:attribute>  
                                </xs:complexType>  
                              </xs:element>  
                            </xs:sequence>  
                            <xs:attribute name="Id" use="required">  
                              <xs:annotation>  
                                <xs:documentation>zero-based index of this audio track. Note: this is not necessarily the TrackID as used in an MP4 file</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="Codec" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>audio track codec string</xs:documentation>  
                              </xs:annotation>  
                            </xs:attribute>  
                            <xs:attribute name="EncoderVersion" type="xs:string">  
                              <xs:annotation>  
                                <xs:documentation>optional encoder version string, required for EAC3</xs:documentation>  
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
                            <xs:attribute name="Bitrate" use="required">  
                              <xs:annotation>  
                                <xs:documentation>average audio bit rate in bits per second, as calculated from the AssetFile. Counts only the elementary stream payload, and does not include the packaging overhead</xs:documentation>  
                              </xs:annotation>  
                              <xs:simpleType>  
                                <xs:restriction base="xs:int">  
                                  <xs:minInclusive value="0"/>  
                                </xs:restriction>  
                              </xs:simpleType>  
                            </xs:attribute>  
                            <xs:attribute name="BitsPerSample" use="required">  
                              <xs:annotation>  
                                <xs:documentation>Bits per sample for the wFormatTag format type</xs:documentation>  
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
                <xs:attribute name="Duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:duration"/>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  



## <a name="xml"></a> Пример XML-файла

Ниже приведен пример XML-файла выходных метаданных.  

    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
                xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2013/05/mediaencoder/metadata">  
      <AssetFile Name="BigBuckBunny_H264_3400kbps_AAC_und_ch2_96kbps.mp4" Size="4646283" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.2" Width="1280" Height="720" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="4250" TargetBitrate="3400" MaxGOPBitrate="5514"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_2250kbps_AAC_und_ch2_96kbps.mp4" Size="3166728" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="2846" TargetBitrate="2250" MaxGOPBitrate="3630"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1500kbps_AAC_und_ch2_96kbps.mp4" Size="2205095" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.1" Width="960" Height="540" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1932" TargetBitrate="1500" MaxGOPBitrate="2513"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_1000kbps_AAC_und_ch2_96kbps.mp4" Size="1508567" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="1271" TargetBitrate="1000" MaxGOPBitrate="1527"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4" Size="1057155" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="3.0" Width="640" Height="360" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="843" TargetBitrate="650" MaxGOPBitrate="1086"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_H264_400kbps_AAC_und_ch2_96kbps.mp4" Size="699262" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <VideoTracks>  
          <VideoTrack Id="0" FourCC="AVC1" Profile="Main" Level="1.3" Width="320" Height="180" DisplayAspectRatioNumerator="16" DisplayAspectRatioDenominator="9" Framerate="23.974" TargetFramerate="23.974" Bitrate="503" TargetBitrate="400" MaxGOPBitrate="661"/>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_96kbps.mp4" Size="166780" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="93" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
      <AssetFile Name="BigBuckBunny_AAC_und_ch2_56kbps.mp4" Size="124576" Duration="PT8.4288444S">  
        <Sources>  
          <Source Name="BigBuckBunny.mp4"/>  
        </Sources>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="AacLc" Channels="2" SamplingRate="44100" Bitrate="53" BitsPerSample="16"/>  
        </AudioTracks>  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a>Дополнительная информация
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
