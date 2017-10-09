Можно проверить успешность подключения с помощью командлета hello «Get-AzureVNetConnection».

1. Hello используйте следующий пример командлета, настройку hello значения toomatch свои собственные. Имя Hello hello виртуальной сети должно быть заключено в кавычки, если он содержит пробелы.

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. После завершения работы командлета hello Просмотр значений hello. В следующем примере hello отображается состояние подключения hello «Подключен», и вы увидите входящего и исходящего байт.

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : hello connectivity state for hello local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal