---
title: "Расширение панели доступа Azure для IE, воспользовавшись объектом групповой Политики aaaDeploy | Документы Microsoft"
description: "Как toouse группы политики toodeploy hello Internet Explorer надстройку для hello Мои приложения портала."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 7c2d49c8-5be0-4e7e-abac-332f9dfda736
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 926f15950bbe81d2fbfe1b0b856470da40880d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-hello-access-panel-extension-for-internet-explorer-using-group-policy"></a>Как tooDeploy hello расширение панели доступа для Internet Explorer с помощью групповой политики
В этом учебнике показано, как установить toouse групповой политики tooremotely расширение панели доступа hello для Internet Explorer на компьютерах пользователей. Это расширение является обязательным для пользователей Internet Explorer, которые нуждаются в приложения, настроенные с помощью toosign [паролю единого входа](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).

Рекомендуется, администраторам автоматизировать развертывание hello этого расширения. В противном случае пользователи имеют toodownload и Установка расширения hello, сами себя, какая toouser вероятность возникновения ошибок и требуются права администратора. В этом руководстве рассматривается один из методов автоматизированного развертывания программного обеспечения с помощью групповой политики. [Дополнительные сведения о групповой политике.](https://technet.microsoft.com/windowsserver/bb310732.aspx)

Hello расширение панели доступа также доступна для [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) и [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), ни один из которых требуется tooinstall разрешения администратора.

## <a name="prerequisites"></a>Предварительные требования
* Вы настроили [доменных служб Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), и вы присоединились к домену tooyour машин пользователей.
* Необходимо иметь hello «Изменить параметры» разрешение tooedit hello объекта групповой политики (GPO). По умолчанию это разрешение имеют члены элемента hello следующие группы безопасности: Администраторы домена "," Администраторы предприятия "и" Владельцы-создатели групповой политики. [Подробнее.](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-hello-distribution-point"></a>Шаг 1: Создание точки распространения hello
Во-первых необходимо разместить на сетевом ресурсе, доступном hello машинами, на котором необходимо расширение hello tooremotely установки на пакет установщика hello. toodo это, выполните следующие действия:

1. Войдите на сервер toohello в качестве администратора
2. В hello **диспетчера сервера** окне перейдите слишком**файлы и службы хранилища**.
   
    ![Откройте «Файловые службы и службы хранилища»](./media/active-directory-saas-ie-group-policy/files-services.png)
3. Go toohello **долей** вкладки. Затем выберите **Задачи** > **Новый общий ресурс...**
   
    ![Откройте «Файловые службы и службы хранилища»](./media/active-directory-saas-ie-group-policy/shares.png)
4. Полный hello **мастер создания общих ресурсов** и tooensure набор разрешений, что он может осуществляться из компьютеров пользователей. [Дополнительные сведения об общих ресурсах.](https://technet.microsoft.com/library/cc753175.aspx)
5. Загрузите следующие пакеты установщика Windows (MSI-файл) hello: [Extension.msi панели доступа](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)
6. Скопируйте расположение требуемого tooa пакета установщика hello в общей папке hello.
   
    ![Скопируйте общую toohello hello MSI-файл.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. Убедитесь, что на клиентских компьютерах может tooaccess пакет установщика hello из общей папки hello. 

## <a name="step-2-create-hello-group-policy-object"></a>Шаг 2: Создание hello объекта групповой политики
1. Войдите на сервер toohello, на котором установки доменных служб Active Directory (AD DS).
2. В hello диспетчера серверов выберите слишком**средства** > **Управление групповой политикой**.
   
    ![Go tooTools > Managment групповой политики](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. В левой области hello hello **Управление групповой политикой** окна, просматривать иерархию организационное подразделение (OU) и определить, в какой области хотелось бы tooapply hello групповой политики. Для экземпляра toopick небольшой tooa toodeploy Подразделения может возникнуть несколько пользователей для тестирования или выборе верхнего уровня Подразделения toodeploy tooyour всей организации.
   
   > [!NOTE]
   > Если бы как toocreate или изменить вашей организации подразделения (OU), перейдите назад toohello диспетчера сервера и перейти слишком**средства** > **Active Directory — пользователи и компьютеры**.
   > 
   > 
4. Выбрав организационное подразделение, щелкните его правой кнопкой мыши и выберите пункт **Создать объект групповой политики в этом домене и связать его...**
   
    ![Создайте новый объект групповой политики](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. В hello **новый объект групповой Политики** приглашение, введите имя для hello новый объект групповой политики.
   
    ![Новый объект групповой Политики имя hello](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. Щелкните правой кнопкой мыши hello объекта групповой политики, созданного и выберите **изменить**.
   
    ![Изменение нового hello объекта групповой Политики](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-hello-installation-package"></a>Шаг 3: Назначение hello пакета установки
1. Определите, хотите ли вы toodeploy hello расширения на основе **Конфигурация компьютера** или **Конфигурация пользователя**. При использовании [Конфигурация компьютера](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), hello расширение установлено на компьютере hello, независимо от того, что пользователи будут входить на tooit. С [Конфигурация пользователя](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), пользователи имеют расширения hello, установить для них независимо от того, какие компьютеры они входят в систему.
2. В левой области hello hello **редактор управления групповыми политиками** окне перейдите tooeither hello, следующие пути к папке, в зависимости от того, какой тип конфигурации выбрано:
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. Щелкните правой кнопкой мыши пункт **Установка программного обеспечения**, а затем выберите **Создать** > **Пакет…**
   
    ![Создайте новый пакет установки программного обеспечения](./media/active-directory-saas-ie-group-policy/new-package.png)
4. Последовательно выберите toohello общей папке, содержащей пакет установщика hello [шаг 1: Создание точки распространения hello](#step-1-create-the-distribution-point)выберите hello MSI-файл и нажмите кнопку **откройте**.
   
   > [!IMPORTANT]
   > Если hello ресурс находится на этом же сервере, проверьте посредством hello сетевой путь файла, а не путь к локальному файлу hello обращаются hello MSI-файл.
   > 
   > 
   
    ![Выберите пакет установки hello из общей папки hello.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. В hello **развертывания программного обеспечения** запрос, выберите **назначено** для вашего развертывания. Нажмите кнопку **ОК**.
   
    ![Выберите значение «Назначено» и нажмите кнопку ОК.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

расширение Hello сейчас развернутой toohello Подразделения, выбран. [Дополнительные сведения о групповой политике установки программного обеспечения.](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-hello-extension-for-internet-explorer"></a>Шаг 4: Включение автоматического hello расширение для Internet Explorer
Кроме toorunning hello установщика, все расширения для Internet Explorer необходимо явно включить прежде чем можно будет использовать. Повторите шаги hello ниже tooenable hello расширение панели доступа, с помощью групповой политики:

1. В hello **редактор управления групповыми политиками** перейдите tooeither hello, имеющие пути, в зависимости от того, какой тип конфигурации, выбранного в окне [Step 3: hello назначить пакет установки](#step-3-assign-the-installation-package):
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. Щелкните правой кнопкой мыши **Список надстроек** и выберите пункт **Изменить**.
    ![Измените список надстроек.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)
3. В hello **список надстроек** выберите **включено**. После этого в разделе hello **параметры** щелкните **Показать...** .
   
    ![Щелкните «Включить», а затем «Показать».](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. В hello **Показать содержимое** окна, выполните следующие шаги hello:
   
   1. Для первого столбца hello (hello **имя значения** поле), скопируйте и вставьте hello следующим Идентификатором класса:`{030E9A3F-7B18-4122-9A60-B87235E4F59E}`
   2. Для второго столбца hello (hello **значение** поле), тип в hello следующие значения:`1`
   3. Нажмите кнопку **ОК** tooclose hello **Показать содержимое** окна.
      
      ![Заполните hello значения, указанные выше.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. Нажмите кнопку **ОК** tooapply изменения и закрыть hello **список надстроек** окна.

Hello расширения включен для машин hello в hello выбранного Подразделения. [Дополнительные сведения об использовании групповой политики tooenable или отключение надстроек Internet Explorer.](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a>Шаг 5 (необязательный). Отключение запроса "Запомнить пароль"
Когда пользователи вход toowebsites с помощью hello расширение панели доступа, Internet Explorer может показать hello сообщение запросом» следует как toostore свой пароль?»

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

При желании tooprevent пользователей из означает этот запрос, выполните действия hello ниже tooprevent Автозаполнение от запоминание паролей:

1. В hello **редактор управления групповыми политиками** окна, откройте toohello путь, перечисленные ниже. Этот параметр конфигурации доступен только в разделе **Конфигурация пользователя**.
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. Найти hello параметр с именем **включить функцию автозаполнения hello для имен пользователей и паролей в формах**.
   
   > [!NOTE]
   > Предыдущие версии Active Directory может содержать этот параметр с именем hello **toosave Автозаполнение пароли запрещены**. Hello конфигурации для этого параметра отличается от настроек hello, описанного в этом учебнике.
   > 
   > 
   
    ![Помните toolook для этого в группе параметров пользователя.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. Щелкните правой кнопкой мыши hello выше параметр и выберите **изменить**.
4. В окне приветствия под названием **включить функцию автозаполнения hello для имен пользователей и паролей в формах**выберите **отключено**.
   
    ![Выберите "Отключено".](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. Нажмите кнопку **ОК** tooapply эти изменения и закрыть hello окна.

Пользователи будут больше не будет toostore свои учетные данные или использовать автозаполнение tooaccess ранее сохраненные учетные данные. Однако эта политика разрешить toouse toocontinue пользователей автозаполнения для других типов полей формы, например, поля поиска.

> [!WARNING]
> Если эта политика включена после пользователи выбрали toostore некоторые учетные данные, эта политика будет *не* снимите hello учетные данные, которые уже сохранены.
> 
> 

## <a name="step-6-testing-hello-deployment"></a>Шаг 6: Тестирование развертывания hello
Выполните действия hello ниже tooverify, при успешном выполнении расширения развертывания hello.

1. При развертывании с помощью **Конфигурация компьютера**, войдите в клиентский компьютер, который принадлежит toohello Подразделения, выбранного в [шаг 2: создание hello объекта групповой политики](#step-2-create-the-group-policy-object). При развертывании с помощью **Конфигурация пользователя**, убедитесь, что toosign в как пользователь, принадлежащий toothat Подразделения.
2. Может потребоваться несколько входа модули для hello групповой политики изменяется toofully обновления с этого компьютера. Обновление hello tooforce, откройте **командной строки** окна и выполнения hello следующую команду:`gpupdate /force`
3. Необходимо перезапустить машину hello для hello установки tootake месте. Загрузки может занять значительно больше времени, чем обычные при hello расширение устанавливает.
4. После перезагрузки откройте браузер **Internet Explorer**. На hello правом верхнем углу окна hello, нажмите кнопку **средства** (значок шестеренки hello), а затем выберите **Управление надстройками**.
   
    ![Go tooTools > Управление надстройками](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. В hello **Управление надстройками** окна, убедитесь, что hello **расширение панели доступа** установлен и что его **состояние** задано слишком**включено**.
   
    ![Убедитесь, что hello расширение панели доступа установлен и включен.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a>Связанные статьи
* [Указатель статьей по управлению приложениями в Azure Active Directory](active-directory-apps-index.md)
* [Доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Устранение неполадок hello расширение панели доступа для Internet Explorer](active-directory-saas-ie-troubleshooting.md)

