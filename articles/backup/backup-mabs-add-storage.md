---
title: "aaaUse современных хранилища резервных копий с помощью Azure Backup Server v2 | Документы Microsoft"
description: "Дополнительные сведения о новых возможностях Azure Backup Server v2 hello. В этой статье описывается как tooupgrade установки сервер резервного копирования."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a>Добавление хранилища tooAzure v2 резервное копирование сервера

Azure Backup Server версии 2 поставляется с Modern Backup Storage System Center 2016 Data Protection Manager. Modern Backup Storage обеспечивает до 50 % экономии пространства хранения, архивацию, которая в три раза быстрее, и более эффективное хранилище. Кроме того, предлагается хранение с учетом рабочих нагрузок. 

> [!NOTE]
> toouse современных хранения резервной копии, необходимо запустить v2 резервное копирование сервера в Windows Server 2016. Если запустить Backup Server версии 2 на более ранней версии Windows Server, Azure Backup Server не сможет реализовать преимущества Modern Backup Storage. Вместо этого он будет обеспечивать защиту рабочих нагрузок, как в случае с Backup Server версии 1. Дополнительные сведения см. в разделе hello резервное копирование сервера версии [защиты матрицы](backup-mabs-protection-matrix.md).

## <a name="volumes-in-backup-server-v2"></a>Тома в Backup Server версии 2

Backup Server версии 2 поддерживает тома хранилища. При добавлении тома, резервное копирование форматирует том hello tooResilient файловая система (ReFS), требующий современных хранилища резервных копий. tooadd томом и tooexpand его позже, если вам нужно, мы рекомендуем использовать этот рабочий процесс:

1.  Настройте Backup Server версии 2 на виртуальной машине.
2.  Создайте том на виртуальном диске в пуле носителей:
    1.  Добавление пула носителей tooa диск и создать виртуальный диск с простую структуру.
    2.  Добавьте дополнительные диски и расширить hello виртуального диска.
    3.  Создание тома на виртуальном диске hello.
3.  Добавьте tooBackup hello томов сервера.
4.  Настройте хранилище с учетом рабочих нагрузок.

## <a name="create-a-volume-for-modern-backup-storage"></a>Создание тома для Modern Backup Storage

Использование Backup Server версии 2 в качестве дискового накопителя поможет полностью контролировать хранилище. Томом может быть один диск. Однако следует tooextend хранилища в hello будущих создайте том из дисков, созданных с помощью дисковых пространств. Это может помочь, если требуется tooexpand hello тома для хранения резервных копий. В данном разделе приведены рекомендации по созданию тома с такой конфигурацией.

1. В диспетчере сервера выберите **Файловые службы и службы хранилища** > **Тома** > **Пулы носителей**. В разделе **ФИЗИЧЕСКИЕ ДИСКИ** выберите **Новый пул носителей**. 

    ![Создание учетной записи хранения](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. В hello **ЗАДАЧИ** раскрывающегося списка выберите **новый виртуальный диск**.

    ![Добавление виртуального диска](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. Выберите пул носителей hello, а затем выберите **Добавление физического диска**.

    ![Добавление физического диска](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. Выберите физический диск hello, а затем выберите **расширить виртуальный диск**.

    ![Расширение виртуального диска hello](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. Выберите виртуальный диск hello, а затем выберите **новый том**.

    ![Создание нового тома](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. В hello **выберите hello сервер и диск** диалоговое окно, выберите hello server и hello новый диск. Затем нажмите кнопку **Далее**.

    ![Выберите сервер hello и диск](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a>Добавление дискового пространства тома tooBackup сервера

tooadd tooBackup тома сервера, в hello **управления** области повторное сканирование хранилища hello, а затем выберите **добавить**. Появится список всех hello тома доступны toobe добавлена для хранения резервной копии сервера. После добавления списка toohello выбранных томов доступные тома дать им toohelp понятное имя, управлять ими. Эти tooReFS тома, резервное копирование сервера можно использовать преимущества hello современных хранилища резервной копии, выберите tooformat **ОК**.

![Добавление доступных томов](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a>Настройка хранилища с учетом рабочих нагрузок

С учетом рабочей нагрузки хранилища можно выбрать hello томов, которые более хранят определенных типов рабочих нагрузок. Например можно задать дорогих тома, которые поддерживают большое количество операций ввода вывода на второй (IOPS) toostore только hello рабочих нагрузок, требующих частые резервные большого объема. Примером может быть SQL Server с журналами транзакций. Другие рабочие нагрузки, резервное копирование реже, таких как виртуальные машины, резервное копирование томов toolow затрат.

### <a name="update-dpmdiskstorage"></a>Update-DPMDiskStorage

Хранилище с поддержкой рабочей нагрузки можно настроить с помощью командлета PowerShell hello обновления DPMDiskStorage, который обновляет свойства hello тома в пуле носителей hello на сервере Data Protection Manager.

Синтаксис:

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
Hello следующей картинке показан командлет Update-DPMDiskStorage hello в окне PowerShell hello.

![Команда DPMDiskStorage обновления в окне PowerShell hello Hello](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

Hello изменения, внесенные с помощью PowerShell, отражаются в hello консоли администратора сервера для резервного копирования.

![Диски и тома в консоли администрирования hello](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a>Дальнейшие действия
После установки сервер резервного копирования, узнайте, как tooprepare сервере или включите защиту рабочей нагрузки.

- [Подготовка к резервному копированию рабочих нагрузок с использованием Azure Backup Server](backup-azure-microsoft-azure-backup.md)
- [Используйте резервное копирование сервера tooback сервер VMware](backup-azure-backup-server-vmware.md)
- [Используйте резервное копирование сервера tooback копирование SQL Server](backup-azure-sql-mabs.md)

