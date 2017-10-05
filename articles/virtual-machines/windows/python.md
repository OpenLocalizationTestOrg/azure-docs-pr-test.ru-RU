---
title: "Создание виртуальных машин Windows в Azure с помощью Python и управление ими | Документация Майкрософт"
description: "Сведения об использовании Python для создания виртуальных машин Windows в Azure с помощью Python и управления ими."
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
ms.openlocfilehash: bb777d41570d7b1dc97402d532519488912948e3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a><span data-ttu-id="ba4ca-103">Развертывание виртуальной машины Azure с помощью Python</span><span class="sxs-lookup"><span data-stu-id="ba4ca-103">Create and manage Windows VMs in Azure using Python</span></span>

<span data-ttu-id="ba4ca-104">[Виртуальной машине Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) требуется несколько вспомогательных ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="ba4ca-105">В этой статье описывается создание, управление и удаление ресурсов виртуальной машины с помощью Python.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-105">This article covers creating, managing, and deleting VM resources using Python.</span></span> <span data-ttu-id="ba4ca-106">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ba4ca-107">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ba4ca-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="ba4ca-108">Установка пакетов.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-108">Install packages</span></span>
> * <span data-ttu-id="ba4ca-109">Создание учетных данных.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-109">Create credentials</span></span>
> * <span data-ttu-id="ba4ca-110">Создание ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-110">Create resources</span></span>
> * <span data-ttu-id="ba4ca-111">Выполнение задач управления.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-111">Perform management tasks</span></span>
> * <span data-ttu-id="ba4ca-112">Удаление ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-112">Delete resources</span></span>
> * <span data-ttu-id="ba4ca-113">Выполнение приложения</span><span class="sxs-lookup"><span data-stu-id="ba4ca-113">Run the application</span></span>

<span data-ttu-id="ba4ca-114">На выполнение этих действий требуется примерно 20 минут.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-114">It takes about 20 minutes to do these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="ba4ca-115">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ba4ca-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="ba4ca-116">Если вы этого еще не сделали, установите [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="ba4ca-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="ba4ca-117">На странице рабочих нагрузок выберите **Разработка на Python** и нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-117">Select **Python development** on the Workloads page, and then click **Install**.</span></span> <span data-ttu-id="ba4ca-118">В сводке вы увидите, что вариант **64-разрядная версия Python 3 (3.6.0)** выберется автоматически.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-118">In the summary, you can see that **Python 3 64-bit (3.6.0)** is automatically selected for you.</span></span> <span data-ttu-id="ba4ca-119">Если вы уже установили Visual Studio, можно добавить рабочую нагрузку Python с помощью средства запуска Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-119">If you have already installed Visual Studio, you can add the Python workload using the Visual Studio Launcher.</span></span>
2. <span data-ttu-id="ba4ca-120">После установки и запуска Visual Studio щелкните **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-120">After installing and starting Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="ba4ca-121">В разделе **Шаблоны** > **Python** > **Приложение Python** укажите имя *myPythonProject* и расположение проекта, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-121">Click **Templates** > **Python** > **Python Application**, enter *myPythonProject* for the name of the project, select the location of the project, and then click **OK**.</span></span>

## <a name="install-packages"></a><span data-ttu-id="ba4ca-122">Установка пакетов</span><span class="sxs-lookup"><span data-stu-id="ba4ca-122">Install packages</span></span>

1. <span data-ttu-id="ba4ca-123">В обозревателе решений в разделе *myPythonProject* щелкните правой кнопкой мыши **Python Environments** (Среды Python) и выберите **Add virtual environment** (Добавление виртуальной среды).</span><span class="sxs-lookup"><span data-stu-id="ba4ca-123">In Solution Explorer, under *myPythonProject*, right-click **Python Environments**, and then select **Add virtual environment**.</span></span>
2. <span data-ttu-id="ba4ca-124">На странице добавления виртуальной среды примите имя по умолчанию *env*, убедитесь, что в качестве базового интерпретатора выбран *Python 3.6 (64-разрядная версия)* и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-124">On the Add Virtual Environment screen, accept the default name of *env*, make sure that *Python 3.6 (64-bit)* is selected for the base interpreter, and then click **Create**.</span></span>
3. <span data-ttu-id="ba4ca-125">Щелкните правой кнопкой мыши созданную среду *env*, затем щелкните **Install Python Package** (Установить пакет Python), введите *azure* в поле поиска и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-125">Right-click the *env* environment that you created, click **Install Python Package**, enter *azure* in the search box, and then press Enter.</span></span>

<span data-ttu-id="ba4ca-126">В окнах вывода вы увидите, что пакеты Аzure успешно установлены.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-126">You should see in the output windows that the azure packages were successfully installed.</span></span> 

## <a name="create-credentials"></a><span data-ttu-id="ba4ca-127">Создание учетных данных</span><span class="sxs-lookup"><span data-stu-id="ba4ca-127">Create credentials</span></span>

<span data-ttu-id="ba4ca-128">Прежде чем выполнить этот шаг, убедитесь, что у вас есть [субъект-служба Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ba4ca-128">Before you start this step, make sure that you have an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="ba4ca-129">Кроме того, необходимо записать идентификатор приложения, ключ проверки подлинности и идентификатор клиента, которые понадобятся позже.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-129">You should also record the application ID, the authentication key, and the tenant ID that you need in a later step.</span></span>

1. <span data-ttu-id="ba4ca-130">Откройте созданный файл *myPythonProject.py*, а затем добавьте следующий код, который позволит запускать приложение:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-130">Open *myPythonProject.py* file that was created, and then add this code to enable your application to run:</span></span>

    ```python
    if __name__ == "__main__":
    ```

2. <span data-ttu-id="ba4ca-131">Чтобы импортировать необходимый код, добавьте эти операторы в начало PY-файла:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-131">To import the code that is needed, add these statements to the top of the .py file:</span></span>

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. <span data-ttu-id="ba4ca-132">Затем в PY-файле добавьте переменные после операторов импорта, чтобы указать общие значения, используемые в коде:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-132">Next in the .py file, add variables after the import statements to specify common values used in the code:</span></span>
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    <span data-ttu-id="ba4ca-133">Замените **subscription-id** идентификатором вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-133">Replace **subscription-id** with your subscription identifier.</span></span>

4. <span data-ttu-id="ba4ca-134">Чтобы создать учетные данные Active Directory, необходимые для выполнения запросов, добавьте эту функцию после переменных в PY-файле:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-134">To create the Active Directory credentials that you need to make requests, add this function after the variables in the .py file:</span></span>

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    <span data-ttu-id="ba4ca-135">Замените **application-id**, **authentication-key** и **tenant-id** значениями, записанными при создании субъекта-службы Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-135">Replace **application-id**, **authentication-key**, and **tenant-id** with the values that you previously collected when you created your Azure Active Directory service principal.</span></span>

5. <span data-ttu-id="ba4ca-136">Чтобы вызвать добавленный ранее метод, добавьте этот код после оператора **if** в конце PY-файла:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-136">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a><span data-ttu-id="ba4ca-137">Создание ресурсов</span><span class="sxs-lookup"><span data-stu-id="ba4ca-137">Create resources</span></span>
 
### <a name="initialize-management-clients"></a><span data-ttu-id="ba4ca-138">Создание клиентов управления</span><span class="sxs-lookup"><span data-stu-id="ba4ca-138">Initialize management clients</span></span>

<span data-ttu-id="ba4ca-139">Клиенты управления необходимы для создания ресурсов и управления ими с помощью пакета SDK Python в Azure.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-139">Management clients are needed to create and manage resources using the Python SDK in Azure.</span></span> <span data-ttu-id="ba4ca-140">Чтобы создать клиенты управления, добавьте этот код после оператора **if** в конце PY-файла:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-140">To create the management clients, add this code under the **if** statement at then end of the .py file:</span></span>

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

### <a name="create-the-vm-and-supporting-resources"></a><span data-ttu-id="ba4ca-141">Создание виртуальной машины и ресурсов поддержки</span><span class="sxs-lookup"><span data-stu-id="ba4ca-141">Create the VM and supporting resources</span></span>

<span data-ttu-id="ba4ca-142">Все ресурсы должны содержаться в [группе ресурсов](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ba4ca-142">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="ba4ca-143">Чтобы создать группу ресурсов, добавьте эту функцию после переменных в PY-файле:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-143">To create a resource group, add this function after the variables in the .py file:</span></span>

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. <span data-ttu-id="ba4ca-144">Чтобы вызвать добавленный ранее метод, добавьте этот код после оператора **if** в конце PY-файла:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-144">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter to continue...')
    ```

<span data-ttu-id="ba4ca-145">[Группы доступности](tutorial-availability-sets.md) упрощают обслуживание виртуальных машин, используемых приложением.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-145">[Availability sets](tutorial-availability-sets.md) make it easier for you to maintain the virtual machines used by your application.</span></span>

1. <span data-ttu-id="ba4ca-146">Чтобы создать группу доступности, добавьте эту функцию после переменных в PY-файле:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-146">To create an availability set, add this function after the variables in the .py file:</span></span>
   
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

2. <span data-ttu-id="ba4ca-147">Чтобы вызвать добавленный ранее метод, добавьте этот код после оператора **if** в конце PY-файла:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-147">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter to continue...')
    ```

<span data-ttu-id="ba4ca-148">[Общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) необходим для взаимодействия с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-148">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed to communicate with the virtual machine.</span></span>

1. <span data-ttu-id="ba4ca-149">Чтобы создать общедоступный IP-адрес для виртуальной машины, добавьте эту функцию после переменных в PY-файле:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-149">To create a public IP address for the virtual machine, add this function after the variables in the .py file:</span></span>

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

2. <span data-ttu-id="ba4ca-150">Чтобы вызвать добавленный ранее метод, добавьте этот код после оператора **if** в конце PY-файла:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-150">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

<span data-ttu-id="ba4ca-151">Виртуальная машина должна быть в подсети [виртуальной сети](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ba4ca-151">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="ba4ca-152">Чтобы создать виртуальную сеть, добавьте эту функцию после переменных в PY-файле:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-152">To create a virtual network, add this function after the variables in the .py file:</span></span>

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

2. <span data-ttu-id="ba4ca-153">Чтобы вызвать добавленный ранее метод, добавьте этот код после оператора **if** в конце PY-файла:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-153">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

3. <span data-ttu-id="ba4ca-154">Чтобы добавить подсеть к виртуальной сети, добавьте эту функцию после переменных в PY-файле:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-154">To add a subnet to the virtual network, add this function after the variables in the .py file:</span></span>
    
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
        
4. <span data-ttu-id="ba4ca-155">Чтобы вызвать добавленный ранее метод, добавьте этот код после оператора **if** в конце PY-файла:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-155">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

<span data-ttu-id="ba4ca-156">Для обмена данными в виртуальной сети виртуальной машине нужен сетевой интерфейс.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-156">A virtual machine needs a network interface to communicate on the virtual network.</span></span>

1. <span data-ttu-id="ba4ca-157">Чтобы создать сетевой интерфейс, добавьте эту функцию после переменных в PY-файле:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-157">To create a network interface, add this function after the variables in the .py file:</span></span>

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

2. <span data-ttu-id="ba4ca-158">Чтобы вызвать добавленный ранее метод, добавьте этот код после оператора **if** в конце PY-файла:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-158">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

<span data-ttu-id="ba4ca-159">Теперь, когда вы создали все вспомогательные ресурсы, можно создать виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-159">Now that you created all the supporting resources, you can create a virtual machine.</span></span>

1. <span data-ttu-id="ba4ca-160">Чтобы создать виртуальную машину, добавьте эту функцию после переменных в PY-файле:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-160">To create the virtual machine, add this function after the variables in the .py file:</span></span>
   
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
    > <span data-ttu-id="ba4ca-161">В этом учебнике создается виртуальная машина под управлением одной из версий операционной системы Windows Server.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-161">This tutorial creates a virtual machine running a version of the Windows Server operating system.</span></span> <span data-ttu-id="ba4ca-162">Дополнительные сведения о выборе других образов см. в статье [Просмотр и выбор образов виртуальных машин Windows в Azure с помощью оболочки PowerShell или интерфейса командной строки](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ba4ca-162">To learn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and the Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

2. <span data-ttu-id="ba4ca-163">Чтобы вызвать добавленный ранее метод, добавьте этот код после оператора **if** в конце PY-файла:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-163">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter to continue...')
    ```

## <a name="perform-management-tasks"></a><span data-ttu-id="ba4ca-164">Выполнение задач управления</span><span class="sxs-lookup"><span data-stu-id="ba4ca-164">Perform management tasks</span></span>

<span data-ttu-id="ba4ca-165">В течение жизненного цикла виртуальной машины можно выполнять задачи управления, такие как запуск, остановка или удаление виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-165">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="ba4ca-166">Кроме того, можно создавать код для автоматизации повторяющихся или сложных задач.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-166">Additionally, you may want to create code to automate repetitive or complex tasks.</span></span>

### <a name="get-information-about-the-vm"></a><span data-ttu-id="ba4ca-167">Получение информации о виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="ba4ca-167">Get information about the VM</span></span>

1. <span data-ttu-id="ba4ca-168">Чтобы получить сведения о виртуальной машине, добавьте эту функцию после переменных в PY-файле:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-168">To get information about the virtual machine, add this function after the variables in the .py file:</span></span>

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
2. <span data-ttu-id="ba4ca-169">Чтобы вызвать добавленный ранее метод, добавьте этот код после оператора **if** в конце PY-файла:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-169">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter to continue...')
    ```

### <a name="stop-the-vm"></a><span data-ttu-id="ba4ca-170">Остановка виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="ba4ca-170">Stop the VM</span></span>

<span data-ttu-id="ba4ca-171">Вы можете остановить виртуальную машину, сохранив все ее настройки (при этом за нее будет продолжать взиматься плата) или остановить ее и отменить ее распределение.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-171">You can stop a virtual machine and keep all its settings, but continue to be charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="ba4ca-172">При этом освобождаются все ресурсы, связанные с ней, а также прекращается выставление счетов за эту виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-172">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

1. <span data-ttu-id="ba4ca-173">Чтобы остановить виртуальную машину без ее освобождения, добавьте эту функцию после переменных в PY-файле:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-173">To stop the virtual machine without deallocating it, add this function after the variables in the .py file:</span></span>

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    <span data-ttu-id="ba4ca-174">Если вы хотите отменить распределение виртуальной машины, измените вызов power_off на следующий код:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-174">If you want to deallocate the virtual machine, change the power_off call to this code:</span></span>

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="ba4ca-175">Чтобы вызвать добавленный ранее метод, добавьте этот код после оператора **if** в конце PY-файла:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-175">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    stop_vm(compute_client)
    input('Press enter to continue...')
    ```

### <a name="start-the-vm"></a><span data-ttu-id="ba4ca-176">Запуск виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="ba4ca-176">Start the VM</span></span>

1. <span data-ttu-id="ba4ca-177">Чтобы запустить виртуальную машину, добавьте эту функцию после переменных в PY-файле:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-177">To start the virtual machine, add this function after the variables in the .py file:</span></span>

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="ba4ca-178">Чтобы вызвать добавленный ранее метод, добавьте этот код после оператора **if** в конце PY-файла:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-178">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    start_vm(compute_client)
    input('Press enter to continue...')
    ```

### <a name="resize-the-vm"></a><span data-ttu-id="ba4ca-179">Изменение размера виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="ba4ca-179">Resize the VM</span></span>

<span data-ttu-id="ba4ca-180">При выборе размера виртуальной машины необходимо учесть многие аспекты развертывания.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-180">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="ba4ca-181">Дополнительные сведения см. в статье [Размеры виртуальных машин Windows в Azure](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="ba4ca-181">For more information, see [VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="ba4ca-182">Чтобы изменить размер виртуальной машины, добавьте эту функцию после переменных в PY-файле:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-182">To change the size of the virtual machine, add this function after the variables in the .py file:</span></span>

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

2. <span data-ttu-id="ba4ca-183">Чтобы вызвать добавленный ранее метод, добавьте этот код после оператора **if** в конце PY-файла:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-183">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter to continue...')
    ```

### <a name="add-a-data-disk-to-the-vm"></a><span data-ttu-id="ba4ca-184">Добавление диска данных в виртуальную машину</span><span class="sxs-lookup"><span data-stu-id="ba4ca-184">Add a data disk to the VM</span></span>

<span data-ttu-id="ba4ca-185">Виртуальные машины могут иметь один или несколько [дисков данных](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), которые хранятся на виртуальных жестких дисках.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-185">Virtual machines can have one or more [data disks](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) that are stored as VHDs.</span></span>

1. <span data-ttu-id="ba4ca-186">Чтобы добавить диск данных в виртуальную машину, добавьте эту функцию после переменных в PY-файле:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-186">To add a data disk to the virtual machine, add this function after the variables in the .py file:</span></span> 

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

2. <span data-ttu-id="ba4ca-187">Чтобы вызвать добавленный ранее метод, добавьте этот код после оператора **if** в конце PY-файла:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-187">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter to continue...')
    ```

## <a name="delete-resources"></a><span data-ttu-id="ba4ca-188">Удаление ресурсов</span><span class="sxs-lookup"><span data-stu-id="ba4ca-188">Delete resources</span></span>

<span data-ttu-id="ba4ca-189">Так как за использование ресурсов Azure взимается плата, рекомендуется всегда удалять ресурсы, которые больше не нужны.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-189">Because you are charged for resources used in Azure, it's always a good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="ba4ca-190">Если вы хотите удалить виртуальные машины и все вспомогательные ресурсы, достаточно удалить группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-190">If you want to delete the virtual machines and all the supporting resources, all you have to do is delete the resource group.</span></span>

1. <span data-ttu-id="ba4ca-191">Чтобы удалить группу ресурсов и все ресурсы, добавьте эту функцию после переменных в PY-файле.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-191">To delete the resource group and all resources, add this function after the variables in the .py file:</span></span>
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. <span data-ttu-id="ba4ca-192">Чтобы вызвать добавленный ранее метод, добавьте этот код после оператора **if** в конце PY-файла:</span><span class="sxs-lookup"><span data-stu-id="ba4ca-192">To call the function that you previously added, add this code under the **if** statement at the end of the .py file:</span></span>
   
    ```python
    delete_resources(resource_group_client)
    ```

3. <span data-ttu-id="ba4ca-193">Сохраните *myPythonProject.py*.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-193">Save *myPythonProject.py*.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="ba4ca-194">Выполнение приложения</span><span class="sxs-lookup"><span data-stu-id="ba4ca-194">Run the application</span></span>

1. <span data-ttu-id="ba4ca-195">Чтобы запустить консольное приложение, нажмите кнопку **Запустить** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-195">To run the console application, click **Start** in Visual Studio.</span></span>

2. <span data-ttu-id="ba4ca-196">Нажмите клавишу **ВВОД** после возвращения сведений о состоянии каждого ресурса.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-196">Press **Enter** after the status of each resource is returned.</span></span> <span data-ttu-id="ba4ca-197">В сведениях о состоянии должно отобразиться состояние подготовки **Успешно**.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-197">In the status information, you should see a **Succeeded** provisioning state.</span></span> <span data-ttu-id="ba4ca-198">После создания виртуальной машины вы можете удалить все созданные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-198">After the virtual machine is created, you have the opportunity to delete all the resources that you create.</span></span> <span data-ttu-id="ba4ca-199">Прежде чем нажать клавишу **ВВОД** и начать удаление ресурсов, потратьте несколько минут и проверьте на портале Azure, созданы ли эти ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-199">Before you press **Enter** to start deleting resources, you could take a few minutes to verify their creation in the Azure portal.</span></span> <span data-ttu-id="ba4ca-200">Если у вас открыт портал Azure, может потребоваться обновить колонку, чтобы увидеть новые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-200">If you have the Azure portal open, you might have to refresh the blade to see new resources.</span></span>  

    <span data-ttu-id="ba4ca-201">На полное выполнение этого консольного приложения потребуется примерно 5 минут.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-201">It should take about five minutes for this console application to run completely from start to finish.</span></span> <span data-ttu-id="ba4ca-202">После закрытия приложения на удаление ресурсов и групп ресурсов может потребоваться несколько минут.</span><span class="sxs-lookup"><span data-stu-id="ba4ca-202">It may take several minutes after the application has finished before all the resources and the resource group are deleted.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ba4ca-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ba4ca-203">Next steps</span></span>

- <span data-ttu-id="ba4ca-204">При наличии проблем с развертыванием ознакомьтесь с информацией об [устранении неполадок развертываний групп ресурсов с помощью портала Azure](../../resource-manager-troubleshoot-deployments-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ba4ca-204">If there were issues with the deployment, a next step would be to look at [Troubleshooting resource group deployments with Azure portal](../../resource-manager-troubleshoot-deployments-portal.md)</span></span>
- <span data-ttu-id="ba4ca-205">Узнайте больше о [библиотеке Azure для Python](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python).</span><span class="sxs-lookup"><span data-stu-id="ba4ca-205">Learn more about the [Azure Python Library](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span></span>

