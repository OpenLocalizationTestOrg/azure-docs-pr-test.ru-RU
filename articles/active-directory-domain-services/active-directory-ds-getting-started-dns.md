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
ms.openlocfilehash: e6eaff555cb9b7bb89ab7581d8de0b8cfc844529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a>Включение доменных служб Azure Active Directory (предварительная версия)

## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a>Задача 4: обновите параметры DNS для hello виртуальной сети Azure
Hello предшествующей задачи настройки вы включили успешно Azure доменных служб Active Directory для вашего каталога. Следующая задача Hello-tooensure, что компьютеры в hello виртуальной сети могут подключаться и этих служб. В этой статье обновление hello параметры DNS-сервера для вашей виртуальной сети toopoint toohello два IP-адреса доменных служб Active Directory Azure доступно hello виртуальной сети.

tooupdate hello параметров сервера DNS для hello виртуальной сети, в котором требуется включить Azure доменных служб Active Directory, полный hello, следующие шаги:

1. Hello **Обзор** вкладке отображается набор **необходимые действия по настройке** toobe выполняется после полного выделения ресурсов для управляемого домена. Сначала конфигурации Hello **параметры обновления DNS-сервера, для виртуальной сети**.

    ![Доменные службы — вкладка "Обзор" после полной подготовки](./media/getting-started/domain-services-provisioned-overview.png)

2. По завершении полной подготовки домена на этой плитке отобразятся два IP-адреса. Каждый IP-адрес представляет контроллер домена для управляемого домена.

3. toocopy hello первый IP адрес tooclipboard, нажмите кнопку Далее tooit hello копирования кнопки. Нажмите кнопку hello **настроить DNS-серверы** кнопки.

4. Вставьте первый IP-адрес hello в hello **добавить DNS-сервер** текстовое поле в hello **DNS-серверы** колонку. Горизонтальная прокрутка toohello слева toocopy hello второй IP-адрес и вставьте его в hello **добавить DNS-сервер** текстового поля.

    ![Доменные службы — обновление DNS](./media/getting-started/domain-services-update-dns.png)

5. Нажмите кнопку **Сохранить** после tooupdate hello DNS-серверов для виртуальной сети hello.

> [!NOTE]
> Виртуальные машины в сети hello hello новых параметров DNS получить только после перезагрузки. Если они вам требуются параметры DNS tooget hello обновить прямо сейчас, включать перезапуск портала hello, PowerShell или hello CLI.
>
>

## <a name="next-step"></a>Дальнейшие действия
[Задача 5: Включение синхронизации паролей tooAzure доменных служб Active Directory](active-directory-ds-getting-started-password-sync.md)
