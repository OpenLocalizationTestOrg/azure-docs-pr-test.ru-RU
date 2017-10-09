---
title: "aaaSet копирование Apache Tomcat на виртуальной машине Linux | Документы Microsoft"
description: "Узнайте, как tooset копирование Apache Tomcat7 с помощью Azure виртуальных машин Linux."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 45ecc89c-1cb0-4e80-8944-bd0d0bbedfdc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: ningk
ms.openlocfilehash: b837a73e91fcb25d5459d993a0e93ceef1a1fc8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a><span data-ttu-id="86192-103">Настройка Tomcat7 на виртуальной машине Linux с использованием Azure</span><span class="sxs-lookup"><span data-stu-id="86192-103">Set up Tomcat7 on a Linux virtual machine with Azure</span></span>
<span data-ttu-id="86192-104">Apache Tomcat (или просто Tomcat, также называемая ранее Tomcat Джакарта) является открытым исходным кодом веб-сервера и контейнера сервлетов, разработанный hello Foundation программного обеспечения Apache ASF.</span><span class="sxs-lookup"><span data-stu-id="86192-104">Apache Tomcat (or simply Tomcat, also formerly called Jakarta Tomcat) is an open source web server and servlet container developed by hello Apache Software Foundation (ASF).</span></span> <span data-ttu-id="86192-105">Tomcat реализует hello сервлетов Java и спецификации JavaServer страниц (JSP) hello компании Sun Microsystems.</span><span class="sxs-lookup"><span data-stu-id="86192-105">Tomcat implements hello Java Servlet and hello JavaServer Pages (JSP) specifications from Sun Microsystems.</span></span> <span data-ttu-id="86192-106">Tomcat предоставляет чисто среде Java HTTP веб-сервера в какие toorun код Java.</span><span class="sxs-lookup"><span data-stu-id="86192-106">Tomcat provides a pure Java HTTP web server environment in which toorun Java code.</span></span> <span data-ttu-id="86192-107">В простейшую конфигурацию hello Tomcat выполняется в процессе одной операционной системы.</span><span class="sxs-lookup"><span data-stu-id="86192-107">In hello simplest configuration, Tomcat runs in a single operating system process.</span></span> <span data-ttu-id="86192-108">Этот процесс запускает виртуальную машину Java.</span><span class="sxs-lookup"><span data-stu-id="86192-108">This process runs a Java virtual machine (JVM).</span></span> <span data-ttu-id="86192-109">Каждый запрос HTTP tooTomcat браузера обрабатывается как отдельный поток в процессе Tomcat hello.</span><span class="sxs-lookup"><span data-stu-id="86192-109">Every HTTP request from a browser tooTomcat is processed as a separate thread in hello Tomcat process.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="86192-110">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="86192-110">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="86192-111">В этой статье рассказывается, как toouse hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="86192-111">This article covers how toouse hello classic deployment model.</span></span> <span data-ttu-id="86192-112">Корпорация Майкрософт рекомендует наиболее новые развертывания для использования модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="86192-112">We recommend that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="86192-113">toouse toodeploy шаблона диспетчера ресурсов Виртуальной машине Ubuntu с Open JDK и Tomcat, в разделе [в этой статье](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span><span class="sxs-lookup"><span data-stu-id="86192-113">toouse a Resource Manager template toodeploy an Ubuntu VM with Open JDK and Tomcat, see [this article](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span></span>

<span data-ttu-id="86192-114">В этой статье показано, как установить Tomcat7 в образе Linux и развернуть его в службе Azure.</span><span class="sxs-lookup"><span data-stu-id="86192-114">In this article, you will install Tomcat7 on a Linux image and deploy it in Azure.</span></span>  

<span data-ttu-id="86192-115">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="86192-115">You will learn:</span></span>  

* <span data-ttu-id="86192-116">Как toocreate виртуальную машину в Azure.</span><span class="sxs-lookup"><span data-stu-id="86192-116">How toocreate a virtual machine in Azure.</span></span>
* <span data-ttu-id="86192-117">Как tooprepare hello виртуальной машины для Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="86192-117">How tooprepare hello virtual machine for Tomcat7.</span></span>
* <span data-ttu-id="86192-118">Как tooinstall Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="86192-118">How tooinstall Tomcat7.</span></span>

<span data-ttu-id="86192-119">Предполагается, что у вас уже есть подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="86192-119">It is assumed that you already have an Azure subscription.</span></span>  <span data-ttu-id="86192-120">Если нет, можно зарегистрироваться для получения бесплатной пробной версии на [hello веб-сайте Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="86192-120">If not, you can sign up for a free trial at [hello Azure website](https://azure.microsoft.com/).</span></span> <span data-ttu-id="86192-121">Если у вас есть подписка MSDN, сведения о специальных ценах Microsoft Azure на MSDN, MPN и Bizspark см. на [этой странице](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span><span class="sxs-lookup"><span data-stu-id="86192-121">If you have an MSDN subscription, see [Microsoft Azure Special Pricing: MSDN, MPN, and BizSpark Benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span></span> <span data-ttu-id="86192-122">toolearn Дополнительные сведения о Azure, в разделе [что такое Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span><span class="sxs-lookup"><span data-stu-id="86192-122">toolearn more about Azure, see [What is Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span></span>

<span data-ttu-id="86192-123">В этой статье предполагается, что вы располагаете достаточными знаниями по работе с Tomcat и Linux.</span><span class="sxs-lookup"><span data-stu-id="86192-123">This article assumes that you have a basic working knowledge of Tomcat and Linux.</span></span>  

## <a name="phase-1-create-an-image"></a><span data-ttu-id="86192-124">Этап 1. Создание образа</span><span class="sxs-lookup"><span data-stu-id="86192-124">Phase 1: Create an image</span></span>
<span data-ttu-id="86192-125">На этом этапе вы создадите виртуальную машину с помощью образа Linux в Azure.</span><span class="sxs-lookup"><span data-stu-id="86192-125">In this phase, you will create a virtual machine by using a Linux image in Azure.</span></span>  

### <a name="step-1-generate-an-ssh-authentication-key"></a><span data-ttu-id="86192-126">Шаг 1. Создание ключа проверки подлинности SSH</span><span class="sxs-lookup"><span data-stu-id="86192-126">Step 1: Generate an SSH authentication key</span></span>
<span data-ttu-id="86192-127">SSH — это важный инструмент для системных администраторов.</span><span class="sxs-lookup"><span data-stu-id="86192-127">SSH is an important tool for system administrators.</span></span> <span data-ttu-id="86192-128">Однако для настройки безопасности доступа не рекомендуется использовать пароль, определенный пользователем.</span><span class="sxs-lookup"><span data-stu-id="86192-128">However, configuring access security based on a human-determined password is not recommended.</span></span> <span data-ttu-id="86192-129">Злоумышленники могут взломать ненадежный пароль и проникнуть в вашу систему, использовав имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="86192-129">Malicious users can break into your system based on a username and a weak password.</span></span>

<span data-ttu-id="86192-130">хорошие новости Hello является способом tooleave удаленного доступа откройте и не беспокоиться о пароли.</span><span class="sxs-lookup"><span data-stu-id="86192-130">hello good news is that there is a way tooleave remote access open and not worry about passwords.</span></span> <span data-ttu-id="86192-131">Этот метод состоит в проверке подлинности с асимметричным шифрованием.</span><span class="sxs-lookup"><span data-stu-id="86192-131">This method consists of authentication with asymmetric cryptography.</span></span> <span data-ttu-id="86192-132">Hello закрытого ключа пользователя — hello, который предоставляет hello проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="86192-132">hello user’s private key is hello one that grants hello authentication.</span></span> <span data-ttu-id="86192-133">Можно даже заблокировать учетную запись пользователя hello toonot разрешить проверку подлинности пароль.</span><span class="sxs-lookup"><span data-stu-id="86192-133">You can even lock hello user’s account toonot allow password authentication.</span></span>

<span data-ttu-id="86192-134">Еще одним преимуществом использования этого метода является toosign разные пароли в toodifferent серверов не требуется.</span><span class="sxs-lookup"><span data-stu-id="86192-134">Another advantage of this method is that you do not need different passwords toosign in toodifferent servers.</span></span> <span data-ttu-id="86192-135">Вы можете проверять подлинность с помощью hello личных закрытый ключ на всех серверах, что позволяет избежать tooremember несколько паролей.</span><span class="sxs-lookup"><span data-stu-id="86192-135">You can authenticate by using hello personal private key on all servers, which prevents you from having tooremember several passwords.</span></span>



<span data-ttu-id="86192-136">Выполните эти шаги ключ toogenerate hello SSH проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="86192-136">Follow these steps toogenerate hello SSH authentication key.</span></span>

1. <span data-ttu-id="86192-137">Загрузите и установите PuTTYgen hello следующие расположения: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="86192-137">Download and install PuTTYgen from hello following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="86192-138">Запустите Puttygen.exe.</span><span class="sxs-lookup"><span data-stu-id="86192-138">Run Puttygen.exe.</span></span>
3. <span data-ttu-id="86192-139">Нажмите кнопку **формирования** toogenerate hello ключей.</span><span class="sxs-lookup"><span data-stu-id="86192-139">Click **Generate** toogenerate hello keys.</span></span> <span data-ttu-id="86192-140">В процессе hello можно увеличить случайности, движения мыши hello на пустую область hello в окне приветствия.</span><span class="sxs-lookup"><span data-stu-id="86192-140">In hello process, you can increase randomness by moving hello mouse over hello blank area in hello window.</span></span>  
   <span data-ttu-id="86192-141">![Кнопка нового ключа создания puTTY генератор ключа снимок экрана, показывающий hello][1]</span><span class="sxs-lookup"><span data-stu-id="86192-141">![PuTTY Key Generator screenshot that shows hello generate new key button][1]</span></span>
4. <span data-ttu-id="86192-142">После hello создать процесс, Puttygen.exe покажет нового открытого ключа.</span><span class="sxs-lookup"><span data-stu-id="86192-142">After hello generate process, Puttygen.exe will show your new public key.</span></span>  
   ![PuTTY генератор ключа снимок экрана, показывающий новый открытый ключ hello "и" hello "Сохранить" закрытого ключа][2]
5. <span data-ttu-id="86192-144">Выберите и скопируйте hello открытый ключ и сохранить его в файл с именем publicKey.pem.</span><span class="sxs-lookup"><span data-stu-id="86192-144">Select and copy hello public key, and save it in a file named publicKey.pem.</span></span> <span data-ttu-id="86192-145">Не щелкайте **сохранить открытый ключ**, так как hello сохраненного формата файла открытого ключа, отличается от hello открытый ключ, нам нужно.</span><span class="sxs-lookup"><span data-stu-id="86192-145">Don’t click **Save public key**, because hello saved public key’s file format is different from hello public key we want.</span></span>
6. <span data-ttu-id="86192-146">Нажмите кнопку **Save private key** (Сохранить закрытый ключ) и сохраните его в файл с именем privateKey.ppk.</span><span class="sxs-lookup"><span data-stu-id="86192-146">Click **Save private key**, and save it in a file named privateKey.ppk.</span></span>

### <a name="step-2-create-hello-image-in-hello-azure-portal"></a><span data-ttu-id="86192-147">Шаг 2: Создание образа hello в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="86192-147">Step 2: Create hello image in hello Azure portal</span></span>
1. <span data-ttu-id="86192-148">В hello [портала](https://portal.azure.com/), нажмите кнопку **New** в hello задач панели toocreate изображения.</span><span class="sxs-lookup"><span data-stu-id="86192-148">In hello [portal](https://portal.azure.com/), click **New** in hello task bar toocreate an image.</span></span> <span data-ttu-id="86192-149">Выберите образ hello Linux, в зависимости от потребностей.</span><span class="sxs-lookup"><span data-stu-id="86192-149">Then choose hello Linux image that is based on your needs.</span></span> <span data-ttu-id="86192-150">Hello следующем примере hello Ubuntu 14.04 изображения.</span><span class="sxs-lookup"><span data-stu-id="86192-150">hello following example uses hello Ubuntu 14.04 image.</span></span>
<span data-ttu-id="86192-151">![Снимок экрана: hello портал, который показывает hello новая кнопка][3]</span><span class="sxs-lookup"><span data-stu-id="86192-151">![Screenshot of hello portal that shows hello New button][3]</span></span>

2. <span data-ttu-id="86192-152">Для **имя узла**, укажите имя hello hello URL-адрес, Интернет-клиенты будут использовать и tooaccess этой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="86192-152">For **Host Name**, specify hello name for hello URL that you and Internet clients will use tooaccess this virtual machine.</span></span> <span data-ttu-id="86192-153">Определите последнюю часть hello DNS-имя, например, tomcatdemo hello.</span><span class="sxs-lookup"><span data-stu-id="86192-153">Define hello last part of hello DNS name, for example, tomcatdemo.</span></span> <span data-ttu-id="86192-154">Azure затем создаст hello URL-адрес, что tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="86192-154">Azure will then generate hello URL as tomcatdemo.cloudapp.net.</span></span>  

3. <span data-ttu-id="86192-155">Для **ключ SSH проверки подлинности**, скопируйте значение ключа hello из hello publicKey.pem файл, содержащий открытый ключ hello созданные PuTTYgen.</span><span class="sxs-lookup"><span data-stu-id="86192-155">For **SSH Authentication Key**, copy hello key value from hello publicKey.pem file, which contains hello public key generated by PuTTYgen.</span></span>  
<span data-ttu-id="86192-156">![Введите ключ проверки подлинности SSH в портале hello][4]</span><span class="sxs-lookup"><span data-stu-id="86192-156">![SSH Authentication Key box in hello portal][4]</span></span>

4. <span data-ttu-id="86192-157">При необходимости настройте другие параметры и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="86192-157">Configure other settings as needed, and then click **Create**.</span></span>  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a><span data-ttu-id="86192-158">Этап 2. Подготовка виртуальной машины для Tomcat7</span><span class="sxs-lookup"><span data-stu-id="86192-158">Phase 2: Prepare your virtual machine for Tomcat7</span></span>
<span data-ttu-id="86192-159">На этом этапе будет настроить конечную точку для трафика Tomcat и подключитесь tooyour новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="86192-159">In this phase, you will configure an endpoint for Tomcat traffic, and then connect tooyour new virtual machine.</span></span>

### <a name="step-1-open-hello-http-port-tooallow-web-access"></a><span data-ttu-id="86192-160">Шаг 1: Откройте hello HTTP порт tooallow web access</span><span class="sxs-lookup"><span data-stu-id="86192-160">Step 1: Open hello HTTP port tooallow web access</span></span>
<span data-ttu-id="86192-161">Конечные точки в Azure состоят из протокола (TCP или UDP), а также общего и частного порта.</span><span class="sxs-lookup"><span data-stu-id="86192-161">Endpoints in Azure consist of a TCP or UDP protocol, along with a public and private port.</span></span> <span data-ttu-id="86192-162">частный порт Hello — порт hello, что hello служба ожидает tooon hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="86192-162">hello private port is hello port that hello service is listening tooon hello virtual machine.</span></span> <span data-ttu-id="86192-163">Общий порт Hello — tooexternally для входящего трафика на Интернет-прослушивает порт hello, hello Azure облачной службы.</span><span class="sxs-lookup"><span data-stu-id="86192-163">hello public port is hello port that hello Azure cloud service listens tooexternally for incoming, Internet-based traffic.</span></span>  

<span data-ttu-id="86192-164">TCP-порт 8080 — номер порта по умолчанию hello, что Tomcat использует toolisten.</span><span class="sxs-lookup"><span data-stu-id="86192-164">TCP port 8080 is hello default port number that Tomcat uses toolisten.</span></span> <span data-ttu-id="86192-165">Открытие этого порта с помощью конечной точки Azure обеспечивает вам и другим интернет-клиентам доступ к страницам Tomcat.</span><span class="sxs-lookup"><span data-stu-id="86192-165">If this port is opened with an Azure endpoint, you and other Internet clients can access Tomcat pages.</span></span>  

1. <span data-ttu-id="86192-166">На портале hello щелкните **Обзор** > **виртуальные машины**и нажмите кнопку hello виртуальную машину, созданную.</span><span class="sxs-lookup"><span data-stu-id="86192-166">In hello portal, click **Browse** > **Virtual machines**, and then click hello virtual machine that you created.</span></span>  
   <span data-ttu-id="86192-167">![Снимок экрана: hello каталог виртуальные машины][5]</span><span class="sxs-lookup"><span data-stu-id="86192-167">![Screenshot of hello Virtual machines directory][5]</span></span>
2. <span data-ttu-id="86192-168">tooadd конечная точка tooyour виртуальной машине, щелкните hello **конечные точки** поле.</span><span class="sxs-lookup"><span data-stu-id="86192-168">tooadd an endpoint tooyour virtual machine, click hello **Endpoints** box.</span></span>
   <span data-ttu-id="86192-169">![Снимок экрана, показывающий поля hello конечных точек][6]</span><span class="sxs-lookup"><span data-stu-id="86192-169">![Screenshot that shows hello Endpoints box][6]</span></span>
3. <span data-ttu-id="86192-170">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="86192-170">Click **Add**.</span></span>  

   1. <span data-ttu-id="86192-171">Для конечной точки hello, введите имя для конечной точки hello в **конечной точки**, а затем введите 80 в **общий порт**.</span><span class="sxs-lookup"><span data-stu-id="86192-171">For hello endpoint, enter a name for hello endpoint in **Endpoint**, and then enter 80 in **Public Port**.</span></span>  

      <span data-ttu-id="86192-172">Если задано too80, нет необходимости номер порта tooinclude hello в hello URL-адрес, используемый tooaccess Tomcat.</span><span class="sxs-lookup"><span data-stu-id="86192-172">If you set it too80, you don’t need tooinclude hello port number in hello URL that is used tooaccess Tomcat.</span></span> <span data-ttu-id="86192-173">Например, http://tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="86192-173">For example, http://tomcatdemo.cloudapp.net.</span></span>    

      <span data-ttu-id="86192-174">Если задать значение tooanother, например 81, необходимо tooadd hello порт номер toohello URL-адрес tooaccess Tomcat.</span><span class="sxs-lookup"><span data-stu-id="86192-174">If you set it tooanother value, such as 81, you need tooadd hello port number toohello URL tooaccess Tomcat.</span></span> <span data-ttu-id="86192-175">Например, http://tomcatdemo.cloudapp.net:81/.</span><span class="sxs-lookup"><span data-stu-id="86192-175">For example,  http://tomcatdemo.cloudapp.net:81/.</span></span>
   2. <span data-ttu-id="86192-176">Введите 8080 в поле **Частный порт**.</span><span class="sxs-lookup"><span data-stu-id="86192-176">Enter 8080 in **Private Port**.</span></span> <span data-ttu-id="86192-177">По умолчанию Tomcat прослушивает TCP-порт 8080.</span><span class="sxs-lookup"><span data-stu-id="86192-177">By default, Tomcat listens on TCP port 8080.</span></span> <span data-ttu-id="86192-178">Если вы изменили hello по умолчанию прослушивания порта Tomcat, необходимо обновить **частный порт** toobe hello так же, как hello порт прослушивания Tomcat.</span><span class="sxs-lookup"><span data-stu-id="86192-178">If you changed hello default listen port of Tomcat, you should update **Private Port** toobe hello same as hello Tomcat listen port.</span></span>  
      <span data-ttu-id="86192-179">![Снимок экрана пользовательского интерфейса, где отображается команда "Добавить" и поля "Общий порт" и "Частный порт"][7]</span><span class="sxs-lookup"><span data-stu-id="86192-179">![Screenshot of UI that shows Add command, Public Port, and Private Port][7]</span></span>
4. <span data-ttu-id="86192-180">Нажмите кнопку **ОК** tooadd hello конечной точки tooyour виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="86192-180">Click **OK** tooadd hello endpoint tooyour virtual machine.</span></span>

### <a name="step-2-connect-toohello-image-you-created"></a><span data-ttu-id="86192-181">Шаг 2: Подключение toohello образ, созданный</span><span class="sxs-lookup"><span data-stu-id="86192-181">Step 2: Connect toohello image you created</span></span>
<span data-ttu-id="86192-182">Можно выбрать любой SSH средство tooconnect tooyour виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="86192-182">You can choose any SSH tool tooconnect tooyour virtual machine.</span></span> <span data-ttu-id="86192-183">В этом примере мы используем средство PuTTY.</span><span class="sxs-lookup"><span data-stu-id="86192-183">In this example, we use PuTTY.</span></span>  

1. <span data-ttu-id="86192-184">Получите hello DNS-имя виртуальной машины из портала hello.</span><span class="sxs-lookup"><span data-stu-id="86192-184">Get hello DNS name of your virtual machine from hello portal.</span></span>
    1. <span data-ttu-id="86192-185">Щелкните **Обзор** > **Виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="86192-185">Click **Browse** > **Virtual machines**.</span></span>
    2. <span data-ttu-id="86192-186">Выберите имя hello виртуальной машины и нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="86192-186">Select hello name of your virtual machine, and then click **Properties**.</span></span>
    3. <span data-ttu-id="86192-187">В hello **свойства** плитки, поиск в hello **доменное имя** поле tooget hello DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="86192-187">In hello **Properties** tile, look in hello **Domain Name** box tooget hello DNS name.</span></span>  

2. <span data-ttu-id="86192-188">Получить номер порта hello для соединений по протоколу SSH с hello **SSH** поле.</span><span class="sxs-lookup"><span data-stu-id="86192-188">Get hello port number for SSH connections from hello **SSH** box.</span></span>  
<span data-ttu-id="86192-189">![Снимок экрана, показывающий номер порта для подключения SSH hello][8]</span><span class="sxs-lookup"><span data-stu-id="86192-189">![Screenshot that shows hello SSH connection port number][8]</span></span>

3. <span data-ttu-id="86192-190">Скачайте [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="86192-190">Download [PuTTY](http://www.putty.org/).</span></span>  

4. <span data-ttu-id="86192-191">После загрузки запустите исполняемый файл hello Putty.exe.</span><span class="sxs-lookup"><span data-stu-id="86192-191">After downloading, click hello executable file Putty.exe.</span></span> <span data-ttu-id="86192-192">В PuTTY конфигурации настроить основные параметры hello hello имя узла и порта номер, полученный из свойства hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="86192-192">In PuTTY configuration, configure hello basic options with hello host name and port number that is obtained from hello properties of your virtual machine.</span></span>   
![Снимок экрана, показывающий параметры имя и порт hello PuTTY конфигурации узла][9]

5. <span data-ttu-id="86192-194">Hello левой панели щелкните **подключения** > **SSH** > **Auth**, а затем нажмите кнопку **Обзор** toospecify расположение файла privateKey.ppk hello Hello.</span><span class="sxs-lookup"><span data-stu-id="86192-194">In hello left pane, click **Connection** > **SSH** > **Auth**, and then click **Browse** toospecify hello location of hello privateKey.ppk file.</span></span> <span data-ttu-id="86192-195">файл privateKey.ppk Hello содержит hello закрытый ключ, созданный ранее в hello PuTTYgen «этап 1: Создание образа» этой статьи.</span><span class="sxs-lookup"><span data-stu-id="86192-195">hello privateKey.ppk file contains hello private key that is generated by PuTTYgen earlier in hello "Phase 1: Create an image" section of this article.</span></span>  
<span data-ttu-id="86192-196">![Снимок экрана, показывающий иерархии каталогов подключения hello и кнопку обзора][10]</span><span class="sxs-lookup"><span data-stu-id="86192-196">![Screenshot that shows hello Connection directory hierarchy and Browse button][10]</span></span>

6. <span data-ttu-id="86192-197">Щелкните **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="86192-197">Click **Open**.</span></span> <span data-ttu-id="86192-198">Может отобразиться оповещение в окне сообщения.</span><span class="sxs-lookup"><span data-stu-id="86192-198">You might be alerted by a message box.</span></span> <span data-ttu-id="86192-199">Если вы настроили hello DNS-имя и номер порта правильно, нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="86192-199">If you have configured hello DNS name and port number correctly, click **Yes**.</span></span>
<span data-ttu-id="86192-200">![Снимок экрана, показывающий hello уведомления][11]</span><span class="sxs-lookup"><span data-stu-id="86192-200">![Screenshot that shows hello notification][11]</span></span>

7. <span data-ttu-id="86192-201">Вы являются запрашиваемые tooenter свое имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="86192-201">You are prompted tooenter your username.</span></span>  
![Снимок экрана, показывающий, где имя пользователя tooenter][12]

8. <span data-ttu-id="86192-203">Введите имя пользователя hello, которое вы использовали toocreate hello виртуальной машины в hello «этап 1: Создание образа» ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="86192-203">Enter hello username that you used toocreate hello virtual machine in hello "Phase 1: Create an image" section earlier in this article.</span></span> <span data-ttu-id="86192-204">Вы увидите примерно hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="86192-204">You will see something like hello following:</span></span>  
![Снимок экрана, показывающий подтверждения подлинности hello][13]

## <a name="phase-3-install-software"></a><span data-ttu-id="86192-206">Этап 3. Установка программного обеспечения</span><span class="sxs-lookup"><span data-stu-id="86192-206">Phase 3: Install software</span></span>
<span data-ttu-id="86192-207">На этом этапе установки среды выполнения Java hello, Tomcat7 и других компонентов Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="86192-207">In this phase, you install hello Java runtime environment, Tomcat7, and other Tomcat7 components.</span></span>  

### <a name="java-runtime-environment"></a><span data-ttu-id="86192-208">Среда выполнения Java</span><span class="sxs-lookup"><span data-stu-id="86192-208">Java runtime environment</span></span>
<span data-ttu-id="86192-209">Программное обеспечение Tomcat написано на языке Java.</span><span class="sxs-lookup"><span data-stu-id="86192-209">Tomcat is written in Java.</span></span> <span data-ttu-id="86192-210">Есть два вида комплектов Java Development Kit (JDK) — OpenJDK и Oracle JDK.</span><span class="sxs-lookup"><span data-stu-id="86192-210">There are two kinds of Java Development Kits (JDKs), OpenJDK and Oracle JDK.</span></span> <span data-ttu-id="86192-211">Можно выбрать необходимый hello.</span><span class="sxs-lookup"><span data-stu-id="86192-211">You can choose hello one you want.</span></span>  

> [!NOTE]
> <span data-ttu-id="86192-212">Оба пакетов JDK имеют практически hello же код для классов hello в hello Java API, но код hello для hello виртуальной машины отличается.</span><span class="sxs-lookup"><span data-stu-id="86192-212">Both JDKs have almost hello same code for hello classes in hello Java API, but hello code for hello virtual machine is different.</span></span> <span data-ttu-id="86192-213">OpenJDK, как правило, открытые библиотеки toouse, пока Oracle JDK, как правило, toouse закрыто историй.</span><span class="sxs-lookup"><span data-stu-id="86192-213">OpenJDK tends toouse open libraries, while Oracle JDK tends toouse closed ones.</span></span> <span data-ttu-id="86192-214">В Oracle JDK доступно больше классов и в нем исправлены некоторые ошибки. К тому же Oracle JDK работает стабильнее, чем OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="86192-214">Oracle JDK has more classes and some fixed bugs, and Oracle JDK is more stable than OpenJDK.</span></span>

#### <a name="install-openjdk"></a><span data-ttu-id="86192-215">Установка OpenJDK</span><span class="sxs-lookup"><span data-stu-id="86192-215">Install OpenJDK</span></span>  

<span data-ttu-id="86192-216">Используйте следующие команды toodownload OpenJDK hello.</span><span class="sxs-lookup"><span data-stu-id="86192-216">Use hello following command toodownload OpenJDK.</span></span>   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* <span data-ttu-id="86192-217">toocreate directory toocontain hello JDK файлов:</span><span class="sxs-lookup"><span data-stu-id="86192-217">toocreate a directory toocontain hello JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="86192-218">файлы JDK tooextract hello в hello/usr/lib/виртуальной машины Java/directory:</span><span class="sxs-lookup"><span data-stu-id="86192-218">tooextract hello JDK files into hello /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a><span data-ttu-id="86192-219">Установка Oracle JDK</span><span class="sxs-lookup"><span data-stu-id="86192-219">Install Oracle JDK</span></span>


<span data-ttu-id="86192-220">Используйте следующую команду toodownload Oracle JDK из веб-сайте Oracle hello hello.</span><span class="sxs-lookup"><span data-stu-id="86192-220">Use hello following command toodownload Oracle JDK from hello Oracle website.</span></span>  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* <span data-ttu-id="86192-221">toocreate directory toocontain hello JDK файлов:</span><span class="sxs-lookup"><span data-stu-id="86192-221">toocreate a directory toocontain hello JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="86192-222">файлы JDK tooextract hello в hello/usr/lib/виртуальной машины Java/directory:</span><span class="sxs-lookup"><span data-stu-id="86192-222">tooextract hello JDK files into hello /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* <span data-ttu-id="86192-223">tooset JDK Oracle как hello виртуальной машины Java по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="86192-223">tooset Oracle JDK as hello default Java virtual machine:</span></span>  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a><span data-ttu-id="86192-224">Убедитесь, что установка Java выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="86192-224">Confirm that Java installation is successful</span></span>
<span data-ttu-id="86192-225">Можно использовать такую команду hello следующие tootest, если среда выполнения Java hello установлена правильно:</span><span class="sxs-lookup"><span data-stu-id="86192-225">You can use a command like hello following tootest if hello Java runtime environment is installed correctly:</span></span>  

    java -version  

<span data-ttu-id="86192-226">Если вы установили OpenJDK, вы увидите сообщение hello следующим образом: ![сообщения OpenJDK успешной установки][14]</span><span class="sxs-lookup"><span data-stu-id="86192-226">If you installed OpenJDK, you should see a message like hello following: ![Successful OpenJDK installation message][14]</span></span>

<span data-ttu-id="86192-227">Если вы установили Oracle JDK, вы увидите сообщение hello следующим образом: ![сообщения установки успешно JDK Oracle][15]</span><span class="sxs-lookup"><span data-stu-id="86192-227">If you installed Oracle JDK, you should see a message like hello following: ![Successful Oracle JDK installation message][15]</span></span>

### <a name="install-tomcat7"></a><span data-ttu-id="86192-228">Установка Tomcat7</span><span class="sxs-lookup"><span data-stu-id="86192-228">Install Tomcat7</span></span>
<span data-ttu-id="86192-229">Используйте следующие команды tooinstall Tomcat7 hello.</span><span class="sxs-lookup"><span data-stu-id="86192-229">Use hello following command tooinstall Tomcat7.</span></span>  

    sudo apt-get install tomcat7  

<span data-ttu-id="86192-230">Если вы не используете Tomcat7, используйте аналогичную hello этой команды.</span><span class="sxs-lookup"><span data-stu-id="86192-230">If you are not using Tomcat7, use hello appropriate variation of this command.</span></span>  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a><span data-ttu-id="86192-231">Убедитесь, что Tomcat7 успешно установлен.</span><span class="sxs-lookup"><span data-stu-id="86192-231">Confirm that Tomcat7 installation is successful</span></span>
<span data-ttu-id="86192-232">toocheck после успешной установки Tomcat7 Обзор сервера Tomcat tooyour DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="86192-232">toocheck if Tomcat7 is successfully installed, browse tooyour Tomcat server’s DNS name.</span></span> <span data-ttu-id="86192-233">В этой статье пример hello URL-адреса — http://tomcatexample.cloudapp.net/.</span><span class="sxs-lookup"><span data-stu-id="86192-233">In this article, hello example URL is http://tomcatexample.cloudapp.net/.</span></span> <span data-ttu-id="86192-234">Если появится сообщение следующего вида hello, Tomcat7 установлена правильно.</span><span class="sxs-lookup"><span data-stu-id="86192-234">If you see a message like hello following, Tomcat7 is installed correctly.</span></span>
<span data-ttu-id="86192-235">![Сообщение об успешной установке Tomcat7][16]</span><span class="sxs-lookup"><span data-stu-id="86192-235">![Successful Tomcat7 installation message][16]</span></span>

### <a name="install-other-tomcat7-components"></a><span data-ttu-id="86192-236">Установка других компонентов Tomcat7</span><span class="sxs-lookup"><span data-stu-id="86192-236">Install other Tomcat7 components</span></span>
<span data-ttu-id="86192-237">Существуют другие дополнительные компоненты Tomcat, которые вы можете установить.</span><span class="sxs-lookup"><span data-stu-id="86192-237">There are other optional Tomcat components that you can install.</span></span>  

<span data-ttu-id="86192-238">Используйте hello **tomcat7 поиска apt кэша sudo** команда toosee все доступные компоненты hello.</span><span class="sxs-lookup"><span data-stu-id="86192-238">Use hello **sudo apt-cache search tomcat7** command toosee all of hello available components.</span></span> <span data-ttu-id="86192-239">Используйте следующие команды tooinstall hello некоторые полезные компоненты.</span><span class="sxs-lookup"><span data-stu-id="86192-239">Use hello following commands tooinstall some useful components.</span></span>  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools toocreate user instances  

## <a name="phase-4-configure-tomcat7"></a><span data-ttu-id="86192-240">Этап 4. Настройка Tomcat7</span><span class="sxs-lookup"><span data-stu-id="86192-240">Phase 4: Configure Tomcat7</span></span>
<span data-ttu-id="86192-241">На этом этапе вы узнаете о том, как управлять Tomcat.</span><span class="sxs-lookup"><span data-stu-id="86192-241">In this phase, you administer Tomcat.</span></span>

### <a name="start-and-stop-tomcat7"></a><span data-ttu-id="86192-242">Запуск и остановка Tomcat7</span><span class="sxs-lookup"><span data-stu-id="86192-242">Start and stop Tomcat7</span></span>
<span data-ttu-id="86192-243">сервер Tomcat7 Hello запускается автоматически при установке.</span><span class="sxs-lookup"><span data-stu-id="86192-243">hello Tomcat7 server automatically starts when you install it.</span></span> <span data-ttu-id="86192-244">Можно также запустить с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="86192-244">You can also start it with hello following command:</span></span>   

    sudo /etc/init.d/tomcat7 start

<span data-ttu-id="86192-245">toostop Tomcat7:</span><span class="sxs-lookup"><span data-stu-id="86192-245">toostop Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 stop

<span data-ttu-id="86192-246">состояние hello tooview Tomcat7:</span><span class="sxs-lookup"><span data-stu-id="86192-246">tooview hello status of Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 status

<span data-ttu-id="86192-247">службы toorestart Tomcat:</span><span class="sxs-lookup"><span data-stu-id="86192-247">toorestart Tomcat services:</span></span> 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a><span data-ttu-id="86192-248">Администрирование Tomcat7</span><span class="sxs-lookup"><span data-stu-id="86192-248">Tomcat7 administration</span></span>
<span data-ttu-id="86192-249">Можно изменить файл конфигурации tooset для hello Tomcat пользователя копирование свои учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="86192-249">You can edit hello Tomcat user configuration file tooset up your admin credentials.</span></span> <span data-ttu-id="86192-250">Hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="86192-250">Use hello following command:</span></span>  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

<span data-ttu-id="86192-251">Пример:</span><span class="sxs-lookup"><span data-stu-id="86192-251">Here is an example:</span></span>  
![Снимок экрана, показывающий выходные данные команды vi sudo hello][17]  

> [!NOTE]
> <span data-ttu-id="86192-253">Создайте надежный пароль для пользователя с правами администратора hello.</span><span class="sxs-lookup"><span data-stu-id="86192-253">Create a strong password for hello admin username.</span></span>  

<span data-ttu-id="86192-254">После изменения этого файла, следует перезапустить службы Tomcat7 с hello, следующая команда tooensure, что hello изменения вступили в силу:</span><span class="sxs-lookup"><span data-stu-id="86192-254">After editing this file, you should restart Tomcat7 services with hello following command tooensure that hello changes take effect:</span></span>  

    sudo /etc/init.d/tomcat7 restart  

<span data-ttu-id="86192-255">Откройте браузер и введите **http://<your tomcat server DNS name>html-manager/** как hello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="86192-255">Open your browser, and enter **http://<your tomcat server DNS name>/manager/html** as hello URL.</span></span> <span data-ttu-id="86192-256">Например hello в этой статье hello URL-адрес является http://tomcatexample.cloudapp.net/manager/html.</span><span class="sxs-lookup"><span data-stu-id="86192-256">For hello example in this article, hello URL is http://tomcatexample.cloudapp.net/manager/html.</span></span>  

<span data-ttu-id="86192-257">После подключения вы увидите нечто похожее toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="86192-257">After connecting, you should see something similar toohello following:</span></span>  
![Снимок экрана: hello Диспетчер приложений Tomcat Web][18]

## <a name="common-issues"></a><span data-ttu-id="86192-259">Распространенные проблемы</span><span class="sxs-lookup"><span data-stu-id="86192-259">Common issues</span></span>
### <a name="cant-access-hello-virtual-machine-with-tomcat-and-moodle-from-hello-internet"></a><span data-ttu-id="86192-260">Hello виртуальную машину с Tomcat и Moodle нельзя получить доступ из Интернета hello</span><span class="sxs-lookup"><span data-stu-id="86192-260">Can't access hello virtual machine with Tomcat and Moodle from hello Internet</span></span>
#### <a name="symptom"></a><span data-ttu-id="86192-261">Симптом</span><span class="sxs-lookup"><span data-stu-id="86192-261">Symptom</span></span>  
  <span data-ttu-id="86192-262">Tomcat выполняется, но не отображается страница по умолчанию hello Tomcat с браузером.</span><span class="sxs-lookup"><span data-stu-id="86192-262">Tomcat is running but you can’t see hello Tomcat default page with your browser.</span></span>
#### <a name="possible-root-cause"></a><span data-ttu-id="86192-263">Возможная основная причина</span><span class="sxs-lookup"><span data-stu-id="86192-263">Possible root cause</span></span>   

  * <span data-ttu-id="86192-264">порт прослушивания Tomcat Hello не является hello аналогично hello частный порт конечной точки виртуальной машины для трафика Tomcat.</span><span class="sxs-lookup"><span data-stu-id="86192-264">hello Tomcat listen port is not hello same as hello private port of your virtual machine's endpoint for Tomcat traffic.</span></span>  

     <span data-ttu-id="86192-265">Порт прослушивания проверьте общий порт и частного порта параметры конечной точки и убедитесь, частный порт hello Здравствуйте, так же, как hello Tomcat.</span><span class="sxs-lookup"><span data-stu-id="86192-265">Check your public port and private port endpoint settings and make sure hello private port is hello same as hello Tomcat listen port.</span></span> <span data-ttu-id="86192-266">Дополнительные инструкции по настройке конечных точек см. в разделе "Этап 1. Создание образа" этой статьи.</span><span class="sxs-lookup"><span data-stu-id="86192-266">See "Phase 1: Create an image" section of this article for instructions on configuring endpoints for your virtual machine.</span></span>  

     <span data-ttu-id="86192-267">toodetermine hello Tomcat порт прослушивания, откройте /etc/httpd/conf/httpd.conf (Red Hat выпуск) или /etc/tomcat7/server.xml (Debian выпуск).</span><span class="sxs-lookup"><span data-stu-id="86192-267">toodetermine hello Tomcat listen port, open /etc/httpd/conf/httpd.conf (Red Hat release), or /etc/tomcat7/server.xml (Debian release).</span></span> <span data-ttu-id="86192-268">По умолчанию hello порт прослушивания Tomcat — 8080.</span><span class="sxs-lookup"><span data-stu-id="86192-268">By default, hello Tomcat listen port is 8080.</span></span> <span data-ttu-id="86192-269">Пример:</span><span class="sxs-lookup"><span data-stu-id="86192-269">Here is an example:</span></span>  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     <span data-ttu-id="86192-270">При использовании виртуальной машины, как Debian и Ubuntu и вы хотите toochange hello по умолчанию порт из Tomcat ожидания передачи данных (например 8081), также следует открыть порт hello для hello операционной системы.</span><span class="sxs-lookup"><span data-stu-id="86192-270">If you are using a virtual machine like Debian or Ubuntu and you want toochange hello default port of Tomcat Listen (for example 8081), you should also open hello port for hello operating system.</span></span> <span data-ttu-id="86192-271">Во-первых откройте hello профиля:</span><span class="sxs-lookup"><span data-stu-id="86192-271">First, open hello profile:</span></span>  

        sudo vi /etc/default/tomcat7  

     <span data-ttu-id="86192-272">Затем удалите комментарий последнюю строку hello и измените «no» слишком «Да».</span><span class="sxs-lookup"><span data-stu-id="86192-272">Then uncomment hello last line and change “no” too“yes”.</span></span>  

        AUTHBIND=yes
  2. <span data-ttu-id="86192-273">брандмауэр Hello отключил прослушивания hello порт Tomcat.</span><span class="sxs-lookup"><span data-stu-id="86192-273">hello firewall has disabled hello listen port of Tomcat.</span></span>

     <span data-ttu-id="86192-274">Только вы увидите страницу по умолчанию hello Tomcat из локального узла hello.</span><span class="sxs-lookup"><span data-stu-id="86192-274">You can only see hello Tomcat default page from hello local host.</span></span> <span data-ttu-id="86192-275">проблема Hello, скорее всего, hello порт, который является прослушиваемом tooby Tomcat, заблокирован брандмауэром hello.</span><span class="sxs-lookup"><span data-stu-id="86192-275">hello problem is most likely that hello port, which is listened tooby Tomcat, is blocked by hello firewall.</span></span> <span data-ttu-id="86192-276">Можно использовать веб-страницу приветствия w3m средство toobrowse hello.</span><span class="sxs-lookup"><span data-stu-id="86192-276">You can use hello w3m tool toobrowse hello webpage.</span></span> <span data-ttu-id="86192-277">Hello следующие команды установки w3m и перейдите на страницу по умолчанию Tomcat toohello:</span><span class="sxs-lookup"><span data-stu-id="86192-277">hello following commands install w3m and browse toohello Tomcat default page:</span></span>  


        <span data-ttu-id="86192-278">sudo yum  install w3m w3m-img</span><span class="sxs-lookup"><span data-stu-id="86192-278">sudo yum  install w3m w3m-img</span></span>


        <span data-ttu-id="86192-279">w3m http://localhost:8080</span><span class="sxs-lookup"><span data-stu-id="86192-279">w3m http://localhost:8080</span></span>  
#### <a name="solution"></a><span data-ttu-id="86192-280">Решение</span><span class="sxs-lookup"><span data-stu-id="86192-280">Solution</span></span>

  * <span data-ttu-id="86192-281">Если порт прослушивания Tomcat hello не является hello таким же как частный порт hello hello конечной точки для виртуальной машины toohello трафика, необходимо изменить частный порт hello toobe hello так же, как hello порт прослушивания Tomcat.</span><span class="sxs-lookup"><span data-stu-id="86192-281">If hello Tomcat listen port is not hello same as hello private port of hello endpoint for traffic toohello virtual machine, you need change hello private port toobe hello same as hello Tomcat listen port.</span></span>   
  2. <span data-ttu-id="86192-282">Если hello проблема вызвана брандмауэра или утилита iptables, добавьте следующие строки слишком/д/sysconfig/утилита iptables hello.</span><span class="sxs-lookup"><span data-stu-id="86192-282">If hello issue is caused by firewall/iptables, add hello following lines too/etc/sysconfig/iptables.</span></span> <span data-ttu-id="86192-283">Вторая строка Hello требуется только для трафика https:</span><span class="sxs-lookup"><span data-stu-id="86192-283">hello second line is only needed for https traffic:</span></span>  

      <span data-ttu-id="86192-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="86192-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span></span>

      <span data-ttu-id="86192-285">A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="86192-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span></span>  

     > [!IMPORTANT]
     > <span data-ttu-id="86192-286">Убедитесь, что hello предыдущих строк позиционируются над все строки, глобально ограничит доступа, например hello следующее: -j ОТКЛОНИТЬ--отклонить-с помощью запрета сервера icmp - ввод</span><span class="sxs-lookup"><span data-stu-id="86192-286">Make sure hello previous lines are positioned above any lines that would globally restrict access, such as hello following: -A INPUT -j REJECT --reject-with icmp-host-prohibited</span></span>



<span data-ttu-id="86192-287">Утилита iptables tooreload hello, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="86192-287">tooreload hello iptables, run hello following command:</span></span>

    service iptables restart

<span data-ttu-id="86192-288">Протестировано в CentOS 6.3.</span><span class="sxs-lookup"><span data-stu-id="86192-288">This has been tested on CentOS 6.3.</span></span>

### <a name="permission-denied-when-you-upload-project-files-toovarlibtomcat7webapps"></a><span data-ttu-id="86192-289">Отказано в разрешении при загрузке проекта файлы слишком/var/lib/tomcat7/веб-приложений и</span><span class="sxs-lookup"><span data-stu-id="86192-289">Permission denied when you upload project files too/var/lib/tomcat7/webapps/</span></span>
#### <a name="symptom"></a><span data-ttu-id="86192-290">Симптом</span><span class="sxs-lookup"><span data-stu-id="86192-290">Symptom</span></span>
  <span data-ttu-id="86192-291">При использовании SFTP клиента (например, FileZilla) tooconnect tooyour виртуальной машине и перейдите слишком/var/lib/tomcat7/веб-приложений и toopublish веб-сайта, вы получаете ошибки сообщения аналогичные toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="86192-291">When you use an SFTP client (such as FileZilla) tooconnect tooyour virtual machine and navigate too/var/lib/tomcat7/webapps/ toopublish your site, you get an error message similar toohello following:</span></span>  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a><span data-ttu-id="86192-292">Возможная основная причина</span><span class="sxs-lookup"><span data-stu-id="86192-292">Possible root cause</span></span>
  <span data-ttu-id="86192-293">У вас нет разрешения tooaccess hello /var/lib/tomcat7/webapps папки.</span><span class="sxs-lookup"><span data-stu-id="86192-293">You have no permissions tooaccess hello /var/lib/tomcat7/webapps folder.</span></span>  
#### <a name="solution"></a><span data-ttu-id="86192-294">Решение</span><span class="sxs-lookup"><span data-stu-id="86192-294">Solution</span></span>  
  <span data-ttu-id="86192-295">Требуется разрешение tooget из учетной записи root hello.</span><span class="sxs-lookup"><span data-stu-id="86192-295">You need tooget permission from hello root account.</span></span> <span data-ttu-id="86192-296">Можно изменить владельца hello этой папке от корневого имени пользователя toohello, используемые при подготовке компьютера hello.</span><span class="sxs-lookup"><span data-stu-id="86192-296">You can change hello ownership of that folder from root toohello username you used when you provisioned hello machine.</span></span> <span data-ttu-id="86192-297">Ниже приведен пример hello azureuser учетной записи:</span><span class="sxs-lookup"><span data-stu-id="86192-297">Here is an example with hello azureuser account name:</span></span>  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  <span data-ttu-id="86192-298">Используйте hello -R параметр tooapply hello разрешения для всех файлов в каталоге.</span><span class="sxs-lookup"><span data-stu-id="86192-298">Use hello -R option tooapply hello permissions for all files inside of a directory too.</span></span>  

  <span data-ttu-id="86192-299">Эта команда также работает для каталогов.</span><span class="sxs-lookup"><span data-stu-id="86192-299">This command also works for directories.</span></span> <span data-ttu-id="86192-300">изменения параметров Hello -R hello разрешения для всех файлов и каталогов в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="86192-300">hello -R option changes hello permissions for all files and directories inside hello directory.</span></span> <span data-ttu-id="86192-301">Пример:</span><span class="sxs-lookup"><span data-stu-id="86192-301">Here is an example:</span></span>  

     sudo chown -R username:group directory  

  <span data-ttu-id="86192-302">Эта команда изменяет владельца (пользователей и групп) для всех файлов и папок, вложенных в каталог hello.</span><span class="sxs-lookup"><span data-stu-id="86192-302">This command changes ownership (both user and group) for all files and directories that are inside hello directory.</span></span>  

  <span data-ttu-id="86192-303">Hello следующая команда изменяет только разрешение hello hello папки каталога.</span><span class="sxs-lookup"><span data-stu-id="86192-303">hello following command only changes hello permission of hello folder directory.</span></span> <span data-ttu-id="86192-304">Hello файлы и папки в каталоге hello не изменяются.</span><span class="sxs-lookup"><span data-stu-id="86192-304">hello files and folders inside hello directory are not changed.</span></span>  

     sudo chown username:group directory

[1]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-01.png
[2]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-02.png
[3]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-03.png
[4]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-04.png
[5]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-05.png
[6]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-06.png
[7]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-07.png
[8]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-08.png
[9]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-09.png
[10]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-10.png
[11]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-11.png
[12]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-12.png
[13]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-13.png
[14]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-14.png
[15]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-15.png
[16]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-16.png
[17]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-17.png
[18]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-18.png
