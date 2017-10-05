---
title: "Подключение приложения к виртуальной сети с помощью PowerShell"
description: "Инструкции по подключению виртуальных сетей и работы с ними с помощью PowerShell"
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
ms.openlocfilehash: 6fae6a6c162fa326161d2b47a259b3151d6e3dd0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-app-to-your-virtual-network-by-using-powershell"></a><span data-ttu-id="bc76c-103">Подключение приложения к виртуальной сети с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc76c-103">Connect your app to your virtual network by using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="bc76c-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="bc76c-104">Overview</span></span>
<span data-ttu-id="bc76c-105">В службе приложений Azure приложение (веб-приложение, мобильное приложение или приложение API) можно подключить к виртуальной сети Azure в подписке.</span><span class="sxs-lookup"><span data-stu-id="bc76c-105">In Azure App Service, you can connect your app (web, mobile, or API) to an Azure virtual network (VNet) in your subscription.</span></span> <span data-ttu-id="bc76c-106">Эта функция называется интеграцией с виртуальной сетью.</span><span class="sxs-lookup"><span data-stu-id="bc76c-106">This feature is called VNet Integration.</span></span> <span data-ttu-id="bc76c-107">Функцию интеграции с виртуальной сетью не следует путать с функцией среды службы приложений, которая позволяет запустить экземпляр службы приложений Azure в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bc76c-107">The VNet Integration feature should not be confused with the App Service Environment feature, which allows you to run an instance of Azure App Service in your virtual network.</span></span>

<span data-ttu-id="bc76c-108">Для функции интеграции с виртуальной сетью предусмотрен пользовательский интерфейс на новом портале, который можно использовать для выполнения интеграции с виртуальными сетями, развертываемыми с помощью классической модели развертывания или модели развертывания Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bc76c-108">The VNet Integration feature has a user interface (UI) in the new portal that you can use to integrate with virtual networks that are deployed by using either the classic deployment model or the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="bc76c-109">Дополнительные сведения об этой функции см. в статье [Интеграция приложения с виртуальной сетью Azure](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="bc76c-109">If you want to learn more about the feature, see [Integrate your app with an Azure virtual network](web-sites-integrate-with-vnet.md).</span></span>

<span data-ttu-id="bc76c-110">Эта статья посвящена не использованию пользовательского интерфейса, а включению интеграции с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bc76c-110">This article is not about how to use the UI but rather about how to enable integration by using PowerShell.</span></span> <span data-ttu-id="bc76c-111">Так как команды для разных моделей развертывания отличаются, в этой статье есть отдельные разделы для каждой модели.</span><span class="sxs-lookup"><span data-stu-id="bc76c-111">Because the commands for each deployment model are different, this article has a section for each deployment model.</span></span>  

<span data-ttu-id="bc76c-112">Прежде чем продолжить работу с этой статьей, убедитесь, что:</span><span class="sxs-lookup"><span data-stu-id="bc76c-112">Before you continue with this article, ensure that you have:</span></span>

* <span data-ttu-id="bc76c-113">установлена последняя версия пакета SDK для Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bc76c-113">The latest Azure PowerShell SDK installed.</span></span> <span data-ttu-id="bc76c-114">Ее можно установить с помощью установщика веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="bc76c-114">You can install this with the Web Platform Installer.</span></span>
* <span data-ttu-id="bc76c-115">У вас есть приложение в службе приложений Azure, работающее в системе SKU класса "Стандартный" или "Премиум".</span><span class="sxs-lookup"><span data-stu-id="bc76c-115">An app in Azure App Service running in a Standard or Premium SKU.</span></span>

## <a name="classic-virtual-networks"></a><span data-ttu-id="bc76c-116">Классические виртуальные сети</span><span class="sxs-lookup"><span data-stu-id="bc76c-116">Classic virtual networks</span></span>
<span data-ttu-id="bc76c-117">В этом разделе описываются три задачи для виртуальных сетей, в которых используется классическая модель развертывания:</span><span class="sxs-lookup"><span data-stu-id="bc76c-117">This section explains three tasks for virtual networks that use the classic deployment model:</span></span>

1. <span data-ttu-id="bc76c-118">подключение приложения к ранее созданной виртуальной сети, в которой есть шлюз и которая настроена для подключения типа "точка — сеть";</span><span class="sxs-lookup"><span data-stu-id="bc76c-118">Connect your app to a preexisting virtual network that has a gateway and is configured for point-to-site connectivity.</span></span>
2. <span data-ttu-id="bc76c-119">обновление сведений об интеграции с виртуальной сетью для приложения;</span><span class="sxs-lookup"><span data-stu-id="bc76c-119">Update your virtual network integration information for your app.</span></span>
3. <span data-ttu-id="bc76c-120">отключение приложения от виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bc76c-120">Disconnect your app from your virtual network.</span></span>

### <a name="connect-an-app-to-a-classic-vnet"></a><span data-ttu-id="bc76c-121">Подключение приложения к классической виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="bc76c-121">Connect an app to a classic VNet</span></span>
<span data-ttu-id="bc76c-122">Чтобы подключить приложение к виртуальной сети, выполните три шага:</span><span class="sxs-lookup"><span data-stu-id="bc76c-122">To connect an app to a virtual network, follow these three steps:</span></span>

1. <span data-ttu-id="bc76c-123">Объявите веб-приложению о том, что оно будет присоединено к конкретной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bc76c-123">Declare to the web app that it will be joining a particular virtual network.</span></span> <span data-ttu-id="bc76c-124">Приложение создаст сертификат, который будет передан виртуальной сети для подключения типа "точка — сеть".</span><span class="sxs-lookup"><span data-stu-id="bc76c-124">The app will generate a certificate that will be given to the virtual network for point-to-site connectivity.</span></span>
2. <span data-ttu-id="bc76c-125">Отправьте сертификат веб-приложения в виртуальную сеть, а затем получите URI пакета VPN для подключения типа "точка — сеть".</span><span class="sxs-lookup"><span data-stu-id="bc76c-125">Upload the web app certificate to the virtual network, and then retrieve the point-to-site VPN package URI.</span></span>
3. <span data-ttu-id="bc76c-126">Обновите подключение веб-приложений к виртуальной сети с помощью URI пакета для подключения типа "точка — сеть".</span><span class="sxs-lookup"><span data-stu-id="bc76c-126">Update the web app's virtual network connection with the point-to-site package URI.</span></span>

<span data-ttu-id="bc76c-127">Первый и третий шаги можно полностью реализовать в качестве скриптов, но для второго шага необходимо выполнить однократное действие на портале или получить доступ для выполнения действий **PUT** и **PATCH** в конечной точке Azure Resource Manager виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bc76c-127">The first and third steps are fully scriptable, but the second step requires a one-time, manual action through the portal, or access to perform **PUT** or **PATCH** actions on the virtual network Azure Resource Manager endpoint.</span></span> <span data-ttu-id="bc76c-128">(чтобы включить его, обратитесь в службу поддержки Azure).</span><span class="sxs-lookup"><span data-stu-id="bc76c-128">Contact Azure Support to have this enabled.</span></span> <span data-ttu-id="bc76c-129">Перед выполнением действий убедитесь, что у вас есть классическая виртуальная сеть со включенным подключением типа "точка — сеть" и развернутым шлюзом.</span><span class="sxs-lookup"><span data-stu-id="bc76c-129">Before you start, make sure that you have a classic virtual network that has point-to-site connectivity already enabled and a deployed gateway.</span></span> <span data-ttu-id="bc76c-130">Для создания шлюза и включения подключения "точка — сеть" выполните на портале действия, описанные в статье [Настройка VPN-подключения типа "точка — сеть" к виртуальной сети с помощью классического портала][createvpngateway].</span><span class="sxs-lookup"><span data-stu-id="bc76c-130">To create the gateway and enable point-to-site connectivity, you need to use the portal as described at [Creating a VPN gateway][createvpngateway].</span></span>

<span data-ttu-id="bc76c-131">Классическая виртуальная сеть должна находиться в той же подписке, что и план службы приложений, содержащий приложение, с которым выполняется интеграция.</span><span class="sxs-lookup"><span data-stu-id="bc76c-131">The classic virtual network needs to be in the same subscription as your App Service plan that holds the app that you are integrating with.</span></span>

##### <a name="set-up-azure-powershell-sdk"></a><span data-ttu-id="bc76c-132">Настройка пакета SDK для Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc76c-132">Set up Azure PowerShell SDK</span></span>
<span data-ttu-id="bc76c-133">Откройте окно PowerShell и настройте учетную запись и подписку Azure, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bc76c-133">Open a PowerShell window and set up your Azure account and subscription by using:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="bc76c-134">При выполнении этой команды появится запрос на ввод учетных данных Azure.</span><span class="sxs-lookup"><span data-stu-id="bc76c-134">That command will open a prompt to get your Azure credentials.</span></span> <span data-ttu-id="bc76c-135">После входа в систему используйте одну из команд ниже, чтобы выбрать необходимую подписку.</span><span class="sxs-lookup"><span data-stu-id="bc76c-135">After you sign in, use either of the following commands to select the subscription that you want to use.</span></span> <span data-ttu-id="bc76c-136">Убедитесь, что вы используете именно ту подписку, в которой находятся виртуальная сеть и план службы приложений.</span><span class="sxs-lookup"><span data-stu-id="bc76c-136">Make sure that you are using the subscription that your virtual network and App Service plan are in.</span></span>

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

<span data-ttu-id="bc76c-137">или</span><span class="sxs-lookup"><span data-stu-id="bc76c-137">or</span></span>

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a><span data-ttu-id="bc76c-138">Переменные, используемые в этой статье</span><span class="sxs-lookup"><span data-stu-id="bc76c-138">Variables used in this article</span></span>
<span data-ttu-id="bc76c-139">Чтобы упростить команды, мы запишем необходимую конфигурацию в переменную PowerShell **$Configuration** .</span><span class="sxs-lookup"><span data-stu-id="bc76c-139">To simplify commands, we will set a **$Configuration** PowerShell variable with the specific configuration.</span></span>

<span data-ttu-id="bc76c-140">Установите эту переменную в PowerShell со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="bc76c-140">Set a variable as follows in PowerShell with the following parameters:</span></span>

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

<span data-ttu-id="bc76c-141">Расположение приложения необходимо указывать без пробелов,</span><span class="sxs-lookup"><span data-stu-id="bc76c-141">The app location should be the location without any spaces.</span></span> <span data-ttu-id="bc76c-142">например westus для западной части США.</span><span class="sxs-lookup"><span data-stu-id="bc76c-142">For example, West US is westus.</span></span>

    $Configuration.WebAppLocation = "[Your web app Location]"

<span data-ttu-id="bc76c-143">Следующий элемент представляет собой расположение будущего сертификата.</span><span class="sxs-lookup"><span data-stu-id="bc76c-143">The next item is where the certificate should be written.</span></span> <span data-ttu-id="bc76c-144">Этот путь должен быть доступным для записи на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="bc76c-144">It should be a writable path on your local computer.</span></span> <span data-ttu-id="bc76c-145">Обязательно укажите ".cer" в конце.</span><span class="sxs-lookup"><span data-stu-id="bc76c-145">Make sure to include .cer at the end.</span></span>

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

<span data-ttu-id="bc76c-146">Для просмотра установленной переменной введите **$Configuration**.</span><span class="sxs-lookup"><span data-stu-id="bc76c-146">To see what you set, type **$Configuration**.</span></span>

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

<span data-ttu-id="bc76c-147">В остальной части раздела предполагается, что вы создали переменную описанным способом.</span><span class="sxs-lookup"><span data-stu-id="bc76c-147">The rest of this section assumes that you have a variable created as just described.</span></span>

##### <a name="declare-the-virtual-network-to-the-app"></a><span data-ttu-id="bc76c-148">Объявление виртуальной сети для приложения</span><span class="sxs-lookup"><span data-stu-id="bc76c-148">Declare the virtual network to the app</span></span>
<span data-ttu-id="bc76c-149">При помощи команды ниже сообщите приложению, что оно будет использовать указанную виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="bc76c-149">Use the following command to tell the app that it will be using this particular virtual network.</span></span> <span data-ttu-id="bc76c-150">При выполнении этой команды приложение создаст необходимые сертификаты:</span><span class="sxs-lookup"><span data-stu-id="bc76c-150">This will cause the app to generate necessary certificates:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

<span data-ttu-id="bc76c-151">Если команда выполнится успешно, **$vnet** будет содержать переменную **Properties**.</span><span class="sxs-lookup"><span data-stu-id="bc76c-151">If this command succeeds, **$vnet** should have a **Properties** variable in it.</span></span> <span data-ttu-id="bc76c-152">Переменная **Properties** должна содержать отпечаток и данные сертификата.</span><span class="sxs-lookup"><span data-stu-id="bc76c-152">The **Properties** variable should contain both a certificate thumbprint and the certificate data.</span></span>

##### <a name="upload-the-web-app-certificate-to-the-virtual-network"></a><span data-ttu-id="bc76c-153">Отправка сертификата веб-приложения в виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="bc76c-153">Upload the web app certificate to the virtual network</span></span>
<span data-ttu-id="bc76c-154">Для каждого сочетания виртуальной сети и подписки необходимо выполнить однократное действие вручную.</span><span class="sxs-lookup"><span data-stu-id="bc76c-154">A manual, one-time step is required for each subscription and virtual network combination.</span></span> <span data-ttu-id="bc76c-155">То есть при подключении приложений в подписке A к виртуальной сети A это действие нужно выполнить только один раз независимо от того, сколько приложений вы настраиваете.</span><span class="sxs-lookup"><span data-stu-id="bc76c-155">That is, if you are connecting apps in Subscription A to Virtual Network A, you will need to do this step only once regardless of how many apps you configure.</span></span> <span data-ttu-id="bc76c-156">При добавлении нового приложения в другую виртуальную сеть вам понадобится сделать это снова.</span><span class="sxs-lookup"><span data-stu-id="bc76c-156">If you are adding a new app to another virtual network, you'll need to do this again.</span></span> <span data-ttu-id="bc76c-157">Это связано с тем, что набор сертификатов создается на уровне подписки в службе приложений Azure и один раз для каждой виртуальной сети, к которой будут подключаться приложения.</span><span class="sxs-lookup"><span data-stu-id="bc76c-157">The reason for this is that a set of certificates is generated at a subscription level in Azure App Service, and the set is generated once for each virtual network that the apps will connect to.</span></span>

<span data-ttu-id="bc76c-158">Если вы выполнили эти действия или выполнили интеграцию с той же виртуальной сетью с помощью портала, сертификаты уже будут настроены.</span><span class="sxs-lookup"><span data-stu-id="bc76c-158">The certificates will have already been set if you followed these steps or if you integrated with the same virtual network by using the portal.</span></span>

<span data-ttu-id="bc76c-159">Сначала необходимо создать CER-файл.</span><span class="sxs-lookup"><span data-stu-id="bc76c-159">The first step is to generate the .cer file.</span></span> <span data-ttu-id="bc76c-160">Затем необходимо отправить CER-файл в виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="bc76c-160">The second step is to upload the .cer file to your virtual network.</span></span> <span data-ttu-id="bc76c-161">Чтобы создать CER-файл с помощью вызова API на предыдущем шаге, выполните следующие команды.</span><span class="sxs-lookup"><span data-stu-id="bc76c-161">To generate the .cer file from the API call in the earlier step, run the following commands.</span></span>

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

<span data-ttu-id="bc76c-162">Сертификат будет находиться в расположении, которое задано с помощью параметра **$Configuration.GeneratedCertificatePath** .</span><span class="sxs-lookup"><span data-stu-id="bc76c-162">The certificate will be found in the location that **$Configuration.GeneratedCertificatePath** specifies.</span></span>

<span data-ttu-id="bc76c-163">Чтобы отправить сертификат вручную, на [портале Azure][azureportal] выберите **Browse Virtual Network (classic)** (Обзор виртуальных сетей (классических)) > **VPN-подключения** > **Точка-сеть** > **Управление сертификатами**.</span><span class="sxs-lookup"><span data-stu-id="bc76c-163">To upload the certificate manually, use the [Azure portal][azureportal] and **Browse Virtual Network (classic)** > **VPN connections** > **Point-to-site** > **Manage certificates**.</span></span> <span data-ttu-id="bc76c-164">Здесь можно отправить сертификат.</span><span class="sxs-lookup"><span data-stu-id="bc76c-164">From here, upload your certificate.</span></span>

##### <a name="get-the-point-to-site-package"></a><span data-ttu-id="bc76c-165">Получение пакета "точка — сеть"</span><span class="sxs-lookup"><span data-stu-id="bc76c-165">Get the point-to-site package</span></span>
<span data-ttu-id="bc76c-166">Следующий шаг при настройке подключения веб-приложения к виртуальной сети — получение пакета "точка — сеть" и его указание в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="bc76c-166">The next step in setting up a virtual network connection on a web app is to get the point-to-site package and provide it to your web app.</span></span>

<span data-ttu-id="bc76c-167">Сохраните следующий шаблон в файл с именем GetNetworkPackageUri.json в произвольном каталоге на вашем компьютере, например C:\Azure\Templates\GetNetworkPackageUri.json.</span><span class="sxs-lookup"><span data-stu-id="bc76c-167">Save the following template to a file called GetNetworkPackageUri.json somewhere on your computer, for example, C:\Azure\Templates\GetNetworkPackageUri.json.</span></span>

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


<span data-ttu-id="bc76c-168">Задайте входные параметры.</span><span class="sxs-lookup"><span data-stu-id="bc76c-168">Set input parameters:</span></span>

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

<span data-ttu-id="bc76c-169">Вызовите сценарий:</span><span class="sxs-lookup"><span data-stu-id="bc76c-169">Call the script:</span></span>

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


<span data-ttu-id="bc76c-170">Переменная **$output.Outputs.packageUri** будет содержать URI пакета, который передастся веб-приложению.</span><span class="sxs-lookup"><span data-stu-id="bc76c-170">The variable **$output.Outputs.packageUri** will now contain the package URI to be given to your web app.</span></span>

##### <a name="upload-the-point-to-site-package-to-your-app"></a><span data-ttu-id="bc76c-171">Отправка пакета "точка-сеть" в приложение</span><span class="sxs-lookup"><span data-stu-id="bc76c-171">Upload the point-to-site package to your app</span></span>
<span data-ttu-id="bc76c-172">Последним шагом является отправка пакета в приложение.</span><span class="sxs-lookup"><span data-stu-id="bc76c-172">The final step is to provide the app with this package.</span></span> <span data-ttu-id="bc76c-173">Для этого просто выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bc76c-173">Simply run the next command:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

<span data-ttu-id="bc76c-174">Если появится сообщение о перезаписи существующего ресурса, обязательно подтвердите перезапись.</span><span class="sxs-lookup"><span data-stu-id="bc76c-174">If a message asks you to confirm that you are overwriting an existing resource, make sure to allow it.</span></span>

<span data-ttu-id="bc76c-175">После успешного выполнения этой команды приложение будет подключено к виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bc76c-175">After this command succeeds, your app should now be connected to the virtual network.</span></span> <span data-ttu-id="bc76c-176">Чтобы убедиться в этом, перейдите к консоли приложения и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="bc76c-176">To confirm success, go to your app console, and type the following:</span></span>

    SET WEBSITE_

<span data-ttu-id="bc76c-177">Если вы видите переменную среды WEBSITE_VNETNAME со значением, соответствующим имени целевой виртуальной сети, это означает, что все конфигурации успешно установлены.</span><span class="sxs-lookup"><span data-stu-id="bc76c-177">If there is an environment variable called WEBSITE_VNETNAME that has a value that matches the name of the target virtual network, all configurations have succeeded.</span></span>

### <a name="update-classic-vnet-integration-information"></a><span data-ttu-id="bc76c-178">Обновление сведений об интеграции с классической виртуальной сетью</span><span class="sxs-lookup"><span data-stu-id="bc76c-178">Update classic VNet integration information</span></span>
<span data-ttu-id="bc76c-179">Чтобы обновить или повторно синхронизировать данные, просто повторите действия, выполненные при первоначальной настройке интеграции.</span><span class="sxs-lookup"><span data-stu-id="bc76c-179">To update or resync your information, simply repeat the steps that you followed when you created the integration in the first place.</span></span> <span data-ttu-id="bc76c-180">К этим действиям относятся:</span><span class="sxs-lookup"><span data-stu-id="bc76c-180">Those steps are:</span></span>

1. <span data-ttu-id="bc76c-181">Определение данных конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bc76c-181">Define your configuration information.</span></span>
2. <span data-ttu-id="bc76c-182">Объявление виртуальной сети для приложения.</span><span class="sxs-lookup"><span data-stu-id="bc76c-182">Declare the virtual network to the app.</span></span>
3. <span data-ttu-id="bc76c-183">Получение пакета "точка — сеть".</span><span class="sxs-lookup"><span data-stu-id="bc76c-183">Get the point-to-site package.</span></span>
4. <span data-ttu-id="bc76c-184">Отправка пакета "точка — сеть" в приложение.</span><span class="sxs-lookup"><span data-stu-id="bc76c-184">Upload the point-to-site package to your app.</span></span>

### <a name="disconnect-your-app-from-a-classic-vnet"></a><span data-ttu-id="bc76c-185">Отключение приложения от классической виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="bc76c-185">Disconnect your app from a classic VNet</span></span>
<span data-ttu-id="bc76c-186">Для отключения приложения вам понадобятся данные конфигурации, которые использовались при интеграции с виртуальной сетью.</span><span class="sxs-lookup"><span data-stu-id="bc76c-186">To disconnect the app, you need the configuration information that was set during virtual network integration.</span></span> <span data-ttu-id="bc76c-187">После получения этих данных достаточно выполнить команду ниже, чтобы отключить приложение от виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bc76c-187">Using that information, there is then one command to disconnect your app from your virtual network.</span></span>

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a><span data-ttu-id="bc76c-188">Виртуальные сети Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bc76c-188">Resource Manager virtual networks</span></span>
<span data-ttu-id="bc76c-189">У виртуальных сетей Resource Manager есть интерфейсы API Azure Resource Manager, которые упрощают некоторые процессы по сравнению с классическими виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="bc76c-189">Resource Manager virtual networks have Azure Resource Manager APIs, which simplify some processes when compared with classic virtual networks.</span></span> <span data-ttu-id="bc76c-190">У нас есть скрипт, который поможет вам выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="bc76c-190">We have a script that will help you complete the following tasks:</span></span>

* <span data-ttu-id="bc76c-191">создать виртуальную сеть Resource Manager и интегрировать свое приложение с ней;</span><span class="sxs-lookup"><span data-stu-id="bc76c-191">Create a Resource Manager virtual network and integrate your app with it.</span></span>
* <span data-ttu-id="bc76c-192">создать шлюз, настроить подключение "точка — сеть" в созданной ранее виртуальной сети Resource Manager, а затем интегрировать свое приложение с ней;</span><span class="sxs-lookup"><span data-stu-id="bc76c-192">Create a gateway, configure point-to-site connectivity in a preexisting Resource Manager virtual network, and then integrate your app with it.</span></span>
* <span data-ttu-id="bc76c-193">интегрировать свое приложение с созданной ранее виртуальной сетью Resource Manager, у которой есть шлюз и включенное подключение "точка — сеть";</span><span class="sxs-lookup"><span data-stu-id="bc76c-193">Integrate your app with a preexisting Resource Manager virtual network that has a gateway and point-to-site connectivity enabled.</span></span>
* <span data-ttu-id="bc76c-194">отключение приложения от виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bc76c-194">Disconnect your app from your virtual network.</span></span>

### <a name="resource-manager-vnet-app-service-integration-script"></a><span data-ttu-id="bc76c-195">Скрипт для интеграции службы приложений для виртуальной сети Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bc76c-195">Resource Manager VNet App Service integration script</span></span>
<span data-ttu-id="bc76c-196">Скопируйте приведенный ниже скрипт и сохраните его в файл.</span><span class="sxs-lookup"><span data-stu-id="bc76c-196">Copy the following script and save it to a file.</span></span> <span data-ttu-id="bc76c-197">Если вы не хотите использовать скрипт, изучите его, чтобы узнать, как выполнить настройку для виртуальной сети Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bc76c-197">If you don’t want to use the script, feel free to learn from it to see how to set things up with a Resource Manager virtual network.</span></span>

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

        Write-Host "Adding a root certificate to this VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up to an hour."
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
            Write-Host "Currently, I will create a VNET with the following settings:"
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
            $changeRequested = PromptYesNo "" "Do you wish to change these settings?" 1

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

        # We create the virtual network and add it here. The way this works is:
        # 1) Add the VNET association to the App. This allows the App to generate certificates, etc. for the VNET.
        # 2) Create the VNET and VNET gateway, add the certificates, create the public IP, etc., required for the gateway
        # 3) Get the VPN package from the gateway and pass it back to the App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association to VNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying to App"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at the start and the end of the URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put the VPN client configuration package onto the App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, the gateway should be able to be joined to an App, but may require some minor tweaking. We will declare to the App now to use this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected to VNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET to integrate with" $vnets $vnetNames

        # We need to check if this VNET is able to be joined to a App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have the right certificate, we will need to add it.
                # If it doesn't have a point-to-site range, we will need to add it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need to create one.
            Write-Host "This Virtual Network has no gateway. I will need to create one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in the address space $($vnet.AddressSpace.AddressPrefixes), with the following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with the following settings:"
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
                $changeRequested = PromptYesNo "" "Do you wish to change these settings?" 1

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

            Write-Host "Creating App association to VNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need to create one.
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
                Write-Error "This gateway is not of the Vpn type. It cannot be joined to an App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined to an App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association to VNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need to check if the certificate here exists in the gateway.
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

        # Now finish joining by getting the VPN package and giving it to the App
        Write-Host "Retrieving VPN Package and supplying to App"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at the start and the end of the URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put the VPN client configuration package onto the App
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
            Write-Host "Currently connected to VNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected to a VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound to this account."
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

    $resourceGroup = Read-Host "Please enter the Resource Group of your App"

    $appName = Read-Host "Please enter the Name of your App"

    $options = @("Add a NEW Virtual Network to an App", "Add an EXISTING Virtual Network to an App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want to do?" $optionValues $options

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

<span data-ttu-id="bc76c-198">Сохраните копию сценария.</span><span class="sxs-lookup"><span data-stu-id="bc76c-198">Save a copy of the script.</span></span> <span data-ttu-id="bc76c-199">В этой статье он называется V2VnetAllinOne.ps1, но можно использовать другое имя.</span><span class="sxs-lookup"><span data-stu-id="bc76c-199">In this article, it is called V2VnetAllinOne.ps1, but you can use another name.</span></span> <span data-ttu-id="bc76c-200">Для этого сценария не нужно указывать никаких аргументов.</span><span class="sxs-lookup"><span data-stu-id="bc76c-200">There are no arguments for this script.</span></span> <span data-ttu-id="bc76c-201">Просто запустите его.</span><span class="sxs-lookup"><span data-stu-id="bc76c-201">You simply run it.</span></span> <span data-ttu-id="bc76c-202">Сначала сценарий попросит вас выполнить вход в систему.</span><span class="sxs-lookup"><span data-stu-id="bc76c-202">The first thing the script will do is prompt you to sign in.</span></span> <span data-ttu-id="bc76c-203">После входа сценарий отображает сведения о вашей учетной записи и список подписок.</span><span class="sxs-lookup"><span data-stu-id="bc76c-203">After you sign in, the script gets details about your account and returns a list of subscriptions.</span></span> <span data-ttu-id="bc76c-204">Не считая запроса на ввод учетных данных, первоначальный запуск скрипта выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="bc76c-204">Not counting the request for your credentials, the initial script execution looks like this:</span></span>

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) <span data-ttu-id="bc76c-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span><span class="sxs-lookup"><span data-stu-id="bc76c-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span></span>
    2) <span data-ttu-id="bc76c-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span><span class="sxs-lookup"><span data-stu-id="bc76c-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span></span>
    3) <span data-ttu-id="bc76c-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span><span class="sxs-lookup"><span data-stu-id="bc76c-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span></span>

    <span data-ttu-id="bc76c-208">Выберите вариант: 3</span><span class="sxs-lookup"><span data-stu-id="bc76c-208">Choose an option: 3</span></span>

    <span data-ttu-id="bc76c-209">Учетная запись      : ccompy@microsoft.com Среда  : AzureCloud Подписка : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Клиент       : 722278f-fef1-499f-91ab-2323d011db47</span><span class="sxs-lookup"><span data-stu-id="bc76c-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span></span>

    <span data-ttu-id="bc76c-210">Введите группу ресурсов своего приложения: hcdemo-rg Введите имя своего приложения: v2vnetpowershell Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bc76c-210">Please enter the Resource Group of your App: hcdemo-rg Please enter the Name of your App: v2vnetpowershell What do you want to do?</span></span>

    1) <span data-ttu-id="bc76c-211">Добавление НОВОЙ виртуальной сети в приложение</span><span class="sxs-lookup"><span data-stu-id="bc76c-211">Add a NEW Virtual Network to an App</span></span>
    2) <span data-ttu-id="bc76c-212">Добавление ИМЕЮЩЕЙСЯ виртуальной сети в приложение</span><span class="sxs-lookup"><span data-stu-id="bc76c-212">Add an EXISTING Virtual Network to an App</span></span>
    3) <span data-ttu-id="bc76c-213">Удаление виртуальной сети из приложения</span><span class="sxs-lookup"><span data-stu-id="bc76c-213">Remove a Virtual Network from an App</span></span>

<span data-ttu-id="bc76c-214">В остальной части раздела описываются все три варианта.</span><span class="sxs-lookup"><span data-stu-id="bc76c-214">The rest of this section explains each of those three options.</span></span>

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a><span data-ttu-id="bc76c-215">Создание виртуальной сети Resource Manager и интеграция с ней</span><span class="sxs-lookup"><span data-stu-id="bc76c-215">Create a Resource Manager VNet and integrate with it</span></span>
<span data-ttu-id="bc76c-216">Чтобы создать новую виртуальную сеть, которая использует модель развертывания Resource Manager, и интегрировать ее с вашим приложением, выберите вариант **1) Добавить к приложению НОВУЮ виртуальную сеть**.</span><span class="sxs-lookup"><span data-stu-id="bc76c-216">To create a new virtual network that uses the Resource Manager deployment model and integrate it with your app, select **1) Add a NEW Virtual Network to an App**.</span></span> <span data-ttu-id="bc76c-217">После этого вам будет предложено указать имя виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bc76c-217">This will prompt you for the name of the virtual network.</span></span> <span data-ttu-id="bc76c-218">В этом случае, как видно в следующих параметрах, используется имя v2pshell.</span><span class="sxs-lookup"><span data-stu-id="bc76c-218">In my case, as you can see in the following settings, I used the name, v2pshell.</span></span>

<span data-ttu-id="bc76c-219">Скрипт сообщает сведения о создаваемой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bc76c-219">The script gives the details about the virtual network that's being created.</span></span> <span data-ttu-id="bc76c-220">При желании можно изменить любой из параметров.</span><span class="sxs-lookup"><span data-stu-id="bc76c-220">If I want, I can change any of the values.</span></span> <span data-ttu-id="bc76c-221">При выполнении этого примера созданная виртуальная сеть имеет следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="bc76c-221">In this example execution, I created a virtual network that has the following settings:</span></span>

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish to change these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

<span data-ttu-id="bc76c-222">Если требуется изменить какой-то параметр, нажмите клавишу **Y** и внесите необходимые изменения.</span><span class="sxs-lookup"><span data-stu-id="bc76c-222">If you want to change any of the values, type **Y** and make the changes.</span></span> <span data-ttu-id="bc76c-223">После изменения всех параметров виртуальной сети нажмите клавишу **N** или ВВОД при появлении запроса на изменение параметров.</span><span class="sxs-lookup"><span data-stu-id="bc76c-223">When you are happy with the virtual network settings, type **N** or simply press Enter when prompted about changing the settings.</span></span> <span data-ttu-id="bc76c-224">После этого скрипт будет сообщать вам о некоторых выполняемых действиях вплоть до создания шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bc76c-224">From there on until completion, the script will tell you some of what it' i's doing until it starts to create the virtual network gateway.</span></span> <span data-ttu-id="bc76c-225">Создание шлюза может занять до одного часа.</span><span class="sxs-lookup"><span data-stu-id="bc76c-225">That step can take up to an hour.</span></span> <span data-ttu-id="bc76c-226">Хотя на этом шаге нет индикатора выполнения, по завершении создания шлюза вы получите соответствующее сообщение.</span><span class="sxs-lookup"><span data-stu-id="bc76c-226">There is no progress indicator during this phase, but the script will let you know when the gateway has been created.</span></span>

<span data-ttu-id="bc76c-227">После выполнения скрипта на экране появится сообщение **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="bc76c-227">When the script finishes, it will say **Finished**.</span></span> <span data-ttu-id="bc76c-228">На этом этапе у вас есть виртуальная сеть Resource Manager с выбранными вами именем и параметрами.</span><span class="sxs-lookup"><span data-stu-id="bc76c-228">At this point, you will have a Resource Manager virtual network that has the name and settings that you selected.</span></span> <span data-ttu-id="bc76c-229">Эта новая виртуальная сеть также будет интегрирована с приложением.</span><span class="sxs-lookup"><span data-stu-id="bc76c-229">This new virtual network will also be integrated with your app.</span></span>

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a><span data-ttu-id="bc76c-230">Интеграция приложения с созданной ранее виртуальной сетью Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bc76c-230">Integrate your app with a preexisting Resource Manager VNet</span></span>
<span data-ttu-id="bc76c-231">Если при интеграции с созданной ранее виртуальной сетью указать виртуальную сеть Resource Manager, у которой нет шлюза или для которой не настроено подключение "точка — сеть", то скрипт настроит их.</span><span class="sxs-lookup"><span data-stu-id="bc76c-231">When you're integrating with a preexisting virtual network, if you provide a Resource Manager virtual network that doesn’t have a gateway or point-to-site connectivity, the script will set that up.</span></span> <span data-ttu-id="bc76c-232">Если они уже настроены, скрипт сразу перейдет к интеграции приложения.</span><span class="sxs-lookup"><span data-stu-id="bc76c-232">If the VNET already has those things set up, the script goes straight to the app integration.</span></span> <span data-ttu-id="bc76c-233">Чтобы запустить этот процесс, просто выберите вариант **2) Добавить к приложению СУЩЕСТВУЮЩУЮ виртуальную сеть**.</span><span class="sxs-lookup"><span data-stu-id="bc76c-233">To start this process, simply select **2) Add an EXISTING Virtual Network to an App**.</span></span>

<span data-ttu-id="bc76c-234">Этот вариант можно использовать только в том случае, если у вас есть созданная ранее виртуальная сеть Resource Manager, которая находится в той же подписке, что приложение.</span><span class="sxs-lookup"><span data-stu-id="bc76c-234">This option works only if you have a preexisting Resource Manager virtual network that is in the same subscription as your app.</span></span> <span data-ttu-id="bc76c-235">После выбора варианта появится список виртуальных сетей Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bc76c-235">After you select the option, you will be presented with a list of your Resource Manager virtual networks.</span></span>   

    Select a VNET to integrate with

    1) <span data-ttu-id="bc76c-236">v2demonetwork</span><span class="sxs-lookup"><span data-stu-id="bc76c-236">v2demonetwork</span></span>
    2) <span data-ttu-id="bc76c-237">v2pshell</span><span class="sxs-lookup"><span data-stu-id="bc76c-237">v2pshell</span></span>
    3) <span data-ttu-id="bc76c-238">v2vnetintdemo</span><span class="sxs-lookup"><span data-stu-id="bc76c-238">v2vnetintdemo</span></span>
    4) <span data-ttu-id="bc76c-239">v2asenetwork</span><span class="sxs-lookup"><span data-stu-id="bc76c-239">v2asenetwork</span></span>
    5) <span data-ttu-id="bc76c-240">v2pshell2</span><span class="sxs-lookup"><span data-stu-id="bc76c-240">v2pshell2</span></span>

    <span data-ttu-id="bc76c-241">Выберите вариант: 5</span><span class="sxs-lookup"><span data-stu-id="bc76c-241">Choose an option: 5</span></span>

<span data-ttu-id="bc76c-242">Просто выберите виртуальную сеть, с которой нужно выполнить интеграцию.</span><span class="sxs-lookup"><span data-stu-id="bc76c-242">Simply select the virtual network that you want to integrate with.</span></span> <span data-ttu-id="bc76c-243">Если у вас уже есть шлюз с настроенным подключением "точка — сеть", то скрипт просто интегрирует ваше приложение с виртуальной сетью.</span><span class="sxs-lookup"><span data-stu-id="bc76c-243">If you already have a gateway that has point-to-site connectivity enabled, the script will simply integrate your app with your virtual network.</span></span> <span data-ttu-id="bc76c-244">Если у вас нет шлюза, потребуется указать подсеть шлюза.</span><span class="sxs-lookup"><span data-stu-id="bc76c-244">If you do not have a gateway, you will need to specify the gateway subnet.</span></span> <span data-ttu-id="bc76c-245">Подсеть шлюза должна находиться в адресном пространстве виртуальной сети и не может находиться ни в какой другой подсети.</span><span class="sxs-lookup"><span data-stu-id="bc76c-245">Your gateway subnet must be in your virtual network address space, and it cannot be in any other subnet.</span></span> <span data-ttu-id="bc76c-246">При выполнении этого шага для виртуальной сети без шлюза вы получите следующий результат:</span><span class="sxs-lookup"><span data-stu-id="bc76c-246">If you have a virtual network without a gateway and run this step, things look like this:</span></span>

    This Virtual Network has no gateway. I will need to create one.
    Your VNET is in the address space 172.16.0.0/16, with the following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

<span data-ttu-id="bc76c-247">В этом примере создан шлюз виртуальной сети со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="bc76c-247">In this example, I created a virtual network gateway that has the following settings:</span></span>

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish to change these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association to VNET

<span data-ttu-id="bc76c-248">При необходимости эти параметры можно изменить.</span><span class="sxs-lookup"><span data-stu-id="bc76c-248">If you want to change any of those settings, you can do so.</span></span> <span data-ttu-id="bc76c-249">Если такой необходимости нет, нажмите клавишу ВВОД, чтобы скрипт создал шлюз и подключил приложение к виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bc76c-249">Otherwise, press Enter and the script will create your gateway and attach your app to your virtual network.</span></span> <span data-ttu-id="bc76c-250">При этом на создание шлюза все равно требуется около часа.</span><span class="sxs-lookup"><span data-stu-id="bc76c-250">The gateway creation time is still an hour, though, so make sure you keep that in mind.</span></span> <span data-ttu-id="bc76c-251">После выполнения всех действий скрипт выдаст сообщение **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="bc76c-251">When everything is finished, the script will say **Finished**.</span></span>

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a><span data-ttu-id="bc76c-252">Отключение приложения от виртуальной сети Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bc76c-252">Disconnect your app from a Resource Manager VNet</span></span>
<span data-ttu-id="bc76c-253">При отключении приложения от виртуальной сети не происходит отключение шлюза или подключения "точка — сеть".</span><span class="sxs-lookup"><span data-stu-id="bc76c-253">Disconnecting your app from your virtual network does not take down the gateway or disable point-to-site connectivity.</span></span> <span data-ttu-id="bc76c-254">В конце концов, их можно использовать и для других целей.</span><span class="sxs-lookup"><span data-stu-id="bc76c-254">You might, after all, be using it for something else.</span></span> <span data-ttu-id="bc76c-255">Они также не отключаются от других приложений, кроме указанных вами.</span><span class="sxs-lookup"><span data-stu-id="bc76c-255">It also does not disconnect it from any other apps other than the one you provided.</span></span> <span data-ttu-id="bc76c-256">Чтобы выполнить это действие, выберите вариант **3) Удалить виртуальную сеть из приложения**.</span><span class="sxs-lookup"><span data-stu-id="bc76c-256">To perform this action, select **3) Remove a Virtual Network from an App**.</span></span> <span data-ttu-id="bc76c-257">При выборе этого варианта вы увидите следующее:</span><span class="sxs-lookup"><span data-stu-id="bc76c-257">When you do so, you will see something like this:</span></span>

    Currently connected to VNET v2pshell

    Confirm
    Are you sure you want to delete the following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

<span data-ttu-id="bc76c-258">Несмотря на то, что в скрипте говорится об удалении, виртуальная сеть не будет удалена.</span><span class="sxs-lookup"><span data-stu-id="bc76c-258">Although the script says delete, it does not delete the virtual network.</span></span> <span data-ttu-id="bc76c-259">Он удаляет только интеграцию.</span><span class="sxs-lookup"><span data-stu-id="bc76c-259">It’s just removing the integration.</span></span> <span data-ttu-id="bc76c-260">После подтверждения действия команда будет выполнена довольно быстро, а после ее завершения вы увидите сообщение **True** .</span><span class="sxs-lookup"><span data-stu-id="bc76c-260">After you confirm that this is what you want to do, the command is processed quite quickly and tells you **True** when it is done.</span></span>

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
