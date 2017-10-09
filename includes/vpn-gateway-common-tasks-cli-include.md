### <a name="tooview-local-network-gateways"></a><span data-ttu-id="4c11b-101">tooview локальных сетевых шлюзов</span><span class="sxs-lookup"><span data-stu-id="4c11b-101">tooview local network gateways</span></span>

<span data-ttu-id="4c11b-102">список локальных сетевых шлюзов hello, используйте hello tooview [список шлюза локальной сети az](https://docs.microsoft.com/cli/azure/network/local-gateway#list) команды.</span><span class="sxs-lookup"><span data-stu-id="4c11b-102">tooview a list of hello local network gateways, use hello [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#list) command.</span></span>

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a><span data-ttu-id="4c11b-103">tooverify hello общих значений ключей</span><span class="sxs-lookup"><span data-stu-id="4c11b-103">tooverify hello shared key values</span></span>

<span data-ttu-id="4c11b-104">Убедитесь, что значение ключа hello общих hello же значение, которое используется для конфигурации устройства VPN.</span><span class="sxs-lookup"><span data-stu-id="4c11b-104">Verify that hello shared key value is hello same value that you used for your VPN device configuration.</span></span> <span data-ttu-id="4c11b-105">Если это не так, выполнить снова, используя значение hello с устройства hello подключения hello или обновить устройство hello hello значением из возвращаемого hello.</span><span class="sxs-lookup"><span data-stu-id="4c11b-105">If it is not, either run hello connection again using hello value from hello device, or update hello device with hello value from hello return.</span></span> <span data-ttu-id="4c11b-106">Hello значения должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="4c11b-106">hello values must match.</span></span> <span data-ttu-id="4c11b-107">tooview hello общий ключ, используйте hello [az сетевой список vpn подключения](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span><span class="sxs-lookup"><span data-stu-id="4c11b-107">tooview hello shared key, use hello [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span></span>

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a><span data-ttu-id="4c11b-108">шлюз VPN hello tooview общедоступный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="4c11b-108">tooview hello VPN gateway Public IP address</span></span>

<span data-ttu-id="4c11b-109">toofind hello общедоступный IP-адрес шлюза виртуальной сети, используйте hello [список открытый ip-сетей az](https://docs.microsoft.com/cli/azure/network/public-ip#list) команды.</span><span class="sxs-lookup"><span data-stu-id="4c11b-109">toofind hello public IP address of your virtual network gateway, use hello [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="4c11b-110">Для облегчения процесса чтения hello выходные данные для этого примера — форматированные toodisplay hello список общедоступных IP-адресов в формате таблицы.</span><span class="sxs-lookup"><span data-stu-id="4c11b-110">For easy reading, hello output for this example is formatted toodisplay hello list of public IPs in table format.</span></span>

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
