---
title: "aaaUse hello Java SDK toodevelop приложения в хранилище Озера данных Azure | Документы Microsoft"
description: "Использовать хранилище Озера данных Azure, Java SDK toocreate учетной записи хранилища Озера данных и выполнения основных операций в hello хранилища Озера данных"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d10e09db-5232-4e84-bb50-52efc2c21887
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/28/2017
ms.author: nitinme
ms.openlocfilehash: d3bcee449c2a2a4bd2f7b241af46ecc010b6b62e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-java"></a><span data-ttu-id="be8a8-103">Начало работы с хранилищем озера данных Azure с помощью Java</span><span class="sxs-lookup"><span data-stu-id="be8a8-103">Get started with Azure Data Lake Store using Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="be8a8-104">Портал</span><span class="sxs-lookup"><span data-stu-id="be8a8-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="be8a8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="be8a8-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="be8a8-106">Пакет SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="be8a8-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="be8a8-107">Пакет SDK для Java</span><span class="sxs-lookup"><span data-stu-id="be8a8-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="be8a8-108">REST API</span><span class="sxs-lookup"><span data-stu-id="be8a8-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="be8a8-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="be8a8-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="be8a8-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="be8a8-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="be8a8-111">Python</span><span class="sxs-lookup"><span data-stu-id="be8a8-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="be8a8-112">Узнайте, как основных операций SDK для Java хранилища Озера данных Azure hello tooperform toouse такие как создание папками, отправка и загрузка файлов данных и т. д. Дополнительные сведения об Azure Data Lake Store см. в [этой статье](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="be8a8-112">Learn how toouse hello Azure Data Lake Store Java SDK tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="be8a8-113">Можно открыть документы hello API пакета SDK для Java для хранилища Озера данных Azure в [API Java хранилища Озера данных Azure docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span><span class="sxs-lookup"><span data-stu-id="be8a8-113">You can access hello Java SDK API docs for Azure Data Lake Store at [Azure Data Lake Store Java API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be8a8-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="be8a8-114">Prerequisites</span></span>
* <span data-ttu-id="be8a8-115">Комплект разработчика Java (JDK 7 или более поздней версии с использованием Java версии 1.7 или более поздней).</span><span class="sxs-lookup"><span data-stu-id="be8a8-115">Java Development Kit (JDK 7 or higher, using Java version 1.7 or higher)</span></span>
* <span data-ttu-id="be8a8-116">Учетная запись Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="be8a8-116">Azure Data Lake Store account.</span></span> <span data-ttu-id="be8a8-117">Следуйте инструкциям hello в [Приступая к работе с хранилища Озера данных Azure, с помощью портала Azure hello](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="be8a8-117">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span>
* <span data-ttu-id="be8a8-118">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="be8a8-118">[Maven](https://maven.apache.org/install.html).</span></span> <span data-ttu-id="be8a8-119">В этом руководстве это средство используется для создания зависимостей проекта.</span><span class="sxs-lookup"><span data-stu-id="be8a8-119">This tutorial uses Maven for build and project dependencies.</span></span> <span data-ttu-id="be8a8-120">Несмотря на возможные toobuild без использования системы построения как Maven или Gradle, убедитесь, этих систем является гораздо проще toomanage зависимости.</span><span class="sxs-lookup"><span data-stu-id="be8a8-120">Although it is possible toobuild without using a build system like Maven or Gradle, these systems make is much easier toomanage dependencies.</span></span>
* <span data-ttu-id="be8a8-121">Интегрированная среда разработки, например [IntelliJ IDEA](https://www.jetbrains.com/idea/download/), [Eclipse](https://www.eclipse.org/downloads/) или аналогичная (необязательно).</span><span class="sxs-lookup"><span data-stu-id="be8a8-121">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="be8a8-122">Как выполнить аутентификацию с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="be8a8-122">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="be8a8-123">В этом учебнике мы используем tooretrieve клиента секрет маркера Azure Active Directory (проверка подлинности service to service) приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be8a8-123">In this tutorial we use a Azure AD application client secret tooretrieve an Azure Active Directory token (service-to-service authentication).</span></span> <span data-ttu-id="be8a8-124">Мы используем этот токен toocreate файл хранилища Озера данных tooperform объекта клиента операций и операций с каталогами.</span><span class="sxs-lookup"><span data-stu-id="be8a8-124">We use this token toocreate an Data Lake Store client object tooperform operations file and directory operations.</span></span> <span data-ttu-id="be8a8-125">Инструкции по как tooauthenticate с помощью хранилища Озера данных Azure hello секрет клиента мы выполните следующие общие действия hello.</span><span class="sxs-lookup"><span data-stu-id="be8a8-125">For instructions on how tooauthenticate with Azure Data Lake Store using hello client secret, we perform hello following high-level steps:</span></span>

1. <span data-ttu-id="be8a8-126">Создать веб-приложение Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be8a8-126">Create an Azure AD web application</span></span>
2. <span data-ttu-id="be8a8-127">Получить идентификатор клиента hello, секрет клиента и конечная точка маркера для hello веб-приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="be8a8-127">Retrieve hello client ID, client secret, and token endpoint for hello Azure AD web application.</span></span>
3. <span data-ttu-id="be8a8-128">Настройка доступа для веб-приложения hello Azure AD в хранилище Озера данных файла или папки, будет tooaccess из приложения Java, который вы создаете hello hello.</span><span class="sxs-lookup"><span data-stu-id="be8a8-128">Configure access for hello Azure AD web application on hello Data Lake Store file/folder that you want tooaccess from hello Java application you are creating.</span></span>

<span data-ttu-id="be8a8-129">Инструкции по tooperform следующие действия. в статье [создать приложение Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="be8a8-129">For instructions on how tooperform these steps, see [Create an Active Directory application](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="be8a8-130">Azure Active Directory предоставляет другие параметры также tooretrieve маркер.</span><span class="sxs-lookup"><span data-stu-id="be8a8-130">Azure Active Directory provides other options as well tooretrieve a token.</span></span> <span data-ttu-id="be8a8-131">Можно выбрать из ряд toosuit механизмов проверки подлинности, отличный сценария, например, приложение, работающее в браузере, распространяемых в виде классического приложения приложение или серверное приложение выполняется локально или в Azure виртуальные компьютер.</span><span class="sxs-lookup"><span data-stu-id="be8a8-131">You can pick from a number of different authentication mechanisms toosuit your scenario, for example, an application running in a browser, an application distributed as a desktop application, or a server application running on-premises or in an Azure virtual machine.</span></span> <span data-ttu-id="be8a8-132">Доступны также различные типы учетных данных, например пароли, сертификаты, метод двухфакторной проверки подлинности и т. д. Кроме того, Azure Active Directory позволяет toosynchronize локальных пользователей Active Directory с облаком hello.</span><span class="sxs-lookup"><span data-stu-id="be8a8-132">You can also pick from different types of credentials like passwords, certificates, 2-factor authentication, etc. In addition, Azure Active Directory allows you toosynchronize your on-premises Active Directory users with hello cloud.</span></span> <span data-ttu-id="be8a8-133">Дополнительные сведения см. в статье [Сценарии аутентификации в Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="be8a8-133">For details, see [Authentication Scenarios for Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span></span> 

## <a name="create-a-java-application"></a><span data-ttu-id="be8a8-134">Создание приложения Java</span><span class="sxs-lookup"><span data-stu-id="be8a8-134">Create a Java application</span></span>
<span data-ttu-id="be8a8-135">Образец кода Hello доступных [на GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) пошагово рассматривается процесс hello Создание файлов в хранилище hello, объединения файлов, загрузку файла, и удалить некоторые файлы в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="be8a8-135">hello code sample available [on GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) walks you through hello process of creating files in hello store, concatenating files, downloading a file, and deleting some files in hello store.</span></span> <span data-ttu-id="be8a8-136">В этом разделе статьи hello пошаговыми руководствами по hello основной части кода hello.</span><span class="sxs-lookup"><span data-stu-id="be8a8-136">This section of hello article walk you through hello main parts of hello code.</span></span>

1. <span data-ttu-id="be8a8-137">Создайте проект Maven с помощью [архетипа mvn](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) hello из командной строки или с помощью интегрированной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="be8a8-137">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from hello command-line or using an IDE.</span></span> <span data-ttu-id="be8a8-138">Инструкции как проект с помощью IntelliJ toocreate Java см. в разделе [здесь](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span><span class="sxs-lookup"><span data-stu-id="be8a8-138">For instructions on how toocreate a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span></span> <span data-ttu-id="be8a8-139">Дополнительные сведения о разделе toocreate проект с помощью Eclipse, [здесь](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span><span class="sxs-lookup"><span data-stu-id="be8a8-139">For instructions on how toocreate a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span></span> 
2. <span data-ttu-id="be8a8-140">Добавьте следующие зависимости tooyour Maven hello **pom.xml** файла.</span><span class="sxs-lookup"><span data-stu-id="be8a8-140">Add hello following dependencies tooyour Maven **pom.xml** file.</span></span> <span data-ttu-id="be8a8-141">Добавьте следующий фрагмент текста между hello hello  **\</Version >** тег и hello  **\</project >** тег:</span><span class="sxs-lookup"><span data-stu-id="be8a8-141">Add hello following snippet of text between hello **\</version>** tag and hello **\</project>** tag:</span></span>
   
        <dependencies>
          <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-data-lake-store-sdk</artifactId>
            <version>2.1.5</version>
          </dependency>
          <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-nop</artifactId>
            <version>1.7.21</version>
          </dependency>
        </dependencies>
   
    <span data-ttu-id="be8a8-142">Первая зависимость Hello — toouse hello SDK хранилища Озера данных (`azure-data-lake-store-sdk`) из репозитория maven hello.</span><span class="sxs-lookup"><span data-stu-id="be8a8-142">hello first dependency is toouse hello Data Lake Store SDK (`azure-data-lake-store-sdk`) from hello maven repository.</span></span> <span data-ttu-id="be8a8-143">Здравствуйте, вторая зависимость (`slf4j-nop`) является toospecify toouse framework какие ведения журнала для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="be8a8-143">hello second dependency (`slf4j-nop`) is toospecify which logging framework toouse for this application.</span></span> <span data-ttu-id="be8a8-144">Hello SDK хранилища Озера данных использует [slf4j](http://www.slf4j.org/) фасадной ведения журнала, которая позволяет выбирать из нескольких популярных ведения журнала платформы, такие как log4j, ведение журнала, logback, т. д., Java или без регистрации.</span><span class="sxs-lookup"><span data-stu-id="be8a8-144">hello Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span></span> <span data-ttu-id="be8a8-145">В этом примере мы будет отключить ведение журнала, поэтому мы используем hello **slf4j nop** привязки.</span><span class="sxs-lookup"><span data-stu-id="be8a8-145">For this example, we will disable logging, hence we use hello **slf4j-nop** binding.</span></span> <span data-ttu-id="be8a8-146">toouse см. другие параметры ведения журнала в вашем приложении [здесь](http://www.slf4j.org/manual.html#projectDep).</span><span class="sxs-lookup"><span data-stu-id="be8a8-146">toouse other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span></span>

### <a name="add-hello-application-code"></a><span data-ttu-id="be8a8-147">Добавьте код приложения hello</span><span class="sxs-lookup"><span data-stu-id="be8a8-147">Add hello application code</span></span>
<span data-ttu-id="be8a8-148">Существует три основные части toohello кода.</span><span class="sxs-lookup"><span data-stu-id="be8a8-148">There are three main parts toohello code.</span></span>

1. <span data-ttu-id="be8a8-149">Получить маркер hello Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="be8a8-149">Obtain hello Azure Active Directory token</span></span>
2. <span data-ttu-id="be8a8-150">С помощью маркера toocreate hello клиента хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="be8a8-150">Use hello token toocreate a Data Lake Store client.</span></span>
3. <span data-ttu-id="be8a8-151">Использование клиента tooperform hello хранилища Озера данных операций.</span><span class="sxs-lookup"><span data-stu-id="be8a8-151">Use hello Data Lake Store client tooperform operations.</span></span>

#### <a name="step-1-obtain-an-azure-active-directory-token"></a><span data-ttu-id="be8a8-152">Шаг 1. Получение маркера Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="be8a8-152">Step 1: Obtain an Azure Active Directory token.</span></span>
<span data-ttu-id="be8a8-153">Hello SDK хранилища Озера данных предоставляет удобные методы, позволяющие управлять hello маркеров безопасности требуется tootalk toohello хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="be8a8-153">hello Data Lake Store SDK provides convenient methods that let you manage hello security tokens needed tootalk toohello Data Lake Store account.</span></span> <span data-ttu-id="be8a8-154">Однако hello SDK не требует использования только эти методы.</span><span class="sxs-lookup"><span data-stu-id="be8a8-154">However, hello SDK does not mandate that only these methods be used.</span></span> <span data-ttu-id="be8a8-155">Можно использовать другие средства получения токена, например использование hello [пакет SDK Azure Active Directory](https://github.com/AzureAD/azure-activedirectory-library-for-java), или пользовательский код.</span><span class="sxs-lookup"><span data-stu-id="be8a8-155">You can use any other means of obtaining token as well, like using hello [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span></span>

<span data-ttu-id="be8a8-156">hello toouse токен tooobtain SDK хранилища Озера данных для приложения hello Active Directory Web, созданного ранее, используйте один из подклассов hello `AccessTokenProvider` (hello приведенном ниже примере используется `ClientCredsTokenProvider`).</span><span class="sxs-lookup"><span data-stu-id="be8a8-156">toouse hello Data Lake Store SDK tooobtain token for hello Active Directory Web application you created earlier, use one of hello subclasses of `AccessTokenProvider` (hello example below uses `ClientCredsTokenProvider`).</span></span> <span data-ttu-id="be8a8-157">Поставщик маркеров кэши Hello hello-учетные данные используется токен tooobtain hello в памяти и автоматически обновляет токен hello, если он стал примерно tooexpire.</span><span class="sxs-lookup"><span data-stu-id="be8a8-157">hello token provider caches hello creds used tooobtain hello token in memory, and automatically renews hello token if it is about tooexpire.</span></span> <span data-ttu-id="be8a8-158">Это возможно toocreate собственные подклассы `AccessTokenProvider` токены извлекаются в коде клиента, но сейчас Давайте просто hello использования одного, предоставляемых в hello SDK.</span><span class="sxs-lookup"><span data-stu-id="be8a8-158">It is possible toocreate your own subclasses of `AccessTokenProvider` so tokens are obtained by your customer code, but for now let's just use hello one provided in hello SDK.</span></span>

<span data-ttu-id="be8a8-159">Замените **ЗАПОЛНЕНИЯ здесь** hello фактическими значениями для hello Azure Active Directory, веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="be8a8-159">Replace **FILL-IN-HERE** with hello actual values for hello Azure Active Directory Web application.</span></span>

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a><span data-ttu-id="be8a8-160">Шаг 2. Создание клиентского объекта Azure Data Lake Store (ADLStoreClient)</span><span class="sxs-lookup"><span data-stu-id="be8a8-160">Step 2: Create an Azure Data Lake Store client (ADLStoreClient) object</span></span>
<span data-ttu-id="be8a8-161">Создание [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) объект требует toospecify hello хранилища Озера данных учетной записи имя и hello поставщик маркеров был создан в последнем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="be8a8-161">Creating an [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) object requires you toospecify hello Data Lake Store account name and hello token provider you generated in hello last step.</span></span> <span data-ttu-id="be8a8-162">Обратите внимание, что hello хранилища Озера данных учетной записи, имя должно toobe полное доменное имя.</span><span class="sxs-lookup"><span data-stu-id="be8a8-162">Note that hello Data Lake Store account name needs toobe a fully qualified domain name.</span></span> <span data-ttu-id="be8a8-163">Например, замените часть **FILL-IN-HERE** примерно таким значением: **mydatalakestore.azuredatalakestore.net**.</span><span class="sxs-lookup"><span data-stu-id="be8a8-163">For example, replace **FILL-IN-HERE** with something like **mydatalakestore.azuredatalakestore.net**.</span></span>

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just hello account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-hello-adlstoreclient-tooperform-file-and-directory-operations"></a><span data-ttu-id="be8a8-164">Шаг 3: Используйте hello ADLStoreClient tooperform файлов и каталогов операции</span><span class="sxs-lookup"><span data-stu-id="be8a8-164">Step 3: Use hello ADLStoreClient tooperform file and directory operations</span></span>
<span data-ttu-id="be8a8-165">Приведенный ниже код Hello содержит фрагменты примеров некоторых распространенных операций.</span><span class="sxs-lookup"><span data-stu-id="be8a8-165">hello code below contains example snippets of some common operations.</span></span> <span data-ttu-id="be8a8-166">Вы можете просмотреть полный hello [docs API пакета SDK для Java хранилища Озера данных](https://azure.github.io/azure-data-lake-store-java/javadoc/) из hello **ADLStoreClient** объекта toosee других операций.</span><span class="sxs-lookup"><span data-stu-id="be8a8-166">You can look at hello full [Data Lake Store Java SDK API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/) of hello **ADLStoreClient** object toosee other operations.</span></span>

<span data-ttu-id="be8a8-167">Обратите внимание, что чтение файлов и запись в них осуществляется с помощью стандартных потоков Java.</span><span class="sxs-lookup"><span data-stu-id="be8a8-167">Note that files are read from and written into using standard Java streams.</span></span> <span data-ttu-id="be8a8-168">Это означает, что слоя любого из потоков Java по hello поверх hello хранилища Озера данных потоки toobenefit из стандартных функциональных возможностей Java (например, печать потоков для Форматированные выходные данные или any hello сжатия или шифрования потоков для дополнительных возможностей сверху, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="be8a8-168">This means that you can layer any of hello Java streams on top of hello Data Lake Store streams toobenefit from standard Java functionality (e.g., Print streams for formatted output, or any of hello compression or encryption streams for additional functionality on top, etc.).</span></span>

     // create file and write some content
     String filename = "/a/b/c.txt";
     OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
     PrintStream out = new PrintStream(stream);
     for (int i = 1; i <= 10; i++) {
         out.println("This is line #" + i);
         out.format("This is hello same line (%d), but using formatted output. %n", i);
     }
     out.close();
    
    // set file permission
    client.setPermission(filename, "744");

    // append toofile
    stream = client.getAppendStream(filename);
    stream.write(getSampleContent());
    stream.close();

    // Read File
    InputStream in = client.getReadStream(filename);
    byte[] b = new byte[64000];
    while (in.read(b) != -1) {
        System.out.write(b);
    }
    in.close();

    // concatenate hello two files into one
    List<String> fileList = Arrays.asList("/a/b/c.txt", "/a/b/d.txt");
    client.concatenateFiles("/a/b/f.txt", fileList);

    //rename hello file
    client.rename("/a/b/f.txt", "/a/b/g.txt");

    // list directory contents
    List<DirectoryEntry> list = client.enumerateDirectory("/a/b", 2000);
    System.out.println("Directory listing for directory /a/b:");
    for (DirectoryEntry entry : list) {
        printDirectoryInfo(entry);
    }

    // delete directory along with all hello subdirectories and files in it
    client.deleteRecursive("/a");

#### <a name="step-4-build-and-run-hello-application"></a><span data-ttu-id="be8a8-169">Шаг 4: Построение и запуск приложения hello</span><span class="sxs-lookup"><span data-stu-id="be8a8-169">Step 4: Build and run hello application</span></span>
1. <span data-ttu-id="be8a8-170">toorun из в IDE, найдите и нажмите клавишу hello **запуска** кнопки.</span><span class="sxs-lookup"><span data-stu-id="be8a8-170">toorun from within an IDE, locate and press hello **Run** button.</span></span> <span data-ttu-id="be8a8-171">toorun из Maven, используйте [exec: exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span><span class="sxs-lookup"><span data-stu-id="be8a8-171">toorun from Maven, use [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span></span>
2. <span data-ttu-id="be8a8-172">автономный JAR-файл, который можно запустить из jar hello построения из командной строки с включен, все зависимости с помощью hello tooproduce [подключаемого модуля сборки Maven](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span><span class="sxs-lookup"><span data-stu-id="be8a8-172">tooproduce a standalone jar that you can run from command-line build hello jar with all dependencies included, using hello [Maven assembly plugin](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span></span> <span data-ttu-id="be8a8-173">Здравствуйте, pom.xml в hello [примере исходный код на github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) приводится пример того, как toodo это.</span><span class="sxs-lookup"><span data-stu-id="be8a8-173">hello pom.xml in hello [example source code on github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) has an example of how toodo this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be8a8-174">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="be8a8-174">Next steps</span></span>
* [<span data-ttu-id="be8a8-175">Просмотр JavaDoc для пакета Java SDK hello</span><span class="sxs-lookup"><span data-stu-id="be8a8-175">Explore JavaDoc for hello Java SDK</span></span>](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [<span data-ttu-id="be8a8-176">Защита данных в хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="be8a8-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="be8a8-177">Использование аналитики озера данных Azure с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="be8a8-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="be8a8-178">Использование Azure HDInsight с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="be8a8-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

