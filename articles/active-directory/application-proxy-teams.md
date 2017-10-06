---
title: "aaaAccess приложений прокси приложения Azure AD в командах | Документы Microsoft"
description: "Используйте локальное приложение, через групп Майкрософт tooaccess прокси приложения Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 13c36e43ae6349df09272e308ad4f40451cbbeb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a>Доступ к приложениям в локальной среде через Microsoft Teams

Прокси приложения с Azure Active Directory позволяет единого входа tooon локальные приложения независимо от того, где вы находитесь и групп Майкрософт упрощает процесс совместной работы в одном месте. Интеграция hello два вместе означает, что пользователи могут эффективно с коллегами в любой ситуации. 

Пользователи могут добавлять облачные приложения tootheir команды каналы [с помощью вкладок](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), но что произойдет, если этот сайт SharePoint или средств планирования, то все они используют размещается локально? Прокси приложения — решение hello. Они могут добавлять приложения hello опубликованных через прокси-сервер приложения tootheir каналы с использованием же внешние URL-адреса, всегда используют tooaccess приложений удаленно. И поскольку прокси-сервер приложения выполняет проверку подлинности через Azure Active Directory, hello, которое выполняется на одном один вход.


## <a name="install-hello-application-proxy-connector-and-publish-your-app"></a>Установите соединитель прокси приложения hello и публикация приложения

Если это еще не сделано, [настройки прокси-сервера приложений для вашего клиента и установить соединитель hello](active-directory-application-proxy-enable.md). Затем [опубликуйте свое локальное приложение](application-proxy-publish-azure-portal.md) для удаленного доступа. Если вы публикуете приложение hello, запишите hello внешний URL-адрес, так как к конечным пользователям необходимы эти сведения при добавлении tooTeams приложения hello.

Если уже имеется опубликованных приложений, но не помните их внешние URL-адреса, находить их в hello [портал Azure](https://portal.azure.com). Вход, затем перейдите слишком**Azure Active Directory** > **корпоративных приложений** > **всех приложений** > Выбор приложения > **Прокси приложения**.

## <a name="add-your-app-tooteams"></a>Добавить tooTeams вашего приложения

После публикации приложения hello через прокси-сервер приложения Проинформируйте пользователей о том, что их можно добавить непосредственно в связанные с командами каналы в виде вкладки. Для этого им потребуется выполнить следующие три шага:

1. Перейдите toohello команды каналов место tooadd этого приложения и выберите  **+**  tooadd вкладки.

   ![Выберите "Добавить вкладку"](./media/application-proxy-teams/add-tab.png)

2. Выберите **веб-сайт** из параметры вкладки «hello».

   ![Добавление веб-сайта](./media/application-proxy-teams/website.png)

3. Присвойте имя вкладке hello и задайте hello toohello прокси приложения внешний URL-АДРЕСЕ. 

   ![Настройка имени вкладки и URL-адреса](./media/application-proxy-teams/tab-name-url.png)

Как только один член команды добавляет вкладку hello, оно отображается для всех пользователей в канале hello. Все пользователи, имеющие доступ toohello приложения получить единого входа с учетными данными hello, которые они используют для групп Майкрософт. Все пользователи, у которых нет доступа приложения toohello увидите вкладку hello в группах, но заблокированы, пока не предоставить им разрешения toohello локальных приложений и hello Azure портала опубликованной версии приложение hello. 

## <a name="next-steps"></a>Дальнейшие действия

- Узнайте, каким образом слишком[публикации локальных сайтов SharePoint](application-proxy-enable-remote-access-sharepoint.md) с помощью прокси приложения.
- Настройка вашего приложения toouse [пользовательских доменов](active-directory-application-proxy-custom-domains.md) для их внешний URL-адрес. 
