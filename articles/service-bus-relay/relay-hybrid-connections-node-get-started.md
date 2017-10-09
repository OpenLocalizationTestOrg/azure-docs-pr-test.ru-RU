---
title: "aaaGet работы с Azure ретрансляции гибридных подключений в узле | Документы Microsoft"
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
ms.openlocfilehash: 235548399570074f7fd160fec28de8d3633625c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="ff844-103">Приступая к работе с гибридными подключениями к ретранслятору</span><span class="sxs-lookup"><span data-stu-id="ff844-103">Get started with Relay Hybrid Connections</span></span>

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="ff844-104">Этот учебник содержит введение слишком[гибридных подключений ретрансляции Azure](relay-what-is-it.md#hybrid-connections)и показано, как toocreate Node.js toouse клиентское приложение, которое отправляет сообщения tooa соответствующее приложение прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="ff844-104">This tutorial provides an introduction too[Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how toouse Node.js toocreate a client application that sends messages tooa corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="ff844-105">Что будет выполнено</span><span class="sxs-lookup"><span data-stu-id="ff844-105">What will be accomplished</span></span>

<span data-ttu-id="ff844-106">Так как для гибридных подключений требуется компонент клиента и сервера, в этом руководстве мы создадим два консольных приложения.</span><span class="sxs-lookup"><span data-stu-id="ff844-106">Because Hybrid Connections requires both a client and a server component, we will create two console applications in this tutorial.</span></span> <span data-ttu-id="ff844-107">Ниже приведены шаги hello.</span><span class="sxs-lookup"><span data-stu-id="ff844-107">Here are hello steps:</span></span>

1. <span data-ttu-id="ff844-108">Создание ретрансляции пространства имен, с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ff844-108">Create a Relay namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="ff844-109">Создайте гибридное подключение, с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ff844-109">Create a hybrid connection, using hello Azure portal.</span></span>
3. <span data-ttu-id="ff844-110">Запись сообщения tooreceive приложения консоли сервера.</span><span class="sxs-lookup"><span data-stu-id="ff844-110">Write a server console application tooreceive messages.</span></span>
4. <span data-ttu-id="ff844-111">Запись сообщений toosend консольного приложения клиента.</span><span class="sxs-lookup"><span data-stu-id="ff844-111">Write a client console application toosend messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff844-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ff844-112">Prerequisites</span></span>

1. <span data-ttu-id="ff844-113">[Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="ff844-113">[Node.js](https://nodejs.org/en/).</span></span>
2. <span data-ttu-id="ff844-114">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="ff844-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="ff844-115">1. Создание пространства имен с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="ff844-115">1. Create a namespace using hello Azure portal</span></span>

<span data-ttu-id="ff844-116">При наличии ретрансляции пространство имен, созданное перехода toohello [создать гибридное подключение с помощью портала Azure hello](#2-create-a-hybrid-connection-using-the-azure-portal) раздела.</span><span class="sxs-lookup"><span data-stu-id="ff844-116">If you already have a Relay namespace created, jump toohello [Create a hybrid connection using hello Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a><span data-ttu-id="ff844-117">2. Создайте гибридное подключение с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="ff844-117">2. Create a hybrid connection using hello Azure portal</span></span>

<span data-ttu-id="ff844-118">Если уже создан гибридное подключение, перейдите к toohello [создать серверное приложение](#3-create-a-server-application-listener) раздела.</span><span class="sxs-lookup"><span data-stu-id="ff844-118">If you already have a hybrid connection created, jump toohello [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="ff844-119">3. Создание серверного приложения (прослушивателя)</span><span class="sxs-lookup"><span data-stu-id="ff844-119">3. Create a server application (listener)</span></span>

<span data-ttu-id="ff844-120">toolisten и получать сообщения от hello ретрансляции, мы напишем консольное приложение Node.js.</span><span class="sxs-lookup"><span data-stu-id="ff844-120">toolisten and receive messages from hello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="ff844-121">4. Создание клиентского приложения (отправителя)</span><span class="sxs-lookup"><span data-stu-id="ff844-121">4. Create a client application (sender)</span></span>

<span data-ttu-id="ff844-122">toosend сообщений toohello ретрансляции, мы напишем консольное приложение Node.js.</span><span class="sxs-lookup"><span data-stu-id="ff844-122">toosend messages toohello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a><span data-ttu-id="ff844-123">5. Запускать приложения hello</span><span class="sxs-lookup"><span data-stu-id="ff844-123">5. Run hello applications</span></span>

1. <span data-ttu-id="ff844-124">Запустите серверное приложение hello: в командной строке введите Node.js `node listener.js`.</span><span class="sxs-lookup"><span data-stu-id="ff844-124">Run hello server application: from a Node.js command prompt type `node listener.js`.</span></span>
2. <span data-ttu-id="ff844-125">Запуск клиентского приложения hello: в командной строке введите Node.js `node sender.js`и введите любой текст.</span><span class="sxs-lookup"><span data-stu-id="ff844-125">Run hello client application: from a Node.js command prompt type `node sender.js`, and enter some text.</span></span>
3. <span data-ttu-id="ff844-126">Убедитесь, что hello сервере приложения консоли выходы hello текст был введен в клиентском приложении hello.</span><span class="sxs-lookup"><span data-stu-id="ff844-126">Ensure that hello server application console outputs hello text that was entered in hello client application.</span></span>

![running-applications](./media/relay-hybrid-connections-node-get-started/running-applications.png)

<span data-ttu-id="ff844-128">Поздравляем, вы создали приложение для гибридных подключений с помощью Node.js!</span><span class="sxs-lookup"><span data-stu-id="ff844-128">Congratulations, you have created an end-to-end Hybrid Connections application using Node.js!</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff844-129">Дальнейшие действия:</span><span class="sxs-lookup"><span data-stu-id="ff844-129">Next steps:</span></span>

* [<span data-ttu-id="ff844-130">Вопросы и ответы по ретранслятору</span><span class="sxs-lookup"><span data-stu-id="ff844-130">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="ff844-131">Создание пространства имен</span><span class="sxs-lookup"><span data-stu-id="ff844-131">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="ff844-132">Приступая к работе с .NET</span><span class="sxs-lookup"><span data-stu-id="ff844-132">Get started with .NET</span></span>](relay-hybrid-connections-dotnet-get-started.md)
* [<span data-ttu-id="ff844-133">Приступая к работе с Node</span><span class="sxs-lookup"><span data-stu-id="ff844-133">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

