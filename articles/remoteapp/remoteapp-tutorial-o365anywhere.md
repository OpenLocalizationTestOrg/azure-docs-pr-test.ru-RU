---
title: "такие же возможности Office 365 на любом устройстве с Azure RemoteApp hello aaaGet | Документы Microsoft"
description: "Узнайте, как tooshare любое приложение Office 365 с пользователями с помощью Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 0c971ce9-7d45-4cfb-9737-15b6706047e8
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: guscatal;elizapo
ms.openlocfilehash: 140056c22c8c69b9ec605318e35a72b144da07eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-same-office-365-experience-on-any-device-with-azure-remoteapp"></a>Get hello же взаимодействие с Office 365 на любом устройстве с Azure RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

В этой статье рассматривается как toodeploy Office 365 на любом устройстве вашей компании. Пользователи могут получать hello те же возможности и пользовательского интерфейса experience на Android, Apple и Windows.

Это достигается с помощью платформы Azure RemoteApp — она позволяет размещать Office 365 на масштабируемых виртуальных машинах Azure, к которым подключаются пользователи. Такой набор виртуальных машин называется «облачной коллекцией».

## <a name="create-a-cloud-collection"></a>Создание облачной коллекции
После создания учетной записи Azure пройти слишком**RemoteApp** , щелкнув ссылку hello на hello слева.
![Отображение на портале Azure hello Azure RemoteApp](./media/remoteapp-tutorial-o365anywhere/1-menu.png)

Затем продолжить, щелкнув **новый** на нижней hello и «быстрое создание» коллекции. Укажите имя, регион hello, hello подписки, план hello и образ hello «Proffesional Office 2013», который мы предоставляем.
![Создание диалогового окна](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)

После завершения процесса создания коллекции hello формы hello должна начаться. Это может занять tooan часа.

![Waiting](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

После завершения процесса hello, он будет выглядеть примерно следующим образом. Если щелкнуть **Публикация**, вы увидите, что основная часть приложений Office уже опубликована.
![Созданная коллекция](./media/remoteapp-tutorial-o365anywhere/4-done.png)

![Опубликованные приложения](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

На этом этапе можно добавить несколько пользователей, имеющих коллекции toothis доступа, нажав кнопку **доступа пользователей**.
![настройка доступа пользователей](./media/remoteapp-tutorial-o365anywhere/6-user.png)

Теперь давайте испытать подключение tooOffice 365!

## <a name="connect-toooffice-365"></a>Подключение tooOffice 365
Мы будем перейдите слишком[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), прокрутите список вниз и нажмите кнопку **загрузить клиенты** tooinstall hello Azure RemoteApp клиента на устройстве hello, вы работаете. снимки экрана приветствия ниже предназначены для Windows.

После запуска приложения hello запрашивается toosign учетной записью Майкрософт (ранее называвшиеся «Live ID»), используйте hello того же, как учетная запись Azure сейчас. Выполнив вход, вы увидите уведомление о новых приглашениях, щелкнув которое, вы откроете список представленного ниже вида. Примите приглашение hello, соответствующий вашей электронной почты владельца учетной записи Azure.

![Новое приглашение](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

Экран с новыми приглашениями.

![Принятие приглашения](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

После принятия приглашения hello вы увидите все приложения Office hello в клиенте hello Azure RemoteApp.

![Список приложений](./media/remoteapp-tutorial-o365anywhere/9-work.png)

При нажатии кнопки на любом из этих приложений, hello следует запустить на hello виртуальной машины Azure и должно быть задано! Вот и все!

![запуск](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![PowerPoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

