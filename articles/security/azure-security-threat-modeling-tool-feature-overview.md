---
title: "aaaMicrosoft средства моделирования угроз - Azure | Документы Microsoft"
description: "Дополнительные сведения о все возможности hello hello средства моделирования угроз"
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
ms.openlocfilehash: f9ad5e623e7758063084cb7fc723c5735161a846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="threat-modeling-tool-feature-overview"></a><span data-ttu-id="8ae1e-103">Общие сведения о функциях средства моделирования угроз</span><span class="sxs-lookup"><span data-stu-id="8ae1e-103">Threat Modeling Tool feature overview</span></span>

<span data-ttu-id="8ae1e-104">Мы рады, что было выбрано hello toouse средства моделирования угроз для потребностей моделирования угроз!</span><span class="sxs-lookup"><span data-stu-id="8ae1e-104">We are glad you chose toouse hello Threat Modeling Tool for your threat modeling needs!</span></span> <span data-ttu-id="8ae1e-105">Если вы еще не сделали этого, посетите  **[Приступая к работе с hello средства моделирования угроз](./azure-security-threat-modeling-tool-getting-started.md)**  toolearn основы hello.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-105">If you haven’t done so, visit **[Getting Started with hello Threat Modeling Tool](./azure-security-threat-modeling-tool-getting-started.md)** toolearn hello basics.</span></span>

> <span data-ttu-id="8ae1e-106">Наши средства часто обновляется, поэтому это руководство по часто toosee нашей новейших возможностях и улучшениях.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-106">Our tool is updated often, so check this guide often toosee our latest features and improvements.</span></span>

<span data-ttu-id="8ae1e-107">Нажав на кнопку «Создать новую модель» hello откроется пустой начальной страницы, подобных изображений toohello ниже:</span><span class="sxs-lookup"><span data-stu-id="8ae1e-107">Clicking on hello "Create a New Model" button opens a blank start page, similar toohello image below:</span></span>

![Пустая начальная страница](./media/azure-security-threat-modeling-tool/tmtstart.png)

<span data-ttu-id="8ae1e-109">С помощью модели угроз hello созданных нашей команды в hello  **[Приступая к работе](./azure-security-threat-modeling-tool-getting-started.md)**  пример, давайте ознакомимся с использованием все возможности hello hello средство сегодня.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-109">Using hello threat model created by our team in hello **[Getting Started](./azure-security-threat-modeling-tool-getting-started.md)** example, let’s check out all hello features available in hello tool today.</span></span>

![Базовая модель рисков](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a><span data-ttu-id="8ae1e-111">Навигации</span><span class="sxs-lookup"><span data-stu-id="8ae1e-111">Navigation</span></span>

<span data-ttu-id="8ae1e-112">Прежде чем углубляться в hello встроенных функций, давайте посмотрим, hello основные компоненты, находящиеся в средство hello</span><span class="sxs-lookup"><span data-stu-id="8ae1e-112">Before diving into hello built-in features, let’s go over hello main components found in hello tool</span></span>

### <a name="menu-items"></a><span data-ttu-id="8ae1e-113">Пункты меню</span><span class="sxs-lookup"><span data-stu-id="8ae1e-113">Menu items</span></span>

<span data-ttu-id="8ae1e-114">взаимодействие Hello должен быть аналогичные продукты Microsoft tooother.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-114">hello experience should be similar tooother Microsoft products.</span></span> <span data-ttu-id="8ae1e-115">Давайте начнем через hello пункты меню верхнего уровня:</span><span class="sxs-lookup"><span data-stu-id="8ae1e-115">Let’s begin by going through hello top-level menu items:</span></span>

![Пункты меню](./media/azure-security-threat-modeling-tool/menuitems.png)

| <span data-ttu-id="8ae1e-117">Метка</span><span class="sxs-lookup"><span data-stu-id="8ae1e-117">Label</span></span>                               | <span data-ttu-id="8ae1e-118">Сведения</span><span class="sxs-lookup"><span data-stu-id="8ae1e-118">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="8ae1e-119">**File**</span><span class="sxs-lookup"><span data-stu-id="8ae1e-119">**File**</span></span> | <ul><li><span data-ttu-id="8ae1e-120">Открытие, сохранение и закрытие файлов.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-120">Open, Save and Close Files</span></span></li><li><span data-ttu-id="8ae1e-121">Учетные записи OneDrive для входа и выхода.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-121">Sign In/Out of OneDrive accounts</span></span></li><li><span data-ttu-id="8ae1e-122">Предоставление общего доступа к ссылкам (просмотр и изменение).</span><span class="sxs-lookup"><span data-stu-id="8ae1e-122">Share Links (View + Edit)</span></span></li><li><span data-ttu-id="8ae1e-123">Просмотр сведений о файле.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-123">View File Information</span></span></li><li><span data-ttu-id="8ae1e-124">Применение моделей tooExisting новый шаблон</span><span class="sxs-lookup"><span data-stu-id="8ae1e-124">Apply New Template tooExisting Models</span></span></li></ul> |
| <span data-ttu-id="8ae1e-125">**Edit** (Изменение)</span><span class="sxs-lookup"><span data-stu-id="8ae1e-125">**Edit**</span></span> | <span data-ttu-id="8ae1e-126">Отмена, повтор, копирование, вставка и удаление.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-126">Undo/redo actions, as well a copy, paste and delete</span></span> |
| <span data-ttu-id="8ae1e-127">**View** (Вид)</span><span class="sxs-lookup"><span data-stu-id="8ae1e-127">**View**</span></span> | <ul><li><span data-ttu-id="8ae1e-128">Переключение между представлениями **Analysis** (Анализ) и **Design** (Конструктор).</span><span class="sxs-lookup"><span data-stu-id="8ae1e-128">Switch between **Analysis** and **Design** views</span></span></li><li><span data-ttu-id="8ae1e-129">Открытие закрытых окон (например, наборы элементов, свойства элемента и сообщения)</span><span class="sxs-lookup"><span data-stu-id="8ae1e-129">Open closed windows (e.g.stencils, element properties and messages)</span></span></li><li><span data-ttu-id="8ae1e-130">Сброс параметров toodefault макета</span><span class="sxs-lookup"><span data-stu-id="8ae1e-130">Reset layout toodefault settings</span></span></li></ul> |
| <span data-ttu-id="8ae1e-131">**Diagram** (Схема)</span><span class="sxs-lookup"><span data-stu-id="8ae1e-131">**Diagram**</span></span> | <span data-ttu-id="8ae1e-132">Добавление и удаление схем и перемещение по вкладкам схем</span><span class="sxs-lookup"><span data-stu-id="8ae1e-132">Add/Delete diagrams and navigate through “tabs” of diagrams</span></span> |
| <span data-ttu-id="8ae1e-133">**Отчеты**</span><span class="sxs-lookup"><span data-stu-id="8ae1e-133">**Reports**</span></span> | <span data-ttu-id="8ae1e-134">Создание отчетов tooshare HTML с другими пользователями</span><span class="sxs-lookup"><span data-stu-id="8ae1e-134">Create HTML reports tooshare with others</span></span> |
| <span data-ttu-id="8ae1e-135">**Help** (Справка)</span><span class="sxs-lookup"><span data-stu-id="8ae1e-135">**Help**</span></span> | <span data-ttu-id="8ae1e-136">Используйте средство hello toohelp направляющие</span><span class="sxs-lookup"><span data-stu-id="8ae1e-136">Guides toohelp you use hello tool</span></span> |

<span data-ttu-id="8ae1e-137">сочетания клавиш для меню верхнего уровня hello используются значки Hello.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-137">hello icons are shortcuts for hello top-level menus:</span></span>

| <span data-ttu-id="8ae1e-138">Значок</span><span class="sxs-lookup"><span data-stu-id="8ae1e-138">Icon</span></span>                               | <span data-ttu-id="8ae1e-139">Сведения</span><span class="sxs-lookup"><span data-stu-id="8ae1e-139">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="8ae1e-140">**Open** (Открыть)</span><span class="sxs-lookup"><span data-stu-id="8ae1e-140">**Open**</span></span> | <span data-ttu-id="8ae1e-141">Открывает новый файл</span><span class="sxs-lookup"><span data-stu-id="8ae1e-141">Opens a new file</span></span> |
| <span data-ttu-id="8ae1e-142">**Сохранить**</span><span class="sxs-lookup"><span data-stu-id="8ae1e-142">**Save**</span></span> | <span data-ttu-id="8ae1e-143">Сохраняет текущий файл</span><span class="sxs-lookup"><span data-stu-id="8ae1e-143">Saves current file</span></span> |
| <span data-ttu-id="8ae1e-144">**Design** (Конструктор)</span><span class="sxs-lookup"><span data-stu-id="8ae1e-144">**Design**</span></span> | <span data-ttu-id="8ae1e-145">Позволяет перейти в представление конструктора, где можно создавать модели</span><span class="sxs-lookup"><span data-stu-id="8ae1e-145">Goes into design view, where you can create models</span></span> |
| <span data-ttu-id="8ae1e-146">**Анализ**</span><span class="sxs-lookup"><span data-stu-id="8ae1e-146">**Analyze**</span></span> | <span data-ttu-id="8ae1e-147">Показывает созданные угрозы и их свойства</span><span class="sxs-lookup"><span data-stu-id="8ae1e-147">Shows generated threats and their properties</span></span> |
| <span data-ttu-id="8ae1e-148">**Add Diagram** (Добавить схему)</span><span class="sxs-lookup"><span data-stu-id="8ae1e-148">**Add Diagram**</span></span> | <span data-ttu-id="8ae1e-149">Добавляет новую схему (аналогичный вкладок toonew в Excel)</span><span class="sxs-lookup"><span data-stu-id="8ae1e-149">Adds new diagram (similar toonew tabs in Excel)</span></span> |
| <span data-ttu-id="8ae1e-150">**Delete Diagram** (Удалить схему)</span><span class="sxs-lookup"><span data-stu-id="8ae1e-150">**Delete Diagram**</span></span> | <span data-ttu-id="8ae1e-151">Удаляет текущую схему</span><span class="sxs-lookup"><span data-stu-id="8ae1e-151">Deletes current diagram</span></span> |
| <span data-ttu-id="8ae1e-152">**Copy/Cut/Paste** ("Копировать", "Вырезать", "Вставить")</span><span class="sxs-lookup"><span data-stu-id="8ae1e-152">**Copy/Cut/Paste**</span></span> | <span data-ttu-id="8ae1e-153">Копирует, вырезает или вставляет элементы</span><span class="sxs-lookup"><span data-stu-id="8ae1e-153">Copies/cuts/pastes elements</span></span> |
| <span data-ttu-id="8ae1e-154">**Undo/Redo** ("Отменить", "Повторить")</span><span class="sxs-lookup"><span data-stu-id="8ae1e-154">**Undo/Redo**</span></span> | <span data-ttu-id="8ae1e-155">Отменяет и повторяет действия</span><span class="sxs-lookup"><span data-stu-id="8ae1e-155">Undoes/redoes actions</span></span> |
| <span data-ttu-id="8ae1e-156">**Zoom In/Zoom Out** ("Увеличить", "Уменьшить")</span><span class="sxs-lookup"><span data-stu-id="8ae1e-156">**Zoom In/Zoom Out**</span></span> | <span data-ttu-id="8ae1e-157">Устанавливает масштаб и из него hello схемы для удобства просмотра</span><span class="sxs-lookup"><span data-stu-id="8ae1e-157">Zooms in and out of hello diagram for a better view</span></span> |
| <span data-ttu-id="8ae1e-158">**Отзывы и предложения**</span><span class="sxs-lookup"><span data-stu-id="8ae1e-158">**Feedback**</span></span> | <span data-ttu-id="8ae1e-159">Открывает hello форум MSDN</span><span class="sxs-lookup"><span data-stu-id="8ae1e-159">Opens hello MSDN Forum</span></span> |

### <a name="canvas"></a><span data-ttu-id="8ae1e-160">Холст</span><span class="sxs-lookup"><span data-stu-id="8ae1e-160">Canvas</span></span>

<span data-ttu-id="8ae1e-161">Hello места, где можно путем перетаскивания элементов в.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-161">hello space where you drag and drop elements into.</span></span> <span data-ttu-id="8ae1e-162">Перетаскивание является быстрым hello и наиболее эффективный способ toobuild моделей.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-162">Drag and drop is hello quickest and most efficient way toobuild models.</span></span> <span data-ttu-id="8ae1e-163">Можно также правой кнопкой мыши и выберите из меню hello, которое добавляет универсальных версий элементов hello, которую вы используете, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-163">You may also right click and select from hello menu, which adds generic versions of hello elements you’re using, as shown below.</span></span>

#### <a name="dropping-hello-stencil-on-hello-canvas"></a><span data-ttu-id="8ae1e-164">Удаление hello набора элементов на холсте hello</span><span class="sxs-lookup"><span data-stu-id="8ae1e-164">Dropping hello stencil on hello canvas</span></span>

![Перенос на холст](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-hello-stencil"></a><span data-ttu-id="8ae1e-166">Щелкнув трафарета hello</span><span class="sxs-lookup"><span data-stu-id="8ae1e-166">Clicking on hello stencil</span></span>

![Свойства элемента](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a><span data-ttu-id="8ae1e-168">Набор элементов</span><span class="sxs-lookup"><span data-stu-id="8ae1e-168">Stencils</span></span>

<span data-ttu-id="8ae1e-169">Где можно найти все наборы элементов доступны toouse на основе выбранного шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-169">Where you can find all stencils available toouse based on hello template selected.</span></span> <span data-ttu-id="8ae1e-170">Если не удается найти hello вправо элементов, попробуйте использовать другой шаблон или измените один toofit вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-170">If you can’t find hello right elements, try using another template, or modify one toofit your needs.</span></span> <span data-ttu-id="8ae1e-171">В общем случае следует может toofind сочетание категории как hello из них ниже.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-171">Generally, you should be able toofind a combination of categories like hello ones below:</span></span>

| <span data-ttu-id="8ae1e-172">Имя набора элементов</span><span class="sxs-lookup"><span data-stu-id="8ae1e-172">Stencil Name</span></span>                               | <span data-ttu-id="8ae1e-173">Сведения</span><span class="sxs-lookup"><span data-stu-id="8ae1e-173">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="8ae1e-174">**Описание процесса**</span><span class="sxs-lookup"><span data-stu-id="8ae1e-174">**Process**</span></span> | <span data-ttu-id="8ae1e-175">Приложения, подключаемые модули браузера, потоки, виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="8ae1e-175">Applications, Browser Plugins, Threads, Virtual Machines</span></span> |
| <span data-ttu-id="8ae1e-176">**External Interactor** (Внешний элемент)</span><span class="sxs-lookup"><span data-stu-id="8ae1e-176">**External Interactor**</span></span> | <span data-ttu-id="8ae1e-177">Поставщики проверки подлинности, браузеры, пользователи, веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-177">Authentication Providers, Browsers, Users, Web Applications</span></span> |
| <span data-ttu-id="8ae1e-178">**Data Store** (Хранилище данных)</span><span class="sxs-lookup"><span data-stu-id="8ae1e-178">**Data Store**</span></span> | <span data-ttu-id="8ae1e-179">Кэш, хранилище, файлы конфигурации, базы данных, реестр.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-179">Cache, Storage, Configuration Files, Databases, Registry</span></span> |
| <span data-ttu-id="8ae1e-180">**Поток данных**</span><span class="sxs-lookup"><span data-stu-id="8ae1e-180">**Data Flow**</span></span> | <span data-ttu-id="8ae1e-181">Двоичные файлы, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, именованный канал, RPC/DCOM, SMB, UDP</span><span class="sxs-lookup"><span data-stu-id="8ae1e-181">Binary, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, Named Pipe, RPC/DCOM, SMB, UDP</span></span> |
| <span data-ttu-id="8ae1e-182">**Trust Line/Border Boundary** ("Линия доверия", "Ограничение границы")</span><span class="sxs-lookup"><span data-stu-id="8ae1e-182">**Trust Line/Border Boundary**</span></span> | <span data-ttu-id="8ae1e-183">Корпоративные сети, Интернет, компьютер, песочница, режим пользователя или ядра</span><span class="sxs-lookup"><span data-stu-id="8ae1e-183">Corporate Networks, Internet, Machine, Sandbox, User/Kernel Mode</span></span> |

### <a name="notesmessages"></a><span data-ttu-id="8ae1e-184">Примечания и сообщения</span><span class="sxs-lookup"><span data-stu-id="8ae1e-184">Notes/Messages</span></span>

| <span data-ttu-id="8ae1e-185">Компонент</span><span class="sxs-lookup"><span data-stu-id="8ae1e-185">Component</span></span>                               | <span data-ttu-id="8ae1e-186">Сведения</span><span class="sxs-lookup"><span data-stu-id="8ae1e-186">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="8ae1e-187">**Сообщения**</span><span class="sxs-lookup"><span data-stu-id="8ae1e-187">**Messages**</span></span> | <span data-ttu-id="8ae1e-188">Внутренняя логика средства, которая оповещает пользователей каждый раз, когда возникает ошибка (например, нет потоков данных между элементами).</span><span class="sxs-lookup"><span data-stu-id="8ae1e-188">Internal tool logic that alerts users whenever there is an error, such as no data flows between elements</span></span> |
| <span data-ttu-id="8ae1e-189">**Примечания**</span><span class="sxs-lookup"><span data-stu-id="8ae1e-189">**Notes**</span></span> | <span data-ttu-id="8ae1e-190">Вручную добавленные toohello примечаниях, участвующим полное hello разработки и процесс анализа</span><span class="sxs-lookup"><span data-stu-id="8ae1e-190">Manual notes added toohello file by engineering teams throughout hello design and review process</span></span> |

### <a name="element-properties"></a><span data-ttu-id="8ae1e-191">Свойства элемента</span><span class="sxs-lookup"><span data-stu-id="8ae1e-191">Element properties</span></span>

<span data-ttu-id="8ae1e-192">Они различаются в зависимости от выбранных элементов hello.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-192">These vary by hello elements selected.</span></span> <span data-ttu-id="8ae1e-193">Помимо границы доверия все остальные элементы содержат 3 общих параметра:</span><span class="sxs-lookup"><span data-stu-id="8ae1e-193">Apart from Trust Boundaries, all other elements contain 3 general selections:</span></span>

| <span data-ttu-id="8ae1e-194">Свойство элемента</span><span class="sxs-lookup"><span data-stu-id="8ae1e-194">Element Property</span></span>                               | <span data-ttu-id="8ae1e-195">Сведения</span><span class="sxs-lookup"><span data-stu-id="8ae1e-195">Details</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="8ae1e-196">**Имя**</span><span class="sxs-lookup"><span data-stu-id="8ae1e-196">**Name**</span></span> | <span data-ttu-id="8ae1e-197">Полезно для именования легко распознавать процессы, хранилища, посредники и потоки toobe</span><span class="sxs-lookup"><span data-stu-id="8ae1e-197">Useful for naming your processes, stores, interactors and flows toobe easily recognized</span></span> |
| <span data-ttu-id="8ae1e-198">**Out of Scope** (Вывод за область)</span><span class="sxs-lookup"><span data-stu-id="8ae1e-198">**Out of Scope**</span></span> | <span data-ttu-id="8ae1e-199">Если флажок установлен, hello элемента берется из hello угроз создания матрицы (не рекомендуется)</span><span class="sxs-lookup"><span data-stu-id="8ae1e-199">If selected, hello element is taken out of hello threat generation matrix (not recommended)</span></span> |
| <span data-ttu-id="8ae1e-200">**Reason for Out of Scope** (Причина для вывода за область)</span><span class="sxs-lookup"><span data-stu-id="8ae1e-200">**Reason for Out of Scope**</span></span> | <span data-ttu-id="8ae1e-201">При выравнивании по ширине поля toolet пользователи знают, почему был выбран вне области</span><span class="sxs-lookup"><span data-stu-id="8ae1e-201">Justification field toolet users know why out of scope was selected</span></span> |

<span data-ttu-id="8ae1e-202">Свойства изменяются в каждой категории элементов.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-202">Properties are changed under each element category.</span></span> <span data-ttu-id="8ae1e-203">Щелкните каждый элемент tooinspect hello параметрах, доступных или открыть дополнительные toolearn шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-203">Click on each element tooinspect hello available options, or open hello template toolearn more.</span></span> <span data-ttu-id="8ae1e-204">Давайте функциями, hello.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-204">Let’s get into hello features.</span></span>

## <a name="welcome-screen"></a><span data-ttu-id="8ae1e-205">Экран приветствия</span><span class="sxs-lookup"><span data-stu-id="8ae1e-205">Welcome screen</span></span>

<span data-ttu-id="8ae1e-206">экран приветствия Hello — hello первое, что вы видите можно, открыв приложение hello.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-206">hello welcome screen is hello first thing you see when you open hello app.</span></span>

### <a name="open-a-model"></a><span data-ttu-id="8ae1e-207">Открытие модели</span><span class="sxs-lookup"><span data-stu-id="8ae1e-207">Open A model</span></span>

<span data-ttu-id="8ae1e-208">При наведении курсора мыши на кнопку Open a Model (Открыть модель) отобразится 2 скрытых параметра: Open From this Computer (Открыть на этом компьютере) и Open from OneDrive (Открыть в OneDrive).</span><span class="sxs-lookup"><span data-stu-id="8ae1e-208">Hovering over “Open a Model” button shows you 2 hidden options: “Open From this Computer” and “Open from OneDrive.”</span></span> <span data-ttu-id="8ae1e-209">Hello сначала открывает Открытие файла экран приветствия, пока hello второй проводит пользователя через hello входа в систему для OneDrive, позволяя toopick папок и файлов после успешной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-209">hello first opens hello File Open screen, while hello second takes you through hello sign in process for OneDrive, allowing you toopick folders and files after a successful authentication.</span></span>

![Открытие модели](./media/azure-security-threat-modeling-tool/openmodel.png)

![Открытие с компьютера или из OneDrive](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a><span data-ttu-id="8ae1e-212">Кнопка Feedback, suggestions and issues (Отзывы, предложения и проблемы)</span><span class="sxs-lookup"><span data-stu-id="8ae1e-212">Feedback, suggestions and issues</span></span>

<span data-ttu-id="8ae1e-213">При выборе этого параметра вы перейдете toohello форумы MSDN для средств SDL.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-213">Selecting this option will take you toohello MSDN Forums for SDL Tools.</span></span> <span data-ttu-id="8ae1e-214">Это отличный способ toocheck, что другие пользователи говорят о hello инструмента, включая способы решения проблем и идеи.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-214">It’s a great way toocheck out what other people are saying about hello tool, including workarounds and new ideas.</span></span>

![Отзыв](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a><span data-ttu-id="8ae1e-216">Конструктор</span><span class="sxs-lookup"><span data-stu-id="8ae1e-216">Design view</span></span>

<span data-ttu-id="8ae1e-217">При каждом открытии или создать новую модель, вы будете перенаправлены toohello представление конструктора.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-217">Whenever you open or create a new model, you’ll be taken toohello design view.</span></span>

### <a name="adding-elements"></a><span data-ttu-id="8ae1e-218">Добавление элементов</span><span class="sxs-lookup"><span data-stu-id="8ae1e-218">Adding elements</span></span>

<span data-ttu-id="8ae1e-219">Можно двумя способами tooadd элементы в сетке hello:</span><span class="sxs-lookup"><span data-stu-id="8ae1e-219">There are 2 ways tooadd elements on hello grid:</span></span>

- <span data-ttu-id="8ae1e-220">**Перетаскивание** – перетащите hello нужный элемент toohello сетки, а затем использовать hello свойства tooprovide Дополнительные сведения об элементе.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-220">**Drag and Drop** – drag hello desired element toohello grid, then use hello element properties tooprovide additional information.</span></span>
- <span data-ttu-id="8ae1e-221">**Щелкните правой кнопкой мыши** — щелкните правой кнопкой мыши в сетке hello и выберите в раскрывающемся меню hello.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-221">**Right Click** – right click anywhere on hello grid and select from hello dropdown menu.</span></span> <span data-ttu-id="8ae1e-222">Универсальный представление этого элемента будут отображаться на экране приветствия.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-222">A generic representation of that element will appear on hello screen.</span></span>

### <a name="connecting-elements"></a><span data-ttu-id="8ae1e-223">Подключение элементов</span><span class="sxs-lookup"><span data-stu-id="8ae1e-223">Connecting elements</span></span>

<span data-ttu-id="8ae1e-224">Можно двумя способами tooconnect элементов в средстве hello:</span><span class="sxs-lookup"><span data-stu-id="8ae1e-224">There are 2 ways tooconnect elements in hello tool:</span></span>

- <span data-ttu-id="8ae1e-225">**Перетаскивание** — перетащите сетки toohello hello требуемой потока данных и подключите соответствующие элементы обоих концах toohello.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-225">**Drag and Drop** – drag hello desired dataflow toohello grid, and connect both ends toohello appropriate elements.</span></span>
- <span data-ttu-id="8ae1e-226">**Нажмите кнопку + Shift** — щелкните первый элемент hello (отправка данных) нажмите и удерживайте клавишу Shift hello, а затем выберите hello второй элемент (получение данных).</span><span class="sxs-lookup"><span data-stu-id="8ae1e-226">**Click + Shift** – click on hello first element (sending data), press and hold hello Shift key, then select hello second element (receiving data).</span></span> <span data-ttu-id="8ae1e-227">Щелкните правой кнопкой мыши и выберите "Подключение".</span><span class="sxs-lookup"><span data-stu-id="8ae1e-227">Right click, and select “Connect.”</span></span> <span data-ttu-id="8ae1e-228">При использовании двунаправленного потоков данных, порядок hello не столь важным.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-228">If you’re using a bi-directional dataflow, hello order is not as important.</span></span>

### <a name="properties"></a><span data-ttu-id="8ae1e-229">Свойства</span><span class="sxs-lookup"><span data-stu-id="8ae1e-229">Properties</span></span>

<span data-ttu-id="8ae1e-230">Показывает все свойства hello, которые могут быть изменены hello наборы элементов в схеме hello.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-230">Shows all hello properties that can be modified on hello stencils placed in hello diagram.</span></span> <span data-ttu-id="8ae1e-231">свойства toosee hello, просто щелкните набор элементов hello и сведения hello заполняется соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-231">toosee hello properties, just click on hello stencil and hello information will be populated accordingly.</span></span> <span data-ttu-id="8ae1e-232">Hello ниже примере до и после «Database», набор элементов перетаскивании на схему hello:</span><span class="sxs-lookup"><span data-stu-id="8ae1e-232">hello example below shows before and after a "Database" stencil is dragged onto hello diagram:</span></span>

#### <a name="before"></a><span data-ttu-id="8ae1e-233">До</span><span class="sxs-lookup"><span data-stu-id="8ae1e-233">Before</span></span>

![До](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a><span data-ttu-id="8ae1e-235">после</span><span class="sxs-lookup"><span data-stu-id="8ae1e-235">After</span></span>

![после](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a><span data-ttu-id="8ae1e-237">Сообщения</span><span class="sxs-lookup"><span data-stu-id="8ae1e-237">Messages</span></span>

<span data-ttu-id="8ae1e-238">При создании модели угроз и забыть, что потоки данных tooconnect tooelements, окно сообщений hello уведомляет tooact.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-238">If you create a threat model and forget tooconnect data flows tooelements, hello message window notifies you tooact.</span></span> <span data-ttu-id="8ae1e-239">Вы можете tooignore его или выполните hello инструкции toofix hello проблему.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-239">You can choose tooignore it or follow hello instructions toofix hello issue.</span></span> 

![Сообщения](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a><span data-ttu-id="8ae1e-241">Примечания</span><span class="sxs-lookup"><span data-stu-id="8ae1e-241">Notes</span></span>

<span data-ttu-id="8ae1e-242">Переключение вкладок tooNotes сообщений позволяет вам tooadd заметки tooyour схема toocapture своими мыслями</span><span class="sxs-lookup"><span data-stu-id="8ae1e-242">Switching tabs from Messages tooNotes allows you tooadd notes tooyour diagram toocapture all your thoughts</span></span>

## <a name="analysis-view"></a><span data-ttu-id="8ae1e-243">Представление "Анализ"</span><span class="sxs-lookup"><span data-stu-id="8ae1e-243">Analysis view</span></span>

<span data-ttu-id="8ae1e-244">После завершения построения диаграммы, переключить представление tooanalysis toohello верхнем меню выбора и выбор hello лупы Далее toohello paint палитры.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-244">Once you're done building your diagram, switch over tooanalysis view by going toohello top menu selections and choosing hello magnifying glass next toohello paint palette.</span></span>

![Представление "Анализ"](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a><span data-ttu-id="8ae1e-246">Выбор созданной угрозы</span><span class="sxs-lookup"><span data-stu-id="8ae1e-246">Generated threat selection</span></span>

<span data-ttu-id="8ae1e-247">Щелкнув угрозу, можно использовать три уникальные функции:</span><span class="sxs-lookup"><span data-stu-id="8ae1e-247">When you click on a threat, you can leverage three unique functions:</span></span>

| <span data-ttu-id="8ae1e-248">Функция</span><span class="sxs-lookup"><span data-stu-id="8ae1e-248">Feature</span></span>                               | <span data-ttu-id="8ae1e-249">Сведения</span><span class="sxs-lookup"><span data-stu-id="8ae1e-249">Info</span></span>      |
| --------------------------------------- | ------------ |
| <span data-ttu-id="8ae1e-250">**Индикатор прочитанного**</span><span class="sxs-lookup"><span data-stu-id="8ae1e-250">**Read Indicator**</span></span> | <p><span data-ttu-id="8ae1e-251">Угрозы будет помечен как read, которые легко позволяют хранить список элементов hello, которые вы уже прошли</span><span class="sxs-lookup"><span data-stu-id="8ae1e-251">Threat is now marked as read, which can easily help you keep track of hello items you already went through</span></span></p><p>![Индикатор прочитанного и непрочитанного](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| <span data-ttu-id="8ae1e-253">**Фокус на взаимодействии**</span><span class="sxs-lookup"><span data-stu-id="8ae1e-253">**Interaction Focus**</span></span> | <p><span data-ttu-id="8ae1e-254">Будет выделен взаимодействия в диаграмме hello, принадлежащий toothat угроз</span><span class="sxs-lookup"><span data-stu-id="8ae1e-254">Interaction in hello diagram belonging toothat threat is highlighted</span></span></p><p>![Фокус на взаимодействии](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| <span data-ttu-id="8ae1e-256">**Свойства угрозы**</span><span class="sxs-lookup"><span data-stu-id="8ae1e-256">**Threat Properties**</span></span> | <p><span data-ttu-id="8ae1e-257">Дополнительные сведения об угрозах hello заполняется в окне свойств угроз hello</span><span class="sxs-lookup"><span data-stu-id="8ae1e-257">Additional information about hello threat is populated in hello threat properties window</span></span></p><p>![Свойства угрозы](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a><span data-ttu-id="8ae1e-259">Изменение приоритета</span><span class="sxs-lookup"><span data-stu-id="8ae1e-259">Priority change</span></span>

<span data-ttu-id="8ae1e-260">Изменение hello уровень приоритета каждого созданного угрозы приводит к изменению их цвета toomake его легко tooidentify угроз высокий, средний и низкий приоритет.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-260">Changing hello priority level of each generated threat also changes their colors toomake it easy tooidentify high, medium and low priority threats.</span></span>

![Изменение приоритета](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a><span data-ttu-id="8ae1e-262">Изменяемые поля свойств угроз.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-262">Threat properties editable fields</span></span>

<span data-ttu-id="8ae1e-263">Как показано на рисунке hello выше, пользователи могут изменять сведения hello, созданный средством hello также добавить toocertain поля сведений, например при выравнивании по ширине.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-263">As seen in hello image above, users can change hello information generated by hello tool an also add information toocertain fields, such as justification.</span></span> <span data-ttu-id="8ae1e-264">Эти поля создаваемые шаблоном hello, поэтому если вам нужна дополнительная информация для каждой из угроз, вы рекомендуется toomake изменения.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-264">These fields are generated by hello template, so if you need more information for each threat, you're encouraged toomake modifications.</span></span>

![Свойства угрозы](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a><span data-ttu-id="8ae1e-266">Отчеты</span><span class="sxs-lookup"><span data-stu-id="8ae1e-266">Reports</span></span>

<span data-ttu-id="8ae1e-267">После завершения изменения приоритетов и обновления состояния hello каждого созданы угроз, можно сохранить файл hello и распечатать отчет слишком «Report» и выберите «создать полный отчет.»</span><span class="sxs-lookup"><span data-stu-id="8ae1e-267">Once you're done changing priorities and updating hello status of each generated threat, you can save hello file and/or print out a report by going too"Report" and then "Create Full Report."</span></span> <span data-ttu-id="8ae1e-268">Появится запрос отчета tooname hello и после этого вы увидите нечто похожее toohello рисунке ниже:</span><span class="sxs-lookup"><span data-stu-id="8ae1e-268">You'll be asked tooname hello report, and once you do, you should see something similar toohello image below:</span></span>

![Отчет](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a><span data-ttu-id="8ae1e-270">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8ae1e-270">Next steps</span></span>

<span data-ttu-id="8ae1e-271">toocontribute шаблона для hello сообщества, посетите страницу tooour  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**  страницы.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-271">toocontribute a template for hello community, please go tooour **[GitHub](https://github.com/Microsoft/threat-modeling-templates)** page.</span></span> <span data-ttu-id="8ae1e-272">**[Загрузить](https://aka.ms/tmtpreview)**  tooget средство hello по адресу.</span><span class="sxs-lookup"><span data-stu-id="8ae1e-272">**[Download](https://aka.ms/tmtpreview)** hello tool tooget started today.</span></span>
