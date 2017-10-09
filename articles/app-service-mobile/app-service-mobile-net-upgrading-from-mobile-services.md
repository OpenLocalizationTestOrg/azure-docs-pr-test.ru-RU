---
title: "aaaUpgrade из мобильных служб tooAzure службы приложений"
description: "Узнайте, как tooeasily обновление вашего tooan приложения мобильных служб приложение службы мобильных приложений"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 9c0ac353-afb6-462b-ab94-d91b8247322f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 2b75a1b824e8ef0d36c9053f2f19af051479f928
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-existing-net-azure-mobile-service-tooapp-service"></a>Обновление вашей существующей мобильной службы .NET Azure tooApp службы
Мобильные приложения службы-это новый способ toobuild мобильных приложений с помощью Microsoft Azure. toolearn более, в разделе [Каковы мобильные приложения?].

В этом разделе описывается способ tooupgrade существующее приложение серверной части .NET из мобильных служб Azure tooa новые мобильные приложения службы приложений. При выполнении этого обновления существующего приложения мобильных служб можно продолжить toooperate.   Если вам требуется tooupgrade Node.js внутреннее приложение, см. слишком[обновление мобильных служб Node.js](app-service-mobile-node-backend-upgrading-from-mobile-services.md).

Когда мобильной серверной части tooAzure обновленной службы приложений, он имеет доступ tooall функции службы приложений и являются выставлен счет на слишком в соответствии с[служб приложений Ценовая], цены не мобильных служб.

## <a name="migrate-vs-upgrade"></a>Миграция или обновление
[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

> [!TIP]
> Перед обновлением рекомендуется [выполнить миграцию](app-service-mobile-migrating-from-mobile-services.md) . Таким образом, можно поместить обе версии приложения hello же план службы приложений и создают без дополнительных затрат.
>
>

### <a name="improvements-in-mobile-apps-net-server-sdk"></a>Улучшения в пакете SDK сервера .NET мобильных приложений
Обновление нового toohello [пакет SDK для мобильных приложений](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) предоставляет hello следующие преимущества:

* Дополнительная гибкость для зависимостей NuGet. Hello, среда размещения больше не предоставляет собственные версии пакетов NuGet, чтобы можно было использовать альтернативные совместимые версии. Если имеются новые критические bugfixes или toohello обновлений безопасности SDK сервера мобильных или зависимости, службы необходимо обновить вручную.
* Более гибкие возможности hello SDK для мобильных устройств. Явно управлять тем, какие компоненты и маршруты настраиваются, такие как проверка подлинности, API-интерфейсы, таблицы и hello конечной точке регистрации push. toolearn более, в разделе [как toouse hello .NET server SDK для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).
* Поддержка других маршрутов и типов проектов ASP.NET. Теперь можно размещать контроллеров MVC и веб-API в hello же проект как проект мобильной серверной части.
* Поддержка новой функции проверки подлинности службы приложений, позволяющих toouse общую конфигурацию проверки подлинности между веб- и мобильных приложений.

## <a name="overview"></a>Общие сведения об обновлении
Во многих случаях обновление будет таким же простым, как переключение toohello новые мобильные приложения SDK сервера, а также переиздание кода на новый экземпляр мобильного приложения. Однако существует несколько сценариев, в которых потребуется дополнительная настройка, например расширенные сценарии проверки подлинности и работа с запланированными заданиями. Каждый из них рассматривается hello далее разделах.

> [!TIP]
> Рекомендуется прочитать и полностью понимать hello остальной части этого раздела до начала обновления. Запишите все используемые функции, которые вызываются ниже.
>
>

Hello клиента мобильных служб, пакеты SDK **не** совместимой с сервером новые мобильные приложения hello SDK. Непрерывность tooprovide порядок службу для своего приложения не следует публиковать изменения tooa сайта в настоящее время обслуживая клиентов, опубликованной. Вместо этого нужно создать новое мобильное приложение, которое является дубликатом. Можно поместить это приложение hello же приложение службы плана tooavoid дополнительных финансовых затрат.

Затем имеется две версии приложения hello: один какие остается таким же hello и служит опубликованные приложения hello подстановки и hello в другой, которую затем можно обновить и целевой с новым выпуском клиента. Можно перемещать и тестирования кода в темпе, но следует убедиться в том, все исправления, внесенные get примененных tooboth. Если вы считаете, что требуемое число клиентских приложений в hello подстановки обновили toohello последней версии, при желании можно удалить исходный перенесенные приложение hello.

Hello полной структуры для hello процесс обновления выглядит следующим образом:

1. Создание нового мобильного приложения.
2. Обновление hello проекта toouse hello новых пакетов SDK сервера
3. Выпуск новой версии клиентского приложения.
4. (Необязательно) Удаление исходного перенесенного экземпляра миграции

## <a name="mobile-app-version"></a>Создание второго экземпляра приложения
Hello первым шагом при обновлении является toocreate hello мобильное приложение ресурса, который будет размещаться новая версия приложения hello. Если вы уже перенесли существующую мобильную службу, можно toocreate эту версию на hello же плана размещения. Откройте hello [портал Azure] и перейдите tooyour миграции приложения. Запишите hello план службы приложений, он выполняется.

Затем нужно создать второй экземпляр приложения hello, следующие hello [инструкции создания серверной части .NET](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app). Когда запрос tooselect выбрать план служб приложений или «план размещения» hello план миграции приложения.

Скорее всего, вы будете toouse hello одной базе данных и концентратор уведомлений, как вы делали на мобильных служб. Эти значения можно скопировать, открыв [портал Azure] и перемещение toohello исходного приложения, нажмите кнопку **параметры** > **параметры приложения**. В разделе **Строки подключения** скопируйте `MS_NotificationHubConnectionString` и `MS_TableConnectionString`. Перейдите tooyour нового обновления сайта и вставьте их на сервер, перезаписывая все существующие значения. Повторите эту процедуру для других необходимых параметров приложения. Если не используется перенесенной службы, можно считывать строки подключения и параметры приложения из hello **Настройка** вкладка hello мобильных служб раздел hello [классический портал Azure].

Создайте копию hello проекта ASP.NET для приложения и опубликовать его tooyour новый сайт. Используя копию клиентское приложение обновляется hello новый URL-адрес, проверьте, что все работает правильно.

## <a name="updating-hello-server-project"></a>Обновление проекта сервера hello
Мобильные приложения предоставляет новый [пакет SDK для мобильных приложений сервера] которого содержится значительная часть hello функциональных возможностей среды выполнения hello мобильных служб. Во-первых необходимо удалить все пакеты для мобильных служб toohello ссылки. В диспетчере пакетов NuGet hello, поиск `WindowsAzure.MobileServices.Backend`. Для большинства пакетов здесь будет отображаться несколько пакетов, включая `WindowsAzure.MobileServices.Backend.Tables` и `WindowsAzure.MobileServices.Backend.Entity`. В этом случае запустите с наименьшим пакета hello в дереве зависимостей hello, например `Entity`и удалите его. При выводе запроса не удаляйте все зависимые пакеты. Повторяйте этот процесс, пока не будет удален сам `WindowsAzure.MobileServices.Backend` .

На этом этапе в вашем распоряжении будет находиться проект, который больше не ссылается на пакеты SDK мобильных служб.

Мы добавим hello ссылки на пакет SDK для мобильных приложений. Для этого обновления, большинство разработчиков будет toodownload и установить hello `Microsoft.Azure.Mobile.Server.Quickstart` пакета, как это будет опрашивать в hello весь необходимый набор.

Будет довольно много ошибки компилятора, возникающие из-за различий между hello пакеты SDK, но это просто tooaddress, охваченных hello оставшейся части этого раздела.

### <a name="base-configuration"></a>Базовая конфигурация
Затем в файле WebApiConfig.cs можно заменить

        // Use this class tooset configuration options for your mobile service
        ConfigOptions options = new ConfigOptions();

        // Use this class tooset WebAPI configuration options
        HttpConfiguration config = ServiceConfig.Initialize(new ConfigBuilder(options));

на

        HttpConfiguration config = new HttpConfiguration();
        new MobileAppConfiguration()
            .UseDefaultConfiguration()
        .ApplyTo(config);

> [!NOTE]
> Если вы хотите toolearn подробные сведения о новом сервере .NET SDK hello и как функции tooadd или удалить из приложения, см. в разделе hello [как toouse hello .NET server SDK] раздела.
>
>

Если приложение позволяет использовать функции hello проверки подлинности, необходимо также tooregister по промежуточного слоя OWIN. В этом случае следует перемещать hello выше код конфигурации в новый класс запуска OWIN.

1. Добавьте пакет NuGet hello `Microsoft.Owin.Host.SystemWeb` , если он уже не включен в проект.
2. В Visual Studio щелкните правой кнопкой мыши проект и последовательно выберите **Добавить** -> **Новый элемент**. Выберите **Интернет** -> **Общие** -> **Класс Startup OWIN**.
3. Переместить hello над кодом для MobileAppConfiguration из `WebApiConfig.Register()` toohello `Configuration()` метод запуска нового класса.

Убедитесь, что hello `Configuration()` заканчивается метод:

        app.UseWebApi(config)
        app.UseAppServiceAuthentication(config);

Существуют дополнительные изменения связанных tooauthentication рассматривается в разделе полная проверка подлинности hello ниже.

### <a name="working-with-data"></a>Работа с данными
В мобильных службах имя мобильное приложение hello предоставлена как имя схемы по умолчанию hello в программе установки hello Entity Framework.

tooensure, у вас есть hello же схемы адресуемым как раньше hello используется следующая схема tooset hello в hello DbContext для приложения:

        string schema = System.Configuration.ConfigurationManager.AppSettings.Get("MS_MobileServiceName");

Убедитесь, что у вас есть набор, если hello выше MS_MobileServiceName. Если имя схемы в приложении было настроено ранее, можно также указать другое имя.

### <a name="system-properties"></a>Свойства системы
#### <a name="naming"></a>Именование
В SDK сервера мобильных служб Azure hello системные свойства всегда содержат двух символов подчеркивания (`__`) префикс для hello свойства:

* __createdAt
* __updatedAt
* __deleted
* __version

Клиент мобильных служб Hello SDK имеет специальную логику для синтаксического анализа системные свойства в этом формате.

В мобильных приложениях Azure свойства системы больше нет специального форматирования и иметь hello следующие имена:

* дата создания
* дата обновления
* deleted
* версия

Hello мобильные приложения клиента пакеты SDK используйте hello новых системы свойства имен, поэтому изменять не требуется tooclient кода. Тем не менее при работе непосредственно внесения REST вызывает службу tooyour, затем следует соответственно изменить запросы.

#### <a name="local-store"></a>Локальное хранилище
имена toohello Hello изменения системных свойств означает, что автономной синхронизации локальной базы данных для мобильных служб не совместимы с приложениями для мобильных устройств. Если это возможно следует избегать клиентских приложений, обновляющих tooMobile мобильных служб, приложений, пока после ожидающих изменений отправлен toohello сервера. Затем приложение обновленной hello следует использовать новое имя файла базы данных.

Если клиентское приложение обновляется с tooMobile мобильных служб приложений, пока имеются ожидающие изменения в автономном режиме в очередь операций hello, hello системной базы данных необходимо обновленные toouse hello новые имена столбцов. На iOS это можно сделать с помощью имен столбцов hello toochange упрощенных миграции. На Android и hello клиентских управляемых .NET следует писать пользовательские toorename SQL hello столбцов для таблиц данных объекта.

На iOS следует изменить схему основных данных для вашего следующего hello toomatch сущности данных. Обратите внимание, что свойства hello `createdAt`, `updatedAt` и `version` больше нет `ms_` префикс:

| Атрибут | Тип | Примечание. |
| --- | --- | --- |
| id |Строка, помеченная как обязательная |первичный ключ в удаленном хранилище |
| дата создания |Дата |(необязательно) maps toocreatedAt системного свойства |
| дата обновления |Дата |(необязательно) maps tooupdatedAt системного свойства |
| версия |Строка |(необязательно) используется toodetect конфликты, tooversion карты |

#### <a name="querying-system-properties"></a>Выполнение запросов к свойствам системы
В мобильных службах Azure системные свойства не отправляются по умолчанию, но только в том случае, когда они запрашиваются с помощью строки запроса hello `__systemProperties`. В отличие от этого, в системе мобильных приложений Azure свойства являются **всегда выбран** так, как они являются частью hello server SDK объектной модели.

Это изменение влияет главным образом на настраиваемые реализации диспетчеров доменов, такие как расширения `MappedEntityDomainManager`. Мобильные службы, если клиент никогда не запрашивает все системные свойства при возможных toouse `MappedEntityDomainManager` , не сопоставленный фактически все свойства. Однако в мобильных приложениях Azure эти несопоставленные свойства приведут к возникновению ошибок в запросах GET.

Здравствуйте, наиболее простым способом tooresolve hello проблема является toomodify вашей DTO, чтобы они наследуют от `ITableData` вместо `EntityData`. Затем добавьте hello `[NotMapped]` атрибута toohello поля, которые следует пропустить.

Например, следующие hello определяет `TodoItem` без указания свойств системы:

    using System.ComponentModel.DataAnnotations.Schema;

    public class TodoItem : ITableData
    {
        public string Text { get; set; }

        public bool Complete { get; set; }

        public string Id { get; set; }

        [NotMapped]
        public DateTimeOffset? CreatedAt { get; set; }

        [NotMapped]
        public DateTimeOffset? UpdatedAt { get; set; }

        [NotMapped]
        public bool Deleted { get; set; }

        [NotMapped]
        public byte[] Version { get; set; }
    }

Примечание: Если вы получаете ошибки `NotMapped`, добавьте ссылочную сборку toohello `System.ComponentModel.DataAnnotations`.

### <a name="cors"></a>CORS
Мобильные службы включены некоторую поддержку CORS, заключив hello решений ASP.NET CORS. Этот уровень изоляции был удален toogive hello разработчика более широкие возможности управления, поэтому можно напрямую использовать [поддержка ASP.NET CORS](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).

Hello основных проблем при использовании CORS являются этого hello `eTag` и `Location` заголовки должен быть разрешен в порядке для hello клиента SDK toowork должным образом.

### <a name="push-notifications"></a>Push-уведомления
Для принудительной отправки класс PushRegistrationHandler hello является hello основных элементов, которые могут оказаться в hello Server SDK отсутствует. Регистрации в мобильных приложениях обрабатываются немного по-другому, и способы регистрации без тегов включены по умолчанию. Управление тегами осуществляется с помощью пользовательских API. См. в разделе hello [регистрация для тегов](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags) инструкции для получения дополнительной информации.

### <a name="scheduled-jobs"></a>Запланированные задания
Запланированные задания не встроены в мобильные приложения и все существующие задания, которые имеют в серверной части .NET потребуется toobe обновлены по отдельности. Один из вариантов — запланированного toocreate [веб-задание] на сайте кода hello мобильного приложения. Можно также настроить контроллер, который содержит код задания и настройки hello [планировщика Azure] toohit этой конечной точки по расписанию требуется hello.

### <a name="miscellaneous-changes"></a>Прочие изменения
Все ApiControllers, которые будут использоваться мобильного клиента должна иметь hello `[MobileAppController]` атрибута. Это больше не включены по умолчанию, чтобы другие ApiControllers toogo влиянию hello мобильных модулей форматирования.

Hello `ApiServices` объект больше не является частью пакета SDK для hello. tooaccess параметры мобильного приложения, можно использовать следующие hello:

    MobileAppSettingsDictionary settings = this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

Аналогичным образом ведение журнала теперь выполняется с помощью hello Стандартная ASP.NET трассировки записи:

    ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
    traceWriter.Info("Hello, World");  

## <a name="authentication"></a>Рекомендации по проверке подлинности
Теперь были перемещены в компонент приложения службы проверки подлинности и авторизации hello Hello компонентов проверки подлинности мобильных служб. Вы можете узнать о Включение этого узла при чтении hello [мобильное приложение добавить authentication tooyour](app-service-mobile-ios-get-started-users.md) раздела.

Для некоторых поставщиков, например AAD и Facebook, Google должны принадлежать копии приложения могут tooleverage hello существующую регистрацию. Просто toonavigate toohello поставщика удостоверений на портале и добавьте новую регистрацию toohello URL-адрес перенаправления. Затем настройте приложение службы проверки подлинности и авторизации идентификатор клиента hello и секрет.

### <a name="controller-action-authorization"></a>Авторизация действий контроллера
Все экземпляры hello `[AuthorizeLevel(AuthorizationLevel.User)]` атрибут теперь должен быть измененные toouse hello Стандартная ASP.NET `[Authorize]` атрибута. Кроме того, теперь контроллеры являются анонимными по умолчанию, как и в других приложениях ASP.NET.
При использовании одного из hello другие параметры AuthorizeLevel, таких как администратор или приложения, обратите внимание, что они удалены. Вместо этого можно настроить AuthorizationFilters для общие секреты или настроить service to service участника-службы AAD tooenable вызовы безопасно.

### <a name="getting-additional-user-information"></a>Получение дополнительных сведений о пользователе
Можно получить дополнительные сведения, включая маркеры доступа через hello `GetAppServiceIdentityAsync()` метод:

        FacebookCredentials creds = await this.User.GetAppServiceIdentityAsync<FacebookCredentials>();

Кроме того Если приложение принимает зависимости пользователя идентификаторы, например для сохранения их в базе данных, очень важно toonote, hello идентификаторы пользователя мобильных служб и мобильные приложения службы приложений не совпадают. Вы все равно можете hello идентификатор пользователя мобильных служб, однако. Все подклассы ProviderCredentials hello имеют свойства UserId. Поэтому продолжении из пример hello раньше:

        string mobileServicesUserId = creds.Provider + ":" + creds.UserId;

Если приложение принимает все зависимости в коде пользователя, важно использовать hello аналогичной регистрации с помощью поставщика удостоверений, если это возможно. Идентификаторы пользователей являются обычно области toohello регистрации приложения, который был использован, поэтому Представляем новую регистрацию может создать проблемы с соответствующим пользователям tootheir данные.

### <a name="custom-authentication"></a>Настраиваемая проверка подлинности
Если приложение использует решение нестандартной проверки подлинности, требуется toomake hello обновленного узла содержит систему toohello доступа. Следуйте инструкциям новый hello для нестандартной проверки подлинности в hello [Обзор пакета SDK для .NET server] toointegrate решения. Обратите внимание на то, что компоненты hello нестандартной проверки подлинности все еще находятся в предварительной версии.

## <a name="updating-clients"></a>Обновление клиентов
После получения рабочей серверной части мобильных приложений вы можете работать с новой версией клиентского приложения, которое использует эту серверную часть. Мобильные приложения также включает в себя новую версию клиента hello пакеты SDK и аналогичные обновления сервера toohello выше, необходимо будет tooremove все ссылки toohello Mobile Services SDK перед установкой версии мобильные приложения hello.

Одним из hello основные различия между версиями hello является то, что конструкторы hello больше не требуется ключ приложения. Теперь просто передать URL-адрес hello мобильного приложения. Например, для клиентов .NET hello, hello `MobileServiceClient` конструктор больше не:

        public static MobileServiceClient MobileService = new MobileServiceClient(
            "https://contoso.azurewebsites.net", // URL of hello Mobile App
        );

Вы можете прочесть об установке hello новых пакетов SDK и с помощью новой структуры hello через hello ссылки ниже:

* [iOS 3.0.0 или более поздней версии](app-service-mobile-ios-how-to-use-client-library.md)
* [.NET (Windows/Xamarin) 2.0.0 или более поздней версии](app-service-mobile-dotnet-how-to-use-client-library.md)

Если приложение принимает использовать push-уведомлений, запишите hello инструкции конкретной регистрации для каждой платформы, как будут внесены некоторые изменения также.

При наличии hello новую версию клиента готов, попробуйте для проекта на обновленном сервере. После проверки того, что он работает, можно освободить новую версию toocustomers вашего приложения. Со временем Если ваши клиенты уже есть tooreceive вероятность эти обновления, можно удалить версии приложения для мобильных служб hello. В этот момент по окончании обновления tooan приложение службы мобильных приложений с помощью сервера последнюю мобильные приложения hello SDK.

<!-- URLs. -->

[портал Azure]: https://portal.azure.com/
[классический портал Azure]: https://manage.windowsazure.com/
[Каковы мобильные приложения?]: app-service-mobile-value-prop.md
[I already use web sites and mobile services – how does App Service help me?]: /en-us/documentation/articles/app-service-mobile-value-prop-migration-from-mobile-services
[пакет SDK для мобильных приложений сервера]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[Create a Mobile App]: app-service-mobile-xamarin-ios-get-started.md
[Add push notifications tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-push.md
[Add authentication tooyour mobile app]: app-service-mobile-xamarin-ios-get-started-users.md
[планировщика Azure]: /en-us/documentation/services/scheduler/
[веб-задание]: ../app-service-web/websites-webjobs-resources.md
[как toouse hello .NET server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Migrate from Mobile Services tooan App Service Mobile App]: app-service-mobile-migrating-from-mobile-services.md
[Migrate your existing Mobile Service tooApp Service]: app-service-mobile-migrating-from-mobile-services.md
[служб приложений Ценовая]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[Обзор пакета SDK для .NET server]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
