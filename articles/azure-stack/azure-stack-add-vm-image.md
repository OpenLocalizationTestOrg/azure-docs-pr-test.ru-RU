---
title: "Добавление образа виртуальной Машины Azure стек | Документы Microsoft"
description: "Добавить организации Windows или Linux VM образ для клиентов на использование"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: e5a4236b-1b32-4ee6-9aaa-fcde297a020f
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 793f6c0f1ad92cec4cbb56662685ca151f90b48c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="make-a-custom-virtual-machine-image-available-in-azure-stack"></a>Выбрать изображение настраиваемой виртуальной машины, доступные в стек Azure

Стек Azure позволяет администраторам облака образы настраиваемой виртуальной машины сделать доступными для пользователей. Эти образы можно ссылаться на шаблоны Azure Resource Manager или добавлен к пользовательскому Интерфейсу Azure Marketplace с созданием элементов Marketplace. 

## <a name="add-a-vm-image-to-marketplace-with-powershell"></a>Добавление образа виртуальной Машины для магазина с помощью PowerShell

Выполнить следующие предварительные требования, либо из [пакет средств разработки](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), или из внешнего клиента Windows в случае [подключен через виртуальную частную сеть](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)

* [Установите PowerShell для Azure стека](azure-stack-powershell-install.md).  

* Загрузить [инструменты, необходимые для работы с Azure стека](azure-stack-powershell-download.md).  

* Подготовка образа виртуального жесткого диска операционной системы Windows или Linux в формате VHD (не VHDX).
   
   * Для образов Windows, статьи [загрузить образ виртуальной Машины Windows Azure для развертывания диспетчера ресурсов](../virtual-machines/windows/upload-generalized-managed.md) содержит инструкции по подготовке образа в **Подготовка виртуального жесткого диска для передачи** раздела.
   * Для образов Linux, выполните шаги, чтобы подготовить образ или использовать существующий образ Azure Linux стека, как описано в статье [виртуальные машины Linux развертывания в Azure стека](azure-stack-linux.md).  

Теперь выполните следующие действия, чтобы добавить изображение в стек Azure marketplace:

1. Импортируйте модули Connect и ComputeAdmin:
   
   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import the Connect and ComputeAdmin modules
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1
   ``` 

2. Войдите в среду Azure стека. Выполните следующий сценарий, в зависимости от среды стека Azure развертывается с помощью AAD или AD FS (Убедитесь, что для замены имени клиента AAD): 

   а. **Azure Active Directory**, используйте следующий командлет:

   ```PowerShell
   # Create the Azure Stack cloud administrator's AzureRM environment by using the following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

   Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience "https://graph.windows.net/"

   $TenantID = Get-AzsDirectoryTenantId `
     -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
     -EnvironmentName AzureStackAdmin

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```

   b. **Службы федерации Active Directory**, используйте следующий командлет:
    
   ```PowerShell
   # Create the Azure Stack cloud administrator's AzureRM environment by using the following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external"

   Set-AzureRmEnvironment `
     -Name "AzureStackAdmin" `
     -GraphAudience "https://graph.local.azurestack.external/" `
     -EnableAdfsAuthentication:$true

   $TenantID = Get-AzsDirectoryTenantId `
     -ADFS 
     -EnvironmentName AzureStackAdmin 

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```
    
3. Добавить образ виртуальной Машины путем вызова `Add-AzsVMImage` командлета. В командлет Add-AzsVMImage укажите osType как Windows или Linux. Включают издатель, предложение, SKU и версия для образа виртуальной Машины. В разделе [параметры](#parameters) сведения о допустимых параметров. Эти параметры используются шаблоны Azure Resource Manager для ссылки на образ виртуальной Машины. Ниже приведен пример вызова скрипта.
     
     ```powershell
     Add-AzsVMImage `
       -publisher "Canonical" `
       -offer "UbuntuServer" `
       -sku "14.04.3-LTS" `
       -version "1.0.0" `
       -osType Linux `
       -osDiskLocalPath 'C:\Users\AzureStackAdmin\Desktop\UbuntuServer.vhd' `
     ```

Команда выполняет следующие задачи.

* Выполняет проверку подлинности в среде Azure стека
* Отправляет локального VHD в учетную запись только что созданный временного хранилища
* Добавляет образ виртуальной Машины в репозиторий образов виртуальных Машин и
* Создает элемент Marketplace

Убедитесь, что команда успешно выполнена, перейдите в Marketplace на портале и убедитесь, что образ виртуальной Машины доступен в **виртуальные машины** категории.

![Образ виртуальной Машины успешно добавлено](./media/azure-stack-add-vm-image/image5.PNG) 

## <a name="remove-a-vm-image-with-powershell"></a>Удаление образа виртуальной Машины с помощью PowerShell

Если вам больше не требуется образ виртуальной машины, который вы отправили ранее, можно удалить его из marketplace, с помощью следующего командлета:

```powershell
Remove-AzsVMImage `
  -publisher "Canonical" `
  -offer "UbuntuServer" `
  -sku "14.04.3-LTS" `
  -version "1.0.0" `
```

## <a name="parameters"></a>Параметры

| Параметр | Описание |
| --- | --- |
| **Издатель** |Сегмент имени издателя образа виртуальной Машины, которую пользователи применять при развертывании образа. Например, «Microsoft». Не включайте пробел или другие специальные символы в этом поле. |
| **предложение** |Сегмент предложение имя образа виртуальной Машины, которую пользователи применять при развертывании образа виртуальной Машины. Пример: 'WindowsServer». Не включайте пробел или другие специальные символы в этом поле. |
| **sku** |Сегмент имя SKU образа виртуальной Машины, которую пользователи применять при развертывании образа виртуальной Машины. Например, «Datacenter2016». Не включайте пробел или другие специальные символы в этом поле. |
| **Версия** |Версия образа виртуальной Машины, которую пользователи применять при развертывании образа виртуальной Машины. Эта версия имеет формат  *\#.\#. \#*. Например, "1.0.0». Не включайте пробел или другие специальные символы в этом поле. |
| **osType** |OsType изображения должен быть «Windows» или «Linux». |
| **osDiskLocalPath** |Локальный путь для виртуального жесткого диска, который загружается как образ виртуальной Машины в Azure стек диск операционной системы. |
| **dataDiskLocalPaths** |Необязательный массив локальных путей для дисков данных, которые могут быть загружены как часть образа виртуальной Машины. |
| **CreateGalleryItem** |Логический флаг, который определяет, следует ли создать элемент в Marketplace. По умолчанию установлено значение true. |
| **Заголовок** |Отображаемое имя элемента Marketplace. По умолчанию он имеет значение издателя-предложение-Sku образа виртуальной Машины. |
| **description** |Описание элемента Marketplace. |
| **расположение** |Расположение, к которому должны публиковаться образа виртуальной Машины. По умолчанию это значение задано для локальных.|
| **osDiskBlobURI** |При необходимости этот сценарий также принимает URI хранилища BLOB-объектов для osDisk. |
| **dataDiskBlobURIs** |При необходимости этот сценарий также принимает массив URI хранилища BLOB-объект для добавления дисков с данными в образе. |

## <a name="add-a-vm-image-through-the-portal"></a>Добавление образа виртуальной Машины на портале

> [!NOTE]
> Этот метод требует создания элемент Marketplace отдельно.

Одно из требований образов заключается в том, что они могут ссылаться URI хранилища BLOB-объектов. Подготовка образа операционной системы Windows или Linux в формате VHD (не VHDX), а затем отправьте образ в учетную запись хранения в Azure или Azure стека. Если образ уже отправлено в хранилище больших двоичных объектов в Azure или Azure стека, можно пропустить шаг 1.

1. [Загрузить образ виртуальной Машины Windows Azure для развертывания диспетчера ресурсов](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/) или для создания образа Linux, следуйте инструкциям, описанным в [виртуальные машины Linux развертывания в Azure стека](azure-stack-linux.md) статьи. Перед отправкой образа необходимо учитывать следующие моменты.

   * Это более эффективно будет передать изображение в хранилище больших двоичных объектов Azure стека, чем хранилище больших двоичных объектов Azure, поскольку требуется меньше времени для передачи образа в репозиторий образов Azure стека. 
   
   * При передаче [образа виртуальной Машины Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/), не забудьте подставить **входа в Azure** пошаговое с [настройки среды PowerShell оператор стек Azure](azure-stack-powershell-configure-admin.md) шаг.  

   * Запишите хранилище больших двоичных объектов URI, где загруженный образ, который находится в следующем формате:  *&lt;storageAccount&gt;/&lt;blobContainer&gt; / &lt;targetVHDName&gt;*.vhd

   * Чтобы сделать BLOB-объект применимым для анонимного доступа, перейдите в контейнер BLOB-объектов учетной записи хранилища, где ВМ образа виртуального жесткого диска, отправленному в **большого двоичного объекта,** , а затем выберите **политики доступа**. Если требуется, можно создать подпись общего доступа для контейнера и включить его как часть URI большого двоичного объекта.

   ![Перейдите к учетной записи хранилища больших двоичных объектов](./media/azure-stack-add-vm-image/image1.png)

   ![Набор больших двоичных объектов доступ к открытым](./media/azure-stack-add-vm-image/image2.png)

2. Войдите в стеке Azure как администратор облака > в меню пункт **дополнительные службы** > **поставщиков ресурсов** > выберите **вычислений**  >  **Образов виртуальных Машин** > **добавить**

3. На **добавить образ виртуальной Машины** колонке введите издателя, предложение, SKU и версия образа виртуальной машины. См. Эти сегменты имя образа виртуальной Машины в шаблоны диспетчера ресурсов. Убедитесь в том выбрать **osType** правильно. Для **URI большого двоичного объекта диска OD**введите URI BLOB-объекта, где был загружен образ и нажмите кнопку **создать** Чтобы приступить к созданию образа виртуальной Машины.
   
   ![Начало для создания образа](./media/azure-stack-add-vm-image/image4.png)

   При успешно создан образ, меняется состояние образа виртуальной Машины «Выполнено».

4. Чтобы сделать более легко доступны для потребления пользователями образ виртуальной машины в пользовательском Интерфейсе, лучше всего [создать элемент Marketplace](azure-stack-create-and-publish-marketplace-item.md).

## <a name="next-steps"></a>Дальнейшие действия

[Подготовка виртуальной машины](azure-stack-provision-vm.md)