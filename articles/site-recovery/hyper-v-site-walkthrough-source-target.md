---
title: "aaaSet hello исходного и целевого объекта для tooAzure репликации Hyper-V (без System Center VMM) с Azure Site Recovery | Документы Microsoft"
description: "Перечислены tooset действия hello исходных и целевых параметров репликации хранилища tooAzure виртуальных машин Hyper-V с помощью Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d2010d85-77fd-4dea-84f3-1c960ed4c63f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 105b90e6ac053d5b842c54a36c460a26d0f5c2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-replication-tooazure"></a>Шаг 8: Настройка hello исходной и целевой для tooAzure репликации Hyper-V

В этой статье описывается, как tooconfigure источника и целевых параметров при репликации локально tooAzure Hyper-V виртуальных машин (без System Center VMM), с помощью hello [Azure Site Recovery](site-recovery-overview.md) в hello портал Azure.

Учет комментарии и вопросы hello нижней части этой статьи, или на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Настройка среды источника hello

Настройка сайта hello Hyper-V и установки hello поставщика Azure Site Recovery и агента служб восстановления Azure hello на узлах Hyper-V зарегистрировать узел hello в хранилище hello.

1. В разделе **Подготовка инфраструктуры** щелкните **Источник**. Щелкните новый узел Hyper-V как контейнер для узлов Hyper-V или кластеры tooadd **+ сайт Hyper-V**.

    ![Настройка источника](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. В **узла Hyper-V, создайте**, укажите имя для сайта hello. Нажмите кнопку **ОК**. Теперь выберите hello сайт создан и нажмите кнопку **+ Hyper-V Server** tooadd toohello узла на сервере.

    ![Настройка источника](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. Убедитесь, что **сервер Hyper-V** отображается в разделе **Добавить сервер** > **Тип сервера**.

    - Убедитесь, что этот сервер hello Hyper-V, требуется tooadd соответствует hello [необходимых компонентов](#on-premises-prerequisites), и является может tooaccess hello указанного URL-адреса.
    - Загрузите файл установки поставщика Azure Site Recovery hello. Запустите этот файл tooinstall hello поставщика и hello агента служб восстановления на каждом узле Hyper-V.

    ![Настройка источника](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-hello-provider-and-agent"></a>Установите hello поставщика и агента

1. Запустите файл установки поставщика hello на каждом узле вы добавили сайта toohello Hyper-V. Если установка выполняется в кластер Hyper-V, программу установки необходимо запустить на каждом узле кластера. Установка и регистрация всех узлов кластера Hyper-V гарантирует, что виртуальные машины будут защищены даже при переносе между узлами.
2. Обновления можно включить на странице **Центр обновления Майкрософт**. Это позволит устанавливать обновления поставщика в соответствии с политикой Центра обновления Майкрософт.
3. В **установки**примите или измените расположение установки поставщика по умолчанию hello и нажмите кнопку **установить**.
4. В **параметры хранилища**, нажмите кнопку **Обзор** tooselect hello хранилище ключей загруженный файл. Укажите подписку Azure Site Recovery hello, имя хранилища hello, и принадлежит hello Hyper-V сайта toowhich hello Hyper-V server.

    ![Регистрация сервера](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. В **параметры прокси-сервера**, укажите, как поставщик, запущенный на узлах Hyper-V подключается tooAzure Site Recovery через hello hello Интернета.

    * Если выбирается tooconnect hello поставщика непосредственно **подключаться напрямую tooAzure Site Recovery без учетной записи-посредника**.
    * Если требуется toouse настраиваемого прокси-сервера для соединения с поставщиком hello существующего прокси-сервер требует проверки подлинности, выберите **подключения tooAzure Site Recovery с использованием прокси-сервер**.
    * При использовании прокси-сервера:
        - Укажите адрес hello, порт и учетные данные
        - Убедитесь, что hello URL-адреса, описанные в hello [необходимые компоненты](#prerequisites) разрешены через прокси-сервер hello.

    ![Интернет](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. После завершения установки, нажмите кнопку **зарегистрировать** tooregister hello сервера в хранилище hello.

    ![Расположение установки](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. После завершения регистрации Azure Site Recovery извлекает метаданные с сервера hello Hyper-V, и hello сервера отображается в **инфраструктура Site Recovery** > **узлов Hyper-V**.


## <a name="set-up-hello-target-environment"></a>Настройка целевой среды hello

Укажите учетную запись хранилища Azure hello для репликации и hello toowhich сети Azure виртуальные машины Azure будут подключаться после отработки отказа.

1. Выберите **Подготовка инфраструктуры** > **Цель**.
2. Выберите подписку hello и hello группы ресурсов, в котором нужно toocreate hello виртуальные машины Azure после отработки отказа. Выберите hello развертывания модели, что требуется toouse в Azure (классического или ресурса управления) для hello виртуальных машин.

3. Site Recovery проверяет наличие одной или нескольких совместимых учетных записей хранения и сетей Azure.

    - Если у вас нет учетной записи хранилища, нажмите кнопку **+ хранилище** toocreate встроенный диспетчер ресурсов на основе учетной записи. 
    - Если у вас нет сети Azure, щелкните **+ сети** toocreate встроенного сети на основе диспетчера ресурсов.






## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 9: настроить политику репликации](hyper-v-site-walkthrough-replication.md)
