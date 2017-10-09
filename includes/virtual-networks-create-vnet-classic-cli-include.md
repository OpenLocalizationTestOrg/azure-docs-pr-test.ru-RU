## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a>Как toocreate классической виртуальной сети, с помощью Azure CLI
Можно использовать toomanage hello Azure CLI из командной строки hello с любого компьютера под управлением Windows, Linux или OSX ресурсами Azure. toocreate виртуальной сети с помощью hello Azure CLI, выполните шаги hello.

1. Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../articles/cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.
2. Запустите hello **Создание виртуальной сети azure сети** команды toocreate виртуальную сеть и подсеть, как показано ниже. Список Hello отображаться после вывода hello объясняется hello параметров, используемых.
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    Ожидаемые выходные данные:
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * **--vnet**. Имя создания toobe виртуальной сети hello. В данном сценарии это *TestVNet*
   * **-e (или --address-space)**. Адресное пространство виртуальной сети. В данном сценарии это *192.168.0.0*
   * **-i (или -cidr)**. Маска подсети в формате CIDR. В данном сценарии это *16*.
   * **-n (или --subnet-name**). Имя первой подсети hello. В данном сценарии это *FrontEnd*.
   * **-p (или --subnet-start-ip)**. Начальный IP-адрес для подсети или адресное пространство подсети. В нашем сценарии это *192.168.1.0*.
   * **-r (или --subnet-cidr)**. Маска подсети в формате CIDR для подсети. В данном сценарии это *24*.
   * **-l (или --location)**. Регион Azure, где будут создаваться hello виртуальной сети. В данном сценарии это *Central US*.
3. Запустите hello **создать подсеть виртуальной сети azure сети** toocreate команда подсеть, как показано ниже. Список Hello отображаться после вывода hello объясняется hello параметров, используемых.
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    Вот hello ожидается выходных данных для приведенных выше команд hello.
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * **-t (или --vnet-name**. Имя виртуальной сети, где будут создаваться подсети hello hello. В данном сценарии это *TestVNet*.
   * **-n (или --name)**. Имя новой подсети hello. В нашем сценарии это *BackEnd*.
   * **-a (или --address-prefix)**. Блок подсети CIDR. В данном сценарии это *192.168.2.0/24*.
4. Запустите hello **Показать виртуальной сети azure сети** команды tooview свойства hello hello новой виртуальной сети, как показано ниже.
   
            azure network vnet show
   
    Вот hello ожидается выходных данных для приведенных выше команд hello.
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

