---
title: "Настройка среды разработки для микрослужб Azure | Документация Майкрософт"
description: "Установите среду выполнения, пакет SDK и инструменты и создайте локальный кластер разработки. После этого вы сможете создавать приложения."
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
ms.openlocfilehash: f0c6957217c21bdfd76498944e248fc808f2d271
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="prepare-your-development-environment"></a><span data-ttu-id="6133d-104">Подготовка среды разработки</span><span class="sxs-lookup"><span data-stu-id="6133d-104">Prepare your development environment</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6133d-105">Windows</span><span class="sxs-lookup"><span data-stu-id="6133d-105">Windows</span></span>](service-fabric-get-started.md) 
> * [<span data-ttu-id="6133d-106">Linux</span><span class="sxs-lookup"><span data-stu-id="6133d-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="6133d-107">OSX</span><span class="sxs-lookup"><span data-stu-id="6133d-107">OSX</span></span>](service-fabric-get-started-mac.md)
> 
> 

 <span data-ttu-id="6133d-108">Чтобы создавать и запускать [приложения Service Fabric][1] на компьютере для разработки, установите среду выполнения, пакет SDK и инструменты.</span><span class="sxs-lookup"><span data-stu-id="6133d-108">To build and run [Azure Service Fabric applications][1] on your development machine, install the runtime, SDK, and tools.</span></span> <span data-ttu-id="6133d-109">Вам также нужно включить выполнение сценариев Windows PowerShell, включенных в пакет SDK.</span><span class="sxs-lookup"><span data-stu-id="6133d-109">You also need to enable execution of the Windows PowerShell scripts included in the SDK.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6133d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6133d-110">Prerequisites</span></span>
### <a name="supported-operating-system-versions"></a><span data-ttu-id="6133d-111">Поддерживаемые версии операционных систем</span><span class="sxs-lookup"><span data-stu-id="6133d-111">Supported operating system versions</span></span>
<span data-ttu-id="6133d-112">Для разработки поддерживаются следующие операционные системы:</span><span class="sxs-lookup"><span data-stu-id="6133d-112">The following operating system versions are supported for development:</span></span>

* <span data-ttu-id="6133d-113">Windows 7</span><span class="sxs-lookup"><span data-stu-id="6133d-113">Windows 7</span></span>
* <span data-ttu-id="6133d-114">Windows 8 и Windows 8.1;</span><span class="sxs-lookup"><span data-stu-id="6133d-114">Windows 8/Windows 8.1</span></span>
* <span data-ttu-id="6133d-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="6133d-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="6133d-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="6133d-116">Windows Server 2016</span></span>
* <span data-ttu-id="6133d-117">Windows 10</span><span class="sxs-lookup"><span data-stu-id="6133d-117">Windows 10</span></span>

> [!NOTE]
> <span data-ttu-id="6133d-118">Windows 7 по умолчанию поставляется с Windows PowerShell версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="6133d-118">Windows 7 only includes Windows PowerShell 2.0 by default.</span></span> <span data-ttu-id="6133d-119">Для выполнения командлетов PowerShell для Service Fabric требуется PowerShell начиная с версии 3.0.</span><span class="sxs-lookup"><span data-stu-id="6133d-119">Service Fabric PowerShell cmdlets requires PowerShell 3.0 or higher.</span></span> <span data-ttu-id="6133d-120">В центре загрузки Майкрософт можно [скачать Windows PowerShell 5.0][powershell5-download].</span><span class="sxs-lookup"><span data-stu-id="6133d-120">You can [download Windows PowerShell 5.0][powershell5-download] from the Microsoft Download Center.</span></span>
> 
> 

## <a name="install-the-sdk-and-tools"></a><span data-ttu-id="6133d-121">Установка пакета SDK и инструментов</span><span class="sxs-lookup"><span data-stu-id="6133d-121">Install the SDK and tools</span></span>
### <a name="to-use-visual-studio-2017"></a><span data-ttu-id="6133d-122">Для использования Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="6133d-122">To use Visual Studio 2017</span></span>
<span data-ttu-id="6133d-123">Средства Service Fabric являются частью рабочей нагрузки по разработке и управлению в Azure в Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="6133d-123">Service Fabric Tools are part of the Azure Development and Management workload in Visual Studio 2017.</span></span> <span data-ttu-id="6133d-124">Эту рабочую нагрузку необходимо включить при установке Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6133d-124">Enable this workload as part of your Visual Studio installation.</span></span>
<span data-ttu-id="6133d-125">Кроме того, необходимо установить пакет SDK Microsoft Azure Service Fabric, используя установщик веб-платформы.</span><span class="sxs-lookup"><span data-stu-id="6133d-125">In addition, you need to install the Microsoft Azure Service Fabric SDK, using Web Platform Installer.</span></span>

* <span data-ttu-id="6133d-126">[Установка пакета SDK Microsoft Azure Service Fabric][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="6133d-126">[Install the Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

### <a name="to-use-visual-studio-2015-requires-visual-studio-2015-update-2-or-later"></a><span data-ttu-id="6133d-127">Для использования Visual Studio 2015 (требуется Visual Studio 2015 с обновлением 2 или более поздней версии)</span><span class="sxs-lookup"><span data-stu-id="6133d-127">To use Visual Studio 2015 (requires Visual Studio 2015 Update 2 or later)</span></span>
<span data-ttu-id="6133d-128">Для Visual Studio 2015 средства Service Fabric устанавливаются вместе с пакетом SDK с помощью установщика веб-платформы:</span><span class="sxs-lookup"><span data-stu-id="6133d-128">For Visual Studio 2015, Service Fabric tools are installed together with the SDK, using the Web Platform Installer:</span></span>

* <span data-ttu-id="6133d-129">[Установка пакета SDK и средств Microsoft Azure Service Fabric][full-bundle-vs2015]</span><span class="sxs-lookup"><span data-stu-id="6133d-129">[Install the Microsoft Azure Service Fabric SDK and Tools][full-bundle-vs2015]</span></span>

### <a name="sdk-installation-only"></a><span data-ttu-id="6133d-130">Только установка пакета SDK</span><span class="sxs-lookup"><span data-stu-id="6133d-130">SDK installation only</span></span>
<span data-ttu-id="6133d-131">Если вам требуется только пакет SDK, можно установить этот пакет:</span><span class="sxs-lookup"><span data-stu-id="6133d-131">If you only need the SDK, you can install this package:</span></span>
* <span data-ttu-id="6133d-132">[Установка пакета SDK Microsoft Azure Service Fabric][core-sdk]</span><span class="sxs-lookup"><span data-stu-id="6133d-132">[Install the Microsoft Azure Service Fabric SDK][core-sdk]</span></span>

<span data-ttu-id="6133d-133">Текущие версии:</span><span class="sxs-lookup"><span data-stu-id="6133d-133">The current versions are:</span></span>
* <span data-ttu-id="6133d-134">Пакет SDK для Service Fabric 2.7.198</span><span class="sxs-lookup"><span data-stu-id="6133d-134">Service Fabric SDK 2.7.198</span></span>
* <span data-ttu-id="6133d-135">Среда выполнения Service Fabric 5.7.198</span><span class="sxs-lookup"><span data-stu-id="6133d-135">Service Fabric runtime 5.7.198</span></span>
* <span data-ttu-id="6133d-136">Средства Service Fabric для Visual Studio 2015 1.7.50721</span><span class="sxs-lookup"><span data-stu-id="6133d-136">Service Fabric Tools for Visual Studio 2015 1.7.50721</span></span>
* <span data-ttu-id="6133d-137">Visual Studio 2017 с обновлением 2 включает средства Service Fabric для Visual Studio 1.6.20170504</span><span class="sxs-lookup"><span data-stu-id="6133d-137">Visual Studio 2017 Update 2 includes Service Fabric Tools for Visual Studio 1.6.20170504</span></span>
* <span data-ttu-id="6133d-138">Visual Studio 2017 с обновлением 3 (предварительная версия 7) (15.3.0, предварительная версия 7.0) включает средства Service Fabric для Visual Studio 1.7.20170721</span><span class="sxs-lookup"><span data-stu-id="6133d-138">Visual Studio 2017 Update 3 Preview 7 (15.3.0 Preview 7.0) includes Service Fabric Tools for Visual Studio 1.7.20170721</span></span>

<span data-ttu-id="6133d-139">Список поддерживаемых версий см. в статье [Azure Service Fabric support options](service-fabric-support.md) (Варианты поддержки Azure Service Fabric).</span><span class="sxs-lookup"><span data-stu-id="6133d-139">For a list of supported versions, see [Service Fabric support](service-fabric-support.md)</span></span>

## <a name="enable-powershell-script-execution"></a><span data-ttu-id="6133d-140">Включение сценариев PowerShell</span><span class="sxs-lookup"><span data-stu-id="6133d-140">Enable PowerShell script execution</span></span>
<span data-ttu-id="6133d-141">Для создания локального кластера разработки и развертывания приложений из Visual Studio в Service Fabric используются сценарии Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6133d-141">Service Fabric uses Windows PowerShell scripts for creating a local development cluster and for deploying applications from Visual Studio.</span></span> <span data-ttu-id="6133d-142">По умолчанию ОС Windows блокирует выполнение этих сценариев.</span><span class="sxs-lookup"><span data-stu-id="6133d-142">By default, Windows blocks these scripts from running.</span></span> <span data-ttu-id="6133d-143">Чтобы включить их, необходимо изменить политику выполнения PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6133d-143">To enable them, you must modify your PowerShell execution policy.</span></span> <span data-ttu-id="6133d-144">Для этого запустите PowerShell с правами администратора и введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6133d-144">Open PowerShell as an administrator and enter the following command:</span></span>

```powershell
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
```

## <a name="next-steps"></a><span data-ttu-id="6133d-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6133d-145">Next steps</span></span>
<span data-ttu-id="6133d-146">Среда разработки настроена, и вы готовы к созданию и запуску собственных приложений.</span><span class="sxs-lookup"><span data-stu-id="6133d-146">Now that you've finished setting up your development environment, start building and running apps.</span></span>

* [<span data-ttu-id="6133d-147">Создание первого приложения Service Fabric в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6133d-147">Create your first Service Fabric application in Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
* [<span data-ttu-id="6133d-148">Информация о развертывании приложений в локальном кластере и управлении ими</span><span class="sxs-lookup"><span data-stu-id="6133d-148">Learn how to deploy and manage applications on your local cluster</span></span>](service-fabric-get-started-with-a-local-cluster.md)
* [<span data-ttu-id="6133d-149">Информация о моделях программирования: Reliable Services и Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="6133d-149">Learn about the programming models: Reliable Services and Reliable Actors</span></span>](service-fabric-choose-framework.md)
* [<span data-ttu-id="6133d-150">Ознакомление с примерами кода Service Fabric на GitHub</span><span class="sxs-lookup"><span data-stu-id="6133d-150">Check out the Service Fabric code samples on GitHub</span></span>](https://aka.ms/servicefabricsamples)
* [<span data-ttu-id="6133d-151">Визуализация кластера с помощью обозревателя Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6133d-151">Visualize your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)
* [<span data-ttu-id="6133d-152">Используйте схему обучения Service Fabric, чтобы получить общие сведения о платформе</span><span class="sxs-lookup"><span data-stu-id="6133d-152">Follow the Service Fabric learning path to get a broad introduction to the platform</span></span>](https://azure.microsoft.com/documentation/learning-paths/service-fabric/)
* <span data-ttu-id="6133d-153">[Сведения о вариантах поддержки Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="6133d-153">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

<span data-ttu-id="6133d-154">[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Страница кампании Service Fabric"</span><span class="sxs-lookup"><span data-stu-id="6133d-154">[1]: http://azure.microsoft.com/en-us/campaigns/service-fabric/ "Service Fabric campaign page"</span></span>
<span data-ttu-id="6133d-155">[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"</span><span class="sxs-lookup"><span data-stu-id="6133d-155">[2]: http://go.microsoft.com/fwlink/?LinkId=517106 "VS RC"</span></span>
<span data-ttu-id="6133d-156">[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "Ссылка на WebPI VS 2015"</span><span class="sxs-lookup"><span data-stu-id="6133d-156">[full-bundle-vs2015]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015 "VS 2015 WebPI link"</span></span>
<span data-ttu-id="6133d-157">[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Ссылка на WebPI Dev15"</span><span class="sxs-lookup"><span data-stu-id="6133d-157">[full-bundle-dev15]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-Dev15 "Dev15 WebPI link"</span></span>
<span data-ttu-id="6133d-158">[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Ссылка на WebPI Core SDK"</span><span class="sxs-lookup"><span data-stu-id="6133d-158">[core-sdk]:http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK "Core SDK WebPI link"</span></span>
[powershell5-download]:https://www.microsoft.com/en-us/download/details.aspx?id=50395
