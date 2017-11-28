---
title: "hello toouse aaaHow начальный Spring загрузки с API DocumentDB Azure DB Cosmos"
description: "Узнайте, как tooconfigure приложение создано в hello Spring загрузки инициализатор с hello Azure Cosmos DB DocumentDB API."
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
keywords: "Spring, начальное приложение Spring Boot, Cosmos DB"
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/08/2017
ms.author: robmcm;yungez;kevinzha
ms.openlocfilehash: a2c6de678f850676cb2887e224e5c12950db0e53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="ca3c9-104">Как toouse hello Spring начальный загрузки с помощью Azure Cosmos DB DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="ca3c9-104">How toouse hello Spring Boot Starter with Azure Cosmos DB DocumentDB API</span></span>

## <a name="overview"></a><span data-ttu-id="ca3c9-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="ca3c9-105">Overview</span></span>

<span data-ttu-id="ca3c9-106">Hello  **[Spring Framework]**  — это решение открытым исходным кодом, разработчики Java могут создавать корпоративные приложения.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-106">hello **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="ca3c9-107">Один из проектов более популярных hello, построенных на основе этой платформы является [загрузки Spring], который предоставляет упрощенный подход для создания изолированного приложения Java.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-107">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="ca3c9-108">Разработчики toohelp начать работу с загрузкой Spring, несколько образцов Spring загрузки пакетов можно найти по адресу <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-108">toohelp developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="ca3c9-109">В дополнение к этому toochoosing списке hello базового загрузочного Spring проекты, hello  **[Spring Initializr]**  помогает разработчикам Приступая к работе с созданием пользовательских приложений Spring загрузки.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-109">In addition toochoosing from hello list of basic Spring Boot projects, hello **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="ca3c9-110">Azure Cosmos DB является глобально распределенной базы данных службы, которая позволяет разработчикам toowork с данными, с помощью различных стандартных API, например DocumentDB, MongoDB, диаграммы и таблицы API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-110">Azure Cosmos DB is a globally-distributed database service that allows developers toowork with data using a variety of standard APIs, such as DocumentDB, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="ca3c9-111">Начальный загрузки Spring корпорации Майкрософт позволяет приложений Spring загрузки toouse разработчики, которые легко интегрируются с Azure Cosmos DB с помощью интерфейсов API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-111">Microsoft's Spring Boot Starter enables developers toouse Spring Boot applications that easily integrate with Azure Cosmos DB by using DocumentDB APIs.</span></span>

<span data-ttu-id="ca3c9-112">В этой статье демонстрируется создание DB Cosmos Azure с помощью hello портал Azure, а затем с помощью hello **Spring Initializr** toocreate приложении пользовательских java и затем добавить hello Spring загрузки начального функциональность tooyour пользовательские данные toostore приложения и получение данных из базы данных Cosmos Azure с помощью DocumentDB API hello.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-112">This article demonstrates creating an Azure Cosmos DB using hello Azure portal, then using hello **Spring Initializr** toocreate a custom java application, and then add hello Spring Boot Starter functionality tooyour custom application toostore data in and retrieve data from your Azure Cosmos DB by using hello DocumentDB API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca3c9-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ca3c9-113">Prerequisites</span></span>

<span data-ttu-id="ca3c9-114">в порядке toofollow hello действия, описанные в этой статье требуются следующие необходимые условия Hello:</span><span class="sxs-lookup"><span data-stu-id="ca3c9-114">hello following prerequisites are required in order toofollow hello steps in this article:</span></span>

* <span data-ttu-id="ca3c9-115">Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].</span><span class="sxs-lookup"><span data-stu-id="ca3c9-115">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="ca3c9-116">[Пакет разработчиков Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) версии 1.7 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-116">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="ca3c9-117">[Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-117">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-hello-azure-portal"></a><span data-ttu-id="ca3c9-118">Создайте Azure Cosmos DB с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="ca3c9-118">Create an Azure Cosmos DB by using hello Azure portal</span></span>

1. <span data-ttu-id="ca3c9-119">Обзор toohello Azure портала в <https://portal.azure.com/> и нажмите кнопку **+ создать**.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-119">Browse toohello Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Портал Azure][AZ01]

1. <span data-ttu-id="ca3c9-121">Щелкните **Базы данных** и **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-121">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Портал Azure][AZ02]

1. <span data-ttu-id="ca3c9-123">На hello **Azure Cosmos DB** введите hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="ca3c9-123">On hello **Azure Cosmos DB** page, enter hello following information:</span></span>

   * <span data-ttu-id="ca3c9-124">Введите уникальный **идентификатор**, который будет использоваться как hello URI для базы данных.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-124">Enter a unique **ID**, which you will use as hello URI for your database.</span></span> <span data-ttu-id="ca3c9-125">например *wingtiptoysdata.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-125">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="ca3c9-126">Выберите **SQL (DB документа)** для hello API.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-126">Choose **SQL (Document DB)** for hello API.</span></span>
   * <span data-ttu-id="ca3c9-127">Выберите hello **подписки** требуется toouse для базы данных.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-127">Choose hello **Subscription** you want toouse for your database.</span></span>
   * <span data-ttu-id="ca3c9-128">Укажите ли toocreate новый **группы ресурсов** для базы данных, или выберите существующую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-128">Specify whether toocreate a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="ca3c9-129">Укажите hello **расположение** для базы данных.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-129">Specify hello **Location** for your database.</span></span>
   
   <span data-ttu-id="ca3c9-130">При указании этих параметров щелкните **создать** toocreate базы данных.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-130">When you have specified these options, click **Create** toocreate your database.</span></span>

   ![Портал Azure][AZ03]

1. <span data-ttu-id="ca3c9-132">При создании базы данных она присутствует в Azure **мониторинга**, а также в разделе hello **все ресурсы** и **Azure Cosmos DB** страниц.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-132">When your database has been created, it is listed on your Azure **Dashboard**, as well as under hello **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="ca3c9-133">Можно щелкнуть базу данных на любой из этих расположений tooopen hello страница «свойства» для кэша.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-133">You can click on your database on any of those locations tooopen hello properties page for your cache.</span></span>

   ![Портал Azure][AZ04]

1. <span data-ttu-id="ca3c9-135">Когда откроется страница свойств hello для базы данных, нажмите кнопку **ключи доступа** и скопируйте ключи URI и доступа для базы данных; эти значения будут использоваться в приложении Spring загрузки.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-135">When hello properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Портал Azure][AZ05]

## <a name="create-a-simple-spring-boot-application-with-hello-spring-initializr"></a><span data-ttu-id="ca3c9-137">Создание простого приложения загрузки Spring с hello Initializr пружины</span><span class="sxs-lookup"><span data-stu-id="ca3c9-137">Create a simple Spring Boot application with hello Spring Initializr</span></span>

1. <span data-ttu-id="ca3c9-138">Обзор слишком<https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-138">Browse too<https://start.spring.io/>.</span></span>

1. <span data-ttu-id="ca3c9-139">Укажите, требуется toogenerate **Maven** проекта с **Java**, введите hello **группы** и **артефакта** имена для вашего приложения, и Нажмите кнопку hello слишком**создания проекта**.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-139">Specify that you want toogenerate a **Maven** project with **Java**, enter hello **Group** and **Artifact** names for your application, and then click hello button too**Generate Project**.</span></span>

   ![Основные параметры Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="ca3c9-141">Hello Spring Initializr использует hello **группы** и **артефакта** имя пакета hello toocreate имена, например: *com.example.wintiptoys*.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-141">hello Spring Initializr uses hello **Group** and **Artifact** names toocreate hello package name; for example: *com.example.wintiptoys*.</span></span>
   >

1. <span data-ttu-id="ca3c9-142">При появлении соответствующего запроса загрузите hello путь tooa проекта на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-142">When prompted, download hello project tooa path on your local computer.</span></span>

   ![Скачивание пользовательского проекта Spring Boot][SI02]

1. <span data-ttu-id="ca3c9-144">После извлечения файлов hello в локальной системе простого приложения Spring загрузки будет готова для редактирования.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-144">After you have extracted hello files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Пользовательские файлы проекта Spring Boot][SI03]

## <a name="configure-your-spring-boot-app-toouse-hello-azure-spring-boot-starter"></a><span data-ttu-id="ca3c9-146">Настройка приложения hello toouse начальный загрузки Spring Azure вашей Spring загрузки</span><span class="sxs-lookup"><span data-stu-id="ca3c9-146">Configure your Spring Boot app toouse hello Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="ca3c9-147">Найдите hello *pom.xml* файл в каталоге hello приложения; например:</span><span class="sxs-lookup"><span data-stu-id="ca3c9-147">Locate hello *pom.xml* file in hello directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\pom.xml`

   <span data-ttu-id="ca3c9-148">-или-</span><span class="sxs-lookup"><span data-stu-id="ca3c9-148">-or-</span></span>

   `/users/example/home/wingtiptoys/pom.xml`

   ![Найдите файл pom.xml hello][PM01]

1. <span data-ttu-id="ca3c9-150">Откройте hello *pom.xml* файл в текстовом редакторе и добавить следующие строки toolist из hello `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="ca3c9-150">Open hello *pom.xml* file in a text editor, and add hello following lines toolist of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Изменение файла pom.xml hello][PM02]

1. <span data-ttu-id="ca3c9-152">Сохраните и закройте hello *pom.xml* файла.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-152">Save and close hello *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-toouse-your-azure-cosmos-db"></a><span data-ttu-id="ca3c9-153">Настройка вашего toouse приложения загрузки Spring Cosmos базы данных Azure</span><span class="sxs-lookup"><span data-stu-id="ca3c9-153">Configure your Spring Boot app toouse your Azure Cosmos DB</span></span>

1. <span data-ttu-id="ca3c9-154">Найдите hello *application.properties* файла в hello *ресурсов* каталог приложения, например:</span><span class="sxs-lookup"><span data-stu-id="ca3c9-154">Locate hello *application.properties* file in hello *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   <span data-ttu-id="ca3c9-155">-или-</span><span class="sxs-lookup"><span data-stu-id="ca3c9-155">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Найдите файл application.properties hello][RE01]

1. <span data-ttu-id="ca3c9-157">Откройте hello *application.properties* в текстовом редакторе и добавьте следующие строки toohello файл hello и замените значения образец hello hello соответствующих свойств для базы данных:</span><span class="sxs-lookup"><span data-stu-id="ca3c9-157">Open hello *application.properties* file in a text editor, and add hello following lines toohello file, and replace hello sample values with hello appropriate properties for your database:</span></span>

   ```yaml
   # Specify hello DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify hello access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify hello name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Изменение файла application.properties hello][RE02]

1. <span data-ttu-id="ca3c9-159">Сохраните и закройте hello *application.properties* файла.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-159">Save and close hello *application.properties* file.</span></span>

## <a name="add-sample-code-tooimplement-basic-database-functionality"></a><span data-ttu-id="ca3c9-160">Добавить функциональность баз данных basic tooimplement образец кода</span><span class="sxs-lookup"><span data-stu-id="ca3c9-160">Add sample code tooimplement basic database functionality</span></span>

<span data-ttu-id="ca3c9-161">В этом разделе создайте два класса Java для хранения пользовательских данных и затем изменить ваш toocreate класс основного приложения экземпляра класса пользователя hello и сохранить его tooyour базы данных.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-161">In this section you create two Java classes for storing user data, and then you modify your main application class toocreate an instance of hello user class and save it tooyour database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="ca3c9-162">Определение базового класса для хранения пользовательских данных</span><span class="sxs-lookup"><span data-stu-id="ca3c9-162">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="ca3c9-163">Создайте новый файл с именем *User.java* в hello же каталоге, что файл основного приложения Java.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-163">Create a new file named *User.java* in hello same directory as your main application Java file.</span></span>

1. <span data-ttu-id="ca3c9-164">Откройте hello *User.java* файл в текстовом редакторе и добавьте hello следующие строки файла toodefine toohello класс универсального пользователя, хранит и извлечение значений в базе данных:</span><span class="sxs-lookup"><span data-stu-id="ca3c9-164">Open hello *User.java* file in a text editor, and add hello following lines toohello file toodefine a generic user class that stores and retrieve values in your database:</span></span>

   ```java
   package com.example.wingtiptoys;

   public class User {
      private String id;
      private String firstName;
      private String lastName;
 
      public User(String id, String firstName, String lastName) {
         this.id = id;
         this.firstName = firstName;
         this.lastName = lastName;
      }
   
      public String getId() {
         return this.id;
      }

      public void setId(String id) {
         this.id = id;
      }

      public String getFirstName() {
         return firstName;
      }

      public void setFirstName(String firstName) {
         this.firstName = firstName;
      }

      public String getLastName() {
         return lastName;
      }

      public void setLastName(String lastName) {
         this.lastName = lastName;
      }

      @Override
      public String toString() {
         return String.format("User: %s %s", firstName, lastName);
      }
   }
   ```

1. <span data-ttu-id="ca3c9-165">Сохраните и закройте hello *User.java* файла.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-165">Save and close hello *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="ca3c9-166">Определение интерфейса хранилища данных</span><span class="sxs-lookup"><span data-stu-id="ca3c9-166">Define a data repository interface</span></span>

1. <span data-ttu-id="ca3c9-167">Создайте новый файл с именем *UserRepository.java* в hello же каталоге, что файл основного приложения Java.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-167">Create a new file named *UserRepository.java* in hello same directory as your main application Java file.</span></span>

1. <span data-ttu-id="ca3c9-168">Откройте hello *UserRepository.java* файл в текстовом редакторе и добавьте hello следующие строки файла toodefine toohello репозитория пользовательский интерфейс, который расширяет интерфейс репозитория DocumentDB по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="ca3c9-168">Open hello *UserRepository.java* file in a text editor, and add hello following lines toohello file toodefine a user repository interface that extends hello default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. <span data-ttu-id="ca3c9-169">Сохраните и закройте hello *UserRepository.java* файла.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-169">Save and close hello *UserRepository.java* file.</span></span>

### <a name="modify-hello-main-application-class"></a><span data-ttu-id="ca3c9-170">Измените класс основного приложения hello</span><span class="sxs-lookup"><span data-stu-id="ca3c9-170">Modify hello main application class</span></span>

1. <span data-ttu-id="ca3c9-171">Найдите файл Java hello основного приложения в каталоге пакета hello приложения; Например:</span><span class="sxs-lookup"><span data-stu-id="ca3c9-171">Locate hello main application Java file in hello package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   <span data-ttu-id="ca3c9-172">-или-</span><span class="sxs-lookup"><span data-stu-id="ca3c9-172">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Найдите файл Java приложения hello][JV01]

1. <span data-ttu-id="ca3c9-174">Откройте файл Java hello основного приложения в текстовом редакторе и добавьте следующие строки toohello файл hello:</span><span class="sxs-lookup"><span data-stu-id="ca3c9-174">Open hello main application Java file in a text editor, and add hello following lines toohello file:</span></span>

   ```java
   package com.example.wingtiptoys;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class WingtiptoysApplication implements CommandLineRunner {

      @Autowired
      private UserRepository repository;
    
      public static void main(String[] args) {
         SpringApplication.run(WingtiptoysApplication.class, args);
      }

      public void run(String... var1) throws Exception {
         final User testUser = new User("testId", "testFirstName", "testLastName");

         repository.deleteAll();
         repository.save(testUser);

         final User result = repository.findOne(testUser.getId());

         System.out.printf("\n\n%s\n\n",result.toString());
      }
   }
   ```

1. <span data-ttu-id="ca3c9-175">Сохраните и закройте файл Java hello основного приложения.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-175">Save and close hello main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="ca3c9-176">Создание и тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="ca3c9-176">Build and test your app</span></span>

1. <span data-ttu-id="ca3c9-177">Откройте командную строку и измените папку каталога toohello где вашей *pom.xml* расположен файл, например:</span><span class="sxs-lookup"><span data-stu-id="ca3c9-177">Open a command prompt and change directory toohello folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoys`

   <span data-ttu-id="ca3c9-178">-или-</span><span class="sxs-lookup"><span data-stu-id="ca3c9-178">-or-</span></span>

   `cd /users/example/home/wingtiptoys`

1. <span data-ttu-id="ca3c9-179">Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ca3c9-179">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. <span data-ttu-id="ca3c9-180">Отображения нескольких сообщений среды выполнения в приложении, и вы увидите сообщение hello `User: testFirstName testLastName` отображаются tooindicate, что значения были успешно хранятся и извлечь из базы данных.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-180">Your application will display several runtime messages, and you should see hello message `User: testFirstName testLastName` displayed tooindicate that values have been successfully stored and retrieved from your database.</span></span>

   ![Успешно вывода приложения hello][JV02]

1. <span data-ttu-id="ca3c9-182">Необязательно: Можно использовать hello Azure портала tooview hello содержимое базы данных Azure Cosmos со страницы приветствия свойства для базы данных, щелкнув **обозреватель документов**и затем выбрав и элемента из hello отображается список tooview hello содержимое.</span><span class="sxs-lookup"><span data-stu-id="ca3c9-182">OPTIONAL: You can use hello Azure portal tooview hello contents of your Azure Cosmos DB from hello properties page for your database by clicking  **Document Explorer**, and then selecting and item from hello displayed list tooview hello contents.</span></span>

   ![С помощью обозревателя документов tooview hello данных][JV03]

## <a name="next-steps"></a><span data-ttu-id="ca3c9-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ca3c9-184">Next steps</span></span>

<span data-ttu-id="ca3c9-185">Дополнительные сведения об использовании Azure Cosmos DB и Java см. следующие статьи hello:</span><span class="sxs-lookup"><span data-stu-id="ca3c9-185">For more information about using Azure Cosmos DB and Java, see hello following articles:</span></span>

* <span data-ttu-id="ca3c9-186">[Документация по Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="ca3c9-186">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="ca3c9-187">[Azure Cosmos DB: Сборка приложения DocumentDB API с помощью Java и hello портал Azure][Build a DocumentDB API app with Java]</span><span class="sxs-lookup"><span data-stu-id="ca3c9-187">[Azure Cosmos DB: Build a DocumentDB API app with Java and hello Azure portal][Build a DocumentDB API app with Java]</span></span>

<span data-ttu-id="ca3c9-188">Дополнительные сведения об использовании приложений Spring загрузки в Azure см. следующие статьи hello:</span><span class="sxs-lookup"><span data-stu-id="ca3c9-188">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* <span data-ttu-id="ca3c9-189">[Spring Boot DocumenDB Starter for Azure](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample) (Начальное приложение Spring Boot DocumenDB для Azure)</span><span class="sxs-lookup"><span data-stu-id="ca3c9-189">[Spring Boot DocumenDB Starter for Azure](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)</span></span>

* [<span data-ttu-id="ca3c9-190">Развертывание приложения загрузки Spring toohello службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="ca3c9-190">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="ca3c9-191">Запуск приложения загрузки Spring в кластере Kubernetes в hello контейнера службы Azure</span><span class="sxs-lookup"><span data-stu-id="ca3c9-191">Running a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="ca3c9-192">Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure] и hello [Java средств для Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="ca3c9-192">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Документация по Azure Cosmos DB]: /azure/cosmos-db/
[центра разработчиков Java Azure]: https://azure.microsoft.com/develop/java/
[Build a DocumentDB API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-documentdb-java
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Java средств для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[загрузки Spring]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ01.png
[AZ02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ02.png
[AZ03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ03.png
[AZ04]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ04.png
[AZ05]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ05.png

[SI01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI01.png
[SI02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI02.png
[SI03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI03.png

[RE01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/RE01.png
[RE02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/RE02.png

[PM01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/PM01.png
[PM02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/PM02.png

[JV01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV01.png
[JV02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV02.png
[JV03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV03.png
