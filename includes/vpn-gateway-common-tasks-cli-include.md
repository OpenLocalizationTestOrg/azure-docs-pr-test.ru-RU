### <a name="to-view-local-network-gateways"></a><span data-ttu-id="7d027-101">Просмотр локальных сетевых шлюзов</span><span class="sxs-lookup"><span data-stu-id="7d027-101">To view local network gateways</span></span>

<span data-ttu-id="7d027-102">Чтобы просмотреть список шлюзов локальной сети, используйте команду [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#list).</span><span class="sxs-lookup"><span data-stu-id="7d027-102">To view a list of the local network gateways, use the [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#list) command.</span></span>

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="to-verify-the-shared-key-values"></a><span data-ttu-id="7d027-103">Проверка значений общего ключа</span><span class="sxs-lookup"><span data-stu-id="7d027-103">To verify the shared key values</span></span>

<span data-ttu-id="7d027-104">Убедитесь, что значение общего ключа совпадает со значением, использованным для настройки VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="7d027-104">Verify that the shared key value is the same value that you used for your VPN device configuration.</span></span> <span data-ttu-id="7d027-105">Если это не так, выполните подключение еще раз, используя значение с устройства, или воспользуйтесь предыдущим значением устройства.</span><span class="sxs-lookup"><span data-stu-id="7d027-105">If it is not, either run the connection again using the value from the device, or update the device with the value from the return.</span></span> <span data-ttu-id="7d027-106">Значения должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="7d027-106">The values must match.</span></span> <span data-ttu-id="7d027-107">Чтобы просмотреть общий ключ, используйте команду [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span><span class="sxs-lookup"><span data-stu-id="7d027-107">To view the shared key, use the [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span></span>

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="to-view-the-vpn-gateway-public-ip-address"></a><span data-ttu-id="7d027-108">Просмотр общедоступного IP-адреса VPN-шлюза</span><span class="sxs-lookup"><span data-stu-id="7d027-108">To view the VPN gateway Public IP address</span></span>

<span data-ttu-id="7d027-109">Чтобы найти общедоступный IP-адрес шлюза виртуальной сети, используйте команду [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list).</span><span class="sxs-lookup"><span data-stu-id="7d027-109">To find the public IP address of your virtual network gateway, use the [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="7d027-110">Для удобства чтения выходные данные в этом примере форматируются для отображения списка общедоступных IP-адресов в формате таблицы.</span><span class="sxs-lookup"><span data-stu-id="7d027-110">For easy reading, the output for this example is formatted to display the list of public IPs in table format.</span></span>

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
