---
title: "Azure доменных служб Active Directory: Обновить параметры DNS для hello виртуальной сети Azure | Документы Microsoft"
description: "Приступая к работе с доменными службами Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: 484ff1a197a651bccb2b416448056acf69b0d8c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="update-dns-settings-for-hello-azure-virtual-network"></a>Обновите параметры DNS для hello виртуальной сети Azure
## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a>Задача 4: Обновите параметры DNS для hello виртуальной сети Azure
Hello предшествующей задачи настройки вы включили успешно Azure доменных служб Active Directory для вашего каталога. Следующая задача Hello-tooensure, что компьютеры в hello виртуальной сети могут подключаться и этих служб. В этой статье обновление hello параметры DNS-сервера для вашей виртуальной сети toopoint toohello два IP-адреса доменных служб Active Directory Azure доступно hello виртуальной сети.

> [!NOTE]
> После включения Azure доменных служб Active Directory для каталога hello, обратите внимание, hello IP-адресов для Azure доменных служб Active Directory, которые отображаются на hello **Настройка** вашего каталога.
>
>

tooupdate hello параметров сервера DNS для hello виртуальной сети, в котором требуется включить Azure доменных служб Active Directory, полный hello, следующие шаги:

1. Go toohello [классический портал Azure](https://manage.windowsazure.com).
2. Выберите в левой области hello **сетей**.  
    Hello **сетей** открывается окно.

    ![Окно виртуальных сетей](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. На hello **виртуальных сетей** вкладке, выберите hello виртуальной сети, в котором требуется включить tooview доменных служб Active Directory Azure его свойства.
4. Нажмите кнопку hello **Настройка** вкладки.

    ![Окно виртуальных сетей](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. В hello **DNS-серверы** введите оба hello IP-адресов, которые отображались в hello **доменных служб** раздела, посвященного hello **Настройка** вашего каталога.
6. Нажмите кнопку Параметры toosave hello DNS-сервера для этой виртуальной сети, в области задач hello hello нижней части окна hello **Сохранить**.

   ![Обновите параметры DNS-сервера hello для hello виртуальной сети](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  Виртуальные машины в сети hello hello новых параметров DNS получить только после перезагрузки. Если они вам требуются параметры DNS tooget hello обновить прямо сейчас, включать перезапуск портала hello, PowerShell или hello CLI.
>
>

## <a name="next-steps"></a>Дальнейшие действия
Задача 5. [включить синхронизацию паролей tooAzure доменных служб Active Directory](active-directory-ds-getting-started-password-sync.md)
