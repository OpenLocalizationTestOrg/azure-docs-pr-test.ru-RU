### <a name="to-modify-the-local-network-gateway-gatewayipaddress"></a><span data-ttu-id="42700-101">Изменение шлюза локальной сети gateway-ip-address</span><span class="sxs-lookup"><span data-stu-id="42700-101">To modify the local network gateway 'gatewayIpAddress'</span></span>

<span data-ttu-id="42700-102">Если общедоступный IP-адрес VPN-устройства, к которому вы хотите подключиться, изменился, измените шлюз локальной сети в соответствии с изменениями.</span><span class="sxs-lookup"><span data-stu-id="42700-102">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="42700-103">IP-адрес шлюза можно изменить, не удаляя существующее подключение VPN-шлюза (если имеется).</span><span class="sxs-lookup"><span data-stu-id="42700-103">The gateway IP address can be changed without removing an existing VPN gateway connection (if you have one).</span></span> <span data-ttu-id="42700-104">Чтобы изменить IP-адрес шлюза, замените значения Site2 и TestRG1 собственными, используя команду [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update).</span><span class="sxs-lookup"><span data-stu-id="42700-104">To modify the gateway IP address, replace the values 'Site2' and 'TestRG1' with your own using the [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) command.</span></span>

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

<span data-ttu-id="42700-105">Проверьте правильность IP-адреса в выходных данных:</span><span class="sxs-lookup"><span data-stu-id="42700-105">Verify that the IP address is correct in the output:</span></span>

```
"gatewayIpAddress": "23.99.222.170",
```