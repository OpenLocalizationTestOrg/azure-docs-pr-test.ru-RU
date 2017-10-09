## <a name="prepare-for-akv-integration"></a>Подготовка к интеграции AKV
Интеграция хранилища ключей Azure tooconfigure toouse ВМ SQL Server существует несколько предварительных требований: 

1. [Установите Azure PowerShell](#install-azure-powershell)
2. [Создайте Azure Active Directory](#create-an-azure-active-directory)
3. [Создайте хранилище ключей.](#create-a-key-vault)

Hello следующих разделах описаны эти необходимые условия и hello сведения, которые требуются командлеты PowerShell hello toocollect toolater запуска.

### <a name="install-azure-powershell"></a>Установка Azure PowerShell
Убедитесь, что вы установили hello последнего выпуска пакета SDK Azure PowerShell. Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs).

### <a name="create-an-azure-active-directory"></a>Создайте Azure Active Directory
Во-первых, требуется toohave [Azure Active Directory](https://azure.microsoft.com/trial/get-started-active-directory/) (AAD) в вашей подписке. Помимо много преимуществ это позволяет toogrant разрешение tooyour хранилища ключей для определенных пользователей и приложений.

Далее необходимо зарегистрировать приложение в AAD. Это позволит получить учетную запись субъекта-службы, имеющую ключа хранилища tooyour доступа, который потребуется ВМ. В статье hello хранилище ключей Azure, эти действия можно найти в hello [зарегистрировать приложение в Azure Active Directory](../articles/key-vault/key-vault-get-started.md#register) раздела, или можно в разделе hello действия с снимков экрана в hello **получение удостоверения приложения hello раздел** из [этой записи блога](http://blogs.technet.com/b/kv/archive/2015/01/09/azure-key-vault-step-by-step.aspx). Перед выполнением этих действий, помните, что вы должны hello toocollect следующую информацию во время этого регистрации, которая понадобится в дальнейшем при включении интеграция хранилища ключей Azure в вашей виртуальной Машине SQL.

* После добавления приложения hello найти hello **идентификатор КЛИЕНТА** на hello **Настройка** вкладки.   ![Идентификатор клиента Azure Active Directory](./media/virtual-machines-sql-server-akv-prepare/aad-client-id.png)
  
    Идентификатор клиента Hello назначается более поздней версии toohello **$spName** параметр (имя участника-службы) в tooenable сценария PowerShell hello интеграция хранилища ключей Azure. 
* Кроме того при выполнении этой процедуры при создании ключа скопируйте hello секрет ключа как показано на следующий снимок экрана приветствия. Этот ключ в секрете назначается более поздней версии toohello **$spSecret** (субъекта-службы секрет) параметра в скрипте PowerShell hello.  
    ![Секрет Azure Active Directory](./media/virtual-machines-sql-server-akv-prepare/aad-sp-secret.png)
* Необходимо авторизовать этот новый идентификатор toohave приветствия клиента следующие разрешения доступа: **шифрования**, **расшифровать**, **wrapKey**, **unwrapKey**, **входа**, и **проверить**. Это делается с hello [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/azure/mt603625.aspx) командлета. Дополнительные сведения см. [авторизовать hello приложения toouse hello ключа или секрета](../articles/key-vault/key-vault-get-started.md#authorize).

### <a name="create-a-key-vault"></a>Создайте хранилище ключей.
В порядке toouse хранилище ключей Azure toostore hello ключи, которые будут использоваться для шифрования на виртуальной машине необходим хранилища ключей tooa доступа. Если вы еще не настроили копии хранилища ключей, создайте его, выполнив следующие шаги hello hello [Приступая к работе с хранилищем ключей Azure](../articles/key-vault/key-vault-get-started.md) раздела. Перед выполнением этих действий, обратите внимание, что есть некоторые сведения, необходимые toocollect во время этой установки, понадобится в дальнейшем при включении интеграция хранилища ключей Azure в вашей виртуальной Машине SQL.

При получении toohello создать шаг хранилища ключей, возвращаемых hello Примечание **vaultUri** свойство, которое является URL-адрес хранилища ключей hello. В примере hello в этот шаг, показанный ниже имя хранилища ключей hello ContosoKeyVault, таким образом URL-адрес хранилища ключей hello будет https://contosokeyvault.vault.azure.net/.

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

URL-адрес хранилища ключей Hello назначается более поздней версии toohello **$akvURL** параметр в tooenable сценария PowerShell hello интеграция хранилища ключей Azure.

