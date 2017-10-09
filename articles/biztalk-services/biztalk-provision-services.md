---
title: "aaaCreate служб Azure BizTalk в hello портал Azure | Документы Microsoft"
description: "Узнайте, как tooprovision или создание служб Azure BizTalk в hello портал Azure; MABS СЛУЖБЫ BIZTALK WINDOWS AZURE"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a>Создание службы BizTalk с помощью портала Azure hello

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> toosign в toohello портал Azure, требуется учетная запись Azure и подписку Azure. Если учетной записи нет, можно создать бесплатную пробную учетную запись всего за несколько минут. См. страницу [Бесплатная пробная версия Azure](http://go.microsoft.com/fwlink/p/?LinkID=239738).


## <a name="CreateService"></a>Создание службы BizTalk
В зависимости от hello выбранного выпуска могут быть доступны не все параметры службы BizTalk.

1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Hello нижней панели навигации, выберите **NEW**:  
   ![Выберите новую кнопку hello][NEWButton]
3. Выберите **Службы приложений** > **Служба BizTalk** > **Настраиваемое создание**:  
   ![Выбор элементов "Служба BizTalk" и "Настраиваемое создание"][NewBizTalkService]
4. Введите параметры hello службы BizTalk:
   
    <table border="1">
    <tr>
    <td><strong>Имя службы BizTalk</strong></td>
    <td>Можно ввести любое имя, но рекомендуется использовать конкретные имена. Некоторые примеры:<br/><br/>
    <em>mycompany</em>.biztalk.windows.net<br/>
    <em>mycompanymyapplication</em>.biztalk.windows.net<br/>
    <em>myapplication</em>.biztalk.windows.net<br/><br/>«. biztalk.windows.net» — имя автоматически добавлены toohello ввода. При этом создается URL-адреса, используемые tooaccess вашей BizTalk службы как <strong>https://<em>myapplication</em>. biztalk.windows.net</strong>.
    </td>
    </tr>
    <tr>
    <td><strong>Выпуск</strong></td>
    <td>Если на этапе тестирования или разработки hello выберите <strong>разработчика</strong>. На этапе производства hello, использовать hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">службы BizTalk: схема с выпусками</a> toodetermine Если <strong>Premium</strong>, <strong>Стандартная</strong>, или <strong>Basic</strong>является правильным выбором hello для бизнес-сценария.
    </td>
    </tr>
    <tr>
    <td><strong>Регион</strong></td>
    <td>Выделите службу BizTalk toohost hello географического региона.</td>
    </tr>
    <tr>
    <td><strong>URL-адрес домена</strong></td>
    <td><strong>Необязательно</strong>. По умолчанию используется URL-адрес домена hello <em>адрес YourBizTalkServiceName</em>. biztalk.windows.net. Можно также указать пользовательский домен. Например, если вы используете домен <em>contoso</em>, можно ввести следующее: <br/><br/>
    <em>MyCompany</em>.contoso.com<br/>
    <em>MyCompanyMyApplication</em>.contoso.com<br/>
    <em>MyApplication</em>.contoso.com<br/>
    <em>YourBizTalkServiceName</em>.contoso.com<br/>
    </td>
    </tr>
    </table>
Выберите стрелку hello.
5. Введите hello хранения и настройки базы данных:  <table border="1">
    <tr>
    <td><strong>Учетная запись хранения для мониторинга и архивации</strong></td>
    <td>Выберите существующую учетную запись хранения или параметр «Создать новую учетную запись хранения». <br/><br/>При создании новой учетной записи хранения, введите hello <strong>имя учетной записи хранения</strong>.</td>
    </tr>
    <tr>
    <td><strong>База данных отслеживания</strong></td>
    <td>Если используется существующая база данных SQL Azure, ее нельзя использовать в другой службе BizTalk. Необходимо hello имя входа и пароль, введенный в процессе создания этот сервер базы данных SQL Azure.<br/><br/><strong>Совет</strong> создать базу данных отслеживания hello и учетной записи мониторинга и архивации на hello же регионе, как hello службы BizTalk.</td>
    </tr>
    </table>
Выберите стрелку hello.
6. Введите параметры hello базы данных:  <table border="1">
    <tr>
    <td><strong>Имя</strong></td>
    <td>Доступна при <strong>создать новый экземпляр базы данных SQL</strong> выбранных в предыдущем экране приветствия.
    <br/><br/>
Введите toobe имя базы данных SQL, используемой службы BizTalk.</td>
    </tr>
    <tr>
    <td><strong>Сервер</strong></td>
    <td>Доступна при <strong>создать новый экземпляр базы данных SQL</strong> выбранных в предыдущем экране приветствия.
    <br/><br/>
Выберите существующий сервер базы данных SQL или создайте новый.</td>
    </tr>
    <tr>
    <td><strong>Имя входа на сервер</strong></td>
    <td>Введите имя пользователя для входа в систему hello.</td>
    </tr>
    <tr>
    <td><strong>Пароль для входа на сервер</strong></td>
    <td>Введите пароль для входа hello.</td>
    </tr>
    <tr>
    <td><strong>Регион</strong></td>
    <td>Параметр доступен, если выбран параметр <strong>Создать экземпляр базы данных SQL</strong>. Выберите географический регион toohost hello базы данных SQL.</td>
    </tr>
    </table>

Выберите hello флажок toocomplete приветствия мастера. появится значок хода выполнения Hello:  
![Значок хода выполнения, отображаемый при завершении процесса][ProgressComplete]

По завершении hello службы Azure BizTalk, созданы и готовы для ваших приложений. значения по умолчанию Hello подходят. Параметры по умолчанию hello toochange установите **службы BIZTALK** в hello левой панели навигации, а затем выберите службу BizTalk. Дополнительные параметры отображаются на hello [вкладки панели мониторинга, монитора и масштабирования](biztalk-dashboard-monitor-scale-tabs.md) вверху hello.

В зависимости от состояния hello hello службы BizTalk существуют некоторые операции, которые не может быть завершена. Список этих операций, go слишком[диаграммы состояния служб BizTalk](biztalk-service-state-chart.md).

## <a name="post-provisioning-steps"></a>Действия после подготовки
* [Установите сертификат hello на локальном компьютере](#InstallCert)
* [Добавление готового сертификата для рабочей среды](#AddCert)
* [Получение имен Access Control hello](#ACS)

#### <a name="InstallCert"></a>Установите сертификат hello на локальном компьютере
На этапе подготовки службы BizTalk создается самозаверяющий сертификат, который связывается с вашей подпиской службы BizTalk. Необходимо загрузить этот сертификат и установить его на компьютерах, в котором развертывания приложений службы BizTalk или отправки сообщений tooa конечной точки службы BizTalk.

1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Выберите **службы BIZTALK** в hello левой панели навигации, а затем выберите подписке на службу BizTalk.
3. Выберите hello **мониторинга** вкладки.
4. Выберите **Загрузить SSL-сертификат**:  
   ![Изменение SSL-сертификата][QuickGlance]
5. Дважды щелкните сертификат hello и выполните приветствия мастера tooinstall hello сертификата. Убедитесь, что установить сертификат hello hello **доверенные корневые центры сертификации** хранения.

#### <a name="AddCert"></a>Добавление готового сертификата для рабочей среды
Hello самозаверяющий сертификат, который создается автоматически при создании службы BizTalk предназначен для использования в средах разработки только. Для выполнения рабочих сценариев замените его готовым сертификатом для рабочей среды.

1. На hello **мониторинга** выберите **обновления SSL-сертификат**.
2. Обзор tooyour закрытый сертификат SSL (*CertificateName*PFX-файл), включает имя службы BizTalk, введите пароль hello и нажмите кнопку флажок hello.

#### <a name="ACS"></a>Получение имен Access Control hello
1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Выберите **службы BIZTALK** в hello левой панели навигации, а затем выберите службу BizTalk.
3. На панели задач hello, выберите **сведения о соединении**:  
   ![Выбор элемента "Сведения о подключении"][ACSConnectInfo]
4. Скопируйте значения hello контроля доступа.

Это пространство имен Access Control вводится при развертывании проекта службы BizTalk из Visual Studio. пространство имен Access Control Hello автоматически создается для службы BizTalk.

значения Hello контроля доступа могут использоваться с любым приложением. При создании службы BizTalk Azure это пространство имен контроля доступа управляет hello проверку подлинности с помощью развертывания службы BizTalk. Если требуется toochange hello подписки или управление приветствия имен, выберите **ACTIVE DIRECTORY** в hello левой панели навигации, а затем выберите пространство имен. панель задач Hello список параметров.

Щелкнув **управление** Здравствуйте, откроется портал управления Access Control. В hello портал управления Access Control, hello служба BizTalk использует **удостоверения службы**:  
![Удостоверения службы ACS в hello портал управления Access Control][ACSServiceIdentities]

Hello удостоверение службы управления доступом — это набор учетных данных, которые позволяют приложениям или tooauthenticate клиентов напрямую с помощью контроля доступа и получать токен.

> [!IMPORTANT]
> Hello служба BizTalk использует **владельца** для удостоверения службы по умолчанию hello и hello **пароль** значение. Если вы используете значение симметричного ключа hello вместо hello значение пароля, hello может возникнуть следующая ошибка.<br/><br/>*Не удалось подключиться учетной записи службы управления для управления доступом toohello hello указан учетные данные*
> 
> 

[Управление пространством имен ACS](https://msdn.microsoft.com/library/azure/hh674478.aspx) приведены некоторые правила и рекомендации.

## <a name="requirements-explained"></a>Пояснение требований
Эти требования не применяются toohello бесплатный выпуск.

<table border="1">
<tr bgcolor="FAF9F9">
        <td><strong>Необходимые элементы</strong></td>
        <td><strong>Их назначение</strong></td>
</tr>
<tr>
<td>Подписка Azure.</td>
<td>Hello подписка определяет, кто может входить в toohello портал Azure. Владелец учетной записи Hello создается подписка hello в <a HREF="https://account.windowsazure.com/Subscriptions"> подписок Azure</a>.
<br/><br/>
Hello Azure учетная запись может иметь несколько подписок и можно управлять всеми пользователями, которым разрешено. Например, лица вашей учетной записи Azure создает подписку с именем <em>BizTalkServiceSubscription</em> и дает hello Администраторы BizTalk в вашей организации (например, ContosoBTSAdmins@live.com) получить доступ к подписке toothis. В этом сценарии Администраторы BizTalk hello вход toohello портал Azure и имеют полный администратор права tooall hello размещенных служб в подписке hello, включая службы Azure BizTalk. Администраторы BizTalk Hello не будут носителями hello учетная запись Azure и нет сведений о выставлении счетов tooany доступа.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Управление подписками и учетными записями хранения в hello портал Azure</a> предоставляет дополнительные сведения.
</td>
</tr>
<tr>
<td>База данных SQL Azure</td>
<td>Хранит hello таблицы, представления и хранимые процедуры, используемые hello службы BizTalk, включая данные отслеживания hello.
<br/><br/>
При создании службы BizTalk можно использовать существующий сервер SQL Server Azure, базу данных SQL Azure или автоматически создать новый сервер или базу данных.
<br/><br/>
автоматически настраивается Hello масштабирование базы данных SQL. Как правило масштаб по умолчанию hello достаточно для службы BizTalk. Изменение масштаба hello влияет на цены. См. статью о <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930">стоимости услуг Azure</a>
.<br/><br/>
<strong>Примечания</strong>
<br/>
<ul>
<li> При создании нового сервера SQL Server и базы данных Azure автоматически включаются службы Azure. Служба BizTalk Hello требуются службы Azure включить.</li>
<li>При создании новой базы данных SQL Azure на существующем сервере SQL Azure, hello правила брандмауэра сервера не изменяются hello. В результате возможна других служб Azure не допускаются доступа toohello сервера баз данных.</li>
</ul>
</td>
</tr>
<tr>
<td>Пространство имен Azure Access Control</td>
<td>Выполняет проверку подлинности с помощью служб BizTalk Azure. Это пространство имен Access Control вводится при развертывании проекта службы BizTalk из Visual Studio. При создании службы BizTalk, автоматически создается пространство имен Access Control hello.</td>
</tr>

<tr>
<td>Учетная запись хранения Azure</td>
<td>Предоставляет доступ tootables, больших двоичных объектов и очередей, используемых службой вашей службы BizTalk toosave hello следующее:

<ul>
<li>Файлы журналов, монитор hello службы BizTalk. Привет, отслеживающую выходные данные также отображаются в hello **мониторинг** hello портал Azure на вкладке.</li>
<li>При создании X12 или соглашения AS2 между партнерами, можно включить свойства сообщения toostore функция архивации hello. Эти данные сохраняются в hello учетной записи хранилища.</li>
</ul>
<br/>
При создании службы BizTalk можно использовать существующую или автоматически созданную новую учетную запись хранения.
<br/><br/>
настройки хранилища по умолчанию Hello достаточны для службы BizTalk.
<br/><br/>
При создании учетной записи хранения автоматически создаются первичный ключ и вторичный ключ. Эти ключи управляют tooyour доступа к учетной записи хранилища. Hello службы BizTalk автоматически использует hello первичный ключ.
<br/><br/>
Дополнительные сведения см. в статье <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">Хранилище</a>.
</td>
</tr>

<tr>
<td>Закрытый сертификат SSL</td>
<td>
При создании службы BizTalk Azure также создается URL-адрес HTTPS-узла, включающий имя службы BizTalk. Этот URL-адрес будет автоматически настроенного toouse самозаверяющий сертификат только для разработки. На рабочем этапе вам потребуется личный SSL-сертификат.
<br/><br/>
<strong>Важные сведения об SSL-сертификате</strong>

<ul>
<li>Срок действия сертификата Hello должно быть меньше 5 лет.</li>
<li>Все личные сертификаты требуют наличия пароля. Запомните этот пароль, а также сообщите его вашим администраторам.</li>
<li>Самозаверяющие сертификаты используются в средах разработки/тестирования. При использовании самозаверяющих сертификатов, импортируйте хранилище личных сертификатов tooyour сертификатов hello и hello хранилище сертификатов доверенных корневых центров сертификации.</li>
</ul>
<br/>При отправке центра сертификации tooyour запрос сертификата hello производства, предоставьте hello следующие свойства сертификата:
<br/>

<ul>
<li><strong>Расширенное использование ключа.</strong> Службы BizTalk Azure требуют как минимум проверки подлинности сервера.</li>
<li><strong>Общее имя</strong>: Введите hello полное доменное имя (FQDN) URL-адрес службы BizTalk Azure. См. раздел <a HREF="#CreateService">Создание службы BizTalk</a> в этой статье.</li>
</ul>
<br/>
После создания службы BizTalk hello можно добавить новые или другой сертификат.
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a>через гибридные подключения
При создании службы BizTalk Azure hello **гибридных подключений** вкладка доступна:

![вкладка "Гибридные подключения"][HybridConnectionTab]

Гибридные подключения, используемые tooconnect Azure веб-сайта или tooany мобильной службы Azure локального ресурса, который использует статический порт TCP, таких как SQL Server, MySQL, веб-API HTTP, мобильных служб и большинство пользовательских веб-служб.  Гибридные подключения и hello службы адаптера BizTalk отличаются. Hello службы адаптера BizTalk — используется tooconnect служб Azure BizTalk tooan в локальной строке из БИЗНЕС-системе.

 В разделе [гибридных подключений](integration-hybrid-connection-overview.md) toolearn, включая создание и управление гибридных подключений.

## <a name="next-steps"></a>Дальнейшие действия
После создания службы BizTalk ознакомиться с разных hello [службы BizTalk: вкладки панели мониторинга, монитора и масштабирования](biztalk-dashboard-monitor-scale-tabs.md). Служба BizTalk готова для использования в приложениях. Создание приложений, перейдите в слишком toostart[служб Azure BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="see-also"></a>См. также
* [Службы BizTalk: диаграмма выпусков](biztalk-editions-feature-chart.md)<br/>
* [Службы BizTalk: диаграмма состояния](biztalk-service-state-chart.md)<br/>
* [Службы BizTalk: резервное копирование и восстановление](biztalk-backup-restore.md)<br/>
* [Службы BizTalk: регулирование](biztalk-throttling-thresholds.md)<br/>
* [Службы BizTalk: имя и ключ издателя](biztalk-issuer-name-issuer-key.md)<br/>
* [Как я запустить с помощью hello пакета SDK служб BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [гибридных подключений](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
