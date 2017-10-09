
<br>

> [!NOTE]
> Если вы получили имя пользователя и пароль от администратора, велика вероятность, что у вас уже есть рабочий или учебный идентификатор (иногда его также называют *идентификатором организации*). Если Да, можно немедленно начать toouse вашей учетной записи Azure tooaccess ресурсы Azure, которые ее требуют. Если обнаружится, что нельзя использовать эти ресурсы, может потребоваться tooreturn toothis статьи для получения справки. Дополнительные сведения см. в разделе [учетные записи, которые можно использовать для входа в](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SignInAccounts) и [подписка Azure — это связанные tooAzure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx#BKMK_SubRelationToDir).
> 
> 

Hello действия являются простыми. Требуется toolocate выполнен вход на удостоверение в классический портал Azure hello обнаружения домена Azure Active Directory по умолчанию и добавить новый tooit пользователя как соадминистратор Azure.

## <a name="locate-your-default-directory-in-hello-azure-classic-portal"></a>Найдите каталог по умолчанию в hello классический портал Azure
Начните с ведения журналов в toohello [классический портал Azure](https://manage.windowsazure.com) с удостоверением личной учетной записи Майкрософт. После входа прокрутите вниз на hello левая сторона hello синей панели и нажмите кнопку **ACTIVE DIRECTORY**.

![Azure Active Directory](./media/virtual-machines-common-create-aad-work-id/azureactivedirectorywidget.png)

Давайте начнем с поиска некоторых сведений о вашем удостоверении в Azure. Вы увидите нечто похожее на hello следующую команду в главной области hello, показывающая, что имеется один каталог по умолчанию.

![](./media/virtual-machines-common-create-aad-work-id/defaultaadlisting.png)

Давайте выясним некоторые дополнительные сведения о нем. Щелкните строку каталог по умолчанию hello, который обеспечивает высокую в свойства каталога по умолчанию hello.  

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectorypage.png)

имя домена по умолчанию hello tooview щелкните **ДОМЕНЫ**.

![](./media/virtual-machines-common-create-aad-work-id/domainclicktoseeyourdefaultdomain.png)

Здесь можно будет toosee, что при создании hello учетная запись Azure, Azure Active Directory создан домену личные по умолчанию, который является хэш-значение (число, сформированное из текстовой строки) своего личного идентификатора используется в качестве поддомена onmicrosoft.com. Это toowhich домена hello, теперь необходимо добавить нового пользователя.

## <a name="creating-a-new-user-in-hello-default-domain"></a>Создание нового пользователя в домене по умолчанию hello
Щелкните **ПОЛЬЗОВАТЕЛИ** и найдите среди них личную учетную запись. Вы должны увидеть в hello **SOURCED FROM** столбец, который является **учетную запись Майкрософт**. Мы хотим toocreate пользователя в используемом по умолчанию. onmicrosoft.com домена Azure Active Directory.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryuserslisting.png)

Мы будем toofollow [эти инструкции](https://technet.microsoft.com/library/hh967632.aspx#BKMK_1) в следующих шагах hello, но использовать один из примеров.

Внизу hello страницы приветствия щелкните **+ добавить пользователя**. На появившейся странице hello, введите новое имя пользователя hello и сделать hello **тип пользователя** **новый пользователь в вашей организации**. В этом примере — новое имя пользователя hello `ahmet`. Выберите домен по умолчанию hello, обнаруженной ранее как домен hello ahmet в качестве адреса электронной почты. Щелкните стрелку Далее hello после завершения.

![](./media/virtual-machines-common-create-aad-work-id/addingauserwithdirectorydropdown.png)

Добавить дополнительные сведения для Ahmet, но убедитесь, что tooselect hello соответствующие **РОЛИ** значение. Это легко toouse **глобального администратора** toomake что все работает, но при использовании меньшей роли, имеет смысл. В этом примере используется hello **пользователя** роли. (Узнайте больше о [разрешениях администратора на основе роли](https://msdn.microsoft.com/library/azure/dn468213.aspx#BKMK_1).) Не включайте многофакторной проверки подлинности, если не требуется, чтобы toouse многофакторной проверки подлинности для каждого журнала, в операции. Щелкните стрелку hello при завершении.

![](./media/virtual-machines-common-create-aad-work-id/userprofileuseradmin.png)

Нажмите кнопку hello **создания** кнопку toogenerate и отобразить временный пароль для Ahmet.

![](./media/virtual-machines-common-create-aad-work-id/gettemporarypasswordforuser.png)

Скопировать адрес электронной почты имени пользователя hello, или использовать **отправить электронное ПИСЬМО пароль в**. Вам потребуется hello toolog сведения на ближайшее время.

![](./media/virtual-machines-common-create-aad-work-id/receivedtemporarypassworddialog.png)

Теперь вы увидите новый пользователь hello, **Ahmet hello разработчика**, источника из Azure Active Directory. Вы создали hello нового рабочего или учебного заведения удостоверение с Azure Active Directory. Тем не менее, это удостоверение еще не toouse разрешения Azure ресурсы.

![](./media/virtual-machines-common-create-aad-work-id/defaultdirectoryusersaftercreate.png)

При использовании **отправить электронное ПИСЬМО пароль в**, отправляется hello следующий тип электронной почты.

![](./media/virtual-machines-common-create-aad-work-id/emailreceivedfromnewusercreation.png)

## <a name="adding-azure-co-administrator-rights-for-subscriptions"></a>Добавление прав соадминистратора Azure для подписок
Теперь вам требуется tooadd hello нового пользователя как соадминистратора подписки, hello новый пользователь сможет войти в toohello портала управления. Это, на панели слева hello щелкните toodo **параметры**.

![](./media/virtual-machines-common-create-aad-work-id/thesettingswidget.png)

Щелкните ссылку в области Основные параметры hello **АДМИНИСТРАТОРЫ** на hello верхней и увидеть только ваш личный удостоверение учетной записи Майкрософт. Внизу hello страницы приветствия щелкните **+ добавить** toospecify соадминистратора. Здесь введите адрес электронной почты hello hello нового пользователя, который был создан, включая ваш домен по умолчанию. Как показано на следующем снимке экрана приветствия, зеленая галочка следующий пользователь toohello hello каталога по умолчанию. Помните, tooselect все подписки hello, желательно этой возможности tooadminister toobe пользователя.

![](./media/virtual-machines-common-create-aad-work-id/addingnewuserascoadmin.png)

После завершения будут отображаться уже два пользователя с новым удостоверением соадминистратора. Выйдите из портала hello.

![](./media/virtual-machines-common-create-aad-work-id/newuseraddedascoadministrator.png)

## <a name="logging-in-and-changing-hello-new-users-password"></a>Вход и изменение пароля hello нового пользователя
Войдите в систему как созданный новый пользователь hello.

![](./media/virtual-machines-common-create-aad-work-id/signinginwithnewuser.png)

Запрашиваемые toocreate новый пароль будет сразу же.

![](./media/virtual-machines-common-create-aad-work-id/mustupdateyourpassword.png)

Вы должны вознаграждены с успехом, который выглядит как следующий hello.

![](./media/virtual-machines-common-create-aad-work-id/successtourdialog.png)

## <a name="next-steps"></a>Дальнейшие действия
Теперь вы можете использовать ваш новый toouse удостоверение Azure Active Directory [шаблонов группы ресурсов Azure](../articles/xplat-cli-azure-resource-manager.md).

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
