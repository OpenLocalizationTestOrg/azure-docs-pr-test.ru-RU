---
title: "Клиент Azure Active Directory aaaChange hello в Azure RemoteApp | Документы Microsoft"
description: "Узнайте, как клиент Azure Active Directory hello toochange связан с Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 20faf169-6e48-428a-8bdd-f231daff19fa
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d0928b099b7fcfb3ab16077e295d7aaf519c3653
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-azure-active-directory-tenant-in-azure-remoteapp"></a>Изменение клиента Azure Active Directory hello в Azure RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Azure RemoteApp использует Azure Active Directory (Azure AD) tooallow пользователю доступ. Клиент Hello только в Azure AD, который можно использовать в Azure RemoteApp — hello, связанную с hello подписки Azure. Вы можете просмотреть связанные hello подписки на hello **параметры** портале hello. Рассмотрим hello **каталога** столбца на hello **подписки** вкладки.

> [!NOTE]
> Для этого toosucceed изменение сначала удалите всех пользователей из существующего клиента Azure Active Directory hello из всех коллекций Azure RemoteApp. toodo это, откройте toohello портал Azure, откройте toohello **Azure RemoteApp** и откройте каждой коллекции Azure RemoteApp. Go toohello **пользователей** вкладку и удалять пользователей, принадлежащих текущему клиенту Azure Active Directory tooyour. Повторите эту операцию для всех существующих коллекций Azure RemoteApp. Без таким образом, нельзя будет toocreate или исправление для коллекции.
> 
> 

Toouse другой клиент, используйте эти ассоциации hello действия toochange для вашей подписки:

1. Hello портале удалите любые toowhich пользователей Azure AD вы предоставили доступ tooAzure коллекции RemoteApp. (См. Примечание hello выше пошаговые инструкции о том, как toodo это.)
2. Задайте учетную запись Майкрософт (ранее называвшиеся Live ID) в качестве администратора службы hello. (Не знаете, уже являются Здравствуйте, администратор службы? Это можно узнать, выбрав **Параметры -> Администраторы**.) А вот как вы можете изменить это:
   
   1. Выберите пользователя hello в правом верхнем углу приветствия и нажмите кнопку **просмотреть Мой счет**.
   2. Щелкните подписку hello. На новую страницу приветствия, прокрутите список вниз и нажмите кнопку **изменить сведения о подписке** в правом hello. (Hello посередине в нижней части справа, если что-то поможет вам найти его.)
   3. Введите учетную запись Майкрософт hello для hello пользователя, который должен быть администратором hello службы.
3. Теперь выйти из портала hello и снова войдите, используя учетную запись Майкрософт, указанных в предыдущем шаге hello hello.
4. Щелкните **Создать > Службы приложений > Active Directory > Каталог > Настраиваемое создание**.
5. В разделе **Каталог** выберите **Использовать существующий каталог**. Мы будем toohave toosign из портала hello, теперь это необходимо **я готов toobe выходу из системы**.
6. Знак обратно в hello портала как глобальный администратор каталога hello tooadd требуется. (Если ранее вы не являлись глобальным администратором, то стали им после выхода и повторного входа в систему.)
7. У пользователя запрашивается при входе в, если требуется toouse к существующему клиенту AD с вашей подпиской. Щелкните **Продолжить**, а затем выберите **Выйти сейчас**.
8. Снова выполнить вход и вернитесь слишком**параметры -> подписки**. Выберите свою подписку и щелкните **Изменить каталог**. Выберите требуемый toouse клиента hello Azure AD.

Теперь можно использовать новый Azure AD hello клиента toocontrol доступа toohello Azure подписки и tooconfigure доступа пользователей в Azure RemoteApp.

