### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a><span data-ttu-id="43016-101">шлюз локальной сети toomodify hello «gatewayIpAddress»</span><span class="sxs-lookup"><span data-stu-id="43016-101">toomodify hello local network gateway 'gatewayIpAddress'</span></span>

<span data-ttu-id="43016-102">Если hello VPN-устройства, которые должны tooconnect toohas изменено его общедоступный IP-адрес, необходимо tooreflect шлюза локальной сети hello toomodify, изменяется.</span><span class="sxs-lookup"><span data-stu-id="43016-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="43016-103">IP-адрес шлюза Hello можно изменить без удаления существующего VPN-подключения шлюза (если имеется).</span><span class="sxs-lookup"><span data-stu-id="43016-103">hello gateway IP address can be changed without removing an existing VPN gateway connection (if you have one).</span></span> <span data-ttu-id="43016-104">toomodify hello IP-адреса шлюза, замена значений hello «Сайт2» и «TestRG1» с собственные с помощью hello [обновления шлюза локальной сети az](https://docs.microsoft.com/cli/azure/network/local-gateway#update) команды.</span><span class="sxs-lookup"><span data-stu-id="43016-104">toomodify hello gateway IP address, replace hello values 'Site2' and 'TestRG1' with your own using hello [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) command.</span></span>

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

<span data-ttu-id="43016-105">Проверьте правильность IP-адрес hello в выходных данных hello:</span><span class="sxs-lookup"><span data-stu-id="43016-105">Verify that hello IP address is correct in hello output:</span></span>

```
"gatewayIpAddress": "23.99.222.170",
```