### <a name="to-view-local-network-gateways"></a>Просмотр локальных сетевых шлюзов

Чтобы просмотреть список шлюзов локальной сети, используйте команду [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#list).

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="to-verify-the-shared-key-values"></a>Проверка значений общего ключа

Убедитесь, что значение общего ключа совпадает со значением, использованным для настройки VPN-устройства. Если это не так, выполните подключение еще раз, используя значение с устройства, или воспользуйтесь предыдущим значением устройства. Значения должны совпадать. Чтобы просмотреть общий ключ, используйте команду [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="to-view-the-vpn-gateway-public-ip-address"></a>Просмотр общедоступного IP-адреса VPN-шлюза

Чтобы найти общедоступный IP-адрес шлюза виртуальной сети, используйте команду [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list). Для удобства чтения выходные данные в этом примере форматируются для отображения списка общедоступных IP-адресов в формате таблицы.

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
