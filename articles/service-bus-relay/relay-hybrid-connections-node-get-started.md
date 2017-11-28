---
title: "Приступая к работе с гибридными подключениями к ретранслятору Azure в Node | Документация Майкрософт"
description: "Написание консольного приложения Node.js для гибридных подключений ретранслятора Azure."
services: service-bus-relay
documentationcenter: node
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e44e4867-3cf3-46be-8f8a-7671e2013bc4
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: node
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: c3bfc45969f250059988129f532edd12dfe3dcfe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="aac04-103">Приступая к работе с гибридными подключениями к ретранслятору</span><span class="sxs-lookup"><span data-stu-id="aac04-103">Get started with Relay Hybrid Connections</span></span>

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="aac04-104">В этом руководстве содержатся обзорные сведения о [гибридных подключениях ретранслятора Azure](relay-what-is-it.md#hybrid-connections) и показано, как с помощью Node.js создать клиентское приложение, которое отправляет сообщения соответствующему приложению прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="aac04-104">This tutorial provides an introduction to [Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how to use Node.js to create a client application that sends messages to a corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="aac04-105">Что будет выполнено</span><span class="sxs-lookup"><span data-stu-id="aac04-105">What will be accomplished</span></span>

<span data-ttu-id="aac04-106">Так как для гибридных подключений требуется компонент клиента и сервера, в этом руководстве мы создадим два консольных приложения.</span><span class="sxs-lookup"><span data-stu-id="aac04-106">Because Hybrid Connections requires both a client and a server component, we will create two console applications in this tutorial.</span></span> <span data-ttu-id="aac04-107">Для этого выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="aac04-107">Here are the steps:</span></span>

1. <span data-ttu-id="aac04-108">Создайте пространство имен ретранслятора с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="aac04-108">Create a Relay namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="aac04-109">Создайте гибридное подключение с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="aac04-109">Create a hybrid connection, using the Azure portal.</span></span>
3. <span data-ttu-id="aac04-110">Создайте серверное консольное приложение для получения сообщений.</span><span class="sxs-lookup"><span data-stu-id="aac04-110">Write a server console application to receive messages.</span></span>
4. <span data-ttu-id="aac04-111">Создайте клиентское консольное приложение для отправки сообщений.</span><span class="sxs-lookup"><span data-stu-id="aac04-111">Write a client console application to send messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aac04-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="aac04-112">Prerequisites</span></span>

1. <span data-ttu-id="aac04-113">[Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="aac04-113">[Node.js](https://nodejs.org/en/).</span></span>
2. <span data-ttu-id="aac04-114">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="aac04-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="aac04-115">1. Создание пространства имен с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="aac04-115">1. Create a namespace using the Azure portal</span></span>

<span data-ttu-id="aac04-116">Если пространство имен ретранслятора уже создано, перейдите к разделу [Создание гибридного подключения с помощью портала Azure](#2-create-a-hybrid-connection-using-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="aac04-116">If you already have a Relay namespace created, jump to the [Create a hybrid connection using the Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-the-azure-portal"></a><span data-ttu-id="aac04-117">2. Создание гибридного подключения с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="aac04-117">2. Create a hybrid connection using the Azure portal</span></span>

<span data-ttu-id="aac04-118">Если гибридное подключение уже создано, перейдите к разделу [Создание серверного приложения](#3-create-a-server-application-listener).</span><span class="sxs-lookup"><span data-stu-id="aac04-118">If you already have a hybrid connection created, jump to the [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="aac04-119">3. Создание серверного приложения (прослушивателя)</span><span class="sxs-lookup"><span data-stu-id="aac04-119">3. Create a server application (listener)</span></span>

<span data-ttu-id="aac04-120">Для прослушивания и получения сообщений, отправленных ретранслятором, мы создадим консольное приложение Node.js.</span><span class="sxs-lookup"><span data-stu-id="aac04-120">To listen and receive messages from the Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="aac04-121">4. Создание клиентского приложения (отправителя)</span><span class="sxs-lookup"><span data-stu-id="aac04-121">4. Create a client application (sender)</span></span>

<span data-ttu-id="aac04-122">Для отправки сообщений в ретранслятор мы создадим консольное приложение Node.js.</span><span class="sxs-lookup"><span data-stu-id="aac04-122">To send messages to the Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-the-applications"></a><span data-ttu-id="aac04-123">5. Запуск приложений</span><span class="sxs-lookup"><span data-stu-id="aac04-123">5. Run the applications</span></span>

1. <span data-ttu-id="aac04-124">Запустите серверное приложение. Для этого в командной строке Node.js введите `node listener.js`.</span><span class="sxs-lookup"><span data-stu-id="aac04-124">Run the server application: from a Node.js command prompt type `node listener.js`.</span></span>
2. <span data-ttu-id="aac04-125">Запустите клиентское приложение. Для этого в командной строке Node.js введите `node sender.js`, а затем любой текст.</span><span class="sxs-lookup"><span data-stu-id="aac04-125">Run the client application: from a Node.js command prompt type `node sender.js`, and enter some text.</span></span>
3. <span data-ttu-id="aac04-126">Убедитесь, что серверное консольное приложение выводит текст, введенный в клиентском приложении.</span><span class="sxs-lookup"><span data-stu-id="aac04-126">Ensure that the server application console outputs the text that was entered in the client application.</span></span>

![running-applications](./media/relay-hybrid-connections-node-get-started/running-applications.png)

<span data-ttu-id="aac04-128">Поздравляем, вы создали приложение для гибридных подключений с помощью Node.js!</span><span class="sxs-lookup"><span data-stu-id="aac04-128">Congratulations, you have created an end-to-end Hybrid Connections application using Node.js!</span></span>

## <a name="next-steps"></a><span data-ttu-id="aac04-129">Дальнейшие действия:</span><span class="sxs-lookup"><span data-stu-id="aac04-129">Next steps:</span></span>

* [<span data-ttu-id="aac04-130">Вопросы и ответы по ретранслятору</span><span class="sxs-lookup"><span data-stu-id="aac04-130">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="aac04-131">Создание пространства имен</span><span class="sxs-lookup"><span data-stu-id="aac04-131">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="aac04-132">Приступая к работе с .NET</span><span class="sxs-lookup"><span data-stu-id="aac04-132">Get started with .NET</span></span>](relay-hybrid-connections-dotnet-get-started.md)
* [<span data-ttu-id="aac04-133">Приступая к работе с Node</span><span class="sxs-lookup"><span data-stu-id="aac04-133">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

