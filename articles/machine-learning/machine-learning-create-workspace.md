---
title: "aaaCreate рабочей области машинного обучения | Документы Microsoft"
description: "Как toocreate в рабочую область для студии машинного обучения Azure"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: aa96b784-ac6c-44bc-a28a-85d49fbe90a2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye;bradsev;ahgyger
ms.openlocfilehash: 178293af222365993fade666124f34269d892325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-an-azure-machine-learning-workspace"></a>Создание рабочей области машинного обучения Azure и предоставление к ней общего доступа
Это меню связывает tootopics, которые описывают возможности tooset копирование hello различных средах обработки и анализа данных по использованию hello процесса Cortana аналитика (CAP).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

toouse студии машинного обучения Azure, необходимо toohave рабочей области машинного обучения. Эта рабочая область содержит hello средства toocreate, управлять и публиковать экспериментов.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="toocreate-a-workspace"></a>toocreate рабочей области
1. Войдите в toohello [портал Azure](https://portal.azure.com/)

    > [!NOTE]
    > toosign в и создать рабочую область, необходимо toobe администратора подписки Azure. 
    >
    > 

2. Щелкните **+Создать**.

3. Выберите **Аналитика**, щелкните **Рабочая область машинного обучения**, а затем — **Создать**.

4. Введите сведения о рабочей области.

    - Hello *имя рабочей области* может быть активным too260 символов, не заканчивается пробелом. Hello имя не может содержать следующие символы:`< > * % & : \ ? + /`
    - Hello *веб-службы план* вы выберите (или создайте), вместе с hello связанные *ценовой категории* выберите, используется при развертывании веб-служб из этой рабочей области.

    ![Создание рабочей области](media/machine-learning-create-workspace/create-new-workspace.png)

5. Нажмите кнопку **Создать**

После развертывания hello рабочей области, можно открыть его в студии машинного обучения.

1. Обзор tooMachine Studio обучения на [https://studio.azureml.net/](https://studio.azureml.net/).

2. Выберите рабочую область в верхнем правом углу hello.

    ![Выбор рабочей области](media/machine-learning-create-workspace/open-workspace.png)

3. Щелкните **my experiments** (Мои эксперименты).

    ![Открытие экспериментов](media/machine-learning-create-workspace/my-experiments.png)

Сведения об управлении рабочей областью см. в статье [Управление рабочей областью машинного обучения Azure](machine-learning-manage-workspace.md).
Если возникли проблемы при создании рабочей области в разделе [руководство по устранению неполадок: создать и присоединить рабочей области машинного обучения tooa](machine-learning-troubleshooting-creating-ml-workspace.md).


## <a name="sharing-an-azure-machine-learning-workspace"></a>Предоставление общего доступа к рабочей области машинного обучения Azure
После создания рабочей области машинного обучения, вы можете пригласить пользователей tooyour рабочей tooshare доступа tooyour рабочей области и все его экспериментов, наборы данных, портативные компьютеры, и т. д. Вы можете добавлять пользователей со следующими ролями:

* **Пользователь** -рабочей области пользователя можно создать, открывать, изменять и удалять экспериментов, наборы данных, т. д., в рабочей области hello.
* **Владелец** - владельца можно пригласить и удаление пользователей в рабочей области hello в toowhat Добавление пользователя можно сделать.

> [!NOTE]
> Hello учетной записи администратора, который создает hello рабочей toohello рабочей области автоматически добавляется в качестве владельца рабочей области. Тем не менее, другие Администраторы или пользователи в том, что подписки не являются автоматически предоставил доступ рабочей toohello: требуется tooinvite их явно.
> 
> 

### <a name="tooshare-a-workspace"></a>tooshare рабочей области

1. Войдите в tooMachine Studio обучения на [https://studio.azureml.net/Home](https://studio.azureml.net/Home)

2. Hello левой панели щелкните **параметры**

3. Нажмите кнопку hello **пользователей** вкладка

4. Нажмите кнопку **ПРИГЛАШЕНИЯ более пользователей** hello нижней части страницы приветствия

    ![Параметры Студии](media/machine-learning-create-workspace/settings.png)

5. Укажите один или несколько адресов электронной почты. Hello пользователям требуется допустимую учетную запись Майкрософт или учетная запись организации (из Azure Active Directory).

6. Выберите пользователей hello tooadd владельцем или пользователя.

7. Нажмите кнопку hello **ОК** кнопку с галочкой.

Каждый пользователь получит сообщение электронной почты с инструкциями совместным использованием toosign в toohello рабочей области.

> [!NOTE]
> Для возможности toodeploy toobe пользователей или управления веб-службами в этой рабочей области, они должны быть участника или администратора в hello подписки Azure. 



