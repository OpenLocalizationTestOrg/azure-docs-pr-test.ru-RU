---
title: "aaaConnect виртуальной сети tooyour приложения с помощью PowerShell"
description: "Инструкции о способах tooconnect tooand работы с виртуальными сетями с помощью PowerShell"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: a5c76e77-972a-431c-b14b-3611dae1631b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: ccompy
ms.openlocfilehash: c9d0fa99d02cab7b2c7211a1b2f7b7d0cd27ee8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a><span data-ttu-id="fe84c-103">Подключение виртуальной сети tooyour приложения с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe84c-103">Connect your app tooyour virtual network by using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="fe84c-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="fe84c-104">Overview</span></span>
<span data-ttu-id="fe84c-105">В службе приложений Azure, можно подключить ваше приложение (веб, мобильных или API) tooan виртуальной сети (VNet) Azure в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="fe84c-105">In Azure App Service, you can connect your app (web, mobile, or API) tooan Azure virtual network (VNet) in your subscription.</span></span> <span data-ttu-id="fe84c-106">Эта функция называется интеграцией с виртуальной сетью.</span><span class="sxs-lookup"><span data-stu-id="fe84c-106">This feature is called VNet Integration.</span></span> <span data-ttu-id="fe84c-107">Функция интеграции виртуальной сети Hello не следует путать с функцией hello среды службы приложений, позволяющую toorun экземпляр службы приложений Azure в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fe84c-107">hello VNet Integration feature should not be confused with hello App Service Environment feature, which allows you toorun an instance of Azure App Service in your virtual network.</span></span>

<span data-ttu-id="fe84c-108">Функция интеграции виртуальной сети Hello имеет пользовательский интерфейс (UI) в новый портал hello toointegrate можно использовать с виртуальными сетями, которые развертываются с помощью модели развертывания диспетчера ресурсов Azure hello либо hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="fe84c-108">hello VNet Integration feature has a user interface (UI) in hello new portal that you can use toointegrate with virtual networks that are deployed by using either hello classic deployment model or hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="fe84c-109">Дополнительные сведения о функции hello toolearn см [интегрировать приложения с помощью виртуальной сети Azure](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="fe84c-109">If you want toolearn more about hello feature, see [Integrate your app with an Azure virtual network](web-sites-integrate-with-vnet.md).</span></span>

<span data-ttu-id="fe84c-110">Эта статья является не о как toouse hello пользовательского интерфейса, но вместо о том, как tooenable интеграции с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fe84c-110">This article is not about how toouse hello UI but rather about how tooenable integration by using PowerShell.</span></span> <span data-ttu-id="fe84c-111">Поскольку отличаются hello команды для каждой модели развертывания, в этой статье имеется раздел для каждой модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="fe84c-111">Because hello commands for each deployment model are different, this article has a section for each deployment model.</span></span>  

<span data-ttu-id="fe84c-112">Прежде чем продолжить работу с этой статьей, убедитесь, что:</span><span class="sxs-lookup"><span data-stu-id="fe84c-112">Before you continue with this article, ensure that you have:</span></span>

* <span data-ttu-id="fe84c-113">Здравствуйте, который установлен последний пакет SDK Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fe84c-113">hello latest Azure PowerShell SDK installed.</span></span> <span data-ttu-id="fe84c-114">Это можно установить с hello установщика веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="fe84c-114">You can install this with hello Web Platform Installer.</span></span>
* <span data-ttu-id="fe84c-115">У вас есть приложение в службе приложений Azure, работающее в системе SKU класса "Стандартный" или "Премиум".</span><span class="sxs-lookup"><span data-stu-id="fe84c-115">An app in Azure App Service running in a Standard or Premium SKU.</span></span>

## <a name="classic-virtual-networks"></a><span data-ttu-id="fe84c-116">Классические виртуальные сети</span><span class="sxs-lookup"><span data-stu-id="fe84c-116">Classic virtual networks</span></span>
<span data-ttu-id="fe84c-117">В этом разделе объясняется три задачи для виртуальных сетей, использующих hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="fe84c-117">This section explains three tasks for virtual networks that use hello classic deployment model:</span></span>

1. <span data-ttu-id="fe84c-118">Подключение приложения tooa ранее существовавших виртуальной сети, шлюз и настроенной для подключения точки сайтами.</span><span class="sxs-lookup"><span data-stu-id="fe84c-118">Connect your app tooa preexisting virtual network that has a gateway and is configured for point-to-site connectivity.</span></span>
2. <span data-ttu-id="fe84c-119">обновление сведений об интеграции с виртуальной сетью для приложения;</span><span class="sxs-lookup"><span data-stu-id="fe84c-119">Update your virtual network integration information for your app.</span></span>
3. <span data-ttu-id="fe84c-120">отключение приложения от виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fe84c-120">Disconnect your app from your virtual network.</span></span>

### <a name="connect-an-app-tooa-classic-vnet"></a><span data-ttu-id="fe84c-121">Подключение приложения tooa классической виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="fe84c-121">Connect an app tooa classic VNet</span></span>
<span data-ttu-id="fe84c-122">tooconnect приложения tooa виртуальной сетью, выполните следующие три действия.</span><span class="sxs-lookup"><span data-stu-id="fe84c-122">tooconnect an app tooa virtual network, follow these three steps:</span></span>

1. <span data-ttu-id="fe84c-123">Объявите toohello веб-приложения, что он будет присоединение к конкретной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fe84c-123">Declare toohello web app that it will be joining a particular virtual network.</span></span> <span data-ttu-id="fe84c-124">приложение Hello создаст сертификат, который получит toohello виртуальной сети для подключения точки сайтами.</span><span class="sxs-lookup"><span data-stu-id="fe84c-124">hello app will generate a certificate that will be given toohello virtual network for point-to-site connectivity.</span></span>
2. <span data-ttu-id="fe84c-125">Отправка hello web app сертификат toohello виртуальной сети, а затем извлечь hello точка сеть VPN пакет URI.</span><span class="sxs-lookup"><span data-stu-id="fe84c-125">Upload hello web app certificate toohello virtual network, and then retrieve hello point-to-site VPN package URI.</span></span>
3. <span data-ttu-id="fe84c-126">Обновите подключение виртуальной сети hello веб-приложения с URI пакета точки сайтами hello.</span><span class="sxs-lookup"><span data-stu-id="fe84c-126">Update hello web app's virtual network connection with hello point-to-site package URI.</span></span>

<span data-ttu-id="fe84c-127">Hello первый и третий шаги можно использовать в сценариях, но второй шаг hello требует однократное действие вручную через портал hello или tooperform доступа **ПОМЕСТИТЬ** или **PATCH** действия hello виртуальной сети Конечная точка диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="fe84c-127">hello first and third steps are fully scriptable, but hello second step requires a one-time, manual action through hello portal, or access tooperform **PUT** or **PATCH** actions on hello virtual network Azure Resource Manager endpoint.</span></span> <span data-ttu-id="fe84c-128">Обратитесь в службу поддержки Azure toohave это включена.</span><span class="sxs-lookup"><span data-stu-id="fe84c-128">Contact Azure Support toohave this enabled.</span></span> <span data-ttu-id="fe84c-129">Перед выполнением действий убедитесь, что у вас есть классическая виртуальная сеть со включенным подключением типа "точка — сеть" и развернутым шлюзом.</span><span class="sxs-lookup"><span data-stu-id="fe84c-129">Before you start, make sure that you have a classic virtual network that has point-to-site connectivity already enabled and a deployed gateway.</span></span> <span data-ttu-id="fe84c-130">toocreate hello шлюза и включить точки сайтами подключения, необходимо toouse hello портала, описанную в [создание VPN-шлюза][createvpngateway].</span><span class="sxs-lookup"><span data-stu-id="fe84c-130">toocreate hello gateway and enable point-to-site connectivity, you need toouse hello portal as described at [Creating a VPN gateway][createvpngateway].</span></span>

<span data-ttu-id="fe84c-131">Hello классической виртуальной сети должен toobe в hello той же подписке, службе приложений план содержит приложение hello, который интегрируется с.</span><span class="sxs-lookup"><span data-stu-id="fe84c-131">hello classic virtual network needs toobe in hello same subscription as your App Service plan that holds hello app that you are integrating with.</span></span>

##### <a name="set-up-azure-powershell-sdk"></a><span data-ttu-id="fe84c-132">Настройка пакета SDK для Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe84c-132">Set up Azure PowerShell SDK</span></span>
<span data-ttu-id="fe84c-133">Откройте окно PowerShell и настройте учетную запись и подписку Azure, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fe84c-133">Open a PowerShell window and set up your Azure account and subscription by using:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="fe84c-134">Этой команды откроется запрос tooget учетные данные Azure.</span><span class="sxs-lookup"><span data-stu-id="fe84c-134">That command will open a prompt tooget your Azure credentials.</span></span> <span data-ttu-id="fe84c-135">После входа в воспользуйтесь одним из следующих команд tooselect hello подписки, которые должны toouse hello.</span><span class="sxs-lookup"><span data-stu-id="fe84c-135">After you sign in, use either of hello following commands tooselect hello subscription that you want toouse.</span></span> <span data-ttu-id="fe84c-136">Убедитесь, что вы используете подписки hello, виртуальную сеть и план служб приложений в.</span><span class="sxs-lookup"><span data-stu-id="fe84c-136">Make sure that you are using hello subscription that your virtual network and App Service plan are in.</span></span>

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

<span data-ttu-id="fe84c-137">или</span><span class="sxs-lookup"><span data-stu-id="fe84c-137">or</span></span>

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a><span data-ttu-id="fe84c-138">Переменные, используемые в этой статье</span><span class="sxs-lookup"><span data-stu-id="fe84c-138">Variables used in this article</span></span>
<span data-ttu-id="fe84c-139">команды toosimplify, мы установим **$Configuration** переменной PowerShell с определенной конфигурацией hello.</span><span class="sxs-lookup"><span data-stu-id="fe84c-139">toosimplify commands, we will set a **$Configuration** PowerShell variable with hello specific configuration.</span></span>

<span data-ttu-id="fe84c-140">Задайте переменную следующим образом в PowerShell с hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="fe84c-140">Set a variable as follows in PowerShell with hello following parameters:</span></span>

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

<span data-ttu-id="fe84c-141">расположение приложения Hello должно быть расположение hello без пробелов.</span><span class="sxs-lookup"><span data-stu-id="fe84c-141">hello app location should be hello location without any spaces.</span></span> <span data-ttu-id="fe84c-142">например westus для западной части США.</span><span class="sxs-lookup"><span data-stu-id="fe84c-142">For example, West US is westus.</span></span>

    $Configuration.WebAppLocation = "[Your web app Location]"

<span data-ttu-id="fe84c-143">Следующий элемент Hello —, где должен быть записан hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="fe84c-143">hello next item is where hello certificate should be written.</span></span> <span data-ttu-id="fe84c-144">Этот путь должен быть доступным для записи на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="fe84c-144">It should be a writable path on your local computer.</span></span> <span data-ttu-id="fe84c-145">Убедитесь, что tooinclude CER-файл в конце hello.</span><span class="sxs-lookup"><span data-stu-id="fe84c-145">Make sure tooinclude .cer at hello end.</span></span>

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

<span data-ttu-id="fe84c-146">toosee можно задать тип **$Configuration**.</span><span class="sxs-lookup"><span data-stu-id="fe84c-146">toosee what you set, type **$Configuration**.</span></span>

    > $Configuration

    Name                           Value
    ----                           -----
    GeneratedCertificatePath       C:\vnetcert.cer
    VnetSubscriptionId             efc239a4-88f9-2c5e-a9a1-3034c21ad496
    WebAppResourceGroup            vnetdemo-rg
    VnetResourceGroup              testase1-rg
    VnetName                       TestNetwork
    WebAppName                     vnetintdemoapp
    WebAppLocation                 centralus

<span data-ttu-id="fe84c-147">Hello оставшейся части этого раздела предполагается, что переменная, созданная, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="fe84c-147">hello rest of this section assumes that you have a variable created as just described.</span></span>

##### <a name="declare-hello-virtual-network-toohello-app"></a><span data-ttu-id="fe84c-148">Объявите toohello приложение hello виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="fe84c-148">Declare hello virtual network toohello app</span></span>
<span data-ttu-id="fe84c-149">Используйте hello следующая команда приложение hello tootell, что он будет использоваться этой конкретной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fe84c-149">Use hello following command tootell hello app that it will be using this particular virtual network.</span></span> <span data-ttu-id="fe84c-150">Это приведет к toogenerate приложения hello необходимые сертификаты:</span><span class="sxs-lookup"><span data-stu-id="fe84c-150">This will cause hello app toogenerate necessary certificates:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

<span data-ttu-id="fe84c-151">Если команда выполнится успешно, **$vnet** будет содержать переменную **Properties**.</span><span class="sxs-lookup"><span data-stu-id="fe84c-151">If this command succeeds, **$vnet** should have a **Properties** variable in it.</span></span> <span data-ttu-id="fe84c-152">Hello **свойства** переменной должен содержать оба сертификата отпечаток и hello данные сертификата.</span><span class="sxs-lookup"><span data-stu-id="fe84c-152">hello **Properties** variable should contain both a certificate thumbprint and hello certificate data.</span></span>

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a><span data-ttu-id="fe84c-153">Отправка hello web app сертификат toohello виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="fe84c-153">Upload hello web app certificate toohello virtual network</span></span>
<span data-ttu-id="fe84c-154">Для каждого сочетания виртуальной сети и подписки необходимо выполнить однократное действие вручную.</span><span class="sxs-lookup"><span data-stu-id="fe84c-154">A manual, one-time step is required for each subscription and virtual network combination.</span></span> <span data-ttu-id="fe84c-155">То есть при подключении приложения в подписке A tooVirtual сети A необходимо будет toodo этот шаг только один раз, независимо от того, сколько приложений можно настроить.</span><span class="sxs-lookup"><span data-stu-id="fe84c-155">That is, if you are connecting apps in Subscription A tooVirtual Network A, you will need toodo this step only once regardless of how many apps you configure.</span></span> <span data-ttu-id="fe84c-156">При добавлении новой виртуальной сети tooanother приложения toodo потребуется снова.</span><span class="sxs-lookup"><span data-stu-id="fe84c-156">If you are adding a new app tooanother virtual network, you'll need toodo this again.</span></span> <span data-ttu-id="fe84c-157">Hello причиной этого является набор сертификатов, созданный на уровне подписки в службе приложений Azure, что набор hello формируется один раз для каждой виртуальной сети, к которому будут подключаться приложения hello.</span><span class="sxs-lookup"><span data-stu-id="fe84c-157">hello reason for this is that a set of certificates is generated at a subscription level in Azure App Service, and hello set is generated once for each virtual network that hello apps will connect to.</span></span>

<span data-ttu-id="fe84c-158">Hello сертификаты будут уже заданы Если выполнены эти действия или интегрируется с hello же виртуальной сети с помощью портала hello.</span><span class="sxs-lookup"><span data-stu-id="fe84c-158">hello certificates will have already been set if you followed these steps or if you integrated with hello same virtual network by using hello portal.</span></span>

<span data-ttu-id="fe84c-159">Hello первым шагом является toogenerate hello CER-файл.</span><span class="sxs-lookup"><span data-stu-id="fe84c-159">hello first step is toogenerate hello .cer file.</span></span> <span data-ttu-id="fe84c-160">второй шаг Hello — tooupload hello .cer файл tooyour виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fe84c-160">hello second step is tooupload hello .cer file tooyour virtual network.</span></span> <span data-ttu-id="fe84c-161">toogenerate hello CER-файл из вызова hello API в hello предыдущих шага, выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="fe84c-161">toogenerate hello .cer file from hello API call in hello earlier step, run hello following commands.</span></span>

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

<span data-ttu-id="fe84c-162">Hello сертификат будет находится в папке hello, **$Configuration.GeneratedCertificatePath** указывает.</span><span class="sxs-lookup"><span data-stu-id="fe84c-162">hello certificate will be found in hello location that **$Configuration.GeneratedCertificatePath** specifies.</span></span>

<span data-ttu-id="fe84c-163">сертификат hello tooupload вручную, используйте hello [портал Azure] [ azureportal] и **Обзор виртуальной сети (классические)** > **VPN-подключений**  >  **Точки сайтами** > **Управление сертификатами**.</span><span class="sxs-lookup"><span data-stu-id="fe84c-163">tooupload hello certificate manually, use hello [Azure portal][azureportal] and **Browse Virtual Network (classic)** > **VPN connections** > **Point-to-site** > **Manage certificates**.</span></span> <span data-ttu-id="fe84c-164">Здесь можно отправить сертификат.</span><span class="sxs-lookup"><span data-stu-id="fe84c-164">From here, upload your certificate.</span></span>

##### <a name="get-hello-point-to-site-package"></a><span data-ttu-id="fe84c-165">Получение пакета hello точка сеть</span><span class="sxs-lookup"><span data-stu-id="fe84c-165">Get hello point-to-site package</span></span>
<span data-ttu-id="fe84c-166">Hello следующим шагом в настройке подключения к виртуальной сети на веб-приложения является пакетом точки сайтами tooget hello и предоставить ему tooyour веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="fe84c-166">hello next step in setting up a virtual network connection on a web app is tooget hello point-to-site package and provide it tooyour web app.</span></span>

<span data-ttu-id="fe84c-167">Сохраните hello следующий файл шаблона tooa вызывается GetNetworkPackageUri.json где-либо на компьютере, например, C:\Azure\Templates\GetNetworkPackageUri.json.</span><span class="sxs-lookup"><span data-stu-id="fe84c-167">Save hello following template tooa file called GetNetworkPackageUri.json somewhere on your computer, for example, C:\Azure\Templates\GetNetworkPackageUri.json.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "certData": {
                "type": "string"
            },
            "certThumbprint": {
                "type": "string"
            },
            "networkName": {
                "type": "string"
            }
        },
        "variables": {
            "legacyVnetName": "[concat('Group ', resourceGroup().name, ' ', parameters('networkName'))]"
            },
            "resources": [
            ],
        "outputs" : {
            "PackageUri" :
            {
            "value" : "[listPackage(resourceId('Microsoft.ClassicNetwork/virtualNetworks/gateways/clientRootCertificates', parameters('networkName'), 'primary', parameters('certThumbprint')), '2014-06-01').packageUri]", "type" : "string"
            }
        }
    }


<span data-ttu-id="fe84c-168">Задайте входные параметры.</span><span class="sxs-lookup"><span data-stu-id="fe84c-168">Set input parameters:</span></span>

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

<span data-ttu-id="fe84c-169">Вызов скрипта hello:</span><span class="sxs-lookup"><span data-stu-id="fe84c-169">Call hello script:</span></span>

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


<span data-ttu-id="fe84c-170">переменная приветствия **$output. Outputs.packageUri** теперь будет содержать toobe URI пакета hello, учитывая tooyour веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="fe84c-170">hello variable **$output.Outputs.packageUri** will now contain hello package URI toobe given tooyour web app.</span></span>

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a><span data-ttu-id="fe84c-171">Отправка tooyour приложения hello пакета точка сеть</span><span class="sxs-lookup"><span data-stu-id="fe84c-171">Upload hello point-to-site package tooyour app</span></span>
<span data-ttu-id="fe84c-172">последним шагом Hello является приложение hello tooprovide с этим пакетом.</span><span class="sxs-lookup"><span data-stu-id="fe84c-172">hello final step is tooprovide hello app with this package.</span></span> <span data-ttu-id="fe84c-173">Просто выполните hello следующей команды:</span><span class="sxs-lookup"><span data-stu-id="fe84c-173">Simply run hello next command:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

<span data-ttu-id="fe84c-174">Если сообщение с запросом tooconfirm перезаписи существующего ресурса, убедитесь, что tooallow его.</span><span class="sxs-lookup"><span data-stu-id="fe84c-174">If a message asks you tooconfirm that you are overwriting an existing resource, make sure tooallow it.</span></span>

<span data-ttu-id="fe84c-175">После успешного выполнения этой команды, приложение должно быть toohello подключенной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fe84c-175">After this command succeeds, your app should now be connected toohello virtual network.</span></span> <span data-ttu-id="fe84c-176">в случае успешного выполнения tooconfirm перейдите tooyour консольного приложения и введите ниже hello:</span><span class="sxs-lookup"><span data-stu-id="fe84c-176">tooconfirm success, go tooyour app console, and type hello following:</span></span>

    SET WEBSITE_

<span data-ttu-id="fe84c-177">Если переменной среды WEBSITE_VNETNAME со значением, совпадающим с именем hello hello целевой виртуальной сети, все конфигурации успешно выполнено.</span><span class="sxs-lookup"><span data-stu-id="fe84c-177">If there is an environment variable called WEBSITE_VNETNAME that has a value that matches hello name of hello target virtual network, all configurations have succeeded.</span></span>

### <a name="update-classic-vnet-integration-information"></a><span data-ttu-id="fe84c-178">Обновление сведений об интеграции с классической виртуальной сетью</span><span class="sxs-lookup"><span data-stu-id="fe84c-178">Update classic VNet integration information</span></span>
<span data-ttu-id="fe84c-179">tooupdate или повторной синхронизации информации, просто повторите действия hello, которая использовалась при создании hello интеграции на первом месте hello.</span><span class="sxs-lookup"><span data-stu-id="fe84c-179">tooupdate or resync your information, simply repeat hello steps that you followed when you created hello integration in hello first place.</span></span> <span data-ttu-id="fe84c-180">К этим действиям относятся:</span><span class="sxs-lookup"><span data-stu-id="fe84c-180">Those steps are:</span></span>

1. <span data-ttu-id="fe84c-181">Определение данных конфигурации.</span><span class="sxs-lookup"><span data-stu-id="fe84c-181">Define your configuration information.</span></span>
2. <span data-ttu-id="fe84c-182">Объявите toohello приложение hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fe84c-182">Declare hello virtual network toohello app.</span></span>
3. <span data-ttu-id="fe84c-183">Получение пакета точки сайтами hello.</span><span class="sxs-lookup"><span data-stu-id="fe84c-183">Get hello point-to-site package.</span></span>
4. <span data-ttu-id="fe84c-184">Отправьте приложение tooyour hello точки сайтами пакета.</span><span class="sxs-lookup"><span data-stu-id="fe84c-184">Upload hello point-to-site package tooyour app.</span></span>

### <a name="disconnect-your-app-from-a-classic-vnet"></a><span data-ttu-id="fe84c-185">Отключение приложения от классической виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="fe84c-185">Disconnect your app from a classic VNet</span></span>
<span data-ttu-id="fe84c-186">приложение hello toodisconnect, необходимо hello сведения о конфигурации, который был задан во время интеграции виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fe84c-186">toodisconnect hello app, you need hello configuration information that was set during virtual network integration.</span></span> <span data-ttu-id="fe84c-187">Используя эту информацию, нет нажмите одну команду toodisconnect приложения из виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fe84c-187">Using that information, there is then one command toodisconnect your app from your virtual network.</span></span>

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a><span data-ttu-id="fe84c-188">Виртуальные сети Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fe84c-188">Resource Manager virtual networks</span></span>
<span data-ttu-id="fe84c-189">У виртуальных сетей Resource Manager есть интерфейсы API Azure Resource Manager, которые упрощают некоторые процессы по сравнению с классическими виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="fe84c-189">Resource Manager virtual networks have Azure Resource Manager APIs, which simplify some processes when compared with classic virtual networks.</span></span> <span data-ttu-id="fe84c-190">У нас есть скрипт, который поможет вам выполнить hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="fe84c-190">We have a script that will help you complete hello following tasks:</span></span>

* <span data-ttu-id="fe84c-191">создать виртуальную сеть Resource Manager и интегрировать свое приложение с ней;</span><span class="sxs-lookup"><span data-stu-id="fe84c-191">Create a Resource Manager virtual network and integrate your app with it.</span></span>
* <span data-ttu-id="fe84c-192">создать шлюз, настроить подключение "точка — сеть" в созданной ранее виртуальной сети Resource Manager, а затем интегрировать свое приложение с ней;</span><span class="sxs-lookup"><span data-stu-id="fe84c-192">Create a gateway, configure point-to-site connectivity in a preexisting Resource Manager virtual network, and then integrate your app with it.</span></span>
* <span data-ttu-id="fe84c-193">интегрировать свое приложение с созданной ранее виртуальной сетью Resource Manager, у которой есть шлюз и включенное подключение "точка — сеть";</span><span class="sxs-lookup"><span data-stu-id="fe84c-193">Integrate your app with a preexisting Resource Manager virtual network that has a gateway and point-to-site connectivity enabled.</span></span>
* <span data-ttu-id="fe84c-194">отключение приложения от виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fe84c-194">Disconnect your app from your virtual network.</span></span>

### <a name="resource-manager-vnet-app-service-integration-script"></a><span data-ttu-id="fe84c-195">Скрипт для интеграции службы приложений для виртуальной сети Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fe84c-195">Resource Manager VNet App Service integration script</span></span>
<span data-ttu-id="fe84c-196">Скопируйте hello следующий скрипт и сохраните его файл tooa.</span><span class="sxs-lookup"><span data-stu-id="fe84c-196">Copy hello following script and save it tooa file.</span></span> <span data-ttu-id="fe84c-197">Если вы не хотите toouse hello скрипт, вы свободного toolearn от него toosee как tooset всех компонентов с помощью диспетчера ресурсов для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fe84c-197">If you don’t want toouse hello script, feel free toolearn from it toosee how tooset things up with a Resource Manager virtual network.</span></span>

    function ReadHostWithDefault($message, $default)
    {
        $result = Read-Host "$message [$default]"
        if($result -eq "")
        {
            $result = $default
        }
            return $result
        }

    function PromptCustom($title, $optionValues, $optionDescriptions)
    {
        Write-Host $title
        Write-Host
        $a = @()
        for($i = 0; $i -lt $optionValues.Length; $i++){
            Write-Host "$($i+1))" $optionDescriptions[$i]
        }
        Write-Host

        while($true)
        {
            Write-Host "Choose an option: "
            $option = Read-Host
            $option = $option -as [int]

            if($option -ge 1 -and $option -le $optionValues.Length)
            {
                return $optionValues[$option-1]
            }
        }
    }

    function PromptYesNo($title, $message, $default = 0)
    {
        $yes = New-Object System.Management.Automation.Host.ChoiceDescription "&Yes", ""
        $no = New-Object System.Management.Automation.Host.ChoiceDescription "&No", ""
        $options = [System.Management.Automation.Host.ChoiceDescription[]]($yes, $no)
        $result = $host.ui.PromptForChoice($title, $message, $options, $default)
        return $result
    }

    function CreateVnet($resourceGroupName, $vnetName, $vnetAddressSpace, $vnetGatewayAddressSpace, $location)
    {
        Write-Host "Creating a new VNET"
        $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
        New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location -AddressPrefix $vnetAddressSpace -Subnet $gatewaySubnet
    }

    function CreateVnetGateway($resourceGroupName, $vnetName, $vnetIpName, $location, $vnetIpConfigName, $vnetGatewayName, $certificateData, $vnetPointToSiteAddressSpace)
    {
        $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName
        $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet

        Write-Host "Creating a public IP address for this VNET"
        $pip = New-AzureRmPublicIpAddress -Name $vnetIpName -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
        $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $vnetIpConfigName -Subnet $subnet -PublicIpAddress $pip

        Write-Host "Adding a root certificate toothis VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up tooan hour."
        New-AzureRmVirtualNetworkGateway -Name $vnetGatewayName -ResourceGroupName $resourceGroupName -Location $location -IpConfigurations $ipconf -GatewayType Vpn -VpnType RouteBased -EnableBgp $false -GatewaySku Basic -VpnClientAddressPool $vnetPointToSiteAddressSpace -VpnClientRootCertificates $root
    }

    function AddNewVnet($subscriptionId, $webAppResourceGroup, $webAppName)
    {
        Write-Host "Adding a new Vnet"
        Write-Host
        $vnetName = Read-Host "Specify a name for this Virtual Network"

        $vnetGatewayName="$($vnetName)-gateway"
        $vnetIpName="$($vnetName)-ip"
        $vnetIpConfigName="$($vnetName)-ipconf"

        # Virtual Network settings
        $vnetAddressSpace="10.0.0.0/8"
        $vnetGatewayAddressSpace="10.5.0.0/16"
        $vnetPointToSiteAddressSpace="172.16.0.0/16"

        $changeRequested = 0
        $resourceGroupName = $webAppResourceGroup

        while($changeRequested -eq 0)
        {
            Write-Host
            Write-Host "Currently, I will create a VNET with hello following settings:"
            Write-Host
            Write-Host "Virtual Network Name: $vnetName"
            Write-Host "Resource Group Name:  $resourceGroupName"
            Write-Host "Gateway Name: $vnetGatewayName"
            Write-Host "Vnet IP name: $vnetIpName"
            Write-Host "Vnet IP config name:  $vnetIpConfigName"
            Write-Host "Address Space:$vnetAddressSpace"
            Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
            Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
            Write-Host
            $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

            if($changeRequested -eq 0)
            {
                $vnetName = ReadHostWithDefault "Virtual Network Name" $vnetName
                $resourceGroupName = ReadHostWithDefault "Resource Group Name" $resourceGroupName
                $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                $vnetAddressSpace = ReadHostWithDefault "Vnet Address Space" $vnetAddressSpace
                $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
            }
        }

        $ErrorActionPreference = "Stop";

        # We create hello virtual network and add it here. hello way this works is:
        # 1) Add hello VNET association toohello App. This allows hello App toogenerate certificates, etc. for hello VNET.
        # 2) Create hello VNET and VNET gateway, add hello certificates, create hello public IP, etc., required for hello gateway
        # 3) Get hello VPN package from hello gateway and pass it back toohello App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association tooVNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, hello gateway should be able toobe joined tooan App, but may require some minor tweaking. We will declare toohello App now toouse this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET toointegrate with" $vnets $vnetNames

        # We need toocheck if this VNET is able toobe joined tooa App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have hello right certificate, we will need tooadd it.
                # If it doesn't have a point-to-site range, we will need tooadd it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need toocreate one.
            Write-Host "This Virtual Network has no gateway. I will need toocreate one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in hello address space $($vnet.AddressSpace.AddressPrefixes), with hello following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with hello following settings:"
                Write-Host
                Write-Host "Virtual Network Name: $vnetName"
                Write-Host "Resource Group Name:  $($vnet.ResourceGroupName)"
                Write-Host "Gateway Name: $vnetGatewayName"
                Write-Host "Vnet IP name: $vnetIpName"
                Write-Host "Vnet IP config name:  $vnetIpConfigName"
                Write-Host "Address Space:$($vnet.AddressSpace.AddressPrefixes)"
                Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
                Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
                Write-Host
                $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

                if($changeRequested -eq 0)
                {
                    $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                    $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                    $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                    $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                    $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
                }
            }

            $ErrorActionPreference = "Stop";

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need toocreate one.
            if($gatewaySubnet -eq $null)
            {
                $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
                $vnet.Subnets.Add($gatewaySubnet);
                Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
            }

            CreateVnetGateway $vnet.ResourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $vnetGatewayName
        }
        else
        {
            $uriParts = $gatewaySubnet.IpConfigurations[0].Id.Split('/')
            $gatewayResourceGroup = $uriParts[4]
            $gatewayName = $uriParts[8]

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $gatewayName

            # validate gateway types, etc.
            if($gateway.GatewayType -ne "Vpn")
            {
                Write-Error "This gateway is not of hello Vpn type. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need toocheck if hello certificate here exists in hello gateway.
            $certificates = $gateway.VpnClientConfiguration.VpnClientRootCertificates

            $certFound = $false
            foreach($certificate in $certificates)
            {
                if($certificate.PublicCertData -eq $virtualNetwork.Properties.CertBlob)
                {
                    $certFound = $true
                    break
                }
            }

            if(-not $certFound)
            {
                Write-Host "Adding certificate"
                Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName "AppServiceCertificate.cer" -PublicCertData $virtualNetwork.Properties.CertBlob -VirtualNetworkGatewayName $gateway.Name
            }
        }

        # Now finish joining by getting hello VPN package and giving it toohello App
        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $vnet.Name; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

        Write-Host "Finished!"
    }

    function RemoveVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected tooa VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound toothis account."
        return
    }

    if($subs.Length -eq 1)
    {
        $subscriptionId = $subs[0].SubscriptionId
    }
    else
    {
        $subscriptionChoices = @()
        $subscriptionValues = @()

        foreach($subscription in $subs){
        $subscriptionChoices += "$($subscription.SubscriptionName) ($($subscription.SubscriptionId))";
        $subscriptionValues += ($subscription.SubscriptionId);
        }

        $subscriptionId = PromptCustom "Choose a subscription" $subscriptionValues $subscriptionChoices
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    $resourceGroup = Read-Host "Please enter hello Resource Group of your App"

    $appName = Read-Host "Please enter hello Name of your App"

    $options = @("Add a NEW Virtual Network tooan App", "Add an EXISTING Virtual Network tooan App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want toodo?" $optionValues $options

    if($option -eq 0)
    {
        AddNewVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 1)
    {
        AddExistingVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 2)
    {
        RemoveVnet $subscriptionId $resourceGroup $appName
    }

<span data-ttu-id="fe84c-198">Сохраните копию скрипта hello.</span><span class="sxs-lookup"><span data-stu-id="fe84c-198">Save a copy of hello script.</span></span> <span data-ttu-id="fe84c-199">В этой статье он называется V2VnetAllinOne.ps1, но можно использовать другое имя.</span><span class="sxs-lookup"><span data-stu-id="fe84c-199">In this article, it is called V2VnetAllinOne.ps1, but you can use another name.</span></span> <span data-ttu-id="fe84c-200">Для этого сценария не нужно указывать никаких аргументов.</span><span class="sxs-lookup"><span data-stu-id="fe84c-200">There are no arguments for this script.</span></span> <span data-ttu-id="fe84c-201">Просто запустите его.</span><span class="sxs-lookup"><span data-stu-id="fe84c-201">You simply run it.</span></span> <span data-ttu-id="fe84c-202">Hello первое, что скрипт hello будет выполнять является toosign в запрос.</span><span class="sxs-lookup"><span data-stu-id="fe84c-202">hello first thing hello script will do is prompt you toosign in.</span></span> <span data-ttu-id="fe84c-203">После входа в скрипт hello получает сведения о вашей учетной записи и возвращает список подписок.</span><span class="sxs-lookup"><span data-stu-id="fe84c-203">After you sign in, hello script gets details about your account and returns a list of subscriptions.</span></span> <span data-ttu-id="fe84c-204">Не считая hello запрос учетных данных, выполнения начального сценария hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="fe84c-204">Not counting hello request for your credentials, hello initial script execution looks like this:</span></span>

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) <span data-ttu-id="fe84c-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span><span class="sxs-lookup"><span data-stu-id="fe84c-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span></span>
    2) <span data-ttu-id="fe84c-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span><span class="sxs-lookup"><span data-stu-id="fe84c-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span></span>
    3) <span data-ttu-id="fe84c-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span><span class="sxs-lookup"><span data-stu-id="fe84c-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span></span>

    <span data-ttu-id="fe84c-208">Выберите вариант: 3</span><span class="sxs-lookup"><span data-stu-id="fe84c-208">Choose an option: 3</span></span>

    <span data-ttu-id="fe84c-209">Учетная запись      : ccompy@microsoft.com Среда  : AzureCloud Подписка : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Клиент       : 722278f-fef1-499f-91ab-2323d011db47</span><span class="sxs-lookup"><span data-stu-id="fe84c-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span></span>

    <span data-ttu-id="fe84c-210">Введите группу ресурсов приложения hello: hcdemo rg введите имя приложения hello: v2vnetpowershell что вам требуется toodo?</span><span class="sxs-lookup"><span data-stu-id="fe84c-210">Please enter hello Resource Group of your App: hcdemo-rg Please enter hello Name of your App: v2vnetpowershell What do you want toodo?</span></span>

    1) <span data-ttu-id="fe84c-211">Добавить новую виртуальную сеть tooan приложения</span><span class="sxs-lookup"><span data-stu-id="fe84c-211">Add a NEW Virtual Network tooan App</span></span>
    2) <span data-ttu-id="fe84c-212">Добавление СУЩЕСТВУЮЩЕЙ виртуальной сети tooan приложения</span><span class="sxs-lookup"><span data-stu-id="fe84c-212">Add an EXISTING Virtual Network tooan App</span></span>
    3) <span data-ttu-id="fe84c-213">Удаление виртуальной сети из приложения</span><span class="sxs-lookup"><span data-stu-id="fe84c-213">Remove a Virtual Network from an App</span></span>

<span data-ttu-id="fe84c-214">Hello оставшейся части этого раздела описана каждая из этих трех параметров.</span><span class="sxs-lookup"><span data-stu-id="fe84c-214">hello rest of this section explains each of those three options.</span></span>

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a><span data-ttu-id="fe84c-215">Создание виртуальной сети Resource Manager и интеграция с ней</span><span class="sxs-lookup"><span data-stu-id="fe84c-215">Create a Resource Manager VNet and integrate with it</span></span>
<span data-ttu-id="fe84c-216">Выберите новую виртуальную сеть, использует hello модели развертывания диспетчера ресурсов и интегрировать его с вашим приложением toocreate **1) добавьте новую виртуальную сеть tooan приложения**.</span><span class="sxs-lookup"><span data-stu-id="fe84c-216">toocreate a new virtual network that uses hello Resource Manager deployment model and integrate it with your app, select **1) Add a NEW Virtual Network tooan App**.</span></span> <span data-ttu-id="fe84c-217">Это предложит ввести имя hello hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fe84c-217">This will prompt you for hello name of hello virtual network.</span></span> <span data-ttu-id="fe84c-218">В моем случае как видно в hello следующие параметры, я использовал имя hello, v2pshell.</span><span class="sxs-lookup"><span data-stu-id="fe84c-218">In my case, as you can see in hello following settings, I used hello name, v2pshell.</span></span>

<span data-ttu-id="fe84c-219">сценарий Hello подробно описывает hello hello виртуальной сети, которая находится в процессе создания.</span><span class="sxs-lookup"><span data-stu-id="fe84c-219">hello script gives hello details about hello virtual network that's being created.</span></span> <span data-ttu-id="fe84c-220">Если я хочу ли изменения любых значений hello.</span><span class="sxs-lookup"><span data-stu-id="fe84c-220">If I want, I can change any of hello values.</span></span> <span data-ttu-id="fe84c-221">При выполнении этого примера я создал виртуальной сети, которая имеет hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="fe84c-221">In this example execution, I created a virtual network that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

<span data-ttu-id="fe84c-222">Toochange любых значений hello, введите **Y** и внесите изменения hello.</span><span class="sxs-lookup"><span data-stu-id="fe84c-222">If you want toochange any of hello values, type **Y** and make hello changes.</span></span> <span data-ttu-id="fe84c-223">Когда будет удовлетворен hello параметры виртуальной сети, введите **N** или просто нажмите клавишу ВВОД, ответ на запрос об изменении параметров hello.</span><span class="sxs-lookup"><span data-stu-id="fe84c-223">When you are happy with hello virtual network settings, type **N** or simply press Enter when prompted about changing hello settings.</span></span> <span data-ttu-id="fe84c-224">Отсюда до ее завершения, скрипт hello сообщает некоторые ею "буквами" i ", выполнив до начала шлюз виртуальной сети toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="fe84c-224">From there on until completion, hello script will tell you some of what it' i's doing until it starts toocreate hello virtual network gateway.</span></span> <span data-ttu-id="fe84c-225">Этот шаг может занять час tooan.</span><span class="sxs-lookup"><span data-stu-id="fe84c-225">That step can take up tooan hour.</span></span> <span data-ttu-id="fe84c-226">Отсутствует на этом этапе не индикатор хода выполнения, но сценарий hello позволит узнать, был ли создан шлюз hello.</span><span class="sxs-lookup"><span data-stu-id="fe84c-226">There is no progress indicator during this phase, but hello script will let you know when hello gateway has been created.</span></span>

<span data-ttu-id="fe84c-227">По завершении сценария hello укажет **завершен**.</span><span class="sxs-lookup"><span data-stu-id="fe84c-227">When hello script finishes, it will say **Finished**.</span></span> <span data-ttu-id="fe84c-228">На этом этапе будет создана диспетчера ресурсов виртуальной сети, которая имеет имя hello и выбранные параметры.</span><span class="sxs-lookup"><span data-stu-id="fe84c-228">At this point, you will have a Resource Manager virtual network that has hello name and settings that you selected.</span></span> <span data-ttu-id="fe84c-229">Эта новая виртуальная сеть также будет интегрирована с приложением.</span><span class="sxs-lookup"><span data-stu-id="fe84c-229">This new virtual network will also be integrated with your app.</span></span>

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a><span data-ttu-id="fe84c-230">Интеграция приложения с созданной ранее виртуальной сетью Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fe84c-230">Integrate your app with a preexisting Resource Manager VNet</span></span>
<span data-ttu-id="fe84c-231">При интегрируете с существующие ранее виртуальной сети, если диспетчер ресурсов виртуальной сети, у которого нет шлюза или подключение точка сеть, hello скрипт будет настроить это подключение.</span><span class="sxs-lookup"><span data-stu-id="fe84c-231">When you're integrating with a preexisting virtual network, if you provide a Resource Manager virtual network that doesn’t have a gateway or point-to-site connectivity, hello script will set that up.</span></span> <span data-ttu-id="fe84c-232">Если hello виртуальная сеть уже тем элементам, Настройка, скрипт hello переходит toohello прямой интеграцией приложений.</span><span class="sxs-lookup"><span data-stu-id="fe84c-232">If hello VNET already has those things set up, hello script goes straight toohello app integration.</span></span> <span data-ttu-id="fe84c-233">toostart этот процесс, просто выберите **2) добавьте СУЩЕСТВУЮЩУЮ виртуальную сеть tooan приложения**.</span><span class="sxs-lookup"><span data-stu-id="fe84c-233">toostart this process, simply select **2) Add an EXISTING Virtual Network tooan App**.</span></span>

<span data-ttu-id="fe84c-234">Этот параметр работает только в том случае, если имеется уже существующий диспетчер ресурсов виртуальной сети, которая находится в hello той же подписке, ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="fe84c-234">This option works only if you have a preexisting Resource Manager virtual network that is in hello same subscription as your app.</span></span> <span data-ttu-id="fe84c-235">После выбора параметра hello, появится список виртуальных сетей диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fe84c-235">After you select hello option, you will be presented with a list of your Resource Manager virtual networks.</span></span>   

    Select a VNET toointegrate with

    1) <span data-ttu-id="fe84c-236">v2demonetwork</span><span class="sxs-lookup"><span data-stu-id="fe84c-236">v2demonetwork</span></span>
    2) <span data-ttu-id="fe84c-237">v2pshell</span><span class="sxs-lookup"><span data-stu-id="fe84c-237">v2pshell</span></span>
    3) <span data-ttu-id="fe84c-238">v2vnetintdemo</span><span class="sxs-lookup"><span data-stu-id="fe84c-238">v2vnetintdemo</span></span>
    4) <span data-ttu-id="fe84c-239">v2asenetwork</span><span class="sxs-lookup"><span data-stu-id="fe84c-239">v2asenetwork</span></span>
    5) <span data-ttu-id="fe84c-240">v2pshell2</span><span class="sxs-lookup"><span data-stu-id="fe84c-240">v2pshell2</span></span>

    <span data-ttu-id="fe84c-241">Выберите вариант: 5</span><span class="sxs-lookup"><span data-stu-id="fe84c-241">Choose an option: 5</span></span>

<span data-ttu-id="fe84c-242">Просто выберите hello виртуальную сеть, которую вы хотите toointegrate с.</span><span class="sxs-lookup"><span data-stu-id="fe84c-242">Simply select hello virtual network that you want toointegrate with.</span></span> <span data-ttu-id="fe84c-243">При наличии шлюза с подключением точки сайтами включена hello скрипт просто интегрировать приложения виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fe84c-243">If you already have a gateway that has point-to-site connectivity enabled, hello script will simply integrate your app with your virtual network.</span></span> <span data-ttu-id="fe84c-244">Если у вас шлюз, необходимо будет подсеть шлюза toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="fe84c-244">If you do not have a gateway, you will need toospecify hello gateway subnet.</span></span> <span data-ttu-id="fe84c-245">Подсеть шлюза должна находиться в адресном пространстве виртуальной сети и не может находиться ни в какой другой подсети.</span><span class="sxs-lookup"><span data-stu-id="fe84c-245">Your gateway subnet must be in your virtual network address space, and it cannot be in any other subnet.</span></span> <span data-ttu-id="fe84c-246">При выполнении этого шага для виртуальной сети без шлюза вы получите следующий результат:</span><span class="sxs-lookup"><span data-stu-id="fe84c-246">If you have a virtual network without a gateway and run this step, things look like this:</span></span>

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

<span data-ttu-id="fe84c-247">В этом примере создан шлюз виртуальной сети, имеющий hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="fe84c-247">In this example, I created a virtual network gateway that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association tooVNET

<span data-ttu-id="fe84c-248">Если требуется toochange любой из этих параметров, это можно сделать.</span><span class="sxs-lookup"><span data-stu-id="fe84c-248">If you want toochange any of those settings, you can do so.</span></span> <span data-ttu-id="fe84c-249">В противном случае нажмите клавишу ВВОД и создаст шлюза и присоединить виртуальную сеть tooyour приложения hello скрипта.</span><span class="sxs-lookup"><span data-stu-id="fe84c-249">Otherwise, press Enter and hello script will create your gateway and attach your app tooyour virtual network.</span></span> <span data-ttu-id="fe84c-250">время создания шлюза Hello по-прежнему один час, однако, поэтому убедитесь, что, следует учитывать.</span><span class="sxs-lookup"><span data-stu-id="fe84c-250">hello gateway creation time is still an hour, though, so make sure you keep that in mind.</span></span> <span data-ttu-id="fe84c-251">По окончании все, что скрипт hello укажет **завершен**.</span><span class="sxs-lookup"><span data-stu-id="fe84c-251">When everything is finished, hello script will say **Finished**.</span></span>

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a><span data-ttu-id="fe84c-252">Отключение приложения от виртуальной сети Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fe84c-252">Disconnect your app from a Resource Manager VNet</span></span>
<span data-ttu-id="fe84c-253">Отключение приложение от виртуальной сети не остановить работу шлюза hello и отключить подключение точка сеть.</span><span class="sxs-lookup"><span data-stu-id="fe84c-253">Disconnecting your app from your virtual network does not take down hello gateway or disable point-to-site connectivity.</span></span> <span data-ttu-id="fe84c-254">В конце концов, их можно использовать и для других целей.</span><span class="sxs-lookup"><span data-stu-id="fe84c-254">You might, after all, be using it for something else.</span></span> <span data-ttu-id="fe84c-255">Он также не отключить его от других приложений, отличный от hello, который вы указали.</span><span class="sxs-lookup"><span data-stu-id="fe84c-255">It also does not disconnect it from any other apps other than hello one you provided.</span></span> <span data-ttu-id="fe84c-256">tooperform это действие, выберите **3) удалить виртуальную сеть из приложения**.</span><span class="sxs-lookup"><span data-stu-id="fe84c-256">tooperform this action, select **3) Remove a Virtual Network from an App**.</span></span> <span data-ttu-id="fe84c-257">При выборе этого варианта вы увидите следующее:</span><span class="sxs-lookup"><span data-stu-id="fe84c-257">When you do so, you will see something like this:</span></span>

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

<span data-ttu-id="fe84c-258">Несмотря на то, что скрипт hello говорит delete, не удаляя hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="fe84c-258">Although hello script says delete, it does not delete hello virtual network.</span></span> <span data-ttu-id="fe84c-259">Он лишь удаляет hello интеграции.</span><span class="sxs-lookup"><span data-stu-id="fe84c-259">It’s just removing hello integration.</span></span> <span data-ttu-id="fe84c-260">Убедившись, что это желаемый toodo, команда hello обрабатывается довольно быстро и сообщает, **True** после его завершения.</span><span class="sxs-lookup"><span data-stu-id="fe84c-260">After you confirm that this is what you want toodo, hello command is processed quite quickly and tells you **True** when it is done.</span></span>

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
