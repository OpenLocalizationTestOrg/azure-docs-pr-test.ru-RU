---
title: "Приступая к работе с Azure AD с помощью командной строки Java | Документация Майкрософт"
description: "Создание приложения командной строки Java, выполняющего вход для пользователей для доступа к API."
services: active-directory
documentationcenter: java
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 51e1a8f9-6ff0-4643-a350-0ba794e26fd1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 01/23/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 91e4a7b2ac454465d5cce4948a4d5f0b542d2b55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="using-java-command-line-app-to-access-an-api-with-azure-ad"></a><span data-ttu-id="0d324-103">Использование приложения командной строки Java для доступа к API с помощью Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d324-103">Using Java Command Line App To Access An API with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="0d324-104">Azure AD позволяет простым и удобным образом выполнять функции управления удостоверением вашего веб-приложения, обеспечивая единый вход и выход с помощью всего лишь нескольких строк кода.</span><span class="sxs-lookup"><span data-stu-id="0d324-104">Azure AD makes it simple and straightforward to outsource your web app's identity management, providing single sign-in and sign-out with only a few lines of code.</span></span>  <span data-ttu-id="0d324-105">В веб-приложениях Java это можно делать с помощью реализации корпорации Майкрософт, поддерживаемой сообществом библиотеки ADAL4J.</span><span class="sxs-lookup"><span data-stu-id="0d324-105">In Java web apps, you can accomplish this using Microsoft's implementation of the community-driven ADAL4J.</span></span>

  <span data-ttu-id="0d324-106">Мы будем использовать ADAL4J для следующего:</span><span class="sxs-lookup"><span data-stu-id="0d324-106">Here we'll use ADAL4J to:</span></span>

* <span data-ttu-id="0d324-107">Вход пользователя в приложение с использованием Azure AD как поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="0d324-107">Sign the user into the app using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="0d324-108">Отображение некоторой информации о пользователе.</span><span class="sxs-lookup"><span data-stu-id="0d324-108">Display some information about the user.</span></span>
* <span data-ttu-id="0d324-109">Выход пользователя из приложения.</span><span class="sxs-lookup"><span data-stu-id="0d324-109">Sign the user out of the app.</span></span>

<span data-ttu-id="0d324-110">Для этого необходимо:</span><span class="sxs-lookup"><span data-stu-id="0d324-110">In order to do this, you'll need to:</span></span>

1. <span data-ttu-id="0d324-111">зарегистрировать приложение в Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0d324-111">Register an application with Azure AD</span></span>
2. <span data-ttu-id="0d324-112">настроить приложение для использования библиотеки ADAL4J;</span><span class="sxs-lookup"><span data-stu-id="0d324-112">Set up your app to use the ADAL4J library.</span></span>
3. <span data-ttu-id="0d324-113">использовать библиотеку ADAL4J для отправки запросов в службу Azure AD на вход и выход;</span><span class="sxs-lookup"><span data-stu-id="0d324-113">Use the ADAL4J library to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="0d324-114">распечатать данные о пользователе.</span><span class="sxs-lookup"><span data-stu-id="0d324-114">Print out data about the user.</span></span>

<span data-ttu-id="0d324-115">Чтобы начать работу, [скачайте схему приложения](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) или [скачайте готовый пример](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="0d324-115">To get started, [download the app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) or [download the completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span></span>  <span data-ttu-id="0d324-116">Вам также потребуется клиент Azure AD для регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="0d324-116">You'll also need an Azure AD tenant in which to register your application.</span></span>  <span data-ttu-id="0d324-117">Если у вас нет клиента, [узнайте, как его получить](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="0d324-117">If you don't have one already, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1--register-an-application-with-azure-ad"></a><span data-ttu-id="0d324-118">1.  Регистрация приложения в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d324-118">1.  Register an Application with Azure AD</span></span>
<span data-ttu-id="0d324-119">Чтобы ваше приложение могло осуществлять проверку подлинности пользователей, сначала необходимо зарегистрировать новое приложение в своем клиенте.</span><span class="sxs-lookup"><span data-stu-id="0d324-119">To enable your app to authenticate users, you'll first need to register a new application in your tenant.</span></span>

1. <span data-ttu-id="0d324-120">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0d324-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0d324-121">На верхней панели щелкните учетную запись и в списке **Каталог** выберите клиент Active Directory, в котором хотите зарегистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="0d324-121">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="0d324-122">В левой области навигации щелкните **Другие службы** и выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0d324-122">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="0d324-123">Щелкните **Регистрация приложений** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0d324-123">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="0d324-124">Следуйте инструкциям на экране, а затем создайте новое **веб-приложение и/или WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="0d324-124">Follow the prompts and create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="0d324-125">**Имя** приложения отображает его описание конечным пользователям.</span><span class="sxs-lookup"><span data-stu-id="0d324-125">The **name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="0d324-126">**URL-адрес входа** — это базовый URL-адрес вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="0d324-126">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="0d324-127">Схема по умолчанию — `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="0d324-127">The skeleton's default is `http://localhost:8080/adal4jsample/`.</span></span>
6. <span data-ttu-id="0d324-128">После завершения регистрации служба Azure AD присваивает приложению уникальный идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="0d324-128">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="0d324-129">Это значение вам понадобится в следующих разделах, поэтому скопируйте его с вкладки приложения.</span><span class="sxs-lookup"><span data-stu-id="0d324-129">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="0d324-130">На странице **Параметры** -> **Свойства** приложения обновите его универсальный код ресурса (URI) идентификатора.</span><span class="sxs-lookup"><span data-stu-id="0d324-130">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="0d324-131">**URI идентификатора приложения** — это уникальный идентификатор вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="0d324-131">The **App ID URI** is a unique identifier for your application.</span></span>  <span data-ttu-id="0d324-132">В соответствии с соглашением, следует использовать `https://<tenant-domain>/<app-name>`, например `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="0d324-132">The convention is to use `https://<tenant-domain>/<app-name>`, e.g. `http://localhost:8080/adal4jsample/`.</span></span>

<span data-ttu-id="0d324-133">Войдите на портал приложения, создайте **ключ** на странице **Настройки** своего приложения и скопируйте его.</span><span class="sxs-lookup"><span data-stu-id="0d324-133">Once in the portal for your app create a **Key** from the **Settings** page for your application and copy it down.</span></span>  <span data-ttu-id="0d324-134">Скоро он вам понадобится.</span><span class="sxs-lookup"><span data-stu-id="0d324-134">You will need it shortly.</span></span>

## <a name="2-set-up-your-app-to-use-adal4j-library-and-prerequisites-using-maven"></a><span data-ttu-id="0d324-135">2) Настройка приложения для использования библиотеки ADAL4J и всех необходимых компонентов с помощью Maven</span><span class="sxs-lookup"><span data-stu-id="0d324-135">2. Set up your app to use ADAL4J library and prerequisites using Maven</span></span>
<span data-ttu-id="0d324-136">Здесь мы настроим библиотеку ADAL4J для использования протокола проверки подлинности OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="0d324-136">Here, we'll configure ADAL4J to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="0d324-137">Кроме всего прочего, ADAL4J будет использоваться для выдачи запросов на вход и выход, управления сеансом пользователя и получения сведений о пользователе.</span><span class="sxs-lookup"><span data-stu-id="0d324-137">ADAL4J will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

* <span data-ttu-id="0d324-138">В корневом каталоге проекта откройте или создайте файл `pom.xml`, найдите строку `// TODO: provide dependencies for Maven` и замените ее следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="0d324-138">In the root directory of your project, open/create `pom.xml` and locate the `// TODO: provide dependencies for Maven` and replace with the following:</span></span>

```Java
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>public-client-adal4j-sample</artifactId>
    <packaging>jar</packaging>
    <version>0.0.1-SNAPSHOT</version>
    <name>public-client-adal4j-sample</name>
    <url>http://maven.apache.org</url>
    <properties>
        <spring.version>3.0.5.RELEASE</spring.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>adal4j</artifactId>
            <version>1.1.2</version>
        </dependency>
        <dependency>
            <groupId>com.nimbusds</groupId>
            <artifactId>oauth2-oidc-sdk</artifactId>
            <version>4.5</version>
        </dependency>
        <dependency>
            <groupId>org.json</groupId>
            <artifactId>json</artifactId>
            <version>20090211</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.0.1</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>1.7.5</version>
        </dependency>
</dependencies>
    <build>
        <finalName>public-client-adal4j-sample</finalName>
        <plugins>
                <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <version>1.2.1</version>
            <configuration>
                <mainClass>PublicClient</mainClass>
            </configuration>
        </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.7</source>
                    <target>1.7</target>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <executions>
                    <execution>
                        <id>install</id>
                        <phase>install</phase>
                        <goals>
                            <goal>sources</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-resources-plugin</artifactId>
                <version>2.5</version>
                <configuration>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
        <artifactId>maven-assembly-plugin</artifactId>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>single</goal>
            </goals>
          </execution>
        </executions>
        <configuration>
          <descriptorRefs>
            <descriptorRef>jar-with-dependencies</descriptorRef>
          </descriptorRefs>
        </configuration>
      </plugin>
      <plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-assembly-plugin</artifactId>
  <configuration>
    <archive>
      <manifest>
        <mainClass>PublicClient</mainClass>
      </manifest>
    </archive>
  </configuration>
</plugin>
        </plugins>
    </build>

</project>


```



## <a name="3-create-the-java-publicclient-file"></a><span data-ttu-id="0d324-139">3. Создание файла Java PublicClient</span><span class="sxs-lookup"><span data-stu-id="0d324-139">3. Create the Java PublicClient file</span></span>
<span data-ttu-id="0d324-140">Как упоминалось выше, мы будет использовать API Graph для получения данных о вошедшем в систему пользователе.</span><span class="sxs-lookup"><span data-stu-id="0d324-140">As indicated above, we will be using the Graph API to get data about the logged in user.</span></span> <span data-ttu-id="0d324-141">Для этого нам нужно создать файл, который будет представлять **объект каталога**, и отдельный файл, который будет представлять **пользователя**, чтобы можно было использовать объектно-ориентированный шаблон Java.</span><span class="sxs-lookup"><span data-stu-id="0d324-141">For this to be easy for us we should create both a file to represent a **Directory Object** and an individual file to represent the **User** so that the OO pattern of Java can be used.</span></span>

* <span data-ttu-id="0d324-142">Создайте файл с именем `DirectoryObject.java`, в котором будут храниться данные о любом объекте DirectoryObject. Вы можете использовать этот объект для любых других запросов Graph.</span><span class="sxs-lookup"><span data-stu-id="0d324-142">Create a file called `DirectoryObject.java` which we will use to store basic data about any DirectoryObject (you can feel free to use this later for any other Graph Queries you may do).</span></span> <span data-ttu-id="0d324-143">Вставьте в файл следующий код:</span><span class="sxs-lookup"><span data-stu-id="0d324-143">You can cut/paste this from below:</span></span>

```Java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

import javax.naming.ServiceUnavailableException;

import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;

public class PublicClient {

    private final static String AUTHORITY = "https://login.microsoftonline.com/common/";
    private final static String CLIENT_ID = "2a4da06c-ff07-410d-af8a-542a512f5092";

    public static void main(String args[]) throws Exception {

        try (BufferedReader br = new BufferedReader(new InputStreamReader(
                System.in))) {
            System.out.print("Enter username: ");
            String username = br.readLine();
            System.out.print("Enter password: ");
            String password = br.readLine();

            AuthenticationResult result = getAccessTokenFromUserCredentials(
                    username, password);
            System.out.println("Access Token - " + result.getAccessToken());
            System.out.println("Refresh Token - " + result.getRefreshToken());
            System.out.println("ID Token - " + result.getIdToken());
        }
    }

    private static AuthenticationResult getAccessTokenFromUserCredentials(
            String username, String password) throws Exception {
        AuthenticationContext context = null;
        AuthenticationResult result = null;
        ExecutorService service = null;
        try {
            service = Executors.newFixedThreadPool(1);
            context = new AuthenticationContext(AUTHORITY, false, service);
            Future<AuthenticationResult> future = context.acquireToken(
                    "https://graph.windows.net", CLIENT_ID, username, password,
                    null);
            result = future.get();
        } finally {
            service.shutdown();
        }

        if (result == null) {
            throw new ServiceUnavailableException(
                    "authentication result was null");
        }
        return result;
    }
}


```


## <a name="compile-and-run-the-sample"></a><span data-ttu-id="0d324-144">Компиляция и запуск примера</span><span class="sxs-lookup"><span data-stu-id="0d324-144">Compile and run the sample</span></span>
<span data-ttu-id="0d324-145">Вернитесь в корневой каталог и выполните следующую команду, чтобы скомпилировать пример, который вы только что собрали с помощью `maven`.</span><span class="sxs-lookup"><span data-stu-id="0d324-145">Change back out to your root directory and run the following command to build the sample you just put together using `maven`.</span></span> <span data-ttu-id="0d324-146">Эта команда будет использовать файл `pom.xml` , созданный для зависимостей.</span><span class="sxs-lookup"><span data-stu-id="0d324-146">This will use the `pom.xml` file you wrote for dependencies.</span></span>

`$ mvn package`

<span data-ttu-id="0d324-147">Теперь в каталоге `/targets` должен быть файл `adal4jsample.war`.</span><span class="sxs-lookup"><span data-stu-id="0d324-147">You should now have a `adal4jsample.war` file in your `/targets` directory.</span></span> <span data-ttu-id="0d324-148">Вы можете развернуть его в контейнер Tomcat и открыть URL-адрес</span><span class="sxs-lookup"><span data-stu-id="0d324-148">You may deploy that in your Tomcat container and visit the URL</span></span> 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> <span data-ttu-id="0d324-149">WAR-файлы очень просто развертывать с помощью последних версий серверов Tomcat.</span><span class="sxs-lookup"><span data-stu-id="0d324-149">It is very easy to deploy a WAR with the latest Tomcat servers.</span></span> <span data-ttu-id="0d324-150">Просто перейдите в папку `http://localhost:8080/manager/` и следуйте инструкциям по передаче файла adal4jsample.war.</span><span class="sxs-lookup"><span data-stu-id="0d324-150">Simply navigate to `http://localhost:8080/manager/` and follow the instructions on uploading your ``adal4jsample.war\` file.</span></span> <span data-ttu-id="0d324-151">Он будет автоматически развернут с правильной конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="0d324-151">It will autodeploy for you with the correct endpoint.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0d324-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0d324-152">Next Steps</span></span>
<span data-ttu-id="0d324-153">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="0d324-153">Congratulations!</span></span> <span data-ttu-id="0d324-154">Теперь у нас есть рабочее приложение Java, которое позволяет проверять подлинность пользователей, безопасно вызывать методы веб-API по протоколу OAuth 2.0 и получать основные сведения о пользователе.</span><span class="sxs-lookup"><span data-stu-id="0d324-154">You now have a working Java application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="0d324-155">Если же вы этого еще не сделали, пришло время добавить в клиент нескольких пользователей.</span><span class="sxs-lookup"><span data-stu-id="0d324-155">If you haven't already, now is the time to populate your tenant with some users.</span></span>

<span data-ttu-id="0d324-156">Готовый пример (без ваших значений конфигурации) [можно скачать в виде ZIP-файла здесь](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip)или клонировать с портала GitHub.</span><span class="sxs-lookup"><span data-stu-id="0d324-156">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

