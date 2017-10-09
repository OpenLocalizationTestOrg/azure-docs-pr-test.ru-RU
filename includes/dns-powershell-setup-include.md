## <a name="set-up-azure-powershell-for-azure-dns"></a>Настройка Azure PowerShell для Azure DNS

### <a name="before-you-begin"></a>Перед началом работы

Проверьте наличие следующих элементов перед началом настройки hello.

* Подписка Azure. Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).
* Необходимо tooinstall hello последнюю версию hello командлеты PowerShell диспетчера ресурсов Azure. Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs).

### <a name="sign-in-tooyour-azure-account"></a>Войдите в tooyour учетная запись Azure

Откройте консоль PowerShell и подключить tooyour учетную запись. Дополнительные сведения см. в статье [Использование Azure PowerShell с диспетчером ресурсов Azure](../articles/azure-resource-manager/powershell-azure-resource-manager.md).

```powershell
Login-AzureRmAccount
```

### <a name="select-hello-subscription"></a>Выберите подписку hello
 
Проверьте hello подписки для учетной записи hello.

```powershell
Get-AzureRmSubscription
```

Выберите, какие toouse вашей подписки Azure.

```powershell
Select-AzureRmSubscription -SubscriptionName "your_subscription_name"
```

### <a name="create-a-resource-group"></a>Создание группы ресурсов

В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение. Это расположение используется в качестве расположения по умолчанию hello для ресурсов в этой группе ресурсов. Тем не менее так как все ресурсы DNS глобального, не язык, выбор hello расположение группы ресурсов не оказывает влияния на Azure DNS.

Если используется существующая группа ресурсов, можно пропустить этот шаг.

```powershell
New-AzureRmResourceGroup -Name MyAzureResourceGroup -location "West US"
```

### <a name="register-resource-provider"></a>Регистрация поставщика ресурсов

Служба Azure DNS Hello управляется поставщика ресурсов Microsoft.Network hello. Ваша подписка Azure должен быть зарегистрированных toouse этого поставщика ресурсов, прежде чем можно будет использовать Azure DNS. Эта операция выполняется один раз для каждой подписки.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```