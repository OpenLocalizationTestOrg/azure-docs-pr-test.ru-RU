---
title: "Прокси приложения Azure AD в классическом портале hello aaaEnable | Документы Microsoft"
description: "Включите прокси приложения в окне приветствия классический портал Azure и установка hello соединителей для hello обратного прокси-сервера."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: c7186f98-dd80-4910-92a4-a7b8ff6272b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 8be9416a61993e1b46a20152e172c5133e54c0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-proxy-in-hello-classic-portal-and-download-connectors"></a>Включите прокси приложения в классическом портале hello и загрузите соединителей
В этой статье описывается tooenable действия hello прокси приложения Microsoft Azure AD для облачного каталога в Azure AD.

Если вы знакомы с что прокси-сервер приложения можно выполнить, Дополнительные сведения о [как tooprovide безопасный удаленный доступ tooon локальные приложения](active-directory-application-proxy-get-started.md).

## <a name="application-proxy-prerequisites"></a>Необходимые условия для прокси приложения
Прежде чем можно включить и использовать прокси-сервер приложения службы, необходимые toohave.

* [Подписка на Microsoft Azure AD Basic или Premium](active-directory-editions.md) , а также каталог Azure AD, для которого вы являетесь глобальным администратором.
* Сервер под управлением Windows Server 2012 R2 или 2016 г., на котором можно установить соединитель прокси приложения hello. Hello сервер отправляет запросы toohello службы прокси приложения в облаке hello, и он должен HTTP или HTTPS соединений toohello приложения, публикуемые.
  * Для tooyour — публикации приложений, этой машины должны быть присоединенных к домену в домене hello же AD как приложения hello, публикуемые. Дополнительные сведения см. в статье [Единый вход с помощью прокси приложения](active-directory-application-proxy-sso-using-kcd.md).
* Если ваша организация использует прокси-сервер toohello tooconnect серверов Интернета, чтение [работы с существующими локальными прокси-серверы](application-proxy-working-with-proxy-servers.md) подробные сведения о том, как tooconfigure их.

## <a name="open-your-ports"></a>Открытие портов

tooprepare среды для прокси приложения Azure AD, необходимо сначала центров данных tooAzure tooenable связи. Если путь hello установлен брандмауэр, убедитесь, что он открыт, что приветствия соединителя можно сделать HTTPS (TCP) запрашивает toohello прокси приложения.

1. Привет открыть следующие порты слишком**исходящих** трафика:

   | Номер порта | Как он используется |
   | --- | --- |
   | 80 | Загрузка отзыва сертификатов списки отзыва сертификатов при проверке сертификата SSL hello |
   | 443 | Все исходящей связи с прокси-служба приложения hello |

   Если брандмауэр инициирует трафик в соответствии с toooriginating пользователей, откройте эти порты для трафика, поступающего от служб Windows, работающих как сетевая служба.

   > [!IMPORTANT]
   > Таблица Hello отражает hello требованиях к портам для версии соединителя 1.5.132.0 и более поздних. Если по-прежнему имеется более старой версии соединителя, необходимо также tooenable hello следующие порты: 5671, 8080, 9090, 9091, 9350, 9352 и 10100 — 10120.
   >
   >Сведения об обновлении последнюю версию toohello соединителей см. в разделе [соединителей прокси приложения Azure понять AD](application-proxy-understand-connectors.md#automatic-updates).

2. Если брандмауэр или прокси-сервер разрешает DNS ведения списка разрешений, можно toomsappproxy.net белый список подключений и servicebus.windows.net. Если не требуется доступ toohello tooallow [диапазоны IP-центра обработки данных Azure](https://www.microsoft.com/download/details.aspx?id=41653), которой обновляются каждую неделю.

3. Используйте hello [Azure средство тестирования порты соединителя AD приложения прокси](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify, что соединитель доступ службы прокси приложения hello. Как минимум убедитесь, что у всех зеленой галочки области центральной части США hello и tooyou ближайший регион hello. Учитывайте также, что большее число зеленых флажков означает большую устойчивость.

## <a name="enable-application-proxy-in-azure-ad"></a>Включение прокси приложения в Azure AD
1. Войдите как администратор в hello [классический портал Azure](https://manage.windowsazure.com/).
2. Перейдите в каталог tooActive и выберите hello каталог, в котором нужно tooenable прокси-сервера приложения.

    ![Active Directory — значок](./media/active-directory-application-proxy-enable/ad_icon.png)
3. Выберите **Настройка** веб-странице directory hello и прокрутите вниз слишком**прокси приложения**.
4. Переключить **включить службы прокси приложения для этого каталога** слишком**включено**.

    ![Включение прокси приложения](./media/active-directory-application-proxy-enable/app_proxy_enable.png)
5. Выберите **Скачать сейчас**. Hello **Azure AD загрузка приложения для прокси-сервера соединителя** открывается. Прочтите и примите условия лицензионного соглашения на приветствия и нажмите кнопку **загрузки** toosave hello MSI-файл (.exe) для соединителя hello.

## <a name="install-and-register-hello-connector"></a>Установите и зарегистрируйте соединитель hello
1. Запустите **AADApplicationProxyConnectorInstaller.exe** на сервере hello подготовлены соответствующим toohello необходимые компоненты.
2. Следуйте инструкциям мастера tooinstall hello в hello.
3. Во время установки, запрашиваемые tooregister hello соединителя с hello прокси приложения клиента Azure AD.

   * Укажите учетные данные глобального администратора Azure AD. Ваш клиент глобального администратора может отличаться от учетных данных Microsoft Azure.
   * Убедитесь, что администратор hello, который регистрирует соединитель hello находится в hello же каталоге, где вы включили hello прокси-сервер приложения службы. К примеру, если hello клиента домена contoso.com, Здравствуйте, администратор должен быть admin@contoso.com или другой псевдоним в этом домене.
   * Если **конфигурация усиленной безопасности Internet Explorer** задано слишком**на** на сервере hello hello экран регистрации может быть заблокирован. доступ tooallow hello инструкции в сообщении об ошибке hello. Убедитесь, что конфигурация усиленной безопасности Internet Explorer отключена.
   * Если не удается зарегистрировать соединитель, см. сведения в статье [Устранение неполадок прокси-сервера приложений](active-directory-application-proxy-troubleshoot.md).  
4. После завершения установки hello две новых службы добавляются tooyour сервера:

   * **Соединитель прокси приложения Microsoft AAD** обеспечивает возможность подключения.

     * **Средство обновления соединителя прокси приложения Microsoft AAD** выполняет роль службы автоматического обновления. Периодически проверяет новые версии соединителя hello и обновляет hello соединителя, при необходимости.

     ![Службы соединителей прокси приложения — снимок экрана](./media/active-directory-application-proxy-enable/app_proxy_services.png)
5. Нажмите кнопку **Готово** hello в окне в установки.

Сведения о соединителях см. в статье [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md) (Сведения о соединителях прокси приложения Azure AD).

Чтобы обеспечить высокий уровень доступности, разверните как минимум два соединителя. toodeploy несколько соединителей, повторите шаги 2 и 3. Каждый соединитель необходимо зарегистрировать отдельно.

Если toouninstall hello соединителя, удалите службу соединителя hello и hello обновления. Перезапустите службу hello remove toofully компьютера.

## <a name="next-steps"></a>Дальнейшие действия
Теперь вы готовы слишком[публикации приложений с помощью прокси приложения](active-directory-application-proxy-publish.md).

При наличии приложений, которые находятся в отдельных сетях или в разных местах, можно использовать разные соединители tooorganize групп hello соединителя на логические единицы. См. дополнительные сведения о [работе с соединителями прокси приложения](active-directory-application-proxy-connectors.md).
