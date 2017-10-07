---
title: "aaaImplement аварийного восстановления с помощью резервного копирования и восстановления в службе управления API Azure | Документы Microsoft"
description: "Узнайте, как toouse резервного копирования и восстановления tooperform аварийного восстановления в Azure API Management."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f10be3c-f796-4a6c-bacd-7931b6aa82af
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 058bfb579e3a3f51fb1dac8ea37eb4fdbc83a4ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a>Как tooimplement аварийного восстановления с помощью службы резервного копирования и восстановления в Azure API Management
Путем выбора toopublish и управлять собственные интерфейсы API через API управления Azure, вы пользуетесь преимуществами многие ошибки отказоустойчивость и инфраструктуры, в противном случае пришлось бы toodesign, реализации и управления. Hello платформы Azure уменьшает большую часть потенциальных сбоев в малую долю стоимости hello.

размещенные toorecover от доступности проблем, влияющих на hello регион, где служба управления API вы должно быть готово tooreconstitute службы в другом регионе, в любое время. В зависимости от целей доступности и цель времени восстановления может требуется tooreserve службы резервного копирования в одной или несколькими областями и повторите toomaintain своей конфигурации и содержимого в соответствии с hello активной службы. резервное копирование службы Hello и функция восстановления предоставляет необходимые стандартного блока hello для реализации стратегии аварийного восстановления.

В этом руководстве показано, как запросы tooauthenticate диспетчера ресурсов Azure и как toobackup и восстановлении экземпляров служб управления API.

> [!NOTE]
> Hello процесс резервного копирования и восстановления экземпляра службы управления API для аварийного восстановления можно использовать также для репликации экземпляров службы управления API для сценариев, например промежуточного хранения.
>
> Обратите внимание, что срок действия каждой резервной копии истекает через 30 дней. При попытке toorestore резервной копии hello 30-дневный срок действия которого истек, hello восстановление с `Cannot restore: backup expired` сообщения.
>
>

## <a name="authenticating-azure-resource-manager-requests"></a>Проверка подлинности запросов к диспетчеру ресурсов Azure
> [!IMPORTANT]
> Hello API REST для резервного копирования и восстановления использует диспетчера ресурсов Azure и содержит другой механизм проверки подлинности, чем hello API-интерфейс REST управления API управления сущностей. Hello в этом разделе описывается, каким образом запросы tooauthenticate диспетчера ресурсов Azure. Дополнительные сведения см. в [справочнике REST API Azure](http://msdn.microsoft.com/library/azure/dn790557.aspx).
>
>

Все hello задачи, выполняемые с ресурсами с помощью диспетчера ресурсов Azure hello должен пройти проверку подлинности в Azure Active Directory с помощью hello следующие шаги.

* Добавление клиента Azure Active Directory toohello приложения.
* Разрешения для приложения hello, который был добавлен.
* Получите токен hello для проверки подлинности запросов tooAzure диспетчера ресурсов.

Hello первым шагом является toocreate приложение Azure Active Directory. Войти в hello [классический портал Azure](http://manage.windowsazure.com/) hello подписку, которая содержит службу управления API с помощью экземпляра и перейдите toohello **приложений** вкладка по умолчанию, Azure Active Directory.

> [!NOTE]
> Если каталог по умолчанию hello Azure Active Directory не видны tooyour учетной записи, обратитесь в службу hello администратор hello toogrant hello подписки Azure требуется учетной записи разрешения tooyour.

![Создание приложения Azure Active Directory][api-management-add-aad-application]

Щелкните **Добавить**, выберите **Добавить приложение, разрабатываемое моей организацией**, а затем — **Собственное клиентское приложение**. Введите описательное имя и нажмите стрелку hello. Введите URL-адрес заполнителя, например `http://resources` для hello **URI перенаправления**, как это поле является обязательным, но значение hello не будет использоваться позднее. Щелкните приложение hello toosave флажок hello.

После сохранения приложения hello, нажмите кнопку **Настройка**, прокрутите вниз toohello **разрешения приложений tooother** и нажмите кнопку **добавить приложение**.

![Добавление разрешений][api-management-aad-permissions-add]

Выберите **Windows** **API управления службами Azure** и выберите приложение hello tooadd флажок hello.

![Добавление разрешений][api-management-aad-permissions]

Нажмите кнопку **делегированные разрешения** рядом с добавленным hello **Windows** **API управления службами Azure** приложения hello флажок для **доступ к Azure Управление службами (Предварительная версия)**и нажмите кнопку **Сохранить**.

![Добавление разрешений][api-management-aad-delegated-permissions]

Hello предыдущих tooinvoking API-интерфейсы для создания hello резервного копирования и восстановления, необходимые tooget маркер. Hello следующий пример использует hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) токен hello tooretrieve пакета nuget.

```c#
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;

namespace GetTokenResourceManagerRequests
{
    class Program
    {
        static void Main(string[] args)
        {
            var authenticationContext = new AuthenticationContext("https://login.microsoftonline.com/{tenant id}");
            var result = authenticationContext.AcquireToken("https://management.azure.com/", {application id}, new Uri({redirect uri});

            if (result == null) {
                throw new InvalidOperationException("Failed tooobtain hello JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

Замените `{tentand id}`, `{application id}`, и `{redirect uri}` с помощью hello, следуйте инструкциям.

Замените `{tenant id}` с идентификатором клиента hello hello приложения Azure Active Directory, вы только что создали. Идентификатор hello можно открыть, щелкнув **просмотреть конечные точки**.

![Endpoints][api-management-aad-default-directory]

![Endpoints][api-management-endpoint]

Замените `{application id}` и `{redirect uri}` с помощью hello **идентификатор клиента** и hello URL-адрес из hello **URI перенаправления** раздела из приложения Azure Active Directory **Настройка**  вкладки.

![Ресурсы][api-management-aad-resources]

После hello значения указаны, пример кода hello должен вернуться маркера аналогичные toohello, следующий пример.

![Маркер][api-management-arm-token]

Перед вызовом hello резервного копирования и восстановления операции, описанные в следующих разделах hello, задайте заголовок запроса hello авторизации для своего вызова REST.

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <a name="step1"> </a>Архивация службы управления API
tooback копирование hello проблемы службы управления API, следующие HTTP-запроса:

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

Описание:

* `subscriptionId`— идентификатор подписки hello, содержащего службу управления API hello, вы пытаетесь toobackup
* `resourceGroupName`-Строка в форме «Api - по умолчанию — {региона службы}» hello где `service-region` идентифицирует hello регион Azure, где размещена служба управления API, которые вы пытаетесь toobackup hello, например`North-Central-US`
* `serviceName`-Имя hello hello службы управления API, создании резервной копии указан во время его создания hello
* `api-version` замените `2014-02-14`.

В тексте hello hello запроса укажите имя учетной записи хранилища Azure целевой hello, ключ доступа, имя контейнера BLOB-объекта и имя архива:

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

Задайте значение hello hello `Content-Type` заголовок запроса слишком`application/json`.

Резервная копия — это длительная операция, может занять несколько минут toocomplete.  Если hello запрос выполнен успешно, и была инициирована hello процесс резервного копирования вы получите `202 Accepted` код состояния ответа с `Location` заголовок.  Создание «GET» запрашивает toohello URL-адрес в hello `Location` toofind заголовок hello состояние операции hello. Во время резервного копирования hello tooreceive код состояния 202 Accepted будет продолжено. Код ответа `200 OK` покажет успешного завершения операции резервного копирования hello.

Следует учитывать следующие ограничения при выполнении резервного копирования запроса hello.

* **Контейнер** указан в тексте запроса hello **должен существовать**.
* Пока выполняется резервное копирование, **не предпринимайте никаких действий по управлению службами**, таких как повышение или понижение уровня SKU, смена доменного имени и т. д.
* Восстановление **резервного копирования гарантируется только в течение 30 дней** с момента hello момент его создания.
* **Данные об использовании** используется для создания отчетов аналитики **не включено** hello резервного копирования. Используйте [API REST управления API Azure] [ Azure API Management REST API] tooperiodically извлечь аналитика отчеты для длительного хранения.
* Hello частоту, с которой создавать резервные копии службы будет влиять на вашей цели точки восстановления. его мы рекомендуем регулярного создания резервных копий, а также для выполнения резервного копирования по запросу после внесения важных toominimize изменяет tooyour службы управления API.
* **Изменения** сделан toohello конфигурации службы (например, API-интерфейсы, политики, внешний вид портала разработчиков) во время операции резервного копирования находится в процессе **не могут быть включены в резервную копию hello и поэтому будут потеряны**.

## <a name="step2"> </a>Восстановление службы управления API
toorestore службу управления API из ранее созданной резервной копии внести hello, выполнив HTTP-запроса.

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

Описание:

* `subscriptionId`— идентификатор подписки hello, содержащий восстановлении резервной копии в службе управления API hello
* `resourceGroupName`-Строка в форме «Api - по умолчанию — {региона службы}» hello где `service-region` идентифицирует hello регион Azure, где размещается hello восстановлении резервной копии в службе управления API, например`North-Central-US`
* `serviceName`-Имя hello hello во время его создания hello. Указанная служба выполняется восстановление в службе управления API
* `api-version` замените `2014-02-14`.

В тексте hello hello запроса укажите расположение файла резервной копии hello, т. е. имя учетной записи хранилища Azure, ключ доступа, имя контейнера BLOB-объекта и имя архива:

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

Задайте значение hello hello `Content-Type` заголовок запроса слишком`application/json`.

Восстановление проводится длительная операция, которая может занять до too30 или дополнительные toocomplete минут.  Если hello запрос выполнен успешно, и процесс восстановления hello была инициирована вы получите `202 Accepted` код состояния ответа с `Location` заголовок.  Создание «GET» запрашивает toohello URL-адрес в hello `Location` toofind заголовок hello состояние операции hello. Во время восстановления hello код состояния "202 принято» tooreceive будет продолжено. Код ответа `200 OK` покажет успешного завершения операции восстановления hello.

> [!IMPORTANT]
> **Hello SKU** службы hello, восстанавливаемой в **должно соответствовать** hello SKU hello резервная копия службы выполняется восстановление.
>
> **Изменения** сделан toohello конфигурации службы (например, API-интерфейсы, политики, внешний вид портала разработчиков) во время операции восстановления идет **, могут быть заменены**.
>
>

## <a name="next-steps"></a>Дальнейшие действия
Извлечь hello, следуя блогов Майкрософт для двух разных пошаговых hello процесса резервного копирования и восстановления.

* [Репликация учетных записей управления API Azure](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * Благодарим вас tooGisela для статьи toothis свой вклад.
* [Управление API Azure: резервное копирование и восстановление конфигурации](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * Подробные с Стюарт подход Hello не соответствует hello официальные рекомендации, но очень интересно.

[Backup an API Management service]: #step1
[Restore an API Management service]: #step2


[Azure API Management REST API]: http://msdn.microsoft.com/library/azure/dn781421.aspx

[api-management-add-aad-application]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-add-aad-application.png

[api-management-aad-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions.png
[api-management-aad-permissions-add]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions-add.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-delegated-permissions.png
[api-management-aad-default-directory]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-default-directory.png
[api-management-aad-resources]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-resources.png
[api-management-arm-token]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-arm-token.png
[api-management-endpoint]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-endpoint.png
