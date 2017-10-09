---
title: "Здравствуйте, aaaEnable сходство сеансов с помощью средств Azure для Eclipse"
description: "Узнайте, как hello tooenable сходство сеанса с помощью средств Azure для Eclipse."
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
ms.openlocfilehash: 523e728c58bda95e7af4b242e831694eb6d75cb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-session-affinity"></a><span data-ttu-id="dc579-103">Включение сходства сеансов</span><span class="sxs-lookup"><span data-stu-id="dc579-103">Enable Session Affinity</span></span>
<span data-ttu-id="dc579-104">В hello средств Azure для Eclipse можно включить соответствие сеанса HTTP или «закрепленные сеансы» для ваших ролей.</span><span class="sxs-lookup"><span data-stu-id="dc579-104">Within hello Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles.</span></span> <span data-ttu-id="dc579-105">Hello на рисунке показаны hello **балансировки нагрузки** функции соответствия сеанса hello tooenable использование диалогового окна свойств:</span><span class="sxs-lookup"><span data-stu-id="dc579-105">hello following image shows hello **Load Balancing** properties dialog used tooenable hello session affinity feature:</span></span>

![][ic719492]

## <a name="tooenable-session-affinity-for-your-role"></a><span data-ttu-id="dc579-106">сходство сеансов tooenable для роли</span><span class="sxs-lookup"><span data-stu-id="dc579-106">tooenable session affinity for your role</span></span>
1. <span data-ttu-id="dc579-107">Щелкните правой кнопкой мыши роль hello в обозревателе проектов Eclipse, щелкните **Azure**, а затем нажмите кнопку **балансировки нагрузки**.</span><span class="sxs-lookup"><span data-stu-id="dc579-107">Right-click hello role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.</span></span>

2. <span data-ttu-id="dc579-108">В hello **свойства для балансировки нагрузки WorkerRole1** диалогового окна:</span><span class="sxs-lookup"><span data-stu-id="dc579-108">In hello **Properties for WorkerRole1 Load Balancing** dialog:</span></span>

   <span data-ttu-id="dc579-109">а.</span><span class="sxs-lookup"><span data-stu-id="dc579-109">a.</span></span> <span data-ttu-id="dc579-110">Установите флажок **Enable HTTP session affinity (sticky sessions) for this role**</span><span class="sxs-lookup"><span data-stu-id="dc579-110">Check **Enable HTTP session affinity (sticky sessions) for this role.**</span></span>

   <span data-ttu-id="dc579-111">b.</span><span class="sxs-lookup"><span data-stu-id="dc579-111">b.</span></span> <span data-ttu-id="dc579-112">Для **входной конечной точки toouse**, выберите toouse входную конечную точку, например, **http (общедоступный: 80, частный: 8080)**.</span><span class="sxs-lookup"><span data-stu-id="dc579-112">For **Input endpoint toouse**, select an input endpoint toouse, for example, **http (public:80, private:8080)**.</span></span> <span data-ttu-id="dc579-113">Ваше приложение должно использовать эту конечную точку в качестве своей конечной точки HTTP.</span><span class="sxs-lookup"><span data-stu-id="dc579-113">Your application must use this endpoint as its HTTP endpoint.</span></span> <span data-ttu-id="dc579-114">Можно включить несколько конечных точек для роли, но можно выбрать только один из них toosupport закрепленных сеансов.</span><span class="sxs-lookup"><span data-stu-id="dc579-114">You can enable multiple endpoints for your role, but you can select only one of them toosupport sticky sessions.</span></span>

   <span data-ttu-id="dc579-115">c.</span><span class="sxs-lookup"><span data-stu-id="dc579-115">c.</span></span> <span data-ttu-id="dc579-116">Перестройте приложение.</span><span class="sxs-lookup"><span data-stu-id="dc579-116">Rebuild your application.</span></span>

<span data-ttu-id="dc579-117">После включения, если имеется более одного экземпляра роли, HTTP-запросы, поступающие от конкретного клиента продолжит обрабатываются hello же экземпляра роли.</span><span class="sxs-lookup"><span data-stu-id="dc579-117">Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by hello same role instance.</span></span>

<span data-ttu-id="dc579-118">Hello средств Eclipse позволяет сделать это путем установки специального модуля IIS маршрутизации запросов приложений (ARR) в каждый из экземпляров ролей.</span><span class="sxs-lookup"><span data-stu-id="dc579-118">hello Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances.</span></span> <span data-ttu-id="dc579-119">ARR перенаправляет HTTP запросы toohello соответствующий экземпляр роли.</span><span class="sxs-lookup"><span data-stu-id="dc579-119">ARR reroutes HTTP requests toohello appropriate role instance.</span></span> <span data-ttu-id="dc579-120">набор средств Hello автоматически настроит hello выбранной конечной точки, таким образом, чтобы входящий трафик HTTP hello первый ARR перенаправленное toohello программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="dc579-120">hello toolkit automatically reconfigures hello selected endpoint so that hello incoming HTTP traffic is first routed toohello ARR software.</span></span> <span data-ttu-id="dc579-121">набор средств Hello также создает новую внутреннюю конечную точку, toolisten, настроенных на сервере Java.</span><span class="sxs-lookup"><span data-stu-id="dc579-121">hello toolkit also creates a new internal endpoint that your Java server is configured toolisten to.</span></span> <span data-ttu-id="dc579-122">Это hello конечная точка, используемая с ARR tooreroute hello HTTP трафика toohello соответствующий экземпляр роли.</span><span class="sxs-lookup"><span data-stu-id="dc579-122">That is hello endpoint used by ARR tooreroute hello HTTP traffic toohello appropriate role instance.</span></span> <span data-ttu-id="dc579-123">Таким образом, каждый экземпляр роли в развертывании с несколькими экземплярами служит в качестве обратного прокси-сервера для всех hello других экземпляров, включая закрепленные сеансы.</span><span class="sxs-lookup"><span data-stu-id="dc579-123">This way, each role instance in your multi-instance deployment serves as a reverse proxy for all hello other instances, enabling sticky sessions.</span></span>

## <a name="notes-about-session-affinity"></a><span data-ttu-id="dc579-124">Заметки о сходстве сеансов</span><span class="sxs-lookup"><span data-stu-id="dc579-124">Notes about session affinity</span></span>
* <span data-ttu-id="dc579-125">Соответствие сеанса не работает в эмуляторе вычислений hello.</span><span class="sxs-lookup"><span data-stu-id="dc579-125">Session affinity does not work in hello compute emulator.</span></span> <span data-ttu-id="dc579-126">Параметры Hello может применяться в эмуляторе вычислений hello, не нарушая процесса построения или выполнения эмулятора вычислений, но сама функция hello не работает в эмуляторе вычислений hello.</span><span class="sxs-lookup"><span data-stu-id="dc579-126">hello settings can be applied in hello compute emulator without interfering with your build process or compute emulator execution, but hello feature itself does not function within hello compute emulator.</span></span>

* <span data-ttu-id="dc579-127">Включение соответствия сеанса приведет к увеличению hello объем дискового пространства, занимаемого развертыванием в Azure, как дополнительное программное обеспечение будет загружен и установлен в экземпляры роли, при запуске службы в облаке Azure hello.</span><span class="sxs-lookup"><span data-stu-id="dc579-127">Enabling session affinity will result in an increase in hello amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in hello Azure cloud.</span></span>

* <span data-ttu-id="dc579-128">время tooinitialize Hello каждой роли займет больше времени.</span><span class="sxs-lookup"><span data-stu-id="dc579-128">hello time tooinitialize each role will take longer.</span></span>

* <span data-ttu-id="dc579-129">Внутренняя конечная точка, toofunction перенаправления трафика, как было сказано выше, будут добавлены.</span><span class="sxs-lookup"><span data-stu-id="dc579-129">An internal endpoint, toofunction as a traffic rerouter as mentioned above, will be added.</span></span>


## <a name="see-also"></a><span data-ttu-id="dc579-130">См. также</span><span class="sxs-lookup"><span data-stu-id="dc579-130">See Also</span></span>
<span data-ttu-id="dc579-131">[Набор средств Azure для Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="dc579-131">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="dc579-132">[Создание приложения Hello World для Azure в Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="dc579-132">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="dc579-133">[Установка средств Azure для Eclipse hello][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="dc579-133">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="dc579-134">Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="dc579-134">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How tooMaintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
