---
title: "Действия меню MMC в StorSimple Snapshot Manager | Документация Майкрософт"
description: "Узнайте, как использовать стандартные действия меню консоли управления (MMC) в диспетчере моментальных снимков StorSimple."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 78ef81af-0d3a-4802-be54-ad192f9ac8a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 48f439a566a8067e153aab4fb789937d2f91268d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-mmc-menu-actions-in-storsimple-snapshot-manager"></a><span data-ttu-id="c544b-103">Использование действий меню MMC в диспетчере моментальных снимков StorSimple</span><span class="sxs-lookup"><span data-stu-id="c544b-103">Use the MMC menu actions in StorSimple Snapshot Manager</span></span>

## <a name="overview"></a><span data-ttu-id="c544b-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="c544b-104">Overview</span></span>
<span data-ttu-id="c544b-105">В диспетчере моментальных снимков StorSimple все меню действия и варианты панели **Действия** включают указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="c544b-105">In StorSimple Snapshot Manager, you will see the following actions listed on all action menus and all variations of the **Actions** pane.</span></span>

* <span data-ttu-id="c544b-106">Просмотр</span><span class="sxs-lookup"><span data-stu-id="c544b-106">View</span></span>
* <span data-ttu-id="c544b-107">Новое окно отсюда</span><span class="sxs-lookup"><span data-stu-id="c544b-107">New Window from Here</span></span> 
* <span data-ttu-id="c544b-108">Обновить</span><span class="sxs-lookup"><span data-stu-id="c544b-108">Refresh</span></span> 
* <span data-ttu-id="c544b-109">Экспорт списка</span><span class="sxs-lookup"><span data-stu-id="c544b-109">Export List</span></span> 
* <span data-ttu-id="c544b-110">Справка</span><span class="sxs-lookup"><span data-stu-id="c544b-110">Help</span></span> 

<span data-ttu-id="c544b-111">Эти действия доступны в консоли управления (MMC), а не только в диспетчере моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c544b-111">These actions are part of the Microsoft Management Console (MMC) and are not specific to StorSimple Snapshot Manager.</span></span> <span data-ttu-id="c544b-112">В этом учебнике описываются эти действия и объясняется, как использовать каждую из них в диспетчере моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c544b-112">This tutorial describes these actions and explains how to use each of them in StorSimple Snapshot Manager.</span></span>

## <a name="view"></a><span data-ttu-id="c544b-113">Просмотр</span><span class="sxs-lookup"><span data-stu-id="c544b-113">View</span></span>
<span data-ttu-id="c544b-114">Параметр **Вид** позволяет изменить представления панели **Результаты** и окна консоли.</span><span class="sxs-lookup"><span data-stu-id="c544b-114">You can use the **View** option to change the **Results** pane view and to change the console window view.</span></span> 

#### <a name="to-change-the-results-pane-view"></a><span data-ttu-id="c544b-115">Изменение представления панели "Результаты"</span><span class="sxs-lookup"><span data-stu-id="c544b-115">To change the Results pane view</span></span>
1. <span data-ttu-id="c544b-116">Щелкните соответствующий значок на рабочем столе, чтобы запустить диспетчер моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c544b-116">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="c544b-117">На панели **Область** щелкните правой кнопкой мыши любой узел либо разверните узел и щелкните правой кнопкой мыши элемент на панели **Результаты**, а затем щелкните **Вид**.</span><span class="sxs-lookup"><span data-stu-id="c544b-117">In the **Scope** pane, right-click any node or expand the node and right-click an item in the **Results** pane, and then click the **View** option.</span></span> 
3. <span data-ttu-id="c544b-118">Чтобы добавить или удалить столбцы, которые отображаются на панели **Результаты**, щелкните **Добавить или удалить столбцы**.</span><span class="sxs-lookup"><span data-stu-id="c544b-118">To add or remove the columns that appear in the **Results** pane, click **Add/Remove Columns**.</span></span> <span data-ttu-id="c544b-119">Откроется диалоговое окно **Добавление или удаление столбцов** .</span><span class="sxs-lookup"><span data-stu-id="c544b-119">The **Add/Remove Columns** dialog box appears.</span></span>
   
    ![Добавление или удаление столбцов на панели "Результаты"](./media/storsimple-snapshot-manager-mmc-menu/HCS_SSM_Add_remove_columns.png) 
4. <span data-ttu-id="c544b-121">Заполните форму следующим образом.</span><span class="sxs-lookup"><span data-stu-id="c544b-121">Complete the form as follows:</span></span>
   
   * <span data-ttu-id="c544b-122">В списке **Доступные столбцы** выберите элементы и нажмите кнопку **Добавить**, чтобы добавить их в список **Отображаемые столбцы**.</span><span class="sxs-lookup"><span data-stu-id="c544b-122">Select items from the **Available** columns list and click **Add** to add them to the **Displayed columns** list.</span></span> 
   * <span data-ttu-id="c544b-123">Щелкните элементы в списке **Отображаемые столбцы** и нажмите кнопку **Удалить**, чтобы удалить их из списка.</span><span class="sxs-lookup"><span data-stu-id="c544b-123">Click items in the **Displayed columns** list, and click **Remove** to remove them from the list.</span></span> 
   * <span data-ttu-id="c544b-124">Выберите элемент в списке **Отображаемые столбцы** и нажмите кнопку **Вверх** или **Вниз**, чтобы переместить элемент вверх или вниз в списке.</span><span class="sxs-lookup"><span data-stu-id="c544b-124">Select an item in the **Displayed** columns list and click **Move Up** or **Move Down** to move the item up or down in the list.</span></span> 
   * <span data-ttu-id="c544b-125">Щелкните **Восстановить значения по умолчанию**, чтобы вернуться к конфигурации панели **Результаты** по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c544b-125">Click **Restore Defaults** to return to the default **Results** pane configuration.</span></span> 
5. <span data-ttu-id="c544b-126">Выбрав необходимые параметры, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c544b-126">When you are finished with your selections, click **OK**.</span></span> 

#### <a name="to-change-the-console-window-view"></a><span data-ttu-id="c544b-127">Изменение представления окна консоли</span><span class="sxs-lookup"><span data-stu-id="c544b-127">To change the console window view</span></span>
1. <span data-ttu-id="c544b-128">Щелкните соответствующий значок на рабочем столе, чтобы запустить диспетчер моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c544b-128">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="c544b-129">На панели **Область** щелкните правой кнопкой мыши любой узел, выберите пункт **Вид**, а затем нажмите кнопку **Настроить**.</span><span class="sxs-lookup"><span data-stu-id="c544b-129">In the **Scope** pane, right-click any node, click **View**, and then click **Customize**.</span></span> <span data-ttu-id="c544b-130">Откроется диалоговое окно **Настройка** .</span><span class="sxs-lookup"><span data-stu-id="c544b-130">The **Customize** dialog box appears.</span></span>
   
    ![Настройка окна консоли](./media/storsimple-snapshot-manager-mmc-menu/HCS_SSM_Customize.png) 
3. <span data-ttu-id="c544b-132">Установите или снимите флажки, чтобы показать или скрыть элементы в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="c544b-132">Select or clear the check boxes to show or hide items in the console window.</span></span> <span data-ttu-id="c544b-133">Выбрав необходимые параметры, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c544b-133">When you are finished with your selections, click **OK**.</span></span>

## <a name="new-window-from-here"></a><span data-ttu-id="c544b-134">Новое окно отсюда</span><span class="sxs-lookup"><span data-stu-id="c544b-134">New Window from Here</span></span>
<span data-ttu-id="c544b-135">Параметр **Новое окно отсюда** позволяет открыть новое окно консоли.</span><span class="sxs-lookup"><span data-stu-id="c544b-135">You can use the **New Window from Here** option to open a new console window.</span></span>

#### <a name="to-open-a-new-console-window"></a><span data-ttu-id="c544b-136">Открытие нового окна консоли</span><span class="sxs-lookup"><span data-stu-id="c544b-136">To open a new console window</span></span>
1. <span data-ttu-id="c544b-137">Щелкните соответствующий значок на рабочем столе, чтобы запустить диспетчер моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c544b-137">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="c544b-138">На панели **Область** щелкните правой кнопкой мыши любой узел, а затем выберите пункт **Новое окно отсюда**.</span><span class="sxs-lookup"><span data-stu-id="c544b-138">In the **Scope** pane, right-click any node, and then click **New Window from Here**.</span></span> 
   
    <span data-ttu-id="c544b-139">В новом окне отобразятся только выбранные параметры.</span><span class="sxs-lookup"><span data-stu-id="c544b-139">A new window appears, showing only the scope that you selected.</span></span> <span data-ttu-id="c544b-140">Например, если щелкнуть правой кнопкой мыши узел **Политики архивации**, то в новом окне отобразятся только узел **Политики архивации** на панели **Область** и список заданных политик архивации на панели **Результаты**.</span><span class="sxs-lookup"><span data-stu-id="c544b-140">For example, if you right-click the **Backup Policies** node, the new window will show only the **Backup Policies** node in the **Scope** pane and a list of defined backup policies in the **Results** pane.</span></span> <span data-ttu-id="c544b-141">См. указанный ниже пример.</span><span class="sxs-lookup"><span data-stu-id="c544b-141">See the following example.</span></span>
   
    ![Создать окно отсюда](./media/storsimple-snapshot-manager-mmc-menu/HCS_SSM_NewWindow.png) 

## <a name="refresh"></a><span data-ttu-id="c544b-143">Обновить</span><span class="sxs-lookup"><span data-stu-id="c544b-143">Refresh</span></span>
<span data-ttu-id="c544b-144">Действие **Обновить** позволяет обновить окно консоли.</span><span class="sxs-lookup"><span data-stu-id="c544b-144">You can use the **Refresh** action to update the console window.</span></span>

#### <a name="to-update-the-console-window"></a><span data-ttu-id="c544b-145">Обновление окна консоли</span><span class="sxs-lookup"><span data-stu-id="c544b-145">To update the console window</span></span>
1. <span data-ttu-id="c544b-146">Щелкните соответствующий значок на рабочем столе, чтобы запустить диспетчер моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c544b-146">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="c544b-147">На панели **Область** щелкните правой кнопкой мыши любой узел либо разверните узел и щелкните правой кнопкой мыши элемент на панели **Результаты**, а затем щелкните **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="c544b-147">In the **Scope** pane, right-click any node or expand the node and right-click an item in the **Results** pane, and then click **Refresh**.</span></span> 

## <a name="export-list"></a><span data-ttu-id="c544b-148">Экспорт списка</span><span class="sxs-lookup"><span data-stu-id="c544b-148">Export List</span></span>
<span data-ttu-id="c544b-149">Действие **Экспорт списка** позволяет сохранить список как файл с разделителями-запятыми (CSV).</span><span class="sxs-lookup"><span data-stu-id="c544b-149">You can use the **Export List** action to save a list in a comma-separated value (CSV) file.</span></span> <span data-ttu-id="c544b-150">Например, можно экспортировать список политик архивации или каталог резервных копий.</span><span class="sxs-lookup"><span data-stu-id="c544b-150">For example, you can export the list of backup policies or the backup catalog.</span></span> <span data-ttu-id="c544b-151">Затем CSV-файл можно импортировать в приложение электронных таблиц для анализа.</span><span class="sxs-lookup"><span data-stu-id="c544b-151">You can then import the CSV file into a spreadsheet application for analysis.</span></span>

#### <a name="to-save-a-list-in-a-comma-separated-value-csv-file"></a><span data-ttu-id="c544b-152">Сохранение списка как файла с разделителями-запятыми (CSV)</span><span class="sxs-lookup"><span data-stu-id="c544b-152">To save a list in a comma-separated value (CSV) file</span></span>
1. <span data-ttu-id="c544b-153">Щелкните соответствующий значок на рабочем столе, чтобы запустить диспетчер моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c544b-153">Click the desktop icon to start StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="c544b-154">На панели **Область** щелкните правой кнопкой мыши любой узел либо разверните узел и щелкните правой кнопкой мыши элемент на панели **Результаты**, а затем щелкните **Экспорт списка**.</span><span class="sxs-lookup"><span data-stu-id="c544b-154">In the **Scope** pane, right-click any node or expand the node and right-click an item in the **Results** pane, and then click **Export List**.</span></span> 
3. <span data-ttu-id="c544b-155">Откроется диалоговое окно **Экспорт списка** .</span><span class="sxs-lookup"><span data-stu-id="c544b-155">The **Export List** dialog box appears.</span></span> <span data-ttu-id="c544b-156">Заполните форму следующим образом.</span><span class="sxs-lookup"><span data-stu-id="c544b-156">Complete the form as follows:</span></span> 
   
   1. <span data-ttu-id="c544b-157">В поле **Имя файла** введите имя CSV-файла или щелкните стрелку, чтобы выбрать файл в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="c544b-157">In the **File name** box, type a name for the CSV file or click the arrow to select from the drop-down list.</span></span>
   2. <span data-ttu-id="c544b-158">В поле **Тип файла** щелкните стрелку и выберите тип файла в раскрывающемся списке.</span><span class="sxs-lookup"><span data-stu-id="c544b-158">In the **Save as type** box, click the arrow and select a file type from the drop-down list.</span></span>
   3. <span data-ttu-id="c544b-159">Чтобы сохранить только выбранные элементы, выделите строки и установите флажок **Сохранить только выбранные строки** .</span><span class="sxs-lookup"><span data-stu-id="c544b-159">To save only selected items, select the rows and then click the **Save Only Selected Rows** check box.</span></span> <span data-ttu-id="c544b-160">Чтобы сохранить все экспортированные списки, снимите флажок **Сохранить только выбранные строки** .</span><span class="sxs-lookup"><span data-stu-id="c544b-160">To save all exported lists, clear the **Save Only Selected Rows** check box.</span></span>
   4. <span data-ttu-id="c544b-161">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c544b-161">Click **Save**.</span></span>
      
      ![Экспорт списка в виде файла с разделителями-запятыми](./media/storsimple-snapshot-manager-mmc-menu/HCS_SSM_Export_List.png) 

## <a name="help"></a><span data-ttu-id="c544b-163">Справка</span><span class="sxs-lookup"><span data-stu-id="c544b-163">Help</span></span>
<span data-ttu-id="c544b-164">В меню **Справка** вы можете просмотреть справку по диспетчеру моментальных снимков StorSimple и MMC, доступную в Интернете.</span><span class="sxs-lookup"><span data-stu-id="c544b-164">You can use the **Help** menu to view available online help for StorSimple Snapshot Manager and the MMC.</span></span>

#### <a name="to-view-available-online-help"></a><span data-ttu-id="c544b-165">Просмотр доступной справки в Интернете</span><span class="sxs-lookup"><span data-stu-id="c544b-165">To view available online help</span></span>
1. <span data-ttu-id="c544b-166">Щелкните соответствующий значок на рабочем столе, чтобы запустить диспетчер моментальных снимков StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c544b-166">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="c544b-167">На панели **Область** щелкните правой кнопкой мыши любой узел либо разверните узел и щелкните правой кнопкой мыши элемент на панели **Результаты**, а затем щелкните **Справка**.</span><span class="sxs-lookup"><span data-stu-id="c544b-167">In the **Scope** pane, right-click any node or expand the node and right-click an item in the **Results** pane, and then click **Help**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c544b-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c544b-168">Next steps</span></span>
* <span data-ttu-id="c544b-169">Узнайте больше о [пользовательском интерфейсе диспетчера моментальных снимков StorSimple](storsimple-use-snapshot-manager.md).</span><span class="sxs-lookup"><span data-stu-id="c544b-169">Learn more about the [StorSimple Snapshot Manager user interface](storsimple-use-snapshot-manager.md).</span></span>
* <span data-ttu-id="c544b-170">Узнайте больше об [использовании диспетчера моментальных снимков StorSimple для администрирования решения StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="c544b-170">Learn more about [using StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>

