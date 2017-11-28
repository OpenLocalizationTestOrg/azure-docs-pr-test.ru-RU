---
title: "Устранение неполадок, связанных с расширением панели доступа Azure для Internet Explorer | Документация Майкрософт"
description: "Как применить групповую политику для развертывания надстройки Internet Explorer для работы с порталом «Мои приложения»."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56b3230-26fd-42ec-9e3d-2c12daf15479
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 938d0b4046afa8c80eabe542f4541d0554948f5d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshooting-the-access-panel-extension-for-internet-explorer"></a><span data-ttu-id="af974-103">Устранение неполадок, связанных с расширением панели доступа для Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="af974-103">Troubleshooting the Access Panel Extension for Internet Explorer</span></span>
<span data-ttu-id="af974-104">Эта статья поможет устранить следующие проблемы.</span><span class="sxs-lookup"><span data-stu-id="af974-104">This article helps you troubleshoot the following problems:</span></span>

* <span data-ttu-id="af974-105">Не удается получить доступ к приложениям через портал «Мои приложения» при использовании Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="af974-105">You're unable to access your apps through the My Apps portal while using Internet Explorer.</span></span>
* <span data-ttu-id="af974-106">Отображается сообщение «Установка программного обеспечения», хотя программное обеспечение уже установлено.</span><span class="sxs-lookup"><span data-stu-id="af974-106">You see the "Install Software" message even though you've already installed the software.</span></span>

<span data-ttu-id="af974-107">Если вы являетесь администратором, также прочтите статью [Развертывание расширения панели доступа для Internet Explorer с помощью групповой политики](active-directory-saas-ie-group-policy.md)</span><span class="sxs-lookup"><span data-stu-id="af974-107">If you are an admin, see also: [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)</span></span>

## <a name="run-the-diagnostic-tool"></a><span data-ttu-id="af974-108">Запуск средства диагностики</span><span class="sxs-lookup"><span data-stu-id="af974-108">Run the Diagnostic Tool</span></span>
<span data-ttu-id="af974-109">Для диагностики проблем с установкой расширения панели доступа загрузите и запустите средство диагностики панели доступа.</span><span class="sxs-lookup"><span data-stu-id="af974-109">You can diagnose installation problems with the Access Panel Extension by downloading and running the Access Panel diagnostic tool:</span></span>

1. [<span data-ttu-id="af974-110">Щелкните здесь, чтобы загрузить средство диагностики.</span><span class="sxs-lookup"><span data-stu-id="af974-110">Click here to download the diagnostic tool.</span></span>](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. <span data-ttu-id="af974-111">Откройте файл и нажмите кнопку **Извлечь все** .</span><span class="sxs-lookup"><span data-stu-id="af974-111">Open the file, and press **Extract all** button.</span></span>
   
    ![Нажмите кнопку «Извлечь все».](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. <span data-ttu-id="af974-113">Нажмите кнопку **Извлечь** , чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="af974-113">Then press the **Extract** button to continue.</span></span>
   
    ![Нажмите кнопку «Извлечь».](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. <span data-ttu-id="af974-115">Чтобы запустить инструмент, щелкните правой кнопкой мыши файл **AccessPanelExtensionDiagnosticTool**, а затем выберите **Открыть с помощью > Microsoft Windows Based Script Host** (Сервер сценариев на базе Microsoft Windows).</span><span class="sxs-lookup"><span data-stu-id="af974-115">To run the tool, right-click the file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span></span>
   
    ![Открыть с помощью > Сервер сценариев на базе Microsoft Windows](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. <span data-ttu-id="af974-117">Откроется следующее окно диагностики, описывающее возможные проблемы с вашей установкой.</span><span class="sxs-lookup"><span data-stu-id="af974-117">You will then see the following diagnostic window, which describes what might be wrong with your installation.</span></span>
   
    ![Образец окна диагностики](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. <span data-ttu-id="af974-119">Нажмите кнопку**ДА**, чтобы программа могла решить обнаруженные проблемы.</span><span class="sxs-lookup"><span data-stu-id="af974-119">Click "**YES**" to let the program fix the issues that have been found.</span></span>
7. <span data-ttu-id="af974-120">Чтобы сохранить эти изменения, закройте все окна Internet Explorer и откройте браузер снова.</span><span class="sxs-lookup"><span data-stu-id="af974-120">To save these changes, close every Internet Explorer window, and then open Internet Explorer again.</span></span><br /><span data-ttu-id="af974-121">Если приложения по-прежнему недоступны, попробуйте выполнить описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="af974-121">If you still can't access your apps, try the steps below.</span></span>

## <a name="check-that-the-access-panel-extension-is-enabled"></a><span data-ttu-id="af974-122">Убедитесь, что расширение панели доступа включено.</span><span class="sxs-lookup"><span data-stu-id="af974-122">Check that the Access Panel Extension is enabled</span></span>
<span data-ttu-id="af974-123">Чтобы убедиться, что расширение панели доступа в Internet Explorer включено, выполните описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="af974-123">To verify that the Access Panel Extension is enabled in Internet Explorer:</span></span>

1. <span data-ttu-id="af974-124">В правом верхнем углу Internet Explorer щелкните **значок шестеренки**.</span><span class="sxs-lookup"><span data-stu-id="af974-124">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="af974-125">Выберите **Свойства браузера**.</span><span class="sxs-lookup"><span data-stu-id="af974-125">Then select **Internet options**.</span></span><br /><span data-ttu-id="af974-126">(В более ранних версиях Internet Explorer они находятся в разделе **Сервис > Параметры Интернета**).</span><span class="sxs-lookup"><span data-stu-id="af974-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Выберите пункты Сервис > Параметры Интернета.](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. <span data-ttu-id="af974-128">Откройте вкладку **Программы** и нажмите кнопку **Настроить надстройки**.</span><span class="sxs-lookup"><span data-stu-id="af974-128">Click the **Programs** tab, then click the **Manage add-ons** button.</span></span>
   
    ![Щелкните «Управление надстройками».](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. <span data-ttu-id="af974-130">В этом диалоговом окне выберите **Access Panel Extension** (Расширение панели доступа) и нажмите кнопку **Включить**.</span><span class="sxs-lookup"><span data-stu-id="af974-130">In this dialog, select **Access Panel Extension** and then click the **Enable** button.</span></span>
   
    ![Щелкните «Включить».](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. <span data-ttu-id="af974-132">Чтобы сохранить эти изменения, закройте все окна Internet Explorer и откройте браузер снова.</span><span class="sxs-lookup"><span data-stu-id="af974-132">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="enable-extensions-for-inprivate-browsing"></a><span data-ttu-id="af974-133">Включение расширений для просмотра InPrivate</span><span class="sxs-lookup"><span data-stu-id="af974-133">Enable Extensions for InPrivate Browsing</span></span>
<span data-ttu-id="af974-134">Если используется режим просмотра InPrivate, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="af974-134">If you are using the InPrivate Browsing mode:</span></span>

1. <span data-ttu-id="af974-135">В правом верхнем углу Internet Explorer щелкните **значок шестеренки**.</span><span class="sxs-lookup"><span data-stu-id="af974-135">In Internet Explorer, click the **Gear icon** on the top right corner of the window.</span></span> <span data-ttu-id="af974-136">Выберите **Свойства браузера**.</span><span class="sxs-lookup"><span data-stu-id="af974-136">Then select **Internet options**.</span></span><br /><span data-ttu-id="af974-137">(В более ранних версиях Internet Explorer они находятся в разделе **Сервис > Параметры Интернета**).</span><span class="sxs-lookup"><span data-stu-id="af974-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Образец окна диагностики](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. <span data-ttu-id="af974-139">Откройте вкладку **Конфиденциальность**, **снимите** флажок **Отключать панели инструментов и расширения в режиме InPrivate**.</span><span class="sxs-lookup"><span data-stu-id="af974-139">Go to the **Privacy** tab, then **uncheck** the checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span></span></p>
   
    ![Снимите флажок «Отключить панели инструментов и расширения при запуске просмотра InPrivate».](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. <span data-ttu-id="af974-141">Чтобы сохранить эти изменения, закройте все окна Internet Explorer и откройте браузер снова.</span><span class="sxs-lookup"><span data-stu-id="af974-141">To save these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="uninstall-the-access-panel-extension"></a><span data-ttu-id="af974-142">Удаление расширения панели доступа</span><span class="sxs-lookup"><span data-stu-id="af974-142">Uninstall the Access Panel Extension</span></span>
<span data-ttu-id="af974-143">Чтобы удалить расширение панели доступа с компьютера, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="af974-143">To uninstall the Access Panel extension from your computer:</span></span>

1. <span data-ttu-id="af974-144">Нажмите на клавиатуре **клавишу Windows** , чтобы открыть меню «Пуск».</span><span class="sxs-lookup"><span data-stu-id="af974-144">On your keyboard, press the **Windows key** to open the Start menu.</span></span> <span data-ttu-id="af974-145">Открыв меню, введите параметры поиска.</span><span class="sxs-lookup"><span data-stu-id="af974-145">When the menu is open, you can type anything to do a search.</span></span> <span data-ttu-id="af974-146">Введите «Панель управления», а затем откройте **Панель управления** , когда она появится в результатах поиска.</span><span class="sxs-lookup"><span data-stu-id="af974-146">Type "Control Panel" and then open the **Control Panel** when it appears in the search results.</span></span>
   
    ![Поиск панели управления](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. <span data-ttu-id="af974-148">В правом верхнем углу панели управления выберите для параметра **Просмотр** значение **Крупные значки**.</span><span class="sxs-lookup"><span data-stu-id="af974-148">In the top right corner of the Control Panel, change the **View by** option to **Large icons**.</span></span> <span data-ttu-id="af974-149">Затем найдите и нажмите кнопку **Программы и компоненты**.</span><span class="sxs-lookup"><span data-stu-id="af974-149">Then find and click the **Programs and Features** button.</span></span>
   
    ![Измените представление для отображения крупных значков.](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. <span data-ttu-id="af974-151">В списке выберите **Access Panel Extension** (Расширение панели доступа) и нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="af974-151">From the list, select **Access Panel Extension**, and the click the **Uninstall** button.</span></span>
   
    ![Нажмите кнопку удаления.](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. <span data-ttu-id="af974-153">Затем попробуйте установить расширение еще раз, чтобы проверить, удалось ли решить проблему.</span><span class="sxs-lookup"><span data-stu-id="af974-153">You can then try to install the extension again to see if the problem has been resolved.</span></span>

<span data-ttu-id="af974-154">Если при удалении расширения возникнут проблемы, удалите его с помощью инструмента [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) .</span><span class="sxs-lookup"><span data-stu-id="af974-154">If you encounter issues uninstalling the extension, you can also remove it using the [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span></span>

## <a name="related-articles"></a><span data-ttu-id="af974-155">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="af974-155">Related Articles</span></span>
* [<span data-ttu-id="af974-156">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af974-156">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="af974-157">Доступ к приложениям и единый вход с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="af974-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="af974-158">Развертывание расширения панели доступа для Internet Explorer с помощью групповой политики</span><span class="sxs-lookup"><span data-stu-id="af974-158">How to Deploy the Access Panel Extension for Internet Explorer using Group Policy</span></span>](active-directory-saas-ie-group-policy.md)

