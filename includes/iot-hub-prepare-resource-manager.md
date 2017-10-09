## <a name="prepare-tooauthenticate-azure-resource-manager-requests"></a>Подготовка tooauthenticate запросов диспетчера ресурсов Azure
Вы должны пройти проверку подлинности всех hello операций, выполняемых с ресурсами с помощью hello [диспетчера ресурсов Azure] [ lnk-authenticate-arm] с Azure Active Directory (AD). Здравствуйте, наиболее простым способом tooconfigure toouse PowerShell или Azure CLI.

Установка hello [командлетов Azure PowerShell] [ lnk-powershell-install] перед продолжением.

Здравствуйте, следующие шаги Показать как tooset проверку подлинности пароль для приложения AD с помощью PowerShell. Эти команды можно выполнять в обычном сеансе PowerShell.

1. Вход tooyour подписку Azure с помощью hello следующую команду:

    ```powershell
    Login-AzureRmAccount
    ```

1. Если у вас несколько подписок Azure, предоставляет доступ tooall вход tooAzure hello подписок Azure, связанных с учетными данными. Используйте следующую команду, toolist hello подписки Azure доступны для вас toouse hello.

    ```powershell
    Get-AzureRMSubscription
    ```

    Используется следующая команда tooselect подписки требуется toouse toorun hello команды toomanage концентратор IoT hello. Можно использовать имя подписки hello или идентификатор из hello выходные данные предыдущей команды hello:

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

2. Обратите внимание на **TenantId** и **SubscriptionId**. Они потребуются вам позднее.
3. Создайте новое приложение Azure Active Directory с помощью hello следующую команду, заменив заполнителями hello:
   
   * **{Display name}:** отображаемое имя вашего приложения, например **MySampleApp**.
   * **{URL-адрес домашней страницы}:** hello URL-адрес домашней страницы приложения hello, таких как **http://mysampleapp/home**. Этот URL-адрес не обязательно toopoint tooa реальному приложению.
   * **{Application identifier}:** уникальный идентификатор, например **http://mysampleapp**. Этот URL-адрес не обязательно toopoint tooa реальному приложению.
   * **{Password}:** пароль, использовать tooauthenticate вместе с приложением.
     
     ```powershell
     New-AzureRmADApplication -DisplayName {Display name} -HomePage {Home page URL} -IdentifierUris {Application identifier} -Password {Password}
     ```
4. Запишите hello **ApplicationId** приложения hello, вы создали. Этот идентификатор потребуется позднее.
5. Создание нового субъекта-службы с помощью hello следующую команду, заменив **{MyApplicationId}** с hello **ApplicationId** из предыдущего шага hello:
   
    ```powershell
    New-AzureRmADServicePrincipal -ApplicationId {MyApplicationId}
    ```
6. Настройка назначения роли с помощью hello следующую команду, заменив **{MyApplicationId}** с вашей **ApplicationId**.
   
    ```powershell
    New-AzureRmRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName {MyApplicationId}
    ```

Создание приложения hello Azure AD, позволяющая tooauthenticate из вашего приложения C# завершена. Необходимы следующие значения в этом руководстве позднее hello.

* TenantId
* SubscriptionId
* ApplicationId
* Пароль

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
