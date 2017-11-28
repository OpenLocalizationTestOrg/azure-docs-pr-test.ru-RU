---
title: "Создание сервера Jenkins в Azure"
description: "Установите Jenkins на виртуальной машине Azure под управлением Linux на основе шаблона решения Jenkins и создайте образец приложения Java."
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 7bb74f297d52fb25171817175cce64187b397c38
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-the-azure-portal"></a><span data-ttu-id="a1a2e-103">Создание сервера Jenkins на виртуальной машине Azure под управлением Linux на портале Azure</span><span class="sxs-lookup"><span data-stu-id="a1a2e-103">Create a Jenkins server on an Azure Linux VM from the Azure portal</span></span>

<span data-ttu-id="a1a2e-104">В этом кратком руководстве описано, как установить [Jenkins](https://jenkins.io) на виртуальной машине под управлением Ubuntu Linux с помощью средств и подключаемых модулей, настроенных для работы с Azure.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-104">This quickstart shows how to install [Jenkins](https://jenkins.io) on an Ubuntu Linux VM with the tools and plug-ins configured to work with Azure.</span></span> <span data-ttu-id="a1a2e-105">Мы создадим в Azure сервер Jenkins для сборки образца приложения Java из [GitHub](https://github.com).</span><span class="sxs-lookup"><span data-stu-id="a1a2e-105">When you're finished, you have a Jenkins server running in Azure building a sample Java app from [GitHub](https://github.com).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1a2e-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a1a2e-106">Prerequisites</span></span>

* <span data-ttu-id="a1a2e-107">Подписка Azure</span><span class="sxs-lookup"><span data-stu-id="a1a2e-107">An Azure subscription</span></span>
* <span data-ttu-id="a1a2e-108">Доступ к SSH в командной строке компьютера (например, в оболочке Bash или [PuTTY](http://www.putty.org/))</span><span class="sxs-lookup"><span data-stu-id="a1a2e-108">Access to SSH on your computer's command line (such as the Bash shell or [PuTTY](http://www.putty.org/))</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-the-jenkins-vm-from-the-solution-template"></a><span data-ttu-id="a1a2e-109">Создание виртуальной машины Jenkins на основе шаблона решения</span><span class="sxs-lookup"><span data-stu-id="a1a2e-109">Create the Jenkins VM from the solution template</span></span>

<span data-ttu-id="a1a2e-110">Откройте [образ marketplace для Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) в веб-браузере и нажмите кнопку **ПОЛУЧИТЬ СЕЙЧАС** в левой части страницы.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-110">Open the [marketplace image for Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) in your web browser and select  **GET IT NOW** from the left-hand side of the page.</span></span> <span data-ttu-id="a1a2e-111">Просмотрите сведения о ценах и выберите **Продолжить**, а затем нажмите **Создание**, чтобы настроить сервер Jenkins на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-111">Review the pricing details and select **Continue**, then select **Create** to configure the Jenkins server in the Azure portal.</span></span> 
   
![Диалоговое окно на портале Azure](./media/install-jenkins-solution-template/ap-create.png)

<span data-ttu-id="a1a2e-113">На вкладке **Настройка основных параметров** заполните следующие поля:</span><span class="sxs-lookup"><span data-stu-id="a1a2e-113">In the **Configure basic settings** tab, fill in the following fields:</span></span>

![Настройка основных параметров.](./media/install-jenkins-solution-template/ap-basic.png)

* <span data-ttu-id="a1a2e-115">Установите значение **Jenkins** для параметра **Имя**.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-115">Use **Jenkins** for **Name**.</span></span>
* <span data-ttu-id="a1a2e-116">Введите данные в поле **Имя пользователя**.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-116">Enter a **User name**.</span></span> <span data-ttu-id="a1a2e-117">Имя пользователя должно соответствовать [особым требованиям](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="a1a2e-117">The user name must meet [specific requirements](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span></span>
* <span data-ttu-id="a1a2e-118">Установите значение **Пароль** для параметра **Тип проверки подлинности** и введите пароль.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-118">Select **Password** as the **Authentication type** and enter a password.</span></span> <span data-ttu-id="a1a2e-119">Пароль должен содержать прописную букву, цифру и один специальный символ.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-119">The password must have an upper case character, a number, and one special character.</span></span>
* <span data-ttu-id="a1a2e-120">Установите значение **myJenkinsResourceGroup** для параметра **Группа ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-120">Use **myJenkinsResourceGroup** for the **Resource Group**.</span></span>
* <span data-ttu-id="a1a2e-121">Выберите значение **Восток США** для параметра [Регион Azure](https://azure.microsoft.com/regions/) из раскрывающегося списка **Расположение**.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-121">Choose the **East US** [Azure region](https://azure.microsoft.com/regions/) from the **Location** drop-down.</span></span>

<span data-ttu-id="a1a2e-122">Нажмите **ОК**, чтобы перейти к вкладке **Настройка дополнительных параметров**. Введите уникальное доменное имя для идентификации сервера Jenkins и нажмите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-122">Select **OK** to proceed to the **Configure additional options** tab. Enter a unique domain name to identify the Jenkins server and select **OK**.</span></span>

![Настройка дополнительных параметров](./media/install-jenkins-solution-template/ap-addtional.png)  

 <span data-ttu-id="a1a2e-124">После успешной проверки еще раз нажмите **ОК** на вкладке **Сводка**. Наконец выберите **Приобретение**, чтобы создать виртуальную машину Jenkins.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-124">Once validation passes, select **OK** again from the **Summary** tab. Finally, select **Purchase** to create the Jenkins VM.</span></span> <span data-ttu-id="a1a2e-125">Когда сервер будет готов, вы получите уведомление на портале Azure:</span><span class="sxs-lookup"><span data-stu-id="a1a2e-125">When your server is ready, you get a notification in the Azure portal:</span></span>   

![Уведомление о готовности Jenkins](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-to-jenkins"></a><span data-ttu-id="a1a2e-127">Подключение к Jenkins</span><span class="sxs-lookup"><span data-stu-id="a1a2e-127">Connect to Jenkins</span></span>

<span data-ttu-id="a1a2e-128">Перейдите к виртуальной машине (например, http://jenkins2517454.eastus.cloudapp.azure.com/) в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-128">Navigate to your virtual machine (for example, http://jenkins2517454.eastus.cloudapp.azure.com/) in  your web browser.</span></span> <span data-ttu-id="a1a2e-129">Консоль Jenkins недоступна по незащищенному протоколу HTTP, поэтому на странице приведены инструкции по безопасному доступу к консоли Jenkins с компьютера с использованием туннеля SSH.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-129">The Jenkins console is inaccessible through unsecured HTTP so instructions are provided on the page to access the Jenkins console securely from your computer using an SSH tunnel.</span></span>

![Разблокировка Jenkins](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

<span data-ttu-id="a1a2e-131">Настройте туннель на странице из командной строки, используя команду `ssh`. Для этого замените `username` именем администратора виртуальной машины, указанным ранее при настройке виртуальной машины на основе шаблона решения.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-131">Set up the tunnel using the `ssh` command on the page from the command line, replacing `username` with the name of the virtual machine admin user chosen earlier when setting up the virtual machine from the solution template.</span></span>

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

<span data-ttu-id="a1a2e-132">После запуска туннеля перейдите по адресу http://localhost:8080/ на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-132">After you have started the tunnel, navigate to http://localhost:8080/ on your local machine.</span></span> 

<span data-ttu-id="a1a2e-133">Получите первоначальный пароль, выполнив команду ниже в командной строке при подключении к виртуальной машине Jenkins через SSH.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-133">Get the initial password by running the following command in the command line while connected through SSH to the Jenkins VM.</span></span>

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

<span data-ttu-id="a1a2e-134">При первом использовании разблокируйте панель мониторинга Jenkins с помощью этого пароля.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-134">Unlock the Jenkins dashboard for the first time using this initial password.</span></span>

![Разблокировка Jenkins](./media/install-jenkins-solution-template/jenkins-unlock.png)

<span data-ttu-id="a1a2e-136">Выберите **Install suggested plugins** (Установить предлагаемые подключаемые модули) на следующей странице и создайте учетную запись администратора Jenkins для доступа к панели мониторинга Jenkins.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-136">Select **Install suggested plugins** on the next page and then create a Jenkins admin user used to access the Jenkins dashboard.</span></span>

![Экземпляр Jenkins готов!](./media/install-jenkins-solution-template/jenkins-welcome.png)

<span data-ttu-id="a1a2e-138">Сервер Jenkins готов к созданию кода.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-138">The Jenkins server is now ready to build code.</span></span>

## <a name="create-your-first-job"></a><span data-ttu-id="a1a2e-139">Создание первого задания</span><span class="sxs-lookup"><span data-stu-id="a1a2e-139">Create your first job</span></span>

<span data-ttu-id="a1a2e-140">Выберите **Create new jobs** (Создать задания) в консоли Jenkins. Назовите задание **mySampleApp**, выберите **Freestyle project** (Универсальный проект) и нажмите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-140">Select **Create new jobs** from the Jenkins console, then name it **mySampleApp** and select **Freestyle project**, then select **OK**.</span></span>

![Создание задания](./media/install-jenkins-solution-template/jenkins-new-job.png) 

<span data-ttu-id="a1a2e-142">Выберите вкладку **Управление исходным кодом**, включите **Git** и введите следующий URL-адрес в поле **URL-адрес репозитория**: `https://github.com/spring-guides/gs-spring-boot.git`</span><span class="sxs-lookup"><span data-stu-id="a1a2e-142">Select the **Source Code Management** tab, enable **Git**, and enter the following URL in **Repository URL**  field: `https://github.com/spring-guides/gs-spring-boot.git`</span></span>

![Определение репозитория Git](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

<span data-ttu-id="a1a2e-144">Выберите вкладку **Создание**, нажмите **Добавление шага сборки** и **Invoke Gradle script** (Вызов сценария Gradle).</span><span class="sxs-lookup"><span data-stu-id="a1a2e-144">Select the **Build** tab, then select **Add build step**, **Invoke Gradle script**.</span></span> <span data-ttu-id="a1a2e-145">Выберите **Use Gradle Wrapper** (Использовать программу-оболочку Gradle), затем введите значение `complete` для параметра **Wrapper location** (Расположение программы-оболочки) и `build` для параметра **Задачи**.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-145">Select **Use Gradle Wrapper**, then enter `complete` in **Wrapper location** and `build` for **Tasks**.</span></span>

![Использование программы-оболочки Gradle для сборки](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

<span data-ttu-id="a1a2e-147">Нажмите кнопку **Advanced..** (Дополнительно...)</span><span class="sxs-lookup"><span data-stu-id="a1a2e-147">Select **Advanced..**</span></span> <span data-ttu-id="a1a2e-148">и введите `complete` в поле **Root Build script** (Корневой скрипт сборки).</span><span class="sxs-lookup"><span data-stu-id="a1a2e-148">and then enter `complete` in the **Root Build script** field.</span></span> <span data-ttu-id="a1a2e-149">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-149">Select **Save**.</span></span>

![Установка дополнительных параметров на этапе сборки программы-оболочки Gradle](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-the-code"></a><span data-ttu-id="a1a2e-151">Сборка кода</span><span class="sxs-lookup"><span data-stu-id="a1a2e-151">Build the code</span></span>

<span data-ttu-id="a1a2e-152">Выберите **Build Now** (Собрать сейчас), чтобы скомпилировать код и создать пакет для примера приложения.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-152">Select **Build Now** to compile the code and package the sample app.</span></span> <span data-ttu-id="a1a2e-153">По завершении сборки выберите для проекта ссылку **Рабочая область**.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-153">When your build completes, select the **Workspace** link for the project.</span></span>

![Перейдите в рабочую область, чтобы получить JAR-файл из сборки](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

<span data-ttu-id="a1a2e-155">Перейдите к `complete/build/libs` и проверьте наличие `gs-spring-boot-0.1.0.jar`, чтобы удостовериться в успешности сборки.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-155">Navigate to `complete/build/libs` and ensure the `gs-spring-boot-0.1.0.jar` is there to verify that your build was successful.</span></span> <span data-ttu-id="a1a2e-156">Теперь сервер Jenkins готов к сборке ваших собственных проектов в Azure.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-156">Your Jenkins server is now ready to build your own projects in Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1a2e-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a1a2e-157">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a1a2e-158">Использование агентов виртуальных машин для непрерывной интеграции с Jenkins.</span><span class="sxs-lookup"><span data-stu-id="a1a2e-158">Add Azure VMs as Jenkins agents</span></span>](jenkins-azure-vm-agents.md)
