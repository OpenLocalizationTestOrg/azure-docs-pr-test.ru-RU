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
# <a name="delivering-live-streaming-with-azure-media-services"></a>Доставка динамической потоковой передачи с помощью служб мультимедиа Azure

## <a name="overview"></a>Обзор

Службы мультимедиа Microsoft Azure предлагает API которые отправляют запросы операций toostart tooMedia служб (например: создание, запуск, остановка или удаление канала). Эти операции являются долговременными.

Hello Media Services .NET SDK предоставляет интерфейсы API, отправка запроса hello и дождитесь toocomplete hello операции (на внутреннем уровне приветствия API запрашивают прогресс операции через определенные промежутки времени). Например, при вызове канала. Start(), hello метод возвращается после запуска канала hello. Можно также использовать асинхронную версию hello: await канала. StartAsync() (сведения об асинхронной модели на основе задач см. в разделе [КОСНИТЕСЬ](https://msdn.microsoft.com/library/hh873175\(v=vs.110\).aspx)). API-интерфейсы, которые отправляют запрос на операцию и затем запрашивают состояние hello до завершения операции hello, называются «методы опроса». Эти методы (особенно hello асинхронная версия) рекомендуются для полнофункциональных клиентских приложений или служб с отслеживанием состояния.

Существуют сценарии, где приложение нельзя ждать долговременного HTTP-запроса и хочет toopoll hello прогресс операции вручную. Типичным примером может быть браузер, взаимодействующий со службой без учета состояния: при hello браузер запрашивает toocreate канал, длительная операция инициирует hello веб-службы и возвращает hello браузера toohello идентификатор операции. затем Hello браузер может запросить hello состояние веб-службы tooget hello операции на основе идентификатора hello. Hello Media Services .NET SDK предоставляет интерфейсы API, которые удобно использовать для этого сценария. Такие API называются неопросными методами.
Hello «неопросные методы» имеют следующий шаблон именования hello: Отправка*Имя_операции*операции (например, SendCreateOperation). Отправить*Имя_операции*операции методы возвращают hello **IOperation** объекта; hello возвращаемый объект содержит сведения, которые можно используется tootrack hello операции. Hello отправки*OperationName*OperationAsync методы возвращают **задачи<IOperation>**.

В настоящее время hello следующие классы поддержки неопросные методы: **канала**, **StreamingEndpoint**, и **программы**.

toopoll статус операции hello, используйте hello **GetOperation** метод hello **OperationBaseCollection** класса. Используйте следующие состояния операции hello toocheck интервалы hello: для **канала** и **конечной точки потоковой передачи** операции, используйте 30 секунд; для **программы** операции, при использовании 10 количество секунд.

## <a name="create-and-configure-a-visual-studio-project"></a>Создание и настройка проекта Visual Studio

Настройка среды разработки и заполнить hello файл app.config с данными подключения, как описано в [разработки служб мультимедиа с помощью .NET](media-services-dotnet-how-to-use.md).

## <a name="example"></a>Пример

Hello в примере определяется класс с именем **ChannelOperations**. Это определение класса может быть стартовой точкой для определения класса веб-службы. Для простоты hello следующих примерах используется hello синхронные версии методов.

Hello примере также показано, как hello клиент может использовать этот класс.

### <a name="channeloperations-class-definition"></a>Определение класса ChannelOperations

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

### <a name="hello-client-code"></a>клиентский код Hello
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



## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

