---
title: "aaaHow toomanage хранилища Azure File с hello портал Azure | Документы Microsoft"
description: "Узнайте хранилища Azure File toouse hello Azure toomanage портала."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 385b99ac1c3d97ca79059ae8229afb53f1e825cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a>Как toouse хранилища Azure File с hello портала Azure
Hello [портал Azure](https://portal.azure.com) предоставляет пользовательский интерфейс для управления хранилищем файлов Azure. Вы можете выполнять hello, выполнив действия из веб-браузере.

* Создание файлового ресурса
* Отправка и загрузка файлов tooand из файлового ресурса.
* Наблюдение за hello фактического потребления ресурсов для каждой общей папки.
* Измените размер квоты для hello общей папки.
* Скопируйте hello команды mount toouse toomount вашей общей папки из клиента Windows или Linux.

## <a name="create-file-share"></a>Создание общей папки
1. Войдите в систему toohello портал Azure.
2. Hello навигации в меню **учетные записи хранения** или **учетные записи хранения (классические)**.
    
    ![Снимок экрана, показывающий, как файл toocreate поделиться hello портала](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. Выберите учетную запись хранения.

    ![Снимок экрана, показывающий, как файл toocreate поделиться hello портала](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. Выберите службу "Файлы".

    ![Снимок экрана, показывающий, как файл toocreate поделиться hello портала](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. Выберите «Общие папки» и следуйте hello toocreate связи, совместно использовать первый файл.

    ![Снимок экрана, показывающий, как файл toocreate поделиться hello портала](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. Введите имя общей папки hello и hello размер общей папки (вверх ГБ too5120) toocreate hello файл первый файлового ресурса. После создания общей папки hello можно подключить ее из какой файловой системы, который поддерживает SMB 2.1 или SMB 3.0. Можно щелкнуть на **квоты** на hello toochange hello размер общего файлового ресурса файла hello too5120 Гбайт. См. слишком[калькулятор цен Azure](https://azure.microsoft.com/pricing/calculator/) tooestimate hello хранилища стоимость использования хранилища Azure File.

    ![Снимок экрана, показывающий, как файл toocreate поделиться hello портала](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a>Отправка и загрузка файлов
1. Выберите ранее созданную общую папку.

    ![Снимок экрана, показывающий, как tooupload и загрузки файлов с hello портала](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. Нажмите кнопку **отправить** Открытие hello пользовательский интерфейс для передачи файлов.

    ![Снимок экрана, показывающий, как tooupload файлы с портала hello](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a>Подключение toofile общей папки
-  Нажмите кнопку **Connect** для получения hello командной строки для монтажа hello общей папки из Windows и Linux. Для пользователей Linux можно также ссылаться слишком[как toouse хранилища Azure File с Linux](storage-how-to-use-files-linux.md) для получения дополнительных инструкций подключение для других дистрибутивах Linux.

    ![Снимок экрана, показывающий, каким образом toomount hello общей папки](media/storage-file-how-to-use-files-portal/use-files-portal-connect.png)
-  Можно скопировать hello команды для подключения файла делиться на Windows или Linux и запустите его из вы виртуальной Машины Azure или в локальной машины.

    ![Снимок экрана, показывающий команды присоединения hello для Windows и Linux](media/storage-file-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

**Подсказка.**  
Щелкните ключ доступа учетной записи хранения hello toofind для монтажа, **доступ для просмотра ключи для этой учетной записи хранения** внизу hello hello страница подключения.

## <a name="see-also"></a>См. также
Дополнительную информацию о хранилище файлов Azure см. по этим ссылкам.

* [Часто задаваемые вопросы](storage-files-faq.md)
* [Устранение неполадок](storage-troubleshoot-file-connection-problems.md)