---
title: "aaaHow tooSet компьютеров для разработки служб мультимедиа с помощью .NET"
description: "Дополнительные сведения о предварительных требованиях hello для служб мультимедиа с помощью hello пакета SDK служб мультимедиа для .NET. Также узнаете, как toocreate приложения Visual Studio."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: juliako
ms.openlocfilehash: a5a2af3211d8156fd7dea99831fb769df4130d41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-development-with-net"></a><span data-ttu-id="3de65-104">Разработка служб мультимедиа с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="3de65-104">Media Services development with .NET</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="3de65-105">В этом разделе обсуждается, как toostart разработки Media Services приложений с помощью .NET.</span><span class="sxs-lookup"><span data-stu-id="3de65-105">This topic discusses how toostart developing Media Services applications using .NET.</span></span>

<span data-ttu-id="3de65-106">Hello **Azure Media Services .NET SDK** библиотека позволяет tooprogram к службам мультимедиа с помощью .NET.</span><span class="sxs-lookup"><span data-stu-id="3de65-106">hello **Azure Media Services .NET SDK** library enables you tooprogram against Media Services using .NET.</span></span> <span data-ttu-id="3de65-107">Он даже проще toodevelop в .NET Framework, hello toomake **расширения SDK .NET служб мультимедиа Azure** предоставляется библиотеки.</span><span class="sxs-lookup"><span data-stu-id="3de65-107">toomake it even easier toodevelop with .NET, hello **Azure Media Services .NET SDK Extensions** library is provided.</span></span> <span data-ttu-id="3de65-108">Эта библиотека содержит набор методов расширения и вспомогательные функции, упрощающие код .NET.</span><span class="sxs-lookup"><span data-stu-id="3de65-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span></span> <span data-ttu-id="3de65-109">Обе библиотеки доступны в **NuGet** и на **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="3de65-109">Both libraries are available through **NuGet** and **GitHub**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3de65-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3de65-110">Prerequisites</span></span>
* <span data-ttu-id="3de65-111">Учетная запись служб мультимедиа в новой или существующей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="3de65-111">A Media Services account in a new or existing Azure subscription.</span></span> <span data-ttu-id="3de65-112">В разделе hello [как tooCreate учетную запись служб мультимедиа](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="3de65-112">See hello topic [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="3de65-113">Операционные системы: Windows 10, Windows 7, Windows 2008 R2 или Windows 8.</span><span class="sxs-lookup"><span data-stu-id="3de65-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="3de65-114">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="3de65-114">.NET Framework 4.5.</span></span>
* <span data-ttu-id="3de65-115">приведенному.</span><span class="sxs-lookup"><span data-stu-id="3de65-115">Visual Studio.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="3de65-116">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3de65-116">Create and configure a Visual Studio project</span></span>
<span data-ttu-id="3de65-117">В этом разделе показано, как toocreate проекта в Visual Studio и настроить его для разработки служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="3de65-117">This section shows you how toocreate a project in Visual Studio and set it up for Media Services development.</span></span>  <span data-ttu-id="3de65-118">В этом случае hello проект представляет собой консольное приложение C# Windows, но hello показанные здесь шаги установки применения tooother типов проектов, которые можно создать для приложений служб мультимедиа (например, приложение Windows Forms или веб-приложения ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="3de65-118">In this case, hello project is a C# Windows console application, but hello same setup steps shown here apply tooother types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span></span>

<span data-ttu-id="3de65-119">В этом разделе показано, как toouse **NuGet** tooadd Media Services .NET SDK расширений и другие зависимые библиотеки.</span><span class="sxs-lookup"><span data-stu-id="3de65-119">This section shows how toouse **NuGet** tooadd Media Services .NET SDK extensions and other dependent libraries.</span></span>

<span data-ttu-id="3de65-120">Кроме того, можно получить последние Media Services .NET SDK bits hello GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) или [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), построить решение hello и добавить hello ссылки toohello клиентский проект.</span><span class="sxs-lookup"><span data-stu-id="3de65-120">Alternatively, you can get hello latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build hello solution, and add hello references toohello client project.</span></span> <span data-ttu-id="3de65-121">Все необходимые зависимости hello загружаются и извлекаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="3de65-121">All hello necessary dependencies get downloaded and extracted automatically.</span></span>

1. <span data-ttu-id="3de65-122">Создайте в Visual Studio консольное приложение C#.</span><span class="sxs-lookup"><span data-stu-id="3de65-122">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="3de65-123">Введите hello **имя**, **расположение**, и **имя решения**, а затем нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="3de65-123">Enter hello **Name**, **Location**, and **Solution name**, and then click OK.</span></span>
2. <span data-ttu-id="3de65-124">Выполните сборку решения hello.</span><span class="sxs-lookup"><span data-stu-id="3de65-124">Build hello solution.</span></span>
3. <span data-ttu-id="3de65-125">Используйте **NuGet** tooinstall и добавьте **расширения SDK .NET служб мультимедиа Azure** (**windowsazure.mediaservices.extensions**).</span><span class="sxs-lookup"><span data-stu-id="3de65-125">Use **NuGet** tooinstall and add **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span></span> <span data-ttu-id="3de65-126">При установке этого пакета также устанавливается **пакет SDK служб мультимедиа для .NET** и добавляются все остальные необходимые зависимости.</span><span class="sxs-lookup"><span data-stu-id="3de65-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>
   
    <span data-ttu-id="3de65-127">Убедитесь, что hello последняя версия NuGet установлен.</span><span class="sxs-lookup"><span data-stu-id="3de65-127">Ensure that you have hello newest version of NuGet installed.</span></span> <span data-ttu-id="3de65-128">Дополнительную информацию и инструкции по установке см. на сайте [NuGet](http://nuget.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="3de65-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span></span>
4. <span data-ttu-id="3de65-129">В обозревателе решений щелкните правой кнопкой мыши имя проекта, hello hello и выберите Управление пакетами NuGet.</span><span class="sxs-lookup"><span data-stu-id="3de65-129">In Solution Explorer, right-click hello name of hello project and choose Manage NuGet packages.</span></span>
   
    <span data-ttu-id="3de65-130">Откроется диалоговое окно Управление пакетами NuGet Hello.</span><span class="sxs-lookup"><span data-stu-id="3de65-130">hello Manage NuGet Packages dialog box appears.</span></span>
5. <span data-ttu-id="3de65-131">В коллекции hello сети, поиск расширения служб Azure, выберите расширения SDK .NET служб мультимедиа Azure и нажмите кнопку "установить" hello ".</span><span class="sxs-lookup"><span data-stu-id="3de65-131">In hello Online gallery, search for Azure MediaServices Extensions, choose Azure Media Services .NET SDK Extensions, and then click hello Install button.</span></span>
   
    <span data-ttu-id="3de65-132">Hello проект будет изменен, ссылается на toohello расширения SDK .NET служб мультимедиа, Media Services .NET SDK и другие зависимые сборки добавляются.</span><span class="sxs-lookup"><span data-stu-id="3de65-132">hello project is modified and references toohello Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span></span>
6. <span data-ttu-id="3de65-133">toopromote очистки среды разработки, то можно попробовать включить восстановление пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="3de65-133">toopromote a cleaner development environment, consider enabling NuGet Package Restore.</span></span> <span data-ttu-id="3de65-134">Дополнительную информацию см. в статье [Восстановление пакета NuGet](http://docs.nuget.org/consume/package-restore).</span><span class="sxs-lookup"><span data-stu-id="3de65-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span></span>
7. <span data-ttu-id="3de65-135">Добавьте ссылку на слишком**System.Configuration** сборки.</span><span class="sxs-lookup"><span data-stu-id="3de65-135">Add a reference too**System.Configuration** assembly.</span></span> <span data-ttu-id="3de65-136">Эта сборка содержит hello System.Configuration. **ConfigurationManager** класс, являющийся используется tooaccess файлы конфигурации (например, файл App.config).</span><span class="sxs-lookup"><span data-stu-id="3de65-136">This assembly contains hello System.Configuration.**ConfigurationManager** class that is used tooaccess configuration files (for example, App.config).</span></span>
   
    <span data-ttu-id="3de65-137">ссылки на tooadd, с помощью диалогового окна Управление ссылками hello, щелкните правой кнопкой мыши hello имя проекта в обозревателе решений hello.</span><span class="sxs-lookup"><span data-stu-id="3de65-137">tooadd references using hello Manage References dialog, right-click hello project name in hello Solution Explorer.</span></span> <span data-ttu-id="3de65-138">Выберите "Добавить ссылки".</span><span class="sxs-lookup"><span data-stu-id="3de65-138">Then, select Add and References.</span></span>
   
    <span data-ttu-id="3de65-139">Откроется диалоговое окно Управление ссылками Hello.</span><span class="sxs-lookup"><span data-stu-id="3de65-139">hello Manage References dialog appears.</span></span>
8. <span data-ttu-id="3de65-140">В списке сборок платформы .NET framework найти выберите сборку System.Configuration hello и нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="3de65-140">Under .NET framework assemblies, find and select hello System.Configuration assembly and press OK.</span></span>
9. <span data-ttu-id="3de65-141">Откройте файл App.config hello и добавьте *appSettings* файл toohello раздела.</span><span class="sxs-lookup"><span data-stu-id="3de65-141">Open hello App.config file and add an *appSettings* section toohello file.</span></span>     
   
    <span data-ttu-id="3de65-142">Установить значения hello, необходимые tooconnect toohello API служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="3de65-142">Set hello values that are needed tooconnect toohello Media Services API.</span></span> <span data-ttu-id="3de65-143">Дополнительные сведения см. в разделе [hello доступа к API служб мультимедиа Azure с проверкой подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="3de65-143">For more information, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

    <span data-ttu-id="3de65-144">Если вы используете [проверки подлинности пользователя](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) файл конфигурации, скорее всего, будет иметь значение доменом клиента Azure AD и конечной точкой AMS API hello.</span><span class="sxs-lookup"><span data-stu-id="3de65-144">If you are using [user authentication](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) your config file will probably have values for your Azure AD tenant domain and hello AMS REST API endpoint.</span></span>
    
    >[!Important]
    ><span data-ttu-id="3de65-145">Большинство примеров кода в документации по службам мультимедиа Azure hello набора, используйте тип пользователя (интерактивные) toohello tooconnect проверки подлинности AMS API.</span><span class="sxs-lookup"><span data-stu-id="3de65-145">Most code samples in hello Azure Media Services documentation set, use a user (interactive) type of authentication tooconnect toohello AMS API.</span></span> <span data-ttu-id="3de65-146">Такой метод аутентификации неплохо работает для приложений управления или мониторинга на устройствах: мобильные приложения, приложения Windows и консольные приложения.</span><span class="sxs-lookup"><span data-stu-id="3de65-146">This authentication method will work well for management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="3de65-147">Но он совершенно не пригоден для аутентификации приложений, работающих на серверах, в веб-службах или API-интерфейсах.</span><span class="sxs-lookup"><span data-stu-id="3de65-147">This authentication method is not suitable for server, web services, APIs type of applications.</span></span>  <span data-ttu-id="3de65-148">Дополнительные сведения см. в разделе [hello доступа AMS API с проверкой подлинности Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="3de65-148">For more information, see [Access hello AMS API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. <span data-ttu-id="3de65-149">Перезаписать существующую hello **с помощью** операторы в начале hello из файла Program.cs hello hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="3de65-149">Overwrite hello existing **using** statements at hello beginning of hello Program.cs file with hello following code.</span></span>
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

<span data-ttu-id="3de65-150">На этом этапе вы являются готов toostart разработки приложений служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="3de65-150">At this point, you are ready toostart developing a Media Services application.</span></span>    

## <a name="example"></a><span data-ttu-id="3de65-151">Пример</span><span class="sxs-lookup"><span data-stu-id="3de65-151">Example</span></span>

<span data-ttu-id="3de65-152">Ниже приведен небольшой пример, который подключается к toohello AMS API и перечислены все доступные процессоры носителя.</span><span class="sxs-lookup"><span data-stu-id="3de65-152">Here is a small example that connects toohello AMS API and lists all available Media Processors.</span></span>
    
    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
    
        private static CloudMediaContext _context = null;
        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
    
            // List all available Media Processors
            foreach (var mp in _context.MediaProcessors)
            {
                Console.WriteLine(mp.Name);
            }
    
        }

##<a name="next-steps"></a><span data-ttu-id="3de65-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3de65-153">Next steps</span></span>

<span data-ttu-id="3de65-154">Теперь [подключении toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md) и запустить [разработке](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3de65-154">Now [you can connect toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md) and start [developing](media-services-dotnet-get-started.md).</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="3de65-155">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="3de65-155">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="3de65-156">Отзывы</span><span class="sxs-lookup"><span data-stu-id="3de65-156">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

