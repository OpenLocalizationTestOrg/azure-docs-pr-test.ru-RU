---
title: "Хранилище ключей Azure с использованием интерфейса CLI aaaManage | Документы Microsoft"
description: "Использование этого учебника tooautomate типичных задач в хранилище ключей с помощью hello CLI"
services: key-vault
documentationcenter: 
author: BrucePerlerMS
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 66be6e44-684a-411b-802e-884628458ae7
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: bruceper
ms.openlocfilehash: 9ef506faa67e1f0db5b9e303300d63b135ddd7b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli"></a>Управление хранилищем ключей с помощью CLI

Хранилище ключей Azure доступно в большинстве регионов. Дополнительные сведения см. в разделе hello [страница цен в хранилище ключей](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Введение

Использовать этот учебник toohelp, вы получаете работы с хранилищем ключей Azure toocreate жесткой контейнера (хранилище) в Azure, toostore и управлять ими, криптографические ключи и секретные данные в Azure. Помогает выполнить процесс с помощью интерфейса командной строки Azure кросс-платформенных toocreate hello хранилище, в котором содержится ключ или пароль, который затем можно использовать вместе с приложением Azure. В нем также показано, как приложение может использовать этот ключ или пароль в дальнейшем.

**Предполагаемое время toocomplete:** 20 минут

> [!NOTE]
> Этот учебник включает инструкции о том, как toowrite hello приложения Azure, в котором один из шагов hello, показывающий, как tooauthorize приложения toouse ключа или секрета в ключе hello хранилище.
> 
> В настоящее время вы не можете настроить хранилище ключей Azure hello портал Azure. Вместо этого воспользуйтесь этими инструкциями по кроссплатформенному интерфейсу командной строки Azure. Инструкции по Azure PowerShell см. в [этом руководстве](key-vault-get-started.md).
> 
> 

Общие сведения о хранилище ключей Azure см. в статье [Что такое хранилище ключей Azure?](key-vault-whatis.md)

## <a name="prerequisites"></a>Предварительные требования

toocomplete этого учебника необходимо иметь следующие hello:

* TooMicrosoft подписки Azure. Если у вас нет подписки, вы можете зарегистрироваться для использования [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial);
* Интерфейс командной строки версии 0.9.1 или более поздней. tooinstall hello последнюю версию и подключите tooyour подписки Azure в разделе [Установка и настройка hello Azure межплатформенного интерфейса командной строки](../cli-install-nodejs.md).
* Приложение, настроенное toouse hello ключ или пароль, который создан в этом учебнике. Образец приложения доступно из hello [центра загрузки Майкрософт](http://www.microsoft.com/download/details.aspx?id=45343). Инструкции см. в файле Readme, сопровождающие hello.

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a>Справка по межплатформенному интерфейсу командной строки Azure

В этом учебнике предполагается, что вы знакомы с интерфейсом командной строки hello (Bash, терминалов, Командная строка)

Hello--справки или -h параметр можно использовать tooview справки для определенных команд. Кроме того hello azure help [команда] [параметры] формата также можно использовать tooreturn hello одинаковые сведения. Например, hello следующие команды возвращают все hello одинаковые сведения:

    azure account set --help

    azure account set -h

    azure help account set

В случае сомнений о hello параметров, используемых в команде ссылаться с помощью toohelp--справки, -h или azure help [команда].

Также можно прочитать следующие учебники tooget знакомы с помощью диспетчера ресурсов Azure в интерфейс командной строки Azure кросс-платформенных hello.

* [Как tooinstall и настройка Azure кросс-платформенных командной строки](../cli-install-nodejs.md)
* [Использование межплатформенного интерфейса командной строки Azure совместно с диспетчером ресурсов](../xplat-cli-azure-resource-manager.md)

## <a name="connect-tooyour-subscriptions"></a>Подключение tooyour подписки

toolog с помощью учетной записи организации, hello используйте следующую команду:

    azure login -u username -p password

или если требуется toolog в интерактивном режиме введите

    azure login

> [!NOTE]
> метод входа Hello работает только с учетной записью организации. Учетная запись организации — это пользователь, который управляется вашей организацией и определен в клиенте Azure Active Directory организации.
> 
> 

Если в настоящее время не имеют учетной записи организации и используется учетная запись Майкрософт toolog в tooyour подписки Azure, можно легко создать ее, используя hello следующие действия.

1. Toohello входа toohello входа [портала управления Azure](https://manage.windowsazure.com/)и нажмите кнопку на основе Active Directory.
2. Если каталог не существует, выберите создать каталог и предоставьте hello затребовал информацию.
3. Выберите каталог и добавьте нового пользователя. Этот пользователь будет представлять учетную запись организации. Во время создания hello hello пользователя будут предоставляться с адресом электронной почты для пользователя hello и временный пароль. Эти данные используются на следующем шаге. Сохраните их.
4. Из портала hello выберите параметры, а затем выберите администраторов. Выберите Добавить и добавить нового пользователя hello в качестве соадминистратора. Это позволяет учетной записи организации toomanage hello подписки Azure.
5. Наконец, выйдите из hello портал Azure и затем войдите снова с помощью учетной записи организации новый hello. Если это hello первый раз вход с помощью этой учетной записи, будет использоваться пароля hello toochange запрос.

Дополнительные сведения об использовании рабочей учетной записи в Microsoft Azure см. в статье [Подпишитесь на Azure как организация](../active-directory/sign-up-organization.md).

Если есть несколько подписок и требуется toospecify конкретных один toouse для хранилища ключей Azure, введите hello, следуя toosee hello подписки для учетной записи:

    azure account list

Затем toospecify hello подписки toouse, тип:

    azure account set <subscription name>

Дополнительные сведения о настройке Azure межплатформенного интерфейса командной строки см. в разделе [как tooInstall и настройка интерфейса командной строки Azure кросс-платформенных](../cli-install-nodejs.md).

## <a name="switch-toousing-azure-resource-manager"></a>Переключение toousing диспетчера ресурсов Azure
Hello хранилище ключей требуется диспетчер ресурсов Azure, поэтому введите следующий режим диспетчера ресурсов tooAzure tooswitch hello:

    azure config mode arm

## <a name="create-a-new-resource-group"></a>Создание новой группы ресурсов
При использовании диспетчера ресурсов Azure все связанные ресурсы создаются внутри группы ресурсов. Для примера мы создадим новую группу ресурсов с именем ContosoResourceGroup:

    azure group create 'ContosoResourceGroup' 'East Asia'

Hello первым параметром является имя группы ресурсов, если второй параметр hello расположение hello. Для расположения, используйте команду hello `azure location list` tooidentify как toospecify альтернативное расположение toohello один в этом примере. Если вам необходима дополнительная информация, введите `azure help location`

## <a name="register-hello-key-vault-resource-provider"></a>Регистрация поставщика ресурсов хранилища ключей hello
Убедитесь, что поставщик ресурсов хранилища ключей зарегистрирован в вашей подписке:

`azure provider register Microsoft.KeyVault`

Это достаточно выполнить один раз для каждой подписки toobe.

## <a name="create-a-key-vault"></a>Создайте хранилище ключей.

Используйте hello `azure keyvault create` toocreate команда хранилища ключей. Этот сценарий имеет три обязательных параметра: имя группы ресурсов, имя хранилища ключей и географическое расположение hello.

Например если вы используете hello хранилище с именем ContosoKeyVault hello группу ресурсов с именем ContosoResourceGroup и расположение hello Восточная Азия, введите:

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

выходные данные этой команды Hello отображает свойства hello хранилища ключей, который вы только что создали. Hello двух наиболее важных свойств:

* **Имя**: пример hello это ContosoKeyVault. Вы будете использовать это имя для выполнения других командлетов хранилища ключей;
* **vaultUri**: пример hello это https://contosokeyvault.vault.azure.net. Необходимо, чтобы приложения, использующие ваше хранилище через REST API, использовали этот URI.

Учетная запись Azure — теперь авторизованным tooperform все операции в этот ключ в хранилище. Пока что это недоступно для других учетных записей.

## <a name="add-a-key-or-secret-toohello-key-vault"></a>Добавление ключа или секрета toohello хранилища ключей

Хранилище ключей Azure toocreate программно защищенного ключа для вас, используйте hello `azure key create` команд и введите hello ниже:

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

Тем не менее при наличии существующего ключа в PEM-файл сохранен как локальный файл в файл с именем softkey.pem, что требуется tooupload tooAzure хранилище ключей, введите следующую tooimport hello ключ из hello hello. PEM-файла, который защищает hello с помощью программного обеспечения в hello службы хранилища ключей:

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

Теперь можно ссылаться на ключ hello, созданные или переданные tooAzure хранилище ключей с помощью URI-адрес. Используйте **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways получения текущей версии hello и **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget этой конкретной версии.

tooadd секретный toohello хранилища, которой это пароль SQLPassword с именем и значением hello Pa$ $w0rd tooAzure хранилище ключей, тип hello следующие:

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

Теперь можно ссылаться на этот пароль добавили tooAzure хранилище ключей с помощью URI-адрес. Используйте **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways получения текущей версии hello и **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget этой конкретной версии.

Позволяет просмотреть hello ключа или секрета, который вы только что создали:

* tooview вашей, введите:`azure keyvault key list --vault-name 'ContosoKeyVault'`
* tooview в тайне, тип:`azure keyvault secret list --vault-name 'ContosoKeyVault'`

## <a name="register-an-application-with-azure-active-directory"></a>Зарегистрируйте приложение с Azure Active Directory.

Обычно этот шаг выполняет разработчик на отдельном компьютере. Он не является tooAzure конкретного хранилища ключей, но указан, для обеспечения полноты.

> [!IMPORTANT]
> Учебник toocomplete hello, учетная запись, хранилище hello и приложения hello, которое будет зарегистрирован на этом шаге необходимо в hello один каталог Azure.
> 
> 

Приложения, которые используют хранилища ключей, должны пройти аутентификацию с использованием токена Azure Active Directory. toodo, hello владелец приложения hello сначала необходимо зарегистрировать приложение hello в своем Azure Active Directory. В конце hello регистрации владелец приложения hello возвращает hello следующие значения:

* **Идентификатор приложения** (также известный как идентификатор клиента) и **ключ проверки подлинности** (также известный как общий секрет hello). приложение Hello должен представить оба этих значения tooAzure Active Directory, tooget маркер. Как приложение hello настраивается toodo это зависит от приложения hello. Для hello образец приложения хранилища ключей владелец приложения hello устанавливает эти значения в файле app.config hello.

приложение hello tooregister в Azure Active Directory:

1. Войдите в систему toohello портал Azure.
2. В левой части экрана приветствия щелкните **Active Directory**и выберите каталог hello, в котором будет зарегистрировать приложение. <br> <br> 

>[!NOTE] 
> Необходимо выбрать hello каталоге, содержащем hello подписки Azure, в которой для создания хранилища ключей. Если вы не знаете, какой каталог это, нажмите кнопку **параметры**идентификации hello подписки, в которой для создания хранилища ключей и Примечание hello hello directory название hello последнего столбца.

3. Щелкните **ПРИЛОЖЕНИЯ**. Если приложения не были добавлены tooyour каталога, эта страница отобразит только hello **добавить приложение** ссылку. Щелкните ссылку hello, или в качестве альтернативы можно щелкнуть hello **добавить** на панели команд hello.
4. В hello **добавить приложение** мастера hello **что вам требуется toodo?** щелкните **добавить приложение, разрабатываемое моей организацией**.
5. На hello **Расскажите о своем приложении** укажите имя для вашего приложения и выберите **веб-приложение и/или WEB API** (по умолчанию hello). Щелкните значок "следующий" hello.
6. На hello **свойства приложения** укажите hello **URL-адрес входа** и **URI идентификатора приложения** для веб-приложения. Если в вашем приложении нет этих значений, можно придумать их для этого шага (например, можно указать http://test1.contoso.com в обоих полях). Не важно, эти веб-сайты, если существует. Важно то, что URI идентификатора приложения hello для каждого приложения отличается для каждого приложения в каталоге. каталог Hello используется этой строки tooidentify приложений.
7. Щелкните значок завершения toosave hello изменения в мастере hello.
8. На странице быстрого запуска приветствия щелкните **Настройка**.
9. Прокрутите toohello **ключей** выберите длительность hello и нажмите кнопку **Сохранить**. Страница приветствия обновляется и теперь отображается значение ключа. Необходимо настроить приложение с таким значением ключа и hello **идентификатор КЛИЕНТА** значение. (указания по этой конфигурации зависят от конкретного приложения).
10. На этой странице, который будет использоваться в hello следующий шаг tooset разрешения на ваше хранилище, скопируйте значение идентификатора клиента hello.

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a>Авторизовать hello приложения toouse hello ключа или секрета
tooaccess приложения hello tooauthorize hello ключа или секрета в хранилище hello, используйте hello `azure keyvault set-policy` команды.

Например если имя хранилища — ContosoKeyVault и hello приложения требуется tooauthorize имеет идентификатор клиента 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, и вы хотите toodecrypt приложения hello tooauthorize и войдите с ключами в хранилище, а затем запустите hello следующие:

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> При запуске в командной строке Windows следует замените одинарные и двойные кавычки и также escape-hello внутренней двойные кавычки. Например: "[\"decrypt\",\"sign\"]".
> 
> 

Tooauthorize этой же tooread секреты приложения в хранилище, выполните следующие hello:

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a>Если требуется, чтобы toouse аппаратный модуль безопасности (HSM)
Для повышения надежности можно импортировать или создавать ключи в аппаратных модулях безопасности (HSM), никогда не покидают границ HSM hello. Hello аппаратные модули безопасности являются FIPS 140-2 уровня 2 проверки. Если это требование не распространяется tooyou, пропустите этот раздел и перейдите слишком[удалить hello хранилища ключей и связанные ключи и секретные данные](#delete-the-key-vault-and-associated-keys-and-secrets).

toocreate этих ключей, защищенных HSM, необходимо иметь подписку хранилища, который поддерживает ключей, защищенных HSM.

При создании hello keyvault, добавьте параметр «Конфигурация» hello:

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

Можно добавить программно защищенных ключей (как показано выше) и хранилище ключей, защищенных HSM toothis. toocreate Перенос аппаратно защищенного ключа набора hello назначения параметра too'HSM ":

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

Можно использовать следующую команду tooimport ключа из PEM-файл на компьютере hello. Эта команда импортирует ключ hello в аппаратные модули безопасности в hello службы хранилища ключей:

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

Hello следующая команда импортирует «принеси свой собственный ключ» (BYOK) пакета. Это дает возможность создания ключа в ваш локальный HSM и передачи tooHSMs в hello службы хранилища ключей без ключа hello, оставляя границ HSM hello:

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

Более подробные инструкции о том, как toogenerate этот пакет BYOK разделе [как toouse HSM-Protected ключи с хранилищем ключей Azure](key-vault-hsm-protected-keys.md).

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a>Удаление хранилища ключей hello и связанные ключи и секретные данные
Если вы больше не нужна hello хранилища ключей и hello ключа или секрета, который его содержит, hello хранилища ключей можно удалить с помощью команды delete keyvault hello azure:

    azure keyvault delete --vault-name 'ContosoKeyVault'

Или можно удалить группы весь ресурс Azure, которая включает в себя хранилище ключей hello и другие ресурсы, которые включены в эту группу:

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a>Другие команды в межплатформенном интерфейсе командной строки Azure
Вот другие команды, которые могут быть полезны при управлении хранилищем ключей Azure.

Эта команда перечисляет все ключи и выбранные свойства в виде таблицы:

    azure keyvault key list --vault-name 'ContosoKeyVault'

Эта команда отображает полный список свойств для указанного ключа hello:

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

Эта команда перечисляет все имена секретов и выбранные свойства в виде таблицы:

    azure keyvault secret list --vault-name 'ContosoKeyVault'

Ниже приведен пример того, как tooremove определенного ключа:

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

Ниже приведен пример того, как tooremove конкретных секрет:

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a>Дальнейшие действия
Программирование ссылки, в разделе [hello хранилище ключей Azure в руководстве разработчика](key-vault-developers-guide.md).

