---
title: "Как создать пространство имен служебной шины с помощью портала Azure | Документация Майкрософт"
description: "Создание пространства имен служебной шины с помощью портала Azure."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fbb10e62-b133-4851-9d27-40bd844db3ba
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: c8654ed547a9001e2e968d2a45d990a73ef27d3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-service-bus-namespace-using-the-azure-portal"></a><span data-ttu-id="9aca7-103">Создание пространства имен служебной шины с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="9aca7-103">Create a Service Bus namespace using the Azure portal</span></span>

<span data-ttu-id="9aca7-104">Пространство имен — это контейнер, определяющий область действия для всех компонентов обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="9aca7-104">A namespace is a scoping container for all messaging components.</span></span> <span data-ttu-id="9aca7-105">В одном пространстве имен могут содержаться несколько очередей и разделов. Часто пространства имен выполняют роль контейнеров приложений.</span><span class="sxs-lookup"><span data-stu-id="9aca7-105">Multiple queues and topics can reside within a single namespace, and namespaces often serve as application containers.</span></span> <span data-ttu-id="9aca7-106">Сейчас создать пространство имен служебной шины можно двумя способами.</span><span class="sxs-lookup"><span data-stu-id="9aca7-106">There are two different ways to create a Service Bus namespace:</span></span>

1. <span data-ttu-id="9aca7-107">Портал Azure (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="9aca7-107">Azure portal (this article)</span></span>
2. <span data-ttu-id="9aca7-108">[Шаблоны Resource Manager][create-namespace-using-arm]</span><span class="sxs-lookup"><span data-stu-id="9aca7-108">[Resource Manager templates][create-namespace-using-arm]</span></span>

## <a name="create-a-namespace-in-the-azure-portal"></a><span data-ttu-id="9aca7-109">Создание пространства имен на портале Azure</span><span class="sxs-lookup"><span data-stu-id="9aca7-109">Create a namespace in the Azure portal</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

<span data-ttu-id="9aca7-110">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="9aca7-110">Congratulations!</span></span> <span data-ttu-id="9aca7-111">Вы создали пространство имен служебной шины, предназначенное для обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="9aca7-111">You have now created a Service Bus Messaging namespace.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9aca7-112">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9aca7-112">Next steps</span></span>

<span data-ttu-id="9aca7-113">Ознакомьтесь с [примерами GitHub][github-samples], демонстрирующими расширенные возможности обмена сообщениями служебной шины Azure.</span><span class="sxs-lookup"><span data-stu-id="9aca7-113">Check out our [GitHub samples][github-samples], which show some of the more advanced features of Azure Service Bus Messaging.</span></span>

[create-namespace-using-arm]: service-bus-resource-manager-overview.md
[github-samples]: https://github.com/Azure/azure-service-bus/tree/master/samples
