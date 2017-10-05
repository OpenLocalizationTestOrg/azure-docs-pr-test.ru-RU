---
title: "Средство моделирования угроз Microsoft Azure | Документация Майкрософт"
description: "Узнайте обо всех функциях, доступных в средстве моделирования угроз."
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 621ff305d7e782f85eeaae6c3fb02031673549c6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="threat-modeling-tool-feature-overview"></a><span data-ttu-id="616ba-103">Общие сведения о функциях средства моделирования угроз</span><span class="sxs-lookup"><span data-stu-id="616ba-103">Threat Modeling Tool feature overview</span></span>

<span data-ttu-id="616ba-104">Мы рады, что вы решили использовать средство моделирования угроз для своих потребностей в этом направлении.</span><span class="sxs-lookup"><span data-stu-id="616ba-104">We are glad you chose to use the Threat Modeling Tool for your threat modeling needs!</span></span> <span data-ttu-id="616ba-105">Ознакомьтесь со статьей **[Начало работы со средством моделирования угроз](./azure-security-threat-modeling-tool-getting-started.md)**, если вы еще не сделали этого. В ней представлены основные понятия на эту тему.</span><span class="sxs-lookup"><span data-stu-id="616ba-105">If you haven’t done so, visit **[Getting Started with the Threat Modeling Tool](./azure-security-threat-modeling-tool-getting-started.md)** to learn the basics.</span></span>

> <span data-ttu-id="616ba-106">Наше средство часто обновляется, поэтому чаще проверяйте это руководство, чтобы узнать о последних функциях и улучшениях.</span><span class="sxs-lookup"><span data-stu-id="616ba-106">Our tool is updated often, so check this guide often to see our latest features and improvements.</span></span>

<span data-ttu-id="616ba-107">При нажатии кнопки Create a New Model (Создать модель) откроется пустая начальная страница, как на изображении ниже:</span><span class="sxs-lookup"><span data-stu-id="616ba-107">Clicking on the "Create a New Model" button opens a blank start page, similar to the image below:</span></span>

![Пустая начальная страница](./media/azure-security-threat-modeling-tool/tmtstart.png)

<span data-ttu-id="616ba-109">Используйте модель угрозы от нашей команды, созданную в примере в статье **[Начало работы со средством моделирования угроз](./azure-security-threat-modeling-tool-getting-started.md)**. Давайте просмотрим все функции, доступные в средстве сейчас.</span><span class="sxs-lookup"><span data-stu-id="616ba-109">Using the threat model created by our team in the **[Getting Started](./azure-security-threat-modeling-tool-getting-started.md)** example, let’s check out all the features available in the tool today.</span></span>

![Базовая модель рисков](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a><span data-ttu-id="616ba-111">Навигации</span><span class="sxs-lookup"><span data-stu-id="616ba-111">Navigation</span></span>

<span data-ttu-id="616ba-112">Прежде чем углубиться в изучение встроенных функций, рассмотрим основные компоненты средства.</span><span class="sxs-lookup"><span data-stu-id="616ba-112">Before diving into the built-in features, let’s go over the main components found in the tool</span></span>

### <a name="menu-items"></a><span data-ttu-id="616ba-113">Пункты меню</span><span class="sxs-lookup"><span data-stu-id="616ba-113">Menu items</span></span>

<span data-ttu-id="616ba-114">Возможности должны быть аналогичны возможностям других продуктов корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="616ba-114">The experience should be similar to other Microsoft products.</span></span> <span data-ttu-id="616ba-115">Начнем с рассмотрения пунктов меню верхнего уровня:</span><span class="sxs-lookup"><span data-stu-id="616ba-115">Let’s begin by going through the top-level menu items:</span></span>

![Пункты меню](./media/azure-security-threat-modeling-tool/menuitems.png)

| <span data-ttu-id="616ba-117">Метка</span><span class="sxs-lookup"><span data-stu-id="616ba-117">Label</span></span>                               | <span data-ttu-id="616ba-118">Сведения</span><span class="sxs-lookup"><span data-stu-id="616ba-118">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="616ba-119">**File**</span><span class="sxs-lookup"><span data-stu-id="616ba-119">**File**</span></span> | <ul><li><span data-ttu-id="616ba-120">Открытие, сохранение и закрытие файлов.</span><span class="sxs-lookup"><span data-stu-id="616ba-120">Open, Save and Close Files</span></span></li><li><span data-ttu-id="616ba-121">Учетные записи OneDrive для входа и выхода.</span><span class="sxs-lookup"><span data-stu-id="616ba-121">Sign In/Out of OneDrive accounts</span></span></li><li><span data-ttu-id="616ba-122">Предоставление общего доступа к ссылкам (просмотр и изменение).</span><span class="sxs-lookup"><span data-stu-id="616ba-122">Share Links (View + Edit)</span></span></li><li><span data-ttu-id="616ba-123">Просмотр сведений о файле.</span><span class="sxs-lookup"><span data-stu-id="616ba-123">View File Information</span></span></li><li><span data-ttu-id="616ba-124">Применение нового шаблона к имеющимся моделям.</span><span class="sxs-lookup"><span data-stu-id="616ba-124">Apply New Template to Existing Models</span></span></li></ul> |
| <span data-ttu-id="616ba-125">**Edit** (Изменение)</span><span class="sxs-lookup"><span data-stu-id="616ba-125">**Edit**</span></span> | <span data-ttu-id="616ba-126">Отмена, повтор, копирование, вставка и удаление.</span><span class="sxs-lookup"><span data-stu-id="616ba-126">Undo/redo actions, as well a copy, paste and delete</span></span> |
| <span data-ttu-id="616ba-127">**View** (Вид)</span><span class="sxs-lookup"><span data-stu-id="616ba-127">**View**</span></span> | <ul><li><span data-ttu-id="616ba-128">Переключение между представлениями **Analysis** (Анализ) и **Design** (Конструктор).</span><span class="sxs-lookup"><span data-stu-id="616ba-128">Switch between **Analysis** and **Design** views</span></span></li><li><span data-ttu-id="616ba-129">Открытие закрытых окон (например, наборы элементов, свойства элемента и сообщения)</span><span class="sxs-lookup"><span data-stu-id="616ba-129">Open closed windows (e.g.stencils, element properties and messages)</span></span></li><li><span data-ttu-id="616ba-130">Сброс макета до параметров по умолчанию</span><span class="sxs-lookup"><span data-stu-id="616ba-130">Reset layout to default settings</span></span></li></ul> |
| <span data-ttu-id="616ba-131">**Diagram** (Схема)</span><span class="sxs-lookup"><span data-stu-id="616ba-131">**Diagram**</span></span> | <span data-ttu-id="616ba-132">Добавление и удаление схем и перемещение по вкладкам схем</span><span class="sxs-lookup"><span data-stu-id="616ba-132">Add/Delete diagrams and navigate through “tabs” of diagrams</span></span> |
| <span data-ttu-id="616ba-133">**Отчеты**</span><span class="sxs-lookup"><span data-stu-id="616ba-133">**Reports**</span></span> | <span data-ttu-id="616ba-134">Создание отчетов HTML для совместного использования с другими пользователями</span><span class="sxs-lookup"><span data-stu-id="616ba-134">Create HTML reports to share with others</span></span> |
| <span data-ttu-id="616ba-135">**Help** (Справка)</span><span class="sxs-lookup"><span data-stu-id="616ba-135">**Help**</span></span> | <span data-ttu-id="616ba-136">Руководство по использованию средства</span><span class="sxs-lookup"><span data-stu-id="616ba-136">Guides to help you use the tool</span></span> |

<span data-ttu-id="616ba-137">Значки являются ярлыками для меню верхнего уровня:</span><span class="sxs-lookup"><span data-stu-id="616ba-137">The icons are shortcuts for the top-level menus:</span></span>

| <span data-ttu-id="616ba-138">Значок</span><span class="sxs-lookup"><span data-stu-id="616ba-138">Icon</span></span>                               | <span data-ttu-id="616ba-139">Сведения</span><span class="sxs-lookup"><span data-stu-id="616ba-139">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="616ba-140">**Open** (Открыть)</span><span class="sxs-lookup"><span data-stu-id="616ba-140">**Open**</span></span> | <span data-ttu-id="616ba-141">Открывает новый файл</span><span class="sxs-lookup"><span data-stu-id="616ba-141">Opens a new file</span></span> |
| <span data-ttu-id="616ba-142">**Сохранить**</span><span class="sxs-lookup"><span data-stu-id="616ba-142">**Save**</span></span> | <span data-ttu-id="616ba-143">Сохраняет текущий файл</span><span class="sxs-lookup"><span data-stu-id="616ba-143">Saves current file</span></span> |
| <span data-ttu-id="616ba-144">**Design** (Конструктор)</span><span class="sxs-lookup"><span data-stu-id="616ba-144">**Design**</span></span> | <span data-ttu-id="616ba-145">Позволяет перейти в представление конструктора, где можно создавать модели</span><span class="sxs-lookup"><span data-stu-id="616ba-145">Goes into design view, where you can create models</span></span> |
| <span data-ttu-id="616ba-146">**Анализ**</span><span class="sxs-lookup"><span data-stu-id="616ba-146">**Analyze**</span></span> | <span data-ttu-id="616ba-147">Показывает созданные угрозы и их свойства</span><span class="sxs-lookup"><span data-stu-id="616ba-147">Shows generated threats and their properties</span></span> |
| <span data-ttu-id="616ba-148">**Add Diagram** (Добавить схему)</span><span class="sxs-lookup"><span data-stu-id="616ba-148">**Add Diagram**</span></span> | <span data-ttu-id="616ba-149">Добавляет новую схему (аналогично новым вкладкам в Excel).</span><span class="sxs-lookup"><span data-stu-id="616ba-149">Adds new diagram (similar to new tabs in Excel)</span></span> |
| <span data-ttu-id="616ba-150">**Delete Diagram** (Удалить схему)</span><span class="sxs-lookup"><span data-stu-id="616ba-150">**Delete Diagram**</span></span> | <span data-ttu-id="616ba-151">Удаляет текущую схему</span><span class="sxs-lookup"><span data-stu-id="616ba-151">Deletes current diagram</span></span> |
| <span data-ttu-id="616ba-152">**Copy/Cut/Paste** ("Копировать", "Вырезать", "Вставить")</span><span class="sxs-lookup"><span data-stu-id="616ba-152">**Copy/Cut/Paste**</span></span> | <span data-ttu-id="616ba-153">Копирует, вырезает или вставляет элементы</span><span class="sxs-lookup"><span data-stu-id="616ba-153">Copies/cuts/pastes elements</span></span> |
| <span data-ttu-id="616ba-154">**Undo/Redo** ("Отменить", "Повторить")</span><span class="sxs-lookup"><span data-stu-id="616ba-154">**Undo/Redo**</span></span> | <span data-ttu-id="616ba-155">Отменяет и повторяет действия</span><span class="sxs-lookup"><span data-stu-id="616ba-155">Undoes/redoes actions</span></span> |
| <span data-ttu-id="616ba-156">**Zoom In/Zoom Out** ("Увеличить", "Уменьшить")</span><span class="sxs-lookup"><span data-stu-id="616ba-156">**Zoom In/Zoom Out**</span></span> | <span data-ttu-id="616ba-157">Масштабирование схемы для оптимального просмотра</span><span class="sxs-lookup"><span data-stu-id="616ba-157">Zooms in and out of the diagram for a better view</span></span> |
| <span data-ttu-id="616ba-158">**Отзывы и предложения**</span><span class="sxs-lookup"><span data-stu-id="616ba-158">**Feedback**</span></span> | <span data-ttu-id="616ba-159">Открывает форум MSDN</span><span class="sxs-lookup"><span data-stu-id="616ba-159">Opens the MSDN Forum</span></span> |

### <a name="canvas"></a><span data-ttu-id="616ba-160">Холст</span><span class="sxs-lookup"><span data-stu-id="616ba-160">Canvas</span></span>

<span data-ttu-id="616ba-161">Пространство, куда можно перетаскивать элементы.</span><span class="sxs-lookup"><span data-stu-id="616ba-161">The space where you drag and drop elements into.</span></span> <span data-ttu-id="616ba-162">Перетаскивание является самым быстрым и эффективным способом создания моделей.</span><span class="sxs-lookup"><span data-stu-id="616ba-162">Drag and drop is the quickest and most efficient way to build models.</span></span> <span data-ttu-id="616ba-163">Кроме того, можно щелкнуть правой кнопкой мыши и выбрать меню, которое добавляет универсальные версии используемых элементов, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="616ba-163">You may also right click and select from the menu, which adds generic versions of the elements you’re using, as shown below.</span></span>

#### <a name="dropping-the-stencil-on-the-canvas"></a><span data-ttu-id="616ba-164">Перенос набора элементов на холст</span><span class="sxs-lookup"><span data-stu-id="616ba-164">Dropping the stencil on the canvas</span></span>

![Перенос на холст](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-the-stencil"></a><span data-ttu-id="616ba-166">Щелчок набора элементов</span><span class="sxs-lookup"><span data-stu-id="616ba-166">Clicking on the stencil</span></span>

![Свойства элемента](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a><span data-ttu-id="616ba-168">Набор элементов</span><span class="sxs-lookup"><span data-stu-id="616ba-168">Stencils</span></span>

<span data-ttu-id="616ba-169">Здесь можно найти все наборы элементов, которые доступны для использования на основе выбранного шаблона.</span><span class="sxs-lookup"><span data-stu-id="616ba-169">Where you can find all stencils available to use based on the template selected.</span></span> <span data-ttu-id="616ba-170">Если не удается найти нужный элемент, попробуйте использовать другой шаблон или изменить его в соответствии со своими потребностями.</span><span class="sxs-lookup"><span data-stu-id="616ba-170">If you can’t find the right elements, try using another template, or modify one to fit your needs.</span></span> <span data-ttu-id="616ba-171">Как правило, можно найти сочетание категорий, похожих на представленные ниже:</span><span class="sxs-lookup"><span data-stu-id="616ba-171">Generally, you should be able to find a combination of categories like the ones below:</span></span>

| <span data-ttu-id="616ba-172">Имя набора элементов</span><span class="sxs-lookup"><span data-stu-id="616ba-172">Stencil Name</span></span>                               | <span data-ttu-id="616ba-173">Сведения</span><span class="sxs-lookup"><span data-stu-id="616ba-173">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="616ba-174">**Описание процесса**</span><span class="sxs-lookup"><span data-stu-id="616ba-174">**Process**</span></span> | <span data-ttu-id="616ba-175">Приложения, подключаемые модули браузера, потоки, виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="616ba-175">Applications, Browser Plugins, Threads, Virtual Machines</span></span> |
| <span data-ttu-id="616ba-176">**External Interactor** (Внешний элемент)</span><span class="sxs-lookup"><span data-stu-id="616ba-176">**External Interactor**</span></span> | <span data-ttu-id="616ba-177">Поставщики проверки подлинности, браузеры, пользователи, веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="616ba-177">Authentication Providers, Browsers, Users, Web Applications</span></span> |
| <span data-ttu-id="616ba-178">**Data Store** (Хранилище данных)</span><span class="sxs-lookup"><span data-stu-id="616ba-178">**Data Store**</span></span> | <span data-ttu-id="616ba-179">Кэш, хранилище, файлы конфигурации, базы данных, реестр.</span><span class="sxs-lookup"><span data-stu-id="616ba-179">Cache, Storage, Configuration Files, Databases, Registry</span></span> |
| <span data-ttu-id="616ba-180">**Поток данных**</span><span class="sxs-lookup"><span data-stu-id="616ba-180">**Data Flow**</span></span> | <span data-ttu-id="616ba-181">Двоичные файлы, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, именованный канал, RPC/DCOM, SMB, UDP</span><span class="sxs-lookup"><span data-stu-id="616ba-181">Binary, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, Named Pipe, RPC/DCOM, SMB, UDP</span></span> |
| <span data-ttu-id="616ba-182">**Trust Line/Border Boundary** ("Линия доверия", "Ограничение границы")</span><span class="sxs-lookup"><span data-stu-id="616ba-182">**Trust Line/Border Boundary**</span></span> | <span data-ttu-id="616ba-183">Корпоративные сети, Интернет, компьютер, песочница, режим пользователя или ядра</span><span class="sxs-lookup"><span data-stu-id="616ba-183">Corporate Networks, Internet, Machine, Sandbox, User/Kernel Mode</span></span> |

### <a name="notesmessages"></a><span data-ttu-id="616ba-184">Примечания и сообщения</span><span class="sxs-lookup"><span data-stu-id="616ba-184">Notes/Messages</span></span>

| <span data-ttu-id="616ba-185">Компонент</span><span class="sxs-lookup"><span data-stu-id="616ba-185">Component</span></span>                               | <span data-ttu-id="616ba-186">Сведения</span><span class="sxs-lookup"><span data-stu-id="616ba-186">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="616ba-187">**Сообщения**</span><span class="sxs-lookup"><span data-stu-id="616ba-187">**Messages**</span></span> | <span data-ttu-id="616ba-188">Внутренняя логика средства, которая оповещает пользователей каждый раз, когда возникает ошибка (например, нет потоков данных между элементами).</span><span class="sxs-lookup"><span data-stu-id="616ba-188">Internal tool logic that alerts users whenever there is an error, such as no data flows between elements</span></span> |
| <span data-ttu-id="616ba-189">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="616ba-189">**Notes**</span></span> | <span data-ttu-id="616ba-190">Примечания, добавляемые в файл инженерами вручную на протяжении всего процесса проектирования и проверки.</span><span class="sxs-lookup"><span data-stu-id="616ba-190">Manual notes added to the file by engineering teams throughout the design and review process</span></span> |

### <a name="element-properties"></a><span data-ttu-id="616ba-191">Свойства элемента</span><span class="sxs-lookup"><span data-stu-id="616ba-191">Element properties</span></span>

<span data-ttu-id="616ba-192">Они различаются в зависимости от выбранных элементов.</span><span class="sxs-lookup"><span data-stu-id="616ba-192">These vary by the elements selected.</span></span> <span data-ttu-id="616ba-193">Помимо границы доверия все остальные элементы содержат 3 общих параметра:</span><span class="sxs-lookup"><span data-stu-id="616ba-193">Apart from Trust Boundaries, all other elements contain 3 general selections:</span></span>

| <span data-ttu-id="616ba-194">Свойство элемента</span><span class="sxs-lookup"><span data-stu-id="616ba-194">Element Property</span></span>                               | <span data-ttu-id="616ba-195">Сведения</span><span class="sxs-lookup"><span data-stu-id="616ba-195">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="616ba-196">**Имя**</span><span class="sxs-lookup"><span data-stu-id="616ba-196">**Name**</span></span> | <span data-ttu-id="616ba-197">Полезно для именования процессов, хранилищ, элементов и потоков, чтобы облегчить их распознавание.</span><span class="sxs-lookup"><span data-stu-id="616ba-197">Useful for naming your processes, stores, interactors and flows to be easily recognized</span></span> |
| <span data-ttu-id="616ba-198">**Out of Scope** (Вывод за область)</span><span class="sxs-lookup"><span data-stu-id="616ba-198">**Out of Scope**</span></span> | <span data-ttu-id="616ba-199">Если этот параметр выбран, элемент изымается из матрицы создания угроз (не рекомендуется).</span><span class="sxs-lookup"><span data-stu-id="616ba-199">If selected, the element is taken out of the threat generation matrix (not recommended)</span></span> |
| <span data-ttu-id="616ba-200">**Reason for Out of Scope** (Причина для вывода за область)</span><span class="sxs-lookup"><span data-stu-id="616ba-200">**Reason for Out of Scope**</span></span> | <span data-ttu-id="616ba-201">Поле для обоснования, чтобы сообщить пользователям, почему выбран вывод за область.</span><span class="sxs-lookup"><span data-stu-id="616ba-201">Justification field to let users know why out of scope was selected</span></span> |

<span data-ttu-id="616ba-202">Свойства изменяются в каждой категории элементов.</span><span class="sxs-lookup"><span data-stu-id="616ba-202">Properties are changed under each element category.</span></span> <span data-ttu-id="616ba-203">Щелкните каждый элемент для проверки доступных параметров или откройте шаблон, чтобы получить дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="616ba-203">Click on each element to inspect the available options, or open the template to learn more.</span></span> <span data-ttu-id="616ba-204">Давайте рассмотрим функции.</span><span class="sxs-lookup"><span data-stu-id="616ba-204">Let’s get into the features.</span></span>

## <a name="welcome-screen"></a><span data-ttu-id="616ba-205">Экран приветствия</span><span class="sxs-lookup"><span data-stu-id="616ba-205">Welcome screen</span></span>

<span data-ttu-id="616ba-206">Экран приветствия — это первое, что отображается при открытии приложения.</span><span class="sxs-lookup"><span data-stu-id="616ba-206">The welcome screen is the first thing you see when you open the app.</span></span>

### <a name="open-a-model"></a><span data-ttu-id="616ba-207">Открытие модели</span><span class="sxs-lookup"><span data-stu-id="616ba-207">Open A model</span></span>

<span data-ttu-id="616ba-208">При наведении курсора мыши на кнопку Open a Model (Открыть модель) отобразится 2 скрытых параметра: Open From this Computer (Открыть на этом компьютере) и Open from OneDrive (Открыть в OneDrive).</span><span class="sxs-lookup"><span data-stu-id="616ba-208">Hovering over “Open a Model” button shows you 2 hidden options: “Open From this Computer” and “Open from OneDrive.”</span></span> <span data-ttu-id="616ba-209">Первый открывает экран "Открытие файла", а второй вызывает процесс входа в OneDrive, позволяя выбрать папки и файлы после успешной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="616ba-209">The first opens the File Open screen, while the second takes you through the sign in process for OneDrive, allowing you to pick folders and files after a successful authentication.</span></span>

![Открытие модели](./media/azure-security-threat-modeling-tool/openmodel.png)

![Открытие с компьютера или из OneDrive](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a><span data-ttu-id="616ba-212">Кнопка Feedback, suggestions and issues (Отзывы, предложения и проблемы)</span><span class="sxs-lookup"><span data-stu-id="616ba-212">Feedback, suggestions and issues</span></span>

<span data-ttu-id="616ba-213">При выборе этого параметра вы перейдете на форум MSDN для средств SDL.</span><span class="sxs-lookup"><span data-stu-id="616ba-213">Selecting this option will take you to the MSDN Forums for SDL Tools.</span></span> <span data-ttu-id="616ba-214">Это отличный способ узнать мнение других пользователей об этом средстве, включая способы решения проблем и новые идеи.</span><span class="sxs-lookup"><span data-stu-id="616ba-214">It’s a great way to check out what other people are saying about the tool, including workarounds and new ideas.</span></span>

![Отзыв](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a><span data-ttu-id="616ba-216">Конструктор</span><span class="sxs-lookup"><span data-stu-id="616ba-216">Design view</span></span>

<span data-ttu-id="616ba-217">При каждом открытии или создании модели вы будете переходить в конструктор.</span><span class="sxs-lookup"><span data-stu-id="616ba-217">Whenever you open or create a new model, you’ll be taken to the design view.</span></span>

### <a name="adding-elements"></a><span data-ttu-id="616ba-218">Добавление элементов</span><span class="sxs-lookup"><span data-stu-id="616ba-218">Adding elements</span></span>

<span data-ttu-id="616ba-219">Есть 2 способа добавления элементов в сетку:</span><span class="sxs-lookup"><span data-stu-id="616ba-219">There are 2 ways to add elements on the grid:</span></span>

- <span data-ttu-id="616ba-220">**Перетаскивание.** Перетащите нужный элемент в сетку, а затем используйте свойства элемента для предоставления дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="616ba-220">**Drag and Drop** – drag the desired element to the grid, then use the element properties to provide additional information.</span></span>
- <span data-ttu-id="616ba-221">**Щелчок правой кнопкой мыши.** Щелкните правой кнопкой мыши в любой части сетки и выберите раскрывающееся меню.</span><span class="sxs-lookup"><span data-stu-id="616ba-221">**Right Click** – right click anywhere on the grid and select from the dropdown menu.</span></span> <span data-ttu-id="616ba-222">Универсальное представление этого элемента отобразится на экране.</span><span class="sxs-lookup"><span data-stu-id="616ba-222">A generic representation of that element will appear on the screen.</span></span>

### <a name="connecting-elements"></a><span data-ttu-id="616ba-223">Подключение элементов</span><span class="sxs-lookup"><span data-stu-id="616ba-223">Connecting elements</span></span>

<span data-ttu-id="616ba-224">Есть 2 способа подключения элементов в средстве:</span><span class="sxs-lookup"><span data-stu-id="616ba-224">There are 2 ways to connect elements in the tool:</span></span>

- <span data-ttu-id="616ba-225">**Перетаскивание.** Перетащите нужный поток данных на сетку и соедините оба конца с соответствующими элементами.</span><span class="sxs-lookup"><span data-stu-id="616ba-225">**Drag and Drop** – drag the desired dataflow to the grid, and connect both ends to the appropriate elements.</span></span>
- <span data-ttu-id="616ba-226">**Щелчок и клавиша SHIFT.** Щелкните первый элемент (отправляющий данные), нажмите и удерживайте клавишу SHIFT, а затем выберите второй элемент (получающий данные).</span><span class="sxs-lookup"><span data-stu-id="616ba-226">**Click + Shift** – click on the first element (sending data), press and hold the Shift key, then select the second element (receiving data).</span></span> <span data-ttu-id="616ba-227">Щелкните правой кнопкой мыши и выберите "Подключение".</span><span class="sxs-lookup"><span data-stu-id="616ba-227">Right click, and select “Connect.”</span></span> <span data-ttu-id="616ba-228">При использовании двунаправленного потока данных порядок не столь важен.</span><span class="sxs-lookup"><span data-stu-id="616ba-228">If you’re using a bi-directional dataflow, the order is not as important.</span></span>

### <a name="properties"></a><span data-ttu-id="616ba-229">Свойства</span><span class="sxs-lookup"><span data-stu-id="616ba-229">Properties</span></span>

<span data-ttu-id="616ba-230">При выборе этого параметра отображаются все свойства, которые могут быть изменены в наборах элементов, размещенных на схеме.</span><span class="sxs-lookup"><span data-stu-id="616ba-230">Shows all the properties that can be modified on the stencils placed in the diagram.</span></span> <span data-ttu-id="616ba-231">Чтобы увидеть свойства, щелкните набор элементов и информация будет заполнена соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="616ba-231">To see the properties, just click on the stencil and the information will be populated accordingly.</span></span> <span data-ttu-id="616ba-232">В приведенном ниже примере показывается набор элементов Database до и после перетаскивания на схему:</span><span class="sxs-lookup"><span data-stu-id="616ba-232">The example below shows before and after a "Database" stencil is dragged onto the diagram:</span></span>

#### <a name="before"></a><span data-ttu-id="616ba-233">До</span><span class="sxs-lookup"><span data-stu-id="616ba-233">Before</span></span>

![До](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a><span data-ttu-id="616ba-235">после</span><span class="sxs-lookup"><span data-stu-id="616ba-235">After</span></span>

![после](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a><span data-ttu-id="616ba-237">Сообщения</span><span class="sxs-lookup"><span data-stu-id="616ba-237">Messages</span></span>

<span data-ttu-id="616ba-238">Если при создании модели угрозы вы забыли подключить потоки данных к элементам, окно сообщения уведомит вас о необходимости сделать это. Его можно пропустить или следовать инструкциям для устранения проблемы.</span><span class="sxs-lookup"><span data-stu-id="616ba-238">If you create a threat model and forget to connect data flows to elements, the message window notifies you to act. You can choose to ignore it or follow the instructions to fix the issue.</span></span> 

![Сообщения](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a><span data-ttu-id="616ba-240">Примечания</span><span class="sxs-lookup"><span data-stu-id="616ba-240">Notes</span></span>

<span data-ttu-id="616ba-241">Если переключиться с вкладки "Сообщения" на "Уведомления", можно добавлять заметки к схеме, чтобы ничего не упустить.</span><span class="sxs-lookup"><span data-stu-id="616ba-241">Switching tabs from Messages to Notes allows you to add notes to your diagram to capture all your thoughts</span></span>

## <a name="analysis-view"></a><span data-ttu-id="616ba-242">Представление "Анализ"</span><span class="sxs-lookup"><span data-stu-id="616ba-242">Analysis view</span></span>

<span data-ttu-id="616ba-243">Создав схему, переключитесь на представление "Анализ". Для этого перейдите к параметрам в верхнем меню и выберите увеличительное стекло рядом с палитрой для рисования.</span><span class="sxs-lookup"><span data-stu-id="616ba-243">Once you're done building your diagram, switch over to analysis view by going to the top menu selections and choosing the magnifying glass next to the paint palette.</span></span>

![Представление "Анализ"](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a><span data-ttu-id="616ba-245">Выбор созданной угрозы</span><span class="sxs-lookup"><span data-stu-id="616ba-245">Generated threat selection</span></span>

<span data-ttu-id="616ba-246">Щелкнув угрозу, можно использовать три уникальные функции:</span><span class="sxs-lookup"><span data-stu-id="616ba-246">When you click on a threat, you can leverage three unique functions:</span></span>

| <span data-ttu-id="616ba-247">Функция</span><span class="sxs-lookup"><span data-stu-id="616ba-247">Feature</span></span>                               | <span data-ttu-id="616ba-248">Сведения</span><span class="sxs-lookup"><span data-stu-id="616ba-248">Info</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="616ba-249">**Индикатор прочитанного**</span><span class="sxs-lookup"><span data-stu-id="616ba-249">**Read Indicator**</span></span> | <p><span data-ttu-id="616ba-250">Угроза будет помечена как прочитанная, что поможет вам легко отслеживать просмотренные элементы.</span><span class="sxs-lookup"><span data-stu-id="616ba-250">Threat is now marked as read, which can easily help you keep track of the items you already went through</span></span></p><p>![Индикатор прочитанного и непрочитанного](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| <span data-ttu-id="616ba-252">**Фокус на взаимодействии**</span><span class="sxs-lookup"><span data-stu-id="616ba-252">**Interaction Focus**</span></span> | <p><span data-ttu-id="616ba-253">На схеме выделяется взаимодействие, которое принадлежит этой угрозе.</span><span class="sxs-lookup"><span data-stu-id="616ba-253">Interaction in the diagram belonging to that threat is highlighted</span></span></p><p>![Фокус на взаимодействии](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| <span data-ttu-id="616ba-255">**Свойства угрозы**</span><span class="sxs-lookup"><span data-stu-id="616ba-255">**Threat Properties**</span></span> | <p><span data-ttu-id="616ba-256">Дополнительные сведения об угрозах заполняются в окне свойств угроз.</span><span class="sxs-lookup"><span data-stu-id="616ba-256">Additional information about the threat is populated in the threat properties window</span></span></p><p>![Свойства угрозы](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a><span data-ttu-id="616ba-258">Изменение приоритета</span><span class="sxs-lookup"><span data-stu-id="616ba-258">Priority change</span></span>

<span data-ttu-id="616ba-259">При изменении уровня приоритета каждой созданной угрозы также изменяются их цвета, чтобы упростить идентификацию угроз с высоким, средним и низким приоритетом.</span><span class="sxs-lookup"><span data-stu-id="616ba-259">Changing the priority level of each generated threat also changes their colors to make it easy to identify high, medium and low priority threats.</span></span>

![Изменение приоритета](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a><span data-ttu-id="616ba-261">Изменяемые поля свойств угроз.</span><span class="sxs-lookup"><span data-stu-id="616ba-261">Threat properties editable fields</span></span>

<span data-ttu-id="616ba-262">Как показано на приведенном выше рисунке, пользователи могут изменять данные, созданные средством, а также добавлять сведения в некоторые поля, такие как обоснование.</span><span class="sxs-lookup"><span data-stu-id="616ba-262">As seen in the image above, users can change the information generated by the tool an also add information to certain fields, such as justification.</span></span> <span data-ttu-id="616ba-263">Эти поля создаются шаблоном, поэтому, если необходима дополнительная информация для каждой угрозы, рекомендуется вносить изменения.</span><span class="sxs-lookup"><span data-stu-id="616ba-263">These fields are generated by the template, so if you need more information for each threat, you're encouraged to make modifications.</span></span>

![Свойства угрозы](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a><span data-ttu-id="616ba-265">Отчеты</span><span class="sxs-lookup"><span data-stu-id="616ba-265">Reports</span></span>

<span data-ttu-id="616ba-266">Изменив приоритеты и обновив состояние каждой созданной угрозы, вы можете сохранить файл и/или распечатать отчет, перейдя в раздел "Отчет", а затем выбрав пункт Create Full Report (Создать полный отчет).</span><span class="sxs-lookup"><span data-stu-id="616ba-266">Once you're done changing priorities and updating the status of each generated threat, you can save the file and/or print out a report by going to "Report" and then "Create Full Report."</span></span> <span data-ttu-id="616ba-267">Вам будет предложено назвать отчет. После этого отобразится подобный экран:</span><span class="sxs-lookup"><span data-stu-id="616ba-267">You'll be asked to name the report, and once you do, you should see something similar to the image below:</span></span>

![Отчет](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a><span data-ttu-id="616ba-269">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="616ba-269">Next steps</span></span>

<span data-ttu-id="616ba-270">Чтобы разместить шаблон для сообщества, перейдите на нашу станицу **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**.</span><span class="sxs-lookup"><span data-stu-id="616ba-270">To contribute a template for the community, please go to our **[GitHub](https://github.com/Microsoft/threat-modeling-templates)** page.</span></span> <span data-ttu-id="616ba-271">**[Скачайте](https://aka.ms/tmtpreview)** средство, чтобы начать работу уже сегодня.</span><span class="sxs-lookup"><span data-stu-id="616ba-271">**[Download](https://aka.ms/tmtpreview)** the tool to get started today.</span></span>
