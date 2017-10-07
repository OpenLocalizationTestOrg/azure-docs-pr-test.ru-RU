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
# <a name="using-java-command-line-app-tooaccess-an-api-with-azure-ad"></a>С помощью приложения командной строки Java tooAccess API в Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure AD делает простым и понятным toooutsource управления идентификацией веб-приложения, предоставляя единого входа и выхода с помощью всего нескольких строк кода.  В веб-приложений Java это можно сделать с помощью реализации hello сообщество ведет ADAL4J корпорации Майкрософт.

  Мы будем использовать ADAL4J для следующего:

* Пользователь hello входа в приложение hello, с помощью Azure AD как поставщика удостоверений hello.
* Отображать некоторые сведения о пользователе hello.
* Знак hello выход пользователя из приложения hello.

В заказ toodo это, вам потребуется:

1. зарегистрировать приложение в Azure AD;
2. Настройка библиотеки приложения hello toouse ADAL4J.
3. Используйте hello ADAL4J библиотеки tooissue вход и запросах на выход tooAzure AD.
4. Выводит данные о пользователе hello.

tooget к работе, [загрузить каркас приложения hello](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) или [загрузить образец hello завершения](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).  Кроме того, потребуется клиент Azure AD, в которой tooregister приложения.  Если вы их еще нет, [Узнайте, как один tooget](active-directory-howto-tenant.md).

## <a name="1--register-an-application-with-azure-ad"></a>1.  Регистрация приложения в Azure AD
tooenable tooauthenticate пользователи вашего приложения, сначала необходимо tooregister новое приложение в клиенте.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. На верхней панели hello, нажмите кнопку в вашей учетной записи, а также в разделе hello **каталога** выберите hello клиента Active Directory, где будут tooregister приложения.
3. Щелкните **более служб** в hello левую панель навигации и выберите **Azure Active Directory**.
4. Щелкните **Регистрация приложений** и нажмите кнопку **Добавить**.
5. Следуйте инструкциям hello и создайте новый **веб-приложение или WebAPI**.
  * Hello **имя** из hello приложения будет описывать tooend пользователей вашего приложения
  * Hello **URL-адрес входа** hello базовый URL-адрес приложения.  по умолчанию Hello основу — `http://localhost:8080/adal4jsample/`.
6. После завершения регистрации служба Azure AD присваивает приложению уникальный идентификатор приложения.  Это значение необходимо в следующих разделах hello, поэтому скопируйте его с вкладка "приложение" hello.
7. Из hello **параметры** -> **свойства** страницы приложения, обновите URI идентификатора приложения hello. Hello **URI идентификатора приложения** — это уникальный идентификатор для вашего приложения.  соглашение о Hello — toouse `https://<tenant-domain>/<app-name>`, например `http://localhost:8080/adal4jsample/`.

Один раз в портале hello для приложения создать **ключ** из hello **параметры** для приложения и скопируйте его.  Скоро он вам понадобится.

## <a name="2-set-up-your-app-toouse-adal4j-library-and-prerequisites-using-maven"></a>2. Настройка библиотеки ADAL4J toouse приложения и необходимые компоненты с помощью Maven
Здесь мы настроим ADAL4J toouse hello OpenID Connect протокол проверки подлинности.  ADAL4J быть используется tooissue запросы на вход и выход, управлять сеансом пользователя hello и получения сведений о пользователе hello, среди прочего.

* В корневом каталоге проекта hello, открыть или создать `pom.xml` и найдите hello `// TODO: provide dependencies for Maven` и замените hello следующее:

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



## <a name="3-create-hello-java-publicclient-file"></a>3. Создайте файл Java PublicClient hello
Как указано выше, мы используем hello Graph API tooget данные о приветствия вошедшего пользователя. Для этого нам без труда toobe следует создать оба файла toorepresent **объект каталога** и hello отдельного файла toorepresent **пользователя** , чтобы hello OO шаблон Java, можно использовать.

* Создайте файл с именем `DirectoryObject.java` которой мы будем использовать toostore основные данные о любой DirectoryObject (вы можете бесплатно toouse это позже для других запросов Graph, вы можете). Вставьте в файл следующий код:

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


## <a name="compile-and-run-hello-sample"></a>Компиляция и выполнение образца hello
Измените обратно out tooyour корневой каталог и запустите hello, следующая команда toobuild hello образец только что выполнена с помощью `maven`. Будут использованы hello `pom.xml` файла, написанного для зависимостей.

`$ mvn package`

Теперь в каталоге `/targets` должен быть файл `adal4jsample.war`. Вы можете развернуть, в контейнере Tomcat и посетите URL-адрес hello 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> Это очень легко toodeploy WAR с последней серверы Tomcat hello. Просто перейдите слишком`http://localhost:8080/manager/` и следуйте инструкциям, hello об отправке вашего '' adal4jsample.war "файла. Он будет autodeploy для вас с hello правильную конечную точку.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
Поздравляем! Теперь имеют работающее приложение Java, которое имеет hello возможность tooauthenticate пользователей, безопасно вызвать веб-API с помощью OAuth 2.0 и получить основные сведения о пользователе hello.  Если это еще не сделано, пришло время toopopulate hello вашего клиента с некоторым пользователям.

Справочник по hello выполнить пример (без настройки) [предоставляется как .zip здесь](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), или вы можете клонировать из GitHub:

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

