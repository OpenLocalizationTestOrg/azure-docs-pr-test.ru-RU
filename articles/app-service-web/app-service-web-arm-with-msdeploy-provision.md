---
title: "aaaDeploy использование MSDeploy с узла и ssl-сертификат веб-приложения"
description: "Использовать веб-приложения с помощью MSDeploy и настройка пользовательское имя узла и SSL-сертификат toodeploy шаблона диспетчера ресурсов Azure"
services: app-service\web
manager: erikre
documentationcenter: 
author: jodehavi
ms.assetid: 66366a72-cef7-4d75-8779-f4d32ed33cf7
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2016
ms.author: jodehavi
ms.openlocfilehash: ac13f4a7d14ae182e8e7ced5adff30491422d1e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a>Развертывание веб-приложения с использованием MSDeploy, пользовательского имени узла и SSL-сертификата
В этом руководстве описывается создание конца в конец развертывания для веб-приложение Azure, используя MSDeploy, а также добавляет пользовательское имя узла и шаблон ARM toohello сертификат SSL.

Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

### <a name="create-sample-application"></a>Создание примера приложения
Здесь описывается развертывание веб-приложения ASP.NET. Hello первым шагом является toocreate простого веб-приложения (или можно выбрать toouse существующего - в противном случае этот шаг можно пропустить).

Откройте Visual Studio 2015 и последовательно выберите «Файл» > «Создать проект». В диалоговом окне приветствия, появившемся выберите Web > веб-приложения ASP.NET. В списке шаблонов выберите Web и щелкните шаблон MVC hello. Выберите *изменить тип проверки подлинности* слишком*без проверки подлинности*. Это просто toomake hello образец приложения как можно более простыми.

На этом этапе вы получите основные ASP.Net web app готов toouse как часть процесса развертывания.

### <a name="create-msdeploy-package"></a>Создание пакета MSDeploy
Следующим шагом является toocreate hello пакета toodeploy hello web app tooAzure. toodo, сохранить проект и запустите из командной строки hello hello следующее:

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

Это будет создан ZIP-пакет в папке PackageLocation hello. Hello приложения готов к работе теперь toobe развертывания, который теперь можно построить toodo шаблона диспетчера ресурсов Azure.

### <a name="create-arm-template"></a>Создание шаблона ARM
Начнем с базового шаблона ARM, который позволит создать веб-приложение и план размещения. (Обратите внимание, что для краткости параметры и переменные опущены.)

    {
        "name": "[parameters('appServicePlanName')]",
        "type": "Microsoft.Web/serverfarms",
        "location": "[resourceGroup().location]",
        "apiVersion": "2014-06-01",
        "dependsOn": [ ],
        "tags": {
            "displayName": "appServicePlan"
        },
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "sku": "[parameters('appServicePlanSKU')]",
            "workerSize": "[parameters('appServicePlanWorkerSize')]",
            "numberOfWorkers": 1
        }
    },
    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        }
    }

Далее необходимо tootake toomodify hello web app ресурсов вложенных ресурсов MSDeploy. Это будет разрешить вы tooreference hello пакет, созданный ранее и сообщите пакета диспетчера ресурсов Azure toouse MSDeploy toodeploy hello toohello веб-приложения Azure. Hello ниже показан hello Microsoft.Web/sites ресурс с вложенными hello MSDeploy ресурсов:

    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        },
        "resources": [
            {
                "name": "MSDeploy",
                "type": "extensions",
                "location": "[resourceGroup().location]",
                "apiVersion": "2015-08-01",
                "dependsOn": [
                    "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
                ],
                "tags": {
                    "displayName": "webDeploy"
                },
                "properties": {
                    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]",
                    "dbType": "None",
                    "connectionString": "",
                    "setParameters": {
                        "IIS Web Application Name": "[variables('webAppName')]"
                    }
                }
            }
        ]
    }

Теперь можно заметить, что hello MSDeploy ресурсов принимает **packageUri** свойство, которое определяется следующим образом:

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

Это **packageUri** принимает hello uri учетной записи хранилища, который учетную запись хранилища toohello, где нужно будет загрузить zip вашего пакета для точек. Hello Azure Resource Manager будет использовать [подписей общего доступа](../storage/common/storage-dotnet-shared-access-signature-part-1.md) пакета hello toopull вниз локально из учетной записи хранения hello при развертывании шаблона hello. Этот процесс будет автоматизирован через сценарий PowerShell, отправить пакет hello и вызывает hello toocreate ключа, hello API управления Azure и передавать их в шаблоне hello в качестве параметров (*_artifactsLocation* и *_artifactsLocationSasToken*). Вам потребуется toodefine параметры для папки hello, а пакет hello filename — контейнер хранилища отправленного toounder hello.

Затем следует записать tooadd в другой вложенный ресурсов toosetup hello имя узла привязки tooleverage пользовательского домена. Будет первой необходимости tooensure владельцем hello hostname и настроить toobe протестирован Azure принадлежит вам — см. [настроить пользовательское доменное имя в службе приложений Azure](app-service-web-tutorial-custom-domain.md). После этого можно добавить следующий шаблон tooyour в разделе "hello Microsoft.Web/sites ресурсов" hello.

    {
        "apiVersion": "2015-08-01",
        "type": "hostNameBindings",
        "name": "www.yourcustomdomain.com",
        "dependsOn": [
            "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
        ],
        "properties": {
            "domainId": null,
            "hostNameType": "Verified",
            "siteName": "variables('webAppName')"
        }
    }

Наконец необходимо tooadd другой ресурс верхнего уровня, Microsoft.Web/certificates. Этот ресурс будет содержать SSL-сертификата, будут существовать на приветствия же уровня в качестве веб-приложения и размещения плана.

    {
        "name": "[parameters('certificateName')]",
        "apiVersion": "2014-04-01",
        "type": "Microsoft.Web/certificates",
        "location": "[resourceGroup().location]",
        "properties": {
            "pfxBlob": "pfx base64 blob",
            "password": "some pass"
        }
    }

Вам потребуется toohave действительного сертификата SSL в порядке tooset этого ресурса. После этого действительный сертификат необходимо tooextract hello pfx байтов как строка base64. Один из вариантов tooextract это hello toouse следующую команду PowerShell:

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

Затем можно передать таким как шаблон развертывания параметра tooyour ARM.

На этом этапе hello ARM шаблон готов.

### <a name="deploy-template"></a>Развертывание шаблона
Здравствуйте, последние действия имеют toopiece этот все вместе в развертывание полной начала до конца. toomake развертывания проще, можно использовать hello **Deploy-AzureResourceGroup.ps1** сценарий PowerShell, которое добавляется при создании проекта группы ресурсов Azure в Visual Studio toohelp с артефакты, необходимые на загрузку шаблон Hello. Он требует toohave создал учетную запись хранилища, требуется toouse заранее. В этом примере я создал учетную запись общего хранилища для отправки toobe package.zip hello. Hello скрипт будет использовать учетную запись хранения toohello пакета в hello tooupload AzCopy. Передается в расположении папки артефактов и hello сценарий будет автоматически загружать все файлы в этой toohello каталог с именем контейнера хранилища. После вызова Deploy-AzureResourceGroup.ps1 toothen обновление hello SSL привязок toomap hello пользовательское имя узла с SSL-сертификат.

полное развертывание вызывающему Привет развернуть hello Hello, следуя PowerShell показано-AzureResourceGroup.ps1:

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script toodeploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app toobind ssl certificate toohostname. This has toobe done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

На этом этапе приложения должны были развернуты, и должен быть tooit может toobrowse через https://www.yourcustomdomain.com

