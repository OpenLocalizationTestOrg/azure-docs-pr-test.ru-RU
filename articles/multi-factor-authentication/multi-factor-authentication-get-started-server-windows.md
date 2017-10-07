---
title: "aaaWindows проверки подлинности и сервера Azure MFA | Документы Microsoft"
description: "Это является hello Azure многофакторной проверки подлинности, будет полезен при развертывании проверки подлинности Windows и сервера Azure Multi-factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 0fc38fd751966bf883d4eae7c48055988922af80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a>Проверка подлинности Windows и сервер Azure Multi-Factor Authentication
Использовать проверку подлинности Windows hello раздел tooenable сервера Azure Multi-factor Authentication hello и настроить проверку подлинности Windows для приложений. Перед тем как настроить проверку подлинности Windows, оставьте hello после списка в виду:

* После завершения установки перезагрузите hello многофакторной проверки подлинности Azure для служб терминалов tootake эффекта.
* Если установлен флажок «Требовать многофакторную проверку подлинности Azure сопоставление пользователей» и вы не hello список пользователей, нельзя будет toolog в машину hello после перезагрузки.
* Надежные IP-адреса зависят от того, может ли приложение hello предоставлять hello IP-адрес клиента с проверкой подлинности hello. В настоящее время поддерживаются только службы терминалов.  

> [!NOTE]
> Эта функция не поддерживается toosecure служб терминалов в Windows Server 2012 R2.

## <a name="toosecure-an-application-with-windows-authentication-use-hello-following-procedure"></a>toosecure приложения с проверкой подлинности Windows, hello используйте следующие процедуры.
1. В hello сервера Azure Multi-factor Authentication щелкните значок проверки подлинности Windows hello.
   ![Проверка подлинности Windows](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)
2. Проверьте hello **включить проверку подлинности Windows** флажок. По умолчанию этот флажок не установлен.
3. Вкладка "приложения" Hello позволяет администратору tooconfigure hello одно или несколько приложений для проверки подлинности Windows.
4. Выберите сервер или приложение — укажите, включен ли hello сервер или приложение. Нажмите кнопку **ОК**.
5. Щелкните **Добавить…**
6. Вкладка Hello надежных IP-адресов позволяет tooskip Azure многофакторной проверки подлинности для сеансов Windows с определенных IP-адресов. Например если сотрудники используют приложение hello из офиса hello и из дома, можно, не требуется их отвечать на звонки многофакторной проверки подлинности в Azure во время hello office. Для этого следует указать подсети hello office как операция надежных IP-адресов.
7. Щелкните **Добавить…**
8. Выберите **один IP-адрес** при желании tooskip один IP-адрес.
9. Выберите **диапазон IP-адресов** при желании tooskip весь диапазон IP-адресов. Пример: 10.63.193.1-10.63.193.100.
10. Выберите **подсети** при желании toospecify диапазон IP-адресов в нотации подсети. Введите начальный IP-адрес подсети hello и выберите соответствующую маску сети из раскрывающегося списка hello hello.
11. Нажмите кнопку **ОК**.

## <a name="next-steps"></a>Дальнейшие действия

- [Расширенные сценарии с использованием Многофакторной идентификации Azure и VPN-решений сторонних поставщиков](multi-factor-authentication-advanced-vpn-configurations.md)

- [Расширить существующую инфраструктуру проверки подлинности с hello NPS расширения для многофакторной проверки Подлинности Azure](multi-factor-authentication-nps-extension.md)
