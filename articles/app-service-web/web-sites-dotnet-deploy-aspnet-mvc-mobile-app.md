---
title: "ASP.NET MVC 5 aaaDeploy мобильного веб-приложения в службе приложений Azure"
description: "Учебник, в котором объясняется, как toodeploy tooAzure приложения web службы приложений с помощью мобильных функции в ASP.NET MVC 5 веб-приложения."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 0752c802-8609-4956-a755-686116913645
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 01119c07246c0252fd357562774a2e90b3ef77d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a>Развертывание мобильного веб-приложения ASP.NET MVC 5 в службе приложений Azure
В этом учебнике объясняется hello основы как toobuild ASP.NET MVC 5 веб-приложения, мобильные и развернуть ее tooAzure службы приложений. В этом учебнике требуется [Visual Studio Express 2013 для Web] [ Visual Studio Express 2013] или профессиональных выпусков Visual Studio, если у вас уже есть, hello. Можно использовать [Visual Studio 2015] снимков экрана приветствия будут отличаться, но необходимо использовать hello ASP.NET 4.x шаблоны.

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a>Что вы создадите
В этом учебнике вы добавите мобильные функции toohello простое конференции листинг приложение, которое предоставляется в hello [начальный проект][StarterProject]. Hello следующем снимке экрана показано hello сеансов ASP.NET в приложении hello завершена, как видно в эмуляторе hello браузера в Internet Explorer 11 F12 средств разработчика.

![][FixedSessionsByTag]

Можно использовать средства разработчика Internet Explorer 11 F12 hello и hello [инструмента Fiddler] [ Fiddler] toohelp отладки приложения. 

## <a name="skills-youll-learn"></a>Чему вы научитесь
В этом учебнике вы узнаете:

* Как toopublish toouse Visual Studio 2013 веб-приложения непосредственно tooa веб-приложения в службе приложений Azure.
* Использование CSS Bootstrap framework hello шаблоны hello ASP.NET MVC 5 для улучшения отображения на мобильных устройствах
* Как toocreate mobile конкретного представления tootarget конкретных браузеры для мобильных устройств, таких как hello iPhone и Android
* Как отвечать на запросы представления toocreate (представления, реагирующие на устройствах toodifferent браузеры)

## <a name="set-up-hello-development-environment"></a>Настройка среды разработки hello
Настройка среды разработки, установив hello Azure SDK для .NET 2.5.1 или более поздней версии. 

1. tooinstall hello Azure SDK для .NET, щелкните ссылку hello. Если у вас нет Visual Studio 2013, пока установлен, то оно будет установлено по каналу hello. Для работы с этим учебником требуется Visual Studio 2013. [Пакет SDK Azure для Visual Studio 2013][AzureSDKVs2013]
2. В окне приветствия установщика веб-платформы нажмите кнопку **установить** и продолжите установку hello.

Кроме того, понадобится эмулятор браузера для мобильного устройства. Любой из следующих hello будет работать:

* Эмулятор браузера в [инструментах разработчика F12 Internet Explorer 11][EmulatorIE11] (используется в снимках экрана всех браузеров мобильного устройства). Он содержит предустановки строк агента пользователя для Windows Phone 8, Windows Phone 7 и Apple iPad.
* Эмулятор браузера в [Google Chrome DevTools][EmulatorChrome]. Содержит предустановки для многих устройств Android, а также Apple iPhone, Apple iPad и Amazon Kindle Fire. Также поддерживает эмуляцию событий прикосновения.
* [Эмулятор Opera Mobile][EmulatorOpera]

Проекты Visual Studio с C\# исходный код, являются доступными tooaccompany в этом разделе:

* [Скачивание начального проекта][StarterProject]
* [Скачивание полного проекта][CompletedProject]

## <a name="bkmk_DeployStarterProject"></a>Развертывание hello начального проекта tooan веб-приложение Azure
1. Загрузить приложение hello листинг конференции [начальный проект][StarterProject].
2. Затем в проводнике Windows щелкните правой кнопкой мыши hello загружен ZIP-файл и выберите *свойства*.
3. В hello **свойства** диалогового окна выберите hello **Unblock** кнопки. (Разблокировке предотвращает предупреждение системы безопасности, которая возникает при попытке toouse *.zip* файл, загруженный с веб-узла hello.)
4. Щелкните правой кнопкой мыши hello ZIP-файл и выберите **извлечь все** распаковать файл hello. 
5. В Visual Studio откройте hello *C#\Mvc5Mobile.sln* файла.
6. В обозревателе решений щелкните правой кнопкой мыши проект hello и нажмите кнопку **публикации**.
   
   ![][DeployClickPublish]
7. В окне веб-публикации щелкните **Служба приложений Microsoft Azure**.
   
   ![][DeployClickWebSites]
8. Если вы еще не выполнили вход в Azure, щелкните **Добавить учетную запись**.
   
   ![][DeploySignIn]
9. Выполните запросы toolog hello в учетную запись Azure.
10. диалоговое окно службы приложения Hello появляются вы как вход. Нажмите кнопку **Создать**.
    
    ![][DeployNewWebsite]  
11. В hello **имя веб-приложения** укажите префикс имени уникальный приложения. Полностью определенным именем вашего веб-приложения будет *&lt;префикс>*.azurewebsites.net. Также выберите или укажите имя существующей группы ресурсов в поле **Группа ресурсов**. Нажмите кнопку **New** toocreate новый план служб приложений.
    
    ![][DeploySiteSettings]
12. Настройте новый план служб приложений hello и нажмите кнопку **ОК**. 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. Вернувшись в диалоговое окно создания службы приложения hello, нажмите кнопку **создать**.
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. После того как hello ресурсы Azure, диалоговое окно приветствия веб-публикация будет заполняться hello параметры для нового приложения. Щелкните **Опубликовать**.
    
    ![][DeployPublishSite]
    
    После завершения публикации hello начального проекта toohello веб-приложение Azure Visual Studio браузер для настольных компьютеров hello открывает toodisplay hello динамической веб-приложения.
15. Запустите симулятор мобильных браузеров, скопируйте URL-адрес hello приложения hello конференции (*<prefix>*. azurewebsites.net) в эмуляторе hello, нажмите кнопку сверху справа и выберите **Обзор тегом**. Если вы используете Internet Explorer 11 в качестве браузера по умолчанию hello, необходимо просто tootype `F12`, затем `Ctrl+8`и измените профиль браузера hello слишком**Windows Phone**. На рисунке ниже показана hello *AllTags* представления в книжной ориентации (в выборе **Обзор тегом**).
    
    ![][AllTags]

> [!TIP]
> При отладке приложения MVC 5 в среде Visual Studio можно опубликовать вашей tooAzure web app снова tooverify hello динамической веб-приложения непосредственно из браузера мобильных или эмулятор браузера.
> 
> 

экран приветствия удобочитаемым на мобильном устройстве. Уже также можно увидеть некоторые визуальные эффекты hello применены платформой hello CSS начальной загрузки.
Нажмите кнопку hello **ASP.NET** ссылку.

![][SessionsByTagASP.NET]

Hello представление тега ASP.NET — они масштаба toohello экран, который начальной загрузки может сделать для вас автоматически. Тем не менее можно улучшить это представление toobetter масть hello мобильных браузеров. Например, hello **даты** столбца трудно читать. Далее в учебнике hello изменим hello *AllTags* просмотра toomake его мобильной.

## <a name="bkmk_bootstrap"></a> Платформа начальной загрузки CSS
Новое в hello MVC 5 шаблона является встроенной поддержки начальной загрузки. Вы уже видели как усовершенствует немедленно hello различных представлений в приложении. Например hello панели навигации в верхней hello автоматически сворачиваемого когда меньше ширины обозревателя hello. В браузер для настольных компьютеров hello попробуйте изменить размер окна браузера hello и см. Изменение внешнего вида панели навигации hello. Это отвечать на запросы веб-дизайн hello, который встроен в начальной загрузки.

toosee о том, как будет выглядеть hello веб-приложения без начальной загрузки, откройте *приложения\_запустить\\BundleConfig.cs* и закомментируйте hello строки, содержащие *bootstrap.js* и *bootstrap.css*. Hello код отображает hello последних двух инструкций hello `RegisterBundles` метод после изменения hello:

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

Нажмите клавишу `Ctrl+F5` toorun приложения hello.

Обратите внимание, что эту панель навигации сворачиваемого hello теперь является просто обычный неупорядоченный список. Еще раз щелкните **Browse by tag** (Поиск по тегу), затем щелкните **ASP.NET**.
В представлении мобильном эмуляторе hello вы увидите теперь, когда он больше не соответствует масштаба toohello экрана и необходимо прокрутки сбоку в порядке toosee hello правой части таблицы hello.

![][SessionsByTagASP.NETNoBootstrap]

Отменить изменения и обновить tooverify мобильных браузеров hello, экрана приветствия мобильные восстановлена.

Начальной загрузки не определенного tooASP.NET MVC 5, и воспользоваться преимуществами этих функций в любой веб-приложения. Теперь эта функция встроена в шаблон проекта ASP.NET MVC 5, таким образом, ваше веб-приложение MVC 5 сможет по умолчанию использовать преимущества Bootstrap.

Дополнительные сведения о начальной загрузки go toothe [начальной загрузки] [ BootstrapSite] сайта.

В следующем разделе hello будет отображен как tooprovide браузера mobile определенным представлениям.

## <a name="bkmk_overrideviews"></a>Переопределить hello, макеты и частичные представления
Вы можете переопределить любое представление (включая макеты и частичные представления) для браузеров мобильных устройств вообще, для отдельного браузера мобильных устройств или для любого конкретного браузера. Просмотр конкретного mobile tooprovide, можно скопировать файл представления и добавление *. Mobile* toohello имя файла. Например, toocreate мобильного телефона *индекс* представления, можно скопировать *представления\\Главная\\Index.cshtml* для *представления\\Главная\\ Index.Mobile.cshtml*.

В этом разделе для мобильных устройств будет создан специальный файл макета.

toostart копирования *представления\\Shared\\\_Layout.cshtml* для *представления\\Shared\\\_Layout.Mobile.cshtml* . Откройте  *\_Layout.Mobile.cshtml* и измените заголовок hello из **приложения MVC5** слишком**MVC5 приложения (мобильный)**.

В каждом `Html.ActionLink` вызова для hello панели навигации, удалите «Просмотр по» в каждой связи *ActionLink*. Hello код отображает hello завершения `<ul class="nav navbar-nav">` тег hello мобильных макета файла.

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

Копировать hello *представления\\Главная\\AllTags.cshtml* файл *представления\\Главная\\AllTags.Mobile.cshtml*. Откройте новый файл hello и измените `<h2>` элемент из «Теги» слишком "теги (M)»:

    <h2>Tags (M)</h2>

Обзор toohello теги страницы с использованием браузер для настольных компьютеров и мобильных браузеров эмулятора. эмулятор мобильных браузеров Hello показывает hello два изменения, внесенные (hello заголовка из  *\_Layout.Mobile.cshtml* и заголовок hello от *AllTags.Mobile.cshtml*).

![][AllTagsMobile_LayoutMobile]

Напротив, не изменилась hello рабочего стола (с заголовками из  *\_Layout.cshtml* и *AllTags.cshtml*).

![][AllTagsMobile_LayoutMobileDesktop]

## <a name="bkmk_browserviews"></a> Создание представлений для браузера
Кроме того при представления отдельных toomobile или рабочего стола, можно создать представления для отдельного браузера. Например можно создать представления, которые специально предназначены для hello iPhone или браузера Android hello. В этом разделе вы создадите макет для браузера iPhone hello и версию iPhone hello *AllTags* представления.

Откройте hello *Global.asax* и добавьте следующий код toohello внизу hello `Application_Start` метод.

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

Этот код определяет новый режим отображения с именем iPhone, который будет использоваться для каждого входящего запроса. Если hello входящий запрос соответствует условию, заданных (то есть, если агент пользователя hello содержит строку hello «iPhone»), ASP.NET MVC будет искать представления, имя которого содержит суффикс «iPhone».

> [!NOTE]
> При добавлении мобильных обозревателем режимы отображения, такие как для iPhone и Android, будет убедиться, что первый аргумент hello tooset слишком`0` toomake (вставки в начале hello hello списка), убедиться, что, режим обозревателем hello имеет приоритет над мобильными шаблона hello (*. Mobile.cshtml). Если hello мобильных шаблон находится в начале hello списка hello, она будет выбрана по вашей режим отображения предполагаемой (hello первого совпадения wins и соответствует hello мобильных шаблон все браузеры для мобильных устройств). 
> 
> 

Щелкните правой кнопкой мыши в коде hello `DefaultDisplayMode`, выберите **Разрешить**и нажмите кнопку `using System.Web.WebPages;`. Это добавляет toothe ссылки `System.Web.WebPages` пространство имен, что, если `DisplayModeProvider` и `DefaultDisplayMode` определенных типов.

![][ResolveDefaultDisplayMode]

Кроме того, можно просто вручную добавить следующие строки toothe hello `using` раздел файла hello.

    using System.Web.WebPages;

Сохраните изменения hello. Скопируйте файл*Views\\Shared\\\_Layout.Mobile.cshtml* в *Views\\Shared\\\_Layout.iPhone.cshtml*. Откройте новый файл hello и измените заголовок hello от `MVC5 Application (Mobile)` для `MVC5 Application (iPhone)`.

Копировать hello *представления\\Главная\\AllTags.Mobile.cshtml* файл *представления\\Главная\\AllTags.iPhone.cshtml*. В новом файле hello, измените hello `<h2>` из «теги (M)» слишком» тегами элемента (iPhone)».

Запустите приложение hello. Запуск эмулятора мобильных браузеров, убедитесь, что его агент пользователя установлено слишком «iPhone» и найдите toohello *AllTags* представления. При использовании эмулятора hello в средствах разработчика Internet Explorer 11 F12 настройте эмуляции toohello ниже:

* профиль браузера — **Windows Phone**
* строка агента пользователя — **Custom**
* настраиваемая строка — **Apple-iPhone5C1/1001.525**

Hello следующем снимке экрана показано hello *AllTags* представление в эмуляторе в средствах разработчика Internet Explorer 11 F12 с hello специальную строку агента пользователя (это строки агента пользователя iPhone 5 C).

![][AllTagsIPhone_LayoutIPhone]

В браузере мобильного hello выберите hello **динамики** ссылку. Так как не представлением для мобильных устройств (*AllSpeakers.Mobile.cshtml*), просматривать динамики по умолчанию hello (*AllSpeakers.cshtml*) отображается с помощью мобильных режиме hello ( *\_ Layout.Mobile.cshtml*). Как показано ниже, заголовок hello **MVC5 приложения (мобильный)** определяется в  *\_Layout.Mobile.cshtml*.

![][AllSpeakers_LayoutMobile]

Глобально, представление по умолчанию (не для мобильных устройств) к просмотру в макете мобильных устройств можно отключить, установив `RequireConsistentDisplayMode` для `true` в hello *представления\\\_ViewStart.cshtml* файла следующим образом:

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

Когда `RequireConsistentDisplayMode` задано слишком`true`, hello мобильных макета (*\_Layout.Mobile.cshtml*) используется только для мобильных представлений (т. е. Если файл представления имеет форму hello  ***ViewName** . Mobile.cshtml*). Может потребоваться tooset `RequireConsistentDisplayMode` слишком`true` Если мобильных макет плохо работает с вашим представлениям не для мобильных устройств. Hello снимке экрана ниже показано как hello *динамики* при отображении страницы `RequireConsistentDisplayMode` задано слишком`true` (без строку hello «(мобильный)» в hello навигации панели hello верхней).

![][AllSpeakers_LayoutMobileOverridden]

Согласованный режим отображения в определенных режимах можно отключить, установив `RequireConsistentDisplayMode` слишком`false` в файл представления hello. Приведенный ниже код в hello *представления\\Главная\\AllSpeakers.cshtml* файл задает `RequireConsistentDisplayMode` слишком`false`:

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

В этом разделе мы видели как toocreate мобильных макеты, представлений и hello как toocreate макеты и представлений для конкретных устройств, таких как iPhone.
Однако главным преимуществом hello hello CSS начальной загрузки framework является динамический макет, что означает, что одной таблицы стилей могут применяться за пределами рабочего стола, телефон и планшет браузеры toocreate согласованного внешнего вида и поведения. В следующем разделе hello вы увидите, как tooleverage начальной загрузки toocreate мобильной представления.

## <a name="bkmk_Improvespeakerslist"></a>Улучшения hello динамики списка
Как вы только что увидели hello *динамики* представление доступен для чтения, но ссылки hello невелики и являются трудно tootap на мобильном устройстве. В этом разделе мы сделаем hello *AllSpeakers* представление мобильные, отображаются большой, чтобы коснитесь ссылки и содержит поле поиска tooquickly найти динамики.

Можно использовать hello начальной загрузки [связанного списка группы] [ linked list group] стили для улучшения hello *динамики* представления. В *представления\\Главная\\AllSpeakers.cshtml*, замените содержимое файла Razor hello hello приведенный ниже код hello.

     @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, "SessionsBySpeaker", new { speaker }, new { @class = "list-group-item" })
        }
    </div>

Hello `class="list-group"` атрибута в hello `<div>` тег применяет начальной загрузки список стилей и hello `class="input-group-item"` атрибут применяется, связи tooeach стиля элемента списка начальной загрузки.

Обновите hello мобильных браузеров. Hello обновить представление выглядит следующим образом:

![][AllSpeakersFixed]

Hello начальной загрузки [связанного списка группы] [ linked list group] стили делает hello всей поле каждой связи интерактивными, являющийся гораздо более широкие пользователя. Переключитесь в представление рабочего стола toothe и понаблюдайте за hello согласованный внешний вид.

![][AllSpeakersFixedDesktop]

Несмотря на то, что представление мобильных браузеров hello была улучшена, и громоздкими hello длинный список динамики. Исходные настройки Bootstrap не предусматривают функцию фильтра поиска, но вы можете ее добавить с помощью нескольких строк кода. Сначала будет добавлено представление toohello поле поиска, затем подключить hello код JavaScript для функции фильтра hello. В *представления\\Главная\\AllSpeakers.cshtml*, добавьте \<формы\> тег сразу после hello \<h2\> тег, как показано ниже:

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <form class="input-group">
        <span class="input-group-addon"><span class="glyphicon glyphicon-search"></span></span>
        <input type="text" class="form-control" placeholder="Search speaker">
    </form>
    <br />
    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class = "list-group-item" })
        }
    </div>

Обратите внимание, что hello `<form>` и `<input>` теги оба имеют toothem начальной загрузки стили, примененные hello. Hello `<span>` элемент добавляет начальной загрузкой [glyphicon] [ glyphicon] toothe поле поиска.

В hello *сценариев* папки, добавьте файл JavaScript с именем *filter.js*. Откройте файл hello и вставьте следующий код в него hello:

    $(function () {

        // reset hello search form when hello page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up hello events toohello <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with hello typed text and hide others
            for (var i = 0; i < items.length; i++) {
                var val = items[i].text.toLowerCase();
                val = val.substring(0, searchtxt.length);
                if (val == searchtxt) {
                    $(items[i]).show();
                }
                else {
                    $(items[i]).hide();
                }
            }
        });
    });

Необходимо также tooinclude filter.js в ваш зарегистрированных пакетов. Откройте *приложения\_запустить\\BundleConfig.cs* и измените первый пакеты hello. Изменить первый `bundles.Add` инструкции (для hello **jquery** пакета) tooinclude *сценариев\\filter.js*, как показано ниже:

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

Hello **jquery** пакета уже отображается по умолчанию hello  *\_макета* представления. Более поздней версии, могут использовать hello же JavaScript code tooapply представлений списка tooother функции фильтра.

Обновите hello мобильный браузер и перейдите toohello *AllSpeakers* представления. В поле поиска введите «sc». Hello динамики список теперь должны быть отфильтрованы согласно tooyour строку поиска.

![][AllSpeakersFixedSearchBySC]

## <a name="bkmk_improvetags"></a>Улучшения hello списка тегов
Как hello *динамики* просмотреть, hello *теги* представление доступен для чтения, но hello ссылки — это небольшой и сложной tootap на мобильном устройстве. Вы можете исправить hello *теги* представление hello таким же способом устранения hello *динамики* просмотра, если использовать описанные ранее, но с hello следующих изменений кода hello `Html.ActionLink` синтаксис методов в  *Представления\\Главная\\AllTags.cshtml*:

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

Hello обновить браузер для настольных компьютеров выглядит следующим образом:

![][AllTagsFixedDesktop]

И hello обновляется мобильных браузеров выглядит следующим образом: 

![][AllTagsFixed]

> [!NOTE]
> Если вы заметили, что hello исходного списка форматирования осталась в Здравствуйте мобильных браузеров и определить, какая ошибка tooyour стили начальной загрузки работы с низким приоритетом является, это является артефактом предыдущих действий toocreate мобильных конкретного представления. Однако теперь, когда вы используете toocreate framework hello CSS начальной загрузки конструктора быстродействующих веб-приложений, перейдите head и удалите эти мобильные особых представлений и представления структуры для конкретной mobile hello. Это сделано, hello обновить мобильных браузеров будут отображены начальной загрузки стили hello.
> 
> 

## <a name="bkmk_improvedates"></a>Улучшения hello списка дат
Можно улучшить hello *даты* просмотреть, как повысить hello *динамики* и *теги* представления при использовании описанных выше, но с hello после изменения кода hello `Html.ActionLink` синтаксис методов в *представления\\Главная\\AllDates.cshtml*:

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

Вот как будет выглядеть обновленное представление браузера мобильного устройства:

![][AllDatesFixed]

Можно улучшить hello *даты* представление, организуя hello значений даты и времени по дате. Это можно сделать с помощью hello начальной загрузки [панелей] [ panels] Задание стиля. Замените содержимое hello hello *представления\\Главная\\AllDates.cshtml* файла следующим кодом:

    @model IEnumerable<DateTime>

    @{
        ViewBag.Title = "All Dates";
    }

    <h2>Dates</h2>

    @foreach (var dategroup in Model.GroupBy(x=>x.Date))
    {
        <div class="panel panel-primary">
            <div class="panel-heading">
                @dategroup.Key.ToString("ddd, MMM dd")
            </div>
            <div class="panel-body list-group">
                @foreach (var date in dategroup)
                {
                    @Html.ActionLink(date.ToString("h:mm tt"), 
                                     "SessionsByDate", 
                                     new { date }, 
                                     new { @class = "list-group-item" })
                }
            </div>
        </div>
    }

Этот код создает отдельную `<div class="panel panel-primary">` тег для каждой даты distinct в списке hello и использует hello [связанного списка группы] [ linked list group] для соответствующего связывает как раньше. Вот какие hello мобильных браузеров выглядит как при выполнении этого кода:

![][AllDatesFixed2]

Коммутатор toohello браузер для настольных компьютеров. Обратите внимание, согласованного вида hello.

![][AllDatesFixed2Desktop]

## <a name="bkmk_improvesessionstable"></a>Улучшить представление SessionsTable hello
В этом разделе мы сделаем hello *SessionsTable* просмотреть дополнительные мобильные. Это изменение является более существенные изменения предыдущих hello.

В браузере мобильного hello, коснитесь hello **тега** , а затем введите `asp` в поле поиска.

![][AllTagsFixedSearchByASP]

Коснитесь hello **ASP.NET** ссылку.

![][SessionsTableTagASP.NET]

Как видите, экрана приветствия форматируется как таблицы, которая является в настоящее время спроектированный toobe просмотре в браузере рабочего стола hello. Однако это немного сложным tooread на мобильный браузер. toofix, откройте *представления\\Главная\\SessionsTable.cshtml* и затем замените содержимое файла hello hello, следующий код:

    @model IEnumerable<Mvc5Mobile.Models.Session>

    <h2>@ViewBag.Title</h2>

    <div class="container">
        <div class="row">
            @foreach (var session in Model)
            {
                <div class="col-md-4">
                    <div class="list-group">
                        @Html.ActionLink(session.Title, 
                                         "SessionByCode", 
                                         new { session.Code }, 
                                         new { @class="list-group-item active" })
                        <div class="list-group-item">
                            <div class="list-group-item-text">
                                @Html.Partial("_SpeakersLinks", session)
                            </div>
                            <div class="list-group-item-info">
                                @session.DateText
                            </div>
                            <div class="list-group-item-info small hidden-xs">
                                @Html.Partial("_TagsLinks", session)
                            </div>
                        </div>
                    </div>
                </div>
            }
        </div>
    </div>

Код Hello выполняет три вещи:

* использует hello начальной загрузки [группы пользовательских связанного списка] [ custom linked list group] tooformat Здравствуйте, сведения о сеансе по вертикали, чтобы эта информация доступна для чтения на мобильный браузер (с помощью классов такие как Список группа элемент текст)
* применяет hello [сетки системы] [ grid system] toothe макета, поэтому сеанса hello элементы потока в браузер для настольных компьютеров hello по горизонтали и по вертикали в мобильных браузеров hello (с помощью класса hello col-md-4)
* использует hello [отвечать на запросы программы] [ responsive utilities] скрытие hello сеанса теги при просмотре в мобильных браузеров hello (с помощью класса скрытые xs hello)

Вы также можете нажать заголовок ссылки toogo toohello соответствующих сеанса. ниже рисунке Hello отражает изменения кода hello.

![][FixedSessionsByTag]

системы начальной загрузки сетки Hello примененное автоматически упорядочивает сеансы по вертикали в браузере мобильного hello. Кроме того Обратите внимание, что теги hello не отображаются. Коммутатор toohello браузер для настольных компьютеров.

![][SessionsTableFixedTagASP.NETDesktop]

Обратите внимание hello теги отображаются в браузер для настольных компьютеров hello. Кроме того вы увидите, что hello сетки начальной загрузки системы, примененные упорядочивает элементы сеанса hello в двух столбцах. Если увеличить браузер изменится, упорядочение hello toothree столбцов.

## <a name="bkmk_improvesessionbycode"></a>Улучшить представление SessionByCode hello
Наконец, можно исправить hello *SessionByCode* просмотра toomake его мобильной.

В браузере мобильного hello, коснитесь hello **тега** , а затем введите `asp` в поле поиска.

![][AllTagsFixedSearchByASP]

Коснитесь hello **ASP.NET** ссылку. Отображаются сеансы для тега ASP.NET hello.

![][FixedSessionsByTag]

Выберите hello **построение одностраничного приложения с помощью ASP.NET и AngularJS** ссылку.

![][SessionByCode3-644]

Представление рабочего стола по умолчанию Hello нормально, но можно улучшить вид hello легко с помощью некоторые компоненты начальной загрузки графического интерфейса пользователя.

Откройте *представления\\Главная\\SessionByCode.cshtml* и замените содержимое hello hello следующая разметка:

    @model Mvc5Mobile.Models.Session

    @{
        ViewBag.Title = "Session details";
    }
    <h3>@Model.Title (@Model.Code)</h3>
    <p>
        <strong>@Model.DateText</strong> in <strong>@Model.Room</strong>
    </p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Speakers
        </div>
        @foreach (var speaker in Model.Speakers)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class="panel-body" })
        }
    </div>

    <p>@Model.Abstract</p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Tags
        </div>
        @foreach (var tag in Model.Tags)
        {
            @Html.ActionLink(tag, 
                             "SessionsByTag", 
                             new { tag }, 
                             new { @class = "panel-body" })
        }
    </div>

Разметка нового Hello использует начальной загрузки панелей стиля tooimprove hello мобильного представления. 

Обновите hello мобильных браузеров. Hello рисунке отражает только что внесенные изменения кода hello:

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a>Заключение и сводка
Этого учебника было показано, как toouse ASP.NET MVC 5 toodevelop мобильные веб-приложений. В частности, описаны такие возможности:

* Развертывание tooan приложения ASP.NET MVC 5 веб-приложения служб приложений
* Используйте начальной загрузки toocreate отвечать на запросы веб-документа в приложении MVC 5
* переопределение макетов, представлений и частичных представлений, как глобально, так и для отдельного представления;
* управления макетом и принудительное частичное переопределение с помощью свойства `RequireConsistentDisplayMode`;
* Создание представлений, предназначенных для определенных обозревателей, например iPhone браузер hello
* применение стиля Bootstrap в коде Razor.

## <a name="see-also"></a>См. также
* [9 основных принципов динамического веб-дизайна](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* [Bootstrap][BootstrapSite]
* [Официальный блог о начальной загрузке][Official Bootstrap Blog]
* [Учебник по начальной загрузке Twitter от Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]
* [Hello площадки начальной загрузки][hello Bootstrap Playground]
* [Рекомендации от W3C по веб-приложениям для мобильных устройств][W3C Recommendation Mobile Web Application Best Practices]
* [Проектные рекомендации от W3C по запросам мультимедиа][W3C Candidate Recommendation for media queries]

## <a name="whats-changed"></a>Изменения
* Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- Internal Links -->
[Deploy hello starter project tooan Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override hello Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve hello Speakers List]: #bkmk_Improvespeakerslist
[Improve hello Tags List]: #bkmk_improvetags
[Improve hello Dates List]: #bkmk_improvedates
[Improve hello SessionsTable View]: #bkmk_improvesessionstable
[Improve hello SessionByCode View]: #bkmk_improvesessionbycode

<!-- External Links -->
[Visual Studio Express 2013]: http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-web
[Visual Studio 2015]: https://www.visualstudio.com/downloads/download-visual-studio-vs
[AzureSDKVs2013]: http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409
[Fiddler]: http://www.fiddler2.com/fiddler2/
[EmulatorIE11]: http://msdn.microsoft.com/library/ie/dn255001.aspx
[EmulatorChrome]: https://developers.google.com/chrome-developer-tools/docs/mobile-emulation
[EmulatorOpera]: http://www.opera.com/developer/tools/mobile/
[StarterProject]: http://go.microsoft.com/fwlink/?LinkID=398780&clcid=0x409
[CompletedProject]: http://go.microsoft.com/fwlink/?LinkID=398781&clcid=0x409
[BootstrapSite]: http://getbootstrap.com/
[WebPIAzureSdk23NetVS13]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/WebPIAzureSdk23NetVS13.png
[linked list group]: http://getbootstrap.com/components/#list-group-linked
[glyphicon]: http://getbootstrap.com/components/#glyphicons
[panels]: http://getbootstrap.com/components/#panels
[custom linked list group]: http://getbootstrap.com/components/#list-group-custom-content
[grid system]: http://getbootstrap.com/css/#grid
[responsive utilities]: http://getbootstrap.com/css/#responsive-utilities
[Official Bootstrap Blog]: http://blog.getbootstrap.com/
[Twitter Bootstrap Tutorial from Tutorial Republic]: http://www.tutorialrepublic.com/twitter-bootstrap-tutorial/
[hello Bootstrap Playground]: http://www.bootply.com/
[W3C Recommendation Mobile Web Application Best Practices]: http://www.w3.org/TR/mwabp/
[W3C Candidate Recommendation for media queries]: http://www.w3.org/TR/css3-mediaqueries/

<!-- Images -->
[DeployClickPublish]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-1.png
[DeployClickWebSites]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-2.png
[DeploySignIn]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-3.png
[DeployUsername]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-4.png
[DeployPassword]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-5.png
[DeployNewWebsite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-6.png
[DeploySiteSettings]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7.png
[DeployPublishSite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-8.png
[MobileHomePage]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/mobile-home-page.png
[FixedSessionsByTag]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-Fixed.png
[AllTags]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags.png
[SessionsByTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET.png
[SessionsByTagASP.NETNoBootstrap]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-NoBootstrap.png
[AllTagsMobile_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile.png
[AllTagsMobile_LayoutMobileDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile-Desktop.png
[ResolveDefaultDisplayMode]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/Resolve-DefaultDisplayMode.png
[AllTagsIPhone_LayoutIPhone]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsIPhone-_LayoutIPhone.png
[AllSpeakers_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile.png
[AllSpeakers_LayoutMobileOverridden]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile-Overridden.png
[AllSpeakersFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed.png
[AllSpeakersFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-Desktop.png
[AllSpeakersFixedSearchBySC]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-SearchBySC.png
[AllTagsFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-Desktop.png 
[AllTagsFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed.png
[AllDatesFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed.png
[AllDatesFixed2]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2.png
[AllDatesFixed2Desktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2-Desktop.png
[AllTagsFixedSearchByASP]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-SearchByASP.png
[SessionsTableTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Tag-ASP.NET.png
[SessionsTableFixedTagASP.NETDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Fixed-Tag-ASP.NET-Desktop.png
[SessionByCode3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-3-644.png
[SessionByCodeFixed3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-Fixed-3-644.png

