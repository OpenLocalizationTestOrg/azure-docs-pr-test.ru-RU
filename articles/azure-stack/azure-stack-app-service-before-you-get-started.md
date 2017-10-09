---
title: "развертывание службы приложений Azure стеке aaaBefore | Документы Microsoft"
description: "Toocomplete действия перед развертыванием службы приложений Azure стеке"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: anwestg
ms.openlocfilehash: fad758232ef2795105036640c2a26abf3fa2c3c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="before-you-get-started-with-app-service-on-azure-stack"></a>Перед началом работы со службой приложения на стек Azure

Необходимо несколько элементов tooinstall службе приложений Azure в стеке Azure:

- Завершено развертывание hello [пакет средств разработки Azure стека](azure-stack-run-powershell-script.md).
- Недостаточно места в системе Azure стека для небольшого развертывания службы приложений Azure стек.  Hello обязательные пространства — примерно 20 ГБ пространства на диске.
- Образ виртуальной Машины Windows Server для использования при создании виртуальных машин для службы приложений Azure стек.
- [Сервер, на котором выполняется SQL Server](#SQL-Server).

>[!NOTE] 
> Здравствуйте, следующие действия *все* вступят в силу на хост-компьютере hello Azure стека.

hello PowerShell интегрированная среда сценариев (ISE) toodeploy поставщик ресурсов должен запускаться от имени администратора. По этой причине необходимо tooallow файлы cookie и JavaScript в профиле Internet Explorer hello использовать toosign в tooAzure Active Directory.

## <a name="turn-off-internet-explorer-enhanced-security"></a>Отключите в Internet Explorer Усиленная безопасность

1.  Войдите в компьютер для комплекта средств для разработки toohello стека Azure как **AzureStack или администратор**, а затем откройте **диспетчера сервера**.

2.  Отключить **конфигурация усиленной безопасности Internet Explorer** для администраторов и пользователей.

3.  Войдите в компьютер для комплекта средств для разработки toohello стека Azure с правами администратора, а затем откройте **диспетчера сервера**.

4.  Отключить **конфигурация усиленной безопасности Internet Explorer** для администраторов и пользователей.

## <a name="enable-cookies"></a>Разрешить файлы cookie

1.  Выберите **запустить** > **все приложения** > **стандартные Windows**. Щелкните правой кнопкой мыши **Internet Explorer** > **дополнительные** > **запустить с правами администратора**.

2.  Если появится запрос, выберите **безопасности рекомендуется использовать**, а затем выберите **ОК**.

3.  В Internet Explorer выберите **средства** (значок шестеренки hello) > **обозревателя** > **конфиденциальности** > **Дополнительно**.

4.  Нажмите кнопку **Advanced** (Дополнительно). Убедитесь, что оба **Accept** флажки. Выберите **ОК** дважды.

5.  Закройте Internet Explorer и перезапустите hello интегрированной среды Сценариев PowerShell от имени администратора.

## <a name="install-powershell-for-azure-stack"></a>Установите PowerShell для Azure стека

tooinstall PowerShell для Azure стека, следуйте указаниям hello [установите PowerShell](azure-stack-powershell-install.md).

## <a name="use-visual-studio-with-azure-stack"></a>Использование Visual Studio с стек Azure

toouse Visual Studio с стек Azure, следуйте указаниям hello [установите Visual Studio](azure-stack-install-visual-studio.md).

## <a name="add-a-windows-server-2016-vm-image-tooazure-stack"></a>Добавьте tooAzure образа виртуальной Машины Windows Server 2016 стека

Поскольку службы приложений развертывает число виртуальных машин, требуется образ виртуальной Машины Windows Server 2016 в стек Azure. tooinstall образ виртуальной Машины, выполните действия hello в [добавить образ виртуальной машины по умолчанию](azure-stack-add-default-image.md).

## <a name="SQL-Server"></a>SQL Server

Службы приложений Azure стеке требуется доступ tooa SQL Server экземпляр toocreate и узла две базы данных toorun hello поставщик ресурсов службы приложений.  Следует выбрать toodeploy ВМ SQL Server в стеке Azure, он должен иметь значение слишком уровня подключения SQL hello**открытый**.  Вы можете toouse экземпляр SQL Server hello при завершении параметры hello в hello службы приложений Azure стека установщика.

## <a name="next-steps"></a>Дальнейшие действия

- [Установить поставщик ресурсов службы приложения hello](azure-stack-app-service-deploy.md).

<!--Image references-->
[1]: ./media/azure-stack-app-service-before-you-get-started/PSGallery.png
[2]: ./media/azure-stack-app-service-before-you-get-started/WebPI_InstalledProducts.png
