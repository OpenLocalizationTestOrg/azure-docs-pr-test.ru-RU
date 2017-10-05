---
title: "Создание рабочих процессов на основе шаблонов с помощью Azure Logic Apps | Документация Майкрософт"
description: "Приступая к работе с шаблонами Azure Logic Apps. Как быстро создать рабочие процессы для подключения приложений и интеграции данных."
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 3656acfb-eefd-4e75-b5d2-73da56c424c9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: LADocs; klam
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 89272869f7dfaa34cbd2ad32d67dca0955e6158b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-workflow-using-a-pre-built-template-or-pattern-to-get-started-quickly"></a><span data-ttu-id="a5d1d-103">Настройка рабочего процесса с помощью встроенного шаблона или схемы для быстрого начала работы</span><span class="sxs-lookup"><span data-stu-id="a5d1d-103">Configure a workflow using a pre-built template or pattern to get started quickly</span></span>

## <a name="what-are-logic-app-templates"></a><span data-ttu-id="a5d1d-104">Что такое шаблоны приложений логики</span><span class="sxs-lookup"><span data-stu-id="a5d1d-104">What are logic app templates</span></span>
<span data-ttu-id="a5d1d-105">Шаблон приложения логики — это готовое приложение логики, с помощью которого можно быстро создать собственный рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-105">A logic app template is a pre-built logic app that you can use to quickly get started creating your own workflow.</span></span> 

<span data-ttu-id="a5d1d-106">Эти шаблоны позволяют обнаружить множество типов процессов, которые можно создать с помощью приложений логики.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-106">These templates are a good way to discover various patterns that can be built using logic apps.</span></span> <span data-ttu-id="a5d1d-107">Можно использовать их как есть или изменить их в соответствии с необходимым сценарием.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-107">You can either use these templates as-is or modify them to fit your scenario.</span></span>

## <a name="overview-of-available-templates"></a><span data-ttu-id="a5d1d-108">Общие сведения о доступных шаблонах</span><span class="sxs-lookup"><span data-stu-id="a5d1d-108">Overview of available templates</span></span>
<span data-ttu-id="a5d1d-109">Сейчас доступны разные шаблоны, опубликованные в платформе приложения логики.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-109">There are many available templates currently published in the logic app platform.</span></span> <span data-ttu-id="a5d1d-110">Ниже перечислены некоторые категории, а также тип используемого в них соединителя.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-110">Some example categories, as well as the type of connectors used in them, are listed below.</span></span>

### <a name="enterprise-cloud-templates"></a><span data-ttu-id="a5d1d-111">Шаблоны для корпоративных облачных решений</span><span class="sxs-lookup"><span data-stu-id="a5d1d-111">Enterprise cloud templates</span></span>
<span data-ttu-id="a5d1d-112">Шаблоны, которые интегрируют Dynamics CRM, Salesforce, Box, большие двоичные объекты Azure и другие соединители в соответствии с потребностями корпоративных облачных решений.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-112">Templates that integrate Dynamics CRM, Salesforce, Box, Azure Blob, and other connectors for your enterprise cloud needs.</span></span> <span data-ttu-id="a5d1d-113">С помощью этих шаблонов можно, например, упорядочить свои идеи и выполнить резервное копирование данных корпоративных файлов.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-113">Some examples of what can be done with these templates include organizing your leads and backing up your corporate file data.</span></span>

### <a name="enterprise-integration-pack-templates"></a><span data-ttu-id="a5d1d-114">Шаблоны для пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="a5d1d-114">Enterprise integration pack templates</span></span>
<span data-ttu-id="a5d1d-115">Конфигурации конвейеров VETER (проверка, извлечение, преобразование, расширение, маршрутизация), получение документа EDI X12 через AS2 и его преобразование в формат XML, а также обработка сообщений X12 и AS2.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-115">Configurations of VETER (validate, extract, transform, enrich, route) pipelines, receiving an X12 EDI document over AS2 and transforming it to XML, as well as X12 and AS2 message handling.</span></span>

### <a name="protocol-pattern-templates"></a><span data-ttu-id="a5d1d-116">Шаблоны для схем протоколов</span><span class="sxs-lookup"><span data-stu-id="a5d1d-116">Protocol pattern templates</span></span>
<span data-ttu-id="a5d1d-117">Эти шаблоны состоят из приложений логики, которые содержат контейнеры "запрос-ответ" HTTP, а также схемы интеграции FTP и SFTP.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-117">These templates consist of logic apps that contain protocol patterns such as request-response over HTTP as well as integrations across FTP and SFTP.</span></span> <span data-ttu-id="a5d1d-118">Их можно использовать отдельно или как основу для создания более сложных схем протоколов.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-118">Use these as they exist, or as a basis for creating more complex protocol patterns.</span></span>  

### <a name="personal-productivity-templates"></a><span data-ttu-id="a5d1d-119">Шаблоны для личной производительности</span><span class="sxs-lookup"><span data-stu-id="a5d1d-119">Personal productivity templates</span></span>
<span data-ttu-id="a5d1d-120">Шаблоны для повышения личной производительности включают шаблоны для настройки ежедневных напоминаний, преобразования важных рабочих элементов в списки дел, а также автоматизации и упрощения продолжительных задач до одноэтапных процедур, утверждаемых пользователем.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-120">Patterns to help improve personal productivity include templates that set daily reminders, turn important work items into to-do lists, and automate lengthy tasks down to a single user approval step.</span></span>

### <a name="consumer-cloud-templates"></a><span data-ttu-id="a5d1d-121">Шаблоны облака клиента</span><span class="sxs-lookup"><span data-stu-id="a5d1d-121">Consumer cloud templates</span></span>
<span data-ttu-id="a5d1d-122">Простые шаблоны, которые интегрируются со службами социальных сетей, включая Twitter и Slack, а также почтовыми службами. Эти шаблоны могут повышать эффективность маркетинговых программ, реализуемых через сети.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-122">Simple templates that integrate with social media services such as Twitter, Slack, and email, ultimately capable of strengthening social media marketing initiatives.</span></span> <span data-ttu-id="a5d1d-123">Сюда также относятся, например, шаблоны облачного копирования, которые повышают производительность благодаря экономии времени, которое обычно тратится на выполнение повторяющихся задач.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-123">These also include templates such as cloudy copying, which can help increase productivity by saving time spent on traditionally repetitive tasks.</span></span> 

## <a name="how-to-create-a-logic-app-using-a-template"></a><span data-ttu-id="a5d1d-124">Как создать приложение логики с помощью шаблона</span><span class="sxs-lookup"><span data-stu-id="a5d1d-124">How to create a logic app using a template</span></span>
<span data-ttu-id="a5d1d-125">Для начала перейдите в конструктор приложений логики.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-125">To get started using a logic app template, go into the logic app designer.</span></span> <span data-ttu-id="a5d1d-126">Если вы входите в конструктор, открывая существующее приложение логики, оно автоматически загружается в представление конструктора.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-126">If you're entering the designer by opening an existing logic app, the logic app automatically loads in your designer view.</span></span> <span data-ttu-id="a5d1d-127">Если же вы создаете приложение логики, отображается окно, показанное ниже.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-127">However, if you're creating a new logic app, you see the screen below.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template7.png)  

<span data-ttu-id="a5d1d-128">В этом окне можно выбрать запуск пустого приложения логики или предварительно созданного шаблона.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-128">From this screen, you can either choose to start with a blank logic app or a pre-built template.</span></span> <span data-ttu-id="a5d1d-129">Если вы выберете один из шаблонов, отобразится дополнительная информация.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-129">If you select one of the templates, you are provided with additional information.</span></span> <span data-ttu-id="a5d1d-130">В этом примере мы воспользуемся шаблоном *Когда в Dropbox создается новый файл, копировать его в OneDrive* .</span><span class="sxs-lookup"><span data-stu-id="a5d1d-130">In this example, we use the *When a new file is created in Dropbox, copy it to OneDrive* template.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template2.png)  

<span data-ttu-id="a5d1d-131">Выбрав шаблон, просто нажмите кнопку *Использовать этот шаблон*.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-131">If you choose to use the template, just select the *use this template* button.</span></span> <span data-ttu-id="a5d1d-132">Вам будет предложено войти в учетные записи на основании того, какие соединители использует шаблон.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-132">You'll be asked to sign in to your accounts based on which connectors the template utilizes.</span></span> <span data-ttu-id="a5d1d-133">Если вы уже подключились к соединителям, нажмите кнопку "Продолжить" (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="a5d1d-133">Or, if you've previously established a connection with these connectors, you can select continue as seen below.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template3.png)  

<span data-ttu-id="a5d1d-134">Когда вы подключитесь и нажмете кнопку *Продолжить*, приложение логики откроется в представлении конструктора.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-134">After establishing the connection and selecting *continue*, the logic app opens in designer view.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template4.png)  

<span data-ttu-id="a5d1d-135">В приведенном выше примере (как и в случае с другими шаблонами) некоторые обязательные поля свойств могут автоматически заполняться в соединителях. Но есть и поля, которые нужно заполнять специально, чтобы правильно развернуть приложение логики.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-135">In the example above, as is the case with many templates, some of the mandatory property fields may be filled out within the connectors; however, some might still require a value before being able to properly deploy the logic app.</span></span> <span data-ttu-id="a5d1d-136">Если вы пробуете выполнить развертывание, а некоторые поля не заполнены, вы получаете сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-136">If you try to deploy without entering some of the missing fields, you'll be notified with an error message.</span></span>

<span data-ttu-id="a5d1d-137">Чтобы вернуться в средство просмотра шаблона, нажмите кнопку *Шаблоны* на панели навигации вверху.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-137">If you wish to return to the template viewer, select the *Templates* button in the top navigation bar.</span></span> <span data-ttu-id="a5d1d-138">Когда вы возвращаетесь в это средство, все несохраненные изменения теряются.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-138">By switching back to the template viewer, you lose any unsaved progress.</span></span> <span data-ttu-id="a5d1d-139">Поэтому перед переключением появляется соответствующее предупреждение.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-139">Prior to switching back into template viewer, you'll see a warning message notifying you of this.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template5.png)  

## <a name="how-to-deploy-a-logic-app-created-from-a-template"></a><span data-ttu-id="a5d1d-140">Как развернуть приложение логики, созданное из шаблона</span><span class="sxs-lookup"><span data-stu-id="a5d1d-140">How to deploy a logic app created from a template</span></span>
<span data-ttu-id="a5d1d-141">Загрузите шаблон, внесите необходимые изменения и нажмите кнопку "Сохранить" в левом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-141">Once you have loaded your template and made any desired changes, select the save button in the upper left corner.</span></span> <span data-ttu-id="a5d1d-142">Так вы сохраните и опубликуете свое приложение логики.</span><span class="sxs-lookup"><span data-stu-id="a5d1d-142">This saves and publishes your logic app.</span></span>  
 ![](../../includes/media/app-service-logic-templates/template6.png)  

<span data-ttu-id="a5d1d-143">Сведения о добавлении дополнительных шагов в готовый шаблон приложения логики или внесении изменений в целом см. в статье [Создание нового приложения логики, подключающего службы SaaS](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a5d1d-143">If you would like more information on how to add more steps into an existing logic app template, or make edits in general, read more at [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

