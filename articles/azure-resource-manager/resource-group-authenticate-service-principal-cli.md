---
title: "aaaCreate удостоверение для приложения Azure с помощью Azure CLI | Документы Microsoft"
description: "Описание управления toocreate Azure CLI toouse приложение Azure Active Directory и участника-службы, а также предоставляет доступ к tooresources посредством доступа на основе ролей. Здесь показано, как tooauthenticate приложения с помощью пароля или сертификата."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c224a189-dd28-4801-b3e3-26991b0eb24d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 0d693ec801d4f4d6c24ec420580776e73014b325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-cli-toocreate-a-service-principal-tooaccess-resources"></a>Используйте основной tooaccess ресурсов службы toocreate Azure CLI

При наличии приложения или скрипт, который необходимо tooaccess ресурсов, можно установить удостоверение для приложения hello и проверки подлинности приложения hello в свои собственные учетные данные. Этот идентификатор известен как субъект-служба. Такой подход позволяет выполнить следующие действия:

* Назначение разрешений удостоверение приложения toohello, отличаются от собственных разрешений. Как правило эти разрешения являются ограниченными tooexactly какие hello приложению toodo.
* Использовать сертификат для аутентификации при выполнении автоматического сценария.

В этой статье показано, как toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset копирование toorun приложения под свои собственные учетные данные и удостоверений. Установить hello последнюю версию [Azure CLI 1.0](../cli-install-nodejs.md) toomake должен соответствовать среды hello примеры в этой статье.

## <a name="required-permissions"></a>Необходимые разрешения
toocomplete в этом разделе, необходимо иметь достаточные разрешения в Azure Active Directory и вашей подписке Azure. В частности необходимо быть может toocreate приложение в Azure Active Directory hello и назначить роль участника tooa hello службы. 

Hello ли ваша учетная запись имеет достаточные разрешения — с помощью портала hello простой toocheck способом. Ознакомьтесь с [проверкой наличия необходимых разрешений на портале](resource-group-create-service-principal-portal.md#required-permissions).

Теперь, либо продолжить tooa раздел [пароль](#create-service-principal-with-password) или [сертификат](#create-service-principal-with-certificate) проверки подлинности.

## <a name="create-service-principal-with-password"></a>Создание субъекта-службы с использованием пароля
В этом разделе выполняется hello toocreate hello действия приложения AD с помощью пароля и назначить участника службы toohello роль модуля чтения hello.

1. Войдите в учетную запись tooyour.
   
   ```azurecli
   azure login
   ```
2. toocreate удостоверение приложения укажите приложение hello hello имя и пароль, как показано в hello следующую команду:
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   возвращается Hello нового субъекта-службы. При предоставлении разрешений требуется Hello объекта с идентификатором. требуется guid Hello hello имена участника-службы в списке при входе в систему. Этот идентификатор guid — hello совпадает со значением идентификатора приложения hello. В примерах приложений hello, это значение является ссылка tooas hello `Client ID`. 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating application exampleapp
     / Creating service principal for application 7132aca4-1bdb-4238-ad81-996ff91d8db+
     data:    Object Id:               ff863613-e5e2-4a6b-af07-fff6f2de3f4e
     data:    Display Name:            exampleapp
     data:    Service Principal Names:
     data:                             7132aca4-1bdb-4238-ad81-996ff91d8db4
     data:                             https://www.contoso.org/example
     info:    ad sp create command OK
   ```

3. Предоставить разрешения участника службы hello в вашей подписке. В этом примере добавляется hello службы основной toohello чтения роль, которая предоставляет разрешение tooread все ресурсы в подписке hello. Сведения о других ролях см. в статье [RBAC: встроенные роли](../active-directory/role-based-access-built-in-roles.md). Параметр objectid hello укажите идентификатор объекта, который использовался при создании приложения hello hello. Перед выполнением этой команды, необходимо разрешить некоторое время для hello новой службы основной toopropagate во всей Azure Active Directory. При выполнении этих команд вручную между задачами обычно проходит достаточно времени. В сценарии, следует добавить шаг toosleep между командами hello (например `sleep 15`). Если вы увидите, что ошибка сообщение о hello участника не существует в каталоге hello, повторно запустите команду hello.
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
Вот и все! Приложение AD и субъект-служба настроены. Hello следующем разделе показано, как toolog вход с помощью hello учетных данных через Azure CLI. Если требуется учетных данных toouse hello в код приложения, не обязательно toocontinue с этим разделом. Можно легко toohello [образцы приложений](#sample-applications) примеры вход с помощью идентификатора приложения и пароль. 

### <a name="provide-credentials-through-azure-cli"></a>Предоставление учетных данных через Azure CLI
Теперь требуется toolog в качестве операции tooperform приложения hello.

1. При каждом входе в качестве участника-службы для приложения AD необходимо ИД клиента hello tooprovide hello каталога. Клиент — это экземпляр Azure Active Directory. ИД клиента hello tooretrieve для прошедшего подписки, используйте:
   
   ```azurecli
   azure account show
   ```
   
   Возвращаемые данные:
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     Если вам требуется идентификатор клиента hello tooget другую подписку, используйте hello следующую команду:
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. Toouse идентификатор клиента hello tooretrieve для входа, используйте:
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     toouse значение Hello для входа является hello код guid, указанный в приветствия имен участников-служб.
   
   ```azurecli
   [
     {
       "objectId": "ff863613-e5e2-4a6b-af07-fff6f2de3f4e",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "7132aca4-1bdb-4238-ad81-996ff91d8db4",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "7132aca4-1bdb-4238-ad81-996ff91d8db4"
       ]
     }
   ]
   ```
3. Войдите в систему как участник службы hello.
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    Запрашивается пароль hello. Укажите пароль hello, указанные при создании приложения hello AD.
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

Теперь вы прошли проверку подлинности как субъект-службу hello для hello участника-службы, вы создали.

Кроме того могут вызывать операции REST из toolog Командная строка hello в. Из hello ответ проверки подлинности можно получить маркер доступа hello для использования с другими операциями. Пример получения токена доступа hello путем вызова операции REST см. в разделе [создания токена доступа](resource-manager-rest-api.md#generating-an-access-token).

## <a name="create-service-principal-with-certificate"></a>Создание субъекта-службы с использованием сертификата
В этом разделе необходимо выполнить действия hello для.

* создать самозаверяющий сертификат;
* Создайте hello приложения AD сертификат hello и hello участника-службы
* назначить участника службы toohello роль модуля чтения hello

toocomplete следующие действия, необходимо иметь [OpenSSL](http://www.openssl.org/) установлен.

1. Создать самозаверяющий сертификат.
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. Здравствуйте, предшествующий шаг создания двух файлов - privkey.pem и cert.pem. Открытый и закрытый ключи hello объединить в один файл.

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. Откройте hello **examplecert.pem** файл и выполните поиск hello длинную последовательность символов между **---BEGIN CERTIFICATE---** и **---конечный СЕРТИФИКАТ---**. Скопируйте данные сертификата hello. Эти данные можно передать как параметр при создании hello участника-службы.

4. Войдите в учетную запись tooyour.

   ```azurecli
   azure login
   ```
5. участника-службы toocreate hello, укажите имя hello приложение hello и данные сертификата hello, как показано в hello следующую команду:
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   возвращается Hello нового субъекта-службы. При предоставлении разрешений требуется Hello объекта с идентификатором. требуется guid Hello hello имена участника-службы в списке при входе в систему. Этот идентификатор guid — hello совпадает со значением идентификатора приложения hello. В примерах приложений hello это значение является ссылка tooas hello идентификатор клиента. 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating service principal for application 4fd39843-c338-417d-b549-a545f584a74+
     data:    Object Id:        7dbc8265-51ed-4038-8e13-31948c7f4ce7
     data:    Display Name:     exampleapp
     data:    Service Principal Names:
     data:                      4fd39843-c338-417d-b549-a545f584a745
     data:                      https://www.contoso.org/example
     info:    ad sp create command OK
   ```
6. Предоставить разрешения участника службы hello в вашей подписке. В этом примере добавляется hello службы основной toohello чтения роль, которая предоставляет разрешение tooread все ресурсы в подписке hello. Сведения о других ролях см. в статье [RBAC: встроенные роли](../active-directory/role-based-access-built-in-roles.md). Параметр objectid hello укажите идентификатор объекта, который использовался при создании приложения hello hello. Перед выполнением этой команды, необходимо разрешить некоторое время для hello новой службы основной toopropagate во всей Azure Active Directory. При выполнении этих команд вручную между задачами обычно проходит достаточно времени. В сценарии, следует добавить шаг toosleep между командами hello (например `sleep 15`). Если вы увидите, что ошибка сообщение о hello участника не существует в каталоге hello, повторно запустите команду hello.
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a>Предоставление сертификата с помощью автоматизированного сценария для интерфейса командной строки Azure
Теперь требуется toolog в качестве операции tooperform приложения hello.

1. При каждом входе в качестве участника-службы для приложения AD необходимо ИД клиента hello tooprovide hello каталога. Клиент — это экземпляр Azure Active Directory. ИД клиента hello tooretrieve для прошедшего подписки, используйте:
   
   ```azurecli
   azure account show
   ```
   
   Возвращаемые данные:
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   Если вам требуется идентификатор клиента hello tooget другую подписку, используйте hello следующую команду:
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. tooretrieve hello отпечаток сертификата и удалите ненужные символы, используйте:
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   Возвращается значение отпечатка следующего вида:
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. Toouse идентификатор клиента hello tooretrieve для входа, используйте:
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   toouse значение Hello для входа является hello код guid, указанный в приветствия имен участников-служб.
     
   ```azurecli
   [
     {
       "objectId": "7dbc8265-51ed-4038-8e13-31948c7f4ce7",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "4fd39843-c338-417d-b549-a545f584a745",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "4fd39843-c338-417d-b549-a545f584a745"
       ]
     }
   ]
   ```
4. Войдите в систему как участник службы hello.
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

Теперь вы прошли проверку подлинности как hello субъекта-службы для hello созданное приложение Azure Active Directory.

## <a name="change-credentials"></a>Изменение учетных данных

использовать учетные данные hello toochange для приложения AD, либо из-за нарушение безопасности или истечения срока действия учетных данных, `azure ad app set`.

Используйте toochange пароль:

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

Используйте toochange значение сертификата:

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a>Отладка

Возможны следующие ошибки при создании участника службы hello.

* **«Authentication_Unauthorized»** или **«подписка не найден в контексте hello».** -Эта ошибка появляется, когда ваша учетная запись не имеет hello [разрешения, необходимые](#required-permissions) на hello Azure Active Directory tooregister приложения. Как правило, эта ошибка возникает в тех случаях, когда регистрировать приложения в Azure Active Directory могут только администраторы, а ваша учетная запись не является административной. Попросите вашего администратора tooeither назначить вы tooan роль администратора или tooenable пользователей tooregister приложений.

* Ваша учетная запись **«не имеют авторизации tooperform действия «Microsoft.Authorization/roleAssignments/write» с областью «/ subscriptions / {guid}».»**  -Эта ошибка появляется, когда учетная запись имеет достаточные разрешения tooassign удостоверением tooan роли. Попросите администратора вашей подписки tooadd вы tooUser доступа к роли администратора.

## <a name="sample-applications"></a>Примеры приложений
Сведения о входе в систему как hello приложения с помощью различных платформ см. в разделе:

* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a>Дальнейшие действия
* Подробные инструкции по установке приложения в Azure для управления ресурсами см. в разделе [tooauthorization руководство разработчика с hello API диспетчера ресурсов Azure](resource-manager-api-authentication.md).
* см. Дополнительные сведения об использовании сертификатов и Azure CLI tooget [сертификат проверки подлинности на основе субъектов-служб Azure из командной строки Linux](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx). 
* Список доступных действий, которые могут быть предоставлены или запрещены toousers см. в разделе [операций поставщика ресурсов диспетчера ресурсов Azure](../active-directory/role-based-access-control-resource-provider-operations.md).
