---
title: "aaaAzure ретрансляции WCF гибридного на локальные и облачные приложения (.NET) | Документы Microsoft"
description: "Узнайте, как toocreate .NET на локальная/облачная гибридного приложения с помощью ретрансляции WCF в Azure."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9ed02f7c-ebfb-4f39-9c97-b7dc15bcb4c1
ms.service: service-bus-relay
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: sethm
ms.openlocfilehash: aab8b1dbdc85c4edf7b0ccef0921b69524b2d306
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a><span data-ttu-id="de323-103">Создание локального или облачного гибридного приложения .NET с использованием ретранслятора WCF Azure</span><span class="sxs-lookup"><span data-stu-id="de323-103">.NET on-premises/cloud hybrid application using Azure WCF Relay</span></span>
## <a name="introduction"></a><span data-ttu-id="de323-104">Введение</span><span class="sxs-lookup"><span data-stu-id="de323-104">Introduction</span></span>

<span data-ttu-id="de323-105">В этой статье показано, как toobuild гибридной облачные приложения с Microsoft Azure и Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="de323-105">This article shows how toobuild a hybrid cloud application with Microsoft Azure and Visual Studio.</span></span> <span data-ttu-id="de323-106">Hello учебнике предполагается, что у вас есть нет опыта работы с Azure.</span><span class="sxs-lookup"><span data-stu-id="de323-106">hello tutorial assumes you have no prior experience using Azure.</span></span> <span data-ttu-id="de323-107">Менее чем за 30 минут будет иметь приложение, которое использует несколько ресурсов Azure и работающих в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="de323-107">In less than 30 minutes, you will have an application that uses multiple Azure resources up and running in hello cloud.</span></span>

<span data-ttu-id="de323-108">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="de323-108">You will learn:</span></span>

* <span data-ttu-id="de323-109">Как toocreate или адаптировать существующей веб-службы, для использования с веб-решений.</span><span class="sxs-lookup"><span data-stu-id="de323-109">How toocreate or adapt an existing web service for consumption by a web solution.</span></span>
* <span data-ttu-id="de323-110">Как toouse hello Azure WCF ретрансляции tooshare данных между приложением Azure и веб-служба размещается в другом месте.</span><span class="sxs-lookup"><span data-stu-id="de323-110">How toouse hello Azure WCF Relay service tooshare data between an Azure application and a web service hosted elsewhere.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a><span data-ttu-id="de323-111">Как ретранслятор Azure помогает работать с гибридными решениями</span><span class="sxs-lookup"><span data-stu-id="de323-111">How Azure Relay helps with hybrid solutions</span></span>

<span data-ttu-id="de323-112">Бизнес-решения обычно состоят из сочетание пользовательским кодом, написанным tootackle новый и уникальные бизнес-требований и существующие функциональные возможности, предоставляемые решения и систем, которые уже находятся на месте.</span><span class="sxs-lookup"><span data-stu-id="de323-112">Business solutions are typically composed of a combination of custom code written tootackle new and unique business requirements and existing functionality provided by solutions and systems that are already in place.</span></span>

<span data-ttu-id="de323-113">Архитекторам решений запускаются облачные hello toouse для упрощения обработки требований масштабирования и снизить эксплуатационные затраты.</span><span class="sxs-lookup"><span data-stu-id="de323-113">Solution architects are starting toouse hello cloud for easier handling of scale requirements and lower operational costs.</span></span> <span data-ttu-id="de323-114">При этом можно найти что существующие ресурсы службы, они бы хотели tooleverage строительными блоками для своих решений являются корпоративным брандмауэром hello и из легко охватить для доступа, hello облачного решения.</span><span class="sxs-lookup"><span data-stu-id="de323-114">In doing so, they find that existing service assets they'd like tooleverage as building blocks for their solutions are inside hello corporate firewall and out of easy reach for access by hello cloud solution.</span></span> <span data-ttu-id="de323-115">Многие внутренних служб не строятся или размещенных таким образом, они могут быть легко предоставлены на краю корпоративной сети hello.</span><span class="sxs-lookup"><span data-stu-id="de323-115">Many internal services are not built or hosted in a way that they can be easily exposed at hello corporate network edge.</span></span>

<span data-ttu-id="de323-116">[Azure ретрансляции](https://azure.microsoft.com/services/service-bus/) предназначен для hello вариант использования принятия существующих веб-служб Windows Communication Foundation (WCF) и внесения тех служб toosolutions получить безопасный доступ, которые находятся за пределами корпоративной сети hello без необходимости Инфраструктура корпоративной сети toohello влияние изменений.</span><span class="sxs-lookup"><span data-stu-id="de323-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/) is designed for hello use-case of taking existing Windows Communication Foundation (WCF) web services and making those services securely accessible toosolutions that reside outside hello corporate perimeter without requiring intrusive changes toohello corporate network infrastructure.</span></span> <span data-ttu-id="de323-117">Такие службы ретрансляции по-прежнему размещены внутри существующей средой, но они делегировать прослушивание входящих сеансов и запросов службы toohello ретрансляции, размещенных в облаке.</span><span class="sxs-lookup"><span data-stu-id="de323-117">Such relay services are still hosted inside their existing environment, but they delegate listening for incoming sessions and requests toohello cloud-hosted relay service.</span></span> <span data-ttu-id="de323-118">Ретранслятор Azure также защищает эти службы от несанкционированного доступа, применяя аутентификацию на основе [подписанного URL-адреса](../service-bus-messaging/service-bus-sas.md) (SAS).</span><span class="sxs-lookup"><span data-stu-id="de323-118">Azure Relay also protects those services from unauthorized access by using [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) authentication.</span></span>

## <a name="solution-scenario"></a><span data-ttu-id="de323-119">Сценарий решений</span><span class="sxs-lookup"><span data-stu-id="de323-119">Solution scenario</span></span>
<span data-ttu-id="de323-120">В этом учебнике вы создадите на веб-сайт ASP.NET, позволяющую toosee список продуктов на странице запасов продукции hello.</span><span class="sxs-lookup"><span data-stu-id="de323-120">In this tutorial, you will create an ASP.NET website that enables you toosee a list of products on hello product inventory page.</span></span>

![][0]

<span data-ttu-id="de323-121">Hello учебника предполагается, что иметь сведения о продукте в существующей локальной системе и использует tooreach Azure ретрансляции в этой системе.</span><span class="sxs-lookup"><span data-stu-id="de323-121">hello tutorial assumes that you have product information in an existing on-premises system, and uses Azure Relay tooreach into that system.</span></span> <span data-ttu-id="de323-122">Это имитируется веб-службой, запущенной в простом консольном приложении и поддерживаемой набором продуктов в памяти.</span><span class="sxs-lookup"><span data-stu-id="de323-122">This is simulated by a web service that runs in a simple console application and is backed by an in-memory set of products.</span></span> <span data-ttu-id="de323-123">Необходимо будет toorun это консольное приложение на локальном компьютере и развернуть hello веб-роли в Azure.</span><span class="sxs-lookup"><span data-stu-id="de323-123">You will be able toorun this console application on your own computer and deploy hello web role into Azure.</span></span> <span data-ttu-id="de323-124">Таким образом, вы увидите как веб-роль hello в центре обработки данных Azure hello действительно вызвать на вашем компьютере, несмотря на то, что компьютер почти наверняка будет находиться по крайней мере один брандмауэр и слоя сетевой адрес преобразования Сетевых адресов.</span><span class="sxs-lookup"><span data-stu-id="de323-124">By doing so, you will see how hello web role running in hello Azure datacenter will indeed call into your computer, even though your computer will almost certainly reside behind at least one firewall and a network address translation (NAT) layer.</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="de323-125">Настройка среды разработки hello</span><span class="sxs-lookup"><span data-stu-id="de323-125">Set up hello development environment</span></span>

<span data-ttu-id="de323-126">Прежде чем начать, разработке приложений Azure, загрузите средства hello и настройка среды разработки:</span><span class="sxs-lookup"><span data-stu-id="de323-126">Before you can begin developing Azure applications, download hello tools and set up your development environment:</span></span>

1. <span data-ttu-id="de323-127">Установить hello Azure SDK для .NET из пакета SDK для hello [страницу загрузки](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="de323-127">Install hello Azure SDK for .NET from hello SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="de323-128">В hello **.NET** столбец, выберите версию hello [Visual Studio](http://www.visualstudio.com) вы используете.</span><span class="sxs-lookup"><span data-stu-id="de323-128">In hello **.NET** column, click hello version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="de323-129">Hello шаги в данном руководстве используйте Visual Studio 2015, но они также работают с Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="de323-129">hello steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="de323-130">При запросе toorun или сохранить hello установщика нажмите **запуска**.</span><span class="sxs-lookup"><span data-stu-id="de323-130">When prompted toorun or save hello installer, click **Run**.</span></span>
4. <span data-ttu-id="de323-131">В hello **Web Platform Installer**, нажмите кнопку **установить** и продолжите установку hello.</span><span class="sxs-lookup"><span data-stu-id="de323-131">In hello **Web Platform Installer**, click **Install** and proceed with hello installation.</span></span>
5. <span data-ttu-id="de323-132">После завершения установки hello, будет иметь все необходимые toostart приложение hello toodevelop.</span><span class="sxs-lookup"><span data-stu-id="de323-132">Once hello installation is complete, you will have everything necessary toostart toodevelop hello app.</span></span> <span data-ttu-id="de323-133">Hello SDK содержит средства, позволяющие легко разрабатывать приложения Azure в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="de323-133">hello SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="de323-134">Создание пространства имен</span><span class="sxs-lookup"><span data-stu-id="de323-134">Create a namespace</span></span>

<span data-ttu-id="de323-135">с помощью toobegin Здравствуйте возможности ретрансляции в Azure, необходимо сначала создать пространство имен службы.</span><span class="sxs-lookup"><span data-stu-id="de323-135">toobegin using hello relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="de323-136">Пространство имен предоставляет контейнер для адресации ресурсов Azure в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="de323-136">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="de323-137">Выполните hello [инструкциям](relay-create-namespace-portal.md) toocreate имен ретрансляции.</span><span class="sxs-lookup"><span data-stu-id="de323-137">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="create-an-on-premises-server"></a><span data-ttu-id="de323-138">Создание локального сервера</span><span class="sxs-lookup"><span data-stu-id="de323-138">Create an on-premises server</span></span>

<span data-ttu-id="de323-139">Во-первых, нужно создать (макетную) локальную систему каталогов продукции.</span><span class="sxs-lookup"><span data-stu-id="de323-139">First, you will build a (mock) on-premises product catalog system.</span></span> <span data-ttu-id="de323-140">Он будет достаточно простой; Это можно увидеть, представляющее фактическое локальной системе каталога продукции с рабочей областью полный службы, что мы пытаетесь toointegrate.</span><span class="sxs-lookup"><span data-stu-id="de323-140">It will be fairly simple; you can see this as representing an actual on-premises product catalog system with a complete service surface that we're trying toointegrate.</span></span>

<span data-ttu-id="de323-141">Этот проект представляет собой консольное приложение Visual Studio и использует hello [пакет шины обслуживания Azure NuGet](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello библиотеки служебной шины и параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="de323-141">This project is a Visual Studio console application, and uses hello [Azure Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello Service Bus libraries and configuration settings.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="de323-142">Создание проекта hello</span><span class="sxs-lookup"><span data-stu-id="de323-142">Create hello project</span></span>

1. <span data-ttu-id="de323-143">Запустите Microsoft Visual Studio, используя привилегии администратора.</span><span class="sxs-lookup"><span data-stu-id="de323-143">Using administrator privileges, start Microsoft Visual Studio.</span></span> <span data-ttu-id="de323-144">Таким образом, щелкните правой кнопкой мыши значок программы Visual Studio hello toodo и нажмите кнопку **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="de323-144">toodo so, right-click hello Visual Studio program icon, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="de323-145">В Visual Studio в hello **файл** меню, нажмите кнопку **New**и нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="de323-145">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="de323-146">В разделе **Visual C#** области **Установленные шаблоны** щелкните **Консольное приложение (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="de323-146">From **Installed Templates**, under **Visual C#**, click **Console App (.NET Framework)**.</span></span> <span data-ttu-id="de323-147">В hello **имя** hello введите имя **ProductsServer**:</span><span class="sxs-lookup"><span data-stu-id="de323-147">In hello **Name** box, type hello name **ProductsServer**:</span></span>

   ![][11]
4. <span data-ttu-id="de323-148">Нажмите кнопку **ОК** toocreate hello **ProductsServer** проекта.</span><span class="sxs-lookup"><span data-stu-id="de323-148">Click **OK** toocreate hello **ProductsServer** project.</span></span>
5. <span data-ttu-id="de323-149">Если вы уже установили hello диспетчера пакетов NuGet для Visual Studio, пропустите следующий шаг toohello.</span><span class="sxs-lookup"><span data-stu-id="de323-149">If you have already installed hello NuGet package manager for Visual Studio, skip toohello next step.</span></span> <span data-ttu-id="de323-150">В противном случае посетите сайт [NuGet][NuGet] и щелкните [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) (Установить NuGet).</span><span class="sxs-lookup"><span data-stu-id="de323-150">Otherwise, visit [NuGet][NuGet] and click [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span></span> <span data-ttu-id="de323-151">Выполните диспетчер пакетов NuGet hello tooinstall hello приглашения, а затем повторно запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="de323-151">Follow hello prompts tooinstall hello NuGet package manager, then re-start Visual Studio.</span></span>
6. <span data-ttu-id="de323-152">В обозревателе решений щелкните правой кнопкой мыши hello **ProductsServer** проекта, а затем нажмите кнопку **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="de323-152">In Solution Explorer, right-click hello **ProductsServer** project, then click **Manage NuGet Packages**.</span></span>
7. <span data-ttu-id="de323-153">Нажмите кнопку hello **Обзор** вкладку, а затем поиск `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="de323-153">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="de323-154">Выберите hello **WindowsAzure.ServiceBus** пакета.</span><span class="sxs-lookup"><span data-stu-id="de323-154">Select hello **WindowsAzure.ServiceBus** package.</span></span>
8. <span data-ttu-id="de323-155">Нажмите кнопку **установить**и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="de323-155">Click **Install**, and accept hello terms of use.</span></span>

   ![][13]

   <span data-ttu-id="de323-156">Обратите внимание, что требуемые hello, теперь существуют ссылки на сборки клиента.</span><span class="sxs-lookup"><span data-stu-id="de323-156">Note that hello required client assemblies are now referenced.</span></span>
8. <span data-ttu-id="de323-157">Добавьте новый класс для контракта на свою продукцию.</span><span class="sxs-lookup"><span data-stu-id="de323-157">Add a new class for your product contract.</span></span> <span data-ttu-id="de323-158">В обозревателе решений щелкните правой кнопкой мыши hello **ProductsServer** проекта и нажмите кнопку **добавить**, а затем нажмите кнопку **класса**.</span><span class="sxs-lookup"><span data-stu-id="de323-158">In Solution Explorer, right-click hello **ProductsServer** project and click **Add**, and then click **Class**.</span></span>
9. <span data-ttu-id="de323-159">В hello **имя** hello введите имя **ProductsContract.cs**.</span><span class="sxs-lookup"><span data-stu-id="de323-159">In hello **Name** box, type hello name **ProductsContract.cs**.</span></span> <span data-ttu-id="de323-160">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="de323-160">Then click **Add**.</span></span>
10. <span data-ttu-id="de323-161">В **ProductsContract.cs**, замените следующий код, который определяет hello контракт для службы hello hello hello определения пространства имен.</span><span class="sxs-lookup"><span data-stu-id="de323-161">In **ProductsContract.cs**, replace hello namespace definition with hello following code, which defines hello contract for hello service.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define hello data contract for hello service
        [DataContract]
        // Declare hello serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define hello service contract.
        [ServiceContract]
        interface IProducts
        {
            [OperationContract]
            IList<ProductData> GetProducts();

        }

        interface IProductsChannel : IProducts, IClientChannel
        {
        }
    }
    ```
11. <span data-ttu-id="de323-162">В файле Program.cs замените определение пространства имен hello hello, следующий код, который добавляет службы профиля hello и hello узла для него.</span><span class="sxs-lookup"><span data-stu-id="de323-162">In Program.cs, replace hello namespace definition with hello following code, which adds hello profile service and hello host for it.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement hello IProducts interface.
        class ProductsService : IProducts
        {

            // Populate array of products for display on website
            ProductData[] products =
                new []
                    {
                        new ProductData{ Id = "1", Name = "Rock",
                                         Quantity = "1"},
                        new ProductData{ Id = "2", Name = "Paper",
                                         Quantity = "3"},
                        new ProductData{ Id = "3", Name = "Scissors",
                                         Quantity = "5"},
                        new ProductData{ Id = "4", Name = "Well",
                                         Quantity = "2500"},
                    };

            // Display a message in hello service console application
            // when hello list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define hello Main() function in hello service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER tooclose");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. <span data-ttu-id="de323-163">В обозревателе решений дважды щелкните hello **App.config** файл tooopen его в редакторе Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="de323-163">In Solution Explorer, double-click hello **App.config** file tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="de323-164">Внизу hello hello `<system.ServiceModel>` элемента (но по-прежнему в `<system.ServiceModel>`), добавьте следующий XML-кода hello.</span><span class="sxs-lookup"><span data-stu-id="de323-164">At hello bottom of hello `<system.ServiceModel>` element (but still within `<system.ServiceModel>`), add hello following XML code.</span></span> <span data-ttu-id="de323-165">Быть убедиться, что tooreplace *yourServiceNamespace* с именем hello пространства имен, и *yourKey* с ключом SAS hello ранее получены из портала hello:</span><span class="sxs-lookup"><span data-stu-id="de323-165">Be sure tooreplace *yourServiceNamespace* with hello name of your namespace, and *yourKey* with hello SAS key you retrieved earlier from hello portal:</span></span>

    ```xml
    <system.serviceModel>
    ...
      <services>
         <service name="ProductsServer.ProductsService">
           <endpoint address="sb://yourServiceNamespace.servicebus.windows.net/products" binding="netTcpRelayBinding" contract="ProductsServer.IProducts" behaviorConfiguration="products"/>
         </service>
      </services>
      <behaviors>
         <endpointBehaviors>
           <behavior name="products">
             <transportClientEndpointBehavior>
                <tokenProvider>
                   <sharedAccessSignature keyName="RootManageSharedAccessKey" key="yourKey" />
                </tokenProvider>
             </transportClientEndpointBehavior>
           </behavior>
         </endpointBehaviors>
      </behaviors>
    </system.serviceModel>
    ```
13. <span data-ttu-id="de323-166">По-прежнему в файл App.config, в hello `<appSettings>` элемента, замените значение строки подключения hello со строкой подключения hello ранее получены из портала hello.</span><span class="sxs-lookup"><span data-stu-id="de323-166">Still in App.config, in hello `<appSettings>` element, replace hello connection string value with hello connection string you previously obtained from hello portal.</span></span>

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. <span data-ttu-id="de323-167">Нажмите клавишу **Ctrl + Shift + B** или из hello **построения** меню, нажмите кнопку **построить решение** toobuild hello приложения и проверить правильность hello выполненной работы до сих.</span><span class="sxs-lookup"><span data-stu-id="de323-167">Press **Ctrl+Shift+B** or from hello **Build** menu, click **Build Solution** toobuild hello application and verify hello accuracy of your work so far.</span></span>

## <a name="create-an-aspnet-application"></a><span data-ttu-id="de323-168">Создание приложения ASP.NET</span><span class="sxs-lookup"><span data-stu-id="de323-168">Create an ASP.NET application</span></span>

<span data-ttu-id="de323-169">В этом разделе будет выполнено построение простого приложения ASP.NET, которое будет отображать данные, полученные из службы продукции.</span><span class="sxs-lookup"><span data-stu-id="de323-169">In this section you will build a simple ASP.NET application that displays data retrieved from your product service.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="de323-170">Создание проекта hello</span><span class="sxs-lookup"><span data-stu-id="de323-170">Create hello project</span></span>

1. <span data-ttu-id="de323-171">Убедитесь, что система Visual Studio запущена с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="de323-171">Ensure that Visual Studio is running with administrator privileges.</span></span>
2. <span data-ttu-id="de323-172">В Visual Studio в hello **файл** меню, нажмите кнопку **New**и нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="de323-172">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="de323-173">В разделе **Visual C#** области **Установленные шаблоны** щелкните **Веб-приложение ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="de323-173">From **Installed Templates**, under **Visual C#**, click **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="de323-174">Имя проекта hello **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="de323-174">Name hello project **ProductsPortal**.</span></span> <span data-ttu-id="de323-175">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="de323-175">Then click **OK**.</span></span>

   ![][15]

4. <span data-ttu-id="de323-176">Из hello **шаблоны ASP.NET** списка в hello **новое веб-приложение ASP.NET** диалоговое окно, нажмите кнопку **MVC**.</span><span class="sxs-lookup"><span data-stu-id="de323-176">From hello **ASP.NET Templates** list in hello **New ASP.NET Web Application** dialog, click **MVC**.</span></span>

   ![][16]

6. <span data-ttu-id="de323-177">Нажмите кнопку hello **изменить аутентификацию** кнопки.</span><span class="sxs-lookup"><span data-stu-id="de323-177">Click hello **Change Authentication** button.</span></span> <span data-ttu-id="de323-178">В hello **изменить аутентификацию** диалогового окна убедитесь, что **без проверки подлинности** выбран и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="de323-178">In hello **Change Authentication** dialog box, ensure that **No Authentication** is selected, and then click **OK**.</span></span> <span data-ttu-id="de323-179">В этом руководстве развертывается приложение, для которого не требуется имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="de323-179">For this tutorial, you're deploying an app that does not need a user login.</span></span>

    ![][18]

7. <span data-ttu-id="de323-180">Вернитесь на hello **новое веб-приложение ASP.NET** диалоговое окно, нажмите кнопку **ОК** приложение MVC toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="de323-180">Back in hello **New ASP.NET Web Application** dialog, click **OK** toocreate hello MVC app.</span></span>
8. <span data-ttu-id="de323-181">Теперь необходимо настроить ресурсы Azure для нового веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="de323-181">Now you must configure Azure resources for a new web app.</span></span> <span data-ttu-id="de323-182">Следуйте указаниям hello hello [tooAzure части этой статьи публикации](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="de323-182">Follow hello steps in hello [Publish tooAzure section of this article](../app-service-web/app-service-web-get-started-dotnet.md).</span></span> <span data-ttu-id="de323-183">Затем возвращают учебника toothis и продолжить toohello следующий шаг.</span><span class="sxs-lookup"><span data-stu-id="de323-183">Then, return toothis tutorial and proceed toohello next step.</span></span>
10. <span data-ttu-id="de323-184">В обозревателе решений щелкните правой кнопкой мыши **Модели**, а затем выберите **Добавить** и **Класс**.</span><span class="sxs-lookup"><span data-stu-id="de323-184">In Solution Explorer, right-click **Models** and then click **Add**, then click **Class**.</span></span> <span data-ttu-id="de323-185">В hello **имя** hello введите имя **Product.cs**.</span><span class="sxs-lookup"><span data-stu-id="de323-185">In hello **Name** box, type hello name **Product.cs**.</span></span> <span data-ttu-id="de323-186">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="de323-186">Then click **Add**.</span></span>

    ![][17]

### <a name="modify-hello-web-application"></a><span data-ttu-id="de323-187">Изменить веб-приложение hello</span><span class="sxs-lookup"><span data-stu-id="de323-187">Modify hello web application</span></span>

1. <span data-ttu-id="de323-188">В файле Product.cs hello в Visual Studio замените существующее определение пространства имен hello после кода hello.</span><span class="sxs-lookup"><span data-stu-id="de323-188">In hello Product.cs file in Visual Studio, replace hello existing namespace definition with hello following code.</span></span>

   ```csharp
    // Declare properties for hello products inventory.
    namespace ProductsWeb.Models
    {
       public class Product
       {
           public string Id { get; set; }
           public string Name { get; set; }
           public string Quantity { get; set; }
       }
    }
    ```
2. <span data-ttu-id="de323-189">В обозревателе решений разверните hello **контроллеров** папки, дважды щелкните hello **HomeController.cs** файл tooopen его в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="de323-189">In Solution Explorer, expand hello **Controllers** folder, then double-click hello **HomeController.cs** file tooopen it in Visual Studio.</span></span>
3. <span data-ttu-id="de323-190">В **HomeController.cs**, замените существующее определение пространства имен hello hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="de323-190">In **HomeController.cs**, replace hello existing namespace definition with hello following code.</span></span>

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of hello products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. <span data-ttu-id="de323-191">В обозревателе решений разверните hello одну папку, а затем дважды щелкните **_Layout.cshtml** tooopen его в редакторе Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="de323-191">In Solution Explorer, expand hello Views\Shared folder, then double-click **_Layout.cshtml** tooopen it in hello Visual Studio editor.</span></span>
5. <span data-ttu-id="de323-192">Замените все вхождения **Мое приложение ASP.NET** слишком**продуктов LITWARE**.</span><span class="sxs-lookup"><span data-stu-id="de323-192">Change all occurrences of **My ASP.NET Application** too**LITWARE's Products**.</span></span>
6. <span data-ttu-id="de323-193">Удалите hello **Главная**, **о**, и **контакт** ссылки.</span><span class="sxs-lookup"><span data-stu-id="de323-193">Remove hello **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="de323-194">В следующем примере hello удалите код выделен hello.</span><span class="sxs-lookup"><span data-stu-id="de323-194">In hello following example, delete hello highlighted code.</span></span>

    ![][41]

7. <span data-ttu-id="de323-195">В обозревателе решений разверните папку Views\Home hello, а затем дважды щелкните **Index.cshtml** tooopen его в редакторе Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="de323-195">In Solution Explorer, expand hello Views\Home folder, then double-click **Index.cshtml** tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="de323-196">Замените все содержимое файла hello hello hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="de323-196">Replace hello entire contents of hello file with hello following code.</span></span>

   ```html
   @model IEnumerable<ProductsWeb.Models.Product>

   @{
            ViewBag.Title = "Index";
   }

   <h2>Prod Inventory</h2>

   <table>
             <tr>
                 <th>
                     @Html.DisplayNameFor(model => model.Name)
                 </th>
                 <th></th>
                 <th>
                     @Html.DisplayNameFor(model => model.Quantity)
                 </th>
             </tr>

   @foreach (var item in Model) {
             <tr>
                 <td>
                     @Html.DisplayFor(modelItem => item.Name)
                 </td>
                 <td>
                     @Html.DisplayFor(modelItem => item.Quantity)
                 </td>
             </tr>
   }

   </table>
   ```
8. <span data-ttu-id="de323-197">tooverify hello точности своей работы таким образом, можно нажать клавишу **Ctrl + Shift + B** toobuild hello проекта.</span><span class="sxs-lookup"><span data-stu-id="de323-197">tooverify hello accuracy of your work so far, you can press **Ctrl+Shift+B** toobuild hello project.</span></span>

### <a name="run-hello-app-locally"></a><span data-ttu-id="de323-198">Выполните приложение hello локально</span><span class="sxs-lookup"><span data-stu-id="de323-198">Run hello app locally</span></span>

<span data-ttu-id="de323-199">Запустите tooverify приложения hello его работы.</span><span class="sxs-lookup"><span data-stu-id="de323-199">Run hello application tooverify that it works.</span></span>

1. <span data-ttu-id="de323-200">Убедитесь, что **ProductsPortal** — hello активного проекта.</span><span class="sxs-lookup"><span data-stu-id="de323-200">Ensure that **ProductsPortal** is hello active project.</span></span> <span data-ttu-id="de323-201">Щелкните правой кнопкой мыши имя проекта hello в обозревателе решений и выберите **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="de323-201">Right-click hello project name in Solution Explorer and select **Set As Startup Project**.</span></span>
2. <span data-ttu-id="de323-202">В Visual Studio нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="de323-202">In Visual Studio, press **F5**.</span></span>
3. <span data-ttu-id="de323-203">Приложение должно начать выполняться в браузере.</span><span class="sxs-lookup"><span data-stu-id="de323-203">Your application should appear, running in a browser.</span></span>

   ![][21]

## <a name="put-hello-pieces-together"></a><span data-ttu-id="de323-204">Объединить фрагменты hello</span><span class="sxs-lookup"><span data-stu-id="de323-204">Put hello pieces together</span></span>

<span data-ttu-id="de323-205">Hello следующим шагом является toohook копирование hello на локальном сервере продуктов с hello приложения ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="de323-205">hello next step is toohook up hello on-premises products server with hello ASP.NET application.</span></span>

1. <span data-ttu-id="de323-206">Если он не открыт, в Visual Studio повторно открыть hello **ProductsPortal** проект, созданный в hello [создать приложение ASP.NET](#create-an-aspnet-application) раздела.</span><span class="sxs-lookup"><span data-stu-id="de323-206">If it is not already open, in Visual Studio re-open hello **ProductsPortal** project you created in hello [Create an ASP.NET application](#create-an-aspnet-application) section.</span></span>
2. <span data-ttu-id="de323-207">Аналогичный шаг toohello в разделе «Создать локальный сервер» hello, добавьте ссылки на проект toohello hello NuGet пакета.</span><span class="sxs-lookup"><span data-stu-id="de323-207">Similar toohello step in hello "Create an On-Premises Server" section, add hello NuGet package toohello project references.</span></span> <span data-ttu-id="de323-208">В обозревателе решений щелкните правой кнопкой мыши hello **ProductsPortal** проекта, а затем нажмите кнопку **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="de323-208">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="de323-209">Для поиска «Service Bus» и выберите hello **WindowsAzure.ServiceBus** элемента.</span><span class="sxs-lookup"><span data-stu-id="de323-209">Search for "Service Bus" and select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="de323-210">Затем завершить установку hello и закрыть диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="de323-210">Then complete hello installation and close this dialog box.</span></span>
4. <span data-ttu-id="de323-211">В обозревателе решений щелкните правой кнопкой мыши hello **ProductsPortal** проекта, а затем нажмите кнопку **добавить**, затем **существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="de323-211">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Add**, then **Existing Item**.</span></span>
5. <span data-ttu-id="de323-212">Перейдите toohello **ProductsContract.cs** файл из hello **ProductsServer** консольного проекта.</span><span class="sxs-lookup"><span data-stu-id="de323-212">Navigate toohello **ProductsContract.cs** file from hello **ProductsServer** console project.</span></span> <span data-ttu-id="de323-213">Щелкните toohighlight ProductsContract.cs.</span><span class="sxs-lookup"><span data-stu-id="de323-213">Click toohighlight ProductsContract.cs.</span></span> <span data-ttu-id="de323-214">Нажмите кнопку hello стрелку вниз рядом слишком**добавить**, нажмите кнопку **добавить как ссылку**.</span><span class="sxs-lookup"><span data-stu-id="de323-214">Click hello down arrow next too**Add**, then click **Add as Link**.</span></span>

   ![][24]

6. <span data-ttu-id="de323-215">Теперь откройте hello **HomeController.cs** в редакторе Visual Studio hello и замените определение пространства имен hello hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="de323-215">Now open hello **HomeController.cs** file in hello Visual Studio editor and replace hello namespace definition with hello following code.</span></span> <span data-ttu-id="de323-216">Быть убедиться, что tooreplace *yourServiceNamespace* с именем hello пространства имен службы, и *yourKey* ваш ключ SAS.</span><span class="sxs-lookup"><span data-stu-id="de323-216">Be sure tooreplace *yourServiceNamespace* with hello name of your service namespace, and *yourKey* with your SAS key.</span></span> <span data-ttu-id="de323-217">Это позволит hello клиента toocall hello локальной службы, возвращая результат hello hello вызова.</span><span class="sxs-lookup"><span data-stu-id="de323-217">This will enable hello client toocall hello on-premises service, returning hello result of hello call.</span></span>

   ```csharp
   namespace ProductsWeb.Controllers
   {
       using System.Linq;
       using System.ServiceModel;
       using System.Web.Mvc;
       using Microsoft.ServiceBus;
       using Models;
       using ProductsServer;

       public class HomeController : Controller
       {
           // Declare hello channel factory.
           static ChannelFactory<IProductsChannel> channelFactory;

           static HomeController()
           {
               // Create shared access signature token credentials for authentication.
               channelFactory = new ChannelFactory<IProductsChannel>(new NetTcpRelayBinding(),
                   "sb://yourServiceNamespace.servicebus.windows.net/products");
               channelFactory.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior {
                   TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                       "RootManageSharedAccessKey", "yourKey") });
           }

           public ActionResult Index()
           {
               using (IProductsChannel channel = channelFactory.CreateChannel())
               {
                   // Return a view of hello products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. <span data-ttu-id="de323-218">В обозревателе решений щелкните правой кнопкой мыши hello **ProductsPortal** решения (Убедитесь, что tooright щелчком hello решение, не hello проект).</span><span class="sxs-lookup"><span data-stu-id="de323-218">In Solution Explorer, right-click hello **ProductsPortal** solution (make sure tooright-click hello solution, not hello project).</span></span> <span data-ttu-id="de323-219">Щелкните **Добавить**, а затем — **Существующий проект**.</span><span class="sxs-lookup"><span data-stu-id="de323-219">Click **Add**, then click **Existing Project**.</span></span>
8. <span data-ttu-id="de323-220">Перейдите toohello **ProductsServer** проекта, а затем дважды щелкните hello **ProductsServer.csproj** tooadd файл решения его.</span><span class="sxs-lookup"><span data-stu-id="de323-220">Navigate toohello **ProductsServer** project, then double-click hello **ProductsServer.csproj** solution file tooadd it.</span></span>
9. <span data-ttu-id="de323-221">**ProductsServer** на должна быть запущена в данные о заказах toodisplay hello **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="de323-221">**ProductsServer** must be running in order toodisplay hello data on **ProductsPortal**.</span></span> <span data-ttu-id="de323-222">В обозревателе решений щелкните правой кнопкой мыши hello **ProductsPortal** решения и нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="de323-222">In Solution Explorer, right-click hello **ProductsPortal** solution and click **Properties**.</span></span> <span data-ttu-id="de323-223">Hello **страницы свойств** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="de323-223">hello **Property Pages** dialog box is displayed.</span></span>
10. <span data-ttu-id="de323-224">На hello слева, нажмите кнопку **запускаемый проект**.</span><span class="sxs-lookup"><span data-stu-id="de323-224">On hello left side, click **Startup Project**.</span></span> <span data-ttu-id="de323-225">На правой стороне hello, нажмите кнопку **несколько запускаемых проектов**.</span><span class="sxs-lookup"><span data-stu-id="de323-225">On hello right side, click **Multiple startup projects**.</span></span> <span data-ttu-id="de323-226">Убедитесь, что **ProductsServer** и **ProductsPortal** отображается, в указанном порядке с **запустить** задать как действие hello для обоих.</span><span class="sxs-lookup"><span data-stu-id="de323-226">Ensure that **ProductsServer** and **ProductsPortal** appear, in that order, with **Start** set as hello action for both.</span></span>

      ![][25]

11. <span data-ttu-id="de323-227">По-прежнему в hello **свойства** диалоговое окно, нажмите кнопку **зависимости проекта** на hello слева.</span><span class="sxs-lookup"><span data-stu-id="de323-227">Still in hello **Properties** dialog box, click **Project Dependencies** on hello left side.</span></span>
12. <span data-ttu-id="de323-228">В hello **проекты** выберите **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="de323-228">In hello **Projects** list, click **ProductsServer**.</span></span> <span data-ttu-id="de323-229">Снимите флажок **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="de323-229">Ensure that **ProductsPortal** is not selected.</span></span>
13. <span data-ttu-id="de323-230">В hello **проекты** выберите **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="de323-230">In hello **Projects** list, click **ProductsPortal**.</span></span> <span data-ttu-id="de323-231">Установите флажок **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="de323-231">Ensure that **ProductsServer** is selected.</span></span>

    ![][26]

14. <span data-ttu-id="de323-232">Нажмите кнопку **ОК** в hello **страницы свойств** диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="de323-232">Click **OK** in hello **Property Pages** dialog box.</span></span>

## <a name="run-hello-project-locally"></a><span data-ttu-id="de323-233">Запустите проект hello локально</span><span class="sxs-lookup"><span data-stu-id="de323-233">Run hello project locally</span></span>

<span data-ttu-id="de323-234">приложения hello tootest локально, в Visual Studio нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="de323-234">tootest hello application locally, in Visual Studio press **F5**.</span></span> <span data-ttu-id="de323-235">на локальном сервере Hello (**ProductsServer**) следует запустить первой, а затем hello **ProductsPortal** приложение должно запускаться в окне браузера.</span><span class="sxs-lookup"><span data-stu-id="de323-235">hello on-premises server (**ProductsServer**) should start first, then hello **ProductsPortal** application should start in a browser window.</span></span> <span data-ttu-id="de323-236">На этот раз вы увидите запасов продукта hello списки данных, полученных из hello продукта службы в локальной системе.</span><span class="sxs-lookup"><span data-stu-id="de323-236">This time, you will see that hello product inventory lists data retrieved from hello product service on-premises system.</span></span>

![][10]

<span data-ttu-id="de323-237">Нажмите клавишу **обновление** на hello **ProductsPortal** страницы.</span><span class="sxs-lookup"><span data-stu-id="de323-237">Press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="de323-238">Каждый раз, обновите страницу приветствия, вы увидите приложение hello server отображать сообщение при `GetProducts()` из **ProductsServer** вызывается.</span><span class="sxs-lookup"><span data-stu-id="de323-238">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

<span data-ttu-id="de323-239">Закройте оба приложения перед продолжением toohello следующий шаг.</span><span class="sxs-lookup"><span data-stu-id="de323-239">Close both applications before proceeding toohello next step.</span></span>

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a><span data-ttu-id="de323-240">Развертывание hello ProductsPortal проекта tooan веб-приложение Azure</span><span class="sxs-lookup"><span data-stu-id="de323-240">Deploy hello ProductsPortal project tooan Azure web app</span></span>

<span data-ttu-id="de323-241">Hello следующим шагом является toorepublish hello Azure Web app **ProductsPortal** переднего плана.</span><span class="sxs-lookup"><span data-stu-id="de323-241">hello next step is toorepublish hello Azure Web app **ProductsPortal** frontend.</span></span> <span data-ttu-id="de323-242">Здравствуйте, следующие:</span><span class="sxs-lookup"><span data-stu-id="de323-242">Do hello following:</span></span>

1. <span data-ttu-id="de323-243">В обозревателе решений щелкните правой кнопкой мыши hello **ProductsPortal** проекта, а затем нажмите кнопку **публикации**.</span><span class="sxs-lookup"><span data-stu-id="de323-243">In Solution Explorer, right-click hello **ProductsPortal** project, and click **Publish**.</span></span> <span data-ttu-id="de323-244">Нажмите кнопку **публикации** на hello **публикации** страницы.</span><span class="sxs-lookup"><span data-stu-id="de323-244">Then, click **Publish** on hello **Publish** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="de323-245">Может появиться сообщение об ошибке в окне браузера hello при hello **ProductsPortal** веб-проекта запускается автоматически после развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="de323-245">You may see an error message in hello browser window when hello **ProductsPortal** web project is automatically launched after hello deployment.</span></span> <span data-ttu-id="de323-246">Это нормально и возникает из-за hello **ProductsServer** приложения еще не запущен.</span><span class="sxs-lookup"><span data-stu-id="de323-246">This is expected, and occurs because hello **ProductsServer** application isn't running yet.</span></span>
>
>

2. <span data-ttu-id="de323-247">Копировать URL-адрес hello объекта hello развернуть веб-приложения, как он потребуется hello URL-адрес в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="de323-247">Copy hello URL of hello deployed web app, as you will need hello URL in hello next step.</span></span> <span data-ttu-id="de323-248">Этот URL-адрес можно получить из окна hello активности службы приложения Azure в Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="de323-248">You can also obtain this URL from hello Azure App Service Activity window in Visual Studio:</span></span>

  ![][9]

3. <span data-ttu-id="de323-249">Закройте hello окна браузера toostop hello запущено приложение.</span><span class="sxs-lookup"><span data-stu-id="de323-249">Close hello browser window toostop hello running application.</span></span>

### <a name="set-productsportal-as-web-app"></a><span data-ttu-id="de323-250">Настройка ProductsPortal в качестве веб-приложения</span><span class="sxs-lookup"><span data-stu-id="de323-250">Set ProductsPortal as web app</span></span>

<span data-ttu-id="de323-251">Прежде чем приложения hello в облаке hello, необходимо убедиться, что **ProductsPortal** , запускаемого из среды Visual Studio, что веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="de323-251">Before running hello application in hello cloud, you must ensure that **ProductsPortal** is launched from within Visual Studio as a web app.</span></span>

1. <span data-ttu-id="de323-252">В Visual Studio щелкните правой кнопкой мыши hello **ProductsPortal** проект и выберите пункт **свойства**.</span><span class="sxs-lookup"><span data-stu-id="de323-252">In Visual Studio, right-click hello **ProductsPortal** project and then click **Properties**.</span></span>
2. <span data-ttu-id="de323-253">В левом столбце hello щелкните **Web**.</span><span class="sxs-lookup"><span data-stu-id="de323-253">In hello left-hand column, click **Web**.</span></span>
3. <span data-ttu-id="de323-254">В hello **действие при запуске** щелкните hello **начальный URL-адрес** , а в hello текстовом поле введите URL-адрес hello ранее развернутого веб-приложения; например, `http://productsportal1234567890.azurewebsites.net/`.</span><span class="sxs-lookup"><span data-stu-id="de323-254">In hello **Start Action** section, click hello **Start URL** button, and in hello text box enter hello URL for your previously deployed web app; for example, `http://productsportal1234567890.azurewebsites.net/`.</span></span>

    ![][27]

4. <span data-ttu-id="de323-255">Из hello **файл** меню в Visual Studio щелкните **сохранить все**.</span><span class="sxs-lookup"><span data-stu-id="de323-255">From hello **File** menu in Visual Studio, click **Save All**.</span></span>
5. <span data-ttu-id="de323-256">В меню сборка hello в Visual Studio, нажмите кнопку **Перестроить решение**.</span><span class="sxs-lookup"><span data-stu-id="de323-256">From hello Build menu in Visual Studio, click **Rebuild Solution**.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="de323-257">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="de323-257">Run hello application</span></span>

1. <span data-ttu-id="de323-258">Нажмите клавишу F5 toobuild и запустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="de323-258">Press F5 toobuild and run hello application.</span></span> <span data-ttu-id="de323-259">на локальном сервере Hello (hello **ProductsServer** консольное приложение) следует запустить первой, а затем hello **ProductsPortal** приложение должно запускаться в окне браузера, как показано в следующий экран приветствия снимок.</span><span class="sxs-lookup"><span data-stu-id="de323-259">hello on-premises server (hello **ProductsServer** console application) should start first, then hello **ProductsPortal** application should start in a browser window, as shown in hello following screen shot.</span></span> <span data-ttu-id="de323-260">Снова Обратите внимание, запасов продукта hello перечислены данные, полученные из hello продукта службы в локальной системе и отображает их в веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="de323-260">Notice again that hello product inventory lists data retrieved from hello product service on-premises system, and displays that data in hello web app.</span></span> <span data-ttu-id="de323-261">Проверьте что toomake URL-адрес hello, **ProductsPortal** работает в облаке hello, как Azure веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="de323-261">Check hello URL toomake sure that **ProductsPortal** is running in hello cloud, as an Azure web app.</span></span>

   ![][1]

   > [!IMPORTANT]
   > <span data-ttu-id="de323-262">Hello **ProductsServer** консольного приложения должен быть запущен и может toohello данных hello tooserve **ProductsPortal** приложения.</span><span class="sxs-lookup"><span data-stu-id="de323-262">hello **ProductsServer** console application must be running and able tooserve hello data toohello **ProductsPortal** application.</span></span> <span data-ttu-id="de323-263">Если hello браузер отображает ошибку, подождите несколько секунд, дополнительные для **ProductsServer** tooload и отображения hello следующие сообщения.</span><span class="sxs-lookup"><span data-stu-id="de323-263">If hello browser displays an error, wait a few more seconds for **ProductsServer** tooload and display hello following message.</span></span> <span data-ttu-id="de323-264">Нажмите клавишу **обновление** в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="de323-264">Then press **Refresh** in hello browser.</span></span>
   >
   >

   ![][37]
2. <span data-ttu-id="de323-265">Вернувшись в браузере hello, нажмите **обновление** на hello **ProductsPortal** страницы.</span><span class="sxs-lookup"><span data-stu-id="de323-265">Back in hello browser, press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="de323-266">Каждый раз, обновите страницу приветствия, вы увидите приложение hello server отображать сообщение при `GetProducts()` из **ProductsServer** вызывается.</span><span class="sxs-lookup"><span data-stu-id="de323-266">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

    ![][38]

## <a name="next-steps"></a><span data-ttu-id="de323-267">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="de323-267">Next steps</span></span>

<span data-ttu-id="de323-268">toolearn Дополнительные сведения о ретрансляции Azure см. следующие ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="de323-268">toolearn more about Azure Relay, see hello following resources:</span></span>  

* [<span data-ttu-id="de323-269">Что такое ретранслятор Azure?</span><span class="sxs-lookup"><span data-stu-id="de323-269">What is Azure Relay?</span></span>](relay-what-is-it.md)  
* [<span data-ttu-id="de323-270">Как toouse ретрансляции</span><span class="sxs-lookup"><span data-stu-id="de323-270">How toouse Relay</span></span>](service-bus-dotnet-how-to-use-relay.md)  

[0]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hybrid.png
[1]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[NuGet]: http://nuget.org

[11]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-con-1.png
[13]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-13.png
[15]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-2.png
[16]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-4.png
[17]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-7.png
[18]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-5.png
[9]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-9.png
[10]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App3.png

[21]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App1.png
[24]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-12.png
[25]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-13.png
[26]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-14.png
[27]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-8.png

[36]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[37]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service1.png
[38]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service2.png
[41]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-40.png
[43]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-hybrid-43.png
