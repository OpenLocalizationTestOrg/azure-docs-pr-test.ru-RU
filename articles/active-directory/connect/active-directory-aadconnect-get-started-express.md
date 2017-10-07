---
title: "Azure AD Connect: приступая к работе с использованием стандартных параметров | Документация Майкрософт"
description: "Узнайте, как toodownload, установите и запустите мастер установки hello для Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: curtand
ms.assetid: b6ce45fd-554d-4f4d-95d1-47996d561c9f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 79f796fa7738b85e9236e856bddb529379f60390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-ad-connect-using-express-settings"></a>Приступая к работе с Azure AD Connect с использованием стандартных параметров
**Стандартные параметры** Azure AD Connect применяются, если вы используете для проверки подлинности топологию с одним лесом и [синхронизацию паролей](active-directory-aadconnectsync-implement-password-synchronization.md). **Стандартные параметры** является параметром по умолчанию hello и используется для наиболее часто развертывается hello сценария. Вы являются только несколько щелчков короткий дальней tooextend облако toohello локального каталога.

Прежде чем начать установку Azure AD Connect, убедитесь, что слишком[скачать Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) и завершения hello предварительные шаги в [Azure AD Connect: оборудование и компоненты](active-directory-aadconnect-prerequisites.md).

Если стандартные параметры не соответствуют топологии, см. сведения о других сценариях в [дополнительной документации](#related-documentation).

## <a name="express-installation-of-azure-ad-connect"></a>Экспресс-установка Azure AD Connect
Можно увидеть следующие действия в действии hello [видео](#videos) раздела.

1. Войдите в качестве локального администратора сервера toohello которых надо tooinstall Azure AD Connect на. Это следует делать на сервере hello нужно toobe hello синхронизации сервера.
2. Дважды щелкните tooand перейдите **AzureADConnect.msi**.
3. На экране приветствия hello выберите toohello agreeing окно приветствия, условия лицензии и нажмите кнопку **Продолжить**.  
4. На экране параметров hello Express, нажмите кнопку **использовать стандартные параметры**.  
   ![Добро пожаловать tooAzure AD Connect](./media/active-directory-aadconnect-get-started-express/express.png)
5. На экране приветствия tooAzure AD Connect введите hello пользователя и пароль для глобального администратора для Azure AD. Щелкните **Далее**.  
   ![Подключение tooAzure AD](./media/active-directory-aadconnect-get-started-express/connectaad.png) Если возникнет ошибка и возникают проблемы с подключением, затем в разделе [Устранение неполадок подключения к](active-directory-aadconnect-troubleshoot-connectivity.md).
6. На экране приветствия Connect tooAD доменных служб Active Directory введите hello имя пользователя и пароль для учетной записи администратора предприятия. Можно ввести часть домена hello в формате NetBios или полное доменное имя, то есть FABRIKAM\administrator или fabrikam.com\administrator. Щелкните **Далее**.  
   ![Подключение tooAD доменных служб Active Directory](./media/active-directory-aadconnect-get-started-express/connectad.png)
7. Hello [ **конфигурации входа в Azure AD** ](active-directory-aadconnect-user-signin.md#azure-ad-sign-in-configuration) странице отображаются только если вы не прошли [проверить домены](../active-directory-add-domain.md) в hello [необходимых компонентов](active-directory-aadconnect-prerequisites.md).
   ![Непроверенные домены](./media/active-directory-aadconnect-get-started-express/unverifieddomain.png)  
   Если отобразилась эта страница, просмотрите все домены с пометкой **Не добавлено** и **Не проверено**. Убедитесь, что используемые домены прошли проверку в Azure AD. Щелкните символ hello обновления, когда вы проверили доменов.
8. На экране приветствия готов tooconfigure, нажмите кнопку **установить**.
   * При необходимости на странице готовности tooconfigure hello, можно отменить выбор hello **запуск процесса синхронизации hello сразу же после завершения настройки** флажок. Следует снять этот флажок, если требуется дополнительная настройка toodo, [фильтрации](active-directory-aadconnectsync-configure-filtering.md). Если вы отмените выбор этого параметра, hello мастер настраивает синхронизации, но оставляет планировщика hello отключена. Он не работает, пока не будет включена вручную путем [повторный запуск мастера установки hello](active-directory-aadconnectsync-installation-wizard.md).
   * Если у вас есть Exchange в локальной службе Active Directory, то также имеется параметр tooenable [ **гибридное развертывание Exchange**](https://technet.microsoft.com/library/jj200581.aspx). Включите этот параметр, если план toohave почтовые ящики Exchange как в облаке hello и локально в hello же время.
     ![Все готово tooconfigure Azure AD Connect](./media/active-directory-aadconnect-get-started-express/readytoconfigure.png)
9. После завершения установки hello нажмите **выхода**.
10. После завершения установки hello, выйдите из системы и войти снова, прежде чем использовать диспетчер службы синхронизации или редактор правил синхронизации.

## <a name="videos"></a>Видеоролики
Видео об использовании hello экспресс-установки см.:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player]
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
Теперь, после установки Azure AD Connect можно [проверка установки hello и назначить лицензии](active-directory-aadconnect-whats-next.md).

Дополнительные сведения об этих функциях, которые были включены с установкой hello: [автоматическое обновление](active-directory-aadconnect-feature-automatic-upgrade.md), [избежать случайного удаления](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), и [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Дополнительные сведения об этих основных разделов: [планировщик и как синхронизировать tootrigger](active-directory-aadconnectsync-feature-scheduler.md).

Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).

## <a name="related-documentation"></a>Дополнительная документация
| Раздел |
| --- | --- |
| Обзор Azure AD Connect |
| Установка с помощью настроенных параметров |
| Обновление из DirSync |
| Учетные записи, используемые для установки |

