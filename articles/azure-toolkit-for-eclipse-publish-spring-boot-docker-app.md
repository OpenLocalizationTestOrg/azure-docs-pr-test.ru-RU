---
title: "Здравствуйте, aaaPublish Spring загрузки приложения в качестве контейнера Docker с помощью средств Azure для Eclipse | Документы Microsoft"
description: "Узнайте, как toopublish tooMicrosoft приложения web Azure в качестве контейнера Docker с помощью hello средств Azure для Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: 29390c49c339a1ebb87cb3951b21cea01c0da15f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a>Опубликовать приложение Spring загрузки как контейнер Docker с помощью hello набора средств Azure для Eclipse

Hello [Spring Framework] — это решение открытым исходным кодом, разработчики Java могут создавать корпоративные приложения. Один из проектов более популярных hello, построенных на основе этой платформы является [загрузки Spring], который предоставляет упрощенный подход для создания автономных приложений Java.

[Docker] — это решение открытым исходным кодом, которое помогает разработчикам автоматизировать развертывание hello, масштабирование и управление их приложений, выполняющихся в контейнерах.

Этот учебник поможет выполнить действия toodeploy hello приложение Spring загрузки как tooMicrosoft контейнера Docker Azure с помощью hello набора средств Azure для Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repository"></a>Клонирование репозитория Docker Spring загрузки по умолчанию hello

### <a name="import-hello-public-repository"></a>Общедоступный репозиторий hello импорта

Hello следующие шаги описывают клонирования hello Docker загрузки Spring репозитория tooyour локального компьютера с помощью IntelliJ. Если toouse командной строки, см. [развернуть приложение в Linux в службе контейнера Azure Spring загрузки][Deploy Spring Boot on Linux in ACS].

1. Откройте Eclipse.

1. Последовательно выберите **Файл** > **Импортировать**.

   ![Меню "File" (Файл) > "Import" (Импортировать)][CL01]

1. Здравствуйте, когда **импорта** откроется диалоговое окно:

   а. Разверните элемент **Git**.

   b. Выберите **Projects from Git** (Проекты из Git).
   
   c. Щелкните **Далее**.

   ![Диалоговое окно "Import" (Импорт)][CL02]

1. На hello **Выбор источника репозитория** страницы:

   а. Выберите **Клонировать URI**.
   
   b. Щелкните **Далее**.

   ![Страница "Выбор источника репозитория"][CL03]

1. На hello **источника репозитории** страницы:

   а. В поле **URI** введите `https://github.com/spring-guides/gs-spring-boot-docker.git`. Этот шаг должен автоматически заполнять hello **узла** и **путь репозитория** поля с hello исправьте значения.
   
   b. репозиторий Hello Spring загрузки является открытым, поэтому не следует tooenter Git имя пользователя и пароль.
   
   c. Щелкните **Далее**.

   ![Страница "Исходный репозиторий Git"][CL04]

1. На hello **ветвь выбора** щелкните **Далее**.

   ![Страница "Выбор ветви"][CL05]

1. На hello **локальной целевой** страницы:

   а. Укажите локальную папку hello место вашего локального репозитория.
   
   b. Щелкните **Далее**.

   ![Страница "Локальное назначение"][CL06]

1. На hello **toouse мастер импорта проектов выберите** страницы:

   а. Выберите **Import as a general project** (Импортировать как универсальный проект).
   
   b. Щелкните **Далее**.

   ![Страница «Выбор toouse мастер импорта проектов»][CL07]

1. На hello **импорта проектов** страницы:

   а. Укажите имя проекта.
   
   b. Нажмите кнопку **Готово**

   ![Страница "Импорт проектов"][CL08]

1. При клонировании репозитория hello можно увидеть все файлы hello, перечисленные в Eclipse.

   ![Локальный репозиторий][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a>Создание проекта Maven из локального репозитория

репозиторий Hello Spring загрузки Docker содержит завершенный проект Maven, который будет использоваться для этого учебника. 

1. Последовательно выберите **Файл** > **Импортировать**.

   ![Команда «Импорт» в меню файл hello][CL01]

1. Здравствуйте, когда **импорта** откроется диалоговое окно:

   а. Разверните элемент **Maven**.
   
   b. Выберите **Existing Maven Projects** (Существующие проекты Maven).
   
   c. Щелкните **Далее**.

   ![Диалоговое окно "Import" (Импорт)][MV01]

1. На hello **проекты Maven** страницы:

   а. Для **корневой каталог**, укажите hello **завершения** папки в ваш локальный репозиторий.
   
   b. Разверните hello **Дополнительно** раздела и введите имя файла для **шаблона имени**.
   
   c. Поле выберите hello hello **pom.xml** файл в проекте hello.
   
   d. Нажмите кнопку **Готово**

   ![Страница "Проекты Maven"][MV02]

1. При открытии проекта Maven hello появится второй проект, перечисленные в Eclipse.

   ![Локальный проект Maven][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a>Построение приложения Spring Boot с помощью Maven

1. Выберите проект Maven hello в hello обозревателя проектов Eclipse.

1. Последовательно выберите **Запуск** > **Запуск от имени** > **Сборка Maven**.

   ![Команды toorun как сборки Maven][BU01]

1. Если приложение успешно создано, hello окна консоли отображается состояние hello.

   ![Успешное выполнение сборки Maven][BU02]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Публикация вашего tooAzure web app с помощью контейнера Docker

1. Выберите проект Maven hello в hello обозревателя проектов Eclipse.

1. Нажмите кнопку hello Azure **публикации** меню, а затем нажмите **опубликовать как контейнер Docker**.

   ![Команда публикации в виде контейнера Docker][PU01]

1. Здравствуйте, когда **развертывание контейнера Docker в Azure** откроется диалоговое окно:

   а. Введите пользовательское имя образа Docker.
   
   b. Для **toodeploy артефакта**, укажите путь toohello hello **gs spring загрузки docker-0.1.0.jar** только что созданного файла.

   ![Задание параметров Docker][PU02]

   Отобразятся все существующие узлы Docker. 

1. Если выбрать существующий узел tooan toodeploy toostep 5 можно пропустить. В противном случае используйте следующие шаги toocreate узел hello:

   а. Щелкните **Добавить**.

      ![Добавление нового узла Docker][PU03]

   b. Здравствуйте, когда **создать узел Docker** откроется диалоговое окно, можно выбрать значения по умолчанию hello tooaccept или можно задать пользовательские параметры для нового узла Docker. (Подробное описание hello различные параметры в разделе [публикации веб-приложения как контейнер Docker с помощью hello Azure Toolkit для IntelliJ][Publish Container with Azure Toolkit].) Нажмите кнопку **Далее** после указания toouse какие параметры.

      ![Задание параметров узла Docker][PU04]

   c. Можно выбрать существующие учетные данные входа toouse хранилище ключей Azure или для выбора tooenter новые учетные данные входа Docker. После задания параметров нажмите кнопку **Finish** (Готово).

      ![Задание учетных данных узла Docker][PU05]

1. Выберите узел Docker и нажмите кнопку **Next** (Далее).

   ![Выберите toouse узла Docker][PU06]

1. На последней странице hello hello **развертывание контейнера Docker в Azure** диалоговом окне укажите hello следующие параметры:

   а. Вы можете toospecify пользовательское имя для hello контейнер, который будет содержать контейнер Docker, либо может принимать по умолчанию hello.

   b. Введите hello TCP-портов для узла docker с помощью hello, используя синтаксис: *[внешний порт]*:*[внутренний порт]*. Например **80:8080** указывает внешний порт 80 и hello по умолчанию внутренние загрузки Spring порт 8080.
   
      После настройки вашей внутренний порт (например, путем редактирования файла application.yml hello) для правильного маршрутизации toooccur hello в Azure необходимо номер порта toospecify hello.

   c. После настройки этих параметров щелкните **Finish** (Готово).

   ![Развертывание контейнера Docker в Azure][PU07]

1. После завершения публикации hello Azure Toolkit hello отображается журнал действий Azure **опубликовано** статуса hello.

   ![Успешно развернутый узел Docker][PU08]

## <a name="next-steps"></a>Дальнейшие действия

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[загрузки Spring]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
