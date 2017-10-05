---
title: "Доменные службы Azure Active Directory: обновление настроек DNS для виртуальной сети Azure | Документация Майкрософт"
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
ms.openlocfilehash: c704ee189072ce8ed196d1ef0a23edd528a10025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a>Включение доменных служб Azure Active Directory (предварительная версия)

## <a name="task-4-update-dns-settings-for-the-azure-virtual-network"></a>Задача 4. Обновление настроек DNS для виртуальной сети Azure
В предыдущих задачах по настройке вы успешно включили доменные службы Azure Active Directory для своего каталога. Следующая задача — сделать так, чтобы компьютеры в виртуальной сети могли подключаться к этим службам и использовать их. В этой статье мы обновим параметры DNS-сервера для виртуальной сети, указав два IP-адреса, по которым доменные службы Azure Active Directory доступны в виртуальной сети.

Чтобы обновить параметр DNS-сервера для виртуальной сети, в которой включены доменные службы Azure Active Directory, сделайте следующее.

1. На вкладке **Обзор** отображается набор **требуемых шагов конфигурации**, которые следует выполнить после полной подготовки управляемого домена. Первый шаг конфигурации — **обновление параметров DNS-сервера для виртуальной сети**.

    ![Доменные службы — вкладка "Обзор" после полной подготовки](./media/getting-started/domain-services-provisioned-overview.png)

2. По завершении полной подготовки домена на этой плитке отобразятся два IP-адреса. Каждый IP-адрес представляет контроллер домена для управляемого домена.

3. Чтобы скопировать первый IP-адрес в буфер обмена, нажмите кнопку копирования рядом с адресом. Затем нажмите кнопку **Настроить DNS-серверы**.

4. Вставьте первый IP-адрес в текстовое поле **Добавить DNS-сервер** в колонке **DNS-серверы**. Прокрутите по горизонтали влево, чтобы скопировать второй IP-адрес. Вставьте его в текстовое поле **Добавить DNS-сервер**.

    ![Доменные службы — обновление DNS](./media/getting-started/domain-services-update-dns.png)

5. После обновления DNS-серверов для виртуальной сети нажмите кнопку **Сохранить**.

> [!NOTE]
> Виртуальные машины в сети получат новые параметры DNS только после перезапуска. Чтобы получить обновленные параметры DNS сразу, активируйте перезапуск с помощью портала, PowerShell или CLI.
>
>

## <a name="next-step"></a>Дальнейшие действия
[Задача 5. Включение синхронизации паролей с доменными службами Azure AD](active-directory-ds-getting-started-password-sync.md)
