---
title: "Автоматическая подготовка пользователей и групп из Azure Active Directory tooapplications aaaUsing системы для управления удостоверениями междоменной | Документы Microsoft"
description: "Azure Active Directory автоматически подготавливать пользователей и групп tooany приложения или идентификатор магазина, аппаратные веб-службой с hello интерфейс, определенный в спецификации протокола SCIM hello"
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 4d86f3dc-e2d3-4bde-81a3-4a0e092551c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.custom: aaddev;it-pro;oldportal
ms.openlocfilehash: 43045c97e68d0d22db598dcb5ec23481c4e97718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-system-for-cross-domain-identity-management-tooautomatically-provision-users-and-groups-from-azure-active-directory-tooapplications"></a>При использовании системы для подготовки tooautomatically между доменами удостоверений пользователей и группы из tooapplications Azure Active Directory

## <a name="overview"></a>Обзор
Azure Active Directory (Azure AD) автоматически подготавливать пользователей и групп tooany приложения или идентификатор магазина, аппаратные веб-службой с hello интерфейс, определенный в hello [система для идентификации управления доменами (SCIM) 2.0 Спецификация протокола](https://tools.ietf.org/html/draft-ietf-scim-api-19). Azure Active Directory можно отправлять запросы toocreate, изменение или удаление назначенных пользователей и групп toohello веб-службы. Hello веб-службы можно преобразовать эти запросы в операции над hello целевого хранилища удостоверений. 

> [!IMPORTANT]
> Корпорация Майкрософт рекомендует управлять Azure AD, используя hello [Центр администрирования Azure AD](https://aad.portal.azure.com) в hello портал Azure, вместо использования hello классический портал Azure, в этой статье. 



![][0]
*Рисунок 1: Подготовка из хранилища удостоверений Azure Active Directory tooan через веб-службу*

Эту возможность можно использовать в сочетании с возможностью «принеси свое приложение» hello в Azure AD tooenable-единого входа и автоматической подготовки пользователей для приложений, предоставляющих или аппаратные веб-службой SCIM.

Существуют два варианта использования SCIM в Azure Active Directory.

* **Подготовка tooapplications пользователей и групп, которые поддерживают SCIM** приложений, которые поддерживают SCIM 2.0 и проверка подлинности работает в Azure AD без настройки применения маркеров носителя OAuth.
* **Построение подготовки решения для приложений, поддерживающих другие API-инициализации на основе** для приложений, не являющихся SCIM, можно создать tootranslate конечная точка SCIM между конечной точкой Azure AD SCIM hello и поддерживает приложения hello любого API для подготовки пользователей. Разработка конечную точку SCIM toohelp, мы предоставляем библиотеки Common Language Infrastructure (CLI), а также примеры кода, которые показывают, как указать конечную точку SCIM и преобразования сообщений SCIM toodo.  

## <a name="provisioning-users-and-groups-tooapplications-that-support-scim"></a>Подготовка пользователей и групп tooapplications, который поддерживает SCIM
Azure AD может быть настроенный tooautomatically назначенный подготовки пользователей и групп tooapplications, реализовать [системы для управления удостоверениями междоменной 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) веб-службы и принять маркеров носителя OAuth для проверки подлинности . Согласно спецификации hello SCIM 2.0 приложений должно соответствовать следующим требованиям:

* Поддерживает создание пользователей и/или групп, согласно разделе 3.3 hello SCIM протокола.  
* Поддерживает изменение пользователей и/или групп, имеющих запросы patch согласно раздел 3.5.2 hello SCIM протокола.  
* Поддерживает извлечение известному ресурсу согласно раздел 3.4.1 hello SCIM протокола.  
* Поддерживает запросы пользователей и/или групп, как описано в разделе 3.4.2 из hello SCIM протокола.  (по умолчанию пользователи запрашиваются по атрибуту externalI, а группы по атрибуту displayName).  
* Поддерживает запросы пользователя по Идентификатору и диспетчером, как описано в разделе 3.4.2 из hello SCIM протокола.  
* Поддерживает группы по Идентификатору и для элементов, как описано в разделе 3.4.2 из hello SCIM протокол запросов.  
* Принимает маркеров носителя OAuth для авторизации, как описано в разделе 2.1 hello SCIM протокола.

Рекомендуется связаться с поставщиком приложения или ознакомиться с документацией поставщика для получения подтверждения соответствия этим требованиям.

### <a name="getting-started"></a>Приступая к работе
Приложения, поддерживающие профиль SCIM hello описанные в этой статье может быть подключенным tooAzure Active Directory с помощью функции hello «приложение не галереи» в галерее приложения hello Azure AD. После подключена, Azure AD запускает процесс синхронизации каждые 20 минут, где он запрашивает конечную точку SCIM приложения hello для назначенных пользователей и групп и создает или изменяет их в соответствии с toohello сведения о назначении.

**tooconnect приложение, поддерживающее SCIM:**

1. Войдите в слишком[hello портал Azure](https://portal.azure.com). 
2. Обзор слишком ** Azure Active Directory > корпоративных приложений и выберите **нового приложения > все > приложения без коллекции**.
3. Введите имя для вашего приложения и нажмите кнопку **добавить** toocreate значок объекта приложения.
    
  ![][1]
  *Рисунок 2. Использование коллекции приложений Azure AD*
    
4. На экране полученный hello выберите hello **Provisioning** вкладку в левом столбце hello.
5. В hello **режим подготовки** последовательно выберите пункты **автоматического**.
    
  ![][2]
  *Рисунок 3: Настройка подготовки в hello портал Azure*
    
6. В hello **URL-адрес клиента** введите hello URL-адрес конечной точки SCIM приложения hello. Пример: https://api.contoso.com/scim/v2/
7. Если конечная точка SCIM hello требует токена носителя OAuth от издателя, отличные от Azure AD, то копирование hello required токена носителя OAuth в hello необязательно **секрет маркера** поля. Если оставить это поле пустым, то Azure AD будет добавлять в каждый запрос токен носителя OAuth, выданный Azure AD. Приложения, использующие Azure AD в качестве поставщика удостоверений, могут проверить этот выданный Azure AD токен.
8. Нажмите кнопку hello **проверить подключение** кнопку toohave Azure Active Directory попытки tooconnect toohello SCIM конечной точки. Если hello попытки не удались, отображаются сведения об ошибке.  
9. Если приложение toohello tooconnect попыток hello выполняются успешно, нажмите кнопку **Сохранить** toosave учетные данные администратора hello.
10. В hello **сопоставления** статьи, два набора можно выбрать сопоставлений атрибутов: для пользовательских объектов и объектов групп. Выберите каждый один атрибуты tooreview hello, которые синхронизируются из tooyour приложения Azure Active Directory. Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello пользователей и групп в приложении для операций обновления. Выберите toocommit кнопку hello сохранить все изменения.

    >[!NOTE]
    >При необходимости можно отключить синхронизации группы объектов, отключив hello «groups» сопоставления. 

11. В разделе **параметры**, hello **область** поле определяет, какие пользователи и группы синхронизации. При выборе «Синхронизации только назначенные пользователи и группы» (рекомендуется) будет синхронизировать только пользователей и группы, назначенные в hello **пользователей и групп** вкладки.
12. После завершения настройки изменить hello **состояние подготовки** слишком**на**.
13. Нажмите кнопку **Сохранить** toostart hello подготовки службы Azure AD. 
14. Если синхронизация только назначены пользователи и группы (рекомендуется), быть убедиться, что hello tooselect **пользователей и групп** и назначьте hello пользователей или групп, которые нужно toosync.

После запуска начальной синхронизации hello, можно использовать hello **журналы аудита** вкладке toomonitor хода выполнения, показывающий все действия, выполняемые hello подготовки службы в приложении. Дополнительные сведения о способ подготовки tooread hello Azure AD использует для входа см. в разделе [отчеты о автоматический подготовки пользователей. учетной записи](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

>[!NOTE]
>Начальная синхронизация Hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello. 


## <a name="building-your-own-provisioning-solution-for-any-application"></a>Создание собственного решения подготовки для любого приложения
Создав веб-службу SCIM, взаимодействующую с Azure Active Directory, можно включить единый вход и автоматическую подготовку пользователей практически для любого приложения, которое предоставляет API подготовки пользователей REST или SOAP.

Вот как это работает

1. Azure AD предоставляет библиотеку CLI с именем [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/). Системные интеграторы и разработчиков можно использовать этот toocreate библиотеки и развернуть веб-SCIM конечной точки службы можно подключаться хранилище удостоверений tooany приложения Azure AD.
2. Сопоставления реализованы в hello web service toomap hello унифицировать toohello пользователя схемы и необходимые приложения hello протокола.
3. URL-адрес конечной точки Hello регистрируется в Azure AD в рамках пользовательского приложения в галерее приложения hello.
4. Пользователи и группы назначаются toothis приложения в Azure AD. После назначения они помещаются в очередь toobe синхронизированы toohello целевое приложение. процесс синхронизации Hello обработки hello очереди выполняется каждые 20 минут.

### <a name="code-samples"></a>Примеры кода
toomake это удобным процесс, набор [примеры кода](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) предоставляются, создайте конечную точку службы web SCIM и демонстрируют автоматическую подготовку к работе. В одном примере поставщик службы использует файл, в котором пользователи и группы представлены строками значений, разделенных запятыми.  Hello других — поставщика, который работает со службой hello Amazon Web Services удостоверений и управления доступом.  

**Предварительные требования**

* Visual Studio 2013 или более поздней версии
* [Пакет Azure SDK для .NET](https://azure.microsoft.com/downloads/)
* Компьютере Windows, который поддерживает toobe framework 4.5 hello ASP.NET используется в качестве hello SCIM конечной точки. Этот компьютер должен быть доступен из облака hello
* [Подписка Azure с пробной или лицензированной версией Azure AD Premium.](https://azure.microsoft.com/services/active-directory/)
* Образец Hello Amazon AWS требует библиотек из не hello [AWS набор средств для Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html). Дополнительные сведения см. в разделе hello README файл, входящий в состав образца hello.

### <a name="getting-started"></a>Приступая к работе
Самый простой способ tooimplement Hello SCIM конечной точки, которое может принять подготовки запросов из Azure AD toobuild и разверните образец кода hello, выводит файл значений с разделителями запятыми (CSV) tooa подготовленные пользователи hello.

**toocreate конечную точку SCIM образца:**

1. Загрузите пакет образца кода hello в [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)
2. Распакуйте пакет hello и поместите его на компьютере Windows в расположении, например C:\AzureAD-BYOA-Provisioning-Samples\.
3. В этой папке запустите hello FileProvisioningAgent решения в Visual Studio.
4. Выберите **Сервис > Диспетчер пакетов библиотеки > консоль диспетчера пакетов**и выполните следующие команды для ссылки на решение hello tooresolve в проект FileProvisioningAgent hello hello:
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. Построение проекта FileProvisioningAgent hello.
6. Запустите приложение hello командной строки в Windows (с правами администратора) и использовать hello **cd** hello directory команда toochange tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** папки.
7. Выполните hello следующую команду, заменив < ip адрес > hello IP-адрес или домен, имя компьютера Windows hello.
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. В Windows, под **параметры Windows > сети и Интернету параметров**выберите hello **брандмауэра Windows > Дополнительные параметры**и создать **правила входящего подключения** , Разрешает доступ входящего трафика tooport 9000.
9. Если компьютер Windows hello за маршрутизатором, hello маршрутизатора потребностей toobe настроен tooperform перевод доступа к сети между его порта 9000, предоставляемый toohello Интернета и порта 9000 на компьютере Windows hello. Это необходимо для возможности tooaccess toobe Azure AD эту конечную точку в облаке hello.

**tooregister hello образец SCIM конечной точки в Azure AD:**

1. Войдите в слишком[hello портал Azure](https://portal.azure.com). 
2. Обзор слишком ** Azure Active Directory > корпоративных приложений и выберите **нового приложения > все > приложения без коллекции**.
3. Введите имя для вашего приложения и нажмите кнопку **добавить** toocreate значок объекта приложения. создать объект приложения Hello — предполагаемого toorepresent hello целевого приложения будет подготовки tooand реализации единого входа, а не просто hello SCIM endpoint.
4. На экране полученный hello выберите hello **Provisioning** вкладку в левом столбце hello.
5. В hello **режим подготовки** последовательно выберите пункты **автоматического**.
    
  ![][2]
  *Рисунок 4: Настройка подготовки в hello портал Azure*
    
6. В hello **URL-адрес клиента** введите hello предоставляется Интернет URL-адрес и порт SCIM конечной точки. Это может быть что-то, как http://testmachine.contoso.com:9000 или http://<ip-address>:9000/, где < ip адрес > является hello Интернета, предоставляемым IP адрес.  
7. Если конечная точка SCIM hello требует токена носителя OAuth от издателя, отличные от Azure AD, то копирование hello required токена носителя OAuth в hello необязательно **секрет маркера** поля. Если оставить это поле пустым, то Azure AD будет добавлять в каждый запрос токен носителя OAuth, выданный Azure AD. Приложения, использующие Azure AD в качестве поставщика удостоверений, могут проверить этот выданный Azure AD токен.
8. Нажмите кнопку hello **проверить подключение** кнопку toohave Azure Active Directory попытки tooconnect toohello SCIM конечной точки. Если hello попытки не удались, отображаются сведения об ошибке.  
9. Если приложение toohello tooconnect попыток hello выполняются успешно, нажмите кнопку **Сохранить** toosave учетные данные администратора hello.
10. В hello **сопоставления** статьи, два набора можно выбрать сопоставлений атрибутов: для пользовательских объектов и объектов групп. Выберите каждый один атрибуты tooreview hello, которые синхронизируются из tooyour приложения Azure Active Directory. Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello пользователей и групп в приложении для операций обновления. Выберите toocommit кнопку hello сохранить все изменения.
11. В разделе **параметры**, hello **область** поле определяет, какие пользователи и группы синхронизации. При выборе «Синхронизации только назначенные пользователи и группы» (рекомендуется) будет синхронизировать только пользователей и группы, назначенные в hello **пользователей и групп** вкладки.
12. После завершения настройки изменить hello **состояние подготовки** слишком**на**.
13. Нажмите кнопку **Сохранить** toostart hello подготовки службы Azure AD. 
14. Если синхронизация только назначены пользователи и группы (рекомендуется), быть убедиться, что hello tooselect **пользователей и групп** и назначьте hello пользователей или групп, которые нужно toosync.

После запуска начальной синхронизации hello, можно использовать hello **журналы аудита** вкладке toomonitor хода выполнения, показывающий все действия, выполняемые hello подготовки службы в приложении. Дополнительные сведения о способ подготовки tooread hello Azure AD использует для входа см. в разделе [отчеты о автоматический подготовки пользователей. учетной записи](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

Последний шаг Hello Проверка образца hello — hello tooopen TargetFile.csv файл в папке \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug hello на компьютере Windows. После выполнения процесса подготовки hello в этом файле отображаются сведения hello всех назначенных и подготовить пользователей и групп.

### <a name="development-libraries"></a>Библиотеки для разработчика
toodevelop собственной веб-службы, который соответствует спецификации SCIM toohello, сначала ознакомьтесь с hello следующих библиотек, предоставляемых корпорацией Майкрософт toohelp ускорить процесс разработки hello. 

1. Библиотеки Common Language Infrastructure (CLI) для использования с языками, основанными на этой инфраструктуре, например C#. Одно из этих библиотек [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), объявляет интерфейс, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, показано в следующих рисунке hello: A разработчик, использующий hello библиотеки будет реализовывать этот интерфейс с классом, который может ссылаться, универсальной поставщика. Hello библиотеки позволяют toodeploy developer Привет веб-службы, который соответствует спецификации SCIM toohello. Hello веб-служба может размещаться либо в службах IIS или любой исполняемая сборка Общеязыковая инфраструктура. Запрос преобразуется в поставщик toohello вызовы методов, которые может быть запрограммировано toooperate developer Привет на некоторых хранилище удостоверений.
  
  ![][3]
  
2. [Express обработчики маршрутов](http://expressjs.com/guide/routing.html) доступны для синтаксического анализа node.js запрос объектов, представляющих вызовы (в соответствии с hello спецификации SCIM), tooa node.js веб-службы.   

### <a name="building-a-custom-scim-endpoint"></a>Создание пользовательской конечной точки SCIM
Использование библиотек CLI hello, разработчики, использующие эти библиотеки можно размещать свои службы в любой исполняемая сборка Общеязыковая инфраструктура или в службах IIS. Ниже приведен пример кода для размещения службы в исполняемую сборку, по адресу hello http://localhost:9000: 

    private static void Main(string[] arguments)
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IProvider and 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
      new DevelopersMonitor();
    Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
      new DevelopersProvider(arguments[1]);
    Microsoft.SystemForCrossDomainIdentityManagement.Service webService = null;
    try
    {
        webService = new WebService(monitor, provider);
        webService.Start("http://localhost:9000");

        Console.ReadKey(true);
    }
    finally
    {
        if (webService != null)
        {
            webService.Dispose();
            webService = null;
        }
    }
    }

    public class WebService : Microsoft.SystemForCrossDomainIdentityManagement.Service
    {
    private Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor;
    private Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider;

    public WebService(
      Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitoringBehavior, 
      Microsoft.SystemForCrossDomainIdentityManagement.IProvider providerBehavior)
    {
        this.monitor = monitoringBehavior;
        this.provider = providerBehavior;
    }

    public override IMonitor MonitoringBehavior
    {
        get
        {
            return this.monitor;
        }

        set
        {
            this.monitor = value;
        }
    }

    public override IProvider ProviderBehavior
    {
        get
        {
            return this.provider;
        }

        set
        {
            this.provider = value;
        }
    }
    }

Эту службу необходимо иметь HTTP адреса и сервера проверки подлинности сертификат какие hello корневого центра сертификации — одно из следующих hello: 

* CNNIC;
* Comodo;
* CyberTrust;
* DigiCert;
* GeoTrust;
* GlobalSign;
* Go Daddy;
* VeriSign;
* WoSign.

Сертификат проверки подлинности сервера может быть привязанного tooa-порту на узле Windows с помощью служебной программы оболочки сети hello: 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

Здесь hello значение аргумента certhash hello — hello отпечаток сертификата hello, пока значение hello аргумента appid hello произвольный глобальный уникальный идентификатор.  

Служба toohost hello в службах IIS, разработчик построение будет осуществляться библиотечная сборка кодом CLA на класс с именем запуска в пространстве имен по умолчанию hello сборки hello.  Ниже приведен пример такого класса. 

    public class Startup
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor and  
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter starter;

    public Startup()
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
          new DevelopersMonitor();
        Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
          new DevelopersProvider();
        this.starter = 
          new Microsoft.SystemForCrossDomainIdentityManagement.WebApplicationStarter(
            provider, 
            monitor);
    }

    public void Configuration(
      Owin.IAppBuilder builder) // Defined in in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a>Обработка аутентификации на конечной точке
Запросы от Azure Active Directory содержат токен носителя OAuth 2.0.   Любой запрос службы принимающей hello должен проверить подлинность издателя hello как Azure Active Directory от имени клиента Azure Active Directory hello ожидалось, для доступа toohello веб-службы Azure Active Directory Graph.  В токене hello hello издателя идентифицируется утверждение iss, такие как «iss»: «https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/».  В этом примере базовый адрес hello hello значение утверждения, https://sts.windows.net, определяет Azure Active Directory, как hello издателя, пока hello относительный адрес сегмента, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, уникальный идентификатор hello Azure Active Клиент каталога, от имени которой hello выдачи токена.  Если токен hello был выдан для доступа к веб-службы для Azure Active Directory Graph hello, затем hello идентификатор этой службы, 00000002-0000-0000-c000-000000000000, должны быть в значение hello aud hello токен утверждений.  

Разработчики, использующие hello CLA библиотек, предоставляемых корпорацией Майкрософт для построения службы SCIM могут проходить проверку подлинности запросы от Azure Active Directory с помощью пакета Microsoft.Owin.Security.ActiveDirectory hello, выполните следующие действия: 

1. В поставщике реализация свойства Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior hello наличием возвращать метод toobe, вызывается при каждом запуске службы hello: 

  ````
    public override Action\<Owin.IAppBuilder, System.Web.Http.HttpConfiguration.HttpConfiguration\> StartupBehavior
    {
      get
      {
        return this.OnServiceStartup;
      }
    }

    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder,  // Defined in Owin.dll.  
      System.Web.Http.HttpConfiguration configuration)  // Defined in System.Web.Http.dll.  
    {
    }
  ````

2. Добавьте следующий код toothat метод toohave hello любой запрос tooany конечных точек службы hello, проверку подлинности как подшипника маркер, выданный службой Azure Active Directory от имени указанного клиента, для toohello доступа Azure AD Graph веб-службы: 

  ````
    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder IAppBuilder applicationBuilder, 
      System.Web.Http.HttpConfiguration HttpConfiguration configuration)
    {
      // IFilter is defined in System.Web.Http.dll.  
      System.Web.Http.Filters.IFilter authorizationFilter = 
        new System.Web.Http.AuthorizeAttribute(); // Defined in System.Web.Http.dll.configuration.Filters.Add(authorizationFilter);

      // SystemIdentityModel.Tokens.TokenValidationParameters is defined in    
      // System.IdentityModel.Token.Jwt.dll.
      SystemIdentityModel.Tokens.TokenValidationParameters tokenValidationParameters =     
        new TokenValidationParameters()
        {
          ValidAudience = "00000002-0000-0000-c000-000000000000"
        };

      // WindowsAzureActiveDirectoryBearerAuthenticationOptions is defined in 
      // Microsoft.Owin.Security.ActiveDirectory.dll
      Microsoft.Owin.Security.ActiveDirectory.
      WindowsAzureActiveDirectoryBearerAuthenticationOptions authenticationOptions =
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions()    {
        TokenValidationParameters = tokenValidationParameters,
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute hello appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a>Схема пользователей и групп
Azure Active Directory можно подготовить два типа ресурсов tooSCIM веб-служб.  Этими типами являются пользователи и группы.  

Ресурсы пользовательского идентифицируются идентификатор схемы hello, urn: ietf:params:scim:schemas:extension:enterprise:2.0:User, который входит в данную спецификацию протокола: http://tools.ietf.org/html/draft-ietf-scim-core-schema.  сопоставление по умолчанию Hello hello атрибутов пользователей в Azure Active Directory атрибуты toohello urn: ietf:params:scim:schemas:extension:enterprise:2.0:User ресурсов приведены в таблице 1, ниже.  

Ресурсы группы определяются hello идентификатор схемы, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.  В таблице 2 ниже показано сопоставление по умолчанию hello hello атрибутов групп в Azure Active Directory toohello атрибуты http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group ресурсов.  

### <a name="table-1-default-user-attribute-mapping"></a>Таблица 1. Сопоставление атрибутов пользователя по умолчанию
| Пользователь Azure Active Directory | urn:ietf:params:scim:schemas:extension:enterprise:2.0:User |
| --- | --- |
| IsSoftDeleted |активно |
| displayName |displayName |
| Facsimile-TelephoneNumber |phoneNumbers[type eq "fax"].value |
| givenName |name.givenName |
| jobTitle |title |
| mail |emails[type eq "work"].value |
| mailNickname |externalId |
| manager |manager |
| mobile |phoneNumbers[type eq "mobile"].value |
| objectId |id |
| postalCode |addresses[type eq "work"].postalCode |
| proxy-Addresses |emails[type eq "other"].Value |
| physical-Delivery-OfficeName |addresses[type eq "other"].Formatted |
| streetAddress |addresses[type eq "work"].streetAddress |
| surname |name.familyName |
| telephone-Number |phoneNumbers[type eq "work"].value |
| user-PrincipalName |userName |

### <a name="table-2-default-group-attribute-mapping"></a>Таблица 2. Сопоставление атрибутов группы по умолчанию
| Группа Azure Active Directory | http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group |
| --- | --- |
| displayName |externalId |
| mail |emails[type eq "work"].value |
| mailNickname |displayName |
| members |members |
| objectId |id |
| proxyAddresses |emails[type eq "other"].Value |

## <a name="user-provisioning-and-de-provisioning"></a>Подготовка и отзыв пользователей
Здравствуйте, следуя сообщений hello иллюстрации показано, что Azure Active Directory отправляет tooa службы SCIM toomanage жизненного цикла hello пользователя в другом хранилище удостоверений. Hello схема также показывает, как службы SCIM, реализовано с помощью библиотеки CLI hello предоставленная корпорацией Майкрософт для разработки, такие службы преобразования этих запросов в вызовы методов toohello поставщика.  

![][4]
*Рисунок 5. Последовательность действий при подготовке и отзыве пользователя*

1. Запросы Azure Active Directory hello службу для пользователя со значением атрибута externalId сопоставления значения атрибута mailNickname hello пользователя в Azure AD. запрос Hello выражается как запрос протокола передачи гипертекста (HTTP), как показано в примере, при котором jyoung приводится образец mailNickname пользователя в Azure Active Directory: 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  Если служба hello строится с помощью библиотек Общеязыковая инфраструктура hello, предоставляемых корпорацией Майкрософт для реализации службы SCIM, hello запрос преобразуется в toohello вызова метода запроса поставщика услуг hello.  Вот hello подпись этого метода. 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);
  ````
  Вот hello определение интерфейса Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters hello. 
  ````
    public interface IQueryParameters: 
      Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
        System.Collections.Generic.IReadOnlyCollection <Microsoft.SystemForCrossDomainIdentityManagement.IFilter> AlternateFilters 
        { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
      system.Collections.Generic.IReadOnlyCollection<string> ExcludedAttributePaths 
      { get; }
      System.Collections.Generic.IReadOnlyCollection<string> RequestedAttributePaths 
      { get; }
      string SchemaIdentifier 
      { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IFilter
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IFilter AdditionalFilter 
          { get; set; }
        string AttributePath 
          { get; } 
        Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator FilterOperator 
          { get; }
        string ComparisonValue 
          { get; }
    }

    public enum Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator
    {
        Equals
    }
  ````
  В следующий образец запроса для пользователя с указанным значением для атрибута externalId hello hello доступны следующие значения hello аргументов, передаваемых toohello метод запроса: 
  * parameters.AlternateFilters.Count: 1
  * parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"
  * parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"
  * correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"] 

2. Если hello ответа tooa запроса toohello веб-службу для пользователя, имеющего значение атрибута externalId, соответствующее значению атрибута mailNickname hello пользователь возвращает всех пользователей, Azure Active Directory запрашивает, hello службы подготовки пользователя соответствующий toohello один в Azure Active Directory.  Ниже приведен пример такого запроса. 
  ````
    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas":
      [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0User"],
      "externalId":"jyoung",
      "userName":"jyoung",
      "active":true,
      "addresses":null,
      "displayName":"Joy Young",
      "emails": [
        {
          "type":"work",
          "value":"jyoung@Contoso.com",
          "primary":true}],
      "meta": {
        "resourceType":"User"},
       "name":{
        "familyName":"Young",
        "givenName":"Joy"},
      "phoneNumbers":null,
      "preferredLanguage":null,
      "title":null,
      "department":null,
      "manager":null}
  ````
  Hello Общеязыковая инфраструктура библиотек, предоставляемых корпорацией Майкрософт для реализации службы SCIM преобразует этот запрос в toohello вызов метода Create поставщика услуг hello.  Метод Create Hello имеет следующую сигнатуру: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  В запрос tooprovision пользователя значение hello hello ресурсов аргумент является экземпляром hello Microsoft.SystemForCrossDomainIdentityManagement. Класс Core2EnterpriseUser, определенные в библиотеке Microsoft.SystemForCrossDomainIdentityManagement.Schemas hello.  Если tooprovision hello hello запрос пользователя завершается успешно, то hello реализация метода hello является ожидаемой tooreturn экземпляр hello Microsoft.SystemForCrossDomainIdentityManagement. Класс Core2EnterpriseUser, со значением hello свойство идентификатора hello установить toohello уникальный идентификатор hello нового пользователя.  

3. SCIM Azure Active Directory продолжается с помощью запроса службы hello hello текущее состояние этого пользователя с помощью запроса, таких как аппаратные tooupdate известные tooexist в хранилище удостоверение пользователя: 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  В службе, построенных с использованием предоставленных корпорацией Майкрософт для реализации службы SCIM библиотеки Общеязыковая инфраструктура hello hello запрос преобразуется в вызов toohello метод получения поставщика услуг hello.  Вот hello сигнатура метода извлечения hello. 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource and 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
    // are defined in Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> 
       Retrieve(
         Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
           parameters, 
           string correlationIdentifier);

    public interface 
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters:   
        IRetrievalParameters
        {
          Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
            ResourceIdentifier 
              { get; }
    }
    public interface Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier
    {
        string Identifier 
          { get; set; }
        string Microsoft.SystemForCrossDomainIdentityManagement.SchemaIdentifier 
          { get; set; }
    }
  ````
  В примере hello запроса tooretrieve hello текущего состояния пользователя hello значения свойств hello hello объекта, предоставленных в качестве значения hello аргумента параметров hello определяются следующим образом: 
  
  * Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

4. Если ссылочный атрибут toobe обновлена, затем Azure Active Directory запросы hello службы toodetermine ли hello текущее значение атрибута ссылки hello в хранилище удостоверений hello аппаратные hello службы уже соответствует значению hello этого атрибута в Azure Active Directory. Для пользователей, из какой hello запрашивается текущее значение в этом случае единственным атрибутом hello является атрибутом диспетчер hello. Ниже приведен пример toodetermine запрос ли атрибут manager hello объекта конкретного пользователя в настоящее время имеет определенное значение: 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  Здравствуйте, значение параметра запроса атрибуты hello, идентификатор, обозначает, удовлетворяющую hello выражение, предоставленное в качестве значения параметра запроса фильтра hello hello, если объект пользователя существует, то служба hello является ожидаемым toorespond с urn: ietf:params:scim:schemas: основной: 2.0:User или urn: ietf:params:scim:schemas:extension:enterprise:2.0:User ресурсов, включая только hello значение атрибута id этого ресурса.  Здравствуйте, значение hello **идентификатор** атрибут известен toohello запрашивающей стороны. Он включен в hello значение параметра запроса фильтра hello; Hello запрашиваются он предназначен фактически toorequest минимальное представление ресурса, удовлетворяющие hello критерий фильтра, как показатель того, является ли этих объекта существует.   

  Если служба hello строится с помощью библиотек Общеязыковая инфраструктура hello, предоставляемых корпорацией Майкрософт для реализации службы SCIM, hello запрос преобразуется в toohello вызова метода запроса поставщика услуг hello. Hello значение свойства hello объекта hello, предоставленных в качестве значения hello аргумента параметров hello выглядят следующим образом: 
  
  * parameters.AlternateFilters.Count: 2
  * parameters.AlternateFilters.ElementAt(x).AttributePath: "id"
  * parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"
  * parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals
  * parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"
  * parameters.RequestedAttributePaths.ElementAt(0): "id"
  * parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

  Здесь hello значение индекса hello x может быть равно 0 и hello значение y hello индекс может быть 1, или значение hello x может быть 1 и hello значение y может быть равно 0, в зависимости от порядка hello hello выражений параметр запроса фильтра hello.   

5. Ниже приведен пример запроса из Azure Active Directory tooan SCIM службы tooupdate пользователь: 
  ````
    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas": 
      [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"],
      "Operations":
      [
        {
          "op":"Add",
          "path":"manager",
          "value":
            [
              {
                "$ref":"http://.../scim/Users/2819c223-7f76-453a-919d-413861904646",
                "value":"2819c223-7f76-453a-919d-413861904646"}]}]}
  ````
  библиотеки Microsoft Общеязыковая инфраструктура Hello для реализации службы SCIM будут переводиться hello запроса toohello вызова метода Update поставщика услуг hello. Вот подпись hello hello метод обновления: 
  ````
    // System.Threading.Tasks.Tasks and 
    // System.Collections.Generic.IReadOnlyCollection<T>
    // are defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IPatch, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation, 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationName, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IPath and 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationValue 
    // are all defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 

    System.Threading.Tasks.Task Update(
      Microsoft.SystemForCrossDomainIdentityManagement.IPatch patch, 
      string correlationIdentifier);

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IPatch
    {
    Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase 
      PatchRequest 
        { get; set; }
    Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
      ResourceIdentifier 
        { get; set; }        
    }

    public class PatchRequest2: 
      Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase
    {
    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation> 
        Operations
        { get;}

    public void AddOperation(
      Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation operation);
    }

    public class PatchOperation
    {
    public Microsoft.SystemForCrossDomainIdentityManagement.OperationName 
      Name
      { get; set; }

    public Microsoft.SystemForCrossDomainIdentityManagement.IPath 
      Path
      { get; set; }

    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.OperationValue> Value
      { get; }

    public void AddValue(
      Microsoft.SystemForCrossDomainIdentityManagement.OperationValue value);
    }

    public enum OperationName
    {
      Add,
      Remove,
      Replace
    }

    public interface IPath
    {
      string AttributePath { get; }
      System.Collections.Generic.IReadOnlyCollection<IFilter> SubAttributes { get; }
      Microsoft.SystemForCrossDomainIdentityManagement.IPath ValuePath { get; }
    }

    public class OperationValue
    {
      public string Reference
      { get; set; }

      public string Value
      { get; set; }
    }
  ````
    В примере hello tooupdate запрос пользователя hello объекта, предоставленных в качестве значения hello аргумента исправление hello имеет значения этих свойств: 
  
  * ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"
  * (PatchRequest as PatchRequest2).Operations.Count: 1
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646
  * (PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646

6. toode Подготовка пользователя из хранилища удостоверений аппаратные службой SCIM, Azure AD отправляет запрос, например: 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  Если hello служба была создана с помощью библиотек Общеязыковая инфраструктура hello, предоставляемых корпорацией Майкрософт для реализации службы SCIM, hello запрос преобразуется в вызов toohello метод удаления поставщика услуг hello.   Подпись метода Delete будет выглядеть так: 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  значения этих свойств имеет Hello объекта, предоставленных в качестве значения hello аргумента resourceIdentifier hello в пример hello запроса toode подготовки пользователя: 
  
  * ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"
  * ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"

## <a name="group-provisioning-and-de-provisioning"></a>Подготовка и отзыв групп
Здравствуйте, следуя сообщений hello иллюстрации показано, что Azure AcD отправляет tooa SCIM toomanage hello на протяжении срока службы группы в другом хранилище удостоверений.  Эти сообщения отличаются от hello относится toousers тремя способами: 

* Схема Hello ресурс группы определяется как http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.  
* Запросы групп tooretrieve указания этого атрибута элементы hello — toobe, исключенные из любой ресурс, указанный в запросе toohello ответа.  
* Запросы toodetermine ли ссылочный атрибут имеет определенное значение — это запросы о hello элементов атрибута.  

![][5]
*Рисунок 6. Последовательность действий при подготовке и отзыве группы*

## <a name="related-articles"></a>Связанные статьи
* [Указатель статьей по управлению приложениями в Azure Active Directory](active-directory-apps-index.md)
* [Автоматизация пользователя подготовки и отзыва tooSaaS приложений](active-directory-saas-app-provisioning.md)
* [Настройка сопоставления атрибутов для подготовки пользователей](active-directory-saas-customizing-attribute-mappings.md)
* [Запись выражений для сопоставления атрибутов](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Фильтры области для подготовки пользователей](active-directory-saas-scoping-filters.md)
* [Уведомления о подготовке учетных записей](active-directory-saas-account-provisioning-notifications.md)
* [Список учебников по tooIntegrate приложений SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
