---
title: "aaaBind существующие пользовательские SSL-сертификатов tooAzure веб-приложений | Документы Microsoft"
description: "Узнайте tootoobind пользовательские SSL сертификат tooyour веб-приложения, внутреннего сервера мобильного приложения или приложения API в службе приложений Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 5d5bf588-b0bb-4c6d-8840-1b609cfb5750
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3503ba9f96c8ea8d18451e8bf9a9b441797ef44d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-tooazure-web-apps"></a>Привязать существующий пользовательский SSL сертификат tooAzure веб-приложений

Веб-приложения Azure — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости. В этом учебнике показано, как toobind пользовательские SSL сертификат слишком приобретенные у доверенного центра сертификации, который[веб-приложениях Azure](app-service-web-overview.md). После завершения вы будете иметь доступ tooaccess веб-приложения в конечной точки HTTPS hello своего пользовательского домена DNS.

![Веб-приложение с настраиваемым SSL-сертификатом](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

Из этого руководства вы узнаете, как выполнять такие задачи:

> [!div class="checklist"]
> * Выбор более высокой ценовой категории.
> * Привязка к пользовательской tooApp сертификат SSL службы
> * Принудительное использование HTTPS для приложения.
> * Автоматизация привязки SSL-сертификата с помощью скриптов.

> [!NOTE]
> Если вам требуется tooget пользовательский сертификат SSL, можно получить в hello портал Azure напрямую и привязать его tooyour веб-приложения. Выполните hello [сертификатов службы приложений учебника](web-sites-purchase-ssl-web-site.md).

## <a name="prerequisites"></a>Предварительные требования

toocomplete этого учебника:

- [Создано приложение службы приложений](/azure/app-service/).
- [Сопоставление пользовательских веб-приложения tooyour DNS имя](app-service-web-tutorial-custom-domain.md)
- Получен SSL-сертификат из доверенного центра сертификации.

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a>Требования к SSL-сертификату

toouse сертификатов в службе приложений hello сертификат должен удовлетворять все hello следующие требования:

* должен быть подписан доверенным центром сертификации;
* должен быть экспортирован в PFX-файл, защищенный паролем;
* должен содержать закрытый ключ длиной не менее 2048 битов;
* Содержит все промежуточные сертификаты в цепочке сертификатов hello

> [!NOTE]
> **Сертификаты с шифрованием на основе эллиптических кривых (ECC)** можно использовать со службой приложений, но это не описано в этой статье. Работа с вашего центра сертификации на toocreate ECC hello точные действия сертификатов.

## <a name="prepare-your-web-app"></a>Подготовка веб-приложения

toobind пользовательские SSL-сертификатов tooyour веб-приложения вашей [план служб приложений](https://azure.microsoft.com/pricing/details/app-service/) должен находиться в hello **основные**, **Стандартная**, или **Premium** уровня. На этом шаге вы убедитесь, что веб-приложения в hello поддерживается ценовой категории.

### <a name="log-in-tooazure"></a>Войдите в tooAzure

Откройте hello [портал Azure](https://portal.azure.com).

### <a name="navigate-tooyour-web-app"></a>Перейдите tooyour веб-приложения

Hello в левом меню, щелкните **службы приложений**и щелкните имя веб-приложения hello.

![Выбор веб-приложения](./media/app-service-web-tutorial-custom-ssl/select-app.png)

Выбран на странице управления hello веб-приложения.  

### <a name="check-hello-pricing-tier"></a>Проверьте hello ценовой категории

В левой навигационной hello приложения веб-страницы, прокрутите toohello **параметры** , выберите **масштаб (план службы приложений)**.

![Меню увеличения масштаба](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

Убедитесь том, что веб-приложения не hello toomake **Free** или **Shared** уровня. Текущая ценовая категория веб-приложения выделена синей рамкой.

![Проверка ценовой категории](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

Пользовательские SSL не поддерживается в hello **Free** или **Shared** уровня. Если вам требуется tooscale вверх, выполните действия hello в следующем разделе hello. В противном случае закройте hello **выберите ценовую категорию** страницы и пропуска слишком[отправка и привязать SSL-сертификат](#upload).

### <a name="scale-up-your-app-service-plan"></a>Изменение уровня плана службы приложений

Выберите один из hello **основные**, **Стандартная**, или **Premium** уровней.

Нажмите кнопку **Выбрать**.

![Выбор ценовой категории](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

При появлении hello после уведомления hello шкалы операция завершена.

![Уведомление об увеличении масштаба](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a>Привязка SSL-сертификата

Вам будут готовы tooupload веб-приложения tooyour сертификат SSL.

### <a name="merge-intermediate-certificates"></a>Объединение промежуточных сертификатов

Если ваш центр сертификации дает несколько сертификатов в цепочке сертификатов hello, требуются сертификаты toomerge hello в порядке. 

toodo это, откройте каждого сертификата полученный в текстовом редакторе. 

Создание файла для объединенных сертификат hello, с именем _mergedcertificate.crt_. В текстовом редакторе скопируйте содержимое hello каждый сертификат в этот файл. порядок Hello сертификатов должен выглядеть hello следующий шаблон:

```
-----BEGIN CERTIFICATE-----
<your Base64 encoded SSL certificate>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 1>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 2>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded root certificate>
-----END CERTIFICATE-----
```

### <a name="export-certificate-toopfx"></a>Экспорт сертификата tooPFX

Экспорт объединенных SSL-сертификат с закрытым ключом hello, ваш запрос на сертификат, созданный с.

Если запрос сертификата был создан с помощью OpenSSL, то вы создали файл закрытого ключа. tooexport tooPFX ваш сертификат, запустите следующую команду hello. Замените заполнители hello  _&lt;файла закрытого ключа >_ и  _&lt;слияние сертификат файл->_.

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

При появлении запроса определите пароль для экспорта. Этот пароль будет использоваться при отправке вашего SSL сертификат tooApp службы позже.

Если используется IIS или _Certreq.exe_ toogenerate запроса на сертификат, установить hello сертификат tooyour локальный компьютер и затем [экспорта сертификата tooPFX hello](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).

### <a name="upload-your-ssl-certificate"></a>Передача SSL-сертификата

tooupload SSL-сертификат, нажмите кнопку **SSL-сертификаты** в hello слева навигации веб-приложения.

Щелкните **Отправить сертификат**.

В разделе **PFX-файл сертификата** выберите свой PFX-файл. В **пароль сертификата**, введите пароль hello, созданный при экспорте hello PFX-файла.

Щелкните **Отправить**.

![Передача сертификата](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

По завершении отправке сертификата службы приложений он появится в hello **SSL-сертификаты** страницы.

![Сертификат добавлен](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a>Привязка SSL-сертификата

В hello **привязки SSL** щелкните **добавить привязку**.

В hello **Добавление привязки SSL** используйте hello раскрывающихся списках tooselect hello домена имя toosecure и toouse сертификат hello.

> [!NOTE]
> Если переданы свой сертификат, но не видите hello имена доменов в hello **Hostname** раскрывающийся список, обновите страницу браузера hello.
>
>

В **тип SSL**выберите ли toouse  **[Указание имени сервера (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  или SSL на основе IP-адресов.

- **SSL на основе SNI** позволяет добавить несколько привязок SSL на основе SNI. Этот параметр позволяет нескольким toosecure сертификаты SSL несколько доменов на hello же IP-адрес. Большинство современных браузеров (включая Internet Explorer, Chrome, Firefox и Opera) поддерживает SNI (более подробную информацию о поддержки браузеров можно найти в статье [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication) (Указание имени сервера)).
- **SSL на основе IP-адреса** позволяет добавить только одну привязку SSL на основе IP-адреса. Этот параметр позволяет только один toosecure сертификат SSL выделенный общедоступный IP-адрес. toosecure несколько доменов, необходимо защитить их с помощью hello же SSL-сертификат. Этот вариант hello традиционных для привязки SSL.

Щелкните **Добавить привязку**.

![Привязка SSL-сертификата](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

По завершении отправке сертификата службы приложений он появится в hello **привязки SSL** разделы.

![Сертификат, привязанный tooweb приложения](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a>Переназначение записи A для SSL на основе IP-адреса

Если вы не используете SSL на основе IP в веб-приложении, пропустите слишком[теста HTTPS для пользовательского домена](#test).

По умолчанию веб-приложение использует общий общедоступный IP-адрес. После привязки сертификата с помощью SSL на основе IP-адреса служба приложений создает выделенный IP-адрес для вашего веб-приложения.

Если веб-приложение A записей tooyour сопоставлена, обновления реестра домена этот новый, выделенный IP-адрес.

Веб-приложения **пользовательский домен** страница обновляется при hello нового, выделенного IP-адрес. [Скопируйте этот IP-адрес](app-service-web-tutorial-custom-domain.md#info), затем [преобразования hello запись](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis новый IP-адрес.

<a name="test"></a>

## <a name="test-https"></a>Тестирование HTTPS

Все, что теперь покинул toodo — toomake, убедившись в наличии HTTPS для вашего домена. В различных браузерах Обзор слишком`https://<your.custom.domain>` toosee, он обслуживающего веб-приложения.

![Приложение портала навигации tooAzure](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> Если веб-приложение выдает ошибки проверки сертификата, вероятно, вы используете самозаверяющий сертификат.
>
> Если это не так hello, вы может были пропущены промежуточные сертификаты при экспорте сертификата toohello PFX-файл.

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a>Принудительное использование HTTPS

Служба приложений *не* принуждает использовать протокол HTTPS, чтобы кто угодно мог обратиться к веб-приложению с помощью протокола HTTP. tooenforce HTTPS для веб-приложения, определите правило подстановки в hello _web.config_ файла для веб-приложения. Приложение службы использует этот файл, независимо от языковой платформе hello веб-приложения.

> [!NOTE]
> Для каждого языка используется определенное перенаправление запросов. ASP.NET MVC можно использовать hello [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) фильтра вместо правило подстановки hello в _web.config_.

Если вы разработчик для .NET, то этот файл должен быть вам в общем и целом знаком. Он находится в корне hello решения.

Кроме того, если вы программируете на PHP, Node.js, Python или Java, существует вероятность того, что этот файл создан от вашего имени в службе приложений.

Подключения конечной точки FTP tooyour веб-приложения в соответствии с инструкциями hello в [развертывание вашего приложения tooAzure службы приложений с помощью FTP/S](app-service-deploy-ftp.md).

Этот файл должен находиться в каталоге _/home/site/wwwroot_. Если нет, создайте _web.config_ файл в этой папке с hello следующий XML-код:

```xml   
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <!-- BEGIN rule ELEMENT FOR HTTPS REDIRECT -->
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
        <!-- END rule ELEMENT FOR HTTPS REDIRECT -->
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

Для существующей _web.config_ файл, скопировать весь hello `<rule>` элемент в вашей _web.config_ `configuration/system.webServer/rewrite/rules` элемент. Если существуют другие `<rule>` элементов в вашей _web.config_, скопировать hello месте `<rule>` перед hello других элемент `<rule>` элементов.

Это правило возвращает toohello HTTP 301 (постоянное перенаправление) по протоколу HTTPS, каждый раз, когда пользователь hello делает веб-приложение tooyour запроса HTTP. Например, он перенаправляет `http://contoso.com` слишком`https://contoso.com`.

Дополнительные сведения о модуль переопределения URL-адреса IIS hello. в разделе hello [переопределения URL-адресов](http://www.iis.net/downloads/microsoft/url-rewrite) документации.

## <a name="enforce-https-for-web-apps-on-linux"></a>Принудительное использование HTTPS для веб-приложений на платформе Linux

Служба приложений на платформе Linux *не* принуждает использовать протокол HTTPS, чтобы кто угодно мог обратиться к веб-приложению с помощью протокола HTTP. tooenforce HTTPS для веб-приложения, определите правило подстановки в hello _.htaccess_ файла для веб-приложения. 

Подключения конечной точки FTP tooyour веб-приложения в соответствии с инструкциями hello в [развертывание вашего приложения tooAzure службы приложений с помощью FTP/S](app-service-deploy-ftp.md).

В _/home/site/wwwroot_, создайте _.htaccess_ файл с hello, следующий код:

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

Это правило возвращает toohello HTTP 301 (постоянное перенаправление) по протоколу HTTPS, каждый раз, когда пользователь hello делает веб-приложение tooyour запроса HTTP. Например, он перенаправляет `http://contoso.com` слишком`https://contoso.com`.

## <a name="automate-with-scripts"></a>Автоматизация с помощью сценариев

Можно автоматизировать привязки SSL для веб-приложения с помощью скриптов, с помощью hello [Azure CLI](/cli/azure/install-azure-cli) или [Azure PowerShell](/powershell/azure/overview).

### <a name="azure-cli"></a>Инфраструктура CLI Azure

Hello, следующая команда отправляет экспортированного PFX-файла и возвращает отпечаток hello.

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

Hello следующая команда добавляет привязки на основе SNI SSL, с помощью отпечатка hello из предыдущей команды hello.

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a>Azure PowerShell

Hello следующая команда отправляет экспортированного PFX-файла и добавляет привязку на основе SNI SSL.

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a>Дальнейшие действия

Из этого руководства вы узнали, как выполнять такие задачи:

> [!div class="checklist"]
> * Выбор более высокой ценовой категории.
> * Привязка к пользовательской tooApp сертификат SSL службы
> * Принудительное использование HTTPS для приложения.
> * Автоматизация привязки SSL-сертификата с помощью скриптов.

Как переместить следующий учебник toolearn toohello toouse сети доставки содержимого Azure.

> [!div class="nextstepaction"]
> [Добавление сети доставки содержимого (CDN) tooan службы приложений Azure](app-service-web-tutorial-content-delivery-network.md)
