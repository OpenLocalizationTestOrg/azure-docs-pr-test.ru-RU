---
title: "aaaLog в tooAzure из hello CLI | Документы Microsoft"
description: "Подключение tooyour подписки Azure из hello Azure командной строки (CLI Azure) для Mac, Linux и Windows"
editor: tysonn
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: ed856527-d75e-4e16-93fb-253dafad209d
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: rasquill
"\"/": 
ms.openlocfilehash: 42682c00c8dea78b2c624e640379716d1d4d7a2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="log-in-tooazure-from-hello-azure-cli"></a>Войдите в tooAzure из hello Azure CLI
Hello Azure CLI — это набор открытым исходным кодом, кросс платформенных команды для работы с ресурсами Azure. Этой статье описывается tooprovide различными способами hello вашей tooyour Azure CLI hello tooconnect учетные данные учетной записи Azure подписки Azure.

* Запустите hello `azure login` tooauthenticate команд CLI из Azure Active Directory. Это дает метод, можно получить доступ к командам tooCLI в обоих [команда режимы](#cli-command-modes). При выполнении команды hello без дополнительных параметров, `azure login` предложит toocontinue ведения журналов в интерактивном режиме веб-портале. Для дополнительных `azure login` параметров см. в разделе сценарии hello в этой статье, или тип `azure login --help`.
* Если требуется только toouse режим управления службами Azure CLI команд (не рекомендуется для наиболее новых развертываний), можно загрузить и установить файл параметров публикации на вашем компьютере.

Если вы еще не установили hello CLI, см. раздел [Install hello Azure CLI](cli-install-nodejs.md). Если у вас нет подписки Azure, то всего за несколько минут можно создать [бесплатную учетную запись](http://azure.microsoft.com/free/).

Основные сведения о различных удостоверениях учетной записи и подписках Azure см. в разделе [Как подписки Azure связаны с Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a name="scenario-1-azure-login-with-interactive-login"></a>Сценарий 1. Интерактивный вход в Azure
С определенным учетным записям hello CLI требуется toorun `azure login` и продолжите процесс входа в систему hello веб-браузера через веб-портал, этот процесс называется *интерактивного входа в систему*. Обычная причина — у вас есть рабочая или учебная учетная запись (также называется *учетную запись организации*), настроенная toorequire многофакторной проверки подлинности. Также используется интерактивный вход в систему с учетной записью Майкрософт команды режим toouse диспетчера ресурсов.

Интерактивный вход в систему можно легко: тип `azure login` — без параметров, как показано в следующий пример hello:

```
azure login
```                                                                                             

выходные данные Hello появится примерно hello следующим образом:

```         
info:    Executing command login
info:    toosign in, use a web browser tooopen hello page http://aka.ms/devicelogin. Enter hello code XXXXXXXXX tooauthenticate.
```
Скопируйте код hello, предлагаемых tooyou в выходных данных команды hello и откройте toohttp://aka.ms/devicelogin браузера или другие страницы, если указано. (Можно открыть браузер на hello же компьютере или на другом компьютере или устройстве.) Укажите код hello, а затем, запрашиваемые tooenter hello пользователя и пароль для удостоверения hello требуется toouse. После завершения этого процесса командной оболочки hello завершения входа hello. Это будет иметь следующий вид:

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> При интерактивном входе в систему проверка подлинности и авторизация выполняются с помощью Azure Active Directory. При использовании с удостоверением учетной записи Майкрософт, процесс входа в систему hello обращается к Azure Active Directory домена по умолчанию. (Если вы зарегистрировались для получения бесплатной учетной записи Azure, в Azure Active Directory создается домен по умолчанию для вашей учетной записи.)
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a>Сценарий 2. Вход в Azure с именем пользователя и паролем
Используйте hello `azure login` команду с именем пользователя hello (`-u`) параметр tooauthenticate toouse рабочую или учебную учетную запись, которая не требует многофакторной проверки подлинности. Появится hello командной строки для пароля hello (или при необходимости можно передать пароль hello как дополнительный параметр hello `azure login` команды). Hello следующий пример передает hello имя пользователя учетной записи организации:

    azure login -u myUserName@contoso.onmicrosoft.com

Вы получаете запрос tooenter пароль:

    info:    Executing command login
    Password: *********

завершает процесс входа в систему Hello.

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

Если это ваш первый время вход с помощью этих учетных данных, будет предложено tooverify обратиться toocache маркер проверки подлинности. Это предупреждение также возникает, если вы ранее использовали hello `azure logout` команда (описывается далее в статье hello). Запустите этот запрос для сценариев автоматизации toobypass `azure login` с hello `-q` параметра.

## <a name="scenario-3-azure-login-with-a-service-principal"></a>Сценарий 3. Вход в Azure с субъектом-службой
Если создание субъекта-службы для приложения Active Directory, а hello участника-службы имеет разрешения на свою подписку, воспользуйтесь hello `azure login` участника-службы hello tooauthenticate команды. В зависимости от вашего сценария можно предоставить учетные данные hello hello субъекта-службы как явные параметры hello `azure login` команды. Например hello следующая команда передает hello имя участника-службы и идентификатор клиента Active Directory:

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

Вы являетесь запрашиваемые tooprovide hello пароль. Можно предоставить учетные данные hello через интерфейс командной строки сценарий или приложение код или использовать субъекта-службы сертификатов tooauthenticate hello не в интерактивном режиме для сценариев автоматизации. Дополнительные сведения и примеры см. в статье [Проверка подлинности субъекта-службы в Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).

## <a name="scenario-4-use-a-publish-settings-file"></a>Сценарий 4. Использование файла параметров публикации
Если требуется только команды toouse hello управления службами Azure режиме CLI (например, toodeploy виртуальных машинах Azure в hello классической модели развертывания), можно подключиться с помощью файла параметров публикации. Этот метод устанавливает сертификат на локальном компьютере, который позволяет tooperform задачи управления для до тех пор, пока hello подписке и сертификате hello являются допустимыми.

* **файл параметров публикации toodownload hello** для вашей учетной записи убедитесь, что hello CLI находится в режиме управления службой, введя `azure config mode asm`. Затем выполните следующую команду hello:

        azure account download

Это открывает в браузере по умолчанию и предлагает toosign в toohello [классический портал Azure](https://manage.windowsazure.com). После входа в систему загрузится файл `.publishsettings` . Запишите место сохранения этого файла.

> [!NOTE]
> Если ваша учетная запись связана с несколькими клиентами Azure Active Directory, может быть tooselect запрос, который вы хотите toodownload параметры публикации Active Directory в файле.
>
>

После выбора с помощью страницы загрузки hello, или посетите hello классический портал Azure, hello выбранного Active Directory становится hello по умолчанию используется классический портал hello и страницы загрузки. После установки по умолчанию, вы видите текст hello "**tooreturn toohello на странице щелкните здесь**" вверху hello hello загрузки страницы. Используйте предоставляет ссылку tooreturn toohello выбора страницу приветствия.

* **файл параметров публикации tooimport hello**, запустите hello следующую команду:

        azure account import <path tooyour .publishsettings file>

> [!IMPORTANT]
> После импорта вашего параметры публикации, следует удалить hello `.publishsettings` файла. Он больше не требуется hello Azure CLI и представляет угрозу безопасности, как он может быть tooyour подписки используется toogain доступа.
>
>

## <a name="cli-command-modes"></a>Режимы команд CLI
Hello Azure CLI обеспечивает два режима команды для работы с ресурсами Azure, с различные наборы команд:

* **Режим диспетчера ресурсов** — для работы с ресурсами Azure в модель развертывания диспетчера ресурсов hello. tooset этот режим, выполните `azure config mode arm`.
* **Режим управления службами** — для работы с ресурсами Azure в hello классической модели развертывания. tooset этот режим, выполните `azure config mode asm`.

При первой установке hello в текущем выпуске hello CLI находится в режим диспетчера ресурсов.

> [!NOTE]
> Диспетчер ресурсов Hello и режим управления службами являются взаимоисключающими. То есть ресурсы, созданные в режиме не могут управляться из hello другим режимом.
>
>

## <a name="multiple-subscriptions"></a>Несколько подписок
Если у вас несколько подписок Azure, подключение tooAzure предоставляет доступ tooall подписок, связанных с учетными данными. Одна подписка по умолчанию hello и используемые hello Azure CLI, при выполнении операций. Можно просмотреть подписки hello, включая текущую подписку по умолчанию hello, с помощью hello `azure account list` команды. Эта команда возвращает аналогичные toohello следующие сведения:

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

В hello списка, hello **текущей** столбец показывает текущую подписку по умолчанию hello Azure-sub-1. Подписка по умолчанию hello toochange, используйте hello `azure account set` команду и укажите, нужно по умолчанию hello toobe подписки hello. Например:

    azure account set Azure-sub-2

При этом изменяется подписки по умолчанию hello tooAzure-sub-2.

> [!NOTE]
> Изменение подписки по умолчанию hello вступает в силу немедленно и глобальных изменений; новые команды Azure CLI, выполняются ли они от hello же экземпляр командной строки или в другом экземпляре, использовать новую подписку по умолчанию hello.
>
>

Если вы хотите toouse подписки не по умолчанию с hello Azure CLI, но не текущего значения по умолчанию toochange hello, можно использовать hello `--subscription` для команды hello и укажите имя hello hello подписки нужно toouse для операции hello.

После tooyour подключенных подписка Azure, можно запустить с помощью команды toowork hello Azure CLI с ресурсами Azure.

## <a name="storage-of-cli-settings"></a>Хранение параметров CLI
Ли войти hello `azure login` команды или импорт параметров публикации, профиль CLI и журналы хранятся в `.azure` каталог расположен в вашей `user` каталога. Каталог `user` защищен операционной системой. Тем не менее, рекомендуется выполнить дополнительные шаги tooencrypt вашей `user` каталога. Это можно сделать в hello следующих способов:

* В Windows измените свойства directory hello или с помощью BitLocker.
* На Mac включите FileVault hello каталога.
* В Ubuntu — команду используйте функцию каталог Encrypted домашней hello. Другие дистрибутивы Linux включают аналогичные функции.

## <a name="logging-out"></a>Выход из системы
toolog out hello используйте следующую команду:

    azure logout -u <username>

Если hello подписки, связанные с учетной записи hello только проверка подлинности выполняется с Active Directory, ведение журнала операции удаления сведений подписки hello из hello локальный профиль. Тем не менее если файл параметров публикации также был импортирован hello подписок, выход только для удаления Active Directory сведений о связанных с локальным профилем hello.

## <a name="next-steps"></a>Дальнейшие действия
* команды toouse Azure CLI, см. [команды Azure CLI в режим диспетчера ресурсов](virtual-machines/azure-cli-arm-commands.md) и [Azure CLI команд в режиме управления службой](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).
* toolearn Дополнительные сведения о hello Azure CLI Загрузка исходного кода, сообщения о проблемах, или передавать toohello проекта см. hello [репозиторий GitHub для hello Azure CLI](https://github.com/azure/azure-xplat-cli).
* Если возникли проблемы при использовании hello Azure CLI или Azure, посетите hello [форумы Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).
