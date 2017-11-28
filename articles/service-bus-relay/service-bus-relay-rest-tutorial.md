---
title: "Руководство по REST служебной шины с использованием ретранслятора Azure | Документация Майкрософт"
description: "Создание простого ведущего приложения ретранслятора служебной шины Azure, которое предоставляет интерфейс на основе REST."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1312b2db-94c4-4a48-b815-c5deb5b77a6a
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2017
ms.author: sethm
ms.openlocfilehash: 0db9dbd2d2743907e3f0b259228201d4f5d0c3c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a><span data-ttu-id="556cf-103">Руководство по REST для ретранслятора WCF Azure</span><span class="sxs-lookup"><span data-stu-id="556cf-103">Azure WCF Relay REST tutorial</span></span>

<span data-ttu-id="556cf-104">В этом руководстве описано, как создать простое ведущее приложение ретранслятора Azure, предоставляющее интерфейс на основе REST.</span><span class="sxs-lookup"><span data-stu-id="556cf-104">This tutorial describes how to build a simple Azure Relay host application that exposes a REST-based interface.</span></span> <span data-ttu-id="556cf-105">REST позволяет веб-клиенту, например веб-браузеру, получить доступ к интерфейсам API служебной шины с помощью HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="556cf-105">REST enables a web client, such as a web browser, to access the Service Bus APIs through HTTP requests.</span></span>

<span data-ttu-id="556cf-106">В этом руководстве для создания службы REST в служебной шине используется модель программирования REST Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="556cf-106">The tutorial uses the Windows Communication Foundation (WCF) REST programming model to construct a REST service on Service Bus.</span></span> <span data-ttu-id="556cf-107">Дополнительные сведения см. в разделах [Модель программирования REST WCF](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) и [Разработка и реализация служб](/dotnet/framework/wcf/designing-and-implementing-services) в документации по WCF.</span><span class="sxs-lookup"><span data-stu-id="556cf-107">For more information, see [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) and [Designing and Implementing Services](/dotnet/framework/wcf/designing-and-implementing-services) in the WCF documentation.</span></span>

## <a name="step-1-create-a-namespace"></a><span data-ttu-id="556cf-108">Шаг 1. Создание пространства имен</span><span class="sxs-lookup"><span data-stu-id="556cf-108">Step 1: Create a namespace</span></span>

<span data-ttu-id="556cf-109">Чтобы начать использовать функции ретранслятора Azure, необходимо сначала создать пространство имен службы.</span><span class="sxs-lookup"><span data-stu-id="556cf-109">To begin using the relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="556cf-110">Пространство имен предоставляет контейнер для адресации ресурсов Azure в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="556cf-110">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="556cf-111">Выполните [эти инструкции](relay-create-namespace-portal.md), чтобы создать пространство имен ретранслятора.</span><span class="sxs-lookup"><span data-stu-id="556cf-111">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="step-2-define-a-rest-based-wcf-service-contract-to-use-with-azure-relay"></a><span data-ttu-id="556cf-112">Шаг 2. Определение контракта службы WCF на основе REST, используемого в ретрансляторе Azure</span><span class="sxs-lookup"><span data-stu-id="556cf-112">Step 2: Define a REST-based WCF service contract to use with Azure Relay</span></span>

<span data-ttu-id="556cf-113">При создании службы WCF на основе REST необходимо определить контракт.</span><span class="sxs-lookup"><span data-stu-id="556cf-113">When you create a WCF REST-style service, you must define the contract.</span></span> <span data-ttu-id="556cf-114">Контракт определяет, какие операции поддерживает узел.</span><span class="sxs-lookup"><span data-stu-id="556cf-114">The contract specifies what operations the host supports.</span></span> <span data-ttu-id="556cf-115">Операцию службы можно рассматривать как метод веб-службы.</span><span class="sxs-lookup"><span data-stu-id="556cf-115">A service operation can be thought of as a web service method.</span></span> <span data-ttu-id="556cf-116">Контракты создаются путем определения интерфейса C++, C# или Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="556cf-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="556cf-117">Каждый метод в интерфейсе соответствует определенной операции службы.</span><span class="sxs-lookup"><span data-stu-id="556cf-117">Each method in the interface corresponds to a specific service operation.</span></span> <span data-ttu-id="556cf-118">К каждому интерфейсу должен быть применен атрибут [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx), а к каждой операции — атрибут [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx).</span><span class="sxs-lookup"><span data-stu-id="556cf-118">The [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute must be applied to each interface, and the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute must be applied to each operation.</span></span> <span data-ttu-id="556cf-119">Если у метода в интерфейсе с атрибутом [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) нет атрибута [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), такой метод не предоставляется.</span><span class="sxs-lookup"><span data-stu-id="556cf-119">If a method in an interface that has the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) does not have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), that method is not exposed.</span></span> <span data-ttu-id="556cf-120">Код для выполнения этих задач показан в примере, приведенном после описания последовательности выполнения действий.</span><span class="sxs-lookup"><span data-stu-id="556cf-120">The code used for these tasks is shown in the example following the procedure.</span></span>

<span data-ttu-id="556cf-121">Основное различие между WCF и контрактом REST заключается в добавлении свойства к атрибуту [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span><span class="sxs-lookup"><span data-stu-id="556cf-121">The primary difference between a WCF contract and a REST-style contract is the addition of a property to the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span></span> <span data-ttu-id="556cf-122">Это свойство позволяет сопоставить метод в интерфейсе с методом на другой стороне интерфейса.</span><span class="sxs-lookup"><span data-stu-id="556cf-122">This property enables you to map a method in your interface to a method on the other side of the interface.</span></span> <span data-ttu-id="556cf-123">В нашем примере атрибут [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) используется для связывания метода с HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="556cf-123">In this case, we will use [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) to link a method to HTTP GET.</span></span> <span data-ttu-id="556cf-124">Это позволяет служебной шине точно извлекать и интерпретировать команды, отправляемые в интерфейс.</span><span class="sxs-lookup"><span data-stu-id="556cf-124">This allows Service Bus to accurately retrieve and interpret commands sent to the interface.</span></span>

### <a name="to-create-a-contract-with-an-interface"></a><span data-ttu-id="556cf-125">Создание контракта с помощью интерфейса</span><span class="sxs-lookup"><span data-stu-id="556cf-125">To create a contract with an interface</span></span>

1. <span data-ttu-id="556cf-126">Откройте Visual Studio с правами администратора, щелкнув программу правой кнопкой мыши в меню **Пуск** и выбрав **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="556cf-126">Open Visual Studio as an administrator: right-click the program in the **Start** menu, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="556cf-127">Создайте новый проект консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="556cf-127">Create a new console application project.</span></span> <span data-ttu-id="556cf-128">В меню **Файл** выберите **Создать**, а затем — **Проект**.</span><span class="sxs-lookup"><span data-stu-id="556cf-128">Click the **File** menu and select **New**, then select **Project**.</span></span> <span data-ttu-id="556cf-129">В диалоговом окне **Новый проект** щелкните **Visual C#**, выберите шаблон **Консольное приложение** и назовите его **ImageListener**.</span><span class="sxs-lookup"><span data-stu-id="556cf-129">In the **New Project** dialog box, click **Visual C#**, select the **Console Application** template, and name it **ImageListener**.</span></span> <span data-ttu-id="556cf-130">Используйте **расположение** по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="556cf-130">Use the default **Location**.</span></span> <span data-ttu-id="556cf-131">Нажмите кнопку **ОК** , чтобы создать проект.</span><span class="sxs-lookup"><span data-stu-id="556cf-131">Click **OK** to create the project.</span></span>
3. <span data-ttu-id="556cf-132">Для проекта C# в Visual Studio создается файл с именем `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="556cf-132">For a C# project, Visual Studio creates a `Program.cs` file.</span></span> <span data-ttu-id="556cf-133">Этот класс содержит пустой метод `Main()`, необходимый для правильной сборки проекта консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="556cf-133">This class contains an empty `Main()` method, required for a console application project to build correctly.</span></span>
4. <span data-ttu-id="556cf-134">Добавьте в проект ссылки на служебную шину и файл **System.ServiceModel.dll**. Для этого установите пакет NuGet для служебной шины.</span><span class="sxs-lookup"><span data-stu-id="556cf-134">Add references to Service Bus and **System.ServiceModel.dll** to the project by installing the Service Bus NuGet package.</span></span> <span data-ttu-id="556cf-135">Этот пакет автоматически добавляет ссылки на библиотеки служебной шины, а также элемент WCF **System.ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="556cf-135">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span></span> <span data-ttu-id="556cf-136">В обозревателе решений щелкните правой кнопкой мыши проект **ImageListener** и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="556cf-136">In Solution Explorer, right-click the **ImageListener** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="556cf-137">Щелкните вкладку **Обзор** и выполните поиск `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="556cf-137">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="556cf-138">Щелкните **Установить**и примите условия использования.</span><span class="sxs-lookup"><span data-stu-id="556cf-138">Click **Install**, and accept the terms of use.</span></span>
5. <span data-ttu-id="556cf-139">Явным образом добавьте в проект ссылку на библиотеку **System.ServiceModel.Web.dll**.</span><span class="sxs-lookup"><span data-stu-id="556cf-139">You must explicitly add a reference to **System.ServiceModel.Web.dll** to the project:</span></span>
   
    <span data-ttu-id="556cf-140">а.</span><span class="sxs-lookup"><span data-stu-id="556cf-140">a.</span></span> <span data-ttu-id="556cf-141">В обозревателе решений в папке проекта щелкните правой кнопкой мыши папку **Ссылки** и выберите **Добавить ссылку**.</span><span class="sxs-lookup"><span data-stu-id="556cf-141">In Solution Explorer, right-click the **References** folder under the project folder and then click **Add Reference**.</span></span>
   
    <span data-ttu-id="556cf-142">b.</span><span class="sxs-lookup"><span data-stu-id="556cf-142">b.</span></span> <span data-ttu-id="556cf-143">В диалоговом окне **Добавление ссылки** откройте вкладку **Платформа** в области слева и в поле **поиска** введите **System.ServiceModel.Web**.</span><span class="sxs-lookup"><span data-stu-id="556cf-143">In the **Add Reference** dialog box, click the **Framework** tab on the left-hand side and in the **Search** box, type **System.ServiceModel.Web**.</span></span> <span data-ttu-id="556cf-144">Установите флажок **System.ServiceModel.Web**, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="556cf-144">Select the **System.ServiceModel.Web** check box, then click **OK**.</span></span>
6. <span data-ttu-id="556cf-145">Добавьте следующие инструкции `using` в начало файла Program.cs.</span><span class="sxs-lookup"><span data-stu-id="556cf-145">Add the following `using` statements at the top of the Program.cs file.</span></span>
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    <span data-ttu-id="556cf-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) — это пространство имен, которое предоставляет программный доступ к основным функциям WCF.</span><span class="sxs-lookup"><span data-stu-id="556cf-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is the namespace that enables programmatic access to basic features of WCF.</span></span> <span data-ttu-id="556cf-147">Ретранслятор WCF использует множество объектов и атрибутов WCF для определения контрактов службы.</span><span class="sxs-lookup"><span data-stu-id="556cf-147">WCF Relay uses many of the objects and attributes of WCF to define service contracts.</span></span> <span data-ttu-id="556cf-148">Это пространство имен будет использоваться в большинстве приложений ретранслятора.</span><span class="sxs-lookup"><span data-stu-id="556cf-148">You will use this namespace in most of your relay applications.</span></span> <span data-ttu-id="556cf-149">Аналогичным образом [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) помогает определить канал, т. е. объект, посредством которого ретранслятор Azure взаимодействует с веб-браузером клиента.</span><span class="sxs-lookup"><span data-stu-id="556cf-149">Similarly, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helps define the channel, which is the object through which you communicate with Azure Relay and the client web browser.</span></span> <span data-ttu-id="556cf-150">Наконец, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) содержит типы, позволяющие создавать веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="556cf-150">Finally, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contains the types that enable you to create web-based applications.</span></span>
7. <span data-ttu-id="556cf-151">Переименуйте пространство имен `ImageListener` в **Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="556cf-151">Rename the `ImageListener` namespace to **Microsoft.ServiceBus.Samples**.</span></span>
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. <span data-ttu-id="556cf-152">Сразу после открывающей фигурной скобки в объявлении пространства имен определите новый интерфейс с именем **IImageContract** и примените к нему атрибут **ServiceContractAttribute** со значением `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="556cf-152">Directly after the opening curly brace of the namespace declaration, define a new interface named **IImageContract** and apply the **ServiceContractAttribute** attribute to the interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="556cf-153">Значение пространства имен отличается от пространства имен, которое используется во всей области кода.</span><span class="sxs-lookup"><span data-stu-id="556cf-153">The namespace value differs from the namespace that you use throughout the scope of your code.</span></span> <span data-ttu-id="556cf-154">Значение пространства имен служит в качестве уникального идентификатора для данного контракта и должно содержать сведения о версии.</span><span class="sxs-lookup"><span data-stu-id="556cf-154">The namespace value is used as a unique identifier for this contract, and should have version information.</span></span> <span data-ttu-id="556cf-155">Дополнительные сведения см. в статье [Управление версиями службы](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="556cf-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="556cf-156">Явное указание пространства позволяет предотвратить добавление значение пространства имен по умолчанию к имени контракта.</span><span class="sxs-lookup"><span data-stu-id="556cf-156">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span></span>
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. <span data-ttu-id="556cf-157">В интерфейсе `IImageContract` объявите метод для отдельной операции, которую контракт `IImageContract` предоставляет в интерфейсе. Затем примените атрибут `OperationContractAttribute` к методу, который требуется предоставить как часть открытого контракта служебной шины.</span><span class="sxs-lookup"><span data-stu-id="556cf-157">Within the `IImageContract` interface, declare a method for the single operation the `IImageContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public Service Bus contract.</span></span>
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. <span data-ttu-id="556cf-158">В атрибут **OperationContract** добавьте значение **WebGet**.</span><span class="sxs-lookup"><span data-stu-id="556cf-158">In the **OperationContract** attribute, add the **WebGet** value.</span></span>
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    <span data-ttu-id="556cf-159">Это позволит службе ретрансляции перенаправлять HTTP-запросы GET в `GetImage` и преобразовывать возвращаемые значения `GetImage` в HTTP-ответ GETRESPONSE.</span><span class="sxs-lookup"><span data-stu-id="556cf-159">Doing so enables the relay service to route HTTP GET requests to `GetImage`, and to translate the return values of `GetImage` into an HTTP GETRESPONSE reply.</span></span> <span data-ttu-id="556cf-160">Далее в этом учебнике для доступа к этому методу и отображения изображения в браузере будет использоваться веб-браузер.</span><span class="sxs-lookup"><span data-stu-id="556cf-160">Later in the tutorial, you will use a web browser to access this method, and to display the image in the browser.</span></span>
11. <span data-ttu-id="556cf-161">Сразу после определения `IImageContract` объявите канал, наследующий от интерфейсов `IImageContract` и `IClientChannel`.</span><span class="sxs-lookup"><span data-stu-id="556cf-161">Directly after the `IImageContract` definition, declare a channel that inherits from both the `IImageContract` and `IClientChannel` interfaces.</span></span>
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    <span data-ttu-id="556cf-162">Канал представляет собой объект WCF, посредством которого служба и клиент обмениваются информацией.</span><span class="sxs-lookup"><span data-stu-id="556cf-162">A channel is the WCF object through which the service and client pass information to each other.</span></span> <span data-ttu-id="556cf-163">Канал в своем хост-приложении вы создадите позже.</span><span class="sxs-lookup"><span data-stu-id="556cf-163">Later, you will create the channel in your host application.</span></span> <span data-ttu-id="556cf-164">Ретранслятор Azure использует этот канал для передачи HTTP-запросов GET из браузера в реализацию **GetImage**.</span><span class="sxs-lookup"><span data-stu-id="556cf-164">Azure Relay then uses this channel to pass the HTTP GET requests from the browser to your **GetImage** implementation.</span></span> <span data-ttu-id="556cf-165">Канал также требуется ретранслятору для получения возвращаемого значения **GetImage** и его преобразования в HTTP-ответ GETRESPONSE для браузера клиента.</span><span class="sxs-lookup"><span data-stu-id="556cf-165">The relay also uses the channel to take the **GetImage** return value and translate it into an HTTP GETRESPONSE for the client browser.</span></span>
12. <span data-ttu-id="556cf-166">В меню **Сборка** щелкните **Построить решение**, чтобы проверить правильность выполнения действий.</span><span class="sxs-lookup"><span data-stu-id="556cf-166">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="556cf-167">Пример</span><span class="sxs-lookup"><span data-stu-id="556cf-167">Example</span></span>
<span data-ttu-id="556cf-168">Ниже приведен код базового интерфейса, определяющего контракт ретранслятора WCF.</span><span class="sxs-lookup"><span data-stu-id="556cf-168">The following code shows a basic interface that defines a WCF Relay contract.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="step-3-implement-a-rest-based-wcf-service-contract-to-use-service-bus"></a><span data-ttu-id="556cf-169">Шаг 3. Реализуйте контракт службы WCF на основе REST, используемого в служебной шине</span><span class="sxs-lookup"><span data-stu-id="556cf-169">Step 3: Implement a REST-based WCF service contract to use Service Bus</span></span>
<span data-ttu-id="556cf-170">Перед созданием службы ретрансляции WCF на основе REST необходимо сначала создать контракт, который определяется с помощью интерфейса.</span><span class="sxs-lookup"><span data-stu-id="556cf-170">Creating a REST-style WCF Relay service requires that you first create the contract, which is defined by using an interface.</span></span> <span data-ttu-id="556cf-171">Следующим шагом является реализация интерфейса.</span><span class="sxs-lookup"><span data-stu-id="556cf-171">The next step is to implement the interface.</span></span> <span data-ttu-id="556cf-172">Она предполагает создание класса с именем **ImageService**, который реализует пользовательский интерфейс **IImageContract**.</span><span class="sxs-lookup"><span data-stu-id="556cf-172">This involves creating a class named **ImageService** that implements the user-defined **IImageContract** interface.</span></span> <span data-ttu-id="556cf-173">После реализации контракта необходимо настроить интерфейс с помощью файла App.config.</span><span class="sxs-lookup"><span data-stu-id="556cf-173">After you implement the contract, you then configure the interface using an App.config file.</span></span> <span data-ttu-id="556cf-174">Файл конфигурации содержит сведения, необходимые для приложения, такие как имя службы, имя контракта и тип протокола, используемого для взаимодействия с службой ретрансляции.</span><span class="sxs-lookup"><span data-stu-id="556cf-174">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span></span> <span data-ttu-id="556cf-175">Код для выполнения этих задач приведен в примере после описания последовательности выполнения действий.</span><span class="sxs-lookup"><span data-stu-id="556cf-175">The code used for these tasks is provided in the example following the procedure.</span></span>

<span data-ttu-id="556cf-176">Как и на предыдущих шагах, разница между реализацией контракта REST и контракта ретранслятора WCF невелика.</span><span class="sxs-lookup"><span data-stu-id="556cf-176">As with the previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span></span>

### <a name="to-implement-a-rest-style-service-bus-contract"></a><span data-ttu-id="556cf-177">Реализация контракта REST служебной шины</span><span class="sxs-lookup"><span data-stu-id="556cf-177">To implement a REST-style Service Bus contract</span></span>
1. <span data-ttu-id="556cf-178">Создайте новый класс с именем **ImageService** сразу после определения интерфейса **IImageContract**.</span><span class="sxs-lookup"><span data-stu-id="556cf-178">Create a new class named **ImageService** directly after the definition of the **IImageContract** interface.</span></span> <span data-ttu-id="556cf-179">Класс **ImageService** реализует интерфейс **IImageContract**.</span><span class="sxs-lookup"><span data-stu-id="556cf-179">The **ImageService** class implements the **IImageContract** interface.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    <span data-ttu-id="556cf-180">Как и в случае с другими реализациями интерфейсов, определение можно реализовать в другом файле.</span><span class="sxs-lookup"><span data-stu-id="556cf-180">Similar to other interface implementations, you can implement the definition in a different file.</span></span> <span data-ttu-id="556cf-181">Но в этом руководстве реализация осуществляется в том же файле, что и определение интерфейса и метод `Main()`.</span><span class="sxs-lookup"><span data-stu-id="556cf-181">However, for this tutorial, the implementation appears in the same file as the interface definition and `Main()` method.</span></span>
2. <span data-ttu-id="556cf-182">Примените атрибут [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) к классу **IImageService**, чтобы указать, что класс является реализацией контракта WCF.</span><span class="sxs-lookup"><span data-stu-id="556cf-182">Apply the [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute to the **IImageService** class to indicate that the class is an implementation of a WCF contract.</span></span>
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    <span data-ttu-id="556cf-183">Как упоминалось ранее, это пространство имен не является обычным.</span><span class="sxs-lookup"><span data-stu-id="556cf-183">As mentioned previously, this namespace is not a traditional namespace.</span></span> <span data-ttu-id="556cf-184">Оно является частью архитектуры WCF, которая идентифицирует контракт.</span><span class="sxs-lookup"><span data-stu-id="556cf-184">Instead, it is part of the WCF architecture that identifies the contract.</span></span> <span data-ttu-id="556cf-185">Дополнительные сведения см. в разделе [Имена контрактов данных](https://msdn.microsoft.com/library/ms731045.aspx) документации по WCF.</span><span class="sxs-lookup"><span data-stu-id="556cf-185">For more information, see the [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) topic in the WCF documentation.</span></span>
3. <span data-ttu-id="556cf-186">Добавьте в проект изображение в формате JPG.</span><span class="sxs-lookup"><span data-stu-id="556cf-186">Add a .jpg image to your project.</span></span>  
   
    <span data-ttu-id="556cf-187">Это рисунок, отображаемый службой в браузере-получателе.</span><span class="sxs-lookup"><span data-stu-id="556cf-187">This is a picture that the service displays in the receiving browser.</span></span> <span data-ttu-id="556cf-188">Щелкните проект правой кнопкой мыши и выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="556cf-188">Right-click your project, then click **Add**.</span></span> <span data-ttu-id="556cf-189">Затем выберите **Существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="556cf-189">Then click **Existing Item**.</span></span> <span data-ttu-id="556cf-190">В диалоговом окне **Добавление существующего элемента** найдите необходимый файл в формате JPG и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="556cf-190">Use the **Add Existing Item** dialog box to browse to an appropriate .jpg, and then click **Add**.</span></span>
   
    <span data-ttu-id="556cf-191">При добавлении файла убедитесь, что в раскрывающемся списке рядом с полем **Имя файла** выбран пункт **Все файлы**.</span><span class="sxs-lookup"><span data-stu-id="556cf-191">When adding the file, make sure that **All Files** is selected in the drop-down list next to the **File name:** field.</span></span> <span data-ttu-id="556cf-192">Далее в этом учебнике предполагается, что изображение называется image.jpg.</span><span class="sxs-lookup"><span data-stu-id="556cf-192">The rest of this tutorial assumes that the name of the image is "image.jpg".</span></span> <span data-ttu-id="556cf-193">При использовании другого файла необходимо переименовать изображение или изменить код соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="556cf-193">If you have a different file, you will have to rename the image, or change your code to compensate.</span></span>
4. <span data-ttu-id="556cf-194">Чтобы убедиться, что запущенная служба может найти файл изображения, в **обозревателе решений** щелкните файл изображения правой кнопкой мыши, а затем выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="556cf-194">To make sure that the running service can find the image file, in **Solution Explorer** right-click the image file, then click **Properties**.</span></span> <span data-ttu-id="556cf-195">На панели **Свойства** задайте для параметра **Копировать в выходной каталог** значение **Копировать, если новее**.</span><span class="sxs-lookup"><span data-stu-id="556cf-195">In the **Properties** pane, set **Copy to Output Directory** to **Copy if newer**.</span></span>
5. <span data-ttu-id="556cf-196">Добавьте в проект ссылку на сборку **System.Drawing.dll** и добавьте следующие связанные инструкции `using`.</span><span class="sxs-lookup"><span data-stu-id="556cf-196">Add a reference to the **System.Drawing.dll** assembly to the project, and also add the following associated `using` statements.</span></span>  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. <span data-ttu-id="556cf-197">В классе **ImageService** добавьте следующий конструктор, который загружает точечный рисунок и подготавливает его для отправки в браузер клиента.</span><span class="sxs-lookup"><span data-stu-id="556cf-197">In the **ImageService** class, add the following constructor that loads the bitmap and prepares to send it to the client browser.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";
   
        Image bitmap;
   
        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }
    }
    ```
7. <span data-ttu-id="556cf-198">Сразу после предыдущего кода добавьте следующий метод **GetImage** в класс **ImageService** для возврата HTTP-сообщения, содержащего изображение.</span><span class="sxs-lookup"><span data-stu-id="556cf-198">Directly after the previous code, add the following **GetImage** method in the **ImageService** class to return an HTTP message that contains the image.</span></span>
   
    ```csharp
    public Stream GetImage()
    {
        MemoryStream stream = new MemoryStream();
        this.bitmap.Save(stream, ImageFormat.Jpeg);
   
        stream.Position = 0;
        WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
   
        return stream;
    }
    ```
   
    <span data-ttu-id="556cf-199">Эта реализация использует класс **MemoryStream** для извлечения изображения и его подготовки к потоковой передаче в браузер.</span><span class="sxs-lookup"><span data-stu-id="556cf-199">This implementation uses **MemoryStream** to retrieve the image and prepare it for streaming to the browser.</span></span> <span data-ttu-id="556cf-200">Он начинает позицию потока с нуля, объявляет содержимое потока как jpeg и передает информацию.</span><span class="sxs-lookup"><span data-stu-id="556cf-200">It starts the stream position at zero, declares the stream content as a jpeg, and streams the information.</span></span>
8. <span data-ttu-id="556cf-201">В меню **Сборка** выберите **Построить решение**.</span><span class="sxs-lookup"><span data-stu-id="556cf-201">From the **Build** menu, click **Build Solution**.</span></span>

### <a name="to-define-the-configuration-for-running-the-web-service-on-service-bus"></a><span data-ttu-id="556cf-202">Определение конфигурации для запуска веб-службы в служебной шине</span><span class="sxs-lookup"><span data-stu-id="556cf-202">To define the configuration for running the web service on Service Bus</span></span>
1. <span data-ttu-id="556cf-203">В **обозревателе решений** дважды щелкните файл **App.config**, чтобы открыть его в редакторе Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="556cf-203">In **Solution Explorer**, double-click **App.config** to open it in the Visual Studio editor.</span></span>
   
    <span data-ttu-id="556cf-204">Файл **App.config** также содержит имя службы, конечную точку (то есть расположение, которое ретранслятор Azure предоставляет клиентам и узлам для взаимодействия) и привязку (тип протокола, используемый для связи).</span><span class="sxs-lookup"><span data-stu-id="556cf-204">The **App.config** file includes the service name, endpoint (that is, the location Azure Relay exposes for clients and hosts to communicate with each other), and binding (the type of protocol that is used to communicate).</span></span> <span data-ttu-id="556cf-205">Основное различие состоит в том, что настроенная конечная точка службы ссылается на привязку [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding).</span><span class="sxs-lookup"><span data-stu-id="556cf-205">The main difference here is that the configured service endpoint refers to a [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span></span>
2. <span data-ttu-id="556cf-206">Элемент XML `<system.serviceModel>` представляет собой элемент WCF, определяющий одну или несколько служб.</span><span class="sxs-lookup"><span data-stu-id="556cf-206">The `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span></span> <span data-ttu-id="556cf-207">Здесь он используется для определения имени службы и конечной точки.</span><span class="sxs-lookup"><span data-stu-id="556cf-207">Here, it is used to define the service name and endpoint.</span></span> <span data-ttu-id="556cf-208">В нижней части элемента `<system.serviceModel>` (но не выходя за рамки элемента `<system.serviceModel>`) добавьте элемент `<bindings>` с указанным ниже содержимым.</span><span class="sxs-lookup"><span data-stu-id="556cf-208">At the bottom of the `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has the following content.</span></span> <span data-ttu-id="556cf-209">Оно определяет привязки, используемые в приложении.</span><span class="sxs-lookup"><span data-stu-id="556cf-209">This defines the bindings used in the application.</span></span> <span data-ttu-id="556cf-210">Можно определить несколько привязок, но в этом учебнике определяется только одна.</span><span class="sxs-lookup"><span data-stu-id="556cf-210">You can define multiple bindings, but for this tutorial you are defining only one.</span></span>
   
    ```xml
    <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
            <binding name="default">
                <security relayClientAuthenticationType="None" />
            </binding>
        </webHttpRelayBinding>
    </bindings>
    ```
   
    <span data-ttu-id="556cf-211">Предыдущий код определяет привязку [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) ретранслятора WCF, в которой для свойства **relayClientAuthenticationType** установлено значение **None**.</span><span class="sxs-lookup"><span data-stu-id="556cf-211">The previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set to **None**.</span></span> <span data-ttu-id="556cf-212">Этот параметр указывает, что для конечной точки, использующей эту привязку, не требуются учетные данные клиента.</span><span class="sxs-lookup"><span data-stu-id="556cf-212">This setting indicates that an endpoint using this binding does not require a client credential.</span></span>
3. <span data-ttu-id="556cf-213">После элемента `<bindings>` добавьте элемент `<services>`.</span><span class="sxs-lookup"><span data-stu-id="556cf-213">After the `<bindings>` element, add a `<services>` element.</span></span> <span data-ttu-id="556cf-214">Как и в случае с привязками, в одном файле конфигурации можно определить несколько служб.</span><span class="sxs-lookup"><span data-stu-id="556cf-214">Similar to the bindings, you can define multiple services in a single configuration file.</span></span> <span data-ttu-id="556cf-215">Но в этом учебнике определяется только одна.</span><span class="sxs-lookup"><span data-stu-id="556cf-215">However, for this tutorial, you define only one.</span></span>
   
    ```xml
    <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
            <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IImageContract"
                    binding="webHttpRelayBinding"
                    bindingConfiguration="default"
                    behaviorConfiguration="sbTokenProvider"
                    address="" />
        </service>
    </services>
    ```
   
    <span data-ttu-id="556cf-216">На этом этапе выполняется настройка службы, которая использует заданную ранее привязку по умолчанию **webHttpRelayBinding**.</span><span class="sxs-lookup"><span data-stu-id="556cf-216">This step configures a service that uses the previously defined default **webHttpRelayBinding**.</span></span> <span data-ttu-id="556cf-217">Здесь также используется значение по умолчанию **sbTokenProvider**, которое будет определено на следующем этапе.</span><span class="sxs-lookup"><span data-stu-id="556cf-217">It also uses the default **sbTokenProvider**, which is defined in the next step.</span></span>
4. <span data-ttu-id="556cf-218">После элемента `<services>` создайте элемент `<behaviors>` с указанным ниже содержимым, заменив SAS_KEY ключом *подписанного URL-адреса* (SAS), полученным ранее [на портале Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="556cf-218">After the `<services>` element, create a `<behaviors>` element with the following content, replacing "SAS_KEY" with the *Shared Access Signature* (SAS) key you previously obtained from the [Azure portal][Azure portal].</span></span>
   
    ```xml
    <behaviors>
        <endpointBehaviors>
            <behavior name="sbTokenProvider">
                <transportClientEndpointBehavior>
                    <tokenProvider>
                        <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
                    </tokenProvider>
                </transportClientEndpointBehavior>
            </behavior>
            </endpointBehaviors>
            <serviceBehaviors>
                <behavior name="default">
                    <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
                </behavior>
            </serviceBehaviors>
    </behaviors>
    ```
5. <span data-ttu-id="556cf-219">В файле App.config в элементе `<appSettings>` целиком замените значение строки подключения значением, полученным ранее на портале.</span><span class="sxs-lookup"><span data-stu-id="556cf-219">Still in App.config, in the `<appSettings>` element, replace the entire connection string value with the connection string you previously obtained from the portal.</span></span> 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. <span data-ttu-id="556cf-220">В меню **Сборка** выберите **Построить решение**, чтобы создать решение полностью.</span><span class="sxs-lookup"><span data-stu-id="556cf-220">From the **Build** menu, click **Build Solution** to build the entire solution.</span></span>

### <a name="example"></a><span data-ttu-id="556cf-221">Пример</span><span class="sxs-lookup"><span data-stu-id="556cf-221">Example</span></span>
<span data-ttu-id="556cf-222">В следующем коде показана реализация контракта и службы для службы REST, запущенной в служебной шине с помощью привязки **WebHttpRelayBinding**.</span><span class="sxs-lookup"><span data-stu-id="556cf-222">The following code shows the contract and service implementation for a REST-based service that is running on  Service Bus using the **WebHttpRelayBinding** binding.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{


    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

<span data-ttu-id="556cf-223">Ниже представлен пример файла App.config, связанного со службой.</span><span class="sxs-lookup"><span data-stu-id="556cf-223">The following example shows the App.config file associated with the service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove the ones they don't need. -->
            <behaviorExtensions>
                <add name="connectionStatusBehavior"
                    type="Microsoft.ServiceBus.Configuration.ConnectionStatusElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="transportClientEndpointBehavior"
                    type="Microsoft.ServiceBus.Configuration.TransportClientEndpointBehaviorElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="serviceRegistrySettings"
                    type="Microsoft.ServiceBus.Configuration.ServiceRegistrySettingsElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </behaviorExtensions>
            <bindingElementExtensions>
                <add name="netMessagingTransport"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingTransportExtensionElement, Microsoft.ServiceBus,  Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="tcpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.TcpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpsRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpsRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="onewayRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.RelayedOnewayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingElementExtensions>
            <bindingExtensions>
                <add name="basicHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.BasicHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="webHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WebHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="ws2007HttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WS2007HttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netOnewayRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetOnewayRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netEventRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetEventRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netMessagingBinding"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingExtensions>
        </extensions>
      <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
          <binding name="default">
            <security relayClientAuthenticationType="None" />
          </binding>
        </webHttpRelayBinding>
      </bindings>
      <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
          <endpoint name="RelayEndpoint"
                  contract="Microsoft.ServiceBus.Samples.IImageContract"
                  binding="webHttpRelayBinding"
                  bindingConfiguration="default"
                  behaviorConfiguration="sbTokenProvider"
                  address="" />
        </service>
      </services>
      <behaviors>
        <endpointBehaviors>
          <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
        <serviceBehaviors>
          <behavior name="default">
            <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
          </behavior>
        </serviceBehaviors>
      </behaviors>
    </system.serviceModel>
    <appSettings>
        <!-- Service Bus specific app setings for messaging connections -->
        <add key="Microsoft.ServiceBus.ConnectionString"
            value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey="YOUR_SAS_KEY"/>
    </appSettings>
</configuration>
```

## <a name="step-4-host-the-rest-based-wcf-service-to-use-azure-relay"></a><span data-ttu-id="556cf-224">Шаг 4. Размещение службы WCF на основе REST для использования ретранслятора Azure</span><span class="sxs-lookup"><span data-stu-id="556cf-224">Step 4: Host the REST-based WCF service to use Azure Relay</span></span>
<span data-ttu-id="556cf-225">В этом разделе описан запуск веб-службы с помощью консольного приложения и ретранслятора WCF.</span><span class="sxs-lookup"><span data-stu-id="556cf-225">This step describes how to run a web service using a console application with WCF Relay.</span></span> <span data-ttu-id="556cf-226">Полный код этого шага представлен в примере после описания последовательности выполнения действий.</span><span class="sxs-lookup"><span data-stu-id="556cf-226">A complete listing of the code written in this step is provided in the example following the procedure.</span></span>

### <a name="to-create-a-base-address-for-the-service"></a><span data-ttu-id="556cf-227">Создание базового адреса для службы</span><span class="sxs-lookup"><span data-stu-id="556cf-227">To create a base address for the service</span></span>
1. <span data-ttu-id="556cf-228">В объявлении функции `Main()` создайте переменную для хранения пространства имен своего проекта.</span><span class="sxs-lookup"><span data-stu-id="556cf-228">In the `Main()` function declaration, create a variable to store the namespace of your project.</span></span> <span data-ttu-id="556cf-229">Не забудьте заменить `yourNamespace` именем созданного ранее пространства имен ретранслятора.</span><span class="sxs-lookup"><span data-stu-id="556cf-229">Make sure to replace `yourNamespace` with the name of the Relay namespace you created previously.</span></span>
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    <span data-ttu-id="556cf-230">Пространство имен используется в служебной шине для создания уникального URI.</span><span class="sxs-lookup"><span data-stu-id="556cf-230">Service Bus uses the name of your namespace to create a unique URI.</span></span>
2. <span data-ttu-id="556cf-231">Создайте экземпляр `Uri` для базового адреса службы на основе пространства имен.</span><span class="sxs-lookup"><span data-stu-id="556cf-231">Create a `Uri` instance for the base address of the service that is based on the namespace.</span></span>
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="to-create-and-configure-the-web-service-host"></a><span data-ttu-id="556cf-232">Создание и настройка узла веб-службы</span><span class="sxs-lookup"><span data-stu-id="556cf-232">To create and configure the web service host</span></span>
* <span data-ttu-id="556cf-233">Создайте узел веб-службы с помощью URI-адреса, созданного на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="556cf-233">Create the web service host, using the URI address created earlier in this section.</span></span>
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    <span data-ttu-id="556cf-234">Узел службы представляет собой объект WCF, который создает экземпляры хост-приложения.</span><span class="sxs-lookup"><span data-stu-id="556cf-234">The service host is the WCF object that instantiates the host application.</span></span> <span data-ttu-id="556cf-235">В этом примере ему передаются тип создаваемого узла (**ImageService**) и адрес, по которому предоставляется ведущее приложение.</span><span class="sxs-lookup"><span data-stu-id="556cf-235">This example passes it the type of host you want to create (an **ImageService**), and also the address at which you want to expose the host application.</span></span>

### <a name="to-run-the-web-service-host"></a><span data-ttu-id="556cf-236">Запуск узла веб-службы</span><span class="sxs-lookup"><span data-stu-id="556cf-236">To run the web service host</span></span>
1. <span data-ttu-id="556cf-237">Откройте службу.</span><span class="sxs-lookup"><span data-stu-id="556cf-237">Open the service.</span></span>
   
    ```csharp
    host.Open();
    ```
    <span data-ttu-id="556cf-238">Теперь служба запущена.</span><span class="sxs-lookup"><span data-stu-id="556cf-238">The service is now running.</span></span>
2. <span data-ttu-id="556cf-239">Отобразите сообщение о том, что служба запущена, и о том, как остановить ее.</span><span class="sxs-lookup"><span data-stu-id="556cf-239">Display a message indicating that the service is running, and how to stop the service.</span></span>
   
    ```csharp
    Console.WriteLine("Copy the following address into a browser to see the image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] to exit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="556cf-240">После завершения закройте узел службы.</span><span class="sxs-lookup"><span data-stu-id="556cf-240">When finished, close the service host.</span></span>
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a><span data-ttu-id="556cf-241">Пример</span><span class="sxs-lookup"><span data-stu-id="556cf-241">Example</span></span>
<span data-ttu-id="556cf-242">В следующем примере показаны контракт и реализация службы, созданные на предыдущих шагах, а также размещение службы в консольном приложении.</span><span class="sxs-lookup"><span data-stu-id="556cf-242">The following example includes the service contract and implementation from previous steps in the tutorial and hosts the service in a console application.</span></span> <span data-ttu-id="556cf-243">Скомпилируйте следующий код в исполняемый файл с именем "ImageListener.exe":</span><span class="sxs-lookup"><span data-stu-id="556cf-243">Compile the following code into an executable named ImageListener.exe.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string serviceNamespace = "InsertServiceNamespaceHere";
            Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");

            WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
            host.Open();

            Console.WriteLine("Copy the following address into a browser to see the image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] to exit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-the-code"></a><span data-ttu-id="556cf-244">Компиляция кода</span><span class="sxs-lookup"><span data-stu-id="556cf-244">Compiling the code</span></span>
<span data-ttu-id="556cf-245">После построения решения выполните следующие действия, чтобы запустить приложение:</span><span class="sxs-lookup"><span data-stu-id="556cf-245">After building the solution, do the following to run the application:</span></span>

1. <span data-ttu-id="556cf-246">Нажмите клавишу **F5** или перейдите в расположение исполняемого файла (ImageListener\bin\Debug\ImageListener.exe), чтобы запустить службу.</span><span class="sxs-lookup"><span data-stu-id="556cf-246">Press **F5**, or browse to the executable file location (ImageListener\bin\Debug\ImageListener.exe), to run the service.</span></span> <span data-ttu-id="556cf-247">Оставьте приложение в работающем состоянии, так как это необходимо для выполнения следующего этапа.</span><span class="sxs-lookup"><span data-stu-id="556cf-247">Keep the app running, as it's required to perform the next step.</span></span>
2. <span data-ttu-id="556cf-248">Скопируйте из командной строки адрес и вставьте его в браузере, чтобы увидеть изображение.</span><span class="sxs-lookup"><span data-stu-id="556cf-248">Copy and paste the address from the command prompt into a browser to see the image.</span></span>
3. <span data-ttu-id="556cf-249">По завершении откройте окно командной строки и нажмите клавишу **ВВОД**, чтобы закрыть приложение.</span><span class="sxs-lookup"><span data-stu-id="556cf-249">When you are finished, press **Enter** in the command prompt window to close the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="556cf-250">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="556cf-250">Next steps</span></span>
<span data-ttu-id="556cf-251">Вы научились создавать приложение, которое использует службу ретранслятора служебной шины. Дополнительные сведения о ретрансляторе Azure можно найти в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="556cf-251">Now that you've built an application that uses the Service Bus relay service, see the following articles to learn more about Azure Relay:</span></span>

* [<span data-ttu-id="556cf-252">Обзор архитектуры служебной шины Azure</span><span class="sxs-lookup"><span data-stu-id="556cf-252">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="556cf-253">Что такое ретранслятор Azure?</span><span class="sxs-lookup"><span data-stu-id="556cf-253">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="556cf-254">Как использовать ретранслятор WCF служебной шины с .NET</span><span class="sxs-lookup"><span data-stu-id="556cf-254">How to use the WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
