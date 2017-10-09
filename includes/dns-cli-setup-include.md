## <a name="set-up-azure-cli-for-azure-dns"></a>Настройка интерфейса командной строки Azure для Azure DNS

### <a name="before-you-begin"></a>Перед началом работы

Проверьте наличие следующих элементов перед началом настройки hello.

* Подписка Azure. Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).
* Установите последнюю версию hello hello Azure CLI, доступные для Windows, Linux или MAC. Дополнительные сведения можно найти по адресу [Install hello Azure CLI](../articles/cli-install-nodejs.md).

### <a name="sign-in-tooyour-azure-account"></a>Войдите в tooyour учетная запись Azure

Откройте окно консоли и пройдите проверку подлинности с помощью своих учетных данных. Дополнительные сведения см. в разделе [входа tooAzure из hello Azure CLI](../articles/xplat-cli-connect.md)

```azurecli
azure login
```

### <a name="switch-cli-mode"></a>Переключение режима интерфейса командной строки

Azure DNS использует диспетчер ресурсов Azure. Убедитесь, что переключение команд диспетчера ресурсов Azure toouse режиме CLI.

```azurecli
azure config mode arm
```

### <a name="select-hello-subscription"></a>Выберите подписку hello

Проверьте hello подписки для учетной записи hello.

```azurecli
azure account list
```

Выберите, какие toouse вашей подписки Azure.

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a>Создание группы ресурсов

В диспетчере ресурсов Azure для всех групп ресурсов должно быть указано расположение. Используется как расположение по умолчанию hello для ресурсов в этой группе ресурсов. Тем не менее так как все ресурсы DNS глобального, не язык, выбор hello расположение группы ресурсов не оказывает влияния на Azure DNS.

Если используется существующая группа ресурсов, можно пропустить этот шаг.

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a>Регистрация поставщика ресурсов

Служба Azure DNS Hello управляется поставщика ресурсов Microsoft.Network hello. Ваша подписка Azure должен быть зарегистрированных toouse этого поставщика ресурсов, прежде чем можно будет использовать Azure DNS. Эта операция выполняется один раз для каждой подписки.

```azurecli
azure provider register --namespace Microsoft.Network
```

