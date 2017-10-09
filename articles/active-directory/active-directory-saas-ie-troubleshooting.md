---
title: "hello aaaTroubleshooting расширение панели доступа Azure для IE | Документы Microsoft"
description: "Как toouse группы политики toodeploy hello Internet Explorer надстройку для hello Мои приложения портала."
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
ms.openlocfilehash: 23cbb6117f34759330206de3a26f1397486acedb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-access-panel-extension-for-internet-explorer"></a><span data-ttu-id="ee4e3-103">Устранение неполадок hello расширение панели доступа для Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="ee4e3-103">Troubleshooting hello Access Panel Extension for Internet Explorer</span></span>
<span data-ttu-id="ee4e3-104">Эта статья поможет вам устранить hello следующие проблемы:</span><span class="sxs-lookup"><span data-stu-id="ee4e3-104">This article helps you troubleshoot hello following problems:</span></span>

* <span data-ttu-id="ee4e3-105">Вы являетесь приложений через портал Мои приложения hello не удается tooaccess при использовании Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-105">You're unable tooaccess your apps through hello My Apps portal while using Internet Explorer.</span></span>
* <span data-ttu-id="ee4e3-106">Вы увидите hello сообщения «Установка программного обеспечения», даже если вы уже установили hello программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-106">You see hello "Install Software" message even though you've already installed hello software.</span></span>

<span data-ttu-id="ee4e3-107">Если вы являетесь администратором, см. также: [как tooDeploy hello расширение панели доступа для Internet Explorer с помощью групповой политики](active-directory-saas-ie-group-policy.md)</span><span class="sxs-lookup"><span data-stu-id="ee4e3-107">If you are an admin, see also: [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](active-directory-saas-ie-group-policy.md)</span></span>

## <a name="run-hello-diagnostic-tool"></a><span data-ttu-id="ee4e3-108">Запустите средство диагностики hello</span><span class="sxs-lookup"><span data-stu-id="ee4e3-108">Run hello Diagnostic Tool</span></span>
<span data-ttu-id="ee4e3-109">Произвести диагностику проблем установки с hello расширение панели доступа по загрузке и запуске средства диагностики hello панели доступа:</span><span class="sxs-lookup"><span data-stu-id="ee4e3-109">You can diagnose installation problems with hello Access Panel Extension by downloading and running hello Access Panel diagnostic tool:</span></span>

1. [<span data-ttu-id="ee4e3-110">Щелкните здесь, средство диагностики toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-110">Click here toodownload hello diagnostic tool.</span></span>](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. <span data-ttu-id="ee4e3-111">Привет открыть файл и нажмите кнопку **извлечь все** кнопки.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-111">Open hello file, and press **Extract all** button.</span></span>
   
    ![Нажмите кнопку «Извлечь все».](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. <span data-ttu-id="ee4e3-113">Нажмите клавишу hello **извлечь** toocontinue кнопки.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-113">Then press hello **Extract** button toocontinue.</span></span>
   
    ![Нажмите кнопку «Извлечь».](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. <span data-ttu-id="ee4e3-115">Средство toorun hello, щелкните правой кнопкой мыши hello файл с именем **AccessPanelExtensionDiagnosticTool**, а затем выберите **открыть с помощью > на основе сервера сценариев Windows**.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-115">toorun hello tool, right-click hello file named **AccessPanelExtensionDiagnosticTool**, then select **Open with > Microsoft Windows Based Script Host**.</span></span>
   
    ![Открыть с помощью > Сервер сценариев на базе Microsoft Windows](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. <span data-ttu-id="ee4e3-117">Вы увидите следующие диагностики окна, который описывает, что может быть причиной установки hello.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-117">You will then see hello following diagnostic window, which describes what might be wrong with your installation.</span></span>
   
    ![Образец hello диагностики окна](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. <span data-ttu-id="ee4e3-119">Нажмите кнопку «**Да**» toolet hello программы исправление hello проблемы, которые были найдены.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-119">Click "**YES**" toolet hello program fix hello issues that have been found.</span></span>
7. <span data-ttu-id="ee4e3-120">toosave эти изменения, закройте каждого окна Internet Explorer и снова откройте Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-120">toosave these changes, close every Internet Explorer window, and then open Internet Explorer again.</span></span><br /><span data-ttu-id="ee4e3-121">Если открыть приложений по-прежнему не удается, попробуйте hello описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-121">If you still can't access your apps, try hello steps below.</span></span>

## <a name="check-that-hello-access-panel-extension-is-enabled"></a><span data-ttu-id="ee4e3-122">Проверьте, hello включено расширение панели доступа</span><span class="sxs-lookup"><span data-stu-id="ee4e3-122">Check that hello Access Panel Extension is enabled</span></span>
<span data-ttu-id="ee4e3-123">в Internet Explorer включена tooverify, hello расширение панели доступа:</span><span class="sxs-lookup"><span data-stu-id="ee4e3-123">tooverify that hello Access Panel Extension is enabled in Internet Explorer:</span></span>

1. <span data-ttu-id="ee4e3-124">В обозревателе Internet Explorer щелкните hello **значок шестеренки** в hello правом верхнем углу окна hello.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-124">In Internet Explorer, click hello **Gear icon** on hello top right corner of hello window.</span></span> <span data-ttu-id="ee4e3-125">Выберите **Свойства браузера**.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-125">Then select **Internet options**.</span></span><br /><span data-ttu-id="ee4e3-126">(В более ранних версиях Internet Explorer они находятся в разделе **Сервис > Параметры Интернета**).</span><span class="sxs-lookup"><span data-stu-id="ee4e3-126">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Go tooTools > Свойства обозревателя](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. <span data-ttu-id="ee4e3-128">Нажмите кнопку hello **программы** , щелкните hello **Управление надстройками** кнопки.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-128">Click hello **Programs** tab, then click hello **Manage add-ons** button.</span></span>
   
    ![Щелкните «Управление надстройками».](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. <span data-ttu-id="ee4e3-130">В этом диалоговом окне выберите **расширение панели доступа** и нажмите кнопку hello **включить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-130">In this dialog, select **Access Panel Extension** and then click hello **Enable** button.</span></span>
   
    ![Щелкните «Включить».](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. <span data-ttu-id="ee4e3-132">toosave эти изменения, закройте каждого окна Internet Explorer и снова откройте Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-132">toosave these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="enable-extensions-for-inprivate-browsing"></a><span data-ttu-id="ee4e3-133">Включение расширений для просмотра InPrivate</span><span class="sxs-lookup"><span data-stu-id="ee4e3-133">Enable Extensions for InPrivate Browsing</span></span>
<span data-ttu-id="ee4e3-134">При использовании режима просмотра InPrivate hello:</span><span class="sxs-lookup"><span data-stu-id="ee4e3-134">If you are using hello InPrivate Browsing mode:</span></span>

1. <span data-ttu-id="ee4e3-135">В обозревателе Internet Explorer щелкните hello **значок шестеренки** в hello правом верхнем углу окна hello.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-135">In Internet Explorer, click hello **Gear icon** on hello top right corner of hello window.</span></span> <span data-ttu-id="ee4e3-136">Выберите **Свойства браузера**.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-136">Then select **Internet options**.</span></span><br /><span data-ttu-id="ee4e3-137">(В более ранних версиях Internet Explorer они находятся в разделе **Сервис > Параметры Интернета**).</span><span class="sxs-lookup"><span data-stu-id="ee4e3-137">(In older versions of Internet Explorer you can find this under **Tools > Internet options**.</span></span>
   
    ![Образец hello диагностики окна](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. <span data-ttu-id="ee4e3-139">Go toohello **конфиденциальности** вкладку, затем **снимите** hello флажок **отключить панели инструментов и расширения в начале просмотра InPrivate**</span><span class="sxs-lookup"><span data-stu-id="ee4e3-139">Go toohello **Privacy** tab, then **uncheck** hello checkbox labeled **Disable toolbars and extensions when InPrivate Browsing starts**</span></span></p>
   
    ![Снимите флажок «Отключить панели инструментов и расширения при запуске просмотра InPrivate».](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. <span data-ttu-id="ee4e3-141">toosave эти изменения, закройте каждого окна Internet Explorer и снова откройте Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-141">toosave these changes, close every Internet Explorer window and then open Internet Explorer again.</span></span>

## <a name="uninstall-hello-access-panel-extension"></a><span data-ttu-id="ee4e3-142">Удаление hello расширение панели доступа</span><span class="sxs-lookup"><span data-stu-id="ee4e3-142">Uninstall hello Access Panel Extension</span></span>
<span data-ttu-id="ee4e3-143">hello toouninstall расширение панели доступа с вашего компьютера:</span><span class="sxs-lookup"><span data-stu-id="ee4e3-143">toouninstall hello Access Panel extension from your computer:</span></span>

1. <span data-ttu-id="ee4e3-144">На клавиатуре нажмите клавишу hello **ключа Windows** tooopen hello меню "Пуск".</span><span class="sxs-lookup"><span data-stu-id="ee4e3-144">On your keyboard, press hello **Windows key** tooopen hello Start menu.</span></span> <span data-ttu-id="ee4e3-145">При открытии меню hello можно ввести любое toodo поиска.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-145">When hello menu is open, you can type anything toodo a search.</span></span> <span data-ttu-id="ee4e3-146">Введите «Панель управления», а затем откройте hello **панели управления** когда он появится в результатах поиска hello.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-146">Type "Control Panel" and then open hello **Control Panel** when it appears in hello search results.</span></span>
   
    ![Поиск панели управления](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. <span data-ttu-id="ee4e3-148">В hello правом верхнем углу hello панели управления, измените hello **просмотра** параметр слишком**крупные значки**.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-148">In hello top right corner of hello Control Panel, change hello **View by** option too**Large icons**.</span></span> <span data-ttu-id="ee4e3-149">Затем найдите и щелкните hello **программы и компоненты** кнопки.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-149">Then find and click hello **Programs and Features** button.</span></span>
   
    ![Изменить hello представление tooshow крупные значки](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. <span data-ttu-id="ee4e3-151">Выберите из списка hello **расширение панели доступа**и нажмите кнопку hello hello **удаления** кнопки.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-151">From hello list, select **Access Panel Extension**, and hello click hello **Uninstall** button.</span></span>
   
    ![Нажмите кнопку удаления.](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. <span data-ttu-id="ee4e3-153">Повторите расширения hello tooinstall снова toosee Если hello проблема решена.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-153">You can then try tooinstall hello extension again toosee if hello problem has been resolved.</span></span>

<span data-ttu-id="ee4e3-154">Если возникли проблемы при удалении расширения hello, можно также удалить его с помощью hello [Microsoft ее исправить](https://go.microsoft.com/?linkid=9779673) средства.</span><span class="sxs-lookup"><span data-stu-id="ee4e3-154">If you encounter issues uninstalling hello extension, you can also remove it using hello [Microsoft Fix It](https://go.microsoft.com/?linkid=9779673) tool.</span></span>

## <a name="related-articles"></a><span data-ttu-id="ee4e3-155">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="ee4e3-155">Related Articles</span></span>
* [<span data-ttu-id="ee4e3-156">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ee4e3-156">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="ee4e3-157">Доступ к приложениям и единый вход с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ee4e3-157">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ee4e3-158">Как tooDeploy hello расширение панели доступа для Internet Explorer с помощью групповой политики</span><span class="sxs-lookup"><span data-stu-id="ee4e3-158">How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy</span></span>](active-directory-saas-ie-group-policy.md)

