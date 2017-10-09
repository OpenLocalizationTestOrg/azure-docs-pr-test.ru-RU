---
title: "aaaSet среду разработки для Azure микрослужбами | Документы Microsoft"
description: "Установка среды выполнения hello, пакета SDK и средств и создайте кластер локальной разработки. После завершения этой установки, будет готов toobuild приложений."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b94e2d2e-435c-474a-ae34-4adecd0e6f8f
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/10/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: 9b0442778999d4c3d2b99adb98f6596dcbdc36d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment"></a><span data-ttu-id="c7e70-104">Подготовка среды разработки</span><span class="sxs-lookup"><span data-stu-id="c7e70-104">Prepare your development environment</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c7e70-105">Windows</span><span class="sxs-lookup"><span data-stu-id="c7e70-105">Windows</span></span>](service-fabric-get-started.md) 
> * [<span data-ttu-id="c7e70-106">Linux</span><span class="sxs-lookup"><span data-stu-id="c7e70-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="c7e70-107">OSX</span><span class="sxs-lookup"><span data-stu-id="c7e70-107">OSX</span></span>](service-fabric-get-started-mac.md)
> 
> 

 <span data-ttu-id="c7e70-108">toobuild и запустите [приложения Azure Service Fabric] [ 1] на компьютере разработки установите hello среды выполнения, пакет SDK и средства.</span><span class="sxs-lookup"><span data-stu-id="c7e70-108">toobuild and run [Azure Service Fabric applications][1] on your development machine, install hello runtime, SDK, and tools.</span></span> <span data-ttu-id="c7e70-109">Необходимо также tooenable выполнение сценариев Windows PowerShell hello, включенных в пакет SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="c7e70-109">You also need tooenable execution of hello Windows PowerShell scripts included in hello SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7e70-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c7e70-110">Prerequisites</span></span>
### <a name="supported-operating-system-versions"></a><span data-ttu-id="c7e70-111">Поддерживаемые версии операционных систем</span><span class="sxs-lookup"><span data-stu-id="c7e70-111">Supported operating system versions</span></span>
<span data-ttu-id="c7e70-112">для разработки поддерживаются Hello следующих версий операционной системы:</span><span class="sxs-lookup"><span data-stu-id="c7e70-112">hello following operating system versions are supported for development:</span></span>

* <span data-ttu-id="c7e70-113">Windows 7</span><span class="sxs-lookup"><span data-stu-id="c7e70-113">Windows 7</span></span>
* <span data-ttu-id="c7e70-114">Windows 8 и Windows 8.1;</span><span class="sxs-lookup"><span data-stu-id="c7e70-114">Windows 8/Windows 8.1</span></span>
* <span data-ttu-id="c7e70-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="c7e70-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="c7e70-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="c7e70-116">Windows Server 2016</span></span>
* <span data-ttu-id="c7e70-117">Windows 10</span><span class="sxs-lookup"><span data-stu-id="c7e70-117">Windows 10</span></span>

> [!NOTE]
> <span data-ttu-id="c7e70-118">Windows 7 по умолчанию поставляется с Windows PowerShell версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="c7e70-118">Windows 7 only includes Windows PowerShell 2.0 by default.</span></span> <span data-ttu-id="c7e70-119">Для выполнения командлетов PowerShell для Service Fabric требуется PowerShell начиная с версии 3.0.</span><span class="sxs-lookup"><span data-stu-id="c7e70-119">Service Fabric PowerShell cmdlets requires PowerShell 3.0 or higher.</span></span> <span data-ttu-id="c7e70-120">Вы можете [загрузить Windows PowerShell 5.0] [ powershell5-download] из центра загрузки Майкрософт hello.</span><span class="sxs-lookup"><span data-stu-id="c7e70-120">You can [download Windows PowerShell 5.0][powershell5-download] from hello Microsoft Download Center.</span></span>
> 
> 

## <a name="install-hello-sdk-and-tools"></a><span data-ttu-id="c7e70-121">Установка пакета SDK для hello и средств</span><span class="sxs-lookup"><span data-stu-id="c7e70-121">Install hello SDK and tools</span></span>
### <a name="toouse-visual-studio-2017"></a><span data-ttu-id="c7e70-122">toouse Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="c7e70-122">toouse Visual Studio 2017</span></span>
<span data-ttu-id="c7e70-123">Средства Service Fabric являются частью рабочей нагрузки Azure разработки и управления hello в Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="c7e70-123">Service Fabric Tools are part of hello Azure Development and Management workload in Visual Studio 2017.</span></span> <span data-ttu-id="c7e70-124">Эту рабочую нагрузку необходимо включить при установке Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c7e70-124">Enable this workload as part of your Visual Studio installation.</span></span>
<span data-ttu-id="c7e70-125">Кроме того необходимо tooinstall hello Microsoft Azure Service Fabric SDK, с помощью установщика веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="c7e70-125">In addition, you need tooinstall hello Microsoft Azure Service Fabric SDK, using Web Platform Installer.</span></span>

* <span data-ttu-id="c7e70-126">[Установить пакет Microsoft Azure Service Fabric SDK hello][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="c7e70-126">[Install hello Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

### <a name="toouse-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a><span data-ttu-id="c7e70-127">toouse Visual Studio 2015 (требуется Visual Studio 2015 с обновлением 2 или более поздней версии)</span><span class="sxs-lookup"><span data-stu-id="c7e70-127">toouse Visual Studio 2015 (requires Visual Studio 2015 Update 2 or later)</span></span>
<span data-ttu-id="c7e70-128">Для Visual Studio 2015 средств Service Fabric устанавливаются вместе с hello SDK, с помощью установщика веб-платформы hello:</span><span class="sxs-lookup"><span data-stu-id="c7e70-128">For Visual Studio 2015, Service Fabric tools are installed together with hello SDK, using hello Web Platform Installer:</span></span>

* <span data-ttu-id="c7e70-129">[Установить пакет Microsoft Azure Service Fabric SDK hello и средства][full-bundle-vs2015]</span><span class="sxs-lookup"><span data-stu-id="c7e70-129">[Install hello Microsoft Azure Service Fabric SDK and Tools][full-bundle-vs2015]</span></span>

### <a name="sdk-installation-only"></a><span data-ttu-id="c7e70-130">Только установка пакета SDK</span><span class="sxs-lookup"><span data-stu-id="c7e70-130">SDK installation only</span></span>
<span data-ttu-id="c7e70-131">Если требуется только hello SDK, можно установить этот пакет:</span><span class="sxs-lookup"><span data-stu-id="c7e70-131">If you only need hello SDK, you can install this package:</span></span>
* <span data-ttu-id="c7e70-132">[Установить пакет Microsoft Azure Service Fabric SDK hello][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="c7e70-132">[Install hello Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

<span data-ttu-id="c7e70-133">Ниже перечислены текущие версии Hello</span><span class="sxs-lookup"><span data-stu-id="c7e70-133">hello current versions are:</span></span>
* <span data-ttu-id="c7e70-134">Пакет SDK для Service Fabric 2.7.198</span><span class="sxs-lookup"><span data-stu-id="c7e70-134">Service Fabric SDK 2.7.198</span></span>
* <span data-ttu-id="c7e70-135">Среда выполнения Service Fabric 5.7.198</span><span class="sxs-lookup"><span data-stu-id="c7e70-135">Service Fabric runtime 5.7.198</span></span>
* <span data-ttu-id="c7e70-136">Средства Service Fabric для Visual Studio 2015 1.7.50721</span><span class="sxs-lookup"><span data-stu-id="c7e70-136">Service Fabric Tools for Visual Studio 2015 1.7.50721</span></span>
* <span data-ttu-id="c7e70-137">Visual Studio 2017 с обновлением 2 включает средства Service Fabric для Visual Studio 1.6.20170504</span><span class="sxs-lookup"><span data-stu-id="c7e70-137">Visual Studio 2017 Update 2 includes Service Fabric Tools for Visual Studio 1.6.20170504</span></span>
* <span data-ttu-id="c7e70-138">Visual Studio 2017 с обновлением 3 (предварительная версия 7) (15.3.0, предварительная версия 7.0) включает средства Service Fabric для Visual Studio 1.7.20170721</span><span class="sxs-lookup"><span data-stu-id="c7e70-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) includes Service Fabric Tools for Visual Studio 1.7.20170721</span></span>

<span data-ttu-id="c7e70-139">Список поддерживаемых версий см. в статье [Azure Service Fabric support options](service-fabric-support.md) (Варианты поддержки Azure Service Fabric).</span><span class="sxs-lookup"><span data-stu-id="c7e70-139">For a list of supported versions, see [Service Fabric support](service-fabric-support.md)</span></span>

## <a name="enable-powershell-script-execution"></a><span data-ttu-id="c7e70-140">Включение сценариев PowerShell</span><span class="sxs-lookup"><span data-stu-id="c7e70-140">Enable PowerShell script execution</span></span>
<span data-ttu-id="c7e70-141">Для создания локального кластера разработки и развертывания приложений из Visual Studio в Service Fabric используются сценарии Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7e70-141">Service Fabric uses Windows PowerShell scripts for creating a local development cluster and for deploying applications from Visual Studio.</span></span> <span data-ttu-id="c7e70-142">По умолчанию ОС Windows блокирует выполнение этих сценариев.</span><span class="sxs-lookup"><span data-stu-id="c7e70-142">By default, Windows blocks these scripts from running.</span></span> <span data-ttu-id="c7e70-143">tooenable их, необходимо изменить политику выполнения PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c7e70-143">tooenable them, you must modify your PowerShell execution policy.</span></span> <span data-ttu-id="c7e70-144">Откройте PowerShell с правами администратора и введите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c7e70-144">Open PowerShell as an administrator and enter hello following command:</span></span>

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a><span data-ttu-id="c7e70-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c7e70-145">Next steps</span></span>
<span data-ttu-id="c7e70-146">Среда разработки настроена, и вы готовы к созданию и запуску собственных приложений.</span><span class="sxs-lookup"><span data-stu-id="c7e70-146">Now that you've finished setting up your development environment, start building and running apps.</span></span>

* [<span data-ttu-id="c7e70-147">Создание первого приложения Service Fabric в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c7e70-147">Create your first Service Fabric application in Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
* [<span data-ttu-id="c7e70-148">Узнайте, как toodeploy приложений в локальном кластере и управление ими</span><span class="sxs-lookup"><span data-stu-id="c7e70-148">Learn how toodeploy and manage applications on your local cluster</span></span>](service-fabric-get-started-with-a-local-cluster.md)
* [<span data-ttu-id="c7e70-149">Дополнительные сведения о модели программирования hello: надежные службы и службы Reliable Actor</span><span class="sxs-lookup"><span data-stu-id="c7e70-149">Learn about hello programming models: Reliable Services and Reliable Actors</span></span>](service-fabric-choose-framework.md)
* [<span data-ttu-id="c7e70-150">Извлечение hello Service Fabric примеры кода на GitHub</span><span class="sxs-lookup"><span data-stu-id="c7e70-150">Check out hello Service Fabric code samples on GitHub</span></span>](https://aka.ms/servicefabricsamples)
* [<span data-ttu-id="c7e70-151">Визуализация кластера с помощью обозревателя Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c7e70-151">Visualize your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)
* [<span data-ttu-id="c7e70-152">Выполните hello обучения tooget путь платформы toohello начальные сведения о Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c7e70-152">Follow hello Service Fabric learning path tooget a broad introduction toohello platform</span></span>](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* <span data-ttu-id="c7e70-153">[Сведения о вариантах поддержки Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="c7e70-153">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Страница кампании Service Fabric"
[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"
[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "Ссылка на WebPI VS 2015"
[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Ссылка на WebPI Dev15"
[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Ссылка на WebPI Core SDK"
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
