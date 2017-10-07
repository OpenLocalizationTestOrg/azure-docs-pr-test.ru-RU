---
title: "базы данных служб Analysis Services aaaAzure резервного копирования и восстановления | Документы Microsoft"
description: "Описывает, как toobackup и восстановления служб Azure Analysis Services базы данных."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: cf0a782d237a95fdfa5ef628f998bd053aac0d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore"></a>Архивация и восстановление

Резервное копирование баз данных табличной модели в службах Analysis Services Azure является намного hello таким же как и для локальных служб Analysis. Hello основное различие заключается в хранения файлов резервных копий. Файлы резервной копии необходимо сохранить контейнера tooa в [учетной записи хранилища Azure](../storage/common/storage-create-storage-account.md). Можно использовать уже имеющиеся учетную запись хранения и контейнер либо создать их при настройке параметров хранилища для сервера.

> [!NOTE]
> Создание учетной записи хранения может привести к дополнительным расходам. toolearn более, в разделе [цены на хранилища Azure](https://azure.microsoft.com/pricing/details/storage/blobs/).
> 
> 

Архивные копии сохраняются с расширением ABF. Для табличных моделей в памяти сохраняются как данные, так и метаданные модели. Для табличных моделей с прямым запросом (DirectQuery) сохраняются только метаданные моделей. Резервные копии сжимаются и шифруются, в зависимости от выбранных параметров hello. 



## <a name="configure-storage-settings"></a>Настройка параметров хранения
Перед созданием резервной копии необходимо tooconfigure настройки хранилища для вашего сервера.


### <a name="tooconfigure-storage-settings"></a>Параметры хранилища tooconfigure
1.  На портале Azure выберите **Параметры** и щелкните **Архивация**.

    ![Архивация в параметрах](./media/analysis-services-backup/aas-backup-backups.png)

2.  Щелкните **Включено**, а затем — **Параметры хранилища**.

    ![Включение](./media/analysis-services-backup/aas-backup-enable.png)

3. Выберите имеющуюся учетную запись хранения или создайте новую.

4. Выберите контейнер или создайте новый.

    ![Выбор контейнера](./media/analysis-services-backup/aas-backup-container.png)

5. Сохраните параметры архивации.

    ![Сохранение параметров архивации](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a>Резервное копирование

### <a name="toobackup-by-using-ssms"></a>toobackup с помощью среды SSMS

1. В среде SSMS щелкните правой кнопкой мыши базу данных и выберите **Архивировать**.

2. В разделе **Резервное копирование базы данных** > **Файл резервной копии** нажмите кнопку **Обзор**.

3. В hello **сохранить файл как** диалогового окна, проверьте путь к папке hello, а затем введите имя для файла резервной копии hello. 

4. В hello **Backup Database** диалоговое окно, выберите параметры.

    **Позволяет создать файл перезаписать** -выберите этот параметр toooverwrite файлы резервной копии hello таким же именем. Если этот параметр не выбран, сохранении файла hello не может иметь hello точно такое же имя файла, который уже существует в hello же расположение.

    **Выполнить сжатие** -выберите данный параметр toocompress hello файл резервной копии. Сжатые архивные файлы экономят место на диске, но немного повышают использование ЦП. 

    **Зашифровать файл резервной копии** -выберите данный параметр tooencrypt hello файл резервной копии. Этот параметр требует пользовательского пароля toosecure hello файл резервной копии. Hello пароль предотвращает считывания резервных копий данных hello другим способом, чем операции восстановления. При выборе tooencrypt резервные копии, сохраните пароль hello в безопасном месте.

5. Нажмите кнопку **ОК** toocreate и сохраните файл резервной копии hello.


### <a name="powershell"></a>PowerShell
Используйте командлет [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet).

## <a name="restore"></a>восстановление;
При восстановлении файла резервной копии необходимо в учетной записи хранилища hello, настроенные для сервера. Файл резервной копии из локальной учетной записи хранилища расположение tooyour toomove используйте [обозреватель хранилищ Microsoft Azure](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) или hello [AzCopy](../storage/common/storage-use-azcopy.md) программы командной строки. 



> [!NOTE]
> Если производится восстановление с локального сервера, необходимо удалить все пользователи домена hello из роли модели hello и добавьте их обратно toohello роли в качестве пользователей Azure Active Directory.
> 
> 

### <a name="toorestore-by-using-ssms"></a>toorestore с помощью среды SSMS

1. В среде SSMS щелкните правой кнопкой мыши базу данных и выберите **Восстановить**.

2. В hello **Backup Database** диалоговое окно, в **файл резервной копии**, нажмите кнопку **Обзор**.

3. В hello **расположение файлов базы данных** диалоговое окно, выберите hello файл toorestore.

4. В **инструкцию Restore database**выберите hello базы данных.

5. Укажите параметры. Параметры безопасности, должны соответствовать hello параметры резервного копирования, которая использовалась при создании резервной копии.


### <a name="powershell"></a>PowerShell

Используйте командлет [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet).


## <a name="related-information"></a>Связанные сведения

[Учетные записи хранения Azure](../storage/common/storage-create-storage-account.md)  
[Высокая доступность](analysis-services-bcdr.md)     
[Управление службами Azure Analysis Services](analysis-services-manage.md)
