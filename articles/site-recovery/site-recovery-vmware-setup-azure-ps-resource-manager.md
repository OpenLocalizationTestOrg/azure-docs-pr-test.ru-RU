---
title: " Управление сервером обработки, запущенным в Azure (модель Resource Manager) | Документация Майкрософт"
description: "В этой статье описывает обработку tooset копирование и восстановление размещения сервера (диспетчер ресурсов) в Azure."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 70426b96095cc42befff6c4114fb56536284a667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a>Управление сервером обработки, запущенным в Azure (модель Resource Manager)
> [!div class="op_single_selector"]
> * [Диспетчер ресурсов](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [Классическая модель](./site-recovery-vmware-setup-azure-ps-classic.md)

При отработке отказа toodeploy сервера обработки в Azure рекомендуется при наличии высокой задержки между hello виртуальной сети Azure и локальной сетью. В этой статье описывается, как установить, настроить и управлять серверами процесса hello в Azure.

> [!NOTE]
> Эта статья является используется, если вы использовали toobe **диспетчера ресурсов** как hello модель развертывания для hello виртуальных машин во время отработки отказа. Если вы использовали **классический** как hello модели развертывания, выполните действия hello в [как tooset о & Настройка восстановления размещения процесса сервера (классические)](./site-recovery-vmware-setup-azure-ps-classic.md)

## <a name="prerequisites"></a>Предварительные требования

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a>Развертывание сервера обработки в Azure
1. В хранилище hello > **инфраструктура Site Recovery** (под заголовком «Manage» hello) > **серверы конфигурации** (под заголовком «Для VMware и физические компьютеры»), выберите сервер конфигурации hello.
2. На приветствия сервера конфигурации сведения открывшейся странице нажмите кнопку «+ обработать сервера»

  ![Добавление коллекции сервера обработки](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  На hello **добавить сервер обработки** страницы выберите hello последующих значений

  ![Добавление элемента коллекции сервера обработки](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|**Имя поля**|**Значение**|
|-|-|
|Укажите, куда toodeploy сервера обработки|Выберите значение hello **развернуть сервер обработки восстановление после сбоя в Azure** |
|Подписки|Выберите подписку Azure, где отработку отказа виртуальных машин hello hello|
|Группа ресурсов|Можно создать toodeploy группы ресурсов этого процесса сервера или выберите сервер обработки toodeploy hello в существующую группу ресурсов|
|Расположение|Выберите центр обработки данных Azure hello в виртуальных машин hello где отработку отказа в|
|Сеть Azure|Выберите hello Network(VNet) виртуального Azure, виртуальные машины hello где отработку отказа в. Если отработка отказа виртуальных машин выполняется в несколько виртуальных сетей Azure, сервер обработки нужно развернуть в каждую из них.|

4. Заполните остальные hello hello свойства для сервера обработки hello

  ![Добавление сводных данных о сервере обработки](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|**Имя поля**|**Значение**|
|-|-|
|Имя сервера|Отображаемое имя и имя узла для виртуальной машины на сервере обработки.|
| Имя пользователя|Имя пользователя, который становится администратором на этой виртуальной машине.|
|Учетная запись хранения|Имя учетной записи хранилища, там, где размещены виртуального диска виртуальной машины hello hello|
|Подсеть|подключен подсети Hello hello виртуальной сети Azure toowhich hello виртуальной машины|
| IP-адрес|IP-адрес, желательно tooassume сервера hello процесса, когда он загружается|
5. Щелкните toostart кнопку "ОК" hello, развертывание виртуальной машины hello процесса сервера.

> [!NOTE]
> возможности toouse toobe сервер обработки для восстановления размещения, должны tooregister его с сервера конфигурации локальной hello.

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a>Регистрация hello процесса сервера (под управлением Azure) tooa конфигурации сервер (локальный)

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a>Обновление версии toolatest hello процесса сервера.

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a>Отмена регистрации hello процесса сервера (под управлением Azure) из конфигурации сервер (локальный)

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
