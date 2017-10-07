---
title: "Пользователи tooindividual aaaPublish приложений в коллекцию Azure RemoteApp (Предварительная версия) | Документы Microsoft"
description: "Узнайте, как публиковать приложения tooindividual пользователей, а не в зависимости от группы в Azure RemoteApp."
services: remoteapp-preview
documentationcenter: 
author: piotrci
manager: mbaldwin
editor: 
ms.assetid: 1fd0539d-fa65-4ea5-a98e-0be0cf580690
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: piotrci
ms.openlocfilehash: 87b435552ddbfc2c6d03aeb01d95a44985e71f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-tooindividual-users-in-an-azure-remoteapp-collection-preview"></a>Публикация приложений tooindividual пользователей в коллекции Azure RemoteApp (Предварительная версия)
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

В этой статье объясняется, как пользователи tooindividual toopublish приложений в коллекцию Azure RemoteApp. Это новые функциональные возможности в Azure RemoteApp, в настоящее время в личной предварительной версии и первыми tooselect доступны только для ознакомительных целей.

Первоначально Azure RemoteApp включен только один способ публикации приложений: Здравствуйте, администратор может опубликовать приложения из образа hello и могли бы быть видимым tooall пользователей в коллекции hello.

Распространенным сценарием является tooinclude многих приложений в одном образ и развертывать одной коллекции в порядке расходы на управление tooreduce. Зачастую не все приложения, соответствующие tooall пользователей — администраторы предпочли бы пользователей tooindividual toopublish приложения, они не увидят ненужные приложения, в приложении веб-канала.

Теперь это возможно в Azure RemoteApp — в настоящее время в виде функции в ограниченной предварительной версии. Вот краткое описание новых функциональных возможностей hello.

1. Для коллекции можно настроить один из двух режимов.
   
   * Hello исходный режим сбора, где все пользователи в коллекции могут просматривать все опубликованные приложения. Это режим по умолчанию hello.
   * новые приложения режим Hello, где пользователи видят только приложения, которые были явно назначены toothem
2. В момент hello режим приложения hello можно включить только с помощью командлетов Azure RemoteApp PowerShell.
   
   * Если установить tooapplication режим назначение пользователя в коллекции hello нельзя управлять с помощью hello портал Azure. Назначение пользователя имеет toobe, управляемых с помощью командлетов PowerShell.
3. Пользователи будут видеть только приложения hello опубликованы непосредственно toothem. Однако по-прежнему возможно для других приложений, доступных на изображении hello Здравствуйте, toolaunch пользователя путем доступа к их непосредственно в операционной системе hello.
   
   * Этот компонент не предоставляет безопасного блокировки приложений; ограничивает только видимости в приложение hello веб-канала.
   * Если требуется, чтобы пользователи tooisolate из приложений, необходимо будет toouse отдельные коллекции для этого.

## <a name="how-tooget-azure-remoteapp-powershell-cmdlets"></a>Как tooget командлеты Azure RemoteApp PowerShell
функциональность tootry hello новой предварительной версии, необходимо будет toouse командлетов Azure PowerShell. Оно не возможные toouse hello Azure портала tooenable hello нового приложения публикации режим управления.

Во-первых, убедитесь, что у вас есть hello [модуля Azure PowerShell](/powershell/azure/overview) установлен.

Запустите консоль PowerShell hello в режиме администратора и выполнения hello, выполнив командлет:

        Add-AzureAccount

Он запросит имя пользователя и пароль Azure. После входа командлеты Azure RemoteApp могут toorun будут выполняться для ваших подписок Azure.

## <a name="how-toocheck-which-mode-a-collection-is-in"></a>Как toocheck режим, который является коллекция в
Выполните следующий командлет hello.

        Get-AzureRemoteAppCollection <collectionName>

![Проверьте режим сбора hello](./media/remoteapp-perapp/araacllelvel.png)

Hello AclLevel свойство может иметь hello следующие значения:

* Сбор данных: hello исходной публикации режим. Все пользователи видят все опубликованные приложения.
* Приложение: hello новой публикации режим. Пользователи видят только приложения hello непосредственно опубликованные toothem.

## <a name="how-tooswitch-tooapplication-publishing-mode"></a>Как режим публикации tooapplication tooswitch
Выполните следующий командлет hello.

        Set-AzureRemoteAppCollection -CollectionName -AclLevel Application

Будут сохранены приложения состояния публикации: изначально все пользователи будут видеть все исходные опубликованные приложения hello.

## <a name="how-toolist-users-who-can-see-a-specific-application"></a>Как toolist пользователей, которые можно просмотреть определенное приложение
Выполните следующий командлет hello.

        Get-AzureRemoteAppUser -CollectionName <collectionName> -Alias <appAlias>

Это список всех пользователей, можно увидеть приложения hello.

Примечание: Вы увидите псевдонимы приложения hello (называемые «alias приложения» в синтаксисе hello выше), запустив Get-AzureRemoteAppProgram - CollectionName <collectionName>.

## <a name="how-tooassign-an-application-tooa-user"></a>Как tooassign пользователь tooa приложения
Выполните следующий командлет hello.

        Add-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

Hello пользователь увидит приложения hello в клиенте Azure RemoteApp hello и может tooconnect tooit.

## <a name="how-tooremove-an-application-from-a-user"></a>Как tooremove приложения от пользователя
Выполните следующий командлет hello.

        Remove-AzureRemoteAppUser -CollectionName <collectionName> -UserUpn <user@domain.com> -Type <OrgId|MicrosoftAccount> -Alias <appAlias>

## <a name="providing-feedback"></a>Обратная связь
Мы будем признательны за ваши отзывы и предложения относительно этой функции в предварительной версии. Заполните hello [опроса](http://www.instant.ly/s/FDdrb) toolet нам о своих впечатлениях.

## <a name="havent-had-a-chance-tootry-hello-preview-feature"></a>Не было функцию предварительного просмотра hello вероятность tootry?
Если вы не участвовали в предварительной версии hello еще, используйте это [опроса](http://www.instant.ly/s/AY83p) toorequest доступа.

