---
title: "Руководство. Обработка счетов-фактур EDIFACT с помощью служб BizTalk Azure | Документация Майкрософт"
description: "Как toocreate и настроить приложение hello соединитель поле или API и использовать его в приложение логики в службе приложений Azure"
services: biztalk-services
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
ms.assetid: 7e0b93fa-3e2b-4a9c-89ef-abf1d3aa8fa9
ms.service: biztalk-services
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/31/2016
ms.author: deonhe
ms.openlocfilehash: 4ca021c9084b9b6540c93ef15fc3d44be0966970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-process-edifact-invoices-using-azure-biztalk-services"></a>Руководство по обработке счетов EDIFACT с помощью служб BizTalk Azure

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Можно использовать tooconfigure hello портале служб BizTalk и развертывание соглашения X12 и EDIFACT. В этом учебнике рассматривается как toocreate соглашения EDIFACT для обмена накладных между торговыми партнерами. В качестве примера здесь используется комплексное бизнес-решение с двумя торговыми партнерами, компаниями Contoso и Northwind, которые обмениваются сообщениями EDIFACT.  

## <a name="sample-based-on-this-tutorial"></a>Пример, который используется в этом руководстве
Этот учебник написан на основе примера **Отправка EDIFACT счетов с помощью служб BizTalk**, являющееся доступных toodownload из hello [коллекции кода MSDN](http://go.microsoft.com/fwlink/?LinkId=401005). Можно использовать образец hello и пройти этот учебник toounderstand, как был построен образец hello. Или можно использовать этот учебник toocreate собственное решение основ. Этот учебник ориентирован hello второй подход, чтобы понять, как было построено данное решение. Кроме того насколько возможно, hello учебник согласован с образец hello и использует hello же имена артефактов (например, схем, преобразований и), которые заданы в образце hello.  

> [!NOTE]
> Поскольку это решение подразумевает отправку сообщения из моста EAI tooan мост EDI, он повторно использует hello [пример цепочки мостов служб BizTalk](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104) образца.  
> 
> 

## <a name="what-does-hello-solution-do"></a>Что делает hello решение?
В рамках этого решения компания Northwind получает счета EDIFACT от компании Contoso. Эти счета передаются не в стандартном формате EDI. Таким образом перед отправкой счета tooNorthwind hello, он должен быть преобразованный tooan EDIFACT (также называемый INVOIC) документа. По получении Northwind необходимо обработать счет EDIFACT hello и вернуть tooContoso сообщение (также называемое CONTRL) элемента управления.

![][1]  

tooachieve этот бизнес-сценарий, Contoso использует функции hello, в состав служб BizTalk Microsoft Azure.

* Contoso использует EAI мосты tootransform hello исходного счета tooEDIFACT INVOIC.
* мост EAI Hello отправляет tooan сообщение hello развернут мост отправки EDI в рамках соглашения, настроенного в hello портале служб BizTalk.
* Hello мост отправки EDI обрабатывает EDIFACT INVOIC hello и направляет его tooNorthwind.
* После получения счета hello, Northwind возвращает CONTRL toohello сообщений, развернутый в рамках соглашения hello моста получения EDI.  

> [!NOTE]
> При необходимости это решение также демонстрирует, как пакетная обработка toosend hello toouse счетов в пакетах, вместо того чтобы отправлять каждой накладной отдельно.  
> 
> 

сценарий toocomplete hello, мы используем очереди Service Bus toosend счета из Contoso tooNorthwind или получать подтверждения от Northwind. Эти очереди могут быть созданы с помощью клиентского приложения, который доступен для загрузки и входит в пакет образца hello, который доступен в рамках этого учебника.  

## <a name="prerequisites"></a>Предварительные требования
* Вам понадобится пространство имен служебной шины. Чтобы создать пространство имен, выполните действия, описанные в статье [Руководство по созданию или изменению пространства имен службы служебной шины](https://msdn.microsoft.com/library/azure/hh674478.aspx). Предположим, вы уже подготовили пространство имен служебной шины с именем **edifactbts**.
* Необходимо подписаться на службы BizTalk. Инструкции см. в статье [Создание служб BizTalk с помощью портала Azure](http://go.microsoft.com/fwlink/?LinkID=302280). В этом руководстве давайте предположим, что у вас есть подписка на службы BizTalk с именем **contosowabs**.
* Зарегистрируйте подписку служб BizTalk на портале служб BizTalk hello. Инструкции см. в разделе [регистрация развертывания службы BizTalk на портале служб BizTalk hello](https://msdn.microsoft.com/library/hh689837.aspx)
* Необходимо установить Visual Studio.
* Необходимо установить пакет SDK для служб BizTalk. Вы можете загрузить hello SDK из [http://go.microsoft.com/fwlink/?LinkId=235057](http://go.microsoft.com/fwlink/?LinkId=235057)  

## <a name="step-1-create-hello-service-bus-queues"></a>Шаг 1: Создание hello очереди шины обслуживания
Это решение использует Service Bus очереди tooexchange сообщениями между торговыми партнерами. Contoso и Northwind отправляют сообщения toohello очередей из которых мосты EAI и EDI hello смогут использовать их. Для этого решения требуется три очереди служебной шины:

* **northwindreceive** — Northwind получает счет hello из Contoso по этой очереди.
* **contosoreceive** — Contoso получает подтверждение hello от Northwind по этой очереди.
* **Приостановить** — все приостановленные сообщения, перенаправленные toothis очереди. Сообщения приостанавливаются, если во время их обработки происходит ошибка.

В этих очередях шины обслуживания можно создать с помощью клиентского приложения, включенные в пакет образца hello.  

1. Hello расположение, куда вы загрузили пример hello, откройте **учебника отправка счетов с помощью BizTalk Services EDI Bridges.sln**.
2. Нажмите клавишу **F5** toobuild и начала hello **Tutorial Client** приложения.
3. На экране «hello» введите пространство имен ACS шины службы hello, имя издателя и ключ издателя.
   
   ![][2]  
4. Появится сообщение с предложением создать в пространстве имен служебной шины три очереди. Нажмите кнопку **ОК**.
5. Оставьте Tutorial Client запущена hello. Откройте hello, щелкните **Service Bus** > ***пространство имен Service Bus*** > **очереди**и убедитесь, что hello три очереди создаются.  

## <a name="step-2-create-and-deploy-trading-partner-agreement"></a>Шаг 2. Создание и развертывание соглашения между торговыми партнерами
Создайте соглашение между торговыми партнерами Contoso и Northwind. Соглашение между торговыми партнерами определяет контракт trade между hello двух деловых партнеров, например какие toouse схемы сообщений, который обмена сообщениями toouse протокола и т. д. Соглашение между торговыми партнерами включает два мосты EDI, один toosend сообщений tootrading партнеров (называется hello **мост отправки EDI**) и один tooreceive сообщений от торговых партнеров (вызывается hello **моста получения EDI**).

В контексте hello данного решения мост отправки EDI hello соответствует toohello отправляющей стороне соглашения hello и не используется toosend счета EDIFACT hello из Contoso tooNorthwind. Аналогично, мост получения hello EDI соответствует toohello на стороне приема соглашения hello и не используется tooreceive подтверждения от Northwind.  

### <a name="create-hello-trading-partners"></a>Создание торговых партнеров hello
toostart, создать Торговые партнеры Contoso и Northwind.  

1. В hello портала служб BizTalk на hello **партнеров** щелкните **добавить**.
2. В новую страницу приветствия партнера, введите **Contoso** как имя участника, а затем щелкните **Сохранить**.
3. Повторите hello шаг toocreate hello вторым партнером **Northwind**.  

### <a name="create-hello-agreement"></a>Создание соглашения hello
Соглашения между торговыми партнерами — это соглашения между бизнес-профилями торговых партнеров. Это решение использует профили участника по умолчанию hello, создаваемых автоматически, когда мы создавали hello партнеров.  

1. В hello портале служб BizTalk, щелкните **соглашения** > **добавить**.
2. В новое соглашение hello **Общие параметры** , укажите значения hello, как показано в приведенном ниже рисунке hello и выберите **Продолжить**.
   
   ![][3]  
   
   После нажатия кнопки **Продолжить** станут доступными две вкладки: **Настройки получения** и **Настройки отправки**.
3. Создайте hello соглашение отправки между Contoso и Northwind. Данное соглашение регламентирует, каким образом Contoso отправляет счет tooNorthwind hello EDIFACT.
   
   1. Щелкните **Параметры отправки**.
   2. Сохранить значения по умолчанию hello на hello **входящий URL-адрес**, **преобразования**, и **Пакетная обработка** вкладок.
   3. На hello **протокола** в группе hello **схемы** Загрузите hello **EFACT_D93A_INVOIC.xsd** схемы. Эта схема доступен в пакете образца hello.
      
      ![][4]  
   4. На hello **транспорта** укажите hello подробные сведения об очередях Service Bus hello. В соглашение на стороне отправителя hello, мы будем использовать hello **northwindreceive** очередь tooNorthwind счета EDIFACT hello toosend и hello **приостановки** очереди все сообщения, для которых не выполняется во время обработки и являются tooroute Приостановить. Вы создали эти очереди в **шаг 1: Создание очереди Service Bus hello** (в этом разделе).
      
      ![][5]  
      
      В разделе **параметры транспорта > тип транспорта** и **параметры приостановки сообщений > тип транспорта**выберите Azure Service Bus и задать значения hello, показанную hello.
4. Создать hello получать соглашение между Contoso и Northwind. Это соглашение регулирует, как Contoso получает подтверждение hello из Northwind.
   
   1. Щелкните **Параметры получения**.
   2. Сохранить значения по умолчанию hello на hello **транспорта** и **преобразования** вкладок.
   3. На hello **протокола** в группе hello **схемы** Загрузите hello **EFACT_4.1_CONTRL.xsd** схемы. Эта схема доступен в пакете образца hello.
   4. На hello **маршрута** создайте tooensure фильтр, только подтверждения от Northwind перенаправленное tooContoso. В разделе **параметры маршрутизации**, нажмите кнопку **добавить** toocreate hello фильтра маршрутизации.
      
      ![][6]  
      
      1. Укажите значения для **имя правила**, **правило маршрутизации**, и **назначение маршрутизации** как показано на рисунке hello.
      2. Щелкните **Сохранить**.
   5. На hello **маршрута** укажите, куда направляются приостановленные подтверждения (которых возник сбой во время обработки). Задать tooAzure тип транспорта hello Service Bus, назначение маршрутизации слишком**очереди**, тип проверки подлинности слишком**подписи общего доступа** (SAS), укажите строку подключения SAS hello hello Service Bus пространство имен, а затем введите имя очереди hello **приостановки**.
5. Наконец, нажмите кнопку **развернуть** toodeploy hello соглашения. Конечные точки hello Примечание где hello отправки и получения соглашений развертывается.
   
   * На hello **параметры отправки** в разделе **входящий URL-адрес**, обратите внимание hello конечную точку. toosend сообщение от tooNorthwind Contoso с помощью hello мост отправки EDI, необходимо отправить toothis конечную точку сообщения.
   * На hello **параметры получения** в разделе **транспорта**, обратите внимание hello конечную точку. toosend сообщение от Northwind tooContoso hello EDI с помощью моста получения, вы должны отправить toothis конечную точку сообщения.  

## <a name="step-3-create-and-deploy-hello-biztalk-services-project"></a>Шаг 3: Создание и развертывание проекта служб BizTalk hello
В предыдущем шаге hello вы уже развернули hello EDI, отправки и получения счетов EDIFACT tooprocess соглашений и подтверждений. Эти соглашения могут обрабатывать только сообщения, соответствующие стандарту схемы сообщений EDIFACT toohello. Однако по сценариям hello для этого решения, Contoso отправляет счет tooNorthwind в собственной схеме. Таким образом перед отправкой сообщения hello toohello мост отправки EDI, его необходимо преобразовать из hello собственная схема toohello стандартную схему счетов EDIFACT. Hello EAI служб BizTalk проект делает это.

проект служб BizTalk Hello, **InvoiceProcessingBridge**, hello, преобразований сообщений также включается как часть образца hello, загруженный. Hello проект включает следующие артефакты hello.

* **INHOUSEINVOICE. XSD** — схема счета hello, отправляется tooNorthwind.
* **EFACT_D93A_INVOIC. XSD** — схема счета EDIFACT Стандартная hello.
* **EFACT_4.1_CONTRL. XSD** — схема подтверждения EDIFACT hello, Northwind отправляет tooContoso.
* **INHOUSEINVOICE_to_D93AINVOIC. TRFM** — hello преобразование, которое отображает hello корпоративного счета схемы toohello стандартную схему счетов EDIFACT.  

### <a name="create-hello-biztalk-services-project"></a>Создание проекта служб BizTalk hello
1. В hello решения Visual Studio, разверните проект InvoiceProcessingBridge hello, а затем откройте hello **MessageFlowItinerary.bcs** файла.
2. Щелкните в любом месте холста hello и задайте hello **URL-адрес службы BizTalk** в hello toospecify поле свойства имя своей подписки служб BizTalk. Например, `https://contosowabs.biztalk.windows.net`.
   
   ![][7]  
3. Перетащите из элементов hello **односторонний мост Xml** toohello холста. Набор hello **имя сущности** и **относительный адрес** свойства hello мост слишком**ProcessInvoiceBridge**. Дважды щелкните **ProcessInvoiceBridge** tooopen hello конструктора моста.
4. В пределах hello **типы сообщений** щелкните плюс hello (**+**) кнопку toospecify hello схему входящего сообщения hello. Поскольку входящее сообщение hello для hello мост EAI всегда hello корпоративного счета, установите это слишком**INHOUSEINVOICE**.
   
   ![][8]  
5. Щелкните hello **преобразование Xml** фигуры и в поле свойства hello, hello **Maps** свойства, нажмите кнопку с многоточием hello (**...** ) кнопки. В hello **Выбор сопоставлений** диалоговое окно, выберите hello **INHOUSEINVOICE_to_D93AINVOIC** преобразования файла и нажмите кнопку **ОК**.
   
   ![][9]  
6. Возврат слишком**MessageFlowItinerary.bcs**и перетащите из элементов hello **конечная точка двусторонней внешней службы** toohello справа от приветствия **ProcessInvoiceBridge**. Задайте его **имя сущности** свойство слишком**EDIBridge**.
7. В hello в обозревателе решений, разверните hello **MessageFlowItinerary.bcs** и дважды щелкните hello **EDIBridge.config** файла. Замените содержимое hello hello **EDIBridge.config** hello следующее.
   
   > [!NOTE]
   > Почему необходимо tooedit hello config-файл? Hello внешней конечной точки службы, добавленный toohello холст представляет hello мосты EDI, развернутые ранее. Мосты EDI являются двусторонними, то есть обеспечивают отправку и получение. Однако hello мост EAI, добавленный конструктора моста toohello является однонаправленным. Поэтому toohandle hello различных шаблонов обмена сообщениями hello двух мостов, мы используем настраиваемый мост, включая настройки в файле .config hello. Кроме того hello пользовательское поведение также отвечает конечной точке моста отправки EDI в toohello проверки подлинности hello. Это поведение доступно как отдельный пример на [пример - EAI tooEDI цепочки мостов служб BizTalk](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104). Это решение использует образец hello.  
   > 
   > 
   
   ```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
     <system.serviceModel>
       <extensions>
         <behaviorExtensions>
           <add name="BridgeAuthentication" 
                 type="Microsoft.BizTalk.Bridge.Behaviour.BridgeBehaviorElement, Microsoft.BizTalk.Bridge.Behaviour, Version=1.0.0.0, Culture=neutral, PublicKeyToken=ae58f69b69495c05" />
         </behaviorExtensions>
       </extensions>
       <behaviors>
         <endpointBehaviors>
           <behavior name="BridgeAuthenticationConfiguration">
             <!-- Enter hello ACS namespace, issuer name and issuer secret of hello BizTalk Services deployment -->
             <BridgeAuthentication acsnamespace="[YOUR ACS NAMESPACE]" 
                                   issuername="owner" 
                                   issuersecret="[YOUR ACS SECRET]" />
             <webHttp />
           </behavior>
         </endpointBehaviors>
       </behaviors>
       <bindings>
         <webHttpBinding>
           <binding name="BridgeBindingConfiguration">
             <security mode="Transport" />
           </binding>
         </webHttpBinding>
       </bindings>
       <client>
         <clear />
         <!--
           Go BizTalk Portal > Agreement > Send Settings > Inbound URL
           Copy hello Endpoint URL and paste it in hello below address field
         -->
         <endpoint name="TwoWayExternalServiceEndpointReference1" 
                   address="[YOUR EDI BRIDGE SEND URI]" 
                   behaviorConfiguration="BridgeAuthenticationConfiguration" 
                   binding="webHttpBinding" 
                   bindingConfiguration="BridgeBindingConfiguration" 
                   contract="System.ServiceModel.Routing.IRequestReplyRouter" />
       </client>
     </system.serviceModel>
   </configuration>
   
   ```
8. Обновление сведений о конфигурации tooinclude файла EDIBridge.config hello
   
   * В разделе  *<behaviors>* укажите приветствия имен ACS и ключ, связанный с hello подписки служб BizTalk.
   * В разделе  *<client>* , предоставляют hello конечной точки, где развернуто соглашение отправки EDI hello.
   
   Сохраните изменения и закройте файл конфигурации hello.
9. Hello элементов щелкните hello **соединитель** и соединения hello **ProcessInvoiceBridge** и **EDIBridge** компонентов. Выберите соединитель hello и в окно «Свойства» задайте **условие фильтра** слишком**сопоставить все**. Это гарантирует, что все сообщения, обрабатываемые hello мост EAI, направляются toohello мост EDI.
   
   ![][10]  
10. Сохраните изменения toohello решения.  

### <a name="deploy-hello-project"></a>Развертывание проекта hello
1. На компьютере hello, где создан проект служб BizTalk hello Загрузите и установите hello SSL-сертификат для подписки на службы BizTalk. В разделе служб BizTalk щелкните **Панель мониторинга**, а затем нажмите кнопку **Загрузить SSL-сертификат**. Дважды щелкните сертификат hello и выполните установку hello prompt toocomplete hello. Убедитесь, что установки сертификата hello под **доверенные корневые центры сертификации** хранилище сертификатов.
2. В обозревателе решений Visual Studio, щелкните правой кнопкой мыши hello **InvoiceProcessingBridge** проекта, а затем нажмите кнопку **развернуть**.
3. Укажите значения hello, как показано на рисунке hello и нажмите кнопку **развернуть**. Можно получить учетные данные hello ACS для служб BizTalk, щелкнув **сведения о соединении** из панели мониторинга службы BizTalk hello.
   
   ![][11]  
   
   Из области вывода hello, копирование hello конечной точки, где hello мост EAI развернут, например, `https://contosowabs.biztalk.windows.net/default/ProcessInvoiceBridge`. Этот URL-адрес конечной точки понадобится вам позже.  

## <a name="step-4-test-hello-solution"></a>Шаг 4: Тестирование решения hello
В этом разделе рассматривается, как tootest hello решения с помощью hello **Tutorial Client** приложения предоставляется как часть образца hello.  

1. В Visual Studio нажмите клавишу F5 toostart hello **Tutorial Client**.
2. экран приветствия должен иметь hello значения, заданные hello шаг создания hello очереди Service Bus. Щелкните **Далее**.
3. В следующем окне приветствия учетные данные ACS для служб BizTalk подписки и hello конечных точек которой EAI и EDI (получения) развернуты мосты.
   
   Вы скопировали конечную точку моста EAI hello в предыдущем шаге hello. Для конечной точки моста получения EDI в портале служб BizTalk hello, go toohello соглашения > Параметры получения > транспорта > конечной точки.
   
   ![][12]  
4. В следующем окне приветствия в разделе Contoso нажмите кнопку hello **Send In-house Invoice** кнопки. В файл Привет открыть диалоговое окно, откройте файл INHOUSEINVOICE.txt hello. Изучите содержимое hello hello файла и нажмите кнопку **ОК** toosend hello счета.
   
   ![][13]  
5. В hello несколько секунд счет будет получен в Northwind. Нажмите кнопку hello **просмотреть сообщение** ссылку toosee hello счета, полученного из базы данных Northwind. Обратите внимание, каким образом является hello счета, полученного из базы данных Northwind в стандартную схему EDIFACT при hello один Contoso отправляется была собственная схема.
   
   ![][14]  
6. Выберите счет hello и нажмите кнопку **отправить подтверждение**. Обратите внимание, hello обмена, когда идентификатор же hello полученного счета и hello подтверждение отправки hello диалоговом появившемся. Нажмите кнопку "ОК" в hello **отправить подтверждение** диалоговое окно.
   
   ![][15]  
7. Через несколько секунд hello успешно подтверждения в Contoso.
   
   ![][16]  

## <a name="step-5-optional-send-edifact-invoice-in-batches"></a>Шаг 5 (необязательный). Пакетная отправка счетов EDIFACT
Мосты EDI служб BizTalk также поддерживают пакетную обработку исходящих сообщений. Эта возможность полезна для принимающих партнеров, которые предпочитают tooreceive пакет сообщений (по определенному критерию) вместо отдельных сообщений.

Hello наиболее важным аспектом при работе с пакетами является фактический выпуск пакета hello, называемый также условия выпуска hello hello. условия выпуска Hello могут определяться как принимающий партнер hello хочет tooreceive сообщений. При включенной пакетной обработке hello мост EDI не отправлять исходящие сообщения toohello hello получение партнера, пока hello выполнения условий выпуска. Например, условия отправки пакета на основе размера сообщения будут выполнены, только когда количество сообщений в пакете достигнет определенного значения. Условия также могут определяться временем отправки (например, пакет будет отправляться ежедневно в указанное время). В данном решении мы пытаемся условия на основе размера сообщения hello.

1. В hello портале служб BizTalk щелкните hello соглашения, которое было создано ранее. Щелкните «Параметры отправки» > «Пакетная обработка» > «Добавить пакет».
2. В качестве имени пакета укажите **InvoiceBatch**, введите описание и нажмите кнопку **Далее**.
3. Укажите условия пакетной обработки, в соответствии с которыми сообщения будут включены в пакет. В этом решении будут включены все сообщения. Таким образом, выберите hello использовать расширенные определения параметр и введите **1 = 1**. Так как это условие всегда будет иметь значение Тrue, пакетной обработке будут подлежать все сообщения. Щелкните **Далее**.
   
   ![][17]  
4. Укажите условия пакетной отправки. Hello раскрывающемся списке выберите **MessageCountBased**, а также для **число**, укажите **3**. Это означает, что пакет из трех сообщений будет отправлено tooNorthwind. Щелкните **Далее**.
   
   ![][18]  
5. Просмотрите сводку hello и нажмите кнопку **Сохранить**. Нажмите кнопку **развернуть** tooredeploy hello соглашения.
6. Вернитесь к предыдущему окну toohello **Tutorial Client**, нажмите кнопку **Send In-house Invoice**и следуйте hello приглашения toosend hello счета. Обратите внимание, что счет не получен в Northwind, так как размер пакета hello не выполнены. Повторите это действие еще два раза, чтобы получить набрать три сообщения tooNorthwind. Это удовлетворяет условия выпуска пакета 3 сообщений hello и должно отобразиться счет в Northwind.

<!--Image references-->
[1]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-1.PNG  
[2]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-2.PNG  
[3]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-3.PNG
[4]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-4.PNG  
[5]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-5.PNG  
[6]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-6.PNG  
[7]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-7.PNG  
[8]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-8.PNG
[9]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-9.PNG  
[10]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-10.PNG  
[11]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-11.PNG  
[12]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-12.PNG  
[13]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-13.PNG
[14]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-14.PNG  
[15]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-15.PNG  
[16]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-16.PNG  
[17]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-17.PNG  
[18]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-18.PNG

