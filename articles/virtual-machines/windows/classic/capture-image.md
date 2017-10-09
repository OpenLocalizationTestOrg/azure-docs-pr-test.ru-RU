---
title: "aaaCapture образ виртуальной Машины Windows Azure | Документы Microsoft"
description: "Запись образа виртуальной машины Microsoft Azure, созданных с помощью hello классической модели развертывания."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: a5986eac-4cf3-40bd-9b79-7c811806b880
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: b9bbc437012aa44295f90941c9d72e39509df28f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-hello-classic-deployment-model"></a>Запись образа виртуальной машины Microsoft Azure, созданных с помощью hello классической модели развертывания.
> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Сведения о модели диспетчера ресурсов см. в разделе [Запись управляемого образа универсальной виртуальной машины в Azure](../capture-image-resource.md).

В этой статье показано, как toocapture виртуальной машине Azure под управлением Windows, ее можно использовать в качестве образа toocreate других виртуальных машин. Этот образ содержит hello диска операционной системы и диски с данными, которые являются присоединенного toohello виртуальной машины. Они не включают конфигурации сети, поэтому вам понадобится tooset конфигурации сети, при создании других виртуальных машин, использующих изображения hello hello.

Хранилища Azure hello образ в столбце **образов виртуальных Машин (классические)**, **вычислений** службу, которая отображается при просмотре всех hello служб Azure. Это hello же месте, где хранятся все отправленные образы. Дополнительные сведения об образах см. в разделе [Об образах виртуальных машин](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).

## <a name="before-you-begin"></a>Перед началом работы
Эти шаги предполагают, что уже создана виртуальная машина Azure и настроить hello операционной системы, включая присоединение диски с данными. Если вы еще не сделали это, см. следующие статьи для получения сведений о создании и Подготовка виртуальной машины hello hello:

* [Создание виртуальной машины из образа](createportal.md)
* [Как tooattach данных на диске tooa виртуальной машины](attach-disk.md)
* Убедитесь, что ролей сервера hello поддерживается с помощью средства Sysprep. Дополнительные сведения см. в разделе [Поддержка ролей сервера в Sysprep](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).

> [!WARNING]
> Этот процесс удаляет hello исходной виртуальной машины, после его снятия.
>
>

Предыдущий toocapturing образа виртуальной машины Azure рекомендуется hello целевая виртуальная машина резервного копирования. Это можно сделать с помощью службы архивации Azure. Дополнительные сведения см. в статье [Архивация виртуальных машин Azure](../../../backup/backup-azure-vms.md). Доступны другие решения от сертифицированных партнеров. toofind о том, что в настоящее время недоступно, найдите hello Azure Marketplace.

## <a name="capture-hello-virtual-machine"></a>Запись hello виртуальной машины
1. В hello [портал Azure](http://portal.azure.com), **Connect** toohello виртуальной машины. Инструкции см. в разделе [как toosign tooa виртуальной машине под управлением Windows Server][How toosign in tooa virtual machine running Windows Server].
2. Откройте окно командной строки с правами администратора.
3. Измените каталог hello слишком`%windir%\system32\sysprep`, а затем запустите sysprep.exe.
4. Hello **средство подготовки системы** откроется диалоговое окно. Здравствуйте, следующие:

   * В разделе **Действие по очистке системы** выберите **Запуск при первом включении компьютера (OOBE)** и убедитесь, что установлен флажок **Обобщить**. Дополнительные сведения об использовании Sysprep см. в разделе [как tooUse Sysprep: введение][How tooUse Sysprep: An Introduction].
   * В разделе **Параметры завершения работы** выберите **Завершение работы**.
   * Нажмите кнопку **ОК**.

   ![Запуск Sysprep](./media/capture-image/SysprepGeneral.png)
5. Sysprep завершает работу виртуальной машины hello, изменяющая состояние hello hello виртуальной машины в Azure portal hello слишком**остановлена**.
6. В hello портал Azure, щелкните **виртуальные машины (классические)** и выберите hello виртуальную машину будет toocapture. Hello **образов виртуальных Машин (классические)** группа указана в разделе **вычислений** при просмотре **дополнительные службы**.

7. На панели команд hello, нажмите кнопку **записи**.

   ![Запись виртуальной машины](./media/capture-image/CaptureVM.png)

   Hello **hello записи виртуальной машины** откроется диалоговое окно.

8. В **имя образа**, введите имя для нового образа hello. В **метка образа**, введите метку для нового образа hello.

9. Нажмите кнопку **запущено средство Sysprep на виртуальной машине hello**. Этот флажок указывает toohello действия с помощью средства Sysprep в шагах 3 – 5. Изображение _должен_ обобщить, запустив программу Sysprep перед добавлением Windows Server tooyour набор пользовательских образов.

10. После завершения записи hello hello новый образ не станет доступным в hello **Marketplace**, в hello **вычислений**, **образов виртуальных Машин (классические)** контейнера.

    ![Успешная запись образа](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a>Дальнейшие действия
изображение Hello — Готово toobe используется toocreate виртуальных машин. toodo это, вы создадите виртуальную машину, выбрав hello **дополнительные службы** пункта меню hello нижней части меню служб hello, затем **образов виртуальных Машин (классические)** в hello **вычислений**группы. Инструкции см. в статье [Создание виртуальной машины из образа](createportal.md).

[How toosign in tooa virtual machine running Windows Server]:connect-logon.md
[How tooUse Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[hello virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of hello virtual machine]: ./media/capture-image/CaptureVM.png
[Enter hello image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use hello captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
