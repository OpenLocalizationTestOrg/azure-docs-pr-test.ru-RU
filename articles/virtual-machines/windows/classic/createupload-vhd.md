---
title: "изображений с aaaCreate и отправки виртуальной Машины с помощью Powershell | Документы Microsoft"
description: "Узнайте toocreate и отправить обобщенный образа Windows Server (VHD) с помощью hello классической модели развертывания и Azure Powershell."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8c4a08fe-7714-4bf0-be87-c728a7806d3f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: 093b57c9157cea5f348c8ba02b5700c917adbcdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-windows-server-vhd-tooazure"></a>Создание и отправка tooAzure виртуального жесткого диска Windows Server
В этой статье показано, как tooupload ВМ обобщенный образ как виртуальный жесткий диск (VHD) чтобы вы могли использовать toocreate виртуальных машин. Дополнительные сведения о дисках и виртуальных жестких дисках в Microsoft Azure см. в статье [О дисках и виртуальных жестких дисках для виртуальных машин](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Вы также можете [отправить](../upload-generalized-managed.md) виртуальную машину, используя модель hello диспетчера ресурсов.

## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что у вас есть следующие компоненты.

* **Подписка Azure.** Если подписка отсутствует, можно [создать учетную запись Azure бесплатно](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
* **[Microsoft Azure PowerShell](/powershell/azure/overview)**  -у вас есть hello Microsoft Azure PowerShell модуль установлен и настроен toouse вашей подписки.
* **ОБЪЕКТ. VHD-файл** — поддерживаемые версии операционной системы, хранящиеся в VHD-файл и вложенные tooa виртуальной машины Windows. Проверьте toosee Если hello серверных ролей на hello виртуального жесткого диска поддерживаются Sysprep. Дополнительные сведения см. в разделе [Поддержка ролей сервера в Sysprep](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).

    > [!IMPORTANT]
    > Hello формат VHDX не поддерживается в Microsoft Azure. Вы можете преобразовать формат tooVHD hello диска, с помощью диспетчера Hyper-V или hello [командлет Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx). Дополнительные сведения см. в [этом блоге](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).

## <a name="step-1-prep-hello-vhd"></a>Шаг 1: Подготовьте hello виртуального жесткого диска
Перед отправкой tooAzure hello виртуального жесткого диска, он должен toobe обобщить с помощью средства Sysprep hello. Это подготавливает toobe hello виртуального жесткого диска, используемое в качестве изображения. Дополнительные сведения о программе Sysprep см. в разделе [как tooUse Sysprep: введение](http://technet.microsoft.com/library/bb457073.aspx). Резервное копирование hello виртуальной Машины перед запуском Sysprep.

С помощью hello виртуальную машину, которая hello операционной системы был установлен для завершения процедуры hello:

1. Войдите в toohello операционной системы.
2. Откройте окно командной строки с правами администратора. Измените каталог hello слишком**%windir%\system32\sysprep**, а затем запустите `sysprep.exe`.

    ![Откройте окно командной строки.](./media/createupload-vhd/sysprep_commandprompt.png)
3. Hello **средство подготовки системы** откроется диалоговое окно.

   ![Запуск Sysprep](./media/createupload-vhd/sysprepgeneral.png)
4. В hello **средство подготовки системы**выберите **переход в окно приветствия системы (OOBE)** и убедитесь, что **Generalize** проверяется.
5. В разделе **Параметры завершения работы** выберите **Завершение работы**.
6. Нажмите кнопку **ОК**.

## <a name="step-2-create-a-storage-account-and-a-container"></a>Шаг 2. Создание учетной записи хранения и контейнера
Необходимо учетной записи хранилища в Azure, чтобы у вас есть место tooupload hello VHD-файл. В этом шаге показано, как toocreate учетную запись или get hello сведения из существующей учетной записи. Замените переменные hello в &lsaquo; скобки &rsaquo; со своих собственных сведений.

1. Вход

    ```powershell
    Add-AzureAccount
    ```

2. Настройте свою подписку Azure.

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. Создайте учетную запись хранения. Имя Hello hello учетной записи хранения должно быть уникальным, 3 до 24 символов. Hello имя может быть любым сочетанием букв и цифр. Необходимо также toospecify местоположение, например «East US»

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. Установить hello новой учетной записи хранения по умолчанию hello.

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. Создайте новый контейнер.

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-hello-vhd-file"></a>Шаг 3: Отправка hello VHD-файл
Используйте hello [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) tooupload hello виртуального жесткого диска.

Из окна Azure PowerShell hello, используемый в предыдущем шаге hello, тип hello следующую команду и замените переменные hello в &lsaquo; скобки &rsaquo; со своих собственных сведений.

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-hello-image-tooyour-list-of-custom-images"></a>Шаг 4: Добавление hello изображения tooyour список пользовательских образов
Используйте hello [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) командлет tooadd hello изображения toohello список пользовательских образов.

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь вы можете [Создание пользовательской виртуальной Машины](createportal.md) загружен с помощью hello образа.
