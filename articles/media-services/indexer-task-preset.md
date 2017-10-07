---
title: "aaaTask предустановки для индексатора мультимедиа Azure"
description: "В этом разделе содержится обзор предустановки задачи для индексатора мультимедийных данных Azure."
services: media-services
documentationcenter: 
author: Asolanki
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: ca0b3e7aa9f6dd9fdecddfc5b3137281ed5cef35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="task-preset-for-azure-media-indexer"></a>Предустановка задачи для индексатора мультимедийных данных Azure

Индексатор мультимедиа Azure является обработчиком мультимедиа использовать hello tooperform следующие задачи: сделать доступным для поиска файлов мультимедиа и контента, создания дорожек со скрытыми субтитрами и ключевых слов, индексировать файлы активов, которые являются частью актива.

В этом разделе описывается hello задач конфигурации, необходимые tooyour toopass задания индексации. Полный пример см. в статье [Индексирование файлов мультимедиа с помощью индексатора мультимедийных данных Azure](media-services-index-content.md).

## <a name="azure-media-indexer-configuration-xml"></a>XML-файл конфигурации индексатора мультимедийных данных Azure

Hello следующей таблице описаны элементы и атрибуты XML-ФАЙЛ конфигурации hello.

|Имя|Обязательный параметр|Описание|
|---|---|---|
|Входные данные|Да|Файлы активов, которые должны tooindex.<br/>Индексатор мультимедиа Azure поддерживает следующие форматы файлов мультимедиа hello: MP4, MOV, WMV, MP3, M4A, WMA, AAC, WAV-файла. <br/><br/>Можно указать имя файла hello (s) в hello **имя** или **списка** атрибут hello **ввода** (как показано ниже). Если не указать какие tooindex файла актива, выбирается первичный файл hello. Если первичный файл актива, индексируется первый файл hello hello входного актива.<br/><br/>tooexplicitly укажите имя файла актива hello, выполните действия.<br/>```<input name="TestFile.wmv" />```<br/><br/>Также можно индексировать несколько файлов актива одновременно (копии файлов too10). toodo это:<br/>- Создайте текстовый файл (файл манифеста) с расширением LST.<br/>-Добавьте список всех имен файлов активов hello в файле манифеста toothis входного актива.<br/>-Добавьте активов toohello файл thanifest (отправить).<br/>— Укажите имя hello hello файла манифеста в атрибут списка входного актива hello.<br/>```<input list="input.lst">```<br/><br/>**Примечание:** при добавлении файла манифеста более 10 файлов toohello hello задание индексирования завершится ошибкой с кодом ошибки hello 2006.|
|metadata|нет|Метаданные для hello указанных файлов актива.<br/>```<metadata key="..." value="..." />```<br/><br/>Вы можете указать значения (value) для предопределенных ключей (key). <br/><br/>В настоящее время поддерживаются следующие ключи hello:<br/><br/>**Заголовок** и **описание** -используется tooupdate модель языка hello tooimprove точности распознавания речи.<br/>```<metadata key="title" value="[Title of hello media file]" /><metadata key="description" value="[Description of hello media file]" />```<br/><br/>**username** и **password** — применяются для проверки подлинности при загрузке файлов из Интернета по протоколу HTTP или HTTPS.<br/>```<metadata key="username" value="[UserName]" /><metadata key="password" value="[Password]" />```<br/>Здравствуйте, имя пользователя и пароль значения применяются tooall URL-адресам мультимедиа в hello входной манифест.|
|features<br/><br/>Добавлено в версии 1.2. В настоящее время функция hello поддерживается только — распознавания речи «(ASR)».|нет|функция распознавания речи Hello имеет следующие ключи параметров hello:<br/><br/>Language:<br/>-hello toobe естественный язык, распознаваемые в файл мультимедиа hello.<br/>- English, Spanish (английский, испанский).<br/><br/>CaptionFormats:<br/>-Список разделенных точкой с запятой hello требуемого форматах заголовок (если есть)<br/>- ttml;sami;webvtt.<br/><br/><br/>GenerateAIB:<br/>-Логический флаг Указание, требуется ли AIB-файл (для использования с SQL Server и hello клиентом индексатора IFilter). Подробнее этот вопрос раскрыт в записи блога Using AIB Files with Azure Media Indexer and SQL Server(Использование AIB-файлов с индексатором мультимедийных данных Azure и SQL Server).<br/>- True; False.<br/><br/>GenerateKeywords:<br/>- Логический флаг. Если он установлен, создается XML-файл ключевых слов.<br/>- True; False.|

## <a name="azure-media-indexer-configuration-xml-example"></a>Пример XML-файла конфигурации индексатора мультимедийных данных Azure

``` 
<?xml version="1.0" encoding="utf-8"?>  
<configuration version="2.0">  
  <input>  
    <metadata key="title" value="[Title of hello media file]" />  
    <metadata key="description" value="[Description of hello media file]" />  
  </input>  
  <settings>  
  </settings>  
  
  <features>  
    <feature name="ASR">    
      <settings>  
        <add key="Language" value="English"/>  
        <add key="CaptionFormats" value="ttml;sami;webvtt"/>  
        <add key="GenerateAIB" value ="true" />  
        <add key="GenerateKeywords" value ="true" />  
      </settings>  
    </feature>  
  </features>  
  
</configuration>  
```
  
## <a name="next-steps"></a>Дальнейшие действия

См. статью [Индексирование файлов мультимедиа с помощью индексатора мультимедийных данных Azure](media-services-index-content.md).

