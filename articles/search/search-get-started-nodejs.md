---
title: "aaaGet работы с поиском Azure в Node.js | Документы Microsoft"
description: "Пошаговое создание приложения поиска в облачной службе поиска Azure с использованием Node.js в качестве языка программирования."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: evboyle
ms.openlocfilehash: e9c7d756c2ea191ee2a285485c90439b96aa73b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a>Начало работы со службой поиска Azure на Node.js
> [!div class="op_single_selector"]
> * [Портал](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

Узнайте, как toobuild пользовательские Node.js поиск приложения, использующего поиска Azure для его результатов поиска. В этом учебнике используется hello [API REST службы поиска Azure](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello объекты и операции, используемые в этом упражнении.

Мы использовали [Node.js](https://Nodejs.org) и NPM, [Sublime текст 3](http://www.sublimetext.com/3)и Windows PowerShell на Windows 8.1 toodevelop и проверки кода.

toorun в этом примере необходимо иметь службы поиска Azure, который можно выполнить вход для hello [портал Azure](https://portal.azure.com). В разделе [Создание службы поиска Azure на портале hello](search-create-service-portal.md) пошаговые инструкции.

## <a name="about-hello-data"></a>О данных hello
В этом примере приложение использует данные из hello [США геологическое службы (универсальные группы безопасности)](http://geonames.usgs.gov/domestic/download_data.htm)фильтрацией на размер набора данных hello tooreduce состояние из Род-Айленд hello. Мы будем использовать этот toobuild данных поиска приложения, которое возвращает ориентиров здания, например больницы школы, а также геологическое таких компонентов, как потоки, Озера и конференции.

В этом приложении hello **DataIndexer** программа создает и загружает hello индекса с помощью [индексатора](https://msdn.microsoft.com/library/azure/dn798918.aspx) конструкции, получение hello фильтрация набора данных универсальные группы безопасности из общей базы данных SQL Azure. Учетные данные и подключения источника данных в сети toohello информация представлена в коде программы hello. Дальнейшая настройка не требуется.

> [!NOTE]
> Мы применен фильтр на этот набор данных toostay под hello 10 000 документов ограничение hello бесплатной ценовой категории. При использовании стандартного уровня hello, это ограничение не применяется. Дополнительные сведения об ограничениях каждой ценовой категории см. в статье [Ограничения поиска Azure](search-limits-quotas-capacity.md).
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a>Найти имя службы hello и ключ api службы поиска Azure
После создания службы hello, возвращают URL-адрес hello портала tooget toohello или `api-key`. Tooyour подключений службы поиска требует наличия обоих URL-адрес hello и `api-key` tooauthenticate hello вызовов.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. В панели переходов hello, щелкните **службы поиска** toolist подготовить все службы поиска Azure для вашей подписки.
3. Выберите службу hello требуется toouse.
4. На панели мониторинга службы hello вы увидите плитки основные сведения, такие как hello значок ключа для доступа к ключи администратора hello.
5. Скопируйте URL-адрес службы hello ключа администратора и ключ запроса. Все три необходимые данные при их добавлении файла config.js toohello.

## <a name="download-hello-sample-files"></a>Загрузка файлов образца hello
Используйте один из следующих подходов toodownload hello образец hello.

1. Go слишком[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).
2. Нажмите кнопку **загрузить ZIP**, сохранить hello ZIP-файл, а затем извлечь все файлы hello в ней.

Все последующие изменения и операторы выполнения применяются к файлам в этой папке.

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a>Обновите hello config.js. с помощью URL-адреса службы поиска и ключа API
С помощью hello URL-адрес и ключ api, который был скопирован ранее, укажите URL-адрес hello, ключ администратора и ключ запроса в файле конфигурации.

Ключи администратора предоставляют полный контроль над операциями службы, включая создание или удаление индекса и загрузку документов. Напротив ключи запроса используются для операций чтения, обычно используется клиентскими приложениями, которые подключаются tooAzure поиска.

В этом примере мы включать hello запроса ключа toohelp дополнять hello рекомендация, с помощью ключа запроса hello в клиентских приложениях.

Привет, следуя снимке экрана показано **config.js** открыть в текстовом редакторе с hello соответствующие операции demarcated, чтобы можно было увидеть, где файл hello tooupdate с hello значения, которые являются допустимыми для службы поиска.

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a>Узел среды выполнения для образца hello
Образец Hello требует HTTP-сервер, который можно установить глобально с помощью npm.

Окно PowerShell для hello, следующие команды.

1. Перейдите в папку toohello, содержащую hello **package.json** файла.
2. Введите `npm install`.
3. Введите `npm install -g http-server`.

## <a name="build-hello-index-and-run-hello-application"></a>Создание индекса hello и запустите приложение hello
1. Введите `npm run indexDocuments`.
2. Введите `npm run build`.
3. Введите `npm run start_server`.
4. В браузере откройте страницу `http://localhost:8080/index.html`

## <a name="search-on-usgs-data"></a>Поиск по данным USGS
набор данных Hello универсальные группы безопасности включает записи, соответствующие toohello состояние из Род-Айленд. Если щелкнуть **поиска** на поле поиска пустым, вы получаете hello 50 первых записей, которое является по умолчанию hello.

Ввести поисковый термин дает hello поисковой системы что-нибудь toogo на. Попробуйте ввести региональное имя или название. «Roger Вильямса» был первый регулятор Род-Айленд hello. В его честь названы многие парки, здания и школы.

![][9]

Вы также можете попробовать одно из следующих условий поиска:

* Потакет
* Пемброк
* гусь +мыс

## <a name="next-steps"></a>Дальнейшие действия
Это hello учебник первого поиска Azure на основе Node.js и hello dataset универсальные группы безопасности. Со временем мы расширим этого учебника toodemonstrate дополнительные функции, может потребоваться toouse пользовательских решений.

Если у вас уже есть опыт работы с Поиском Azure, вы можете использовать этот пример как фундамент для средств подбора (запросы опережающего ввода или автозаполнения), фильтров и фасетной навигации. Можно также повышают эффективность hello страницы результатов поиска, добавив счетчики и пакетную обработку документов, чтобы пользователи могут постраничного просмотра результатов hello.

Новый tooAzure поиска? Рекомендуется попробовать другие учебники toodevelop понимание можно создать. Посетите наш [страницы документации](https://azure.microsoft.com/documentation/services/search/) toofind больше ресурсов. Можно также просмотреть ссылки hello в нашем [список видео и учебник](search-video-demo-tutorial-list.md) tooaccess Дополнительные сведения.

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
