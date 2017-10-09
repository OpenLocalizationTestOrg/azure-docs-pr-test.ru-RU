---
title: "Учебник по REST шины aaaService, с помощью ретрансляции Azure | Документы Microsoft"
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
ms.openlocfilehash: b68650993a0390e7cef891ccb4236095cd86d4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a><span data-ttu-id="00fae-103">Руководство по REST для ретранслятора WCF Azure</span><span class="sxs-lookup"><span data-stu-id="00fae-103">Azure WCF Relay REST tutorial</span></span>

<span data-ttu-id="00fae-104">В данном учебнике как toobuild простой ретранслятор Azure размещения приложения, предоставляющего интерфейс на основе REST.</span><span class="sxs-lookup"><span data-stu-id="00fae-104">This tutorial describes how toobuild a simple Azure Relay host application that exposes a REST-based interface.</span></span> <span data-ttu-id="00fae-105">REST позволяет веб-клиента, такие как веб-браузер, hello tooaccess интерфейсов API служебной шины по протоколу HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="00fae-105">REST enables a web client, such as a web browser, tooaccess hello Service Bus APIs through HTTP requests.</span></span>

<span data-ttu-id="00fae-106">Учебник Hello использует tooconstruct программирования модели hello REST Windows Communication Foundation (WCF) к службе REST Service Bus.</span><span class="sxs-lookup"><span data-stu-id="00fae-106">hello tutorial uses hello Windows Communication Foundation (WCF) REST programming model tooconstruct a REST service on Service Bus.</span></span> <span data-ttu-id="00fae-107">Дополнительные сведения см. в разделе [модель программирования WCF REST](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) и [проектирование и реализация служб](/dotnet/framework/wcf/designing-and-implementing-services) в документации по WCF hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-107">For more information, see [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) and [Designing and Implementing Services](/dotnet/framework/wcf/designing-and-implementing-services) in hello WCF documentation.</span></span>

## <a name="step-1-create-a-namespace"></a><span data-ttu-id="00fae-108">Шаг 1. Создание пространства имен</span><span class="sxs-lookup"><span data-stu-id="00fae-108">Step 1: Create a namespace</span></span>

<span data-ttu-id="00fae-109">с помощью toobegin Здравствуйте возможности ретрансляции в Azure, необходимо сначала создать пространство имен службы.</span><span class="sxs-lookup"><span data-stu-id="00fae-109">toobegin using hello relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="00fae-110">Пространство имен предоставляет контейнер для адресации ресурсов Azure в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="00fae-110">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="00fae-111">Выполните hello [инструкциям](relay-create-namespace-portal.md) toocreate имен ретрансляции.</span><span class="sxs-lookup"><span data-stu-id="00fae-111">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="step-2-define-a-rest-based-wcf-service-contract-toouse-with-azure-relay"></a><span data-ttu-id="00fae-112">Шаг 2: Определение toouse контракта службы WCF на основе REST, с Azure ретрансляции</span><span class="sxs-lookup"><span data-stu-id="00fae-112">Step 2: Define a REST-based WCF service contract toouse with Azure Relay</span></span>

<span data-ttu-id="00fae-113">При создании WCF REST-службы, необходимо определить контракт hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-113">When you create a WCF REST-style service, you must define hello contract.</span></span> <span data-ttu-id="00fae-114">Контракт Hello указывает Здравствуйте, какие операции поддерживает узел.</span><span class="sxs-lookup"><span data-stu-id="00fae-114">hello contract specifies what operations hello host supports.</span></span> <span data-ttu-id="00fae-115">Операцию службы можно рассматривать как метод веб-службы.</span><span class="sxs-lookup"><span data-stu-id="00fae-115">A service operation can be thought of as a web service method.</span></span> <span data-ttu-id="00fae-116">Контракты создаются путем определения интерфейса C++, C# или Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="00fae-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="00fae-117">Каждый метод в интерфейсе hello соответствует tooa определенной операции службы.</span><span class="sxs-lookup"><span data-stu-id="00fae-117">Each method in hello interface corresponds tooa specific service operation.</span></span> <span data-ttu-id="00fae-118">Hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) атрибут должен быть применен tooeach интерфейс и hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) атрибут должен быть применен tooeach операции.</span><span class="sxs-lookup"><span data-stu-id="00fae-118">hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute must be applied tooeach interface, and hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute must be applied tooeach operation.</span></span> <span data-ttu-id="00fae-119">Если метод в интерфейсе, имеющем hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) имеет hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), что метод не предоставляется.</span><span class="sxs-lookup"><span data-stu-id="00fae-119">If a method in an interface that has hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) does not have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), that method is not exposed.</span></span> <span data-ttu-id="00fae-120">Hello код для выполнения этих задач отображается в примере hello, после процедуры hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-120">hello code used for these tasks is shown in hello example following hello procedure.</span></span>

<span data-ttu-id="00fae-121">Hello основное различие между контракта WCF и контракт REST-является добавление hello toohello свойство [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span><span class="sxs-lookup"><span data-stu-id="00fae-121">hello primary difference between a WCF contract and a REST-style contract is hello addition of a property toohello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span></span> <span data-ttu-id="00fae-122">Это свойство позволяет toomap метод в методе интерфейса tooa на hello другой стороне интерфейса hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-122">This property enables you toomap a method in your interface tooa method on hello other side of hello interface.</span></span> <span data-ttu-id="00fae-123">В этом случае мы используем [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink tooHTTP метод GET.</span><span class="sxs-lookup"><span data-stu-id="00fae-123">In this case, we will use [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink a method tooHTTP GET.</span></span> <span data-ttu-id="00fae-124">Это позволяет Service Bus tooaccurately извлекать и интерпретировать команды, отправляемые toohello интерфейса.</span><span class="sxs-lookup"><span data-stu-id="00fae-124">This allows Service Bus tooaccurately retrieve and interpret commands sent toohello interface.</span></span>

### <a name="toocreate-a-contract-with-an-interface"></a><span data-ttu-id="00fae-125">toocreate контракта с помощью интерфейса</span><span class="sxs-lookup"><span data-stu-id="00fae-125">toocreate a contract with an interface</span></span>

1. <span data-ttu-id="00fae-126">Откройте Visual Studio с правами администратора: щелкните правой кнопкой мыши программу hello в hello **запустить** меню, а затем нажмите **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="00fae-126">Open Visual Studio as an administrator: right-click hello program in hello **Start** menu, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="00fae-127">Создайте новый проект консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="00fae-127">Create a new console application project.</span></span> <span data-ttu-id="00fae-128">Нажмите кнопку hello **файл** и выбрать пункт **New**, а затем выберите **проекта**.</span><span class="sxs-lookup"><span data-stu-id="00fae-128">Click hello **File** menu and select **New**, then select **Project**.</span></span> <span data-ttu-id="00fae-129">В hello **новый проект** диалоговое окно, нажмите кнопку **Visual C#**выберите hello **консольное приложение** шаблона и назовите его **ImageListener**.</span><span class="sxs-lookup"><span data-stu-id="00fae-129">In hello **New Project** dialog box, click **Visual C#**, select hello **Console Application** template, and name it **ImageListener**.</span></span> <span data-ttu-id="00fae-130">Использовать значение по умолчанию hello **расположение**.</span><span class="sxs-lookup"><span data-stu-id="00fae-130">Use hello default **Location**.</span></span> <span data-ttu-id="00fae-131">Нажмите кнопку **ОК** toocreate hello проекта.</span><span class="sxs-lookup"><span data-stu-id="00fae-131">Click **OK** toocreate hello project.</span></span>
3. <span data-ttu-id="00fae-132">Для проекта C# в Visual Studio создается файл с именем `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="00fae-132">For a C# project, Visual Studio creates a `Program.cs` file.</span></span> <span data-ttu-id="00fae-133">Этот класс содержит пустой `Main()` метод, необходимый для консольного приложения проекта toobuild правильно.</span><span class="sxs-lookup"><span data-stu-id="00fae-133">This class contains an empty `Main()` method, required for a console application project toobuild correctly.</span></span>
4. <span data-ttu-id="00fae-134">Добавьте ссылки на tooService шины и **System.ServiceModel.dll** toohello проекта путем установки пакета шины обслуживания NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-134">Add references tooService Bus and **System.ServiceModel.dll** toohello project by installing hello Service Bus NuGet package.</span></span> <span data-ttu-id="00fae-135">Этот пакет автоматически добавляет ссылки на библиотеки служебной шины toohello, а также hello WCF **System.ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="00fae-135">This package automatically adds references toohello Service Bus libraries, as well as hello WCF **System.ServiceModel**.</span></span> <span data-ttu-id="00fae-136">В обозревателе решений щелкните правой кнопкой мыши hello **ImageListener** проекта, а затем нажмите кнопку **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="00fae-136">In Solution Explorer, right-click hello **ImageListener** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="00fae-137">Нажмите кнопку hello **Обзор** вкладку, а затем поиск `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="00fae-137">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="00fae-138">Нажмите кнопку **установить**и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-138">Click **Install**, and accept hello terms of use.</span></span>
5. <span data-ttu-id="00fae-139">Необходимо явно добавить ссылки слишком**System.ServiceModel.Web.dll** toohello проекта:</span><span class="sxs-lookup"><span data-stu-id="00fae-139">You must explicitly add a reference too**System.ServiceModel.Web.dll** toohello project:</span></span>
   
    <span data-ttu-id="00fae-140">а.</span><span class="sxs-lookup"><span data-stu-id="00fae-140">a.</span></span> <span data-ttu-id="00fae-141">В обозревателе решений щелкните правой кнопкой мыши hello **ссылки** папки в папку проекта hello, а затем нажмите кнопку **добавить ссылку**.</span><span class="sxs-lookup"><span data-stu-id="00fae-141">In Solution Explorer, right-click hello **References** folder under hello project folder and then click **Add Reference**.</span></span>
   
    <span data-ttu-id="00fae-142">b.</span><span class="sxs-lookup"><span data-stu-id="00fae-142">b.</span></span> <span data-ttu-id="00fae-143">В hello **добавить ссылку** диалоговое окно, нажмите кнопку hello **Framework** вкладка на левой стороне hello и hello **поиска** введите **System.ServiceModel.Web** .</span><span class="sxs-lookup"><span data-stu-id="00fae-143">In hello **Add Reference** dialog box, click hello **Framework** tab on hello left-hand side and in hello **Search** box, type **System.ServiceModel.Web**.</span></span> <span data-ttu-id="00fae-144">Выберите hello **System.ServiceModel.Web** флажок, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="00fae-144">Select hello **System.ServiceModel.Web** check box, then click **OK**.</span></span>
6. <span data-ttu-id="00fae-145">Добавьте следующее hello `using` инструкций hello верхней части файла Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-145">Add hello following `using` statements at hello top of hello Program.cs file.</span></span>
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    <span data-ttu-id="00fae-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) hello пространство имен, которое обеспечивает программный доступ toobasic возможности WCF.</span><span class="sxs-lookup"><span data-stu-id="00fae-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is hello namespace that enables programmatic access toobasic features of WCF.</span></span> <span data-ttu-id="00fae-147">Ретрансляции WCF использует множество объектов hello и атрибутов контрактов службы WCF toodefine.</span><span class="sxs-lookup"><span data-stu-id="00fae-147">WCF Relay uses many of hello objects and attributes of WCF toodefine service contracts.</span></span> <span data-ttu-id="00fae-148">Это пространство имен будет использоваться в большинстве приложений ретранслятора.</span><span class="sxs-lookup"><span data-stu-id="00fae-148">You will use this namespace in most of your relay applications.</span></span> <span data-ttu-id="00fae-149">Аналогичным образом [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) помогает определить канал hello, являющийся hello объекта, посредством которого осуществляется взаимодействие с веб-браузером клиента Azure ретрансляции и hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-149">Similarly, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helps define hello channel, which is hello object through which you communicate with Azure Relay and hello client web browser.</span></span> <span data-ttu-id="00fae-150">Наконец [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) содержит hello типы, позволяющие toocreate веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="00fae-150">Finally, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contains hello types that enable you toocreate web-based applications.</span></span>
7. <span data-ttu-id="00fae-151">Переименование hello `ImageListener` пространство имен слишком**Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="00fae-151">Rename hello `ImageListener` namespace too**Microsoft.ServiceBus.Samples**.</span></span>
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. <span data-ttu-id="00fae-152">Непосредственно после фигурной деклараций пространств имен hello hello, определите новый интерфейс с именем **IImageContract** и применить hello **ServiceContractAttribute** интерфейс toohello атрибута с значение `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="00fae-152">Directly after hello opening curly brace of hello namespace declaration, define a new interface named **IImageContract** and apply hello **ServiceContractAttribute** attribute toohello interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="00fae-153">Значение пространства имен Hello отличается от hello пространства имен, используемого во всей области действия своего кода hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-153">hello namespace value differs from hello namespace that you use throughout hello scope of your code.</span></span> <span data-ttu-id="00fae-154">Значение пространства имен Hello используется в качестве уникального идентификатора для данного контракта и должно содержать сведения о версии.</span><span class="sxs-lookup"><span data-stu-id="00fae-154">hello namespace value is used as a unique identifier for this contract, and should have version information.</span></span> <span data-ttu-id="00fae-155">Дополнительные сведения см. в статье [Управление версиями службы](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="00fae-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="00fae-156">Явное указание пространства имен hello запрещает значение пространства имен по умолчанию hello toohello имя контракта.</span><span class="sxs-lookup"><span data-stu-id="00fae-156">Specifying hello namespace explicitly prevents hello default namespace value from being added toohello contract name.</span></span>
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. <span data-ttu-id="00fae-157">В рамках hello `IImageContract` интерфейсом, объявите метод для отдельной операции hello hello `IImageContract` предоставляет контракт в hello интерфейс и применение hello `OperationContractAttribute` атрибута toohello способ tooexpose как часть службы открытого hello шины контракт.</span><span class="sxs-lookup"><span data-stu-id="00fae-157">Within hello `IImageContract` interface, declare a method for hello single operation hello `IImageContract` contract exposes in hello interface and apply hello `OperationContractAttribute` attribute toohello method that you want tooexpose as part of hello public Service Bus contract.</span></span>
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. <span data-ttu-id="00fae-158">В hello **OperationContract** , добавьте hello **WebGet** значение.</span><span class="sxs-lookup"><span data-stu-id="00fae-158">In hello **OperationContract** attribute, add hello **WebGet** value.</span></span>
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    <span data-ttu-id="00fae-159">Таким образом, включает hello tooroute службы ретрансляции HTTP-запросы GET слишком`GetImage`и значений, возвращаемых из hello tootranslate `GetImage` в ответ HTTP GETRESPONSE.</span><span class="sxs-lookup"><span data-stu-id="00fae-159">Doing so enables hello relay service tooroute HTTP GET requests too`GetImage`, and tootranslate hello return values of `GetImage` into an HTTP GETRESPONSE reply.</span></span> <span data-ttu-id="00fae-160">Далее в учебнике hello используется tooaccess веб браузера этот метод и toodisplay hello изображения в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-160">Later in hello tutorial, you will use a web browser tooaccess this method, and toodisplay hello image in hello browser.</span></span>
11. <span data-ttu-id="00fae-161">Непосредственно после hello `IImageContract` определение, объявите канал, который наследует от обоих hello `IImageContract` и `IClientChannel` интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="00fae-161">Directly after hello `IImageContract` definition, declare a channel that inherits from both hello `IImageContract` and `IClientChannel` interfaces.</span></span>
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    <span data-ttu-id="00fae-162">Канал представляет hello объекта WCF, через который hello службы и клиента передачи tooeach сведения о других.</span><span class="sxs-lookup"><span data-stu-id="00fae-162">A channel is hello WCF object through which hello service and client pass information tooeach other.</span></span> <span data-ttu-id="00fae-163">Позже можно создать канал hello в основное приложение.</span><span class="sxs-lookup"><span data-stu-id="00fae-163">Later, you will create hello channel in your host application.</span></span> <span data-ttu-id="00fae-164">Ретранслятор Azure затем использует этот канал toopass hello HTTP-запросы GET из браузера tooyour hello **GetImage** реализации.</span><span class="sxs-lookup"><span data-stu-id="00fae-164">Azure Relay then uses this channel toopass hello HTTP GET requests from hello browser tooyour **GetImage** implementation.</span></span> <span data-ttu-id="00fae-165">Hello ретрансляции также использует hello канала tootake hello **GetImage** возвращаемое значение и преобразовать его в ответ HTTP GETRESPONSE для браузера клиента hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-165">hello relay also uses hello channel tootake hello **GetImage** return value and translate it into an HTTP GETRESPONSE for hello client browser.</span></span>
12. <span data-ttu-id="00fae-166">Из hello **построения** меню, нажмите кнопку **построить решение** tooconfirm hello правильность выполненной работы к текущему моменту.</span><span class="sxs-lookup"><span data-stu-id="00fae-166">From hello **Build** menu, click **Build Solution** tooconfirm hello accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="00fae-167">Пример</span><span class="sxs-lookup"><span data-stu-id="00fae-167">Example</span></span>
<span data-ttu-id="00fae-168">Hello после кода показан базовый интерфейс, определяющий контракт ретрансляции WCF.</span><span class="sxs-lookup"><span data-stu-id="00fae-168">hello following code shows a basic interface that defines a WCF Relay contract.</span></span>

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

## <a name="step-3-implement-a-rest-based-wcf-service-contract-toouse-service-bus"></a><span data-ttu-id="00fae-169">Шаг 3: Реализация toouse контракта службы WCF на основе REST Service Bus</span><span class="sxs-lookup"><span data-stu-id="00fae-169">Step 3: Implement a REST-based WCF service contract toouse Service Bus</span></span>
<span data-ttu-id="00fae-170">Создание службы ретрансляции WCF в стиле REST необходимо сначала создать контракт hello, который определен с помощью интерфейса.</span><span class="sxs-lookup"><span data-stu-id="00fae-170">Creating a REST-style WCF Relay service requires that you first create hello contract, which is defined by using an interface.</span></span> <span data-ttu-id="00fae-171">Hello следующим шагом является интерфейс tooimplement hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-171">hello next step is tooimplement hello interface.</span></span> <span data-ttu-id="00fae-172">Это предполагает создание класса с именем **ImageService** , реализующий hello определяемых пользователем **IImageContract** интерфейса.</span><span class="sxs-lookup"><span data-stu-id="00fae-172">This involves creating a class named **ImageService** that implements hello user-defined **IImageContract** interface.</span></span> <span data-ttu-id="00fae-173">После реализации контракта hello, необходимо настроить интерфейс hello, с помощью файла App.config.</span><span class="sxs-lookup"><span data-stu-id="00fae-173">After you implement hello contract, you then configure hello interface using an App.config file.</span></span> <span data-ttu-id="00fae-174">Hello файл конфигурации содержит сведения, необходимые для приложения hello, например имя службы hello hello, hello hello контракта и тип протокола, используемые toocommunicate со службой ретрансляции hello hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-174">hello configuration file contains necessary information for hello application, such as hello name of hello service, hello name of hello contract, and hello type of protocol that is used toocommunicate with hello relay service.</span></span> <span data-ttu-id="00fae-175">Hello код для выполнения этих задач приведен в примере hello, после процедуры hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-175">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

<span data-ttu-id="00fae-176">Как и hello предыдущие действия, существует очень небольшая разница в реализации контракт REST- и контракта WCF ретрансляции.</span><span class="sxs-lookup"><span data-stu-id="00fae-176">As with hello previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span></span>

### <a name="tooimplement-a-rest-style-service-bus-contract"></a><span data-ttu-id="00fae-177">Контракт tooimplement стиле REST Service Bus</span><span class="sxs-lookup"><span data-stu-id="00fae-177">tooimplement a REST-style Service Bus contract</span></span>
1. <span data-ttu-id="00fae-178">Создайте новый класс с именем **ImageService** непосредственно после определения hello hello **IImageContract** интерфейса.</span><span class="sxs-lookup"><span data-stu-id="00fae-178">Create a new class named **ImageService** directly after hello definition of hello **IImageContract** interface.</span></span> <span data-ttu-id="00fae-179">Hello **ImageService** класс реализует hello **IImageContract** интерфейса.</span><span class="sxs-lookup"><span data-stu-id="00fae-179">hello **ImageService** class implements hello **IImageContract** interface.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    <span data-ttu-id="00fae-180">Определение hello схожие реализации интерфейса tooother, можно реализовать в другой файл.</span><span class="sxs-lookup"><span data-stu-id="00fae-180">Similar tooother interface implementations, you can implement hello definition in a different file.</span></span> <span data-ttu-id="00fae-181">Однако в этом учебнике реализация hello появляется в тот же файл как определение интерфейса hello hello и `Main()` метод.</span><span class="sxs-lookup"><span data-stu-id="00fae-181">However, for this tutorial, hello implementation appears in hello same file as hello interface definition and `Main()` method.</span></span>
2. <span data-ttu-id="00fae-182">Применить hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) атрибута toohello **IImageService** tooindicate класс, который hello класс — это реализация контракта WCF.</span><span class="sxs-lookup"><span data-stu-id="00fae-182">Apply hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute toohello **IImageService** class tooindicate that hello class is an implementation of a WCF contract.</span></span>
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    <span data-ttu-id="00fae-183">Как упоминалось ранее, это пространство имен не является обычным.</span><span class="sxs-lookup"><span data-stu-id="00fae-183">As mentioned previously, this namespace is not a traditional namespace.</span></span> <span data-ttu-id="00fae-184">Вместо этого он является частью WCF архитектуру, которая идентифицирует контракт hello hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-184">Instead, it is part of hello WCF architecture that identifies hello contract.</span></span> <span data-ttu-id="00fae-185">Дополнительные сведения см. в разделе hello [имена контрактов данных](https://msdn.microsoft.com/library/ms731045.aspx) раздела hello документации WCF.</span><span class="sxs-lookup"><span data-stu-id="00fae-185">For more information, see hello [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) topic in hello WCF documentation.</span></span>
3. <span data-ttu-id="00fae-186">Добавьте проект tooyour .jpg изображения.</span><span class="sxs-lookup"><span data-stu-id="00fae-186">Add a .jpg image tooyour project.</span></span>  
   
    <span data-ttu-id="00fae-187">Это рисунок, службой hello в hello получение браузера.</span><span class="sxs-lookup"><span data-stu-id="00fae-187">This is a picture that hello service displays in hello receiving browser.</span></span> <span data-ttu-id="00fae-188">Щелкните проект правой кнопкой мыши и выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="00fae-188">Right-click your project, then click **Add**.</span></span> <span data-ttu-id="00fae-189">Затем выберите **Существующий элемент**.</span><span class="sxs-lookup"><span data-stu-id="00fae-189">Then click **Existing Item**.</span></span> <span data-ttu-id="00fae-190">Используйте hello **Добавление существующего элемента** tooan toobrowse поле диалогового окна, возможно .jpg и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="00fae-190">Use hello **Add Existing Item** dialog box toobrowse tooan appropriate .jpg, and then click **Add**.</span></span>
   
    <span data-ttu-id="00fae-191">При добавлении файла hello, убедитесь, что **все файлы** в toohello Далее hello раскрывающемся списке выбран **имя файла:** поля.</span><span class="sxs-lookup"><span data-stu-id="00fae-191">When adding hello file, make sure that **All Files** is selected in hello drop-down list next toohello **File name:** field.</span></span> <span data-ttu-id="00fae-192">Hello конца данного учебника предполагается, что hello hello изображение называется «image.jpg».</span><span class="sxs-lookup"><span data-stu-id="00fae-192">hello rest of this tutorial assumes that hello name of hello image is "image.jpg".</span></span> <span data-ttu-id="00fae-193">Если имеется другой файл, будет toorename hello образ или изменить toocompensate вашего кода.</span><span class="sxs-lookup"><span data-stu-id="00fae-193">If you have a different file, you will have toorename hello image, or change your code toocompensate.</span></span>
4. <span data-ttu-id="00fae-194">hello, что запущена служба могли находить в файл изображения hello, toomake **обозревателе решений** щелкните правой кнопкой мыши файл изображения hello, а затем нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="00fae-194">toomake sure that hello running service can find hello image file, in **Solution Explorer** right-click hello image file, then click **Properties**.</span></span> <span data-ttu-id="00fae-195">В hello **свойства** задайте **скопируйте каталог tooOutput** слишком**копировать, если новее**.</span><span class="sxs-lookup"><span data-stu-id="00fae-195">In hello **Properties** pane, set **Copy tooOutput Directory** too**Copy if newer**.</span></span>
5. <span data-ttu-id="00fae-196">Добавить toohello ссылки **System.Drawing.dll** toohello сборки проекта, а также добавить hello следующие связанные `using` инструкции.</span><span class="sxs-lookup"><span data-stu-id="00fae-196">Add a reference toohello **System.Drawing.dll** assembly toohello project, and also add hello following associated `using` statements.</span></span>  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. <span data-ttu-id="00fae-197">В hello **ImageService** добавьте hello за конструктором, загружаются hello точечный рисунок и подготавливает toosend его toohello клиентского браузера.</span><span class="sxs-lookup"><span data-stu-id="00fae-197">In hello **ImageService** class, add hello following constructor that loads hello bitmap and prepares toosend it toohello client browser.</span></span>
   
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
7. <span data-ttu-id="00fae-198">Непосредственно после кода предыдущего hello добавьте следующее hello **GetImage** метод в hello **ImageService** класса tooreturn HTTP сообщения, содержащего изображение hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-198">Directly after hello previous code, add hello following **GetImage** method in hello **ImageService** class tooreturn an HTTP message that contains hello image.</span></span>
   
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
   
    <span data-ttu-id="00fae-199">Эта реализация использует **MemoryStream** tooretrieve hello изображения и подготовить его для потоковой передачи toohello браузера.</span><span class="sxs-lookup"><span data-stu-id="00fae-199">This implementation uses **MemoryStream** tooretrieve hello image and prepare it for streaming toohello browser.</span></span> <span data-ttu-id="00fae-200">Запускает hello нуля позицию потока, объявляет содержимое потока hello в формате jpeg и отправляет сведения hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-200">It starts hello stream position at zero, declares hello stream content as a jpeg, and streams hello information.</span></span>
8. <span data-ttu-id="00fae-201">Из hello **построения** меню, нажмите кнопку **построить решение**.</span><span class="sxs-lookup"><span data-stu-id="00fae-201">From hello **Build** menu, click **Build Solution**.</span></span>

### <a name="toodefine-hello-configuration-for-running-hello-web-service-on-service-bus"></a><span data-ttu-id="00fae-202">Конфигурация hello toodefine запустить hello веб-службы для служебной шины</span><span class="sxs-lookup"><span data-stu-id="00fae-202">toodefine hello configuration for running hello web service on Service Bus</span></span>
1. <span data-ttu-id="00fae-203">В **обозревателе решений**, дважды щелкните **App.config** tooopen его в редакторе Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-203">In **Solution Explorer**, double-click **App.config** tooopen it in hello Visual Studio editor.</span></span>
   
    <span data-ttu-id="00fae-204">Hello **App.config** файл, содержащий имя службы hello, конечной точки (то есть hello расположение ретрансляции Azure предоставляет клиентам и узлам toocommunicate друг с другом) и привязки (hello тип протокола, который будет использоваться toocommunicate).</span><span class="sxs-lookup"><span data-stu-id="00fae-204">hello **App.config** file includes hello service name, endpoint (that is, hello location Azure Relay exposes for clients and hosts toocommunicate with each other), and binding (hello type of protocol that is used toocommunicate).</span></span> <span data-ttu-id="00fae-205">Hello основное различие состоит в этой конечной точкой службы настроены hello ссылается tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) привязки.</span><span class="sxs-lookup"><span data-stu-id="00fae-205">hello main difference here is that hello configured service endpoint refers tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span></span>
2. <span data-ttu-id="00fae-206">Hello `<system.serviceModel>` XML-элемент — это элемент WCF, который определяет одну или несколько служб.</span><span class="sxs-lookup"><span data-stu-id="00fae-206">hello `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span></span> <span data-ttu-id="00fae-207">В данном случае имя службы используется toodefine hello и конечной точки.</span><span class="sxs-lookup"><span data-stu-id="00fae-207">Here, it is used toodefine hello service name and endpoint.</span></span> <span data-ttu-id="00fae-208">Внизу hello hello `<system.serviceModel>` элемент (но по-прежнему в `<system.serviceModel>`), добавить `<bindings>` элемент, имеющий hello после содержимого.</span><span class="sxs-lookup"><span data-stu-id="00fae-208">At hello bottom of hello `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has hello following content.</span></span> <span data-ttu-id="00fae-209">Этот параметр определяет hello привязки, используемые в приложении hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-209">This defines hello bindings used in hello application.</span></span> <span data-ttu-id="00fae-210">Можно определить несколько привязок, но в этом учебнике определяется только одна.</span><span class="sxs-lookup"><span data-stu-id="00fae-210">You can define multiple bindings, but for this tutorial you are defining only one.</span></span>
   
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
   
    <span data-ttu-id="00fae-211">Предыдущий код Hello определяет ретрансляции WCF [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) привязки с **relayClientAuthenticationType** значение слишком**нет**.</span><span class="sxs-lookup"><span data-stu-id="00fae-211">hello previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set too**None**.</span></span> <span data-ttu-id="00fae-212">Этот параметр указывает, что для конечной точки, использующей эту привязку, не требуются учетные данные клиента.</span><span class="sxs-lookup"><span data-stu-id="00fae-212">This setting indicates that an endpoint using this binding does not require a client credential.</span></span>
3. <span data-ttu-id="00fae-213">После hello `<bindings>` элемента, добавьте `<services>` элемента.</span><span class="sxs-lookup"><span data-stu-id="00fae-213">After hello `<bindings>` element, add a `<services>` element.</span></span> <span data-ttu-id="00fae-214">Аналогичными привязками toohello можно определить несколько служб в одном файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="00fae-214">Similar toohello bindings, you can define multiple services in a single configuration file.</span></span> <span data-ttu-id="00fae-215">Но в этом учебнике определяется только одна.</span><span class="sxs-lookup"><span data-stu-id="00fae-215">However, for this tutorial, you define only one.</span></span>
   
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
   
    <span data-ttu-id="00fae-216">Этот шаг позволяет настроить службу, которая использует по умолчанию hello ранее определенные **webHttpRelayBinding**.</span><span class="sxs-lookup"><span data-stu-id="00fae-216">This step configures a service that uses hello previously defined default **webHttpRelayBinding**.</span></span> <span data-ttu-id="00fae-217">Кроме того, используются по умолчанию hello **sbTokenProvider**, которая определена в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-217">It also uses hello default **sbTokenProvider**, which is defined in hello next step.</span></span>
4. <span data-ttu-id="00fae-218">После hello `<services>` элемент, создайте `<behaviors>` элемент с hello вслед содержимым, заменив «SAS_KEY» hello *подписи общего доступа* ключа (SAS), ранее получены из hello [портал Azure ][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="00fae-218">After hello `<services>` element, create a `<behaviors>` element with hello following content, replacing "SAS_KEY" with hello *Shared Access Signature* (SAS) key you previously obtained from hello [Azure portal][Azure portal].</span></span>
   
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
5. <span data-ttu-id="00fae-219">По-прежнему в файл App.config, в hello `<appSettings>` элемент замены hello все подключение строковое значение со строкой подключения hello ранее получены из портала hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-219">Still in App.config, in hello `<appSettings>` element, replace hello entire connection string value with hello connection string you previously obtained from hello portal.</span></span> 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. <span data-ttu-id="00fae-220">Из hello **построения** меню, нажмите кнопку **построить решение** toobuild hello всего решения.</span><span class="sxs-lookup"><span data-stu-id="00fae-220">From hello **Build** menu, click **Build Solution** toobuild hello entire solution.</span></span>

### <a name="example"></a><span data-ttu-id="00fae-221">Пример</span><span class="sxs-lookup"><span data-stu-id="00fae-221">Example</span></span>
<span data-ttu-id="00fae-222">Hello код отображает hello контракта и реализации службы для службы на основе REST, которая выполняется на Service Bus с помощью hello **WebHttpRelayBinding** привязки.</span><span class="sxs-lookup"><span data-stu-id="00fae-222">hello following code shows hello contract and service implementation for a REST-based service that is running on  Service Bus using hello **WebHttpRelayBinding** binding.</span></span>

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

<span data-ttu-id="00fae-223">Hello пример hello файла App.config, связанного со службой hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-223">hello following example shows hello App.config file associated with hello service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove hello ones they don't need. -->
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

## <a name="step-4-host-hello-rest-based-wcf-service-toouse-azure-relay"></a><span data-ttu-id="00fae-224">Шаг 4: Размещения toouse службы WCF на основе REST hello Azure ретрансляции</span><span class="sxs-lookup"><span data-stu-id="00fae-224">Step 4: Host hello REST-based WCF service toouse Azure Relay</span></span>
<span data-ttu-id="00fae-225">В этом разделе описывается, как toorun веб-узел службы с помощью консольного приложения с WCF ретрансляции.</span><span class="sxs-lookup"><span data-stu-id="00fae-225">This step describes how toorun a web service using a console application with WCF Relay.</span></span> <span data-ttu-id="00fae-226">Полный листинг кода hello, написанного на этом шаге приведен в примере hello, после процедуры hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-226">A complete listing of hello code written in this step is provided in hello example following hello procedure.</span></span>

### <a name="toocreate-a-base-address-for-hello-service"></a><span data-ttu-id="00fae-227">toocreate базовый адрес для службы hello</span><span class="sxs-lookup"><span data-stu-id="00fae-227">toocreate a base address for hello service</span></span>
1. <span data-ttu-id="00fae-228">В hello `Main()` объявление функции, создать пространство имен переменной toostore hello проекта.</span><span class="sxs-lookup"><span data-stu-id="00fae-228">In hello `Main()` function declaration, create a variable toostore hello namespace of your project.</span></span> <span data-ttu-id="00fae-229">Убедитесь, что tooreplace `yourNamespace` с именем hello пространства имен hello ретрансляции, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="00fae-229">Make sure tooreplace `yourNamespace` with hello name of hello Relay namespace you created previously.</span></span>
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    <span data-ttu-id="00fae-230">Service Bus использует имя hello в пространство имен toocreate уникальный URI.</span><span class="sxs-lookup"><span data-stu-id="00fae-230">Service Bus uses hello name of your namespace toocreate a unique URI.</span></span>
2. <span data-ttu-id="00fae-231">Создание `Uri` экземпляр hello базового адреса службы hello, основанный на пространство имен hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-231">Create a `Uri` instance for hello base address of hello service that is based on hello namespace.</span></span>
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="toocreate-and-configure-hello-web-service-host"></a><span data-ttu-id="00fae-232">toocreate и настроить узел веб-службы hello</span><span class="sxs-lookup"><span data-stu-id="00fae-232">toocreate and configure hello web service host</span></span>
* <span data-ttu-id="00fae-233">Создайте hello узел веб-службы, с помощью созданного ранее в этом разделе hello URI-адрес.</span><span class="sxs-lookup"><span data-stu-id="00fae-233">Create hello web service host, using hello URI address created earlier in this section.</span></span>
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    <span data-ttu-id="00fae-234">узел службы Hello: hello объекта WCF, который создает экземпляры ведущего приложения hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-234">hello service host is hello WCF object that instantiates hello host application.</span></span> <span data-ttu-id="00fae-235">В этом примере передается hello тип узла требуется toocreate ( **ImageService**), а также hello адрес, по которому требуется tooexpose hello ведущего приложения.</span><span class="sxs-lookup"><span data-stu-id="00fae-235">This example passes it hello type of host you want toocreate (an **ImageService**), and also hello address at which you want tooexpose hello host application.</span></span>

### <a name="toorun-hello-web-service-host"></a><span data-ttu-id="00fae-236">узел toorun hello веб-служб</span><span class="sxs-lookup"><span data-stu-id="00fae-236">toorun hello web service host</span></span>
1. <span data-ttu-id="00fae-237">Откройте службу hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-237">Open hello service.</span></span>
   
    ```csharp
    host.Open();
    ```
    <span data-ttu-id="00fae-238">Теперь Hello служба работает.</span><span class="sxs-lookup"><span data-stu-id="00fae-238">hello service is now running.</span></span>
2. <span data-ttu-id="00fae-239">Сообщение, указывающее, что запущена служба hello и как toostop hello службы.</span><span class="sxs-lookup"><span data-stu-id="00fae-239">Display a message indicating that hello service is running, and how toostop hello service.</span></span>
   
    ```csharp
    Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="00fae-240">После завершения закройте узел службы hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-240">When finished, close hello service host.</span></span>
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a><span data-ttu-id="00fae-241">Пример</span><span class="sxs-lookup"><span data-stu-id="00fae-241">Example</span></span>
<span data-ttu-id="00fae-242">Следующий пример Hello включает hello контракт и реализацию службы из предыдущих шагов в hello учебник и узлы служб hello в консольном приложении.</span><span class="sxs-lookup"><span data-stu-id="00fae-242">hello following example includes hello service contract and implementation from previous steps in hello tutorial and hosts hello service in a console application.</span></span> <span data-ttu-id="00fae-243">Скомпилируйте следующий код в исполняемый файл с именем ImageListener.exe hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-243">Compile hello following code into an executable named ImageListener.exe.</span></span>

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

            Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-hello-code"></a><span data-ttu-id="00fae-244">Компиляция кода hello</span><span class="sxs-lookup"><span data-stu-id="00fae-244">Compiling hello code</span></span>
<span data-ttu-id="00fae-245">После построения решения hello, hello следующие приложения hello toorun:</span><span class="sxs-lookup"><span data-stu-id="00fae-245">After building hello solution, do hello following toorun hello application:</span></span>

1. <span data-ttu-id="00fae-246">Нажмите клавишу **F5**, или найдите расположение исполняемого файла toohello (ImageListener\bin\Debug\ImageListener.exe) toorun hello службы.</span><span class="sxs-lookup"><span data-stu-id="00fae-246">Press **F5**, or browse toohello executable file location (ImageListener\bin\Debug\ImageListener.exe), toorun hello service.</span></span> <span data-ttu-id="00fae-247">Оставьте hello приложение выполняется, так как он является обязательным, следующим шагом tooperform hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-247">Keep hello app running, as it's required tooperform hello next step.</span></span>
2. <span data-ttu-id="00fae-248">Скопируйте и вставьте адрес hello из командной строки hello в изображение hello toosee браузера.</span><span class="sxs-lookup"><span data-stu-id="00fae-248">Copy and paste hello address from hello command prompt into a browser toosee hello image.</span></span>
3. <span data-ttu-id="00fae-249">Когда вы закончите, нажмите клавишу **ввод** в приложение hello tooclose окно командной строки hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-249">When you are finished, press **Enter** in hello command prompt window tooclose hello app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00fae-250">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="00fae-250">Next steps</span></span>
<span data-ttu-id="00fae-251">Теперь, когда вы создали приложение, использующее службы ретрансляции Service Bus hello, см. следующие статьи toolearn больше о Azure ретрансляции hello.</span><span class="sxs-lookup"><span data-stu-id="00fae-251">Now that you've built an application that uses hello Service Bus relay service, see hello following articles toolearn more about Azure Relay:</span></span>

* [<span data-ttu-id="00fae-252">Обзор архитектуры служебной шины Azure</span><span class="sxs-lookup"><span data-stu-id="00fae-252">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="00fae-253">Что такое ретранслятор Azure?</span><span class="sxs-lookup"><span data-stu-id="00fae-253">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="00fae-254">Как службу в .NET Framework посредника toouse hello WCF</span><span class="sxs-lookup"><span data-stu-id="00fae-254">How toouse hello WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
