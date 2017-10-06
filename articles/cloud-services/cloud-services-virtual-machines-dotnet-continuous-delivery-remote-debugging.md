---
title: "Удаленная отладка при помощи непрерывной поставки aaaEnable | Документы Microsoft"
description: "Узнайте, как tooenable удаленную отладку при использовании непрерывной поставки toodeploy tooAzure"
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
ms.openlocfilehash: d9d9d1cfe5304c9526586a9164f172746a448e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-debugging-when-using-continuous-delivery-toopublish-tooazure"></a><span data-ttu-id="1e7d3-103">Включить удаленную отладку при использовании непрерывной поставки toopublish tooAzure</span><span class="sxs-lookup"><span data-stu-id="1e7d3-103">Enable remote debugging when using continuous delivery toopublish tooAzure</span></span>
<span data-ttu-id="1e7d3-104">Можно включить удаленную отладку в Azure, для облачных служб или виртуальных машин при использовании [непрерывной поставки](cloud-services-dotnet-continuous-delivery.md) tooAzure toopublish, выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="1e7d3-104">You can enable remote debugging in Azure, for cloud services or virtual machines, when you use [continuous delivery](cloud-services-dotnet-continuous-delivery.md) toopublish tooAzure by following these steps.</span></span>

## <a name="enabling-remote-debugging-for-cloud-services"></a><span data-ttu-id="1e7d3-105">Включение удаленной отладки для облачных служб</span><span class="sxs-lookup"><span data-stu-id="1e7d3-105">Enabling remote debugging for cloud services</span></span>
1. <span data-ttu-id="1e7d3-106">На агент сборки hello, настройте hello исходную среду для Azure, перечисленные в [построения командной строки для Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e7d3-106">On hello build agent, set up hello initial environment for Azure as outlined in [Command-Line Build for Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span></span>
2. <span data-ttu-id="1e7d3-107">Поскольку выполнения hello удаленной отладки (msvsmon.exe) является обязательным для hello пакета, установите hello **инструменты удаленной отладки для Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="1e7d3-107">Because hello remote debug runtime (msvsmon.exe) is required for hello package, install hello **Remote Tools for Visual Studio**.</span></span>

    * [<span data-ttu-id="1e7d3-108">Инструменты удаленной отладки для Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="1e7d3-108">Remote Tools for Visual Studio 2017</span></span>](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [<span data-ttu-id="1e7d3-109">Инструменты удаленной отладки для Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="1e7d3-109">Remote Tools for Visual Studio 2015</span></span>](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [<span data-ttu-id="1e7d3-110">Инструменты удаленной отладки для Visual Studio 2013 с обновлением 5</span><span class="sxs-lookup"><span data-stu-id="1e7d3-110">Remote Tools for Visual Studio 2013 Update 5</span></span>](https://www.microsoft.com/download/details.aspx?id=48156)
    
    <span data-ttu-id="1e7d3-111">В качестве альтернативы можно скопировать двоичные файлы удаленной отладки hello из в системе, где установлено приложение Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1e7d3-111">As an alternative, you can copy hello remote debug binaries from a system that has Visual Studio installed.</span></span>

3. <span data-ttu-id="1e7d3-112">Создайте сертификат, как описано в разделе [Общие сведения о сертификатах для облачных служб Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="1e7d3-112">Create a certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="1e7d3-113">Следите за hello .pfx и отпечаток сертификата протокола удаленного рабочего СТОЛА и отправка hello сертификат toohello целевой облачной службы.</span><span class="sxs-lookup"><span data-stu-id="1e7d3-113">Keep hello .pfx and RDP certificate thumbprint and upload hello certificate toohello target cloud service.</span></span>
4. <span data-ttu-id="1e7d3-114">Используйте hello, удаленных с включенной функцией отладки из следующих параметров в toobuild командной строки MSBuild hello и пакета.</span><span class="sxs-lookup"><span data-stu-id="1e7d3-114">Use hello following options in hello MSBuild command line toobuild and package with remote debug enabled.</span></span> <span data-ttu-id="1e7d3-115">(Укажите фактические пути tooyour системы и файлов проекта для элементов, заключенных в угловые скобки hello).</span><span class="sxs-lookup"><span data-stu-id="1e7d3-115">(Substitute actual paths tooyour system and project files for hello angle-bracketed items.)</span></span>
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of hello certificate added toohello cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path tooyour VS solution file>"
   
    <span data-ttu-id="1e7d3-116">`VSX64RemoteDebuggerPath`hello путь toohello папку, содержащую msvsmon.exe в hello инструменты удаленной отладки для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1e7d3-116">`VSX64RemoteDebuggerPath` is hello path toohello folder containing msvsmon.exe in hello Remote Tools for Visual Studio.</span></span>
    <span data-ttu-id="1e7d3-117">`RemoteDebuggerConnectorVersion`— версия пакета Azure SDK hello в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="1e7d3-117">`RemoteDebuggerConnectorVersion` is hello Azure SDK version in your cloud service.</span></span> <span data-ttu-id="1e7d3-118">Кроме того, он должен соответствовать версии hello вместе с Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1e7d3-118">It should also match hello version installed with Visual Studio.</span></span>
5. <span data-ttu-id="1e7d3-119">Публикация toohello целевой облачной службы с помощью hello пакета и cscfg-файл создан в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="1e7d3-119">Publish toohello target cloud service by using hello package and .cscfg file generated in hello previous step.</span></span>
6. <span data-ttu-id="1e7d3-120">Импорт toohello машины hello сертификат (PFX-файл), с Visual Studio с пакетом SDK Azure для установки .NET.</span><span class="sxs-lookup"><span data-stu-id="1e7d3-120">Import hello certificate (.pfx file) toohello machine that has Visual Studio with Azure SDK for .NET installed.</span></span> <span data-ttu-id="1e7d3-121">Убедитесь, что toohello tooimport `CurrentUser\My` хранилище сертификатов, в противном случае присоединение toohello отладчик Visual Studio не удастся.</span><span class="sxs-lookup"><span data-stu-id="1e7d3-121">Make sure tooimport toohello `CurrentUser\My` certificate store, otherwise attaching toohello debugger in Visual Studio will fail.</span></span>

## <a name="enabling-remote-debugging-for-virtual-machines"></a><span data-ttu-id="1e7d3-122">Включение удаленной отладки для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="1e7d3-122">Enabling remote debugging for virtual machines</span></span>
1. <span data-ttu-id="1e7d3-123">Создайте виртуальную машину Azure.</span><span class="sxs-lookup"><span data-stu-id="1e7d3-123">Create an Azure virtual machine.</span></span> <span data-ttu-id="1e7d3-124">См. статью [Создание первой виртуальной машины Windows на портале Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) или [Создание виртуальных машин Windows и управление ими в Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1e7d3-124">See [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [Create and Manage Azure Virtual Machines in Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
2. <span data-ttu-id="1e7d3-125">На hello [странице классического портала Azure](http://go.microsoft.com/fwlink/p/?LinkID=269851), просмотреть hello виртуальной машины мониторинга toosee hello виртуальной машины **ОТПЕЧАТОК сертификата RDP**.</span><span class="sxs-lookup"><span data-stu-id="1e7d3-125">On hello [Azure classic portal page](http://go.microsoft.com/fwlink/p/?LinkID=269851), view hello virtual machine's dashboard toosee hello virtual machine’s **RDP CERTIFICATE THUMBPRINT**.</span></span> <span data-ttu-id="1e7d3-126">Это значение используется для hello `ServerThumbprint` значение в конфигурации расширения hello.</span><span class="sxs-lookup"><span data-stu-id="1e7d3-126">This value is used for hello `ServerThumbprint` value in hello extension configuration.</span></span>
3. <span data-ttu-id="1e7d3-127">Создайте сертификат клиента, как описано в [Общие сведения о сертификатах для облачных служб Azure](cloud-services-certs-create.md) (оставьте hello .pfx и отпечаток сертификата протокола удаленного рабочего СТОЛА).</span><span class="sxs-lookup"><span data-stu-id="1e7d3-127">Create a client certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md) (keep hello .pfx and RDP certificate thumbprint).</span></span>
4. <span data-ttu-id="1e7d3-128">Установка Azure Powershell (версии 0.7.4 или более поздней версии), перечисленные в [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1e7d3-128">Install Azure Powershell (version 0.7.4 or later) as outlined in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
5. <span data-ttu-id="1e7d3-129">Запустите следующий скрипт tooenable hello RemoteDebug расширения hello.</span><span class="sxs-lookup"><span data-stu-id="1e7d3-129">Run hello following script tooenable hello RemoteDebug extension.</span></span> <span data-ttu-id="1e7d3-130">Замените пути hello и личные данные собственный, такие как имя службы, имя подписки и отпечаток.</span><span class="sxs-lookup"><span data-stu-id="1e7d3-130">Replace hello paths and personal data with your own, such as your subscription name, service name, and thumbprint.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1e7d3-131">Этот сценарий настроен для Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="1e7d3-131">This script is configured for Visual Studio 2015.</span></span> <span data-ttu-id="1e7d3-132">Если вы используете Visual Studio 2013 или Visual Studio 2017 г., измените hello `$referenceName` и `$extensionName` следующие назначения слишком`RemoteDebugVS2013` или `RemoteDebugVS2017`.</span><span class="sxs-lookup"><span data-stu-id="1e7d3-132">If you’re using Visual Studio 2013 or Visual Studio 2017, modify hello `$referenceName` and `$extensionName` assignments below too`RemoteDebugVS2013` or `RemoteDebugVS2017`.</span></span>

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

6. <span data-ttu-id="1e7d3-133">Импорт hello сертификата (.pfx) toohello компьютере с Visual Studio с пакетом SDK Azure для установки .NET.</span><span class="sxs-lookup"><span data-stu-id="1e7d3-133">Import hello certificate (.pfx) toohello machine that has Visual Studio with Azure SDK for .NET installed.</span></span>

