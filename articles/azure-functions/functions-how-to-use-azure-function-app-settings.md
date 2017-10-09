---
title: "Параметры приложения Azure функция aaaConfigure | Документы Microsoft"
description: "Узнайте, как tooconfigure Azure функция параметров приложения."
services: 
documentationcenter: .net
author: rachelappel
manager: erikre
editor: 
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 04/23/2017
ms.author: glenga
ms.openlocfilehash: 539e203ac449061ef3ceae5e93df3bdbb326e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-a-function-app-in-hello-azure-portal"></a><span data-ttu-id="4d688-103">Как toomanage приложении функции в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="4d688-103">How toomanage a function app in hello Azure portal</span></span> 

<span data-ttu-id="4d688-104">В функциях Azure приложения функция предоставляет контекст выполнения hello для отдельных функций.</span><span class="sxs-lookup"><span data-stu-id="4d688-104">In Azure Functions, a function app provides hello execution context for your individual functions.</span></span> <span data-ttu-id="4d688-105">Функции приложения поведения применяются функции tooall, размещаемую в приложении заданной функции.</span><span class="sxs-lookup"><span data-stu-id="4d688-105">Function app behaviors apply tooall functions hosted by a given function app.</span></span> <span data-ttu-id="4d688-106">В этом разделе описывается способ tooconfigure и управляйте своими приложениями функции hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4d688-106">This topic describes how tooconfigure and manage your function apps in hello Azure portal.</span></span>

<span data-ttu-id="4d688-107">toobegin перейдите toohello [портал Azure](http://portal.azure.com) и выполните вход tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="4d688-107">toobegin, go toohello [Azure portal](http://portal.azure.com) and sign in tooyour Azure account.</span></span> <span data-ttu-id="4d688-108">В строке поиска hello hello верхней части портала hello введите имя функции приложения hello и выберите его из списка hello.</span><span class="sxs-lookup"><span data-stu-id="4d688-108">In hello search bar at hello top of hello portal, type hello name of your function app and select it from hello list.</span></span> <span data-ttu-id="4d688-109">После выбора функции приложения, появится следующая страница приветствия:</span><span class="sxs-lookup"><span data-stu-id="4d688-109">After selecting your function app, you see hello following page:</span></span>

![Обзор функции приложения в hello портал Azure](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <span data-ttu-id="4d688-111"><a name="manage-app-service-settings"></a>Вкладка параметров приложения-функции</span><span class="sxs-lookup"><span data-stu-id="4d688-111"><a name="manage-app-service-settings"></a>Function app settings tab</span></span>

![Обзор функции приложения в hello портал Azure.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

<span data-ttu-id="4d688-113">Hello **параметры** вкладка —, где вы можете обновить версию среды выполнения функции hello, используемые приложением функции.</span><span class="sxs-lookup"><span data-stu-id="4d688-113">hello **Settings** tab is where you can update hello Functions runtime version used by your function app.</span></span> <span data-ttu-id="4d688-114">Также он служит для управления hello узла ключи, используемые toorestrict HTTP tooall функции для доступа к размещенным функция приложение hello.</span><span class="sxs-lookup"><span data-stu-id="4d688-114">It is also where you manage hello host keys used toorestrict HTTP access tooall functions hosted by hello function app.</span></span>

<span data-ttu-id="4d688-115">Компонент функции поддерживает планы размещения как для потребления, так и для службы приложений.</span><span class="sxs-lookup"><span data-stu-id="4d688-115">Functions supports both Consumption hosting and App Service hosting plans.</span></span> <span data-ttu-id="4d688-116">Дополнительные сведения см. в разделе [Выбор плана правильную службу hello для функций Azure](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="4d688-116">For more information, see [Choose hello correct service plan for Azure Functions](functions-scale.md).</span></span> <span data-ttu-id="4d688-117">Позволяет лучше прогнозировать в плане использования hello функций позволяет ограничить использование платформы, установив ежедневной квоты на использование в секундах гигабайт.</span><span class="sxs-lookup"><span data-stu-id="4d688-117">For better predictability in hello Consumption plan, Functions lets you limit platform usage by setting a daily usage quota, in gigabytes-seconds.</span></span> <span data-ttu-id="4d688-118">После достижения hello ежедневной квоты на использование функции приложение hello остановлена.</span><span class="sxs-lookup"><span data-stu-id="4d688-118">Once hello daily usage quota is reached, hello function app is stopped.</span></span> <span data-ttu-id="4d688-119">Функции приложения, остановлена в результате достижения hello тратит квоты можно будет снова включить из hello же контексте, что установление hello ежедневно тратит квоты.</span><span class="sxs-lookup"><span data-stu-id="4d688-119">A function app stopped as a result of reaching hello spending quota can be re-enabled from hello same context as establishing hello daily spending quota.</span></span> <span data-ttu-id="4d688-120">В разделе hello [функции Azure странице цен](http://azure.microsoft.com/pricing/details/functions/) подробные сведения о счете.</span><span class="sxs-lookup"><span data-stu-id="4d688-120">See hello [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on billing.</span></span>   

## <a name="platform-features-tab"></a><span data-ttu-id="4d688-121">Вкладка функций платформы</span><span class="sxs-lookup"><span data-stu-id="4d688-121">Platform features tab</span></span>

![Вкладка функций платформы для приложения-функции](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

<span data-ttu-id="4d688-123">Функции приложения выполняются и поддерживаются платформой hello службе приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="4d688-123">Function apps run in, and are maintained, by hello Azure App Service platform.</span></span> <span data-ttu-id="4d688-124">Таким образом ваши функции приложения имеют доступ toomost функции hello Azure core платформу веб-хостинга.</span><span class="sxs-lookup"><span data-stu-id="4d688-124">As such, your function apps have access toomost of hello features of Azure's core web hosting platform.</span></span> <span data-ttu-id="4d688-125">Hello **возможности платформы** вкладка — где доступ hello многие функции платформы службы приложений, можно использовать в приложениях функции hello.</span><span class="sxs-lookup"><span data-stu-id="4d688-125">hello **Platform features** tab is where you access hello many features of hello App Service platform that you can use in your function apps.</span></span> 

> [!NOTE]
> <span data-ttu-id="4d688-126">Не все функции службы приложений доступны при запуске приложения функции для плана размещения потребления hello.</span><span class="sxs-lookup"><span data-stu-id="4d688-126">Not all App Service features are available when a function app runs on hello Consumption hosting plan.</span></span>

<span data-ttu-id="4d688-127">Hello остальной части этого раздела основное внимание уделяется hello следующие функции службы приложений в hello портал Azure, которые удобно использовать для функции:</span><span class="sxs-lookup"><span data-stu-id="4d688-127">hello rest of this topic focuses on hello following App Service features in hello Azure portal that are useful for Functions:</span></span>

+ [<span data-ttu-id="4d688-128">Редактор службы приложений</span><span class="sxs-lookup"><span data-stu-id="4d688-128">App Service editor</span></span>](#editor)
+ [<span data-ttu-id="4d688-129">Параметры приложения</span><span class="sxs-lookup"><span data-stu-id="4d688-129">Application settings</span></span>](#settings) 
+ [<span data-ttu-id="4d688-130">Console</span><span class="sxs-lookup"><span data-stu-id="4d688-130">Console</span></span>](#console)
+ [<span data-ttu-id="4d688-131">Дополнительные инструменты (Kudu)</span><span class="sxs-lookup"><span data-stu-id="4d688-131">Advanced tools (Kudu)</span></span>](#kudu)
+ [<span data-ttu-id="4d688-132">Варианты развертывания</span><span class="sxs-lookup"><span data-stu-id="4d688-132">Deployment options</span></span>](#deployment)
+ [<span data-ttu-id="4d688-133">CORS</span><span class="sxs-lookup"><span data-stu-id="4d688-133">CORS</span></span>](#cors)
+ [<span data-ttu-id="4d688-134">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="4d688-134">Authentication</span></span>](#auth)
+ [<span data-ttu-id="4d688-135">Определение интерфейса API</span><span class="sxs-lookup"><span data-stu-id="4d688-135">API definition</span></span>](#swagger)

<span data-ttu-id="4d688-136">Дополнительные сведения о том, как toowork с параметрами приложения службы в разделе [настройки параметров службы приложения Azure](../app-service-web/web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4d688-136">For more information about how toowork with App Service settings, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).</span></span>

### <span data-ttu-id="4d688-137"><a name="editor"></a>Редактор службы приложений</span><span class="sxs-lookup"><span data-stu-id="4d688-137"><a name="editor"></a>App Service Editor</span></span>

| | |
|-|-|
| ![Редактор службы приложений для приложения-функции](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | <span data-ttu-id="4d688-139">Редактор служб приложения Hello является расширенный редактор через портал можно использовать toomodify JSON-файлов конфигурации и файлы кода одинаково.</span><span class="sxs-lookup"><span data-stu-id="4d688-139">hello App Service editor is an advanced in-portal editor that you can use toomodify JSON configuration files and code files alike.</span></span> <span data-ttu-id="4d688-140">При выборе этого параметра откроется отдельная вкладка браузера с базовым редактором.</span><span class="sxs-lookup"><span data-stu-id="4d688-140">Choosing this option launches a separate browser tab with a basic editor.</span></span> <span data-ttu-id="4d688-141">Это позволяет toointegrate с Git hello репозитория, выполнения и отладки кода, а также изменить параметры функции приложения.</span><span class="sxs-lookup"><span data-stu-id="4d688-141">This enables you toointegrate with hello Git repository, run and debug code, and modify function app settings.</span></span> <span data-ttu-id="4d688-142">Этот редактор предоставляет расширенные возможности разработки среду для функций по сравнению с колонкой приложения функции по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="4d688-142">This editor provides an enhanced development environment for your functions compared with hello default function app blade.</span></span>    |

![Редактор служб приложения Hello](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <span data-ttu-id="4d688-144"><a name="settings"></a>Параметры приложения</span><span class="sxs-lookup"><span data-stu-id="4d688-144"><a name="settings"></a>Application settings</span></span>

| | |
|-|-|
| ![Параметры приложения-функции](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | <span data-ttu-id="4d688-146">Службы приложений Hello **параметры приложения** колонка находится где требуется настроить и управлять версии framework, удаленная отладка, параметры приложения и строки подключения.</span><span class="sxs-lookup"><span data-stu-id="4d688-146">hello App Service **Application settings** blade is where you configure and manage framework versions, remote debugging, app settings, and connection strings.</span></span> <span data-ttu-id="4d688-147">При интеграции приложения-функции с Azure и сторонними службами соответствующие параметры можно изменить здесь.</span><span class="sxs-lookup"><span data-stu-id="4d688-147">When you integrate your function app with other Azure and third-party services, you can modify those settings here.</span></span> |

![Настройка параметров приложения](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <span data-ttu-id="4d688-149"><a name="console"></a>Консоль</span><span class="sxs-lookup"><span data-stu-id="4d688-149"><a name="console"></a>Console</span></span>

| | |
|-|-|
| ![Функция консоли приложения hello портал Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | <span data-ttu-id="4d688-151">консоль Hello в портал является средством идеальный разработчика при желании toointeract вместе с приложением функцию из командной строки hello.</span><span class="sxs-lookup"><span data-stu-id="4d688-151">hello in-portal console is an ideal developer tool when you prefer toointeract with your function app from hello command line.</span></span> <span data-ttu-id="4d688-152">Стандартные команды включают создание каталогов и файлов и навигацию по ним, а также выполнение пакетных файлов и сценариев.</span><span class="sxs-lookup"><span data-stu-id="4d688-152">Common commands include directory and file creation and navigation, as well as executing batch files and scripts.</span></span> |

![Консоль приложения-функции](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <span data-ttu-id="4d688-154"><a name="kudu"></a>Дополнительные инструменты (Kudu)</span><span class="sxs-lookup"><span data-stu-id="4d688-154"><a name="kudu"></a>Advanced tools (Kudu)</span></span>

| | |
|-|-|
| ![Функции приложения Kudu в hello портал Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | <span data-ttu-id="4d688-156">Hello мощные средства для службы приложений (также известный как Kudu) предоставляют доступ tooadvanced административные функции, функции приложения.</span><span class="sxs-lookup"><span data-stu-id="4d688-156">hello advanced tools for App Service (also known as Kudu) provide access tooadvanced administrative features of your function app.</span></span> <span data-ttu-id="4d688-157">С помощью Kudu можно управлять системными сведениями, параметрами приложения, переменными среды, заголовками HTTP и переменными сервера.</span><span class="sxs-lookup"><span data-stu-id="4d688-157">From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables.</span></span> <span data-ttu-id="4d688-158">Можно также запустить **Kudu** путем просмотра toohello конечную точку SCM для функции приложения, например`https://<myfunctionapp>.scm.azurewebsites.net/`</span><span class="sxs-lookup"><span data-stu-id="4d688-158">You can also launch **Kudu** by browsing toohello SCM endpoint for your function app, like `https://<myfunctionapp>.scm.azurewebsites.net/`</span></span> |

![Настройка Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><span data-ttu-id="4d688-160"><a name="deployment">Варианты развертывания</span><span class="sxs-lookup"><span data-stu-id="4d688-160"><a name="deployment">Deployment options</span></span>

| | |
|-|-|
| ![Функция варианты развертывания приложений в hello портал Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | <span data-ttu-id="4d688-162">Компонент функции позволяет разрабатывать код функций на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="4d688-162">Functions lets you develop your function code on your local machine.</span></span> <span data-ttu-id="4d688-163">Затем вы можете передать tooAzure проекта приложения вашей локальной функции.</span><span class="sxs-lookup"><span data-stu-id="4d688-163">You can then upload your local function app project tooAzure.</span></span> <span data-ttu-id="4d688-164">В дополнение к этому tootraditional передачи FTP, функции позволяет развертывать с помощью решений популярных непрерывная интеграция, как GitHub, VSTS, Dropbox, Bitbucket и другие функции приложения.</span><span class="sxs-lookup"><span data-stu-id="4d688-164">In addition tootraditional FTP upload, Functions lets you deploy your function app using popular continuous integration solutions, like GitHub, VSTS, Dropbox, Bitbucket, and others.</span></span> <span data-ttu-id="4d688-165">Дополнительные сведения см. в статье [Непрерывное развертывание для функций Azure](functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="4d688-165">For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span> <span data-ttu-id="4d688-166">tooupload вручную с помощью FTP или local Git, вы также должны [настроить учетные данные развертывания](functions-continuous-deployment.md#credentials).</span><span class="sxs-lookup"><span data-stu-id="4d688-166">tooupload manually using FTP or local Git, you also must [configure your deployment credentials](functions-continuous-deployment.md#credentials).</span></span> |


### <span data-ttu-id="4d688-167"><a name="cors"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="4d688-167"><a name="cors"></a>CORS</span></span>

| | |
|-|-|
| ![Функции приложения CORS в hello портал Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | <span data-ttu-id="4d688-169">tooprevent выполнения вредоносного кода в службах, блоки службы приложений вызывает tooyour приложений-функций из внешних источников.</span><span class="sxs-lookup"><span data-stu-id="4d688-169">tooprevent malicious code execution in your services, App Service blocks calls tooyour function apps from external sources.</span></span> <span data-ttu-id="4d688-170">Функции поддерживает ресурсов независимо от источника (CORS) toolet определяют «список» допускается источников, из которых функций может принимать удаленные запросы для управления доступом.</span><span class="sxs-lookup"><span data-stu-id="4d688-170">Functions supports cross-origin resource sharing (CORS) toolet you define a "whitelist" of allowed origins from which your functions can accept remote requests.</span></span>  |

![Настройка CORS приложения-функции](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <span data-ttu-id="4d688-172"><a name="auth"></a>Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="4d688-172"><a name="auth"></a>Authentication</span></span>

| | |
|-|-|
| ![Проверка подлинности приложения функции в hello портал Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | <span data-ttu-id="4d688-174">Если функции используют триггер HTTP, можно потребовать, чтобы вызовы toofirst пройти проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="4d688-174">When functions use an HTTP trigger, you can require calls toofirst be authenticated.</span></span> <span data-ttu-id="4d688-175">Служба приложений поддерживает проверку подлинности Azure Active Directory и вход в систему с помощью поставщиков социальных сетей, таких как Facebook, Майкрософт и Twitter.</span><span class="sxs-lookup"><span data-stu-id="4d688-175">App Service supports Azure Active Directory authentication and sign in with social providers, such as Facebook, Microsoft, and Twitter.</span></span> <span data-ttu-id="4d688-176">Дополнительные сведения о настройке определенных поставщиков аутентификации см. в разделе [Проверка подлинности и авторизация в службе приложений Azure](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4d688-176">For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span> |

![Настройка проверки подлинности для приложения-функции](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <span data-ttu-id="4d688-178"><a name="swagger"></a>Определение интерфейса API</span><span class="sxs-lookup"><span data-stu-id="4d688-178"><a name="swagger"></a>API definition</span></span>

| | |
|-|-|
| ![Функция API приложения swagger определения в hello портал Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | <span data-ttu-id="4d688-180">Функции поддерживает Swagger toomore tooallow клиентам возможность использования функции активации HTTP.</span><span class="sxs-lookup"><span data-stu-id="4d688-180">Functions supports Swagger tooallow clients toomore easily consume your HTTP-triggered functions.</span></span> <span data-ttu-id="4d688-181">Дополнительные сведения о создании определений API с помощью Swagger см. в статье [Приступая к работе с приложениями API, ASP.NET и Swagger в службе приложений Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4d688-181">For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="4d688-182">Также можно использовать функции прокси-серверы toodefine одну область API для нескольких функций.</span><span class="sxs-lookup"><span data-stu-id="4d688-182">You can also use Functions Proxies toodefine a single API surface for multiple functions.</span></span> <span data-ttu-id="4d688-183">Дополнительные сведения см. в статье [Работа с прокси-серверами для функций Azure](functions-proxies.md).</span><span class="sxs-lookup"><span data-stu-id="4d688-183">For more information, see [Working with Azure Functions Proxies](functions-proxies.md).</span></span> |

![Настройка API приложения-функции](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a><span data-ttu-id="4d688-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4d688-185">Next steps</span></span>

+ [<span data-ttu-id="4d688-186">Настройка параметров службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="4d688-186">Configure Azure App Service Settings</span></span>](../app-service-web/web-sites-configure.md)
+ [<span data-ttu-id="4d688-187">Непрерывное развертывание для функций Azure</span><span class="sxs-lookup"><span data-stu-id="4d688-187">Continuous deployment for Azure Functions</span></span>](functions-continuous-deployment.md)



