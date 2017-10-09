экземпляр кэша Azure Redis tooan tooconnect, клиенты кэша должны hello имя узла, порты и ключей кэша hello. Некоторые клиенты могут ссылаться элементы toothese немного разные имена. Можно получить эту информацию в hello портал Azure или с помощью средства командной строки, таких как Azure CLI.

### <a name="retrieve-host-name-ports-and-access-keys-using-hello-azure-portal"></a>Получить имя узла, порта и клавиши доступа, с помощью портала Azure hello
tooretrieve имя узла, порты и клавиши доступа, с помощью портала Azure hello [Обзор](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour кэша в hello [портал Azure](https://portal.azure.com) и нажмите кнопку **ключи доступа** и  **Свойства** в hello **ресурсов меню**. 

![Параметры кэша Redis](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a>Получение имени узла, портов и ключей доступа с помощью Azure CLI
Имя узла tooretrieve hello и портам с помощью Azure CLI 2.0 можно вызвать [Показать az redis](https://docs.microsoft.com/cli/azure/redis#show)и tooretrieve hello ключей, вы можете вызвать [az redis список ключей](https://docs.microsoft.com/cli/azure/redis#list-keys). Hello следующий скрипт вызывает эти две команды и Здравствуйте, обозначающие имя узла, порты и ключи toohello консоли.

```azurecli
#/bin/bash

# Retrieve hello hostname, ports, and keys for contosoCache located in contosoGroup

# Retrieve hello hostname and ports for an Azure Redis Cache instance
redis=($(az redis show --name contosoCache --resource-group contosoGroup --query [hostName,enableNonSslPort,port,sslPort] --output tsv))

# Retrieve hello keys for an Azure Redis Cache instance
keys=($(az redis list-keys --name contosoCache --resource-group contosoGroup --query [primaryKey,secondaryKey] --output tsv))

# Display hello retrieved hostname, keys, and ports
echo "Hostname:" ${redis[0]}
echo "Non SSL Port:" ${redis[2]}
echo "Non SSL Port Enabled:" ${redis[1]}
echo "SSL Port:" ${redis[3]}
echo "Primary Key:" ${keys[0]}
echo "Secondary Key:" ${keys[1]}
```

Дополнительные сведения об этом сценарии см. в разделе [получить имя узла hello, порты и ключи для кэша Azure Redis](../articles/redis-cache/scripts/cache-keys-ports.md). Дополнительные сведения об Azure CLI 2.0 см. в статье [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Установка Azure CLI 2.0) и [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) (Приступая к работе с Azure CLI 2.0).
