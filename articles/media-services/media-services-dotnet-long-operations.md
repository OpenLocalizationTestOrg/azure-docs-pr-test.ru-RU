---
title: "Длительные операции aaaPolling | Документы Microsoft"
description: "В этом разделе показано, как toopoll длительных операций."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 9a68c4b1-6159-42fe-9439-a3661a90ae03
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: juliako
ms.openlocfilehash: f8315a5ddbe484d794c3e2164e47dd9e70521671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="delivering-live-streaming-with-azure-media-services"></a><span data-ttu-id="61d41-103">Доставка динамической потоковой передачи с помощью служб мультимедиа Azure</span><span class="sxs-lookup"><span data-stu-id="61d41-103">Delivering Live Streaming with Azure Media Services</span></span>

## <a name="overview"></a><span data-ttu-id="61d41-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="61d41-104">Overview</span></span>

<span data-ttu-id="61d41-105">Службы мультимедиа Microsoft Azure предлагает API которые отправляют запросы операций toostart tooMedia служб (например: создание, запуск, остановка или удаление канала).</span><span class="sxs-lookup"><span data-stu-id="61d41-105">Microsoft Azure Media Services offers APIs that send requests tooMedia Services toostart operations (for example: create, start, stop, or delete a channel).</span></span> <span data-ttu-id="61d41-106">Эти операции являются долговременными.</span><span class="sxs-lookup"><span data-stu-id="61d41-106">These operations are long-running.</span></span>

<span data-ttu-id="61d41-107">Hello Media Services .NET SDK предоставляет интерфейсы API, отправка запроса hello и дождитесь toocomplete hello операции (на внутреннем уровне приветствия API запрашивают прогресс операции через определенные промежутки времени).</span><span class="sxs-lookup"><span data-stu-id="61d41-107">hello Media Services .NET SDK provides APIs that send hello request and wait for hello operation toocomplete (internally, hello APIs are polling for operation progress at some intervals).</span></span> <span data-ttu-id="61d41-108">Например, при вызове канала. Start(), hello метод возвращается после запуска канала hello.</span><span class="sxs-lookup"><span data-stu-id="61d41-108">For example, when you call channel.Start(), hello method returns after hello channel is started.</span></span> <span data-ttu-id="61d41-109">Можно также использовать асинхронную версию hello: await канала. StartAsync() (сведения об асинхронной модели на основе задач см. в разделе [КОСНИТЕСЬ](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span><span class="sxs-lookup"><span data-stu-id="61d41-109">You can also use hello asynchronous version: await channel.StartAsync() (for information about Task-based Asynchronous Pattern, see [TAP](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)).</span></span> <span data-ttu-id="61d41-110">API-интерфейсы, которые отправляют запрос на операцию и затем запрашивают состояние hello до завершения операции hello, называются «методы опроса».</span><span class="sxs-lookup"><span data-stu-id="61d41-110">APIs that send an operation request and then poll for hello status until hello operation is complete are called “polling methods”.</span></span> <span data-ttu-id="61d41-111">Эти методы (особенно hello асинхронная версия) рекомендуются для полнофункциональных клиентских приложений или служб с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="61d41-111">These methods (especially hello Async version) are recommended for rich client applications and/or stateful services.</span></span>

<span data-ttu-id="61d41-112">Существуют сценарии, где приложение нельзя ждать долговременного HTTP-запроса и хочет toopoll hello прогресс операции вручную.</span><span class="sxs-lookup"><span data-stu-id="61d41-112">There are scenarios where an application cannot wait for a long running http request and wants toopoll for hello operation progress manually.</span></span> <span data-ttu-id="61d41-113">Типичным примером может быть браузер, взаимодействующий со службой без учета состояния: при hello браузер запрашивает toocreate канал, длительная операция инициирует hello веб-службы и возвращает hello браузера toohello идентификатор операции.</span><span class="sxs-lookup"><span data-stu-id="61d41-113">A typical example would be a browser interacting with a stateless web service: when hello browser requests toocreate a channel, hello web service initiates a long running operation and returns hello operation ID toohello browser.</span></span> <span data-ttu-id="61d41-114">затем Hello браузер может запросить hello состояние веб-службы tooget hello операции на основе идентификатора hello.</span><span class="sxs-lookup"><span data-stu-id="61d41-114">hello browser could then ask hello web service tooget hello operation status based on hello ID.</span></span> <span data-ttu-id="61d41-115">Hello Media Services .NET SDK предоставляет интерфейсы API, которые удобно использовать для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="61d41-115">hello Media Services .NET SDK provides APIs that are useful for this scenario.</span></span> <span data-ttu-id="61d41-116">Такие API называются неопросными методами.</span><span class="sxs-lookup"><span data-stu-id="61d41-116">These APIs are called “non-polling methods”.</span></span>
<span data-ttu-id="61d41-117">Hello «неопросные методы» имеют следующий шаблон именования hello: Отправка*Имя_операции*операции (например, SendCreateOperation).</span><span class="sxs-lookup"><span data-stu-id="61d41-117">hello “non-polling methods” have hello following naming pattern: Send*OperationName*Operation (for example, SendCreateOperation).</span></span> <span data-ttu-id="61d41-118">Отправить*Имя_операции*операции методы возвращают hello **IOperation** объекта; hello возвращаемый объект содержит сведения, которые можно используется tootrack hello операции.</span><span class="sxs-lookup"><span data-stu-id="61d41-118">Send*OperationName*Operation methods return hello **IOperation** object; hello returned object contains information that can be used tootrack hello operation.</span></span> <span data-ttu-id="61d41-119">Hello отправки*OperationName*OperationAsync методы возвращают **задачи<IOperation>**.</span><span class="sxs-lookup"><span data-stu-id="61d41-119">hello Send*OperationName*OperationAsync methods return **Task<IOperation>**.</span></span>

<span data-ttu-id="61d41-120">В настоящее время hello следующие классы поддержки неопросные методы: **канала**, **StreamingEndpoint**, и **программы**.</span><span class="sxs-lookup"><span data-stu-id="61d41-120">Currently, hello following classes support non-polling methods:  **Channel**, **StreamingEndpoint**, and **Program**.</span></span>

<span data-ttu-id="61d41-121">toopoll статус операции hello, используйте hello **GetOperation** метод hello **OperationBaseCollection** класса.</span><span class="sxs-lookup"><span data-stu-id="61d41-121">toopoll for hello operation status, use hello **GetOperation** method on hello **OperationBaseCollection** class.</span></span> <span data-ttu-id="61d41-122">Используйте следующие состояния операции hello toocheck интервалы hello: для **канала** и **конечной точки потоковой передачи** операции, используйте 30 секунд; для **программы** операции, при использовании 10 количество секунд.</span><span class="sxs-lookup"><span data-stu-id="61d41-122">Use hello following intervals toocheck hello operation status: for **Channel** and **StreamingEndpoint** operations, use 30 seconds; for **Program** operations, use 10 seconds.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="61d41-123">Создание и настройка проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="61d41-123">Create and configure a Visual Studio project</span></span>

<span data-ttu-id="61d41-124">Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="61d41-124">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span>

## <a name="example"></a><span data-ttu-id="61d41-125">Пример</span><span class="sxs-lookup"><span data-stu-id="61d41-125">Example</span></span>

<span data-ttu-id="61d41-126">Hello в примере определяется класс с именем **ChannelOperations**.</span><span class="sxs-lookup"><span data-stu-id="61d41-126">hello following example defines a class called **ChannelOperations**.</span></span> <span data-ttu-id="61d41-127">Это определение класса может быть стартовой точкой для определения класса веб-службы.</span><span class="sxs-lookup"><span data-stu-id="61d41-127">This class definition could be a starting point for your web service class definition.</span></span> <span data-ttu-id="61d41-128">Для простоты hello следующих примерах используется hello синхронные версии методов.</span><span class="sxs-lookup"><span data-stu-id="61d41-128">For simplicity, hello following examples use hello non-async versions of methods.</span></span>

<span data-ttu-id="61d41-129">Hello примере также показано, как hello клиент может использовать этот класс.</span><span class="sxs-lookup"><span data-stu-id="61d41-129">hello example also shows how hello client might use this class.</span></span>

### <a name="channeloperations-class-definition"></a><span data-ttu-id="61d41-130">Определение класса ChannelOperations</span><span class="sxs-lookup"><span data-stu-id="61d41-130">ChannelOperations class definition</span></span>

    using Microsoft.WindowsAzure.MediaServices.Client;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Net;

    /// <summary> 
    /// hello ChannelOperations class only implements 
    /// hello Channel’s creation operation. 
    /// </summary> 
    public class ChannelOperations
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];

        // Field for service context.
        private static CloudMediaContext _context = null;

        public ChannelOperations()
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
        }

        /// <summary>  
        /// Initiates hello creation of a new channel.  
        /// </summary>  
        /// <param name="channelName">Name toobe given toohello new channel</param>  
        /// <returns>  
        /// Operation Id for hello long running operation being executed by Media Services. 
        /// Use this operation Id toopoll for hello channel creation status. 
        /// </returns> 
        public string StartChannelCreation(string channelName)
        {
            var operation = _context.Channels.SendCreateOperation(
                new ChannelCreationOptions
                {
                    Name = channelName,
                    Input = CreateChannelInput(),
                    Preview = CreateChannelPreview(),
                    Output = CreateChannelOutput()
                });

            return operation.Id;
        }

        /// <summary> 
        /// Checks if hello operation has been completed. 
        /// If hello operation succeeded, hello created channel Id is returned in hello out parameter.
        /// </summary> 
        /// <param name="operationId">hello operation Id.</param> 
        /// <param name="channel">
        /// If hello operation succeeded, 
        /// hello created channel Id is returned in hello out parameter.</param>
        /// <returns>Returns false if hello operation is still in progress; otherwise, true.</returns> 
        public bool IsCompleted(string operationId, out string channelId)
        {
            IOperation operation = _context.Operations.GetOperation(operationId);
            bool completed = false;

            channelId = null;

            switch (operation.State)
            {
                case OperationState.Failed:
                    // Handle hello failure. 
                    // For example, throw an exception. 
                    // Use hello following information in hello exception: operationId, operation.ErrorMessage.
                    break;
                case OperationState.Succeeded:
                    completed = true;
                    channelId = operation.TargetEntityId;
                    break;
                case OperationState.InProgress:
                    completed = false;
                    break;
            }
            return completed;
        }

        private static ChannelInput CreateChannelInput()
        {
            return new ChannelInput
            {
                StreamingProtocol = StreamingProtocol.RTMP,
                AccessControl = new ChannelAccessControl
                {
                    IPAllowList = new List<IPRange>
                        {
                            new IPRange
                            {
                                Name = "TestChannelInput001",
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelPreview CreateChannelPreview()
        {
            return new ChannelPreview
            {
                AccessControl = new ChannelAccessControl
                {
                    IPAllowList = new List<IPRange>
                        {
                            new IPRange
                            {
                                Name = "TestChannelPreview001",
                                Address = IPAddress.Parse("0.0.0.0"),
                                SubnetPrefixLength = 0
                            }
                        }
                }
            };
        }

        private static ChannelOutput CreateChannelOutput()
        {
            return new ChannelOutput
            {
                Hls = new ChannelOutputHls { FragmentsPerSegment = 1 }
            };
        }
    }

### <a name="hello-client-code"></a><span data-ttu-id="61d41-131">клиентский код Hello</span><span class="sxs-lookup"><span data-stu-id="61d41-131">hello client code</span></span>
    ChannelOperations channelOperations = new ChannelOperations();
    string opId = channelOperations.StartChannelCreation("MyChannel001");

    string channelId = null;
    bool isCompleted = false;

    while (isCompleted == false)
    {
        System.Threading.Thread.Sleep(TimeSpan.FromSeconds(30));
        isCompleted = channelOperations.IsCompleted(opId, out channelId);
    }

    // If we got here, we should have hello newly created channel id.
    Console.WriteLine(channelId);



## <a name="media-services-learning-paths"></a><span data-ttu-id="61d41-132">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="61d41-132">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="61d41-133">Отзывы</span><span class="sxs-lookup"><span data-stu-id="61d41-133">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

