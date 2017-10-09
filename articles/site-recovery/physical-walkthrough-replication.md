---
title: "aaaSet политику репликации для физического сервера tooAzure репликации с помощью Azure Site Recovery | Документы Microsoft"
description: "Собраны действия hello потребуется tooset политику репликации при репликации локального хранилища tooAzure физических серверов, с помощью службы Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: d6bdeeffc24ffc8eaba24311f7c76452edb65648
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy-for-physical-server-replication-tooazure"></a>Шаг 8: Настройка политики репликации для репликации tooAzure физического сервера


В этой статье описывается как tooset политику репликации при репликации tooAzure физических серверов Windows и Linux с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.


Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="configure-a-policy"></a>Настройка политики

1. Щелкните **Site Recovery infrastructure** (Инфраструктура Site Recovery) > **Политики репликации** > **+Replication Policy** (+Политика репликации).
2. На странице **Создать политику репликации** укажите имя политики.
3. В **пороговое значение RPO**, ограничить количество RPO hello. Это значение указывает, как часто создаются точки восстановления данных. Если непрерывная репликация превышает это значение, выдаются оповещения.
4. В **хранения точки восстановления**, укажите длительность (в часах) является окном приветствия хранения для каждой точки восстановления. Реплицированные виртуальные машины могут быть восстановлены tooany точки в окне. Копирование too24 часов хранения поддерживается для машин реплицируются toopremium хранилища и 72 часа для стандартного хранилища.
5. В поле **Периодичность создания моментальных снимков с согласованием приложений**укажите, с какой периодичностью (в минутах) будут создаваться точки восстановления, содержащие моментальные снимки, согласованные на уровне приложений. Нажмите кнопку **ОК** toocreate hello политики.

    ![Политика репликации](./media/physical-walkthrough-replication/gs-replication2.png)
8. При создании новой политики она автоматически связывается с сервера конфигурации hello. Для восстановления размещения по умолчанию автоматически создается соответствующая политика. Например, если hello политика репликации — **политики rep** политика восстановления размещения hello будет **rep политика восстановления размещения**. Эта политика не используется, пока не будет запущено восстановление размещения из Azure.

## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 9: Установка службы Mobility hello](physical-walkthrough-install-mobility.md)
