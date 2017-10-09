---
title: "aaaCreate сервера Jenkins в Azure"
description: "Установите на виртуальной машине Azure Linux с помощью шаблона решения Jenkins hello Jenkins и постройте образец приложения Java."
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 82ab2ac52594acba131414b449b608978591d4b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-hello-azure-portal"></a>Создать сервер Jenkins на виртуальной Машине Linux Azure из hello портал Azure

Краткого руководства показано, как tooinstall [Jenkins](https://jenkins.io) на виртуальной Машине Linux Ubuntu с помощью средств hello и toowork настроен подключаемых модулей с помощью Azure. Мы создадим в Azure сервер Jenkins для сборки образца приложения Java из [GitHub](https://github.com).

## <a name="prerequisites"></a>Предварительные требования

* Подписка Azure
* TooSSH доступ в командной строке компьютера (например hello Bash оболочки или [PuTTY](http://www.putty.org/))

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-jenkins-vm-from-hello-solution-template"></a>Создание hello Jenkins виртуальной Машины из шаблона решения hello

Откройте hello [образа marketplace для Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) в веб-браузере и выберите **получение ИТ ТЕПЕРЬ** с левой стороны страницы приветствия hello. Просмотрите hello, ценах и выберите **Продолжить**, а затем выберите **создать** сервера Jenkins tooconfigure hello в hello портал Azure. 
   
![Диалоговое окно на портале Azure](./media/install-jenkins-solution-template/ap-create.png)

В hello **настройки основных параметров** вкладку, заполните следующие поля hello:

![Настройка основных параметров.](./media/install-jenkins-solution-template/ap-basic.png)

* Установите значение **Jenkins** для параметра **Имя**.
* Введите данные в поле **Имя пользователя**. имя пользователя Hello должен соответствовать [особые требования](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).
* Выберите **пароль** как hello **тип проверки подлинности** и введите пароль. Hello пароль должен содержать прописной буквы, числа и один специальный символ.
* Используйте **myJenkinsResourceGroup** для hello **группы ресурсов**.
* Выберите hello **Восток США** [регион Azure](https://azure.microsoft.com/regions/) из hello **расположение** раскрывающегося списка.

Выберите **ОК** tooproceed toohello **Настройка дополнительных параметров** вкладки. Укажите сервер Jenkins tooidentify hello уникальное доменное имя и выберите **ОК**.

![Настройка дополнительных параметров](./media/install-jenkins-solution-template/ap-addtional.png)  

 После успешной проверке выбрать **ОК** еще раз из hello **Сводка** вкладки. Наконец, выберите **покупки** toocreate hello Jenkins виртуальной Машины. Если сервер готов, вы получаете уведомление в hello портала Azure:   

![Уведомление о готовности Jenkins](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-toojenkins"></a>Подключение tooJenkins

Tooyour виртуальной машины (например, http://jenkins2517454.eastus.cloudapp.azure.com/) перейдите в веб-браузере. Hello Jenkins консоли недоступен через незащищенную HTTP, инструкции на консоли hello страницы tooaccess hello Jenkins безопасно с компьютера с использованием туннеля SSH.

![Разблокировка Jenkins](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

Настройка туннеля hello hello `ssh` команды на странице приветствия из командной строки hello, заменив `username` hello имя пользователя администратора виртуальной машины hello, указанного ранее при настройке hello виртуальной машины из шаблона решения hello.

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

После запуска туннеля hello перейдите toohttp://localhost:8080 / на локальном компьютере. 

Получение исходного пароля hello, выполнив следующую команду в командной строке приветствия при подключении через SSH toohello Jenkins ВМ hello.

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

Разблокируйте hello Jenkins мониторинга для hello первый раз, используя этот исходный пароль.

![Разблокировка Jenkins](./media/install-jenkins-solution-template/jenkins-unlock.png)

Выберите **установить предлагаемые подключаемых модулей** на hello Следующая страница, а затем создать Jenkins администратора пользователя, используемое tooaccess hello Jenkins информационной панели.

![Экземпляр Jenkins готов!](./media/install-jenkins-solution-template/jenkins-welcome.png)

сервер Jenkins Hello теперь является готов toobuild кода.

## <a name="create-your-first-job"></a>Создание первого задания

Выберите **создавать новые задания** из консоли Jenkins hello, назовите его **mySampleApp** и выберите **проекта в свободном стиле**, а затем выберите **ОК**.

![Создание задания](./media/install-jenkins-solution-template/jenkins-new-job.png) 

Выберите hello **управление исходным кодом** включите **Git**и введите URL-адреса в hello **URL-адрес репозитория** поля:`https://github.com/spring-guides/gs-spring-boot.git`

![Определение hello репозитория Git](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

Выберите hello **построения** , затем выберите **добавить шаг сборки**, **Gradle вызвать сценарий**. Выберите **Use Gradle Wrapper** (Использовать программу-оболочку Gradle), затем введите значение `complete` для параметра **Wrapper location** (Расположение программы-оболочки) и `build` для параметра **Задачи**.

![Использовать toobuild программы-оболочки Gradle hello](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

Нажмите кнопку **Advanced..** (Дополнительно...) а затем введите `complete` в hello **скрипт построения корневой** поля. Щелкните **Сохранить**.

![Установка дополнительных параметров на этапе построения программы-оболочки Gradle hello](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-hello-code"></a>Построение кода hello

Выберите **сборки теперь** toocompile hello код и пакет образца приложение hello. После завершения построения выберите hello **рабочей** ссылку проекта hello.

![Обзор toohello рабочей tooget hello JAR-файл из сборки hello](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

Перейдите в слишком`complete/build/libs` и обеспечить hello `gs-spring-boot-0.1.0.jar` есть tooverify успешности построения. К Jenkins, в которой находится сервер готов toobuild проектов в Azure.

## <a name="next-steps"></a>Дальнейшие действия

> [!div class="nextstepaction"]
> [Использование агентов виртуальных машин для непрерывной интеграции с Jenkins.](jenkins-azure-vm-agents.md)
