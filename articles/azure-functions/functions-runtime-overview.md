---
title: "Обзор среды выполнения Функций Azure | Документация Майкрософт"
description: "Обзор предварительной версии среды выполнения Функций Azure."
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: cb98d5f2aaa526555820c15ba5a32fb7e78ffc5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-runtime-overview"></a><span data-ttu-id="7525d-103">Обзор среды выполнения Функций Azure</span><span class="sxs-lookup"><span data-stu-id="7525d-103">Azure Functions Runtime Overview</span></span>

<span data-ttu-id="7525d-104">Среда выполнения Функций Azure позволяет воспользоваться преимуществами простоты и гибкости модели программирования Функций Azure в локальной системе.</span><span class="sxs-lookup"><span data-stu-id="7525d-104">The Azure Functions Runtime provides a new way for you to take advantage of the simplicity and flexibility of the Azure Functions programming model on-premises.</span></span> <span data-ttu-id="7525d-105">Разработанная на базе той же технологии с открытым исходным кодом, что и Функции Azure, среда выполнения Функций Azure развертывается в локальной среде, предоставляя практически тот же интерфейс разработки, что и облачная служба.</span><span class="sxs-lookup"><span data-stu-id="7525d-105">Built on the same open source roots as Azure Functions, Azure Functions Runtime is deployed on-premises to provide a nearly identical development experience as the cloud service.</span></span>

![Портал предварительной версии среды выполнения Функций Azure][1]

<span data-ttu-id="7525d-107">Среда выполнения Функций Azure позволяет испытать Функции Azure перед фиксацией в облаке.</span><span class="sxs-lookup"><span data-stu-id="7525d-107">The Azure Functions Runtime provides a way for you to experience Azure Functions before committing to the cloud.</span></span> <span data-ttu-id="7525d-108">Таким образом при миграции созданные вами ресурсы можно перенести в облако.</span><span class="sxs-lookup"><span data-stu-id="7525d-108">In this way, the code assets you build can then be taken with you to the cloud when you migrate.</span></span>  <span data-ttu-id="7525d-109">Среда выполнения также открывает новые возможности, например использование свободной вычислительной мощности локальных компьютеров для запуска однодневных пакетных процессов.</span><span class="sxs-lookup"><span data-stu-id="7525d-109">The runtime also opens up new options for you, such as using the spare compute power of your on-premises computers to run batch processes overnight.</span></span> <span data-ttu-id="7525d-110">Вы также можете использовать устройства в организации, чтобы выполнять условную отправку данных в другие системы (как локальные, так и облачные).</span><span class="sxs-lookup"><span data-stu-id="7525d-110">You can also use devices within your organization to conditionally send data to other systems, both on-premises and in the cloud.</span></span>

<span data-ttu-id="7525d-111">Среда выполнения Функций Azure состоит из двух компонентов:</span><span class="sxs-lookup"><span data-stu-id="7525d-111">The Azure Functions Runtime consists of two pieces:</span></span>
* <span data-ttu-id="7525d-112">роль управления средой выполнения Функций Azure;</span><span class="sxs-lookup"><span data-stu-id="7525d-112">Azure Functions Runtime Management Role</span></span>
* <span data-ttu-id="7525d-113">рабочая роль среды выполнения Функций Azure.</span><span class="sxs-lookup"><span data-stu-id="7525d-113">Azure Functions Runtime Worker Role</span></span>

## <a name="azure-functions-management-role"></a><span data-ttu-id="7525d-114">Роль управления Функциями Azure</span><span class="sxs-lookup"><span data-stu-id="7525d-114">Azure Functions Management Role</span></span>

<span data-ttu-id="7525d-115">Компонент роли управления Функциями Azure предоставляет площадку для управления функциями в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="7525d-115">The Azure Functions Management Role provides a host for the management of your Functions on-premises.</span></span> <span data-ttu-id="7525d-116">Этот компонент выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="7525d-116">This role performs the following tasks:</span></span>

* <span data-ttu-id="7525d-117">Размещает портал управления Функциями Azure, который аналогичен [порталу Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7525d-117">Hosting of the Azure Functions Management Portal, which is the the same one you see in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7525d-118">Таким образом, вы можете разрабатывать функции так же, как и на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7525d-118">This lets you develop your functions in the same way as you would in the Azure portal.</span></span>
* <span data-ttu-id="7525d-119">Распределяет функции между несколькими рабочими ролями функций.</span><span class="sxs-lookup"><span data-stu-id="7525d-119">Distributing functions across multiple Functions workers.</span></span>
* <span data-ttu-id="7525d-120">Предоставляет конечную точку публикации, чтобы публиковать функции непосредственно из Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7525d-120">Providing a publishing endpoint so that you can publish your functions direct from Microsoft Visual Studio.</span></span>

## <a name="azure-functions-worker-role"></a><span data-ttu-id="7525d-121">Рабочая роль Функций Azure</span><span class="sxs-lookup"><span data-stu-id="7525d-121">Azure Functions Worker Role</span></span>

<span data-ttu-id="7525d-122">Рабочие роли Функций Azure развертываются в контейнерах Windows, в которых выполняется код функции.</span><span class="sxs-lookup"><span data-stu-id="7525d-122">The Azure Functions Worker Roles are deployed in Windows Containers and this is where your function code executes.</span></span>  <span data-ttu-id="7525d-123">Вы можете развернуть в своей организации несколько рабочих ролей. Это ключевой метод, позволяющий клиентам использовать свободную вычислительную мощность.</span><span class="sxs-lookup"><span data-stu-id="7525d-123">You can deploy multiple Worker Roles throughout your organization and is a key way in which customers can make use of spare compute power.</span></span>

## <a name="minimum-requirements"></a><span data-ttu-id="7525d-124">Минимальные требования</span><span class="sxs-lookup"><span data-stu-id="7525d-124">Minimum Requirements</span></span>

<span data-ttu-id="7525d-125">Чтобы можно было приступить к работе со средой выполнения Функций Azure, на вашем компьютере должна быть установлена версия **Windows Server 2016 или Windows 10 Creators Update** с доступом к экземпляру **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="7525d-125">To get started with the Azure Functions Runtime you must have a machine with **Windows Server 2016 or Windows 10 Creators Update** with access to a **SQL Server** instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7525d-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7525d-126">Next Steps</span></span>

<span data-ttu-id="7525d-127">Установите [предварительную версию среды выполнения Функций Azure](https://aka.ms/azafr).</span><span class="sxs-lookup"><span data-stu-id="7525d-127">Install the [Azure Functions Runtime preview](https://aka.ms/azafr)</span></span>

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
