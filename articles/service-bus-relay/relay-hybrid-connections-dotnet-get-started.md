---
title: "aaaGet работы с Azure ретрансляции гибридных подключений в .NET | Документы Microsoft"
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
ms.openlocfilehash: 1e4af28e7cd4393c8ca965a149a0b83ebcc44f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="9949c-103">Приступая к работе с гибридными подключениями к ретранслятору</span><span class="sxs-lookup"><span data-stu-id="9949c-103">Get started with Relay Hybrid Connections</span></span>
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="9949c-104">Этот учебник содержит введение слишком[гибридных подключений ретрансляции Azure](relay-what-is-it.md#hybrid-connections)и показано, как .NET toouse toocreate клиентское приложение, которое отправляет сообщения tooa соответствующее приложение прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="9949c-104">This tutorial provides an introduction too[Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how toouse .NET toocreate a client application that sends messages tooa corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="9949c-105">Что будет выполнено</span><span class="sxs-lookup"><span data-stu-id="9949c-105">What will be accomplished</span></span>
<span data-ttu-id="9949c-106">Так как гибридные подключения требуется клиентом и серверным компонентом, учебник hello создает два консольных приложений.</span><span class="sxs-lookup"><span data-stu-id="9949c-106">Because Hybrid Connections requires both a client and a server component, hello tutorial creates two console applications.</span></span> <span data-ttu-id="9949c-107">Ниже приведены шаги hello.</span><span class="sxs-lookup"><span data-stu-id="9949c-107">Here are hello steps:</span></span>

1. <span data-ttu-id="9949c-108">Создание ретрансляции пространства имен, с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9949c-108">Create a Relay namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="9949c-109">Создайте гибридное подключение в этом пространстве имен, с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9949c-109">Create a hybrid connection in that namespace, using hello Azure portal.</span></span>
3. <span data-ttu-id="9949c-110">Запись сообщений tooreceive приложения консоли сервера (прослушиватель).</span><span class="sxs-lookup"><span data-stu-id="9949c-110">Write a server (listener) console application tooreceive messages.</span></span>
4. <span data-ttu-id="9949c-111">Запись сообщений toosend приложения консоли клиента (отправителя).</span><span class="sxs-lookup"><span data-stu-id="9949c-111">Write a client (sender) console application toosend messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9949c-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9949c-112">Prerequisites</span></span>

<span data-ttu-id="9949c-113">toocomplete этого учебника вам потребуется hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="9949c-113">toocomplete this tutorial, you'll need hello following prerequisites:</span></span>

1. <span data-ttu-id="9949c-114">[Visual Studio 2015 или более поздней версии.](http://www.visualstudio.com)</span><span class="sxs-lookup"><span data-stu-id="9949c-114">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="9949c-115">Hello примерах в этом учебнике используется Visual Studio 2017 г.</span><span class="sxs-lookup"><span data-stu-id="9949c-115">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="9949c-116">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="9949c-116">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="9949c-117">1. Создание пространства имен с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="9949c-117">1. Create a namespace using hello Azure portal</span></span>
<span data-ttu-id="9949c-118">Если вы уже создали имен ретрансляции, перехода toohello [создать гибридное подключение с помощью портала Azure hello](#2-create-a-hybrid-connection-using-the-azure-portal) раздела.</span><span class="sxs-lookup"><span data-stu-id="9949c-118">If you have already created a Relay namespace, jump toohello [Create a hybrid connection using hello Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a><span data-ttu-id="9949c-119">2. Создайте гибридное подключение с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="9949c-119">2. Create a hybrid connection using hello Azure portal</span></span>
<span data-ttu-id="9949c-120">Если вы уже создали гибридное подключение, перейдите к toohello [создать серверное приложение](#3-create-a-server-application-listener) раздела.</span><span class="sxs-lookup"><span data-stu-id="9949c-120">If you have already created a hybrid connection, jump toohello [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="9949c-121">3. Создание серверного приложения (прослушивателя)</span><span class="sxs-lookup"><span data-stu-id="9949c-121">3. Create a server application (listener)</span></span>
<span data-ttu-id="9949c-122">toolisten и получать сообщения из hello ретрансляции, мы напишем консольное приложение C# с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9949c-122">toolisten and receive messages from hello Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="9949c-123">4. Создание клиентского приложения (отправителя)</span><span class="sxs-lookup"><span data-stu-id="9949c-123">4. Create a client application (sender)</span></span>
<span data-ttu-id="9949c-124">Пересылать сообщения toohello toosend, мы напишем консольное приложение C# с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9949c-124">toosend messages toohello Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-hello-applications"></a><span data-ttu-id="9949c-125">5. Запускать приложения hello</span><span class="sxs-lookup"><span data-stu-id="9949c-125">5. Run hello applications</span></span>
1. <span data-ttu-id="9949c-126">Запустите серверное приложение hello.</span><span class="sxs-lookup"><span data-stu-id="9949c-126">Run hello server application.</span></span>
2. <span data-ttu-id="9949c-127">Запустите клиентское приложение hello и введите текст.</span><span class="sxs-lookup"><span data-stu-id="9949c-127">Run hello client application and enter some text.</span></span>
3. <span data-ttu-id="9949c-128">Убедитесь, что hello сервере приложения консоли выходы hello текст был введен в клиентском приложении hello.</span><span class="sxs-lookup"><span data-stu-id="9949c-128">Ensure that hello server application console outputs hello text that was entered in hello client application.</span></span>

![running-applications](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

<span data-ttu-id="9949c-130">Поздравляем, вы создали приложение для гибридных подключений.</span><span class="sxs-lookup"><span data-stu-id="9949c-130">Congratulations, you have created an end-to-end Hybrid Connections application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9949c-131">Дальнейшие действия:</span><span class="sxs-lookup"><span data-stu-id="9949c-131">Next steps:</span></span>
* [<span data-ttu-id="9949c-132">Вопросы и ответы по ретранслятору</span><span class="sxs-lookup"><span data-stu-id="9949c-132">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="9949c-133">Создание пространства имен</span><span class="sxs-lookup"><span data-stu-id="9949c-133">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="9949c-134">Приступая к работе с Node</span><span class="sxs-lookup"><span data-stu-id="9949c-134">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

