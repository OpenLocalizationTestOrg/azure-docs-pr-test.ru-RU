---
title: "API (Python) — руководство по функциям управления службами hello toouse aaaHow"
description: "Узнайте, как tooprogrammatically выполнять общие задачи управления службы из Python."
services: cloud-services
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: 61538ec0-1536-4a7e-ae89-95967fe35d73
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/30/2017
ms.author: lmazuel
ms.openlocfilehash: b59622203470e1586484cec4033515edb39ca4d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-management-from-python"></a>Как toouse управления службами с Python
В этом руководстве показано, как tooprogrammatically выполнять общие задачи управления службы из Python. Hello **ServiceManagementService** класса в hello [Azure SDK для Python](https://github.com/Azure/azure-sdk-for-python) поддерживает программный доступ toomuch hello службы связанных с управлением функциональных возможностей, доступных в hello [Классический портал azure] [ management-portal] (такие как **создание, обновление и удаление облачных служб, развертывания, службы управления данными и виртуальные машины**). Эту функцию можно использовать для построения приложений, требующих управления tooservice программный доступ.

## <a name="WhatIs"> </a>Что такое управление службами
Hello API управления службами предоставляет программный доступ toomuch функций службы управления hello через hello [классический портал Azure][management-portal]. Hello Azure SDK для Python позволяет toomanage облачных служб и учетных записей хранилища.

API управления службами hello toouse требуется слишком[создать учетную запись Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="Concepts"> </a>Основные понятия
Hello Azure SDK для Python упаковывает hello [API управления службами Azure][svc-mgmt-rest-api], который представляет собой API REST. Все операции API выполняются по SSL и проходят взаимную проверку подлинности с использованием сертификатов X.509 v3. Служба управления Hello может осуществляться из службы, работающей в Azure, или непосредственно через hello Интернет из любого приложения, способного отправить HTTPS-запрос и получить HTTPS-ответ.

## <a name="Installation"> </a>Установка
Доступны все функции hello, описанных в этой статье в hello `azure-servicemanagement-legacy` пакет, который можно установить с помощью PIP-адрес. Дополнительные сведения об установке (например, при наличии нового tooPython) см. в этой статье: [Установка Python и hello Azure SDK](../python-how-to-install.md)

## <a name="Connect"></a>Как: подключение tooservice management
Конечная точка службы управления toohello tooconnect, требуются идентификатор подписки Azure и действительный сертификат управления. Вы можете получить идентификатор подписки через hello [классический портал Azure][management-portal].

> [!NOTE]
> Теперь стало возможно toouse сертификаты, созданные с помощью OpenSSL, при работе в Windows.  Для этого требуется Python 2.7.4 или более поздняя версия. Корпорация Майкрософт рекомендует пользователям toouse OpenSSL вместо PFX-файл, учитывая, что поддержка для PFX-файл, скорее всего сертификаты будут удалены в будущем hello.
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a>Сертификаты управления в Windows/Mac/Linux (OpenSSL)
Можно использовать [OpenSSL](http://www.openssl.org/) toocreate своего сертификата управления.  Действительно нужны два сертификата toocreate, один для сервера hello ( `.cer` файл) и один для клиента hello ( `.pem` файла). toocreate hello `.pem` файл, выполните:

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

toocreate hello `.cer` сертификатов, выполните:

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

Дополнительные сведения о сертификатах Azure см. в статье [Общие сведения о сертификатах для облачных служб Azure](cloud-services-certs-create.md). Полное описание параметров OpenSSL документации hello в [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).

После создания этих файлов необходимо tooupload hello `.cer` файл tooAzure с помощью действия «Отправка» hello вкладка «Параметры» hello hello [классический портал Azure][management-portal], и необходимо записать toomake где был сохранен hello `.pem` файла.

После получения Идентификатором подписки, сертификат создан и загружен hello `.cer` tooAzure файл конечную toohello управления Azure можно соединить, передавая идентификатор подписки hello и hello путь toohello `.pem` файл слишком**ServiceManagementService**:

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

В предыдущих примере hello `sms` — **ServiceManagementService** объекта. Hello **ServiceManagementService** класса — основной класс, используемый toomanage hello служб Azure.

### <a name="management-certificates-on-windows-makecert"></a>Управление сертификатами в Windows (MakeCert)
Вы можете создать самозаверяющий сертификат управления на своем компьютере с помощью программы `makecert.exe`.  Откройте **командную строку Visual Studio** как **администратора** и использовать hello следующую команду, заменив *AzureCertificate* с именем сертификата hello хотелось бы toouse.

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

Команда Hello создает hello `.cer` файл и помещает его в hello **личных** хранилище сертификатов. Дополнительные сведения см. в статье [Общие сведения о сертификатах для облачных служб Azure](cloud-services-certs-create.md).

После создания сертификата hello требуется tooupload hello `.cer` файл tooAzure с помощью действия «Отправка» hello вкладка «Параметры» hello hello [классический портал Azure][management-portal].

После получения Идентификатором подписки, сертификат создан и загружен hello `.cer` tooAzure файл toohello конечную управления Azure можно соединить, передавая идентификатор подписки hello и hello расположение сертификата hello в вашей **Личные** хранилище сертификатов слишком**ServiceManagementService** (опять же, замените *AzureCertificate* с именем hello сертификата):

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

В предыдущих примере hello `sms` — **ServiceManagementService** объекта. Hello **ServiceManagementService** класса — основной класс, используемый toomanage hello служб Azure.

## <a name="ListAvailableLocations"> </a>Практическое руководство. Отображение списка доступных расположений
toolist hello расположений, доступных для размещения служб, использовать hello **списка\_расположения** метод:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

При создании облачной службы или службы хранилища необходимо tooprovide допустимое расположение. Hello **списка\_расположения** метод всегда возвращает текущий список доступных расположений hello. На момент написания этой статьи приведены hello доступных расположений.

* Западная Европа
* Северная Европа
* Юго-Восточная Азия
* Восточная Азия
* Центральный регион США
* Северо-центральный регион США
* Южно-центральный регион США
* Запад США
* Восток США
* Восточная часть Японии
* Западная часть Японии
* Южная Бразилия
* Восточная часть Австралии
* Юго-Восточная часть Австралии

## <a name="CreateCloudService"> </a>Практическое руководство. Создание облачной службы
При создании приложения и запустите его в Azure, hello код и конфигурация вместе называются Azure [облачная служба] [ cloud service] (известный как *размещенной службы* в более ранних версий Выпуски Azure). Hello **создания\_размещенных\_службы** метод позволяет toocreate новую размещенную службу, указав имя размещенной службы (которое должно быть уникальным в Azure), метки (автоматически кодировке toobase64) Описание и расположение.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

Вы можете вывести список всех hello размещенных служб для вашей подписки с hello **списка\_размещенных\_служб** метод:

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

Если требуется tooget сведения о конкретной размещенной службы, это можно сделать, передав имя toohello hello размещенной службы **получить\_размещенных\_службы\_свойства** метод:

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

После создания облачной службы можно развернуть службы toohello кода с hello **создания\_развертывания** метод.

## <a name="DeleteCloudService"> </a>Практическое руководство. Удаление облачной службы
Можно удалить облачную службу, передавая имя toohello hello службы **удаление\_размещенных\_службы** метод:

    sms.delete_hosted_service('myhostedservice')

Прежде чем можно будет удалить службу, необходимо сначала удалить все развертывания для службы hello. (Дополнительные сведения см. в разделе [Практическое руководство. Удаление развертывания](#DeleteDeployment).)

## <a name="DeleteDeployment"> </a>Практическое руководство. Удаление развертывания
toodelete развертывания, используйте hello **удаление\_развертывания** метод. Hello следующем примере показано как toodelete развертывания с именем `v1`.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <a name="CreateStorageService"> </a>Практическое руководство. Создание службы хранилища
Объект [службы хранилища](../storage/common/storage-create-storage-account.md) предоставляет вам доступ tooAzure [большие двоичные объекты](../storage/blobs/storage-python-how-to-use-blob-storage.md), [таблиц](../cosmos-db/table-storage-how-to-use-python.md), и [очереди](../storage/queues/storage-python-how-to-use-queue-storage.md). toocreate службы хранилища, необходимо имя для службы hello (от 3 до 24 символов нижнего регистра и уникальным в пределах Azure), описание, метку (вверх too100 символов, автоматически кодировке toobase64) и расположение. Hello в следующем примере показано, как службы toocreate хранилища, указав местоположение.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mystorageaccount'
    label = 'mystorageaccount'
    location = 'West US'
    desc = 'My storage account description.'

    result = sms.create_storage_account(name, desc, label, location=location)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

Обратите внимание, в предыдущих пример hello состояния hello hello **создания\_хранения\_учетной записи** операции можно получить, передав hello результата, возвращаемого методом **создания\_хранилища \_учетной записи** toohello **получить\_операции\_состояние** метод.  

Можно составить список учетных записей хранилища и их свойства с hello **списка\_хранения\_учетные записи** метод:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <a name="DeleteStorageService"> </a>Практическое руководство. Удаление службы хранилища
Служба хранилища можно удалить, передав toohello имя службы хранилища hello **удаление\_хранения\_учетной записи** метод. Удаление службы хранилища удаляет все данные, хранящиеся в службе hello (больших двоичных объектов, таблиц и очередей).

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <a name="ListOperatingSystems"> </a>Практическое руководство. Список доступных операционных систем
toolist hello операционных систем, доступных для размещения служб, использовать hello **списка\_операционной\_систем** метод:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

Кроме того, можно использовать hello **списка\_операционной\_системы\_семейства** метод, который группирует hello операционных систем семейства:

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <a name="CreateVMImage"> </a>Практическое руководство. Создание образа операционной системы
tooadd репозиторием изображения toohello образа операционной системы используйте hello **добавить\_ОС\_изображения** метод:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mycentos'
    label = 'mycentos'
    os = 'Linux' # Linux or Windows
    media_link = 'url_to_storage_blob_for_source_image_vhd'

    result = sms.add_os_image(label, media_link, name, os)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

образы операционной системы toolist hello, которые недоступны, используйте hello **списка\_ОС\_изображения** метод. Сюда входят все образы платформ и пользовательские образы.

    result = sms.list_os_images()

    for image in result:
        print('Name: ' + image.name)
        print('Label: ' + image.label)
        print('OS: ' + image.os)
        print('Category: ' + image.category)
        print('Description: ' + image.description)
        print('Location: ' + image.location)
        print('Media link: ' + image.media_link)
        print('')

## <a name="DeleteVMImage"> </a>Практическое руководство. Удаление образа операционной системы
toodelete пользовательский образ, используйте hello **удаление\_ОС\_изображения** метод:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <a name="CreateVM"> </a>Практическое руководство. Создание виртуальной машины
toocreate виртуальной машины, необходимо сначала toocreate [облачная служба](#CreateCloudService).  Затем создайте hello развертывания виртуальной машины, с помощью hello **создания\_виртуальных\_машины\_развертывания** метод:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where hello VM disk
    # will be created
    media_link = 'url_to_target_storage_blob_for_vm_hd'

    # Linux VM configuration, you can use WindowsConfigurationSet
    # for a Windows VM instead
    linux_config = LinuxConfigurationSet('myhostname', 'myuser', 'mypassword', True)

    os_hd = OSVirtualHardDisk(image_name, media_link)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=os_hd,
        role_size='Small')

## <a name="DeleteVM"> </a>Практическое руководство. Удаление виртуальной машины
toodelete виртуальной машины, сначала удалите hello развертывания с помощью hello **удаление\_развертывания** метод:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

Hello облачной службы могут быть удалены с помощью hello **удаление\_размещенных\_службы** метод:

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a>Практическое руководство. Создание виртуальной машины из записанного образа виртуальной машины
toocapture образ ВМ, сначала вызвать метод hello **захвата\_ВМ\_изображения** метод:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace hello below three parameters with actual values
    hosted_service_name = 'hs1'
    deployment_name = 'dep1'
    vm_name = 'vm1'

    image_name = vm_name + 'image'
    image = CaptureRoleAsVMImage    ('Specialized',
        image_name,
        image_name + 'label',
        image_name + 'description',
        'english',
        'mygroup')

    result = sms.capture_vm_image(
            hosted_service_name,
            deployment_name,
            vm_name,
            image
        )

Далее, toomake в том, что успешно захвачены hello образ, используйте hello **списка\_ВМ\_изображения** api и убедитесь, что выбранное изображение отображается в результатах hello:

    images = sms.list_vm_images()

toofinally Создание hello виртуальной машины с помощью hello записанный образ, используйте hello **создания\_виртуальных\_машины\_развертывания** как до, но на этот раз передать hello vm_image_name вместо

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=None,
        role_size='Small',
        vm_image_name = image_name)

Дополнительные сведения о toolearn toocapture виртуальной машины Linux. в статье [как tooCapture виртуальной машины Linux.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

Дополнительные сведения о toolearn toocapture виртуальной машины Windows. в статье [как tooCapture виртуальной машине.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="What's Next"> </a>Дальнейшие действия
Теперь, когда вы узнали основы hello управления службами, можно получить доступ к hello [полный набор API справочную документацию по hello Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) и выполнения сложных задач легко toomanage приложения python.

Дополнительные сведения см. в разделе hello [центре разработчиков Python](/develop/python/).

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect tooservice management]: #Connect
[How to: List available locations]: #ListAvailableLocations
[How to: Create a cloud service]: #CreateCloudService
[How to: Delete a cloud service]: #DeleteCloudService
[How to: Create a deployment]: #CreateDeployment
[How to: Update a deployment]: #UpdateDeployment
[How to: Move deployments between staging and production]: #MoveDeployments
[How to: Delete a deployment]: #DeleteDeployment
[How to: Create a storage service]: #CreateStorageService
[How to: Delete a storage service]: #DeleteStorageService
[How to: List available operating systems]: #ListOperatingSystems
[How to: Create an operating system image]: #CreateVMImage
[How to: Delete an operating system image]: #DeleteVMImage
[How to: Create a virtual machine]: #CreateVM
[How to: Delete a virtual machine]: #DeleteVM
[Next Steps]: #NextSteps
[management-portal]: https://manage.windowsazure.com/
[svc-mgmt-rest-api]: http://msdn.microsoft.com/library/windowsazure/ee460799.aspx


[cloud service]:/services/cloud-services/
