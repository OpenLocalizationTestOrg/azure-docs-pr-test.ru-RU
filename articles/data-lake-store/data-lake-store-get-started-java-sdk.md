---
title: "Разработка приложений с помощью пакета Java SDK для Azure Data Lake Store | Документация Майкрософт"
description: "Создание учетной записи Azure Data Lake Store и выполнение базовых операций в Data Lake Store с помощью пакета Java SDK для Azure Data Lake Store"
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
ms.openlocfilehash: 91128b53a2f1cd3ddcbee5b07da0d67668944fb4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-java"></a><span data-ttu-id="c6ed4-103">Начало работы с хранилищем озера данных Azure с помощью Java</span><span class="sxs-lookup"><span data-stu-id="c6ed4-103">Get started with Azure Data Lake Store using Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c6ed4-104">Портал</span><span class="sxs-lookup"><span data-stu-id="c6ed4-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="c6ed4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6ed4-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="c6ed4-106">Пакет SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="c6ed4-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="c6ed4-107">Пакет SDK для Java</span><span class="sxs-lookup"><span data-stu-id="c6ed4-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="c6ed4-108">REST API</span><span class="sxs-lookup"><span data-stu-id="c6ed4-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="c6ed4-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c6ed4-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="c6ed4-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="c6ed4-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="c6ed4-111">Python</span><span class="sxs-lookup"><span data-stu-id="c6ed4-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="c6ed4-112">Узнайте, как с помощью пакета Java SDK для Azure Data Lake Store выполнять базовые операции, такие как создание папок, отправка и скачивание файлов данных и т. д. Дополнительные сведения об Azure Data Lake Store см. в [этой статье](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6ed4-112">Learn how to use the Azure Data Lake Store Java SDK to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="c6ed4-113">Документацию по API пакета Java SDK для Azure Data Lake Store можно найти [здесь](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span><span class="sxs-lookup"><span data-stu-id="c6ed4-113">You can access the Java SDK API docs for Azure Data Lake Store at [Azure Data Lake Store Java API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6ed4-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c6ed4-114">Prerequisites</span></span>
* <span data-ttu-id="c6ed4-115">Комплект разработчика Java (JDK 7 или более поздней версии с использованием Java версии 1.7 или более поздней).</span><span class="sxs-lookup"><span data-stu-id="c6ed4-115">Java Development Kit (JDK 7 or higher, using Java version 1.7 or higher)</span></span>
* <span data-ttu-id="c6ed4-116">Учетная запись Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-116">Azure Data Lake Store account.</span></span> <span data-ttu-id="c6ed4-117">Следуйте инструкциям в разделе [Приступая к работе с хранилищем озера данных Azure на портале Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c6ed4-117">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span>
* <span data-ttu-id="c6ed4-118">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="c6ed4-118">[Maven](https://maven.apache.org/install.html).</span></span> <span data-ttu-id="c6ed4-119">В этом руководстве это средство используется для создания зависимостей проекта.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-119">This tutorial uses Maven for build and project dependencies.</span></span> <span data-ttu-id="c6ed4-120">Хотя зависимости можно создать и без использования таких систем, как Maven или Gradle, они существенно упрощают управление ими.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-120">Although it is possible to build without using a build system like Maven or Gradle, these systems make is much easier to manage dependencies.</span></span>
* <span data-ttu-id="c6ed4-121">Интегрированная среда разработки, например [IntelliJ IDEA](https://www.jetbrains.com/idea/download/), [Eclipse](https://www.eclipse.org/downloads/) или аналогичная (необязательно).</span><span class="sxs-lookup"><span data-stu-id="c6ed4-121">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="c6ed4-122">Как выполнить аутентификацию с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c6ed4-122">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="c6ed4-123">В этом руководстве мы используем секрет клиента приложения Azure AD, чтобы получить маркер Azure Active Directory (для проверки подлинности с взаимодействием между службами).</span><span class="sxs-lookup"><span data-stu-id="c6ed4-123">In this tutorial we use a Azure AD application client secret to retrieve an Azure Active Directory token (service-to-service authentication).</span></span> <span data-ttu-id="c6ed4-124">Он используется для создания клиентского объекта Data Lake Store, позволяющего выполнять операции с файлами и каталогами.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-124">We use this token to create an Data Lake Store client object to perform operations file and directory operations.</span></span> <span data-ttu-id="c6ed4-125">Для проверки подлинности в Azure Data Lake Store с помощью секрета клиента требуется выполнить следующие основные этапы.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-125">For instructions on how to authenticate with Azure Data Lake Store using the client secret, we perform the following high-level steps:</span></span>

1. <span data-ttu-id="c6ed4-126">Создать веб-приложение Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-126">Create an Azure AD web application</span></span>
2. <span data-ttu-id="c6ed4-127">Получить идентификатор клиента, секрет клиента и конечную точку маркера для веб-приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-127">Retrieve the client ID, client secret, and token endpoint for the Azure AD web application.</span></span>
3. <span data-ttu-id="c6ed4-128">Настроить для веб-приложения Azure AD доступ к файлу или папке Data Lake Store, к которым вы хотите получать доступ из создаваемого приложения Java.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-128">Configure access for the Azure AD web application on the Data Lake Store file/folder that you want to access from the Java application you are creating.</span></span>

<span data-ttu-id="c6ed4-129">Инструкции по выполнению этих шагов см. в разделе о [создании приложения Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="c6ed4-129">For instructions on how to perform these steps, see [Create an Active Directory application](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="c6ed4-130">Помимо получения маркера Azure Active Directory предоставляет и другие возможности.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-130">Azure Active Directory provides other options as well to retrieve a token.</span></span> <span data-ttu-id="c6ed4-131">Вы можете выбрать один из нескольких методов проверки подлинности в соответствии с вашим сценарием, например для приложения, выполняемого в браузере, приложения, распространяемого в виде классического приложения, или серверного приложения, выполняемого в локальной среде или в виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-131">You can pick from a number of different authentication mechanisms to suit your scenario, for example, an application running in a browser, an application distributed as a desktop application, or a server application running on-premises or in an Azure virtual machine.</span></span> <span data-ttu-id="c6ed4-132">Доступны также различные типы учетных данных, например пароли, сертификаты, метод двухфакторной проверки подлинности и т. д. Кроме того, Azure Active Directory позволяет синхронизировать локальных пользователей Active Directory с облаком.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-132">You can also pick from different types of credentials like passwords, certificates, 2-factor authentication, etc. In addition, Azure Active Directory allows you to synchronize your on-premises Active Directory users with the cloud.</span></span> <span data-ttu-id="c6ed4-133">Дополнительные сведения см. в статье [Сценарии аутентификации в Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="c6ed4-133">For details, see [Authentication Scenarios for Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span></span> 

## <a name="create-a-java-application"></a><span data-ttu-id="c6ed4-134">Создание приложения Java</span><span class="sxs-lookup"><span data-stu-id="c6ed4-134">Create a Java application</span></span>
<span data-ttu-id="c6ed4-135">На [сайте GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) доступен пример кода, который используется для создания файлов в хранилище, объединения и скачивания файлов, а также для удаления файлов из хранилища.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-135">The code sample available [on GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) walks you through the process of creating files in the store, concatenating files, downloading a file, and deleting some files in the store.</span></span> <span data-ttu-id="c6ed4-136">В этом разделе статьи рассматриваются основные части этого кода.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-136">This section of the article walk you through the main parts of the code.</span></span>

1. <span data-ttu-id="c6ed4-137">Создайте проект Maven с использованием [архетипа mvn](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) с помощью командной строки или интегрированной среды разработки (IDE).</span><span class="sxs-lookup"><span data-stu-id="c6ed4-137">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from the command-line or using an IDE.</span></span> <span data-ttu-id="c6ed4-138">Инструкции по созданию проекта Java с использованием IntelliJ см. [здесь](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span><span class="sxs-lookup"><span data-stu-id="c6ed4-138">For instructions on how to create a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span></span> <span data-ttu-id="c6ed4-139">Инструкции по созданию проекта с использованием Eclipse см. [здесь](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span><span class="sxs-lookup"><span data-stu-id="c6ed4-139">For instructions on how to create a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span></span> 
2. <span data-ttu-id="c6ed4-140">Добавьте приведенные ниже зависимости в файл Maven **pom.xml**.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-140">Add the following dependencies to your Maven **pom.xml** file.</span></span> <span data-ttu-id="c6ed4-141">Добавьте следующий фрагмент текста между тегами **\</version>** и **\</project>**.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-141">Add the following snippet of text between the **\</version>** tag and the **\</project>** tag:</span></span>
   
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
   
    <span data-ttu-id="c6ed4-142">Первая зависимость предназначена для использования пакета SDK для Data Lake Store (`azure-data-lake-store-sdk`) из репозитория Maven.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-142">The first dependency is to use the Data Lake Store SDK (`azure-data-lake-store-sdk`) from the maven repository.</span></span> <span data-ttu-id="c6ed4-143">Вторая зависимость (`slf4j-nop`) нужна, чтобы указать, какие платформы ведения журналов будут использоваться для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-143">The second dependency (`slf4j-nop`) is to specify which logging framework to use for this application.</span></span> <span data-ttu-id="c6ed4-144">Пакет SDK для Data Lake Store использует библиотеку [SLF4J](http://www.slf4j.org/), которая позволяет выбрать любую из ряда популярных платформ ведения журналов, таких как Log4j, платформа для Java, Logback и др., или отключить ведение журнала.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-144">The Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span></span> <span data-ttu-id="c6ed4-145">В этом примере мы отключим ведение журнала, так как используем привязку **slf4j-nop**.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-145">For this example, we will disable logging, hence we use the **slf4j-nop** binding.</span></span> <span data-ttu-id="c6ed4-146">Сведения о других вариантах ведения журнала в приложении см. [здесь](http://www.slf4j.org/manual.html#projectDep).</span><span class="sxs-lookup"><span data-stu-id="c6ed4-146">To use other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span></span>

### <a name="add-the-application-code"></a><span data-ttu-id="c6ed4-147">Добавление кода приложения</span><span class="sxs-lookup"><span data-stu-id="c6ed4-147">Add the application code</span></span>
<span data-ttu-id="c6ed4-148">Код состоит из трех основных частей.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-148">There are three main parts to the code.</span></span>

1. <span data-ttu-id="c6ed4-149">Получение маркера Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-149">Obtain the Azure Active Directory token</span></span>
2. <span data-ttu-id="c6ed4-150">Использование маркера для создания клиента Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-150">Use the token to create a Data Lake Store client.</span></span>
3. <span data-ttu-id="c6ed4-151">Использование клиента Data Lake Store для выполнения операций.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-151">Use the Data Lake Store client to perform operations.</span></span>

#### <a name="step-1-obtain-an-azure-active-directory-token"></a><span data-ttu-id="c6ed4-152">Шаг 1. Получение маркера Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c6ed4-152">Step 1: Obtain an Azure Active Directory token.</span></span>
<span data-ttu-id="c6ed4-153">Пакет SDK для Data Lake Store предоставляет удобные методы управления маркерами безопасности, которые нужны для подключения к учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-153">The Data Lake Store SDK provides convenient methods that let you manage the security tokens needed to talk to the Data Lake Store account.</span></span> <span data-ttu-id="c6ed4-154">Тем не менее пакет SDK не требует использования только этих методов.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-154">However, the SDK does not mandate that only these methods be used.</span></span> <span data-ttu-id="c6ed4-155">Можно использовать любые другие средства получения маркера, например [пакет SDK для Azure Active Directory](https://github.com/AzureAD/azure-activedirectory-library-for-java) или пользовательский код.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-155">You can use any other means of obtaining token as well, like using the [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span></span>

<span data-ttu-id="c6ed4-156">Чтобы получить маркер для веб-приложения Active Directory, созданного ранее, с помощью пакета SDK для Data Lake Store, используйте один из подклассов `AccessTokenProvider` (в примере ниже используется `ClientCredsTokenProvider`).</span><span class="sxs-lookup"><span data-stu-id="c6ed4-156">To use the Data Lake Store SDK to obtain token for the Active Directory Web application you created earlier, use one of the subclasses of `AccessTokenProvider` (the example below uses `ClientCredsTokenProvider`).</span></span> <span data-ttu-id="c6ed4-157">Поставщик маркера кэширует в память учетные данные, которые использовались для получения маркера, и автоматически продлевает его истекающий срок действия.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-157">The token provider caches the creds used to obtain the token in memory, and automatically renews the token if it is about to expire.</span></span> <span data-ttu-id="c6ed4-158">Кроме того, вы можете создать собственные подклассы `AccessTokenProvider`. В этом случае маркеры будет получать код вашего клиента. Для наших целей мы будем использовать подкласс из пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-158">It is possible to create your own subclasses of `AccessTokenProvider` so tokens are obtained by your customer code, but for now let's just use the one provided in the SDK.</span></span>

<span data-ttu-id="c6ed4-159">Замените часть **FILL-IN-HERE** фактическими значениями, соответствующими веб-приложению Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-159">Replace **FILL-IN-HERE** with the actual values for the Azure Active Directory Web application.</span></span>

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a><span data-ttu-id="c6ed4-160">Шаг 2. Создание клиентского объекта Azure Data Lake Store (ADLStoreClient)</span><span class="sxs-lookup"><span data-stu-id="c6ed4-160">Step 2: Create an Azure Data Lake Store client (ADLStoreClient) object</span></span>
<span data-ttu-id="c6ed4-161">Создавая объект [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/), укажите имя учетной записи Data Lake Store и поставщик маркера, который вы создали на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-161">Creating an [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) object requires you to specify the Data Lake Store account name and the token provider you generated in the last step.</span></span> <span data-ttu-id="c6ed4-162">Обратите внимание, что для учетной записи Data Lake Store необходимо указать полное доменное имя.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-162">Note that the Data Lake Store account name needs to be a fully qualified domain name.</span></span> <span data-ttu-id="c6ed4-163">Например, замените часть **FILL-IN-HERE** примерно таким значением: **mydatalakestore.azuredatalakestore.net**.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-163">For example, replace **FILL-IN-HERE** with something like **mydatalakestore.azuredatalakestore.net**.</span></span>

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just the account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-the-adlstoreclient-to-perform-file-and-directory-operations"></a><span data-ttu-id="c6ed4-164">Шаг 3. Использование ADLStoreClient для выполнения операций с файлами и каталогами</span><span class="sxs-lookup"><span data-stu-id="c6ed4-164">Step 3: Use the ADLStoreClient to perform file and directory operations</span></span>
<span data-ttu-id="c6ed4-165">Приведенный ниже код содержит фрагменты для выполнения некоторых распространенных операций.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-165">The code below contains example snippets of some common operations.</span></span> <span data-ttu-id="c6ed4-166">Другие операции можно найти в полной [документации по API пакета Java SDK для Data Lake Store](https://azure.github.io/azure-data-lake-store-java/javadoc/) в разделе об объекте **ADLStoreClient**.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-166">You can look at the full [Data Lake Store Java SDK API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/) of the **ADLStoreClient** object to see other operations.</span></span>

<span data-ttu-id="c6ed4-167">Обратите внимание, что чтение файлов и запись в них осуществляется с помощью стандартных потоков Java.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-167">Note that files are read from and written into using standard Java streams.</span></span> <span data-ttu-id="c6ed4-168">Это означает, что вы можете разместить все потоки Java поверх потоков Data Lake Store, чтобы использовать стандартные возможности Java (например, потоки печати для получения отформатированных выходных данных либо потоки сжатия или шифрования для получения дополнительных возможностей поверх потоков и т. д.).</span><span class="sxs-lookup"><span data-stu-id="c6ed4-168">This means that you can layer any of the Java streams on top of the Data Lake Store streams to benefit from standard Java functionality (e.g., Print streams for formatted output, or any of the compression or encryption streams for additional functionality on top, etc.).</span></span>

     // create file and write some content
     String filename = "/a/b/c.txt";
     OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
     PrintStream out = new PrintStream(stream);
     for (int i = 1; i <= 10; i++) {
         out.println("This is line #" + i);
         out.format("This is the same line (%d), but using formatted output. %n", i);
     }
     out.close();
    
    // set file permission
    client.setPermission(filename, "744");

    // append to file
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

    // concatenate the two files into one
    List<String> fileList = Arrays.asList("/a/b/c.txt", "/a/b/d.txt");
    client.concatenateFiles("/a/b/f.txt", fileList);

    //rename the file
    client.rename("/a/b/f.txt", "/a/b/g.txt");

    // list directory contents
    List<DirectoryEntry> list = client.enumerateDirectory("/a/b", 2000);
    System.out.println("Directory listing for directory /a/b:");
    for (DirectoryEntry entry : list) {
        printDirectoryInfo(entry);
    }

    // delete directory along with all the subdirectories and files in it
    client.deleteRecursive("/a");

#### <a name="step-4-build-and-run-the-application"></a><span data-ttu-id="c6ed4-169">Шаг 4. Сборка и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="c6ed4-169">Step 4: Build and run the application</span></span>
1. <span data-ttu-id="c6ed4-170">Для запуска из среды IDE найдите и нажмите кнопку **запуска**.</span><span class="sxs-lookup"><span data-stu-id="c6ed4-170">To run from within an IDE, locate and press the **Run** button.</span></span> <span data-ttu-id="c6ed4-171">Для запуска из Maven выполните команду [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span><span class="sxs-lookup"><span data-stu-id="c6ed4-171">To run from Maven, use [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span></span>
2. <span data-ttu-id="c6ed4-172">Чтобы получить автономный JAR-файл, который можно запустить из командной строки, создайте такой файл со всеми зависимостями с помощью [подключаемого модуля сборки Maven](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span><span class="sxs-lookup"><span data-stu-id="c6ed4-172">To produce a standalone jar that you can run from command-line build the jar with all dependencies included, using the [Maven assembly plugin](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span></span> <span data-ttu-id="c6ed4-173">Код для выполнения этих действий содержится в файле pom.xml в [примере исходного кода на сайте GitHub](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml).</span><span class="sxs-lookup"><span data-stu-id="c6ed4-173">The pom.xml in the [example source code on github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) has an example of how to do this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6ed4-174">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c6ed4-174">Next steps</span></span>
* [<span data-ttu-id="c6ed4-175">Документация по пакету SDK для Java</span><span class="sxs-lookup"><span data-stu-id="c6ed4-175">Explore JavaDoc for the Java SDK</span></span>](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [<span data-ttu-id="c6ed4-176">Защита данных в хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="c6ed4-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="c6ed4-177">Использование аналитики озера данных Azure с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="c6ed4-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="c6ed4-178">Использование Azure HDInsight с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="c6ed4-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

