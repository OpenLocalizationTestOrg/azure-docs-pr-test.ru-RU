---
title: "Настройка параметров приложения-функции Azure | Документация Майкрософт"
description: "Узнайте, как настроить параметры приложения-функции Azure."
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
ms.openlocfilehash: 3b23011f66592151d517d61bf806da8743f38e03
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-manage-a-function-app-in-the-azure-portal"></a><span data-ttu-id="ed778-103">Управление приложением-функцией на портале Azure</span><span class="sxs-lookup"><span data-stu-id="ed778-103">How to manage a function app in the Azure portal</span></span> 

<span data-ttu-id="ed778-104">В функциях Azure приложение-функция предоставляет контекст выполнения для отдельных функций.</span><span class="sxs-lookup"><span data-stu-id="ed778-104">In Azure Functions, a function app provides the execution context for your individual functions.</span></span> <span data-ttu-id="ed778-105">Поведение приложения-функции применяется ко всем содержащимся в нем функциям.</span><span class="sxs-lookup"><span data-stu-id="ed778-105">Function app behaviors apply to all functions hosted by a given function app.</span></span> <span data-ttu-id="ed778-106">Эта статья описывает настройку приложений-функций и управление ими на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ed778-106">This topic describes how to configure and manage your function apps in the Azure portal.</span></span>

<span data-ttu-id="ed778-107">Для начала перейдите на [портал Azure](http://portal.azure.com) и войдите, используя свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="ed778-107">To begin, go to the [Azure portal](http://portal.azure.com) and sign in to your Azure account.</span></span> <span data-ttu-id="ed778-108">На панели поиска в верхней части портала введите имя приложения-функции и выберите его в списке.</span><span class="sxs-lookup"><span data-stu-id="ed778-108">In the search bar at the top of the portal, type the name of your function app and select it from the list.</span></span> <span data-ttu-id="ed778-109">После выбора приложения-функции появляется следующая страница:</span><span class="sxs-lookup"><span data-stu-id="ed778-109">After selecting your function app, you see the following page:</span></span>

![Обзор приложения-функции на портале Azure](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <span data-ttu-id="ed778-111"><a name="manage-app-service-settings"></a>Вкладка параметров приложения-функции</span><span class="sxs-lookup"><span data-stu-id="ed778-111"><a name="manage-app-service-settings"></a>Function app settings tab</span></span>

![Обзор приложения-функции на портале Azure.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

<span data-ttu-id="ed778-113">На вкладке **Параметры** можно обновить версию среды выполнения функций, используемую приложением-функцией.</span><span class="sxs-lookup"><span data-stu-id="ed778-113">The **Settings** tab is where you can update the Functions runtime version used by your function app.</span></span> <span data-ttu-id="ed778-114">Кроме того, здесь также можно управлять ключами узла, используемыми для ограничения доступа по протоколу HTTP ко всем функциям, размещенным в приложении-функции.</span><span class="sxs-lookup"><span data-stu-id="ed778-114">It is also where you manage the host keys used to restrict HTTP access to all functions hosted by the function app.</span></span>

<span data-ttu-id="ed778-115">Компонент функции поддерживает планы размещения как для потребления, так и для службы приложений.</span><span class="sxs-lookup"><span data-stu-id="ed778-115">Functions supports both Consumption hosting and App Service hosting plans.</span></span> <span data-ttu-id="ed778-116">Сведения см. в статье [Выбор правильного плана обслуживания для функций Azure](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="ed778-116">For more information, see [Choose the correct service plan for Azure Functions](functions-scale.md).</span></span> <span data-ttu-id="ed778-117">Чтобы повысить прогнозируемость плана потребления, компонент функции позволяет ограничить использование платформы, задав квоту ежедневного использования в гигабайтах в секунду.</span><span class="sxs-lookup"><span data-stu-id="ed778-117">For better predictability in the Consumption plan, Functions lets you limit platform usage by setting a daily usage quota, in gigabytes-seconds.</span></span> <span data-ttu-id="ed778-118">По достижении квоты использования приложение-функция останавливается.</span><span class="sxs-lookup"><span data-stu-id="ed778-118">Once the daily usage quota is reached, the function app is stopped.</span></span> <span data-ttu-id="ed778-119">Приложение-функция, остановленное в связи с достижением квоты, можно снова включить из того же контекста, где устанавливается квота на дневной расход.</span><span class="sxs-lookup"><span data-stu-id="ed778-119">A function app stopped as a result of reaching the spending quota can be re-enabled from the same context as establishing the daily spending quota.</span></span> <span data-ttu-id="ed778-120">Сведения о выставлении счетов см. на [странице с ценами на Функции Azure](http://azure.microsoft.com/pricing/details/functions/).</span><span class="sxs-lookup"><span data-stu-id="ed778-120">See the [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on billing.</span></span>   

## <a name="platform-features-tab"></a><span data-ttu-id="ed778-121">Вкладка функций платформы</span><span class="sxs-lookup"><span data-stu-id="ed778-121">Platform features tab</span></span>

![Вкладка функций платформы для приложения-функции](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

<span data-ttu-id="ed778-123">Приложения-функции выполняются на платформе службы приложения Azure и обслуживаются ею.</span><span class="sxs-lookup"><span data-stu-id="ed778-123">Function apps run in, and are maintained, by the Azure App Service platform.</span></span> <span data-ttu-id="ed778-124">Поэтому они имеют доступ к большинству функций базовой платформы веб-хостинга Azure.</span><span class="sxs-lookup"><span data-stu-id="ed778-124">As such, your function apps have access to most of the features of Azure's core web hosting platform.</span></span> <span data-ttu-id="ed778-125">Вкладка **Функции платформы** предоставляет доступ ко многим функциям платформы службы приложений, которые можно использовать в приложениях-функциях.</span><span class="sxs-lookup"><span data-stu-id="ed778-125">The **Platform features** tab is where you access the many features of the App Service platform that you can use in your function apps.</span></span> 

> [!NOTE]
> <span data-ttu-id="ed778-126">Не все функции службы приложений доступны при выполнении приложения с планом размещения потребления.</span><span class="sxs-lookup"><span data-stu-id="ed778-126">Not all App Service features are available when a function app runs on the Consumption hosting plan.</span></span>

<span data-ttu-id="ed778-127">Ниже приводится более подробное описание следующих функций службы приложений на портале Azure, которые могут пригодиться при работе с функциями:</span><span class="sxs-lookup"><span data-stu-id="ed778-127">The rest of this topic focuses on the following App Service features in the Azure portal that are useful for Functions:</span></span>

+ [<span data-ttu-id="ed778-128">Редактор службы приложений</span><span class="sxs-lookup"><span data-stu-id="ed778-128">App Service editor</span></span>](#editor)
+ [<span data-ttu-id="ed778-129">Параметры приложения</span><span class="sxs-lookup"><span data-stu-id="ed778-129">Application settings</span></span>](#settings) 
+ [<span data-ttu-id="ed778-130">Console</span><span class="sxs-lookup"><span data-stu-id="ed778-130">Console</span></span>](#console)
+ [<span data-ttu-id="ed778-131">Дополнительные инструменты (Kudu)</span><span class="sxs-lookup"><span data-stu-id="ed778-131">Advanced tools (Kudu)</span></span>](#kudu)
+ [<span data-ttu-id="ed778-132">Варианты развертывания</span><span class="sxs-lookup"><span data-stu-id="ed778-132">Deployment options</span></span>](#deployment)
+ [<span data-ttu-id="ed778-133">CORS</span><span class="sxs-lookup"><span data-stu-id="ed778-133">CORS</span></span>](#cors)
+ [<span data-ttu-id="ed778-134">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="ed778-134">Authentication</span></span>](#auth)
+ [<span data-ttu-id="ed778-135">Определение интерфейса API</span><span class="sxs-lookup"><span data-stu-id="ed778-135">API definition</span></span>](#swagger)

<span data-ttu-id="ed778-136">Дополнительные сведения о работе с параметрами службы приложений см. в статье [Настройка параметров в службе приложений Azure](../app-service-web/web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ed778-136">For more information about how to work with App Service settings, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).</span></span>

### <span data-ttu-id="ed778-137"><a name="editor"></a>Редактор службы приложений</span><span class="sxs-lookup"><span data-stu-id="ed778-137"><a name="editor"></a>App Service Editor</span></span>

| | |
|-|-|
| ![Редактор службы приложений для приложения-функции](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | <span data-ttu-id="ed778-139">Редактор службы приложений — это расширенный редактор на портале, который можно использовать для изменения JSON-файлов конфигурации и файлов с кодом.</span><span class="sxs-lookup"><span data-stu-id="ed778-139">The App Service editor is an advanced in-portal editor that you can use to modify JSON configuration files and code files alike.</span></span> <span data-ttu-id="ed778-140">При выборе этого параметра откроется отдельная вкладка браузера с базовым редактором.</span><span class="sxs-lookup"><span data-stu-id="ed778-140">Choosing this option launches a separate browser tab with a basic editor.</span></span> <span data-ttu-id="ed778-141">Он позволяет выполнять интеграцию с репозиторием Git, запускать и отлаживать код и изменять параметры приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="ed778-141">This enables you to integrate with the Git repository, run and debug code, and modify function app settings.</span></span> <span data-ttu-id="ed778-142">Этот редактор предоставляет расширенную среду разработки для функций по сравнению со стандартной колонкой приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="ed778-142">This editor provides an enhanced development environment for your functions compared with the default function app blade.</span></span>    |

![Редактор службы приложений](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <span data-ttu-id="ed778-144"><a name="settings"></a>Параметры приложения</span><span class="sxs-lookup"><span data-stu-id="ed778-144"><a name="settings"></a>Application settings</span></span>

| | |
|-|-|
| ![Параметры приложения-функции](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | <span data-ttu-id="ed778-146">Колонка **Параметры приложения** службы приложений позволяет настроить версии платформы, удаленную отладку, параметры приложения и строки подключения.</span><span class="sxs-lookup"><span data-stu-id="ed778-146">The App Service **Application settings** blade is where you configure and manage framework versions, remote debugging, app settings, and connection strings.</span></span> <span data-ttu-id="ed778-147">При интеграции приложения-функции с Azure и сторонними службами соответствующие параметры можно изменить здесь.</span><span class="sxs-lookup"><span data-stu-id="ed778-147">When you integrate your function app with other Azure and third-party services, you can modify those settings here.</span></span> |

![Настройка параметров приложения](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <span data-ttu-id="ed778-149"><a name="console"></a>Консоль</span><span class="sxs-lookup"><span data-stu-id="ed778-149"><a name="console"></a>Console</span></span>

| | |
|-|-|
| ![Консоль приложения-функции на портале Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | <span data-ttu-id="ed778-151">Консоль на портале оптимально подходит разработчикам, желающим взаимодействовать с приложением-функцией из командной строки.</span><span class="sxs-lookup"><span data-stu-id="ed778-151">The in-portal console is an ideal developer tool when you prefer to interact with your function app from the command line.</span></span> <span data-ttu-id="ed778-152">Стандартные команды включают создание каталогов и файлов и навигацию по ним, а также выполнение пакетных файлов и сценариев.</span><span class="sxs-lookup"><span data-stu-id="ed778-152">Common commands include directory and file creation and navigation, as well as executing batch files and scripts.</span></span> |

![Консоль приложения-функции](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <span data-ttu-id="ed778-154"><a name="kudu"></a>Дополнительные инструменты (Kudu)</span><span class="sxs-lookup"><span data-stu-id="ed778-154"><a name="kudu"></a>Advanced tools (Kudu)</span></span>

| | |
|-|-|
| ![Kudu приложения-функции на портале Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | <span data-ttu-id="ed778-156">Дополнительные средства для службы приложений (которые также называются Kudu) предоставляют доступ к расширенным административным функциям для приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="ed778-156">The advanced tools for App Service (also known as Kudu) provide access to advanced administrative features of your function app.</span></span> <span data-ttu-id="ed778-157">С помощью Kudu можно управлять системными сведениями, параметрами приложения, переменными среды, заголовками HTTP и переменными сервера.</span><span class="sxs-lookup"><span data-stu-id="ed778-157">From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables.</span></span> <span data-ttu-id="ed778-158">Кроме того, можно также запустить **Kudu**, перейдя на конечную точку SCM для приложения-функции, например `https://<myfunctionapp>.scm.azurewebsites.net/`.</span><span class="sxs-lookup"><span data-stu-id="ed778-158">You can also launch **Kudu** by browsing to the SCM endpoint for your function app, like `https://<myfunctionapp>.scm.azurewebsites.net/`</span></span> |

![Настройка Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><span data-ttu-id="ed778-160"><a name="deployment">Варианты развертывания</span><span class="sxs-lookup"><span data-stu-id="ed778-160"><a name="deployment">Deployment options</span></span>

| | |
|-|-|
| ![Варианты развертывания приложения-функции на портале Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | <span data-ttu-id="ed778-162">Компонент функции позволяет разрабатывать код функций на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="ed778-162">Functions lets you develop your function code on your local machine.</span></span> <span data-ttu-id="ed778-163">Позднее вы можете передать локальный проект приложения-функции в Azure.</span><span class="sxs-lookup"><span data-stu-id="ed778-163">You can then upload your local function app project to Azure.</span></span> <span data-ttu-id="ed778-164">Кроме традиционной передачи по FTP, компонент функции позволяет развернуть приложение-функцию с помощью популярных решений непрерывной интеграции, таких как GitHub, VSTS, Dropbox, Bitbucket и др.</span><span class="sxs-lookup"><span data-stu-id="ed778-164">In addition to traditional FTP upload, Functions lets you deploy your function app using popular continuous integration solutions, like GitHub, VSTS, Dropbox, Bitbucket, and others.</span></span> <span data-ttu-id="ed778-165">Дополнительные сведения см. в статье [Непрерывное развертывание для функций Azure](functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="ed778-165">For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span> <span data-ttu-id="ed778-166">Чтобы отправить данные вручную с помощью FTP или локального Git, нужно [настроить учетные данные развертывания](functions-continuous-deployment.md#credentials).</span><span class="sxs-lookup"><span data-stu-id="ed778-166">To upload manually using FTP or local Git, you also must [configure your deployment credentials](functions-continuous-deployment.md#credentials).</span></span> |


### <span data-ttu-id="ed778-167"><a name="cors"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="ed778-167"><a name="cors"></a>CORS</span></span>

| | |
|-|-|
| ![CORS приложения-функции на портале Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | <span data-ttu-id="ed778-169">Чтобы предотвратить выполнение вредоносного кода в службах, служба приложений блокирует вызовы приложений-функций из внешних источников.</span><span class="sxs-lookup"><span data-stu-id="ed778-169">To prevent malicious code execution in your services, App Service blocks calls to your function apps from external sources.</span></span> <span data-ttu-id="ed778-170">Компонент функции поддерживает общий доступ к ресурсам независимо от источника (CORS), чтобы вы могли определить "список разрешений" из источников, откуда функции могут принимать удаленные запросы.</span><span class="sxs-lookup"><span data-stu-id="ed778-170">Functions supports cross-origin resource sharing (CORS) to let you define a "whitelist" of allowed origins from which your functions can accept remote requests.</span></span>  |

![Настройка CORS приложения-функции](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <span data-ttu-id="ed778-172"><a name="auth"></a>Проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="ed778-172"><a name="auth"></a>Authentication</span></span>

| | |
|-|-|
| ![Проверка подлинности приложения-функции на портале Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | <span data-ttu-id="ed778-174">Если функции используют триггер HTTP, можно настроить обязательную предварительную проверку подлинности для вызовов.</span><span class="sxs-lookup"><span data-stu-id="ed778-174">When functions use an HTTP trigger, you can require calls to first be authenticated.</span></span> <span data-ttu-id="ed778-175">Служба приложений поддерживает проверку подлинности Azure Active Directory и вход в систему с помощью поставщиков социальных сетей, таких как Facebook, Майкрософт и Twitter.</span><span class="sxs-lookup"><span data-stu-id="ed778-175">App Service supports Azure Active Directory authentication and sign in with social providers, such as Facebook, Microsoft, and Twitter.</span></span> <span data-ttu-id="ed778-176">Дополнительные сведения о настройке определенных поставщиков аутентификации см. в разделе [Проверка подлинности и авторизация в службе приложений Azure](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ed778-176">For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span> |

![Настройка проверки подлинности для приложения-функции](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <span data-ttu-id="ed778-178"><a name="swagger"></a>Определение интерфейса API</span><span class="sxs-lookup"><span data-stu-id="ed778-178"><a name="swagger"></a>API definition</span></span>

| | |
|-|-|
| ![Swagger для API приложения-функции на портале Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | <span data-ttu-id="ed778-180">Компонент функции поддерживает Swagger, что позволяет упростить использование функций, активируемых по HTTP, клиентами.</span><span class="sxs-lookup"><span data-stu-id="ed778-180">Functions supports Swagger to allow clients to more easily consume your HTTP-triggered functions.</span></span> <span data-ttu-id="ed778-181">Дополнительные сведения о создании определений API с помощью Swagger см. в статье [Приступая к работе с приложениями API, ASP.NET и Swagger в службе приложений Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ed778-181">For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="ed778-182">Можно также использовать прокси-серверы для функций, чтобы определить единую поверхность API для нескольких функций.</span><span class="sxs-lookup"><span data-stu-id="ed778-182">You can also use Functions Proxies to define a single API surface for multiple functions.</span></span> <span data-ttu-id="ed778-183">Дополнительные сведения см. в статье [Работа с прокси-серверами для функций Azure](functions-proxies.md).</span><span class="sxs-lookup"><span data-stu-id="ed778-183">For more information, see [Working with Azure Functions Proxies](functions-proxies.md).</span></span> |

![Настройка API приложения-функции](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a><span data-ttu-id="ed778-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ed778-185">Next steps</span></span>

+ [<span data-ttu-id="ed778-186">Настройка параметров службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="ed778-186">Configure Azure App Service Settings</span></span>](../app-service-web/web-sites-configure.md)
+ [<span data-ttu-id="ed778-187">Непрерывное развертывание для функций Azure</span><span class="sxs-lookup"><span data-stu-id="ed778-187">Continuous deployment for Azure Functions</span></span>](functions-continuous-deployment.md)



