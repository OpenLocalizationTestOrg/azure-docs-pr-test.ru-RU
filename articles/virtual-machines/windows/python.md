---
title: "aaaCreate и управлять ими в Azure с помощью Python ВМ Windows | Документы Microsoft"
description: "Узнайте toouse Python toocreate и управление виртуальной Машине Windows в Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: davidmu
ms.openlocfilehash: c5553e4e7361e6b9a7183cd935be382f967160cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a>Развертывание виртуальной машины Azure с помощью Python

[Виртуальной машине Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) требуется несколько вспомогательных ресурсов Azure. В этой статье описывается создание, управление и удаление ресурсов виртуальной машины с помощью Python. Вы узнаете, как выполнять следующие задачи:

> [!div class="checklist"]
> * Создание проекта Visual Studio
> * Установка пакетов.
> * Создание учетных данных.
> * Создание ресурсов.
> * Выполнение задач управления.
> * Удаление ресурсов
> * Запустите приложение hello

Занимает около 20 минут toodo следующие действия.

## <a name="create-a-visual-studio-project"></a>Создание проекта Visual Studio

1. Если вы этого еще не сделали, установите [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Выберите **разработки Python** на hello рабочих нагрузок страницы и нажмите кнопку **установить**. В hello сводки, можно видеть, что **Python 3 x 64 (3.6.0)** автоматически выбирается автоматически. Если вы уже установили Visual Studio, можно добавить рабочей нагрузки hello Python, с помощью hello запуска Visual Studio.
2. После установки и запуска Visual Studio щелкните **Файл** > **Создать** > **Проект**.
3. Нажмите кнопку **шаблоны** > **Python** > **приложения Python**, введите *myPythonProject* имени hello hello проекта, выберите расположение hello hello проекта и нажмите кнопку **ОК**.

## <a name="install-packages"></a>Установка пакетов

1. В обозревателе решений в разделе *myPythonProject* щелкните правой кнопкой мыши **Python Environments** (Среды Python) и выберите **Add virtual environment** (Добавление виртуальной среды).
2. На экране приветствия добавить виртуальную среду, примите имя по умолчанию hello *env*, убедитесь, что *3.6 Python (64-разрядная версия)* выбран для базового интерпретатор hello и нажмите кнопку **создать**.
3. Щелкните правой кнопкой мыши hello *env* щелкните созданную среду, **установить пакет Python**, введите *azure* в hello поле поиска и нажмите клавишу ВВОД.

Вы увидите в окнах вывода hello hello azure пакеты были успешно установлены. 

## <a name="create-credentials"></a>Создание учетных данных

Прежде чем выполнить этот шаг, убедитесь, что у вас есть [субъект-служба Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md). Также необходимо записать идентификатор приложения hello, hello ключ проверки подлинности и ИД клиента hello, необходимое на более позднем этапе.

1. Откройте *myPythonProject.py* файл, который был создан, а затем добавьте этот код tooenable toorun вашего приложения:

    ```python
    if __name__ == "__main__":
    ```

2. tooimport hello код, необходимый для, добавьте эти операторы начало toohello hello .py файла:

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. Далее hello .py добавьте в файл переменных после операторы импорта hello общие значения toospecify, используемой в hello кода:
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    Замените **subscription-id** идентификатором вашей подписки.

4. учетные данные Active Directory hello toocreate необходимость toomake запросы, добавьте эту функцию после hello переменные в файлах .py hello:

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    Замените **идентификатор приложения**, **ключ проверки подлинности**, и **ИД клиента** со значениями hello, предварительно собраны при его создании в Azure Active Directory Участник службы.

5. функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a>Создание ресурсов
 
### <a name="initialize-management-clients"></a>Создание клиентов управления

Клиенты управления являются toocreate необходимые ресурсы и управлять ими с помощью пакета SDK для Python hello в Azure. Клиенты управления hello toocreate, добавьте следующий код под hello **Если** инструкции затем конце hello .py файла:

```python
resource_group_client = ResourceManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
network_client = NetworkManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
compute_client = ComputeManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
```

### <a name="create-hello-vm-and-supporting-resources"></a>Создать hello ВМ и ресурсы поддержки

Все ресурсы должны содержаться в [группе ресурсов](../../azure-resource-manager/resource-group-overview.md).

1. toocreate группу ресурсов, добавьте эту функцию после hello переменные в файлах .py hello:

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter toocontinue...')
    ```

[Наборы доступности](tutorial-availability-sets.md) упростить для вас toomaintain hello виртуальных машин, используемых приложением.

1. toocreate доступности значение, добавьте эту функцию после hello переменные в файлах .py hello:
   
    ```python
    def create_availability_set(compute_client):
        avset_params = {
            'location': LOCATION,
            'sku': { 'name': 'Aligned' },
            'platform_fault_domain_count': 3
        }
        availability_set_result = compute_client.availability_sets.create_or_update(
            GROUP_NAME,
            'myAVSet',
            avset_params
        )
    ```

2. функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter toocontinue...')
    ```

Объект [общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) — необходимые toocommunicate с виртуальной машиной hello.

1. toocreate общедоступный IP-адрес для виртуальной машины hello, добавьте эту функцию после hello переменные в файлах .py hello:

    ```python
    def create_public_ip_address(network_client):
        public_ip_addess_params = {
            'location': LOCATION,
            'public_ip_allocation_method': 'Dynamic'
        }
        creation_result = network_client.public_ip_addresses.create_or_update(
            GROUP_NAME,
            'myIPAddress',
            public_ip_addess_params
        )

        return creation_result.result()
    ```

2. функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Виртуальная машина должна быть в подсети [виртуальной сети](../../virtual-network/virtual-networks-overview.md).

1. toocreate виртуальной сети, добавьте эту функцию после hello переменные в файлах .py hello:

    ```python
    def create_vnet(network_client):
        vnet_params = {
            'location': LOCATION,
            'address_space': {
                'address_prefixes': ['10.0.0.0/16']
            }
        }
        creation_result = network_client.virtual_networks.create_or_update(
            GROUP_NAME,
            'myVNet',
            vnet_params
        )
        return creation_result.result()
    ```

2. функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

3. tooadd виртуальной сети toohello подсети, добавьте эту функцию после hello переменные в файлах .py hello:
    
    ```python
    def create_subnet(network_client):
        subnet_params = {
            'address_prefix': '10.0.0.0/24'
        }
        creation_result = network_client.subnets.create_or_update(
            GROUP_NAME,
            'myVNet',
            'mySubnet',
            subnet_params
        )

        return creation_result.result()
    ```
        
4. функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Виртуальная машина должна toocommunicate интерфейса сети hello виртуальной сети.

1. toocreate сетевого интерфейса, добавьте эту функцию после hello переменные в файлах .py hello:

    ```python
    def create_nic(network_client):
        subnet_info = network_client.subnets.get(
            GROUP_NAME, 
            'myVNet', 
            'mySubnet'
        )
        publicIPAddress = network_client.public_ip_addresses.get(
            GROUP_NAME,
            'myIPAddress'
        )
        nic_params = {
            'location': LOCATION,
            'ip_configurations': [{
                'name': 'myIPConfig',
                'public_ip_address': publicIPAddress,
                'subnet': {
                    'id': subnet_info.id
                }
            }]
        }
        creation_result = network_client.network_interfaces.create_or_update(
            GROUP_NAME,
            'myNic',
            nic_params
        )

        return creation_result.result()
    ```

2. функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Теперь, когда вы создали все hello, ресурсы поддержки, можно создать виртуальную машину.

1. toocreate Здравствуйте виртуальной машины, добавьте эту функцию после hello переменные в файлах .py hello:
   
    ```python
    def create_vm(network_client, compute_client):  
        nic = network_client.network_interfaces.get(
            GROUP_NAME, 
            'myNic'
        )
        avset = compute_client.availability_sets.get(
            GROUP_NAME,
            'myAVSet'
        )
        vm_parameters = {
            'location': LOCATION,
            'os_profile': {
                'computer_name': VM_NAME,
                'admin_username': 'azureuser',
                'admin_password': 'Azure12345678'
            },
            'hardware_profile': {
                'vm_size': 'Standard_DS1'
            },
            'storage_profile': {
                'image_reference': {
                    'publisher': 'MicrosoftWindowsServer',
                    'offer': 'WindowsServer',
                    'sku': '2012-R2-Datacenter',
                    'version': 'latest'
                }
            },
            'network_profile': {
                'network_interfaces': [{
                    'id': nic.id
                }]
            },
            'availability_set': {
                'id': avset.id
            }
        }
        creation_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm_parameters
        )
    
        return creation_result.result()
    ```

    > [!NOTE]
    > Данный учебник создает виртуальную машину под управлением версии операционной системы Windows Server hello. toolearn Дополнительные сведения о выборе других изображений. в разделе [перехода, а затем выберите образы виртуальных машин Azure с помощью Windows PowerShell и hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
    > 
    > 

2. функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

## <a name="perform-management-tasks"></a>Выполнение задач управления

Во время жизненного цикла hello виртуальной машины может понадобиться toorun задачи управления, такие как запуск, остановка или удаление виртуальной машины. Кроме того вы можете toocreate tooautomate повторяющихся или сложных задач кода.

### <a name="get-information-about-hello-vm"></a>Получение сведений о hello виртуальной Машины

1. tooget сведения о виртуальной машине hello, добавьте эту функцию после hello переменные в файлах .py hello:

    ```python
    def get_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME, expand='instanceView')
        print("hardwareProfile")
        print("   vmSize: ", vm.hardware_profile.vm_size)
        print("\nstorageProfile")
        print("  imageReference")
        print("    publisher: ", vm.storage_profile.image_reference.publisher)
        print("    offer: ", vm.storage_profile.image_reference.offer)
        print("    sku: ", vm.storage_profile.image_reference.sku)
        print("    version: ", vm.storage_profile.image_reference.version)
        print("  osDisk")
        print("    osType: ", vm.storage_profile.os_disk.os_type.value)
        print("    name: ", vm.storage_profile.os_disk.name)
        print("    createOption: ", vm.storage_profile.os_disk.create_option.value)
        print("    caching: ", vm.storage_profile.os_disk.caching.value)
        print("\nosProfile")
        print("  computerName: ", vm.os_profile.computer_name)
        print("  adminUsername: ", vm.os_profile.admin_username)
        print("  provisionVMAgent: {0}".format(vm.os_profile.windows_configuration.provision_vm_agent))
        print("  enableAutomaticUpdates: {0}".format(vm.os_profile.windows_configuration.enable_automatic_updates))
        print("\nnetworkProfile")
        for nic in vm.network_profile.network_interfaces:
            print("  networkInterface id: ", nic.id)
        print("\nvmAgent")
        print("  vmAgentVersion", vm.instance_view.vm_agent.vm_agent_version)
        print("    statuses")
        for stat in vm_result.instance_view.vm_agent.statuses:
            print("    code: ", stat.code)
            print("    displayStatus: ", stat.display_status)
            print("    message: ", stat.message)
            print("    time: ", stat.time)
        print("\ndisks");
        for disk in vm.instance_view.disks:
            print("  name: ", disk.name)
            print("  statuses")
            for stat in disk.statuses:
                print("    code: ", stat.code)
                print("    displayStatus: ", stat.display_status)
                print("    time: ", stat.time)
        print("\nVM general status")
        print("  provisioningStatus: ", vm.provisioning_state)
        print("  id: ", vm.id)
        print("  name: ", vm.name)
        print("  type: ", vm.type)
        print("  location: ", vm.location)
        print("\nVM instance status")
        for stat in vm.instance_view.statuses:
            print("  code: ", stat.code)
            print("  displayStatus: ", stat.display_status)
    ```
2. функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter toocontinue...')
    ```

### <a name="stop-hello-vm"></a>Остановить hello виртуальной Машины

Остановка виртуальной машины и оставьте все параметры, но продолжить toobe оплачивать или можно остановить виртуальную машину и освободить ее. При этом освобождаются все ресурсы, связанные с ней, а также прекращается выставление счетов за эту виртуальную машину.

1. toostop hello виртуальной машины не освобождает его, добавьте эту функцию после hello переменные в файлах .py hello:

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    При необходимости toodeallocate hello виртуальной машины, измените вызов toothis hello power_off кода:

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:

    ```python
    stop_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="start-hello-vm"></a>Запуск hello виртуальной Машины

1. toostart Здравствуйте виртуальной машины, добавьте эту функцию после hello переменные в файлах .py hello:

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:

    ```python
    start_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="resize-hello-vm"></a>Изменение размера виртуальной Машины hello

При выборе размера виртуальной машины необходимо учесть многие аспекты развертывания. Дополнительные сведения см. в статье [Размеры виртуальных машин Windows в Azure](sizes.md).

1. размер hello toochange hello виртуальной машины, добавьте эту функцию после hello переменные в файлах .py hello:

    ```python
    def update_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        vm.hardware_profile.vm_size = 'Standard_DS3'
        update_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm
        )

    return update_result.result()
    ```

2. функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter toocontinue...')
    ```

### <a name="add-a-data-disk-toohello-vm"></a>Добавить toohello диска данных виртуальной Машины

Виртуальные машины могут иметь один или несколько [дисков данных](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), которые хранятся на виртуальных жестких дисках.

1. Эта функция добавьте tooadd виртуальная машина toohello диск данных после hello переменные в файлах .py hello: 

    ```python
    def add_datadisk(compute_client):
        disk_creation = compute_client.disks.create_or_update(
            GROUP_NAME,
            'myDataDisk1',
            {
                'location': LOCATION,
                'disk_size_gb': 1,
                'creation_data': {
                    'create_option': DiskCreateOption.empty
                }
            }
        )
        data_disk = disk_creation.result()
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        add_result = vm.storage_profile.data_disks.append({
            'lun': 1,
            'name': 'myDataDisk1',
            'create_option': DiskCreateOption.attach,
            'managed_disk': {
                'id': data_disk.id
            }
        })
        add_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME,
            VM_NAME,
            vm)

        return add_result.result()
    ```

2. функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter toocontinue...')
    ```

## <a name="delete-resources"></a>Удаление ресурсов

Поскольку вы оплачивать ресурсы, используемые в Azure, это всегда ресурсов toodelete рекомендаций, которые больше не нужны. Если необходимо, чтобы toodelete hello виртуальных машин и поддержку ресурсов все hello, все, что есть toodo — удалить группу ресурсов hello.

1. группы ресурсов toodelete hello и все ресурсы, добавьте эту функцию после hello переменные в файлах .py hello:
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:
   
    ```python
    delete_resources(resource_group_client)
    ```

3. Сохраните *myPythonProject.py*.

## <a name="run-hello-application"></a>Запустите приложение hello

1. toorun hello консольное приложение, нажмите кнопку **запустить** в Visual Studio.

2. Нажмите клавишу **ввод** после возвращения hello состояния каждого ресурса. Сведения о состоянии hello, вы увидите **успешно** состояние подготовки. После создания виртуальной машины hello, у вас есть возможность toodelete hello все hello ресурсов, созданных. Перед нажатием кнопки **ввод** toostart удаление ресурсов, может потребоваться несколько минут tooverify их создания в hello портал Azure. Если имеют hello Azure откройте портала, возможно toorefresh hello колонке toosee новые ресурсы.  

    Занимает около пяти минут для этого toorun приложения консоли полностью с начала toofinish. Он может занять несколько минут после завершения приложения hello перед всеми ресурсами hello и hello группы ресурсов удаляются.


## <a name="next-steps"></a>Дальнейшие действия

- Если возникли проблемы с развертыванием hello, следующим шагом будет toolook в [Устранение неполадок развертывания группы ресурсов с портала Azure](../../resource-manager-troubleshoot-deployments-portal.md)
- Дополнительные сведения о hello [библиотеки Python в Azure](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)

