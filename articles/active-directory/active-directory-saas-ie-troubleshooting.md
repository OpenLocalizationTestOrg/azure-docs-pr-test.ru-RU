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
# <a name="troubleshooting-hello-access-panel-extension-for-internet-explorer"></a>Устранение неполадок hello расширение панели доступа для Internet Explorer
Эта статья поможет вам устранить hello следующие проблемы:

* Вы являетесь приложений через портал Мои приложения hello не удается tooaccess при использовании Internet Explorer.
* Вы увидите hello сообщения «Установка программного обеспечения», даже если вы уже установили hello программного обеспечения.

Если вы являетесь администратором, см. также: [как tooDeploy hello расширение панели доступа для Internet Explorer с помощью групповой политики](active-directory-saas-ie-group-policy.md)

## <a name="run-hello-diagnostic-tool"></a>Запустите средство диагностики hello
Произвести диагностику проблем установки с hello расширение панели доступа по загрузке и запуске средства диагностики hello панели доступа:

1. [Щелкните здесь, средство диагностики toodownload hello.](https://account.activedirectory.windowsazure.com/applications/AccessPanelExtensionDiagnosticTool/AccessPanelExtensionDiagnosticTool.zip)
2. Привет открыть файл и нажмите кнопку **извлечь все** кнопки.
   
    ![Нажмите кнопку «Извлечь все».](./media/active-directory-saas-ie-troubleshooting/extract1.png)
3. Нажмите клавишу hello **извлечь** toocontinue кнопки.
   
    ![Нажмите кнопку «Извлечь».](./media/active-directory-saas-ie-troubleshooting/extract2.png)
4. Средство toorun hello, щелкните правой кнопкой мыши hello файл с именем **AccessPanelExtensionDiagnosticTool**, а затем выберите **открыть с помощью > на основе сервера сценариев Windows**.
   
    ![Открыть с помощью > Сервер сценариев на базе Microsoft Windows](./media/active-directory-saas-ie-troubleshooting/open_tool.png)
5. Вы увидите следующие диагностики окна, который описывает, что может быть причиной установки hello.
   
    ![Образец hello диагностики окна](./media/active-directory-saas-ie-troubleshooting/tool_preview.png)
6. Нажмите кнопку «**Да**» toolet hello программы исправление hello проблемы, которые были найдены.
7. toosave эти изменения, закройте каждого окна Internet Explorer и снова откройте Internet Explorer.<br />Если открыть приложений по-прежнему не удается, попробуйте hello описанные ниже действия.

## <a name="check-that-hello-access-panel-extension-is-enabled"></a>Проверьте, hello включено расширение панели доступа
в Internet Explorer включена tooverify, hello расширение панели доступа:

1. В обозревателе Internet Explorer щелкните hello **значок шестеренки** в hello правом верхнем углу окна hello. Выберите **Свойства браузера**.<br />(В более ранних версиях Internet Explorer они находятся в разделе **Сервис > Параметры Интернета**).
   
    ![Go tooTools > Свойства обозревателя](./media/active-directory-saas-ie-troubleshooting/internetoptions.png)
2. Нажмите кнопку hello **программы** , щелкните hello **Управление надстройками** кнопки.
   
    ![Щелкните «Управление надстройками».](./media/active-directory-saas-ie-troubleshooting/internetoptions_programs.png)
3. В этом диалоговом окне выберите **расширение панели доступа** и нажмите кнопку hello **включить** кнопки.
   
    ![Щелкните «Включить».](./media/active-directory-saas-ie-troubleshooting/enableaddon.png)
4. toosave эти изменения, закройте каждого окна Internet Explorer и снова откройте Internet Explorer.

## <a name="enable-extensions-for-inprivate-browsing"></a>Включение расширений для просмотра InPrivate
При использовании режима просмотра InPrivate hello:

1. В обозревателе Internet Explorer щелкните hello **значок шестеренки** в hello правом верхнем углу окна hello. Выберите **Свойства браузера**.<br />(В более ранних версиях Internet Explorer они находятся в разделе **Сервис > Параметры Интернета**).
   
    ![Образец hello диагностики окна](./media/active-directory-saas-ie-troubleshooting/inprivateoptions.png)
2. Go toohello **конфиденциальности** вкладку, затем **снимите** hello флажок **отключить панели инструментов и расширения в начале просмотра InPrivate**</p>
   
    ![Снимите флажок «Отключить панели инструментов и расширения при запуске просмотра InPrivate».](./media/active-directory-saas-ie-troubleshooting/enabletoolbars.png)
3. toosave эти изменения, закройте каждого окна Internet Explorer и снова откройте Internet Explorer.

## <a name="uninstall-hello-access-panel-extension"></a>Удаление hello расширение панели доступа
hello toouninstall расширение панели доступа с вашего компьютера:

1. На клавиатуре нажмите клавишу hello **ключа Windows** tooopen hello меню "Пуск". При открытии меню hello можно ввести любое toodo поиска. Введите «Панель управления», а затем откройте hello **панели управления** когда он появится в результатах поиска hello.
   
    ![Поиск панели управления](./media/active-directory-saas-ie-troubleshooting/search_sm.png)
2. В hello правом верхнем углу hello панели управления, измените hello **просмотра** параметр слишком**крупные значки**. Затем найдите и щелкните hello **программы и компоненты** кнопки.
   
    ![Изменить hello представление tooshow крупные значки](./media/active-directory-saas-ie-troubleshooting/control_panel.png)
3. Выберите из списка hello **расширение панели доступа**и нажмите кнопку hello hello **удаления** кнопки.
   
    ![Нажмите кнопку удаления.](./media/active-directory-saas-ie-troubleshooting/uninstall.png)
4. Повторите расширения hello tooinstall снова toosee Если hello проблема решена.

Если возникли проблемы при удалении расширения hello, можно также удалить его с помощью hello [Microsoft ее исправить](https://go.microsoft.com/?linkid=9779673) средства.

## <a name="related-articles"></a>Связанные статьи
* [Указатель статьей по управлению приложениями в Azure Active Directory](active-directory-apps-index.md)
* [Доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Как tooDeploy hello расширение панели доступа для Internet Explorer с помощью групповой политики](active-directory-saas-ie-group-policy.md)

