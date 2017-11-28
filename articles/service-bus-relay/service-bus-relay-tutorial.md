---
title: "Руководство по использованию ретранслятора WCF служебной шины Azure | Документация Майкрософт"
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
ms.openlocfilehash: 5347bf85cad32b59677369d51a1f36529aef6662
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-wcf-relay-tutorial"></a><span data-ttu-id="b125d-103">Руководство по ретранслятору WCF Azure</span><span class="sxs-lookup"><span data-stu-id="b125d-103">Azure WCF Relay tutorial</span></span>

<span data-ttu-id="b125d-104">В этом руководстве описывается создание простого клиентского приложения ретранслятора WCF и службы ретрансляции WCF с помощью ретранслятора Azure.</span><span class="sxs-lookup"><span data-stu-id="b125d-104">This tutorial describes how to build a simple WCF Relay client application and service using Azure Relay.</span></span> <span data-ttu-id="b125d-105">Аналогичное руководство по [обмену сообщениями в служебной шине](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging) представлено в статье [Начало работы с очередями служебной шины](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="b125d-105">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="b125d-106">Выполнив задания в этом руководстве, вы получите представление о том, как создать клиентское приложение ретранслятора WCF и службу ретрансляции WCF.</span><span class="sxs-lookup"><span data-stu-id="b125d-106">Working through this tutorial gives you an understanding of the steps that are required to create a WCF Relay client and service application.</span></span> <span data-ttu-id="b125d-107">Как и в WCF, под службой понимается конструкция, которая предоставляет одну или несколько конечных точек, каждая из которых предоставляет одну или несколько операций службы.</span><span class="sxs-lookup"><span data-stu-id="b125d-107">Like their original WCF counterparts, a service is a construct that exposes one or more endpoints, each of which exposes one or more service operations.</span></span> <span data-ttu-id="b125d-108">Конечная точка службы задает адрес, по которому можно найти службу, привязку, содержащую сведения, которые клиент должен передавать службе, а также контракт, определяющий функциональность, предоставляемую службой клиентам.</span><span class="sxs-lookup"><span data-stu-id="b125d-108">The endpoint of a service specifies an address where the service can be found, a binding that contains the information that a client must communicate with the service, and a contract that defines the functionality provided by the service to its clients.</span></span> <span data-ttu-id="b125d-109">Основное отличие между WCF и ретранслятором WCF состоит в том, что в последнем конечная точка размещается в облаке, а не на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="b125d-109">The main difference between WCF and WCF Relay is that the endpoint is exposed in the cloud instead of locally on your computer.</span></span>

<span data-ttu-id="b125d-110">Проработав это руководство, вы создадите рабочую службу и клиент, который сможет вызывать операции службы.</span><span class="sxs-lookup"><span data-stu-id="b125d-110">After you work through the sequence of topics in this tutorial, you will have a running service, and a client that can invoke the operations of the service.</span></span> <span data-ttu-id="b125d-111">В первом разделе мы рассмотрим процесс настройки учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b125d-111">The first topic describes how to set up an account.</span></span> <span data-ttu-id="b125d-112">В последующих разделах описывается определение службы, использующей контракт, способы реализации службы и настройка службы с помощью кода.</span><span class="sxs-lookup"><span data-stu-id="b125d-112">The next steps describe how to define a service that uses a contract, how to implement the service, and how to configure the service in code.</span></span> <span data-ttu-id="b125d-113">В них также описывается размещение и запуск службы.</span><span class="sxs-lookup"><span data-stu-id="b125d-113">They also describe how to host and run the service.</span></span> <span data-ttu-id="b125d-114">Создаваемая служба является резидентной, то есть и клиент, и служба выполняются на одном компьютере.</span><span class="sxs-lookup"><span data-stu-id="b125d-114">The service that is created is self-hosted and the client and service run on the same computer.</span></span> <span data-ttu-id="b125d-115">Вы можете настроить службу с помощью кода или файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b125d-115">You can configure the service by using either code or a configuration file.</span></span>

<span data-ttu-id="b125d-116">В заключительных трех действиях описывается создание клиентского приложения, его настройка, а также создание и запуск клиента с доступом к функциональности хоста.</span><span class="sxs-lookup"><span data-stu-id="b125d-116">The final three steps describe how to create a client application, configure the client application, and create and use a client that can access the functionality of the host.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b125d-117">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b125d-117">Prerequisites</span></span>

<span data-ttu-id="b125d-118">Для работы с этим учебником требуется:</span><span class="sxs-lookup"><span data-stu-id="b125d-118">To complete this tutorial, you'll need the following:</span></span>

* <span data-ttu-id="b125d-119">[Microsoft Visual Studio 2015 или более поздней версии](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="b125d-119">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="b125d-120">В этом учебнике используется Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b125d-120">This tutorial uses Visual Studio 2017.</span></span>
* <span data-ttu-id="b125d-121">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="b125d-121">An active Azure account.</span></span> <span data-ttu-id="b125d-122">Если ее нет, можно создать бесплатную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="b125d-122">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="b125d-123">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b125d-123">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="b125d-124">Создание пространства имен службы</span><span class="sxs-lookup"><span data-stu-id="b125d-124">Create a service namespace</span></span>

<span data-ttu-id="b125d-125">Сначала необходимо создать пространство имен и получить ключ [подписанного URL-адреса (SAS)](../service-bus-messaging/service-bus-sas.md).</span><span class="sxs-lookup"><span data-stu-id="b125d-125">The first step is to create a namespace, and to obtain a [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) key.</span></span> <span data-ttu-id="b125d-126">Пространство имен определяет границы каждого приложения, предоставляемого через службу ретрансляции.</span><span class="sxs-lookup"><span data-stu-id="b125d-126">A namespace provides an application boundary for each application exposed through the relay service.</span></span> <span data-ttu-id="b125d-127">Ключ SAS автоматически создается системой при создании пространства имен службы.</span><span class="sxs-lookup"><span data-stu-id="b125d-127">A SAS key is automatically generated by the system when a service namespace is created.</span></span> <span data-ttu-id="b125d-128">Сочетание пространства имен и ключа SAS образует учетные данные, на основе которых Azure осуществляет аутентификацию доступа к приложению.</span><span class="sxs-lookup"><span data-stu-id="b125d-128">The combination of service namespace and SAS key provides the credentials for Azure to authenticate access to an application.</span></span> <span data-ttu-id="b125d-129">Выполните [эти инструкции](relay-create-namespace-portal.md), чтобы создать пространство имен ретранслятора.</span><span class="sxs-lookup"><span data-stu-id="b125d-129">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="define-a-wcf-service-contract"></a><span data-ttu-id="b125d-130">Определение контракта службы WCF</span><span class="sxs-lookup"><span data-stu-id="b125d-130">Define a WCF service contract</span></span>

<span data-ttu-id="b125d-131">Контракт службы указывает, какие операции поддерживает служба (в контексте веб-служб под операциями понимаются методы и функции).</span><span class="sxs-lookup"><span data-stu-id="b125d-131">The service contract specifies what operations (the web service terminology for methods or functions) the service supports.</span></span> <span data-ttu-id="b125d-132">Контракты создаются путем определения интерфейса C++, C# или Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="b125d-132">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="b125d-133">Каждый метод в интерфейсе соответствует определенной операции службы.</span><span class="sxs-lookup"><span data-stu-id="b125d-133">Each method in the interface corresponds to a specific service operation.</span></span> <span data-ttu-id="b125d-134">К каждому интерфейсу должен быть применен атрибут [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx), а к каждой операции— атрибут [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx).</span><span class="sxs-lookup"><span data-stu-id="b125d-134">Each interface must have the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute applied to it, and each operation must have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute applied to it.</span></span> <span data-ttu-id="b125d-135">Если у метода в интерфейсе с атрибутом [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) нет атрибута [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), то он не предоставляется.</span><span class="sxs-lookup"><span data-stu-id="b125d-135">If a method in an interface that has the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute does not have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute, that method is not exposed.</span></span> <span data-ttu-id="b125d-136">Код для выполнения задач приведен в примерах после описания последовательности действий.</span><span class="sxs-lookup"><span data-stu-id="b125d-136">The code for these tasks is provided in the example following the procedure.</span></span> <span data-ttu-id="b125d-137">Подробное обсуждение контрактов и служб см. в статье [Разработка и реализация служб](https://msdn.microsoft.com/library/ms729746.aspx) в документации по WCF.</span><span class="sxs-lookup"><span data-stu-id="b125d-137">For a larger discussion of contracts and services, see [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in the WCF documentation.</span></span>

### <a name="create-a-relay-contract-with-an-interface"></a><span data-ttu-id="b125d-138">Создание контракта ретранслятора с помощью интерфейса</span><span class="sxs-lookup"><span data-stu-id="b125d-138">Create a relay contract with an interface</span></span>

1. <span data-ttu-id="b125d-139">Откройте Visual Studio с правами администратора, щелкнув правой кнопкой мыши имя программы в меню **Пуск** и выбрав пункт **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="b125d-139">Open Visual Studio as an administrator by right-clicking the program in the **Start** menu and selecting **Run as administrator**.</span></span>
2. <span data-ttu-id="b125d-140">Создайте новый проект консольного приложения.</span><span class="sxs-lookup"><span data-stu-id="b125d-140">Create a new console application project.</span></span> <span data-ttu-id="b125d-141">В меню **Файл** выберите **Создать**, а затем — **Проект**.</span><span class="sxs-lookup"><span data-stu-id="b125d-141">Click the **File** menu and select **New**, then click **Project**.</span></span> <span data-ttu-id="b125d-142">В диалоговом окне **Новый проект** нажмите кнопку **Visual C#** (если **Visual C#** не отображается, откройте список **Другие языки**).</span><span class="sxs-lookup"><span data-stu-id="b125d-142">In the **New Project** dialog, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**).</span></span> <span data-ttu-id="b125d-143">Выберите шаблон **Консольное приложение (.NET Framework)** и назовите его **EchoService**.</span><span class="sxs-lookup"><span data-stu-id="b125d-143">Click the **Console App (.NET Framework)** template, and name it **EchoService**.</span></span> <span data-ttu-id="b125d-144">Нажмите кнопку **ОК** , чтобы создать проект.</span><span class="sxs-lookup"><span data-stu-id="b125d-144">Click **OK** to create the project.</span></span>

    ![][2]

3. <span data-ttu-id="b125d-145">Установка пакета NuGet для служебной шины.</span><span class="sxs-lookup"><span data-stu-id="b125d-145">Install the Service Bus NuGet package.</span></span> <span data-ttu-id="b125d-146">Этот пакет автоматически добавляет ссылки на библиотеки служебной шины, а также элемент WCF **System.ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="b125d-146">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span></span> <span data-ttu-id="b125d-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) — это пространство имен, которое предоставляет программный доступ к основным функциям WCF.</span><span class="sxs-lookup"><span data-stu-id="b125d-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is the namespace that enables you to programmatically access the basic features of WCF.</span></span> <span data-ttu-id="b125d-148">Служебная шина использует множество объектов и атрибутов WCF для определения контрактов службы.</span><span class="sxs-lookup"><span data-stu-id="b125d-148">Service Bus uses many of the objects and attributes of WCF to define service contracts.</span></span>

    <span data-ttu-id="b125d-149">В обозревателе решений щелкните правой кнопкой мыши проект и выберите пункт **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b125d-149">In Solution Explorer, right-click the project, and then click **Manage NuGet Packages...**.</span></span> <span data-ttu-id="b125d-150">Щелкните вкладку **Обзор** и выполните поиск `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="b125d-150">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="b125d-151">Убедитесь, что имя проекта указано в поле **Версии**.</span><span class="sxs-lookup"><span data-stu-id="b125d-151">Ensure that the project name is selected in the **Version(s)** box.</span></span> <span data-ttu-id="b125d-152">Щелкните **Установить**и примите условия использования.</span><span class="sxs-lookup"><span data-stu-id="b125d-152">Click **Install**, and accept the terms of use.</span></span>

    ![][3]
4. <span data-ttu-id="b125d-153">В обозревателе решений дважды щелкните файл Program.cs, чтобы открыть его в редакторе.</span><span class="sxs-lookup"><span data-stu-id="b125d-153">In Solution Explorer, double-click the Program.cs file to open it in the editor, if it is not already open.</span></span>
5. <span data-ttu-id="b125d-154">Добавьте в начало файла следующие операторы using:</span><span class="sxs-lookup"><span data-stu-id="b125d-154">Add the following using statements at the top of the file:</span></span>

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. <span data-ttu-id="b125d-155">Замените имя пространства имен по умолчанию (**EchoService**) именем **Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="b125d-155">Change the namespace name from its default name of **EchoService** to **Microsoft.ServiceBus.Samples**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="b125d-156">В этом руководстве используется пространство имен C# **Microsoft.ServiceBus.Samples**. Оно относится к управляемому типу на основе контракта и используется в файле конфигурации на этапе [настройки клиента WCF](#configure-the-wcf-client).</span><span class="sxs-lookup"><span data-stu-id="b125d-156">This tutorial uses the C# namespace **Microsoft.ServiceBus.Samples**, which is the namespace of the contract-based managed type that is used in the configuration file in the [Configure the WCF client](#configure-the-wcf-client) step.</span></span> <span data-ttu-id="b125d-157">Для компиляции примера можно указать любое пространство имен. Однако при этом потребуется соответствующим образом изменить пространства имен контракта и службы в файле конфигурации приложения.</span><span class="sxs-lookup"><span data-stu-id="b125d-157">You can specify any namespace you want when you build this sample; however, the tutorial will not work unless you then modify the namespaces of the contract and service accordingly, in the application configuration file.</span></span> <span data-ttu-id="b125d-158">В файле App.config должно быть указано то же самое пространство имен, что и в файлах C#.</span><span class="sxs-lookup"><span data-stu-id="b125d-158">The namespace specified in the App.config file must be the same as the namespace specified in your C# files.</span></span>
   >
   >
7. <span data-ttu-id="b125d-159">Сразу после объявления пространства имен `Microsoft.ServiceBus.Samples`, но внутри этого пространства, определите новый интерфейс `IEchoContract` и примените к нему атрибут `ServiceContractAttribute` со значением `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="b125d-159">Directly after the `Microsoft.ServiceBus.Samples` namespace declaration, but within the namespace, define a new interface named `IEchoContract` and apply the `ServiceContractAttribute` attribute to the interface with a namespace value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="b125d-160">Значение пространства имен отличается от пространства имен, которое используется во всей области кода.</span><span class="sxs-lookup"><span data-stu-id="b125d-160">The namespace value differs from the namespace that you use throughout the scope of your code.</span></span> <span data-ttu-id="b125d-161">Оно используется в качестве уникального идентификатора данного контракта.</span><span class="sxs-lookup"><span data-stu-id="b125d-161">Instead, the namespace value is used as a unique identifier for this contract.</span></span> <span data-ttu-id="b125d-162">Явное указание пространства позволяет предотвратить добавление значение пространства имен по умолчанию к имени контракта.</span><span class="sxs-lookup"><span data-stu-id="b125d-162">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span></span> <span data-ttu-id="b125d-163">Вставьте приведенный ниже фрагмент кода после объявления пространства имен.</span><span class="sxs-lookup"><span data-stu-id="b125d-163">Paste the following code after the namespace declaration:</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="b125d-164">Как правило, пространство имен контракта службы содержит схему именования, которая включает сведения о версии.</span><span class="sxs-lookup"><span data-stu-id="b125d-164">Typically, the service contract namespace contains a naming scheme that includes version information.</span></span> <span data-ttu-id="b125d-165">Включение сведений о версии в пространство имен контракта службы позволяет службам выносить значительные изменения в новый контракт службы с новым пространством имен и предоставлять к нему доступ через новую конечную точку.</span><span class="sxs-lookup"><span data-stu-id="b125d-165">Including version information in the service contract namespace enables services to isolate major changes by defining a new service contract with a new namespace and exposing it on a new endpoint.</span></span> <span data-ttu-id="b125d-166">Таким образом, клиенты могут продолжать использовать старый контракт службы без обновлений.</span><span class="sxs-lookup"><span data-stu-id="b125d-166">In this manner, clients can continue to use the old service contract without having to be updated.</span></span> <span data-ttu-id="b125d-167">Сведения о версии могут включать дату и номер сборки.</span><span class="sxs-lookup"><span data-stu-id="b125d-167">Version information can consist of a date or a build number.</span></span> <span data-ttu-id="b125d-168">Дополнительные сведения см. в статье [Управление версиями службы](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="b125d-168">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="b125d-169">Схема именования пространства имен контракта службы, используемая в этом учебнике, не включает сведения о версии.</span><span class="sxs-lookup"><span data-stu-id="b125d-169">For the purposes of this tutorial, the naming scheme of the service contract namespace does not contain version information.</span></span>
   >
   >
8. <span data-ttu-id="b125d-170">В интерфейсе `IEchoContract` объявите метод для отдельной операции, которую контракт `IEchoContract` предоставляет в интерфейсе. Затем примените атрибут `OperationContractAttribute` к методу, который требуется предоставить как часть общедоступного контракта ретранслятора WCF, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b125d-170">Within the `IEchoContract` interface, declare a method for the single operation the `IEchoContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public WCF Relay contract, as follows:</span></span>

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. <span data-ttu-id="b125d-171">Сразу после определения интерфейса `IEchoContract` объявите канал, наследующий от интерфейсов `IEchoContract` и `IClientChannel`, как показано здесь:</span><span class="sxs-lookup"><span data-stu-id="b125d-171">Directly after the `IEchoContract` interface definition, declare a channel that inherits from both `IEchoContract` and also to the `IClientChannel` interface, as shown here:</span></span>

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    <span data-ttu-id="b125d-172">Канал представляет собой объект WCF, посредством которого служба и клиент обмениваются информацией.</span><span class="sxs-lookup"><span data-stu-id="b125d-172">A channel is the WCF object through which the host and client pass information to each other.</span></span> <span data-ttu-id="b125d-173">Далее мы напишем код канала для обмена данными между двумя приложениями.</span><span class="sxs-lookup"><span data-stu-id="b125d-173">Later, you will write code against the channel to echo information between the two applications.</span></span>
10. <span data-ttu-id="b125d-174">В меню **Сборка** выберите **Собрать решение** или нажмите сочетание клавиш **CTRL+SHIFT+B**, чтобы проверить правильность выполнения действий.</span><span class="sxs-lookup"><span data-stu-id="b125d-174">From the **Build** menu, click **Build Solution** or press **Ctrl+Shift+B** to confirm the accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="b125d-175">Пример</span><span class="sxs-lookup"><span data-stu-id="b125d-175">Example</span></span>

<span data-ttu-id="b125d-176">Ниже приведен код базового интерфейса, определяющего контракт ретранслятора WCF.</span><span class="sxs-lookup"><span data-stu-id="b125d-176">The following code shows a basic interface that defines a WCF Relay contract.</span></span>

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

<span data-ttu-id="b125d-177">Теперь, когда интерфейс создан, можно его реализовать.</span><span class="sxs-lookup"><span data-stu-id="b125d-177">Now that the interface is created, you can implement the interface.</span></span>

## <a name="implement-the-wcf-contract"></a><span data-ttu-id="b125d-178">Реализация контракта WCF</span><span class="sxs-lookup"><span data-stu-id="b125d-178">Implement the WCF contract</span></span>

<span data-ttu-id="b125d-179">Прежде чем создавать ретранслятор Azure, необходимо создать контракт, который определяется с помощью интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b125d-179">Creating an Azure relay requires that you first create the contract, which is defined by using an interface.</span></span> <span data-ttu-id="b125d-180">Сведения о создании интерфейса см. в описании предыдущего шага.</span><span class="sxs-lookup"><span data-stu-id="b125d-180">For more information about creating the interface, see the previous step.</span></span> <span data-ttu-id="b125d-181">Следующим шагом является реализация интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b125d-181">The next step is to implement the interface.</span></span> <span data-ttu-id="b125d-182">Она предполагает создание класса с именем `EchoService`, который реализует пользовательский интерфейс `IEchoContract`.</span><span class="sxs-lookup"><span data-stu-id="b125d-182">This involves creating a class named `EchoService` that implements the user-defined `IEchoContract` interface.</span></span> <span data-ttu-id="b125d-183">После реализации интерфейса необходимо настроить его с помощью файла конфигурации App.config.</span><span class="sxs-lookup"><span data-stu-id="b125d-183">After you implement the interface, you then configure the interface using an App.config configuration file.</span></span> <span data-ttu-id="b125d-184">Файл конфигурации содержит сведения, необходимые для приложения, такие как имя службы, имя контракта и тип протокола, используемого для взаимодействия с службой ретрансляции.</span><span class="sxs-lookup"><span data-stu-id="b125d-184">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span></span> <span data-ttu-id="b125d-185">Код для выполнения этих задач приведен в примере после описания последовательности выполнения действий.</span><span class="sxs-lookup"><span data-stu-id="b125d-185">The code used for these tasks is provided in the example following the procedure.</span></span> <span data-ttu-id="b125d-186">Общие сведения о реализации контракта службы см. в статье [Реализация контрактов служб](https://msdn.microsoft.com/library/ms733764.aspx) в документации WCF.</span><span class="sxs-lookup"><span data-stu-id="b125d-186">For a more general discussion about how to implement a service contract, see [Implementing Service Contracts](https://msdn.microsoft.com/library/ms733764.aspx) in the WCF documentation.</span></span>

1. <span data-ttu-id="b125d-187">Создайте новый класс с именем `EchoService` сразу после определения интерфейса `IEchoContract`.</span><span class="sxs-lookup"><span data-stu-id="b125d-187">Create a new class named `EchoService` directly after the definition of the `IEchoContract` interface.</span></span> <span data-ttu-id="b125d-188">Класс `EchoService` реализует интерфейс `IEchoContract`.</span><span class="sxs-lookup"><span data-stu-id="b125d-188">The `EchoService` class implements the `IEchoContract` interface.</span></span>

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    <span data-ttu-id="b125d-189">Как и в случае с другими реализациями интерфейсов, определение можно реализовать в другом файле.</span><span class="sxs-lookup"><span data-stu-id="b125d-189">Similar to other interface implementations, you can implement the definition in a different file.</span></span> <span data-ttu-id="b125d-190">В этом учебнике реализация включается в тот же файл, что и определение интерфейса и метод `Main`.</span><span class="sxs-lookup"><span data-stu-id="b125d-190">However, for this tutorial, the implementation is located in the same file as the interface definition and the `Main` method.</span></span>
2. <span data-ttu-id="b125d-191">Примените атрибут [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) к интерфейсу `IEchoContract`.</span><span class="sxs-lookup"><span data-stu-id="b125d-191">Apply the [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute to the `IEchoContract` interface.</span></span> <span data-ttu-id="b125d-192">Атрибут определяет имя службы и пространство имен.</span><span class="sxs-lookup"><span data-stu-id="b125d-192">The attribute specifies the service name and namespace.</span></span> <span data-ttu-id="b125d-193">После этого класс `EchoService` будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="b125d-193">After doing so, the `EchoService` class appears as follows:</span></span>

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. <span data-ttu-id="b125d-194">Реализуйте метод `Echo`, определенный в интерфейсе `IEchoContract`, в классе `EchoService`.</span><span class="sxs-lookup"><span data-stu-id="b125d-194">Implement the `Echo` method defined in the `IEchoContract` interface in the `EchoService` class.</span></span>

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. <span data-ttu-id="b125d-195">В меню **Сборка** выберите команду **Собрать решение**, чтобы проверить правильность выполнения действий.</span><span class="sxs-lookup"><span data-stu-id="b125d-195">Click **Build**, then click **Build Solution** to confirm the accuracy of your work.</span></span>

### <a name="define-the-configuration-for-the-service-host"></a><span data-ttu-id="b125d-196">Определение конфигурации узла службы</span><span class="sxs-lookup"><span data-stu-id="b125d-196">Define the configuration for the service host</span></span>

1. <span data-ttu-id="b125d-197">Файл конфигурации аналогичен файлу конфигурации WCF.</span><span class="sxs-lookup"><span data-stu-id="b125d-197">The configuration file is very similar to a WCF configuration file.</span></span> <span data-ttu-id="b125d-198">Он содержит имя службы, конечную точку (то есть расположение, которое ретранслятор Azure предоставляет клиентам и узлам для взаимодействия) и привязку (тип протокола, используемый для связи).</span><span class="sxs-lookup"><span data-stu-id="b125d-198">It includes the service name, endpoint (that is, the location that Azure Relay exposes for clients and hosts to communicate with each other), and the binding (the type of protocol that is used to communicate).</span></span> <span data-ttu-id="b125d-199">Основное отличие заключается в том, что настроенная конечная точка службы ссылается на привязку [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding), которая не является частью платформы .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="b125d-199">The main difference is that this configured service endpoint refers to a [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, which is not part of the .NET Framework.</span></span> <span data-ttu-id="b125d-200">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) — это одна из привязок, определяемых службой.</span><span class="sxs-lookup"><span data-stu-id="b125d-200">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is one of the bindings defined by the service.</span></span>
2. <span data-ttu-id="b125d-201">В **обозревателе решений** дважды щелкните файл App.config, чтобы открыть его в редакторе Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b125d-201">In **Solution Explorer**, double-click the App.config file to open it in the Visual Studio editor.</span></span>
3. <span data-ttu-id="b125d-202">В элементе `<appSettings>` замените местозаполнители именем пространства имен службы и ключом SAS, скопированным на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="b125d-202">In the `<appSettings>` element, replace the placeholders with the name of your service namespace, and the SAS key that you copied in an earlier step.</span></span>
4. <span data-ttu-id="b125d-203">Добавьте элемент `<services>` внутри тегов `<system.serviceModel>`.</span><span class="sxs-lookup"><span data-stu-id="b125d-203">Within the `<system.serviceModel>` tags, add a `<services>` element.</span></span> <span data-ttu-id="b125d-204">В отдельном файле конфигурации можно определить несколько приложений ретранслятора.</span><span class="sxs-lookup"><span data-stu-id="b125d-204">You can define multiple relay applications in a single configuration file.</span></span> <span data-ttu-id="b125d-205">Однако в данном учебнике определяется только одно приложение.</span><span class="sxs-lookup"><span data-stu-id="b125d-205">However, this tutorial defines only one.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. <span data-ttu-id="b125d-206">Добавьте элемент `<service>` в элемент `<services>` для определения имени службы.</span><span class="sxs-lookup"><span data-stu-id="b125d-206">Within the `<services>` element, add a `<service>` element to define the name of the service.</span></span>

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. <span data-ttu-id="b125d-207">Внутри элемента `<service>` определите расположение контракта конечной точки, а также тип привязки для нее.</span><span class="sxs-lookup"><span data-stu-id="b125d-207">Within the `<service>` element, define the location of the endpoint contract, and also the type of binding for the endpoint.</span></span>

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="b125d-208">Конечная точка определяет расположение, в котором клиент будет искать хост-приложение.</span><span class="sxs-lookup"><span data-stu-id="b125d-208">The endpoint defines where the client will look for the host application.</span></span> <span data-ttu-id="b125d-209">Результаты этого шага потребуются позднее для создания универсального кода ресурса (URI), который предоставляет полный доступ к узлу через ретранслятор Azure.</span><span class="sxs-lookup"><span data-stu-id="b125d-209">Later, the tutorial uses this step to create a URI that fully exposes the host through Azure Relay.</span></span> <span data-ttu-id="b125d-210">Привязка объявляет, что для обмена данными со службой ретрансляции используется протокол TCP.</span><span class="sxs-lookup"><span data-stu-id="b125d-210">The binding declares that we are using TCP as the protocol to communicate with the relay service.</span></span>
7. <span data-ttu-id="b125d-211">В меню **Сборка** выберите команду **Собрать решение**, чтобы проверить правильность выполнения действий.</span><span class="sxs-lookup"><span data-stu-id="b125d-211">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work.</span></span>

### <a name="example"></a><span data-ttu-id="b125d-212">Пример</span><span class="sxs-lookup"><span data-stu-id="b125d-212">Example</span></span>

<span data-ttu-id="b125d-213">Следующий код показывает реализацию контракта службы.</span><span class="sxs-lookup"><span data-stu-id="b125d-213">The following code shows the implementation of the service contract.</span></span>

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

<span data-ttu-id="b125d-214">Следующий код показывает базовый формат файла App.config, связанного с хостом службы.</span><span class="sxs-lookup"><span data-stu-id="b125d-214">The following code shows the basic format of the App.config file associated with the service host.</span></span>

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

## <a name="host-and-run-a-basic-web-service-to-register-with-the-relay-service"></a><span data-ttu-id="b125d-215">Размещение и запуск базовой веб-службы для регистрации в службе ретрансляции</span><span class="sxs-lookup"><span data-stu-id="b125d-215">Host and run a basic web service to register with the relay service</span></span>

<span data-ttu-id="b125d-216">В этом разделе описывается запуск службы ретрансляции Azure.</span><span class="sxs-lookup"><span data-stu-id="b125d-216">This step describes how to run an Azure Relay service.</span></span>

### <a name="create-the-relay-credentials"></a><span data-ttu-id="b125d-217">Создание учетных данных ретранслятора</span><span class="sxs-lookup"><span data-stu-id="b125d-217">Create the relay credentials</span></span>

1. <span data-ttu-id="b125d-218">Создайте в `Main()` две переменные для хранения пространства имен и ключа SAS, которые считываются из окна консоли.</span><span class="sxs-lookup"><span data-stu-id="b125d-218">In `Main()`, create two variables in which to store the namespace and the SAS key that are read from the console window.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    <span data-ttu-id="b125d-219">Ключ SAS потребуется позже для доступа к проекту.</span><span class="sxs-lookup"><span data-stu-id="b125d-219">The SAS key will be used later to access your project.</span></span> <span data-ttu-id="b125d-220">Пространство имен передается в качестве параметра в `CreateServiceUri` для создания универсального кода ресурса (URI) службы.</span><span class="sxs-lookup"><span data-stu-id="b125d-220">The namespace is passed as a parameter to `CreateServiceUri` to create a service URI.</span></span>
2. <span data-ttu-id="b125d-221">Используя объект [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior), объявите, что в качестве учетных данных будет использоваться ключ SAS.</span><span class="sxs-lookup"><span data-stu-id="b125d-221">Using a [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, declare that you will be using a SAS key as the credential type.</span></span> <span data-ttu-id="b125d-222">Добавьте следующий код сразу после кода, добавленного на предыдущем шаге:</span><span class="sxs-lookup"><span data-stu-id="b125d-222">Add the following code directly after the code added in the last step.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-the-service"></a><span data-ttu-id="b125d-223">Создание базового адреса для службы</span><span class="sxs-lookup"><span data-stu-id="b125d-223">Create a base address for the service</span></span>

<span data-ttu-id="b125d-224">Создайте экземпляр `Uri` для базового адреса службы после кода, добавленного на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="b125d-224">After the code you added in the last step, create a `Uri` instance for the base address of the service.</span></span> <span data-ttu-id="b125d-225">Этот универсальный код ресурса (URI) указывает схему, пространство имен и путь к интерфейсу службы служебной шины.</span><span class="sxs-lookup"><span data-stu-id="b125d-225">This URI specifies the Service Bus scheme, the namespace, and the path of the service interface.</span></span>

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

<span data-ttu-id="b125d-226">SB — это сокращение, используемое для схемы служебной шины; оно указывает, что используется протокол TCP.</span><span class="sxs-lookup"><span data-stu-id="b125d-226">"sb" is an abbreviation for the Service Bus scheme, and indicates that we are using TCP as the protocol.</span></span> <span data-ttu-id="b125d-227">Этот протокол также задан в файле конфигурации с помощью привязки [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx).</span><span class="sxs-lookup"><span data-stu-id="b125d-227">This was also previously indicated in the configuration file, when [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) was specified as the binding.</span></span>

<span data-ttu-id="b125d-228">В этом учебнике используется универсальный код ресурса (URI) `sb://putServiceNamespaceHere.windows.net/EchoService`.</span><span class="sxs-lookup"><span data-stu-id="b125d-228">For this tutorial, the URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.</span></span>

### <a name="create-and-configure-the-service-host"></a><span data-ttu-id="b125d-229">Создание и настройка узла службы</span><span class="sxs-lookup"><span data-stu-id="b125d-229">Create and configure the service host</span></span>

1. <span data-ttu-id="b125d-230">Установите режим подключения `AutoDetect`.</span><span class="sxs-lookup"><span data-stu-id="b125d-230">Set the connectivity mode to `AutoDetect`.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    <span data-ttu-id="b125d-231">Режим подключения описывает протокол, используемый службой для связи со службой ретрансляции (HTTP или TCP).</span><span class="sxs-lookup"><span data-stu-id="b125d-231">The connectivity mode describes the protocol the service uses to communicate with the relay service; either HTTP or TCP.</span></span> <span data-ttu-id="b125d-232">Если используется значение по умолчанию (`AutoDetect`), то служба пытается подключиться к ретранслятору Azure по протоколу TCP, если он доступен, и по протоколу HTTP, если TCP недоступен.</span><span class="sxs-lookup"><span data-stu-id="b125d-232">Using the default setting `AutoDetect`, the service attempts to connect to Azure Relay over TCP if it is available, and HTTP if TCP is not available.</span></span> <span data-ttu-id="b125d-233">Обратите внимание, что этот параметр не влияет на протокол, который задается в службе для обмена данными с клиентами.</span><span class="sxs-lookup"><span data-stu-id="b125d-233">Note that this differs from the protocol the service specifies for client communication.</span></span> <span data-ttu-id="b125d-234">Этот протокол определяется используемой привязкой.</span><span class="sxs-lookup"><span data-stu-id="b125d-234">That protocol is determined by the binding used.</span></span> <span data-ttu-id="b125d-235">Например, служба может использовать привязку [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx), которая указывает, что ее конечная точка связывается с клиентами по протоколу HTTP.</span><span class="sxs-lookup"><span data-stu-id="b125d-235">For example, a service can use the [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, which specifies that its endpoint communicates with clients over HTTP.</span></span> <span data-ttu-id="b125d-236">Для той же службы можно задать привязку **ConnectivityMode.AutoDetect**, чтобы обмен данными с ретранслятором Azure осуществлялся по протоколу TCP.</span><span class="sxs-lookup"><span data-stu-id="b125d-236">That same service could specify **ConnectivityMode.AutoDetect** so that the service communicates with Azure Relay over TCP.</span></span>
2. <span data-ttu-id="b125d-237">Создайте хост службы с помощью универсального кода ресурса (URI), созданного на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="b125d-237">Create the service host, using the URI created earlier in this section.</span></span>

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    <span data-ttu-id="b125d-238">Хост службы представляет собой объект WCF, который создает экземпляры службы.</span><span class="sxs-lookup"><span data-stu-id="b125d-238">The service host is the WCF object that instantiates the service.</span></span> <span data-ttu-id="b125d-239">На этом шаге нужно передать тип службы, который требуется создать (тип `EchoService`), и адрес, по которому служба должна быть доступна.</span><span class="sxs-lookup"><span data-stu-id="b125d-239">Here, you pass it the type of service you want to create (an `EchoService` type), and also to the address at which you want to expose the service.</span></span>
3. <span data-ttu-id="b125d-240">В начале файла Program.cs добавьте ссылки на [System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) и [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span><span class="sxs-lookup"><span data-stu-id="b125d-240">At the top of the Program.cs file, add references to [System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) and [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span></span>

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. <span data-ttu-id="b125d-241">Включите в `Main()` общий доступ к конечной точке.</span><span class="sxs-lookup"><span data-stu-id="b125d-241">Back in `Main()`, configure the endpoint to enable public access.</span></span>

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    <span data-ttu-id="b125d-242">Этот шаг информирует службу ретрансляции о том, что ваше приложение общедоступно и может быть обнаружено в результате изучения веб-канала ATOM для вашего проекта.</span><span class="sxs-lookup"><span data-stu-id="b125d-242">This step informs the relay service that your application can be found publicly by examining the ATOM feed for your project.</span></span> <span data-ttu-id="b125d-243">Если для **DiscoveryType** задано значение **private**, клиент все равно может получить доступ к службе.</span><span class="sxs-lookup"><span data-stu-id="b125d-243">If you set **DiscoveryType** to **private**, a client would still be able to access the service.</span></span> <span data-ttu-id="b125d-244">Однако она не будет отображаться в результатах поиска в пространстве имен ретранслятора.</span><span class="sxs-lookup"><span data-stu-id="b125d-244">However, the service would not appear when it searches the Relay namespace.</span></span> <span data-ttu-id="b125d-245">Клиенту потребуется знать путь к конечной точке.</span><span class="sxs-lookup"><span data-stu-id="b125d-245">Instead, the client would have to know the endpoint path beforehand.</span></span>
5. <span data-ttu-id="b125d-246">Примените учетные данные службы к конечным точкам службы, определенным в файле App.config.</span><span class="sxs-lookup"><span data-stu-id="b125d-246">Apply the service credentials to the service endpoints defined in the App.config file:</span></span>

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    <span data-ttu-id="b125d-247">Как говорилось на предыдущем шаге, в файле конфигурации можно определить несколько служб и конечных точек.</span><span class="sxs-lookup"><span data-stu-id="b125d-247">As stated in the previous step, you could have declared multiple services and endpoints in the configuration file.</span></span> <span data-ttu-id="b125d-248">Если вы это сделали, код пройдет по всему файлу конфигурации и найдет все конечные точки, к которым следует применить учетные данные.</span><span class="sxs-lookup"><span data-stu-id="b125d-248">If you had, this code would traverse the configuration file and search for every endpoint to which it should apply your credentials.</span></span> <span data-ttu-id="b125d-249">В этом учебнике в файле конфигурации задана только одна конечная точка.</span><span class="sxs-lookup"><span data-stu-id="b125d-249">However, for this tutorial, the configuration file has only one endpoint.</span></span>

### <a name="open-the-service-host"></a><span data-ttu-id="b125d-250">Открытие узла службы</span><span class="sxs-lookup"><span data-stu-id="b125d-250">Open the service host</span></span>

1. <span data-ttu-id="b125d-251">Откройте службу.</span><span class="sxs-lookup"><span data-stu-id="b125d-251">Open the service.</span></span>

    ```csharp
    host.Open();
    ```
2. <span data-ttu-id="b125d-252">Сообщите пользователю о том, что служба работает, и объясните, как ее отключить.</span><span class="sxs-lookup"><span data-stu-id="b125d-252">Inform the user that the service is running, and explain how to shut down the service.</span></span>

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] to exit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="b125d-253">После завершения закройте узел службы.</span><span class="sxs-lookup"><span data-stu-id="b125d-253">When finished, close the service host.</span></span>

    ```csharp
    host.Close();
    ```
4. <span data-ttu-id="b125d-254">Скомпилируйте проект, нажав клавиши **CTRL+SHIFT+B**.</span><span class="sxs-lookup"><span data-stu-id="b125d-254">Press **Ctrl+Shift+B** to build the project.</span></span>

### <a name="example"></a><span data-ttu-id="b125d-255">Пример</span><span class="sxs-lookup"><span data-stu-id="b125d-255">Example</span></span>

<span data-ttu-id="b125d-256">Готовый код службы должен выглядеть так, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="b125d-256">Your completed service code should appear as follows.</span></span> <span data-ttu-id="b125d-257">Он включает в себя контракт и реализацию службы, созданные в предыдущих шагах учебника. Служба размещается в консольном приложении.</span><span class="sxs-lookup"><span data-stu-id="b125d-257">The code includes the service contract and implementation from previous steps in the tutorial, and hosts the service in a console application.</span></span>

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

           // Create the credentials object for the endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create the service URI based on the service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create the service host reading the configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create the ServiceRegistrySettings behavior for the endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add the Relay credentials to all endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open the service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] to exit");
            Console.ReadLine();

            // Close the service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-the-service-contract"></a><span data-ttu-id="b125d-258">Создание клиента WCF для контракта службы</span><span class="sxs-lookup"><span data-stu-id="b125d-258">Create a WCF client for the service contract</span></span>

<span data-ttu-id="b125d-259">На этом шаге вы создадите клиентское приложение и определите контракт службы, который будет реализован на следующих шагах.</span><span class="sxs-lookup"><span data-stu-id="b125d-259">The next step is to create a client application and define the service contract you will implement in later steps.</span></span> <span data-ttu-id="b125d-260">Обратите внимание, что многие шаги повторяют действия по созданию службы: определение контракта, изменение файла App.config, использование учетных данных для подключения к службе ретрансляции и т. д.</span><span class="sxs-lookup"><span data-stu-id="b125d-260">Note that many of these steps resemble the steps used to create a service: defining a contract, editing an App.config file, using credentials to connect to the relay service, and so on.</span></span> <span data-ttu-id="b125d-261">Код для выполнения этих задач приведен в примере после описания последовательности выполнения действий.</span><span class="sxs-lookup"><span data-stu-id="b125d-261">The code used for these tasks is provided in the example following the procedure.</span></span>

1. <span data-ttu-id="b125d-262">Создайте в текущем решении Visual Studio новый проект для клиента. Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b125d-262">Create a new project in the current Visual Studio solution for the client by doing the following:</span></span>

   1. <span data-ttu-id="b125d-263">В обозревателе решений щелкните правой кнопкой мыши решение (не проект), которое содержит службу, и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b125d-263">In Solution Explorer, in the same solution that contains the service, right-click the current solution (not the project), and click **Add**.</span></span> <span data-ttu-id="b125d-264">Выберите **Создать проект**.</span><span class="sxs-lookup"><span data-stu-id="b125d-264">Then click **New Project**.</span></span>
   2. <span data-ttu-id="b125d-265">В диалоговом окне **Добавление нового проекта** выберите **Visual C#** (если элемент **Visual C#** не отображается, откройте список **Другие языки**). Выберите шаблон **Консольное приложение (.NET Framework)** и назовите его **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="b125d-265">In the **Add New Project** dialog box, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**), select the **Console App (.NET Framework)** template, and name it **EchoClient**.</span></span>
   3. <span data-ttu-id="b125d-266">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b125d-266">Click **OK**.</span></span>
      <br />
2. <span data-ttu-id="b125d-267">В обозревателе решений дважды щелкните файл Program.cs в проекте **EchoClient**, чтобы открыть его в редакторе, если он еще не открыт.</span><span class="sxs-lookup"><span data-stu-id="b125d-267">In Solution Explorer, double-click the Program.cs file in the **EchoClient** project to open it in the editor, if it is not already open.</span></span>
3. <span data-ttu-id="b125d-268">Измените имя пространства имен с `EchoClient` (имя по умолчанию) на `Microsoft.ServiceBus.Samples`.</span><span class="sxs-lookup"><span data-stu-id="b125d-268">Change the namespace name from its default name of `EchoClient` to `Microsoft.ServiceBus.Samples`.</span></span>
4. <span data-ttu-id="b125d-269">Установите [пакет NuGet для служебной шины](https://www.nuget.org/packages/WindowsAzure.ServiceBus). В обозревателе решений щелкните правой кнопкой мыши проект **EchoClient** и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b125d-269">Install the [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Solution Explorer, right-click the **EchoClient** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="b125d-270">Щелкните вкладку **Обзор** и выполните поиск `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="b125d-270">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="b125d-271">Щелкните **Установить**и примите условия использования.</span><span class="sxs-lookup"><span data-stu-id="b125d-271">Click **Install**, and accept the terms of use.</span></span>

    ![][3]
5. <span data-ttu-id="b125d-272">Добавьте в файл Program.cs инструкцию `using` для пространства имен [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx).</span><span class="sxs-lookup"><span data-stu-id="b125d-272">Add a `using` statement for the [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace in the Program.cs file.</span></span>

    ```csharp
    using System.ServiceModel;
    ```
6. <span data-ttu-id="b125d-273">Добавьте определение контракта службы в пространство имен, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="b125d-273">Add the service contract definition to the namespace, as shown in the following example.</span></span> <span data-ttu-id="b125d-274">Обратите внимание, что это определение идентично определению в проекте **Service**.</span><span class="sxs-lookup"><span data-stu-id="b125d-274">Note that this definition is identical to the definition used in the **Service** project.</span></span> <span data-ttu-id="b125d-275">Этот код следует добавить в верхнюю часть пространства имен `Microsoft.ServiceBus.Samples`.</span><span class="sxs-lookup"><span data-stu-id="b125d-275">You should add this code at the top of the `Microsoft.ServiceBus.Samples` namespace.</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. <span data-ttu-id="b125d-276">Чтобы построить клиент, нажмите клавиши **CTRL+SHIFT+B**.</span><span class="sxs-lookup"><span data-stu-id="b125d-276">Press **Ctrl+Shift+B** to build the client.</span></span>

### <a name="example"></a><span data-ttu-id="b125d-277">Пример</span><span class="sxs-lookup"><span data-stu-id="b125d-277">Example</span></span>

<span data-ttu-id="b125d-278">В следующем коде показано текущее состояние файла Program.cs в проекте **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="b125d-278">The following code shows the current status of the Program.cs file in the **EchoClient** project.</span></span>

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

## <a name="configure-the-wcf-client"></a><span data-ttu-id="b125d-279">Настройка клиента WCF</span><span class="sxs-lookup"><span data-stu-id="b125d-279">Configure the WCF client</span></span>

<span data-ttu-id="b125d-280">На этом шаге вы создадите файл конфигурации App.config для базового клиентского приложения, которое обращается к службе, созданной ранее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="b125d-280">In this step, you create an App.config file for a basic client application that accesses the service created previously in this tutorial.</span></span> <span data-ttu-id="b125d-281">Файл App.config определяет контракт, привязку и имя конечной точки.</span><span class="sxs-lookup"><span data-stu-id="b125d-281">This App.config file defines the contract, binding, and name of the endpoint.</span></span> <span data-ttu-id="b125d-282">Код для выполнения этих задач приведен в примере после описания последовательности выполнения действий.</span><span class="sxs-lookup"><span data-stu-id="b125d-282">The code used for these tasks is provided in the example following the procedure.</span></span>

1. <span data-ttu-id="b125d-283">В обозревателе решений в проекте **EchoClient** дважды щелкните **App.config**, чтобы открыть файл в редакторе Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b125d-283">In Solution Explorer, in the **EchoClient** project, double-click **App.config** to open the file in the Visual Studio editor.</span></span>
2. <span data-ttu-id="b125d-284">В элементе `<appSettings>` замените местозаполнители именем пространства имен службы и ключом SAS, скопированным на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="b125d-284">In the `<appSettings>` element, replace the placeholders with the name of your service namespace, and the SAS key that you copied in an earlier step.</span></span>
3. <span data-ttu-id="b125d-285">Добавьте элемент `<client>` в элемент system.serviceModel.</span><span class="sxs-lookup"><span data-stu-id="b125d-285">Within the system.serviceModel element, add a `<client>` element.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    <span data-ttu-id="b125d-286">На этом шаге вы объявляете, что определяете клиентское приложение WCF.</span><span class="sxs-lookup"><span data-stu-id="b125d-286">This step declares that you are defining a WCF-style client application.</span></span>
4. <span data-ttu-id="b125d-287">Определите имя, контракт и тип привязки для конечной точки в элементе `client`.</span><span class="sxs-lookup"><span data-stu-id="b125d-287">Within the `client` element, define the name, contract, and binding type for the endpoint.</span></span>

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="b125d-288">Это действие определяет имя конечной точки, контракт, определенный в службе, а также использование клиентским приложением протокола TCP для взаимодействия с ретранслятором Azure.</span><span class="sxs-lookup"><span data-stu-id="b125d-288">This step defines the name of the endpoint, the contract defined in the service, and the fact that the client application uses TCP to communicate with Azure Relay.</span></span> <span data-ttu-id="b125d-289">На следующем шаге имя конечной точки используется для связывания ее конфигурации с универсальным кодом ресурса (URI) службы.</span><span class="sxs-lookup"><span data-stu-id="b125d-289">The endpoint name is used in the next step to link this endpoint configuration with the service URI.</span></span>
5. <span data-ttu-id="b125d-290">В меню **Файл** выберите **Сохранить все**.</span><span class="sxs-lookup"><span data-stu-id="b125d-290">Click **File**, then click **Save All**.</span></span>

## <a name="example"></a><span data-ttu-id="b125d-291">Пример</span><span class="sxs-lookup"><span data-stu-id="b125d-291">Example</span></span>

<span data-ttu-id="b125d-292">В следующем коде показан файл App.config для клиента Echo.</span><span class="sxs-lookup"><span data-stu-id="b125d-292">The following code shows the App.config file for the Echo client.</span></span>

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

## <a name="implement-the-wcf-client"></a><span data-ttu-id="b125d-293">Реализация клиента WCF</span><span class="sxs-lookup"><span data-stu-id="b125d-293">Implement the WCF client</span></span>
<span data-ttu-id="b125d-294">На этом шаге вы реализуете базовое клиентское приложение, которое обращается к службе, которую вы создали ранее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="b125d-294">In this step, you implement a basic client application that accesses the service you created previously in this tutorial.</span></span> <span data-ttu-id="b125d-295">Для доступа к ретранслятору Azure клиент выполняет многие операции, аналогичные операциям, выполняемым службой:</span><span class="sxs-lookup"><span data-stu-id="b125d-295">Similar to the service, the client performs many of the same operations to access Azure Relay:</span></span>

1. <span data-ttu-id="b125d-296">Задает режим подключения.</span><span class="sxs-lookup"><span data-stu-id="b125d-296">Sets the connectivity mode.</span></span>
2. <span data-ttu-id="b125d-297">Создает универсальный код ресурса (URI) расположения хоста службы.</span><span class="sxs-lookup"><span data-stu-id="b125d-297">Creates the URI that locates the host service.</span></span>
3. <span data-ttu-id="b125d-298">Определяет учетные данные для безопасного доступа.</span><span class="sxs-lookup"><span data-stu-id="b125d-298">Defines the security credentials.</span></span>
4. <span data-ttu-id="b125d-299">Применяет учетные данные к подключению.</span><span class="sxs-lookup"><span data-stu-id="b125d-299">Applies the credentials to the connection.</span></span>
5. <span data-ttu-id="b125d-300">Открывает подключение.</span><span class="sxs-lookup"><span data-stu-id="b125d-300">Opens the connection.</span></span>
6. <span data-ttu-id="b125d-301">Выполняет специфические задачи приложения.</span><span class="sxs-lookup"><span data-stu-id="b125d-301">Performs the application-specific tasks.</span></span>
7. <span data-ttu-id="b125d-302">Закрывает подключение.</span><span class="sxs-lookup"><span data-stu-id="b125d-302">Closes the connection.</span></span>

<span data-ttu-id="b125d-303">Однако одно из основных различий заключается в том, что клиентское приложение использует для подключения к службе ретрансляции канал, а служба — вызов **ServiceHost**.</span><span class="sxs-lookup"><span data-stu-id="b125d-303">However, one of the main differences is that the client application uses a channel to connect to the relay service, whereas the service uses a call to **ServiceHost**.</span></span> <span data-ttu-id="b125d-304">Код для выполнения этих задач приведен в примере после описания последовательности выполнения действий.</span><span class="sxs-lookup"><span data-stu-id="b125d-304">The code used for these tasks is provided in the example following the procedure.</span></span>

### <a name="implement-a-client-application"></a><span data-ttu-id="b125d-305">Реализация клиентского приложения</span><span class="sxs-lookup"><span data-stu-id="b125d-305">Implement a client application</span></span>
1. <span data-ttu-id="b125d-306">Установите режим подключения **AutoDetect**.</span><span class="sxs-lookup"><span data-stu-id="b125d-306">Set the connectivity mode to **AutoDetect**.</span></span> <span data-ttu-id="b125d-307">Добавьте следующий код в метод `Main()` приложения **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="b125d-307">Add the following code inside the `Main()` method of the **EchoClient** application.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. <span data-ttu-id="b125d-308">Определите переменные для хранения значений пространства имен службы и ключа SAS, которые считываются из консоли.</span><span class="sxs-lookup"><span data-stu-id="b125d-308">Define variables to hold the values for the service namespace, and SAS key that are read from the console.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. <span data-ttu-id="b125d-309">Создайте универсальный код ресурса (URI), определяющий расположение узла в проекте ретранслятора.</span><span class="sxs-lookup"><span data-stu-id="b125d-309">Create the URI that defines the location of the host in your Relay project.</span></span>

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. <span data-ttu-id="b125d-310">Создайте объект учетных данных для конечной точки пространства имен службы.</span><span class="sxs-lookup"><span data-stu-id="b125d-310">Create the credential object for your service namespace endpoint.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. <span data-ttu-id="b125d-311">Создайте фабрику каналов, загружающую конфигурацию, описанную в файле App.config.</span><span class="sxs-lookup"><span data-stu-id="b125d-311">Create the channel factory that loads the configuration described in the App.config file.</span></span>

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    <span data-ttu-id="b125d-312">Фабрика каналов — это объект WCF, который создает канал взаимодействия между службой и клиентскими приложениями.</span><span class="sxs-lookup"><span data-stu-id="b125d-312">A channel factory is a WCF object that creates a channel through which the service and client applications communicate.</span></span>
6. <span data-ttu-id="b125d-313">Примените учетные данные.</span><span class="sxs-lookup"><span data-stu-id="b125d-313">Apply the credentials.</span></span>

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. <span data-ttu-id="b125d-314">Создайте и откройте канал к службе.</span><span class="sxs-lookup"><span data-stu-id="b125d-314">Create and open the channel to the service.</span></span>

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. <span data-ttu-id="b125d-315">Напишите простой пользовательский интерфейс и функциональность для Echo.</span><span class="sxs-lookup"><span data-stu-id="b125d-315">Write the basic user interface and functionality for the echo.</span></span>

    ```csharp
    Console.WriteLine("Enter text to echo (or [Enter] to exit):");
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

    <span data-ttu-id="b125d-316">Обратите внимание, что в качестве прокси для службы в этом коде используется экземпляр объекта канала.</span><span class="sxs-lookup"><span data-stu-id="b125d-316">Note that the code uses the instance of the channel object as a proxy for the service.</span></span>
9. <span data-ttu-id="b125d-317">Закройте канал и фабрику.</span><span class="sxs-lookup"><span data-stu-id="b125d-317">Close the channel, and close the factory.</span></span>

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a><span data-ttu-id="b125d-318">Пример</span><span class="sxs-lookup"><span data-stu-id="b125d-318">Example</span></span>

<span data-ttu-id="b125d-319">Готовый код должен выглядеть так, как показано ниже. В нем создается клиентское приложение, вызываются операции службы и клиент закрывается после завершения вызова операции.</span><span class="sxs-lookup"><span data-stu-id="b125d-319">Your completed code should appear as follows, showing how to create a client application, how to call the operations of the service, and how to close the client after the operation call is finished.</span></span>

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

            Console.WriteLine("Enter text to echo (or [Enter] to exit):");
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

## <a name="run-the-applications"></a><span data-ttu-id="b125d-320">Запуск приложений</span><span class="sxs-lookup"><span data-stu-id="b125d-320">Run the applications</span></span>

1. <span data-ttu-id="b125d-321">Чтобы построить решение, нажмите клавиши **CTRL+SHIFT+B**.</span><span class="sxs-lookup"><span data-stu-id="b125d-321">Press **Ctrl+Shift+B** to build the solution.</span></span> <span data-ttu-id="b125d-322">Будут скомпилированы клиентский проект и проект службы, созданный на предыдущих этапах.</span><span class="sxs-lookup"><span data-stu-id="b125d-322">This builds both the client project and the service project that you created in the previous steps.</span></span>
2. <span data-ttu-id="b125d-323">Прежде чем запустить клиентское приложение, убедитесь, что приложение службы работает.</span><span class="sxs-lookup"><span data-stu-id="b125d-323">Before running the client application, you must make sure that the service application is running.</span></span> <span data-ttu-id="b125d-324">В Visual Studio в обозревателе решений щелкните правой кнопкой мыши решение **EchoService** и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="b125d-324">In Solution Explorer in Visual Studio, right-click the **EchoService** solution, then click **Properties**.</span></span>
3. <span data-ttu-id="b125d-325">В диалоговом окне свойств решения выберите **Запускаемый проект** и нажмите кнопку **Несколько запускаемых проектов**.</span><span class="sxs-lookup"><span data-stu-id="b125d-325">In the solution properties dialog box, click **Startup Project**, then click the **Multiple startup projects** button.</span></span> <span data-ttu-id="b125d-326">Убедитесь, что проект **EchoService** отображается первым в списке.</span><span class="sxs-lookup"><span data-stu-id="b125d-326">Make sure **EchoService** appears first in the list.</span></span>
4. <span data-ttu-id="b125d-327">В поле **Действие** для проектов **EchoService** и **EchoClient** выберите значение **Запуск**.</span><span class="sxs-lookup"><span data-stu-id="b125d-327">Set the **Action** box for both the **EchoService** and **EchoClient** projects to **Start**.</span></span>

    ![][5]
5. <span data-ttu-id="b125d-328">Щелкните **Зависимости проектов**.</span><span class="sxs-lookup"><span data-stu-id="b125d-328">Click **Project Dependencies**.</span></span> <span data-ttu-id="b125d-329">В поле **Проекты** выберите **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="b125d-329">In the **Projects** box, select **EchoClient**.</span></span> <span data-ttu-id="b125d-330">Убедитесь, что в поле **Зависит от** указано значение **EchoService**.</span><span class="sxs-lookup"><span data-stu-id="b125d-330">In the **Depends on** box, make sure **EchoService** is checked.</span></span>

    ![][6]
6. <span data-ttu-id="b125d-331">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="b125d-331">Click **OK** to dismiss the **Properties** dialog.</span></span>
7. <span data-ttu-id="b125d-332">Нажмите клавишу **F5**, чтобы запустить оба проекта.</span><span class="sxs-lookup"><span data-stu-id="b125d-332">Press **F5** to run both projects.</span></span>
8. <span data-ttu-id="b125d-333">Откроются два окна консоли с предложением указать пространство имен.</span><span class="sxs-lookup"><span data-stu-id="b125d-333">Both console windows open and prompt you for the namespace name.</span></span> <span data-ttu-id="b125d-334">Сначала нужно запустить службу, поэтому в окне консоли **EchoService** введите пространство имен и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="b125d-334">The service must run first, so in the **EchoService** console window, enter the namespace and then press **Enter**.</span></span>
9. <span data-ttu-id="b125d-335">Далее появится запрос на ввод ключа SAS.</span><span class="sxs-lookup"><span data-stu-id="b125d-335">Next, you are prompted for your SAS key.</span></span> <span data-ttu-id="b125d-336">Введите ключ SAS и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="b125d-336">Enter the SAS key and press ENTER.</span></span>

    <span data-ttu-id="b125d-337">В окне консоли вы увидите примерно следующее.</span><span class="sxs-lookup"><span data-stu-id="b125d-337">Here is example output from the console window.</span></span> <span data-ttu-id="b125d-338">Обратите внимание, что здесь приведены лишь примеры возможных значений.</span><span class="sxs-lookup"><span data-stu-id="b125d-338">Note that the values provided here are for example purposes only.</span></span>

    <span data-ttu-id="b125d-339">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span><span class="sxs-lookup"><span data-stu-id="b125d-339">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span></span>

    <span data-ttu-id="b125d-340">Приложение службы выведет в окне консоли адрес, который оно прослушивает (см. следующий пример).</span><span class="sxs-lookup"><span data-stu-id="b125d-340">The service application prints to the console window the address on which it's listening, as seen in the following example.</span></span>

    <span data-ttu-id="b125d-341">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] to exit`</span><span class="sxs-lookup"><span data-stu-id="b125d-341">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] to exit`</span></span>
10. <span data-ttu-id="b125d-342">В окне консоли **EchoClient** введите данные, которые использовались для приложения службы.</span><span class="sxs-lookup"><span data-stu-id="b125d-342">In the **EchoClient** console window, enter the same information that you entered previously for the service application.</span></span> <span data-ttu-id="b125d-343">Выполните приведенные выше инструкции, чтобы ввести те же значения пространства имен службы и ключа SAS для клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="b125d-343">Follow the previous steps to enter the same service namespace and SAS key values for the client application.</span></span>
11. <span data-ttu-id="b125d-344">После ввода значений клиент открывает канал к службе и предлагает ввести некоторый текст, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="b125d-344">After entering these values, the client opens a channel to the service and prompts you to enter some text as seen in the following console output example.</span></span>

    `Enter text to echo (or [Enter] to exit):`

    <span data-ttu-id="b125d-345">Введите текст для отправки в приложение службы и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="b125d-345">Enter some text to send to the service application and press Enter.</span></span> <span data-ttu-id="b125d-346">Этот текст отправляется службе посредством операции службы Echo и отображается в окне консоли службы, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="b125d-346">This text is sent to the service through the Echo service operation and appears in the service console window as in the following example output.</span></span>

    `Echoing: My sample text`

    <span data-ttu-id="b125d-347">Результат операции `Echo` (исходный текст) возвращается в клиентское приложение и отображается в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="b125d-347">The client application receives the return value of the `Echo` operation, which is the original text, and prints it to its console window.</span></span> <span data-ttu-id="b125d-348">Вы увидите примерно следующее.</span><span class="sxs-lookup"><span data-stu-id="b125d-348">The following is example output from the client console window.</span></span>

    `Server echoed: My sample text`
12. <span data-ttu-id="b125d-349">Вы можете отправить еще несколько текстовых сообщений от клиента к службе.</span><span class="sxs-lookup"><span data-stu-id="b125d-349">You can continue sending text messages from the client to the service in this manner.</span></span> <span data-ttu-id="b125d-350">Закончив, нажмите клавишу ВВОД в окнах консоли клиента и службы, чтобы завершить работу приложений.</span><span class="sxs-lookup"><span data-stu-id="b125d-350">When you are finished, press Enter in the client and service console windows to end both applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b125d-351">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b125d-351">Next steps</span></span>

<span data-ttu-id="b125d-352">В этом учебнике мы рассмотрели создание клиентского приложения ретранслятора Azure и службы ретрансляции Azure с использованием возможностей ретранслятора WCF служебной шины.</span><span class="sxs-lookup"><span data-stu-id="b125d-352">This tutorial showed how to build an Azure Relay client application and service using the WCF Relay capabilities of Service Bus.</span></span> <span data-ttu-id="b125d-353">Аналогичное руководство по [обмену сообщениями в служебной шине](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging) представлено в статье [Начало работы с очередями служебной шины](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="b125d-353">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="b125d-354">Дополнительные сведения о ретрансляторе Azure см. в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="b125d-354">To learn more about Azure Relay, see the following topics.</span></span>

* [<span data-ttu-id="b125d-355">Обзор архитектуры служебной шины Azure</span><span class="sxs-lookup"><span data-stu-id="b125d-355">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [<span data-ttu-id="b125d-356">Что такое ретранслятор Azure?</span><span class="sxs-lookup"><span data-stu-id="b125d-356">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="b125d-357">Как использовать ретранслятор WCF служебной шины с .NET</span><span class="sxs-lookup"><span data-stu-id="b125d-357">How to use the WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
