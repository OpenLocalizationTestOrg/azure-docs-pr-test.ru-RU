---
title: "aaaConfigure проверку подлинности с помощью Amazon Web Services | Документы Microsoft"
description: "В этой статье описывается как toocreate и проверки учетных данных для модулей Runbook в автоматизации Azure, управление ресурсами AWS AWS."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: "проверка подлинности aws, настройка aws"
ms.assetid: b6dde4bb-26ac-4876-9aa9-e586bed30d6b
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/11/2016
ms.author: magoedte
ms.openlocfilehash: 6edaa000c1b206d80fe64b18c729dac124849070
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-amazon-web-services"></a>Проверка подлинности модулей Runbook с помощью Amazon Web Services
Автоматизацию стандартных задач с использованием ресурсов в Amazon Web Services (AWS) можно выполнить с помощью модулей Runbook службы автоматизации в Azure.  Многие задачи можно автоматизировать в AWS с помощью модулей Runbook службы автоматизации так же, как и с помощью ресурсов в Azure.  Для этого нужны всего две вещи.

* Подписка на AWS и набор учетных данных, а именно — ключ доступа к AWS и секретный ключ.  Дополнительные сведения см.  Дополнительные сведения см. в статье hello статьи [с помощью учетных данных AWS](http://docs.aws.amazon.com/powershell/latest/userguide/specifying-your-aws-credentials.html).
* Подписка Azure и учетная запись службы автоматизации.  Дополнительные сведения о настройке учетной записи службы автоматизации Azure просмотрите статью hello [Настройка Azure учетная запись запуска от имени](automation-sec-configure-azure-runas-account.md).  

tooauthenticate с AWS, необходимо указать набор учетных данных tooauthenticate AWS под управлением службы автоматизации Azure модули Runbook. Если уже имеется учетная запись службы автоматизации создан и требуется toouse, tooauthenticate с AWS, можно выполнить действия hello в следующем разделе hello.  Если требуется toodedicated учетную запись для модулей Runbook для различных версий AWS ресурсов, необходимо сначала создать новый [автоматизации Запуск от имени учетной записи](automation-sec-configure-azure-runas-account.md) (пропустите параметр hello toocreate субъекта-службы) и затем выполните следующие шаги hello.

## <a name="configure-automation-account"></a>Настройка учетной записи службы автоматизации
Для автоматизации Azure toocommunicate с AWS будет необходимо tooretrieve AWS учетные данные и сохранять их в качестве ресурсов в службе автоматизации Azure.  Выполните следующие действия, описанные в документе AWS hello hello [управление ключи доступа для учетной записи AWS](http://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html) toocreate ключ доступа и скопируйте hello **кода доступа** и **секретный ключ доступа** (при необходимости загрузить ваш файл ключа toostore его в безопасном месте).

После создания и копирования AWS ключей безопасности, необходимо будет toocreate актива учетных данных с помощью учетной записи службы автоматизации Azure toosecurely их хранения и ссылаться на них с помощью модулей Runbook.  Выполните действия hello в разделе "hello" **Создание нового актива учетных данных** в hello [учетных данных средств автоматизации Azure](automation-credentials.md) статью и введите hello следующую информацию:

1. В hello **имя** введите **AWScred** или после именования стандартов соответствующее значение.  
2. В hello **имя пользователя** введите ваш **идентификатор доступа** и **секретный ключ доступа** в hello **пароль** и **подтверждение пароль** поле.   

## <a name="next-steps"></a>Дальнейшие действия
* Просмотреть hello решения статьи [автоматизации развертывания виртуальной машины в Amazon Web Services](automation-scenario-aws-deployment.md) toolearn выполнение задач tooautomate toocreate модулей Runbook на AWS.

