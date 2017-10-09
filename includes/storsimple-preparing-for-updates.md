<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a><span data-ttu-id="66251-101">Подготовка к обновлению</span><span class="sxs-lookup"><span data-stu-id="66251-101">Preparing for updates</span></span>
<span data-ttu-id="66251-102">Вам потребуется tooperform hello, выполнив действия, прежде чем проверить и установить обновления hello:</span><span class="sxs-lookup"><span data-stu-id="66251-102">You will need tooperform hello following steps before you scan and apply hello update:</span></span>

1. <span data-ttu-id="66251-103">Сделайте снимок облачного устройства данных hello.</span><span class="sxs-lookup"><span data-stu-id="66251-103">Take a cloud snapshot of hello device data.</span></span>
2. <span data-ttu-id="66251-104">Убедитесь, что контроллер фиксированные IP-адреса доступны для маршрутизации и могут подключаться к Интернету toohello.</span><span class="sxs-lookup"><span data-stu-id="66251-104">Ensure that your controller fixed IPs are routable and can connect toohello Internet.</span></span> <span data-ttu-id="66251-105">Эти фиксированные IP-адресов будет tooyour устройства используется tooservice обновлений.</span><span class="sxs-lookup"><span data-stu-id="66251-105">These fixed IPs will be used tooservice updates tooyour device.</span></span> <span data-ttu-id="66251-106">Это можно проверить, выполнив следующий командлет на каждом контроллере из интерфейса Windows PowerShell hello устройства hello hello:</span><span class="sxs-lookup"><span data-stu-id="66251-106">You can test this by running hello following cmdlet on each controller from hello Windows PowerShell interface of hello device:</span></span>
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    <span data-ttu-id="66251-107">**Пример выходных данных для тестирования подключения при фиксированные IP-адреса могут подключаться к Интернету toohello**</span><span class="sxs-lookup"><span data-stu-id="66251-107">**Sample output for Test-Connection when fixed IPs can connect toohello Internet**</span></span>

        Controller0>Test-Connection -Source 10.126.173.91 -Destination bing.com

        Source      Destination     IPV4Address      IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200

        Controller0>Test-Connection -Source 10.126.173.91 -Destination  204.79.197.200

        Source      Destination       IPV4Address    IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200

<span data-ttu-id="66251-108">После успешного завершения эти вручную до проверки можно продолжить tooscan и установить обновления hello.</span><span class="sxs-lookup"><span data-stu-id="66251-108">After you have successfully completed these manual pre-checks, you can proceed tooscan and install hello updates.</span></span>

