---
title: "Гибридные локальные и облачные приложения ретранслятора WCF Azure (.NET) | Документация Майкрософт"
description: "Узнайте, как создать локальное или облачное гибридное приложение .NET с использованием ретранслятора WCF Azure."
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
ms.openlocfilehash: 366922a083b9d18ef50e04eb8b459d2725315e1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a><span data-ttu-id="724cd-103">Создание локального или облачного гибридного приложения .NET с использованием ретранслятора WCF Azure</span><span class="sxs-lookup"><span data-stu-id="724cd-103">.NET on-premises/cloud hybrid application using Azure WCF Relay</span></span>
## <a name="introduction"></a><span data-ttu-id="724cd-104">Введение</span><span class="sxs-lookup"><span data-stu-id="724cd-104">Introduction</span></span>

<span data-ttu-id="724cd-105">В этой статье показано, как создать гибридное облачное приложение с помощью Microsoft Azure и Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="724cd-105">This article shows how to build a hybrid cloud application with Microsoft Azure and Visual Studio.</span></span> <span data-ttu-id="724cd-106">В этом учебнике предполагается, что у вас нет опыта использования платформы Azure.</span><span class="sxs-lookup"><span data-stu-id="724cd-106">The tutorial assumes you have no prior experience using Azure.</span></span> <span data-ttu-id="724cd-107">Менее чем за 30 минут вы получите приложение, которое использует несколько ресурсов Microsoft Azure и выполняется в облаке.</span><span class="sxs-lookup"><span data-stu-id="724cd-107">In less than 30 minutes, you will have an application that uses multiple Azure resources up and running in the cloud.</span></span>

<span data-ttu-id="724cd-108">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="724cd-108">You will learn:</span></span>

* <span data-ttu-id="724cd-109">Как создать или адаптировать существующую веб-службу для использования веб-решением.</span><span class="sxs-lookup"><span data-stu-id="724cd-109">How to create or adapt an existing web service for consumption by a web solution.</span></span>
* <span data-ttu-id="724cd-110">Как использовать службу ретранслятора WCF Azure для обмена данными между приложением Azure и веб-службой, которая размещается в другом месте.</span><span class="sxs-lookup"><span data-stu-id="724cd-110">How to use the Azure WCF Relay service to share data between an Azure application and a web service hosted elsewhere.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a><span data-ttu-id="724cd-111">Как ретранслятор Azure помогает работать с гибридными решениями</span><span class="sxs-lookup"><span data-stu-id="724cd-111">How Azure Relay helps with hybrid solutions</span></span>

<span data-ttu-id="724cd-112">Бизнес-решения обычно состоят из сочетания пользовательского кода, написанного для удовлетворения новых и уникальных бизнес-требований, с существующими функциональными возможностями, предоставляемыми уже используемыми решениями и системами.</span><span class="sxs-lookup"><span data-stu-id="724cd-112">Business solutions are typically composed of a combination of custom code written to tackle new and unique business requirements and existing functionality provided by solutions and systems that are already in place.</span></span>

<span data-ttu-id="724cd-113">Архитекторы решений начинают использовать облако для упрощения реализации масштабирования и снижения эксплуатационных расходов.</span><span class="sxs-lookup"><span data-stu-id="724cd-113">Solution architects are starting to use the cloud for easier handling of scale requirements and lower operational costs.</span></span> <span data-ttu-id="724cd-114">При этом они обнаруживают,что существующие активы служб, которые они хотели бы использовать в качестве стандартных блоков для своих решений, находятся за корпоративным брандмауэром, поэтому обращение к ним из облачного решения затруднено.</span><span class="sxs-lookup"><span data-stu-id="724cd-114">In doing so, they find that existing service assets they'd like to leverage as building blocks for their solutions are inside the corporate firewall and out of easy reach for access by the cloud solution.</span></span> <span data-ttu-id="724cd-115">Многие внутренние службы построены или размещены таким образом, который не позволяет легко предоставлять их на границе корпоративной сети.</span><span class="sxs-lookup"><span data-stu-id="724cd-115">Many internal services are not built or hosted in a way that they can be easily exposed at the corporate network edge.</span></span>

<span data-ttu-id="724cd-116">[Ретранслятор Azure](https://azure.microsoft.com/services/service-bus/) предназначен для случаев, когда существующие веб-службы Windows Communication Foundation (WCF) безопасно предоставляются для решений, находящихся вне периметра корпоративной сети, без внесения существенных изменений в инфраструктуру корпоративной сети.</span><span class="sxs-lookup"><span data-stu-id="724cd-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/) is designed for the use-case of taking existing Windows Communication Foundation (WCF) web services and making those services securely accessible to solutions that reside outside the corporate perimeter without requiring intrusive changes to the corporate network infrastructure.</span></span> <span data-ttu-id="724cd-117">Такие службы ретрансляции по-прежнему размещаются внутри существующей среды, однако они делегируют функции прослушивания входящих сеансов и запросов размещенной в облаке службе ретрансляции.</span><span class="sxs-lookup"><span data-stu-id="724cd-117">Such relay services are still hosted inside their existing environment, but they delegate listening for incoming sessions and requests to the cloud-hosted relay service.</span></span> <span data-ttu-id="724cd-118">Ретранслятор Azure также защищает эти службы от несанкционированного доступа, применяя аутентификацию на основе [подписанного URL-адреса](../service-bus-messaging/service-bus-sas.md) (SAS).</span><span class="sxs-lookup"><span data-stu-id="724cd-118">Azure Relay also protects those services from unauthorized access by using [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) authentication.</span></span>

## <a name="solution-scenario"></a><span data-ttu-id="724cd-119">Сценарий решений</span><span class="sxs-lookup"><span data-stu-id="724cd-119">Solution scenario</span></span>
<span data-ttu-id="724cd-120">В этом учебнике вы создадите веб-сайт ASP.NET, который позволит просматривать список продуктов на странице складских запасов.</span><span class="sxs-lookup"><span data-stu-id="724cd-120">In this tutorial, you will create an ASP.NET website that enables you to see a list of products on the product inventory page.</span></span>

![][0]

<span data-ttu-id="724cd-121">В учебнике предполагается, что у вас есть сведения о продуктах в существующей локальной системе, для доступа к которой используется ретранслятор Azure.</span><span class="sxs-lookup"><span data-stu-id="724cd-121">The tutorial assumes that you have product information in an existing on-premises system, and uses Azure Relay to reach into that system.</span></span> <span data-ttu-id="724cd-122">Это имитируется веб-службой, запущенной в простом консольном приложении и поддерживаемой набором продуктов в памяти.</span><span class="sxs-lookup"><span data-stu-id="724cd-122">This is simulated by a web service that runs in a simple console application and is backed by an in-memory set of products.</span></span> <span data-ttu-id="724cd-123">Можно запустить это консольное приложение на своем компьютере и развернуть веб-роль в Azure.</span><span class="sxs-lookup"><span data-stu-id="724cd-123">You will be able to run this console application on your own computer and deploy the web role into Azure.</span></span> <span data-ttu-id="724cd-124">Таким образом вы увидите, как веб-роль, выполняемая в центре обработки данных Azure, действительно вызывает ваш компьютер, даже если он (почти наверняка) будет находиться хотя бы за одним брандмауэром и слоем преобразования сетевых адресов (NAT).</span><span class="sxs-lookup"><span data-stu-id="724cd-124">By doing so, you will see how the web role running in the Azure datacenter will indeed call into your computer, even though your computer will almost certainly reside behind at least one firewall and a network address translation (NAT) layer.</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="724cd-125">Настройка среды разработки</span><span class="sxs-lookup"><span data-stu-id="724cd-125">Set up the development environment</span></span>

<span data-ttu-id="724cd-126">Прежде чем начать разработку приложения для Azure, скачайте нужные инструменты и настройте среду разработки.</span><span class="sxs-lookup"><span data-stu-id="724cd-126">Before you can begin developing Azure applications, download the tools and set up your development environment:</span></span>

1. <span data-ttu-id="724cd-127">Установите пакет SDK Azure для .NET, скачав его с [этой страницы](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="724cd-127">Install the Azure SDK for .NET from the SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="724cd-128">В столбце **.NET** щелкните ссылку, соответствующую используемой версии [Visual Studio](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="724cd-128">In the **.NET** column, click the version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="724cd-129">В этом руководстве используется Visual Studio 2015, но вы также можете работать с Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="724cd-129">The steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="724cd-130">При появлении запроса на выполнение или сохранение файла установки щелкните **Выполнить**.</span><span class="sxs-lookup"><span data-stu-id="724cd-130">When prompted to run or save the installer, click **Run**.</span></span>
4. <span data-ttu-id="724cd-131">В **установщике веб-платформы** щелкните **Установить**, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="724cd-131">In the **Web Platform Installer**, click **Install** and proceed with the installation.</span></span>
5. <span data-ttu-id="724cd-132">После завершения установки у вас будут все компоненты, необходимые для начала разработки приложения.</span><span class="sxs-lookup"><span data-stu-id="724cd-132">Once the installation is complete, you will have everything necessary to start to develop the app.</span></span> <span data-ttu-id="724cd-133">В состав пакета SDK входят инструменты для эффективной разработки приложений Azure в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="724cd-133">The SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="724cd-134">Создание пространства имен</span><span class="sxs-lookup"><span data-stu-id="724cd-134">Create a namespace</span></span>

<span data-ttu-id="724cd-135">Чтобы начать использовать функции ретранслятора Azure, необходимо сначала создать пространство имен службы.</span><span class="sxs-lookup"><span data-stu-id="724cd-135">To begin using the relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="724cd-136">Пространство имен предоставляет контейнер для адресации ресурсов Azure в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="724cd-136">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="724cd-137">Выполните [эти инструкции](relay-create-namespace-portal.md), чтобы создать пространство имен ретранслятора.</span><span class="sxs-lookup"><span data-stu-id="724cd-137">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="create-an-on-premises-server"></a><span data-ttu-id="724cd-138">Создание локального сервера</span><span class="sxs-lookup"><span data-stu-id="724cd-138">Create an on-premises server</span></span>

<span data-ttu-id="724cd-139">Во-первых, нужно создать (макетную) локальную систему каталогов продукции.</span><span class="sxs-lookup"><span data-stu-id="724cd-139">First, you will build a (mock) on-premises product catalog system.</span></span> <span data-ttu-id="724cd-140">Она будет довольно простой. Это выглядит как представление фактической локальной системы каталогов продукции в виде полнофункциональной службы, которую мы пытаемся интегрировать.</span><span class="sxs-lookup"><span data-stu-id="724cd-140">It will be fairly simple; you can see this as representing an actual on-premises product catalog system with a complete service surface that we're trying to integrate.</span></span>

<span data-ttu-id="724cd-141">Этот проект запускается как консольное приложение Visual Studio, используя [пакет NuGet служебной шины Azure](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) для включения библиотек и параметров конфигурации служебной шины.</span><span class="sxs-lookup"><span data-stu-id="724cd-141">This project is a Visual Studio console application, and uses the [Azure Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) to include the Service Bus libraries and configuration settings.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="724cd-142">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="724cd-142">Create the project</span></span>

1. <span data-ttu-id="724cd-143">Запустите Microsoft Visual Studio, используя привилегии администратора.</span><span class="sxs-lookup"><span data-stu-id="724cd-143">Using administrator privileges, start Microsoft Visual Studio.</span></span> <span data-ttu-id="724cd-144">Для этого щелкните правой кнопкой мыши значок программы Visual Studio и выберите **Запустить от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="724cd-144">To do so, right-click the Visual Studio program icon, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="724cd-145">В меню **Файл** Visual Studio выберите **Создать**, а затем — **Проект**.</span><span class="sxs-lookup"><span data-stu-id="724cd-145">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="724cd-146">В разделе **Visual C#** области **Установленные шаблоны** щелкните **Консольное приложение (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="724cd-146">From **Installed Templates**, under **Visual C#**, click **Console App (.NET Framework)**.</span></span> <span data-ttu-id="724cd-147">В поле **Имя** введите **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="724cd-147">In the **Name** box, type the name **ProductsServer**:</span></span>

   ![][11]
4. <span data-ttu-id="724cd-148">Нажмите кнопку **ОК**, чтобы создать проект **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="724cd-148">Click **OK** to create the **ProductsServer** project.</span></span>
5. <span data-ttu-id="724cd-149">Если диспетчер пакетов NuGet для Visual Studio уже установлен, пропустите следующий шаг.</span><span class="sxs-lookup"><span data-stu-id="724cd-149">If you have already installed the NuGet package manager for Visual Studio, skip to the next step.</span></span> <span data-ttu-id="724cd-150">В противном случае посетите сайт [NuGet][NuGet] и щелкните [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) (Установить NuGet).</span><span class="sxs-lookup"><span data-stu-id="724cd-150">Otherwise, visit [NuGet][NuGet] and click [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span></span> <span data-ttu-id="724cd-151">Следуйте инструкциям на экране для установки диспетчера пакетов NuGet, а затем перезапустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="724cd-151">Follow the prompts to install the NuGet package manager, then re-start Visual Studio.</span></span>
6. <span data-ttu-id="724cd-152">В обозревателе решений щелкните правой кнопкой мыши проект **ProductsServer** и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="724cd-152">In Solution Explorer, right-click the **ProductsServer** project, then click **Manage NuGet Packages**.</span></span>
7. <span data-ttu-id="724cd-153">Щелкните вкладку **Обзор** и выполните поиск `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="724cd-153">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="724cd-154">Выберите пакет **WindowsAzure.ServiceBus**.</span><span class="sxs-lookup"><span data-stu-id="724cd-154">Select the **WindowsAzure.ServiceBus** package.</span></span>
8. <span data-ttu-id="724cd-155">Щелкните **Установить**и примите условия использования.</span><span class="sxs-lookup"><span data-stu-id="724cd-155">Click **Install**, and accept the terms of use.</span></span>

   ![][13]

   <span data-ttu-id="724cd-156">Обратите внимание, что на необходимые клиентские сборки теперь имеется ссылка.</span><span class="sxs-lookup"><span data-stu-id="724cd-156">Note that the required client assemblies are now referenced.</span></span>
8. <span data-ttu-id="724cd-157">Добавьте новый класс для контракта на свою продукцию.</span><span class="sxs-lookup"><span data-stu-id="724cd-157">Add a new class for your product contract.</span></span> <span data-ttu-id="724cd-158">В обозревателе решений щелкните правой кнопкой проект **ProductsServer**, а затем выберите **Добавить** и **Класс**.</span><span class="sxs-lookup"><span data-stu-id="724cd-158">In Solution Explorer, right-click the **ProductsServer** project and click **Add**, and then click **Class**.</span></span>
9. <span data-ttu-id="724cd-159">В поле **Имя** введите **ProductsContract.cs**.</span><span class="sxs-lookup"><span data-stu-id="724cd-159">In the **Name** box, type the name **ProductsContract.cs**.</span></span> <span data-ttu-id="724cd-160">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="724cd-160">Then click **Add**.</span></span>
10. <span data-ttu-id="724cd-161">В **ProductsContract.cs** замените определение пространства имен на приведенный ниже код, определяющий контракт для службы.</span><span class="sxs-lookup"><span data-stu-id="724cd-161">In **ProductsContract.cs**, replace the namespace definition with the following code, which defines the contract for the service.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define the data contract for the service
        [DataContract]
        // Declare the serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define the service contract.
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
11. <span data-ttu-id="724cd-162">В Program.cs замените определение пространства имен на следующий код, добавляющий службу профилей и узел для нее.</span><span class="sxs-lookup"><span data-stu-id="724cd-162">In Program.cs, replace the namespace definition with the following code, which adds the profile service and the host for it.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement the IProducts interface.
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

            // Display a message in the service console application
            // when the list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define the Main() function in the service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER to close");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. <span data-ttu-id="724cd-163">В обозревателе решений дважды щелкните файл **App.config**, чтобы открыть его в редакторе Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="724cd-163">In Solution Explorer, double-click the **App.config** file to open it in the Visual Studio editor.</span></span> <span data-ttu-id="724cd-164">В нижней части элемента `<system.ServiceModel>` (но не выходя за рамки элемента `<system.ServiceModel>`) добавьте приведенный ниже код XML.</span><span class="sxs-lookup"><span data-stu-id="724cd-164">At the bottom of the `<system.ServiceModel>` element (but still within `<system.ServiceModel>`), add the following XML code.</span></span> <span data-ttu-id="724cd-165">Не забудьте заменить *yourServiceNamespace* именем пространства имен, а *yourKey* — ключом SAS, полученным ранее на портале.</span><span class="sxs-lookup"><span data-stu-id="724cd-165">Be sure to replace *yourServiceNamespace* with the name of your namespace, and *yourKey* with the SAS key you retrieved earlier from the portal:</span></span>

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
13. <span data-ttu-id="724cd-166">В файле App.config в элементе `<appSettings>` замените значение строки подключения значением, полученным ранее на портале.</span><span class="sxs-lookup"><span data-stu-id="724cd-166">Still in App.config, in the `<appSettings>` element, replace the connection string value with the connection string you previously obtained from the portal.</span></span>

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. <span data-ttu-id="724cd-167">Нажмите клавиши **CTRL+SHIFT+B** или в меню **Сборка** щелкните **Собрать решение**, чтобы создать приложение и проверить результат.</span><span class="sxs-lookup"><span data-stu-id="724cd-167">Press **Ctrl+Shift+B** or from the **Build** menu, click **Build Solution** to build the application and verify the accuracy of your work so far.</span></span>

## <a name="create-an-aspnet-application"></a><span data-ttu-id="724cd-168">Создание приложения ASP.NET</span><span class="sxs-lookup"><span data-stu-id="724cd-168">Create an ASP.NET application</span></span>

<span data-ttu-id="724cd-169">В этом разделе будет выполнено построение простого приложения ASP.NET, которое будет отображать данные, полученные из службы продукции.</span><span class="sxs-lookup"><span data-stu-id="724cd-169">In this section you will build a simple ASP.NET application that displays data retrieved from your product service.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="724cd-170">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="724cd-170">Create the project</span></span>

1. <span data-ttu-id="724cd-171">Убедитесь, что система Visual Studio запущена с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="724cd-171">Ensure that Visual Studio is running with administrator privileges.</span></span>
2. <span data-ttu-id="724cd-172">В меню **Файл** Visual Studio выберите **Создать**, а затем — **Проект**.</span><span class="sxs-lookup"><span data-stu-id="724cd-172">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="724cd-173">В разделе **Visual C#** области **Установленные шаблоны** щелкните **Веб-приложение ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="724cd-173">From **Installed Templates**, under **Visual C#**, click **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="724cd-174">Присвойте проекту имя **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="724cd-174">Name the project **ProductsPortal**.</span></span> <span data-ttu-id="724cd-175">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="724cd-175">Then click **OK**.</span></span>

   ![][15]

4. <span data-ttu-id="724cd-176">В списке **шаблонов ASP.NET** диалогового окна **Создание веб-приложения ASP.NET** выберите **MVC**.</span><span class="sxs-lookup"><span data-stu-id="724cd-176">From the **ASP.NET Templates** list in the **New ASP.NET Web Application** dialog, click **MVC**.</span></span>

   ![][16]

6. <span data-ttu-id="724cd-177">Нажмите кнопку **Изменить способ проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="724cd-177">Click the **Change Authentication** button.</span></span> <span data-ttu-id="724cd-178">В диалоговом окне **Изменить способ проверки подлинности** щелкните **Без проверки подлинности** и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="724cd-178">In the **Change Authentication** dialog box, ensure that **No Authentication** is selected, and then click **OK**.</span></span> <span data-ttu-id="724cd-179">В этом руководстве развертывается приложение, для которого не требуется имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="724cd-179">For this tutorial, you're deploying an app that does not need a user login.</span></span>

    ![][18]

7. <span data-ttu-id="724cd-180">Вернувшись к диалоговому окну **Создание веб-приложения ASP.NET**, нажмите кнопку **ОК**, чтобы создать приложение MVC.</span><span class="sxs-lookup"><span data-stu-id="724cd-180">Back in the **New ASP.NET Web Application** dialog, click **OK** to create the MVC app.</span></span>
8. <span data-ttu-id="724cd-181">Теперь необходимо настроить ресурсы Azure для нового веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="724cd-181">Now you must configure Azure resources for a new web app.</span></span> <span data-ttu-id="724cd-182">Следуйте указаниям в разделе [Публикация в Azure](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="724cd-182">Follow the steps in the [Publish to Azure section of this article](../app-service-web/app-service-web-get-started-dotnet.md).</span></span> <span data-ttu-id="724cd-183">Затем вернитесь к этому учебнику и перейдите к следующему шагу.</span><span class="sxs-lookup"><span data-stu-id="724cd-183">Then, return to this tutorial and proceed to the next step.</span></span>
10. <span data-ttu-id="724cd-184">В обозревателе решений щелкните правой кнопкой мыши **Модели**, а затем выберите **Добавить** и **Класс**.</span><span class="sxs-lookup"><span data-stu-id="724cd-184">In Solution Explorer, right-click **Models** and then click **Add**, then click **Class**.</span></span> <span data-ttu-id="724cd-185">В поле **Имя** введите **Product.cs**.</span><span class="sxs-lookup"><span data-stu-id="724cd-185">In the **Name** box, type the name **Product.cs**.</span></span> <span data-ttu-id="724cd-186">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="724cd-186">Then click **Add**.</span></span>

    ![][17]

### <a name="modify-the-web-application"></a><span data-ttu-id="724cd-187">Изменение веб-приложения</span><span class="sxs-lookup"><span data-stu-id="724cd-187">Modify the web application</span></span>

1. <span data-ttu-id="724cd-188">В Visual Studio замените существующее определение пространства имен в файле на следующий код.</span><span class="sxs-lookup"><span data-stu-id="724cd-188">In the Product.cs file in Visual Studio, replace the existing namespace definition with the following code.</span></span>

   ```csharp
    // Declare properties for the products inventory.
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
2. <span data-ttu-id="724cd-189">В обозревателе решений разверните папку **Контроллеры** и дважды щелкните файл **HomeController.cs**, чтобы открыть его в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="724cd-189">In Solution Explorer, expand the **Controllers** folder, then double-click the **HomeController.cs** file to open it in Visual Studio.</span></span>
3. <span data-ttu-id="724cd-190">В файле **HomeController.cs** замените имеющееся определение пространства имен следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="724cd-190">In **HomeController.cs**, replace the existing namespace definition with the following code.</span></span>

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of the products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. <span data-ttu-id="724cd-191">В обозревателе решений разверните папку Views\Shared, а затем дважды щелкните файл **_Layout.cshtml**, чтобы открыть его в редакторе Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="724cd-191">In Solution Explorer, expand the Views\Shared folder, then double-click **_Layout.cshtml** to open it in the Visual Studio editor.</span></span>
5. <span data-ttu-id="724cd-192">Замените все вхождения элемента **Мое приложение MVC ASP.NET** текстом **Продукты LITWARE**.</span><span class="sxs-lookup"><span data-stu-id="724cd-192">Change all occurrences of **My ASP.NET Application** to **LITWARE's Products**.</span></span>
6. <span data-ttu-id="724cd-193">Удалите ссылки **Главная**, **О программе** и **Контакт**.</span><span class="sxs-lookup"><span data-stu-id="724cd-193">Remove the **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="724cd-194">В следующем примере удалите выделенный код.</span><span class="sxs-lookup"><span data-stu-id="724cd-194">In the following example, delete the highlighted code.</span></span>

    ![][41]

7. <span data-ttu-id="724cd-195">В обозревателе решений разверните папку Views\Home, а затем дважды щелкните файл **Index.cshtml**, чтобы открыть его в редакторе Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="724cd-195">In Solution Explorer, expand the Views\Home folder, then double-click **Index.cshtml** to open it in the Visual Studio editor.</span></span> <span data-ttu-id="724cd-196">Замените все содержимое файла следующим кодом.</span><span class="sxs-lookup"><span data-stu-id="724cd-196">Replace the entire contents of the file with the following code.</span></span>

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
8. <span data-ttu-id="724cd-197">Чтобы проверить текущий результат, нажмите клавиши **CTRL+SHIFT+B** для сборки проекта.</span><span class="sxs-lookup"><span data-stu-id="724cd-197">To verify the accuracy of your work so far, you can press **Ctrl+Shift+B** to build the project.</span></span>

### <a name="run-the-app-locally"></a><span data-ttu-id="724cd-198">Локальный запуск приложения</span><span class="sxs-lookup"><span data-stu-id="724cd-198">Run the app locally</span></span>

<span data-ttu-id="724cd-199">Запустите приложение, чтобы убедиться, что оно работает.</span><span class="sxs-lookup"><span data-stu-id="724cd-199">Run the application to verify that it works.</span></span>

1. <span data-ttu-id="724cd-200">**ProductsPortal** должен быть активным проектом.</span><span class="sxs-lookup"><span data-stu-id="724cd-200">Ensure that **ProductsPortal** is the active project.</span></span> <span data-ttu-id="724cd-201">В обозревателе решений щелкните правой кнопкой мыши имя проекта и выберите пункт **Назначить запускаемым проектом**.</span><span class="sxs-lookup"><span data-stu-id="724cd-201">Right-click the project name in Solution Explorer and select **Set As Startup Project**.</span></span>
2. <span data-ttu-id="724cd-202">В Visual Studio нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="724cd-202">In Visual Studio, press **F5**.</span></span>
3. <span data-ttu-id="724cd-203">Приложение должно начать выполняться в браузере.</span><span class="sxs-lookup"><span data-stu-id="724cd-203">Your application should appear, running in a browser.</span></span>

   ![][21]

## <a name="put-the-pieces-together"></a><span data-ttu-id="724cd-204">Объединение элементов</span><span class="sxs-lookup"><span data-stu-id="724cd-204">Put the pieces together</span></span>

<span data-ttu-id="724cd-205">Следующим шагом является подключение локального сервера продуктов к приложению ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="724cd-205">The next step is to hook up the on-premises products server with the ASP.NET application.</span></span>

1. <span data-ttu-id="724cd-206">В Visual Studio повторно откройте проект **ProductsPortal**, созданный в разделе [Создание приложения ASP.NET](#create-an-aspnet-application).</span><span class="sxs-lookup"><span data-stu-id="724cd-206">If it is not already open, in Visual Studio re-open the **ProductsPortal** project you created in the [Create an ASP.NET application](#create-an-aspnet-application) section.</span></span>
2. <span data-ttu-id="724cd-207">Аналогично шагу в разделе "Создание локального сервера" добавьте пакет NuGet в ссылки проекта.</span><span class="sxs-lookup"><span data-stu-id="724cd-207">Similar to the step in the "Create an On-Premises Server" section, add the NuGet package to the project references.</span></span> <span data-ttu-id="724cd-208">В обозревателе решений щелкните правой кнопкой мыши проект **ProductsPortal** и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="724cd-208">In Solution Explorer, right-click the **ProductsPortal** project, then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="724cd-209">Выполните поиск по фразе "служебная шина" и выберите элемент **WindowsAzure.ServiceBus**.</span><span class="sxs-lookup"><span data-stu-id="724cd-209">Search for "Service Bus" and select the **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="724cd-210">Завершите установку и закройте это диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="724cd-210">Then complete the installation and close this dialog box.</span></span>
4. <span data-ttu-id="724cd-211">В обозревателе решений щелкните правой кнопкой мыши проект **ProductsPortal** и выберите пункт **Добавить**, а затем — **Существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="724cd-211">In Solution Explorer, right-click the **ProductsPortal** project, then click **Add**, then **Existing Item**.</span></span>
5. <span data-ttu-id="724cd-212">Перейдите к файлу **ProductsContract.cs** в консольном проекте **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="724cd-212">Navigate to the **ProductsContract.cs** file from the **ProductsServer** console project.</span></span> <span data-ttu-id="724cd-213">Щелкните, чтобы выделить ProductsContract.cs.</span><span class="sxs-lookup"><span data-stu-id="724cd-213">Click to highlight ProductsContract.cs.</span></span> <span data-ttu-id="724cd-214">Щелкните стрелку вниз рядом с пунктом **Добавить**, затем нажмите кнопку **Добавить как связь**.</span><span class="sxs-lookup"><span data-stu-id="724cd-214">Click the down arrow next to **Add**, then click **Add as Link**.</span></span>

   ![][24]

6. <span data-ttu-id="724cd-215">Теперь откройте файл **HomeController.cs** в редакторе Visual Studio и замените существующее определение пространства имен приведенным ниже кодом.</span><span class="sxs-lookup"><span data-stu-id="724cd-215">Now open the **HomeController.cs** file in the Visual Studio editor and replace the namespace definition with the following code.</span></span> <span data-ttu-id="724cd-216">Замените *yourServiceNamespace* на имя пространства имен вашей службы, а *yourKey* — на ключ SAS.</span><span class="sxs-lookup"><span data-stu-id="724cd-216">Be sure to replace *yourServiceNamespace* with the name of your service namespace, and *yourKey* with your SAS key.</span></span> <span data-ttu-id="724cd-217">Это позволит клиенту вызывать локальную службу, возвращая результат в вызов.</span><span class="sxs-lookup"><span data-stu-id="724cd-217">This will enable the client to call the on-premises service, returning the result of the call.</span></span>

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
           // Declare the channel factory.
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
                   // Return a view of the products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. <span data-ttu-id="724cd-218">В обозревателе решений щелкните правой кнопкой мыши решение **ProductsPortal** (не проект).</span><span class="sxs-lookup"><span data-stu-id="724cd-218">In Solution Explorer, right-click the **ProductsPortal** solution (make sure to right-click the solution, not the project).</span></span> <span data-ttu-id="724cd-219">Щелкните **Добавить**, а затем — **Существующий проект**.</span><span class="sxs-lookup"><span data-stu-id="724cd-219">Click **Add**, then click **Existing Project**.</span></span>
8. <span data-ttu-id="724cd-220">Перейдите к проекту **ProductsServer**, а затем дважды щелкните файл решения **ProductsServer.csproj**, чтобы добавить его.</span><span class="sxs-lookup"><span data-stu-id="724cd-220">Navigate to the **ProductsServer** project, then double-click the **ProductsServer.csproj** solution file to add it.</span></span>
9. <span data-ttu-id="724cd-221">Чтобы данные отобразились в решении **ProductsPortal**, нужно запустить проект **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="724cd-221">**ProductsServer** must be running in order to display the data on **ProductsPortal**.</span></span> <span data-ttu-id="724cd-222">В обозревателе решений щелкните правой кнопкой мыши решение **ProductsPortal** и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="724cd-222">In Solution Explorer, right-click the **ProductsPortal** solution and click **Properties**.</span></span> <span data-ttu-id="724cd-223">Откроется диалоговое окно **Страницы свойств**.</span><span class="sxs-lookup"><span data-stu-id="724cd-223">The **Property Pages** dialog box is displayed.</span></span>
10. <span data-ttu-id="724cd-224">В левой части окна выберите **Запускаемый проект**.</span><span class="sxs-lookup"><span data-stu-id="724cd-224">On the left side, click **Startup Project**.</span></span> <span data-ttu-id="724cd-225">В правой части окна выберите **Несколько запускаемых проектов**.</span><span class="sxs-lookup"><span data-stu-id="724cd-225">On the right side, click **Multiple startup projects**.</span></span> <span data-ttu-id="724cd-226">**ProductsServer** и **ProductsPortal** должны отображаться в указанном порядке с назначенным действием **Запустить**.</span><span class="sxs-lookup"><span data-stu-id="724cd-226">Ensure that **ProductsServer** and **ProductsPortal** appear, in that order, with **Start** set as the action for both.</span></span>

      ![][25]

11. <span data-ttu-id="724cd-227">В левой части диалогового окна **Свойства** щелкните **Зависимости проектов**.</span><span class="sxs-lookup"><span data-stu-id="724cd-227">Still in the **Properties** dialog box, click **Project Dependencies** on the left side.</span></span>
12. <span data-ttu-id="724cd-228">В списке **Проекты** выберите **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="724cd-228">In the **Projects** list, click **ProductsServer**.</span></span> <span data-ttu-id="724cd-229">Снимите флажок **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="724cd-229">Ensure that **ProductsPortal** is not selected.</span></span>
13. <span data-ttu-id="724cd-230">В списке **Проекты** выберите **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="724cd-230">In the **Projects** list, click **ProductsPortal**.</span></span> <span data-ttu-id="724cd-231">Установите флажок **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="724cd-231">Ensure that **ProductsServer** is selected.</span></span>

    ![][26]

14. <span data-ttu-id="724cd-232">В диалоговом окне **Страницы свойств** нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="724cd-232">Click **OK** in the **Property Pages** dialog box.</span></span>

## <a name="run-the-project-locally"></a><span data-ttu-id="724cd-233">Локальный запуск проекта</span><span class="sxs-lookup"><span data-stu-id="724cd-233">Run the project locally</span></span>

<span data-ttu-id="724cd-234">Чтобы проверить приложение локально, в окне Visual Studio нажмите клавишу **F5**.</span><span class="sxs-lookup"><span data-stu-id="724cd-234">To test the application locally, in Visual Studio press **F5**.</span></span> <span data-ttu-id="724cd-235">Первым должен запуститься локальный сервер (**ProductsServer**), а затем в окне браузера должно запуститься приложение **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="724cd-235">The on-premises server (**ProductsServer**) should start first, then the **ProductsPortal** application should start in a browser window.</span></span> <span data-ttu-id="724cd-236">На этот раз вы сможете проследить получение данных списка складских запасов продукции из локальной системы службы продукции.</span><span class="sxs-lookup"><span data-stu-id="724cd-236">This time, you will see that the product inventory lists data retrieved from the product service on-premises system.</span></span>

![][10]

<span data-ttu-id="724cd-237">На странице **ProductsPortal** нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="724cd-237">Press **Refresh** on the **ProductsPortal** page.</span></span> <span data-ttu-id="724cd-238">При каждом обновлении страницы после вызова `GetProducts()` из **ProductsServer** на сервере приложения будет отображаться сообщение.</span><span class="sxs-lookup"><span data-stu-id="724cd-238">Each time you refresh the page, you'll see the server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

<span data-ttu-id="724cd-239">Прежде чем перейти к следующему шагу, закройте оба приложения.</span><span class="sxs-lookup"><span data-stu-id="724cd-239">Close both applications before proceeding to the next step.</span></span>

## <a name="deploy-the-productsportal-project-to-an-azure-web-app"></a><span data-ttu-id="724cd-240">Развертывание проекта ProductsPortal в веб-приложении Azure</span><span class="sxs-lookup"><span data-stu-id="724cd-240">Deploy the ProductsPortal project to an Azure web app</span></span>

<span data-ttu-id="724cd-241">Следующий шаг — повторная публикация внешнего интерфейса **ProductsPortal** веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="724cd-241">The next step is to republish the Azure Web app **ProductsPortal** frontend.</span></span> <span data-ttu-id="724cd-242">Выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="724cd-242">Do the following:</span></span>

1. <span data-ttu-id="724cd-243">В обозревателе решений щелкните правой кнопкой мыши проект **ProductsPortal** и выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="724cd-243">In Solution Explorer, right-click the **ProductsPortal** project, and click **Publish**.</span></span> <span data-ttu-id="724cd-244">Затем на странице **Публикация** щелкните **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="724cd-244">Then, click **Publish** on the **Publish** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="724cd-245">Если веб-проект **ProductsPortal** запустится после развертывания автоматически, в окне браузера может появиться сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="724cd-245">You may see an error message in the browser window when the **ProductsPortal** web project is automatically launched after the deployment.</span></span> <span data-ttu-id="724cd-246">Это ожидаемое поведение, и означает, что приложение **ProductsServer** еще не запущено.</span><span class="sxs-lookup"><span data-stu-id="724cd-246">This is expected, and occurs because the **ProductsServer** application isn't running yet.</span></span>
>
>

2. <span data-ttu-id="724cd-247">Скопируйте URL-адрес развернутого веб-приложения, так как он понадобится для выполнения следующего шага.</span><span class="sxs-lookup"><span data-stu-id="724cd-247">Copy the URL of the deployed web app, as you will need the URL in the next step.</span></span> <span data-ttu-id="724cd-248">Кроме того, этот URL-адрес можно найти в окне "Действие службы приложений Azure" в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="724cd-248">You can also obtain this URL from the Azure App Service Activity window in Visual Studio:</span></span>

  ![][9]

3. <span data-ttu-id="724cd-249">Закройте окно браузера, чтобы остановить выполняющееся приложение.</span><span class="sxs-lookup"><span data-stu-id="724cd-249">Close the browser window to stop the running application.</span></span>

### <a name="set-productsportal-as-web-app"></a><span data-ttu-id="724cd-250">Настройка ProductsPortal в качестве веб-приложения</span><span class="sxs-lookup"><span data-stu-id="724cd-250">Set ProductsPortal as web app</span></span>

<span data-ttu-id="724cd-251">Перед запуском приложения в облаке необходимо, чтобы проект **ProductsPortal** в Visual Studio запускался как веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="724cd-251">Before running the application in the cloud, you must ensure that **ProductsPortal** is launched from within Visual Studio as a web app.</span></span>

1. <span data-ttu-id="724cd-252">В Visual Studio щелкните правой кнопкой мыши проект **ProductsPortal** и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="724cd-252">In Visual Studio, right-click the **ProductsPortal** project and then click **Properties**.</span></span>
2. <span data-ttu-id="724cd-253">В столбце слева щелкните **Веб**.</span><span class="sxs-lookup"><span data-stu-id="724cd-253">In the left-hand column, click **Web**.</span></span>
3. <span data-ttu-id="724cd-254">В разделе **Действие при запуске** нажмите кнопку **Начальный URL-адрес** и введите в текстовое поле URL-адрес развернутого ранее веб-приложения, например `http://productsportal1234567890.azurewebsites.net/`.</span><span class="sxs-lookup"><span data-stu-id="724cd-254">In the **Start Action** section, click the **Start URL** button, and in the text box enter the URL for your previously deployed web app; for example, `http://productsportal1234567890.azurewebsites.net/`.</span></span>

    ![][27]

4. <span data-ttu-id="724cd-255">В меню **Файл** Visual Studio выберите **Сохранить все**.</span><span class="sxs-lookup"><span data-stu-id="724cd-255">From the **File** menu in Visual Studio, click **Save All**.</span></span>
5. <span data-ttu-id="724cd-256">В Visual Studio в меню "Сборка" выберите **Пересобрать решение**.</span><span class="sxs-lookup"><span data-stu-id="724cd-256">From the Build menu in Visual Studio, click **Rebuild Solution**.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="724cd-257">Выполнение приложения</span><span class="sxs-lookup"><span data-stu-id="724cd-257">Run the application</span></span>

1. <span data-ttu-id="724cd-258">Нажмите клавишу F5, чтобы создать и запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="724cd-258">Press F5 to build and run the application.</span></span> <span data-ttu-id="724cd-259">Первым должен запуститься локальный сервер (консольное приложение **ProductsServer**), затем в окне браузера должно запуститься приложение **ProductsPortal**, как показано на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="724cd-259">The on-premises server (the **ProductsServer** console application) should start first, then the **ProductsPortal** application should start in a browser window, as shown in the following screen shot.</span></span> <span data-ttu-id="724cd-260">Обратите внимание, что в списке складских запасов продукции содержатся данные, полученные из локальной системы службы продукции, и они отображаются в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="724cd-260">Notice again that the product inventory lists data retrieved from the product service on-premises system, and displays that data in the web app.</span></span> <span data-ttu-id="724cd-261">Проверьте URL-адрес. Приложение **ProductsPortal** должно запускаться в облаке как веб-приложение Azure.</span><span class="sxs-lookup"><span data-stu-id="724cd-261">Check the URL to make sure that **ProductsPortal** is running in the cloud, as an Azure web app.</span></span>

   ![][1]

   > [!IMPORTANT]
   > <span data-ttu-id="724cd-262">Консольное приложение **ProductsServer** должно запускаться с возможностью передачи данных в приложение **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="724cd-262">The **ProductsServer** console application must be running and able to serve the data to the **ProductsPortal** application.</span></span> <span data-ttu-id="724cd-263">Если в браузере появляется сообщение об ошибке, подождите несколько секунд, пока **ProductsServer** загрузит и отобразит следующее сообщение.</span><span class="sxs-lookup"><span data-stu-id="724cd-263">If the browser displays an error, wait a few more seconds for **ProductsServer** to load and display the following message.</span></span> <span data-ttu-id="724cd-264">Затем нажмите кнопку **Обновить** в браузере.</span><span class="sxs-lookup"><span data-stu-id="724cd-264">Then press **Refresh** in the browser.</span></span>
   >
   >

   ![][37]
2. <span data-ttu-id="724cd-265">В браузере на странице **ProductsPortal** нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="724cd-265">Back in the browser, press **Refresh** on the **ProductsPortal** page.</span></span> <span data-ttu-id="724cd-266">При каждом обновлении страницы после вызова `GetProducts()` из **ProductsServer** на сервере приложения будет отображаться сообщение.</span><span class="sxs-lookup"><span data-stu-id="724cd-266">Each time you refresh the page, you'll see the server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

    ![][38]

## <a name="next-steps"></a><span data-ttu-id="724cd-267">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="724cd-267">Next steps</span></span>

<span data-ttu-id="724cd-268">Дополнительные сведения о ретрансляторе Azure см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="724cd-268">To learn more about Azure Relay, see the following resources:</span></span>  

* [<span data-ttu-id="724cd-269">Что такое ретранслятор Azure?</span><span class="sxs-lookup"><span data-stu-id="724cd-269">What is Azure Relay?</span></span>](relay-what-is-it.md)  
* [<span data-ttu-id="724cd-270">Как использовать ретранслятор</span><span class="sxs-lookup"><span data-stu-id="724cd-270">How to use Relay</span></span>](service-bus-dotnet-how-to-use-relay.md)  

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
