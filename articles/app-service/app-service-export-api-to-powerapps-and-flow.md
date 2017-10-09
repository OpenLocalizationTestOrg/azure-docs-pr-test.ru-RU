---
title: "aaaExporting tooPowerApps API, размещенных в Azure и Microsoft Flow | Документы Microsoft"
description: "Обзор размещения tooexpose API в tooPowerApps службы приложений и Microsoft Flow"
services: app-service
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/20/2017
ms.author: mahender
ms.openlocfilehash: 285b6efa3af5b0feac1ee2f617c0dc56dc3fd198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-an-azure-hosted-api-toopowerapps-and-microsoft-flow"></a>Экспорт tooPowerApps API, размещенных в Azure и Microsoft Flow

## <a name="creating-custom-connectors-for-powerapps-and-microsoft-flow"></a>Создание настраиваемых соединителей для PowerApps и Microsoft Flow

[PowerApps](https://powerapps.com) — это служба, для создания и использования пользовательских бизнес-приложений, которые подключаются tooyour данных и работы на разных платформах. [Microsoft Flow](https://flow.microsoft.com) позволяет легко tooautomate рабочие процессы и бизнес-процессов между избранных приложений и служб. PowerApps и Microsoft Flow имеют различные встроенные соединители toodata источников, таких как Office 365, Dynamics 365, Salesforce и многое другое. Тем не менее пользователи также должны источников данных может tooleverage toobe и API-интерфейсов построенных по своей организации.

Аналогичным образом разработчики, которым требуется tooexpose их интерфейсов API из нескольких широко внутри hello организации может потребоваться toomake своих tooPowerApps доступные интерфейсы API и Microsoft Flow пользователей. В этом разделе показано, как tooexpose API-Интерфейс, созданного с помощью службы приложений Azure или Azure функции tooPowerApps и Microsoft Flow. [Служба приложений Azure](https://azure.microsoft.com/services/app-service/) — это предложение платформа как служба, позволяющая разработчикам tooquickly и легко web корпоративного уровня сборки, мобильных устройств и приложения API. [Функции Azure](https://azure.microsoft.com/services/functions/) — это решение на основе событий без сервера вычислений, позволяющий tooquickly автор код, который можно реагировать tooother части системы и масштабировать по требованию.

toolearn Дополнительные сведения об этих служб, см.:
- [Guided Learning for PowerApps](https://powerapps.microsoft.com/guided-learning/learning-introducing-powerapps/) (Пошаговое изучение PowerApps) 
- [Интерактивное обучение Microsoft Flow](https://flow.microsoft.com/guided-learning/learning-introducing-flow/)
- [Что такое служба приложений?](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- [Обзор функций Azure](https://docs.microsoft.com/azure/azure-functions/functions-overview)

## <a name="sharing-an-api-definition"></a>Предоставление общего доступа к определению API

API-интерфейсы часто описываются с помощью [OpenAPI документа](https://www.openapis.org/) (иногда называется tooas документа «Swagger»). Содержит все сведения hello какие операции доступны и структуру данных hello. С помощью PowerApps и Microsoft Flow можно создавать настраиваемые соединители для любого документа OpenAPI 2.0. После создания пользовательского соединителя, он может использоваться в hello точно так же, как один из hello встроенные соединители и можно быстро интегрировать в приложения.

Служба приложений Azure и Функции Azure имеют [встроенную поддержку](https://docs.microsoft.com/azure/app-service-api/app-service-api-metadata) создания и размещения документа OpenAPI, а также управления им. В порядке toocreate пользовательский соединитель веб-приложений, мобильных устройств, API или функции приложения, PowerApps и потока должны toobe получает копию определения hello.

> [!NOTE]
> Поскольку используется копия hello определения API PowerApps и Microsoft Flow не будет уведомлен немедленно обновления или приложения toohello критические изменения. Если доступна новая версия hello API доступны, эти шаги необходимо выполнить для hello новой версии. 

tooprovide PowerApps и Microsoft Flow с размещенной hello определение API для приложения, выполните следующие действия.

1. Откройте hello [портала Azure](https://portal.azure.com) и перейдите tooyour приложения служб приложений или функций Azure.

    При использовании службы приложений Azure, выберите **определения API** из списка параметров hello. 
    
    При использовании Функции Azure, щелкните приложение-функцию и выберите **Platform features** (Функции платформы), а затем — **Определение API**. Можно также выбрать tooopen hello **определения API (Предварительная версия)** вместо вкладки.

2. Если имеется определение API вы увидите **Экспорт tooPowerApps + Microsoft Flow** кнопки. Нажмите кнопку toobegin hello в ходе экспорта.

3. Выберите hello **режим экспорта**. Определяет действия hello, вам потребуется toofollow toocreate соединителя. Службы приложений предлагают два варианта предоставления PowerApps и Microsoft Flow с определением API:

    **Express** позволяет создавать пользовательский соединитель hello из внутри hello портал Azure. Он требует этот hello текущей вошедшего в систему пользователь имеет разрешение toocreate соединителей в целевой среде hello. Это рекомендованный подход, при этом требование hello. Если в этом режиме выполните hello [Express экспорта](#express) приведенным ниже инструкциям.

    **Вручную** позволяет экспортировать копию определения hello API, которые можно импортировать с помощью приветствия PowerApps и Microsoft Flow порталов. Это рекомендованный подход, если hello Azure пользователя и hello пользователя с помощью соединителей toocreate разрешение — разные люди или hello соединитель должен toobe создан другим клиентом hello. Если в этом режиме выполните hello [вручную экспорта и импорта](#manual) приведенным ниже инструкциям.

<a name="express"></a>
## <a name="express-export"></a>Экспресс экспорт

В этом разделе вы создадите новый пользовательский соединитель из внутри hello портал Azure. Вы должны войти в toowhich hello клиента нужно tooexport и toocreate разрешение необходимо иметь пользовательский соединитель в целевой среде hello.

1. Выберите среду hello, в котором вы хотите toocreate hello соединителя. Затем введите имя для вашего настраиваемого соединителя.

2. Если определение API содержит какие-либо параметры безопасности, они будут вызваны на шаге 2. При необходимости предоставить hello безопасности сведения о конфигурации требуется toogrant пользователи обращаются к tooyour API. Дополнительные сведения см. в разделе [Проверка подлинности](#auth) ниже. 

3. Нажмите кнопку **ОК** toocreate пользовательского соединителя.


<a name="manual"></a>
## <a name="manual-export-and-import"></a>Экспорт и импорт вручную

В порядке toocreate пользовательский соединитель веб-приложений, мобильных устройств, API или функции приложения потребуется два шага:

1. [Получение определения API hello из приложения службы или функции Azure](#export)
2. [Импорт определения API hello в PowerApps и Microsoft Flow](#import)

Это возможно, эти два действия необходимость toobe сопровождающими отдельных лиц в организации, как данный пользователь может не иметь разрешение tooperform обоих этих действий. В этом случае разработчиком, toohello доступа участника службы приложений или функций Azure приложения потребуется определение hello API tooobtain (один JSON-файл) или tooit ссылку. Затем необходимо tooprovide, определение tooa PowerApps и Microsoft Flow пользователем. Владельца этого можно использовать пользовательский соединитель toocreate метаданных hello hello.

<a name="export"></a>
### <a name="retrieving-hello-api-definition-from-app-service-or-azure-functions"></a>Получение определения API hello из приложения службы или функции Azure

В этом разделе будет экспортировать hello определение API для API службы приложения, toobe, используемых в дальнейшем в портал PowerApps и Microsoft Flow hello.

1. Вы можете tooeither **загрузить определение hello API** или **получите ссылку**. Независимости от выбранного варианта, в следующем разделе hello будет отображено hello результат. Выберите один из следующих вариантов и следуйте инструкциям hello.
 
2. Если определение API содержит какие-либо параметры безопасности, они будут вызваны на шаге 2. Во время импорта PowerApps и Microsoft Flow обнаружат их и предложат ввести сведения о безопасности. Соберите hello определения связанных tooeach учетные данные для использования в следующем разделе hello. Дополнительные сведения см. в разделе [Проверка подлинности](#auth) ниже. 

<a name="import"></a>
### <a name="importing-hello-api-definition-into-powerapps-and-microsoft-flow"></a>Импорт определения API hello в PowerApps и Microsoft Flow

В этом разделе вы создадите пользовательский соединитель в PowerApps и Microsoft Flow с использованием определения hello API, полученный ранее. Настраиваемые соединители распределяются между двумя службами hello, поэтому требуется только один раз определение hello tooimport. Дополнительные сведения о настраиваемых соединителях см. в статьях [зарегистрировать и использовать настраиваемые соединители в PowerApps] и [зарегистрировать и использовать настраиваемые соединители в Microsoft Flow].

1. Откройте hello [Powerapps веб-портале](https://web.powerapps.com) или hello [веб-портале Microsoft Flow](https://flow.microsoft.com/)и выполните вход. 

2. Щелкните hello **параметры** hello верхнем правом углу страницы hello и выберите кнопку (значок шестеренки hello) **соединители настраиваемый**. 

3. Щелкните **Создать настраиваемый соединитель**.

4. На hello **Общие** вкладку, задайте имя для API и затем передать определение OpenAPI hello или вставьте URL-адрес метаданных hello. Нажмите кнопку **Продолжить**.

4. На hello **безопасности** вкладку, если tooprovide запрашиваемые сведения о проверке подлинности, введите значения hello, полученный в предыдущем разделе hello. Если нет, продолжить toohello следующий шаг.

5. На hello **определения** вкладку, все операции hello, определенной в файле OpenAPI заполняются автоматически. Если определены все необходимые операции, можно перейти toohello следующий шаг. Если нет, вы можете добавить и изменить операции здесь.

6. Нажмите кнопку **Создать соединитель**. Вызовы API tootest перейдите toohello следующий шаг.

7. На hello **тест** создать соединение, выберите tootest операции и введите все данные, необходимые операции hello.

8. Нажмите кнопку **Тестировать операцию**.


<a name="auth"></a>
## <a name="authentication"></a>Аутентификация

PowerApps и Microsoft Flow поддерживают коллекцию поставщиков удостоверений, которые могут быть используется toolog пользователи вашего пользовательского соединителя. Если для API требуется проверка подлинности, это определение должно быть записано в виде _определения безопасности_ в документе OpenAPI. Во время экспорта вам потребуется tooprovide значения конфигурации, которые предоставляют PowerApps Microsoft Flow tooperform входа действия.

В этом разделе описаны типы проверки подлинности hello, поддерживаемыми hello express потока: ключ API, Azure Active Directory и универсального OAuth 2.0. Полный список поставщиков и каждый требует учетные данные hello см. в разделе [зарегистрировать и использовать настраиваемые соединители в PowerApps] и [зарегистрировать и использовать настраиваемые соединители в Microsoft Flow].

### <a name="api-key"></a>Ключ API
При использовании этой схемы безопасности пользователи hello вашего соединителя будут запрашиваемые tooprovide hello ключ при создании соединения. Чтобы обеспечить toohelp имя ключа API их знать, какой ключ необходим. Для функций Azure это обычно будет один из разделов узла hello, охватывающие несколько функций в приложение функции hello.

### <a name="azure-active-directory"></a>Azure Active Directory
При настройке пользовательского соединителя, требующий входа AAD, требуются два регистрации AAD приложения: один toomodel hello внутренних API и один соединитель hello toomodel в PowerApps и потока.

API должны быть настроенный toowork с первой регистрации hello, и это будет уже возложить при использовании hello [приложения службы проверки подлинности и авторизации](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication) компонентов.

Будет иметь toomanually создать второй регистрацию hello для соединителя hello, используя hello шаги, описанные в [Добавление приложения AAD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-an-application). Hello регистрации требуется делегировать toohave доступа tooyour API и URL-адрес ответа из `https://msmanaged-na.consent.azure-apim.net/redirect`. См. в разделе [в этом примере](
https://powerapps.microsoft.com/tutorials/customapi-azure-resource-manager-tutorial/) для получения дополнительных сведений, заменив API для hello диспетчера ресурсов Azure.

требуются следующие значения конфигурации Hello.
- **Идентификатор клиента** -hello идентификатор клиента для соединителя регистрации AAD
- **Секрет клиента** -секрет клиента hello вашего соединителя регистрации AAD
- **URL-адрес входа** - hello базовый URL-адрес для AAD. В общедоступной версии Azure это, как правило, будет `https://login.windows.net`.
- **Идентификатор клиента** -hello идентификатор hello toobe клиента, используемый для входа hello. Это должен быть «общими» или hello идентификатор hello клиента, в которой hello создается соединитель.
- **URL-адрес ресурса** -hello ресурса URL-адрес регистрации AAD внутренних API

> [!IMPORTANT]
> Если другим лицам требуется импортировать определения hello API в PowerApps и Microsoft Flow как часть потока вручную hello, вам потребуется tooprovide с hello клиента идентификатор и секрет клиента **регистрации соединителя hello**, а также как hello ресурса URL-адрес вашего API. Обеспечьте безопасное управление этими секретами. **Не используйте учетные данные безопасности hello hello сам интерфейс API.**

### <a name="generic-oauth-20"></a>Универсальная OAuth 2.0
Общая поддержка OAuth 2.0 Hello позволяет toointegrate с поставщиками OAuth 2.0. Это позволяет toobring в любой пользовательский поставщик, который изначально не поддерживается.

требуются следующие значения конфигурации Hello.
- **Идентификатор клиента** -hello идентификатор клиента OAuth 2.0
- **Секрет клиента** -секрет клиента OAuth 2.0 hello
- **URL-адрес авторизации** -hello URL-адрес авторизации OAuth 2.0
- **Токен URL-адрес** -hello URL-адрес токена OAuth 2.0
- **Обновить URL-адрес** -hello URL-адрес обновления OAuth 2.0



[зарегистрировать и использовать настраиваемые соединители в PowerApps]: https://powerapps.microsoft.com/tutorials/register-custom-api/
[зарегистрировать и использовать настраиваемые соединители в Microsoft Flow]: https://flow.microsoft.com/documentation/register-custom-api/
