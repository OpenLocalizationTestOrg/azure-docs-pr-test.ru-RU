---
title: "Настройка Apache Tomcat на виртуальной машине Linux | Документация Майкрософт"
description: "Сведения о настройке Apache Tomcat7 с помощью виртуальной машины Azure под управлением Linux."
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
ms.openlocfilehash: fa30c78a5a5d458ba8845c3c10b87538427786c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a><span data-ttu-id="16b6e-103">Настройка Tomcat7 на виртуальной машине Linux с использованием Azure</span><span class="sxs-lookup"><span data-stu-id="16b6e-103">Set up Tomcat7 on a Linux virtual machine with Azure</span></span>
<span data-ttu-id="16b6e-104">Apache Tomcat (или просто Tomcat, ранее также именуемый Jakarta Tomcat) — это веб-сервер с открытым исходным кодом и контейнер сервлетов, разработанный Apache Software Foundation (ASF).</span><span class="sxs-lookup"><span data-stu-id="16b6e-104">Apache Tomcat (or simply Tomcat, also formerly called Jakarta Tomcat) is an open source web server and servlet container developed by the Apache Software Foundation (ASF).</span></span> <span data-ttu-id="16b6e-105">Tomcat реализует спецификации технологий Java Servlet и JavaServer Pages (JSP) от Sun Microsystems,</span><span class="sxs-lookup"><span data-stu-id="16b6e-105">Tomcat implements the Java Servlet and the JavaServer Pages (JSP) specifications from Sun Microsystems.</span></span> <span data-ttu-id="16b6e-106">а также обеспечивает чистую среду HTTP-веб-серверов Java для выполнения Java-кода.</span><span class="sxs-lookup"><span data-stu-id="16b6e-106">Tomcat provides a pure Java HTTP web server environment in which to run Java code.</span></span> <span data-ttu-id="16b6e-107">При самой простой конфигурации Tomcat запускается с помощью одного процесса в операционной системе.</span><span class="sxs-lookup"><span data-stu-id="16b6e-107">In the simplest configuration, Tomcat runs in a single operating system process.</span></span> <span data-ttu-id="16b6e-108">Этот процесс запускает виртуальную машину Java.</span><span class="sxs-lookup"><span data-stu-id="16b6e-108">This process runs a Java virtual machine (JVM).</span></span> <span data-ttu-id="16b6e-109">Каждый HTTP-запрос браузера к серверу Tomcat обрабатывается как отдельный поток в рамках процесса Tomcat.</span><span class="sxs-lookup"><span data-stu-id="16b6e-109">Every HTTP request from a browser to Tomcat is processed as a separate thread in the Tomcat process.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="16b6e-110">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="16b6e-110">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="16b6e-111">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="16b6e-111">This article covers how to use the classic deployment model.</span></span> <span data-ttu-id="16b6e-112">Для большинства новых развертываний рекомендуется использовать модель Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="16b6e-112">We recommend that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="16b6e-113">Сведения о том, как использовать шаблон Resource Manager для развертывания виртуальной машины Ubuntu с Open JDK и Tomcat, см. [в этой статье](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span><span class="sxs-lookup"><span data-stu-id="16b6e-113">To use a Resource Manager template to deploy an Ubuntu VM with Open JDK and Tomcat, see [this article](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span></span>

<span data-ttu-id="16b6e-114">В этой статье показано, как установить Tomcat7 в образе Linux и развернуть его в службе Azure.</span><span class="sxs-lookup"><span data-stu-id="16b6e-114">In this article, you will install Tomcat7 on a Linux image and deploy it in Azure.</span></span>  

<span data-ttu-id="16b6e-115">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="16b6e-115">You will learn:</span></span>  

* <span data-ttu-id="16b6e-116">как создать виртуальную машину в Azure.</span><span class="sxs-lookup"><span data-stu-id="16b6e-116">How to create a virtual machine in Azure.</span></span>
* <span data-ttu-id="16b6e-117">как подготовить виртуальную машину для Tomcat7;</span><span class="sxs-lookup"><span data-stu-id="16b6e-117">How to prepare the virtual machine for Tomcat7.</span></span>
* <span data-ttu-id="16b6e-118">как установить Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="16b6e-118">How to install Tomcat7.</span></span>

<span data-ttu-id="16b6e-119">Предполагается, что у вас уже есть подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="16b6e-119">It is assumed that you already have an Azure subscription.</span></span>  <span data-ttu-id="16b6e-120">В противном случае вы можете оформить подписку на бесплатную пробную версию на [веб-сайте Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="16b6e-120">If not, you can sign up for a free trial at [the Azure website](https://azure.microsoft.com/).</span></span> <span data-ttu-id="16b6e-121">Если у вас есть подписка MSDN, сведения о специальных ценах Microsoft Azure на MSDN, MPN и Bizspark см. на [этой странице](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span><span class="sxs-lookup"><span data-stu-id="16b6e-121">If you have an MSDN subscription, see [Microsoft Azure Special Pricing: MSDN, MPN, and BizSpark Benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span></span> <span data-ttu-id="16b6e-122">Дополнительные сведения о службе Azure см. в статье [Что такое Azure?](https://azure.microsoft.com/overview/what-is-azure/)</span><span class="sxs-lookup"><span data-stu-id="16b6e-122">To learn more about Azure, see [What is Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span></span>

<span data-ttu-id="16b6e-123">В этой статье предполагается, что вы располагаете достаточными знаниями по работе с Tomcat и Linux.</span><span class="sxs-lookup"><span data-stu-id="16b6e-123">This article assumes that you have a basic working knowledge of Tomcat and Linux.</span></span>  

## <a name="phase-1-create-an-image"></a><span data-ttu-id="16b6e-124">Этап 1. Создание образа</span><span class="sxs-lookup"><span data-stu-id="16b6e-124">Phase 1: Create an image</span></span>
<span data-ttu-id="16b6e-125">На этом этапе вы создадите виртуальную машину с помощью образа Linux в Azure.</span><span class="sxs-lookup"><span data-stu-id="16b6e-125">In this phase, you will create a virtual machine by using a Linux image in Azure.</span></span>  

### <a name="step-1-generate-an-ssh-authentication-key"></a><span data-ttu-id="16b6e-126">Шаг 1. Создание ключа проверки подлинности SSH</span><span class="sxs-lookup"><span data-stu-id="16b6e-126">Step 1: Generate an SSH authentication key</span></span>
<span data-ttu-id="16b6e-127">SSH — это важный инструмент для системных администраторов.</span><span class="sxs-lookup"><span data-stu-id="16b6e-127">SSH is an important tool for system administrators.</span></span> <span data-ttu-id="16b6e-128">Однако для настройки безопасности доступа не рекомендуется использовать пароль, определенный пользователем.</span><span class="sxs-lookup"><span data-stu-id="16b6e-128">However, configuring access security based on a human-determined password is not recommended.</span></span> <span data-ttu-id="16b6e-129">Злоумышленники могут взломать ненадежный пароль и проникнуть в вашу систему, использовав имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="16b6e-129">Malicious users can break into your system based on a username and a weak password.</span></span>

<span data-ttu-id="16b6e-130">Хорошая новость заключается в том, что вы можете предоставлять удаленный доступ, не беспокоясь о надежности паролей.</span><span class="sxs-lookup"><span data-stu-id="16b6e-130">The good news is that there is a way to leave remote access open and not worry about passwords.</span></span> <span data-ttu-id="16b6e-131">Этот метод состоит в проверке подлинности с асимметричным шифрованием.</span><span class="sxs-lookup"><span data-stu-id="16b6e-131">This method consists of authentication with asymmetric cryptography.</span></span> <span data-ttu-id="16b6e-132">Пользователь проходит проверку подлинности с помощью своего закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="16b6e-132">The user’s private key is the one that grants the authentication.</span></span> <span data-ttu-id="16b6e-133">Вы можете даже заблокировать учетную запись пользователя, чтобы запретить проверку пароля.</span><span class="sxs-lookup"><span data-stu-id="16b6e-133">You can even lock the user’s account to not allow password authentication.</span></span>

<span data-ttu-id="16b6e-134">Кроме того, при использовании этого метода для входа на разные серверы не нужны разные пароли.</span><span class="sxs-lookup"><span data-stu-id="16b6e-134">Another advantage of this method is that you do not need different passwords to sign in to different servers.</span></span> <span data-ttu-id="16b6e-135">Вы можете пройти проверку подлинности с помощью личного закрытого ключа для всех серверов, благодаря чему не нужно запоминать несколько паролей.</span><span class="sxs-lookup"><span data-stu-id="16b6e-135">You can authenticate by using the personal private key on all servers, which prevents you from having to remember several passwords.</span></span>



<span data-ttu-id="16b6e-136">Выполните следующие действия, чтобы создать ключ проверки подлинности SSH.</span><span class="sxs-lookup"><span data-stu-id="16b6e-136">Follow these steps to generate the SSH authentication key.</span></span>

1. <span data-ttu-id="16b6e-137">Скачайте и установите PuTTYgen из следующего расположения: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="16b6e-137">Download and install PuTTYgen from the following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="16b6e-138">Запустите Puttygen.exe.</span><span class="sxs-lookup"><span data-stu-id="16b6e-138">Run Puttygen.exe.</span></span>
3. <span data-ttu-id="16b6e-139">Нажмите кнопку **Создать** , чтобы создать ключи.</span><span class="sxs-lookup"><span data-stu-id="16b6e-139">Click **Generate** to generate the keys.</span></span> <span data-ttu-id="16b6e-140">В процессе вы можете увеличить степень случайности, двигая указатель мыши в пустой области окна.</span><span class="sxs-lookup"><span data-stu-id="16b6e-140">In the process, you can increase randomness by moving the mouse over the blank area in the window.</span></span>  
   <span data-ttu-id="16b6e-141">![Снимок экрана с окном генератора ключей PuTTY, где отображается кнопка Generate (Создать)][1]</span><span class="sxs-lookup"><span data-stu-id="16b6e-141">![PuTTY Key Generator screenshot that shows the generate new key button][1]</span></span>
4. <span data-ttu-id="16b6e-142">После завершения процесса создания новый открытый ключ отобразится в средстве Puttygen.exe.</span><span class="sxs-lookup"><span data-stu-id="16b6e-142">After the generate process, Puttygen.exe will show your new public key.</span></span>  
   ![Снимок экрана с окном генератора ключей PuTTY, где отображается новый открытый ключ и кнопка Save private key (Сохранить закрытый ключ)][2]
5. <span data-ttu-id="16b6e-144">Выберите и скопируйте открытый ключ и сохраните его в файле с именем publicKey.pem.</span><span class="sxs-lookup"><span data-stu-id="16b6e-144">Select and copy the public key, and save it in a file named publicKey.pem.</span></span> <span data-ttu-id="16b6e-145">Не щелкайте **Сохранить открытый ключ**, так как формат файла сохраненного открытого ключа отличается от необходимого открытого ключа.</span><span class="sxs-lookup"><span data-stu-id="16b6e-145">Don’t click **Save public key**, because the saved public key’s file format is different from the public key we want.</span></span>
6. <span data-ttu-id="16b6e-146">Нажмите кнопку **Save private key** (Сохранить закрытый ключ) и сохраните его в файл с именем privateKey.ppk.</span><span class="sxs-lookup"><span data-stu-id="16b6e-146">Click **Save private key**, and save it in a file named privateKey.ppk.</span></span>

### <a name="step-2-create-the-image-in-the-azure-portal"></a><span data-ttu-id="16b6e-147">Шаг 2. Создание образа на портале Azure</span><span class="sxs-lookup"><span data-stu-id="16b6e-147">Step 2: Create the image in the Azure portal</span></span>
1. <span data-ttu-id="16b6e-148">На [портале](https://portal.azure.com/) на панели задач щелкните **Создать**, чтобы создать образ,</span><span class="sxs-lookup"><span data-stu-id="16b6e-148">In the [portal](https://portal.azure.com/), click **New** in the task bar to create an image.</span></span> <span data-ttu-id="16b6e-149">а затем выберите образ Linux в соответствии с вашими потребностями.</span><span class="sxs-lookup"><span data-stu-id="16b6e-149">Then choose the Linux image that is based on your needs.</span></span> <span data-ttu-id="16b6e-150">В этом примере используется образ Ubuntu 14.04.</span><span class="sxs-lookup"><span data-stu-id="16b6e-150">The following example uses the Ubuntu 14.04 image.</span></span>
<span data-ttu-id="16b6e-151">![Снимок экрана, где отображается расположение кнопки "Создать" на портале][3]</span><span class="sxs-lookup"><span data-stu-id="16b6e-151">![Screenshot of the portal that shows the New button][3]</span></span>

2. <span data-ttu-id="16b6e-152">В поле **Имя узла** укажите имя URL-адреса, с помощью которого интернет-клиенты будут получать доступ к этой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="16b6e-152">For **Host Name**, specify the name for the URL that you and Internet clients will use to access this virtual machine.</span></span> <span data-ttu-id="16b6e-153">Определите последнюю часть DNS-имени, например tomcatdemo,</span><span class="sxs-lookup"><span data-stu-id="16b6e-153">Define the last part of the DNS name, for example, tomcatdemo.</span></span> <span data-ttu-id="16b6e-154">после чего в службе Azure будет создан URL-адрес lampdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="16b6e-154">Azure will then generate the URL as tomcatdemo.cloudapp.net.</span></span>  

3. <span data-ttu-id="16b6e-155">В поле **SSH Authentication Key** (Ключ аутентификации SSH) скопируйте значение ключа из файла publicKey.pem, который содержит открытый ключ, созданный с помощью средства PuTTYgen.</span><span class="sxs-lookup"><span data-stu-id="16b6e-155">For **SSH Authentication Key**, copy the key value from the publicKey.pem file, which contains the public key generated by PuTTYgen.</span></span>  
<span data-ttu-id="16b6e-156">![Поле SSH Authentication Key (Ключ проверки подлинности SSH) на портале][4]</span><span class="sxs-lookup"><span data-stu-id="16b6e-156">![SSH Authentication Key box in the portal][4]</span></span>

4. <span data-ttu-id="16b6e-157">При необходимости настройте другие параметры и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="16b6e-157">Configure other settings as needed, and then click **Create**.</span></span>  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a><span data-ttu-id="16b6e-158">Этап 2. Подготовка виртуальной машины для Tomcat7</span><span class="sxs-lookup"><span data-stu-id="16b6e-158">Phase 2: Prepare your virtual machine for Tomcat7</span></span>
<span data-ttu-id="16b6e-159">На этом этапе вы настроите конечную точку для трафика Tomcat и подключитесь к новой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="16b6e-159">In this phase, you will configure an endpoint for Tomcat traffic, and then connect to your new virtual machine.</span></span>

### <a name="step-1-open-the-http-port-to-allow-web-access"></a><span data-ttu-id="16b6e-160">Шаг 1. Открытие HTTP-порта для разрешения веб-доступа</span><span class="sxs-lookup"><span data-stu-id="16b6e-160">Step 1: Open the HTTP port to allow web access</span></span>
<span data-ttu-id="16b6e-161">Конечные точки в Azure состоят из протокола (TCP или UDP), а также общего и частного порта.</span><span class="sxs-lookup"><span data-stu-id="16b6e-161">Endpoints in Azure consist of a TCP or UDP protocol, along with a public and private port.</span></span> <span data-ttu-id="16b6e-162">Частный порт — это порт, который прослушивает служба на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="16b6e-162">The private port is the port that the service is listening to on the virtual machine.</span></span> <span data-ttu-id="16b6e-163">Общий порт — это порт, который облачная служба Azure прослушивает извне на наличие интернет-трафика.</span><span class="sxs-lookup"><span data-stu-id="16b6e-163">The public port is the port that the Azure cloud service listens to externally for incoming, Internet-based traffic.</span></span>  

<span data-ttu-id="16b6e-164">TCP-порт 8080 — номер порта по умолчанию, который использует Tomcat для прослушивания.</span><span class="sxs-lookup"><span data-stu-id="16b6e-164">TCP port 8080 is the default port number that Tomcat uses to listen.</span></span> <span data-ttu-id="16b6e-165">Открытие этого порта с помощью конечной точки Azure обеспечивает вам и другим интернет-клиентам доступ к страницам Tomcat.</span><span class="sxs-lookup"><span data-stu-id="16b6e-165">If this port is opened with an Azure endpoint, you and other Internet clients can access Tomcat pages.</span></span>  

1. <span data-ttu-id="16b6e-166">На портале щелкните **Обзор** > **Виртуальная машина** и выберите созданную виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="16b6e-166">In the portal, click **Browse** > **Virtual machines**, and then click the virtual machine that you created.</span></span>  
   <span data-ttu-id="16b6e-167">![Снимок экрана, где отображается каталог виртуальных машин][5]</span><span class="sxs-lookup"><span data-stu-id="16b6e-167">![Screenshot of the Virtual machines directory][5]</span></span>
2. <span data-ttu-id="16b6e-168">Чтобы добавить к виртуальной машине конечную точку, щелкните поле **Конечные точки** .</span><span class="sxs-lookup"><span data-stu-id="16b6e-168">To add an endpoint to your virtual machine, click the **Endpoints** box.</span></span>
   <span data-ttu-id="16b6e-169">![Снимок экрана, где отображается плитка "Конечные точки"][6]</span><span class="sxs-lookup"><span data-stu-id="16b6e-169">![Screenshot that shows the Endpoints box][6]</span></span>
3. <span data-ttu-id="16b6e-170">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="16b6e-170">Click **Add**.</span></span>  

   1. <span data-ttu-id="16b6e-171">Введите имя конечной точки в поле **Конечная точка** и значение 80 в поле **Общий порт**.</span><span class="sxs-lookup"><span data-stu-id="16b6e-171">For the endpoint, enter a name for the endpoint in **Endpoint**, and then enter 80 in **Public Port**.</span></span>  

      <span data-ttu-id="16b6e-172">Если задать значение 80, вам не нужно будет добавлять номер порта в URL-адрес, по которому вы получаете доступ к Tomcat.</span><span class="sxs-lookup"><span data-stu-id="16b6e-172">If you set it to 80, you don’t need to include the port number in the URL that is used to access Tomcat.</span></span> <span data-ttu-id="16b6e-173">Например, http://tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="16b6e-173">For example, http://tomcatdemo.cloudapp.net.</span></span>    

      <span data-ttu-id="16b6e-174">Если ему присвоено другое значение, например 81, необходимо добавить номер порта в URL-адрес для доступа к Tomcat.</span><span class="sxs-lookup"><span data-stu-id="16b6e-174">If you set it to another value, such as 81, you need to add the port number to the URL to access Tomcat.</span></span> <span data-ttu-id="16b6e-175">Например, http://tomcatdemo.cloudapp.net:81/.</span><span class="sxs-lookup"><span data-stu-id="16b6e-175">For example,  http://tomcatdemo.cloudapp.net:81/.</span></span>
   2. <span data-ttu-id="16b6e-176">Введите 8080 в поле **Частный порт**.</span><span class="sxs-lookup"><span data-stu-id="16b6e-176">Enter 8080 in **Private Port**.</span></span> <span data-ttu-id="16b6e-177">По умолчанию Tomcat прослушивает TCP-порт 8080.</span><span class="sxs-lookup"><span data-stu-id="16b6e-177">By default, Tomcat listens on TCP port 8080.</span></span> <span data-ttu-id="16b6e-178">Если вы изменили значение по умолчанию для прослушивающего порта Tomcat, обновите **частный порт**, чтобы он совпадал с прослушивающим портом Tomcat.</span><span class="sxs-lookup"><span data-stu-id="16b6e-178">If you changed the default listen port of Tomcat, you should update **Private Port** to be the same as the Tomcat listen port.</span></span>  
      <span data-ttu-id="16b6e-179">![Снимок экрана пользовательского интерфейса, где отображается команда "Добавить" и поля "Общий порт" и "Частный порт"][7]</span><span class="sxs-lookup"><span data-stu-id="16b6e-179">![Screenshot of UI that shows Add command, Public Port, and Private Port][7]</span></span>
4. <span data-ttu-id="16b6e-180">Нажмите кнопку **ОК** , чтобы добавить конечную точку к своей виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="16b6e-180">Click **OK** to add the endpoint to your virtual machine.</span></span>

### <a name="step-2-connect-to-the-image-you-created"></a><span data-ttu-id="16b6e-181">Шаг 2. Подключение к созданному образу</span><span class="sxs-lookup"><span data-stu-id="16b6e-181">Step 2: Connect to the image you created</span></span>
<span data-ttu-id="16b6e-182">Вы можете выбрать любой инструмент SSH для подключения к своей виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="16b6e-182">You can choose any SSH tool to connect to your virtual machine.</span></span> <span data-ttu-id="16b6e-183">В этом примере мы используем средство PuTTY.</span><span class="sxs-lookup"><span data-stu-id="16b6e-183">In this example, we use PuTTY.</span></span>  

1. <span data-ttu-id="16b6e-184">Получите DNS-имя вашей виртуальной машины на портале.</span><span class="sxs-lookup"><span data-stu-id="16b6e-184">Get the DNS name of your virtual machine from the portal.</span></span>
    1. <span data-ttu-id="16b6e-185">Щелкните **Обзор** > **Виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="16b6e-185">Click **Browse** > **Virtual machines**.</span></span>
    2. <span data-ttu-id="16b6e-186">Выберите имя виртуальной машины и щелкните **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="16b6e-186">Select the name of your virtual machine, and then click **Properties**.</span></span>
    3. <span data-ttu-id="16b6e-187">Чтобы получить DNS-имя, выберите плитку **Свойства** и найдите поле **Имя домена**.</span><span class="sxs-lookup"><span data-stu-id="16b6e-187">In the **Properties** tile, look in the **Domain Name** box to get the DNS name.</span></span>  

2. <span data-ttu-id="16b6e-188">Получите номер порта для подключений по протоколу SSH в поле **SSH**.</span><span class="sxs-lookup"><span data-stu-id="16b6e-188">Get the port number for SSH connections from the **SSH** box.</span></span>  
<span data-ttu-id="16b6e-189">![Снимок экрана, где отображается номер порта SSH-подключения][8]</span><span class="sxs-lookup"><span data-stu-id="16b6e-189">![Screenshot that shows the SSH connection port number][8]</span></span>

3. <span data-ttu-id="16b6e-190">Скачайте [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="16b6e-190">Download [PuTTY](http://www.putty.org/).</span></span>  

4. <span data-ttu-id="16b6e-191">После скачивания запустите исполняемый файл Putty.exe.</span><span class="sxs-lookup"><span data-stu-id="16b6e-191">After downloading, click the executable file Putty.exe.</span></span> <span data-ttu-id="16b6e-192">В конфигурации PuTTY настройте основные параметры, указав имя узла и номер порта, полученные в свойствах виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="16b6e-192">In PuTTY configuration, configure the basic options with the host name and port number that is obtained from the properties of your virtual machine.</span></span>   
![Снимок экрана с конфигурацией PuTTY, где отображаются значения полей "Имя узла" и "Порт"][9]

5. <span data-ttu-id="16b6e-194">Чтобы указать расположение файла privateKey.ppk, в левой области выберите **Подключения** > **SSH** > **Проверка подлинности** и нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="16b6e-194">In the left pane, click **Connection** > **SSH** > **Auth**, and then click **Browse** to specify the location of the privateKey.ppk file.</span></span> <span data-ttu-id="16b6e-195">Файл privateKey.ppk содержит закрытый ключ, созданный ранее с помощью средства PuTTYgen в разделе "Этап 1. Создание образа" этой статьи.</span><span class="sxs-lookup"><span data-stu-id="16b6e-195">The privateKey.ppk file contains the private key that is generated by PuTTYgen earlier in the "Phase 1: Create an image" section of this article.</span></span>  
<span data-ttu-id="16b6e-196">![Снимок экрана, где отображается иерархия каталогов подключения и кнопка "Обзор"][10]</span><span class="sxs-lookup"><span data-stu-id="16b6e-196">![Screenshot that shows the Connection directory hierarchy and Browse button][10]</span></span>

6. <span data-ttu-id="16b6e-197">Щелкните **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="16b6e-197">Click **Open**.</span></span> <span data-ttu-id="16b6e-198">Может отобразиться оповещение в окне сообщения.</span><span class="sxs-lookup"><span data-stu-id="16b6e-198">You might be alerted by a message box.</span></span> <span data-ttu-id="16b6e-199">Если вы настроили DNS-имя и номер порта правильно, нажмите кнопку **Да**.</span><span class="sxs-lookup"><span data-stu-id="16b6e-199">If you have configured the DNS name and port number correctly, click **Yes**.</span></span>
<span data-ttu-id="16b6e-200">![Снимок экрана, на котором отображается уведомление][11]</span><span class="sxs-lookup"><span data-stu-id="16b6e-200">![Screenshot that shows the notification][11]</span></span>

7. <span data-ttu-id="16b6e-201">Затем вам будет предложено ввести имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="16b6e-201">You are prompted to enter your username.</span></span>  
![Снимок экрана, на котором показано, где нужно ввести имя пользователя][12]

8. <span data-ttu-id="16b6e-203">Введите имя пользователя, которое использовалось ранее для создания виртуальной машины в разделе "Этап 1. Создание образа" этой статьи.</span><span class="sxs-lookup"><span data-stu-id="16b6e-203">Enter the username that you used to create the virtual machine in the "Phase 1: Create an image" section earlier in this article.</span></span> <span data-ttu-id="16b6e-204">Вы увидите что-то вроде этого: </span><span class="sxs-lookup"><span data-stu-id="16b6e-204">You will see something like the following:</span></span>  
![Снимок экрана с подтверждением проверки подлинности][13]

## <a name="phase-3-install-software"></a><span data-ttu-id="16b6e-206">Этап 3. Установка программного обеспечения</span><span class="sxs-lookup"><span data-stu-id="16b6e-206">Phase 3: Install software</span></span>
<span data-ttu-id="16b6e-207">На этом этапе необходимо установить среду выполнения Java, пакет Tomcat7 и другие компоненты Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="16b6e-207">In this phase, you install the Java runtime environment, Tomcat7, and other Tomcat7 components.</span></span>  

### <a name="java-runtime-environment"></a><span data-ttu-id="16b6e-208">Среда выполнения Java</span><span class="sxs-lookup"><span data-stu-id="16b6e-208">Java runtime environment</span></span>
<span data-ttu-id="16b6e-209">Программное обеспечение Tomcat написано на языке Java.</span><span class="sxs-lookup"><span data-stu-id="16b6e-209">Tomcat is written in Java.</span></span> <span data-ttu-id="16b6e-210">Есть два вида комплектов Java Development Kit (JDK) — OpenJDK и Oracle JDK.</span><span class="sxs-lookup"><span data-stu-id="16b6e-210">There are two kinds of Java Development Kits (JDKs), OpenJDK and Oracle JDK.</span></span> <span data-ttu-id="16b6e-211">Вы можете выбрать наиболее подходящий из них.</span><span class="sxs-lookup"><span data-stu-id="16b6e-211">You can choose the one you want.</span></span>  

> [!NOTE]
> <span data-ttu-id="16b6e-212">В обоих видах JDK для классов в Java API используются почти одинаковые коды, но код для виртуальной машины отличается.</span><span class="sxs-lookup"><span data-stu-id="16b6e-212">Both JDKs have almost the same code for the classes in the Java API, but the code for the virtual machine is different.</span></span> <span data-ttu-id="16b6e-213">В OpenJDK, как правило, используются открытые библиотеки, а в Oracle JDK — закрытые библиотеки.</span><span class="sxs-lookup"><span data-stu-id="16b6e-213">OpenJDK tends to use open libraries, while Oracle JDK tends to use closed ones.</span></span> <span data-ttu-id="16b6e-214">В Oracle JDK доступно больше классов и в нем исправлены некоторые ошибки. К тому же Oracle JDK работает стабильнее, чем OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="16b6e-214">Oracle JDK has more classes and some fixed bugs, and Oracle JDK is more stable than OpenJDK.</span></span>

#### <a name="install-openjdk"></a><span data-ttu-id="16b6e-215">Установка OpenJDK</span><span class="sxs-lookup"><span data-stu-id="16b6e-215">Install OpenJDK</span></span>  

<span data-ttu-id="16b6e-216">Чтобы скачать OpenJDK, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="16b6e-216">Use the following command to download OpenJDK.</span></span>   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* <span data-ttu-id="16b6e-217">Чтобы создать каталог, в котором будут содержаться файлы JDK:</span><span class="sxs-lookup"><span data-stu-id="16b6e-217">To create a directory to contain the JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="16b6e-218">Чтобы извлечь файлы JDK в каталог /usr/lib/jvm/:</span><span class="sxs-lookup"><span data-stu-id="16b6e-218">To extract the JDK files into the /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a><span data-ttu-id="16b6e-219">Установка Oracle JDK</span><span class="sxs-lookup"><span data-stu-id="16b6e-219">Install Oracle JDK</span></span>


<span data-ttu-id="16b6e-220">Чтобы скачать Oracle JDK на веб-сайте Oracle, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="16b6e-220">Use the following command to download Oracle JDK from the Oracle website.</span></span>  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* <span data-ttu-id="16b6e-221">Чтобы создать каталог, в котором будут содержаться файлы JDK:</span><span class="sxs-lookup"><span data-stu-id="16b6e-221">To create a directory to contain the JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="16b6e-222">Чтобы извлечь файлы JDK в каталог /usr/lib/jvm/:</span><span class="sxs-lookup"><span data-stu-id="16b6e-222">To extract the JDK files into the /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* <span data-ttu-id="16b6e-223">Чтобы задать Oracle JDK в качестве виртуальной машины Java по умолчанию, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="16b6e-223">To set Oracle JDK as the default Java virtual machine:</span></span>  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a><span data-ttu-id="16b6e-224">Убедитесь, что установка Java выполнена успешно.</span><span class="sxs-lookup"><span data-stu-id="16b6e-224">Confirm that Java installation is successful</span></span>
<span data-ttu-id="16b6e-225">Вы можете использовать подобную команду, чтобы проверить, правильно ли установлена среда выполнения Java:</span><span class="sxs-lookup"><span data-stu-id="16b6e-225">You can use a command like the following to test if the Java runtime environment is installed correctly:</span></span>  

    java -version  

<span data-ttu-id="16b6e-226">Если вы установили OpenJDK, вы увидите примерно следующее сообщение: ![Сообщение об успешной установке OpenJDK][14]</span><span class="sxs-lookup"><span data-stu-id="16b6e-226">If you installed OpenJDK, you should see a message like the following: ![Successful OpenJDK installation message][14]</span></span>

<span data-ttu-id="16b6e-227">Если вы установили Oracle JDK, вы увидите примерно следующее сообщение: ![Сообщение об успешной установке Oracle JDK][15]</span><span class="sxs-lookup"><span data-stu-id="16b6e-227">If you installed Oracle JDK, you should see a message like the following: ![Successful Oracle JDK installation message][15]</span></span>

### <a name="install-tomcat7"></a><span data-ttu-id="16b6e-228">Установка Tomcat7</span><span class="sxs-lookup"><span data-stu-id="16b6e-228">Install Tomcat7</span></span>
<span data-ttu-id="16b6e-229">Чтобы установить Tomcat7, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="16b6e-229">Use the following command to install Tomcat7.</span></span>  

    sudo apt-get install tomcat7  

<span data-ttu-id="16b6e-230">Если вы не используете Tomcat7, воспользуйтесь соответствующим вариантом этой команды.</span><span class="sxs-lookup"><span data-stu-id="16b6e-230">If you are not using Tomcat7, use the appropriate variation of this command.</span></span>  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a><span data-ttu-id="16b6e-231">Убедитесь, что Tomcat7 успешно установлен.</span><span class="sxs-lookup"><span data-stu-id="16b6e-231">Confirm that Tomcat7 installation is successful</span></span>
<span data-ttu-id="16b6e-232">Чтобы убедиться в успешной установке Tomcat7, выберите имя DNS-сервера, на котором установлен Tomcat.</span><span class="sxs-lookup"><span data-stu-id="16b6e-232">To check if Tomcat7 is successfully installed, browse to your Tomcat server’s DNS name.</span></span> <span data-ttu-id="16b6e-233">В качестве примера в этой статье используется URL-адрес http://tomcatexample.cloudapp.net/.</span><span class="sxs-lookup"><span data-stu-id="16b6e-233">In this article, the example URL is http://tomcatexample.cloudapp.net/.</span></span> <span data-ttu-id="16b6e-234">Если вы видите подобное сообщение, Tomcat7 установлен правильно.</span><span class="sxs-lookup"><span data-stu-id="16b6e-234">If you see a message like the following, Tomcat7 is installed correctly.</span></span>
<span data-ttu-id="16b6e-235">![Сообщение об успешной установке Tomcat7][16]</span><span class="sxs-lookup"><span data-stu-id="16b6e-235">![Successful Tomcat7 installation message][16]</span></span>

### <a name="install-other-tomcat7-components"></a><span data-ttu-id="16b6e-236">Установка других компонентов Tomcat7</span><span class="sxs-lookup"><span data-stu-id="16b6e-236">Install other Tomcat7 components</span></span>
<span data-ttu-id="16b6e-237">Существуют другие дополнительные компоненты Tomcat, которые вы можете установить.</span><span class="sxs-lookup"><span data-stu-id="16b6e-237">There are other optional Tomcat components that you can install.</span></span>  

<span data-ttu-id="16b6e-238">Получить список всех доступных компонентов можно с помощью команды **sudo apt-cache search tomcat7**.</span><span class="sxs-lookup"><span data-stu-id="16b6e-238">Use the **sudo apt-cache search tomcat7** command to see all of the available components.</span></span> <span data-ttu-id="16b6e-239">Чтобы установить некоторые полезные компоненты, используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="16b6e-239">Use the following commands to install some useful components.</span></span>  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools to create user instances  

## <a name="phase-4-configure-tomcat7"></a><span data-ttu-id="16b6e-240">Этап 4. Настройка Tomcat7</span><span class="sxs-lookup"><span data-stu-id="16b6e-240">Phase 4: Configure Tomcat7</span></span>
<span data-ttu-id="16b6e-241">На этом этапе вы узнаете о том, как управлять Tomcat.</span><span class="sxs-lookup"><span data-stu-id="16b6e-241">In this phase, you administer Tomcat.</span></span>

### <a name="start-and-stop-tomcat7"></a><span data-ttu-id="16b6e-242">Запуск и остановка Tomcat7</span><span class="sxs-lookup"><span data-stu-id="16b6e-242">Start and stop Tomcat7</span></span>
<span data-ttu-id="16b6e-243">При установке пакета Tomcat7 сервер Tomcat7 запускается автоматически.</span><span class="sxs-lookup"><span data-stu-id="16b6e-243">The Tomcat7 server automatically starts when you install it.</span></span> <span data-ttu-id="16b6e-244">Вы также можете запустить его, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="16b6e-244">You can also start it with the following command:</span></span>   

    sudo /etc/init.d/tomcat7 start

<span data-ttu-id="16b6e-245">Чтобы остановить Tomcat7, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="16b6e-245">To stop Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 stop

<span data-ttu-id="16b6e-246">Чтобы просмотреть состояние Tomcat7, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="16b6e-246">To view the status of Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 status

<span data-ttu-id="16b6e-247">Чтобы перезапустить службы Tomcat, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="16b6e-247">To restart Tomcat services:</span></span> 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a><span data-ttu-id="16b6e-248">Администрирование Tomcat7</span><span class="sxs-lookup"><span data-stu-id="16b6e-248">Tomcat7 administration</span></span>
<span data-ttu-id="16b6e-249">Вы можете изменить файл конфигурации пользователя Tomcat, чтобы настроить учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="16b6e-249">You can edit the Tomcat user configuration file to set up your admin credentials.</span></span> <span data-ttu-id="16b6e-250">Используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="16b6e-250">Use the following command:</span></span>  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

<span data-ttu-id="16b6e-251">Пример:</span><span class="sxs-lookup"><span data-stu-id="16b6e-251">Here is an example:</span></span>  
![Снимок экрана, где отображаются выходные данные команды sudo vi][17]  

> [!NOTE]
> <span data-ttu-id="16b6e-253">Создайте надежный пароль для имени пользователя администратора.</span><span class="sxs-lookup"><span data-stu-id="16b6e-253">Create a strong password for the admin username.</span></span>  

<span data-ttu-id="16b6e-254">Изменив этот файл, перезапустите службы Tomcat7 с помощью следующей команды, чтобы изменения вступили в силу:</span><span class="sxs-lookup"><span data-stu-id="16b6e-254">After editing this file, you should restart Tomcat7 services with the following command to ensure that the changes take effect:</span></span>  

    sudo /etc/init.d/tomcat7 restart  

<span data-ttu-id="16b6e-255">Откройте браузер и введите URL-адрес **http://<your tomcat server DNS name>/manager/html**.</span><span class="sxs-lookup"><span data-stu-id="16b6e-255">Open your browser, and enter **http://<your tomcat server DNS name>/manager/html** as the URL.</span></span> <span data-ttu-id="16b6e-256">В качестве примера в этой статье используется URL-адрес http://tomcatexample.cloudapp.net/manager/html.</span><span class="sxs-lookup"><span data-stu-id="16b6e-256">For the example in this article, the URL is http://tomcatexample.cloudapp.net/manager/html.</span></span>  

<span data-ttu-id="16b6e-257">После подключения должен появиться результат, аналогичный следующему: </span><span class="sxs-lookup"><span data-stu-id="16b6e-257">After connecting, you should see something similar to the following:</span></span>  
![Снимок экрана, где отображается диспетчер веб-приложений Tomcat][18]

## <a name="common-issues"></a><span data-ttu-id="16b6e-259">Распространенные проблемы</span><span class="sxs-lookup"><span data-stu-id="16b6e-259">Common issues</span></span>
### <a name="cant-access-the-virtual-machine-with-tomcat-and-moodle-from-the-internet"></a><span data-ttu-id="16b6e-260">Не удается получить доступ к виртуальной машине с Tomcat и Moodle из Интернета</span><span class="sxs-lookup"><span data-stu-id="16b6e-260">Can't access the virtual machine with Tomcat and Moodle from the Internet</span></span>
#### <a name="symptom"></a><span data-ttu-id="16b6e-261">Симптом</span><span class="sxs-lookup"><span data-stu-id="16b6e-261">Symptom</span></span>  
  <span data-ttu-id="16b6e-262">Tomcat работает, но в браузере не отображается страница Tomcat по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="16b6e-262">Tomcat is running but you can’t see the Tomcat default page with your browser.</span></span>
#### <a name="possible-root-cause"></a><span data-ttu-id="16b6e-263">Возможная основная причина</span><span class="sxs-lookup"><span data-stu-id="16b6e-263">Possible root cause</span></span>   

  * <span data-ttu-id="16b6e-264">Прослушивающий порт Tomcat отличается от частного порта конечной точки виртуальной машины, предназначенного для трафика Tomcat.</span><span class="sxs-lookup"><span data-stu-id="16b6e-264">The Tomcat listen port is not the same as the private port of your virtual machine's endpoint for Tomcat traffic.</span></span>  

     <span data-ttu-id="16b6e-265">Проверьте параметры конечных точек общего и частного портов и убедитесь, что частный порт совпадает с прослушивающим портом Tomcat.</span><span class="sxs-lookup"><span data-stu-id="16b6e-265">Check your public port and private port endpoint settings and make sure the private port is the same as the Tomcat listen port.</span></span> <span data-ttu-id="16b6e-266">Дополнительные инструкции по настройке конечных точек см. в разделе "Этап 1. Создание образа" этой статьи.</span><span class="sxs-lookup"><span data-stu-id="16b6e-266">See "Phase 1: Create an image" section of this article for instructions on configuring endpoints for your virtual machine.</span></span>  

     <span data-ttu-id="16b6e-267">Чтобы выяснить, какой порт прослушивает Tomcat, откройте файл /etc/httpd/conf/httpd.conf (выпуск Red Hat) или /etc/tomcat7/server.xml (выпуск Debian).</span><span class="sxs-lookup"><span data-stu-id="16b6e-267">To determine the Tomcat listen port, open /etc/httpd/conf/httpd.conf (Red Hat release), or /etc/tomcat7/server.xml (Debian release).</span></span> <span data-ttu-id="16b6e-268">По умолчанию Tomcat прослушивает порт 8080.</span><span class="sxs-lookup"><span data-stu-id="16b6e-268">By default, the Tomcat listen port is 8080.</span></span> <span data-ttu-id="16b6e-269">Пример:</span><span class="sxs-lookup"><span data-stu-id="16b6e-269">Here is an example:</span></span>  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     <span data-ttu-id="16b6e-270">Если вы используете виртуальную машину Debian или Ubuntu и вам необходимо изменить порт, который прослушивает Tomcat по умолчанию (например, 8081), вам следует открыть также порт для операционной системы.</span><span class="sxs-lookup"><span data-stu-id="16b6e-270">If you are using a virtual machine like Debian or Ubuntu and you want to change the default port of Tomcat Listen (for example 8081), you should also open the port for the operating system.</span></span> <span data-ttu-id="16b6e-271">Сначала откройте профиль, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="16b6e-271">First, open the profile:</span></span>  

        sudo vi /etc/default/tomcat7  

     <span data-ttu-id="16b6e-272">Раскомментируйте последнюю строку и измените «no» на «yes».</span><span class="sxs-lookup"><span data-stu-id="16b6e-272">Then uncomment the last line and change “no” to “yes”.</span></span>  

        AUTHBIND=yes
  2. <span data-ttu-id="16b6e-273">Брандмауэр отключил прослушивающий порт Tomcat.</span><span class="sxs-lookup"><span data-stu-id="16b6e-273">The firewall has disabled the listen port of Tomcat.</span></span>

     <span data-ttu-id="16b6e-274">Страница по умолчанию Tomcat отображается только на локальном узле.</span><span class="sxs-lookup"><span data-stu-id="16b6e-274">You can only see the Tomcat default page from the local host.</span></span> <span data-ttu-id="16b6e-275">Скорее всего, проблема состоит в том, что порт, который прослушивает Tomcat, блокируется брандмауэром.</span><span class="sxs-lookup"><span data-stu-id="16b6e-275">The problem is most likely that the port, which is listened to by Tomcat, is blocked by the firewall.</span></span> <span data-ttu-id="16b6e-276">Для просмотра веб-страницы можно использовать средство w3m.</span><span class="sxs-lookup"><span data-stu-id="16b6e-276">You can use the w3m tool to browse the webpage.</span></span> <span data-ttu-id="16b6e-277">Следующие команды позволяют установить программу w3m и перейти на страницу Tomcat по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="16b6e-277">The following commands install w3m and browse to the Tomcat default page:</span></span>  


        <span data-ttu-id="16b6e-278">sudo yum  install w3m w3m-img</span><span class="sxs-lookup"><span data-stu-id="16b6e-278">sudo yum  install w3m w3m-img</span></span>


        <span data-ttu-id="16b6e-279">w3m http://localhost:8080</span><span class="sxs-lookup"><span data-stu-id="16b6e-279">w3m http://localhost:8080</span></span>  
#### <a name="solution"></a><span data-ttu-id="16b6e-280">Решение</span><span class="sxs-lookup"><span data-stu-id="16b6e-280">Solution</span></span>

  * <span data-ttu-id="16b6e-281">Если прослушивающий порт Tomcat отличается от частного порта конечной точки виртуальной машины, предназначенного для трафика, необходимо изменить частный порт, чтобы он совпал с прослушивающим портом Tomcat.</span><span class="sxs-lookup"><span data-stu-id="16b6e-281">If the Tomcat listen port is not the same as the private port of the endpoint for traffic to the virtual machine, you need change the private port to be the same as the Tomcat listen port.</span></span>   
  2. <span data-ttu-id="16b6e-282">Если проблема вызвана брандмауэром или программой iptables, добавьте следующие строки в /etc/sysconfig/iptables.</span><span class="sxs-lookup"><span data-stu-id="16b6e-282">If the issue is caused by firewall/iptables, add the following lines to /etc/sysconfig/iptables.</span></span> <span data-ttu-id="16b6e-283">Вторая строка требуется только для трафика https:</span><span class="sxs-lookup"><span data-stu-id="16b6e-283">The second line is only needed for https traffic:</span></span>  

      <span data-ttu-id="16b6e-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="16b6e-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span></span>

      <span data-ttu-id="16b6e-285">A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span><span class="sxs-lookup"><span data-stu-id="16b6e-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span></span>  

     > [!IMPORTANT]
     > <span data-ttu-id="16b6e-286">Убедитесь, что предыдущие строки расположены над всеми строками, которые глобально ограничивают доступ, например: A INPUT -j REJECT --reject-with icmp-host-prohibited</span><span class="sxs-lookup"><span data-stu-id="16b6e-286">Make sure the previous lines are positioned above any lines that would globally restrict access, such as the following: -A INPUT -j REJECT --reject-with icmp-host-prohibited</span></span>



<span data-ttu-id="16b6e-287">Чтобы перезагрузить iptables, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="16b6e-287">To reload the iptables, run the following command:</span></span>

    service iptables restart

<span data-ttu-id="16b6e-288">Протестировано в CentOS 6.3.</span><span class="sxs-lookup"><span data-stu-id="16b6e-288">This has been tested on CentOS 6.3.</span></span>

### <a name="permission-denied-when-you-upload-project-files-to-varlibtomcat7webapps"></a><span data-ttu-id="16b6e-289">Во время передачи файлов проекта в папку /var/lib/tomcat7/webapps/ вам отказано в доступе.</span><span class="sxs-lookup"><span data-stu-id="16b6e-289">Permission denied when you upload project files to /var/lib/tomcat7/webapps/</span></span>
#### <a name="symptom"></a><span data-ttu-id="16b6e-290">Симптом</span><span class="sxs-lookup"><span data-stu-id="16b6e-290">Symptom</span></span>
  <span data-ttu-id="16b6e-291">Если вы используете любой SFTP-клиент (такой как FileZilla) для подключения к своей виртуальной машине и переходите в папку /var/lib/tomcat7/webapps/ для публикации своего сайта, отображается сообщение об ошибке следующего вида:</span><span class="sxs-lookup"><span data-stu-id="16b6e-291">When you use an SFTP client (such as FileZilla) to connect to your virtual machine and navigate to /var/lib/tomcat7/webapps/ to publish your site, you get an error message similar to the following:</span></span>  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a><span data-ttu-id="16b6e-292">Возможная основная причина</span><span class="sxs-lookup"><span data-stu-id="16b6e-292">Possible root cause</span></span>
  <span data-ttu-id="16b6e-293">У вас нет разрешения на доступ к папке /var/lib/tomcat7/.</span><span class="sxs-lookup"><span data-stu-id="16b6e-293">You have no permissions to access the /var/lib/tomcat7/webapps folder.</span></span>  
#### <a name="solution"></a><span data-ttu-id="16b6e-294">Решение</span><span class="sxs-lookup"><span data-stu-id="16b6e-294">Solution</span></span>  
  <span data-ttu-id="16b6e-295">Необходимо получить разрешение из учетной записи root.</span><span class="sxs-lookup"><span data-stu-id="16b6e-295">You need to get permission from the root account.</span></span> <span data-ttu-id="16b6e-296">Можно изменить владельца этой папки из корневой папки на имя пользователя, которое использовалось при подготовке машины.</span><span class="sxs-lookup"><span data-stu-id="16b6e-296">You can change the ownership of that folder from root to the username you used when you provisioned the machine.</span></span> <span data-ttu-id="16b6e-297">Ниже приведен пример с именем учетной записи azureuser:</span><span class="sxs-lookup"><span data-stu-id="16b6e-297">Here is an example with the azureuser account name:</span></span>  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  <span data-ttu-id="16b6e-298">Кроме того, используйте параметр -R, чтобы применить разрешения для всех файлов в каталоге.</span><span class="sxs-lookup"><span data-stu-id="16b6e-298">Use the -R option to apply the permissions for all files inside of a directory too.</span></span>  

  <span data-ttu-id="16b6e-299">Эта команда также работает для каталогов.</span><span class="sxs-lookup"><span data-stu-id="16b6e-299">This command also works for directories.</span></span> <span data-ttu-id="16b6e-300">Параметр -R изменяет разрешения для всех файлов и каталогов в каталоге.</span><span class="sxs-lookup"><span data-stu-id="16b6e-300">The -R option changes the permissions for all files and directories inside the directory.</span></span> <span data-ttu-id="16b6e-301">Пример:</span><span class="sxs-lookup"><span data-stu-id="16b6e-301">Here is an example:</span></span>  

     sudo chown -R username:group directory  

  <span data-ttu-id="16b6e-302">Эта команда изменяет владельца (как пользователя, так и группу) для всех файлов и каталогов, находящихся внутри каталога.</span><span class="sxs-lookup"><span data-stu-id="16b6e-302">This command changes ownership (both user and group) for all files and directories that are inside the directory.</span></span>  

  <span data-ttu-id="16b6e-303">Следующая команда изменяет только разрешения для каталога папки.</span><span class="sxs-lookup"><span data-stu-id="16b6e-303">The following command only changes the permission of the folder directory.</span></span> <span data-ttu-id="16b6e-304">Файлы и папки внутри каталога не изменяются.</span><span class="sxs-lookup"><span data-stu-id="16b6e-304">The files and folders inside the directory are not changed.</span></span>  

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
