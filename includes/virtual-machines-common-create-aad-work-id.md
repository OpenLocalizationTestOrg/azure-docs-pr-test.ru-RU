
<br>

> [!NOTE]
> <span data-ttu-id="37a6f-101">Если вы получили имя пользователя и пароль от администратора, велика вероятность, что у вас уже есть рабочий или учебный идентификатор (иногда его также называют *идентификатором организации*).</span><span class="sxs-lookup"><span data-stu-id="37a6f-101">If you were given a user name and password by an administrator, there's a good chance that you already have a work or school ID (also sometimes called an *organizational ID*).</span></span> <span data-ttu-id="37a6f-102">В этом случае можно сразу начать использовать учетную запись Azure для доступа к ресурсам Azure, которым она требуется.</span><span class="sxs-lookup"><span data-stu-id="37a6f-102">If so, you can immediately begin to use your Azure account to access Azure resources that require one.</span></span> <span data-ttu-id="37a6f-103">Если вы обнаружили, что не можете воспользоваться этими ресурсами, возможно, вам понадобится вернуться к этой статье.</span><span class="sxs-lookup"><span data-stu-id="37a6f-103">If you find that you cannot use those resources, you may need to return to this article for help.</span></span> <span data-ttu-id="37a6f-104">Дополнительные сведения см. в разделах [Учетные записи, которые можно использовать для входа](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) и [Как подписка Azure связана с Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span><span class="sxs-lookup"><span data-stu-id="37a6f-104">For more information, see [Accounts that you can use for sign in](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) and [How an Azure subscription is related to Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span></span>
> 
> 

<span data-ttu-id="37a6f-105">Необходимые действия просты.</span><span class="sxs-lookup"><span data-stu-id="37a6f-105">The steps are simple.</span></span> <span data-ttu-id="37a6f-106">Вам нужно найти на классическом портале Azure свое подписанное удостоверение, выяснить свой домен Azure Active Directory по умолчанию и добавить в него нового пользователя в качестве соадминистратора Azure.</span><span class="sxs-lookup"><span data-stu-id="37a6f-106">You need to locate your signed on identity in the Azure classic portal, discover your default Azure Active Directory domain, and add a new user to it as an Azure co-administrator.</span></span>

## <a name="locate-your-default-directory-in-the-azure-classic-portal"></a><span data-ttu-id="37a6f-107">Найдите каталог по умолчанию на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="37a6f-107">Locate your default directory in the Azure classic portal</span></span>
<span data-ttu-id="37a6f-108">Перейдите на [классический портал Azure](https://manage.windowsazure.com) с помощью личного удостоверения учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="37a6f-108">Start by logging in to the [Azure classic portal](https://manage.windowsazure.com) with your personal Microsoft account identity.</span></span> <span data-ttu-id="37a6f-109">После входа прокрутите синюю панель слева и щелкните **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="37a6f-109">After you are logged in, scroll down the blue panel on the left side and click **ACTIVE DIRECTORY**.</span></span>

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

<span data-ttu-id="37a6f-111">Давайте начнем с поиска некоторых сведений о вашем удостоверении в Azure.</span><span class="sxs-lookup"><span data-stu-id="37a6f-111">Let's start by finding some information about your identity in Azure.</span></span> <span data-ttu-id="37a6f-112">В главной области должны отображаться сведения, подобные указанным ниже, показывающие, что у вас есть один каталог по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="37a6f-112">You should see something like the following in the main pane, showing that you have one default directory.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

<span data-ttu-id="37a6f-113">Давайте выясним некоторые дополнительные сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="37a6f-113">Let's find out some more information about it.</span></span> <span data-ttu-id="37a6f-114">Щелкните строку каталога по умолчанию, чтобы открыть свойства этого каталога.</span><span class="sxs-lookup"><span data-stu-id="37a6f-114">Click the default directory row, which brings you into the default directory properties.</span></span>  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

<span data-ttu-id="37a6f-115">Чтобы просмотреть имя домена по умолчанию, щелкните **ДОМЕНЫ**.</span><span class="sxs-lookup"><span data-stu-id="37a6f-115">To view the default domain name, click **DOMAINS**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

<span data-ttu-id="37a6f-116">Здесь можно увидеть, что при создании учетной записи Azure служба Azure Active Directory создала личный домен по умолчанию, представляющий собой значение хэша (число, формируемое по текстовой строке) вашего личного идентификатора, используемого как поддомен onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="37a6f-116">Here you should be able to see that when the Azure account was created, Azure Active Directory created a personal default domain that is a hash value (a number generated from a string of text) of your personal ID used as a subdomain of onmicrosoft.com.</span></span> <span data-ttu-id="37a6f-117">Это домен, в который теперь мы добавим нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="37a6f-117">That's the domain to which you will now add a new user.</span></span>

## <a name="creating-a-new-user-in-the-default-domain"></a><span data-ttu-id="37a6f-118">Создание нового пользователя в домене по умолчанию</span><span class="sxs-lookup"><span data-stu-id="37a6f-118">Creating a new user in the default domain</span></span>
<span data-ttu-id="37a6f-119">Щелкните **ПОЛЬЗОВАТЕЛИ** и найдите среди них личную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="37a6f-119">Click **USERS** and look for your single personal account.</span></span> <span data-ttu-id="37a6f-120">В столбце **Источник** можно увидеть, что это **учетная запись Майкрософт**.</span><span class="sxs-lookup"><span data-stu-id="37a6f-120">You should see in the **SOURCED FROM** column that it is a **Microsoft account**.</span></span> <span data-ttu-id="37a6f-121">Мы хотим создать пользователя в используемом по умолчанию домене Azure Active Directory .onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="37a6f-121">We want to create a user in your default .onmicrosoft.com Azure Active Directory domain.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

<span data-ttu-id="37a6f-122">Дальше мы будем выполнять [эти инструкции](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) , но на конкретном примере.</span><span class="sxs-lookup"><span data-stu-id="37a6f-122">We're going to follow [these instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in the next few steps, but use a specific example.</span></span>

<span data-ttu-id="37a6f-123">Внизу страницы щелкните **+ДОБАВИТЬ ПОЛЬЗОВАТЕЛЯ**.</span><span class="sxs-lookup"><span data-stu-id="37a6f-123">At the bottom of the page, click **+ADD USER**.</span></span> <span data-ttu-id="37a6f-124">На открывшейся странице введите имя нового пользователя, а в поле **Тип пользователя** выберите **Новый пользователь в вашей организации**.</span><span class="sxs-lookup"><span data-stu-id="37a6f-124">In the page that appears, type the new user name, and make the **Type of User** a **New user in your organization**.</span></span> <span data-ttu-id="37a6f-125">В этом примере новое имя пользователя — `ahmet`.</span><span class="sxs-lookup"><span data-stu-id="37a6f-125">In this example, the new user name is `ahmet`.</span></span> <span data-ttu-id="37a6f-126">Выберите домен по умолчанию, обнаруженный ранее, в качестве домена для адреса электронной почты пользователя Ahmet.</span><span class="sxs-lookup"><span data-stu-id="37a6f-126">Select the default domain that you discovered previously as the domain for ahmet's email address.</span></span> <span data-ttu-id="37a6f-127">После завершения щелкните стрелку «Далее».</span><span class="sxs-lookup"><span data-stu-id="37a6f-127">Click the next arrow when finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

<span data-ttu-id="37a6f-128">Введите дополнительные сведения о пользователе Ahmet и обязательно выберите соответствующее значение **Роль**.</span><span class="sxs-lookup"><span data-stu-id="37a6f-128">Add more details for Ahmet, but make sure to select the appropriate **ROLE** value.</span></span> <span data-ttu-id="37a6f-129">Для гарантированной работы используйте роль **Глобальный администратор**, но если есть возможность использовать роль с меньшими полномочиями, это прекрасно.</span><span class="sxs-lookup"><span data-stu-id="37a6f-129">It's easy to use **Global Admin** to make sure things are working, but if you can use a lesser role, that's a good idea.</span></span> <span data-ttu-id="37a6f-130">В этом примере используется роль **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="37a6f-130">This example uses the **User** role.</span></span> <span data-ttu-id="37a6f-131">(Узнайте больше о [разрешениях администратора на основе роли](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Не включайте многофакторную проверку подлинности, если только не хотите использовать ее для каждой операции входа.</span><span class="sxs-lookup"><span data-stu-id="37a6f-131">(Find out more at [Administrator permissions by role](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Do not enable multi-factor authentication unless you want to use multifactor authentication for each log in operation.</span></span> <span data-ttu-id="37a6f-132">После завершения щелкните стрелку «Далее».</span><span class="sxs-lookup"><span data-stu-id="37a6f-132">Click the next arrow when you're finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

<span data-ttu-id="37a6f-133">Нажмите кнопку **Создать** , чтобы создать и отобразить временный пароль для пользователя Ahmet.</span><span class="sxs-lookup"><span data-stu-id="37a6f-133">Click the **create** button to generate and display a temporary password for Ahmet.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

<span data-ttu-id="37a6f-134">Скопируйте электронный адрес пользователя или используйте функцию **ОТПРАВИТЬ ПАРОЛЬ ПО ЭЛЕКТРОННОЙ ПОЧТЕ**.</span><span class="sxs-lookup"><span data-stu-id="37a6f-134">Copy the user name email address, or use **SEND PASSWORD IN EMAIL**.</span></span> <span data-ttu-id="37a6f-135">Вскоре вам понадобятся данные для входа.</span><span class="sxs-lookup"><span data-stu-id="37a6f-135">You'll need the information to log on shortly.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

<span data-ttu-id="37a6f-136">Теперь вы должны видеть нового пользователя, в этом случае **Ahmet the Developer**, созданного в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="37a6f-136">Now you should see the new user, **Ahmet the Developer**, sourced from Azure Active Directory.</span></span> <span data-ttu-id="37a6f-137">Вы создали новое рабочее или школьное удостоверение с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="37a6f-137">You've created the new work or school identity with Azure Active Directory.</span></span> <span data-ttu-id="37a6f-138">Но это удостоверение еще не имеет разрешений на использование ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="37a6f-138">However, this identity does not yet have permissions to use Azure resources.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

<span data-ttu-id="37a6f-139">При использовании функции **ОТПРАВИТЬ ПАРОЛЬ ПО ЭЛЕКТРОННОЙ ПОЧТЕ**отправляется электронное сообщение следующего вида.</span><span class="sxs-lookup"><span data-stu-id="37a6f-139">If you use **SEND PASSWORD IN EMAIL**, the following kind of email is sent.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a><span data-ttu-id="37a6f-140">Добавление прав соадминистратора Azure для подписок</span><span class="sxs-lookup"><span data-stu-id="37a6f-140">Adding Azure co-administrator rights for subscriptions</span></span>
<span data-ttu-id="37a6f-141">Теперь необходимо добавить нового пользователя в качестве соадминистратора, чтобы новый пользователь мог войти на портал управления.</span><span class="sxs-lookup"><span data-stu-id="37a6f-141">Now you need to add the new user as a co-administrator of your subscription so the new user can sign in to the Management Portal.</span></span> <span data-ttu-id="37a6f-142">Чтобы сделать это, на панели внизу слева щелкните **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="37a6f-142">To do this, in the lower-left panel click **Settings**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

<span data-ttu-id="37a6f-143">В области основных параметров вверху щелкните **АДМИНИСТРАТОРЫ** , после чего должно отобразиться только ваше личное удостоверение учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="37a6f-143">In the main settings area, click **ADMINISTRATORS** at the top and you should see only your personal Microsoft account identity.</span></span> <span data-ttu-id="37a6f-144">Внизу страницы щелкните **+ДОБАВИТЬ** , чтобы указать соадминистратора.</span><span class="sxs-lookup"><span data-stu-id="37a6f-144">At the bottom of the page, click **+ADD** to specify a co-administrator.</span></span> <span data-ttu-id="37a6f-145">Здесь нужно ввести адрес электронной почты нового пользователя, которого вы создали, с доменом по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="37a6f-145">Here, enter the email address of the new user you had created, including your default domain.</span></span> <span data-ttu-id="37a6f-146">Как показано на следующем снимке экрана, рядом с пользователем каталога по умолчанию отображается зеленая галочка.</span><span class="sxs-lookup"><span data-stu-id="37a6f-146">As shown in the next screenshot, a green check mark appears next to the user for the default directory.</span></span> <span data-ttu-id="37a6f-147">Не забудьте выбрать все подписки, возможность администрирования которых следует добавить этому пользователю.</span><span class="sxs-lookup"><span data-stu-id="37a6f-147">Remember to select all of the subscriptions that you would like this user to be able to administer.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

<span data-ttu-id="37a6f-148">После завершения будут отображаться уже два пользователя с новым удостоверением соадминистратора.</span><span class="sxs-lookup"><span data-stu-id="37a6f-148">When you are done, you should now see two users, including your new co-administrator identity.</span></span> <span data-ttu-id="37a6f-149">Выйдите из портала.</span><span class="sxs-lookup"><span data-stu-id="37a6f-149">Log out of the portal.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-the-new-users-password"></a><span data-ttu-id="37a6f-150">Вход и изменение пароля нового пользователя</span><span class="sxs-lookup"><span data-stu-id="37a6f-150">Logging in and changing the new user's password</span></span>
<span data-ttu-id="37a6f-151">Войдите в систему в качестве созданного вами нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="37a6f-151">Log in as the new user you created.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

<span data-ttu-id="37a6f-152">Вам будет немедленно предложено создать новый пароль.</span><span class="sxs-lookup"><span data-stu-id="37a6f-152">You will immediately be prompted to create a new password.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

<span data-ttu-id="37a6f-153">Вы получите вознаграждение за свои старания, которое выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="37a6f-153">You should be rewarded with success that looks like the following.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a><span data-ttu-id="37a6f-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="37a6f-154">Next steps</span></span>
<span data-ttu-id="37a6f-155">С помощью нового удостоверения Azure Active Directory можно использовать [шаблоны групп ресурсов Azure](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="37a6f-155">You can now use your new Azure Active Directory identity to use [Azure resource group templates](../articles/xplat-cli-azure-resource-manager.md).</span></span>

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how to set them up, please read http://aka.ms/Dhf67j.
    Username: ahmet@aztrainpassxxxxxoutlook.onmicrosoft.com
    Password: *********
    /info:    Added subscription Azure Pass
    info:    Setting subscription Azure Pass as default
    +
    info:    login command OK
    ralph@local:~$ azure config mode arm
    info:    New mode is arm
    ralph@local:~$ azure group list
    info:    Executing command group list
    + Listing resource groups
    info:    No matched resource groups were found
    info:    group list command OK
    ralph@local:~$ azure group create newgroup westus
    info:    Executing command group create
    + Getting resource group newgroup
    + Creating resource group newgroup
    info:    Created resource group newgroup
    data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/newgroup
    data:    Name:                newgroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags:
    data:
    info:    group create command OK
