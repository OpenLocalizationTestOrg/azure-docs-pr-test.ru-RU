Вы можете убедиться в успешном подключение с помощью командлета «Get-AzureRmVirtualNetworkGatewayConnection» hello, независимо от "-Отладка". 

1. Hello используйте следующий пример командлета, настройку hello значения toomatch свои собственные. Если будет предложено, выберите «A» в порядке toorun «All». В примере hello "-имя" имя toohello hello подключение tootest ссылается.

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. После завершения работы командлета hello Просмотр значений hello. В следующем примере hello состояние подключения hello показано, как «Подключен» и вы можете видеть входящего и исходящего байт.
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```