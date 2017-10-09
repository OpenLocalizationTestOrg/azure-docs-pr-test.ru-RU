---
title: "приложение Java интенсивно aaaCompute на виртуальной Машине | Документы Microsoft"
description: "Узнайте, как можно отслеживать toocreate виртуальной машине Azure, работает под управлением приложения Java большим объемом вычислений, другое приложение Java."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: ae6f2737-94c7-4569-9913-d871450c2827
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 02a198802a8d78bd444cd5a9197a78cb94f48e3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-compute-intensive-task-in-java-on-a-virtual-machine"></a><span data-ttu-id="74da9-103">Как toorun интенсивных вычислительных задач на языке Java на виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="74da9-103">How toorun a compute-intensive task in Java on a virtual machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="74da9-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="74da9-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="74da9-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="74da9-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="74da9-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="74da9-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="74da9-107">С помощью Azure можно использовать задачи вычислений toohandle виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="74da9-107">With Azure, you can use a virtual machine toohandle compute-intensive tasks.</span></span> <span data-ttu-id="74da9-108">Например виртуальной машины можно управлять задачами и доставки результатов tooclient компьютеров или мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="74da9-108">For example, a virtual machine can handle tasks and deliver results tooclient machines or mobile applications.</span></span> <span data-ttu-id="74da9-109">После считывания в этой статье, будет иметь представление о том, как можно отслеживать toocreate виртуальной машины, которая запускает приложение Java большим объемом вычислений, другое приложение Java.</span><span class="sxs-lookup"><span data-stu-id="74da9-109">After reading this article, you will have an understanding of how toocreate a virtual machine that runs a compute-intensive Java application that can be monitored by another Java application.</span></span>

<span data-ttu-id="74da9-110">В учебнике предполагается, что вы знаете, как можно импортировать приложение Java tooyour библиотеки toocreate Java консольные приложения и создавать архивом Java (JAR).</span><span class="sxs-lookup"><span data-stu-id="74da9-110">This tutorial assumes you know how toocreate Java console applications, can import libraries tooyour Java application, and can generate a Java archive (JAR).</span></span> <span data-ttu-id="74da9-111">Знания о платформе Microsoft Azure не требуются.</span><span class="sxs-lookup"><span data-stu-id="74da9-111">No knowledge of Microsoft Azure is assumed.</span></span>

<span data-ttu-id="74da9-112">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="74da9-112">You will learn:</span></span>

* <span data-ttu-id="74da9-113">Как toocreate виртуальной машины с Java Development Kit (JDK) уже установлена.</span><span class="sxs-lookup"><span data-stu-id="74da9-113">How toocreate a virtual machine with a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="74da9-114">Каким образом tooremotely вход tooyour виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="74da9-114">How tooremotely log in tooyour virtual machine.</span></span>
* <span data-ttu-id="74da9-115">Как toocreate службы шины пространства имен.</span><span class="sxs-lookup"><span data-stu-id="74da9-115">How toocreate a service bus namespace.</span></span>
* <span data-ttu-id="74da9-116">Как toocreate приложения Java, выполняющей задачу, большим объемом вычислений.</span><span class="sxs-lookup"><span data-stu-id="74da9-116">How toocreate a Java application that performs a compute-intensive task.</span></span>
* <span data-ttu-id="74da9-117">Как toocreate приложение Java, которое отслеживает hello ход выполнения задачи hello вычислений.</span><span class="sxs-lookup"><span data-stu-id="74da9-117">How toocreate a Java application that monitors hello progress of hello compute-intensive task.</span></span>
* <span data-ttu-id="74da9-118">Как toorun hello приложений Java.</span><span class="sxs-lookup"><span data-stu-id="74da9-118">How toorun hello Java applications.</span></span>
* <span data-ttu-id="74da9-119">Как toostop hello приложений Java.</span><span class="sxs-lookup"><span data-stu-id="74da9-119">How toostop hello Java applications.</span></span>

<span data-ttu-id="74da9-120">Этого учебника будет использоваться hello коммивояжера hello ресурсоемких задач.</span><span class="sxs-lookup"><span data-stu-id="74da9-120">This tutorial will use hello Traveling Salesman Problem for hello compute-intensive task.</span></span> <span data-ttu-id="74da9-121">Hello ниже приведен пример выполняемой hello Java приложения hello вычислений задачи.</span><span class="sxs-lookup"><span data-stu-id="74da9-121">hello following is an example of hello Java application running hello compute-intensive task.</span></span>

![Средство поиска решения для задачи коммивояжера][solver_output]

<span data-ttu-id="74da9-123">Hello ниже приведен пример hello задача вычислений мониторинга hello приложений Java.</span><span class="sxs-lookup"><span data-stu-id="74da9-123">hello following is an example of hello Java application monitoring hello compute-intensive task.</span></span>

![Клиент задачи коммивояжера][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a><span data-ttu-id="74da9-125">toocreate виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="74da9-125">toocreate a virtual machine</span></span>
1. <span data-ttu-id="74da9-126">Войдите в toohello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="74da9-126">Log in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="74da9-127">Щелкните **Создать**, **Среда выполнения приложений**, **Виртуальная машина**, а затем — **Из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="74da9-127">Click **New**, click **Compute**, click **Virtual machine**, and then click **From Gallery**.</span></span>
3. <span data-ttu-id="74da9-128">В hello **выберите образ виртуальной машины** выберите **JDK 7 Windows Server 2012**.</span><span class="sxs-lookup"><span data-stu-id="74da9-128">In hello **Virtual machine image select** dialog box, select **JDK 7 Windows Server 2012**.</span></span>
   <span data-ttu-id="74da9-129">Обратите внимание, что **JDK 6 Windows Server 2012** доступен, если у вас есть устаревшие приложения, которые еще не готовы toorun JDK 7.</span><span class="sxs-lookup"><span data-stu-id="74da9-129">Note that **JDK 6 Windows Server 2012** is available in case you have legacy applications that are not yet ready toorun in JDK 7.</span></span>
4. <span data-ttu-id="74da9-130">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="74da9-130">Click **Next**.</span></span>
5. <span data-ttu-id="74da9-131">В hello **конфигурации виртуальной машины** диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="74da9-131">In hello **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="74da9-132">Укажите имя для виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="74da9-132">Specify a name for hello virtual machine.</span></span>
   2. <span data-ttu-id="74da9-133">Укажите hello toouse размер для виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="74da9-133">Specify hello size toouse for hello virtual machine.</span></span>
   3. <span data-ttu-id="74da9-134">Введите имя администратора hello в hello **имя пользователя** поля.</span><span class="sxs-lookup"><span data-stu-id="74da9-134">Enter a name for hello administrator in hello **User Name** field.</span></span> <span data-ttu-id="74da9-135">Запомните этот пароль имя и hello рядом введенной, они будут использоваться при входе удаленно toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="74da9-135">Remember this name and hello password you will enter next, you will use them when you remotely log in toohello virtual machine.</span></span>
   4. <span data-ttu-id="74da9-136">Введите пароль в hello **новый пароль** и повторно введите его в hello **Подтверждение** поля.</span><span class="sxs-lookup"><span data-stu-id="74da9-136">Enter a password in hello **New password** field, and re-enter it in hello **Confirm** field.</span></span> <span data-ttu-id="74da9-137">Это пароль учетной записи администратора hello.</span><span class="sxs-lookup"><span data-stu-id="74da9-137">This is hello Administrator account password.</span></span>
   5. <span data-ttu-id="74da9-138">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="74da9-138">Click **Next**.</span></span>
6. <span data-ttu-id="74da9-139">В hello Далее **конфигурации виртуальной машины** диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="74da9-139">In hello next **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="74da9-140">Для **облачная служба**, использовать значение по умолчанию hello **создать новую облачную службу**.</span><span class="sxs-lookup"><span data-stu-id="74da9-140">For **Cloud service**, use hello default **Create a new cloud service**.</span></span>
   2. <span data-ttu-id="74da9-141">Здравствуйте, значение для **DNS-имя облачной службы** должно быть уникальным среди cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="74da9-141">hello value for **Cloud service DNS name** must be unique across cloudapp.net.</span></span> <span data-ttu-id="74da9-142">При необходимости измените это значение, чтобы система Azure показывала его уникальность.</span><span class="sxs-lookup"><span data-stu-id="74da9-142">If needed, modify this value so that Azure indicates it is unique.</span></span>
   3. <span data-ttu-id="74da9-143">Укажите регион, территориальную группу или виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="74da9-143">Specify a region, affinity group, or virtual network.</span></span> <span data-ttu-id="74da9-144">Для целей данного учебника укажите регион, например **США, запад**.</span><span class="sxs-lookup"><span data-stu-id="74da9-144">For purposes of this tutorial, specify a region such as **West US**.</span></span>
   4. <span data-ttu-id="74da9-145">В поле **Учетная запись хранения** выберите **Использовать автоматически созданную учетную запись хранения**.</span><span class="sxs-lookup"><span data-stu-id="74da9-145">For **Storage Account**, select **Use an automatically generated storage account**.</span></span>
   5. <span data-ttu-id="74da9-146">В разделе **Группа доступности** выберите **(Нет)**.</span><span class="sxs-lookup"><span data-stu-id="74da9-146">For **Availability Set**, select **(None)**.</span></span>
   6. <span data-ttu-id="74da9-147">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="74da9-147">Click **Next**.</span></span>
7. <span data-ttu-id="74da9-148">В окончательной hello **конфигурации виртуальной машины** диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="74da9-148">In hello final **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="74da9-149">Примите записи конечной точки по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="74da9-149">Accept hello default endpoint entries.</span></span>
   2. <span data-ttu-id="74da9-150">Нажмите **Завершено**.</span><span class="sxs-lookup"><span data-stu-id="74da9-150">Click **Complete**.</span></span>

## <a name="tooremotely-log-in-tooyour-virtual-machine"></a><span data-ttu-id="74da9-151">Журнал tooremotely tooyour виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="74da9-151">tooremotely log in tooyour virtual machine</span></span>
1. <span data-ttu-id="74da9-152">Войдите на toohello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="74da9-152">Log on toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="74da9-153">Нажмите **Виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="74da9-153">Click **Virtual machines**.</span></span>
3. <span data-ttu-id="74da9-154">Щелкните имя hello виртуальную машину, которую требуется toolog в hello.</span><span class="sxs-lookup"><span data-stu-id="74da9-154">Click hello name of hello virtual machine that you want toolog in to.</span></span>
4. <span data-ttu-id="74da9-155">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="74da9-155">Click **Connect**.</span></span>
5. <span data-ttu-id="74da9-156">Принятия приглашения toohello необходимые tooconnect toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="74da9-156">Respond toohello prompts as needed tooconnect toohello virtual machine.</span></span> <span data-ttu-id="74da9-157">Когда появится сообщение hello имя и пароль администратора, используйте значения hello, предоставленный при создании виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="74da9-157">When prompted for hello administrator name and password, use hello values that you provided when you created hello virtual machine.</span></span>

<span data-ttu-id="74da9-158">Обратите внимание, что hello функциональность Azure Service Bus требует toobe сертификат Baltimore CyberTrust Root hello, устанавливаются как часть вашего JRE **cacerts** хранения.</span><span class="sxs-lookup"><span data-stu-id="74da9-158">Note that hello Azure Service Bus functionality requires hello Baltimore CyberTrust Root certificate toobe installed as part of your JRE's **cacerts** store.</span></span> <span data-ttu-id="74da9-159">Этот сертификат автоматически включается в hello среда выполнения Java (JRE) используется в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="74da9-159">This certificate is automatically included in hello Java Runtime Environment (JRE) used by this tutorial.</span></span> <span data-ttu-id="74da9-160">Если у вас этот сертификат в вашей JRE **cacerts** хранения см. в разделе [Добавление toohello сертификат, в хранилище сертификатов ЦС Java] [ add_ca_cert] сведения о добавлении она (а также сведения о просмотре hello сертификаты в хранилище cacerts).</span><span class="sxs-lookup"><span data-stu-id="74da9-160">If you do not have this certificate in your JRE **cacerts** store, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert] for information on adding it (as well as information on viewing hello certificates in your cacerts store).</span></span>

## <a name="how-toocreate-a-service-bus-namespace"></a><span data-ttu-id="74da9-161">Как toocreate службы шины пространства имен</span><span class="sxs-lookup"><span data-stu-id="74da9-161">How toocreate a service bus namespace</span></span>
<span data-ttu-id="74da9-162">с помощью Service Bus toobegin очереди в Azure, необходимо сначала создать пространство имен службы.</span><span class="sxs-lookup"><span data-stu-id="74da9-162">toobegin using Service Bus queues in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="74da9-163">Это пространство имен службы предоставляет контейнер для адресации ресурсов служебной шины в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="74da9-163">A service namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="74da9-164">toocreate пространства имен службы:</span><span class="sxs-lookup"><span data-stu-id="74da9-164">toocreate a service namespace:</span></span>

1. <span data-ttu-id="74da9-165">Войдите на toohello [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="74da9-165">Log on toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="74da9-166">В области навигации слева hello hello классический портал Azure, щелкните **шина обслуживания, управление доступом и кэширование**.</span><span class="sxs-lookup"><span data-stu-id="74da9-166">In hello lower-left navigation pane of hello Azure classic portal, click **Service Bus, Access Control & Caching**.</span></span>
3. <span data-ttu-id="74da9-167">В области верхнего левого hello hello классический портал Azure, щелкните hello **Service Bus** узел и нажмите кнопку hello **New** кнопки.</span><span class="sxs-lookup"><span data-stu-id="74da9-167">In hello upper-left pane of hello Azure classic portal, click hello **Service Bus** node, and then click hello **New** button.</span></span>  
   <span data-ttu-id="74da9-168">![Снимок экрана узла Service Bus][svc_bus_node]</span><span class="sxs-lookup"><span data-stu-id="74da9-168">![Service Bus Node screenshot][svc_bus_node]</span></span>
4. <span data-ttu-id="74da9-169">В hello **создания нового пространства имен** диалогового окна введите **пространства имен**, и нажмите кнопку toomake убедиться, что он уникален, **Проверка доступности** кнопки.</span><span class="sxs-lookup"><span data-stu-id="74da9-169">In hello **Create a new Service Namespace** dialog box, enter a **Namespace**, and then toomake sure that it is unique, click the **Check Availability** button.</span></span>  
   <span data-ttu-id="74da9-170">![Снимок экрана создания пространства имен][create_namespace]</span><span class="sxs-lookup"><span data-stu-id="74da9-170">![Create a New Namespace screenshot][create_namespace]</span></span>
5. <span data-ttu-id="74da9-171">Убедившись в том доступен hello пространства имен, выберите страну или регион, должны размещаться пространство имен и нажмите кнопку hello **создать пространство имен** кнопки.</span><span class="sxs-lookup"><span data-stu-id="74da9-171">After making sure hello namespace name is available, choose the country or region in which your namespace should be hosted, and then click hello **Create Namespace** button.</span></span>  
   
   <span data-ttu-id="74da9-172">пространство имен Hello, созданный появится в hello классический портал Azure и принимает tooactivate некоторое время.</span><span class="sxs-lookup"><span data-stu-id="74da9-172">hello namespace you created will then appear in hello Azure classic portal and takes a moment tooactivate.</span></span> <span data-ttu-id="74da9-173">Подождите, пока состояние hello **Active** прежде чем переходить к следующему шагу hello.</span><span class="sxs-lookup"><span data-stu-id="74da9-173">Wait until hello status is **Active** before continuing with hello next step.</span></span>

## <a name="obtain-hello-default-management-credentials-for-hello-namespace"></a><span data-ttu-id="74da9-174">Получить hello управления учетные данные по умолчанию для пространства имен hello</span><span class="sxs-lookup"><span data-stu-id="74da9-174">Obtain hello Default Management Credentials for hello namespace</span></span>
<span data-ttu-id="74da9-175">В операции управления tooperform заказа, например при создании очереди, для hello новое пространство имен необходимо иметь учетные данные управления hello tooobtain для пространства имен.</span><span class="sxs-lookup"><span data-stu-id="74da9-175">In order tooperform management operations, such as creating a queue, on hello new namespace, you need tooobtain hello management credentials for the namespace.</span></span>

1. <span data-ttu-id="74da9-176">В области навигации слева hello щелкните hello **Service Bus** узел, чтобы отобразить список доступных пространств имен hello.</span><span class="sxs-lookup"><span data-stu-id="74da9-176">In hello left navigation pane, click hello **Service Bus** node to display hello list of available namespaces.</span></span>
   <span data-ttu-id="74da9-177">![Снимок экрана доступных пространств имен][avail_namespaces]</span><span class="sxs-lookup"><span data-stu-id="74da9-177">![Available Namespaces screenshot][avail_namespaces]</span></span>
2. <span data-ttu-id="74da9-178">Выберите пространство имен hello, созданную из отображенного списка hello.</span><span class="sxs-lookup"><span data-stu-id="74da9-178">Select hello namespace you just created from hello list shown.</span></span>
   <span data-ttu-id="74da9-179">![Снимок экрана списка пространств имен][namespace_list]</span><span class="sxs-lookup"><span data-stu-id="74da9-179">![Namespace List screenshot][namespace_list]</span></span>
3. <span data-ttu-id="74da9-180">Hello правом **свойства** области перечислены hello свойства для нового пространства имен.</span><span class="sxs-lookup"><span data-stu-id="74da9-180">hello right-hand **Properties** pane lists hello properties for the new namespace.</span></span>
   <span data-ttu-id="74da9-181">![Снимок экрана панели свойств][properties_pane]</span><span class="sxs-lookup"><span data-stu-id="74da9-181">![Properties Pane screenshot][properties_pane]</span></span>
4. <span data-ttu-id="74da9-182">Hello **ключ по умолчанию** скрыт.</span><span class="sxs-lookup"><span data-stu-id="74da9-182">hello **Default Key** is hidden.</span></span> <span data-ttu-id="74da9-183">Нажмите кнопку hello **представление** кнопку toodisplay учетные данные безопасности hello.</span><span class="sxs-lookup"><span data-stu-id="74da9-183">Click hello **View** button toodisplay hello security credentials.</span></span>
   <span data-ttu-id="74da9-184">![Снимок экрана ключа по умолчанию][default_key]</span><span class="sxs-lookup"><span data-stu-id="74da9-184">![Default Key screenshot][default_key]</span></span>
5. <span data-ttu-id="74da9-185">Запишите hello **поставщика по умолчанию** и hello **ключ по умолчанию** как можно будет использовать эту информацию ниже tooperform операции с пространством имен.</span><span class="sxs-lookup"><span data-stu-id="74da9-185">Make a note of hello **Default Issuer** and hello **Default Key** as you will use this information below tooperform operations with the namespace.</span></span>

## <a name="how-toocreate-a-java-application-that-performs-a-compute-intensive-task"></a><span data-ttu-id="74da9-186">Как toocreate приложения Java, выполняющей задачу, большим объемом вычислений</span><span class="sxs-lookup"><span data-stu-id="74da9-186">How toocreate a Java application that performs a compute-intensive task</span></span>
1. <span data-ttu-id="74da9-187">На компьютере разработки (которая не поддерживает toobe hello виртуальную машину, созданную), hello загрузки [пакет Azure SDK для Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="74da9-187">On your development machine (which does not have toobe hello virtual machine that you created), download hello [Azure SDK for Java](https://azure.microsoft.com/develop/java/).</span></span>
2. <span data-ttu-id="74da9-188">Создайте консольное приложение Java, используя hello пример кода в конце hello в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="74da9-188">Create a Java console application using hello example code at hello end of this section.</span></span> <span data-ttu-id="74da9-189">В этом учебнике мы будем использовать **TSPSolver.java** имени файла hello Java.</span><span class="sxs-lookup"><span data-stu-id="74da9-189">In this tutorial, we'll use **TSPSolver.java** as hello Java file name.</span></span> <span data-ttu-id="74da9-190">Изменение hello **вашей\_службы\_шины\_имен**, **вашей\_службы\_шины\_владельца**и **вашей\_службы\_шины\_ключ** toouse заполнители service bus **имен**, **поставщика по умолчанию** и  **Ключ по умолчанию** соответственно.</span><span class="sxs-lookup"><span data-stu-id="74da9-190">Modify hello **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders toouse your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
3. <span data-ttu-id="74da9-191">После программирования экспорта hello tooa запускаемых Java архива приложения (JAR) и пакета hello необходимые библиотеки в hello созданный JAR-ФАЙЛ.</span><span class="sxs-lookup"><span data-stu-id="74da9-191">After coding, export hello application tooa runnable Java archive (JAR), and package hello required libraries into hello generated JAR.</span></span> <span data-ttu-id="74da9-192">В этом учебнике мы будем использовать **TSPSolver.jar** как имя JAR-ФАЙЛ создан hello.</span><span class="sxs-lookup"><span data-stu-id="74da9-192">In this tutorial, we'll use **TSPSolver.jar** as hello generated JAR name.</span></span>

<p/>

    // TSPSolver.java

    import com.microsoft.windowsazure.services.core.Configuration;
    import com.microsoft.windowsazure.services.core.ServiceException;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import java.io.*;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.ArrayList;
    import java.util.Date;
    import java.util.List;

    public class TSPSolver {

        //  Value specifying how often tooprovide an update toohello console.
        private static long loopCheck = 100000000;  

        private static long nTimes = 0, nLoops=0;

        private static double[][] distances;
        private static String[] cityNames;
        private static int[] bestOrder;
        private static double minDistance;
        private static ServiceBusContract service;

        private static void buildDistances(String fileLocation, int numCities) throws Exception{
            try{
                BufferedReader file = new BufferedReader(new InputStreamReader(new DataInputStream(new FileInputStream(new File(fileLocation)))));
                double[][] cityLocs = new double[numCities][2];
                for (int i = 0; i<numCities; i++){
                    String[] line = file.readLine().split(", ");
                    cityNames[i] = line[0];
                    cityLocs[i][0] = Double.parseDouble(line[1]);
                    cityLocs[i][1] = Double.parseDouble(line[2]);
                }
                for (int i = 0; i<numCities; i++){
                    for (int j = i; j<numCities; j++){
                        distances[i][j] = Math.hypot(Math.abs(cityLocs[i][0] - cityLocs[j][0]), Math.abs(cityLocs[i][1] - cityLocs[j][1]));
                        distances[j][i] = distances[i][j];
                    }
                }
            } catch (Exception e){
                throw e;
            }
        }

        private static void permutation(List<Integer> startCities, double distSoFar, List<Integer> restCities) throws Exception {

            try
            {
                nTimes++;
                if (nTimes == loopCheck)
                {
                    nLoops++;
                    nTimes = 0;
                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.print("Current time is " + dateFormat.format(date) + ". ");
                    System.out.println(  "Completed " + nLoops + " iterations of size of " + loopCheck + ".");
                }

                if ((restCities.size() == 1) && ((minDistance == -1) || (distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-1)] < minDistance))){
                    startCities.add(restCities.get(0));
                    newBestDistance(startCities, distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-2)]);
                    startCities.remove(startCities.size()-1);
                }
                else{
                    for (int i=0; i<restCities.size(); i++){
                        startCities.add(restCities.get(0));
                        restCities.remove(0);
                        permutation(startCities, distSoFar + distances[startCities.get(startCities.size()-1)][startCities.get(startCities.size()-2)],restCities);
                        restCities.add(startCities.get(startCities.size()-1));
                        startCities.remove(startCities.size()-1);
                    }
                }
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        private static void newBestDistance(List<Integer> cities, double distance) throws ServiceException, Exception {
            try
            {
                minDistance = distance;
                String cityList = "Shortest distance is "+minDistance+", with route: ";
                for (int i = 0; i<bestOrder.length; i++){
                    bestOrder[i] = cities.get(i);
                    cityList += cityNames[bestOrder[i]];
                    if (i != bestOrder.length -1)
                        cityList += ", ";
                }
                System.out.println(cityList);
                service.sendQueueMessage("TSPQueue", new BrokeredMessage(cityList));
            }
            catch (ServiceException se)
            {
                throw se;
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        public static void main(String args[]){

            try {

                Configuration config = ServiceBusConfiguration.configureWithWrapAuthentication(
                        "your_service_bus_namespace", "your_service_bus_owner",
                        "your_service_bus_key",
                        ".servicebus.windows.net",
                        "-sb.accesscontrol.windows.net/WRAPv0.9");

                service = ServiceBusService.create(config);

                int numCities = 10;  // Use as hello default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing toooccur other than creating hello queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing toooccur other than deleting hello queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume hello value passed in is hello number of cities toosolve.
                    numCities = Integer.valueOf(args[0]);  
                }

                System.out.println("Running for " + numCities + " cities.");

                List<Integer> startCities = new ArrayList<Integer>();
                List<Integer> restCities = new ArrayList<Integer>();
                startCities.add(0);
                for(int i = 1; i<numCities; i++)
                    restCities.add(i);
                distances = new double[numCities][numCities];
                cityNames = new String[numCities];
                buildDistances("c:\\TSP\\cities.txt", numCities);
                minDistance = -1;
                bestOrder = new int[numCities];
                permutation(startCities, 0, restCities);
                System.out.println("Final solution found!");
                service.sendQueueMessage("TSPQueue", new BrokeredMessage("Complete"));
            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }
        }

    }



## <a name="how-toocreate-a-java-application-that-monitors-hello-progress-of-hello-compute-intensive-task"></a><span data-ttu-id="74da9-193">Как toocreate приложение Java, которое отслеживает hello ход выполнения задачи hello вычислений</span><span class="sxs-lookup"><span data-stu-id="74da9-193">How toocreate a Java application that monitors hello progress of hello compute-intensive task</span></span>
1. <span data-ttu-id="74da9-194">На компьютере разработки создайте консольное приложение Java с помощью hello пример кода в конце hello в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="74da9-194">On your development machine, create a Java console application using hello example code at hello end of this section.</span></span> <span data-ttu-id="74da9-195">В этом учебнике мы будем использовать **TSPClient.java** имени файла hello Java.</span><span class="sxs-lookup"><span data-stu-id="74da9-195">In this tutorial, we'll use **TSPClient.java** as hello Java file name.</span></span> <span data-ttu-id="74da9-196">Как показано выше, измените hello **вашей\_службы\_шины\_имен**, **вашей\_службы\_шины\_владельца**, и **вашей\_службы\_шины\_ключ** toouse заполнители service bus **имен**, **поставщика по умолчанию**и **ключ по умолчанию** соответственно.</span><span class="sxs-lookup"><span data-stu-id="74da9-196">As shown earlier, modify hello **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders toouse your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
2. <span data-ttu-id="74da9-197">Экспорт tooa приложения hello запускаемых JAR и hello пакета необходимые библиотеки в hello созданный JAR-ФАЙЛ.</span><span class="sxs-lookup"><span data-stu-id="74da9-197">Export hello application tooa runnable JAR, and package hello required libraries into hello generated JAR.</span></span> <span data-ttu-id="74da9-198">В этом учебнике мы будем использовать **TSPClient.jar** как имя JAR-ФАЙЛ создан hello.</span><span class="sxs-lookup"><span data-stu-id="74da9-198">In this tutorial, we'll use **TSPClient.jar** as hello generated JAR name.</span></span>

<p/>

    // TSPClient.java

    import java.util.Date;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import com.microsoft.windowsazure.services.core.*;

    public class TSPClient
    {

        public static void main(String[] args)
        {
                try
                {

                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.println("Starting at " + dateFormat.format(date) + ".");

                    String namespace = "your_service_bus_namespace";
                    String issuer = "your_service_bus_owner";
                    String key = "your_service_bus_key";

                    Configuration config;
                    config = ServiceBusConfiguration.configureWithWrapAuthentication(
                            namespace, issuer, key,
                            ".servicebus.windows.net",
                            "-sb.accesscontrol.windows.net/WRAPv0.9");

                    ServiceBusContract service = ServiceBusService.create(config);

                    BrokeredMessage message;

                    int waitMinutes = 3;  // Use as hello default, if no value is specified at command line.
                    if (args.length != 0)
                    {
                        waitMinutes = Integer.valueOf(args[0]);  
                    }

                    String waitString;

                    waitString = (waitMinutes == 1) ? "minute." : waitMinutes + " minutes.";

                    // This queue must have previously been created.
                    service.getQueue("TSPQueue");

                    int numRead;

                    String s = null;

                    while (true)
                    {

                        ReceiveQueueMessageResult resultQM = service.receiveQueueMessage("TSPQueue");
                        message = resultQM.getValue();

                        if (null != message && null != message.getMessageId())
                        {

                            // Display hello queue message.
                            byte[] b = new byte[200];

                            System.out.print("From queue: ");

                            s = null;
                            numRead = message.getBody().read(b);
                            while (-1 != numRead)
                            {
                                s = new String(b);
                                s = s.trim();
                                System.out.print(s);
                                numRead = message.getBody().read(b);
                            }
                            System.out.println();
                            if (s.compareTo("Complete") == 0)
                            {
                                // No more processing toooccur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // hello queue is empty.
                            System.out.println("Queue is empty. Sleeping for another " + waitString);
                            Thread.sleep(60000 * waitMinutes);
                        }
                    }

            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }

        }

    }

## <a name="how-toorun-hello-java-applications"></a><span data-ttu-id="74da9-199">Как toorun hello приложений Java</span><span class="sxs-lookup"><span data-stu-id="74da9-199">How toorun hello Java applications</span></span>
<span data-ttu-id="74da9-200">Запустите приложение hello большим объемом вычислений, первый toocreate hello очереди, а затем toosolve hello проходящих Saleseman проблему, в который будет добавлять hello текущего лучший маршрут toohello очередь service bus.</span><span class="sxs-lookup"><span data-stu-id="74da9-200">Run hello compute-intensive application, first toocreate hello queue, then toosolve hello Traveling Saleseman Problem, which will add hello current best route toohello service bus queue.</span></span> <span data-ttu-id="74da9-201">При hello вычислений оно работает (или после него), результаты выполнения hello клиента toodisplay hello очередь service bus.</span><span class="sxs-lookup"><span data-stu-id="74da9-201">While hello compute-intensive application is running (or afterwards), run hello client toodisplay results from hello service bus queue.</span></span>

### <a name="toorun-hello-compute-intensive-application"></a><span data-ttu-id="74da9-202">toorun hello ресурсоемких приложений</span><span class="sxs-lookup"><span data-stu-id="74da9-202">toorun hello compute-intensive application</span></span>
1. <span data-ttu-id="74da9-203">Войдите в систему виртуальной машины tooyour.</span><span class="sxs-lookup"><span data-stu-id="74da9-203">Log on tooyour virtual machine.</span></span>
2. <span data-ttu-id="74da9-204">Создайте папку, где будет выполняться приложение.</span><span class="sxs-lookup"><span data-stu-id="74da9-204">Create a folder where you will run your application.</span></span> <span data-ttu-id="74da9-205">Например, **c:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="74da9-205">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="74da9-206">Копировать **TSPSolver.jar** слишком**c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="74da9-206">Copy **TSPSolver.jar** too**c:\TSP**,</span></span>
4. <span data-ttu-id="74da9-207">Создайте файл с именем **c:\TSP\cities.txt** с hello после содержимого.</span><span class="sxs-lookup"><span data-stu-id="74da9-207">Create a file named **c:\TSP\cities.txt** with hello following contents.</span></span>
   
        City_1, 1002.81, -1841.35
        City_2, -953.55, -229.6
        City_3, -1363.11, -1027.72
        City_4, -1884.47, -1616.16
        City_5, 1603.08, -1030.03
        City_6, -1555.58, 218.58
        City_7, 578.8, -12.87
        City_8, 1350.76, 77.79
        City_9, 293.36, -1820.01
        City_10, 1883.14, 1637.28
        City_11, -1271.41, -1670.5
        City_12, 1475.99, 225.35
        City_13, 1250.78, 379.98
        City_14, 1305.77, 569.75
        City_15, 230.77, 231.58
        City_16, -822.63, -544.68
        City_17, -817.54, -81.92
        City_18, 303.99, -1823.43
        City_19, 239.95, 1007.91
        City_20, -1302.92, 150.39
        City_21, -116.11, 1933.01
        City_22, 382.64, 835.09
        City_23, -580.28, 1040.04
        City_24, 205.55, -264.23
        City_25, -238.81, -576.48
        City_26, -1722.9, -909.65
        City_27, 445.22, 1427.28
        City_28, 513.17, 1828.72
        City_29, 1750.68, -1668.1
        City_30, 1705.09, -309.35
        City_31, -167.34, 1003.76
        City_32, -1162.85, -1674.33
        City_33, 1490.32, 821.04
        City_34, 1208.32, 1523.3
        City_35, 18.04, 1857.11
        City_36, 1852.46, 1647.75
        City_37, -167.44, -336.39
        City_38, 115.4, 0.2
        City_39, -66.96, 917.73
        City_40, 915.96, 474.1
        City_41, 140.03, 725.22
        City_42, -1582.68, 1608.88
        City_43, -567.51, 1253.83
        City_44, 1956.36, 830.92
        City_45, -233.38, 909.93
        City_46, -1750.45, 1940.76
        City_47, 405.81, 421.84
        City_48, 363.68, 768.21
        City_49, -120.3, -463.13
        City_50, 588.51, 679.33
5. <span data-ttu-id="74da9-208">В командной строке измените каталоги tooc:\TSP.</span><span class="sxs-lookup"><span data-stu-id="74da9-208">At a command prompt, change directories tooc:\TSP.</span></span>
6. <span data-ttu-id="74da9-209">Убедитесь, что папка bin hello JRE в переменной среды PATH hello.</span><span class="sxs-lookup"><span data-stu-id="74da9-209">Ensure hello JRE's bin folder is in hello PATH environment variable.</span></span>
7. <span data-ttu-id="74da9-210">Перед запуском hello TSP solver перестановок, вам потребуется очередь service bus toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="74da9-210">You'll need toocreate hello service bus queue before you run hello TSP solver permutations.</span></span> <span data-ttu-id="74da9-211">Выполнения hello следующая команда очередь service bus toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="74da9-211">Run hello following command toocreate hello service bus queue.</span></span>
   
        java -jar TSPSolver.jar createqueue
8. <span data-ttu-id="74da9-212">Hello очередь создана, можно выполнить hello TSP solver перестановок.</span><span class="sxs-lookup"><span data-stu-id="74da9-212">Now that hello queue is created, you can run hello TSP solver permutations.</span></span> <span data-ttu-id="74da9-213">Например запустите hello, следующая команда toorun hello и поиск решения для 8 городов.</span><span class="sxs-lookup"><span data-stu-id="74da9-213">For example, run hello following command toorun hello solver for 8 cities.</span></span>
   
        java -jar TSPSolver.jar 8
   
   <span data-ttu-id="74da9-214">Если число не указано, выполняется поиск для 10 городов.</span><span class="sxs-lookup"><span data-stu-id="74da9-214">If you don't specify a number, it will run for 10 cities.</span></span> <span data-ttu-id="74da9-215">Как hello нахождение текущего кратчайший маршруты, они будут добавлены toohello очереди.</span><span class="sxs-lookup"><span data-stu-id="74da9-215">As hello solver finds current shortest routes, it will add them toohello queue.</span></span>

> [!NOTE]
> <span data-ttu-id="74da9-216">Hello большего hello чисел, которое было задано, будет выполняться дольше hello solver hello.</span><span class="sxs-lookup"><span data-stu-id="74da9-216">hello larger hello number that you specify, hello longer hello solver will run.</span></span> <span data-ttu-id="74da9-217">Например, поиск для 14 городов может занять несколько минут, а для 15 городов — несколько часов.</span><span class="sxs-lookup"><span data-stu-id="74da9-217">For example, running for 14 cities could take several minutes, and running for 15 cities could take several hours.</span></span> <span data-ttu-id="74da9-218">Увеличение too16 или дополнительные города может привести к дней среды выполнения (в конечном счете недель, месяцев и лет).</span><span class="sxs-lookup"><span data-stu-id="74da9-218">Increasing too16 or more cities could result in days of runtime (eventually weeks, months, and years).</span></span> <span data-ttu-id="74da9-219">Это происходит из-за toohello быстрое увеличение hello число перестановок, поиска решения hello истинность города увеличения количества hello.</span><span class="sxs-lookup"><span data-stu-id="74da9-219">This is due toohello rapid increase in hello number of permutations evaluated by hello solver as hello number of cities increases.</span></span>
> 
> 

### <a name="how-toorun-hello-monitoring-client-application"></a><span data-ttu-id="74da9-220">Как toorun hello мониторинга клиентского приложения</span><span class="sxs-lookup"><span data-stu-id="74da9-220">How toorun hello monitoring client application</span></span>
1. <span data-ttu-id="74da9-221">Войдите в систему компьютера tooyour, где будет выполняться клиентское приложение hello.</span><span class="sxs-lookup"><span data-stu-id="74da9-221">Log on tooyour machine where you will run hello client application.</span></span> <span data-ttu-id="74da9-222">Это не обязательно toobe hello компьютере под управлением hello **TSPSolver** приложения, хотя он может быть.</span><span class="sxs-lookup"><span data-stu-id="74da9-222">This does not need toobe hello same machine running hello **TSPSolver** application, although it can be.</span></span>
2. <span data-ttu-id="74da9-223">Создайте папку, где будет выполняться приложение.</span><span class="sxs-lookup"><span data-stu-id="74da9-223">Create a folder where you will run your application.</span></span> <span data-ttu-id="74da9-224">Например, **c:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="74da9-224">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="74da9-225">Копировать **TSPClient.jar** слишком**c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="74da9-225">Copy **TSPClient.jar** too**c:\TSP**,</span></span>
4. <span data-ttu-id="74da9-226">Убедитесь, что папка bin hello JRE в переменной среды PATH hello.</span><span class="sxs-lookup"><span data-stu-id="74da9-226">Ensure hello JRE's bin folder is in hello PATH environment variable.</span></span>
5. <span data-ttu-id="74da9-227">В командной строке измените каталоги tooc:\TSP.</span><span class="sxs-lookup"><span data-stu-id="74da9-227">At a command prompt, change directories tooc:\TSP.</span></span>
6. <span data-ttu-id="74da9-228">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="74da9-228">Run hello following command.</span></span>
   
        java -jar TSPClient.jar
   
    <span data-ttu-id="74da9-229">При необходимости укажите номер hello toosleep минут между проверки очереди hello, передавая аргумент командной строки.</span><span class="sxs-lookup"><span data-stu-id="74da9-229">Optionally, specify hello number of minutes toosleep in between checking hello queue, by passing in a command-line argument.</span></span> <span data-ttu-id="74da9-230">Hello период по умолчанию спящего режима проверки hello очереди — 3 минуты, который используется, если передается аргумент командной строки, не слишком**TSPClient**.</span><span class="sxs-lookup"><span data-stu-id="74da9-230">hello default sleep period for checking hello queue is 3 minutes, which is used if no command-line argument is passed too**TSPClient**.</span></span> <span data-ttu-id="74da9-231">Toouse другое значение для интервала hello спящего режима, например, одну минуту, запустите hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="74da9-231">If you want toouse a different value for hello sleep interval, for example, one minute, run hello following command.</span></span>
   
        java -jar TSPClient.jar 1
   
    <span data-ttu-id="74da9-232">Hello клиента будет выполняться, пока очередь сообщений «Завершено».</span><span class="sxs-lookup"><span data-stu-id="74da9-232">hello client will run until it sees a queue message of "Complete".</span></span> <span data-ttu-id="74da9-233">Обратите внимание, что при запуске несколько вхождений hello поиска решения без запуска клиента hello может потребовать toorun hello клиента очереди пустой hello toocompletely несколько раз.</span><span class="sxs-lookup"><span data-stu-id="74da9-233">Note that if you run multiple occurrences of hello solver without running hello client, you may need toorun hello client multiple times toocompletely empty hello queue.</span></span> <span data-ttu-id="74da9-234">Кроме того можно удалить очередь hello и создайте его заново.</span><span class="sxs-lookup"><span data-stu-id="74da9-234">Alternatively, you can delete hello queue and then create it again.</span></span> <span data-ttu-id="74da9-235">очередь toodelete hello, запустите следующие hello **TSPSolver** (не **TSPClient**) команды.</span><span class="sxs-lookup"><span data-stu-id="74da9-235">toodelete hello queue, run hello following **TSPSolver** (not **TSPClient**)  command.</span></span>
   
        java -jar TSPSolver.jar deletequeue
   
    <span data-ttu-id="74da9-236">Поиск решения Hello будет выполняться, пока закончится ее выполнение проверки всех маршрутов.</span><span class="sxs-lookup"><span data-stu-id="74da9-236">hello solver will run until it finishes examining all routes.</span></span>

## <a name="how-toostop-hello-java-applications"></a><span data-ttu-id="74da9-237">Как toostop hello приложений Java</span><span class="sxs-lookup"><span data-stu-id="74da9-237">How toostop hello Java applications</span></span>
<span data-ttu-id="74da9-238">Для поиска решения hello и клиентских приложений, можно нажать клавишу **Ctrl + C** tooexit, если требуется завершения предыдущего toonormal tooend.</span><span class="sxs-lookup"><span data-stu-id="74da9-238">For both hello solver and client applications, you can press **Ctrl+C** tooexit if you want tooend prior toonormal completion.</span></span>

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md
