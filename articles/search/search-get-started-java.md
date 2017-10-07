---
title: "aaaGet работы с поиском Azure в Java | Документы Microsoft"
description: "Как toobuild размещенного облака поиск приложения в Azure, используя в качестве языка программирования Java."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 8b4df3c9-3ae5-4e3a-b4bb-74b516a91c8e
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 07/14/2016
ms.author: evboyle
ms.openlocfilehash: 5476a2103f3b60fe6ec78ff3d3fdba9fcff55c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-java"></a>Начало работы с Поиском Azure в Java
> [!div class="op_single_selector"]
> * [Портал](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

Узнайте, как toobuild пользовательские Java поиск приложения, использующего поиска Azure для его результатов поиска. В этом учебнике используется hello [API REST службы поиска Azure](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello объекты и операции, используемые в этом упражнении.

toorun в этом примере необходимо иметь службы поиска Azure, который можно выполнить вход для hello [портала Azure](https://portal.azure.com). В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) пошаговые инструкции.

Мы используются следующие toobuild программного обеспечения hello и тестирования в этом примере:

* [Интегрированная среда разработки Eclipse для разработчиков Java EE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar). Быть убедиться, что версия EE hello toodownload. Один из шагов проверки hello требует функцию, которая находится только в этом выпуске.
* [JDK 8u40](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Apache Tomcat 8.0](http://tomcat.apache.org/download-80.cgi)

## <a name="about-hello-data"></a>О данных hello
В этом примере приложение использует данные из hello [США геологическое службы (универсальные группы безопасности)](http://geonames.usgs.gov/domestic/download_data.htm)фильтрацией на размер набора данных hello tooreduce состояние из Род-Айленд hello. Мы будем использовать этот toobuild данных поиска приложения, которое возвращает ориентиров здания, например больницы школы, а также геологическое таких компонентов, как потоки, Озера и конференции.

В этом приложении hello **SearchServlet.java** программа создает и загружает hello индекса с помощью [индексатора](https://msdn.microsoft.com/library/azure/dn798918.aspx) конструкции, получение hello фильтрация набора данных универсальные группы безопасности из общей базы данных SQL Azure. Предопределенных учетных данных и источник данных в сети toohello подключения сведения предоставляются в программном коде hello. С точки зрения доступа к данным дальнейшая настройка не требуется.

> [!NOTE]
> Мы применен фильтр на этот набор данных toostay под hello 10 000 документов ограничение hello бесплатной ценовой категории. При использовании стандартного уровня hello, это ограничение не применяется, и вы можете изменить этот код toouse большего набора данных. Подробнее об ограничениях каждой ценовой категории см. в разделе [Ограничения](search-limits-quotas-capacity.md).
> 
> 

## <a name="about-hello-program-files"></a>Сведения о файлах программы hello
Hello следующий список содержит описание hello файлов, соответствующих toothis выборку.

* Search.JSP: Предоставляет пользовательский интерфейс hello
* SearchServlet.java: Методы (аналогичный контроллер tooa в MVC) предоставляет
* SearchServiceClient.java: обрабатывает HTTP-запросы
* SearchServiceHelper.java: вспомогательный класс, предоставляющий статические методы
* Document.Java: Модель данных hello предоставляет
* config.Properties: задает URL-адрес службы поиска hello и ключ api
* Pom.xml: зависимость Maven

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a>Найти имя службы hello и ключ api службы поиска Azure
Все вызовы REST API службы поиска Azure требуется ввести URL-адрес службы hello и ключ api. 

1. Войдите в toohello [портала Azure](https://portal.azure.com).
2. В панели переходов hello, щелкните **службы поиска** toolist всех служб поиска Azure hello подготовлены для вашей подписки.
3. Выберите службу hello требуется toouse.
4. На панели мониторинга службы hello вы увидите плитки основные сведения, а также значок ключа hello для доступа к ключи администратора hello.
   
      ![][3]
5. Скопируйте URL-адрес службы hello и ключа администратора. Они потребуются позже, при добавлении их toohello **config.properties** файла.

## <a name="download-hello-sample-files"></a>Загрузка файлов образца hello
1. Go слишком[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) на GitHub.
2. Нажмите кнопку **загрузить ZIP**сохранить toodisk файла .zip hello и затем извлечь все файлы в ней hello. Рассмотрите возможность извлечения hello файлов в рабочей области на Java toomake проще проекта toofind hello позже.
3. файлы образца Hello доступны только для чтения. Щелкните правой кнопкой мыши папку свойств и hello снимите атрибут только для чтения.

Все последующие изменения и операторы выполнения будут применяться к файлам в этой папке.  

## <a name="import-project"></a>Импорт проекта
1. В Eclipse выберите **Файл** > **Импорт** > **Общие** > **Existing Projects into Workspace** (Существующие проекты в рабочую область).
   
    ![][4]
2. В **выберите корневой каталог**, Обзор toohello папка, содержащая файлы примеров. Выберите папку hello, содержащая hello папку проекта. Hello проекта должны появиться в hello **проекты** список с выбранным элементом.
   
    ![][12]
3. Нажмите кнопку **Готово**
4. Используйте **обозревателя проектов** tooview и редактирования файлов hello. Если он не открыт, нажмите кнопку **окна** > **Показать представление** > **обозревателя проектов** или используйте контекстное tooopen hello его.

## <a name="configure-hello-service-url-and-api-key"></a>Настройка URL-адрес службы hello и ключ api
1. В **обозревателя проектов**, дважды щелкните **config.properties** параметры конфигурации tooedit hello, содержащего имя сервера hello и ключ api.
2. См. шаги toohello ранее в этой статье, где найти URL-адрес службы hello и ключ api в hello [портала Azure](https://portal.azure.com), tooget значения hello, теперь войдет в **config.properties**.
3. В **config.properties**, замените hello ключ api для службы «Api-ключ». Затем имя службы (hello первый компонент http://servicename.search.windows.net hello URL-адрес) заменяет «имя службы» в hello того же файла.
   
    ![][5]

## <a name="configure-hello-project-build-and-runtime-environments"></a>Настройка сред hello проекта, построения и выполнения
1. В обозревателе проектов Eclipse щелкните правой кнопкой мыши проект hello > **свойства** > **аспекты проекта**.
2. Выберите **Dynamic Web Module** (Динамический веб-модуль), **Java** и **JavaScript**.
   
    ![][6]
3. Нажмите кнопку **Применить**.
4. Выберите **Окно** > **Параметры** > **Сервер** > **Runtime Environments** (Среды выполнения) > **Добавить...**.
5. Разверните Apache и выберите ранее установленный сервер Apache Tomcat hello версии hello. В нашей системе мы установили версию 8.
   
    ![][7]
6. На следующей странице hello укажите каталог установки Tomcat hello. На компьютере под управлением Windows это, скорее всего, будет C:\Program Files\Apache Software Foundation\Tomcat *версия*.
7. Нажмите кнопку **Готово**
8. Выберите **Окно** > **Параметры** > **Java** > **Installed JREs** (Установленные JRE) > **Добавить...**.
9. В окне **Add JRE** (Добавить JRE) выберите **Standard VM** (Стандартная виртуальная машина).
10. Нажмите кнопку **Далее**.
11. В разделе "Определение JRE" в главном окне выберите **Каталог**.
12. Перейдите в слишком**Program Files** > **Java** и выберите hello JDK, ранее была установлена. Это важные tooselect hello JDK как hello JRE.
13. В JREs установлены, выберите hello **JDK**. Параметры должны выглядеть примерно toohello следующий снимок экрана.
    
    ![][9]
14. При необходимости установите **окна** > **веб-браузер** > **Internet Explorer** tooopen приложения hello в окне внешнем браузере. Использование внешнего браузера обеспечивает лучшую работу веб-приложения.
    
    ![][8]

Задачи настройки hello завершена. Далее предстоит Постройте и запустите проект hello.

## <a name="build-hello-project"></a>Построение проекта hello
1. В обозревателе решений, щелкните правой кнопкой мыши имя проекта hello и выберите **запуска от имени** > **Maven сборки...**  tooconfigure hello проекта.
   
    ![][10]
2. В разделе "Изменить конфигурацию" в поле "Цели" введите "чистая установка" и нажмите **Выполнить**.

Сообщения о состоянии, окно консоли toohello выходных данных. Вы увидите УСПЕШНОСТИ ПОСТРОЕНИЯ проекта является признаком того, hello построен без ошибок.

## <a name="run-hello-app"></a>Выполните приложение hello
В этом последнем шаге будет выполняться приложение hello в среде выполнения локального сервера.

Если среде выполнения сервера еще не указаны в Eclipse, вам потребуется toodo сначала.

1. В обозревателе проектов разверните **WebContent**.
2. Щелкните правой кнопкой мыши **Search.jsp** > **Запуск от имени** > **Запустить на сервере**. Выберите сервер Apache Tomcat hello и нажмите кнопку **запуска**.

> [!TIP]
> Если вы использовали toostore рабочей области не по умолчанию проекта, вам потребуется toomodify **Настройка запуска** toopoint toohello проекта расположение tooavoid ошибку при запуске сервера. В обозревателе проектов щелкните правой кнопкой мыши **Search.jsp** > **Запуск от имени** > **Run Configurations** (Конфигурации запуска). Выберите сервер Apache Tomcat hello. Выберите **Аргументы**. Нажмите кнопку **рабочей** или **файловой системы** tooset hello папку, содержащую проект hello.
> 
> 

При запуске приложения hello, вы увидите окно браузера, предоставляя поле поиска для ввода условия.

Подождите около одной минуты, прежде чем нажимать кнопку **поиска** toogive hello службы времени toocreate и загрузка hello индекса. Если возникает ошибка HTTP 404, необходимо просто toowait немного больше времени, прежде чем повторить попытку.

## <a name="search-on-usgs-data"></a>Поиск по данным USGS
набор данных Hello универсальные группы безопасности включает записи, соответствующие toohello состояние из Род-Айленд. Если щелкнуть **поиска** на поле поиска пустым, вы получите hello 50 первых записей, которое является по умолчанию hello.

Ввести условие поиска, даст hello поисковой системы что-нибудь toogo на. Попробуйте ввести региональное имя или название. «Roger Вильямса» был первый регулятор Род-Айленд hello. В его честь названы многие парки, здания и школы.

![][11]

Вы также можете попробовать одно из следующих условий поиска:

* Потакет
* Пемброк
* гусь +мыс

## <a name="next-steps"></a>Дальнейшие действия
Это hello учебник первого поиска Azure на основе Java и hello dataset универсальные группы безопасности. Со временем мы расширим этого учебника toodemonstrate дополнительные функции, может потребоваться toouse пользовательских решений.

Если уже есть определенные знания в поиске Azure, можно использовать этот образец как springboard для дальнейших экспериментов возможно дополнения hello [страницу поиска](search-pagination-page-layout.md), или реализовав [фасетная Навигация](search-faceted-navigation.md). Можно также повышают эффективность hello страницы результатов поиска, добавив счетчики и пакетную обработку документов, чтобы пользователи могут постраничного просмотра результатов hello.

Новый tooAzure поиска? Рекомендуется попробовать другие учебники toodevelop понимание можно создать. Посетите наш [страницы документации](https://azure.microsoft.com/documentation/services/search/) toofind больше ресурсов. Можно также просмотреть ссылки hello в нашем [список видео и учебник](search-video-demo-tutorial-list.md) tooaccess Дополнительные сведения.

<!--Image references-->
[1]: ./media/search-get-started-java/create-search-portal-1.PNG
[2]: ./media/search-get-started-java/create-search-portal-21.PNG
[3]: ./media/search-get-started-java/create-search-portal-31.PNG
[4]: ./media/search-get-started-java/AzSearch-Java-Import1.PNG
[5]: ./media/search-get-started-java/AzSearch-Java-config1.PNG
[6]: ./media/search-get-started-java/AzSearch-Java-ProjectFacets1.PNG
[7]: ./media/search-get-started-java/AzSearch-Java-runtime1.PNG
[8]: ./media/search-get-started-java/AzSearch-Java-Browser1.PNG
[9]: ./media/search-get-started-java/AzSearch-Java-JREPref1.PNG
[10]: ./media/search-get-started-java/AzSearch-Java-BuildProject1.PNG
[11]: ./media/search-get-started-java/rogerwilliamsschool1.PNG
[12]: ./media/search-get-started-java/AzSearch-Java-SelectProject.png
