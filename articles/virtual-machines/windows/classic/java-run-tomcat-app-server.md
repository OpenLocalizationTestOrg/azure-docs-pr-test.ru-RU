---
title: "сервер приложений Java aaaRun в классической виртуальной Машине Azure | Документы Microsoft"
description: "В этом учебнике используются ресурсы, созданные с помощью hello классической модели развертывания и показывает, как toocreate Windows виртуальной машины и настройте его toorun сервера приложений Apache Tomcat."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d627aa09-f7d6-4239-8110-f8fc5111b939
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 03/16/2017
ms.author: robmcm
ms.openlocfilehash: 2d9f586c9f628d3738522b320996b95b078d7454
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-java-application-server-on-a-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="0feba-103">Как toorun сервера приложений Java на виртуальной машине, созданные с hello классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="0feba-103">How toorun a Java application server on a virtual machine created with hello classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0feba-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0feba-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0feba-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="0feba-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="0feba-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0feba-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="0feba-107">Toodeploy веб-приложение, с помощью Java 8 и Tomcat шаблона диспетчера ресурсов. в разделе [здесь](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span><span class="sxs-lookup"><span data-stu-id="0feba-107">For a Resource Manager template toodeploy a webapp with Java 8 and Tomcat, see [here](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span></span>

<span data-ttu-id="0feba-108">С помощью Azure можно использовать возможности сервера tooprovide виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0feba-108">With Azure, you can use a virtual machine tooprovide server capabilities.</span></span> <span data-ttu-id="0feba-109">Например виртуальная машина, работающая в Azure может быть toohost настроенный сервер приложений Java, такие как Apache Tomcat.</span><span class="sxs-lookup"><span data-stu-id="0feba-109">As an example, a virtual machine running on Azure can be configured toohost a Java application server, such as Apache Tomcat.</span></span>

<span data-ttu-id="0feba-110">Изучив это руководство, будет иметь представление о том, как toocreate виртуальной машины в Azure и настройте его toorun сервера приложений Java.</span><span class="sxs-lookup"><span data-stu-id="0feba-110">After completing this guide, you will have an understanding of how toocreate a virtual machine running on Azure and configure it toorun a Java application server.</span></span> <span data-ttu-id="0feba-111">Будет Дополнительные сведения и выполните следующие задачи hello.</span><span class="sxs-lookup"><span data-stu-id="0feba-111">You will learn and perform hello following tasks:</span></span>

* <span data-ttu-id="0feba-112">Как toocreate виртуальной машины имеет Java Development Kit (JDK) уже установлена.</span><span class="sxs-lookup"><span data-stu-id="0feba-112">How toocreate a virtual machine that has a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="0feba-113">Как tooremotely вход tooyour виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0feba-113">How tooremotely sign in tooyour virtual machine.</span></span>
* <span data-ttu-id="0feba-114">Как tooinstall сервера приложений Java — Apache Tomcat — на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="0feba-114">How tooinstall a Java application server--Apache Tomcat--on your virtual machine.</span></span>
* <span data-ttu-id="0feba-115">Как toocreate конечную точку для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0feba-115">How toocreate an endpoint for your virtual machine.</span></span>
* <span data-ttu-id="0feba-116">Как tooopen hello порт брандмауэра для сервера приложений.</span><span class="sxs-lookup"><span data-stu-id="0feba-116">How tooopen a port in hello firewall for your application server.</span></span>

<span data-ttu-id="0feba-117">Hello завершить результаты установки в Tomcat, работающий на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="0feba-117">hello completed installation results in Tomcat running on a virtual machine.</span></span>

![Виртуальная машина с Apache Tomcat][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a><span data-ttu-id="0feba-119">toocreate виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="0feba-119">toocreate a virtual machine</span></span>
1. <span data-ttu-id="0feba-120">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0feba-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="0feba-121">Нажмите кнопку **New**, нажмите кнопку **вычислений**, нажмите кнопку **все** в hello **рекомендуемыми приложениями**.</span><span class="sxs-lookup"><span data-stu-id="0feba-121">Click **New**, click **Compute**, then click **See all** in hello **Featured apps**.</span></span>
3. <span data-ttu-id="0feba-122">Нажмите кнопку **JDK**, нажмите кнопку **JDK 8** в hello **JDK** области.</span><span class="sxs-lookup"><span data-stu-id="0feba-122">Click **JDK**, click **JDK 8** in hello **JDK** pane.</span></span>  
   <span data-ttu-id="0feba-123">Создание образа виртуальной машины, поддерживающие **JDK 6** и **JDK 7** доступны, если у вас есть устаревшие приложения, которые не готовы toorun JDK 8.</span><span class="sxs-lookup"><span data-stu-id="0feba-123">Virtual machine images that support **JDK 6** and **JDK 7** are available if you have legacy applications that are not ready toorun in JDK 8.</span></span>
4. <span data-ttu-id="0feba-124">В области hello JDK 8 выберите **классический**, нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="0feba-124">In hello JDK 8 pane, select **Classic**, then click **Create**.</span></span>
5. <span data-ttu-id="0feba-125">В hello **основы** колонки:</span><span class="sxs-lookup"><span data-stu-id="0feba-125">In hello **Basics** blade:</span></span>
   1. <span data-ttu-id="0feba-126">Укажите имя для виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="0feba-126">Specify a name for hello virtual machine.</span></span>
   2. <span data-ttu-id="0feba-127">Введите имя администратора hello в hello **имя пользователя** поля.</span><span class="sxs-lookup"><span data-stu-id="0feba-127">Enter a name for hello administrator in hello **User Name** field.</span></span> <span data-ttu-id="0feba-128">Запомнить это имя и соответствующий пароль в следующее поле hello hello.</span><span class="sxs-lookup"><span data-stu-id="0feba-128">Remember this name and hello associated password that follows in hello next field.</span></span> <span data-ttu-id="0feba-129">Они необходимы, при удаленном входе в toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0feba-129">You need them when you remotely sign in toohello virtual machine.</span></span>
   3. <span data-ttu-id="0feba-130">Введите пароль в hello **новый пароль** поле, а затем введите его в hello **подтверждение пароля** поля.</span><span class="sxs-lookup"><span data-stu-id="0feba-130">Enter a password in hello **New password** field, and reenter it in hello **Confirm password** field.</span></span> <span data-ttu-id="0feba-131">Этот пароль — для hello учетной записи администратора.</span><span class="sxs-lookup"><span data-stu-id="0feba-131">This password is for hello Administrator account.</span></span>
   4. <span data-ttu-id="0feba-132">Выберите hello соответствующие **подписки**.</span><span class="sxs-lookup"><span data-stu-id="0feba-132">Select hello appropriate **Subscription**.</span></span>
   5. <span data-ttu-id="0feba-133">Для hello **группы ресурсов**, нажмите кнопку **создать новый** и введите имя новой группы ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="0feba-133">For hello **Resource group**, click **Create new** and enter hello name of a new resource group.</span></span> <span data-ttu-id="0feba-134">Или щелкните **использовать существующие** и выберите один из hello доступных групп ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0feba-134">Or, click **Use existing** and select one of hello available resource groups.</span></span>
   6. <span data-ttu-id="0feba-135">Выберите расположение, где находится hello виртуальной машины, такие как **центральных штатах юга США**.</span><span class="sxs-lookup"><span data-stu-id="0feba-135">Select a location where hello virtual machine resides, such as **South Central US**.</span></span>
6. <span data-ttu-id="0feba-136">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0feba-136">Click **Next**.</span></span>
7. <span data-ttu-id="0feba-137">В hello **размер образа виртуальной машины** колонке выберите **A1 Standard** или другой соответствующий образ.</span><span class="sxs-lookup"><span data-stu-id="0feba-137">In hello **Virtual machine image size** blade, select **A1 Standard** or another appropriate image.</span></span>
8. <span data-ttu-id="0feba-138">Нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="0feba-138">Click **Select**.</span></span>

9. <span data-ttu-id="0feba-139">В hello **параметры** колонка, щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0feba-139">In hello **Settings** blade, click **OK**.</span></span> <span data-ttu-id="0feba-140">Можно использовать значения по умолчанию hello, предоставляемых Azure.</span><span class="sxs-lookup"><span data-stu-id="0feba-140">You can use hello default values provided by Azure.</span></span>  
10. <span data-ttu-id="0feba-141">В hello **Сводка** колонка, щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0feba-141">In hello **Summary** blade, click **OK**.</span></span>

## <a name="tooremotely-sign-in-tooyour-virtual-machine"></a><span data-ttu-id="0feba-142">tooremotely входа tooyour виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="0feba-142">tooremotely sign in tooyour virtual machine</span></span>
1. <span data-ttu-id="0feba-143">Войдите на toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0feba-143">Log on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0feba-144">Щелкните **Виртуальные машины (классические)**.</span><span class="sxs-lookup"><span data-stu-id="0feba-144">Click **Virtual machines (classic)**.</span></span> <span data-ttu-id="0feba-145">При необходимости щелкните **больше услуг** на hello нижний левый угол в группе категорий услуг hello.</span><span class="sxs-lookup"><span data-stu-id="0feba-145">If needed, click **More services** at hello bottom left corner under hello service categories.</span></span> <span data-ttu-id="0feba-146">Hello **виртуальные машины (классические)** запись указана в hello **вычислений** группы.</span><span class="sxs-lookup"><span data-stu-id="0feba-146">hello **Virtual machines (classic)** entry is listed in hello **Compute** group.</span></span>
3. <span data-ttu-id="0feba-147">Щелкните имя hello виртуальную машину, которую требуется toosign в hello.</span><span class="sxs-lookup"><span data-stu-id="0feba-147">Click hello name of hello virtual machine that you want toosign in to.</span></span>
4. <span data-ttu-id="0feba-148">После запуска виртуальной машины hello меню вверху hello области hello разрешены подключения.</span><span class="sxs-lookup"><span data-stu-id="0feba-148">After hello virtual machine has started, a menu at hello top of hello pane allows connections.</span></span>
5. <span data-ttu-id="0feba-149">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="0feba-149">Click **Connect**.</span></span>
6. <span data-ttu-id="0feba-150">Принятия приглашения toohello необходимые tooconnect toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0feba-150">Respond toohello prompts as needed tooconnect toohello virtual machine.</span></span> <span data-ttu-id="0feba-151">Как правило сохранении или открытии hello RDP-файл, содержащий сведения о соединении hello.</span><span class="sxs-lookup"><span data-stu-id="0feba-151">Typically, you save or open hello .rdp file that contains hello connection details.</span></span> <span data-ttu-id="0feba-152">Может иметь toocopy hello URL-адрес: порт hello последнюю часть первая строка hello hello RDP-файл и вставьте его в приложение удаленного входа.</span><span class="sxs-lookup"><span data-stu-id="0feba-152">You might have toocopy hello url:port as hello last part of hello first line of hello .rdp file and paste it in a remote sign-in application.</span></span>

## <a name="tooinstall-a-java-application-server-on-your-virtual-machine"></a><span data-ttu-id="0feba-153">tooinstall сервера приложений Java на виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="0feba-153">tooinstall a Java application server on your virtual machine</span></span>
<span data-ttu-id="0feba-154">Можно скопировать виртуальной машины tooyour сервера приложений Java, или можно установить до установки сервера приложений Java.</span><span class="sxs-lookup"><span data-stu-id="0feba-154">You can copy a Java application server tooyour virtual machine, or you can install a Java application server through an installer.</span></span>

<span data-ttu-id="0feba-155">В этом учебнике используется Tomcat как tooinstall сервера приложений Java hello.</span><span class="sxs-lookup"><span data-stu-id="0feba-155">This tutorial uses Tomcat as hello Java application server tooinstall.</span></span>

1. <span data-ttu-id="0feba-156">Если вы вошли в tooyour виртуальной машины, откройте сеанс браузера слишком[Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span><span class="sxs-lookup"><span data-stu-id="0feba-156">When you are signed in tooyour virtual machine, open a browser session too[Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span></span>
2. <span data-ttu-id="0feba-157">Дважды щелкните ссылку hello **установщика службы Windows 32-разрядной или 64-разрядной**.</span><span class="sxs-lookup"><span data-stu-id="0feba-157">Double-click hello link for **32-bit/64-bit Windows Service Installer**.</span></span> <span data-ttu-id="0feba-158">При использовании этого метода сервер Tomcat устанавливается в качестве службы Windows.</span><span class="sxs-lookup"><span data-stu-id="0feba-158">By using this technique, Tomcat installs as a Windows service.</span></span>
3. <span data-ttu-id="0feba-159">При появлении запроса выберите установщик toorun hello.</span><span class="sxs-lookup"><span data-stu-id="0feba-159">When prompted, choose toorun hello installer.</span></span>
4. <span data-ttu-id="0feba-160">В рамках hello **Apache Tomcat установки** tooinstall Tomcat по запросу мастера, выполните hello.</span><span class="sxs-lookup"><span data-stu-id="0feba-160">Within hello **Apache Tomcat Setup** wizard, follow hello prompts tooinstall Tomcat.</span></span> <span data-ttu-id="0feba-161">Для целей этого учебника hello принять значения по умолчанию hello нормально.</span><span class="sxs-lookup"><span data-stu-id="0feba-161">For hello purposes of this tutorial, accepting hello defaults is fine.</span></span> <span data-ttu-id="0feba-162">По достижении hello **hello завершение работы мастера установки Apache Tomcat** диалоговое окно, можно при необходимости проверить **запустить Apache Tomcat** toohave теперь начала Tomcat.</span><span class="sxs-lookup"><span data-stu-id="0feba-162">When you reach hello **Completing hello Apache Tomcat Setup Wizard** dialog box, you can optionally check **Run Apache Tomcat** toohave Tomcat start now.</span></span> <span data-ttu-id="0feba-163">Нажмите кнопку **Готово** toocomplete hello процесс установки Tomcat.</span><span class="sxs-lookup"><span data-stu-id="0feba-163">Click **Finish** toocomplete hello Tomcat setup process.</span></span>

## <a name="toostart-tomcat"></a><span data-ttu-id="0feba-164">toostart Tomcat</span><span class="sxs-lookup"><span data-stu-id="0feba-164">toostart Tomcat</span></span>

<span data-ttu-id="0feba-165">Tomcat можно запустить вручную, открыв командную строку на виртуальной машине и hello команды **net&nbsp;запустить&nbsp;Tomcat8**.</span><span class="sxs-lookup"><span data-stu-id="0feba-165">You can manually start Tomcat by opening a command prompt on your virtual machine and running hello command **net&nbsp;start&nbsp;Tomcat8**.</span></span>

<span data-ttu-id="0feba-166">После запуска Tomcat можно получить доступ к Tomcat, введя URL-адрес hello <http://localhost: 8080> в браузере hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0feba-166">Once Tomcat is running, you can access Tomcat by entering hello URL <http://localhost:8080> in hello virtual machine's browser.</span></span>

<span data-ttu-id="0feba-167">toosee Tomcat при запуске с внешним компьютерам, нужно toocreate конечной точки и открыть порт.</span><span class="sxs-lookup"><span data-stu-id="0feba-167">toosee Tomcat running from external machines, you need toocreate an endpoint and open a port.</span></span>

## <a name="toocreate-an-endpoint-for-your-virtual-machine"></a><span data-ttu-id="0feba-168">toocreate конечную точку для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="0feba-168">toocreate an endpoint for your virtual machine</span></span>
1. <span data-ttu-id="0feba-169">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0feba-169">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0feba-170">Щелкните **Виртуальные машины (классические)**.</span><span class="sxs-lookup"><span data-stu-id="0feba-170">Click **Virtual machines (classic)**.</span></span>
3. <span data-ttu-id="0feba-171">Щелкните имя hello hello виртуальной машины, на котором выполняется сервер приложений Java.</span><span class="sxs-lookup"><span data-stu-id="0feba-171">Click hello name of hello virtual machine that is running your Java application server.</span></span>
4. <span data-ttu-id="0feba-172">Нажмите кнопку **Конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="0feba-172">Click **Endpoints**.</span></span>
5. <span data-ttu-id="0feba-173">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0feba-173">Click **Add**.</span></span>
6. <span data-ttu-id="0feba-174">В hello **добавить конечную точку** диалоговое окно:</span><span class="sxs-lookup"><span data-stu-id="0feba-174">In hello **Add endpoint** dialog box:</span></span>
   1. <span data-ttu-id="0feba-175">Укажите имя для конечной точки hello; например **HttpIn**.</span><span class="sxs-lookup"><span data-stu-id="0feba-175">Specify a name for hello endpoint; for example, **HttpIn**.</span></span>
   2. <span data-ttu-id="0feba-176">Выберите **TCP** для протокола hello.</span><span class="sxs-lookup"><span data-stu-id="0feba-176">Select **TCP** for hello protocol.</span></span>
   3. <span data-ttu-id="0feba-177">Укажите **80** hello открытого порта.</span><span class="sxs-lookup"><span data-stu-id="0feba-177">Specify **80** for hello public port.</span></span>
   4. <span data-ttu-id="0feba-178">Укажите **8080** для hello частный порт.</span><span class="sxs-lookup"><span data-stu-id="0feba-178">Specify **8080** for hello private port.</span></span>
   5. <span data-ttu-id="0feba-179">Выберите **отключено** для hello плавающей IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="0feba-179">Select **Disabled** for hello floating IP address.</span></span>
   6. <span data-ttu-id="0feba-180">Оставьте hello список управления доступом как есть.</span><span class="sxs-lookup"><span data-stu-id="0feba-180">Leave hello access control list as is.</span></span>
   7. <span data-ttu-id="0feba-181">Нажмите кнопку hello **ОК** кнопку hello tooclose-диалоговое окно и создать конечную точку hello.</span><span class="sxs-lookup"><span data-stu-id="0feba-181">Click hello **OK** button tooclose hello dialog box and create hello endpoint.</span></span>

## <a name="tooopen-a-port-in-hello-firewall-for-your-virtual-machine"></a><span data-ttu-id="0feba-182">tooopen порта в брандмауэре hello для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="0feba-182">tooopen a port in hello firewall for your virtual machine</span></span>
1. <span data-ttu-id="0feba-183">Войдите в tooyour виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0feba-183">Sign in tooyour virtual machine.</span></span>
2. <span data-ttu-id="0feba-184">Нажмите **кнопку "Пуск" в Windows**.</span><span class="sxs-lookup"><span data-stu-id="0feba-184">Click **Windows Start**.</span></span>
3. <span data-ttu-id="0feba-185">Нажмите **Панель управления**.</span><span class="sxs-lookup"><span data-stu-id="0feba-185">Click **Control Panel**.</span></span>
4. <span data-ttu-id="0feba-186">Щелкните **Система и безопасность**, **Брандмауэр Windows**, а затем — **Расширенные настройки**.</span><span class="sxs-lookup"><span data-stu-id="0feba-186">Click **System and Security**, click **Windows Firewall**, and then click **Advanced Settings**.</span></span>
5. <span data-ttu-id="0feba-187">Щелкните **Правила для входящих подключений**, а затем — **Создать правило**.</span><span class="sxs-lookup"><span data-stu-id="0feba-187">Click **Inbound Rules**, and then click **New Rule**.</span></span>  
   <span data-ttu-id="0feba-188">![Новое правило для входящего подключения][NewIBRule]</span><span class="sxs-lookup"><span data-stu-id="0feba-188">![New inbound rule][NewIBRule]</span></span>
6. <span data-ttu-id="0feba-189">Для hello **тип правила**выберите **порт**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0feba-189">For hello **Rule Type**, select **Port**, and then click **Next**.</span></span>  
   <span data-ttu-id="0feba-190">![Порт нового правила для входящего подключения][NewRulePort]</span><span class="sxs-lookup"><span data-stu-id="0feba-190">![New inbound rule port][NewRulePort]</span></span>
7. <span data-ttu-id="0feba-191">На hello **протокол и порты** выберите **TCP**, укажите **8080** как hello **определенный порт локального**и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0feba-191">On hello **Protocol and Ports** screen, select **TCP**, specify **8080** as hello **Specific local port**, and then click **Next**.</span></span>  
  <span data-ttu-id="0feba-192">![Новое правило для входящего подключения][NewRuleProtocol]</span><span class="sxs-lookup"><span data-stu-id="0feba-192">![New inbound rule ][NewRuleProtocol]</span></span>
8. <span data-ttu-id="0feba-193">На hello **действия** выберите **разрешить подключение hello**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0feba-193">On hello **Action** screen, select **Allow hello connection**, and then click **Next**.</span></span>
   <span data-ttu-id="0feba-194">![Действие нового правила для входящего подключения][NewRuleAction]</span><span class="sxs-lookup"><span data-stu-id="0feba-194">![New inbound rule action][NewRuleAction]</span></span>
9. <span data-ttu-id="0feba-195">На hello **профиль** экране, убедитесь, что **домена**, **закрытый**, и **открытый** выбраны и нажмите кнопку **Далее** .</span><span class="sxs-lookup"><span data-stu-id="0feba-195">On hello **Profile** screen, ensure that **Domain**, **Private**, and **Public** are selected, and then click **Next**.</span></span>
   <span data-ttu-id="0feba-196">![Профиль нового правила для входящего подключения][NewRuleProfile]</span><span class="sxs-lookup"><span data-stu-id="0feba-196">![New inbound rule profile][NewRuleProfile]</span></span>
10. <span data-ttu-id="0feba-197">На hello **имя** укажите имя для правила hello, таких как **HttpIn** (имя правила hello не имя конечной точки требуется toomatch hello, однако) и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="0feba-197">On hello **Name** screen, specify a name for hello rule, such as **HttpIn** (hello rule name is not required toomatch hello endpoint name, however), and then click **Finish**.</span></span>  
    <span data-ttu-id="0feba-198">![Имя нового правила для входящего подключения][NewRuleName]</span><span class="sxs-lookup"><span data-stu-id="0feba-198">![New inbound rule name][NewRuleName]</span></span>

<span data-ttu-id="0feba-199">С этого момента ваш веб-сайт Tomcat должен быть доступен для просмотра во внешнем браузере.</span><span class="sxs-lookup"><span data-stu-id="0feba-199">At this point, your Tomcat website should be viewable from an external browser.</span></span> <span data-ttu-id="0feba-200">В окне браузера hello адреса введите URL-адрес формы hello  **http://*вашей\_DNS\_имя*. cloudapp.net**, где ***вашей\_DNS\_имя*** hello DNS-именем, указанным при создании hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0feba-200">In hello browser's address window, type a URL of hello form **http://*your\_DNS\_name*.cloudapp.net**, where ***your\_DNS\_name*** is hello DNS name you specified when you created hello virtual machine.</span></span>

## <a name="application-lifecycle-considerations"></a><span data-ttu-id="0feba-201">Вопросы, связанные с жизненным циклом приложения</span><span class="sxs-lookup"><span data-stu-id="0feba-201">Application lifecycle considerations</span></span>
* <span data-ttu-id="0feba-202">Можно создать собственные веб-архива приложения (WAR) и добавьте его toohello **веб-приложений** папки.</span><span class="sxs-lookup"><span data-stu-id="0feba-202">You could create your own web application archive (WAR) and add it toohello **webapps** folder.</span></span> <span data-ttu-id="0feba-203">Например, создайте динамический веб-проект базовой страницы службы Java (JSP) и экспортируйте его как WAR-файл.</span><span class="sxs-lookup"><span data-stu-id="0feba-203">For example, create a basic Java Service Page (JSP) dynamic web project and export it as a WAR file.</span></span> <span data-ttu-id="0feba-204">Затем скопируйте toohello WAR hello Apache Tomcat **веб-приложений** папки на виртуальной машине hello, запустите его в браузере.</span><span class="sxs-lookup"><span data-stu-id="0feba-204">Next, copy hello WAR toohello Apache Tomcat **webapps** folder on hello virtual machine, then run it in a browser.</span></span>
* <span data-ttu-id="0feba-205">По умолчанию при установке службы Tomcat hello, он имеет значение toostart вручную.</span><span class="sxs-lookup"><span data-stu-id="0feba-205">By default when hello Tomcat service is installed, it is set toostart manually.</span></span> <span data-ttu-id="0feba-206">Можно переключить его toostart автоматически с помощью оснастки hello службы.</span><span class="sxs-lookup"><span data-stu-id="0feba-206">You can switch it toostart automatically by using hello Services snap-in.</span></span> <span data-ttu-id="0feba-207">Запустите оснастку hello службы, щелкнув **Пуск**, **Администрирование**, а затем **службы**.</span><span class="sxs-lookup"><span data-stu-id="0feba-207">Start hello Services snap-in by clicking **Windows Start**, **Administrative Tools**, and then **Services**.</span></span> <span data-ttu-id="0feba-208">Дважды щелкните hello **Apache Tomcat** и задайте для **тип запуска** слишком**автоматического**.</span><span class="sxs-lookup"><span data-stu-id="0feba-208">Double-click hello **Apache Tomcat** service and set **Startup type** too**Automatic**.</span></span>

    ![Параметр toostart службы автоматически][service_automatic_startup]

    <span data-ttu-id="0feba-210">Hello преимущество наличия Tomcat автоматический запуск — что он начинает работу во время перезагрузки hello виртуальной машины (например, после установки обновления программного обеспечения, которые требуют перезагрузки).</span><span class="sxs-lookup"><span data-stu-id="0feba-210">hello benefit of having Tomcat start automatically is that it starts running when hello virtual machine is rebooted (for example, after software updates that require a reboot are installed).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0feba-211">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0feba-211">Next steps</span></span>
<span data-ttu-id="0feba-212">Вы можете узнать о других служб (например, хранилище Azure, служебной шины и базы данных SQL), которые вы можете tooinclude с приложениями Java.</span><span class="sxs-lookup"><span data-stu-id="0feba-212">You can learn about other services (such as Azure Storage, service bus, and SQL Database) that you may want tooinclude with your Java applications.</span></span> <span data-ttu-id="0feba-213">Просмотреть hello сведений, доступных в hello [центра разработчиков Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="0feba-213">View hello information available at hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from hello "toocreate an ednpoint for your virtual mache" 3/17/2017,
     toouse hello new portal.
6. In hello **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In hello **New endpoint details** dialog box:
-->
