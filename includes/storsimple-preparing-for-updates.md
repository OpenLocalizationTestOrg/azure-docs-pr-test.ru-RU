<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a>Подготовка к обновлению
Вам потребуется tooperform hello, выполнив действия, прежде чем проверить и установить обновления hello:

1. Сделайте снимок облачного устройства данных hello.
2. Убедитесь, что контроллер фиксированные IP-адреса доступны для маршрутизации и могут подключаться к Интернету toohello. Эти фиксированные IP-адресов будет tooyour устройства используется tooservice обновлений. Это можно проверить, выполнив следующий командлет на каждом контроллере из интерфейса Windows PowerShell hello устройства hello hello:
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    **Пример выходных данных для тестирования подключения при фиксированные IP-адреса могут подключаться к Интернету toohello**

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

После успешного завершения эти вручную до проверки можно продолжить tooscan и установить обновления hello.

