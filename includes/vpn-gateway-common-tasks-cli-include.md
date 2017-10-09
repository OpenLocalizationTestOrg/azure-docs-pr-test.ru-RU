### <a name="tooview-local-network-gateways"></a>tooview локальных сетевых шлюзов

список локальных сетевых шлюзов hello, используйте hello tooview [список шлюза локальной сети az](https://docs.microsoft.com/cli/azure/network/local-gateway#list) команды.

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a>tooverify hello общих значений ключей

Убедитесь, что значение ключа hello общих hello же значение, которое используется для конфигурации устройства VPN. Если это не так, выполнить снова, используя значение hello с устройства hello подключения hello или обновить устройство hello hello значением из возвращаемого hello. Hello значения должны совпадать. tooview hello общий ключ, используйте hello [az сетевой список vpn подключения](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a>шлюз VPN hello tooview общедоступный IP-адрес

toofind hello общедоступный IP-адрес шлюза виртуальной сети, используйте hello [список открытый ip-сетей az](https://docs.microsoft.com/cli/azure/network/public-ip#list) команды. Для облегчения процесса чтения hello выходные данные для этого примера — форматированные toodisplay hello список общедоступных IP-адресов в формате таблицы.

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
