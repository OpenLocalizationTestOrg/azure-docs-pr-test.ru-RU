---
title: "старых устройств, присоединенных к aaaTroubleshooting гибридной Azure Active Directory | Документы Microsoft"
description: "Устранение неполадок на устройствах нижнего уровня с гибридным присоединением к Azure Active Directory."
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
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: edd56b89579fac6b427732902284ad9c568b87b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a>Устранение неполадок на устройствах нижнего уровня с гибридным присоединением к Azure Active Directory 

Этот раздел является применимо только toohello следующих устройств: 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 
 

Сведения об устройствах под управлением Windows 10 и Windows Server 2016 см. в статье [Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices](device-management-troubleshoot-hybrid-join-windows-current.md) (Устранение неполадок на устройствах под управлением Windows 10 и Windows Server 2016 с гибридным присоединением к Azure Active Directory).

В этом разделе предполагается, что [устройств, присоединенных к настроенным гибридной Azure Active Directory](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello следующие сценарии:

- Условный доступ на основе устройств

- [Корпоративное перемещение параметров](active-directory-windows-enterprise-state-roaming-overview.md)

- [Настройка Windows Hello для бизнеса](active-directory-azureadjoin-passport-deployment.md) 





Этот раздел содержит рекомендации по каким образом tooresolve потенциальные проблемы устранения неполадок.  

**Важная информация** 

- Hello максимальное число устройств на пользователя будет состоять из устройства. Например если *jdoe* и *jharnett* tooa входа в устройство, отдельные регистрации (DeviceID) создается для каждого из них в hello **пользователя** вкладка «сведения».  

- Здравствуйте, начальная регистрация / join устройств настроенных tooperform попытка входа в систему или блокировки или разблокировки. Возможна 5-минутная задержка, связанная с выполнением задачи планировщика задач. 

- Переустановка hello операционную систему или вручную отменить регистрацию и повторно зарегистрируйте может создать новую регистрацию в Azure AD и результаты в несколько записей в списке Вкладка сведений пользователя hello в hello портал Azure. 


## <a name="step-1-retrieve-hello-registration-status"></a>Шаг 1: Получить состояние регистрации hello 

**Состояние регистрации hello tooverify:**  

1. Привет открыть командную строку с правами администратора 

2. Введите `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`.

Эта команда отображает диалоговое окно, предоставляет дополнительные сведения о состоянии соединения hello.

![Присоединение к рабочей области для Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-hybrid-azure-ad-join-status"></a>Шаг 2: Оценка состояние соединения Azure AD гибридного hello 

Если hello гибридной Azure AD соединения не прошла успешно, диалоговое окно «hello» предоставляет сведения о возникшей проблемы hello.

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
  
**наиболее распространенными причинами сбоя гибридное соединение Azure AD для Hello являются:** 

- Отсутствует на компьютере hello внутренней сети организации или виртуальная частная сеть без подключения tooan локального контроллера домена AD.

- Вы вошли на компьютер tooyour с учетной записью локального компьютера. 

- Проблемы конфигурации службы: 

  - Hello сервера федерации была настроенных toosupport **WIAORMULTIAUTHN**. 

  - Отсутствует точка подключения службы объект, указывающий tooyour проверенное имя домена в Azure AD в лесу hello AD, которой принадлежит компьютер hello.

  - Пользователь достиг предела hello устройств. 

## <a name="next-steps"></a>Дальнейшие действия

Ответы на вопросы см hello [управление устройствами вопросы и ответы](device-management-faq.md)  
