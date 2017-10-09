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
# <a name="how-toodeploy-hello-access-panel-extension-for-internet-explorer-using-group-policy"></a><span data-ttu-id="09243-103">Как tooDeploy hello расширение панели доступа для Internet Explorer с помощью групповой политики</span><span class="sxs-lookup"><span data-stu-id="09243-103">How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy</span></span>
<span data-ttu-id="09243-104">В этом учебнике показано, как установить toouse групповой политики tooremotely расширение панели доступа hello для Internet Explorer на компьютерах пользователей.</span><span class="sxs-lookup"><span data-stu-id="09243-104">This tutorial shows how toouse group policy tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span> <span data-ttu-id="09243-105">Это расширение является обязательным для пользователей Internet Explorer, которые нуждаются в приложения, настроенные с помощью toosign [паролю единого входа](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="09243-105">This extension is required for Internet Explorer users who need toosign into apps that are configured using [password-based single sign-on](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).</span></span>

<span data-ttu-id="09243-106">Рекомендуется, администраторам автоматизировать развертывание hello этого расширения.</span><span class="sxs-lookup"><span data-stu-id="09243-106">It is recommended that admins automate hello deployment of this extension.</span></span> <span data-ttu-id="09243-107">В противном случае пользователи имеют toodownload и Установка расширения hello, сами себя, какая toouser вероятность возникновения ошибок и требуются права администратора.</span><span class="sxs-lookup"><span data-stu-id="09243-107">Otherwise, users have toodownload and install hello extension themselves, which is prone toouser error and requires administrator permissions.</span></span> <span data-ttu-id="09243-108">В этом руководстве рассматривается один из методов автоматизированного развертывания программного обеспечения с помощью групповой политики.</span><span class="sxs-lookup"><span data-stu-id="09243-108">This tutorial covers one method of automating software deployments by using group policy.</span></span> [<span data-ttu-id="09243-109">Дополнительные сведения о групповой политике.</span><span class="sxs-lookup"><span data-stu-id="09243-109">Learn more about group policy.</span></span>](https://technet.microsoft.com/windowsserver/bb310732.aspx)

<span data-ttu-id="09243-110">Hello расширение панели доступа также доступна для [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) и [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), ни один из которых требуется tooinstall разрешения администратора.</span><span class="sxs-lookup"><span data-stu-id="09243-110">hello Access Panel extension is also available for [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) and [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), neither of which require administrator permissions tooinstall.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09243-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="09243-111">Prerequisites</span></span>
* <span data-ttu-id="09243-112">Вы настроили [доменных служб Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), и вы присоединились к домену tooyour машин пользователей.</span><span class="sxs-lookup"><span data-stu-id="09243-112">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>
* <span data-ttu-id="09243-113">Необходимо иметь hello «Изменить параметры» разрешение tooedit hello объекта групповой политики (GPO).</span><span class="sxs-lookup"><span data-stu-id="09243-113">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="09243-114">По умолчанию это разрешение имеют члены элемента hello следующие группы безопасности: Администраторы домена "," Администраторы предприятия "и" Владельцы-создатели групповой политики.</span><span class="sxs-lookup"><span data-stu-id="09243-114">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> [<span data-ttu-id="09243-115">Подробнее.</span><span class="sxs-lookup"><span data-stu-id="09243-115">Learn more.</span></span>](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-hello-distribution-point"></a><span data-ttu-id="09243-116">Шаг 1: Создание точки распространения hello</span><span class="sxs-lookup"><span data-stu-id="09243-116">Step 1: Create hello Distribution Point</span></span>
<span data-ttu-id="09243-117">Во-первых необходимо разместить на сетевом ресурсе, доступном hello машинами, на котором необходимо расширение hello tooremotely установки на пакет установщика hello.</span><span class="sxs-lookup"><span data-stu-id="09243-117">First, you must place hello installer package on a network location that can be accessed by hello machines that you wish tooremotely install hello extension on.</span></span> <span data-ttu-id="09243-118">toodo это, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="09243-118">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="09243-119">Войдите на сервер toohello в качестве администратора</span><span class="sxs-lookup"><span data-stu-id="09243-119">Log on toohello server as an administrator</span></span>
2. <span data-ttu-id="09243-120">В hello **диспетчера сервера** окне перейдите слишком**файлы и службы хранилища**.</span><span class="sxs-lookup"><span data-stu-id="09243-120">In hello **Server Manager** window, go too**Files and Storage Services**.</span></span>
   
    ![Откройте «Файловые службы и службы хранилища»](./media/active-directory-saas-ie-group-policy/files-services.png)
3. <span data-ttu-id="09243-122">Go toohello **долей** вкладки. Затем выберите **Задачи** > **Новый общий ресурс...**</span><span class="sxs-lookup"><span data-stu-id="09243-122">Go toohello **Shares** tab. Then click **Tasks** > **New Share...**</span></span>
   
    ![Откройте «Файловые службы и службы хранилища»](./media/active-directory-saas-ie-group-policy/shares.png)
4. <span data-ttu-id="09243-124">Полный hello **мастер создания общих ресурсов** и tooensure набор разрешений, что он может осуществляться из компьютеров пользователей.</span><span class="sxs-lookup"><span data-stu-id="09243-124">Complete hello **New Share Wizard** and set permissions tooensure that it can be accessed from your users' machines.</span></span> [<span data-ttu-id="09243-125">Дополнительные сведения об общих ресурсах.</span><span class="sxs-lookup"><span data-stu-id="09243-125">Learn more about shares.</span></span>](https://technet.microsoft.com/library/cc753175.aspx)
5. <span data-ttu-id="09243-126">Загрузите следующие пакеты установщика Windows (MSI-файл) hello: [Extension.msi панели доступа](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span><span class="sxs-lookup"><span data-stu-id="09243-126">Download hello following Microsoft Windows Installer package (.msi file): [Access Panel Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)</span></span>
6. <span data-ttu-id="09243-127">Скопируйте расположение требуемого tooa пакета установщика hello в общей папке hello.</span><span class="sxs-lookup"><span data-stu-id="09243-127">Copy hello installer package tooa desired location on hello share.</span></span>
   
    ![Скопируйте общую toohello hello MSI-файл.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. <span data-ttu-id="09243-129">Убедитесь, что на клиентских компьютерах может tooaccess пакет установщика hello из общей папки hello.</span><span class="sxs-lookup"><span data-stu-id="09243-129">Verify that your client machines are able tooaccess hello installer package from hello share.</span></span> 

## <a name="step-2-create-hello-group-policy-object"></a><span data-ttu-id="09243-130">Шаг 2: Создание hello объекта групповой политики</span><span class="sxs-lookup"><span data-stu-id="09243-130">Step 2: Create hello Group Policy Object</span></span>
1. <span data-ttu-id="09243-131">Войдите на сервер toohello, на котором установки доменных служб Active Directory (AD DS).</span><span class="sxs-lookup"><span data-stu-id="09243-131">Log on toohello server that hosts your Active Directory Domain Services (AD DS) installation.</span></span>
2. <span data-ttu-id="09243-132">В hello диспетчера серверов выберите слишком**средства** > **Управление групповой политикой**.</span><span class="sxs-lookup"><span data-stu-id="09243-132">In hello Server Manager, go too**Tools** > **Group Policy Management**.</span></span>
   
    ![Go tooTools > Managment групповой политики](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. <span data-ttu-id="09243-134">В левой области hello hello **Управление групповой политикой** окна, просматривать иерархию организационное подразделение (OU) и определить, в какой области хотелось бы tooapply hello групповой политики.</span><span class="sxs-lookup"><span data-stu-id="09243-134">In hello left pane of hello **Group Policy Management** window, view your Organizational Unit (OU) hierarchy and determine at which scope you would like tooapply hello group policy.</span></span> <span data-ttu-id="09243-135">Для экземпляра toopick небольшой tooa toodeploy Подразделения может возникнуть несколько пользователей для тестирования или выборе верхнего уровня Подразделения toodeploy tooyour всей организации.</span><span class="sxs-lookup"><span data-stu-id="09243-135">For instance, you may decide toopick a small OU toodeploy tooa few users for testing, or you may pick a top-level OU toodeploy tooyour entire organization.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="09243-136">Если бы как toocreate или изменить вашей организации подразделения (OU), перейдите назад toohello диспетчера сервера и перейти слишком**средства** > **Active Directory — пользователи и компьютеры**.</span><span class="sxs-lookup"><span data-stu-id="09243-136">If you would like toocreate or edit your Organization Units (OUs), switch back toohello Server Manager and go too**Tools** > **Active Directory Users and Computers**.</span></span>
   > 
   > 
4. <span data-ttu-id="09243-137">Выбрав организационное подразделение, щелкните его правой кнопкой мыши и выберите пункт **Создать объект групповой политики в этом домене и связать его...**</span><span class="sxs-lookup"><span data-stu-id="09243-137">Once you have selected an OU, right-click it and select **Create a GPO in this domain, and Link it here...**</span></span>
   
    ![Создайте новый объект групповой политики](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. <span data-ttu-id="09243-139">В hello **новый объект групповой Политики** приглашение, введите имя для hello новый объект групповой политики.</span><span class="sxs-lookup"><span data-stu-id="09243-139">In hello **New GPO** prompt, type in a name for hello new Group Policy Object.</span></span>
   
    ![Новый объект групповой Политики имя hello](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. <span data-ttu-id="09243-141">Щелкните правой кнопкой мыши hello объекта групповой политики, созданного и выберите **изменить**.</span><span class="sxs-lookup"><span data-stu-id="09243-141">Right-click hello Group Policy Object that you created, and select **Edit**.</span></span>
   
    ![Изменение нового hello объекта групповой Политики](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-hello-installation-package"></a><span data-ttu-id="09243-143">Шаг 3: Назначение hello пакета установки</span><span class="sxs-lookup"><span data-stu-id="09243-143">Step 3: Assign hello Installation Package</span></span>
1. <span data-ttu-id="09243-144">Определите, хотите ли вы toodeploy hello расширения на основе **Конфигурация компьютера** или **Конфигурация пользователя**.</span><span class="sxs-lookup"><span data-stu-id="09243-144">Determine whether you would like toodeploy hello extension based on **Computer Configuration** or **User Configuration**.</span></span> <span data-ttu-id="09243-145">При использовании [Конфигурация компьютера](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), hello расширение установлено на компьютере hello, независимо от того, что пользователи будут входить на tooit.</span><span class="sxs-lookup"><span data-stu-id="09243-145">When using [computer configuration](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), hello extension is installed on hello computer regardless of which users log on tooit.</span></span> <span data-ttu-id="09243-146">С [Конфигурация пользователя](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), пользователи имеют расширения hello, установить для них независимо от того, какие компьютеры они входят в систему.</span><span class="sxs-lookup"><span data-stu-id="09243-146">With [user configuration](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), users have hello extension installed for them regardless of which computers they log on to.</span></span>
2. <span data-ttu-id="09243-147">В левой области hello hello **редактор управления групповыми политиками** окне перейдите tooeither hello, следующие пути к папке, в зависимости от того, какой тип конфигурации выбрано:</span><span class="sxs-lookup"><span data-stu-id="09243-147">In hello left pane of hello **Group Policy Management Editor** window, go tooeither of hello following folder paths, depending on which type of configuration you chose:</span></span>
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. <span data-ttu-id="09243-148">Щелкните правой кнопкой мыши пункт **Установка программного обеспечения**, а затем выберите **Создать** > **Пакет…**</span><span class="sxs-lookup"><span data-stu-id="09243-148">Right-click **Software installation**, then select **New** > **Package...**</span></span>
   
    ![Создайте новый пакет установки программного обеспечения](./media/active-directory-saas-ie-group-policy/new-package.png)
4. <span data-ttu-id="09243-150">Последовательно выберите toohello общей папке, содержащей пакет установщика hello [шаг 1: Создание точки распространения hello](#step-1-create-the-distribution-point)выберите hello MSI-файл и нажмите кнопку **откройте**.</span><span class="sxs-lookup"><span data-stu-id="09243-150">Go toohello shared folder that contains hello installer package from [Step 1: Create hello Distribution Point](#step-1-create-the-distribution-point), select hello .msi file, and click **Open**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="09243-151">Если hello ресурс находится на этом же сервере, проверьте посредством hello сетевой путь файла, а не путь к локальному файлу hello обращаются hello MSI-файл.</span><span class="sxs-lookup"><span data-stu-id="09243-151">If hello share is located on this same server, verify that you are accessing hello .msi through hello network file path, rather than hello local file path.</span></span>
   > 
   > 
   
    ![Выберите пакет установки hello из общей папки hello.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. <span data-ttu-id="09243-153">В hello **развертывания программного обеспечения** запрос, выберите **назначено** для вашего развертывания.</span><span class="sxs-lookup"><span data-stu-id="09243-153">In hello **Deploy Software** prompt, select **Assigned** for your deployment method.</span></span> <span data-ttu-id="09243-154">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="09243-154">Then click **OK**.</span></span>
   
    ![Выберите значение «Назначено» и нажмите кнопку ОК.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

<span data-ttu-id="09243-156">расширение Hello сейчас развернутой toohello Подразделения, выбран.</span><span class="sxs-lookup"><span data-stu-id="09243-156">hello extension is now deployed toohello OU that you selected.</span></span> [<span data-ttu-id="09243-157">Дополнительные сведения о групповой политике установки программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="09243-157">Learn more about Group Policy Software Installation.</span></span>](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-hello-extension-for-internet-explorer"></a><span data-ttu-id="09243-158">Шаг 4: Включение автоматического hello расширение для Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="09243-158">Step 4: Auto-Enable hello Extension for Internet Explorer</span></span>
<span data-ttu-id="09243-159">Кроме toorunning hello установщика, все расширения для Internet Explorer необходимо явно включить прежде чем можно будет использовать.</span><span class="sxs-lookup"><span data-stu-id="09243-159">In addition toorunning hello installer, every extension for Internet Explorer must be explicitly enabled before it can be used.</span></span> <span data-ttu-id="09243-160">Повторите шаги hello ниже tooenable hello расширение панели доступа, с помощью групповой политики:</span><span class="sxs-lookup"><span data-stu-id="09243-160">Follow hello steps below tooenable hello Access Panel Extension using group policy:</span></span>

1. <span data-ttu-id="09243-161">В hello **редактор управления групповыми политиками** перейдите tooeither hello, имеющие пути, в зависимости от того, какой тип конфигурации, выбранного в окне [Step 3: hello назначить пакет установки](#step-3-assign-the-installation-package):</span><span class="sxs-lookup"><span data-stu-id="09243-161">In hello **Group Policy Management Editor** window, go tooeither of hello following paths, depending on which type of configuration you chose in [Step 3: Assign hello Installation Package](#step-3-assign-the-installation-package):</span></span>
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. <span data-ttu-id="09243-162">Щелкните правой кнопкой мыши **Список надстроек** и выберите пункт **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="09243-162">Right-click **Add-on List**, and select **Edit**.</span></span>
    <span data-ttu-id="09243-163">![Измените список надстроек.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span><span class="sxs-lookup"><span data-stu-id="09243-163">![Edit Add-on List.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)</span></span>
3. <span data-ttu-id="09243-164">В hello **список надстроек** выберите **включено**.</span><span class="sxs-lookup"><span data-stu-id="09243-164">In hello **Add-on List** window, select **Enabled**.</span></span> <span data-ttu-id="09243-165">После этого в разделе hello **параметры** щелкните **Показать...** .</span><span class="sxs-lookup"><span data-stu-id="09243-165">Then, under hello **Options** section, click **Show...**.</span></span>
   
    ![Щелкните «Включить», а затем «Показать».](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. <span data-ttu-id="09243-167">В hello **Показать содержимое** окна, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="09243-167">In hello **Show Contents** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="09243-168">Для первого столбца hello (hello **имя значения** поле), скопируйте и вставьте hello следующим Идентификатором класса:`{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span><span class="sxs-lookup"><span data-stu-id="09243-168">For hello first column (hello **Value Name** field), copy and paste hello following Class ID: `{030E9A3F-7B18-4122-9A60-B87235E4F59E}`</span></span>
   2. <span data-ttu-id="09243-169">Для второго столбца hello (hello **значение** поле), тип в hello следующие значения:`1`</span><span class="sxs-lookup"><span data-stu-id="09243-169">For hello second column (hello **Value** field), type in hello following value: `1`</span></span>
   3. <span data-ttu-id="09243-170">Нажмите кнопку **ОК** tooclose hello **Показать содержимое** окна.</span><span class="sxs-lookup"><span data-stu-id="09243-170">Click **OK** tooclose hello **Show Contents** window.</span></span>
      
      ![Заполните hello значения, указанные выше.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. <span data-ttu-id="09243-172">Нажмите кнопку **ОК** tooapply изменения и закрыть hello **список надстроек** окна.</span><span class="sxs-lookup"><span data-stu-id="09243-172">Click **OK** tooapply your changes and close hello **Add-on List** window.</span></span>

<span data-ttu-id="09243-173">Hello расширения включен для машин hello в hello выбранного Подразделения.</span><span class="sxs-lookup"><span data-stu-id="09243-173">hello extension should now be enabled for hello machines in hello selected OU.</span></span> [<span data-ttu-id="09243-174">Дополнительные сведения об использовании групповой политики tooenable или отключение надстроек Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="09243-174">Learn more about using group policy tooenable or disable Internet Explorer add-ons.</span></span>](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a><span data-ttu-id="09243-175">Шаг 5 (необязательный). Отключение запроса "Запомнить пароль"</span><span class="sxs-lookup"><span data-stu-id="09243-175">Step 5 (Optional): Disable "Remember Password" Prompt</span></span>
<span data-ttu-id="09243-176">Когда пользователи вход toowebsites с помощью hello расширение панели доступа, Internet Explorer может показать hello сообщение запросом» следует как toostore свой пароль?»</span><span class="sxs-lookup"><span data-stu-id="09243-176">When users sign-in toowebsites using hello Access Panel Extension, Internet Explorer may show hello following prompt asking "Would you like toostore your password?"</span></span>

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

<span data-ttu-id="09243-177">При желании tooprevent пользователей из означает этот запрос, выполните действия hello ниже tooprevent Автозаполнение от запоминание паролей:</span><span class="sxs-lookup"><span data-stu-id="09243-177">If you wish tooprevent your users from seeing this prompt, then follow hello steps below tooprevent auto-complete from remembering passwords:</span></span>

1. <span data-ttu-id="09243-178">В hello **редактор управления групповыми политиками** окна, откройте toohello путь, перечисленные ниже.</span><span class="sxs-lookup"><span data-stu-id="09243-178">In hello **Group Policy Management Editor** window, go toohello path listed below.</span></span> <span data-ttu-id="09243-179">Этот параметр конфигурации доступен только в разделе **Конфигурация пользователя**.</span><span class="sxs-lookup"><span data-stu-id="09243-179">This configuration setting is only available under **User Configuration**.</span></span>
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. <span data-ttu-id="09243-180">Найти hello параметр с именем **включить функцию автозаполнения hello для имен пользователей и паролей в формах**.</span><span class="sxs-lookup"><span data-stu-id="09243-180">Find hello setting named **Turn on hello auto-complete feature for user names and passwords on forms**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="09243-181">Предыдущие версии Active Directory может содержать этот параметр с именем hello **toosave Автозаполнение пароли запрещены**.</span><span class="sxs-lookup"><span data-stu-id="09243-181">Previous versions of Active Directory may list this setting with hello name **Do not allow auto-complete toosave passwords**.</span></span> <span data-ttu-id="09243-182">Hello конфигурации для этого параметра отличается от настроек hello, описанного в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="09243-182">hello configuration for that setting differs from hello setting described in this tutorial.</span></span>
   > 
   > 
   
    ![Помните toolook для этого в группе параметров пользователя.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. <span data-ttu-id="09243-184">Щелкните правой кнопкой мыши hello выше параметр и выберите **изменить**.</span><span class="sxs-lookup"><span data-stu-id="09243-184">Right click hello above setting, and select **Edit**.</span></span>
4. <span data-ttu-id="09243-185">В окне приветствия под названием **включить функцию автозаполнения hello для имен пользователей и паролей в формах**выберите **отключено**.</span><span class="sxs-lookup"><span data-stu-id="09243-185">In hello window titled **Turn on hello auto-complete feature for user names and passwords on forms**, select **Disabled**.</span></span>
   
    ![Выберите "Отключено".](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. <span data-ttu-id="09243-187">Нажмите кнопку **ОК** tooapply эти изменения и закрыть hello окна.</span><span class="sxs-lookup"><span data-stu-id="09243-187">Click **OK** tooapply these changes and close hello window.</span></span>

<span data-ttu-id="09243-188">Пользователи будут больше не будет toostore свои учетные данные или использовать автозаполнение tooaccess ранее сохраненные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="09243-188">Users will no longer be able toostore their credentials or use auto-complete tooaccess previously stored credentials.</span></span> <span data-ttu-id="09243-189">Однако эта политика разрешить toouse toocontinue пользователей автозаполнения для других типов полей формы, например, поля поиска.</span><span class="sxs-lookup"><span data-stu-id="09243-189">However, this policy does allow users toocontinue toouse auto-complete for other types of form fields, such as search fields.</span></span>

> [!WARNING]
> <span data-ttu-id="09243-190">Если эта политика включена после пользователи выбрали toostore некоторые учетные данные, эта политика будет *не* снимите hello учетные данные, которые уже сохранены.</span><span class="sxs-lookup"><span data-stu-id="09243-190">If this policy is enabled after users have chosen toostore some credentials, this policy will *not* clear hello credentials that have already been stored.</span></span>
> 
> 

## <a name="step-6-testing-hello-deployment"></a><span data-ttu-id="09243-191">Шаг 6: Тестирование развертывания hello</span><span class="sxs-lookup"><span data-stu-id="09243-191">Step 6: Testing hello Deployment</span></span>
<span data-ttu-id="09243-192">Выполните действия hello ниже tooverify, при успешном выполнении расширения развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="09243-192">Follow hello steps below tooverify if hello extension deployment was successful:</span></span>

1. <span data-ttu-id="09243-193">При развертывании с помощью **Конфигурация компьютера**, войдите в клиентский компьютер, который принадлежит toohello Подразделения, выбранного в [шаг 2: создание hello объекта групповой политики](#step-2-create-the-group-policy-object).</span><span class="sxs-lookup"><span data-stu-id="09243-193">If you deployed using **Computer Configuration**, sign into a client machine that belongs toohello OU that you selected in [Step 2: Create hello Group Policy Object](#step-2-create-the-group-policy-object).</span></span> <span data-ttu-id="09243-194">При развертывании с помощью **Конфигурация пользователя**, убедитесь, что toosign в как пользователь, принадлежащий toothat Подразделения.</span><span class="sxs-lookup"><span data-stu-id="09243-194">If you deployed using **User Configuration**, make sure toosign in as a user who belongs toothat OU.</span></span>
2. <span data-ttu-id="09243-195">Может потребоваться несколько входа модули для hello групповой политики изменяется toofully обновления с этого компьютера.</span><span class="sxs-lookup"><span data-stu-id="09243-195">It may take a couple sign ins for hello group policy changes toofully update with this machine.</span></span> <span data-ttu-id="09243-196">Обновление hello tooforce, откройте **командной строки** окна и выполнения hello следующую команду:`gpupdate /force`</span><span class="sxs-lookup"><span data-stu-id="09243-196">tooforce hello update, open a **Command Prompt** window and run hello following command: `gpupdate /force`</span></span>
3. <span data-ttu-id="09243-197">Необходимо перезапустить машину hello для hello установки tootake месте.</span><span class="sxs-lookup"><span data-stu-id="09243-197">You must restart hello machine for hello installation tootake place.</span></span> <span data-ttu-id="09243-198">Загрузки может занять значительно больше времени, чем обычные при hello расширение устанавливает.</span><span class="sxs-lookup"><span data-stu-id="09243-198">Bootup may take significantly more time than usual while hello extension installs.</span></span>
4. <span data-ttu-id="09243-199">После перезагрузки откройте браузер **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="09243-199">After restarting, open **Internet Explorer**.</span></span> <span data-ttu-id="09243-200">На hello правом верхнем углу окна hello, нажмите кнопку **средства** (значок шестеренки hello), а затем выберите **Управление надстройками**.</span><span class="sxs-lookup"><span data-stu-id="09243-200">On hello upper-right corner of hello window, click **Tools** (hello gear icon), and then select **Manage add-ons**.</span></span>
   
    ![Go tooTools > Управление надстройками](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. <span data-ttu-id="09243-202">В hello **Управление надстройками** окна, убедитесь, что hello **расширение панели доступа** установлен и что его **состояние** задано слишком**включено**.</span><span class="sxs-lookup"><span data-stu-id="09243-202">In hello **Manage Add-ons** window, verify that hello **Access Panel Extension** has been installed and that its **Status** has been set too**Enabled**.</span></span>
   
    ![Убедитесь, что hello расширение панели доступа установлен и включен.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a><span data-ttu-id="09243-204">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="09243-204">Related Articles</span></span>
* [<span data-ttu-id="09243-205">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09243-205">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="09243-206">Доступ к приложениям и единый вход с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="09243-206">Application access and single sign-on with Azure Active Directory</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="09243-207">Устранение неполадок hello расширение панели доступа для Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="09243-207">Troubleshooting hello Access Panel Extension for Internet Explorer</span></span>](active-directory-saas-ie-troubleshooting.md)

