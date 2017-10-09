---
title: "aaaAzure Active Directory подключения работоспособности часто задаваемые вопросы — Azure | Документы Microsoft"
description: "Эта статья содержит ответы на часто задаваемые вопросы об Azure AD Connect Health. Вопросы и ответы рассматриваются вопросы об использовании службы hello, включая выставление счетов модели, возможности, ограничения и поддержки hello."
services: active-directory
documentationcenter: 
author: billmath
manager: samueld
editor: curtand
ms.assetid: f1b851aa-54d7-4cb4-8f5c-60680e2ce866
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 3f15d9e9b557b09ef74ceff85806579dd51f2412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-frequently-asked-questions"></a>Часто задаваемые вопросы об Azure AD Connect Health
Эта статья содержит ответы toofrequently, задаваемые вопросы (FAQ) о работоспособности подключения Azure Active Directory (Azure AD). Эти вопросы и ответы о охватывает вопросы о как toouse hello службы, включая выставление счетов модели, возможности, ограничения и поддержки hello.

## <a name="general-questions"></a>Общие вопросы
**Вопрос. Я управляю несколькими каталогами Azure AD. Как переключаться toohello ту, которая имеет Azure Active Directory Premium?**

tooswitch между различными Azure AD клиентам, выберите hello в настоящее время выполнившего вход **имя пользователя** на hello в правом верхнем углу, а затем выберите соответствующую учетную запись hello. Если hello учетной записи нет в списке, выберите **выйдите из системы**, а затем использовать учетные данные глобального администратора hello hello каталога с Azure Active Directory Premium toosign в.

**Вопрос. Какая версия ролей удостоверений поддерживается в Azure AD Connect Health?**

Hello следующей таблице перечислены роли, hello и поддерживаемые версии операционной системы.

|Роль| Версия операционной системы|
|--|--|
|Службы федерации Active Directory (AD FS)| <ul> <li> Windows Server 2008 R2 </li><li> Windows Server 2012  </li> <li>Windows Server 2012 R2 </li> <li> Windows Server 2016  </li> </ul>|
|Azure AD Connect | Версия 1.0.9125 или более поздняя|
|Доменные службы Active Directory (AD DS)| <ul> <li> Windows Server 2008 R2 </li><li> Windows Server 2012  </li> <li>Windows Server 2012 R2 </li> <li> Windows Server 2016  </li> </ul>|

Обратите внимание, что hello возможностей, предоставляемых службой hello может отличаться на основе роли hello и hello операционной системы. Другими словами все функции hello не может быть доступен для всех версий операционной системы. В разделе описания характеристик hello подробные сведения.

**В выполните. сколько лицензий требуется toomonitor инфраструктуры?**

* Hello первый агент работоспособности подключения требуется по крайней мере одна лицензия Azure AD Premium.
* Для каждого дополнительного регистрируемого агента нужно еще 25 лицензий Azure AD Premium.
* Количество агентов — эквивалент toohello общее количество агентов, зарегистрированных для всех отслеживаемых ролей (службы федерации Active Directory, Azure AD Connect и AD DS).

Сведения о лицензировании также найти на hello [странице цен Azure AD](https://aka.ms/aadpricing).

Пример:

| Зарегистрированные агенты | Необходимые лицензии | Пример конфигурации мониторинга |
| ------ | --------------- | --- |
| 1 | 1 | 1 сервер Azure AD Connect |
| 2 | 26| 1 сервер Azure AD Connect и 1 контроллер домена |
| 3 | 51 | 1 сервер служб федерации Active Directory (AD FS), 1 прокси-сервер AD FS и 1 контроллер домена |
| 4. | 76 | 1 сервер AD FS, 1 прокси-сервер AD FS и 2 контроллера домена |
| 5 | 101 | 1 сервер Azure AD Connect, 1 сервер AD FS, 1 прокси-сервер AD FS и 2 контроллера домена |


## <a name="installation-questions"></a>Вопросы, связанные с установкой

**Вопрос. Какова hello влияния установки hello Azure AD Connect Health Agent на отдельных серверах?**

Hello влияния установки серверов hello Microsoft Azure AD Connect Health Agent, AD FS, веб-приложений прокси-сервера, серверы Azure AD Connect (sync), контроллеры домена сводится к минимуму с уважением toohello ЦП, потребление памяти, пропускную способность сети и хранилища.

Hello следующие цифры являются приближенными:

* Загрузка ЦП: увеличение примерно на 1–5 %.
* Потребление памяти: % too10 hello общего объема памяти системы.

> [!NOTE]
> Если hello агенту не удается связаться с Azure, агент hello хранит данные hello локально для установленного максимального предела. агент Hello перезаписывает hello «кэшированные» данные по принципу «наиболее давно обслужен».
>
>

* Хранилище локального буфера для агентов Azure AD Connect Health: около 20 МБ.
* Для серверов AD FS рекомендуется обеспечить место на диске 1 024 МБ (1 ГБ) для канала аудита AD FS hello tooprocess агенты Azure AD Connect работоспособности всех данных аудита hello, прежде чем он будет переопределен.

**Вопрос. будут у меня tooreboot Мои серверы во время установки hello агенты hello Azure AD Connect Health?**

Нет. Hello установки агентов hello tooreboot hello сервера не требуется. Тем не менее некоторые обязательные шаги установки может потребоваться перезагрузка сервера hello.

Например, при установке платформы .NET Framework 4.5 на Windows Server 2008 R2 необходима перезагрузка сервера.

**Вопрос. Работает ли Azure AD Connect Health через сквозной прокси-сервер HTTP?**

Да. Для текущих операций можно настроить агент работоспособности toouse hello HTTP прокси-сервера tooforward исходящих HTTP-запросов.
Узнайте больше о [настройке прокси-сервера HTTP для агентов работоспособности](active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy).

Если во время регистрации агента требуется tooconfigure учетную запись-посредник, может потребоваться toomodify параметры прокси-сервера Internet Explorer заранее.

1. Откройте Internet Explorer и последовательно выберите **Сервис** > **Свойства браузера** > **Подключения** > **Настройка параметров локальной сети**.
2. Установите флажок **Использовать прокси-сервер для локальной сети**.
3. Выберите **Дополнительно**, если для HTTP и HTTPS используются различные порты прокси-сервера.

**Вопрос. при подключении tooHTTP прокси является обычной проверки подлинности поддержки Azure AD Connect Health?**

Нет. Механизм toospecify имя пользователя и пароль для обычной проверки подлинности в настоящее время не поддерживается.

**Вопрос. как сделать порты брандмауэра требуется tooopen toowork hello Azure AD Connect Health Agent?**

В разделе hello [раздел "требования"](active-directory-aadconnect-health-agent-install.md#requirements) список hello порты брандмауэра и других требований к подключению.

**Вопрос. Почему я вижу двух серверов с hello точно такое же имя в портале hello Azure AD Connect Health**

При удалении агента с сервера, сервера hello не удаляется автоматически с портала Azure AD Connect Health hello. Если вы вручную удалить агент с сервера или удалить сам сервер hello, необходимо toomanually удаления записи сервера hello из портала hello Azure AD Connect Health.

Может пересоздать сервер или создать новый сервер с hello и те же сведения (такие как имя компьютера). Если вы установили агент hello на новом сервере hello hello уже зарегистрированного сервера не была удалена из портала hello Azure AD Connect Health, может появиться две записи с hello таким же именем.

В этом случае вручную удалите запись hello, к которому относится toohello старую версию сервера. Hello данных для этого сервера должно быть устаревшими.

## <a name="health-agent-registration-and-data-freshness"></a>Регистрация агента работоспособности и актуальность данных

**Вопрос. что такое Общие причины сбоев регистрации агента работоспособности hello и способ устранения неполадок?**

Hello работоспособности может произойти сбой агента tooregister из-за toohello следующие возможные причины:

* Hello агенту не удается связаться с конечными точками hello требуется, так как трафик блокируется брандмауэром. Это особенно часто происходит на прокси-серверах веб-приложений. Убедитесь, что разрешены конечные точки toohello необходимые исходящей связи и порты. В разделе hello [раздел "требования"](active-directory-aadconnect-health-agent-install.md#requirements) подробные сведения.
* Исходящая связь является подвергается tooan проверку SSL на уровне сети hello. В этом случае сертификат hello hello агент использует toobe заменяется hello проверки сервера на сущность, что сбой hello действия toocomplete hello агента регистрации.
* Hello пользователь не имеет доступа к регистрации hello tooperform hello агента. По умолчанию доступ имеют глобальные администраторы. Можно использовать [управления доступом на основе ролей](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) toodelegate доступа tooother пользователей.

**Вопрос. я хочу начало оповещения, «служба работоспособности данные не копирование toodate.» Как решить проблему hello**

Azure AD Connect Health приводит к возникновению ошибки hello предупреждение, когда он получает все точки данных hello от сервера hello в hello последние два часа. Это оповещение может быть создано по нескольким причинам.

* Hello агенту не удается связаться с конечными точками hello требуется, так как трафик блокируется брандмауэром. Это особенно часто происходит на прокси-серверах веб-приложений. Убедитесь, что разрешены исходящей связи toohello необходимые конечные точки и порты. В разделе hello [раздел "требования"](active-directory-aadconnect-health-agent-install.md#requirements) подробные сведения.
* Исходящая связь является подвергается tooan проверку SSL на уровне сети hello. В этом случае сертификат hello hello агент использует toobe заменяется hello проверки сервера на сущность, что hello процесс завершается ошибкой службы Azure AD Connect Health toohello tooupload данных.
* Можно использовать команду подключения hello, встроенные в hello агента. [Подробная информация](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service).
* агенты Hello также поддерживает исходящие подключения через прокси-сервер без проверки подлинности HTTP. [Подробная информация](active-directory-aadconnect-health-agent-install.md##configure-azure-ad-connect-health-agents-to-use-http-proxy).

## <a name="operations-questions"></a>Вопросы, связанные с работой
**Вопрос. необходимо tooenable аудит на прокси-серверы приложения hello web?**

Нет, аудит не обязательно toobe включено на веб-приложения hello прокси-серверах.

**Как разрешаются оповещения Azure AD Connect Health?**

Оповещения Azure AD Connect Health разрешаются при условии успешного завершения. Агенты Azure AD Connect работоспособности обнаруживать и hello успех условия toohello служба отчетов периодически. Для нескольких оповещений подавление hello основан на времени. Другими словами Если hello аналогичное условие ошибки не возникает в 72 часов с момента выдачи оповещения, hello предупреждение автоматически разрешается.

**Вопрос. я хочу начало оповещения, «тестовый запрос проверки подлинности (искусственной транзакции) Ошибка tooobtain маркер». Как решить проблему hello**

Это предупреждение создается в Azure AD Connect Health для AD FS, сбое tooobtain маркер hello работоспособности агента, установленного на сервере служб AD FS в рамках искусственных транзакций, инициированных hello агент работоспособности. Агент работоспособности Hello использует hello контексте локальной системы и пытается tooget маркер для себя проверяющей стороны. Это tooensure универсальный тест, который AD FS находится в состоянии выдачи маркеров.

Чаще всего этот тест не пройден, так как имя фермы AD FS hello не удается tooresolve hello агент работоспособности. Это может произойти, если серверы hello AD FS позади подсистем балансировки нагрузки сети и hello запрос возвращает инициировать из узла, который находится за подсистемой балансировки нагрузки hello (как противоположность tooa регулярного клиента, который закрывает hello балансировки нагрузки). Это можно исправить путем обновления файла hello «узлы», находящийся в разделе «C:\Windows\System32\drivers\etc» hello tooinclude IP-адрес сервера AD FS hello или IP-адрес замыкания на себя (127.0.0.1) для имени фермы AD FS hello (например, sts.contoso.com). Добавление файла hello узла будет сокращенным hello сетевой вызов, позволяя тем самым hello агент работоспособности tooget hello маркер.

**Вопрос. я получил сообщение электронной почты о том, что для последних ransomeware атак hello не исправить компьютерам. Почему мне пришло это письмо?**

Служба Azure AD Connect Health сканирование всех hello установленному машины он отслеживает tooensure hello необходимые исправления. сообщение Hello отправлено администраторов клиента toohello Если по крайней мере один компьютер не имеет важные исправления hello. Здравствуйте, следуя логики был используется toomake это определение.
1. Найти все исправления hello, установленных на компьютере hello.
2. Флажок, если хотя бы один из hello исправления из hello списке присутствует.
3. Если Да, hello машина защищена. В противном случае hello компьютере находятся под угрозой атаки hello.

Можно использовать следующие tooperform сценария PowerShell hello эту проверку вручную. Он реализует hello выше логику.

```
Function CheckForMS17-010 ()
{
    $hotfixes = "KB3205409", "KB3210720", "KB3210721", "KB3212646", "KB3213986", "KB4012212", "KB4012213", "KB4012214", "KB4012215", "KB4012216", "KB4012217", "KB4012218", "KB4012220", "KB4012598", "KB4012606", "KB4013198", "KB4013389", "KB4013429", "KB4015217", "KB4015438", "KB4015546", "KB4015547", "KB4015548", "KB4015549", "KB4015550", "KB4015551", "KB4015552", "KB4015553", "KB4015554", "KB4016635", "KB4019213", "KB4019214", "KB4019215", "KB4019216", "KB4019263", "KB4019264", "KB4019472", "KB4015221", "KB4019474", "KB4015219", "KB4019473"

    #checks hello computer it's run on if any of hello listed hotfixes are present
    $hotfix = Get-HotFix -ComputerName $env:computername | Where-Object {$hotfixes -contains $_.HotfixID} | Select-Object -property "HotFixID"

    #confirms whether hotfix is found or not
    if (Get-HotFix | Where-Object {$hotfixes -contains $_.HotfixID})
    {
        "Found HotFix: " + $hotfix.HotFixID
    } else {
        "Didn't Find HotFix"
    }
}

CheckForMS17-010

```



## <a name="related-links"></a>Связанные ссылки
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Установка агента Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Операции Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Использование Azure AD Connect Health с AD FS](active-directory-aadconnect-health-adfs.md)
* [Использование Azure AD Connect Health для синхронизации](active-directory-aadconnect-health-sync.md)
* [Using Azure AD Connect Health with AD DS (Использование Azure AD Connect Health с AD DS)](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health: история выпусков версий](active-directory-aadconnect-health-version-history.md)
