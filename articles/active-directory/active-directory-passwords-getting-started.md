---
title: "Быстрое начало работы с самостоятельным сбросом пароля в Azure AD | Документация Майкрософт"
description: "Сведения о быстром развертывании самостоятельного сброса пароля в Azure AD."
services: active-directory
keywords: 
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: bde8799f-0b42-446a-ad95-7ebb374c3bec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 4fed3a1c690fd6423ee5d3e5baef690d8896fbe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-azure-ad-self-service-password-reset"></a>Быстрое начало работы с самостоятельным сбросом пароля в Azure AD

> [!IMPORTANT]
> **Вы здесь потому, что возникают проблемы при входе?** Если это так, [с помощью этих инструкций можно изменить и сбросить пароль](active-directory-passwords-update-your-own-password.md).

## <a name="rapidly-deploy-self-service-password-reset"></a>Быстрое развертывание самостоятельного сброса пароля

Самостоятельный сброс пароля (SSPR) предоставляет простое означает для tooreset пользователей tooempower администраторы ИТ или разблокировать свои пароли или учетные записи. Hello включает система подробные tootrack отчетов при использовании системы hello вместе с tooalert уведомления вы toomisuse или нарушений.

В этом руководстве предполагается, что у вас уже есть рабочий пробный или лицензированный клиент Azure AD. Если вам нужна помощь в настройке Azure AD, см. в статье hello [Приступая к работе с Azure AD](https://azure.microsoft.com/trial/get-started-active-directory/).

1. В имеющемся клиенте Azure AD выберите **Сброс пароля**.

2. Из hello **«Свойства»** экрана в разделе «Self пароль сбросить включена служба» выберите один из следующих hello параметр hello
    * Никто не - никто не может toouse SSPR функциональности
    * Группа — конкретных Azure AD только члены группы, можно выбрать, функциональность может toouse SSPR
    * Все — все пользователи с учетными записями в клиенте Azure AD, функциональность может toouse SSPR

3. Из hello **«Методы проверки подлинности»** выберите экрана
    * Несколько методов требуется tooreset — мы поддерживаем как минимум одна или более двух
    * Методы доступны toousers - необходимы по крайней мере один, но никогда не повредит toohave дополнительный параметр доступный
        * **По электронной почте** отправляет сообщение электронной почты с пользователем код toohello настроенного адрес электронной почты для проверки подлинности
        * **Мобильный телефон** дает hello tooreceive Выбор пользователя hello вызов или текста с tootheir кода задан номер мобильного телефона
        * **Рабочий телефон** настроенное пользователем hello вызовов с tootheir код номер рабочего телефона
        * **Вопросы безопасности** требует toochoose
            * Число вопросов, необходимое tooregister: hello минимум для успешной регистрации, то есть пользователь может Выбор tooanswer дополнительные toocreate пул вопросы toopull из. Этот параметр может принимать значения от 3 до 5 и должен быть больше или равен toohello количество необходимых tooreset вопросы.
                * Можно добавить пользовательские вопросы, нажатие кнопки «Custom» hello, когда выбор секретных вопросов
            * Число вопросов tooreset - могут быть установлены из 3-5 вопросов toobe ответ на перед предоставлением toobe паролей пользователей сбросить или разблокирован.

4. Рекомендуется: **«Настройки»** позволяет toochange hello «Обратитесь к администратору» ссылку toopoint tooa страницы или адрес электронной почты определяется

5. Необязательно: hello **«Registration»** экрана предоставляет администраторам hello параметры для:
    * Требуется tooregister пользователей при входе
    * Количество дней, прежде чем пользователи задаваемые tooreconfirm данные проверки подлинности

6. Необязательно: hello **«Уведомления»** экран позволяет администраторам hello:
    * "Уведомлять пользователей о сбросе пароля";
    * "Уведомлять всех администраторов, если другие администраторы сбрасывают свои пароли".

**На этом этапе вы настроили SSPR для своего клиента Azure AD**. Можно остановить здесь или продолжить с tooconfigure синхронизации паролей tooan локального домена AD.

> [!NOTE]
> Тестируйте SSPR с использованием учетной записи пользователя, а не администратора, так как Майкрософт имеет строгие требования к проверке подлинности учетных записей Azure типа "администратор". Дополнительные сведения о политике паролей администратора hello см. наш [статье политики пароля](active-directory-passwords-policy.md#administrator-password-policy-differences).

## <a name="configure-synchronization-tooexisting-identity-source"></a>Настройка синхронизации tooexisting удостоверение источника

tooenable локальной tooAzure синхронизации удостоверений AD, должны tooinstall и настроить [Azure AD Connect](./connect/active-directory-aadconnect.md) на сервере в вашей организации. Это приложение обрабатывает синхронизации пользователей и группы из существующего клиента Azure AD tooyour источника удостоверения.

* [Обновление с DirSync или Azure AD Sync tooAzure AD Connect](./connect/active-directory-aadconnect-dirsync-deprecated.md)
* [Приступая к работе с Azure AD Connect с использованием стандартных параметров](./connect/active-directory-aadconnect-get-started-express.md)
* [Настройка обратной записи паролей](active-directory-passwords-writeback.md#configuring-password-writeback) tooyour локального каталога резервного toowrite пароли из Azure AD.

## <a name="disabling-self-service-password-reset"></a>Выключение самостоятельного сброса пароля

Отключение самостоятельного сброса пароля является просто открыть клиент Azure AD и происходит слишком**сброса пароля > свойства** > выберите **нет** под **самостоятельного сброса пароля Включен**

### <a name="learn-more"></a>Подробнее
Привет, следующие ссылки предоставляют дополнительную информацию об пароль с помощью Azure AD

* [**Licensing requirements for Azure AD self-service password reset**](active-directory-passwords-licensing.md) (Требования к лицензированию самостоятельного сброса пароля в Azure AD). Сведения о настройке лицензирования Azure AD.
* [**Данные** ](active-directory-passwords-data.md) — понять hello данные, которые не требуется и как она используется для управления паролями
* [**Развертывание** ](active-directory-passwords-best-practices.md) -планирование и развертывание SSPR tooyour пользователей с помощью hello рекомендации по следующему адресу
* [**Настройка** ](active-directory-passwords-customize.md) -настроить hello внешний вид и поведение hello SSPR взаимодействие с вашей компании.
* [**Политики и ограничения для паролей в Azure Active Directory**](active-directory-passwords-policy.md). Общие сведения и информация об установке политик паролей Azure AD.
* [**Reporting options for Azure AD password management**](active-directory-passwords-reporting.md) (Параметры отчетов для управления паролями Azure AD). Определяйте, кто и когда использовал функцию SSPR.
* [**Технические глубокое погружение** ](active-directory-passwords-how-it-works.md) -перейдите за занавесом toounderstand hello принцип работы
* [**Вопросы и ответы об управлении паролями**](active-directory-passwords-faq.md). Как? Почему? Что? Где? Кто? Когда? -Ответы tooquestions требуется, чтобы tooask
* [**Устранение неполадок** ](active-directory-passwords-troubleshoot.md) -Узнайте, как tooresolve распространенные проблемы, мы увидим с SSPR

## <a name="next-steps"></a>Дальнейшие действия

В этом кратком руководстве вы узнали, каким образом tooconfigure самостоятельный сброс пароля для пользователей. toocontinue toohello Azure toocomplete портала, выполните следующие действия hello ссылку toohello портала.

> [!div class="nextstepaction"]
> [Включение самостоятельного сброса пароля](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/PasswordReset)

