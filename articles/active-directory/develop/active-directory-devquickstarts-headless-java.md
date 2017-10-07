---
title: "aaaAzure командной строки AD Java начало работы | Документы Microsoft"
description: "Как toobuild Java командной строки приложение, которое подписывает пользователей в tooaccess API."
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
ms.openlocfilehash: 9ba1d1e794928a39ca1f091bd0e6eba57ce3d6aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-java-command-line-app-tooaccess-an-api-with-azure-ad"></a><span data-ttu-id="83c2e-103">С помощью приложения командной строки Java tooAccess API в Azure AD</span><span class="sxs-lookup"><span data-stu-id="83c2e-103">Using Java Command Line App tooAccess An API with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="83c2e-104">Azure AD делает простым и понятным toooutsource управления идентификацией веб-приложения, предоставляя единого входа и выхода с помощью всего нескольких строк кода.</span><span class="sxs-lookup"><span data-stu-id="83c2e-104">Azure AD makes it simple and straightforward toooutsource your web app's identity management, providing single sign-in and sign-out with only a few lines of code.</span></span>  <span data-ttu-id="83c2e-105">В веб-приложений Java это можно сделать с помощью реализации hello сообщество ведет ADAL4J корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="83c2e-105">In Java web apps, you can accomplish this using Microsoft's implementation of hello community-driven ADAL4J.</span></span>

  <span data-ttu-id="83c2e-106">Мы будем использовать ADAL4J для следующего:</span><span class="sxs-lookup"><span data-stu-id="83c2e-106">Here we'll use ADAL4J to:</span></span>

* <span data-ttu-id="83c2e-107">Пользователь hello входа в приложение hello, с помощью Azure AD как поставщика удостоверений hello.</span><span class="sxs-lookup"><span data-stu-id="83c2e-107">Sign hello user into hello app using Azure AD as hello identity provider.</span></span>
* <span data-ttu-id="83c2e-108">Отображать некоторые сведения о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="83c2e-108">Display some information about hello user.</span></span>
* <span data-ttu-id="83c2e-109">Знак hello выход пользователя из приложения hello.</span><span class="sxs-lookup"><span data-stu-id="83c2e-109">Sign hello user out of hello app.</span></span>

<span data-ttu-id="83c2e-110">В заказ toodo это, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="83c2e-110">In order toodo this, you'll need to:</span></span>

1. <span data-ttu-id="83c2e-111">зарегистрировать приложение в Azure AD;</span><span class="sxs-lookup"><span data-stu-id="83c2e-111">Register an application with Azure AD</span></span>
2. <span data-ttu-id="83c2e-112">Настройка библиотеки приложения hello toouse ADAL4J.</span><span class="sxs-lookup"><span data-stu-id="83c2e-112">Set up your app toouse hello ADAL4J library.</span></span>
3. <span data-ttu-id="83c2e-113">Используйте hello ADAL4J библиотеки tooissue вход и запросах на выход tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="83c2e-113">Use hello ADAL4J library tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="83c2e-114">Выводит данные о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="83c2e-114">Print out data about hello user.</span></span>

<span data-ttu-id="83c2e-115">tooget к работе, [загрузить каркас приложения hello](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) или [загрузить образец hello завершения](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="83c2e-115">tooget started, [download hello app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) or [download hello completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span></span>  <span data-ttu-id="83c2e-116">Кроме того, потребуется клиент Azure AD, в которой tooregister приложения.</span><span class="sxs-lookup"><span data-stu-id="83c2e-116">You'll also need an Azure AD tenant in which tooregister your application.</span></span>  <span data-ttu-id="83c2e-117">Если вы их еще нет, [Узнайте, как один tooget](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="83c2e-117">If you don't have one already, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1--register-an-application-with-azure-ad"></a><span data-ttu-id="83c2e-118">1.  Регистрация приложения в Azure AD</span><span class="sxs-lookup"><span data-stu-id="83c2e-118">1.  Register an Application with Azure AD</span></span>
<span data-ttu-id="83c2e-119">tooenable tooauthenticate пользователи вашего приложения, сначала необходимо tooregister новое приложение в клиенте.</span><span class="sxs-lookup"><span data-stu-id="83c2e-119">tooenable your app tooauthenticate users, you'll first need tooregister a new application in your tenant.</span></span>

1. <span data-ttu-id="83c2e-120">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="83c2e-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="83c2e-121">На верхней панели hello, нажмите кнопку в вашей учетной записи, а также в разделе hello **каталога** выберите hello клиента Active Directory, где будут tooregister приложения.</span><span class="sxs-lookup"><span data-stu-id="83c2e-121">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="83c2e-122">Щелкните **более служб** в hello левую панель навигации и выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="83c2e-122">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="83c2e-123">Щелкните **Регистрация приложений** и нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="83c2e-123">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="83c2e-124">Следуйте инструкциям hello и создайте новый **веб-приложение или WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="83c2e-124">Follow hello prompts and create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="83c2e-125">Hello **имя** из hello приложения будет описывать tooend пользователей вашего приложения</span><span class="sxs-lookup"><span data-stu-id="83c2e-125">hello **name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="83c2e-126">Hello **URL-адрес входа** hello базовый URL-адрес приложения.</span><span class="sxs-lookup"><span data-stu-id="83c2e-126">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="83c2e-127">по умолчанию Hello основу — `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="83c2e-127">hello skeleton's default is `http://localhost:8080/adal4jsample/`.</span></span>
6. <span data-ttu-id="83c2e-128">После завершения регистрации служба Azure AD присваивает приложению уникальный идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="83c2e-128">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="83c2e-129">Это значение необходимо в следующих разделах hello, поэтому скопируйте его с вкладка "приложение" hello.</span><span class="sxs-lookup"><span data-stu-id="83c2e-129">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="83c2e-130">Из hello **параметры** -> **свойства** страницы приложения, обновите URI идентификатора приложения hello.</span><span class="sxs-lookup"><span data-stu-id="83c2e-130">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="83c2e-131">Hello **URI идентификатора приложения** — это уникальный идентификатор для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="83c2e-131">hello **App ID URI** is a unique identifier for your application.</span></span>  <span data-ttu-id="83c2e-132">соглашение о Hello — toouse `https://<tenant-domain>/<app-name>`, например `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="83c2e-132">hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `http://localhost:8080/adal4jsample/`.</span></span>

<span data-ttu-id="83c2e-133">Один раз в портале hello для приложения создать **ключ** из hello **параметры** для приложения и скопируйте его.</span><span class="sxs-lookup"><span data-stu-id="83c2e-133">Once in hello portal for your app create a **Key** from hello **Settings** page for your application and copy it down.</span></span>  <span data-ttu-id="83c2e-134">Скоро он вам понадобится.</span><span class="sxs-lookup"><span data-stu-id="83c2e-134">You will need it shortly.</span></span>

## <a name="2-set-up-your-app-toouse-adal4j-library-and-prerequisites-using-maven"></a><span data-ttu-id="83c2e-135">2. Настройка библиотеки ADAL4J toouse приложения и необходимые компоненты с помощью Maven</span><span class="sxs-lookup"><span data-stu-id="83c2e-135">2. Set up your app toouse ADAL4J library and prerequisites using Maven</span></span>
<span data-ttu-id="83c2e-136">Здесь мы настроим ADAL4J toouse hello OpenID Connect протокол проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="83c2e-136">Here, we'll configure ADAL4J toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="83c2e-137">ADAL4J быть используется tooissue запросы на вход и выход, управлять сеансом пользователя hello и получения сведений о пользователе hello, среди прочего.</span><span class="sxs-lookup"><span data-stu-id="83c2e-137">ADAL4J will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

* <span data-ttu-id="83c2e-138">В корневом каталоге проекта hello, открыть или создать `pom.xml` и найдите hello `// TODO: provide dependencies for Maven` и замените hello следующее:</span><span class="sxs-lookup"><span data-stu-id="83c2e-138">In hello root directory of your project, open/create `pom.xml` and locate hello `// TODO: provide dependencies for Maven` and replace with hello following:</span></span>

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



## <a name="3-create-hello-java-publicclient-file"></a><span data-ttu-id="83c2e-139">3. Создайте файл Java PublicClient hello</span><span class="sxs-lookup"><span data-stu-id="83c2e-139">3. Create hello Java PublicClient file</span></span>
<span data-ttu-id="83c2e-140">Как указано выше, мы используем hello Graph API tooget данные о приветствия вошедшего пользователя.</span><span class="sxs-lookup"><span data-stu-id="83c2e-140">As indicated above, we will be using hello Graph API tooget data about hello logged in user.</span></span> <span data-ttu-id="83c2e-141">Для этого нам без труда toobe следует создать оба файла toorepresent **объект каталога** и hello отдельного файла toorepresent **пользователя** , чтобы hello OO шаблон Java, можно использовать.</span><span class="sxs-lookup"><span data-stu-id="83c2e-141">For this toobe easy for us we should create both a file toorepresent a **Directory Object** and an individual file toorepresent hello **User** so that hello OO pattern of Java can be used.</span></span>

* <span data-ttu-id="83c2e-142">Создайте файл с именем `DirectoryObject.java` которой мы будем использовать toostore основные данные о любой DirectoryObject (вы можете бесплатно toouse это позже для других запросов Graph, вы можете).</span><span class="sxs-lookup"><span data-stu-id="83c2e-142">Create a file called `DirectoryObject.java` which we will use toostore basic data about any DirectoryObject (you can feel free toouse this later for any other Graph Queries you may do).</span></span> <span data-ttu-id="83c2e-143">Вставьте в файл следующий код:</span><span class="sxs-lookup"><span data-stu-id="83c2e-143">You can cut/paste this from below:</span></span>

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


## <a name="compile-and-run-hello-sample"></a><span data-ttu-id="83c2e-144">Компиляция и выполнение образца hello</span><span class="sxs-lookup"><span data-stu-id="83c2e-144">Compile and run hello sample</span></span>
<span data-ttu-id="83c2e-145">Измените обратно out tooyour корневой каталог и запустите hello, следующая команда toobuild hello образец только что выполнена с помощью `maven`.</span><span class="sxs-lookup"><span data-stu-id="83c2e-145">Change back out tooyour root directory and run hello following command toobuild hello sample you just put together using `maven`.</span></span> <span data-ttu-id="83c2e-146">Будут использованы hello `pom.xml` файла, написанного для зависимостей.</span><span class="sxs-lookup"><span data-stu-id="83c2e-146">This will use hello `pom.xml` file you wrote for dependencies.</span></span>

`$ mvn package`

<span data-ttu-id="83c2e-147">Теперь в каталоге `/targets` должен быть файл `adal4jsample.war`.</span><span class="sxs-lookup"><span data-stu-id="83c2e-147">You should now have a `adal4jsample.war` file in your `/targets` directory.</span></span> <span data-ttu-id="83c2e-148">Вы можете развернуть, в контейнере Tomcat и посетите URL-адрес hello</span><span class="sxs-lookup"><span data-stu-id="83c2e-148">You may deploy that in your Tomcat container and visit hello URL</span></span> 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> <span data-ttu-id="83c2e-149">Это очень легко toodeploy WAR с последней серверы Tomcat hello.</span><span class="sxs-lookup"><span data-stu-id="83c2e-149">It is very easy toodeploy a WAR with hello latest Tomcat servers.</span></span> <span data-ttu-id="83c2e-150">Просто перейдите слишком`http://localhost:8080/manager/` и следуйте инструкциям, hello об отправке вашего '' adal4jsample.war "файла.</span><span class="sxs-lookup"><span data-stu-id="83c2e-150">Simply navigate too`http://localhost:8080/manager/` and follow hello instructions on uploading your ``adal4jsample.war\` file.</span></span> <span data-ttu-id="83c2e-151">Он будет autodeploy для вас с hello правильную конечную точку.</span><span class="sxs-lookup"><span data-stu-id="83c2e-151">It will autodeploy for you with hello correct endpoint.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="83c2e-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="83c2e-152">Next Steps</span></span>
<span data-ttu-id="83c2e-153">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="83c2e-153">Congratulations!</span></span> <span data-ttu-id="83c2e-154">Теперь имеют работающее приложение Java, которое имеет hello возможность tooauthenticate пользователей, безопасно вызвать веб-API с помощью OAuth 2.0 и получить основные сведения о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="83c2e-154">You now have a working Java application that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="83c2e-155">Если это еще не сделано, пришло время toopopulate hello вашего клиента с некоторым пользователям.</span><span class="sxs-lookup"><span data-stu-id="83c2e-155">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>

<span data-ttu-id="83c2e-156">Справочник по hello выполнить пример (без настройки) [предоставляется как .zip здесь](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), или вы можете клонировать из GitHub:</span><span class="sxs-lookup"><span data-stu-id="83c2e-156">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

