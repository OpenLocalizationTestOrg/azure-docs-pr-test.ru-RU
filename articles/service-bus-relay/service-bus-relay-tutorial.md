---
title: "Учебник ретрансляции WCF Service Bus aaaAzure | Документы Microsoft"
description: "Создание службы и клиентского приложения служебной шины с помощью ретранслятора WCF."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 53dfd236-97f1-4778-b376-be91aa14b842
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: sethm
ms.openlocfilehash: 78cd52ef51e9fcfcda2f13ec54bde3af50d76476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-tutorial"></a><span data-ttu-id="ffcd6-103">Руководство по ретранслятору WCF Azure</span><span class="sxs-lookup"><span data-stu-id="ffcd6-103">Azure WCF Relay tutorial</span></span>

<span data-ttu-id="ffcd6-104">В данном учебнике как toobuild простой WCF ретрансляции клиентского приложения и службы с помощью Azure ретрансляции.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-104">This tutorial describes how toobuild a simple WCF Relay client application and service using Azure Relay.</span></span> <span data-ttu-id="ffcd6-105">Аналогичное руководство по [обмену сообщениями в служебной шине](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging) представлено в статье [Начало работы с очередями служебной шины](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="ffcd6-105">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="ffcd6-106">Прохождение этого учебника дает представление о hello шаги, необходимые toocreate приложении клиента и службы ретрансляции WCF.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-106">Working through this tutorial gives you an understanding of hello steps that are required toocreate a WCF Relay client and service application.</span></span> <span data-ttu-id="ffcd6-107">Как и в WCF, под службой понимается конструкция, которая предоставляет одну или несколько конечных точек, каждая из которых предоставляет одну или несколько операций службы.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-107">Like their original WCF counterparts, a service is a construct that exposes one or more endpoints, each of which exposes one or more service operations.</span></span> <span data-ttu-id="ffcd6-108">Hello конечную точку службы определяет адрес, где можно найти службу hello, привязка, которая содержит сведения hello, клиент должен связаться с hello службы и контракт, определяющий hello функциональные возможности, предоставляемые клиентами tooits hello службы.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-108">hello endpoint of a service specifies an address where hello service can be found, a binding that contains hello information that a client must communicate with hello service, and a contract that defines hello functionality provided by hello service tooits clients.</span></span> <span data-ttu-id="ffcd6-109">Hello основное различие между WCF и ретрансляции WCF — в облаке hello, а не на локальном компьютере, предоставленный этой конечной точке hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-109">hello main difference between WCF and WCF Relay is that hello endpoint is exposed in hello cloud instead of locally on your computer.</span></span>

<span data-ttu-id="ffcd6-110">После работы через последовательность hello разделов в этом учебнике будет иметь запущенной службы и клиента, который можно вызвать операции hello hello службы.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-110">After you work through hello sequence of topics in this tutorial, you will have a running service, and a client that can invoke hello operations of hello service.</span></span> <span data-ttu-id="ffcd6-111">Hello первой статье описывается, как tooset учетную запись.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-111">hello first topic describes how tooset up an account.</span></span> <span data-ttu-id="ffcd6-112">Hello Далее описывается, как toodefine службы, использует контракт, как tooimplement hello службы и как tooconfigure hello службы в коде.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-112">hello next steps describe how toodefine a service that uses a contract, how tooimplement hello service, and how tooconfigure hello service in code.</span></span> <span data-ttu-id="ffcd6-113">В них также рассматриваются как toohost и запустите службу hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-113">They also describe how toohost and run hello service.</span></span> <span data-ttu-id="ffcd6-114">Hello созданная служба является резидентной и hello клиент и служба работают на hello того же компьютера.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-114">hello service that is created is self-hosted and hello client and service run on hello same computer.</span></span> <span data-ttu-id="ffcd6-115">Можно настроить службу hello с помощью кода или файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-115">You can configure hello service by using either code or a configuration file.</span></span>

<span data-ttu-id="ffcd6-116">Hello заключительные три действия описывают, как toocreate клиентского приложения, настройте клиентское приложение hello и создать и использовать клиент, который можно получить доступ к функциональности hello hello узла.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-116">hello final three steps describe how toocreate a client application, configure hello client application, and create and use a client that can access hello functionality of hello host.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffcd6-117">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ffcd6-117">Prerequisites</span></span>

<span data-ttu-id="ffcd6-118">toocomplete этого учебника вам потребуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="ffcd6-118">toocomplete this tutorial, you'll need hello following:</span></span>

* <span data-ttu-id="ffcd6-119">[Microsoft Visual Studio 2015 или более поздней версии](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="ffcd6-119">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="ffcd6-120">В этом учебнике используется Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-120">This tutorial uses Visual Studio 2017.</span></span>
* <span data-ttu-id="ffcd6-121">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-121">An active Azure account.</span></span> <span data-ttu-id="ffcd6-122">Если ее нет, можно создать бесплатную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-122">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="ffcd6-123">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="ffcd6-123">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="ffcd6-124">Создание пространства имен службы</span><span class="sxs-lookup"><span data-stu-id="ffcd6-124">Create a service namespace</span></span>

<span data-ttu-id="ffcd6-125">Hello первым шагом является toocreate пространства имен и tooobtain [подписи общего доступа (SAS)](../service-bus-messaging/service-bus-sas.md) ключа.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-125">hello first step is toocreate a namespace, and tooobtain a [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) key.</span></span> <span data-ttu-id="ffcd6-126">Пространство имен предоставляет границу для каждого приложения, предоставляемые через службу ретрансляции hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-126">A namespace provides an application boundary for each application exposed through hello relay service.</span></span> <span data-ttu-id="ffcd6-127">Ключ SAS автоматически создается системой hello при создании пространства имен службы.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-127">A SAS key is automatically generated by hello system when a service namespace is created.</span></span> <span data-ttu-id="ffcd6-128">Hello сочетание пространства имен службы и ключ SAS содержит учетные данные hello Azure tooauthenticate доступа tooan приложения.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-128">hello combination of service namespace and SAS key provides hello credentials for Azure tooauthenticate access tooan application.</span></span> <span data-ttu-id="ffcd6-129">Выполните hello [инструкциям](relay-create-namespace-portal.md) toocreate имен ретрансляции.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-129">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="define-a-wcf-service-contract"></a><span data-ttu-id="ffcd6-130">Определение контракта службы WCF</span><span class="sxs-lookup"><span data-stu-id="ffcd6-130">Define a WCF service contract</span></span>

<span data-ttu-id="ffcd6-131">контракт службы Hello указывает, какие службы поддерживает hello операций (hello термины веб-служб для методов или функций).</span><span class="sxs-lookup"><span data-stu-id="ffcd6-131">hello service contract specifies what operations (hello web service terminology for methods or functions) hello service supports.</span></span> <span data-ttu-id="ffcd6-132">Контракты создаются путем определения интерфейса C++, C# или Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-132">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="ffcd6-133">Каждый метод в интерфейсе hello соответствует tooa определенной операции службы.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-133">Each method in hello interface corresponds tooa specific service operation.</span></span> <span data-ttu-id="ffcd6-134">Каждый интерфейс должен иметь hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) tooit применен атрибут, и каждая операция должна иметь hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) tooit применен атрибут.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-134">Each interface must have hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute applied tooit, and each operation must have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute applied tooit.</span></span> <span data-ttu-id="ffcd6-135">Если метод в интерфейсе, имеющем hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) атрибут не имеет hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) атрибута, метод не предоставляется.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-135">If a method in an interface that has hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute does not have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute, that method is not exposed.</span></span> <span data-ttu-id="ffcd6-136">Hello код для выполнения этих задач приведен в примере hello, после процедуры hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-136">hello code for these tasks is provided in hello example following hello procedure.</span></span> <span data-ttu-id="ffcd6-137">Более полное обсуждение контрактов и служб в разделе [проектирование и реализация служб](https://msdn.microsoft.com/library/ms729746.aspx) в документации по WCF hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-137">For a larger discussion of contracts and services, see [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in hello WCF documentation.</span></span>

### <a name="create-a-relay-contract-with-an-interface"></a><span data-ttu-id="ffcd6-138">Создание контракта ретранслятора с помощью интерфейса</span><span class="sxs-lookup"><span data-stu-id="ffcd6-138">Create a relay contract with an interface</span></span>

1. <span data-ttu-id="ffcd6-139">Откройте Visual Studio с правами администратора, щелкнув правой кнопкой мыши программу hello в hello **запустить** , выберите в меню **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-139">Open Visual Studio as an administrator by right-clicking hello program in hello **Start** menu and selecting **Run as administrator**.</span></span>
2. <span data-ttu-id="ffcd6-140">Создайте новый проект консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-140">Create a new console application project.</span></span> <span data-ttu-id="ffcd6-141">Нажмите кнопку hello **файл** и выбрать пункт **New**, нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-141">Click hello **File** menu and select **New**, then click **Project**.</span></span> <span data-ttu-id="ffcd6-142">В hello **новый проект** диалоговое окно, нажмите кнопку **Visual C#** (если **Visual C#** не отображается, найдите его в разделе **другие языки**).</span><span class="sxs-lookup"><span data-stu-id="ffcd6-142">In hello **New Project** dialog, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**).</span></span> <span data-ttu-id="ffcd6-143">Нажмите кнопку hello **консольного приложения (.NET Framework)** шаблона и назовите его **EchoService**.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-143">Click hello **Console App (.NET Framework)** template, and name it **EchoService**.</span></span> <span data-ttu-id="ffcd6-144">Нажмите кнопку **ОК** toocreate hello проекта.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-144">Click **OK** toocreate hello project.</span></span>

    ![][2]

3. <span data-ttu-id="ffcd6-145">Установите пакет шины обслуживания NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-145">Install hello Service Bus NuGet package.</span></span> <span data-ttu-id="ffcd6-146">Этот пакет автоматически добавляет ссылки на библиотеки служебной шины toohello, а также hello WCF **System.ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-146">This package automatically adds references toohello Service Bus libraries, as well as hello WCF **System.ServiceModel**.</span></span> <span data-ttu-id="ffcd6-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) hello пространство имен, которое позволяет tooprogrammatically доступа hello основные компоненты служб WCF.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is hello namespace that enables you tooprogrammatically access hello basic features of WCF.</span></span> <span data-ttu-id="ffcd6-148">Шина обслуживания использует множество объектов hello и атрибутов контрактов службы WCF toodefine.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-148">Service Bus uses many of hello objects and attributes of WCF toodefine service contracts.</span></span>

    <span data-ttu-id="ffcd6-149">В обозревателе решений щелкните правой кнопкой мыши проект hello и нажмите кнопку **управление пакетами NuGet...** . Нажмите кнопку hello **Обзор** вкладку, а затем поиск `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-149">In Solution Explorer, right-click hello project, and then click **Manage NuGet Packages...**. Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="ffcd6-150">Убедитесь, что имя проекта hello в hello **версии** поле.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-150">Ensure that hello project name is selected in hello **Version(s)** box.</span></span> <span data-ttu-id="ffcd6-151">Нажмите кнопку **установить**и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-151">Click **Install**, and accept hello terms of use.</span></span>

    ![][3]
4. <span data-ttu-id="ffcd6-152">В обозревателе решений дважды щелкните tooopen файл Program.cs hello, откройте его в редакторе hello, если его еще нет.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-152">In Solution Explorer, double-click hello Program.cs file tooopen it in hello editor, if it is not already open.</span></span>
5. <span data-ttu-id="ffcd6-153">Добавьте hello следующие операторы using в начало hello hello файла:</span><span class="sxs-lookup"><span data-stu-id="ffcd6-153">Add hello following using statements at hello top of hello file:</span></span>

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. <span data-ttu-id="ffcd6-154">Изменить имя пространства имен hello с его имя по умолчанию **EchoService** слишком**Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-154">Change hello namespace name from its default name of **EchoService** too**Microsoft.ServiceBus.Samples**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ffcd6-155">В этом учебнике используется пространство имен hello C# **Microsoft.ServiceBus.Samples**, это пространство имен hello hello на основе контракта управляемого типа, который используется в файле конфигурации hello в hello [клиента WCF hello Настройка](#configure-the-wcf-client) шаг.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-155">This tutorial uses hello C# namespace **Microsoft.ServiceBus.Samples**, which is hello namespace of hello contract-based managed type that is used in hello configuration file in hello [Configure hello WCF client](#configure-the-wcf-client) step.</span></span> <span data-ttu-id="ffcd6-156">Можно задать любое пространство имен, необходимые при выполнении сборки этого примера; Однако hello Учебник не будет работать, если вы измените hello пространства имен контракта hello и службы соответственно, в файле конфигурации приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-156">You can specify any namespace you want when you build this sample; however, hello tutorial will not work unless you then modify hello namespaces of hello contract and service accordingly, in hello application configuration file.</span></span> <span data-ttu-id="ffcd6-157">приветствия имен, указанное в hello App.config, файл должен быть таким же hello hello пространства имен, указанные в файлах C#.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-157">hello namespace specified in hello App.config file must be hello same as hello namespace specified in your C# files.</span></span>
   >
   >
7. <span data-ttu-id="ffcd6-158">Непосредственно после hello `Microsoft.ServiceBus.Samples` объявление пространства имен, но в пространстве имен hello, определите новый интерфейс с именем `IEchoContract` и применить hello `ServiceContractAttribute` интерфейс toohello атрибут со значением пространства имен `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-158">Directly after hello `Microsoft.ServiceBus.Samples` namespace declaration, but within hello namespace, define a new interface named `IEchoContract` and apply hello `ServiceContractAttribute` attribute toohello interface with a namespace value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="ffcd6-159">Значение пространства имен Hello отличается от hello пространства имен, используемого во всей области действия своего кода hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-159">hello namespace value differs from hello namespace that you use throughout hello scope of your code.</span></span> <span data-ttu-id="ffcd6-160">Вместо этого значение hello пространства имен используется как уникальный идентификатор для данного контракта.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-160">Instead, hello namespace value is used as a unique identifier for this contract.</span></span> <span data-ttu-id="ffcd6-161">Явное указание пространства имен hello запрещает значение пространства имен по умолчанию hello toohello имя контракта.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-161">Specifying hello namespace explicitly prevents hello default namespace value from being added toohello contract name.</span></span> <span data-ttu-id="ffcd6-162">Вставьте следующий код после объявления пространства имен hello hello:</span><span class="sxs-lookup"><span data-stu-id="ffcd6-162">Paste hello following code after hello namespace declaration:</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="ffcd6-163">Как правило пространство имен контракта службы hello содержит схему именования, которая содержит сведения о версии.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-163">Typically, hello service contract namespace contains a naming scheme that includes version information.</span></span> <span data-ttu-id="ffcd6-164">Включая сведения о версии в пространство имен контракта службы hello включает службы tooisolate значительные изменения, определяя новый контракт службы с новым пространством имен и предоставляя его в новую конечную точку.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-164">Including version information in hello service contract namespace enables services tooisolate major changes by defining a new service contract with a new namespace and exposing it on a new endpoint.</span></span> <span data-ttu-id="ffcd6-165">Таким образом клиенты можно продолжить без необходимости обновить toobe toouse hello старый контракт службы.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-165">In this manner, clients can continue toouse hello old service contract without having toobe updated.</span></span> <span data-ttu-id="ffcd6-166">Сведения о версии могут включать дату и номер сборки.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-166">Version information can consist of a date or a build number.</span></span> <span data-ttu-id="ffcd6-167">Дополнительные сведения см. в статье [Управление версиями службы](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="ffcd6-167">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="ffcd6-168">Для целей этого учебника hello схему пространства имен контракта службы hello именования hello не содержит сведений о версии.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-168">For hello purposes of this tutorial, hello naming scheme of hello service contract namespace does not contain version information.</span></span>
   >
   >
8. <span data-ttu-id="ffcd6-169">В рамках hello `IEchoContract` интерфейсом, объявите метод для отдельной операции hello hello `IEchoContract` предоставляет контракт в hello интерфейс и применение hello `OperationContractAttribute` метод toohello атрибут, который вы хотите tooexpose как часть hello открытые ретрансляции WCF контракт, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="ffcd6-169">Within hello `IEchoContract` interface, declare a method for hello single operation hello `IEchoContract` contract exposes in hello interface and apply hello `OperationContractAttribute` attribute toohello method that you want tooexpose as part of hello public WCF Relay contract, as follows:</span></span>

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. <span data-ttu-id="ffcd6-170">Непосредственно после hello `IEchoContract` определение интерфейса, объявите канал, который наследует от обоих `IEchoContract` и также toohello `IClientChannel` интерфейс, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="ffcd6-170">Directly after hello `IEchoContract` interface definition, declare a channel that inherits from both `IEchoContract` and also toohello `IClientChannel` interface, as shown here:</span></span>

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    <span data-ttu-id="ffcd6-171">Канал представляет hello объекта WCF, через который hello служба и клиент обмениваются tooeach сведения о других.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-171">A channel is hello WCF object through which hello host and client pass information tooeach other.</span></span> <span data-ttu-id="ffcd6-172">Более поздней версии вы напишете код для hello сведения tooecho канал между двумя приложениями hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-172">Later, you will write code against hello channel tooecho information between hello two applications.</span></span>
10. <span data-ttu-id="ffcd6-173">Из hello **построения** меню, нажмите кнопку **построить решение** или нажмите клавишу **Ctrl + Shift + B** tooconfirm hello правильность выполненной работы до сих.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-173">From hello **Build** menu, click **Build Solution** or press **Ctrl+Shift+B** tooconfirm hello accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="ffcd6-174">Пример</span><span class="sxs-lookup"><span data-stu-id="ffcd6-174">Example</span></span>

<span data-ttu-id="ffcd6-175">Hello после кода показан базовый интерфейс, определяющий контракт ретрансляции WCF.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-175">hello following code shows a basic interface that defines a WCF Relay contract.</span></span>

```csharp
using System;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

<span data-ttu-id="ffcd6-176">Теперь, когда hello интерфейс создан, можно реализовать интерфейс hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-176">Now that hello interface is created, you can implement hello interface.</span></span>

## <a name="implement-hello-wcf-contract"></a><span data-ttu-id="ffcd6-177">Реализация контракта WCF hello</span><span class="sxs-lookup"><span data-stu-id="ffcd6-177">Implement hello WCF contract</span></span>

<span data-ttu-id="ffcd6-178">Создание ретрансляции Azure требуется сначала создать контракт hello, который определен с помощью интерфейса.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-178">Creating an Azure relay requires that you first create hello contract, which is defined by using an interface.</span></span> <span data-ttu-id="ffcd6-179">Дополнительные сведения о создании интерфейса hello см. предыдущий шаг hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-179">For more information about creating hello interface, see hello previous step.</span></span> <span data-ttu-id="ffcd6-180">Hello следующим шагом является интерфейс tooimplement hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-180">hello next step is tooimplement hello interface.</span></span> <span data-ttu-id="ffcd6-181">Это предполагает создание класса с именем `EchoService` , реализующий hello определяемых пользователем `IEchoContract` интерфейса.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-181">This involves creating a class named `EchoService` that implements hello user-defined `IEchoContract` interface.</span></span> <span data-ttu-id="ffcd6-182">После реализации интерфейса hello, необходимо настроить интерфейс hello, с помощью файла конфигурации App.config.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-182">After you implement hello interface, you then configure hello interface using an App.config configuration file.</span></span> <span data-ttu-id="ffcd6-183">Hello файл конфигурации содержит сведения, необходимые для приложения hello, например имя службы hello hello, hello hello контракта и тип протокола, используемые toocommunicate со службой ретрансляции hello hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-183">hello configuration file contains necessary information for hello application, such as hello name of hello service, hello name of hello contract, and hello type of protocol that is used toocommunicate with hello relay service.</span></span> <span data-ttu-id="ffcd6-184">Hello код для выполнения этих задач приведен в примере hello, после процедуры hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-184">hello code used for these tasks is provided in hello example following hello procedure.</span></span> <span data-ttu-id="ffcd6-185">Более общие сведения о как tooimplement службы контракта, в разделе [реализация контрактов службы](https://msdn.microsoft.com/library/ms733764.aspx) в документации по WCF hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-185">For a more general discussion about how tooimplement a service contract, see [Implementing Service Contracts](https://msdn.microsoft.com/library/ms733764.aspx) in hello WCF documentation.</span></span>

1. <span data-ttu-id="ffcd6-186">Создайте новый класс с именем `EchoService` непосредственно после определения hello hello `IEchoContract` интерфейса.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-186">Create a new class named `EchoService` directly after hello definition of hello `IEchoContract` interface.</span></span> <span data-ttu-id="ffcd6-187">Hello `EchoService` класс реализует hello `IEchoContract` интерфейса.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-187">hello `EchoService` class implements hello `IEchoContract` interface.</span></span>

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    <span data-ttu-id="ffcd6-188">Определение hello схожие реализации интерфейса tooother, можно реализовать в другой файл.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-188">Similar tooother interface implementations, you can implement hello definition in a different file.</span></span> <span data-ttu-id="ffcd6-189">Однако в этом учебнике реализация hello расположена в тот же файл определения интерфейса hello и hello hello `Main` метод.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-189">However, for this tutorial, hello implementation is located in hello same file as hello interface definition and hello `Main` method.</span></span>
2. <span data-ttu-id="ffcd6-190">Применить hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) атрибута toohello `IEchoContract` интерфейса.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-190">Apply hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute toohello `IEchoContract` interface.</span></span> <span data-ttu-id="ffcd6-191">атрибут Hello указывает имя службы hello и пространства имен.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-191">hello attribute specifies hello service name and namespace.</span></span> <span data-ttu-id="ffcd6-192">После этого hello `EchoService` класс имеет следующий вид:</span><span class="sxs-lookup"><span data-stu-id="ffcd6-192">After doing so, hello `EchoService` class appears as follows:</span></span>

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. <span data-ttu-id="ffcd6-193">Реализуйте hello `Echo` метода, определенного в hello `IEchoContract` интерфейса в hello `EchoService` класса.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-193">Implement hello `Echo` method defined in hello `IEchoContract` interface in hello `EchoService` class.</span></span>

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. <span data-ttu-id="ffcd6-194">Нажмите кнопку **построения**, нажмите кнопку **построить решение** tooconfirm hello точности своей работы.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-194">Click **Build**, then click **Build Solution** tooconfirm hello accuracy of your work.</span></span>

### <a name="define-hello-configuration-for-hello-service-host"></a><span data-ttu-id="ffcd6-195">Определение конфигурации hello для узла службы hello</span><span class="sxs-lookup"><span data-stu-id="ffcd6-195">Define hello configuration for hello service host</span></span>

1. <span data-ttu-id="ffcd6-196">файл конфигурации Hello — очень похожих файлов конфигурации WCF tooa.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-196">hello configuration file is very similar tooa WCF configuration file.</span></span> <span data-ttu-id="ffcd6-197">Он включает имя службы hello, конечной точки (расположение hello, ретрансляции Azure предоставляет клиентам и узлам toocommunicate друг с другом) и hello привязку (тип протокола, используемые toocommunicate hello).</span><span class="sxs-lookup"><span data-stu-id="ffcd6-197">It includes hello service name, endpoint (that is, hello location that Azure Relay exposes for clients and hosts toocommunicate with each other), and hello binding (hello type of protocol that is used toocommunicate).</span></span> <span data-ttu-id="ffcd6-198">Hello основное отличие состоит в том, что эта конечная точка службы, настроенные ссылается tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) привязки, который не является частью .NET Framework hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-198">hello main difference is that this configured service endpoint refers tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, which is not part of hello .NET Framework.</span></span> <span data-ttu-id="ffcd6-199">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) одна из привязок hello определены службой hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-199">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is one of hello bindings defined by hello service.</span></span>
2. <span data-ttu-id="ffcd6-200">В **обозревателе решений**, tooopen файл App.config hello дважды щелкните его в редакторе Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-200">In **Solution Explorer**, double-click hello App.config file tooopen it in hello Visual Studio editor.</span></span>
3. <span data-ttu-id="ffcd6-201">В hello `<appSettings>` элемента, замените заполнители hello hello имя пространства имен службы и hello ключ SAS, скопированный на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-201">In hello `<appSettings>` element, replace hello placeholders with hello name of your service namespace, and hello SAS key that you copied in an earlier step.</span></span>
4. <span data-ttu-id="ffcd6-202">В рамках hello `<system.serviceModel>` добавление тегов, `<services>` элемент.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-202">Within hello `<system.serviceModel>` tags, add a `<services>` element.</span></span> <span data-ttu-id="ffcd6-203">В отдельном файле конфигурации можно определить несколько приложений ретранслятора.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-203">You can define multiple relay applications in a single configuration file.</span></span> <span data-ttu-id="ffcd6-204">Однако в данном учебнике определяется только одно приложение.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-204">However, this tutorial defines only one.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. <span data-ttu-id="ffcd6-205">В рамках hello `<services>` элемента, добавьте `<service>` элемент toodefine hello имя службы hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-205">Within hello `<services>` element, add a `<service>` element toodefine hello name of hello service.</span></span>

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. <span data-ttu-id="ffcd6-206">В рамках hello `<service>` элемента, определение расположения hello hello контракта конечной точки, а также hello тип привязки для конечной точки hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-206">Within hello `<service>` element, define hello location of hello endpoint contract, and also hello type of binding for hello endpoint.</span></span>

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="ffcd6-207">Hello конечная точка определяет, где hello клиент будет искать ведущее приложение hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-207">hello endpoint defines where hello client will look for hello host application.</span></span> <span data-ttu-id="ffcd6-208">Позже hello учебнике этот шаг toocreate URI, который полностью предоставляет узел hello посредством Azure ретрансляции.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-208">Later, hello tutorial uses this step toocreate a URI that fully exposes hello host through Azure Relay.</span></span> <span data-ttu-id="ffcd6-209">Привязка Hello указывает, что мы используем TCP как hello протокола toocommunicate со службой ретрансляции hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-209">hello binding declares that we are using TCP as hello protocol toocommunicate with hello relay service.</span></span>
7. <span data-ttu-id="ffcd6-210">Из hello **построения** меню, нажмите кнопку **построить решение** tooconfirm hello точности своей работы.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-210">From hello **Build** menu, click **Build Solution** tooconfirm hello accuracy of your work.</span></span>

### <a name="example"></a><span data-ttu-id="ffcd6-211">Пример</span><span class="sxs-lookup"><span data-stu-id="ffcd6-211">Example</span></span>

<span data-ttu-id="ffcd6-212">Hello следующем примере кода показана реализация hello hello контракт службы.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-212">hello following code shows hello implementation of hello service contract.</span></span>

```csharp
[ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]

    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }
```

<span data-ttu-id="ffcd6-213">Hello следующий код показывает hello стандартный формат файла App.config hello, связанный с узлом службы hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-213">hello following code shows hello basic format of hello App.config file associated with hello service host.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceBus.Samples.EchoService">
        <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding" />
      </service>
    </services>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="host-and-run-a-basic-web-service-tooregister-with-hello-relay-service"></a><span data-ttu-id="ffcd6-214">Размещение и запуск tooregister простой службы со службой ретрансляции hello</span><span class="sxs-lookup"><span data-stu-id="ffcd6-214">Host and run a basic web service tooregister with hello relay service</span></span>

<span data-ttu-id="ffcd6-215">В этом разделе описывается, как toorun Azure ретрансляции службы.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-215">This step describes how toorun an Azure Relay service.</span></span>

### <a name="create-hello-relay-credentials"></a><span data-ttu-id="ffcd6-216">Создать учетные данные для ретрансляции hello</span><span class="sxs-lookup"><span data-stu-id="ffcd6-216">Create hello relay credentials</span></span>

1. <span data-ttu-id="ffcd6-217">В `Main()`, создайте две переменные в пространстве имен hello какие toostore и ключ SAS, считываемых из окна консоли hello hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-217">In `Main()`, create two variables in which toostore hello namespace and hello SAS key that are read from hello console window.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    <span data-ttu-id="ffcd6-218">ключ SAS Hello будет tooaccess используется более поздней версии проекта.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-218">hello SAS key will be used later tooaccess your project.</span></span> <span data-ttu-id="ffcd6-219">пространство имен Hello передается как параметр слишком`CreateServiceUri` toocreate URI службы.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-219">hello namespace is passed as a parameter too`CreateServiceUri` toocreate a service URI.</span></span>
2. <span data-ttu-id="ffcd6-220">С помощью [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) объекта, объявите, что вы будете использовать ключ SAS как hello тип учетных данных.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-220">Using a [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, declare that you will be using a SAS key as hello credential type.</span></span> <span data-ttu-id="ffcd6-221">Добавьте следующий код непосредственно после hello код, добавленный в последнем шаге hello hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-221">Add hello following code directly after hello code added in hello last step.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-hello-service"></a><span data-ttu-id="ffcd6-222">Создайте базовый адрес службы hello</span><span class="sxs-lookup"><span data-stu-id="ffcd6-222">Create a base address for hello service</span></span>

<span data-ttu-id="ffcd6-223">После кода hello, добавленный в последнем шаге hello, создайте `Uri` экземпляр hello базового адреса службы hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-223">After hello code you added in hello last step, create a `Uri` instance for hello base address of hello service.</span></span> <span data-ttu-id="ffcd6-224">Этот URI указывает схему Service Bus hello, пространство имен hello и hello путь интерфейса службы hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-224">This URI specifies hello Service Bus scheme, hello namespace, and hello path of hello service interface.</span></span>

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

<span data-ttu-id="ffcd6-225">«sb»-это сокращение для схемы Service Bus hello и указывает, что мы используем hello протокол TCP.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-225">"sb" is an abbreviation for hello Service Bus scheme, and indicates that we are using TCP as hello protocol.</span></span> <span data-ttu-id="ffcd6-226">Это также ранее определено в файле конфигурации hello, когда [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) был указан как hello привязки.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-226">This was also previously indicated in hello configuration file, when [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) was specified as hello binding.</span></span>

<span data-ttu-id="ffcd6-227">В этом учебнике hello URI является `sb://putServiceNamespaceHere.windows.net/EchoService`.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-227">For this tutorial, hello URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.</span></span>

### <a name="create-and-configure-hello-service-host"></a><span data-ttu-id="ffcd6-228">Создание и настройка узла службы hello</span><span class="sxs-lookup"><span data-stu-id="ffcd6-228">Create and configure hello service host</span></span>

1. <span data-ttu-id="ffcd6-229">Установить режим подключения hello слишком`AutoDetect`.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-229">Set hello connectivity mode too`AutoDetect`.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    <span data-ttu-id="ffcd6-230">режим подключения Hello описывает hello протокола hello использует toocommunicate со службой ретрансляции hello; HTTP или TCP.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-230">hello connectivity mode describes hello protocol hello service uses toocommunicate with hello relay service; either HTTP or TCP.</span></span> <span data-ttu-id="ffcd6-231">Использование параметра по умолчанию hello `AutoDetect`, hello служба пытается tooconnect tooAzure ретрансляции через TCP, если он доступен и HTTP, если TCP недоступен.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-231">Using hello default setting `AutoDetect`, hello service attempts tooconnect tooAzure Relay over TCP if it is available, and HTTP if TCP is not available.</span></span> <span data-ttu-id="ffcd6-232">Обратите внимание, что это отличается от службы hello протокола hello указывает для связи с клиентами.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-232">Note that this differs from hello protocol hello service specifies for client communication.</span></span> <span data-ttu-id="ffcd6-233">Этот протокол определяется hello привязку, используемую.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-233">That protocol is determined by hello binding used.</span></span> <span data-ttu-id="ffcd6-234">Например, служба может использовать hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) привязки, который указывает, что ее конечная точка связывается с клиентами по протоколу HTTP.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-234">For example, a service can use hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, which specifies that its endpoint communicates with clients over HTTP.</span></span> <span data-ttu-id="ffcd6-235">Что же службе может указать **ConnectivityMode.AutoDetect** , чтобы служба hello взаимодействует с Azure ретрансляции по протоколу TCP.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-235">That same service could specify **ConnectivityMode.AutoDetect** so that hello service communicates with Azure Relay over TCP.</span></span>
2. <span data-ttu-id="ffcd6-236">Создайте узел службы hello, используя приветствия URI созданного ранее в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-236">Create hello service host, using hello URI created earlier in this section.</span></span>

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    <span data-ttu-id="ffcd6-237">узел службы Hello: hello объекта WCF, создающий экземпляр службы hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-237">hello service host is hello WCF object that instantiates hello service.</span></span> <span data-ttu-id="ffcd6-238">Здесь можно передать его тип hello службы требуется toocreate ( `EchoService` типа) и также toohello адрес, по которому требуется служба tooexpose hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-238">Here, you pass it hello type of service you want toocreate (an `EchoService` type), and also toohello address at which you want tooexpose hello service.</span></span>
3. <span data-ttu-id="ffcd6-239">Вверху hello hello файла Program.cs добавьте ссылки на слишком[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) и [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span><span class="sxs-lookup"><span data-stu-id="ffcd6-239">At hello top of hello Program.cs file, add references too[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) and [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span></span>

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. <span data-ttu-id="ffcd6-240">В `Main()`, настройте hello конечной точки tooenable общего доступа.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-240">Back in `Main()`, configure hello endpoint tooenable public access.</span></span>

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    <span data-ttu-id="ffcd6-241">Это действие позволяет сообщить hello служба ретрансляции, что приложения могут быть найдены публично изучив hello веб-канал ATOM для проекта.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-241">This step informs hello relay service that your application can be found publicly by examining hello ATOM feed for your project.</span></span> <span data-ttu-id="ffcd6-242">Если задать **DiscoveryType** слишком**закрытый**, клиент по-прежнему будет службы может tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-242">If you set **DiscoveryType** too**private**, a client would still be able tooaccess hello service.</span></span> <span data-ttu-id="ffcd6-243">Тем не менее служба hello не будет отображаться, когда он выполняет поиск пространства имен ретрансляции hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-243">However, hello service would not appear when it searches hello Relay namespace.</span></span> <span data-ttu-id="ffcd6-244">Вместо этого клиент hello будет иметь путь конечной точки tooknow hello заранее.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-244">Instead, hello client would have tooknow hello endpoint path beforehand.</span></span>
5. <span data-ttu-id="ffcd6-245">Применить toohello конечные точки, определенные в файле App.config hello, учетные данные службы hello:</span><span class="sxs-lookup"><span data-stu-id="ffcd6-245">Apply hello service credentials toohello service endpoints defined in hello App.config file:</span></span>

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    <span data-ttu-id="ffcd6-246">Как уже говорилось в предыдущем шаге hello, удалось объявлен несколько служб и конечных точек в файле конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-246">As stated in hello previous step, you could have declared multiple services and endpoints in hello configuration file.</span></span> <span data-ttu-id="ffcd6-247">Если у вас есть, передается этот код в файле конфигурации hello и поиска для каждой конечной точки toowhich его следует применять свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-247">If you had, this code would traverse hello configuration file and search for every endpoint toowhich it should apply your credentials.</span></span> <span data-ttu-id="ffcd6-248">Однако в этом учебнике hello файл конфигурации имеет только одну конечную точку.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-248">However, for this tutorial, hello configuration file has only one endpoint.</span></span>

### <a name="open-hello-service-host"></a><span data-ttu-id="ffcd6-249">Привет открыть узел службы</span><span class="sxs-lookup"><span data-stu-id="ffcd6-249">Open hello service host</span></span>

1. <span data-ttu-id="ffcd6-250">Откройте службу hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-250">Open hello service.</span></span>

    ```csharp
    host.Open();
    ```
2. <span data-ttu-id="ffcd6-251">Уведомить пользователя hello, hello служба запущена и объясняется, как tooshut работу службы hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-251">Inform hello user that hello service is running, and explain how tooshut down hello service.</span></span>

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="ffcd6-252">После завершения закройте узел службы hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-252">When finished, close hello service host.</span></span>

    ```csharp
    host.Close();
    ```
4. <span data-ttu-id="ffcd6-253">Нажмите клавишу **Ctrl + Shift + B** toobuild hello проекта.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-253">Press **Ctrl+Shift+B** toobuild hello project.</span></span>

### <a name="example"></a><span data-ttu-id="ffcd6-254">Пример</span><span class="sxs-lookup"><span data-stu-id="ffcd6-254">Example</span></span>

<span data-ttu-id="ffcd6-255">Готовый код службы должен выглядеть так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-255">Your completed service code should appear as follows.</span></span> <span data-ttu-id="ffcd6-256">Код Hello включает hello контракт и реализацию службы из предыдущих шагов в учебнике hello и узлы hello службы в консольном приложении.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-256">hello code includes hello service contract and implementation from previous steps in hello tutorial, and hosts hello service in a console application.</span></span>

```csharp
using System;
using System.ServiceModel;
using System.ServiceModel.Description;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Description;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { };

    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {

            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;         

            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS key: ");
            string sasKey = Console.ReadLine();

           // Create hello credentials object for hello endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create hello service URI based on hello service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create hello service host reading hello configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create hello ServiceRegistrySettings behavior for hello endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add hello Relay credentials tooall endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open hello service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            // Close hello service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-hello-service-contract"></a><span data-ttu-id="ffcd6-257">Создание клиента WCF для контракта службы hello</span><span class="sxs-lookup"><span data-stu-id="ffcd6-257">Create a WCF client for hello service contract</span></span>

<span data-ttu-id="ffcd6-258">Следующий шаг Hello toocreate клиентское приложение и определить hello контракт службы, которая будет создана на последующих этапах.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-258">hello next step is toocreate a client application and define hello service contract you will implement in later steps.</span></span> <span data-ttu-id="ffcd6-259">Обратите внимание, что многие из этих шагов похожие шаги hello использовать toocreate службы: определение контракта, изменение App.config текстовый файл, с помощью службы ретранслятора toohello tooconnect учетные данные и т. д.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-259">Note that many of these steps resemble hello steps used toocreate a service: defining a contract, editing an App.config file, using credentials tooconnect toohello relay service, and so on.</span></span> <span data-ttu-id="ffcd6-260">Hello код для выполнения этих задач приведен в примере hello, после процедуры hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-260">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

1. <span data-ttu-id="ffcd6-261">Создайте новый проект в текущем решении Visual Studio hello для hello клиента, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="ffcd6-261">Create a new project in hello current Visual Studio solution for hello client by doing hello following:</span></span>

   1. <span data-ttu-id="ffcd6-262">В обозревателе решений в решение, содержащее службу hello hello, щелкните правой кнопкой мыши hello текущего решения (не проект hello) и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-262">In Solution Explorer, in hello same solution that contains hello service, right-click hello current solution (not hello project), and click **Add**.</span></span> <span data-ttu-id="ffcd6-263">Выберите **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-263">Then click **New Project**.</span></span>
   2. <span data-ttu-id="ffcd6-264">В hello **Добавление нового проекта** диалоговое окно, нажмите кнопку **Visual C#** (если **Visual C#** не отображается, найдите его в разделе **другие языки**) выберите hello **Консольного приложения (.NET Framework)** шаблона и назовите его **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-264">In hello **Add New Project** dialog box, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**), select hello **Console App (.NET Framework)** template, and name it **EchoClient**.</span></span>
   3. <span data-ttu-id="ffcd6-265">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-265">Click **OK**.</span></span>
      <br />
2. <span data-ttu-id="ffcd6-266">В обозревателе решений дважды щелкните файл Program.cs hello в hello **EchoClient** проекта tooopen, откройте его в редакторе hello, если его еще нет.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-266">In Solution Explorer, double-click hello Program.cs file in hello **EchoClient** project tooopen it in hello editor, if it is not already open.</span></span>
3. <span data-ttu-id="ffcd6-267">Изменить имя пространства имен hello с его имя по умолчанию `EchoClient` слишком`Microsoft.ServiceBus.Samples`.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-267">Change hello namespace name from its default name of `EchoClient` too`Microsoft.ServiceBus.Samples`.</span></span>
4. <span data-ttu-id="ffcd6-268">Установка hello [пакет шины обслуживания NuGet](https://www.nuget.org/packages/WindowsAzure.ServiceBus): в обозревателе решений щелкните правой кнопкой мыши hello **EchoClient** проекта, а затем нажмите кнопку **управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-268">Install hello [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Solution Explorer, right-click hello **EchoClient** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="ffcd6-269">Нажмите кнопку hello **Обзор** вкладку, а затем поиск `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-269">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="ffcd6-270">Нажмите кнопку **установить**и примите условия использования hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-270">Click **Install**, and accept hello terms of use.</span></span>

    ![][3]
5. <span data-ttu-id="ffcd6-271">Добавить `using` инструкции для hello [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) пространства имен в файл Program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-271">Add a `using` statement for hello [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace in hello Program.cs file.</span></span>

    ```csharp
    using System.ServiceModel;
    ```
6. <span data-ttu-id="ffcd6-272">Добавьте hello определения toohello пространства имен контракта службы, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-272">Add hello service contract definition toohello namespace, as shown in hello following example.</span></span> <span data-ttu-id="ffcd6-273">Обратите внимание, что это определение идентичные toohello определение, используемое в hello **службы** проекта.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-273">Note that this definition is identical toohello definition used in hello **Service** project.</span></span> <span data-ttu-id="ffcd6-274">Этот код следует добавить вверху hello hello `Microsoft.ServiceBus.Samples` пространства имен.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-274">You should add this code at hello top of hello `Microsoft.ServiceBus.Samples` namespace.</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. <span data-ttu-id="ffcd6-275">Нажмите клавишу **Ctrl + Shift + B** toobuild hello клиента.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-275">Press **Ctrl+Shift+B** toobuild hello client.</span></span>

### <a name="example"></a><span data-ttu-id="ffcd6-276">Пример</span><span class="sxs-lookup"><span data-stu-id="ffcd6-276">Example</span></span>

<span data-ttu-id="ffcd6-277">Hello следующий код показывает текущее состояние файла Program.cs hello hello в hello **EchoClient** проекта.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-277">hello following code shows hello current status of hello Program.cs file in hello **EchoClient** project.</span></span>

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }


    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="configure-hello-wcf-client"></a><span data-ttu-id="ffcd6-278">Настройка клиента WCF hello</span><span class="sxs-lookup"><span data-stu-id="ffcd6-278">Configure hello WCF client</span></span>

<span data-ttu-id="ffcd6-279">На этом шаге создается файл App.config для простом клиентском приложении, которое обращается к службе hello, созданной ранее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-279">In this step, you create an App.config file for a basic client application that accesses hello service created previously in this tutorial.</span></span> <span data-ttu-id="ffcd6-280">Этот файл App.config определяет hello контракта, привязки и имя конечной точки hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-280">This App.config file defines hello contract, binding, and name of hello endpoint.</span></span> <span data-ttu-id="ffcd6-281">Hello код для выполнения этих задач приведен в примере hello, после процедуры hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-281">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

1. <span data-ttu-id="ffcd6-282">В обозревателе решений в hello **EchoClient** проекта, дважды щелкните **App.config** tooopen hello файл в редакторе Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-282">In Solution Explorer, in hello **EchoClient** project, double-click **App.config** tooopen hello file in hello Visual Studio editor.</span></span>
2. <span data-ttu-id="ffcd6-283">В hello `<appSettings>` элемента, замените заполнители hello hello имя пространства имен службы и hello ключ SAS, скопированный на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-283">In hello `<appSettings>` element, replace hello placeholders with hello name of your service namespace, and hello SAS key that you copied in an earlier step.</span></span>
3. <span data-ttu-id="ffcd6-284">В элементе управления system.serviceModel hello, добавьте `<client>` элемента.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-284">Within hello system.serviceModel element, add a `<client>` element.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    <span data-ttu-id="ffcd6-285">На этом шаге вы объявляете, что определяете клиентское приложение WCF.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-285">This step declares that you are defining a WCF-style client application.</span></span>
4. <span data-ttu-id="ffcd6-286">В рамках hello `client` элемент, определите hello имя контракта и тип привязки для конечной точки hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-286">Within hello `client` element, define hello name, contract, and binding type for hello endpoint.</span></span>

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="ffcd6-287">Этот шаг определяет имя hello hello конечной точки, hello контракт, определенный в службу hello и hello факт, что hello клиентское приложение использует TCP toocommunicate с Azure ретрансляции.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-287">This step defines hello name of hello endpoint, hello contract defined in hello service, and hello fact that hello client application uses TCP toocommunicate with Azure Relay.</span></span> <span data-ttu-id="ffcd6-288">Hello имя конечной точки используется в hello следующий шаг toolink конфигурацию конечной точки URI службы hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-288">hello endpoint name is used in hello next step toolink this endpoint configuration with hello service URI.</span></span>
5. <span data-ttu-id="ffcd6-289">В меню **Файл** выберите **Сохранить все**.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-289">Click **File**, then click **Save All**.</span></span>

## <a name="example"></a><span data-ttu-id="ffcd6-290">Пример</span><span class="sxs-lookup"><span data-stu-id="ffcd6-290">Example</span></span>

<span data-ttu-id="ffcd6-291">Hello код отображает hello файл App.config для клиента Echo hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-291">hello following code shows hello App.config file for hello Echo client.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <client>
      <endpoint name="RelayEndpoint"
                      contract="Microsoft.ServiceBus.Samples.IEchoContract"
                      binding="netTcpRelayBinding"/>
    </client>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="implement-hello-wcf-client"></a><span data-ttu-id="ffcd6-292">Реализуйте клиент WCF hello</span><span class="sxs-lookup"><span data-stu-id="ffcd6-292">Implement hello WCF client</span></span>
<span data-ttu-id="ffcd6-293">На этом шаге вы реализовать простом клиентском приложении, которое обращается к службе hello, созданный ранее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-293">In this step, you implement a basic client application that accesses hello service you created previously in this tutorial.</span></span> <span data-ttu-id="ffcd6-294">Аналогичную службу toohello hello клиент выполняет множество таких hello же операции tooaccess ретрансляции Azure:</span><span class="sxs-lookup"><span data-stu-id="ffcd6-294">Similar toohello service, hello client performs many of hello same operations tooaccess Azure Relay:</span></span>

1. <span data-ttu-id="ffcd6-295">Задает режим подключения hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-295">Sets hello connectivity mode.</span></span>
2. <span data-ttu-id="ffcd6-296">Создает URI расположения узла службы hello hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-296">Creates hello URI that locates hello host service.</span></span>
3. <span data-ttu-id="ffcd6-297">Определяет учетные данные безопасности hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-297">Defines hello security credentials.</span></span>
4. <span data-ttu-id="ffcd6-298">Применяет подключение toohello hello учетные данные.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-298">Applies hello credentials toohello connection.</span></span>
5. <span data-ttu-id="ffcd6-299">Открывает соединение hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-299">Opens hello connection.</span></span>
6. <span data-ttu-id="ffcd6-300">Выполняет задачи, связанные с приложение hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-300">Performs hello application-specific tasks.</span></span>
7. <span data-ttu-id="ffcd6-301">Закрывает соединение hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-301">Closes hello connection.</span></span>

<span data-ttu-id="ffcd6-302">Одно из основных различий hello то, что hello клиентское приложение использует службу ретрансляции toohello tooconnect канала, в то время как hello служба использует вызов слишком**ServiceHost**.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-302">However, one of hello main differences is that hello client application uses a channel tooconnect toohello relay service, whereas hello service uses a call too**ServiceHost**.</span></span> <span data-ttu-id="ffcd6-303">Hello код для выполнения этих задач приведен в примере hello, после процедуры hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-303">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

### <a name="implement-a-client-application"></a><span data-ttu-id="ffcd6-304">Реализация клиентского приложения</span><span class="sxs-lookup"><span data-stu-id="ffcd6-304">Implement a client application</span></span>
1. <span data-ttu-id="ffcd6-305">Установить режим подключения hello слишком**Автообнаружение**.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-305">Set hello connectivity mode too**AutoDetect**.</span></span> <span data-ttu-id="ffcd6-306">Добавьте следующий код внутри hello hello `Main()` метод hello **EchoClient** приложения.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-306">Add hello following code inside hello `Main()` method of hello **EchoClient** application.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. <span data-ttu-id="ffcd6-307">Определите переменные toohold hello значения для пространства имен службы hello и ключ SAS, считываемых с консоли hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-307">Define variables toohold hello values for hello service namespace, and SAS key that are read from hello console.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. <span data-ttu-id="ffcd6-308">Создайте hello URI, определяющий расположение узла hello hello в проекте ретрансляции.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-308">Create hello URI that defines hello location of hello host in your Relay project.</span></span>

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. <span data-ttu-id="ffcd6-309">Создайте hello объекта учетных данных для конечной точки пространства имен службы.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-309">Create hello credential object for your service namespace endpoint.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. <span data-ttu-id="ffcd6-310">Создайте фабрику каналов hello, загружает конфигурацию hello, описанных в файле App.config hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-310">Create hello channel factory that loads hello configuration described in hello App.config file.</span></span>

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    <span data-ttu-id="ffcd6-311">Фабрику каналов является объектом WCF, который создает канал, через который взаимодействия служб и клиентских приложений hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-311">A channel factory is a WCF object that creates a channel through which hello service and client applications communicate.</span></span>
6. <span data-ttu-id="ffcd6-312">Примените учетные данные hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-312">Apply hello credentials.</span></span>

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. <span data-ttu-id="ffcd6-313">Создайте и откройте hello канала toohello службы.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-313">Create and open hello channel toohello service.</span></span>

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. <span data-ttu-id="ffcd6-314">Запись hello основной пользовательский интерфейс и функциональные возможности для hello echo.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-314">Write hello basic user interface and functionality for hello echo.</span></span>

    ```csharp
    Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
    string input = Console.ReadLine();
    while (input != String.Empty)
    {
        try
        {
            Console.WriteLine("Server echoed: {0}", channel.Echo(input));
        }
        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.Message);
        }
        input = Console.ReadLine();
    }
    ```

    <span data-ttu-id="ffcd6-315">Обратите внимание, что hello код использует экземпляр hello hello объекта канала как прокси для службы hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-315">Note that hello code uses hello instance of hello channel object as a proxy for hello service.</span></span>
9. <span data-ttu-id="ffcd6-316">Закройте канал hello и закрыть hello фабрики.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-316">Close hello channel, and close hello factory.</span></span>

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a><span data-ttu-id="ffcd6-317">Пример</span><span class="sxs-lookup"><span data-stu-id="ffcd6-317">Example</span></span>

<span data-ttu-id="ffcd6-318">Отображается как toocreate клиентского приложения, как toocall hello операции службы hello и как tooclose hello клиента после операции hello вызвать завершения завершенного код должен выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-318">Your completed code should appear as follows, showing how toocreate a client application, how toocall hello operations of hello service, and how tooclose hello client after hello operation call is finished.</span></span>

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;


            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS Key: ");
            string sasKey = Console.ReadLine();



            Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));

            channelFactory.Endpoint.Behaviors.Add(sasCredential);

            IEchoChannel channel = channelFactory.CreateChannel();
            channel.Open();

            Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
            string input = Console.ReadLine();
            while (input != String.Empty)
            {
                try
                {
                    Console.WriteLine("Server echoed: {0}", channel.Echo(input));
                }
                catch (Exception e)
                {
                    Console.WriteLine("Error: " + e.Message);
                }
                input = Console.ReadLine();
            }

            channel.Close();
            channelFactory.Close();

        }
    }
}
```

## <a name="run-hello-applications"></a><span data-ttu-id="ffcd6-319">Запускать приложения hello</span><span class="sxs-lookup"><span data-stu-id="ffcd6-319">Run hello applications</span></span>

1. <span data-ttu-id="ffcd6-320">Нажмите клавишу **Ctrl + Shift + B** toobuild hello решения.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-320">Press **Ctrl+Shift+B** toobuild hello solution.</span></span> <span data-ttu-id="ffcd6-321">При этом строится hello клиентский проект и проект службы hello, созданный на предыдущих этапах hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-321">This builds both hello client project and hello service project that you created in hello previous steps.</span></span>
2. <span data-ttu-id="ffcd6-322">Перед запущенному hello клиентскому приложению необходимо убедитесь, что приложение hello-служба запущена.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-322">Before running hello client application, you must make sure that hello service application is running.</span></span> <span data-ttu-id="ffcd6-323">В обозревателе решений в Visual Studio, щелкните правой кнопкой мыши hello **EchoService** решение, нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-323">In Solution Explorer in Visual Studio, right-click hello **EchoService** solution, then click **Properties**.</span></span>
3. <span data-ttu-id="ffcd6-324">В диалоговое окно «Свойства» для hello решение, нажмите кнопку **запускаемый проект**, нажмите кнопку hello **несколько запускаемых проектов** кнопки.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-324">In hello solution properties dialog box, click **Startup Project**, then click hello **Multiple startup projects** button.</span></span> <span data-ttu-id="ffcd6-325">Убедитесь, что **EchoService** отображается первым в списке hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-325">Make sure **EchoService** appears first in hello list.</span></span>
4. <span data-ttu-id="ffcd6-326">Набор hello **действия** поле для обоих hello **EchoService** и **EchoClient** проекты слишком**запустить**.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-326">Set hello **Action** box for both hello **EchoService** and **EchoClient** projects too**Start**.</span></span>

    ![][5]
5. <span data-ttu-id="ffcd6-327">Щелкните **Зависимости проектов**.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-327">Click **Project Dependencies**.</span></span> <span data-ttu-id="ffcd6-328">В hello **проекты** выберите **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-328">In hello **Projects** box, select **EchoClient**.</span></span> <span data-ttu-id="ffcd6-329">В hello **зависит от** убедитесь, что **EchoService** проверяется.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-329">In hello **Depends on** box, make sure **EchoService** is checked.</span></span>

    ![][6]
6. <span data-ttu-id="ffcd6-330">Нажмите кнопку **ОК** toodismiss hello **свойства** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-330">Click **OK** toodismiss hello **Properties** dialog.</span></span>
7. <span data-ttu-id="ffcd6-331">Нажмите клавишу **F5** toorun обоих проектов.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-331">Press **F5** toorun both projects.</span></span>
8. <span data-ttu-id="ffcd6-332">В обоих окнах консоли откройте и указать имя пространства имен hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-332">Both console windows open and prompt you for hello namespace name.</span></span> <span data-ttu-id="ffcd6-333">Hello служба должна запускаться сначала, поэтому в hello **EchoService** окна консоли введите пространство имен hello и нажмите клавишу **ввод**.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-333">hello service must run first, so in hello **EchoService** console window, enter hello namespace and then press **Enter**.</span></span>
9. <span data-ttu-id="ffcd6-334">Далее появится запрос на ввод ключа SAS.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-334">Next, you are prompted for your SAS key.</span></span> <span data-ttu-id="ffcd6-335">Введите ключ SAS hello и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-335">Enter hello SAS key and press ENTER.</span></span>

    <span data-ttu-id="ffcd6-336">Ниже приведен пример выходных данных из окна консоли hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-336">Here is example output from hello console window.</span></span> <span data-ttu-id="ffcd6-337">Обратите внимание, что значения hello приведены здесь пример исключительно в целях.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-337">Note that hello values provided here are for example purposes only.</span></span>

    <span data-ttu-id="ffcd6-338">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span><span class="sxs-lookup"><span data-stu-id="ffcd6-338">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span></span>

    <span data-ttu-id="ffcd6-339">приложение службы Hello печатает toohello окна консоли hello адрес, который он прослушивает, как видно в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-339">hello service application prints toohello console window hello address on which it's listening, as seen in hello following example.</span></span>

    <span data-ttu-id="ffcd6-340">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`</span><span class="sxs-lookup"><span data-stu-id="ffcd6-340">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`</span></span>
10. <span data-ttu-id="ffcd6-341">В hello **EchoClient** окно консоли, введите hello же сведения, введенные ранее для приложения службы hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-341">In hello **EchoClient** console window, enter hello same information that you entered previously for hello service application.</span></span> <span data-ttu-id="ffcd6-342">Выполните hello предыдущего действия tooenter hello одинаковое пространство имен службы и SAS ключевые значения для клиентского приложения hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-342">Follow hello previous steps tooenter hello same service namespace and SAS key values for hello client application.</span></span>
11. <span data-ttu-id="ffcd6-343">После ввода значений, клиент hello открывает канал toohello службы и предлагает вам tooenter текст, как показано в следующий пример выходных данных консоли hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-343">After entering these values, hello client opens a channel toohello service and prompts you tooenter some text as seen in hello following console output example.</span></span>

    `Enter text tooecho (or [Enter] tooexit):`

    <span data-ttu-id="ffcd6-344">Введите некоторые приложения службы toohello toosend текст и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-344">Enter some text toosend toohello service application and press Enter.</span></span> <span data-ttu-id="ffcd6-345">Этот текст отправляется службе toohello через hello эхо-повтор операции службы, отображается в окне консоли службы hello как hello следующий пример выходных данных.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-345">This text is sent toohello service through hello Echo service operation and appears in hello service console window as in hello following example output.</span></span>

    `Echoing: My sample text`

    <span data-ttu-id="ffcd6-346">клиентское приложение Hello получает возвращаемое значение hello hello `Echo` операцию, которая является исходный текст hello и печатает его в окно консоли tooits.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-346">hello client application receives hello return value of hello `Echo` operation, which is hello original text, and prints it tooits console window.</span></span> <span data-ttu-id="ffcd6-347">Hello ниже приведен пример выходных данных в окне консоли клиента hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-347">hello following is example output from hello client console window.</span></span>

    `Server echoed: My sample text`
12. <span data-ttu-id="ffcd6-348">Можно продолжить отправлять текстовые сообщения от службы toohello hello клиента таким образом.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-348">You can continue sending text messages from hello client toohello service in this manner.</span></span> <span data-ttu-id="ffcd6-349">Когда закончите, нажмите клавишу ВВОД в hello клиента и службы консоли windows tooend обоих приложений.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-349">When you are finished, press Enter in hello client and service console windows tooend both applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffcd6-350">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ffcd6-350">Next steps</span></span>

<span data-ttu-id="ffcd6-351">Этого учебника было показано, как toobuild клиентского приложения Azure ретрансляции и службы с помощью hello возможности ретрансляции WCF Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-351">This tutorial showed how toobuild an Azure Relay client application and service using hello WCF Relay capabilities of Service Bus.</span></span> <span data-ttu-id="ffcd6-352">Аналогичное руководство по [обмену сообщениями в служебной шине](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging) представлено в статье [Начало работы с очередями служебной шины](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="ffcd6-352">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="ffcd6-353">toolearn Дополнительные сведения о ретрансляции Azure см. следующие разделы hello.</span><span class="sxs-lookup"><span data-stu-id="ffcd6-353">toolearn more about Azure Relay, see hello following topics.</span></span>

* [<span data-ttu-id="ffcd6-354">Обзор архитектуры служебной шины Azure</span><span class="sxs-lookup"><span data-stu-id="ffcd6-354">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [<span data-ttu-id="ffcd6-355">Что такое ретранслятор Azure?</span><span class="sxs-lookup"><span data-stu-id="ffcd6-355">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="ffcd6-356">Как службу в .NET Framework посредника toouse hello WCF</span><span class="sxs-lookup"><span data-stu-id="ffcd6-356">How toouse hello WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
