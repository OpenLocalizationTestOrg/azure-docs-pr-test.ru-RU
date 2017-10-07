---
title: "aaaIntegrate облачной службы Azure с Azure CDN | Документы Microsoft"
description: "Узнайте, как toodeploy облачной службы, служит содержимое из конечной точке integrated Azure CDN"
services: cdn, cloud-services
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: tysonn
ms.assetid: b3c0108f-9ec5-43a8-8fd0-40eafbd32637
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f20d60b0b5edc133adf06d010633a15f62e2b8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="intro"></a>Интеграция облачной службы с Azure CDN
Облачные службы могут интегрироваться с Azure CDN обслуживает все содержимое из расположения hello облачной службы. Этот подход обеспечивает hello следующие преимущества:

* Упрощение развертывания и обновления образов, скриптов и таблиц стилей в каталогах проекта облачной службы.
* Легко обновите пакеты NuGet hello в облачной службе, например jQuery или начальной загрузки версии
* Управление веб-приложения и обслуживаться CDN вашей содержимого всех hello же интерфейс Visual Studio
* Единый рабочий процесс развертывания для веб-приложения и контента, обслуживаемого CDN.
* Интеграция объединения и минификации ASP.NET с Azure CDN.

## <a name="what-you-will-learn"></a>Новые знания
Из этого учебника вы узнаете следующее:

* [Интеграция конечной точки Azure CDN с облачной службой и обслуживание статического содержимого на веб-страницах из Azure CDN](#deploy)
* [Настройка параметров кэша для статического содержимого в облачной службе](#caching)
* [Обслуживание содержимого из действий контроллера с помощью Azure CDN](#controller)
* [Serve объединено и уменьшена содержимого с помощью Azure CDN, сохраняя hello сценария отладки в Visual Studio](#bundling)
* [Настройка резервирования сценариев и CSS, когда Azure CDN находится в автономном режиме](#fallback)

## <a name="what-you-will-build"></a>Что будет строиться
Развертывание веб-роли облачной службы с помощью hello шаблон по умолчанию ASP.NET MVC, добавлять содержимое tooserve код из интеграции CDN Azure, такие как изображения, результаты действий контроллера и файлы JavaScript и CSS по умолчанию hello и также написать код tooconfigure hello резервный механизм для пакетов, выполненных в событии hello, hello CDN находится в автономном режиме.

## <a name="what-you-will-need"></a>Необходимые условия
Этот учебник содержит hello следующие предварительные требования:

* Активная [учетная запись Microsoft Azure](/account/)
* Наличие Visual Studio 2015 с [пакетом SDK Azure](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409)

> [!NOTE]
> Требуется учетная запись Azure toocomplete этого учебника:
> 
> * Вы можете [открыть учетную запись Azure бесплатно](https://azure.microsoft.com/pricing/free-trial/) -вы получаете кредиты можно использовать tootry out платных служб Azure и даже после того, они используются до можно защитить учетную запись hello и используйте освободить служб Azure, таких как веб-сайтов.
> * Вы имеете возможность [активировать преимущества подписчика MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) — ваша подписка MSDN каждый месяц приносит вам кредиты, которые можно использовать для оплаты за службы Azure.
> 
> 

<a name="deploy"></a>

## <a name="deploy-a-cloud-service"></a>Развертывание облачной службы
В этом разделе развертывания по умолчанию hello шаблона приложения ASP.NET MVC в Visual Studio 2015 tooa облака службы веб-роли и затем интегрировать ее с новой конечной точки CDN. Выполните приведенные ниже инструкции hello.

1. В Visual Studio 2015, создайте новой облачной службы Azure на панели меню hello выбрав слишком**файл > Создать > проект > облака > облачная служба Azure**. Назначьте ей имя и нажмите кнопку **ОК**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-1-new-project.PNG)
2. Выберите **веб-роли ASP.NET** и нажмите кнопку hello  **>**  кнопки. Нажмите кнопку ОК.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-2-select-role.PNG)
3. Выберите **MVC** и нажмите кнопку **ОК**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-3-mvc-template.PNG)
4. Теперь опубликуйте этот tooan роли Web облачной службы Azure. Щелкните правой кнопкой мыши проект облачной службы hello и выберите **публикации**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-4-publish-a.png)
5. Если вы еще не вошли в Microsoft Azure, щелкните hello **добавить учетную запись...**  hello раскрывающегося списка и нажмите кнопку **добавить учетную запись** элемента меню.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-5-publish-signin.png)
6. В hello страницы входа войдите с использованием hello учетной записи Майкрософт, используемых tooactivate учетной записью Azure.
7. После выполнения входа нажмите кнопку **Далее**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-6-publish-signedin.png)
8. Если облачная служба или учетная запись хранения еще не создана, Visual Studio поможет создать их. В hello **Создание облачной службы и учетной записи** диалогового окна, требуемой службы имя типа hello и hello выберите нужный регион. Затем щелкните **Создать**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-7-publish-createserviceandstorage.png)
9. Hello страница параметров публикации, проверьте конфигурацию hello и нажмите кнопку **публикации**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-cs-8-publish-finalize.png)
   
   > [!NOTE]
   > процесс публикации Hello для облачных служб занимает много времени. Hello включить веб-развертывание для всех ролей может сделать отладку намного быстрее, поскольку облачной службы, предоставляя tooyour быстрого (но временные) обновления веб-ролей. Дополнительные сведения об этом параметре см. в разделе [публикация облачной службы с помощью средства Azure hello](http://msdn.microsoft.com/library/ff683672.aspx).
   > 
   > 
   
    Здравствуйте, когда **журнал действий Microsoft Azure** показывает, что состояние публикации **завершено**, создании конечной точки CDN, которое интегрировано с этой облачной службы.
   
   > [!WARNING]
   > Если после публикации, hello развертывания облачной службы отображает экран ошибки, вполне вероятно, так как использует hello облачной службы после развертывания [гостевой ОС, которая не включает .NET 4.5.2](../cloud-services/cloud-services-guestos-update-matrix.md#news-updates).  Чтобы устранить эту проблему, [разверните .NET 4.5.2 в качестве задачи запуска](../cloud-services/cloud-services-dotnet-install-dotnet.md).
   > 
   > 

## <a name="create-a-new-cdn-profile"></a>Создание нового профиля сети CDN
Профиль сети CDN представляет собой коллекцию конечных точек сети CDN.  Каждый профиль содержит одну или несколько конечных точек сети CDN.  Вы можете toouse несколько профилей tooorganize конечными точками CDN с Интернет-домен, веб-приложения или некоторых других критериев.

> [!TIP]
> Если уже имеется профиль CDN, что требуется toouse для этого учебника, перейдите в слишком[создания новой конечной точки CDN](#create-a-new-cdn-endpoint).
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>Создание новой конечной точки сети CDN
**toocreate новой конечной точки CDN для вашей учетной записи**

1. В hello [портала управления Azure](https://portal.azure.com), перейдите tooyour профиля CDN.  Может закрепленной его toohello панели мониторинга в предыдущем шаге hello.  Если вы не, можно найти его, нажав кнопку **Обзор**, затем **CDN профилей**, и щелкнув профиля hello планируется tooadd для конечной точки.
   
    Откроется колонка профиля CDN Hello.
   
    ![Профиль сети CDN][cdn-profile-settings]
2. Нажмите кнопку hello **добавить конечную точку** кнопки.
   
    ![Кнопка "Добавить конечную точку"][cdn-new-endpoint-button]
   
    Hello **добавить конечную точку** колонке отображается.
   
    ![Колонка "Добавление конечной точки"][cdn-add-endpoint]
3. Введите **имя** конечной точки сети CDN.  Это имя будет использоваться tooaccess кэшированные ресурсы в домене hello `<EndpointName>.azureedge.net`.
4. В hello **тип источника** раскрывающийся список, выберите *облачная служба*.  
5. В hello **имя узла источника** раскрывающийся список, выберите вашу облачную службу.
6. Оставьте значения по умолчанию hello для **исходный путь**, **заголовок исходного узла**, и **порта протокола/источника**.  Необходимо указать хотя бы один протокол (HTTP или HTTPS).
7. Нажмите кнопку hello **добавить** toocreate кнопку hello новой конечной точки.
8. После создания конечной точки hello, он отображается в списке конечных точек для профиля hello. представления списка Hello показывает, что tooaccess toouse hello URL-адрес в кэше содержимого, а также hello исходный домен.
   
    ![Конечная точка сети CDN][cdn-endpoint-success]
   
   > [!NOTE]
   > Hello конечной точки не будет сразу же доступны для использования.  Он может занять too90 минут toopropagate hello регистрации через сеть CDN hello. Пользователям, пытающимся имени домена CDN hello toouse немедленно может появиться код состояния 404, пока не будет доступно через hello CDN hello содержимое.
   > 
   > 

## <a name="test-hello-cdn-endpoint"></a>Тест hello конечной точки CDN
При hello, статус публикации **завершено**, откройте окно браузера и перейдите слишком**http://<cdnName>*.azureedge.net/Content/bootstrap.css**. В моей настройке это следующий URL-адрес:

    http://camservice.azureedge.net/Content/bootstrap.css

Соответствующий URL-адреса источника в конечной точке CDN hello toohello:

    http://camcdnservice.cloudapp.net/Content/bootstrap.css

При переходе слишком**http://*&lt;cdnName >*.azureedge.net/Content/bootstrap.css**, в зависимости от браузера будет toodownload запрос или откройте hello bootstrap.css, откуда опубликованных веб-приложения.

![](media/cdn-cloud-service-with-cdn/cdn-1-browser-access.PNG)

Аналогичным образом можно получать доступ к любому общедоступному URL-адресу в **http://*&lt;serviceName>*.cloudapp.net/** прямо из конечной точки CDN. Например:

* JS-файла из пути/Script hello
* Любой файл содержимого из hello /Content путь
* к любому контроллеру или действию;
* Если строка запроса hello включен на конечную точку CDN, любой URL-адрес со строками запроса

На самом деле с hello выше конфигурации, можно разместить hello всей облачной службы из  **http://*&lt;cdnName >*.azureedge.net/**. Если после выхода слишком**http://camservice.azureedge.net/ ** получить результат действия hello из дома или индекса.

![](media/cdn-cloud-service-with-cdn/cdn-2-home-page.PNG)

Это означает, тем не менее, что это всегда рекомендуется tooserve всей облачной службы через Azure CDN. 

CDN с оптимизацией статических доставки не обязательно ускорять доставки динамических средств, которые предназначены не кэшируются toobe или очень часто обновляются, поскольку hello CDN необходимо получить новую версию средств hello из исходного сервера hello очень часто. В этом сценарии можно включить [динамического сайта ускорение](cdn-dynamic-site-acceleration.md) оптимизации (DSA) в вашей конечной точке CDN, который использует различные методы toospeed параметров представления кэширование динамических средств. 

При наличии сайта с сочетание статического и динамического содержимого, вы можете tooserve статическое содержимое из CDN с типом статической оптимизации (например, доставка общие web) и динамического содержимого tooserve непосредственно из исходного сервера hello или через CDN Конечная точка с включенной по случая оптимизацией DSA. конец toothat уже было показано, как содержимое отдельных tooaccess файлы из конечной точки CDN hello. Будет показано как tooserve действие конкретного контроллера до конкретной конечной точки CDN в стать содержимого из действия контроллера через Azure CDN.

Hello альтернативой является toodetermine которого содержимого tooserve из сети доставки Содержимого Azure на основе случая в облачной службе. конец toothat уже было показано, как содержимое отдельных tooaccess файлы из конечной точки CDN hello. Будет показано как tooserve действие конкретному контроллеру через hello конечной точки CDN в [обслуживания содержимого из действия контроллера через Azure CDN](#controller).

<a name="caching"></a>

## <a name="configure-caching-options-for-static-files-in-your-cloud-service"></a>Настройка параметров кэширования для статических файлов в облачной службе
Благодаря интеграции Azure CDN в облачной службе можно указать способ статического содержимого toobe кэширования в конечной точке CDN hello. toodo, откройте *Web.config* из веб-роли проекта (например, WebRole1) и добавьте `<staticContent>` элемент слишком`<system.webServer>`. Hello XML ниже настраивает tooexpire hello кэша через 3 дня.  

    <system.webServer>
      <staticContent>
        <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00"/>
      </staticContent>
      ...
    </system.webServer>

После этого все статические файлы в облачной службе будет контролироваться hello же правило в кэше CDN. Для более детального управления параметрами кэша добавьте файл *Web.config* в папку и добавьте в этом месте свои параметры. Например, добавить *Web.config* файл toohello *\Content* папки и замены hello содержимое с hello следующий XML-код:

    <?xml version="1.0"?>
    <configuration>
      <system.webServer>
        <staticContent>
          <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="15.00:00:00"/>
        </staticContent>
      </system.webServer>
    </configuration>

Этот параметр вызывает все статические файлы из hello *\Content* toobe папки в кэше в течение 15 дней.

Дополнительные сведения о том, как tooconfigure hello `<clientCache>` элемент, в разделе [кэш клиента &lt;clientCache >](http://www.iis.net/configreference/system.webserver/staticcontent/clientcache).

В [обслуживания содержимого из действия контроллера через Azure CDN](#controller), будет также показано как можно настроить параметры кэша для результатов действий контроллера в hello кэша CDN.

<a name="controller"></a>

## <a name="serve-content-from-controller-actions-through-azure-cdn"></a>Обслуживание содержимого из действий контроллера с помощью Azure CDN
При интеграции веб-роли облачной службы с Azure CDN, это довольно просто tooserve содержимое из действия контроллера через hello Azure CDN. Кроме обслуживающий облачной службы напрямую с помощью сети доставки Содержимого Azure (показано выше), [Maarten Balliauw](https://twitter.com/maartenballiauw) показано, как toodo его с интересную MemeGenerator контроллера в [уменьшает задержку на веб-hello с hello Azure CDN ](http://channel9.msdn.com/events/TechDays/Techdays-2014-the-Netherlands/Reducing-latency-on-the-web-with-the-Windows-Azure-CDN). Я просто воспроизведу это здесь.

Предположим, что в облачную службу нужно на основе образа молодых Norris Чак memes toogenerate (фотографий с [свет Алан](http://www.flickr.com/photos/alan-light/218493788/)) следующим образом:

![](media/cdn-cloud-service-with-cdn/cdn-5-memegenerator.PNG)

У вас есть простой `Index` действие, которое позволяет клиентам hello toospecify hello superlatives в образе hello, затем создает мем hello после их toohello действий, выполняемых после. Так как это Norris Чак, можно ожидать этой страницы toobecome очень популярных глобально. Это хороший пример обслуживания полудинамического контента с помощью Azure CDN.

Выполните действия hello выше toosetup этого действия контроллера.

1. В hello *\Controllers* папки, создайте новый файл с именем .cs *MemeGeneratorController.cs* и hello замены содержимого с hello следующий код. Убедиться, что выделенный фрагмент hello tooreplace быть именем своего CDN.  
   
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.Drawing;
        using System.IO;
        using System.Net;
        using System.Web.Hosting;
        using System.Web.Mvc;
        using System.Web.UI;
   
        namespace WebRole1.Controllers
        {
            public class MemeGeneratorController : Controller
            {
                static readonly Dictionary<string, Tuple<string ,string>> Memes = new Dictionary<string, Tuple<string, string>>();
   
                public ActionResult Index()
                {
                    return View();
                }
   
                [HttpPost, ActionName("Index")]
                public ActionResult Index_Post(string top, string bottom)
                {
                    var identifier = Guid.NewGuid().ToString();
                    if (!Memes.ContainsKey(identifier))
                    {
                        Memes.Add(identifier, new Tuple<string, string>(top, bottom));
                    }
   
                    return Content("<a href=\"" + Url.Action("Show", new {id = identifier}) + "\">here's your meme</a>");
                }
   
                [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
                public ActionResult Show(string id)
                {
                    Tuple<string, string> data = null;
                    if (!Memes.TryGetValue(id, out data))
                    {
                        return new HttpStatusCodeResult(HttpStatusCode.NotFound);
                    }
   
                    if (Debugger.IsAttached) // Preserve hello debug experience
                    {
                        return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                    else // Get content from Azure CDN
                    {
                        return Redirect(string.Format("http://<yourCdnName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
                    }
                }
   
                [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]
                public ActionResult Generate(string top, string bottom)
                {
                    string imageFilePath = HostingEnvironment.MapPath("~/Content/chuck.bmp");
                    Bitmap bitmap = (Bitmap)Image.FromFile(imageFilePath);
   
                    using (Graphics graphics = Graphics.FromImage(bitmap))
                    {
                        SizeF size = new SizeF();
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, top.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(top.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), 10f));
                        }
                        using (Font arialFont = FindBestFitFont(bitmap, graphics, bottom.ToUpperInvariant(), new Font("Arial Narrow", 100), out size))
                        {
                            graphics.DrawString(bottom.ToUpperInvariant(), arialFont, Brushes.White, new PointF(((bitmap.Width - size.Width) / 2), bitmap.Height - 10f - arialFont.Height));
                        }
                    }
   
                    MemoryStream ms = new MemoryStream();
                    bitmap.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    return File(ms.ToArray(), "image/png");
                }
   
                private Font FindBestFitFont(Image i, Graphics g, String text, Font font, out SizeF size)
                {
                    // Compute actual size, shrink if needed
                    while (true)
                    {
                        size = g.MeasureString(text, font);
   
                        // It fits, back out
                        if (size.Height < i.Height &&
                             size.Width < i.Width) { return font; }
   
                        // Try a smaller font (90% of old size)
                        Font oldFont = font;
                        font = new Font(font.Name, (float)(font.Size * .9), font.Style);
                        oldFont.Dispose();
                    }
                }
            }
        }
2. Щелкните правой кнопкой мыши по умолчанию hello `Index()` , можно выбрать **добавить представление**.
   
    ![](media/cdn-cloud-service-with-cdn/cdn-6-addview.PNG)
3. Примите следующие параметры hello и нажмите кнопку **добавить**.
   
   ![](media/cdn-cloud-service-with-cdn/cdn-7-configureview.PNG)
4. Откройте hello новый *Views\MemeGenerator\Index.cshtml* и замените содержимое hello hello, следуя простой HTML для отправки hello superlatives:
   
        <h2>Meme Generator</h2>
   
        <form action="" method="post">
            <input type="text" name="top" placeholder="Enter top text here" />
            <br />
            <input type="text" name="bottom" placeholder="Enter bottom text here" />
            <br />
            <input class="btn" type="submit" value="Generate meme" />
        </form>
5. Снова опубликовать облачную службу hello и перейдите слишком**http://*&lt;serviceName >*.cloudapp.net/MemeGenerator/Index** в браузере.

При отправке значения формы hello слишком`/MemeGenerator/Index`, hello `Index_Post` метод действия возвращает toohello ссылку `Show` метод действия с hello соответствующий идентификатор входа. Если щелкнуть ссылку hello, достигнете hello, следующий код:  

    [OutputCache(VaryByParam = "*", Duration = 1, Location = OutputCacheLocation.Downstream)]
    public ActionResult Show(string id)
    {
        Tuple<string, string> data = null;
        if (!Memes.TryGetValue(id, out data))
        {
            return new HttpStatusCodeResult(HttpStatusCode.NotFound);
        }

        if (Debugger.IsAttached) // Preserve hello debug experience
        {
            return Redirect(string.Format("/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
        else // Get content from Azure CDN
        {
            return Redirect(string.Format("http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top={0}&bottom={1}", data.Item1, data.Item2));
        }
    }

Если ваш локальный отладчик подключен, вы получите hello интерфейса регулярного отладки с помощью локального перенаправления. Если он выполняется в облачной службе hello, затем он будет перенаправить на:

    http://<yourCDNName>.azureedge.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>

Соответствующее toohello следующий URL-адрес источника в конечную точку CDN:

    http://<youCloudServiceName>.cloudapp.net/MemeGenerator/Generate?top=<formInput>&bottom=<formInput>


Затем можно использовать hello `OutputCacheAttribute` атрибут hello `Generate` toospecify метод кэширования hello результат действия, который будет поддерживать Azure CDN. Приведенный ниже код Hello задать истечение срока действия кэша 1 часа (3600 секунд).

    [OutputCache(VaryByParam = "*", Duration = 3600, Location = OutputCacheLocation.Downstream)]

Аналогичным образом вы может служить содержимое из любого действия контроллера в облачной службе через CDN Azure, с hello требуемого параметр кэширования.

В следующем разделе hello я покажу как tooserve hello объединенными и уменьшена скриптов и CSS через Azure CDN.

<a name="bundling"></a>

## <a name="integrate-aspnet-bundling-and-minification-with-azure-cdn"></a>Интеграция объединения и минификации ASP.NET с Azure CDN.
Таблицы стилей, сценарии и CSS подскажет и основной подходят для hello кэша Azure CDN. Обслуживание hello весь веб-роли через Azure CDN — самый простой способ toointegrate hello объединение и Минификация с Azure CDN. Тем не менее как вы не можете toodo это, будет показано как toodo его сохранением hello требуемого develper взаимодействие с ASP.NET объединение и Минификация, такие как:

* Отличное взаимодействие в режиме отладки.
* Упрощенное развертывание.
* Tooclients немедленного обновления для обновления версий скриптов и CSS
* Резервный механизм на случай сбоя конечной точки CDN.
* Минимальное изменение кода.

В hello **WebRole1** проекта, созданного в [интегрировать веб-сайте конечной точки Azure CDN и предоставления статического содержимого на веб-страницах из сети доставки Содержимого Azure](#deploy)откройте *App_Start\ BundleConfig.cs* и взгляните на hello `bundles.Add()` вызовы методов.

    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                    "~/Scripts/jquery-{version}.js"));
        ...
    }

Здравствуйте, сначала `bundles.Add()` инструкция добавляет пакет скрипта в виртуальный каталог hello `~/bundles/jquery`. Затем откройте *представления\общие\_Layout.cshtml* toosee просмотру hello тег пакета. Необходимо будет toofind hello, следующей строкой кода Razor.

    @Scripts.Render("~/bundles/jquery")

При выполнении этого кода Razor в hello Azure веб-роли, он будет отображать `<script>` тег для hello скрипт аналогичные toohello следующий пакет:

    <script src="/bundles/jquery?v=FVs3ACwOLIVInrAl5sdzR2jrCDmVOWFbZMY6g6Q0ulE1"></script>

Тем не менее, при запуске в Visual Studio, введя `F5`, он будет отображать каждого файла скрипта в пакет hello по отдельности (в случае hello выше, только один файл скрипта находится в пакет hello):

    <script src="/Scripts/jquery-1.10.2.js"></script>

Это позволит вам код JavaScript toodebug hello в среде разработки во время сократить число одновременных клиентских подключений (объединение) и файл повышение загрузки производительности (минификации) в рабочей среде. Это прекрасная возможность toopreserve с интеграцией Azure CDN. Кроме того, так как к просмотру hello пакет уже содержит автоматически созданную версию строки, вы найдете tooreplicate, функциональные возможности hello, поэтому всякий раз при обновлении версии jQuery через NuGet, его можно обновить на стороне клиента hello как можно скорее невозможно.

Выполните действия hello ниже toointegration ASP.NET объединение и Минификация с конечной точкой CDN.

1. Обратно в *App_Start\BundleConfig.cs*, изменить hello `bundles.Add()` toouse методы другой [конструктор пакета](http://msdn.microsoft.com/library/jj646464.aspx), один задает адрес CDN. toodo, замените hello `RegisterBundles` определения метода с hello, следующий код:  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            bundles.UseCdn = true;
            var version = System.Reflection.Assembly.GetAssembly(typeof(Controllers.HomeController))
                .GetName().Version.ToString();
            var cdnUrl = "http://<yourCDNName>.azureedge.net/{0}?v=" + version;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery")).Include(
                        "~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval")).Include(
                        "~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you're
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer")).Include(
                        "~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap")).Include(
                        "~/Scripts/bootstrap.js",
                        "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    Убедиться, что tooreplace быть `<yourCDNName>` с именем hello Azure CDN.
   
    Своими словами, вы настраиваете `bundles.UseCdn = true` и добавлен набор tooeach аккуратно созданные URL-адрес CDN. Например hello первый конструктор в коде hello:
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
   
    hello такой же, как:
   
        new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "http://<yourCDNName>.azureedge.net/bundles/jquery?v=<W.X.Y.Z>"))
   
    Этот конструктор сообщает ASP.NET объединение и Минификация toorender конкретные файлы сценариев при отладке локально, но использование hello указан CDN адрес tooaccess hello скрипта в вопросе. Однако отметим две важных характеристики этого тщательно созданного URL-адреса CDN.
   
   * Hello источник для этого URL-адрес CDN: `http://<yourCloudService>.cloudapp.net/bundles/jquery?v=<W.X.Y.Z>`, который является фактически hello виртуального каталога пакет сценария hello в облачной службе.
   * Так как вы используете конструктор CDN, hello тега script CDN для пакета hello больше не содержит строку версии hello автоматически создается в hello, просмотру URL-адрес. Необходимо вручную создать строку уникальной версии каждый раз пакет сценария hello измененный tooforce промахом кэша в Azure CDN. AT hello же времени, эта строка уникальной версии должны оставаться постоянным объемах hello попаданий в кэш toomaximize hello развертывания в вашей сети доставки Содержимого Azure после развертывания пакета hello.
   * Здравствуйте, строки запроса v = < W.X.Y.Z > переносит из *Properties\AssemblyInfo.cs* в проект веб-роли. Рабочий процесс развертывания, включающий увеличение версии сборки hello при каждой публикации tooAzure может иметь. Либо можно просто изменить *Properties\AssemblyInfo.cs* в строке версии проекта tooautomatically приращения hello каждый раз при построении с помощью hello подстановочный знак "*". Например:
     
        [assembly: AssemblyVersion("1.0.0.*")]
     
     Здесь будут работать другие toostreamline стратегии, создания уникальной строки для hello жизненного цикла развертывания.
2. Повторная публикация hello облачной службы и доступ hello домашнюю страницу.
3. Здравствуйте, представление кода HTML для страницы приветствия. Должно быть hello может toosee URL-адрес CDN к просмотру со строкой уникальной версии каждый раз при повторной публикации изменений tooyour облачной службы. Например:  
   
        ...
   
        <link href="http://camservice.azureedge.net/Content/css?v=1.0.0.25449" rel="stylesheet"/>
   
        <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25449"></script>
   
        ...
   
        <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25449"></script>
   
        <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25449"></script>
   
        ...
4. В Visual Studio отлаживать hello облачной службы в Visual Studio, введя `F5`.,
5. Здравствуйте, представление кода HTML для страницы приветствия. Вы по-прежнему будете видеть каждый, индивидуально обработанный файл скрипта, так что можно получить последовательные возможности отладки в Visual Studio.  
   
        ...
   
            <link href="/Content/bootstrap.css" rel="stylesheet"/>
        <link href="/Content/site.css" rel="stylesheet"/>
   
            <script src="/Scripts/modernizr-2.6.2.js"></script>
   
        ...
   
            <script src="/Scripts/jquery-1.10.2.js"></script>
   
            <script src="/Scripts/bootstrap.js"></script>
        <script src="/Scripts/respond.js"></script>
   
        ...   

<a name="fallback"></a>

## <a name="fallback-mechanism-for-cdn-urls"></a>Резервный механизм для URL-адресов CDN
Конечная точка Azure CDN завершается ошибкой по любой причине, их нужно вашей веб-странице toobe смарт-недостаточно tooaccess на исходном веб-сервере как hello резервный вариант для загрузки JavaScript или начальной загрузки. Это достаточно серьезной toolose изображений на веб-сайт из-за недоступности tooCDN, но гораздо более серьезные toolose важные страницы, предоставляемой средой скриптов и таблиц стилей.

Hello [пакета](http://msdn.microsoft.com/library/system.web.optimization.bundle.aspx) класс содержит свойство с именем [CdnFallbackExpression](http://msdn.microsoft.com/library/system.web.optimization.bundle.cdnfallbackexpression.aspx) , которые позволяют tooconfigure hello резервный механизм для сбоя CDN. toouse это свойство, выполните следующие действия hello:

1. В проекте веб-роли откройте *App_Start\BundleConfig.cs*, где вы добавили URL-адрес CDN в каждом [конструктор пакета](http://msdn.microsoft.com/library/jj646464.aspx)и сделать выделенный ниже hello изменяет toohello резервный механизм tooadd по умолчанию пакеты:  
   
        public static void RegisterBundles(BundleCollection bundles)
        {
            var version = System.Reflection.Assembly.GetAssembly(typeof(BundleConfig))
                .GetName().Version.ToString();
            var cdnUrl = "http://cdnurl.azureedge.net/.../{0}?" + version;
            bundles.UseCdn = true;
   
            bundles.Add(new ScriptBundle("~/bundles/jquery", string.Format(cdnUrl, "bundles/jquery"))
                        { CdnFallbackExpression = "window.jquery" }
                        .Include("~/Scripts/jquery-{version}.js"));
   
            bundles.Add(new ScriptBundle("~/bundles/jqueryval", string.Format(cdnUrl, "bundles/jqueryval"))
                        { CdnFallbackExpression = "$.validator" }
                        .Include("~/Scripts/jquery.validate*"));
   
            // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
            // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
            bundles.Add(new ScriptBundle("~/bundles/modernizr", string.Format(cdnUrl, "bundles/modernizer"))
                        { CdnFallbackExpression = "window.Modernizr" }
                        .Include("~/Scripts/modernizr-*"));
   
            bundles.Add(new ScriptBundle("~/bundles/bootstrap", string.Format(cdnUrl, "bundles/bootstrap"))     
                        { CdnFallbackExpression = "$.fn.modal" }
                        .Include(
                                  "~/Scripts/bootstrap.js",
                                  "~/Scripts/respond.js"));
   
            bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css")).Include(
                        "~/Content/bootstrap.css",
                        "~/Content/site.css"));
        }
   
    Когда `CdnFallbackExpression` — не равно null, скрипт вставляется в tootest hello HTML ли успешно загружен пакет hello и, в противном случае доступ к hello пакета непосредственно из hello исходном веб-сервере. Это свойство должно toobe набор tooa выражение JavaScript, которое проверяет, является ли hello соответствующих CDN пакета загружается надлежащим образом. выражение Hello необходимости tootest соответствующим toohello содержимого отличается в каждом пакете. Для пакетов по умолчанию hello выше:
   
   * `window.jquery` задается в jquery-{version}.js
   * `$.validator` задается в jquery.validate.js;
   * `window.Modernizr` задается в modernizer-{version}.js;
   * `$.fn.modal` задается в bootstrap.js.
     
     Вы могли заметить, что я не задано CdnFallbackExpression для hello `~/Cointent/css` пакета. Это, поскольку в настоящее время имеется [ошибку в System.Web.Optimization](https://aspnetoptimization.codeplex.com/workitem/104) , внедряет `<script>` тег для hello ожидается резервной CSS вместо hello `<link>` тег.
     
     Однако существует хорошая [резервная форма пакета стилей](https://github.com/EmberConsultingGroup/StyleBundleFallback), предлагаемая [Ember Consulting Group](https://github.com/EmberConsultingGroup).
2. возможное решение hello toouse для CSS, создайте новый CS-файл в проект веб-роли *App_Start* папку с именем *StyleBundleExtensions.cs*и замените его содержимое hello [код из GitHub](https://github.com/EmberConsultingGroup/StyleBundleFallback/blob/master/Website/App_Start/StyleBundleExtensions.cs).
3. В *App_Start\StyleFundleExtensions.cs*, переименовать tooyour веб-приветствия имен роли (например **WebRole1**).
4. Возврат слишком`App_Start\BundleConfig.cs` и последнего изменения hello `bundles.Add` инструкции с hello следующий выделенный код:  
   
        bundles.Add(new StyleBundle("~/Content/css", string.Format(cdnUrl, "Content/css"))
            <mark>.IncludeFallback("~/Content/css", "sr-only", "width", "1px")</mark>
            .Include(
                  "~/Content/bootstrap.css",
                  "~/Content/site.css"));
   
    Этот новый метод расширения используется hello же идеи tooinject сценария в DOM hello toocheck hello HTML для hello соответствующим именем класса, имя правила и значение правила, определенные в CSS пакета hello и Web приходится задней toohello исходного сервера в случае неудачи toofind hello соответствия.
5. Опубликуйте снова hello облачную службу и доступ hello домашней страницы.
6. Здравствуйте, представление кода HTML для страницы приветствия. Вы должны найти примерно следующие toohello подставляемого сценариев:    
   
        ...
   
        <link href="http://az632148.azureedge.net/Content/css?v=1.0.0.25474" rel="stylesheet"/>
        <script>(function() {
                        var loadFallback,
                            len = document.styleSheets.length;
                        for (var i = 0; i < len; i++) {
                            var sheet = document.styleSheets[i];
                            if (sheet.href.indexOf('http://camservice.azureedge.net/Content/css?v=1.0.0.25474') !== -1) {
                                var meta = document.createElement('meta');
                                meta.className = 'sr-only';
                                document.head.appendChild(meta);
                                var value = window.getComputedStyle(meta).getPropertyValue('width');
                                document.head.removeChild(meta);
                                if (value !== '1px') {
                                    document.write('<link href="/Content/css" rel="stylesheet" type="text/css" />');
                                }
                            }
                        }
                        return true;
                    }())||document.write('<script src="/Content/css"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/modernizer?v=1.0.0.25474"></script>
        <script>(window.Modernizr)||document.write('<script src="/bundles/modernizr"><\/script>');</script>
   
        ...
   
            <script src="http://camservice.azureedge.net/bundles/jquery?v=1.0.0.25474"></script>
        <script>(window.jquery)||document.write('<script src="/bundles/jquery"><\/script>');</script>
   
            <script src="http://camservice.azureedge.net/bundles/bootstrap?v=1.0.0.25474"></script>
        <script>($.fn.modal)||document.write('<script src="/bundles/bootstrap"><\/script>');</script>
   
        ...

    Обратите внимание, что внедренный сценарий для пакета hello CSS по-прежнему содержит hello умыслу оставшейся из hello `CdnFallbackExpression` свойства в строке приветствия:

        }())||document.write('<script src="/Content/css"><\/script>');</script>

    Но, поскольку первая часть hello hello || выражение всегда будет возвращать значение true (в строке приветствия непосредственно над ней), функция document.write() hello никогда не будет работать.

## <a name="more-information"></a>Дополнительные сведения
* [Общие сведения о hello Azure доставки содержимого сети (CDN)](http://msdn.microsoft.com/library/azure/ff919703.aspx)
* [Использование Azure CDN](cdn-create-new-endpoint.md)
* [Объединение и минификация ASP.NET](http://www.asp.net/mvc/tutorials/mvc-4/bundling-and-minification)

[new-cdn-profile]: ./media/cdn-cloud-service-with-cdn/cdn-new-profile.png
[cdn-profile-settings]: ./media/cdn-cloud-service-with-cdn/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-cloud-service-with-cdn/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-cloud-service-with-cdn/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-cloud-service-with-cdn/cdn-endpoint-success.png
