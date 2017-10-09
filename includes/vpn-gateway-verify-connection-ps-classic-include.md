<span data-ttu-id="645bb-101">Можно проверить успешность подключения с помощью командлета hello «Get-AzureVNetConnection».</span><span class="sxs-lookup"><span data-stu-id="645bb-101">You can verify that your connection succeeded by using hello 'Get-AzureVNetConnection' cmdlet.</span></span>

1. <span data-ttu-id="645bb-102">Hello используйте следующий пример командлета, настройку hello значения toomatch свои собственные.</span><span class="sxs-lookup"><span data-stu-id="645bb-102">Use hello following cmdlet example, configuring hello values toomatch your own.</span></span> <span data-ttu-id="645bb-103">Имя Hello hello виртуальной сети должно быть заключено в кавычки, если он содержит пробелы.</span><span class="sxs-lookup"><span data-stu-id="645bb-103">hello name of hello virtual network must be in quotes if it contains spaces.</span></span>

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. <span data-ttu-id="645bb-104">После завершения работы командлета hello Просмотр значений hello.</span><span class="sxs-lookup"><span data-stu-id="645bb-104">After hello cmdlet has finished, view hello values.</span></span> <span data-ttu-id="645bb-105">В следующем примере hello отображается состояние подключения hello «Подключен», и вы увидите входящего и исходящего байт.</span><span class="sxs-lookup"><span data-stu-id="645bb-105">In hello example below, hello Connectivity State shows as 'Connected' and you can see ingress and egress bytes.</span></span>

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : hello connectivity state for hello local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal