---
title: "tooAzure стека образа виртуальной Машины aaaAdding | Документы Microsoft"
description: "Добавить вашей организации Windows или Linux VM образ для toouse клиентов"
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
ms.openlocfilehash: 26dd6c289664c4d64d5932f4396ae778f3f1e1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="make-a-custom-virtual-machine-image-available-in-azure-stack"></a>Выбрать изображение настраиваемой виртуальной машины, доступные в стек Azure

Azure позволяет стека облака Администраторы toomake настраиваемой виртуальной машины изображения tootheir доступных пользователей. Эти образы могут ссылаться шаблоны Azure Resource Manager или добавлены toothe пользовательского интерфейса Azure Marketplace с hello создания элемента Marketplace. 

## <a name="add-a-vm-image-toomarketplace-with-powershell"></a>Добавьте toomarketplace образа виртуальной Машины с помощью PowerShell

Запустите hello следующие необходимые компоненты из hello [пакет средств разработки](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), или из внешнего клиента Windows в случае [подключен через виртуальную частную сеть](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)

* [Установите PowerShell для Azure стека](azure-stack-powershell-install.md).  

* Загрузите hello [toowork необходимые средства с Azure стека](azure-stack-powershell-download.md).  

* Подготовка образа виртуального жесткого диска операционной системы Windows или Linux в формате VHD (не VHDX).
   
   * Для образов Windows hello статьи [отправить tooAzure образ виртуальной Машины Windows для развертывания диспетчера ресурсов](../virtual-machines/windows/upload-generalized-managed.md) содержит инструкции по подготовке образа в hello **hello подготовки виртуального жесткого диска для передачи** раздела.
   * Для образов Linux, выполните действия hello для подготовки образа hello или использовать существующий образ Azure Linux стека, как описано в статье hello [виртуальные машины Linux развертывания в Azure стека](azure-stack-linux.md).  

Теперь выполните следующие шаги tooadd hello изображения toohello стека Azure marketplace hello.

1. Импортируйте модули Connect и ComputeAdmin hello:
   
   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import hello Connect and ComputeAdmin modules
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1
   ``` 

2. Войдите в систему tooyour среды Azure стека. Выполнения hello следующий скрипт в зависимости от того, при развертывании среды стека Azure с помощью AAD или AD FS (Убедитесь, что tooreplace hello AAD имя клиента): 

   а. **Azure Active Directory**, используйте следующий командлет hello:

   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
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

   b. **Службы федерации Active Directory**, используйте следующий командлет hello:
    
   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
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
    
3. Добавить образ виртуальной Машины hello путем вызова hello `Add-AzsVMImage` командлета. В командлет Add-AzsVMImage hello укажите hello osType как Windows или Linux. Включить hello издателя, предложение, SKU и версия для hello образа виртуальной Машины. В разделе hello [параметры](#parameters) сведения о hello допускается параметров. Эти параметры используются образа виртуальной Машины hello tooreference шаблонов диспетчера ресурсов Azure. Ниже приведен пример вызова скрипта hello.
     
     ```powershell
     Add-AzsVMImage `
       -publisher "Canonical" `
       -offer "UbuntuServer" `
       -sku "14.04.3-LTS" `
       -version "1.0.0" `
       -osType Linux `
       -osDiskLocalPath 'C:\Users\AzureStackAdmin\Desktop\UbuntuServer.vhd' `
     ```

Команда Hello hello следующие:

* Проверяет подлинность среды toohello стек Azure
* Отправляет локального виртуального жесткого диска tooa hello созданная учетная запись временного хранилища
* Добавляет репозитория образов виртуальных Машин toohello образ виртуальной Машины hello и
* Создает элемент Marketplace

tooverify, команда hello выполнено успешно, перейдите tooMarketplace hello портала, а затем убедитесь этот образ виртуальной Машины hello доступен в hello **виртуальные машины** категории.

![Образ виртуальной Машины успешно добавлено](./media/azure-stack-add-vm-image/image5.PNG) 

## <a name="remove-a-vm-image-with-powershell"></a>Удаление образа виртуальной Машины с помощью PowerShell

При hello образ виртуальной машины, который вы отправили ранее больше не нужна, можно удалить из hello marketplace с помощью hello, выполнив командлет:

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
| **Издатель** |Сегмент имени издателя Hello hello образа виртуальной Машины, который пользователи используют при развертывании образа hello. Например, «Microsoft». Не включайте пробел или другие специальные символы в этом поле. |
| **предложение** |Hello сегмент имени предложение hello образа виртуальной Машины, которую пользователи применять при развертывании образа виртуальной Машины hello. Пример: 'WindowsServer». Не включайте пробел или другие специальные символы в этом поле. |
| **sku** |Hello сегмент имя SKU hello образа виртуальной Машины, которую пользователи применять при развертывании образа виртуальной Машины hello. Например, «Datacenter2016». Не включайте пробел или другие специальные символы в этом поле. |
| **version** |Версия образа виртуальной Машины, которую пользователи применять при развертывании образа виртуальной Машины hello hello Hello. Эта версия имеет формат hello  *\#.\#. \#*. Например, "1.0.0». Не включайте пробел или другие специальные символы в этом поле. |
| **osType** |Hello osType hello изображения должен быть «Windows» или «Linux». |
| **osDiskLocalPath** |диск toohello ОС Hello локальный путь виртуального жесткого диска, который вы отправляете как tooAzure образ виртуальной Машины стека. |
| **dataDiskLocalPaths** |Необязательный массив hello локальных путей для дисков данных, которые могут быть загружены как часть образа виртуальной Машины hello. |
| **CreateGalleryItem** |Логический флаг, который определяет, является ли toocreate элемент в Marketplace. По умолчанию устанавливается tootrue. |
| **Заголовок** |Hello отображаемое имя элемента Marketplace. По умолчанию он имеет значение toohello издателя предложение номера Sku образа ВМ hello. |
| **description** |Описание Hello элемента Marketplace hello. |
| **расположение** |необходимо опубликовать Hello расположение toowhich hello образ операционной системы. По умолчанию это значение имеет значение toolocal.|
| **osDiskBlobURI** |При необходимости этот сценарий также принимает URI хранилища BLOB-объектов для osDisk. |
| **dataDiskBlobURIs** |При необходимости этот сценарий также принимает массив URI хранилища BLOB-объект для добавления образа toohello дисков данных. |

## <a name="add-a-vm-image-through-hello-portal"></a>Добавление образа виртуальной Машины через портал hello

> [!NOTE]
> Этот метод требует создания элементов Marketplace hello отдельно.

Одно из требований образов заключается в том, что они могут ссылаться URI хранилища BLOB-объектов. Подготовка образа операционной системы Windows или Linux в формате VHD (не VHDX), а затем отправьте hello учетная запись хранилища образов tooa в Azure или Azure стека. Если образ уже отправленного toohello хранилища больших двоичных объектов в Azure или Azure стека, можно пропустить шаг 1.

1. [Отправка tooAzure образ виртуальной Машины Windows для развертывания диспетчера ресурсов](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/) или для создания образа Linux, следуйте инструкциям hello, описанным в hello [виртуальные машины Linux развертывания в Azure стека](azure-stack-linux.md) статьи. Необходимо учитывать следующие рекомендации, перед отправкой образа hello hello.

   * Это более эффективно tooupload tooAzure образа хранилища больших двоичных объектов стека чем tooAzure хранилища больших двоичных объектов, поскольку занимает меньше времени toopush hello toohello стека Azure образ репозитория образов. 
   
   * При передаче hello [образа виртуальной Машины Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/), убедитесь, что hello toosubstitute **tooAzure входа** шаг с hello [настройки среды PowerShell hello Azure стека оператор](azure-stack-powershell-configure-admin.md)шаг.  

   * Запишите hello URI, где отправить hello изображение, которое является в кодировке hello хранилища больших двоичных объектов:  *&lt;storageAccount&gt;/&lt;blobContainer&gt; / &lt;targetVHDName&gt;*.vhd

   * toomake hello большого двоичного объекта toohello применимым для анонимного доступа, перейдите контейнера учетной записи хранилища BLOB-объекта где hello ВМ образа виртуального жесткого диска, отправленному слишком**большого двоичного объекта,** , а затем выберите **политики доступа**. Если требуется, можно создать подпись общего доступа для контейнера hello и включить его как часть hello URI большого двоичного объекта.

   ![Перейдите в BLOB-объектов учетной записи toostorage](./media/azure-stack-add-vm-image/image1.png)

   ![Toopublic доступа набор больших двоичных объектов](./media/azure-stack-add-vm-image/image2.png)

2. Вход tooAzure стек как администратор облака > меню "hello" щелкните **дополнительные службы** > **поставщиков ресурсов** > выберите **вычислений**  >  **Образов виртуальных Машин** > **добавить**

3. На hello **добавить образ виртуальной Машины** колонке введите hello издателя, предложение, SKU и версия образа виртуальной машины hello. Эти сегменты имя ссылаться toohello образа виртуальной Машины в шаблоны диспетчера ресурсов. Убедитесь, что tooselect **osType** правильно. Для **URI большого двоичного объекта диска OD**введите hello URI BLOB-объекта, где был загружен образ и нажмите кнопку **создать** toobegin Создание образа виртуальной Машины.
   
   ![Начать toocreate hello изображения](./media/azure-stack-add-vm-image/image4.png)

   Когда hello образ успешно создан, hello состояние образа виртуальной Машины изменяется too'Succeeded ".

4. образ виртуальной машины hello toomake повысить его доступность для их потребления пользователями в hello пользовательского интерфейса, то лучше слишком[создать элемент Marketplace](azure-stack-create-and-publish-marketplace-item.md).

## <a name="next-steps"></a>Дальнейшие действия

[Подготовка виртуальной машины](azure-stack-provision-vm.md)