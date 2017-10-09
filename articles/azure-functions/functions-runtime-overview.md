---
title: "aaaAzure Обзор функций среды CLR | Документы Microsoft"
description: "Общие сведения о предварительной версии среды выполнения Azure функции hello"
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
ms.openlocfilehash: 8ce3e5037731d499c330b395c89c90109d18d65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-runtime-overview"></a><span data-ttu-id="000da-103">Обзор среды выполнения Функций Azure</span><span class="sxs-lookup"><span data-stu-id="000da-103">Azure Functions Runtime Overview</span></span>

<span data-ttu-id="000da-104">Hello среды выполнения функций Azure предлагает новый способ вы tootake преимуществами hello простоту и гибкость функции hello Azure программирования модели в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="000da-104">hello Azure Functions Runtime provides a new way for you tootake advantage of hello simplicity and flexibility of hello Azure Functions programming model on-premises.</span></span> <span data-ttu-id="000da-105">Лежит hello же откройте корни источника, как функции Azure, среда выполнения функций Azure — tooprovide развернутые в локальной среде разработки почти те же возможности hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="000da-105">Built on hello same open source roots as Azure Functions, Azure Functions Runtime is deployed on-premises tooprovide a nearly identical development experience as hello cloud service.</span></span>

![Портал предварительной версии среды выполнения Функций Azure][1]

<span data-ttu-id="000da-107">Hello среды выполнения функций Azure позволяет вам функции Azure tooexperience перед фиксацией toohello облака.</span><span class="sxs-lookup"><span data-stu-id="000da-107">hello Azure Functions Runtime provides a way for you tooexperience Azure Functions before committing toohello cloud.</span></span> <span data-ttu-id="000da-108">Таким образом активы кода hello построении можно выполнен переход с облаком toohello при миграции.</span><span class="sxs-lookup"><span data-stu-id="000da-108">In this way, hello code assets you build can then be taken with you toohello cloud when you migrate.</span></span>  <span data-ttu-id="000da-109">Среда выполнения Hello также открывает новые возможности, например ночью использование запасных вычислительной мощности hello процессов пакета toorun локальных компьютеров.</span><span class="sxs-lookup"><span data-stu-id="000da-109">hello runtime also opens up new options for you, such as using hello spare compute power of your on-premises computers toorun batch processes overnight.</span></span> <span data-ttu-id="000da-110">Устройства также можно использовать в вашей организации tooconditionally отправки tooother системы данных, как в локальных и в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="000da-110">You can also use devices within your organization tooconditionally send data tooother systems, both on-premises and in hello cloud.</span></span>

<span data-ttu-id="000da-111">Hello среды выполнения функций Azure состоит из двух частей:</span><span class="sxs-lookup"><span data-stu-id="000da-111">hello Azure Functions Runtime consists of two pieces:</span></span>
* <span data-ttu-id="000da-112">роль управления средой выполнения Функций Azure;</span><span class="sxs-lookup"><span data-stu-id="000da-112">Azure Functions Runtime Management Role</span></span>
* <span data-ttu-id="000da-113">рабочая роль среды выполнения Функций Azure.</span><span class="sxs-lookup"><span data-stu-id="000da-113">Azure Functions Runtime Worker Role</span></span>

## <a name="azure-functions-management-role"></a><span data-ttu-id="000da-114">Роль управления Функциями Azure</span><span class="sxs-lookup"><span data-stu-id="000da-114">Azure Functions Management Role</span></span>

<span data-ttu-id="000da-115">Hello роль управления функции Azure предоставляет ведущее приложение для управления функциями в локальной hello.</span><span class="sxs-lookup"><span data-stu-id="000da-115">hello Azure Functions Management Role provides a host for hello management of your Functions on-premises.</span></span> <span data-ttu-id="000da-116">Эта роль выполняет следующие задачи hello.</span><span class="sxs-lookup"><span data-stu-id="000da-116">This role performs hello following tasks:</span></span>

* <span data-ttu-id="000da-117">Размещение hello портала управления Azure функции, который является hello hello того же, вы видите в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="000da-117">Hosting of hello Azure Functions Management Portal, which is hello hello same one you see in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="000da-118">Это позволяет разрабатывать функций в hello таким же способом, что и в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="000da-118">This lets you develop your functions in hello same way as you would in hello Azure portal.</span></span>
* <span data-ttu-id="000da-119">Распределяет функции между несколькими рабочими ролями функций.</span><span class="sxs-lookup"><span data-stu-id="000da-119">Distributing functions across multiple Functions workers.</span></span>
* <span data-ttu-id="000da-120">Предоставляет конечную точку публикации, чтобы публиковать функции непосредственно из Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="000da-120">Providing a publishing endpoint so that you can publish your functions direct from Microsoft Visual Studio.</span></span>

## <a name="azure-functions-worker-role"></a><span data-ttu-id="000da-121">Рабочая роль Функций Azure</span><span class="sxs-lookup"><span data-stu-id="000da-121">Azure Functions Worker Role</span></span>

<span data-ttu-id="000da-122">Hello Azure функции рабочей роли развертываются в контейнерах Windows, и это местом исполнения кода функции.</span><span class="sxs-lookup"><span data-stu-id="000da-122">hello Azure Functions Worker Roles are deployed in Windows Containers and this is where your function code executes.</span></span>  <span data-ttu-id="000da-123">Вы можете развернуть в своей организации несколько рабочих ролей. Это ключевой метод, позволяющий клиентам использовать свободную вычислительную мощность.</span><span class="sxs-lookup"><span data-stu-id="000da-123">You can deploy multiple Worker Roles throughout your organization and is a key way in which customers can make use of spare compute power.</span></span>

## <a name="minimum-requirements"></a><span data-ttu-id="000da-124">Минимальные требования</span><span class="sxs-lookup"><span data-stu-id="000da-124">Minimum Requirements</span></span>

<span data-ttu-id="000da-125">tooget работы с hello функции среды выполнения Azure, необходимо иметь компьютер с **Windows Server 2016 или Центр обновления Windows 10 создатели** с доступом tooa **SQL Server** экземпляра.</span><span class="sxs-lookup"><span data-stu-id="000da-125">tooget started with hello Azure Functions Runtime you must have a machine with **Windows Server 2016 or Windows 10 Creators Update** with access tooa **SQL Server** instance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="000da-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="000da-126">Next Steps</span></span>

<span data-ttu-id="000da-127">Установка hello [Предварительная версия среды выполнения функций Azure](https://aka.ms/azafr)</span><span class="sxs-lookup"><span data-stu-id="000da-127">Install hello [Azure Functions Runtime preview](https://aka.ms/azafr)</span></span>

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
