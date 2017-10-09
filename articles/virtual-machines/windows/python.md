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
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a><span data-ttu-id="f2c77-103">Развертывание виртуальной машины Azure с помощью Python</span><span class="sxs-lookup"><span data-stu-id="f2c77-103">Create and manage Windows VMs in Azure using Python</span></span>

<span data-ttu-id="f2c77-104">[Виртуальной машине Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) требуется несколько вспомогательных ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="f2c77-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="f2c77-105">В этой статье описывается создание, управление и удаление ресурсов виртуальной машины с помощью Python.</span><span class="sxs-lookup"><span data-stu-id="f2c77-105">This article covers creating, managing, and deleting VM resources using Python.</span></span> <span data-ttu-id="f2c77-106">Вы узнаете, как выполнять следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="f2c77-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f2c77-107">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f2c77-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="f2c77-108">Установка пакетов.</span><span class="sxs-lookup"><span data-stu-id="f2c77-108">Install packages</span></span>
> * <span data-ttu-id="f2c77-109">Создание учетных данных.</span><span class="sxs-lookup"><span data-stu-id="f2c77-109">Create credentials</span></span>
> * <span data-ttu-id="f2c77-110">Создание ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f2c77-110">Create resources</span></span>
> * <span data-ttu-id="f2c77-111">Выполнение задач управления.</span><span class="sxs-lookup"><span data-stu-id="f2c77-111">Perform management tasks</span></span>
> * <span data-ttu-id="f2c77-112">Удаление ресурсов</span><span class="sxs-lookup"><span data-stu-id="f2c77-112">Delete resources</span></span>
> * <span data-ttu-id="f2c77-113">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="f2c77-113">Run hello application</span></span>

<span data-ttu-id="f2c77-114">Занимает около 20 минут toodo следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f2c77-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="f2c77-115">Создание проекта Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f2c77-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="f2c77-116">Если вы этого еще не сделали, установите [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="f2c77-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="f2c77-117">Выберите **разработки Python** на hello рабочих нагрузок страницы и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="f2c77-117">Select **Python development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="f2c77-118">В hello сводки, можно видеть, что **Python 3 x 64 (3.6.0)** автоматически выбирается автоматически.</span><span class="sxs-lookup"><span data-stu-id="f2c77-118">In hello summary, you can see that **Python 3 64-bit (3.6.0)** is automatically selected for you.</span></span> <span data-ttu-id="f2c77-119">Если вы уже установили Visual Studio, можно добавить рабочей нагрузки hello Python, с помощью hello запуска Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f2c77-119">If you have already installed Visual Studio, you can add hello Python workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="f2c77-120">После установки и запуска Visual Studio щелкните **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="f2c77-120">After installing and starting Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="f2c77-121">Нажмите кнопку **шаблоны** > **Python** > **приложения Python**, введите *myPythonProject* имени hello hello проекта, выберите расположение hello hello проекта и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f2c77-121">Click **Templates** > **Python** > **Python Application**, enter *myPythonProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-packages"></a><span data-ttu-id="f2c77-122">Установка пакетов</span><span class="sxs-lookup"><span data-stu-id="f2c77-122">Install packages</span></span>

1. <span data-ttu-id="f2c77-123">В обозревателе решений в разделе *myPythonProject* щелкните правой кнопкой мыши **Python Environments** (Среды Python) и выберите **Add virtual environment** (Добавление виртуальной среды).</span><span class="sxs-lookup"><span data-stu-id="f2c77-123">In Solution Explorer, under *myPythonProject*, right-click **Python Environments**, and then select **Add virtual environment**.</span></span>
2. <span data-ttu-id="f2c77-124">На экране приветствия добавить виртуальную среду, примите имя по умолчанию hello *env*, убедитесь, что *3.6 Python (64-разрядная версия)* выбран для базового интерпретатор hello и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="f2c77-124">On hello Add Virtual Environment screen, accept hello default name of *env*, make sure that *Python 3.6 (64-bit)* is selected for hello base interpreter, and then click **Create**.</span></span>
3. <span data-ttu-id="f2c77-125">Щелкните правой кнопкой мыши hello *env* щелкните созданную среду, **установить пакет Python**, введите *azure* в hello поле поиска и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="f2c77-125">Right-click hello *env* environment that you created, click **Install Python Package**, enter *azure* in hello search box, and then press Enter.</span></span>

<span data-ttu-id="f2c77-126">Вы увидите в окнах вывода hello hello azure пакеты были успешно установлены.</span><span class="sxs-lookup"><span data-stu-id="f2c77-126">You should see in hello output windows that hello azure packages were successfully installed.</span></span> 

## <a name="create-credentials"></a><span data-ttu-id="f2c77-127">Создание учетных данных</span><span class="sxs-lookup"><span data-stu-id="f2c77-127">Create credentials</span></span>

<span data-ttu-id="f2c77-128">Прежде чем выполнить этот шаг, убедитесь, что у вас есть [субъект-служба Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f2c77-128">Before you start this step, make sure that you have an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="f2c77-129">Также необходимо записать идентификатор приложения hello, hello ключ проверки подлинности и ИД клиента hello, необходимое на более позднем этапе.</span><span class="sxs-lookup"><span data-stu-id="f2c77-129">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

1. <span data-ttu-id="f2c77-130">Откройте *myPythonProject.py* файл, который был создан, а затем добавьте этот код tooenable toorun вашего приложения:</span><span class="sxs-lookup"><span data-stu-id="f2c77-130">Open *myPythonProject.py* file that was created, and then add this code tooenable your application toorun:</span></span>

    ```python
    if __name__ == "__main__":
    ```

2. <span data-ttu-id="f2c77-131">tooimport hello код, необходимый для, добавьте эти операторы начало toohello hello .py файла:</span><span class="sxs-lookup"><span data-stu-id="f2c77-131">tooimport hello code that is needed, add these statements toohello top of hello .py file:</span></span>

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. <span data-ttu-id="f2c77-132">Далее hello .py добавьте в файл переменных после операторы импорта hello общие значения toospecify, используемой в hello кода:</span><span class="sxs-lookup"><span data-stu-id="f2c77-132">Next in hello .py file, add variables after hello import statements toospecify common values used in hello code:</span></span>
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    <span data-ttu-id="f2c77-133">Замените **subscription-id** идентификатором вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="f2c77-133">Replace **subscription-id** with your subscription identifier.</span></span>

4. <span data-ttu-id="f2c77-134">учетные данные Active Directory hello toocreate необходимость toomake запросы, добавьте эту функцию после hello переменные в файлах .py hello:</span><span class="sxs-lookup"><span data-stu-id="f2c77-134">toocreate hello Active Directory credentials that you need toomake requests, add this function after hello variables in hello .py file:</span></span>

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    <span data-ttu-id="f2c77-135">Замените **идентификатор приложения**, **ключ проверки подлинности**, и **ИД клиента** со значениями hello, предварительно собраны при его создании в Azure Active Directory Участник службы.</span><span class="sxs-lookup"><span data-stu-id="f2c77-135">Replace **application-id**, **authentication-key**, and **tenant-id** with hello values that you previously collected when you created your Azure Active Directory service principal.</span></span>

5. <span data-ttu-id="f2c77-136">функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:</span><span class="sxs-lookup"><span data-stu-id="f2c77-136">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a><span data-ttu-id="f2c77-137">Создание ресурсов</span><span class="sxs-lookup"><span data-stu-id="f2c77-137">Create resources</span></span>
 
### <a name="initialize-management-clients"></a><span data-ttu-id="f2c77-138">Создание клиентов управления</span><span class="sxs-lookup"><span data-stu-id="f2c77-138">Initialize management clients</span></span>

<span data-ttu-id="f2c77-139">Клиенты управления являются toocreate необходимые ресурсы и управлять ими с помощью пакета SDK для Python hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="f2c77-139">Management clients are needed toocreate and manage resources using hello Python SDK in Azure.</span></span> <span data-ttu-id="f2c77-140">Клиенты управления hello toocreate, добавьте следующий код под hello **Если** инструкции затем конце hello .py файла:</span><span class="sxs-lookup"><span data-stu-id="f2c77-140">toocreate hello management clients, add this code under hello **if** statement at then end of hello .py file:</span></span>

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

### <a name="create-hello-vm-and-supporting-resources"></a><span data-ttu-id="f2c77-141">Создать hello ВМ и ресурсы поддержки</span><span class="sxs-lookup"><span data-stu-id="f2c77-141">Create hello VM and supporting resources</span></span>

<span data-ttu-id="f2c77-142">Все ресурсы должны содержаться в [группе ресурсов](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f2c77-142">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="f2c77-143">toocreate группу ресурсов, добавьте эту функцию после hello переменные в файлах .py hello:</span><span class="sxs-lookup"><span data-stu-id="f2c77-143">toocreate a resource group, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. <span data-ttu-id="f2c77-144">функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:</span><span class="sxs-lookup"><span data-stu-id="f2c77-144">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter toocontinue...')
    ```

<span data-ttu-id="f2c77-145">[Наборы доступности](tutorial-availability-sets.md) упростить для вас toomaintain hello виртуальных машин, используемых приложением.</span><span class="sxs-lookup"><span data-stu-id="f2c77-145">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

1. <span data-ttu-id="f2c77-146">toocreate доступности значение, добавьте эту функцию после hello переменные в файлах .py hello:</span><span class="sxs-lookup"><span data-stu-id="f2c77-146">toocreate an availability set, add this function after hello variables in hello .py file:</span></span>
   
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

2. <span data-ttu-id="f2c77-147">функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:</span><span class="sxs-lookup"><span data-stu-id="f2c77-147">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter toocontinue...')
    ```

<span data-ttu-id="f2c77-148">Объект [общедоступный IP-адрес](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) — необходимые toocommunicate с виртуальной машиной hello.</span><span class="sxs-lookup"><span data-stu-id="f2c77-148">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

1. <span data-ttu-id="f2c77-149">toocreate общедоступный IP-адрес для виртуальной машины hello, добавьте эту функцию после hello переменные в файлах .py hello:</span><span class="sxs-lookup"><span data-stu-id="f2c77-149">toocreate a public IP address for hello virtual machine, add this function after hello variables in hello .py file:</span></span>

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

2. <span data-ttu-id="f2c77-150">функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:</span><span class="sxs-lookup"><span data-stu-id="f2c77-150">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="f2c77-151">Виртуальная машина должна быть в подсети [виртуальной сети](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f2c77-151">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="f2c77-152">toocreate виртуальной сети, добавьте эту функцию после hello переменные в файлах .py hello:</span><span class="sxs-lookup"><span data-stu-id="f2c77-152">toocreate a virtual network, add this function after hello variables in hello .py file:</span></span>

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

2. <span data-ttu-id="f2c77-153">функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:</span><span class="sxs-lookup"><span data-stu-id="f2c77-153">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

3. <span data-ttu-id="f2c77-154">tooadd виртуальной сети toohello подсети, добавьте эту функцию после hello переменные в файлах .py hello:</span><span class="sxs-lookup"><span data-stu-id="f2c77-154">tooadd a subnet toohello virtual network, add this function after hello variables in hello .py file:</span></span>
    
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
        
4. <span data-ttu-id="f2c77-155">функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:</span><span class="sxs-lookup"><span data-stu-id="f2c77-155">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="f2c77-156">Виртуальная машина должна toocommunicate интерфейса сети hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="f2c77-156">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

1. <span data-ttu-id="f2c77-157">toocreate сетевого интерфейса, добавьте эту функцию после hello переменные в файлах .py hello:</span><span class="sxs-lookup"><span data-stu-id="f2c77-157">toocreate a network interface, add this function after hello variables in hello .py file:</span></span>

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

2. <span data-ttu-id="f2c77-158">функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:</span><span class="sxs-lookup"><span data-stu-id="f2c77-158">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="f2c77-159">Теперь, когда вы создали все hello, ресурсы поддержки, можно создать виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="f2c77-159">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

1. <span data-ttu-id="f2c77-160">toocreate Здравствуйте виртуальной машины, добавьте эту функцию после hello переменные в файлах .py hello:</span><span class="sxs-lookup"><span data-stu-id="f2c77-160">toocreate hello virtual machine, add this function after hello variables in hello .py file:</span></span>
   
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
    > <span data-ttu-id="f2c77-161">Данный учебник создает виртуальную машину под управлением версии операционной системы Windows Server hello.</span><span class="sxs-lookup"><span data-stu-id="f2c77-161">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="f2c77-162">toolearn Дополнительные сведения о выборе других изображений. в разделе [перехода, а затем выберите образы виртуальных машин Azure с помощью Windows PowerShell и hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f2c77-162">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

2. <span data-ttu-id="f2c77-163">функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:</span><span class="sxs-lookup"><span data-stu-id="f2c77-163">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

## <a name="perform-management-tasks"></a><span data-ttu-id="f2c77-164">Выполнение задач управления</span><span class="sxs-lookup"><span data-stu-id="f2c77-164">Perform management tasks</span></span>

<span data-ttu-id="f2c77-165">Во время жизненного цикла hello виртуальной машины может понадобиться toorun задачи управления, такие как запуск, остановка или удаление виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="f2c77-165">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="f2c77-166">Кроме того вы можете toocreate tooautomate повторяющихся или сложных задач кода.</span><span class="sxs-lookup"><span data-stu-id="f2c77-166">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="f2c77-167">Получение сведений о hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="f2c77-167">Get information about hello VM</span></span>

1. <span data-ttu-id="f2c77-168">tooget сведения о виртуальной машине hello, добавьте эту функцию после hello переменные в файлах .py hello:</span><span class="sxs-lookup"><span data-stu-id="f2c77-168">tooget information about hello virtual machine, add this function after hello variables in hello .py file:</span></span>

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
2. <span data-ttu-id="f2c77-169">функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:</span><span class="sxs-lookup"><span data-stu-id="f2c77-169">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter toocontinue...')
    ```

### <a name="stop-hello-vm"></a><span data-ttu-id="f2c77-170">Остановить hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="f2c77-170">Stop hello VM</span></span>

<span data-ttu-id="f2c77-171">Остановка виртуальной машины и оставьте все параметры, но продолжить toobe оплачивать или можно остановить виртуальную машину и освободить ее.</span><span class="sxs-lookup"><span data-stu-id="f2c77-171">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="f2c77-172">При этом освобождаются все ресурсы, связанные с ней, а также прекращается выставление счетов за эту виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="f2c77-172">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

1. <span data-ttu-id="f2c77-173">toostop hello виртуальной машины не освобождает его, добавьте эту функцию после hello переменные в файлах .py hello:</span><span class="sxs-lookup"><span data-stu-id="f2c77-173">toostop hello virtual machine without deallocating it, add this function after hello variables in hello .py file:</span></span>

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    <span data-ttu-id="f2c77-174">При необходимости toodeallocate hello виртуальной машины, измените вызов toothis hello power_off кода:</span><span class="sxs-lookup"><span data-stu-id="f2c77-174">If you want toodeallocate hello virtual machine, change hello power_off call toothis code:</span></span>

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="f2c77-175">функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:</span><span class="sxs-lookup"><span data-stu-id="f2c77-175">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    stop_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="start-hello-vm"></a><span data-ttu-id="f2c77-176">Запуск hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="f2c77-176">Start hello VM</span></span>

1. <span data-ttu-id="f2c77-177">toostart Здравствуйте виртуальной машины, добавьте эту функцию после hello переменные в файлах .py hello:</span><span class="sxs-lookup"><span data-stu-id="f2c77-177">toostart hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="f2c77-178">функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:</span><span class="sxs-lookup"><span data-stu-id="f2c77-178">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    start_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="resize-hello-vm"></a><span data-ttu-id="f2c77-179">Изменение размера виртуальной Машины hello</span><span class="sxs-lookup"><span data-stu-id="f2c77-179">Resize hello VM</span></span>

<span data-ttu-id="f2c77-180">При выборе размера виртуальной машины необходимо учесть многие аспекты развертывания.</span><span class="sxs-lookup"><span data-stu-id="f2c77-180">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="f2c77-181">Дополнительные сведения см. в статье [Размеры виртуальных машин Windows в Azure](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="f2c77-181">For more information, see [VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="f2c77-182">размер hello toochange hello виртуальной машины, добавьте эту функцию после hello переменные в файлах .py hello:</span><span class="sxs-lookup"><span data-stu-id="f2c77-182">toochange hello size of hello virtual machine, add this function after hello variables in hello .py file:</span></span>

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

2. <span data-ttu-id="f2c77-183">функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:</span><span class="sxs-lookup"><span data-stu-id="f2c77-183">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter toocontinue...')
    ```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="f2c77-184">Добавить toohello диска данных виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="f2c77-184">Add a data disk toohello VM</span></span>

<span data-ttu-id="f2c77-185">Виртуальные машины могут иметь один или несколько [дисков данных](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), которые хранятся на виртуальных жестких дисках.</span><span class="sxs-lookup"><span data-stu-id="f2c77-185">Virtual machines can have one or more [data disks](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) that are stored as VHDs.</span></span>

1. <span data-ttu-id="f2c77-186">Эта функция добавьте tooadd виртуальная машина toohello диск данных после hello переменные в файлах .py hello:</span><span class="sxs-lookup"><span data-stu-id="f2c77-186">tooadd a data disk toohello virtual machine, add this function after hello variables in hello .py file:</span></span> 

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

2. <span data-ttu-id="f2c77-187">функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:</span><span class="sxs-lookup"><span data-stu-id="f2c77-187">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter toocontinue...')
    ```

## <a name="delete-resources"></a><span data-ttu-id="f2c77-188">Удаление ресурсов</span><span class="sxs-lookup"><span data-stu-id="f2c77-188">Delete resources</span></span>

<span data-ttu-id="f2c77-189">Поскольку вы оплачивать ресурсы, используемые в Azure, это всегда ресурсов toodelete рекомендаций, которые больше не нужны.</span><span class="sxs-lookup"><span data-stu-id="f2c77-189">Because you are charged for resources used in Azure, it's always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="f2c77-190">Если необходимо, чтобы toodelete hello виртуальных машин и поддержку ресурсов все hello, все, что есть toodo — удалить группу ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="f2c77-190">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

1. <span data-ttu-id="f2c77-191">группы ресурсов toodelete hello и все ресурсы, добавьте эту функцию после hello переменные в файлах .py hello:</span><span class="sxs-lookup"><span data-stu-id="f2c77-191">toodelete hello resource group and all resources, add this function after hello variables in hello .py file:</span></span>
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. <span data-ttu-id="f2c77-192">функция toocall hello, добавленный ранее, добавьте следующий код под hello **Если** инструкции конце hello hello .py файла:</span><span class="sxs-lookup"><span data-stu-id="f2c77-192">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    delete_resources(resource_group_client)
    ```

3. <span data-ttu-id="f2c77-193">Сохраните *myPythonProject.py*.</span><span class="sxs-lookup"><span data-stu-id="f2c77-193">Save *myPythonProject.py*.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="f2c77-194">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="f2c77-194">Run hello application</span></span>

1. <span data-ttu-id="f2c77-195">toorun hello консольное приложение, нажмите кнопку **запустить** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f2c77-195">toorun hello console application, click **Start** in Visual Studio.</span></span>

2. <span data-ttu-id="f2c77-196">Нажмите клавишу **ввод** после возвращения hello состояния каждого ресурса.</span><span class="sxs-lookup"><span data-stu-id="f2c77-196">Press **Enter** after hello status of each resource is returned.</span></span> <span data-ttu-id="f2c77-197">Сведения о состоянии hello, вы увидите **успешно** состояние подготовки.</span><span class="sxs-lookup"><span data-stu-id="f2c77-197">In hello status information, you should see a **Succeeded** provisioning state.</span></span> <span data-ttu-id="f2c77-198">После создания виртуальной машины hello, у вас есть возможность toodelete hello все hello ресурсов, созданных.</span><span class="sxs-lookup"><span data-stu-id="f2c77-198">After hello virtual machine is created, you have hello opportunity toodelete all hello resources that you create.</span></span> <span data-ttu-id="f2c77-199">Перед нажатием кнопки **ввод** toostart удаление ресурсов, может потребоваться несколько минут tooverify их создания в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f2c77-199">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify their creation in hello Azure portal.</span></span> <span data-ttu-id="f2c77-200">Если имеют hello Azure откройте портала, возможно toorefresh hello колонке toosee новые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="f2c77-200">If you have hello Azure portal open, you might have toorefresh hello blade toosee new resources.</span></span>  

    <span data-ttu-id="f2c77-201">Занимает около пяти минут для этого toorun приложения консоли полностью с начала toofinish.</span><span class="sxs-lookup"><span data-stu-id="f2c77-201">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> <span data-ttu-id="f2c77-202">Он может занять несколько минут после завершения приложения hello перед всеми ресурсами hello и hello группы ресурсов удаляются.</span><span class="sxs-lookup"><span data-stu-id="f2c77-202">It may take several minutes after hello application has finished before all hello resources and hello resource group are deleted.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f2c77-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f2c77-203">Next steps</span></span>

- <span data-ttu-id="f2c77-204">Если возникли проблемы с развертыванием hello, следующим шагом будет toolook в [Устранение неполадок развертывания группы ресурсов с портала Azure](../../resource-manager-troubleshoot-deployments-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f2c77-204">If there were issues with hello deployment, a next step would be toolook at [Troubleshooting resource group deployments with Azure portal](../../resource-manager-troubleshoot-deployments-portal.md)</span></span>
- <span data-ttu-id="f2c77-205">Дополнительные сведения о hello [библиотеки Python в Azure](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span><span class="sxs-lookup"><span data-stu-id="f2c77-205">Learn more about hello [Azure Python Library](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span></span>

