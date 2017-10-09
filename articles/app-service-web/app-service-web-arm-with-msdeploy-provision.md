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
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a><span data-ttu-id="8153f-103">Развертывание веб-приложения с использованием MSDeploy, пользовательского имени узла и SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="8153f-103">Deploy a web app with MSDeploy, custom hostname and SSL certificate</span></span>
<span data-ttu-id="8153f-104">В этом руководстве описывается создание конца в конец развертывания для веб-приложение Azure, используя MSDeploy, а также добавляет пользовательское имя узла и шаблон ARM toohello сертификат SSL.</span><span class="sxs-lookup"><span data-stu-id="8153f-104">This guide walks through creating an end-to-end deployment for an Azure Web App, leveraging MSDeploy as well as adding a custom hostname and an SSL certificate toohello ARM template.</span></span>

<span data-ttu-id="8153f-105">Дополнительные сведения о создании шаблонов см. в статье [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8153f-105">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

### <a name="create-sample-application"></a><span data-ttu-id="8153f-106">Создание примера приложения</span><span class="sxs-lookup"><span data-stu-id="8153f-106">Create Sample Application</span></span>
<span data-ttu-id="8153f-107">Здесь описывается развертывание веб-приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8153f-107">You will be deploying an ASP.NET web application.</span></span> <span data-ttu-id="8153f-108">Hello первым шагом является toocreate простого веб-приложения (или можно выбрать toouse существующего - в противном случае этот шаг можно пропустить).</span><span class="sxs-lookup"><span data-stu-id="8153f-108">hello first step is toocreate a simple web application (or you could choose toouse an existing one - in which case you can skip this step).</span></span>

<span data-ttu-id="8153f-109">Откройте Visual Studio 2015 и последовательно выберите «Файл» > «Создать проект».</span><span class="sxs-lookup"><span data-stu-id="8153f-109">Open Visual Studio 2015 and choose File > New Project.</span></span> <span data-ttu-id="8153f-110">В диалоговом окне приветствия, появившемся выберите Web > веб-приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8153f-110">On hello dialog that appears choose Web > ASP.NET Web Application.</span></span> <span data-ttu-id="8153f-111">В списке шаблонов выберите Web и щелкните шаблон MVC hello.</span><span class="sxs-lookup"><span data-stu-id="8153f-111">Under Templates choose Web and choose hello MVC template.</span></span> <span data-ttu-id="8153f-112">Выберите *изменить тип проверки подлинности* слишком*без проверки подлинности*.</span><span class="sxs-lookup"><span data-stu-id="8153f-112">Select *Change authentication type* too*No Authentication*.</span></span> <span data-ttu-id="8153f-113">Это просто toomake hello образец приложения как можно более простыми.</span><span class="sxs-lookup"><span data-stu-id="8153f-113">This is just toomake hello sample application as simple as possible.</span></span>

<span data-ttu-id="8153f-114">На этом этапе вы получите основные ASP.Net web app готов toouse как часть процесса развертывания.</span><span class="sxs-lookup"><span data-stu-id="8153f-114">At this point you will have a basic ASP.Net web app ready toouse as part of your deployment process.</span></span>

### <a name="create-msdeploy-package"></a><span data-ttu-id="8153f-115">Создание пакета MSDeploy</span><span class="sxs-lookup"><span data-stu-id="8153f-115">Create MSDeploy package</span></span>
<span data-ttu-id="8153f-116">Следующим шагом является toocreate hello пакета toodeploy hello web app tooAzure.</span><span class="sxs-lookup"><span data-stu-id="8153f-116">Next step is toocreate hello package toodeploy hello web app tooAzure.</span></span> <span data-ttu-id="8153f-117">toodo, сохранить проект и запустите из командной строки hello hello следующее:</span><span class="sxs-lookup"><span data-stu-id="8153f-117">toodo this, save your project and then run hello following from hello command line:</span></span>

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

<span data-ttu-id="8153f-118">Это будет создан ZIP-пакет в папке PackageLocation hello.</span><span class="sxs-lookup"><span data-stu-id="8153f-118">This will create a zipped package under hello PackageLocation folder.</span></span> <span data-ttu-id="8153f-119">Hello приложения готов к работе теперь toobe развертывания, который теперь можно построить toodo шаблона диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="8153f-119">hello application is now ready toobe deployed, which you can now build out an Azure Resource Manager template toodo that.</span></span>

### <a name="create-arm-template"></a><span data-ttu-id="8153f-120">Создание шаблона ARM</span><span class="sxs-lookup"><span data-stu-id="8153f-120">Create ARM Template</span></span>
<span data-ttu-id="8153f-121">Начнем с базового шаблона ARM, который позволит создать веб-приложение и план размещения. (Обратите внимание, что для краткости параметры и переменные опущены.)</span><span class="sxs-lookup"><span data-stu-id="8153f-121">First, let's start with a basic ARM template that will create a web application and a hosting plan (note that parameters and variables are not shown for brevity).</span></span>

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

<span data-ttu-id="8153f-122">Далее необходимо tootake toomodify hello web app ресурсов вложенных ресурсов MSDeploy.</span><span class="sxs-lookup"><span data-stu-id="8153f-122">Next, you will need toomodify hello web app resource tootake a nested MSDeploy resource.</span></span> <span data-ttu-id="8153f-123">Это будет разрешить вы tooreference hello пакет, созданный ранее и сообщите пакета диспетчера ресурсов Azure toouse MSDeploy toodeploy hello toohello веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="8153f-123">This will allow you tooreference hello package created earlier and tell Azure Resource Manager toouse MSDeploy toodeploy hello package toohello Azure WebApp.</span></span> <span data-ttu-id="8153f-124">Hello ниже показан hello Microsoft.Web/sites ресурс с вложенными hello MSDeploy ресурсов:</span><span class="sxs-lookup"><span data-stu-id="8153f-124">hello following shows hello Microsoft.Web/sites resource with hello nested MSDeploy resource:</span></span>

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

<span data-ttu-id="8153f-125">Теперь можно заметить, что hello MSDeploy ресурсов принимает **packageUri** свойство, которое определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8153f-125">Now you will notice that hello MSDeploy resource takes a **packageUri** property which is defined as follows:</span></span>

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

<span data-ttu-id="8153f-126">Это **packageUri** принимает hello uri учетной записи хранилища, который учетную запись хранилища toohello, где нужно будет загрузить zip вашего пакета для точек.</span><span class="sxs-lookup"><span data-stu-id="8153f-126">This **packageUri** takes hello storage account uri which points toohello storage account where you will upload your package zip to.</span></span> <span data-ttu-id="8153f-127">Hello Azure Resource Manager будет использовать [подписей общего доступа](../storage/common/storage-dotnet-shared-access-signature-part-1.md) пакета hello toopull вниз локально из учетной записи хранения hello при развертывании шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="8153f-127">hello Azure Resource Manager will leverage [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) toopull hello package down locally from hello storage account when you deploy hello template.</span></span> <span data-ttu-id="8153f-128">Этот процесс будет автоматизирован через сценарий PowerShell, отправить пакет hello и вызывает hello toocreate ключа, hello API управления Azure и передавать их в шаблоне hello в качестве параметров (*_artifactsLocation* и *_artifactsLocationSasToken*).</span><span class="sxs-lookup"><span data-stu-id="8153f-128">This process will be automated via a PowerShell script that will upload hello package and call hello Azure Management API toocreate hello keys required and pass those into hello template as parameters (*_artifactsLocation* and *_artifactsLocationSasToken*).</span></span> <span data-ttu-id="8153f-129">Вам потребуется toodefine параметры для папки hello, а пакет hello filename — контейнер хранилища отправленного toounder hello.</span><span class="sxs-lookup"><span data-stu-id="8153f-129">You will need toodefine parameters for hello folder and filename hello package is uploaded toounder hello storage container.</span></span>

<span data-ttu-id="8153f-130">Затем следует записать tooadd в другой вложенный ресурсов toosetup hello имя узла привязки tooleverage пользовательского домена.</span><span class="sxs-lookup"><span data-stu-id="8153f-130">Next you need tooadd in another nested resource toosetup hello hostname bindings tooleverage a custom domain.</span></span> <span data-ttu-id="8153f-131">Будет первой необходимости tooensure владельцем hello hostname и настроить toobe протестирован Azure принадлежит вам — см. [настроить пользовательское доменное имя в службе приложений Azure](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="8153f-131">You will first need tooensure that you own hello hostname and set it up toobe verified by Azure that you own it - see [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span> <span data-ttu-id="8153f-132">После этого можно добавить следующий шаблон tooyour в разделе "hello Microsoft.Web/sites ресурсов" hello.</span><span class="sxs-lookup"><span data-stu-id="8153f-132">Once that is done you can add hello following tooyour template under hello Microsoft.Web/sites resource section:</span></span>

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

<span data-ttu-id="8153f-133">Наконец необходимо tooadd другой ресурс верхнего уровня, Microsoft.Web/certificates.</span><span class="sxs-lookup"><span data-stu-id="8153f-133">Finally you need tooadd another top level resource, Microsoft.Web/certificates.</span></span> <span data-ttu-id="8153f-134">Этот ресурс будет содержать SSL-сертификата, будут существовать на приветствия же уровня в качестве веб-приложения и размещения плана.</span><span class="sxs-lookup"><span data-stu-id="8153f-134">This resource will contain your SSL certificate and will exist at hello same level as your web app and hosting plan.</span></span>

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

<span data-ttu-id="8153f-135">Вам потребуется toohave действительного сертификата SSL в порядке tooset этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="8153f-135">You will need toohave a valid SSL certificate in order tooset up this resource.</span></span> <span data-ttu-id="8153f-136">После этого действительный сертификат необходимо tooextract hello pfx байтов как строка base64.</span><span class="sxs-lookup"><span data-stu-id="8153f-136">Once you have that valid certificate then you need tooextract hello pfx bytes as a base64 string.</span></span> <span data-ttu-id="8153f-137">Один из вариантов tooextract это hello toouse следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8153f-137">One option tooextract this is toouse hello following PowerShell command:</span></span>

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

<span data-ttu-id="8153f-138">Затем можно передать таким как шаблон развертывания параметра tooyour ARM.</span><span class="sxs-lookup"><span data-stu-id="8153f-138">You could then pass this as a parameter tooyour ARM deployment template.</span></span>

<span data-ttu-id="8153f-139">На этом этапе hello ARM шаблон готов.</span><span class="sxs-lookup"><span data-stu-id="8153f-139">At this point hello ARM template is ready.</span></span>

### <a name="deploy-template"></a><span data-ttu-id="8153f-140">Развертывание шаблона</span><span class="sxs-lookup"><span data-stu-id="8153f-140">Deploy Template</span></span>
<span data-ttu-id="8153f-141">Здравствуйте, последние действия имеют toopiece этот все вместе в развертывание полной начала до конца.</span><span class="sxs-lookup"><span data-stu-id="8153f-141">hello final steps are toopiece this all together into a full end-to-end deployment.</span></span> <span data-ttu-id="8153f-142">toomake развертывания проще, можно использовать hello **Deploy-AzureResourceGroup.ps1** сценарий PowerShell, которое добавляется при создании проекта группы ресурсов Azure в Visual Studio toohelp с артефакты, необходимые на загрузку шаблон Hello.</span><span class="sxs-lookup"><span data-stu-id="8153f-142">toomake deployment easier you can leverage hello **Deploy-AzureResourceGroup.ps1** PowerShell script that is added when you create an Azure Resource Group project in Visual Studio toohelp with uploading of any artifacts required in hello template.</span></span> <span data-ttu-id="8153f-143">Он требует toohave создал учетную запись хранилища, требуется toouse заранее.</span><span class="sxs-lookup"><span data-stu-id="8153f-143">It requires you toohave created a storage account you want toouse ahead of time.</span></span> <span data-ttu-id="8153f-144">В этом примере я создал учетную запись общего хранилища для отправки toobe package.zip hello.</span><span class="sxs-lookup"><span data-stu-id="8153f-144">For this example, I created a shared storage account for hello package.zip toobe uploaded.</span></span> <span data-ttu-id="8153f-145">Hello скрипт будет использовать учетную запись хранения toohello пакета в hello tooupload AzCopy.</span><span class="sxs-lookup"><span data-stu-id="8153f-145">hello script will leverage AzCopy tooupload hello package toohello storage account.</span></span> <span data-ttu-id="8153f-146">Передается в расположении папки артефактов и hello сценарий будет автоматически загружать все файлы в этой toohello каталог с именем контейнера хранилища.</span><span class="sxs-lookup"><span data-stu-id="8153f-146">You pass in your artifact folder location and hello script will automatically upload all files within that directory toohello named storage container.</span></span> <span data-ttu-id="8153f-147">После вызова Deploy-AzureResourceGroup.ps1 toothen обновление hello SSL привязок toomap hello пользовательское имя узла с SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="8153f-147">After calling Deploy-AzureResourceGroup.ps1 you have toothen update hello SSL bindings toomap hello custom hostname with your SSL certificate.</span></span>

<span data-ttu-id="8153f-148">полное развертывание вызывающему Привет развернуть hello Hello, следуя PowerShell показано-AzureResourceGroup.ps1:</span><span class="sxs-lookup"><span data-stu-id="8153f-148">hello following PowerShell shows hello complete deployment calling hello Deploy-AzureResourceGroup.ps1:</span></span>

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

<span data-ttu-id="8153f-149">На этом этапе приложения должны были развернуты, и должен быть tooit может toobrowse через https://www.yourcustomdomain.com</span><span class="sxs-lookup"><span data-stu-id="8153f-149">At this point your application should have been deployed and you should be able toobrowse tooit via https://www.yourcustomdomain.com</span></span>

