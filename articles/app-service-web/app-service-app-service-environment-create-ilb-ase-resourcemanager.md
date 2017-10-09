---
title: "aaaHow tooCreate ILB ASE с помощью Azure Resource Manager шаблонов | Документы Microsoft"
description: "Узнайте, как toocreate во внутренней нагрузки ASE балансировки, используя шаблоны Azure Resource Manager."
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 091decb6-b0de-42a1-9f2f-c18d9b2e67df
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: stefsch
ms.openlocfilehash: 16db20eccc232ccc73107fcc8291de180fb2a323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-ilb-ase-using-azure-resource-manager-templates"></a>Как tooCreate ILB ASE с помощью Azure Resource Manager шаблонов

> [!NOTE] 
> Эта статья является о hello v1 среды службы приложений. Имеется более новая версия hello среды службы приложений, удобнее toouse и выполняется на более мощный инфраструктуры. Дополнительные сведения о новой версии hello начинаться с hello toolearn [toohello введение среды службы приложений](../app-service/app-service-environment/intro.md).
>

## <a name="overview"></a>Обзор
Вместо общедоступного виртуального IP-адреса для создания среды службы приложений (ASE) можно использовать внутренний адрес виртуальной сети.  Этот внутренний адрес предоставляется Azure компонентом, называется hello внутренней подсистемы балансировки нагрузки (ILB).  ILB ASE можно создать с помощью портала Azure hello.  Ее также можно создать автоматически с помощью шаблонов Azure Resource Manager.  В этой статье рассматриваются действия hello и синтаксис требуется toocreate ASE ILB с помощью шаблонов диспетчера ресурсов Azure.

Автоматическое создание среды ASE с внутренним балансировщиком нагрузки предусматривает три шага:

1. Первый базовый ASE hello создается в виртуальной сети с помощью адреса балансировщик внутренней нагрузки вместо общедоступный VIP-адрес.  В ходе этого этапа имя корневого домена назначается toohello ILB ASE.
2. После передачи hello создания ILB ASE SSL-сертификат.  
3. Hello отправленный сертификат SSL явно назначен toohello ILB ASE свой SSL-сертификат «default».  SSL-сертификат будет использоваться для SSL tooapps трафика на hello ILB ASE при приложения hello осуществляется посредством hello общих корневого домена, назначенное toohello ASE (например https://someapp.mycustomrootcomain.com)

## <a name="creating-hello-base-ilb-ase"></a>Создание hello базы ILB ASE
Пример шаблона Azure Resource Manager и соответствующий файл параметров доступны на сайте GitHub [здесь][quickstartilbasecreate].

Большинство параметров hello в hello *azuredeploy.parameters.json* файла также ASEs привязан общедоступный VIP tooa описаны распространенные toocreating оба ASEs ILB.  Hello в списке вызовов выходные параметры особое примечание, или что являются уникальными, при создании ILB ASE:

* *interalLoadBalancingMode*: В большинстве случаев значение этого too3, что означает, что трафик HTTP/HTTPS на портах 80 и 443 и портов канала управления и данных hello прослушивал tooby службу hello FTP на hello ASE, привязанные tooan ILB выделяемый виртуальной сети Внутренний адрес.  Если это свойство имеет значение вместо too2, то только hello службы FTP, касающиеся порты (каналы данных и управления) будет привязан адрес tooan ILB пока hello трафик HTTP/HTTPS останется на общедоступный VIP hello.
* *DNS-суффикс*: этот параметр определяет hello по умолчанию корневого домена, который будет назначен toohello ASE.  В варианте открытый hello службе приложений Azure, hello по умолчанию для всех веб-приложений является корневым *azurewebsites.net*.  Однако поскольку ILB ASE внутренней tooa клиента виртуальной сети, не делает hello общедоступной смысле toouse службы по умолчанию корневого домена.  Вместо этого ASE с внутренним балансировщиком нагрузки необходимо назначить корневой домен по умолчанию, который целесообразно использовать в пределах внутренней виртуальной сети компании.  Например, использовать корневым доменом по умолчанию для гипотетического корпорации Contoso *внутренней contoso.com* для приложений, которые предполагаемого tooonly быть разрешаемым и доступно в виртуальной сети Contoso. 
* *ipSslAddressCount*: этот параметр автоматически — по умолчанию установлено значение 0 hello tooa *azuredeploy.json* файла, потому что ILB ASEs иметь только один адрес ILB.  Нет явного адреса SSL на ОСНОВЕ IP для ILB ASE и поэтому hello пул адресов SSL на ОСНОВЕ IP для ILB ASE необходимо задать toozero, в противном случае возникнет ошибка подготовки. 

Здравствуйте, один раз *azuredeploy.parameters.json* файла был введен для ASE ILB hello ILB ASE можно создать с помощью hello, следующий фрагмент кода Powershell.  Измените toomatch пути файла hello, где находятся файлы шаблонов диспетчера ресурсов Azure hello на компьютере.  Также не забудьте toosupply собственные значения для имени развертывания диспетчера ресурсов Azure hello и имя группы ресурсов.

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

После hello Azure Resource Manager шаблона является отправка может занять несколько часов, для создания toobe ILB ASE hello.  После завершения создания hello hello ILB ASE будут отображаться портал hello UX в список hello среды службы приложений для подписки hello, запустившего hello развертывания.

## <a name="uploading-and-configuring-hello-default-ssl-certificate"></a>Загрузка и настройка hello «Default» SSL-сертификата
Один раз hello создания ILB ASE, SSL-сертификат должен быть связан с hello ASE hello «default» используют сертификат SSL для установления tooapps подключения SSL.  Суффикс является продолжением гипотетический пример hello Contoso Corporation, если DNS, по умолчанию hello в ASE *внутренней contoso.com*, затем соединения слишком*https://some-random-app.internal-contoso.com*требуется SSL-сертификат, который допустим **.internal contoso.com*. 

Существуют различные способы tooobtain действительный сертификат SSL, включая внутренние ЦС, приобретая сертификат внешнего поставщика и с помощью самозаверяющего сертификата.  Вне зависимости от источника hello hello SSL-сертификат hello следующие атрибуты сертификатов, необходимые toobe настроен должным образом.

* *Тема*: этот атрибут должен быть задан слишком **.your корневого домена here.com*
* *Альтернативное имя субъекта*: этот атрибут должен включать оба **.your корневого домена here.com*, и **.scm.your-корневого-домена-here.com*.  Hello вторую запись hello обусловлено тем, toohello соединения SSL, SCM/Kudu сайт, связанный с каждого приложения будет осуществляться с использованием адреса формы hello *your-app-name.scm.your-root-domain-here.com*.

После получения действительного SSL-сертификата требуется выполнить еще два дополнительных подготовительных действия.  Hello SSL-сертификат должен toobe преобразуются и сохраняются как PFX-файл.  Помните, hello PFX-файл должен tooinclude всем промежуточным и корневые сертификаты, а также должен быть toobe, защищенным паролем.

Затем hello итоговые PFX-файл должен toobe преобразуется в строку base64, так как hello SSL-сертификат будет загружен с помощью шаблона диспетчера ресурсов Azure.  Поскольку шаблоны диспетчера ресурсов Azure — это текстовые файлы, hello PFX-файл должен toobe преобразуется в строку base64, поэтому ее можно добавить в качестве параметра шаблона hello.

фрагмент кода Hello Powershell ниже показан пример создания самозаверяющего сертификата, Экспорт сертификата hello в PFX-файл преобразования hello PFX-файл в кодировке base64 кодированную строку, а затем сохраняют hello base64 строка tooa отдельный файл в кодировке.  Здравствуйте код Powershell для кодировки base64 адаптирован на основании hello [блоге сценариев Powershell][examplebase64encoding].

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

    $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

    $fileName = "exportedcert.pfx"
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

    $fileContentBytes = get-content -encoding byte $fileName
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
    $fileContentEncoded | set-content ($fileName + ".b64")

После hello SSL-сертификат был успешно создан, и строка в кодировке base64 преобразованный tooa, hello пример шаблона диспетчера ресурсов Azure на GitHub для [Настройка SSL-сертификат по умолчанию hello] [ configuringDefaultSSLCertificate] может использоваться.

Здравствуйте, параметры в hello *azuredeploy.parameters.json* файла, перечислены ниже:

* *appServiceEnvironmentName*: hello имя hello настраивается ASE ILB.
* *existingAseLocation*: строка, содержащая текст hello регион Azure, где hello ILB ASE был развернут.  Например, South Central US.
* *pfxBlobString*: hello based64 кодировке строковое представление hello PFX-файл.  Используя приведенный выше фрагмент кода hello, будет копировать строку hello, содержащихся в «exportedcert.pfx.b64» и вставьте его в как значение hello hello *pfxBlobString* атрибута.
* *пароль*: hello пароль, используемый toosecure hello PFX-файл.
* *certificateThumbprint*: hello отпечатка сертификата.  Если это значение получалось из Powershell (например *$certificate. Отпечаток* из hello расположенного выше фрагмента кода), можно использовать значение hello в виде-является.  Однако если значение hello скопировать из диалогового окна сертификата Windows hello, помните, toostrip out hello лишних пробелов.  Hello *certificateThumbprint* должна выглядеть примерно так: AF3143EB61D43F6727842115BB7F17BBCECAECAE
* *certificateName*: идентификатор понятное строки по собственному выбору используется сертификат tooidentity hello.  Имя Hello используется как часть hello уникальный идентификатор диспетчера ресурсов Azure для hello *Microsoft.Web/certificates* сущность, представляющая hello SSL-сертификат.  Имя Hello **должен** заканчиваться hello следующий суффикс: \_yourASENameHere_InternalLoadBalancingASE.  Этот суффикс используется порталом hello как индикатор, у которого hello сертификат, используемый для обеспечения безопасности ASE поддержкой ILB.

Ниже приведен сокращенный пример файла *azuredeploy.parameters.json* .

    {
         "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json",
         "contentVersion": "1.0.0.0",
         "parameters": {
              "appServiceEnvironmentName": {
                   "value": "yourASENameHere"
              },
              "existingAseLocation": {
                   "value": "East US 2"
              },
              "pfxBlobString": {
                   "value": "MIIKcAIBAz...snip...snip...pkCAgfQ"
              },
              "password": {
                   "value": "PASSWORDGOESHERE"
              },
              "certificateThumbprint": {
                   "value": "AF3143EB61D43F6727842115BB7F17BBCECAECAE"
              },
              "certificateName": {
                   "value": "DefaultCertificateFor_yourASENameHere_InternalLoadBalancingASE"
              }
         }
    }

Здравствуйте, один раз *azuredeploy.parameters.json* файла было заполнено, SSL-сертификат по умолчанию hello, можно настроить с помощью hello, следующий фрагмент кода Powershell.  Измените toomatch пути файла hello, где находятся файлы шаблонов диспетчера ресурсов Azure hello на компьютере.  Также не забудьте toosupply собственные значения для имени развертывания диспетчера ресурсов Azure hello и имя группы ресурсов.

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

После hello Azure Resource Manager шаблона является отправка займет приблизительно 40 минут минут отдельно для каждого ASE переднего плана tooapply hello.  Например значение по умолчанию по размеру ASE, с помощью двух интерфейсных, hello шаблона будет использоваться вокруг один час и двадцать минут toocomplete.  Во время выполнения шаблона hello hello ASE не будет возможности tooscaled.  

По завершении шаблона hello приложений на hello ILB ASE может осуществляться по протоколу HTTPS и подключения hello будут защищены с помощью SSL-сертификат по умолчанию hello.  по умолчанию Hello SSL-сертификат будет использоваться при приложений на hello ILB ASE адресуются с помощью сочетания имени приложения hello, а также имя узла по умолчанию hello.  Например *https://mycustomapp.internal-contoso.com* будет использовать по умолчанию hello SSL-сертификат для **.internal contoso.com*.

Тем не менее так же, как приложения, работающие на нескольких клиентов службы открытых hello, разработчики могут также настроить пользовательские имена узлов для отдельных приложений и затем настройте уникальный привязки сертификатов SNI SSL для отдельных приложений.  

## <a name="getting-started"></a>Приступая к работе
tooget к работе с среды службы приложения, в разделе [tooApp введение среды службы](app-service-app-service-environment-intro.md)

Все статьи и как-для пользователя для среды службы приложений теперь доступны в hello [файл README для среды службы приложения](../app-service/app-service-app-service-environments-readme.md).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[quickstartilbasecreate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-create/
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/ 

