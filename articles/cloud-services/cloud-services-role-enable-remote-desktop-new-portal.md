---
title: "aaaEnable подключение к удаленному рабочему столу для роли в облачных службах Azure | Документы Microsoft"
description: "Как tooconfigure azure облачной службы подключения удаленного рабочего стола tooallow приложения"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: 73ea1d64-1529-4d72-b58e-f6c10499e6bb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: mmccrory
ms.openlocfilehash: 55d7043df571c2e88b04aa9ef01dc8ae1d6784f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a>Включение подключения к удаленному рабочему столу для роли в облачных службах Azure
> [!div class="op_single_selector"]
> * [Портал Azure](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Классический портал Azure](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

Удаленный рабочий стол позволяет tooaccess hello системной роли, работающих в Azure. Можно использовать tootroubleshoot подключения удаленного рабочего стола и диагностировать проблемы с приложением во время его выполнения.

Можно включить удаленный рабочий стол в данной роли во время разработки, включая модули, удаленный рабочий стол hello в определении службы или вы можете tooenable удаленного рабочего стола через hello расширения удаленного рабочего стола. Hello рекомендуется расширение удаленного рабочего стола hello toouse как можно включить удаленный рабочий стол, даже после развертывания приложения hello без необходимости tooredeploy приложения.

## <a name="configure-remote-desktop-from-hello-azure-portal"></a>Настроить удаленный рабочий стол из hello портал Azure
Hello портал Azure использует подход hello расширения удаленного рабочего стола, поэтому можно включить удаленный рабочий стол, даже после развертывания приложения hello. Hello **удаленного рабочего стола** колонку для облачной службы позволяет tooenable удаленного рабочего стола, изменение hello локальную учетную запись администратора используется tooconnect toohello виртуальных машин, сертификат hello, используемые в проверке подлинности и задайте hello Дата окончания срока действия.

1. Нажмите кнопку **облачные службы**, щелкните имя hello hello облачной службы и нажмите кнопку **удаленного рабочего стола**.

    ![Удаленный рабочий стол в облачных службах](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. Выберите ли вы хотите tooenable удаленного рабочего стола для отдельных ролей или для всех ролей, а затем измените значение hello переключателя hello слишком**включено**.

3. Заполните поля hello требуется имя пользователя, пароль, срок действия и сертификата.

    ![Удаленный рабочий стол в облачных службах](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > Если включить удаленный рабочий стол и нажать кнопку «ОК» (флажок), все экземпляры роли будут перезапущены. tooprevent перезагрузки пароль hello hello сертификата используется tooencrypt должен устанавливаться на роли hello. tooprevent перезагрузки [отправка сертификата для облачной службы hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) , а затем возвращают toothis диалогового окна.
   >
   >
3. В **ролей**, выберите роль hello tooupdate или выберите **все** для всех ролей.

4. По завершении обновления настроек нажмите кнопку **Сохранить**. Может занять несколько минут, прежде чем экземпляры ролей готовы tooreceive подключений.

## <a name="remote-into-role-instances"></a>Удаленное подключение к экземплярам ролей
После включения удаленного рабочего стола с ролями hello может инициировать подключение непосредственно из hello портала Azure:

1. Нажмите кнопку **экземпляров** tooopen hello **экземпляров** колонку.
2. Выберите экземпляр роли, где настроен удаленный рабочий стол.
3. Нажмите кнопку **Connect** toodownload RDP-файла для экземпляра роли hello.

    ![Удаленный рабочий стол в облачных службах](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. Нажмите кнопку **откройте** и затем **Connect** toostart hello подключения удаленного рабочего стола.

>[!NOTE]
> Если облачная служба находится на расстоянии за NSG, может потребоваться toocreate правила, разрешающие трафик через порты **3389** и **20000**.  Удаленный рабочий стол использует порт **3389**.  Экземпляров облачной службы, распределяются, поэтому не может напрямую управлять какой экземпляр tooconnect для.  Hello *RemoteForwarder* и *RemoteAccess* агенты управления трафиком протокола удаленного рабочего СТОЛА и разрешить toosend клиента hello куки-файл протокола удаленного рабочего СТОЛА и tooconnect отдельного экземпляра, чтобы указать.  Hello *RemoteForwarder* и *RemoteAccess* агенты имеют этот порт **20000*** открыть, который может блокироваться, если у вас есть NSG.

## <a name="additional-resources"></a>Дополнительные ресурсы

[Как облачные службы tooConfigure](cloud-services-how-to-configure.md)
[облачных служб часто задаваемые вопросы — удаленного рабочего стола](cloud-services-faq.md)
