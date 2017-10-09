---
title: "aaaManage Azure Analysis Services | Документы Microsoft"
description: "Узнайте, как toomanage служб Analysis Services server в Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b03bc440801a68162039e28cdb4f863da374014e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-analysis-services"></a>Управление службами Analysis Services
После создания сервера служб Analysis Services в Azure, могут иметься некоторые задачи администрирования и управления tooperform необходимо немедленно или некоторое время вниз road hello. Например запустите обработку toohello обновления данных, управление правами на доступ к моделям hello на сервере, или наблюдать за исправностью сервера. Некоторые задачи управления можно выполнять только на портале Azure, другие — только в SQL Server Management Studio (SSMS), а некоторые — и там, и там.

## <a name="azure-portal"></a>Портал Azure
[Портал Azure](http://portal.azure.com/) можно создать и удалить серверы, отслеживать ресурсы сервера, изменить размер, и управления, у кого есть доступ tooyour серверов.  При возникновении проблем вы также можете отправить запрос на техническую поддержку.

![Получение имени сервера в Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a>SQL Server Management Studio
Подключение сервера tooyour в Azure выполняется так же, как соединение tooa экземпляра сервера в вашей организации. В SSMS можно выполнять многие hello же задачи, такие как обработки данных или создайте сценарий обработки, управление ролями и с помощью PowerShell.
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a>Скачивание и установка SSMS
tooget все Здравствуйте новейшие функции и возможности наиболее hello, при подключении сервера tooyour Azure Analysis Services, убедитесь, что вы используете последнюю версию SSMS hello. 

[Скачайте SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).


### <a name="tooconnect-with-ssms"></a>tooconnect со средой SSMS
 При использовании SSMS до подключения приветствие сервера tooyour первый раз, убедитесь, что ваше имя пользователя входит в группу "Администраторы" Analysis Services hello. toolearn более, в разделе [администраторам](#server-administrators) далее в этой статье.

1. Перед подключением, необходимо имя сервера tooget hello. В **портал Azure** > сервера > **Обзор** > **имя сервера**, имя сервера hello копирования.
   
    ![Получение имени сервера в Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. В среде SSMS выберите **Обозреватель объектов** и щелкните **Подключиться** > **Analysis Services**.
3. В hello **подключения tooServer** диалоговое окно «», вставьте в поле имя сервера hello, а затем в **проверки подлинности**, выберите один из следующих типов проверки подлинности hello:
   
    **Проверка подлинности Windows** toouse учетные данные Windows домен\имя пользователя и пароль.

    **Пароль проверки подлинности Active Directory** toouse учетной записи организации. Например, при подключении с компьютера, не присоединенного к домену.

    **Универсальной проверки подлинности Active Directory** toouse [неинтерактивной или многофакторной проверки подлинности](../sql-database/sql-database-ssms-mfa-authentication.md). 
   
    ![Подключение в среде SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a>Администраторы сервера и пользователи базы данных
В службах Azure Analysis Services существует два типа пользователей, администраторы сервера и пользователи базы данных. Оба типа пользователей должны находиться в Azure Active Directory и иметь настроенный адрес электронной почты организации или имя участника-пользователя. toolearn более, в разделе [проверки подлинности и пользовательские разрешения](analysis-services-manage-users.md).


## <a name="troubleshooting-connection-problems"></a>Устранение неполадок с подключением
При подключении с помощью SSMS, если возникли проблемы, может потребоваться tooclear hello входа кэша. Ничего не кэшированных toodisc. tooclear hello кэш-памяти, закройте и перезапустите hello подключения процесса. 

## <a name="next-steps"></a>Дальнейшие действия
Если уже еще не развернут новый сервер tooyour табличной модели, сейчас самое подходящее время. toolearn более, в разделе [развертывания служб Analysis Services tooAzure](analysis-services-deploy.md).

При развертывании сервера tooyour модели вы готовы tooconnect tooit с помощью клиента или браузера. toolearn более, в разделе [получение данных из служб Azure Analysis server](analysis-services-connect.md).

