<span data-ttu-id="97bbb-101">Azure определит, что приложение использует Python, **если верны оба следующих условия**:</span><span class="sxs-lookup"><span data-stu-id="97bbb-101">Azure will determine that your application uses Python **if both of these conditions are true**:</span></span>

* <span data-ttu-id="97bbb-102">файл Requirements.txt в корневой папке hello</span><span class="sxs-lookup"><span data-stu-id="97bbb-102">requirements.txt file in hello root folder</span></span>
* <span data-ttu-id="97bbb-103">любой файл .py в корневой папке hello или runtime.txt, указывающее python</span><span class="sxs-lookup"><span data-stu-id="97bbb-103">any .py file in hello root folder OR a runtime.txt that specifies python</span></span>

<span data-ttu-id="97bbb-104">Когда это hello так, в нем используется сценарий Python конкретного развертывания, выполняющий hello Стандартная синхронизации файлов, а также дополнительные Python операций, таких как:</span><span class="sxs-lookup"><span data-stu-id="97bbb-104">When that's hello case, it will use a Python specific deployment script, which performs hello standard synchronization of files, as well as additional Python operations such as:</span></span>

* <span data-ttu-id="97bbb-105">автоматическое управление виртуальной средой;</span><span class="sxs-lookup"><span data-stu-id="97bbb-105">Automatic management of virtual environment</span></span>
* <span data-ttu-id="97bbb-106">установка пакетов, указанных в файле requirements.txt, с помощью pip;</span><span class="sxs-lookup"><span data-stu-id="97bbb-106">Installation of packages listed in requirements.txt using pip</span></span>
* <span data-ttu-id="97bbb-107">Создание соответствующего файла Web.config hello основании hello выбрать версию Python.</span><span class="sxs-lookup"><span data-stu-id="97bbb-107">Creation of hello appropriate web.config based on hello selected Python version.</span></span>
* <span data-ttu-id="97bbb-108">Сбор статических файлов для приложений Django</span><span class="sxs-lookup"><span data-stu-id="97bbb-108">Collect static files for Django applications</span></span>

<span data-ttu-id="97bbb-109">Можно управлять определенными аспектами шагов развертывания по умолчанию hello без необходимости toocustomize hello скрипта.</span><span class="sxs-lookup"><span data-stu-id="97bbb-109">You can control certain aspects of hello default deployment steps without having toocustomize hello script.</span></span>

<span data-ttu-id="97bbb-110">Если вы хотите tooskip все шаги конкретного развертывания Python, можно создать этот пустой файл:</span><span class="sxs-lookup"><span data-stu-id="97bbb-110">If you want tooskip all Python specific deployment steps, you can create this empty file:</span></span>

    \.skipPythonDeployment

<span data-ttu-id="97bbb-111">Для усиления контроля над развертывания скрипта развертывания по умолчанию hello можно переопределить, создав hello следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="97bbb-111">For more control over deployment, you can override hello default deployment script by creating hello following files:</span></span>

    \.deployment
    \deploy.cmd

<span data-ttu-id="97bbb-112">Можно использовать hello [интерфейс командной строки Azure] [ Azure command-line interface] toocreate hello файлы.</span><span class="sxs-lookup"><span data-stu-id="97bbb-112">You can use hello [Azure command-line interface][Azure command-line interface] toocreate hello files.</span></span>  <span data-ttu-id="97bbb-113">Используйте эту команду из папки проекта:</span><span class="sxs-lookup"><span data-stu-id="97bbb-113">Use this command from your project folder:</span></span>

    azure site deploymentscript --python

<span data-ttu-id="97bbb-114">Если эти файлы не существуют, Azure создает временный скрипт развертывания и выполняет его.</span><span class="sxs-lookup"><span data-stu-id="97bbb-114">When these files don't exist, Azure creates a temporary deployment script and runs it.</span></span>  <span data-ttu-id="97bbb-115">Это идентичные toohello один создании с помощью приведенных выше команд hello.</span><span class="sxs-lookup"><span data-stu-id="97bbb-115">It is identical toohello one you create with hello command above.</span></span>

[Azure command-line interface]: http://azure.microsoft.com/downloads/
