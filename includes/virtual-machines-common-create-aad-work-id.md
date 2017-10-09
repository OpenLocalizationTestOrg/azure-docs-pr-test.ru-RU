
<br>

> [!NOTE]
> <span data-ttu-id="2b99a-101">Если вы получили имя пользователя и пароль от администратора, велика вероятность, что у вас уже есть рабочий или учебный идентификатор (иногда его также называют *идентификатором организации*).</span><span class="sxs-lookup"><span data-stu-id="2b99a-101">If you were given a user name and password by an administrator, there's a good chance that you already have a work or school ID (also sometimes called an *organizational ID*).</span></span> <span data-ttu-id="2b99a-102">Если Да, можно немедленно начать toouse вашей учетной записи Azure tooaccess ресурсы Azure, которые ее требуют.</span><span class="sxs-lookup"><span data-stu-id="2b99a-102">If so, you can immediately begin toouse your Azure account tooaccess Azure resources that require one.</span></span> <span data-ttu-id="2b99a-103">Если обнаружится, что нельзя использовать эти ресурсы, может потребоваться tooreturn toothis статьи для получения справки.</span><span class="sxs-lookup"><span data-stu-id="2b99a-103">If you find that you cannot use those resources, you may need tooreturn toothis article for help.</span></span> <span data-ttu-id="2b99a-104">Дополнительные сведения см. в разделе [учетные записи, которые можно использовать для входа в](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) и [подписка Azure — это связанные tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span><span class="sxs-lookup"><span data-stu-id="2b99a-104">For more information, see [Accounts that you can use for sign in](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) and [How an Azure subscription is related tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).</span></span>
> 
> 

<span data-ttu-id="2b99a-105">Hello действия являются простыми.</span><span class="sxs-lookup"><span data-stu-id="2b99a-105">hello steps are simple.</span></span> <span data-ttu-id="2b99a-106">Требуется toolocate выполнен вход на удостоверение в классический портал Azure hello обнаружения домена Azure Active Directory по умолчанию и добавить новый tooit пользователя как соадминистратор Azure.</span><span class="sxs-lookup"><span data-stu-id="2b99a-106">You need toolocate your signed on identity in hello Azure classic portal, discover your default Azure Active Directory domain, and add a new user tooit as an Azure co-administrator.</span></span>

## <a name="locate-your-default-directory-in-hello-azure-classic-portal"></a><span data-ttu-id="2b99a-107">Найдите каталог по умолчанию в hello классический портал Azure</span><span class="sxs-lookup"><span data-stu-id="2b99a-107">Locate your default directory in hello Azure classic portal</span></span>
<span data-ttu-id="2b99a-108">Начните с ведения журналов в toohello [классический портал Azure](https://manage.windowsazure.com) с удостоверением личной учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="2b99a-108">Start by logging in toohello [Azure classic portal](https://manage.windowsazure.com) with your personal Microsoft account identity.</span></span> <span data-ttu-id="2b99a-109">После входа прокрутите вниз на hello левая сторона hello синей панели и нажмите кнопку **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="2b99a-109">After you are logged in, scroll down hello blue panel on hello left side and click **ACTIVE DIRECTORY**.</span></span>

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

<span data-ttu-id="2b99a-111">Давайте начнем с поиска некоторых сведений о вашем удостоверении в Azure.</span><span class="sxs-lookup"><span data-stu-id="2b99a-111">Let's start by finding some information about your identity in Azure.</span></span> <span data-ttu-id="2b99a-112">Вы увидите нечто похожее на hello следующую команду в главной области hello, показывающая, что имеется один каталог по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2b99a-112">You should see something like hello following in hello main pane, showing that you have one default directory.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

<span data-ttu-id="2b99a-113">Давайте выясним некоторые дополнительные сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="2b99a-113">Let's find out some more information about it.</span></span> <span data-ttu-id="2b99a-114">Щелкните строку каталог по умолчанию hello, который обеспечивает высокую в свойства каталога по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="2b99a-114">Click hello default directory row, which brings you into hello default directory properties.</span></span>  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

<span data-ttu-id="2b99a-115">имя домена по умолчанию hello tooview щелкните **ДОМЕНЫ**.</span><span class="sxs-lookup"><span data-stu-id="2b99a-115">tooview hello default domain name, click **DOMAINS**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

<span data-ttu-id="2b99a-116">Здесь можно будет toosee, что при создании hello учетная запись Azure, Azure Active Directory создан домену личные по умолчанию, который является хэш-значение (число, сформированное из текстовой строки) своего личного идентификатора используется в качестве поддомена onmicrosoft.com. Это toowhich домена hello, теперь необходимо добавить нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="2b99a-116">Here you should be able toosee that when hello Azure account was created, Azure Active Directory created a personal default domain that is a hash value (a number generated from a string of text) of your personal ID used as a subdomain of onmicrosoft.com. That's hello domain toowhich you will now add a new user.</span></span>

## <a name="creating-a-new-user-in-hello-default-domain"></a><span data-ttu-id="2b99a-117">Создание нового пользователя в домене по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="2b99a-117">Creating a new user in hello default domain</span></span>
<span data-ttu-id="2b99a-118">Щелкните **ПОЛЬЗОВАТЕЛИ** и найдите среди них личную учетную запись.</span><span class="sxs-lookup"><span data-stu-id="2b99a-118">Click **USERS** and look for your single personal account.</span></span> <span data-ttu-id="2b99a-119">Вы должны увидеть в hello **SOURCED FROM** столбец, который является **учетную запись Майкрософт**.</span><span class="sxs-lookup"><span data-stu-id="2b99a-119">You should see in hello **SOURCED FROM** column that it is a **Microsoft account**.</span></span> <span data-ttu-id="2b99a-120">Мы хотим toocreate пользователя в используемом по умолчанию. onmicrosoft.com домена Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2b99a-120">We want toocreate a user in your default .onmicrosoft.com Azure Active Directory domain.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

<span data-ttu-id="2b99a-121">Мы будем toofollow [эти инструкции](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) в следующих шагах hello, но использовать один из примеров.</span><span class="sxs-lookup"><span data-stu-id="2b99a-121">We're going toofollow [these instructions](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) in hello next few steps, but use a specific example.</span></span>

<span data-ttu-id="2b99a-122">Внизу hello страницы приветствия щелкните **+ добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="2b99a-122">At hello bottom of hello page, click **+ADD USER**.</span></span> <span data-ttu-id="2b99a-123">На появившейся странице hello, введите новое имя пользователя hello и сделать hello **тип пользователя** **новый пользователь в вашей организации**.</span><span class="sxs-lookup"><span data-stu-id="2b99a-123">In hello page that appears, type hello new user name, and make hello **Type of User** a **New user in your organization**.</span></span> <span data-ttu-id="2b99a-124">В этом примере — новое имя пользователя hello `ahmet`.</span><span class="sxs-lookup"><span data-stu-id="2b99a-124">In this example, hello new user name is `ahmet`.</span></span> <span data-ttu-id="2b99a-125">Выберите домен по умолчанию hello, обнаруженной ранее как домен hello ahmet в качестве адреса электронной почты.</span><span class="sxs-lookup"><span data-stu-id="2b99a-125">Select hello default domain that you discovered previously as hello domain for ahmet's email address.</span></span> <span data-ttu-id="2b99a-126">Щелкните стрелку Далее hello после завершения.</span><span class="sxs-lookup"><span data-stu-id="2b99a-126">Click hello next arrow when finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

<span data-ttu-id="2b99a-127">Добавить дополнительные сведения для Ahmet, но убедитесь, что tooselect hello соответствующие **РОЛИ** значение.</span><span class="sxs-lookup"><span data-stu-id="2b99a-127">Add more details for Ahmet, but make sure tooselect hello appropriate **ROLE** value.</span></span> <span data-ttu-id="2b99a-128">Это легко toouse **глобального администратора** toomake что все работает, но при использовании меньшей роли, имеет смысл.</span><span class="sxs-lookup"><span data-stu-id="2b99a-128">It's easy toouse **Global Admin** toomake sure things are working, but if you can use a lesser role, that's a good idea.</span></span> <span data-ttu-id="2b99a-129">В этом примере используется hello **пользователя** роли.</span><span class="sxs-lookup"><span data-stu-id="2b99a-129">This example uses hello **User** role.</span></span> <span data-ttu-id="2b99a-130">(Узнайте больше о [разрешениях администратора на основе роли](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Не включайте многофакторной проверки подлинности, если не требуется, чтобы toouse многофакторной проверки подлинности для каждого журнала, в операции.</span><span class="sxs-lookup"><span data-stu-id="2b99a-130">(Find out more at [Administrator permissions by role](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Do not enable multi-factor authentication unless you want toouse multifactor authentication for each log in operation.</span></span> <span data-ttu-id="2b99a-131">Щелкните стрелку hello при завершении.</span><span class="sxs-lookup"><span data-stu-id="2b99a-131">Click hello next arrow when you're finished.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

<span data-ttu-id="2b99a-132">Нажмите кнопку hello **создания** кнопку toogenerate и отобразить временный пароль для Ahmet.</span><span class="sxs-lookup"><span data-stu-id="2b99a-132">Click hello **create** button toogenerate and display a temporary password for Ahmet.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

<span data-ttu-id="2b99a-133">Скопировать адрес электронной почты имени пользователя hello, или использовать **отправить электронное ПИСЬМО пароль в**.</span><span class="sxs-lookup"><span data-stu-id="2b99a-133">Copy hello user name email address, or use **SEND PASSWORD IN EMAIL**.</span></span> <span data-ttu-id="2b99a-134">Вам потребуется hello toolog сведения на ближайшее время.</span><span class="sxs-lookup"><span data-stu-id="2b99a-134">You'll need hello information toolog on shortly.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

<span data-ttu-id="2b99a-135">Теперь вы увидите новый пользователь hello, **Ahmet hello разработчика**, источника из Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2b99a-135">Now you should see hello new user, **Ahmet hello Developer**, sourced from Azure Active Directory.</span></span> <span data-ttu-id="2b99a-136">Вы создали hello нового рабочего или учебного заведения удостоверение с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2b99a-136">You've created hello new work or school identity with Azure Active Directory.</span></span> <span data-ttu-id="2b99a-137">Тем не менее, это удостоверение еще не toouse разрешения Azure ресурсы.</span><span class="sxs-lookup"><span data-stu-id="2b99a-137">However, this identity does not yet have permissions toouse Azure resources.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

<span data-ttu-id="2b99a-138">При использовании **отправить электронное ПИСЬМО пароль в**, отправляется hello следующий тип электронной почты.</span><span class="sxs-lookup"><span data-stu-id="2b99a-138">If you use **SEND PASSWORD IN EMAIL**, hello following kind of email is sent.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a><span data-ttu-id="2b99a-139">Добавление прав соадминистратора Azure для подписок</span><span class="sxs-lookup"><span data-stu-id="2b99a-139">Adding Azure co-administrator rights for subscriptions</span></span>
<span data-ttu-id="2b99a-140">Теперь вам требуется tooadd hello нового пользователя как соадминистратора подписки, hello новый пользователь сможет войти в toohello портала управления.</span><span class="sxs-lookup"><span data-stu-id="2b99a-140">Now you need tooadd hello new user as a co-administrator of your subscription so hello new user can sign in toohello Management Portal.</span></span> <span data-ttu-id="2b99a-141">Это, на панели слева hello щелкните toodo **параметры**.</span><span class="sxs-lookup"><span data-stu-id="2b99a-141">toodo this, in hello lower-left panel click **Settings**.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

<span data-ttu-id="2b99a-142">Щелкните ссылку в области Основные параметры hello **АДМИНИСТРАТОРЫ** на hello верхней и увидеть только ваш личный удостоверение учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="2b99a-142">In hello main settings area, click **ADMINISTRATORS** at hello top and you should see only your personal Microsoft account identity.</span></span> <span data-ttu-id="2b99a-143">Внизу hello страницы приветствия щелкните **+ добавить** toospecify соадминистратора.</span><span class="sxs-lookup"><span data-stu-id="2b99a-143">At hello bottom of hello page, click **+ADD** toospecify a co-administrator.</span></span> <span data-ttu-id="2b99a-144">Здесь введите адрес электронной почты hello hello нового пользователя, который был создан, включая ваш домен по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2b99a-144">Here, enter hello email address of hello new user you had created, including your default domain.</span></span> <span data-ttu-id="2b99a-145">Как показано на следующем снимке экрана приветствия, зеленая галочка следующий пользователь toohello hello каталога по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2b99a-145">As shown in hello next screenshot, a green check mark appears next toohello user for hello default directory.</span></span> <span data-ttu-id="2b99a-146">Помните, tooselect все подписки hello, желательно этой возможности tooadminister toobe пользователя.</span><span class="sxs-lookup"><span data-stu-id="2b99a-146">Remember tooselect all of hello subscriptions that you would like this user toobe able tooadminister.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

<span data-ttu-id="2b99a-147">После завершения будут отображаться уже два пользователя с новым удостоверением соадминистратора.</span><span class="sxs-lookup"><span data-stu-id="2b99a-147">When you are done, you should now see two users, including your new co-administrator identity.</span></span> <span data-ttu-id="2b99a-148">Выйдите из портала hello.</span><span class="sxs-lookup"><span data-stu-id="2b99a-148">Log out of hello portal.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-hello-new-users-password"></a><span data-ttu-id="2b99a-149">Вход и изменение пароля hello нового пользователя</span><span class="sxs-lookup"><span data-stu-id="2b99a-149">Logging in and changing hello new user's password</span></span>
<span data-ttu-id="2b99a-150">Войдите в систему как созданный новый пользователь hello.</span><span class="sxs-lookup"><span data-stu-id="2b99a-150">Log in as hello new user you created.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

<span data-ttu-id="2b99a-151">Запрашиваемые toocreate новый пароль будет сразу же.</span><span class="sxs-lookup"><span data-stu-id="2b99a-151">You will immediately be prompted toocreate a new password.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

<span data-ttu-id="2b99a-152">Вы должны вознаграждены с успехом, который выглядит как следующий hello.</span><span class="sxs-lookup"><span data-stu-id="2b99a-152">You should be rewarded with success that looks like hello following.</span></span>

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a><span data-ttu-id="2b99a-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2b99a-153">Next steps</span></span>
<span data-ttu-id="2b99a-154">Теперь вы можете использовать ваш новый toouse удостоверение Azure Active Directory [шаблонов группы ресурсов Azure](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="2b99a-154">You can now use your new Azure Active Directory identity toouse [Azure resource group templates](../articles/xplat-cli-azure-resource-manager.md).</span></span>

    azure login
    info:    Executing command login
    warn:    Please note that currently you can login only via Microsoft organizational account or service principal. For instructions on how tooset them up, please read http://aka.ms/Dhf67j.
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
