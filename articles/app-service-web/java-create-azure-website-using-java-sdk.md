---
title: "aaaCreate веб-приложения в службе приложений Azure с помощью hello Azure SDK для Java"
description: "Узнайте, как toocreate веб-приложения в службе приложений Azure программно с помощью hello Azure SDK для Java."
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
ms.openlocfilehash: 42ba86b7fbb5668b3675198d0c5bb454525f706b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-hello-azure-sdk-for-java"></a><span data-ttu-id="82718-103">Создание веб-приложения в службе приложений Azure с помощью hello Azure SDK для Java</span><span class="sxs-lookup"><span data-stu-id="82718-103">Create a Web App in Azure App Service using hello Azure SDK for Java</span></span>
<!-- Azure Active Directory workflow is not yet available on hello Azure Portal -->

## <a name="overview"></a><span data-ttu-id="82718-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="82718-104">Overview</span></span>
<span data-ttu-id="82718-105">В этом пошаговом руководстве показано, как toocreate Azure SDK для Java-приложения, которое создает веб-приложения в [службе приложений Azure][Azure App Service], затем развернуть tooit приложения.</span><span class="sxs-lookup"><span data-stu-id="82718-105">This walkthrough shows you how toocreate an Azure SDK for Java application that creates a Web App in [Azure App Service][Azure App Service], then deploy an application tooit.</span></span> <span data-ttu-id="82718-106">Руководство состоит из двух частей:</span><span class="sxs-lookup"><span data-stu-id="82718-106">It consists of two parts:</span></span>

* <span data-ttu-id="82718-107">Часть 1 показано, как toobuild приложения Java, создает веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="82718-107">Part 1 demonstrates how toobuild a Java application that creates a web app.</span></span>
* <span data-ttu-id="82718-108">Часть 2 показано, как toocreate простой JSP «Hello World» приложения, а затем код toodeploy tooApp службы для использования FTP клиента.</span><span class="sxs-lookup"><span data-stu-id="82718-108">Part 2 demonstrates how toocreate a simple JSP "Hello World" application, then use an FTP client toodeploy code tooApp Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82718-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="82718-109">Prerequisites</span></span>
### <a name="software-installations"></a><span data-ttu-id="82718-110">Установка программного обеспечения</span><span class="sxs-lookup"><span data-stu-id="82718-110">Software Installations</span></span>
<span data-ttu-id="82718-111">Hello AzureWebDemo кода приложения в этой статье было написано с помощью Java SDK Azure 0.7.0, которую можно установить с помощью hello [Web Platform Installer] [ Web Platform Installer] (WebPI).</span><span class="sxs-lookup"><span data-stu-id="82718-111">hello AzureWebDemo application code in this article was written using Azure Java SDK 0.7.0, which you can install using hello [Web Platform Installer][Web Platform Installer] (WebPI).</span></span> <span data-ttu-id="82718-112">Кроме того, убедитесь, что toouse hello последнюю версию hello [средств Azure для Eclipse][Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="82718-112">In addition, make sure toouse hello latest version of hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="82718-113">После установки пакета SDK для hello, обновите hello зависимости в проект Eclipse, запустив **обновления индекса** в **репозиториев Maven**, затем снова добавьте hello последняя версия каждого пакета в hello  **Зависимости** окна.</span><span class="sxs-lookup"><span data-stu-id="82718-113">After you install hello SDK, update hello dependencies in your Eclipse project by running **Update Index** in **Maven Repositories**, then re-add hello latest version of each package in hello **Dependencies** window.</span></span> <span data-ttu-id="82718-114">Можно проверить hello версии установленного программного обеспечения в Eclipse, щелкнув **Справка > сведения об установке**; вы должны иметь по крайней мере hello следующие версии:</span><span class="sxs-lookup"><span data-stu-id="82718-114">You can verify hello version of your installed software in Eclipse by clicking **Help > Installation Details**; you should have at least hello following versions:</span></span>

* <span data-ttu-id="82718-115">пакет для библиотек Microsoft Azure для Java 0.7.0.20150309;</span><span class="sxs-lookup"><span data-stu-id="82718-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span></span>
* <span data-ttu-id="82718-116">интегрированная среда разработки Eclipse для разработчиков Java EE 4.4.2.20150219.</span><span class="sxs-lookup"><span data-stu-id="82718-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span></span>

### <a name="create-and-configure-cloud-resources-in-azure"></a><span data-ttu-id="82718-117">Создание и настройка облачных ресурсов в Azure</span><span class="sxs-lookup"><span data-stu-id="82718-117">Create and Configure Cloud Resources in Azure</span></span>
<span data-ttu-id="82718-118">Перед началом этой процедуры требуется toohave Активная подписка Azure и настроить Active Directory (AD) в Azure по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="82718-118">Before you begin this procedure, you need toohave an active Azure subscription and set up a default Active Directory (AD) on Azure.</span></span>

### <a name="create-an-active-directory-ad-in-azure"></a><span data-ttu-id="82718-119">Создание Active Directory в Azure</span><span class="sxs-lookup"><span data-stu-id="82718-119">Create an Active Directory (AD) in Azure</span></span>
<span data-ttu-id="82718-120">Если Active Directory (AD) еще не установлен на подписки Azure, войдите на hello [классический портал Azure] [ Azure classic portal] с учетной записью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="82718-120">If you do not already have an Active Directory (AD) on your Azure subscription, log into hello [Azure classic portal][Azure classic portal] with your Microsoft account.</span></span> <span data-ttu-id="82718-121">Если у вас несколько подписок, нажмите кнопку **подписки** и выберите hello каталог по умолчанию для подписки hello toouse требуется для этого проекта.</span><span class="sxs-lookup"><span data-stu-id="82718-121">If you have multiple subscriptions, click **Subscriptions** and select hello default directory for hello subscription you want toouse for this project.</span></span> <span data-ttu-id="82718-122">Нажмите кнопку **применить** tooswitch toothat подписки представлении.</span><span class="sxs-lookup"><span data-stu-id="82718-122">Then click **Apply** tooswitch toothat subscription view.</span></span>

1. <span data-ttu-id="82718-123">Выберите **Active Directory** hello меню в левой части.</span><span class="sxs-lookup"><span data-stu-id="82718-123">Select **Active Directory** from hello menu at left.</span></span> <span data-ttu-id="82718-124">Щелкните **Создать > Каталог > Настраиваемое создание**.</span><span class="sxs-lookup"><span data-stu-id="82718-124">**Click New > Directory > Custom Create**.</span></span>
2. <span data-ttu-id="82718-125">В разделе **Добавить каталог** выберите **Создать каталог**.</span><span class="sxs-lookup"><span data-stu-id="82718-125">In **Add Directory**, select **Create New Directory**.</span></span>
3. <span data-ttu-id="82718-126">В поле **Имя**введите имя каталога.</span><span class="sxs-lookup"><span data-stu-id="82718-126">In **Name**, enter a directory name.</span></span>
4. <span data-ttu-id="82718-127">В поле **Домен** введите имя домена.</span><span class="sxs-lookup"><span data-stu-id="82718-127">In **Domain**, enter a domain name.</span></span> <span data-ttu-id="82718-128">Имя основного домена, которое включается по умолчанию в каталоге; имеет форму hello `<domain_name>.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="82718-128">This is a basic domain name that is included by default with your directory; it has hello form `<domain_name>.onmicrosoft.com`.</span></span> <span data-ttu-id="82718-129">Можно назвать его на основе имени каталога hello или другое имя домена, которое вы являетесь владельцем.</span><span class="sxs-lookup"><span data-stu-id="82718-129">You can name it based on hello directory name or another domain name that you own.</span></span> <span data-ttu-id="82718-130">Позже вы сможете добавить другое доменное имя, которое уже использует ваша организация.</span><span class="sxs-lookup"><span data-stu-id="82718-130">Later, you can add another domain name that your organization already uses.</span></span>
5. <span data-ttu-id="82718-131">В поле **Страна или регион**выберите свой языковой стандарт.</span><span class="sxs-lookup"><span data-stu-id="82718-131">In **Country or region**, select your locale.</span></span>

<span data-ttu-id="82718-132">Дополнительную информацию об Active Directory см. в разделе [Что такое каталог Azure AD?][What is an Azure AD directory]</span><span class="sxs-lookup"><span data-stu-id="82718-132">For more information on AD, see [What is an Azure AD directory][What is an Azure AD directory]?</span></span>

### <a name="create-a-management-certificate-for-azure"></a><span data-ttu-id="82718-133">Создание сертификата управления для Azure</span><span class="sxs-lookup"><span data-stu-id="82718-133">Create a Management Certificate for Azure</span></span>
<span data-ttu-id="82718-134">Hello Azure SDK для Java использует tooauthenticate сертификаты управления подписками Azure.</span><span class="sxs-lookup"><span data-stu-id="82718-134">hello Azure SDK for Java uses management certificates tooauthenticate with Azure subscriptions.</span></span> <span data-ttu-id="82718-135">Они являются сертификатами X.509 v3, используется tooauthenticate клиентское приложение, которое использует API управления службами tooact hello от имени ресурсами подписки toomanage владелец подписки hello.</span><span class="sxs-lookup"><span data-stu-id="82718-135">These are X.509 v3 certificates you use tooauthenticate a client application that uses hello Service Management API tooact on behalf of hello subscription owner toomanage subscription resources.</span></span>

<span data-ttu-id="82718-136">Hello кода в этой процедуре используется tooauthenticate самозаверяющий сертификат с Azure.</span><span class="sxs-lookup"><span data-stu-id="82718-136">hello code in this procedure uses a self-signed certificate tooauthenticate with Azure.</span></span> <span data-ttu-id="82718-137">Для выполнения этой процедуры нужно toocreate сертификат и передать его toohello [классический портал Azure] [ Azure classic portal] заранее.</span><span class="sxs-lookup"><span data-stu-id="82718-137">For this procedure, you need toocreate a certificate and upload it toohello [Azure classic portal][Azure classic portal] beforehand.</span></span> <span data-ttu-id="82718-138">Включает в себя hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="82718-138">This involves hello following steps:</span></span>

* <span data-ttu-id="82718-139">Создайте PFX-файл, представляющий собой сертификат клиента, и сохраните его локально.</span><span class="sxs-lookup"><span data-stu-id="82718-139">Generate a PFX file representing your client certificate and save it locally.</span></span>
* <span data-ttu-id="82718-140">Создайте сертификат управления (CER-файл) из PFX-файла hello.</span><span class="sxs-lookup"><span data-stu-id="82718-140">Generate a management certificate (CER file) from hello PFX file.</span></span>
* <span data-ttu-id="82718-141">Отправьте tooyour файл CER hello подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="82718-141">Upload hello CER file tooyour Azure subscription.</span></span>
* <span data-ttu-id="82718-142">Преобразование hello PFX-файла в JKS, так как этот формат tooauthenticate, с помощью сертификатов использует Java.</span><span class="sxs-lookup"><span data-stu-id="82718-142">Convert hello PFX file into JKS, because Java uses that format tooauthenticate using certificates.</span></span>
* <span data-ttu-id="82718-143">Напишите код проверки подлинности приложения hello, который ссылается на локальный файл JKS toohello.</span><span class="sxs-lookup"><span data-stu-id="82718-143">Write hello application's authentication code, which refers toohello local JKS file.</span></span>

<span data-ttu-id="82718-144">По завершении этой процедуры сертификат CER hello будет находиться в вашей подписке Azure и сертификат JKS hello будет находиться на локальном диске.</span><span class="sxs-lookup"><span data-stu-id="82718-144">When you complete this procedure, hello CER certificate will reside in your Azure subscription and hello JKS certificate will reside on your local drive.</span></span> <span data-ttu-id="82718-145">Дополнительную информацию о сертификатах управления см. в разделе [Создание и передача сертификата управления для Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="82718-145">For more information on management certificates, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="create-a-certificate"></a><span data-ttu-id="82718-146">Создание сертификата</span><span class="sxs-lookup"><span data-stu-id="82718-146">Create a certificate</span></span>
<span data-ttu-id="82718-147">toocreate собственный самозаверяющий сертификат, откройте консоль командной строки в операционной системе и выполните hello, следующие команды.</span><span class="sxs-lookup"><span data-stu-id="82718-147">toocreate your own self-signed certificate, open a command console on your operating system and run hello following commands.</span></span>

> <span data-ttu-id="82718-148">**Примечание:** hello компьютера, на котором выполняется эта команда должен иметь hello JDK установлен.</span><span class="sxs-lookup"><span data-stu-id="82718-148">**Note:**  hello computer on which you run this command must have hello JDK installed.</span></span> <span data-ttu-id="82718-149">Кроме того keytool toohello hello пути зависит от hello расположение установки hello JDK.</span><span class="sxs-lookup"><span data-stu-id="82718-149">Also, hello path toohello keytool depends on hello location in which you install hello JDK.</span></span> <span data-ttu-id="82718-150">Дополнительные сведения см. в разделе [ключ и сертификат средство управления (keytool)] [ Key and Certificate Management Tool (keytool)] в hello Java онлайн-документации.</span><span class="sxs-lookup"><span data-stu-id="82718-150">For more information, see [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] in hello Java online docs.</span></span>
> 
> 

<span data-ttu-id="82718-151">toocreate hello PFX-файл:</span><span class="sxs-lookup"><span data-stu-id="82718-151">toocreate hello .pfx file:</span></span>

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

<span data-ttu-id="82718-152">toocreate hello CER-файл:</span><span class="sxs-lookup"><span data-stu-id="82718-152">toocreate hello .cer file:</span></span>

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

<span data-ttu-id="82718-153">Описание:</span><span class="sxs-lookup"><span data-stu-id="82718-153">where:</span></span>

* <span data-ttu-id="82718-154">`<java-install-dir>`— toohello hello каталог, в которой установлены Java.</span><span class="sxs-lookup"><span data-stu-id="82718-154">`<java-install-dir>` is hello path toohello directory in which you installed Java.</span></span>
* <span data-ttu-id="82718-155">`<keystore-id>`Идентификатор записи hello хранилища ключей (например, `AzureRemoteAccess`).</span><span class="sxs-lookup"><span data-stu-id="82718-155">`<keystore-id>` is hello keystore entry identifier (for example, `AzureRemoteAccess`).</span></span>
* <span data-ttu-id="82718-156">`<cert-store-dir>`— toohello hello каталог, в котором нужно toostore сертификаты (например `C:/Certificates`).</span><span class="sxs-lookup"><span data-stu-id="82718-156">`<cert-store-dir>` is hello path toohello directory in which you want toostore certificates (for example `C:/Certificates`).</span></span>
* <span data-ttu-id="82718-157">`<cert-file-name>`— Имя файла сертификата hello hello (например `AzureWebDemoCert`).</span><span class="sxs-lookup"><span data-stu-id="82718-157">`<cert-file-name>` is hello name of hello certificate file (for example `AzureWebDemoCert`).</span></span>
* <span data-ttu-id="82718-158">`<password>`Выберите сертификат hello tooprotect; паролем hello он должен быть по крайней мере 6 символов.</span><span class="sxs-lookup"><span data-stu-id="82718-158">`<password>` is hello password you choose tooprotect hello certificate; it must be at least 6 characters long.</span></span> <span data-ttu-id="82718-159">Вы можете вовсе не указывать пароль, хотя это не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="82718-159">You can enter no password, although this is not recommended.</span></span>
* <span data-ttu-id="82718-160">`<dname>`— toobe hello различающееся имя X.500, связанный с псевдонимом и используется в качестве издателя hello и «тема» в hello самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="82718-160">`<dname>` is hello X.500 Distinguished Name toobe associated with alias, and is used as hello issuer and subject fields in hello self-signed certificate.</span></span>

<span data-ttu-id="82718-161">Дополнительные сведения см. в статье [Общие сведения о сертификатах для облачных служб Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="82718-161">For more information, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="upload-hello-certificate"></a><span data-ttu-id="82718-162">Отправка сертификата hello</span><span class="sxs-lookup"><span data-stu-id="82718-162">Upload hello certificate</span></span>
<span data-ttu-id="82718-163">tooupload tooAzure самозаверяющий сертификат, откройте toohello **параметры** hello классическом портале, а затем щелкните hello **сертификаты управления** вкладки. Нажмите кнопку **отправить** внизу hello hello страницы и перейдите в расположение toohello hello CER-файл был создан.</span><span class="sxs-lookup"><span data-stu-id="82718-163">tooupload a self-signed certificate tooAzure, go toohello **Settings** page in hello classic portal, then click hello **Management Certificates** tab. Click **Upload** at hello bottom of hello page and navigate toohello location of hello CER file you created.</span></span>

#### <a name="convert-hello-pfx-file-into-jks"></a><span data-ttu-id="82718-164">Преобразовать в JKS hello PFX-файла</span><span class="sxs-lookup"><span data-stu-id="82718-164">Convert hello PFX file into JKS</span></span>
<span data-ttu-id="82718-165">Hello командной строки Windows (работы в качестве администратора), каталог toohello компакт-диск, содержащий hello сертификаты и запуск hello следующую команду, где `<java-install-dir>` — hello каталог, в котором установлен Java на компьютере:</span><span class="sxs-lookup"><span data-stu-id="82718-165">In hello Windows Command Prompt (running as admin), cd toohello directory containing hello certificates and run hello following command, where `<java-install-dir>` is hello directory in which you installed Java on your computer:</span></span>

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. <span data-ttu-id="82718-166">При появлении запроса введите пароль ключей hello назначения; Это будет пароль hello для файла JKS hello.</span><span class="sxs-lookup"><span data-stu-id="82718-166">When prompted, enter hello destination keystore password; this will be hello password for hello JKS file.</span></span>
2. <span data-ttu-id="82718-167">При появлении запроса введите пароль ключей hello источника; Это будет пароль hello, указанное для hello PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="82718-167">When prompted, enter hello source keystore password; this is hello password you specified for hello PFX file.</span></span>

<span data-ttu-id="82718-168">два пароля Hello toobe hello же нет.</span><span class="sxs-lookup"><span data-stu-id="82718-168">hello two passwords do not have toobe hello same.</span></span> <span data-ttu-id="82718-169">Вы можете вовсе не указывать пароль, хотя это не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="82718-169">You can enter no password, although this is not recommended.</span></span>

## <a name="build-a-web-app-creation-application"></a><span data-ttu-id="82718-170">Сборка приложения для создания веб-приложения</span><span class="sxs-lookup"><span data-stu-id="82718-170">Build a Web App creation application</span></span>
### <a name="create-hello-eclipse-workspace-and-maven-project"></a><span data-ttu-id="82718-171">Создание hello рабочей области Eclipse и Maven проекта</span><span class="sxs-lookup"><span data-stu-id="82718-171">Create hello Eclipse Workspace and Maven Project</span></span>
<span data-ttu-id="82718-172">В этом разделе создайте рабочую область и проект для hello веб-приложения создания приложения с именем AzureWebDemo Maven.</span><span class="sxs-lookup"><span data-stu-id="82718-172">In this section you create a workspace and a Maven project for hello web app creation application, named AzureWebDemo.</span></span>

1. <span data-ttu-id="82718-173">Создайте проект Maven.</span><span class="sxs-lookup"><span data-stu-id="82718-173">Create a new Maven project.</span></span> <span data-ttu-id="82718-174">Щелкните **File > New > Maven Project** (Файл > Создать > Проект Maven).</span><span class="sxs-lookup"><span data-stu-id="82718-174">Click **File > New > Maven Project**.</span></span> <span data-ttu-id="82718-175">На странице **New Maven Project** (Новый проект Maven) выберите **Create a simple project** (Создать простой проект) и **Use default workspace location** (Использовать расположение рабочей области по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="82718-175">In **New Maven Project**, select **Create a simple project** and **Use default workspace location**.</span></span>
2. <span data-ttu-id="82718-176">На второй странице hello объекта **новый проект Maven**, укажите hello ниже:</span><span class="sxs-lookup"><span data-stu-id="82718-176">On hello second page of **New Maven Project**, specify hello following:</span></span>
   
   * <span data-ttu-id="82718-177">идентификатор группы — `com.<username>.azure.webdemo`</span><span class="sxs-lookup"><span data-stu-id="82718-177">Group ID: `com.<username>.azure.webdemo`</span></span>
   * <span data-ttu-id="82718-178">идентификатор артефакта — AzureWebDemo;</span><span class="sxs-lookup"><span data-stu-id="82718-178">Artifact ID: AzureWebDemo</span></span>
   * <span data-ttu-id="82718-179">версия— 0.0.1-SNAPSHOT;</span><span class="sxs-lookup"><span data-stu-id="82718-179">Version: 0.0.1-SNAPSHOT</span></span>
   * <span data-ttu-id="82718-180">упаковка — JAR;</span><span class="sxs-lookup"><span data-stu-id="82718-180">Packaging: jar</span></span>
   * <span data-ttu-id="82718-181">имя — AzureWebDemo.</span><span class="sxs-lookup"><span data-stu-id="82718-181">Name: AzureWebDemo</span></span>
     
     <span data-ttu-id="82718-182">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="82718-182">Click **Finish**.</span></span>
3. <span data-ttu-id="82718-183">Откройте файл pom.xml hello новый проект в обозревателе проектов.</span><span class="sxs-lookup"><span data-stu-id="82718-183">Open hello new project's pom.xml file in Project Explorer.</span></span> <span data-ttu-id="82718-184">Выберите hello **зависимости** вкладки. Так как это новый проект, здесь еще нет списка пакетов.</span><span class="sxs-lookup"><span data-stu-id="82718-184">Select hello **Dependencies** tab. As this is a new project, no packages are listed yet.</span></span>
4. <span data-ttu-id="82718-185">Просмотреть репозитории Привет открыть Maven.</span><span class="sxs-lookup"><span data-stu-id="82718-185">Open hello Maven Repositories view.</span></span> <span data-ttu-id="82718-186">Щелкните **Window > Show View > Other > Maven > Maven Repositories** (Окно > Показать представление > Другие > Maven > Репозитории Maven) и нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="82718-186">**Click Window > Show View > Other > Maven > Maven Repositories** and click **OK**.</span></span> <span data-ttu-id="82718-187">Hello **Maven репозиториев** представление появится внизу hello hello интегрированной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="82718-187">hello **Maven Repositories** view will appear at hello bottom of hello IDE.</span></span>
5. <span data-ttu-id="82718-188">Откройте **глобального репозиториев**, щелкните правой кнопкой мыши hello **центра** репозитория, а затем выберите **перестроение индекса**.</span><span class="sxs-lookup"><span data-stu-id="82718-188">Open **Global Repositories**, right-click hello **central** repository, and select **Rebuild Index**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="82718-189">Этот шаг может занять несколько минут в зависимости от скорости подключения к hello.</span><span class="sxs-lookup"><span data-stu-id="82718-189">This step can take several minutes depending on hello speed of your connection.</span></span> <span data-ttu-id="82718-190">Перестроение индекса hello, вы увидите hello пакетов Microsoft Azure в hello **центра** Maven репозитория.</span><span class="sxs-lookup"><span data-stu-id="82718-190">When hello index rebuilds, you should see hello Microsoft Azure packages in hello **central** Maven repository.</span></span>
6. <span data-ttu-id="82718-191">На вкладке **Dependencies** (Зависимости) щелкните **Add** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="82718-191">In **Dependencies**, click **Add**.</span></span> <span data-ttu-id="82718-192">В поле **Enter Group ID…** (Введите идентификатор группы…) введите `azure-management`.</span><span class="sxs-lookup"><span data-stu-id="82718-192">In **Enter Group ID...** enter `azure-management`.</span></span> <span data-ttu-id="82718-193">Выберите пакеты hello для базового управления и веб-приложений служб приложений.</span><span class="sxs-lookup"><span data-stu-id="82718-193">Select hello packages for base management and App Service Web Apps management:</span></span>
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > <span data-ttu-id="82718-194">**Примечание:** при обновлении зависимости hello после выпуска новой версии необходимо toore-добавить всех hello зависимых элементов в этом списке.</span><span class="sxs-lookup"><span data-stu-id="82718-194">**Note:** If you are updating hello dependencies after a new version release, you need toore-add each of hello dependencies in this list.</span></span>
   > <span data-ttu-id="82718-195">После нажатия кнопки **добавить** и выберите каждой зависимости, он отображается с hello новый номер версии в hello **зависимости** списка.</span><span class="sxs-lookup"><span data-stu-id="82718-195">After you click **Add** and select each dependency, it appears with hello new version number in hello **Dependencies** list.</span></span>
   > 
   > 

<span data-ttu-id="82718-196">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="82718-196">Click **OK**.</span></span> <span data-ttu-id="82718-197">Здравствуйте пакетов Azure, а затем отображаются в hello **зависимости** списка.</span><span class="sxs-lookup"><span data-stu-id="82718-197">hello Azure packages then appear in hello **Dependencies** list.</span></span>

### <a name="writing-java-code-toocreate-a-web-app-by-calling-hello-azure-sdk"></a><span data-ttu-id="82718-198">Написание кода Java tooCreate веб-приложения с вызовом hello Azure SDK</span><span class="sxs-lookup"><span data-stu-id="82718-198">Writing Java Code tooCreate a Web App by Calling hello Azure SDK</span></span>
<span data-ttu-id="82718-199">Затем напишите hello код, который вызывает API в hello Azure SDK для Java toocreate hello веб-приложения служб приложений.</span><span class="sxs-lookup"><span data-stu-id="82718-199">Next, write hello code that calls APIs in hello Azure SDK for Java toocreate hello App Service web app.</span></span>

1. <span data-ttu-id="82718-200">Создайте точки кода Java класс toocontain hello основные элементы.</span><span class="sxs-lookup"><span data-stu-id="82718-200">Create a Java class toocontain hello main entry point code.</span></span> <span data-ttu-id="82718-201">В обозревателе решений, правой кнопкой мыши узел проекта hello и выберите **Создать > класс**.</span><span class="sxs-lookup"><span data-stu-id="82718-201">In Project Explorer, right-click on hello project node and select **New > Class**.</span></span>
2. <span data-ttu-id="82718-202">В **новый класс Java**, имя класса hello `WebCreator` и проверьте hello **открытый методе static void main** флажок.</span><span class="sxs-lookup"><span data-stu-id="82718-202">In **New Java Class**, name hello class `WebCreator` and check hello **public static void main** checkbox.</span></span> <span data-ttu-id="82718-203">Выбор Hello должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="82718-203">hello selections should appear as follows:</span></span>
   
    ![][2]
3. <span data-ttu-id="82718-204">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="82718-204">Click **Finish**.</span></span> <span data-ttu-id="82718-205">Hello WebCreator.java файл появится в обозревателе проектов.</span><span class="sxs-lookup"><span data-stu-id="82718-205">hello WebCreator.java file appears in Project Explorer.</span></span>

### <a name="calling-hello-azure-api-toocreate-an-app-service-web-app"></a><span data-ttu-id="82718-206">Вызов веб-приложение службы приложения hello tooCreate Azure API</span><span class="sxs-lookup"><span data-stu-id="82718-206">Calling hello Azure API tooCreate an App Service Web App</span></span>
#### <a name="add-necessary-imports"></a><span data-ttu-id="82718-207">Добавление необходимых операций импорта</span><span class="sxs-lookup"><span data-stu-id="82718-207">Add necessary imports</span></span>
<span data-ttu-id="82718-208">В WebCreator.java добавьте следующие импорты; hello Эти операции импорта предоставляют доступ tooclasses в hello библиотеки управления для использования API-интерфейсов Azure:</span><span class="sxs-lookup"><span data-stu-id="82718-208">In WebCreator.java, add hello following imports; these imports provide access tooclasses in hello management libraries for consuming Azure APIs:</span></span>

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


#### <a name="define-hello-main-entry-point-class"></a><span data-ttu-id="82718-209">Определите класс точки hello основные элементы</span><span class="sxs-lookup"><span data-stu-id="82718-209">Define hello main entry point class</span></span>
<span data-ttu-id="82718-210">Для этого приложения, так как hello hello AzureWebDemo приложения служит toocreate веб-приложение службы приложения, name hello основной класс `WebAppCreator`.</span><span class="sxs-lookup"><span data-stu-id="82718-210">Because hello purpose of hello AzureWebDemo application is toocreate an App Service Web App, name hello main class for this application `WebAppCreator`.</span></span> <span data-ttu-id="82718-211">Этот класс предоставляет hello основные элементы точки кода, который вызывает hello API управления службами Azure toocreate hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="82718-211">This class provides hello main entry point code that calls hello Azure Service Management API toocreate hello web app.</span></span>

<span data-ttu-id="82718-212">Добавьте следующие определения параметров для hello веб-приложения и веб-пространства hello.</span><span class="sxs-lookup"><span data-stu-id="82718-212">Add hello following parameter definitions for hello web app and webspace.</span></span> <span data-ttu-id="82718-213">Необходимо будет tooprovide свои собственные подписки Azure код и сведения о сертификате.</span><span class="sxs-lookup"><span data-stu-id="82718-213">You will need tooprovide your own Azure subscription ID and certificate information.</span></span>

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

<span data-ttu-id="82718-214">Описание:</span><span class="sxs-lookup"><span data-stu-id="82718-214">where:</span></span>

* <span data-ttu-id="82718-215">`<subscription-id>`— Идентификатор подписки Azure hello, которой требуется toocreate hello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="82718-215">`<subscription-id>` is hello Azure subscription ID in which you want toocreate hello resource.</span></span>
* <span data-ttu-id="82718-216">`<certificate-store-path>`— hello путь и имя файла toohello JKS файл в каталоге хранилища локальный сертификат.</span><span class="sxs-lookup"><span data-stu-id="82718-216">`<certificate-store-path>` is hello path and filename toohello JKS file in your local certificate store directory.</span></span> <span data-ttu-id="82718-217">(например, `C:/Certificates/CertificateName.jks` — для Linux, а `C:\Certificates\CertificateName.jks` — для Windows);</span><span class="sxs-lookup"><span data-stu-id="82718-217">For example, `C:/Certificates/CertificateName.jks` for Linux and `C:\Certificates\CertificateName.jks` for Windows.</span></span>
* <span data-ttu-id="82718-218">`<certificate-password>`— пароль hello, указываемое при создании сертификата JKS.</span><span class="sxs-lookup"><span data-stu-id="82718-218">`<certificate-password>` is hello password you specified when you created your JKS certificate.</span></span>
* <span data-ttu-id="82718-219">`webAppName`можно использовать любое имя выбранного; в этой процедуре используется имя hello `WebDemoWebApp`.</span><span class="sxs-lookup"><span data-stu-id="82718-219">`webAppName` can be any name you choose; this procedure uses hello name `WebDemoWebApp`.</span></span> <span data-ttu-id="82718-220">Hello полное имя домена — hello `webAppName` с hello `domainName` добавляются, поэтому в этом случае hello полное имя домена — `webdemowebapp.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="82718-220">hello full domain name is hello `webAppName` with hello `domainName` appended, so in this case hello full domain is `webdemowebapp.azurewebsites.net`.</span></span>
* <span data-ttu-id="82718-221">`domainName` следует указать, как показано выше;</span><span class="sxs-lookup"><span data-stu-id="82718-221">`domainName` should be specified as shown above.</span></span>
* <span data-ttu-id="82718-222">`webSpaceName`должен иметь одно из значений hello, определенных в hello [WebSpaceNames] [ WebSpaceNames] класса.</span><span class="sxs-lookup"><span data-stu-id="82718-222">`webSpaceName` should be one of hello values defined in hello [WebSpaceNames][WebSpaceNames] class.</span></span>
* <span data-ttu-id="82718-223">`appServicePlanName` следует указать, как показано выше;</span><span class="sxs-lookup"><span data-stu-id="82718-223">`appServicePlanName` should be specified as shown above.</span></span>

> <span data-ttu-id="82718-224">**Примечание:** каждый раз при запуске этого приложения, вы должны значение hello toochange `webAppName` и `appServicePlanName` (или удалить веб-приложение hello на портале Azure hello) перед запуском приложения hello еще раз.</span><span class="sxs-lookup"><span data-stu-id="82718-224">**Note:** Each time you run this application, you need toochange hello value of `webAppName` and `appServicePlanName` (or delete hello web app on hello Azure Portal) before running hello application again.</span></span> <span data-ttu-id="82718-225">В противном случае выполнение завершится ошибкой, так как hello того же ресурса уже существует в Azure.</span><span class="sxs-lookup"><span data-stu-id="82718-225">Otherwise, execution will fail because hello same resource already exists on Azure.</span></span>
> 
> 

#### <a name="define-hello-web-creation-method"></a><span data-ttu-id="82718-226">Определение метода создания hello web</span><span class="sxs-lookup"><span data-stu-id="82718-226">Define hello web creation method</span></span>
<span data-ttu-id="82718-227">Далее следует определите метод toocreate hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="82718-227">Next, define a method toocreate hello web app.</span></span> <span data-ttu-id="82718-228">Этот метод `createWebApp`, определяет параметры hello hello веб-приложения и веб-пространства hello.</span><span class="sxs-lookup"><span data-stu-id="82718-228">This method, `createWebApp`, specifies hello parameters of hello web app and hello webspace.</span></span> <span data-ttu-id="82718-229">Он также создает и настраивает hello веб-приложений приложения служб управления клиента, который определяется hello [WebSiteManagementClient] [ WebSiteManagementClient] объекта.</span><span class="sxs-lookup"><span data-stu-id="82718-229">It also creates and configures hello App Service Web Apps management client, which is defined by hello [WebSiteManagementClient][WebSiteManagementClient] object.</span></span> <span data-ttu-id="82718-230">клиент управления Hello — ключа toocreating веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="82718-230">hello management client is key toocreating Web Apps.</span></span> <span data-ttu-id="82718-231">Он предоставляет веб-служб RESTful, позволяющие приложениям toomanage веб-приложения (выполнение операций, таких как создание, update и delete) путем вызова API управления службами hello.</span><span class="sxs-lookup"><span data-stu-id="82718-231">It provides RESTful web services that allow applications toomanage web apps (performing operations such as create, update, and delete) by calling hello service management API.</span></span>

    private static void createWebApp() throws Exception {

        // Specify configuration settings for hello App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path toohello JKS file
            keyStorePassword,  // Password for hello JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create hello App Service Web Apps management client toocall Azure APIs
        // and pass it hello App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for hello web app with hello specified parameters.
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
        // Note that hello server farm name takes hello Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define hello web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create hello web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output hello HTTP status code of hello response; 200 indicates hello request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output hello name of hello web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

<span data-ttu-id="82718-232">Hello код будет выводить код состояния HTTP hello hello ответа об успехе или неудаче и в случае успешного выполнения будет выводить имя hello hello веб-приложение создано.</span><span class="sxs-lookup"><span data-stu-id="82718-232">hello code will output hello HTTP status of hello response indicating success or failure, and if successful, will output hello name of hello created web app.</span></span>

#### <a name="define-hello-main-method"></a><span data-ttu-id="82718-233">Определите метод main() hello</span><span class="sxs-lookup"><span data-stu-id="82718-233">Define hello main() method</span></span>
<span data-ttu-id="82718-234">Укажите код метода main() hello вызовов createWebApp() toocreate hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="82718-234">Provide hello main() method code that calls createWebApp() toocreate hello web app.</span></span>

<span data-ttu-id="82718-235">Наконец, вызовите `createWebApp` из `main`:</span><span class="sxs-lookup"><span data-stu-id="82718-235">Finally, call `createWebApp` from `main`:</span></span>

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-hello-application-and-verify-web-app-creation"></a><span data-ttu-id="82718-236">Проверка создания веб-приложения и приложение hello</span><span class="sxs-lookup"><span data-stu-id="82718-236">Run hello application and verify web app creation</span></span>
<span data-ttu-id="82718-237">tooverify, приложение работает, нажмите кнопку **запуска > запустить**.</span><span class="sxs-lookup"><span data-stu-id="82718-237">tooverify that your application runs, click **Run > Run**.</span></span> <span data-ttu-id="82718-238">По завершении работы приложения hello появятся следующие выходные данные в консоли Eclipse hello hello:</span><span class="sxs-lookup"><span data-stu-id="82718-238">When hello application completes running, you should see hello following output in hello Eclipse console:</span></span>

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

<span data-ttu-id="82718-239">Войдите на классический портал Azure hello и щелкните **веб-приложений**.</span><span class="sxs-lookup"><span data-stu-id="82718-239">Log into hello Azure classic portal and click **Web Apps**.</span></span> <span data-ttu-id="82718-240">новое веб-приложение Hello должно отображаться в списке веб-приложения hello в течение нескольких минут.</span><span class="sxs-lookup"><span data-stu-id="82718-240">hello new web app should appear in hello Web Apps list within a few minutes.</span></span>

## <a name="deploying-an-application-toohello-web-app"></a><span data-ttu-id="82718-241">Развертывание приложения toohello веб-приложения</span><span class="sxs-lookup"><span data-stu-id="82718-241">Deploying an Application toohello Web App</span></span>
<span data-ttu-id="82718-242">После запуска AzureWebDemo и создать новое веб-приложение hello, журнала hello классический портал, щелкните **веб-приложений**и выберите **WebDemoWebApp** в hello **веб-приложений** списка.</span><span class="sxs-lookup"><span data-stu-id="82718-242">After you have run AzureWebDemo and created hello new web app, log into hello classic portal, click **Web Apps**, and select **WebDemoWebApp** in hello **Web Apps** list.</span></span> <span data-ttu-id="82718-243">Нажмите кнопку на странице панели мониторинга веб-приложения hello **Обзор** (или выберите URL-адрес hello, `webdemowebapp.azurewebsites.net`) toonavigate tooit.</span><span class="sxs-lookup"><span data-stu-id="82718-243">In hello web app's dashboard page, click **Browse** (or click hello URL, `webdemowebapp.azurewebsites.net`) toonavigate tooit.</span></span> <span data-ttu-id="82718-244">Так как содержимое не была toohello опубликованных веб-приложения еще вы увидите страницу пустым заполнителем.</span><span class="sxs-lookup"><span data-stu-id="82718-244">You will see a blank placeholder page, because no content has been published toohello web app yet.</span></span>

<span data-ttu-id="82718-245">Затем будет создать приложение «Hello World» и развернуть его toohello веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="82718-245">Next you will create a "Hello World" application and deploy it toohello web app.</span></span>

### <a name="create-a-jsp-hello-world-application"></a><span data-ttu-id="82718-246">Создание приложения JSP Hello World</span><span class="sxs-lookup"><span data-stu-id="82718-246">Create a JSP Hello World application</span></span>
#### <a name="create-hello-application"></a><span data-ttu-id="82718-247">Создание приложения hello</span><span class="sxs-lookup"><span data-stu-id="82718-247">Create hello application</span></span>
<span data-ttu-id="82718-248">В порядке toodemonstrate как hello toodeploy toohello веб-приложение, следуя процедуре показано, как toocreate простого приложения «Hello World» Java и отправьте его toohello приложения службы веб-приложения, создать ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="82718-248">In order toodemonstrate how toodeploy an application toohello web, hello following procedure shows you how toocreate a simple "Hello World" Java application and upload it toohello App Service Web App that your application created.</span></span>

1. <span data-ttu-id="82718-249">Щелкните **File > New > Dynamic Web Project** (Файл > Создать > Динамический веб-проект).</span><span class="sxs-lookup"><span data-stu-id="82718-249">Click **File > New > Dynamic Web Project**.</span></span> <span data-ttu-id="82718-250">Назовите его `JSPHello`.</span><span class="sxs-lookup"><span data-stu-id="82718-250">Name it `JSPHello`.</span></span> <span data-ttu-id="82718-251">Необязательно toochange другие параметры в этом диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="82718-251">You do not need toochange any other settings in this dialog.</span></span> <span data-ttu-id="82718-252">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="82718-252">Click **Finish**.</span></span>
   
    ![][3]
2. <span data-ttu-id="82718-253">В обозревателе проектов разверните hello **JSPHello** щелкните правой кнопкой мыши проект **WebContent**, нажмите кнопку **Создать > JSP-файл**.</span><span class="sxs-lookup"><span data-stu-id="82718-253">In Project Explorer, expand hello **JSPHello** project, right-click **WebContent**, then click **New > JSP File**.</span></span> <span data-ttu-id="82718-254">В диалоговом окне приветствия Создание JSP-файла, имя нового файла hello `index.jsp`.</span><span class="sxs-lookup"><span data-stu-id="82718-254">In hello New JSP File dialog, name hello new file `index.jsp`.</span></span> <span data-ttu-id="82718-255">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="82718-255">Click **Next**.</span></span>
3. <span data-ttu-id="82718-256">В hello **Выбор шаблона JSP** диалоговое окно, выберите **новый JSP-файл (html)** и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="82718-256">In hello **Select JSP Template** dialog, select **New JSP File (html)** and click **Finish**.</span></span>
4. <span data-ttu-id="82718-257">В index.jsp, добавьте следующий код в hello hello `<head>` и `<body>` тег разделы:</span><span class="sxs-lookup"><span data-stu-id="82718-257">In index.jsp, add hello following code in hello `<head>` and `<body>` tag sections:</span></span>
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, hello time is <%= date %> 
        </body>

#### <a name="run-hello-hello-world-application-in-localhost"></a><span data-ttu-id="82718-258">Запустите приложение Hello World hello в localhost</span><span class="sxs-lookup"><span data-stu-id="82718-258">Run hello Hello World application in localhost</span></span>
<span data-ttu-id="82718-259">Для запуска этого приложения tooconfigure необходимо несколько свойств.</span><span class="sxs-lookup"><span data-stu-id="82718-259">Before you run this application, you need tooconfigure a few properties.</span></span>

1. <span data-ttu-id="82718-260">Щелкните правой кнопкой мыши hello **JSPHello** проект и выберите **свойства**.</span><span class="sxs-lookup"><span data-stu-id="82718-260">Right-click hello **JSPHello** project and select **Properties**.</span></span>
2. <span data-ttu-id="82718-261">В hello **свойства** диалоговое окно: выберите **путь построения Java**выберите hello **заказа и экспортировать** установите флажок **JRE системная библиотека**, нажмите кнопку **Копирование** toomove его toohello вверху списка hello.</span><span class="sxs-lookup"><span data-stu-id="82718-261">In hello **Properties** dialog: select **Java Build Path**, select hello **Order and Export** tab, check **JRE System Library**, then click **Up** toomove it toohello top of hello list.</span></span>
   
    ![][4]
3. <span data-ttu-id="82718-262">Кроме того, в hello **свойства** диалоговое окно: выберите **целевых сред выполнения** и нажмите кнопку **New**.</span><span class="sxs-lookup"><span data-stu-id="82718-262">Also in hello **Properties** dialog: select **Targeted Runtimes** and click **New**.</span></span>
4. <span data-ttu-id="82718-263">В hello **новой среды выполнения сервера** диалоговое окно, выберите сервер, такие как **v7.0 Apache Tomcat** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="82718-263">In hello **New Server Runtime Environment** dialog, select a server such as **Apache Tomcat v7.0** and click **Next**.</span></span> <span data-ttu-id="82718-264">В hello **сервера Tomcat** диалогового окна, набор **имя** слишком`Apache Tomcat v7.0`и задайте **каталог установки Tomcat** toohello каталога, в котором установлена версия hello Вы хотите toouse сервера Tomcat.</span><span class="sxs-lookup"><span data-stu-id="82718-264">In hello **Tomcat Server** dialog, set **Name** too`Apache Tomcat v7.0`, and set **Tomcat Installation Directory** toohello directory in which you installed hello version of Tomcat server you want toouse.</span></span>
   
    ![][5]
   
    <span data-ttu-id="82718-265">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="82718-265">Click **Finish**.</span></span>
5. <span data-ttu-id="82718-266">Затем вернитесь toohello **целевых сред выполнения** страница hello **свойства** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="82718-266">You then return toohello **Targeted Runtimes** page of hello **Properties** dialog.</span></span> <span data-ttu-id="82718-267">Выберите **Apache Tomcat v7.0** и нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="82718-267">Select **Apache Tomcat v7.0**, then click **OK**.</span></span>
   
    ![][6]
6. <span data-ttu-id="82718-268">В hello Eclipse **запуска** меню, нажмите кнопку **запуска**.</span><span class="sxs-lookup"><span data-stu-id="82718-268">In hello Eclipse **Run** menu, click **Run**.</span></span> <span data-ttu-id="82718-269">В hello **запуска от имени** диалогового окна выберите **выполняются на сервере**.</span><span class="sxs-lookup"><span data-stu-id="82718-269">In hello **Run As** dialog, select **Run on Server**.</span></span> <span data-ttu-id="82718-270">В hello **выполняются на сервере** диалогового окна выберите **Tomcat v7.0 сервера**:</span><span class="sxs-lookup"><span data-stu-id="82718-270">In hello **Run on Server** dialog, select **Tomcat v7.0 Server**:</span></span>
   
    ![][7]
   
    <span data-ttu-id="82718-271">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="82718-271">Click **Finish**.</span></span>
7. <span data-ttu-id="82718-272">Здравствуйте, когда приложение будет работать, вы увидите hello **JSPHello** страницы отображаются в окне localhost в Eclipse (`http://localhost:8080/JSPHello/`), параметры отображения hello следующего сообщения:</span><span class="sxs-lookup"><span data-stu-id="82718-272">When hello application runs, you should see hello **JSPHello** page appear in a localhost window in Eclipse (`http://localhost:8080/JSPHello/`), displaying hello following message:</span></span>
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-hello-application-as-a-war"></a><span data-ttu-id="82718-273">Экспорт приложения hello как WAR</span><span class="sxs-lookup"><span data-stu-id="82718-273">Export hello application as a WAR</span></span>
<span data-ttu-id="82718-274">Экспортируйте файлы веб-проекта hello веб-архив (WAR), чтобы ее можно было развернуть toohello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="82718-274">Export hello web project files as a web archive (WAR) file so that you can deploy it toohello web app.</span></span> <span data-ttu-id="82718-275">Hello следующие файлы веб-проекта находятся в папке WebContent hello:</span><span class="sxs-lookup"><span data-stu-id="82718-275">hello following web project files reside in hello WebContent folder:</span></span>

    META-INF
    WEB-INF
    index.jsp

1. <span data-ttu-id="82718-276">Щелкните правой кнопкой мыши папку WebContent hello и выберите **Экспорт**.</span><span class="sxs-lookup"><span data-stu-id="82718-276">Right-click hello WebContent folder and select **Export**.</span></span>
2. <span data-ttu-id="82718-277">В hello **экспорта выберите** диалоговое окно, нажмите кнопку **Web > WAR** файла, после чего нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="82718-277">In hello **Export Select** dialog, click **Web > WAR** file, then click **Next**.</span></span>
3. <span data-ttu-id="82718-278">В hello **Экспорт WAR** диалоговое окно, выберите каталог src hello в текущем проекте hello и включать имя hello hello WAR-файл в конце hello.</span><span class="sxs-lookup"><span data-stu-id="82718-278">In hello **WAR Export** dialog, select hello src directory in hello current project, and include hello name of hello WAR file at hello end.</span></span> <span data-ttu-id="82718-279">Например:</span><span class="sxs-lookup"><span data-stu-id="82718-279">For example:</span></span>
   
    `<project-path>/JSPHello/src/JSPHello.war`

<span data-ttu-id="82718-280">Дополнительные сведения о развертывании WAR-файлы см. в разделе [добавить tooAzure приложения Java веб-приложений служб приложения](web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="82718-280">For more information on deploying WAR files, see [Add a Java application tooAzure App Service Web Apps](web-sites-java-add-app.md).</span></span>

### <a name="deploying-hello-hello-world-application-using-ftp"></a><span data-ttu-id="82718-281">Развертывание FTP с помощью приложения Hello World hello</span><span class="sxs-lookup"><span data-stu-id="82718-281">Deploying hello Hello World Application Using FTP</span></span>
<span data-ttu-id="82718-282">Выберите приложение hello toopublish клиента FTP сторонних разработчиков.</span><span class="sxs-lookup"><span data-stu-id="82718-282">Select a third-party FTP client toopublish hello application.</span></span> <span data-ttu-id="82718-283">Эта процедура описывает два варианта: hello Kudu консоли встроены в Azure; и FileZilla популярным средством удобны, графический пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="82718-283">This procedure describes two options: hello Kudu console built into Azure; and FileZilla, a popular tool with a convenient, graphical UI.</span></span>

> <span data-ttu-id="82718-284">**Примечание:** hello набора средств Azure для Eclipse поддерживает учетные записи toostorage развертывания и облачных служб, однако в настоящее время не поддерживает приложения tooweb развертывания.</span><span class="sxs-lookup"><span data-stu-id="82718-284">**Note:** hello Azure Toolkit for Eclipse supports deployment toostorage accounts and cloud services, but does not currently support deployment tooweb apps.</span></span> <span data-ttu-id="82718-285">Вы можете развернуть toostorage учетные записи и облачные службы, используя проект развертывания Azure, как описано в [Создание приложения Hello World для Azure в Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), но не tooweb приложений.</span><span class="sxs-lookup"><span data-stu-id="82718-285">You can deploy toostorage accounts and cloud services using an Azure Deployment Project as described in [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), but not tooweb apps.</span></span> <span data-ttu-id="82718-286">Используете другие методы, например FTP или GitHub tootransfer файлы tooyour веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="82718-286">Use other methods such as FTP or GitHub tootransfer files tooyour web app.</span></span>
> 
> <span data-ttu-id="82718-287">**Примечание:** не рекомендуется использовать FTP из командной строки Windows hello (hello FTP.EXE программа, поставляемая с Windows).</span><span class="sxs-lookup"><span data-stu-id="82718-287">**Note:** We do not recommend using FTP from hello Windows command prompt (hello command-line FTP.EXE utility that ships with Windows).</span></span> <span data-ttu-id="82718-288">FTP-клиенты, использующие active FTP, таких как FTP.EXE, часто при сбое toowork брандмауэры.</span><span class="sxs-lookup"><span data-stu-id="82718-288">FTP clients that use active FTP, such as FTP.EXE, often fail toowork over firewalls.</span></span> <span data-ttu-id="82718-289">Активный режим FTP Указывает внутренний адрес Локальных сетей, toowhich FTP-сервер может завершиться неудачей tooconnect.</span><span class="sxs-lookup"><span data-stu-id="82718-289">Active FTP specifies an internal LAN-based address, toowhich an FTP server will likely fail tooconnect.</span></span>
> 
> 

<span data-ttu-id="82718-290">Дополнительные сведения о веб-службы приложений tooan развертывания приложения с помощью протокола FTP. в разделе hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="82718-290">For more information on deployment tooan App Service web app using FTP, see hello following topics:</span></span>

* [<span data-ttu-id="82718-291">Развертывание с помощью служебной программы FTP</span><span class="sxs-lookup"><span data-stu-id="82718-291">Deploy using an FTP utility</span></span>](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a><span data-ttu-id="82718-292">"Настройка учетных данных для развертывания"</span><span class="sxs-lookup"><span data-stu-id="82718-292">Set up deployment credentials</span></span>
<span data-ttu-id="82718-293">Убедитесь, что вы запустили hello **AzureWebDemo** toocreate приложения веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="82718-293">Make sure you have run hello **AzureWebDemo** application toocreate a web app.</span></span> <span data-ttu-id="82718-294">Расположение файлов toothis будут перенесены.</span><span class="sxs-lookup"><span data-stu-id="82718-294">You will transfer files toothis location.</span></span>

1. <span data-ttu-id="82718-295">Войдите на классический портал hello и щелкните **веб-приложений**.</span><span class="sxs-lookup"><span data-stu-id="82718-295">Log into hello classic portal and click **Web Apps**.</span></span> <span data-ttu-id="82718-296">Убедитесь, что **WebDemoWebApp** отображается в списке hello веб-приложений и убедитесь, что он работает.</span><span class="sxs-lookup"><span data-stu-id="82718-296">Make sure **WebDemoWebApp** appears in hello list of web apps, and make sure that it is running.</span></span> <span data-ttu-id="82718-297">Нажмите кнопку **WebDemoWebApp** tooopen его **мониторинга** страницы.</span><span class="sxs-lookup"><span data-stu-id="82718-297">Click **WebDemoWebApp** tooopen its **Dashboard** page.</span></span>
2. <span data-ttu-id="82718-298">На hello **мониторинга** в разделе **быстрый обзор**, нажмите кнопку **настроить учетные данные развертывания** (Если вы уже есть учетные данные развертывания, эта функция считывает  **Сброс учетных данных развертывания**).</span><span class="sxs-lookup"><span data-stu-id="82718-298">On hello **Dashboard** page, under **Quick Glance**, click **Set up your deployment credentials** (if you already have deployment credentials, this reads **Reset your deployment credentials**).</span></span>
   
    <span data-ttu-id="82718-299">Учетные данные развертывания связаны с учетной записью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="82718-299">Deployment credentials are associated with a Microsoft account.</span></span> <span data-ttu-id="82718-300">Необходимо toospecify имя пользователя и пароль, которые можно использовать toodeploy, с помощью Git и FTP.</span><span class="sxs-lookup"><span data-stu-id="82718-300">You need toospecify a username and password that you can use toodeploy using Git and FTP.</span></span> <span data-ttu-id="82718-301">Эти учетные данные toodeploy tooany веб-приложения можно использовать во все подписки Azure, связанный с учетной записью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="82718-301">You can use these credentials toodeploy tooany web app in all Azure subscriptions associated with your Microsoft account.</span></span> <span data-ttu-id="82718-302">Учетные данные Git и FTP-развертывания в диалоговом окне приветствия, записей hello имя пользователя и пароль для использования в будущем.</span><span class="sxs-lookup"><span data-stu-id="82718-302">Provide Git and FTP deployment credentials in hello dialog, and record hello username and password for future use.</span></span>

#### <a name="get-ftp-connection-information"></a><span data-ttu-id="82718-303">Получение информации о подключении по FTP</span><span class="sxs-lookup"><span data-stu-id="82718-303">Get FTP connection information</span></span>
<span data-ttu-id="82718-304">toouse FTP toodeploy приложения файлы toohello только что созданный веб-приложения, необходимо tooobtain сведения о соединении.</span><span class="sxs-lookup"><span data-stu-id="82718-304">toouse FTP toodeploy application files toohello newly created web app, you need tooobtain connection information.</span></span> <span data-ttu-id="82718-305">Существует два способа tooobtain сведения о соединении.</span><span class="sxs-lookup"><span data-stu-id="82718-305">There are two ways tooobtain connection information.</span></span> <span data-ttu-id="82718-306">Одним из способов toovisit hello веб-приложения **мониторинга** страницы; hello другим способом является профиль публикации toodownload hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="82718-306">One way is toovisit hello web app's **Dashboard** page; hello other way is toodownload hello web app's publish profile.</span></span> <span data-ttu-id="82718-307">профиль публикации Hello XML-файл, предоставляющий сведения, например учетных данных имя входа и узла FTP для веб-приложения в службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="82718-307">hello publish profile is an XML file that provides information such as FTP host name and logon credentials for your web apps in Azure App Service.</span></span> <span data-ttu-id="82718-308">Во всех подписках, связанных с hello учетная запись Azure, не только этого класса, можно использовать это имя пользователя и пароль toodeploy tooany веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="82718-308">You can use this username and password toodeploy tooany web app in all subscriptions associated with hello Azure account, not only this one.</span></span>

<span data-ttu-id="82718-309">сведения о соединении tooobtain FTP из колонки веб-приложения hello в hello [портала Azure][Azure Portal]:</span><span class="sxs-lookup"><span data-stu-id="82718-309">tooobtain FTP connection information from hello web app's blade in hello [Azure Portal][Azure Portal]:</span></span>

1. <span data-ttu-id="82718-310">В разделе **Essentials**, найдите и скопируйте hello **имя узла FTP**.</span><span class="sxs-lookup"><span data-stu-id="82718-310">Under **Essentials**, find and copy hello **FTP hostname**.</span></span> <span data-ttu-id="82718-311">Это URI следующего слишком`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="82718-311">This is a URI similar too`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span></span>
2. <span data-ttu-id="82718-312">В разделе **Основные компоненты** найдите и скопируйте **имя пользователя FTP или развертывания**.</span><span class="sxs-lookup"><span data-stu-id="82718-312">Under **Essentials**, find and copy **FTP/Deployment username**.</span></span> <span data-ttu-id="82718-313">Этот файл может иметь форму hello *webappname\deployment-username*, например `WebDemoWebApp\deployer77`.</span><span class="sxs-lookup"><span data-stu-id="82718-313">This will have hello form *webappname\deployment-username*; for example `WebDemoWebApp\deployer77`.</span></span>

<span data-ttu-id="82718-314">сведения о соединении с FTP tooobtain из hello профиль публикации:</span><span class="sxs-lookup"><span data-stu-id="82718-314">tooobtain FTP connection information from hello publish profile:</span></span>

1. <span data-ttu-id="82718-315">В колонке hello веб-приложение, нажмите кнопку **получение профиля публикации**.</span><span class="sxs-lookup"><span data-stu-id="82718-315">In hello web app's blade, click **Get publish profile**.</span></span> <span data-ttu-id="82718-316">Будет загружен файл .publishsettings tooyour локального диска.</span><span class="sxs-lookup"><span data-stu-id="82718-316">This will download a .publishsettings file tooyour local drive.</span></span>
2. <span data-ttu-id="82718-317">Откройте файл PUBLISHSETTINGS hello в редакторе XML или текстовом редакторе и найдите hello `<publishProfile>` элемента, содержащего `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="82718-317">Open hello .publishsettings file in an XML editor or text editor and find hello `<publishProfile>` element containing `publishMethod="FTP"`.</span></span> <span data-ttu-id="82718-318">Он должен выглядеть hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="82718-318">It should look like hello following:</span></span>
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. <span data-ttu-id="82718-319">Обратите внимание, что веб-приложение hello `publishProfile` сопоставление параметров настройки диспетчера сайта FileZilla toohello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="82718-319">Note that hello web app's `publishProfile` settings map toohello FileZilla Site Manager settings as follows:</span></span>

* <span data-ttu-id="82718-320">`publishUrl`Здравствуйте, таким же, как **имя узла FTP**, hello значение, заданное в **узла**.</span><span class="sxs-lookup"><span data-stu-id="82718-320">`publishUrl` is hello same as **FTP host name**, hello value you set in **Host**.</span></span>
* <span data-ttu-id="82718-321">`publishMethod="FTP"`означает, что вы значение **протокола** слишком**FTP - File Transfer Protocol**, и **шифрования** слишком**использовать обычный FTP**.</span><span class="sxs-lookup"><span data-stu-id="82718-321">`publishMethod="FTP"` means that you set **Protocol** too**FTP - File Transfer Protocol**, and **Encryption** too**Use plain FTP**.</span></span>
* <span data-ttu-id="82718-322">`userName`и `userPWD` являются ключевыми для hello фактических значений имя пользователя и пароль, указанный при сбросе hello учетные данные развертывания.</span><span class="sxs-lookup"><span data-stu-id="82718-322">`userName` and `userPWD` are keys for hello actual username and password values you specified when you reset hello deployment credentials.</span></span> <span data-ttu-id="82718-323">`userName`Здравствуйте, таким же, как **развертывание / пользователь FTP**.</span><span class="sxs-lookup"><span data-stu-id="82718-323">`userName` is hello same as **Deployment / FTP user**.</span></span> <span data-ttu-id="82718-324">Они сопоставляют слишком**пользователя** и **пароль** в FileZilla.</span><span class="sxs-lookup"><span data-stu-id="82718-324">They map too**User** and **Password** in FileZilla.</span></span>
* <span data-ttu-id="82718-325">`ftpPassiveMode="True"`означает, что этот узел hello FTP использует пассивный FTP-ПОРТ передача; Выберите **пассивный** на hello **параметры передачи** вкладки.</span><span class="sxs-lookup"><span data-stu-id="82718-325">`ftpPassiveMode="True"` means that hello FTP site uses passive FTP transfer; select **Passive** on hello **Transfer Settings** tab.</span></span>

#### <a name="configure-hello-web-app-toohost-a-java-application"></a><span data-ttu-id="82718-326">Настройка веб-приложения hello toohost приложения Java</span><span class="sxs-lookup"><span data-stu-id="82718-326">Configure hello Web App toohost a Java application</span></span>
<span data-ttu-id="82718-327">Прежде чем публиковать приложение hello, необходимо toochange несколько параметров конфигурации, чтобы hello веб-приложения можно разместить приложение Java.</span><span class="sxs-lookup"><span data-stu-id="82718-327">Before you publish hello application, you need toochange a few configuration settings so that hello web app can host a Java application.</span></span>

1. <span data-ttu-id="82718-328">Hello классического портала, go toohello веб-приложения **мониторинга** и нажмите кнопку **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="82718-328">In hello classic portal, go toohello web app's **Dashboard** page and click **Configure**.</span></span> <span data-ttu-id="82718-329">На hello **Настройка** укажите следующие параметры hello.</span><span class="sxs-lookup"><span data-stu-id="82718-329">On hello **Configure** page, specify hello following settings.</span></span>
2. <span data-ttu-id="82718-330">В **версии Java** по умолчанию hello — **Off**; выберите версии Java hello ориентировано приложение, например 1.7.0_51.</span><span class="sxs-lookup"><span data-stu-id="82718-330">In **Java version** hello default is **Off**; select hello Java version your application targets; for example 1.7.0_51.</span></span> <span data-ttu-id="82718-331">После этого, также убедитесь, что **контейнера Web** задано tooa версию сервера Tomcat.</span><span class="sxs-lookup"><span data-stu-id="82718-331">After you do this, also make sure that **Web container** is set tooa version of Tomcat Server.</span></span>
3. <span data-ttu-id="82718-332">В **документов по умолчанию**добавьте index.jsp и переместите его вверх toohello вверху списка hello.</span><span class="sxs-lookup"><span data-stu-id="82718-332">In **Default Documents**, add index.jsp and move it up toohello top of hello list.</span></span> <span data-ttu-id="82718-333">(файл по умолчанию hello для веб-приложений — hostingstart.html).</span><span class="sxs-lookup"><span data-stu-id="82718-333">(hello default file for web apps is hostingstart.html.)</span></span>
4. <span data-ttu-id="82718-334">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="82718-334">Click **Save**.</span></span>

#### <a name="publish-your-application-using-kudu"></a><span data-ttu-id="82718-335">Публикация приложения с помощью Kudu</span><span class="sxs-lookup"><span data-stu-id="82718-335">Publish your application using Kudu</span></span>
<span data-ttu-id="82718-336">Одним из способов toopublish приложения hello — toouse hello, Kudu отладки консоли, встроенные в Azure.</span><span class="sxs-lookup"><span data-stu-id="82718-336">One way toopublish hello application is toouse hello Kudu debug console built into Azure.</span></span> <span data-ttu-id="82718-337">Kudu известен toobe стабильное и согласованное с веб-приложений служб приложений и сервера Tomcat.</span><span class="sxs-lookup"><span data-stu-id="82718-337">Kudu is known toobe stable and consistent with App Service Web Apps and Tomcat Server.</span></span> <span data-ttu-id="82718-338">Для доступа к консоли hello hello веб-приложения путем просмотра URL-адрес tooa hello следующие формы:</span><span class="sxs-lookup"><span data-stu-id="82718-338">You access hello console for hello web app by browsing tooa URL of hello following form:</span></span>

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. <span data-ttu-id="82718-339">Для выполнения этой процедуры hello Kudu консоли расположен в hello URL-адреса; Поиск расположения toothis:</span><span class="sxs-lookup"><span data-stu-id="82718-339">For this procedure, hello Kudu console is located at hello following URL; browse toothis location:</span></span>
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. <span data-ttu-id="82718-340">Hello в верхнем меню, выберите **консоли отладки > CMD**.</span><span class="sxs-lookup"><span data-stu-id="82718-340">From hello top menu, select **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="82718-341">В командной строке консоли hello перейдите слишком`/site/wwwroot` (или нажмите кнопку `site`, затем `wwwroot` в представлении каталога hello вверху hello hello страницы):</span><span class="sxs-lookup"><span data-stu-id="82718-341">In hello console command line, navigate too`/site/wwwroot` (or click `site`, then `wwwroot` in hello directory view at hello top of hello page):</span></span>
   
    `cd /site/wwwroot`
4. <span data-ttu-id="82718-342">После того как вы укажете значение для **Версия Java**, сервер Tomcat должен создать каталог веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="82718-342">After you specify **Java version**, Tomcat server should create a webapps directory.</span></span> <span data-ttu-id="82718-343">В командной строке консоли hello перейдите toohello каталог веб-приложений:</span><span class="sxs-lookup"><span data-stu-id="82718-343">In hello console command line, navigate toohello webapps directory:</span></span>
   
    `mkdir webapps`
   
    `cd webapps`
5. <span data-ttu-id="82718-344">Перетащите JSPHello.war из `<project-path>/JSPHello/src/` и поместите его в представление каталога Kudu hello в папке `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="82718-344">Drag JSPHello.war from `<project-path>/JSPHello/src/` and drop it into hello Kudu directory view under `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="82718-345">Не перетаскивайте его toohello область «Перетащите. сюда tooupload "и" zip», так как Tomcat будет распакуйте его.</span><span class="sxs-lookup"><span data-stu-id="82718-345">Do not drag it toohello "Drag here tooupload and zip" area, because Tomcat will unzip it.</span></span>
   
   ![][8]

<span data-ttu-id="82718-346">В первом JSPHello.war отображается в области directory hello сама по себе:</span><span class="sxs-lookup"><span data-stu-id="82718-346">At first JSPHello.war appears in hello directory area by itself:</span></span>

  ![][9]

<span data-ttu-id="82718-347">За короткий промежуток времени (возможно не более 5 минут) сервера Tomcat будет Распакуйте hello WAR-файл в распакованную JSPHello каталог.</span><span class="sxs-lookup"><span data-stu-id="82718-347">In a short time (probably less than 5 minutes) Tomcat Server will unzip hello WAR file into an unpacked JSPHello directory.</span></span> <span data-ttu-id="82718-348">Щелкните hello КОРНЕВОЙ каталог toosee ли index.jsp была распаковываются и скопированных туда.</span><span class="sxs-lookup"><span data-stu-id="82718-348">Click hello ROOT directory toosee whether index.jsp has been unzipped and copied there.</span></span> <span data-ttu-id="82718-349">Если Да, перейдите toosee directory задней toohello веб-приложений ли hello распаковать JSPHello создать каталог.</span><span class="sxs-lookup"><span data-stu-id="82718-349">If so, navigate back toohello webapps directory toosee whether hello unpacked JSPHello directory has been created.</span></span> <span data-ttu-id="82718-350">Если эти элементы не отображаются, подождите, а затем повторите процедуру.</span><span class="sxs-lookup"><span data-stu-id="82718-350">If you do not see these items, wait and repeat.</span></span>

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a><span data-ttu-id="82718-351">Публикация приложения с помощью FileZilla (необязательно)</span><span class="sxs-lookup"><span data-stu-id="82718-351">Publish your application using FileZilla (optional)</span></span>
<span data-ttu-id="82718-352">Другое средство, вы можете использовать приложение hello toopublish — FileZilla популярных FTP-клиент сторонних удобны, графический пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="82718-352">Another tool you can use toopublish hello application is FileZilla, a popular third-party FTP client with a convenient, graphical UI.</span></span> <span data-ttu-id="82718-353">Скачать и установить FileZilla можно на веб-сайте [http://filezilla-project.org/](http://filezilla-project.org/).</span><span class="sxs-lookup"><span data-stu-id="82718-353">You can download and install FileZilla from [http://filezilla-project.org/](http://filezilla-project.org/) if you do not already have it.</span></span> <span data-ttu-id="82718-354">Дополнительные сведения об использовании клиента hello см. в разделе hello [документации FileZilla](https://wiki.filezilla-project.org/Documentation) и на запись в блоге [клиентов FTP - часть 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span><span class="sxs-lookup"><span data-stu-id="82718-354">For more information on using hello client, see hello [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) and this blog entry on [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span></span>

1. <span data-ttu-id="82718-355">В FileZilla щелкните **File > Site Manager** (Файл > Диспетчер сайтов).</span><span class="sxs-lookup"><span data-stu-id="82718-355">In FileZilla, click **File > Site Manager**.</span></span>
2. <span data-ttu-id="82718-356">В hello **диспетчер сайта** диалоговое окно, нажмите кнопку **новый сайт**.</span><span class="sxs-lookup"><span data-stu-id="82718-356">In hello **Site Manager** dialog, click **New Site**.</span></span> <span data-ttu-id="82718-357">Новый пустой FTP-узел будет отображаться в **выберите запись** приглашением tooprovide имя.</span><span class="sxs-lookup"><span data-stu-id="82718-357">A new blank FTP site will appear in **Select Entry** prompting you tooprovide a name.</span></span> <span data-ttu-id="82718-358">Укажите имя `AzureWebDemo-FTP`для использования в этой процедуре.</span><span class="sxs-lookup"><span data-stu-id="82718-358">For this procedure, name it `AzureWebDemo-FTP`.</span></span>
   
    <span data-ttu-id="82718-359">На hello **Общие** укажите hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="82718-359">On hello **General** tab, specify hello following settings:</span></span>
   
   * <span data-ttu-id="82718-360">**Узел:** ввод hello **имя узла FTP** , скопированный из панели мониторинга hello.</span><span class="sxs-lookup"><span data-stu-id="82718-360">**Host:** Enter hello **FTP Host Name** that you copied from hello dashboard.</span></span>
   * <span data-ttu-id="82718-361">**Порт:** (оставьте это поле оставить пустым, как это передачи пассивный и hello server определит порт toouse hello.)</span><span class="sxs-lookup"><span data-stu-id="82718-361">**Port:** (Leave this blank, as this is a passive transfer and hello server will determine hello port toouse.)</span></span>
   * <span data-ttu-id="82718-362">**Протокол:** протокол передачи файлов FTP.</span><span class="sxs-lookup"><span data-stu-id="82718-362">**Protocol:** FTP File Transfer Protocol</span></span>
   * <span data-ttu-id="82718-363">**Шифрование:** используйте простой FTP.</span><span class="sxs-lookup"><span data-stu-id="82718-363">**Encryption:** Use plain FTP</span></span>
   * <span data-ttu-id="82718-364">**Тип входа:** обычный.</span><span class="sxs-lookup"><span data-stu-id="82718-364">**Logon Type:** Normal</span></span>
   * <span data-ttu-id="82718-365">**Пользователь:** ввод hello развертывания или FTP, скопированный из панели мониторинга hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="82718-365">**User:** Enter hello Deployment / FTP user that you copied from hello dashboard.</span></span> <span data-ttu-id="82718-366">Это hello полное FTP имя пользователя, который имеет форму hello *webappname\username*.</span><span class="sxs-lookup"><span data-stu-id="82718-366">This is hello full FTP username, which has hello form *webappname\username*.</span></span>
   * <span data-ttu-id="82718-367">**Пароль:** введите пароль hello, указанное при задании учетных данных развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="82718-367">**Password:** Enter hello password that you specified when you set hello deployment credentials.</span></span>
     
     <span data-ttu-id="82718-368">На hello **параметры передачи** выберите **пассивный**.</span><span class="sxs-lookup"><span data-stu-id="82718-368">On hello **Transfer Settings** tab, select **Passive**.</span></span>
3. <span data-ttu-id="82718-369">Щелкните **Подключить**.</span><span class="sxs-lookup"><span data-stu-id="82718-369">Click **Connect**.</span></span> <span data-ttu-id="82718-370">Если успешно, FileZilla элемента будет отображаться консоли `Status: Connected` сообщений и проблемы `LIST` команда содержимое каталога toolist hello.</span><span class="sxs-lookup"><span data-stu-id="82718-370">If successful, FileZilla's console will display a `Status: Connected` message and issue a `LIST` command toolist hello directory contents.</span></span>
4. <span data-ttu-id="82718-371">В hello **локального** находится панель сайта выберите hello исходного каталога, в какой файл JSPHello.war hello; hello путь будет выглядеть аналогично toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="82718-371">In hello **Local** site panel, select hello source directory in which hello JSPHello.war file resides; hello path will be similar toohello following:</span></span>
   
    `<project-path>/JSPHello/src/`
5. <span data-ttu-id="82718-372">В hello **удаленного** узла панели, выберите hello конечную папку.</span><span class="sxs-lookup"><span data-stu-id="82718-372">In hello **Remote** site panel, select hello destination folder.</span></span> <span data-ttu-id="82718-373">Будет развернут файл toohello hello WAR `webapps` каталог в корневом каталоге веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="82718-373">You will deploy hello WAR file toohello `webapps` directory under hello web app's root.</span></span> <span data-ttu-id="82718-374">Перейдите в слишком`/site/wwwroot`, щелкните правой кнопкой мыши `wwwroot`и выберите **создать каталог**.</span><span class="sxs-lookup"><span data-stu-id="82718-374">Navigate too`/site/wwwroot`, right-click on `wwwroot`, and select **Create directory**.</span></span> <span data-ttu-id="82718-375">Имя каталога hello `webapps` и введите этот каталог.</span><span class="sxs-lookup"><span data-stu-id="82718-375">Name hello directory `webapps` and enter that directory.</span></span>
6. <span data-ttu-id="82718-376">Передача JSPHello.war слишком`/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="82718-376">Transfer JSPHello.war too`/site/wwwroot/webapps`.</span></span> <span data-ttu-id="82718-377">Выберите JSPHello.war в hello **локального** список файлов, щелкните его правой кнопкой мыши и выберите **отправить**.</span><span class="sxs-lookup"><span data-stu-id="82718-377">Select JSPHello.war in hello **Local** file list, right-click on it and select **Upload**.</span></span> <span data-ttu-id="82718-378">Вы должны увидеть его в `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="82718-378">You should see it appear in `/site/wwwroot/webapps`.</span></span>
7. <span data-ttu-id="82718-379">После копирования каталога веб-приложений toohello JSPHello.war сервера Tomcat будет автоматически распаковать (Распакуйте) hello файлы в hello WAR-файла.</span><span class="sxs-lookup"><span data-stu-id="82718-379">After you copy JSPHello.war toohello webapps directory, Tomcat Server will automatically unpack (unzip) hello files in hello WAR file.</span></span> <span data-ttu-id="82718-380">Хотя сервера Tomcat начинается немедленно при распаковке, может занять длительное время (возможно, часы) для tooappear файлы hello в клиенте hello FTP.</span><span class="sxs-lookup"><span data-stu-id="82718-380">Although Tomcat Server begins unpacking almost immediately, it might take a long time (possibly hours) for hello files tooappear in hello FTP client.</span></span>

#### <a name="run-hello-hello-world-application-on-hello-web-app"></a><span data-ttu-id="82718-381">Запустите приложение Hello World hello на hello веб-приложения</span><span class="sxs-lookup"><span data-stu-id="82718-381">Run hello Hello World application on hello Web App</span></span>
1. <span data-ttu-id="82718-382">После отправки hello WAR-файл и проверить, что создал распакованы сервера Tomcat `JSPHello` каталога, Обзор слишком`http://webdemowebapp.azurewebsites.net/JSPHello` toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="82718-382">After you have uploaded hello WAR file and verified that Tomcat server has created an unpacked `JSPHello` directory, browse too`http://webdemowebapp.azurewebsites.net/JSPHello` toorun hello application.</span></span>
   
   > <span data-ttu-id="82718-383">**Примечание:** при нажатии кнопки **Обзор** из классического портала hello, может появиться веб-страница по умолчанию hello, о том, «этого веб-приложения на основе Java успешно создан.»</span><span class="sxs-lookup"><span data-stu-id="82718-383">**Note:** If you click **Browse** from hello classic portal, you might get hello default webpage, saying "This Java based web application has been successfully created."</span></span> <span data-ttu-id="82718-384">Может потребоваться toorefresh hello веб-страницы в порядок вывода приложения hello tooview вместо веб-страницы по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="82718-384">You might have toorefresh hello webpage in order tooview hello application output instead of hello default webpage.</span></span>
   > 
   > 
2. <span data-ttu-id="82718-385">При запуске приложения hello, вы увидите веб-страницу с hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="82718-385">When hello application runs, you should see a web page with hello following output:</span></span>
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a><span data-ttu-id="82718-386">Очистка ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="82718-386">Clean up Azure resources</span></span>
<span data-ttu-id="82718-387">Эта процедура создает веб-приложение службы приложений.</span><span class="sxs-lookup"><span data-stu-id="82718-387">This procedure creates an App Service web app.</span></span> <span data-ttu-id="82718-388">Вам будет выставлен счет для hello ресурса при условии, что он существует.</span><span class="sxs-lookup"><span data-stu-id="82718-388">You will be billed for hello resource as long as it exists.</span></span> <span data-ttu-id="82718-389">Если планируется использование hello веб-приложения для тестирования или разработки toocontinue, рассмотрите возможность остановки или удаления.</span><span class="sxs-lookup"><span data-stu-id="82718-389">Unless you plan toocontinue using hello web app for testing or development, you should consider stopping or deleting it.</span></span> <span data-ttu-id="82718-390">За остановленное веб-приложение все равно взимается небольшая плата, зато его можно перезапустить в любое время.</span><span class="sxs-lookup"><span data-stu-id="82718-390">A web app that has been stopped will still incur a small charge, but you can restart it at any time.</span></span> <span data-ttu-id="82718-391">Удаление веб-приложения будут удалены все данные, отправленные tooit.</span><span class="sxs-lookup"><span data-stu-id="82718-391">Deleting a web app erases all data you have uploaded tooit.</span></span>

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
