### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a>шлюз локальной сети toomodify hello «gatewayIpAddress»

Если hello VPN-устройства, которые должны tooconnect toohas изменено его общедоступный IP-адрес, необходимо tooreflect шлюза локальной сети hello toomodify, изменяется. IP-адрес шлюза Hello можно изменить без удаления существующего VPN-подключения шлюза (если имеется). toomodify hello IP-адреса шлюза, замена значений hello «Сайт2» и «TestRG1» с собственные с помощью hello [обновления шлюза локальной сети az](https://docs.microsoft.com/cli/azure/network/local-gateway#update) команды.

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

Проверьте правильность IP-адрес hello в выходных данных hello:

```
"gatewayIpAddress": "23.99.222.170",
```