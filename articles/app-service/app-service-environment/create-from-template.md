---
title: "aaaCreate среду службы приложений Azure с помощью шаблона диспетчера ресурсов"
description: "Объясняет, как toocreate внешние или службе приложений Azure ILB среды с помощью шаблона диспетчера ресурсов"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 6eb7d43d-e820-4a47-818c-80ff7d3b6f8e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: c8aeedee675a6e931169b725ee916cc7fa8f762f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ase-by-using-an-azure-resource-manager-template"></a>Создание среды ASE с помощью шаблона Azure Resource Manager

## <a name="overview"></a>Обзор
Среды службы приложений Azure (ASE) создаются с помощью конечной точки с доступом к Интернету или конечной точки с внутренним адресом в виртуальной сети Azure. Если при создании внутренней конечной точки эта конечная точка предоставляется компонентом Azure, она называется внутренним балансировщиком нагрузки. Hello ASE на внутренний IP-адрес, называется ILB ASE. Hello ASE с общедоступной конечной точки, называется внешних ASE. 

ASE могут создаваться с помощью портала Azure hello или шаблона диспетчера ресурсов Azure. В этой статье рассматриваются шаги hello и синтаксиса, toocreate внешних ASE или ILB ASE с помощью шаблонов диспетчера ресурсов. toocreate ASE в hello портал Azure. в статье toolearn [сделать внешних ASE] [ MakeExternalASE] или [сделать ILB ASE][MakeILBASE].

При создании ASE в hello портал Azure можно создать в hello же время или выберите уже существующий toodeploy виртуальной сети в виртуальной сети. При создании ASE из шаблона необходимо: 

* Создать виртуальную сеть Resource Manager.
* Создать подсеть в этой виртуальной сети. Мы рекомендуем размер подсети ASE `/25` с 128 адресов tooaccomodate будущего роста. После создания hello ASE hello размер нельзя изменить.
* Идентификатор ресурса Hello из виртуальной сети. Эти сведения можно получить из hello портал Azure в группе свойств виртуальной сети.
* Hello подписку, которую вы хотите toodeploy в.
* Hello место toodeploy в.

tooautomate вашей ASE создания:

1. Создание hello ASE на основе шаблона. При создании внешнего ASE это последний шаг. При создании ILB ASE, существует несколько toodo несколько вещей.

2. После создания ASE с внутренним балансировщиком нагрузки отправляется SSL-сертификат, соответствующий домену ASE с внутренним балансировщиком нагрузки.

3. Hello отправленный сертификат SSL назначен toohello ILB ASE свой SSL-сертификат «default».  Этот сертификат используется для tooapps трафик SSL на hello ILB ASE при использовании hello общий корневой домен, назначенный toohello ASE (например, https://someapp.mycustomrootcomain.com).


## <a name="create-hello-ase"></a>Создание hello ASE
Шаблон Resource Manager, с помощью которого создается ASE, и соответствующий файл параметров доступны [в примере][quickstartasev2create], размещенном на сайте GitHub.

Toomake ILB ASE, используйте эти шаблона диспетчера ресурсов [примеры][quickstartilbasecreate]. Они обслуживающие toothat варианта использования. Большинство параметров hello в hello *azuredeploy.parameters.json* файла являются общие toohello Создание ILB ASEs и внешних ASEs. Hello ниже указаны параметры особое примечание, или, являются уникальными, при создании ILB ASE:

* *interalLoadBalancingMode*: В большинстве случаев значение этого too3, что означает, что трафик HTTP/HTTPS на портах 80 и 443 и портов канала управления и данных hello прослушивал tooby службу hello FTP на hello ASE, будет привязанного tooan ILB выделенной виртуальной сети Внутренний адрес. Если это свойство имеет значение too2, только hello FTP относящихся к службам порты (каналы данных и управления), связанный tooan адрес ILB. на общедоступный VIP hello остается Hello трафик HTTP/HTTPS.
* *DNS-суффикс*: этот параметр определяет корневой домен по умолчанию hello, назначенный toohello ASE. В варианте открытый hello службе приложений Azure, hello по умолчанию для всех веб-приложений является корневым *azurewebsites.net*. Так как ILB ASE внутренней tooa клиента виртуальной сети, он не становится корневой домен по умолчанию hello общедоступной смысле toouse службы. Вместо этого ASE с внутренним балансировщиком нагрузки необходимо назначить корневой домен по умолчанию, который целесообразно использовать в пределах внутренней виртуальной сети компании. Предположим, например, Корпорация Contoso использует корневым доменом по умолчанию из *внутренней contoso.com* для приложений, которые предполагаемого toobe разрешаемым и доступен только в пределах виртуальной сети Contoso. 
* *ipSslAddressCount*: этот параметр по умолчанию значение 0 hello tooa *azuredeploy.json* файла, потому что ILB ASEs иметь только один адрес ILB. Для ASE с внутренним балансировщиком нагрузки нет явно заданных адресов SSL на основе IP, Таким образом пул адресов SSL на ОСНОВЕ IP для ILB ASE hello должно быть задано toozero. В противном случае произойдет ошибка подготовки. 

После hello *azuredeploy.parameters.json* заполняется файл, создать с помощью фрагмента кода PowerShell hello hello ASE. Изменять hello пути toomatch hello диспетчера ресурсов файл шаблона расположения файлов на компьютере. Запомните toosupply собственные значения для имени развертывания диспетчера ресурсов hello и имя группы ресурсов hello:

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Это занимает около часа для создания toobe ASE hello. Затем hello ASE отображается портал hello в список hello ASEs для подписки hello, запустившего hello развертывания.

## <a name="upload-and-configure-hello-default-ssl-certificate"></a>Загрузка и Настройка SSL-сертификат hello «default»
SSL-сертификата необходимо связать с hello ASE как SSL-сертификат «default» hello, tooapps подключений SSL используется tooestablish. Если DNS-суффикс по умолчанию hello в ASE *внутренней contoso.com*, toohttps://some-random-app.internal-contoso.com подключения требуется SSL-сертификат, который допустим **.internal contoso.com* . 

Можно получить действительный SSL-сертификат от внутреннего центра сертификации, приобрести у внешнего поставщика или использовать самозаверяющий сертификат. Вне зависимости от источника hello hello SSL-сертификат hello следующие атрибуты сертификата должен быть настроен правильно:

* **Тема**: этот атрибут должен быть задан слишком **.your корневого домена here.com*.
* **Subject Alternative Name** — этот атрибут должен содержать два значения: *.имя_корневого_домена.com* и *.scm.имя_корневого_домена.com*. SCM/Kudu сайта, связанные с каждой приложением toohello подключений SSL использует адрес формы hello *your-app-name.scm.your-root-domain-here.com*.

После получения действительного SSL-сертификата требуется выполнить еще два дополнительных подготовительных действия. Преобразования и сохранения hello SSL-сертификата в PFX-файл. Помните, что hello PFX-файл включает всем промежуточным и корневые сертификаты. Защитите его паролем.

Hello PFX-файл должен toobe преобразуется в строку base64, так как сертификат SSL hello отправки с помощью шаблона диспетчера ресурсов. Поскольку шаблоны диспетчера ресурсов — это текстовые файлы, hello PFX-файл может быть преобразована в строку в кодировке base64. Таким образом, ее можно добавить в качестве параметра шаблона hello.

Используйте следующий фрагмент кода PowerShell hello.

* создать самозаверяющий сертификат;
* Экспорт сертификата hello в PFX-файл.
* Преобразуйте hello PFX-файла в строку в кодировке base64.
* Сохраните hello строки в кодировке base64 tooa отдельный файл. 

Этот код PowerShell для кодировки base64 адаптирован на основании hello [PowerShell скрипты блог][examplebase64encoding]:

        $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

        $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
        $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

        $fileName = "exportedcert.pfx"
        Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

        $fileContentBytes = get-content -encoding byte $fileName
        $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
        $fileContentEncoded | set-content ($fileName + ".b64")

Преобразовать строки в кодировке base64 tooa hello SSL-сертификат успешно создан, используйте шаблон диспетчера ресурсов пример hello [настроить сертификат SSL по умолчанию hello] [ quickstartconfiguressl] на GitHub. 

Здравствуйте, параметры в hello *azuredeploy.parameters.json* файл перечисленные здесь:

* *appServiceEnvironmentName*: hello имя hello настраивается ASE ILB.
* *existingAseLocation*: строка, содержащая текст hello регион Azure, где hello ILB ASE был развернут.  Например, South Central US.
* *pfxBlobString*: hello представление based64 зашифрованную строку hello PFX-файл. Используйте приведенный выше фрагмент кода hello и скопируйте строку hello, содержащихся в «exportedcert.pfx.b64». Вставьте его в виде значения hello hello *pfxBlobString* атрибута.
* *пароль*: hello пароль, используемый toosecure hello PFX-файл.
* *certificateThumbprint*: hello отпечатка сертификата. Если это значение получалось из PowerShell (например, *$certificate. Отпечаток* из hello расположенного выше фрагмента кода), можно использовать значение hello как есть. При копировании hello значение из диалоговое окно сертификата Windows hello помните toostrip out hello лишних пробелов. Hello *certificateThumbprint* должна выглядеть примерно так AF3143EB61D43F6727842115BB7F17BBCECAECAE.
* *certificateName*: идентификатор понятное строки по собственному выбору используется сертификат tooidentity hello. Имя Hello используется как часть hello уникальный идентификатор диспетчера ресурсов для hello *Microsoft.Web/certificates* сущность, представляющая hello SSL-сертификат. Имя Hello *должен* заканчиваться hello следующий суффикс: \_yourASENameHere_InternalLoadBalancingASE. Hello портал Azure использует этот суффикс является признаком того, что сертификат hello используется toosecure ASE поддержкой ILB.

Ниже приведен сокращенный пример файла *azuredeploy.parameters.json*.

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

После hello *azuredeploy.parameters.json* файл заполнено, Настройка SSL-сертификат по умолчанию hello с помощью фрагмента кода PowerShell hello. Изменить toomatch пути файла hello, где находятся файлы шаблонов диспетчера ресурсов hello на компьютере. Запомните toosupply собственные значения для имени развертывания диспетчера ресурсов hello и имя группы ресурсов hello:

     $templatePath="PATH\azuredeploy.json"
     $parameterPath="PATH\azuredeploy.parameters.json"

     New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Занимает примерно 40 минут отдельно для каждого ASE внешнего интерфейса tooapply hello. Например ASE с размерами по умолчанию, использующий два интерфейсных, hello шаблона занимает примерно 1 час и toocomplete 20 минут. Во время шаблона hello hello ASE нельзя масштабировать.  

По завершении шаблона hello приложений на hello ILB ASE может осуществляться по протоколу HTTPS. Hello подключения защищены с помощью SSL-сертификат по умолчанию hello. SSL-сертификат по умолчанию Hello используется, когда приложения на hello ILB ASE адресуются с помощью комбинации имени приложения hello, а также имя узла по умолчанию hello. Например, https://mycustomapp.internal-contoso.com используется сертификат SSL по умолчанию hello для **.internal contoso.com*.

Тем не менее так же, как приложения, которые работают на общей многопользовательской службы hello, разработчики можно настроить пользовательские имена узлов для отдельных приложений. и уникальные привязки сертификатов SNI SSL.

## <a name="app-service-environment-v1"></a>Среда службы приложений версии 1 ##
Среда службы приложений имеет две версии: ASEv1 и ASEv2. предшествующий сведения Hello был основан на ASEv2. В этом разделе представлены hello различия между ASEv1 и ASEv2.

В ASEv1 можно управлять всеми ресурсами hello вручную. Включающий интерфейсных hello, сотрудников и IP-адреса для SSL на основе IP. Прежде чем можно масштабировать плана служб приложений, требуется расширение hello рабочего пула, которые должны toohost его.

ASEv1 использует модель ценообразования отличную от ASEv2. В ASEv1 вы платите за каждое выделенное ядро, включая ядра, используемые для внешних интерфейсов и рабочих процессов, которые не содержат рабочие нагрузки. В ASEv1 размер максимальный масштаб по умолчанию hello ASE составляет 55 общее количество узлов. включая рабочие роли и внешние интерфейсы. Одно из преимуществ tooASEv1 — могут быть развернуты в классической виртуальной сети и диспетчер ресурсов виртуальной сети. toolearn Дополнительные сведения о ASEv1, в разделе [введение v1 среды службы приложений][ASEv1Intro].

toocreate ASEv1 с помощью шаблона диспетчера ресурсов, в разделе [создания v1 ILB ASE с помощью шаблона диспетчера ресурсов][ILBASEv1Template].


<!--Links-->
[quickstartilbasecreate]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-ilb-create
[quickstartasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asev2-create
[quickstartconfiguressl]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl
[quickstartwebapponasev2create]: http://azure.microsoft.com/documentation/templates/201-web-app-asp-app-on-asev2-create
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[ILBASEv1Template]: ../../app-service-web/app-service-app-service-environment-create-ilb-ase-resourcemanager.md
