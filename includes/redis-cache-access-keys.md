<span data-ttu-id="d214c-101">экземпляр кэша Azure Redis tooan tooconnect, клиенты кэша должны hello имя узла, порты и ключей кэша hello.</span><span class="sxs-lookup"><span data-stu-id="d214c-101">tooconnect tooan Azure Redis Cache instance, cache clients need hello host name, ports, and keys of hello cache.</span></span> <span data-ttu-id="d214c-102">Некоторые клиенты могут ссылаться элементы toothese немного разные имена.</span><span class="sxs-lookup"><span data-stu-id="d214c-102">Some clients may refer toothese items by slightly different names.</span></span> <span data-ttu-id="d214c-103">Можно получить эту информацию в hello портал Azure или с помощью средства командной строки, таких как Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d214c-103">You can retrieve this information in hello Azure portal or by using command-line tools such as Azure CLI.</span></span>

### <a name="retrieve-host-name-ports-and-access-keys-using-hello-azure-portal"></a><span data-ttu-id="d214c-104">Получить имя узла, порта и клавиши доступа, с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="d214c-104">Retrieve host name, ports, and access keys using hello Azure Portal</span></span>
<span data-ttu-id="d214c-105">tooretrieve имя узла, порты и клавиши доступа, с помощью портала Azure hello [Обзор](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour кэша в hello [портал Azure](https://portal.azure.com) и нажмите кнопку **ключи доступа** и  **Свойства** в hello **ресурсов меню**.</span><span class="sxs-lookup"><span data-stu-id="d214c-105">tooretrieve host name, ports, and access keys using hello Azure Portal, [browse](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour cache in hello [Azure portal](https://portal.azure.com) and click **Access keys** and **Properties** in hello **Resource menu**.</span></span> 

![Параметры кэша Redis](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a><span data-ttu-id="d214c-107">Получение имени узла, портов и ключей доступа с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d214c-107">Retrieve host name, ports, and access keys using Azure CLI</span></span>
<span data-ttu-id="d214c-108">Имя узла tooretrieve hello и портам с помощью Azure CLI 2.0 можно вызвать [Показать az redis](https://docs.microsoft.com/cli/azure/redis#show)и tooretrieve hello ключей, вы можете вызвать [az redis список ключей](https://docs.microsoft.com/cli/azure/redis#list-keys).</span><span class="sxs-lookup"><span data-stu-id="d214c-108">tooretrieve hello host name and ports using Azure CLI 2.0 you can call [az redis show](https://docs.microsoft.com/cli/azure/redis#show), and tooretrieve hello keys you can call [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys).</span></span> <span data-ttu-id="d214c-109">Hello следующий скрипт вызывает эти две команды и Здравствуйте, обозначающие имя узла, порты и ключи toohello консоли.</span><span class="sxs-lookup"><span data-stu-id="d214c-109">hello following script calls these two commands and echos hello hostname, ports, and keys toohello console.</span></span>

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

<span data-ttu-id="d214c-110">Дополнительные сведения об этом сценарии см. в разделе [получить имя узла hello, порты и ключи для кэша Azure Redis](../articles/redis-cache/scripts/cache-keys-ports.md).</span><span class="sxs-lookup"><span data-stu-id="d214c-110">For more information about this script, see [Get hello hostname, ports, and keys for Azure Redis Cache](../articles/redis-cache/scripts/cache-keys-ports.md).</span></span> <span data-ttu-id="d214c-111">Дополнительные сведения об Azure CLI 2.0 см. в статье [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (Установка Azure CLI 2.0) и [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) (Приступая к работе с Azure CLI 2.0).</span><span class="sxs-lookup"><span data-stu-id="d214c-111">For more information on Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>
