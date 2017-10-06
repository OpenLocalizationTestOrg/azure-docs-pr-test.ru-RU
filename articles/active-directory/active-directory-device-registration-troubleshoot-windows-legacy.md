---
title: "aaaTroubleshooting hello автоматической регистрации Azure AD домена компьютеров, присоединенных к для клиентов нижнего уровня Windows | Документы Microsoft"
description: "Устранение неполадок hello функции автоматической регистрации Azure AD домена компьютеров, присоединенных к для клиентов нижнего уровня Windows."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 84fe666576f13de09d1eaa5692517d45a4dbeebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad-for-windows-down-level-clients"></a>Устранение неполадок автоматической регистрации домена присоединены компьютеры tooAzure AD для клиентов нижнего уровня Windows 

Этот раздел является применимо только toohello следующих клиентов: 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

Windows 10 или Windows Server 2016 см. в разделе [Устранение неполадок автоматической регистрации домена присоединены компьютеры tooAzure AD – Windows 10 и Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).

В этом разделе предполагается, что функции автоматической регистрации устройств, присоединенных к домену, перечисленные в описано в [как tooconfigure Автоматическая регистрация Windows, присоединенных к домену устройствами с помощью Azure Active Directory](active-directory-device-registration-get-started.md).
 
Этот раздел содержит рекомендации по каким образом tooresolve потенциальные проблемы устранения неполадок.  
Toonote некоторые действия для успешного результатов: 

- Регистрация клиентов в Azure AD выполняется для каждого пользователя или устройства. Например: Если jdoe и jharnett входа в систему устройства toothis отдельной регистрации (DeviceID) создается для каждого пользователя на вкладке сведения пользователя hello.  

- Регистрации из этих клиентов стандартной hello является настроенным tootry при входе или заблокировать или разблокировать и возможна задержка 5 минут, что это должно запускаться с помощью задачи планировщика заданий. 

- Повторно установите hello операционной системы или вручную отменить регистрацию и повторно зарегистрировать может создать новую регистрацию в Azure AD, появится несколько записей в разделе вкладка сведений пользователя hello в hello портал Azure. 


## <a name="step-1-retrieve-hello-registration-status"></a>Шаг 1: Получить состояние регистрации hello 

**Состояние регистрации hello tooverify:**  

1. Привет открыть командную строку с правами администратора 

2. Введите `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`.

Эта команда отображает диалоговое окно, предоставляет дополнительные сведения о состоянии соединения hello.

![Присоединение к рабочей области для Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-registration-status"></a>Шаг 2: Оценка hello состояние регистрации 

Если hello соединения не прошла успешно, диалоговое окно «hello» предоставляет сведения о возникшей проблемы hello.

**приведены наиболее часто возникающих проблем Hello.**

- Службы федерации Active Directory или служба Azure AD настроены неправильно

    ![Присоединение к рабочей области для Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- Вы не вошли в качестве пользователя домена

    ![Присоединение к рабочей области для Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- Достигнут предел квоты

    ![Присоединение к рабочей области для Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- Hello служба не отвечает 

    ![Присоединение к рабочей области для Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

Сведения о состоянии hello также можно найти в журнале событий hello **приложений и служб Log\Microsoft — присоединение к**.
  
**наиболее распространенные причины сбоя регистрации Hello** 

- Отсутствует на компьютере hello внутренней сети организации или виртуальная частная сеть без подключения tooan локального контроллера домена AD.

- Вы вошли на компьютер tooyour с учетной записью локального компьютера. 

- Проблемы конфигурации службы: 

  - Hello сервера федерации была настроенных toosupport **WIAORMULTIAUTHN**. 

  - Отсутствует точка подключения службы объект, указывающий tooyour проверенное имя домена в Azure AD в лесу hello AD, которой принадлежит компьютер hello.

  - Пользователь достиг предела hello устройств. Прочитайте статью "Знакомство с регистрацией устройств в Azure Active Directory".

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения см. в разделе hello [автоматической регистрации устройств вопросы и ответы](active-directory-device-registration-faq.md) 
