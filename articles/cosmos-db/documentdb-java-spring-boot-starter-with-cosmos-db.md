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
# <a name="how-toouse-hello-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a>Как toouse hello Spring начальный загрузки с помощью Azure Cosmos DB DocumentDB API

## <a name="overview"></a>Обзор

Hello  **[Spring Framework]**  — это решение открытым исходным кодом, разработчики Java могут создавать корпоративные приложения. Один из проектов более популярных hello, построенных на основе этой платформы является [загрузки Spring], который предоставляет упрощенный подход для создания изолированного приложения Java. Разработчики toohelp начать работу с загрузкой Spring, несколько образцов Spring загрузки пакетов можно найти по адресу <https://github.com/spring-guides/>. В дополнение к этому toochoosing списке hello базового загрузочного Spring проекты, hello  **[Spring Initializr]**  помогает разработчикам Приступая к работе с созданием пользовательских приложений Spring загрузки.

Azure Cosmos DB является глобально распределенной базы данных службы, которая позволяет разработчикам toowork с данными, с помощью различных стандартных API, например DocumentDB, MongoDB, диаграммы и таблицы API-интерфейсы. Начальный загрузки Spring корпорации Майкрософт позволяет приложений Spring загрузки toouse разработчики, которые легко интегрируются с Azure Cosmos DB с помощью интерфейсов API DocumentDB.

В этой статье демонстрируется создание DB Cosmos Azure с помощью hello портал Azure, а затем с помощью hello **Spring Initializr** toocreate приложении пользовательских java и затем добавить hello Spring загрузки начального функциональность tooyour пользовательские данные toostore приложения и получение данных из базы данных Cosmos Azure с помощью DocumentDB API hello.

## <a name="prerequisites"></a>Предварительные требования

в порядке toofollow hello действия, описанные в этой статье требуются следующие необходимые условия Hello:

* Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].

* [Пакет разработчиков Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/) версии 1.7 или более поздней.

* [Apache Maven](http://maven.apache.org/) версии 3.0 или более поздней.

## <a name="create-an-azure-cosmos-db-by-using-hello-azure-portal"></a>Создайте Azure Cosmos DB с помощью портала Azure hello

1. Обзор toohello Azure портала в <https://portal.azure.com/> и нажмите кнопку **+ создать**.

   ![Портал Azure][AZ01]

1. Щелкните **Базы данных** и **Azure Cosmos DB**.

   ![Портал Azure][AZ02]

1. На hello **Azure Cosmos DB** введите hello следующую информацию:

   * Введите уникальный **идентификатор**, который будет использоваться как hello URI для базы данных. например *wingtiptoysdata.documents.azure.com*.
   * Выберите **SQL (DB документа)** для hello API.
   * Выберите hello **подписки** требуется toouse для базы данных.
   * Укажите ли toocreate новый **группы ресурсов** для базы данных, или выберите существующую группу ресурсов.
   * Укажите hello **расположение** для базы данных.
   
   При указании этих параметров щелкните **создать** toocreate базы данных.

   ![Портал Azure][AZ03]

1. При создании базы данных она присутствует в Azure **мониторинга**, а также в разделе hello **все ресурсы** и **Azure Cosmos DB** страниц. Можно щелкнуть базу данных на любой из этих расположений tooopen hello страница «свойства» для кэша.

   ![Портал Azure][AZ04]

1. Когда откроется страница свойств hello для базы данных, нажмите кнопку **ключи доступа** и скопируйте ключи URI и доступа для базы данных; эти значения будут использоваться в приложении Spring загрузки.

   ![Портал Azure][AZ05]

## <a name="create-a-simple-spring-boot-application-with-hello-spring-initializr"></a>Создание простого приложения загрузки Spring с hello Initializr пружины

1. Обзор слишком<https://start.spring.io/>.

1. Укажите, требуется toogenerate **Maven** проекта с **Java**, введите hello **группы** и **артефакта** имена для вашего приложения, и Нажмите кнопку hello слишком**создания проекта**.

   ![Основные параметры Spring Initializr][SI01]

   > [!NOTE]
   >
   > Hello Spring Initializr использует hello **группы** и **артефакта** имя пакета hello toocreate имена, например: *com.example.wintiptoys*.
   >

1. При появлении соответствующего запроса загрузите hello путь tooa проекта на локальном компьютере.

   ![Скачивание пользовательского проекта Spring Boot][SI02]

1. После извлечения файлов hello в локальной системе простого приложения Spring загрузки будет готова для редактирования.

   ![Пользовательские файлы проекта Spring Boot][SI03]

## <a name="configure-your-spring-boot-app-toouse-hello-azure-spring-boot-starter"></a>Настройка приложения hello toouse начальный загрузки Spring Azure вашей Spring загрузки

1. Найдите hello *pom.xml* файл в каталоге hello приложения; например:

   `C:\SpringBoot\wingtiptoys\pom.xml`

   -или-

   `/users/example/home/wingtiptoys/pom.xml`

   ![Найдите файл pom.xml hello][PM01]

1. Откройте hello *pom.xml* файл в текстовом редакторе и добавить следующие строки toolist из hello `<dependencies>`:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Изменение файла pom.xml hello][PM02]

1. Сохраните и закройте hello *pom.xml* файла.

## <a name="configure-your-spring-boot-app-toouse-your-azure-cosmos-db"></a>Настройка вашего toouse приложения загрузки Spring Cosmos базы данных Azure

1. Найдите hello *application.properties* файла в hello *ресурсов* каталог приложения, например:

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   -или-

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Найдите файл application.properties hello][RE01]

1. Откройте hello *application.properties* в текстовом редакторе и добавьте следующие строки toohello файл hello и замените значения образец hello hello соответствующих свойств для базы данных:

   ```yaml
   # Specify hello DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify hello access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify hello name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Изменение файла application.properties hello][RE02]

1. Сохраните и закройте hello *application.properties* файла.

## <a name="add-sample-code-tooimplement-basic-database-functionality"></a>Добавить функциональность баз данных basic tooimplement образец кода

В этом разделе создайте два класса Java для хранения пользовательских данных и затем изменить ваш toocreate класс основного приложения экземпляра класса пользователя hello и сохранить его tooyour базы данных.

### <a name="define-a-basic-class-for-storing-user-data"></a>Определение базового класса для хранения пользовательских данных

1. Создайте новый файл с именем *User.java* в hello же каталоге, что файл основного приложения Java.

1. Откройте hello *User.java* файл в текстовом редакторе и добавьте hello следующие строки файла toodefine toohello класс универсального пользователя, хранит и извлечение значений в базе данных:

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

1. Сохраните и закройте hello *User.java* файла.

### <a name="define-a-data-repository-interface"></a>Определение интерфейса хранилища данных

1. Создайте новый файл с именем *UserRepository.java* в hello же каталоге, что файл основного приложения Java.

1. Откройте hello *UserRepository.java* файл в текстовом редакторе и добавьте hello следующие строки файла toodefine toohello репозитория пользовательский интерфейс, который расширяет интерфейс репозитория DocumentDB по умолчанию hello:

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. Сохраните и закройте hello *UserRepository.java* файла.

### <a name="modify-hello-main-application-class"></a>Измените класс основного приложения hello

1. Найдите файл Java hello основного приложения в каталоге пакета hello приложения; Например:

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   -или-

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Найдите файл Java приложения hello][JV01]

1. Откройте файл Java hello основного приложения в текстовом редакторе и добавьте следующие строки toohello файл hello:

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

1. Сохраните и закройте файл Java hello основного приложения.

## <a name="build-and-test-your-app"></a>Создание и тестирование приложения

1. Откройте командную строку и измените папку каталога toohello где вашей *pom.xml* расположен файл, например:

   `cd C:\SpringBoot\wingtiptoys`

   -или-

   `cd /users/example/home/wingtiptoys`

1. Создайте приложение Spring Boot с помощью Maven и запустите его, например, следующим образом:

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. Отображения нескольких сообщений среды выполнения в приложении, и вы увидите сообщение hello `User: testFirstName testLastName` отображаются tooindicate, что значения были успешно хранятся и извлечь из базы данных.

   ![Успешно вывода приложения hello][JV02]

1. Необязательно: Можно использовать hello Azure портала tooview hello содержимое базы данных Azure Cosmos со страницы приветствия свойства для базы данных, щелкнув **обозреватель документов**и затем выбрав и элемента из hello отображается список tooview hello содержимое.

   ![С помощью обозревателя документов tooview hello данных][JV03]

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения об использовании Azure Cosmos DB и Java см. следующие статьи hello:

* [Документация по Azure Cosmos DB]

* [Azure Cosmos DB: Сборка приложения DocumentDB API с помощью Java и hello портал Azure][Build a DocumentDB API app with Java]

Дополнительные сведения об использовании приложений Spring загрузки в Azure см. следующие статьи hello:

* [Spring Boot DocumenDB Starter for Azure](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample) (Начальное приложение Spring Boot DocumenDB для Azure)

* [Развертывание приложения загрузки Spring toohello службе приложений Azure](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [Запуск приложения загрузки Spring в кластере Kubernetes в hello контейнера службы Azure](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure] и hello [Java средств для Visual Studio Team Services].

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
