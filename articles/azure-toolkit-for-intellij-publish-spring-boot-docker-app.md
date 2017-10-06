---
title: "aaaPublish Spring загрузки приложения в качестве контейнера Docker с помощью hello Azure Toolkit для IntelliJ | Документы Microsoft"
description: "Узнайте, как toopublish tooMicrosoft приложения web Azure в качестве контейнера Docker с помощью hello Azure Toolkit для IntelliJ."
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
ms.openlocfilehash: 8964cb33fd8f61a39f091633ae9074d9658232fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a>Опубликовать приложение Spring загрузки как контейнер Docker с помощью hello Azure Toolkit для IntelliJ

Hello [Spring Framework] — это решение открытым исходным кодом, разработчики Java могут создавать корпоративные приложения. Один из проектов более популярных hello, построенных на основе этой платформы является [загрузки Spring], который предоставляет упрощенный подход для создания автономных приложений Java.

[Docker] — это решение открытым исходным кодом, которое помогает разработчикам автоматизировать развертывание hello, масштабирование и управление их приложений, выполняющихся в контейнерах.

Этот учебник поможет выполнить toodeploy действия hello приложение Spring загрузки как tooMicrosoft контейнера Docker Azure с помощью hello Azure Toolkit для IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repo"></a>Клонировать репозиторий Docker Spring загрузки по умолчанию hello

Hello следующие шаги описывают клонирования репозитория hello Spring загрузки Docker с помощью IntelliJ. Если toouse командной строки, см. [развернуть приложение в Linux в службе контейнера Azure Spring загрузки][Deploy Spring Boot on Linux in ACS].

1. Откройте IntelliJ.

1. На экране приветствия hello выберите hello **GitHub** параметр в hello **извлечь из системы управления версиями** списка.

   ![Параметр GitHub для управления версиями][CL01]

1. Введите свои учетные данные, если запрос toolog в.

   * Если вы используете toolog имя пользователя и пароль в tooGitHub:

      ![Диалоговое окно для ввода имени пользователя и пароля для входа в GitHub][CL02a]

   * При использовании маркера toolog в tooGitHub:

      ![Диалоговое окно для ввода токена GitHub][CL02b]

1. Введите **https://github.com/spring-guides/gs-spring-boot-docker.git** URL-адрес репозитория hello, укажите локальный путь и сведения о папке и нажмите кнопку **клон**.

   ![Диалоговое окно "Clone Repository" (Клонирование репозитория)][CL03]

1. При запросе toocreate IntelliJ проекта, выберите **нет**.

   ![Отклонение toocreate проекте IntelliJ][CL04]

1. На начальной странице приветствия нажмите кнопку **Импорт проекта**.

   ![Пункт "Импорт проекта"][CL05]

1. Найти путь hello, где клонирования репозитория загрузки Spring hello, выберите hello **завершения** папку в корневой hello, а затем щелкните **ОК**.

   ![Выбор папки для импорта][CL06]

1. При появлении запроса выберите **Создать проект из существующих источников**.

   ![Параметр toocreate проекта из существующих источников][CL07]

1. Укажите имя проекта или примите значение по умолчанию hello, проверьте hello правильный путь toohello **завершения** папки, а затем щелкните **Далее**.

   ![Укажите имя проекта hello][CL08]

1. Настройте все каталоги для импорта и нажмите кнопку **Далее**.

   ![Выбор каталогов][CL09]

1. Просмотрите tooimport hello библиотеки и нажмите кнопку **Далее**.

   ![Просмотр библиотек проекта][CL10]

1. Просмотрите структуру модуля hello и нажмите кнопку **Далее**.

   ![Просмотр структуры модулей][CL11]

1. Укажите свой JDK и нажмите кнопку **Далее**.

   ![Указание JDK][CL12]

1. Нажмите кнопку **Готово**

   ![Кнопка "Готово"][CL13]

IntelliJ импортирует приложение hello Spring загрузки как проект и отображает hello структуры после завершения импорта hello.

![Приложение Spring Boot в IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a>Создание приложения Spring Boot

### <a name="build-hello-app-by-using-hello-maven-pom"></a>Сборка приложения hello с помощью hello Maven POM

1. Если он еще не открыта, откройте окно инструментов Maven hello. Последовательно выберите **Вид** > **Окна инструментов** > **Проекты Maven**.

   ![Окна инструментов и команды проектов Maven][BU01]

1. Щелкните правой кнопкой мыши в окне инструментов Maven hello, **пакета** и выберите **выполнить сборки Maven**. (Если Maven проекта не отображается автоматически, нажмите кнопку hello **повторный импорт** значок на панели инструментов Maven hello.)

   ![Команда "Запуск сборки Maven"][BU02]

1. После успешного создания приложения Spring Boot IntelliJ отобразит сообщение **Сборка выполнена успешно**.

   ![Сообщение "Сборка выполнена успешно"][BU03]

### <a name="create-a-deployment-ready-artifact"></a>Создание готового к развертыванию артефакта

toopublish приложение Spring загрузки необходимо toocreate артефакта готовым к развертыванию. Используйте следующие шаги hello.

1. Откройте проект веб-приложения в IntelliJ.

1. В меню **File** (Файл) выберите **Project Structure** (Структура проекта).

   ![Команда "Project Structure" (Структура проекта)][ART01]

1. Щелкните зеленый плюс hello (**+**) символ tooadd артефакта, нажмите кнопку **JAR**и нажмите кнопку **пустой**.

   ![Добавление артефакта][ART02]

1. Имя вашего артефакта делая не tooadd hello расширение «.jar», а затем укажите hello целевую папку для вывода Maven приветствия.

   ![Указание свойств артефакта][ART03]

1. Создайте манифест для артефакта (необязательно).

   а. Нажмите кнопку **Create Manifest** (Создать манифест).

      ![Нажмите кнопку Создать манифест hello][ART04a]

   b. Выберите путь по умолчанию hello для hello артефакта и щелкните **ОК**.

      ![Указание пути к артефакту][ART04b]

   c. Нажмите кнопку с многоточием hello (**...** ) toolocate hello основного класса.

      ![Поиск основного (main) класса][ART04c]

   d. Выберите основной класс и нажмите кнопку **ОК**.

      ![Указание основного (main) класса][ART04d]

1. Нажмите кнопку **ОК**.

   ![Закройте диалоговое окно структуры проекта hello][ART05]

> [!NOTE]
> Дополнительные сведения о создании артефактов в IntelliJ см. в разделе [Настройка артефакты] на веб-сайте JetBrains hello.
>

### <a name="build-hello-artifact-for-deployment"></a>Hello артефакт для развертывания сборки

1. Нажмите кнопку **Build** (Сборка), а затем кнопку **Artifacts** (Артефакты).

   ![Команда "Build Artifacts" (Создать артефакты)][BU04]

1. Здравствуйте, когда **артефактов сборки** контекстное меню, нажмите кнопку **сборки**.

   ![Контекстное меню "Build Artifacts" (Создание артефакта)][BU05]

В окне инструментов проекта hello IntelliJ отображать артефакта hello завершения Spring загрузки приложения.

   ![Созданный артефакт][BU06]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Публикация вашего tooAzure web app с помощью контейнера Docker

1. Если вы не вошли в tooyour учетная запись Azure, следуйте указаниям hello [входа в инструкции для hello Azure Toolkit для IntelliJ][Azure Sign In for IntelliJ].

1. В окне инструментов обозревателя проектов hello, щелкните правой кнопкой мыши проект hello и выберите **Azure** > **опубликовать как контейнер Docker**.

   ![Команда публикации в виде контейнера Docker][PU01]

1. Здравствуйте, когда **развертывания контейнера Docker в Azure** откроется диалоговое окно, отображаются все существующие узлы Docker. Если выбрать существующий узел tooan toodeploy toostep 4 можно пропустить. В противном случае используйте следующие шаги toocreate узел hello:

   а. Щелкните зеленый плюс hello (**+**) символов.

      ![Добавление нового узла Docker][PU02]

   b. Здравствуйте, когда **создать узел Docker** откроется диалоговое окно, можно выбрать значения по умолчанию hello tooaccept или можно задать пользовательские параметры для нового узла Docker. (Подробное описание hello различные параметры в разделе [публикации веб-приложения как контейнер Docker с помощью hello Azure Toolkit для IntelliJ][Publish Container with Azure Toolkit].) Нажмите кнопку **Далее** после указания toouse какие параметры.

      ![Задание параметров узла Docker][PU03a]

   c. Можно выбрать существующие учетные данные входа toouse хранилище ключей Azure или для выбора tooenter новые учетные данные входа Docker. После задания параметров нажмите кнопку **Finish** (Готово).

      ![Задание учетных данных узла Docker][PU03b]

1. Выберите узел Docker и нажмите кнопку **Next** (Далее).

   ![Выберите узел toouse hello Docker][PU04]

1. На последней странице hello hello **развертывания контейнера Docker в Azure** диалоговом окне укажите hello следующие параметры:

   а. Вы можете toospecify пользовательское имя для hello контейнер, который будет содержать контейнер Docker, либо может принимать по умолчанию hello.

   b. Введите hello TCP-портов для узла docker с помощью hello, используя синтаксис: *[внешний порт]*:*[внутренний порт]*. Например **80:8080** указывает внешний порт 80 и hello по умолчанию внутренние загрузки Spring порт 8080.
   
      После настройки вашей внутренний порт (например, путем редактирования файла application.yml hello) для правильного маршрутизации toooccur hello в Azure необходимо номер порта toospecify hello.

   c. После настройки этих параметров щелкните **Finish** (Готово).

   ![Развертывание контейнера Docker в Azure][PU05]

1. После завершения публикации hello Azure Toolkit hello отображается журнал действий Azure **опубликовано** статуса hello.

   ![Успешно развернутый узел Docker][PU06]

## <a name="next-steps"></a>Дальнейшие действия

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

. в разделе toolearn о дополнительных методов для создания загрузочного Spring приложений с помощью IntelliJ, [Создание проектов Spring загрузки](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) на веб-сайте JetBrains hello.

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Настройка артефакты]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[загрузки Spring]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
