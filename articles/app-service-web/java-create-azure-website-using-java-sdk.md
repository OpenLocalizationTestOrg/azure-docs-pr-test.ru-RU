---
title: "Создание веб-приложения в службе приложений Azure с использованием пакета SDK для Azure для Java"
description: "Узнайте, как программным путем создать веб-приложение в службе приложений Azure, используя пакет SDK для Azure для Java."
tags: azure-classic-portal
services: app-service-web
documentationcenter: Java
author: donntrenton
manager: erikre
editor: jimbe
ms.assetid: 8954c456-1275-4d57-aff4-ca7d6374b71e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/25/2016
ms.author: v-donntr
ms.openlocfilehash: 08bb53de8cf437a5a2b1c3b38bce9f81b8349493
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-the-azure-sdk-for-java"></a><span data-ttu-id="cb07a-103">Создание веб-приложения в службе приложений Azure с использованием пакета SDK для Azure для Java</span><span class="sxs-lookup"><span data-stu-id="cb07a-103">Create a Web App in Azure App Service using the Azure SDK for Java</span></span>
<!-- Azure Active Directory workflow is not yet available on the Azure Portal -->

## <a name="overview"></a><span data-ttu-id="cb07a-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="cb07a-104">Overview</span></span>
<span data-ttu-id="cb07a-105">В этом пошаговом руководстве показано, как создать пакет SDK для Azure для приложения Java, которое создает веб-приложение в [службе приложений Azure][Azure App Service], а затем развернуть в ней приложение.</span><span class="sxs-lookup"><span data-stu-id="cb07a-105">This walkthrough shows you how to create an Azure SDK for Java application that creates a Web App in [Azure App Service][Azure App Service], then deploy an application to it.</span></span> <span data-ttu-id="cb07a-106">Руководство состоит из двух частей:</span><span class="sxs-lookup"><span data-stu-id="cb07a-106">It consists of two parts:</span></span>

* <span data-ttu-id="cb07a-107">в первой части показано, как создать приложение Java, которое позволяет создать веб-приложение;</span><span class="sxs-lookup"><span data-stu-id="cb07a-107">Part 1 demonstrates how to build a Java application that creates a web app.</span></span>
* <span data-ttu-id="cb07a-108">во второй части показано, как создать простое приложение JSP Hello World, а затем использовать FTP-клиент для развертывания кода в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="cb07a-108">Part 2 demonstrates how to create a simple JSP "Hello World" application, then use an FTP client to deploy code to App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb07a-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cb07a-109">Prerequisites</span></span>
### <a name="software-installations"></a><span data-ttu-id="cb07a-110">Установка программного обеспечения</span><span class="sxs-lookup"><span data-stu-id="cb07a-110">Software Installations</span></span>
<span data-ttu-id="cb07a-111">Код приложения AzureWebDemo в этой статье написан с использованием пакета SDK Azure для Java 0.7.0, который можно установить с помощью [установщика веб-платформы (WebPI)][Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="cb07a-111">The AzureWebDemo application code in this article was written using Azure Java SDK 0.7.0, which you can install using the [Web Platform Installer][Web Platform Installer] (WebPI).</span></span> <span data-ttu-id="cb07a-112">Вам также следует убедиться, что вы используете последнюю версию [набора средств Azure для Eclipse][Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="cb07a-112">In addition, make sure to use the latest version of the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="cb07a-113">После установки пакета SDK обновите зависимости в проекте Eclipse, выполнив команду **Update Index** (Обновить индекс) в представлении **Maven Repositories** (Репозитории Maven), а затем снова добавьте последнюю версию каждого пакета в окне **Dependencies** (Зависимости).</span><span class="sxs-lookup"><span data-stu-id="cb07a-113">After you install the SDK, update the dependencies in your Eclipse project by running **Update Index** in **Maven Repositories**, then re-add the latest version of each package in the **Dependencies** window.</span></span> <span data-ttu-id="cb07a-114">Вы можете проверить версию установленного программного обеспечения в Eclipse, щелкнув **Help > Installation Details** (Справка > Подробная информация об установке). Вы увидите по крайней мере следующие версии:</span><span class="sxs-lookup"><span data-stu-id="cb07a-114">You can verify the version of your installed software in Eclipse by clicking **Help > Installation Details**; you should have at least the following versions:</span></span>

* <span data-ttu-id="cb07a-115">пакет для библиотек Microsoft Azure для Java 0.7.0.20150309;</span><span class="sxs-lookup"><span data-stu-id="cb07a-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span></span>
* <span data-ttu-id="cb07a-116">интегрированная среда разработки Eclipse для разработчиков Java EE 4.4.2.20150219.</span><span class="sxs-lookup"><span data-stu-id="cb07a-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span></span>

### <a name="create-and-configure-cloud-resources-in-azure"></a><span data-ttu-id="cb07a-117">Создание и настройка облачных ресурсов в Azure</span><span class="sxs-lookup"><span data-stu-id="cb07a-117">Create and Configure Cloud Resources in Azure</span></span>
<span data-ttu-id="cb07a-118">Прежде чем начать эту процедуру, необходимо убедиться, что у вас есть активная подписка Azure, и настроить Active Directory (AD) по умолчанию в Azure.</span><span class="sxs-lookup"><span data-stu-id="cb07a-118">Before you begin this procedure, you need to have an active Azure subscription and set up a default Active Directory (AD) on Azure.</span></span>

### <a name="create-an-active-directory-ad-in-azure"></a><span data-ttu-id="cb07a-119">Создание Active Directory в Azure</span><span class="sxs-lookup"><span data-stu-id="cb07a-119">Create an Active Directory (AD) in Azure</span></span>
<span data-ttu-id="cb07a-120">Если в вашей подписке Azure еще нет каталога Active Directory (AD), войдите на [классический портал Azure][Azure classic portal] с помощью учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="cb07a-120">If you do not already have an Active Directory (AD) on your Azure subscription, log into the [Azure classic portal][Azure classic portal] with your Microsoft account.</span></span> <span data-ttu-id="cb07a-121">Если у вас несколько подписок, щелкните **Подписки** и выберите каталог по умолчанию для подписки, которая будет использоваться для этого проекта.</span><span class="sxs-lookup"><span data-stu-id="cb07a-121">If you have multiple subscriptions, click **Subscriptions** and select the default directory for the subscription you want to use for this project.</span></span> <span data-ttu-id="cb07a-122">Нажмите кнопку **Применить**, чтобы перейти в представление этой подписки.</span><span class="sxs-lookup"><span data-stu-id="cb07a-122">Then click **Apply** to switch to that subscription view.</span></span>

1. <span data-ttu-id="cb07a-123">В меню слева выберите **Active Directory** .</span><span class="sxs-lookup"><span data-stu-id="cb07a-123">Select **Active Directory** from the menu at left.</span></span> <span data-ttu-id="cb07a-124">Щелкните **Создать > Каталог > Настраиваемое создание**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-124">**Click New > Directory > Custom Create**.</span></span>
2. <span data-ttu-id="cb07a-125">В разделе **Добавить каталог** выберите **Создать каталог**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-125">In **Add Directory**, select **Create New Directory**.</span></span>
3. <span data-ttu-id="cb07a-126">В поле **Имя**введите имя каталога.</span><span class="sxs-lookup"><span data-stu-id="cb07a-126">In **Name**, enter a directory name.</span></span>
4. <span data-ttu-id="cb07a-127">В поле **Домен** введите имя домена.</span><span class="sxs-lookup"><span data-stu-id="cb07a-127">In **Domain**, enter a domain name.</span></span> <span data-ttu-id="cb07a-128">Это имя основного домена, включенное по умолчанию вместе с каталогом. У него такой формат: `<domain_name>.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="cb07a-128">This is a basic domain name that is included by default with your directory; it has the form `<domain_name>.onmicrosoft.com`.</span></span> <span data-ttu-id="cb07a-129">Домен можно назвать на основе имени каталога или имени другого домена, которым вы владеете.</span><span class="sxs-lookup"><span data-stu-id="cb07a-129">You can name it based on the directory name or another domain name that you own.</span></span> <span data-ttu-id="cb07a-130">Позже вы сможете добавить другое доменное имя, которое уже использует ваша организация.</span><span class="sxs-lookup"><span data-stu-id="cb07a-130">Later, you can add another domain name that your organization already uses.</span></span>
5. <span data-ttu-id="cb07a-131">В поле **Страна или регион**выберите свой языковой стандарт.</span><span class="sxs-lookup"><span data-stu-id="cb07a-131">In **Country or region**, select your locale.</span></span>

<span data-ttu-id="cb07a-132">Дополнительную информацию об Active Directory см. в разделе [Что такое каталог Azure AD?][What is an Azure AD directory]</span><span class="sxs-lookup"><span data-stu-id="cb07a-132">For more information on AD, see [What is an Azure AD directory][What is an Azure AD directory]?</span></span>

### <a name="create-a-management-certificate-for-azure"></a><span data-ttu-id="cb07a-133">Создание сертификата управления для Azure</span><span class="sxs-lookup"><span data-stu-id="cb07a-133">Create a Management Certificate for Azure</span></span>
<span data-ttu-id="cb07a-134">Пакет SDK для Azure для Java использует сертификаты управления для аутентификации с использованием подписок Azure.</span><span class="sxs-lookup"><span data-stu-id="cb07a-134">The Azure SDK for Java uses management certificates to authenticate with Azure subscriptions.</span></span> <span data-ttu-id="cb07a-135">Вы используете такие сертификаты, а именно X.509 v3, для аутентификации клиентских приложений, использующих API управления службами для работы от имени владельца подписки с целью управления ресурсами подписки.</span><span class="sxs-lookup"><span data-stu-id="cb07a-135">These are X.509 v3 certificates you use to authenticate a client application that uses the Service Management API to act on behalf of the subscription owner to manage subscription resources.</span></span>

<span data-ttu-id="cb07a-136">Для прохождения аутентификации с помощью Azure код в этой процедуре использует самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="cb07a-136">The code in this procedure uses a self-signed certificate to authenticate with Azure.</span></span> <span data-ttu-id="cb07a-137">Чтобы выполнить эту процедуру, необходимо создать сертификат и заранее передать его на [классический портал Azure][Azure classic portal].</span><span class="sxs-lookup"><span data-stu-id="cb07a-137">For this procedure, you need to create a certificate and upload it to the [Azure classic portal][Azure classic portal] beforehand.</span></span> <span data-ttu-id="cb07a-138">Для этого необходимо выполнить следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="cb07a-138">This involves the following steps:</span></span>

* <span data-ttu-id="cb07a-139">Создайте PFX-файл, представляющий собой сертификат клиента, и сохраните его локально.</span><span class="sxs-lookup"><span data-stu-id="cb07a-139">Generate a PFX file representing your client certificate and save it locally.</span></span>
* <span data-ttu-id="cb07a-140">Создайте сертификат управления (CER-файл) из PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="cb07a-140">Generate a management certificate (CER file) from the PFX file.</span></span>
* <span data-ttu-id="cb07a-141">Загрузите CER-файл в подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="cb07a-141">Upload the CER file to your Azure subscription.</span></span>
* <span data-ttu-id="cb07a-142">Преобразуйте PFX-файл в JKS-файл, так как Java использует этот формат для аутентификации с использованием сертификатов.</span><span class="sxs-lookup"><span data-stu-id="cb07a-142">Convert the PFX file into JKS, because Java uses that format to authenticate using certificates.</span></span>
* <span data-ttu-id="cb07a-143">Напишите код для аутентификации приложения, связанный с локальным JKS-файлом.</span><span class="sxs-lookup"><span data-stu-id="cb07a-143">Write the application's authentication code, which refers to the local JKS file.</span></span>

<span data-ttu-id="cb07a-144">При выполнении этой процедуры CER-сертификат будет находиться в подписке Azure, а JKS-сертификат — на локальном диске.</span><span class="sxs-lookup"><span data-stu-id="cb07a-144">When you complete this procedure, the CER certificate will reside in your Azure subscription and the JKS certificate will reside on your local drive.</span></span> <span data-ttu-id="cb07a-145">Дополнительную информацию о сертификатах управления см. в разделе [Создание и передача сертификата управления для Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="cb07a-145">For more information on management certificates, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="create-a-certificate"></a><span data-ttu-id="cb07a-146">Создание сертификата</span><span class="sxs-lookup"><span data-stu-id="cb07a-146">Create a certificate</span></span>
<span data-ttu-id="cb07a-147">Чтобы создать самозаверяющий сертификат, откройте консоль командной строки в своей операционной системе и выполните следующие команды.</span><span class="sxs-lookup"><span data-stu-id="cb07a-147">To create your own self-signed certificate, open a command console on your operating system and run the following commands.</span></span>

> <span data-ttu-id="cb07a-148">**Примечание.** На компьютере, где вы будете выполнять эту команду, должен быть установлен пакет JDK.</span><span class="sxs-lookup"><span data-stu-id="cb07a-148">**Note:**  The computer on which you run this command must have the JDK installed.</span></span> <span data-ttu-id="cb07a-149">Кроме того, путь к keytool зависит от расположения, в котором установлен этот пакет.</span><span class="sxs-lookup"><span data-stu-id="cb07a-149">Also, the path to the keytool depends on the location in which you install the JDK.</span></span> <span data-ttu-id="cb07a-150">Дополнительную информацию см. в разделе [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] (Инструмент управления сертификатами и ключом (keytool)) онлайн-документации по Java.</span><span class="sxs-lookup"><span data-stu-id="cb07a-150">For more information, see [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] in the Java online docs.</span></span>
> 
> 

<span data-ttu-id="cb07a-151">Чтобы создать PFX-файл, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="cb07a-151">To create the .pfx file:</span></span>

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

<span data-ttu-id="cb07a-152">Чтобы создать CER-файл, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="cb07a-152">To create the .cer file:</span></span>

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

<span data-ttu-id="cb07a-153">где:</span><span class="sxs-lookup"><span data-stu-id="cb07a-153">where:</span></span>

* <span data-ttu-id="cb07a-154">`<java-install-dir>` — это путь к каталогу, в котором установлено приложение Java;</span><span class="sxs-lookup"><span data-stu-id="cb07a-154">`<java-install-dir>` is the path to the directory in which you installed Java.</span></span>
* <span data-ttu-id="cb07a-155">`<keystore-id>` — это идентификатор записи в хранилище ключей (например, `AzureRemoteAccess`);</span><span class="sxs-lookup"><span data-stu-id="cb07a-155">`<keystore-id>` is the keystore entry identifier (for example, `AzureRemoteAccess`).</span></span>
* <span data-ttu-id="cb07a-156">`<cert-store-dir>` — это путь к каталогу, в котором вам необходимо хранить сертификаты (например, `C:/Certificates`);</span><span class="sxs-lookup"><span data-stu-id="cb07a-156">`<cert-store-dir>` is the path to the directory in which you want to store certificates (for example `C:/Certificates`).</span></span>
* <span data-ttu-id="cb07a-157">`<cert-file-name>` — это имя файла сертификата (например, `AzureWebDemoCert`);</span><span class="sxs-lookup"><span data-stu-id="cb07a-157">`<cert-file-name>` is the name of the certificate file (for example `AzureWebDemoCert`).</span></span>
* <span data-ttu-id="cb07a-158">`<password>` — это пароль, выбранный для защиты сертификата. Он должен состоять по крайней мере из 6 символов.</span><span class="sxs-lookup"><span data-stu-id="cb07a-158">`<password>` is the password you choose to protect the certificate; it must be at least 6 characters long.</span></span> <span data-ttu-id="cb07a-159">Вы можете вовсе не указывать пароль, хотя это не рекомендуется;</span><span class="sxs-lookup"><span data-stu-id="cb07a-159">You can enter no password, although this is not recommended.</span></span>
* <span data-ttu-id="cb07a-160">`<dname>` — различающееся имя X.500, которое необходимо связать с псевдонимом. Оно используется в полях издателя и субъекта самозаверяющего сертификата.</span><span class="sxs-lookup"><span data-stu-id="cb07a-160">`<dname>` is the X.500 Distinguished Name to be associated with alias, and is used as the issuer and subject fields in the self-signed certificate.</span></span>

<span data-ttu-id="cb07a-161">Дополнительные сведения см. в статье [Общие сведения о сертификатах для облачных служб Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="cb07a-161">For more information, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="upload-the-certificate"></a><span data-ttu-id="cb07a-162">Загрузка сертификата</span><span class="sxs-lookup"><span data-stu-id="cb07a-162">Upload the certificate</span></span>
<span data-ttu-id="cb07a-163">Чтобы отправить самозаверяющий сертификат в Azure, перейдите на страницу **Параметры** на классическом портале, а затем щелкните вкладку **Сертификаты управления**. Щелкните **Загрузить** в нижней части страницы и перейдите к расположению CER-файла, который вы создали.</span><span class="sxs-lookup"><span data-stu-id="cb07a-163">To upload a self-signed certificate to Azure, go to the **Settings** page in the classic portal, then click the **Management Certificates** tab. Click **Upload** at the bottom of the page and navigate to the location of the CER file you created.</span></span>

#### <a name="convert-the-pfx-file-into-jks"></a><span data-ttu-id="cb07a-164">Преобразование PFX-файла в JKS-файл</span><span class="sxs-lookup"><span data-stu-id="cb07a-164">Convert the PFX file into JKS</span></span>
<span data-ttu-id="cb07a-165">В командной строке Windows (ее следует запустить под учетной записью администратора) перейдите в каталог, в котором содержатся сертификаты, и выполните следующую команду, где `<java-install-dir>` — это каталог с установленным приложением Java:</span><span class="sxs-lookup"><span data-stu-id="cb07a-165">In the Windows Command Prompt (running as admin), cd to the directory containing the certificates and run the following command, where `<java-install-dir>` is the directory in which you installed Java on your computer:</span></span>

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. <span data-ttu-id="cb07a-166">При появлении запроса введите пароль назначения для хранилища ключей, который будет паролем JKS-файла.</span><span class="sxs-lookup"><span data-stu-id="cb07a-166">When prompted, enter the destination keystore password; this will be the password for the JKS file.</span></span>
2. <span data-ttu-id="cb07a-167">При появлении запроса введите исходный пароль хранилища ключей. Это пароль, который вы указали для PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="cb07a-167">When prompted, enter the source keystore password; this is the password you specified for the PFX file.</span></span>

<span data-ttu-id="cb07a-168">Эти два пароля могут не совпадать.</span><span class="sxs-lookup"><span data-stu-id="cb07a-168">The two passwords do not have to be the same.</span></span> <span data-ttu-id="cb07a-169">Вы можете вовсе не указывать пароль, хотя это не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="cb07a-169">You can enter no password, although this is not recommended.</span></span>

## <a name="build-a-web-app-creation-application"></a><span data-ttu-id="cb07a-170">Сборка приложения для создания веб-приложения</span><span class="sxs-lookup"><span data-stu-id="cb07a-170">Build a Web App creation application</span></span>
### <a name="create-the-eclipse-workspace-and-maven-project"></a><span data-ttu-id="cb07a-171">Создание рабочей области Eclipse и проекта Maven</span><span class="sxs-lookup"><span data-stu-id="cb07a-171">Create the Eclipse Workspace and Maven Project</span></span>
<span data-ttu-id="cb07a-172">В этом разделе вы создадите рабочую область и проект Maven для приложения, создающего веб-приложение AzureWebDemo.</span><span class="sxs-lookup"><span data-stu-id="cb07a-172">In this section you create a workspace and a Maven project for the web app creation application, named AzureWebDemo.</span></span>

1. <span data-ttu-id="cb07a-173">Создайте проект Maven.</span><span class="sxs-lookup"><span data-stu-id="cb07a-173">Create a new Maven project.</span></span> <span data-ttu-id="cb07a-174">Щелкните **File > New > Maven Project** (Файл > Создать > Проект Maven).</span><span class="sxs-lookup"><span data-stu-id="cb07a-174">Click **File > New > Maven Project**.</span></span> <span data-ttu-id="cb07a-175">На странице **New Maven Project** (Новый проект Maven) выберите **Create a simple project** (Создать простой проект) и **Use default workspace location** (Использовать расположение рабочей области по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="cb07a-175">In **New Maven Project**, select **Create a simple project** and **Use default workspace location**.</span></span>
2. <span data-ttu-id="cb07a-176">На второй странице **Новый проект Maven**укажите следующее:</span><span class="sxs-lookup"><span data-stu-id="cb07a-176">On the second page of **New Maven Project**, specify the following:</span></span>
   
   * <span data-ttu-id="cb07a-177">идентификатор группы — `com.<username>.azure.webdemo`</span><span class="sxs-lookup"><span data-stu-id="cb07a-177">Group ID: `com.<username>.azure.webdemo`</span></span>
   * <span data-ttu-id="cb07a-178">идентификатор артефакта — AzureWebDemo;</span><span class="sxs-lookup"><span data-stu-id="cb07a-178">Artifact ID: AzureWebDemo</span></span>
   * <span data-ttu-id="cb07a-179">версия— 0.0.1-SNAPSHOT;</span><span class="sxs-lookup"><span data-stu-id="cb07a-179">Version: 0.0.1-SNAPSHOT</span></span>
   * <span data-ttu-id="cb07a-180">упаковка — JAR;</span><span class="sxs-lookup"><span data-stu-id="cb07a-180">Packaging: jar</span></span>
   * <span data-ttu-id="cb07a-181">имя — AzureWebDemo.</span><span class="sxs-lookup"><span data-stu-id="cb07a-181">Name: AzureWebDemo</span></span>
     
     <span data-ttu-id="cb07a-182">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="cb07a-182">Click **Finish**.</span></span>
3. <span data-ttu-id="cb07a-183">Откройте файл нового проекта pom.xml в обозревателе проектов.</span><span class="sxs-lookup"><span data-stu-id="cb07a-183">Open the new project's pom.xml file in Project Explorer.</span></span> <span data-ttu-id="cb07a-184">Выберите вкладку **Зависимости** . Так как это новый проект, здесь еще нет списка пакетов.</span><span class="sxs-lookup"><span data-stu-id="cb07a-184">Select the **Dependencies** tab. As this is a new project, no packages are listed yet.</span></span>
4. <span data-ttu-id="cb07a-185">Откройте представление «Репозитории Maven».</span><span class="sxs-lookup"><span data-stu-id="cb07a-185">Open the Maven Repositories view.</span></span> <span data-ttu-id="cb07a-186">Щелкните **Window > Show View > Other > Maven > Maven Repositories** (Окно > Показать представление > Другие > Maven > Репозитории Maven) и нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-186">**Click Window > Show View > Other > Maven > Maven Repositories** and click **OK**.</span></span> <span data-ttu-id="cb07a-187">Представление **Репозитории Maven** будет отображаться в нижней части интегрированной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="cb07a-187">The **Maven Repositories** view will appear at the bottom of the IDE.</span></span>
5. <span data-ttu-id="cb07a-188">Откройте представление **Global Repositories** (Глобальные репозитории), щелкните правой кнопкой мыши **central** (центральный репозиторий), а затем щелкните **Rebuild Index** (Перестроить индекс).</span><span class="sxs-lookup"><span data-stu-id="cb07a-188">Open **Global Repositories**, right-click the **central** repository, and select **Rebuild Index**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="cb07a-189">Выполнение этого шага может длиться несколько минут в зависимости от скорости подключения.</span><span class="sxs-lookup"><span data-stu-id="cb07a-189">This step can take several minutes depending on the speed of your connection.</span></span> <span data-ttu-id="cb07a-190">Когда индекс перестроится, вы увидите пакеты Microsoft Azure в **центральном** репозитори Maven.</span><span class="sxs-lookup"><span data-stu-id="cb07a-190">When the index rebuilds, you should see the Microsoft Azure packages in the **central** Maven repository.</span></span>
6. <span data-ttu-id="cb07a-191">На вкладке **Dependencies** (Зависимости) щелкните **Add** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="cb07a-191">In **Dependencies**, click **Add**.</span></span> <span data-ttu-id="cb07a-192">В поле **Enter Group ID…** (Введите идентификатор группы…) введите `azure-management`.</span><span class="sxs-lookup"><span data-stu-id="cb07a-192">In **Enter Group ID...** enter `azure-management`.</span></span> <span data-ttu-id="cb07a-193">Выберите пакеты для базового управления и управления веб-приложениями службы приложений:</span><span class="sxs-lookup"><span data-stu-id="cb07a-193">Select the packages for base management and App Service Web Apps management:</span></span>
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > <span data-ttu-id="cb07a-194">**Примечание.** При обновлении зависимостей после выпуска новой версии в этот список необходимо повторно добавить все зависимости.</span><span class="sxs-lookup"><span data-stu-id="cb07a-194">**Note:** If you are updating the dependencies after a new version release, you need to re-add each of the dependencies in this list.</span></span>
   > <span data-ttu-id="cb07a-195">После того как вы щелкнете **Add** (Добавить) и выберете зависимости, они будут отображаться с номером новой версии в списке **Dependencies** (Зависимости).</span><span class="sxs-lookup"><span data-stu-id="cb07a-195">After you click **Add** and select each dependency, it appears with the new version number in the **Dependencies** list.</span></span>
   > 
   > 

<span data-ttu-id="cb07a-196">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-196">Click **OK**.</span></span> <span data-ttu-id="cb07a-197">После этого в списке **Зависимости** будут отображаться пакеты Azure.</span><span class="sxs-lookup"><span data-stu-id="cb07a-197">The Azure packages then appear in the **Dependencies** list.</span></span>

### <a name="writing-java-code-to-create-a-web-app-by-calling-the-azure-sdk"></a><span data-ttu-id="cb07a-198">Написание кода Java для создания веб-приложения путем вызова пакета SDK для Azure</span><span class="sxs-lookup"><span data-stu-id="cb07a-198">Writing Java Code to Create a Web App by Calling the Azure SDK</span></span>
<span data-ttu-id="cb07a-199">Теперь напишите код, который вызывает API в пакете SDK для Azure для Java, чтобы создать веб-приложение службы приложений.</span><span class="sxs-lookup"><span data-stu-id="cb07a-199">Next, write the code that calls APIs in the Azure SDK for Java to create the App Service web app.</span></span>

1. <span data-ttu-id="cb07a-200">Создайте класс Java, который будет содержать код главной точки входа.</span><span class="sxs-lookup"><span data-stu-id="cb07a-200">Create a Java class to contain the main entry point code.</span></span> <span data-ttu-id="cb07a-201">В обозревателе проектов щелкните узел проекта правой кнопкой мыши и выберите **Создать > Класс**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-201">In Project Explorer, right-click on the project node and select **New > Class**.</span></span>
2. <span data-ttu-id="cb07a-202">В окне **Новый класс Java`WebCreator` укажите имя класса** и установите флажок **public static void main**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-202">In **New Java Class**, name the class `WebCreator` and check the **public static void main** checkbox.</span></span> <span data-ttu-id="cb07a-203">Значения выбранных параметров должны выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="cb07a-203">The selections should appear as follows:</span></span>
   
    ![][2]
3. <span data-ttu-id="cb07a-204">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="cb07a-204">Click **Finish**.</span></span> <span data-ttu-id="cb07a-205">В обозревателе проектов отобразится файл WebCreator.java.</span><span class="sxs-lookup"><span data-stu-id="cb07a-205">The WebCreator.java file appears in Project Explorer.</span></span>

### <a name="calling-the-azure-api-to-create-an-app-service-web-app"></a><span data-ttu-id="cb07a-206">Вызов API Azure для создания веб-приложения службы приложений</span><span class="sxs-lookup"><span data-stu-id="cb07a-206">Calling the Azure API to Create an App Service Web App</span></span>
#### <a name="add-necessary-imports"></a><span data-ttu-id="cb07a-207">Добавление необходимых операций импорта</span><span class="sxs-lookup"><span data-stu-id="cb07a-207">Add necessary imports</span></span>
<span data-ttu-id="cb07a-208">Добавьте следующие операции импорта в файл WebCreator.java. Эти операции позволяют получить доступ к классам в библиотеках управления для используемых API Azure:</span><span class="sxs-lookup"><span data-stu-id="cb07a-208">In WebCreator.java, add the following imports; these imports provide access to classes in the management libraries for consuming Azure APIs:</span></span>

    // General imports
    import java.net.URI;
    import java.util.ArrayList;

    // Imports for Exceptions
    import java.io.IOException;
    import java.net.URISyntaxException;
    import javax.xml.parsers.ParserConfigurationException;
    import com.microsoft.windowsazure.exception.ServiceException;
    import org.xml.sax.SAXException;

    // Imports for Azure App Service management configuration
    import com.microsoft.windowsazure.Configuration;
    import com.microsoft.windowsazure.management.configuration.ManagementConfiguration;

    // Service management imports for App Service Web Apps creation
    import com.microsoft.windowsazure.management.websites.*;
    import com.microsoft.windowsazure.management.websites.models.*;

    // Imports for authentication
    import com.microsoft.windowsazure.core.utils.KeyStoreType;


#### <a name="define-the-main-entry-point-class"></a><span data-ttu-id="cb07a-209">Определение класса главной точки входа</span><span class="sxs-lookup"><span data-stu-id="cb07a-209">Define the main entry point class</span></span>
<span data-ttu-id="cb07a-210">Так как приложение AzureWebDemo предназначено для создания веб-приложения службы приложений, назовите основной класс для этого приложения — `WebAppCreator`.</span><span class="sxs-lookup"><span data-stu-id="cb07a-210">Because the purpose of the AzureWebDemo application is to create an App Service Web App, name the main class for this application `WebAppCreator`.</span></span> <span data-ttu-id="cb07a-211">Этот класс предоставляет код главной точки входа, который вызывает API управления службами Azure для создания веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="cb07a-211">This class provides the main entry point code that calls the Azure Service Management API to create the web app.</span></span>

<span data-ttu-id="cb07a-212">Добавьте следующие определения параметров для веб-приложения и веб-пространства.</span><span class="sxs-lookup"><span data-stu-id="cb07a-212">Add the following parameter definitions for the web app and webspace.</span></span> <span data-ttu-id="cb07a-213">Вам понадобиться указать идентификатор подписки Azure и информацию о сертификате.</span><span class="sxs-lookup"><span data-stu-id="cb07a-213">You will need to provide your own Azure subscription ID and certificate information.</span></span>

    public class WebAppCreator {

        // Parameter definitions used for authentication.
        private static String uri = "https://management.core.windows.net/";
        private static String subscriptionId = "<subscription-id>";
        private static String keyStoreLocation = "<certificate-store-path>";
        private static String keyStorePassword = "<certificate-password>";

        // Define web app parameter values.
        private static String webAppName = "WebDemoWebApp";
        private static String domainName = ".azurewebsites.net";
        private static String webSpaceName = WebSpaceNames.WESTUSWEBSPACE;
        private static String appServicePlanName = "WebDemoAppServicePlan";

<span data-ttu-id="cb07a-214">где:</span><span class="sxs-lookup"><span data-stu-id="cb07a-214">where:</span></span>

* <span data-ttu-id="cb07a-215">`<subscription-id>` — это идентификатор подписки Azure, в рамках которой нужно создать группу ресурсов;</span><span class="sxs-lookup"><span data-stu-id="cb07a-215">`<subscription-id>` is the Azure subscription ID in which you want to create the resource.</span></span>
* <span data-ttu-id="cb07a-216">`<certificate-store-path>` — это путь и имя JKS-файла в каталоге локального хранилища сертификатов</span><span class="sxs-lookup"><span data-stu-id="cb07a-216">`<certificate-store-path>` is the path and filename to the JKS file in your local certificate store directory.</span></span> <span data-ttu-id="cb07a-217">(например, `C:/Certificates/CertificateName.jks` — для Linux, а `C:\Certificates\CertificateName.jks` — для Windows);</span><span class="sxs-lookup"><span data-stu-id="cb07a-217">For example, `C:/Certificates/CertificateName.jks` for Linux and `C:\Certificates\CertificateName.jks` for Windows.</span></span>
* <span data-ttu-id="cb07a-218">`<certificate-password>` — это пароль, указанный при создании JKS-сертификата;</span><span class="sxs-lookup"><span data-stu-id="cb07a-218">`<certificate-password>` is the password you specified when you created your JKS certificate.</span></span>
* <span data-ttu-id="cb07a-219">в качестве `webAppName` можно указать любое имя. В этой процедуре используется имя `WebDemoWebApp`.</span><span class="sxs-lookup"><span data-stu-id="cb07a-219">`webAppName` can be any name you choose; this procedure uses the name `WebDemoWebApp`.</span></span> <span data-ttu-id="cb07a-220">Полное доменное имя — `webAppName`, к которому добавлено `domainName`, поэтому в этом случае полное имя домена — `webdemowebapp.azurewebsites.net`;</span><span class="sxs-lookup"><span data-stu-id="cb07a-220">The full domain name is the `webAppName` with the `domainName` appended, so in this case the full domain is `webdemowebapp.azurewebsites.net`.</span></span>
* <span data-ttu-id="cb07a-221">`domainName` следует указать, как показано выше;</span><span class="sxs-lookup"><span data-stu-id="cb07a-221">`domainName` should be specified as shown above.</span></span>
* <span data-ttu-id="cb07a-222">для `webSpaceName` следует указать одно из значений, определенных в классе [WebSpaceNames][WebSpaceNames];</span><span class="sxs-lookup"><span data-stu-id="cb07a-222">`webSpaceName` should be one of the values defined in the [WebSpaceNames][WebSpaceNames] class.</span></span>
* <span data-ttu-id="cb07a-223">`appServicePlanName` следует указать, как показано выше;</span><span class="sxs-lookup"><span data-stu-id="cb07a-223">`appServicePlanName` should be specified as shown above.</span></span>

> <span data-ttu-id="cb07a-224">**Примечание.** При каждом запуске этого приложения необходимо изменять значения `webAppName` и `appServicePlanName` (или удалять веб-приложение на портале Azure), прежде чем запускать его повторно.</span><span class="sxs-lookup"><span data-stu-id="cb07a-224">**Note:** Each time you run this application, you need to change the value of `webAppName` and `appServicePlanName` (or delete the web app on the Azure Portal) before running the application again.</span></span> <span data-ttu-id="cb07a-225">В противном случае произойдет сбой выполнения, так как в Azure уже есть такой же ресурс.</span><span class="sxs-lookup"><span data-stu-id="cb07a-225">Otherwise, execution will fail because the same resource already exists on Azure.</span></span>
> 
> 

#### <a name="define-the-web-creation-method"></a><span data-ttu-id="cb07a-226">Определение метода создания веб-приложения</span><span class="sxs-lookup"><span data-stu-id="cb07a-226">Define the web creation method</span></span>
<span data-ttu-id="cb07a-227">Далее следует определить метод создания веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="cb07a-227">Next, define a method to create the web app.</span></span> <span data-ttu-id="cb07a-228">Метод `createWebApp` указывает параметры веб-приложения и веб-пространства.</span><span class="sxs-lookup"><span data-stu-id="cb07a-228">This method, `createWebApp`, specifies the parameters of the web app and the webspace.</span></span> <span data-ttu-id="cb07a-229">Он также создает и настраивает клиент управления веб-приложениями службы приложений, определенный объектом [WebSiteManagementClient][WebSiteManagementClient].</span><span class="sxs-lookup"><span data-stu-id="cb07a-229">It also creates and configures the App Service Web Apps management client, which is defined by the [WebSiteManagementClient][WebSiteManagementClient] object.</span></span> <span data-ttu-id="cb07a-230">Клиент управления — это ключ к созданию веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="cb07a-230">The management client is key to creating Web Apps.</span></span> <span data-ttu-id="cb07a-231">Он позволяет использовать веб-службы RESTful, которые, в свою очередь, позволяют приложениям управлять веб-приложениями (операции создания, обновления и удаления), вызывая API управления службами.</span><span class="sxs-lookup"><span data-stu-id="cb07a-231">It provides RESTful web services that allow applications to manage web apps (performing operations such as create, update, and delete) by calling the service management API.</span></span>

    private static void createWebApp() throws Exception {

        // Specify configuration settings for the App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path to the JKS file
            keyStorePassword,  // Password for the JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create the App Service Web Apps management client to call Azure APIs
        // and pass it the App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for the web app with the specified parameters.
        WebHostingPlanCreateParameters appServicePlanParams = new WebHostingPlanCreateParameters();
        appServicePlanParams.setName(appServicePlanName);
        appServicePlanParams.setSKU(SkuOptions.Free);
        webAppManagementClient.getWebHostingPlansOperations().create(webSpaceName, appServicePlanParams);

        // Set webspace parameters.
        WebSiteCreateParameters.WebSpaceDetails webSpaceDetails = new WebSiteCreateParameters.WebSpaceDetails();
        webSpaceDetails.setGeoRegion(GeoRegionNames.WESTUS);
        webSpaceDetails.setPlan(WebSpacePlanNames.VIRTUALDEDICATEDPLAN);
        webSpaceDetails.setName(webSpaceName);

        // Set web app parameters.
        // Note that the server farm name takes the Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define the web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create the web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output the HTTP status code of the response; 200 indicates the request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output the name of the web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

<span data-ttu-id="cb07a-232">Код будет выводить состояние HTTP из ответа. Это состояние будет свидетельствовать об успешном выполнении или сбое. В случае успешного выполнения выводится имя созданного веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="cb07a-232">The code will output the HTTP status of the response indicating success or failure, and if successful, will output the name of the created web app.</span></span>

#### <a name="define-the-main-method"></a><span data-ttu-id="cb07a-233">Определение метода main()</span><span class="sxs-lookup"><span data-stu-id="cb07a-233">Define the main() method</span></span>
<span data-ttu-id="cb07a-234">Укажите код метода main(), который вызывает createWebApp() для создания веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="cb07a-234">Provide the main() method code that calls createWebApp() to create the web app.</span></span>

<span data-ttu-id="cb07a-235">Наконец, вызовите `createWebApp` из `main`:</span><span class="sxs-lookup"><span data-stu-id="cb07a-235">Finally, call `createWebApp` from `main`:</span></span>

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-the-application-and-verify-web-app-creation"></a><span data-ttu-id="cb07a-236">Запуск приложения и проверка созданного веб-приложения</span><span class="sxs-lookup"><span data-stu-id="cb07a-236">Run the application and verify web app creation</span></span>
<span data-ttu-id="cb07a-237">Чтобы убедиться, что приложение работает, щелкните **Запуск > Запустить**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-237">To verify that your application runs, click **Run > Run**.</span></span> <span data-ttu-id="cb07a-238">После завершения работы приложения вы увидите следующие выходные данные в консоли Eclipse:</span><span class="sxs-lookup"><span data-stu-id="cb07a-238">When the application completes running, you should see the following output in the Eclipse console:</span></span>

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

<span data-ttu-id="cb07a-239">Войдите на классический портал Azure и щелкните **Веб-приложения**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-239">Log into the Azure classic portal and click **Web Apps**.</span></span> <span data-ttu-id="cb07a-240">Через несколько минут в списке «Веб-приложения» должно отобразиться новое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="cb07a-240">The new web app should appear in the Web Apps list within a few minutes.</span></span>

## <a name="deploying-an-application-to-the-web-app"></a><span data-ttu-id="cb07a-241">Развертывание приложения в веб-приложение</span><span class="sxs-lookup"><span data-stu-id="cb07a-241">Deploying an Application to the Web App</span></span>
<span data-ttu-id="cb07a-242">После того, как вы запустили AzureWebDemo и создали веб-приложение, войдите на классический портал, щелкните **Веб-приложения**и выберите **WebDemoWebApp** in the **Веб-приложения** .</span><span class="sxs-lookup"><span data-stu-id="cb07a-242">After you have run AzureWebDemo and created the new web app, log into the classic portal, click **Web Apps**, and select **WebDemoWebApp** in the **Web Apps** list.</span></span> <span data-ttu-id="cb07a-243">На странице панели мониторинга веб-приложения щелкните **Обзор** (или щелкните URL-адрес `webdemowebapp.azurewebsites.net`) для перехода.</span><span class="sxs-lookup"><span data-stu-id="cb07a-243">In the web app's dashboard page, click **Browse** (or click the URL, `webdemowebapp.azurewebsites.net`) to navigate to it.</span></span> <span data-ttu-id="cb07a-244">Вы увидите пустую страницу заполнителя, так как в веб-приложении еще не опубликовали никакого содержимого.</span><span class="sxs-lookup"><span data-stu-id="cb07a-244">You will see a blank placeholder page, because no content has been published to the web app yet.</span></span>

<span data-ttu-id="cb07a-245">Далее мы создадим приложение Hello World и развернем его в веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="cb07a-245">Next you will create a "Hello World" application and deploy it to the web app.</span></span>

### <a name="create-a-jsp-hello-world-application"></a><span data-ttu-id="cb07a-246">Создание приложения JSP Hello World</span><span class="sxs-lookup"><span data-stu-id="cb07a-246">Create a JSP Hello World application</span></span>
#### <a name="create-the-application"></a><span data-ttu-id="cb07a-247">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="cb07a-247">Create the application</span></span>
<span data-ttu-id="cb07a-248">Чтобы продемонстрировать то, как развернуть приложение в веб-приложение, далее описывается процедура создания простого приложения Java Hello World и его загрузки в веб-приложение службы приложений, которое создано с помощью вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="cb07a-248">In order to demonstrate how to deploy an application to the web, the following procedure shows you how to create a simple "Hello World" Java application and upload it to the App Service Web App that your application created.</span></span>

1. <span data-ttu-id="cb07a-249">Щелкните **File > New > Dynamic Web Project** (Файл > Создать > Динамический веб-проект).</span><span class="sxs-lookup"><span data-stu-id="cb07a-249">Click **File > New > Dynamic Web Project**.</span></span> <span data-ttu-id="cb07a-250">Назовите его `JSPHello`.</span><span class="sxs-lookup"><span data-stu-id="cb07a-250">Name it `JSPHello`.</span></span> <span data-ttu-id="cb07a-251">В этом диалоговом окне не нужно менять никакие другие настройки.</span><span class="sxs-lookup"><span data-stu-id="cb07a-251">You do not need to change any other settings in this dialog.</span></span> <span data-ttu-id="cb07a-252">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="cb07a-252">Click **Finish**.</span></span>
   
    ![][3]
2. <span data-ttu-id="cb07a-253">В обозревателе проектов разверните проект **JSPHello**, щелкните правой кнопкой мыши **WebContent**, а затем щелкните **New > JSP File** (Создать > JSP-файл).</span><span class="sxs-lookup"><span data-stu-id="cb07a-253">In Project Explorer, expand the **JSPHello** project, right-click **WebContent**, then click **New > JSP File**.</span></span> <span data-ttu-id="cb07a-254">В диалоговом окне «Создание JSP-файла» укажите имя для нового файла `index.jsp`.</span><span class="sxs-lookup"><span data-stu-id="cb07a-254">In the New JSP File dialog, name the new file `index.jsp`.</span></span> <span data-ttu-id="cb07a-255">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-255">Click **Next**.</span></span>
3. <span data-ttu-id="cb07a-256">В диалоговом окне **Select JSP Template** (Выбор шаблона JSP) выберите **New JSP File (html)** (Новый JSP-файл (HTML)) и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-256">In the **Select JSP Template** dialog, select **New JSP File (html)** and click **Finish**.</span></span>
4. <span data-ttu-id="cb07a-257">В файле index.jsp добавьте следующий код в разделы с тегами `<head>` и `<body>`:</span><span class="sxs-lookup"><span data-stu-id="cb07a-257">In index.jsp, add the following code in the `<head>` and `<body>` tag sections:</span></span>
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, the time is <%= date %> 
        </body>

#### <a name="run-the-hello-world-application-in-localhost"></a><span data-ttu-id="cb07a-258">Запуск приложения Hello World на localhost</span><span class="sxs-lookup"><span data-stu-id="cb07a-258">Run the Hello World application in localhost</span></span>
<span data-ttu-id="cb07a-259">Перед запуском этого приложения необходимо настроить некоторые свойства.</span><span class="sxs-lookup"><span data-stu-id="cb07a-259">Before you run this application, you need to configure a few properties.</span></span>

1. <span data-ttu-id="cb07a-260">Щелкните правой кнопкой мыши проект **JSPHello** и выберите пункт **Properties** (Свойства).</span><span class="sxs-lookup"><span data-stu-id="cb07a-260">Right-click the **JSPHello** project and select **Properties**.</span></span>
2. <span data-ttu-id="cb07a-261">В диалоговом окне **Properties** (Свойства) выберите **Java Build Path** (Путь сборки Java), щелкните вкладку **Order and Export** (Порядок и экспорт) и установите флажок **JRE System Library** (Системная библиотека JRE), а затем щелкните **Up** (Вверх), чтобы переместить библиотеку в начало списка.</span><span class="sxs-lookup"><span data-stu-id="cb07a-261">In the **Properties** dialog: select **Java Build Path**, select the **Order and Export** tab, check **JRE System Library**, then click **Up** to move it to the top of the list.</span></span>
   
    ![][4]
3. <span data-ttu-id="cb07a-262">В диалоговом окне **Properties** (Свойства) выберите **Targeted Runtimes** (Целевые среды выполнения) и щелкните **New** (Создать).</span><span class="sxs-lookup"><span data-stu-id="cb07a-262">Also in the **Properties** dialog: select **Targeted Runtimes** and click **New**.</span></span>
4. <span data-ttu-id="cb07a-263">В диалоговом окне **New Server Runtime Environment** (Создание среды выполнения сервера) выберите сервер, например **Apache Tomcat v7.0**, и щелкните **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="cb07a-263">In the **New Server Runtime Environment** dialog, select a server such as **Apache Tomcat v7.0** and click **Next**.</span></span> <span data-ttu-id="cb07a-264">В диалоговом окне **Tomcat Server** (Сервер Tomcat) в поле **Name** (Имя) задайте `Apache Tomcat v7.0`, а в поле **Tomcat Installation Directory** (Каталог установки Tomcat) — каталог с установленной версией сервера Tomcat, которую необходимо использовать.</span><span class="sxs-lookup"><span data-stu-id="cb07a-264">In the **Tomcat Server** dialog, set **Name** to `Apache Tomcat v7.0`, and set **Tomcat Installation Directory** to the directory in which you installed the version of Tomcat server you want to use.</span></span>
   
    ![][5]
   
    <span data-ttu-id="cb07a-265">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="cb07a-265">Click **Finish**.</span></span>
5. <span data-ttu-id="cb07a-266">Затем вернитесь на страницу **Targeted Runtimes** (Целевые среды выполнения) диалогового окна **Properties** (Свойства).</span><span class="sxs-lookup"><span data-stu-id="cb07a-266">You then return to the **Targeted Runtimes** page of the **Properties** dialog.</span></span> <span data-ttu-id="cb07a-267">Выберите **Apache Tomcat v7.0** и нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-267">Select **Apache Tomcat v7.0**, then click **OK**.</span></span>
   
    ![][6]
6. <span data-ttu-id="cb07a-268">В Eclipse в меню **Run** (Запуск) щелкните **Run** (Запустить).</span><span class="sxs-lookup"><span data-stu-id="cb07a-268">In the Eclipse **Run** menu, click **Run**.</span></span> <span data-ttu-id="cb07a-269">В диалоговом окне **Run As** (Запустить как) выберите **Run on Server** (Запустить на сервере).</span><span class="sxs-lookup"><span data-stu-id="cb07a-269">In the **Run As** dialog, select **Run on Server**.</span></span> <span data-ttu-id="cb07a-270">В диалоговом окне **Run on Server** (Запустить на сервере) выберите **Tomcat v7.0 Server** (Сервер Tomcat версии 7.0):</span><span class="sxs-lookup"><span data-stu-id="cb07a-270">In the **Run on Server** dialog, select **Tomcat v7.0 Server**:</span></span>
   
    ![][7]
   
    <span data-ttu-id="cb07a-271">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="cb07a-271">Click **Finish**.</span></span>
7. <span data-ttu-id="cb07a-272">Когда приложение запустится, вы увидите страницу **JSPHello`http://localhost:8080/JSPHello/` в окне localhost в Eclipse (**), где будет отображаться следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="cb07a-272">When the application runs, you should see the **JSPHello** page appear in a localhost window in Eclipse (`http://localhost:8080/JSPHello/`), displaying the following message:</span></span>
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-the-application-as-a-war"></a><span data-ttu-id="cb07a-273">Экспорт приложения в виде WAR-файла</span><span class="sxs-lookup"><span data-stu-id="cb07a-273">Export the application as a WAR</span></span>
<span data-ttu-id="cb07a-274">Экспортируйте файлы веб-проектов в виде файлов веб-архивов (WAR-файлов), чтобы вы могли развернуть их в веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="cb07a-274">Export the web project files as a web archive (WAR) file so that you can deploy it to the web app.</span></span> <span data-ttu-id="cb07a-275">В папке WebContent находятся следующие файлы веб-проектов:</span><span class="sxs-lookup"><span data-stu-id="cb07a-275">The following web project files reside in the WebContent folder:</span></span>

    META-INF
    WEB-INF
    index.jsp

1. <span data-ttu-id="cb07a-276">Щелкните правой кнопкой мыши папку WebContent и выберите **Экспортировать**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-276">Right-click the WebContent folder and select **Export**.</span></span>
2. <span data-ttu-id="cb07a-277">В диалоговом окне **Export Select** (Экспорт выбранного содержимого) щелкните **Web > WAR** (Веб > WAR-файл), а затем щелкните **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="cb07a-277">In the **Export Select** dialog, click **Web > WAR** file, then click **Next**.</span></span>
3. <span data-ttu-id="cb07a-278">В диалогом окне **Экспорт WAR-файлов** выберите каталог src в текущем проекте и добавьте имя WAR-файла в конце.</span><span class="sxs-lookup"><span data-stu-id="cb07a-278">In the **WAR Export** dialog, select the src directory in the current project, and include the name of the WAR file at the end.</span></span> <span data-ttu-id="cb07a-279">Например:</span><span class="sxs-lookup"><span data-stu-id="cb07a-279">For example:</span></span>
   
    `<project-path>/JSPHello/src/JSPHello.war`

<span data-ttu-id="cb07a-280">Дополнительную информацию о развертывании WAR-файлов см. в статье [Добавление приложения Java в веб-приложения службы приложений Azure](web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="cb07a-280">For more information on deploying WAR files, see [Add a Java application to Azure App Service Web Apps](web-sites-java-add-app.md).</span></span>

### <a name="deploying-the-hello-world-application-using-ftp"></a><span data-ttu-id="cb07a-281">Развертывание приложения Hello World с использованием FTP</span><span class="sxs-lookup"><span data-stu-id="cb07a-281">Deploying the Hello World Application Using FTP</span></span>
<span data-ttu-id="cb07a-282">Выберите сторонний FTP-клиент для публикации приложения.</span><span class="sxs-lookup"><span data-stu-id="cb07a-282">Select a third-party FTP client to publish the application.</span></span> <span data-ttu-id="cb07a-283">Эта процедура описана в двух вариантах — использование консоли Kudu, встроенной в Azure, и использование FileZilla, популярного инструмента с удобным графическим пользовательским интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="cb07a-283">This procedure describes two options: the Kudu console built into Azure; and FileZilla, a popular tool with a convenient, graphical UI.</span></span>

> <span data-ttu-id="cb07a-284">**Примечание.** Набор средств Azure для Eclipse поддерживает развертывание в учетных записях хранения и облачных службах, но сейчас не поддерживает развертывание в веб-приложениях.</span><span class="sxs-lookup"><span data-stu-id="cb07a-284">**Note:** The Azure Toolkit for Eclipse supports deployment to storage accounts and cloud services, but does not currently support deployment to web apps.</span></span> <span data-ttu-id="cb07a-285">Вы можете выполнять развертывание в учетных записях хранения или облачных службах, используя проект развертывания Azure, как описано в разделе [Создание приложения Hello World для Azure в Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), но не можете выполнять развертывания в веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="cb07a-285">You can deploy to storage accounts and cloud services using an Azure Deployment Project as described in [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), but not to web apps.</span></span> <span data-ttu-id="cb07a-286">Используйте другие способы передачи файлов в свое веб-приложение, например с использованием FTP или GitHub.</span><span class="sxs-lookup"><span data-stu-id="cb07a-286">Use other methods such as FTP or GitHub to transfer files to your web app.</span></span>
> 
> <span data-ttu-id="cb07a-287">**Примечание.** Мы не советуем использовать FTP через командную строку Windows (служебную программу командной строки FTP.EXE, которая включена в комплект Windows).</span><span class="sxs-lookup"><span data-stu-id="cb07a-287">**Note:** We do not recommend using FTP from the Windows command prompt (the command-line FTP.EXE utility that ships with Windows).</span></span> <span data-ttu-id="cb07a-288">FTP-клиенты, использующие FTP в активном режиме, например FTP.EXE, зачастую дают сбой при работе с брандмауэрами.</span><span class="sxs-lookup"><span data-stu-id="cb07a-288">FTP clients that use active FTP, such as FTP.EXE, often fail to work over firewalls.</span></span> <span data-ttu-id="cb07a-289">FTP в активном режиме задает внутренний адрес локальной сети, к которой FTP-серверу, скорее всего, не удастся подключится.</span><span class="sxs-lookup"><span data-stu-id="cb07a-289">Active FTP specifies an internal LAN-based address, to which an FTP server will likely fail to connect.</span></span>
> 
> 

<span data-ttu-id="cb07a-290">Дополнительные сведения о развертывании веб-приложения службы приложений с помощью FTP см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="cb07a-290">For more information on deployment to an App Service web app using FTP, see the following topics:</span></span>

* [<span data-ttu-id="cb07a-291">Развертывание с помощью служебной программы FTP</span><span class="sxs-lookup"><span data-stu-id="cb07a-291">Deploy using an FTP utility</span></span>](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a><span data-ttu-id="cb07a-292">"Настройка учетных данных для развертывания"</span><span class="sxs-lookup"><span data-stu-id="cb07a-292">Set up deployment credentials</span></span>
<span data-ttu-id="cb07a-293">Прежде чем начать создание веб-приложения, убедитесь, что запущено приложение **AzureWebDemo** .</span><span class="sxs-lookup"><span data-stu-id="cb07a-293">Make sure you have run the **AzureWebDemo** application to create a web app.</span></span> <span data-ttu-id="cb07a-294">Вы будете передавать файлы в это расположение.</span><span class="sxs-lookup"><span data-stu-id="cb07a-294">You will transfer files to this location.</span></span>

1. <span data-ttu-id="cb07a-295">Войдите на классический портал Azure и щелкните **Веб-приложения**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-295">Log into the classic portal and click **Web Apps**.</span></span> <span data-ttu-id="cb07a-296">Убедитесь, что **WebDemoWebApp** отображается в списке веб-приложений и что приложение работает.</span><span class="sxs-lookup"><span data-stu-id="cb07a-296">Make sure **WebDemoWebApp** appears in the list of web apps, and make sure that it is running.</span></span> <span data-ttu-id="cb07a-297">Щелкните **WebDemoWebApp**, чтобы открыть соответствующую страницу **панели мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-297">Click **WebDemoWebApp** to open its **Dashboard** page.</span></span>
2. <span data-ttu-id="cb07a-298">На странице **панели мониторинга** в разделе **Сводка** щелкните **Настроить учетные данные развертывания** (если у вас уже есть учетные данные развертывания, этот пункт будет называться **Сброс учетных данных развертывания**).</span><span class="sxs-lookup"><span data-stu-id="cb07a-298">On the **Dashboard** page, under **Quick Glance**, click **Set up your deployment credentials** (if you already have deployment credentials, this reads **Reset your deployment credentials**).</span></span>
   
    <span data-ttu-id="cb07a-299">Учетные данные развертывания связаны с учетной записью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="cb07a-299">Deployment credentials are associated with a Microsoft account.</span></span> <span data-ttu-id="cb07a-300">Необходимо указать имя пользователя и пароль, которые можно использовать для развертывания с использованием Git и FTP.</span><span class="sxs-lookup"><span data-stu-id="cb07a-300">You need to specify a username and password that you can use to deploy using Git and FTP.</span></span> <span data-ttu-id="cb07a-301">Вы можете использовать эти учетные данные для развертывания в любое веб-приложение в пределах любой подписки Azure, связанной с учетной записью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="cb07a-301">You can use these credentials to deploy to any web app in all Azure subscriptions associated with your Microsoft account.</span></span> <span data-ttu-id="cb07a-302">Укажите учетные данные развертывания с использованием Git и FTP в диалоговом окне и запишите имя пользователя и пароль, чтобы использовать их в будущем.</span><span class="sxs-lookup"><span data-stu-id="cb07a-302">Provide Git and FTP deployment credentials in the dialog, and record the username and password for future use.</span></span>

#### <a name="get-ftp-connection-information"></a><span data-ttu-id="cb07a-303">Получение информации о подключении по FTP</span><span class="sxs-lookup"><span data-stu-id="cb07a-303">Get FTP connection information</span></span>
<span data-ttu-id="cb07a-304">Чтобы использовать FTP для развертывания файлов приложения в созданное веб-приложение, необходимо получить информацию о подключении.</span><span class="sxs-lookup"><span data-stu-id="cb07a-304">To use FTP to deploy application files to the newly created web app, you need to obtain connection information.</span></span> <span data-ttu-id="cb07a-305">Ее можно получить двумя способами.</span><span class="sxs-lookup"><span data-stu-id="cb07a-305">There are two ways to obtain connection information.</span></span> <span data-ttu-id="cb07a-306">Первый способ — посетить страницу **Панель мониторинга** в веб-приложении, а второй способ — скачать профиль публикации веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="cb07a-306">One way is to visit the web app's **Dashboard** page; the other way is to download the web app's publish profile.</span></span> <span data-ttu-id="cb07a-307">Профиль публикации — это XML-файл, который содержит такую информацию, как имя узла FTP и учетные данные для входа ваших веб-приложений в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="cb07a-307">The publish profile is an XML file that provides information such as FTP host name and logon credentials for your web apps in Azure App Service.</span></span> <span data-ttu-id="cb07a-308">Вы можете использовать эти имя пользователя и пароль не только для развертывания этого приложения, но и для развертывания в любые веб-приложения в рамках любых подписок, связанных с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="cb07a-308">You can use this username and password to deploy to any web app in all subscriptions associated with the Azure account, not only this one.</span></span>

<span data-ttu-id="cb07a-309">Чтобы получить информацию о подключении по FTP из колонки веб-приложения на [портале Azure][Azure Portal], выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="cb07a-309">To obtain FTP connection information from the web app's blade in the [Azure Portal][Azure Portal]:</span></span>

1. <span data-ttu-id="cb07a-310">В разделе **Основные компоненты** найдите и скопируйте имя в поле **Имя узла FTP**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-310">Under **Essentials**, find and copy the **FTP hostname**.</span></span> <span data-ttu-id="cb07a-311">Это URI, аналогичный `ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="cb07a-311">This is a URI similar to `ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span></span>
2. <span data-ttu-id="cb07a-312">В разделе **Основные компоненты** найдите и скопируйте **имя пользователя FTP или развертывания**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-312">Under **Essentials**, find and copy **FTP/Deployment username**.</span></span> <span data-ttu-id="cb07a-313">У него будет такой формат: *webappname\deployment-username* (например, `WebDemoWebApp\deployer77`).</span><span class="sxs-lookup"><span data-stu-id="cb07a-313">This will have the form *webappname\deployment-username*; for example `WebDemoWebApp\deployer77`.</span></span>

<span data-ttu-id="cb07a-314">Чтобы получить информацию о подключении по FTP из профиля публикации:</span><span class="sxs-lookup"><span data-stu-id="cb07a-314">To obtain FTP connection information from the publish profile:</span></span>

1. <span data-ttu-id="cb07a-315">В колонке веб-приложения щелкните **Получить профиль публикации**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-315">In the web app's blade, click **Get publish profile**.</span></span> <span data-ttu-id="cb07a-316">Это позволит скачать PUBLISHSETTINGS-файл на локальный диск.</span><span class="sxs-lookup"><span data-stu-id="cb07a-316">This will download a .publishsettings file to your local drive.</span></span>
2. <span data-ttu-id="cb07a-317">Откройте PUBLISHSETTINGS-файл в редакторе XML-файлов или текстовом редакторе и найдите элемент `<publishProfile>`, в котором содержится `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="cb07a-317">Open the .publishsettings file in an XML editor or text editor and find the `<publishProfile>` element containing `publishMethod="FTP"`.</span></span> <span data-ttu-id="cb07a-318">Он должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="cb07a-318">It should look like the following:</span></span>
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. <span data-ttu-id="cb07a-319">Обратите внимание, что параметры `publishProfile` веб-приложения соответствуют параметрам диспетчера сайта FileZilla, как приведено ниже.</span><span class="sxs-lookup"><span data-stu-id="cb07a-319">Note that the web app's `publishProfile` settings map to the FileZilla Site Manager settings as follows:</span></span>

* <span data-ttu-id="cb07a-320">`publishUrl` — значение этого параметра аналогично значению **Имя узла FTP**, заданному в поле **Узел**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-320">`publishUrl` is the same as **FTP host name**, the value you set in **Host**.</span></span>
* <span data-ttu-id="cb07a-321">`publishMethod="FTP"` означает, что для параметра **Протокол** вы задали значение **FTP — протокол передачи файлов**, а для параметра **Шифрование** — **Use plain FTP** (Использовать простой FTP).</span><span class="sxs-lookup"><span data-stu-id="cb07a-321">`publishMethod="FTP"` means that you set **Protocol** to **FTP - File Transfer Protocol**, and **Encryption** to **Use plain FTP**.</span></span>
* <span data-ttu-id="cb07a-322">`userName` и `userPWD` — это ключи для фактических значений имени пользователя и пароля, которые вы указали при сбросе учетных данных развертывания.</span><span class="sxs-lookup"><span data-stu-id="cb07a-322">`userName` and `userPWD` are keys for the actual username and password values you specified when you reset the deployment credentials.</span></span> <span data-ttu-id="cb07a-323">`userName` — значение этого параметра аналогично значению **Пользователь FTP или развертывания**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-323">`userName` is the same as **Deployment / FTP user**.</span></span> <span data-ttu-id="cb07a-324">Они соответствуют параметрам **User** (Пользователь) и **Password** (Пароль) в FileZilla.</span><span class="sxs-lookup"><span data-stu-id="cb07a-324">They map to **User** and **Password** in FileZilla.</span></span>
* <span data-ttu-id="cb07a-325">`ftpPassiveMode="True"` означает, что FTP-сайт использует пассивный режим передачи FTP. Выберите **Passive** (Пассивный) на вкладке **Transfer Settings** (Параметры передачи).</span><span class="sxs-lookup"><span data-stu-id="cb07a-325">`ftpPassiveMode="True"` means that the FTP site uses passive FTP transfer; select **Passive** on the **Transfer Settings** tab.</span></span>

#### <a name="configure-the-web-app-to-host-a-java-application"></a><span data-ttu-id="cb07a-326">Настройка размещения приложения Java в веб-приложении</span><span class="sxs-lookup"><span data-stu-id="cb07a-326">Configure the Web App to host a Java application</span></span>
<span data-ttu-id="cb07a-327">Прежде чем опубликовать приложение, необходимо изменить некоторые параметры конфигурации, чтобы в веб-приложении можно было разместить приложение Java.</span><span class="sxs-lookup"><span data-stu-id="cb07a-327">Before you publish the application, you need to change a few configuration settings so that the web app can host a Java application.</span></span>

1. <span data-ttu-id="cb07a-328">На классическом портале перейдите на страницу **Панель мониторинга** в веб-приложении и щелкните **Настроить**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-328">In the classic portal, go to the web app's **Dashboard** page and click **Configure**.</span></span> <span data-ttu-id="cb07a-329">На странице **Настройка** укажите следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="cb07a-329">On the **Configure** page, specify the following settings.</span></span>
2. <span data-ttu-id="cb07a-330">Значение по умолчанию для параметра **Версия Java** — **Отключено**. Выберите целевую версию Java для своего приложения, например 1.7.0_51.</span><span class="sxs-lookup"><span data-stu-id="cb07a-330">In **Java version** the default is **Off**; select the Java version your application targets; for example 1.7.0_51.</span></span> <span data-ttu-id="cb07a-331">После этого убедитесь, что для **веб-контейнера** указана версия сервера Tomcat.</span><span class="sxs-lookup"><span data-stu-id="cb07a-331">After you do this, also make sure that **Web container** is set to a version of Tomcat Server.</span></span>
3. <span data-ttu-id="cb07a-332">В раздел **Документы по умолчанию** добавьте файл index.jsp и переместите его в начало списка.</span><span class="sxs-lookup"><span data-stu-id="cb07a-332">In **Default Documents**, add index.jsp and move it up to the top of the list.</span></span> <span data-ttu-id="cb07a-333">(файл по умолчанию для веб-приложений— hostingstart.html).</span><span class="sxs-lookup"><span data-stu-id="cb07a-333">(The default file for web apps is hostingstart.html.)</span></span>
4. <span data-ttu-id="cb07a-334">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-334">Click **Save**.</span></span>

#### <a name="publish-your-application-using-kudu"></a><span data-ttu-id="cb07a-335">Публикация приложения с помощью Kudu</span><span class="sxs-lookup"><span data-stu-id="cb07a-335">Publish your application using Kudu</span></span>
<span data-ttu-id="cb07a-336">Один из способов публикации приложения предусматривает использование консоли отладки Kudu, встроенной в Azure.</span><span class="sxs-lookup"><span data-stu-id="cb07a-336">One way to publish the application is to use the Kudu debug console built into Azure.</span></span> <span data-ttu-id="cb07a-337">Kudu известна своей стабильностью и согласованностью с веб-приложениями службы приложений и сервером Tomcat.</span><span class="sxs-lookup"><span data-stu-id="cb07a-337">Kudu is known to be stable and consistent with App Service Web Apps and Tomcat Server.</span></span> <span data-ttu-id="cb07a-338">Для работы с веб-приложением консоль можно открыть, перейдя по URL-адресу такого формата:</span><span class="sxs-lookup"><span data-stu-id="cb07a-338">You access the console for the web app by browsing to a URL of the following form:</span></span>

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. <span data-ttu-id="cb07a-339">Консоль Kudu для этой процедуры размещена по следующему URL-адресу. Перейдите к этому расположению:</span><span class="sxs-lookup"><span data-stu-id="cb07a-339">For this procedure, the Kudu console is located at the following URL; browse to this location:</span></span>
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. <span data-ttu-id="cb07a-340">В меню вверху щелкните **Консоль отладки > CMD**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-340">From the top menu, select **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="cb07a-341">В командной строке консоли перейдите к `/site/wwwroot` (или щелкните `site`, а затем `wwwroot` в представлении каталога в верхней части страницы):</span><span class="sxs-lookup"><span data-stu-id="cb07a-341">In the console command line, navigate to `/site/wwwroot` (or click `site`, then `wwwroot` in the directory view at the top of the page):</span></span>
   
    `cd /site/wwwroot`
4. <span data-ttu-id="cb07a-342">После того как вы укажете значение для **Версия Java**, сервер Tomcat должен создать каталог веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="cb07a-342">After you specify **Java version**, Tomcat server should create a webapps directory.</span></span> <span data-ttu-id="cb07a-343">В командной строке консоли перейдите к каталогу веб-приложений:</span><span class="sxs-lookup"><span data-stu-id="cb07a-343">In the console command line, navigate to the webapps directory:</span></span>
   
    `mkdir webapps`
   
    `cd webapps`
5. <span data-ttu-id="cb07a-344">Перетащите файл JSPHello.war из `<project-path>/JSPHello/src/` и поместите его в представление каталога Kudu в `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="cb07a-344">Drag JSPHello.war from `<project-path>/JSPHello/src/` and drop it into the Kudu directory view under `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="cb07a-345">Не перетаскивайте его в область «Перетащить сюда, чтобы загрузить и запаковать», так как Tomcat распакует его.</span><span class="sxs-lookup"><span data-stu-id="cb07a-345">Do not drag it to the "Drag here to upload and zip" area, because Tomcat will unzip it.</span></span>
   
   ![][8]

<span data-ttu-id="cb07a-346">Сначала файл JSPHello.war сам собой отобразится в области каталога:</span><span class="sxs-lookup"><span data-stu-id="cb07a-346">At first JSPHello.war appears in the directory area by itself:</span></span>

  ![][9]

<span data-ttu-id="cb07a-347">Через короткий промежуток времени (возможно, меньше 5 минут) сервер Tomcat распакует WAR-файл в распакованный каталог JSPHello.</span><span class="sxs-lookup"><span data-stu-id="cb07a-347">In a short time (probably less than 5 minutes) Tomcat Server will unzip the WAR file into an unpacked JSPHello directory.</span></span> <span data-ttu-id="cb07a-348">Выберите каталог ROOT, чтобы увидеть, распакован и скопирован ли сюда файл index.jsp.</span><span class="sxs-lookup"><span data-stu-id="cb07a-348">Click the ROOT directory to see whether index.jsp has been unzipped and copied there.</span></span> <span data-ttu-id="cb07a-349">Если это выполнено, перейдите назад к каталогу веб-приложений, чтобы убедиться, что создан распакованный каталог JSPHello.</span><span class="sxs-lookup"><span data-stu-id="cb07a-349">If so, navigate back to the webapps directory to see whether the unpacked JSPHello directory has been created.</span></span> <span data-ttu-id="cb07a-350">Если эти элементы не отображаются, подождите, а затем повторите процедуру.</span><span class="sxs-lookup"><span data-stu-id="cb07a-350">If you do not see these items, wait and repeat.</span></span>

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a><span data-ttu-id="cb07a-351">Публикация приложения с помощью FileZilla (необязательно)</span><span class="sxs-lookup"><span data-stu-id="cb07a-351">Publish your application using FileZilla (optional)</span></span>
<span data-ttu-id="cb07a-352">Для публикации своего приложения вы также можете использовать другой инструмент — FileZilla, популярный сторонний FTP-клиент с удобным графическим пользовательским интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="cb07a-352">Another tool you can use to publish the application is FileZilla, a popular third-party FTP client with a convenient, graphical UI.</span></span> <span data-ttu-id="cb07a-353">Скачать и установить FileZilla можно на веб-сайте [http://filezilla-project.org/](http://filezilla-project.org/).</span><span class="sxs-lookup"><span data-stu-id="cb07a-353">You can download and install FileZilla from [http://filezilla-project.org/](http://filezilla-project.org/) if you do not already have it.</span></span> <span data-ttu-id="cb07a-354">Дополнительную информацию об использовании этого клиента см. в [документации по FileZilla](https://wiki.filezilla-project.org/Documentation), а также в записи блога, посвященной [FTP-клиентам (часть 4 — FileZilla)](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb07a-354">For more information on using the client, see the [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) and this blog entry on [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span></span>

1. <span data-ttu-id="cb07a-355">В FileZilla щелкните **File > Site Manager** (Файл > Диспетчер сайтов).</span><span class="sxs-lookup"><span data-stu-id="cb07a-355">In FileZilla, click **File > Site Manager**.</span></span>
2. <span data-ttu-id="cb07a-356">В диалоговом окне **Site Manager** (Диспетчер сайтов) щелкните **New Site** (Создать сайт).</span><span class="sxs-lookup"><span data-stu-id="cb07a-356">In the **Site Manager** dialog, click **New Site**.</span></span> <span data-ttu-id="cb07a-357">В **Выберите запись** отобразиться новый пустой FTP-сайт с запросом на указание имени.</span><span class="sxs-lookup"><span data-stu-id="cb07a-357">A new blank FTP site will appear in **Select Entry** prompting you to provide a name.</span></span> <span data-ttu-id="cb07a-358">Укажите имя `AzureWebDemo-FTP`для использования в этой процедуре.</span><span class="sxs-lookup"><span data-stu-id="cb07a-358">For this procedure, name it `AzureWebDemo-FTP`.</span></span>
   
    <span data-ttu-id="cb07a-359">На вкладке **Общие** укажите следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="cb07a-359">On the **General** tab, specify the following settings:</span></span>
   
   * <span data-ttu-id="cb07a-360">**Host** (Узел): введите **имя узла FTP**, скопированное на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="cb07a-360">**Host:** Enter the **FTP Host Name** that you copied from the dashboard.</span></span>
   * <span data-ttu-id="cb07a-361">**Порт:** (оставьте поле пустым, так как это пассивная передача, и сервер будет определять, какой порт использовать).</span><span class="sxs-lookup"><span data-stu-id="cb07a-361">**Port:** (Leave this blank, as this is a passive transfer and the server will determine the port to use.)</span></span>
   * <span data-ttu-id="cb07a-362">**Протокол:** протокол передачи файлов FTP.</span><span class="sxs-lookup"><span data-stu-id="cb07a-362">**Protocol:** FTP File Transfer Protocol</span></span>
   * <span data-ttu-id="cb07a-363">**Шифрование:** используйте простой FTP.</span><span class="sxs-lookup"><span data-stu-id="cb07a-363">**Encryption:** Use plain FTP</span></span>
   * <span data-ttu-id="cb07a-364">**Тип входа:** обычный.</span><span class="sxs-lookup"><span data-stu-id="cb07a-364">**Logon Type:** Normal</span></span>
   * <span data-ttu-id="cb07a-365">**Пользователь:** укажите пользователя развертывания или узла FTP, который был скопирован из панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="cb07a-365">**User:** Enter the Deployment / FTP user that you copied from the dashboard.</span></span> <span data-ttu-id="cb07a-366">Это полное имя пользователя FTP в формате *имя_веб-приложения\имя_пользователя*.</span><span class="sxs-lookup"><span data-stu-id="cb07a-366">This is the full FTP username, which has the form *webappname\username*.</span></span>
   * <span data-ttu-id="cb07a-367">**Пароль:** введите пароль, указанный при задании учетных данных развертывания.</span><span class="sxs-lookup"><span data-stu-id="cb07a-367">**Password:** Enter the password that you specified when you set the deployment credentials.</span></span>
     
     <span data-ttu-id="cb07a-368">На вкладке **Transfer Settings** (Параметры передачи) выберите **Passive** (Пассивный).</span><span class="sxs-lookup"><span data-stu-id="cb07a-368">On the **Transfer Settings** tab, select **Passive**.</span></span>
3. <span data-ttu-id="cb07a-369">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="cb07a-369">Click **Connect**.</span></span> <span data-ttu-id="cb07a-370">При успешном подключении в консоли FileZilla отобразиться сообщение `Status: Connected` и будет выполнена команда `LIST`, позволяющая вывести список содержимого каталога.</span><span class="sxs-lookup"><span data-stu-id="cb07a-370">If successful, FileZilla's console will display a `Status: Connected` message and issue a `LIST` command to list the directory contents.</span></span>
4. <span data-ttu-id="cb07a-371">На панели сайта **Local** (Локальные) выберите исходный каталог, в котором находится файл JSPHello.war. Путь будет выглядеть приблизительно так:</span><span class="sxs-lookup"><span data-stu-id="cb07a-371">In the **Local** site panel, select the source directory in which the JSPHello.war file resides; the path will be similar to the following:</span></span>
   
    `<project-path>/JSPHello/src/`
5. <span data-ttu-id="cb07a-372">На панели сайта **Удаленные** выберите папку назначения.</span><span class="sxs-lookup"><span data-stu-id="cb07a-372">In the **Remote** site panel, select the destination folder.</span></span> <span data-ttu-id="cb07a-373">Разверните WAR-файл в каталоге `webapps` в корне веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="cb07a-373">You will deploy the WAR file to the `webapps` directory under the web app's root.</span></span> <span data-ttu-id="cb07a-374">Перейдите к `/site/wwwroot`, щелкните правой кнопкой мыши `wwwroot` и выберите **Create directory** (Создать каталог).</span><span class="sxs-lookup"><span data-stu-id="cb07a-374">Navigate to `/site/wwwroot`, right-click on `wwwroot`, and select **Create directory**.</span></span> <span data-ttu-id="cb07a-375">Укажите для каталога имя `webapps` и войдите в этот каталог.</span><span class="sxs-lookup"><span data-stu-id="cb07a-375">Name the directory `webapps` and enter that directory.</span></span>
6. <span data-ttu-id="cb07a-376">Передайте JSPHello.war в `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="cb07a-376">Transfer JSPHello.war to `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="cb07a-377">Выберите JSPHello.war в списке файлов **Local** (Локальные), щелкните его правой кнопкой мыши и выберите **Upload** (Отправить).</span><span class="sxs-lookup"><span data-stu-id="cb07a-377">Select JSPHello.war in the **Local** file list, right-click on it and select **Upload**.</span></span> <span data-ttu-id="cb07a-378">Вы должны увидеть его в `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="cb07a-378">You should see it appear in `/site/wwwroot/webapps`.</span></span>
7. <span data-ttu-id="cb07a-379">После копирования JSPHello.war в каталог веб-приложений сервер Tomcat автоматически распакует файлы в WAR-файле.</span><span class="sxs-lookup"><span data-stu-id="cb07a-379">After you copy JSPHello.war to the webapps directory, Tomcat Server will automatically unpack (unzip) the files in the WAR file.</span></span> <span data-ttu-id="cb07a-380">Несмотря на то, что сервер Tomcat начинает распаковку почти мгновенно, файлы могут отобразиться в FTP-клиенте спустя большой период времени (возможно, через несколько часов).</span><span class="sxs-lookup"><span data-stu-id="cb07a-380">Although Tomcat Server begins unpacking almost immediately, it might take a long time (possibly hours) for the files to appear in the FTP client.</span></span>

#### <a name="run-the-hello-world-application-on-the-web-app"></a><span data-ttu-id="cb07a-381">Запуск приложения Hello World в веб-приложении</span><span class="sxs-lookup"><span data-stu-id="cb07a-381">Run the Hello World application on the Web App</span></span>
1. <span data-ttu-id="cb07a-382">Загрузив WAR-файл и убедившись, что сервер Tomcat создал распакованный каталог `JSPHello`, перейдите к `http://webdemowebapp.azurewebsites.net/JSPHello`, чтобы запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="cb07a-382">After you have uploaded the WAR file and verified that Tomcat server has created an unpacked `JSPHello` directory, browse to `http://webdemowebapp.azurewebsites.net/JSPHello` to run the application.</span></span>
   
   > <span data-ttu-id="cb07a-383">**Примечание.** Если вы щелкнете **Обзор** на классическом портале, может отобразиться стандартная веб-страница с сообщением "This Java based web application has been successfully created" (Это веб-приложение на основе Java успешно создано).</span><span class="sxs-lookup"><span data-stu-id="cb07a-383">**Note:** If you click **Browse** from the classic portal, you might get the default webpage, saying "This Java based web application has been successfully created."</span></span> <span data-ttu-id="cb07a-384">Возможно, понадобится обновить веб-страницу, чтобы просмотреть выходные данные приложения вместо веб-страницы по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="cb07a-384">You might have to refresh the webpage in order to view the application output instead of the default webpage.</span></span>
   > 
   > 
2. <span data-ttu-id="cb07a-385">Когда приложение запустится, вы должны увидеть веб-страницу со следующими выходными данными:</span><span class="sxs-lookup"><span data-stu-id="cb07a-385">When the application runs, you should see a web page with the following output:</span></span>
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a><span data-ttu-id="cb07a-386">Очистка ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="cb07a-386">Clean up Azure resources</span></span>
<span data-ttu-id="cb07a-387">Эта процедура создает веб-приложение службы приложений.</span><span class="sxs-lookup"><span data-stu-id="cb07a-387">This procedure creates an App Service web app.</span></span> <span data-ttu-id="cb07a-388">На протяжении существования ресурсов за них будут выставляться счета.</span><span class="sxs-lookup"><span data-stu-id="cb07a-388">You will be billed for the resource as long as it exists.</span></span> <span data-ttu-id="cb07a-389">Если вы не планируете продолжить использование веб-приложения для тестирования или разработки, вам следует остановить или удалить его.</span><span class="sxs-lookup"><span data-stu-id="cb07a-389">Unless you plan to continue using the web app for testing or development, you should consider stopping or deleting it.</span></span> <span data-ttu-id="cb07a-390">За остановленное веб-приложение все равно взимается небольшая плата, зато его можно перезапустить в любое время.</span><span class="sxs-lookup"><span data-stu-id="cb07a-390">A web app that has been stopped will still incur a small charge, but you can restart it at any time.</span></span> <span data-ttu-id="cb07a-391">При удалении приложения будут стерты все загруженные в него данные.</span><span class="sxs-lookup"><span data-stu-id="cb07a-391">Deleting a web app erases all data you have uploaded to it.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

[1]: ./media/java-create-azure-website-using-java-sdk/eclipse-maven-repositories-rebuild-index.png
[2]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-java-class.png
[3]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-dynamic-web-project.png
[4]: ./media/java-create-azure-website-using-java-sdk/eclipse-java-build-path.png
[5]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-tomcat-server.png
[6]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-properties-page.png
[7]: ./media/java-create-azure-website-using-java-sdk/eclipse-run-on-server.png
[8]: ./media/java-create-azure-website-using-java-sdk/kudu-console-drag-drop.png
[9]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-1.png
[10]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-2.png


[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web Platform Installer]: http://go.microsoft.com/fwlink/?LinkID=252838
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh690946.aspx
[Azure classic portal]: https://manage.windowsazure.com
[What is an Azure AD directory]: http://technet.microsoft.com/library/jj573650.aspx
[Create and Upload a Management Certificate for Azure]: ../cloud-services/cloud-services-certs-create.md
[Key and Certificate Management Tool (keytool)]: http://docs.oracle.com/javase/6/docs/technotes/tools/windows/keytool.html
[WebSiteManagementClient]: http://azure.github.io/azure-sdk-for-java/com/microsoft/azure/management/websites/WebSiteManagementClient.html
[WebSpaceNames]: http://dl.windowsazure.com/javadoc/com/microsoft/windowsazure/management/websites/models/WebSpaceNames.html
[Azure Portal]: https://portal.azure.com
