---
title: "на основе образа Azure RemoteApp на Виртуальной машине Azure aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate изображения для Azure RemoteApp с помощью виртуальной машины Azure."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d41583ef-6cd8-4115-8dcb-b2cd5b3d301a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 2d432bcb15be68a2946d91b5f36f41d980726338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a>Создание образа Azure RemoteApp на основе виртуальной машины Azure
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Можно создать образы Azure RemoteApp (которые содержат приложения hello, отправляемого в коллекции) из виртуальной машины Azure. Можно также выбрать toouse образ виртуальной машины, мы добавили коллекции образов виртуальных Машин Azure toohello, соответствующий всем требованиям образ Azure RemoteApp hello - можно использовать этот образ виртуальной Машины в качестве отправной точки для ВМ, если требуется. Просто найти образ «Удаленный рабочий стол узла сеансов Windows Server» hello в библиотеке hello.

Существует два toocreate действия на основе собственного образа на Виртуальной машине Azure — создать образ hello, а затем передать его из tooAzure библиотеки hello виртуальной Машины Azure RemoteApp.

## <a name="create-a-custom-image-based-on-an-azure-vm"></a>Создание пользовательского образа на основе виртуальной машины Azure
Используйте эти шаги toocreate изображения на Виртуальной машине Azure.

1. Создайте виртуальную машину Azure. Можно использовать hello «Удаленный рабочий стол узла сеансов Windows Server» или «Windows Server удаленного рабочего стола сеанса узла с Microsoft Office 365 профессиональный плюс» image hello из коллекции образов виртуальных машин Azure hello. Этот образ требованиям всех hello Azure RemoteApp шаблона изображения.
   
    Дополнительные сведения см. в статье [Создание первой виртуальной машины Windows на портале Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
2. Подключение toohello ВМ и установить и настроить приложения hello, что требуется tooshare через RemoteApp. Убедитесь, что tooperform все дополнительные конфигурации Windows, необходимые для приложения.
   
    Дополнительные сведения см. в разделе [как tooLog на виртуальной машине под управлением Windows Server tooa](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
3. При использовании одного из образов hello узла сеансов удаленных рабочих столов Windows Server, является сценарий включены проверки, который обеспечит соответствие виртуальной Машины hello RemoteApp pre-reqs. сценарий toorun дважды щелкните **ValidateRemoteAppImage** на рабочем столе hello. Убедитесь, что все ошибки, о которых сообщает скрипт hello имеют фиксированную перед продолжением toohello следующий шаг.
4. SYSPREP обобщения и записи образа hello. В разделе [как tooCapture tooUse виртуальной машине Windows, как шаблон](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) инструкции.

## <a name="import-hello-image-into-hello-azure-remoteapp-image-library"></a>Импорт изображения hello библиотека изображений hello Azure RemoteApp
Используйте эти шаги tooimport hello образ в Azure RemoteApp:

1. В hello **образы шаблонов** вкладки:
   
   * если у вас нет образов, щелкните **Загрузить или импортировать образ шаблона**;
   * Если у вас уже есть по крайней мере один образ, нажмите кнопку  **+**  tooadd новый образ.
2. Выберите библиотеку **Импортировать образ из библиотеки виртуальных машин** и нажмите кнопку **Далее**.
3. На следующей странице приветствия выберите образ из списка hello и убедитесь, что вы выполнили шаги hello, указанные при создании образа. Щелкните **Далее**.
4. Введите имя для нового образа RemoteApp hello и выберите расположение hello, а затем нажмите кнопку Импорт hello флажок toostart hello.

> [!NOTE]
> Изображения можно импортировать из любого расположения Azure, поддерживаются в виртуальных машинах Azure tooany расположение Azure, поддерживаемые Azure RemoteApp. В зависимости от расположения hello hello импорта может занять too25 минут.
> 
> 

Теперь вы готовы toocreate новой коллекции, либо [облака](remoteapp-create-cloud-deployment.md) коллекции или [гибридных](remoteapp-create-hybrid-deployment.md), в зависимости от потребностей.

