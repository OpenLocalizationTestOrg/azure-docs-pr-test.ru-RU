---
title: "Устранение неполадок удаленных приложений RemoteApp - aaaAzure сбоев запуска и подключение приложения | Документы Microsoft"
description: "Узнайте, как tootroubleshoot проблемы с начальным и подключении tooapplications в Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e5cf7171-d1c2-4053-a38b-5af7821305e1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e51d480c9d3fa1f2076f95b63c7a8cd2f6956a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-remoteapp---application-launch-and-connection-failures"></a>Устранение неполадок Azure RemoteApp — ошибки запуска и подключения приложений
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Приложения, размещенные в Azure RemoteApp не смогут toolaunch несколько соображений. В этой статье описываются различные причины и сообщения об ошибках, которые пользователи могут получать при попытке toolaunch приложений. Здесь также рассматриваются сбои подключения. (Но не описаны в этой статье проблемы при входе в клиент Azure RemoteApp hello.)  

Сведения о распространенных сообщений об ошибках из-за сбоев tooapp запуска и соединения, читайте дальше.

## <a name="were-getting-you-set-up-try-again-in-10-minutes"></a>Выполняется настройка... Повторите попытку через 10 минут.
Эта ошибка означает, что Azure RemoteApp, масштабирование мощностях hello toomeet пользователей. В фоновом режиме hello несколько экземпляров виртуальных Машин Azure RemoteApp создается toohandle hello потребностях пользователей. Обычно это занимает около пяти минут, но может занять too10 минут. В некоторых случаях это происходит не так уж быстро, а ресурсы нужны немедленно. Например сценарий 9: 00, где многие пользователи должны toouse приложения в Azure RemoteAppn в hello то же время. В этом случае tooyou можно включить **режиме емкость** на hello серверной части. toodo этом открытые в службу поддержки Azure. Быть определенных tooinclude Идентификатором подписки в запросе hello.  

![Выполняется настройка](./media/remoteapp-apptrouble/ra-apptrouble1.png)

## <a name="could-not-auto-reconnect-tooyour-applications-please-re-launch-your-application"></a>Не удается автоматически переподключиться tooyour приложения, повторно запустите приложение
Это сообщение об ошибке часто возникает, если вы использовали Azure RemoteApp и затем поместить вашего ПК toosleep больше времени, чем 4 часов и затем вывел ПК и повторного подключения клиента попытки hello Azure RemoteApp tooauto и истечения времени ожидания.  Поручить пользователям toonavigate задней toohello приложения и повторите попытку tooopen из клиента hello Azure RemoteApp.

![Не удается автоматически переподключиться tooyour приложений](./media/remoteapp-apptrouble/ra-apptrouble2.png) 

## <a name="problems-with-hello-temp-profile"></a>Проблемы с временным профилем hello
Эта ошибка возникает, если профиль пользователя (диск профиля пользователя) не удалось выполнить toomount и hello пользователя получает временный профиль.  Администраторы должны перемещаться toohello коллекции в hello портал Azure и перейдите toohello **сеансы** вкладку и повторите попытку слишком**Выход** hello пользователя. При этом будет принудительно полного выхода из сеанса пользователя hello - затем заново toolaunch попытки hello пользователя приложения. В случае неудачи обратитесь в службу поддержки Azure.

## <a name="azure-remoteapp-has-stopped-working"></a>Прекращена работа Azure RemoteApp
Это сообщение об ошибке означает hello Azure RemoteApp клиента испытывает проблемы и должен toobe перезапуска. Поручить пользователям tooclose: выберите **закрыть программу** и снова запустите клиент hello Azure RemoteApp.  Если проблема hello остается открытым и обращение в службу поддержки Azure.

![Прекращена работа Azure RemoteApp](./media/remoteapp-apptrouble/ra-apptrouble3.png)  

## <a name="an-error-occurred-while-remote-desktop-connection-was-accessing-this-resource-retry-hello-connection-or-contact-your-system-administrator"></a>Возникла ошибка при доступе к этому ресурсу через подключение к удаленному рабочему столу. Повторить попытку подключения hello, или обратитесь к системному администратору
Это общее сообщение об ошибке — обратитесь в службу поддержки Azure, чтобы мы могли разобраться в причинах ошибки. 

![Общее сообщение Azure RemoteApp](./media/remoteapp-apptrouble/ra-apptrouble4.png) 

