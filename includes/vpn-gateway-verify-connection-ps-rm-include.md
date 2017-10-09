<span data-ttu-id="4e134-101">Вы можете убедиться в успешном подключение с помощью командлета «Get-AzureRmVirtualNetworkGatewayConnection» hello, независимо от "-Отладка".</span><span class="sxs-lookup"><span data-stu-id="4e134-101">You can verify that your connection succeeded by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet, with or without '-Debug'.</span></span> 

1. <span data-ttu-id="4e134-102">Hello используйте следующий пример командлета, настройку hello значения toomatch свои собственные.</span><span class="sxs-lookup"><span data-stu-id="4e134-102">Use hello following cmdlet example, configuring hello values toomatch your own.</span></span> <span data-ttu-id="4e134-103">Если будет предложено, выберите «A» в порядке toorun «All».</span><span class="sxs-lookup"><span data-stu-id="4e134-103">If prompted, select 'A' in order toorun 'All'.</span></span> <span data-ttu-id="4e134-104">В примере hello "-имя" имя toohello hello подключение tootest ссылается.</span><span class="sxs-lookup"><span data-stu-id="4e134-104">In hello example, '-Name' refers toohello name of hello connection that you want tootest.</span></span>

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. <span data-ttu-id="4e134-105">После завершения работы командлета hello Просмотр значений hello.</span><span class="sxs-lookup"><span data-stu-id="4e134-105">After hello cmdlet has finished, view hello values.</span></span> <span data-ttu-id="4e134-106">В следующем примере hello состояние подключения hello показано, как «Подключен» и вы можете видеть входящего и исходящего байт.</span><span class="sxs-lookup"><span data-stu-id="4e134-106">In hello example below, hello connection status shows as 'Connected' and you can see ingress and egress bytes.</span></span>
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```