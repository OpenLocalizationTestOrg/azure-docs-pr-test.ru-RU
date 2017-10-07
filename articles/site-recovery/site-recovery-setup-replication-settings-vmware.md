---
title: "aaaSet настроек репликации для Azure Site Recovery | Документы Microsoft"
description: "Описывает, каким образом облаков tooAzure toodeploy Site Recovery tooorchestrate репликации, отработки отказа и восстановления виртуальных машин Hyper-V в VMM."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 618e92e42411732a2a1bb75c5e5ea8a433cd7d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-replication-policy-for-vmware-tooazure"></a>Управление политикой репликации для VMware tooAzure


## <a name="create-a-replication-policy"></a>Создание политики репликации

1. Выберите **Управление** > **Site Recovery Infrastructure** (Инфраструктура Site Recovery).
2. В разделе **For VMware and Physical machines** (Для виртуальных машин VMware и физических компьютеров) выберите **Политики репликации**.
3. Щеклните **+Replication policy** (+ Политика репликации).

    ![Создание политики репликации](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. Введите имя политики hello.

5. В **пороговое значение RPO**, ограничить количество RPO hello. Если непрерывная репликация превышает это значение, выдаются оповещения.
6. В **хранения точки восстановления**, укажите (в часах) hello продолжительность периода хранения hello для каждой точки восстановления. Защищенные виртуальные машины могут быть восстановлены tooany точка в пределах периода хранения.

    > [!NOTE]
    > Часы too24 удержания поддерживается для хранилища toopremium реплицированной машины. Часы too72 удержания поддерживается для хранилища toostandard реплицированной машины.

    > [!NOTE]
    > Политика репликации для восстановления размещения создается автоматически.

7. В поле **Периодичность создания моментальных снимков с согласованием приложений** укажите, с какой периодичностью (в минутах) будут создаваться точки восстановления, содержащие моментальные снимки, согласованные на уровне приложений.

8. Нажмите кнопку **ОК**. Hello политики должны создаваться в течение 30 секунд too60.

![Создание политики репликации](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a>Связывание сервера конфигурации с политикой репликации
1. Выберите политику toowhich hello репликации требуется tooassociate hello конфигурации сервера.
2. Щелкните **Связать**.
![Связывание сервера конфигурации](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)

3. Выберите сервер конфигурации hello hello список серверов.
4. Нажмите кнопку **ОК**. Сервер конфигурации Hello должен быть связан один tootwo минут.

![Связывание сервера конфигурации](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a>Изменение политики репликации
1. Выберите политику репликации hello, для которого требуется tooedit настройки репликации.
![Изменение политики репликации](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)

2. Нажмите **Изменить параметры**.
![Изменение параметров политики репликации](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)

3. Измените параметры hello на основании потребностями.
4. Щелкните **Сохранить**. Hello политики должны сохраняться в течение двух минут toofive, в зависимости от того, сколько виртуальных машин с помощью этой политики репликации.

![Сохранение политики репликации](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a>Отмена связи сервера конфигурации с политикой репликации
1. Выберите политику toowhich hello репликации требуется tooassociate hello конфигурации сервера.
2. Щелкните **Отменить связь**.
3. Выберите сервер конфигурации hello hello список серверов.
4. Нажмите кнопку **ОК**. Сервер конфигурации Hello следует несвязанной один tootwo минут.

    > [!NOTE]
    > Невозможно разорвать связь сервера конфигурации, при наличии реплицированных хотя бы один элемент, с помощью политики hello. Убедитесь, что нет реплицированных элементов с помощью политики hello, прежде чем отменить связь сервера конфигурации hello.

## <a name="delete-a-replication-policy"></a>Удаление политики репликации

1. Выберите политику репликации hello, которые должны toodelete.
2. Нажмите кнопку **Delete**(Удалить). следует удалить политики Hello too60 за 30 секунд.

    > [!NOTE]
    > Невозможно удалить политику репликации, если у него есть хотя бы один tooit конфигурации сервера, связанного. Убедитесь, что нет реплицированных элементов с помощью политики hello и удалить все hello связанные серверы конфигурации, прежде чем удалять политику hello.
