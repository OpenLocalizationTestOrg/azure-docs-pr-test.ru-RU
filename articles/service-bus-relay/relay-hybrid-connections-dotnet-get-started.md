---
title: "Приступая к работе с гибридными подключениями к ретранслятору Azure в .NET | Документация Майкрософт"
description: "Написание консольного приложения #C для гибридных подключений ретранслятора Azure."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d1386900-b942-4abf-acfc-38d2ef826253
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 1af23bfd46dd7d3781505473f7c1d86e65ea9bc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="4b1a3-103">Приступая к работе с гибридными подключениями к ретранслятору</span><span class="sxs-lookup"><span data-stu-id="4b1a3-103">Get started with Relay Hybrid Connections</span></span>
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="4b1a3-104">В этом руководстве содержатся обзорные сведения о [гибридных подключениях ретранслятора Azure](relay-what-is-it.md#hybrid-connections) и показано, как с помощью .NET создать клиентское приложение, которое отправляет сообщения соответствующему приложению прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="4b1a3-104">This tutorial provides an introduction to [Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how to use .NET to create a client application that sends messages to a corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="4b1a3-105">Что будет выполнено</span><span class="sxs-lookup"><span data-stu-id="4b1a3-105">What will be accomplished</span></span>
<span data-ttu-id="4b1a3-106">Так как для гибридных подключений требуется компонент клиента и сервера, в этом руководстве мы создадим два консольных приложения.</span><span class="sxs-lookup"><span data-stu-id="4b1a3-106">Because Hybrid Connections requires both a client and a server component, the tutorial creates two console applications.</span></span> <span data-ttu-id="4b1a3-107">Для этого выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4b1a3-107">Here are the steps:</span></span>

1. <span data-ttu-id="4b1a3-108">Создайте пространство имен ретранслятора с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="4b1a3-108">Create a Relay namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="4b1a3-109">Создайте гибридное подключение в этом пространстве имен с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="4b1a3-109">Create a hybrid connection in that namespace, using the Azure portal.</span></span>
3. <span data-ttu-id="4b1a3-110">Создайте серверное консольное приложение (прослушиватель) для получения сообщений.</span><span class="sxs-lookup"><span data-stu-id="4b1a3-110">Write a server (listener) console application to receive messages.</span></span>
4. <span data-ttu-id="4b1a3-111">Создайте клиентское консольное приложение (отправитель) для отправки сообщений.</span><span class="sxs-lookup"><span data-stu-id="4b1a3-111">Write a client (sender) console application to send messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b1a3-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4b1a3-112">Prerequisites</span></span>

<span data-ttu-id="4b1a3-113">Для работы с данным руководством вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="4b1a3-113">To complete this tutorial, you'll need the following prerequisites:</span></span>

1. <span data-ttu-id="4b1a3-114">[Visual Studio 2015 или более поздней версии.](http://www.visualstudio.com)</span><span class="sxs-lookup"><span data-stu-id="4b1a3-114">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="4b1a3-115">В описанных в этом руководстве примерах используется Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="4b1a3-115">The examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="4b1a3-116">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="4b1a3-116">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="4b1a3-117">1. Создание пространства имен с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="4b1a3-117">1. Create a namespace using the Azure portal</span></span>
<span data-ttu-id="4b1a3-118">Если пространство имен ретранслятора уже создано, перейдите к разделу [Создание гибридного подключения с помощью портала Azure](#2-create-a-hybrid-connection-using-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="4b1a3-118">If you have already created a Relay namespace, jump to the [Create a hybrid connection using the Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-the-azure-portal"></a><span data-ttu-id="4b1a3-119">2. Создание гибридного подключения с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="4b1a3-119">2. Create a hybrid connection using the Azure portal</span></span>
<span data-ttu-id="4b1a3-120">Если гибридное подключение уже создано, перейдите к разделу [Создание серверного приложения](#3-create-a-server-application-listener).</span><span class="sxs-lookup"><span data-stu-id="4b1a3-120">If you have already created a hybrid connection, jump to the [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="4b1a3-121">3. Создание серверного приложения (прослушивателя)</span><span class="sxs-lookup"><span data-stu-id="4b1a3-121">3. Create a server application (listener)</span></span>
<span data-ttu-id="4b1a3-122">Для прослушивания и получения сообщений, отправленных ретранслятором, мы создадим консольное приложение C# с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4b1a3-122">To listen and receive messages from the Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="4b1a3-123">4. Создание клиентского приложения (отправителя)</span><span class="sxs-lookup"><span data-stu-id="4b1a3-123">4. Create a client application (sender)</span></span>
<span data-ttu-id="4b1a3-124">Для отправки сообщений в ретранслятор мы создадим консольное приложение C# с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4b1a3-124">To send messages to the Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-the-applications"></a><span data-ttu-id="4b1a3-125">5. Запуск приложений</span><span class="sxs-lookup"><span data-stu-id="4b1a3-125">5. Run the applications</span></span>
1. <span data-ttu-id="4b1a3-126">Запустите серверное приложение.</span><span class="sxs-lookup"><span data-stu-id="4b1a3-126">Run the server application.</span></span>
2. <span data-ttu-id="4b1a3-127">Запустите клиентское приложение и введите любой текст.</span><span class="sxs-lookup"><span data-stu-id="4b1a3-127">Run the client application and enter some text.</span></span>
3. <span data-ttu-id="4b1a3-128">Убедитесь, что серверное консольное приложение выводит текст, введенный в клиентском приложении.</span><span class="sxs-lookup"><span data-stu-id="4b1a3-128">Ensure that the server application console outputs the text that was entered in the client application.</span></span>

![running-applications](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

<span data-ttu-id="4b1a3-130">Поздравляем, вы создали приложение для гибридных подключений.</span><span class="sxs-lookup"><span data-stu-id="4b1a3-130">Congratulations, you have created an end-to-end Hybrid Connections application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b1a3-131">Дальнейшие действия:</span><span class="sxs-lookup"><span data-stu-id="4b1a3-131">Next steps:</span></span>
* [<span data-ttu-id="4b1a3-132">Вопросы и ответы по ретранслятору</span><span class="sxs-lookup"><span data-stu-id="4b1a3-132">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="4b1a3-133">Создание пространства имен</span><span class="sxs-lookup"><span data-stu-id="4b1a3-133">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="4b1a3-134">Приступая к работе с Node</span><span class="sxs-lookup"><span data-stu-id="4b1a3-134">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

