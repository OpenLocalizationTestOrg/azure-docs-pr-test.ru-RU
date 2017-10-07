---
title: "aaaSet hello исходного и целевого объекта для физического сервера tooAzure репликации с помощью Azure Site Recovery | Документы Microsoft"
description: "Перечислены tooset действия hello исходных и целевых параметров репликации хранилища tooAzure физических серверов со службой Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 2e3d03bc-4e53-4590-8a01-f702d3cc9500
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e75ef23174d77509bf54380eba8f251a7337a45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-hello-source-and-target-for-physical-server-replication-tooazure"></a>Шаг 7: Настройка hello исходной и целевой для tooAzure репликации физического сервера

В этой статье описывается, как tooconfigure источника и целевых параметров при репликации локально tooAzure физических серверов, с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.

Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Настройка среды источника hello

Настройка сервера конфигурации hello, зарегистрируйте его в хранилище hello и обнаружение компьютеров.

1. Щелкните **Site Recovery** > **Шаг 1. Подготовка инфраструктуры** > **Источник**.
2. Если у вас нет сервера конфигурации, щелкните **+Configuration server** (+ Сервер конфигурации).
3. В колонке **Добавление сервера** в поле **Тип сервера** должно быть указано **Сервер конфигурации**.
4. Загрузите файл установки hello установка единой Site Recovery.
5. Загрузите ключ регистрации в хранилище hello. Он потребуется при запуске единой установки. Hello ключ действителен в течение пяти дней после его создания.

   ![Настройка источника](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a>Зарегистрируйте сервер конфигурации hello в хранилище hello

Следующие hello, прежде чем начать, а затем выполните tooinstall hello конфигурации сервера, сервера обработки hello и главный целевой сервер hello единой программы установки. Hello видео Настройка компонентов hello tooAzure репликации виртуальной Машины VMware. Однако hello одного процесса является допустимым для репликации tooAzure физического сервера.

- На сервере конфигурации hello виртуальной Машины, убедитесь, что системные часы, hello синхронизируется с [сервер времени](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Значения времени должны совпадать. Если системные часы отстают или спешат в пределах 15 минут, установка может завершиться ошибкой.
- Запустите программу установки локального администратора на сервере конфигурации hello.
- Убедитесь в том, что протоколы TLS 1.0 включен в hello виртуальной Машины.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> также можно установить сервер конфигурации Hello [из командной строки hello](http://aka.ms/installconfigsrv).




## <a name="set-up-hello-target-environment"></a>Настройка целевой среды hello

Перед настройкой hello целевой среде, убедитесь, что у вас есть учетная запись хранения Azure и настройка виртуальной сети.

1. Нажмите кнопку **подготовки инфраструктуры** > **целевой**, и выберите hello требуется toouse подписки Azure.
2. Укажите, какая целевая модель развертывания используется: классическая или Resource Manager.
3. Site Recovery проверяет наличие одной или нескольких совместимых учетных записей хранения и сетей Azure.

   ![Цель](./media/physical-walkthrough-source-target/gs-target.png)

4. Если вы еще не создали учетную запись хранения или сети, нажмите кнопку **+ учетная запись хранения** или **+ сети**, toocreate диспетчера ресурсов учетной записи или сети встроенной.

## <a name="next-steps"></a>Дальнейшие действия

Go слишком[Step 8: настроить политику репликации](physical-walkthrough-replication.md)
