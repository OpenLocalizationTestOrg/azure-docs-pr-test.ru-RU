---
title: "Включение сходства сеансов с помощью набора средств Azure для Eclipse"
description: "Узнайте, как включить сходство сеансов с помощью набора средств Azure для Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: ab8623d6f9751ed6d71d9a5b1c0d5e939c442862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="enable-session-affinity"></a><span data-ttu-id="bf488-103">Включение сходства сеансов</span><span class="sxs-lookup"><span data-stu-id="bf488-103">Enable Session Affinity</span></span>
<span data-ttu-id="bf488-104">В наборе средств Azure для Eclipse вы можете включить для ролей сходство сеансов HTTP (называемое также прикрепленным сеансами).</span><span class="sxs-lookup"><span data-stu-id="bf488-104">Within the Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles.</span></span> <span data-ttu-id="bf488-105">На следующем рисунке показано диалоговое окно свойств **Балансировка нагрузки** , используемое для включения функции сходства сеансов:</span><span class="sxs-lookup"><span data-stu-id="bf488-105">The following image shows the **Load Balancing** properties dialog used to enable the session affinity feature:</span></span>

![][ic719492]

## <a name="to-enable-session-affinity-for-your-role"></a><span data-ttu-id="bf488-106">Включение сходства сеансов для роли</span><span class="sxs-lookup"><span data-stu-id="bf488-106">To enable session affinity for your role</span></span>
1. <span data-ttu-id="bf488-107">Щелкните правой кнопкой мыши роль в обозревателе проектов Eclipse, выберите пункт **Azure**, а затем щелкните **Балансировка нагрузки**.</span><span class="sxs-lookup"><span data-stu-id="bf488-107">Right-click the role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.</span></span>

2. <span data-ttu-id="bf488-108">В диалоговом окне **Properties for WorkerRole1 Load Balancing** (Свойства для балансировки нагрузки WorkerRole1) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="bf488-108">In the **Properties for WorkerRole1 Load Balancing** dialog:</span></span>

   <span data-ttu-id="bf488-109">А.</span><span class="sxs-lookup"><span data-stu-id="bf488-109">a.</span></span> <span data-ttu-id="bf488-110">Установите флажок **Enable HTTP session affinity (sticky sessions) for this role**</span><span class="sxs-lookup"><span data-stu-id="bf488-110">Check **Enable HTTP session affinity (sticky sessions) for this role.**</span></span>

   <span data-ttu-id="bf488-111">b.</span><span class="sxs-lookup"><span data-stu-id="bf488-111">b.</span></span> <span data-ttu-id="bf488-112">Для параметра **Input endpoint to use** (Используемая входная конечная точка) выберите используемую входную конечную точку, например **http (public:80, private:8080)**.</span><span class="sxs-lookup"><span data-stu-id="bf488-112">For **Input endpoint to use**, select an input endpoint to use, for example, **http (public:80, private:8080)**.</span></span> <span data-ttu-id="bf488-113">Ваше приложение должно использовать эту конечную точку в качестве своей конечной точки HTTP.</span><span class="sxs-lookup"><span data-stu-id="bf488-113">Your application must use this endpoint as its HTTP endpoint.</span></span> <span data-ttu-id="bf488-114">Вы можете включить для роли несколько конечных точек, однако лишь одну из них можно выбрать для поддержки прикрепленных сеансов.</span><span class="sxs-lookup"><span data-stu-id="bf488-114">You can enable multiple endpoints for your role, but you can select only one of them to support sticky sessions.</span></span>

   <span data-ttu-id="bf488-115">c.</span><span class="sxs-lookup"><span data-stu-id="bf488-115">c.</span></span> <span data-ttu-id="bf488-116">Перестройте приложение.</span><span class="sxs-lookup"><span data-stu-id="bf488-116">Rebuild your application.</span></span>

<span data-ttu-id="bf488-117">Если после включения используется несколько экземпляров роли, HTTP-запросы, поступающие от конкретного клиента, будут по-прежнему обрабатываться в том же экземпляре роли.</span><span class="sxs-lookup"><span data-stu-id="bf488-117">Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by the same role instance.</span></span>

<span data-ttu-id="bf488-118">Набор средств Eclipse позволяет реализовать это путем установки специального модуля IIS — маршрутизация запросов приложений (ARR) — в каждом из экземпляров роли.</span><span class="sxs-lookup"><span data-stu-id="bf488-118">The Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances.</span></span> <span data-ttu-id="bf488-119">Модуль ARR перенаправляет HTTP-запросы в соответствующий экземпляр роли.</span><span class="sxs-lookup"><span data-stu-id="bf488-119">ARR reroutes HTTP requests to the appropriate role instance.</span></span> <span data-ttu-id="bf488-120">Набор средств автоматически перенастраивает выбранную конечную точку, чтобы входящий HTTP-трафик сначала перенаправлялся в программное обеспечение ARR.</span><span class="sxs-lookup"><span data-stu-id="bf488-120">The toolkit automatically reconfigures the selected endpoint so that the incoming HTTP traffic is first routed to the ARR software.</span></span> <span data-ttu-id="bf488-121">Набор средств также создает новую внутреннюю конечную точку, на прослушивание которой настроен ваш сервер Java.</span><span class="sxs-lookup"><span data-stu-id="bf488-121">The toolkit also creates a new internal endpoint that your Java server is configured to listen to.</span></span> <span data-ttu-id="bf488-122">Это конечная точка, используемая ARR для перенаправления HTTP-трафика в соответствующий экземпляр роли.</span><span class="sxs-lookup"><span data-stu-id="bf488-122">That is the endpoint used by ARR to reroute the HTTP traffic to the appropriate role instance.</span></span> <span data-ttu-id="bf488-123">Таким образом, каждый экземпляр роли в развертывании с несколькими экземплярами служит в качестве обратного прокси-сервера для всех других экземпляров, реализуя функцию прикрепленных сеансов.</span><span class="sxs-lookup"><span data-stu-id="bf488-123">This way, each role instance in your multi-instance deployment serves as a reverse proxy for all the other instances, enabling sticky sessions.</span></span>

## <a name="notes-about-session-affinity"></a><span data-ttu-id="bf488-124">Заметки о сходстве сеансов</span><span class="sxs-lookup"><span data-stu-id="bf488-124">Notes about session affinity</span></span>
* <span data-ttu-id="bf488-125">Сходство сеансов не работает в эмуляторе вычислений.</span><span class="sxs-lookup"><span data-stu-id="bf488-125">Session affinity does not work in the compute emulator.</span></span> <span data-ttu-id="bf488-126">Соответствующие параметры можно применить в эмуляторе вычислений, не затрагивая процесс сборки или работу эмулятора вычислений, однако сама эта функция в эмуляторе вычислений не работает.</span><span class="sxs-lookup"><span data-stu-id="bf488-126">The settings can be applied in the compute emulator without interfering with your build process or compute emulator execution, but the feature itself does not function within the compute emulator.</span></span>

* <span data-ttu-id="bf488-127">Включение сходства сеансов приведет к увеличению пространства на диске, занимаемого вашим развертыванием в Azure, так как будет скачано дополнительное программное обеспечение, устанавливаемое в экземплярах роли при запуске службы в облаке Azure.</span><span class="sxs-lookup"><span data-stu-id="bf488-127">Enabling session affinity will result in an increase in the amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in the Azure cloud.</span></span>

* <span data-ttu-id="bf488-128">Инициализация каждой роли будет занимать больше времени.</span><span class="sxs-lookup"><span data-stu-id="bf488-128">The time to initialize each role will take longer.</span></span>

* <span data-ttu-id="bf488-129">Добавляется внутренняя конечная точка, служащая для перенаправления трафика, как было указано выше.</span><span class="sxs-lookup"><span data-stu-id="bf488-129">An internal endpoint, to function as a traffic rerouter as mentioned above, will be added.</span></span>


## <a name="see-also"></a><span data-ttu-id="bf488-130">См. также</span><span class="sxs-lookup"><span data-stu-id="bf488-130">See Also</span></span>
<span data-ttu-id="bf488-131">[Набор средств Azure для Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="bf488-131">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="bf488-132">[Создание приложения Hello World для Azure в Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="bf488-132">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="bf488-133">[Установка набора средств Azure для Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="bf488-133">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="bf488-134">Дополнительные сведения об использовании Azure с Java можно найти в [Центре разработчиков Java для Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="bf488-134">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How to Maintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
