<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a><span data-ttu-id="4dc5f-101">Подготовка к обновлению</span><span class="sxs-lookup"><span data-stu-id="4dc5f-101">Preparing for updates</span></span>
<span data-ttu-id="4dc5f-102">Перед проверкой и установкой обновлений нужно выполнить следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="4dc5f-102">You will need to perform the following steps before you scan and apply the update:</span></span>

1. <span data-ttu-id="4dc5f-103">Создайте резервную копию данных на устройстве.</span><span class="sxs-lookup"><span data-stu-id="4dc5f-103">Take a cloud snapshot of the device data.</span></span>
2. <span data-ttu-id="4dc5f-104">Убедитесь, что фиксированные IP-адреса вашего контроллера поддерживают маршрутизацию и могут подключаться к Интернету.</span><span class="sxs-lookup"><span data-stu-id="4dc5f-104">Ensure that your controller fixed IPs are routable and can connect to the Internet.</span></span> <span data-ttu-id="4dc5f-105">Эти IP-адреса будут использоваться для передачи обновлений на ваше устройство.</span><span class="sxs-lookup"><span data-stu-id="4dc5f-105">These fixed IPs will be used to service updates to your device.</span></span> <span data-ttu-id="4dc5f-106">Это можно проверить, выполнив следующий командлет на каждом контроллере через интерфейс Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4dc5f-106">You can test this by running the following cmdlet on each controller from the Windows PowerShell interface of the device:</span></span>
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    <span data-ttu-id="4dc5f-107">**Пример выходных данных для тестирования соединения, когда фиксированные IP-адреса могут подключаться к Интернету**</span><span class="sxs-lookup"><span data-stu-id="4dc5f-107">**Sample output for Test-Connection when fixed IPs can connect to the Internet**</span></span>

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

<span data-ttu-id="4dc5f-108">Успешно завершив эти проверки, переходите к поиску и установке обновлений.</span><span class="sxs-lookup"><span data-stu-id="4dc5f-108">After you have successfully completed these manual pre-checks, you can proceed to scan and install the updates.</span></span>

