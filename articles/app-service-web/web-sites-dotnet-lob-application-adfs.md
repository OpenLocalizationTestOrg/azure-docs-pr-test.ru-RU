---
title: "бизнес приложения Azure с проверкой подлинности AD FS aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate бизнес приложения в службе приложений Azure, который выполняет проверку подлинности с локальным STS. Этот учебник предназначен для AD FS как hello локальной службы маркеров безопасности."
services: app-service\web
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: 0fa9f7a1-37bd-4d11-845f-aeff6fc9e4ca
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: cfd6f14837642fbf58ca5da9dee72db69cd5ab7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a>Создание бизнес-приложения Azure с проверкой подлинности AD FS
В этой статье показано, как toocreate ASP.NET MVC для бизнес-приложений в [службе приложений Azure](../app-service/app-service-value-prop-what-is.md) с помощью локальной [служб федерации Active Directory](http://technet.microsoft.com/library/hh831502.aspx) как поставщик удостоверений hello. Этот сценарий можно использовать, когда необходимо toocreate бизнес-приложений в службе приложений Azure, но ваша организация требует toobe каталог данных, хранящихся на месте.

> [!NOTE]
> Обзор hello enterprise для разных параметров проверки подлинности и авторизации для службы приложений Azure см. в разделе [аутентификация с помощью локальной Active Directory в приложении Azure](web-sites-authentication-authorization.md).
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>Что будет строиться
Простое приложение ASP.NET в веб-приложениях службы приложений Azure создаст с hello следующие атрибуты:

* проверка подлинности пользователей в AD FS
* Использует `[Authorize]` tooauthorize пользователей для различных действий
* Статическая конфигурация для отладки в Visual Studio и публикации веб-приложений служб tooApp (один раз настройки, отладки и публикации в любое время)  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>Необходимые элементы
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

Требуется hello следующие toocomplete этого учебника:

* Локальному развертывания AD FS (конца в конец Пошаговое руководство по лаборатории тестирования hello, используемые в этом учебнике см. в разделе [лаборатории тестирования: автономный STS с AD FS на виртуальной Машине Azure (для тестирования)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))
* Доверие проверяющей стороны toocreate разрешения в управления AD FS
* Visual Studio 2013 с обновлением 4 или более поздней версии.
* [Пакет SDK Azure, начиная с версии 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) .

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a>Использование примера приложения в качестве шаблона бизнес-приложения
Здравствуйте, образец приложения в этом учебнике [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), созданных team hello Azure Active Directory. Так как службы федерации Active Directory поддерживает WS-Federation, можно использовать как шаблон toocreate бизнес-приложения с легкостью. Он имеет hello следующие атрибуты:

* Использует [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate с локальное развертывание AD FS
* функции входа и выхода
* Использует [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (вместо Windows Identity Foundation), который является hello будущих ASP.NET и гораздо проще tooset для использования проверки подлинности и авторизации, чем WIF

<a name="bkmk_setup"></a>

## <a name="set-up-hello-sample-application"></a>Настройка образца приложения hello
1. Клонировать или загрузить решение образца hello в [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour локальный каталог.
   
   > [!NOTE]
   > Здравствуйте, инструкции по [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) показывается, как tooset приложения hello в Azure Active Directory. Однако в этом учебнике, он настраивается с AD FS, поэтому вместо этого выполните здесь шаги hello.
   > 
   > 
2. Откройте решение hello, а затем Controllers\AccountController.cs в hello **обозревателе решений**.
   
   Вы увидите, что код hello просто направляет пользователя hello tooauthenticate запрос проверки подлинности, с помощью WS-Federation. Вся проверка подлинности настраивается в App_Start\Startup.Auth.cs.
3. Откройте App_Start\Startup.Auth.cs. В hello `ConfigureAuth` метод, строка hello Примечание:
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   В OWIN Здравствуй, мир этот фрагмент действительно является hello минимальные необходимые проверки подлинности WS-Federation tooconfigure исходного состояния системы. Это гораздо проще и более элегантный, чем WIF, где введенный Web.config в XML по всему месте hello. Здравствуйте только сведения, необходимые hello проверяющей стороны (RP) идентификатор и hello URL-адрес файла метаданных службы AD FS. Ниже приведен пример:
   
   * Идентификатор RP: `https://contoso.com/MyLOBApp`
   * Адрес метаданных: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`
4. В App_Start\Startup.Auth.cs измените следующие определения статическую строку hello:  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. Сделан hello соответствующих изменений в файле Web.config. Откройте hello Web.config и добавьте следующие параметры приложения hello:  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter hello App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter hello relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter hello FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   Заполните значения ключа hello в зависимости от соответствующих среде.
6. Построение toomake приложения hello, проверьте, нет ли ошибок.

Вот и все. Теперь пример приложения hello — Готово toowork с AD FS. Необходимо по-прежнему tooconfigure доверия проверяющей Стороны с помощью этого приложения в AD FS более поздней версии.

<a name="bkmk_deploy"></a>

## <a name="deploy-hello-sample-application-tooazure-app-service-web-apps"></a>Развертывание tooAzure приложения hello образец приложения службы веб-приложений
Здесь опубликовать hello приложения tooa веб-приложения в веб-приложениях службы приложений при сохранении среды отладки hello. Обратите внимание, что ты toopublish приложения hello раньше, чем он RP доверия AD FS, чтобы проверка подлинности по-прежнему не работает еще. Однако если сделать это теперь вы можете получить hello web URL-адрес приложения, которые можно использовать позже tooconfigure hello RP доверия.

1. Щелкните правой кнопкой мыши свой проект и выберите **Опубликовать**.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. Щелкните **Служба приложений Microsoft Azure**.
3. Если вы еще не выполнили вход tooAzure, нажмите кнопку **входа** и использовать учетную запись Microsoft hello toosign вашей подписки Azure в.
4. После входа щелкните **New** toocreate веб-приложения.
5. Заполните все обязательные поля. Вы собираетесь tooconnect tooon локальных данных более поздней версии, поэтому нельзя создавать базы данных для этого веб-приложения.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. Щелкните **Создать**. После создания веб-приложения hello открыто диалоговое окно приветствия публикации веб-сайта.
7. В **URL-адрес назначения**, изменить **http** слишком**https**. Скопируйте hello весь URL-адрес tooa текстовый редактор для последующего использования. Затем щелкните **Опубликовать**.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. В Visual Studio откройте в своем проекте файл **Web.Release.config** . Вставьте следующий XML-код в hello hello `<configuration>` тег и замените значение ключа hello URL-адрес веб-приложения вашей публикации.  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

Когда закончите, у вас есть два идентификатора RP настроены в проекте, один для вашей среды отладки в Visual Studio и один для hello опубликованных веб-приложения в Azure. Вы настроите доверие проверяющей Стороны для каждого из двух сред hello в AD FS. Во время отладки, параметры приложения hello в файле Web.config, используемые toomake вашей **отладки** конфигурации работают с AD FS. При публикации (по умолчанию hello **выпуска** публикуется конфигурации), преобразованный Web.config загружается с учетом изменений параметра приложения hello в Web.Release.config.

Если требуется tooattach hello опубликованных веб-приложения в отладчик Azure toohello (т. е. его необходимо загрузить символы отладки кода в hello опубликованных веб-приложения), можно создать клон hello конфигурация для отладки Azure отладки, но с помощью пользовательских файле Web.config преобразовать) Например, Web.AzureDebug.config), используются параметры приложения hello с Web.Release.config. Это позволяет toomaintain статической конфигурации hello различных средах.

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a>Настройка доверия с проверяющей стороной в оснастке управления AD FS
Теперь вам требуется tooconfigure доверия проверяющей Стороны в управления AD FS, прежде чем использовать приложение-образец и фактически проверку подлинности с AD FS. Необходимо будет tooset копирование два отдельных RP доверия: для вашей среды отладки и для опубликованных веб-приложения.

> [!NOTE]
> Убедитесь, что повторить hello следующие шаги для обеих сред.
> 
> 

1. Войдите в систему учетные данные, имеющие права управления tooAD FS на сервере AD FS.
2. Откройте оснастку управления AD FS. Щелкните правой кнопкой мыши **AD FS\Trusted Relationships\Relying Party Trusts** и выберите **Добавить отношение доверия проверяющей стороны**.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. В hello **Выбор источника данных** выберите **вручную вводить данные о проверяющей стороне hello**. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. В hello **укажите отображаемое имя** введите отображаемое имя для приложения hello и нажмите кнопку **Далее**.
5. В hello **выберите протокол** щелкните **Далее**.
6. В hello **Настройка сертификата** щелкните **Далее**.
   
   > [!NOTE]
   > Так как уже должен использоваться протокол HTTPS, зашифрованные токены необязательны. Если действительно tooencrypt токенов AD FS на этой странице, необходимо также добавить расшифровки логика в коде. Дополнительную информацию см. в статье [Ручная настройка промежуточного слоя OWIN WS-Federation и прием зашифрованных маркеров](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).
   > 
   > 
7. Прежде чем выполняется переход к следующему шагу hello, необходим один фрагмент данных из проекта Visual Studio. В свойствах проекта hello, обратите внимание, hello **URL-адрес SSL** приложения hello. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. В управление AD FS в hello **настроить URL-адрес** страница hello **проверяющей стороной мастер добавления отношений доверия**выберите **включить поддержку пассивного протокола WS-Federation hello** и Введите в hello URL-адрес SSL проекта Visual Studio, записанное в предыдущем шаге hello. Затем щелкните **Далее**.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > URL-адрес указывает, где toosend hello клиента после проверки подлинности завершается успешно. Для среды отладки hello, он должен быть <code>https://localhost:&lt;port&gt;/</code>. Для опубликованных веб-приложения hello следует hello URL-адрес приложения.
   > 
   > 
9. В hello **настроить идентификаторы** , убедитесь, что URL-адрес SSL проекта уже присутствует в списке и нажмите кнопку **Далее**. Нажмите кнопку **Далее** все hello способом toohello конец hello мастере с использованием параметров по умолчанию.
   
   > [!NOTE]
   > В App_Start\Startup.Auth.cs проекта Visual Studio этот идентификатор противопоставляется значение hello <code>WsFederationAuthenticationOptions.Wtrealm</code> во время федеративной проверки подлинности. По умолчанию URL-адрес приложения hello из предыдущего шага hello добавляется в качестве идентификатора RP.
   > 
   > 
10. Настройка hello приложение STS для проекта в AD FS теперь завершена. Далее следует настроить этот toosend приложения hello утверждения, необходимые для приложения. Hello **изменение правил для утверждений** открытии диалогового окна по умолчанию для вас в конце hello приветствия мастера, можно запустить немедленно. Настроим Здравствуйте, по крайней мере следующие утверждения (со схемами в круглых скобках):
    
    * Имя (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name -), используемые ASP.NET toohydrate `User.Identity.Name`.
    * Имя участника (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - используется toouniquely пользователя определите пользователей в организации hello.
    * Членство в группах как роли (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - может использоваться с `[Authorize(Roles="role1, role2,...")]` tooauthorize Декорирование контроллеров и действий. На самом деле этот подход может не быть hello большинство высокопроизводительных для авторизации ролей. Если ваши пользователи AD относятся toohundreds групп безопасности, они становятся сотни утверждений ролей в маркере SAML hello. Альтернативный подход — toosend одной роли условно утверждения в зависимости от членства пользователя hello в определенной группе. Однако в нашем учебнике мы будем придерживаться простого подхода.
    * ИД имени (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) — используется для проверки защиты от подделки. Дополнительные сведения об использовании toomake ее защиты от подделки проверки см. в разделе hello **добавить функции бизнес-** раздел [Создание бизнес-приложения Azure с проверкой подлинности Azure Active Directory ](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).
    
    > [!NOTE]
    > Hello типы утверждений вы должны tooconfigure для приложения зависит от потребностей вашего приложения. Hello список утверждений поддерживается в приложениях Azure Active Directory (т. е. отношения доверия проверяющей Стороны) например, см. [типы поддерживаемых токенов и утверждений](http://msdn.microsoft.com/library/azure/dn195587.aspx).
    > 
    > 
11. В диалоговом окне приветствия изменение правил для утверждений, щелкните **добавить правило**.
12. Настройка утверждений hello имя участника-пользователя и роли, как показано на снимке экрана приветствия и нажмите кнопку **Готово**.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    Создайте временный имя, идентификатор утверждений, используя hello шаги демонстрируются в [имя идентификаторы в утверждения SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).
13. Щелкните **Добавить правило** еще раз.
14. Выберите **Отправка утверждений с помощью настраиваемого правила** и нажмите кнопку **Далее**.
15. Вставить hello следующие правила языка в hello **настраиваемого правила** поле, имя правила hello **на идентификатор сеанса** и нажмите кнопку **Готово**.  
    
    <pre class="prettyprint">
    c1:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"] &amp;&amp;
    c2:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant"]
     => add(
         store = "_OpaqueIdStore",
         types = ("<mark>http://contoso.com/internal/sessionid</mark>"),
         query = "{0};{1};{2};{3};{4}",
         param = "useEntropy",
         param = c1.Value,
         param = c1.OriginalIssuer,
         param = "",
         param = c2.Value);
    </pre>
    
    Настраиваемое правило должно выглядеть, как на этом снимке экрана.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. Щелкните **Добавить правило** еще раз.
17. Выберите **Преобразование входящего утверждения** и нажмите кнопку **Далее**.
18. Настройте правила hello, как показано на снимке экрана приветствия (с использованием типа утверждения hello, созданный в настраиваемое правило hello) и нажмите кнопку **Готово**.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    Подробные сведения о hello действия для временного идентификатора имени утверждения hello. в разделе [имя идентификаторы в утверждения SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).
19. Нажмите кнопку **применить** в hello **изменение правил для утверждений** диалогового окна. Он должен выглядеть так hello следующий снимок экрана:
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > Не забудьте, что эти шаги необходимо повторить для среды отладки и опубликованного веб-приложения.
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a>Тестирование федеративной проверки подлинности для приложения
Вам будут готовы tootest логику приложения проверки подлинности для AD FS. В моей лабораторной среды AD FS у меня есть тестового пользователя, к которому относится tooa тестовую группу в Active Directory (AD).

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

tootest проверки подлинности в отладчике hello, все, что нужно toodo теперь является типом `F5`. Если требуется проверка подлинности tootest в опубликованных веб-приложения hello перейдите toohello URL-адрес.

После загрузки веб-приложения hello, нажмите кнопку **входа**. Теперь вы должны получить либо имя входа диалогового окна или hello страницу входа от службы федерации Active Directory, в зависимости от метода проверки подлинности hello, выбранного с помощью AD FS. Вот что получается в Internet Explorer 11.

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

После входа под учетной записью пользователя в домене hello AD развертывания hello AD FS должно отобразиться Домашняя страница приветствия с **Hello, <User Name>!** в углу hello. Вот что у меня получается.

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

Таким образом была успешной hello следующих способов:

* Приложение успешно достигнут AD FS, а также соответствующий идентификатор проверяющей Стороны находится в hello базы данных AD FS
* AD FS успешно прошел проверку подлинности пользователя AD и перенаправления обратно домашней страницы приложения toohello
* Службы федерации Active Directory как имя успешно отправленных hello утверждения приложения tooyour (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name), обозначенный фактов hello hello пользователя имя будет отображаться в углу hello. 

Если отсутствует утверждение "имя" hello, вы бы увидеть **Hello,!**. Если взглянуть на одну\_LoginPartial.cshtml, обнаружится, что он использует `User.Identity.Name` имя пользователя toodisplay hello. Как упоминалось ранее, если имя hello утверждения из hello проверку подлинности пользователей, не доступных в маркере SAML hello, ASP.NET hydrates это свойство вместе с ним. toosee, все hello утверждения, отправляемые службой AD FS, установить точку останова в Controllers\HomeController.cs, при hello индекс метода действия. После проверки подлинности пользователя hello проверять hello `System.Security.Claims.Current.Claims` коллекции.

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a>Авторизация пользователей для определенных контроллеров и действий
С момента включения членства в группах как утверждения роли в конфигурации доверия проверяющей Стороны, теперь можно использовать их непосредственно в hello `[Authorize(Roles="...")]` декорирования для контроллеров и действий. В бизнес приложения с шаблоном hello Создание-чтение-обновления и удаления (CRUD) вы можете разрешить tooaccess конкретных ролей каждого действия. На данном этапе будет просто опробовать эту возможность на существующий контроллер Home hello.

1. Откройте Controllers\HomeController.cs.
2. Украшение hello `About` и `Contact` действие методов аналогичные toohello после кода, с помощью членства в группах безопасности с проверкой подлинности пользователя.  
   
    <pre class="prettyprint">
    <mark>[Authorize(Roles="Test Group")]</mark>
    public ActionResult About()
    {
        ViewBag.Message = "Your application description page.";
   
        return View();
    }
   
    <mark>[Authorize(Roles="Domain Admins")]</mark>
    public ActionResult Contact()
    {
        ViewBag.Message = "Your contact page.";
   
        return View();
    }
    </pre>
   
    Поскольку я добавил **тестового пользователя** слишком**тестовую группу** в моей лабораторной среды AD FS, я буду использовать тестовую группу tootest авторизации на `About`. Для `Contact`, я протестируем hello отрицательное регистр **"Администраторы домена"**, toowhich **проверки пользователя** не принадлежит.
3. Запустите отладчик hello, введя `F5` входа, а затем выберите **о**. Вы теперь должен Просмотр hello `~/About/Index` страница успешно, если ваш прошедший проверку пользователь авторизован для этого действия.
4. Сейчас, нажмите кнопку **контакт**, которой в моем случае не следует авторизовать **тестового пользователя** для hello действия. Тем не менее перенаправленный tooAD федерации Active Directory, в конечном итоге показывает это сообщение используется hello браузера:
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    Если эта ошибка в средстве просмотра событий на сервер AD FS hello изучать, вы увидите это сообщение исключения:  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>hello same client browser session has made '6' requests in hello last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    Hello причина этой ошибки заключается в том, что по умолчанию MVC возвращает подлинности 401 при роли пользователя нет прав. При этом запускается повторная проверка подлинности запроса tooyour поставщика удостоверений (AD FS). Поскольку hello пользователь уже прошел проверку, службы федерации Active Directory возвращает toohello одной странице, которое затем создает другой 401, создания цикла обработки перенаправления. Будут переопределены AuthorizeAttribute `HandleUnauthorizedRequest` метод с простой логики tooshow то, что имеет смысл вместо продолжение цикла перенаправления hello.
5. Создайте файл в проект hello с именем AuthorizeAttribute.cs и hello вставьте следующий код в него.
   
        using System;
        using System.Web.Mvc;
        using System.Web.Routing;
   
        namespace WebApp_WSFederation_DotNet
        {
            [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
            public class AuthorizeAttribute : System.Web.Mvc.AuthorizeAttribute
            {
                protected override void HandleUnauthorizedRequest(AuthorizationContext filterContext)
                {
                    if (filterContext.HttpContext.Request.IsAuthenticated)
                    {
                        filterContext.Result = new System.Web.Mvc.HttpStatusCodeResult((int)System.Net.HttpStatusCode.Forbidden);
                    }
                    else
                    {
                        base.HandleUnauthorizedRequest(filterContext);
                    }
                }
            }
        }
   
    Hello переопределить код отправляет HTTP 403 (запрещено) вместо HTTP 401 (не санкционировано) в случаях, прошедшего проверку подлинности, но несанкционированного.
6. Запуск отладчика hello с `F5`. Щелкнув **Контакт** , теперь можно увидеть более информативное (хотя и непривлекательное) сообщение об ошибке:
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. Повторной публикации приложения hello tooAzure приложения службы веб-приложений и тестирования поведения hello динамической приложения hello.

<a name="bkmk_data"></a>

## <a name="connect-tooon-premises-data"></a>Подключение tooon локальные данные
Что нужно tooimplement бизнес-приложения с AD FS вместо Azure Active Directory обусловлено проблемы соответствия с сохранением организации данных во внешней среде. Это также может означать, что веб-приложения в Azure необходимо получить доступ к локальным базам данных, поскольку toouse не допускаются [базы данных SQL](/services/sql-database/) как hello уровня данных для развертывания веб-приложений.

Веб-приложения службы приложений Azure поддерживают доступ к локальным базам данных двумя способами: с помощью [гибридных подключений](../biztalk-services/integration-hybrid-connection-overview.md) и [виртуальных сетей](web-sites-integrate-with-vnet.md). Дополнительную информацию см. в статье [Использование интеграции VNET и гибридных подключений с веб-приложениями службы приложений Azure](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>Дополнительные ресурсы
* [Проверка подлинности в приложении Azure с помощью локального каталога Active Directory](web-sites-authentication-authorization.md)
* [Создание бизнес-приложения Azure с проверкой подлинности Azure Active Directory](web-sites-dotnet-lob-application-azure-ad.md)
* [Использовать hello в локальной организации параметр проверки подлинности (ADFS) с ASP.NET в Visual Studio 2013](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [Перенос tooKatana VS2013 Web проекта из WIF](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [Обзор служб федерации Active Directory](http://technet.microsoft.com/library/hh831502.aspx)
* [Спецификация WS-Federation 1.1](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

