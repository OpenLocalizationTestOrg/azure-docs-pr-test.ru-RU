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
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-hello-azure-portal"></a><span data-ttu-id="f1b1a-103">Создать сервер Jenkins на виртуальной Машине Linux Azure из hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="f1b1a-103">Create a Jenkins server on an Azure Linux VM from hello Azure portal</span></span>

<span data-ttu-id="f1b1a-104">Краткого руководства показано, как tooinstall [Jenkins](https://jenkins.io) на виртуальной Машине Linux Ubuntu с помощью средств hello и toowork настроен подключаемых модулей с помощью Azure.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-104">This quickstart shows how tooinstall [Jenkins](https://jenkins.io) on an Ubuntu Linux VM with hello tools and plug-ins configured toowork with Azure.</span></span> <span data-ttu-id="f1b1a-105">Мы создадим в Azure сервер Jenkins для сборки образца приложения Java из [GitHub](https://github.com).</span><span class="sxs-lookup"><span data-stu-id="f1b1a-105">When you're finished, you have a Jenkins server running in Azure building a sample Java app from [GitHub](https://github.com).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f1b1a-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f1b1a-106">Prerequisites</span></span>

* <span data-ttu-id="f1b1a-107">Подписка Azure</span><span class="sxs-lookup"><span data-stu-id="f1b1a-107">An Azure subscription</span></span>
* <span data-ttu-id="f1b1a-108">TooSSH доступ в командной строке компьютера (например hello Bash оболочки или [PuTTY](http://www.putty.org/))</span><span class="sxs-lookup"><span data-stu-id="f1b1a-108">Access tooSSH on your computer's command line (such as hello Bash shell or [PuTTY](http://www.putty.org/))</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-jenkins-vm-from-hello-solution-template"></a><span data-ttu-id="f1b1a-109">Создание hello Jenkins виртуальной Машины из шаблона решения hello</span><span class="sxs-lookup"><span data-stu-id="f1b1a-109">Create hello Jenkins VM from hello solution template</span></span>

<span data-ttu-id="f1b1a-110">Откройте hello [образа marketplace для Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) в веб-браузере и выберите **получение ИТ ТЕПЕРЬ** с левой стороны страницы приветствия hello.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-110">Open hello [marketplace image for Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) in your web browser and select  **GET IT NOW** from hello left-hand side of hello page.</span></span> <span data-ttu-id="f1b1a-111">Просмотрите hello, ценах и выберите **Продолжить**, а затем выберите **создать** сервера Jenkins tooconfigure hello в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-111">Review hello pricing details and select **Continue**, then select **Create** tooconfigure hello Jenkins server in hello Azure portal.</span></span> 
   
![Диалоговое окно на портале Azure](./media/install-jenkins-solution-template/ap-create.png)

<span data-ttu-id="f1b1a-113">В hello **настройки основных параметров** вкладку, заполните следующие поля hello:</span><span class="sxs-lookup"><span data-stu-id="f1b1a-113">In hello **Configure basic settings** tab, fill in hello following fields:</span></span>

![Настройка основных параметров.](./media/install-jenkins-solution-template/ap-basic.png)

* <span data-ttu-id="f1b1a-115">Установите значение **Jenkins** для параметра **Имя**.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-115">Use **Jenkins** for **Name**.</span></span>
* <span data-ttu-id="f1b1a-116">Введите данные в поле **Имя пользователя**.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-116">Enter a **User name**.</span></span> <span data-ttu-id="f1b1a-117">имя пользователя Hello должен соответствовать [особые требования](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="f1b1a-117">hello user name must meet [specific requirements](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span></span>
* <span data-ttu-id="f1b1a-118">Выберите **пароль** как hello **тип проверки подлинности** и введите пароль.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-118">Select **Password** as hello **Authentication type** and enter a password.</span></span> <span data-ttu-id="f1b1a-119">Hello пароль должен содержать прописной буквы, числа и один специальный символ.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-119">hello password must have an upper case character, a number, and one special character.</span></span>
* <span data-ttu-id="f1b1a-120">Используйте **myJenkinsResourceGroup** для hello **группы ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-120">Use **myJenkinsResourceGroup** for hello **Resource Group**.</span></span>
* <span data-ttu-id="f1b1a-121">Выберите hello **Восток США** [регион Azure](https://azure.microsoft.com/regions/) из hello **расположение** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-121">Choose hello **East US** [Azure region](https://azure.microsoft.com/regions/) from hello **Location** drop-down.</span></span>

<span data-ttu-id="f1b1a-122">Выберите **ОК** tooproceed toohello **Настройка дополнительных параметров** вкладки. Укажите сервер Jenkins tooidentify hello уникальное доменное имя и выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-122">Select **OK** tooproceed toohello **Configure additional options** tab. Enter a unique domain name tooidentify hello Jenkins server and select **OK**.</span></span>

![Настройка дополнительных параметров](./media/install-jenkins-solution-template/ap-addtional.png)  

 <span data-ttu-id="f1b1a-124">После успешной проверке выбрать **ОК** еще раз из hello **Сводка** вкладки. Наконец, выберите **покупки** toocreate hello Jenkins виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-124">Once validation passes, select **OK** again from hello **Summary** tab. Finally, select **Purchase** toocreate hello Jenkins VM.</span></span> <span data-ttu-id="f1b1a-125">Если сервер готов, вы получаете уведомление в hello портала Azure:</span><span class="sxs-lookup"><span data-stu-id="f1b1a-125">When your server is ready, you get a notification in hello Azure portal:</span></span>   

![Уведомление о готовности Jenkins](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-toojenkins"></a><span data-ttu-id="f1b1a-127">Подключение tooJenkins</span><span class="sxs-lookup"><span data-stu-id="f1b1a-127">Connect tooJenkins</span></span>

<span data-ttu-id="f1b1a-128">Tooyour виртуальной машины (например, http://jenkins2517454.eastus.cloudapp.azure.com/) перейдите в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-128">Navigate tooyour virtual machine (for example, http://jenkins2517454.eastus.cloudapp.azure.com/) in  your web browser.</span></span> <span data-ttu-id="f1b1a-129">Hello Jenkins консоли недоступен через незащищенную HTTP, инструкции на консоли hello страницы tooaccess hello Jenkins безопасно с компьютера с использованием туннеля SSH.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-129">hello Jenkins console is inaccessible through unsecured HTTP so instructions are provided on hello page tooaccess hello Jenkins console securely from your computer using an SSH tunnel.</span></span>

![Разблокировка Jenkins](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

<span data-ttu-id="f1b1a-131">Настройка туннеля hello hello `ssh` команды на странице приветствия из командной строки hello, заменив `username` hello имя пользователя администратора виртуальной машины hello, указанного ранее при настройке hello виртуальной машины из шаблона решения hello.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-131">Set up hello tunnel using hello `ssh` command on hello page from hello command line, replacing `username` with hello name of hello virtual machine admin user chosen earlier when setting up hello virtual machine from hello solution template.</span></span>

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

<span data-ttu-id="f1b1a-132">После запуска туннеля hello перейдите toohttp://localhost:8080 / на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-132">After you have started hello tunnel, navigate toohttp://localhost:8080/ on your local machine.</span></span> 

<span data-ttu-id="f1b1a-133">Получение исходного пароля hello, выполнив следующую команду в командной строке приветствия при подключении через SSH toohello Jenkins ВМ hello.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-133">Get hello initial password by running hello following command in hello command line while connected through SSH toohello Jenkins VM.</span></span>

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

<span data-ttu-id="f1b1a-134">Разблокируйте hello Jenkins мониторинга для hello первый раз, используя этот исходный пароль.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-134">Unlock hello Jenkins dashboard for hello first time using this initial password.</span></span>

![Разблокировка Jenkins](./media/install-jenkins-solution-template/jenkins-unlock.png)

<span data-ttu-id="f1b1a-136">Выберите **установить предлагаемые подключаемых модулей** на hello Следующая страница, а затем создать Jenkins администратора пользователя, используемое tooaccess hello Jenkins информационной панели.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-136">Select **Install suggested plugins** on hello next page and then create a Jenkins admin user used tooaccess hello Jenkins dashboard.</span></span>

![Экземпляр Jenkins готов!](./media/install-jenkins-solution-template/jenkins-welcome.png)

<span data-ttu-id="f1b1a-138">сервер Jenkins Hello теперь является готов toobuild кода.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-138">hello Jenkins server is now ready toobuild code.</span></span>

## <a name="create-your-first-job"></a><span data-ttu-id="f1b1a-139">Создание первого задания</span><span class="sxs-lookup"><span data-stu-id="f1b1a-139">Create your first job</span></span>

<span data-ttu-id="f1b1a-140">Выберите **создавать новые задания** из консоли Jenkins hello, назовите его **mySampleApp** и выберите **проекта в свободном стиле**, а затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-140">Select **Create new jobs** from hello Jenkins console, then name it **mySampleApp** and select **Freestyle project**, then select **OK**.</span></span>

![Создание задания](./media/install-jenkins-solution-template/jenkins-new-job.png) 

<span data-ttu-id="f1b1a-142">Выберите hello **управление исходным кодом** включите **Git**и введите URL-адреса в hello **URL-адрес репозитория** поля:`https://github.com/spring-guides/gs-spring-boot.git`</span><span class="sxs-lookup"><span data-stu-id="f1b1a-142">Select hello **Source Code Management** tab, enable **Git**, and enter hello following URL in **Repository URL**  field: `https://github.com/spring-guides/gs-spring-boot.git`</span></span>

![Определение hello репозитория Git](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

<span data-ttu-id="f1b1a-144">Выберите hello **построения** , затем выберите **добавить шаг сборки**, **Gradle вызвать сценарий**.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-144">Select hello **Build** tab, then select **Add build step**, **Invoke Gradle script**.</span></span> <span data-ttu-id="f1b1a-145">Выберите **Use Gradle Wrapper** (Использовать программу-оболочку Gradle), затем введите значение `complete` для параметра **Wrapper location** (Расположение программы-оболочки) и `build` для параметра **Задачи**.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-145">Select **Use Gradle Wrapper**, then enter `complete` in **Wrapper location** and `build` for **Tasks**.</span></span>

![Использовать toobuild программы-оболочки Gradle hello](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

<span data-ttu-id="f1b1a-147">Нажмите кнопку **Advanced..** (Дополнительно...)</span><span class="sxs-lookup"><span data-stu-id="f1b1a-147">Select **Advanced..**</span></span> <span data-ttu-id="f1b1a-148">а затем введите `complete` в hello **скрипт построения корневой** поля.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-148">and then enter `complete` in hello **Root Build script** field.</span></span> <span data-ttu-id="f1b1a-149">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-149">Select **Save**.</span></span>

![Установка дополнительных параметров на этапе построения программы-оболочки Gradle hello](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-hello-code"></a><span data-ttu-id="f1b1a-151">Построение кода hello</span><span class="sxs-lookup"><span data-stu-id="f1b1a-151">Build hello code</span></span>

<span data-ttu-id="f1b1a-152">Выберите **сборки теперь** toocompile hello код и пакет образца приложение hello.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-152">Select **Build Now** toocompile hello code and package hello sample app.</span></span> <span data-ttu-id="f1b1a-153">После завершения построения выберите hello **рабочей** ссылку проекта hello.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-153">When your build completes, select hello **Workspace** link for hello project.</span></span>

![Обзор toohello рабочей tooget hello JAR-файл из сборки hello](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

<span data-ttu-id="f1b1a-155">Перейдите в слишком`complete/build/libs` и обеспечить hello `gs-spring-boot-0.1.0.jar` есть tooverify успешности построения.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-155">Navigate too`complete/build/libs` and ensure hello `gs-spring-boot-0.1.0.jar` is there tooverify that your build was successful.</span></span> <span data-ttu-id="f1b1a-156">К Jenkins, в которой находится сервер готов toobuild проектов в Azure.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-156">Your Jenkins server is now ready toobuild your own projects in Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1b1a-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f1b1a-157">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f1b1a-158">Использование агентов виртуальных машин для непрерывной интеграции с Jenkins.</span><span class="sxs-lookup"><span data-stu-id="f1b1a-158">Add Azure VMs as Jenkins agents</span></span>](jenkins-azure-vm-agents.md)
