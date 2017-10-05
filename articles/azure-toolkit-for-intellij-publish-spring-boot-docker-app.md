---
title: "Публикация приложения Spring Boot в виде контейнера Docker с помощью набора средств Azure для IntelliJ | Документы Майкрософт"
description: "Вы можете узнать, как опубликовать веб-приложение в Microsoft Azure в виде контейнера Docker с помощью набора средств Azure для IntelliJ."
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
ms.openlocfilehash: b771238934183c953615ac33c42a275d80657556
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a>Публикация приложения Spring Boot в виде контейнера Docker с помощью набора средств Azure для IntelliJ

[Spring Framework] — это решение с открытым исходным кодом, которое помогает разработчикам Java создавать приложения корпоративного класса. Одним из самых популярных проектов, созданных на этой платформе, является проект [Spring Boot]. Он упрощает подход к созданию автономных приложений Java.

[Docker] — это решение с открытым исходным кодом, которое помогает разработчикам автоматизировать развертывание приложений, их масштабирование, а также управление приложениями, которые выполняются в контейнерах.

В данном руководстве описывается процесс развертывания приложения Spring Boot в качестве контейнера Docker в Microsoft Azure с помощью набора средств Azure для IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repo"></a>Клонирование репозитория по умолчанию приложения Docker Spring Boot

Ниже рассмотрена процедура клонирования репозитория приложения Spring Boot Docker с помощью IntelliJ. Процесс использования командной строки см. в разделе [Развертывание приложения Spring Boot в Linux в службе контейнеров Azure][Deploy Spring Boot on Linux in ACS].

1. Откройте IntelliJ.

1. На экране приветствия выберите пункт **GitHub** из списка **Check out from Version Control (Извлечь из системы управления версиями)**.

   ![Параметр GitHub для управления версиями][CL01]

1. При появлении запроса на вход введите свои учетные данные.

   * Если для входа в GitHub вы используете имя пользователя и пароль:

      ![Диалоговое окно для ввода имени пользователя и пароля для входа в GitHub][CL02a]

   * Если для входа в GitHub вы используете токен:

      ![Диалоговое окно для ввода токена GitHub][CL02b]

1. В качестве URL-адреса репозитория введите **https://github.com/spring-guides/gs-spring-boot-docker.git**, укажите локальный путь и сведения о папке, а затем нажмите кнопку **Клонировать**.

   ![Диалоговое окно "Clone Repository" (Клонирование репозитория)][CL03]

1. При появлении запроса на создание проекта IntelliJ выберите **Нет**.

   ![Отклонение создания проекта IntelliJ][CL04]

1. На экране приветствия щелкните пункт **Импорт проекта**.

   ![Пункт "Импорт проекта"][CL05]

1. Найдите путь, по которому был клонирован репозиторий Spring Boot, выделите папку **complete** в корневом каталоге и нажмите кнопку **ОК**.

   ![Выбор папки для импорта][CL06]

1. При появлении запроса выберите **Создать проект из существующих источников**.

   ![Параметр для создания проекта из существующих источников][CL07]

1. Укажите имя проекта или примите имя по умолчанию, проверьте путь к папке **complete**, а затем нажмите кнопку **Далее**.

   ![Выбор имени проекта][CL08]

1. Настройте все каталоги для импорта и нажмите кнопку **Далее**.

   ![Выбор каталогов][CL09]

1. Просмотрите библиотеки для импорта и нажмите кнопку **Далее**.

   ![Просмотр библиотек проекта][CL10]

1. Просмотрите структуру модулей и нажмите кнопку **Далее**.

   ![Просмотр структуры модулей][CL11]

1. Укажите свой JDK и нажмите кнопку **Далее**.

   ![Указание JDK][CL12]

1. Нажмите кнопку **Готово**

   ![Кнопка "Готово"][CL13]

IntelliJ импортирует приложение Spring Boot в качестве проекта и по окончании отобразит структуру.

![Приложение Spring Boot в IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a>Создание приложения Spring Boot

### <a name="build-the-app-by-using-the-maven-pom"></a>Создание приложения с помощью Maven POM

1. Откройте окно инструментов Maven, если это еще не сделано. Последовательно выберите **Вид** > **Окна инструментов** > **Проекты Maven**.

   ![Окна инструментов и команды проектов Maven][BU01]

1. В окне инструментов Maven щелкните правой кнопкой мыши **пакет** и выберите пункт **Выполнить сборку Maven**. (Если проект Maven не отображается автоматически, щелкните значок **Повторный импорт** на панели инструментов Maven.)

   ![Команда "Запуск сборки Maven"][BU02]

1. После успешного создания приложения Spring Boot IntelliJ отобразит сообщение **Сборка выполнена успешно**.

   ![Сообщение "Сборка выполнена успешно"][BU03]

### <a name="create-a-deployment-ready-artifact"></a>Создание готового к развертыванию артефакта

Чтобы опубликовать приложение Spring Boot, необходимо создать готовый к развертыванию артефакт. Выполните следующие действия.

1. Откройте проект веб-приложения в IntelliJ.

1. В меню **File** (Файл) выберите **Project Structure** (Структура проекта).

   ![Команда "Project Structure" (Структура проекта)][ART01]

1. Щелкните зеленый знак "плюс" (**+**), чтобы добавить артефакт, затем щелкните **JAR** и **Empty** (пустой).

   ![Добавление артефакта][ART02]

1. Укажите имя артефакта без расширения JAR, а затем укажите целевую папку назначения для выходных данных Maven.

   ![Указание свойств артефакта][ART03]

1. Создайте манифест для артефакта (необязательно).

   а. Нажмите кнопку **Create Manifest** (Создать манифест).

      ![Кнопка "Создать манифест"][ART04a]

   b. Выберите путь по умолчанию для артефакта и нажмите **ОК**.

      ![Указание пути к артефакту][ART04b]

   c. Нажмите кнопку с многоточием (**...**) для указания основного класса (main).

      ![Поиск основного (main) класса][ART04c]

   d. Выберите основной класс и нажмите кнопку **ОК**.

      ![Указание основного (main) класса][ART04d]

1. Нажмите кнопку **ОК**.

   ![Закрытие диалогового окна "Project Structure" (Структура проекта)][ART05]

> [!NOTE]
> Дополнительные сведения о создании артефактов в IntelliJ см. в разделе [Configuring Artifacts] (Настройка артефактов) на веб-сайте JetBrains.
>

### <a name="build-the-artifact-for-deployment"></a>Создание артефакта для развертывания

1. Нажмите кнопку **Build** (Сборка), а затем кнопку **Artifacts** (Артефакты).

   ![Команда "Build Artifacts" (Создать артефакты)][BU04]

1. При появлении контекстного меню **Build Artifact** (Создание артефактов) нажмите кнопку **Build** (Сборка).

   ![Контекстное меню "Build Artifacts" (Создание артефакта)][BU05]

IntelliJ должен отобразить созданный артефакт для приложения Spring Boot в окне инструментов проекта.

   ![Созданный артефакт][BU06]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Публикация веб-приложения в Azure с помощью контейнера Docker

1. Если вы еще не вошли в свою учетную запись Azure, выполните процедуру в статье [Инструкции по входу для набора средств Azure для IntelliJ][Azure Sign In for IntelliJ].

1. В окне инструментов обозревателя проектов щелкните правой кнопкой мыши проект и выберите **Azure** > **Publish as Docker Container** (Опубликовать как контейнер Docker).

   ![Команда публикации в виде контейнера Docker][PU01]

1. Когда появится диалоговое окно **Развертывание контейнера Docker в Azure**, в нем будут отображаться все существующие узлы Docker. Если требуется развернуть на существующий узел, можно пропустить шаг 4. В противном случае, чтобы создать узел, выполните следующие действия.

   а. Щелкните зеленый знак "плюс" (**+**).

      ![Добавление нового узла Docker][PU02]

   b. При появлении диалогового окна **Создание узла Docker** можно принять значения по умолчанию или задать пользовательские параметры для нового узла Docker. (Подробное описание различных параметров см. в статье [Публикация веб-приложения в виде контейнера Docker с помощью набора средств Azure для IntelliJ][Publish Container with Azure Toolkit].) Нажмите кнопку **Next** (Далее) после задания используемых параметров.

      ![Задание параметров узла Docker][PU03a]

   c. Можно использовать для входа в систему существующие учетные данные, хранящиеся в Azure Key Vault, или ввести новые учетные данные для входа в Docker. После задания параметров нажмите кнопку **Finish** (Готово).

      ![Задание учетных данных узла Docker][PU03b]

1. Выберите узел Docker и нажмите кнопку **Next** (Далее).

   ![Выбор используемого узла Docker][PU04]

1. На последней странице диалогового окна **Deploy Docker Container on Azure** (Развертывание контейнера Docker в Azure) задайте следующие параметры.

   а. Можно указать пользовательское имя для контейнера, в котором будет размещаться контейнер Docker, или принять значение по умолчанию.

   b. Для узла Docker укажите TCP-порты с помощью следующего синтаксиса: *[внешний порт]*:*[внутренний порт]*. Например, **80:8080** означает внешний порт "80" и внутренний порт Spring Boot по умолчанию "8080".
   
      После настройки внутреннего порта (например, с помощью файла application.yml) необходимо указать номер порта для обеспечения корректной маршрутизации в Azure.

   c. После настройки этих параметров щелкните **Finish** (Готово).

   ![Развертывание контейнера Docker в Azure][PU05]

1. После завершения публикации набора средств Azure в журнале действий Azure будет отображаться состояние **Опубликовано**.

   ![Успешно развернутый узел Docker][PU06]

## <a name="next-steps"></a>Дальнейшие действия

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

Сведения о дополнительных методах создания приложений Spring Boot с помощью IntelliJ см. в разделе [Создание проектов Spring Boot](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) на веб-сайте JetBrains.

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Configuring Artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
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
