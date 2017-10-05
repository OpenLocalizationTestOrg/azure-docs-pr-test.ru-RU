---
title: "Включение удаленной отладки при использовании непрерывной доставки | Документация Майкрософт"
description: "Узнайте, как можно включить удаленную отладку при использовании непрерывной доставки, чтобы выполнять развертывание на Azure"
services: cloud-services
documentationcenter: .net
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d423639-3b2f-4ca5-ac5a-9ac19a217c29
ms.service: cloud-services
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 7a8a853a93e3e9915f687a20c871444e6a0de50d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="enable-remote-debugging-when-using-continuous-delivery-to-publish-to-azure"></a><span data-ttu-id="244b3-103">Включение удаленной отладки при использовании непрерывной доставки для публикации на Azure</span><span class="sxs-lookup"><span data-stu-id="244b3-103">Enable remote debugging when using continuous delivery to publish to Azure</span></span>
<span data-ttu-id="244b3-104">Когда для публикации в Azure используется [непрерывная доставка](cloud-services-dotnet-continuous-delivery.md), в службе Azure можно включить удаленную отладку для облачных служб или виртуальных машин. Для этого следует выполнить рассмотренную ниже процедуру.</span><span class="sxs-lookup"><span data-stu-id="244b3-104">You can enable remote debugging in Azure, for cloud services or virtual machines, when you use [continuous delivery](cloud-services-dotnet-continuous-delivery.md) to publish to Azure by following these steps.</span></span>

## <a name="enabling-remote-debugging-for-cloud-services"></a><span data-ttu-id="244b3-105">Включение удаленной отладки для облачных служб</span><span class="sxs-lookup"><span data-stu-id="244b3-105">Enabling remote debugging for cloud services</span></span>
1. <span data-ttu-id="244b3-106">В агенте сборки настройте начальную среду для Azure, как описано в разделе [Сборка с помощью командной строки для Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span><span class="sxs-lookup"><span data-stu-id="244b3-106">On the build agent, set up the initial environment for Azure as outlined in [Command-Line Build for Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span></span>
2. <span data-ttu-id="244b3-107">Так как для пакета требуется среда выполнения удаленной отладки (msvsmon.exe), установите **инструменты удаленной отладки для Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="244b3-107">Because the remote debug runtime (msvsmon.exe) is required for the package, install the **Remote Tools for Visual Studio**.</span></span>

    * [<span data-ttu-id="244b3-108">Инструменты удаленной отладки для Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="244b3-108">Remote Tools for Visual Studio 2017</span></span>](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [<span data-ttu-id="244b3-109">Инструменты удаленной отладки для Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="244b3-109">Remote Tools for Visual Studio 2015</span></span>](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [<span data-ttu-id="244b3-110">Инструменты удаленной отладки для Visual Studio 2013 с обновлением 5</span><span class="sxs-lookup"><span data-stu-id="244b3-110">Remote Tools for Visual Studio 2013 Update 5</span></span>](https://www.microsoft.com/download/details.aspx?id=48156)
    
    <span data-ttu-id="244b3-111">В качестве альтернативы можно скопировать двоичные файлы удаленной отладки из системы, где установлена Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="244b3-111">As an alternative, you can copy the remote debug binaries from a system that has Visual Studio installed.</span></span>

3. <span data-ttu-id="244b3-112">Создайте сертификат, как описано в разделе [Общие сведения о сертификатах для облачных служб Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="244b3-112">Create a certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="244b3-113">Оставьте .pfx и отпечаток сертификата RDP, и загрузите сертификат в целевую облачную службу.</span><span class="sxs-lookup"><span data-stu-id="244b3-113">Keep the .pfx and RDP certificate thumbprint and upload the certificate to the target cloud service.</span></span>
4. <span data-ttu-id="244b3-114">Для сборки и упаковки с включенной функцией удаленной отладки используйте следующие параметры в командной строке MSBuild.</span><span class="sxs-lookup"><span data-stu-id="244b3-114">Use the following options in the MSBuild command line to build and package with remote debug enabled.</span></span> <span data-ttu-id="244b3-115">(Подставьте фактические пути к системным и проектным файлам для элементов, заключенных в угловые скобки).</span><span class="sxs-lookup"><span data-stu-id="244b3-115">(Substitute actual paths to your system and project files for the angle-bracketed items.)</span></span>
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of the certificate added to the cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path to your VS solution file>"
   
    <span data-ttu-id="244b3-116">`VSX64RemoteDebuggerPath` — путь к папке, содержащей msvsmon.exe и инструменты удаленной отладки для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="244b3-116">`VSX64RemoteDebuggerPath` is the path to the folder containing msvsmon.exe in the Remote Tools for Visual Studio.</span></span>
    <span data-ttu-id="244b3-117">`RemoteDebuggerConnectorVersion` — это версия пакета Azure SDK в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="244b3-117">`RemoteDebuggerConnectorVersion` is the Azure SDK version in your cloud service.</span></span> <span data-ttu-id="244b3-118">Она должна соответствовать версии, установленной с Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="244b3-118">It should also match the version installed with Visual Studio.</span></span>
5. <span data-ttu-id="244b3-119">Опубликуйте в целевой облачной службе с помощью пакета и файла .cscfg, созданного на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="244b3-119">Publish to the target cloud service by using the package and .cscfg file generated in the previous step.</span></span>
6. <span data-ttu-id="244b3-120">Импортируйте сертификат (файл .pfx) на машину, на которой имеется Visual Studio с установленным пакетом Azure SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="244b3-120">Import the certificate (.pfx file) to the machine that has Visual Studio with Azure SDK for .NET installed.</span></span> <span data-ttu-id="244b3-121">Импортировать в хранилище сертификатов `CurrentUser\My` обязательно, иначе вы не сможете присоединить отладчик в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="244b3-121">Make sure to import to the `CurrentUser\My` certificate store, otherwise attaching to the debugger in Visual Studio will fail.</span></span>

## <a name="enabling-remote-debugging-for-virtual-machines"></a><span data-ttu-id="244b3-122">Включение удаленной отладки для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="244b3-122">Enabling remote debugging for virtual machines</span></span>
1. <span data-ttu-id="244b3-123">Создайте виртуальную машину Azure.</span><span class="sxs-lookup"><span data-stu-id="244b3-123">Create an Azure virtual machine.</span></span> <span data-ttu-id="244b3-124">См. статью [Создание первой виртуальной машины Windows на портале Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) или [Создание виртуальных машин Windows и управление ими в Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="244b3-124">See [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [Create and Manage Azure Virtual Machines in Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
2. <span data-ttu-id="244b3-125">На [странице классического портала Azure](http://go.microsoft.com/fwlink/p/?LinkID=269851)откройте панель мониторинга виртуальной машины и найдите **ОТПЕЧАТОК СЕРТИФИКАТА RDP**виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="244b3-125">On the [Azure classic portal page](http://go.microsoft.com/fwlink/p/?LinkID=269851), view the virtual machine's dashboard to see the virtual machine’s **RDP CERTIFICATE THUMBPRINT**.</span></span> <span data-ttu-id="244b3-126">Он используется для `ServerThumbprint` значения в конфигурации расширения.</span><span class="sxs-lookup"><span data-stu-id="244b3-126">This value is used for the `ServerThumbprint` value in the extension configuration.</span></span>
3. <span data-ttu-id="244b3-127">Создайте сертификат клиента, как описано в разделе [Общие сведения о сертификатах для облачных служб Azure](cloud-services-certs-create.md) (оставьте PFX-файл и отпечаток сертификата RDP).</span><span class="sxs-lookup"><span data-stu-id="244b3-127">Create a client certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md) (keep the .pfx and RDP certificate thumbprint).</span></span>
4. <span data-ttu-id="244b3-128">Установите Azure Powershell (0.7.4 или более поздней версии), как описано в разделе [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="244b3-128">Install Azure Powershell (version 0.7.4 or later) as outlined in [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
5. <span data-ttu-id="244b3-129">Выполните следующий скрипт, чтобы включить расширение RemoteDebug.</span><span class="sxs-lookup"><span data-stu-id="244b3-129">Run the following script to enable the RemoteDebug extension.</span></span> <span data-ttu-id="244b3-130">Замените пути и персональные данные своими собственными (например, укажите имя своей подписки, имя службы и отпечаток).</span><span class="sxs-lookup"><span data-stu-id="244b3-130">Replace the paths and personal data with your own, such as your subscription name, service name, and thumbprint.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="244b3-131">Этот сценарий настроен для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="244b3-131">This script is configured for Visual Studio 2015.</span></span> <span data-ttu-id="244b3-132">Если вы используете Visual Studio 2013 или Visual Studio 2017, измените назначения `$referenceName` и `$extensionName` ниже, чтобы использовать `RemoteDebugVS2013` или `RemoteDebugVS2017`.</span><span class="sxs-lookup"><span data-stu-id="244b3-132">If you’re using Visual Studio 2013 or Visual Studio 2017, modify the `$referenceName` and `$extensionName` assignments below to `RemoteDebugVS2013` or `RemoteDebugVS2017`.</span></span>

    ```powershell   
    Add-AzureAccount

    Select-AzureSubscription "My Microsoft Subscription"

    $vm = Get-AzureVM -ServiceName "mytestvm1" -Name "mytestvm1"

    $endpoints = @(
                    ,@{Name="RDConnVS2013"; PublicPort=30400; PrivatePort=30398}
                    ,@{Name="RDFwdrVS2013"; PublicPort=31400; PrivatePort=31398}
                )

    foreach($endpoint in $endpoints)
    {
        Add-AzureEndpoint -VM $vm -Name $endpoint.Name -Protocol tcp -PublicPort $endpoint.PublicPort -LocalPort $endpoint.PrivatePort
    }

    $referenceName = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug.RemoteDebugVS2015"
    $publisher = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug"
    $extensionName = "RemoteDebugVS2015"
    $version = "1.*"
    $publicConfiguration = "<PublicConfig><Connector.Enabled>true</Connector.Enabled><ClientThumbprint>56D7D1B25B472268E332F7FC0C87286458BFB6B2</ClientThumbprint><ServerThumbprint>E7DCB00CB916C468CC3228261D6E4EE45C8ED3C6</ServerThumbprint><ConnectorPort>30398</ConnectorPort><ForwarderPort>31398</ForwarderPort></PublicConfig>"

    $vm | Set-AzureVMExtension -ReferenceName $referenceName -Publisher $publisher -ExtensionName $extensionName -Version $version -PublicConfiguration $publicConfiguration

    foreach($extension in $vm.VM.ResourceExtensionReferences)
    {
        if(($extension.ReferenceName -eq $referenceName) `
        -and ($extension.Publisher -eq $publisher) `
        -and ($extension.Name -eq $extensionName) `
        -and ($extension.Version -eq $version))
        {
            $extension.ResourceExtensionParameterValues[0].Key = 'config.txt'
            break
        }
    }

    $vm | Update-AzureVM
    ```

6. <span data-ttu-id="244b3-133">Импортируйте сертификат (.pfx) на машину, на которой имеется Visual Studio с установленным пакетом Azure SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="244b3-133">Import the certificate (.pfx) to the machine that has Visual Studio with Azure SDK for .NET installed.</span></span>

