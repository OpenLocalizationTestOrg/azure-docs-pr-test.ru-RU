---
title: "брандмауэр приложения tooweb aaaIntroduction (WAF) для шлюза приложения Azure | Документы Microsoft"
description: "На этой странице представлен обзор брандмауэра веб-приложения на шлюзе приложений."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 04b362bc-6653-4765-86f6-55ee8ec2a0ff
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: amsriva
ms.openlocfilehash: 5a42ce0fb2bd12a391844099e2de8fa2571195e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="web-application-firewall-waf"></a>Брандмауэр веб-приложения (WAF)

Брандмауэр веб-приложения (WAF) — это компонент шлюза приложений, обеспечивающий централизованную защиту веб-приложений от распространенных эксплойтов и уязвимостей. 

Брандмауэр веб-приложения основан на правилах из hello [наборов правил core OWASP](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) 2.2.9 или 3.0. Веб-приложения все чаще подвергаются вредоносным атакам, использующим общеизвестные уязвимости. Совместно эти эксплойтов атак путем внедрения кода SQL, межузловых сценариев атак tooname несколько. Таких атак в код приложения может быть сложной и может потребоваться жесткое обслуживания, исправления и мониторинг на нескольких уровнях Топология приложения hello. Брандмауэр централизованного веб-приложения помогает упростить управление безопасностью и Администраторы повышения надежности tooapplication от угроз или вторжения. Решение WAF также реагировать угрозу безопасности tooa быстрее путем применения исправлений известные уязвимости в центральном расположении и обеспечения безопасности каждого отдельного веб-приложений. Существующие шлюзы приложений может быть легко преобразованный tooa веб-приложение включен брандмауэр приложения шлюза.

![imageURLroute](./media/application-gateway-web-application-firewall-overview/WAF1.png)

Шлюз приложений работает в качестве приложения доставки контроллера и предложения завершение запросов SSL сходство сеансов на основе файлов cookie, распределения нагрузки с циклическим перебором, маршрутизация на основе содержимого, toohost возможность многочисленные улучшения, связанные веб-сайтов и безопасности. Усовершенствования системы безопасности, предоставляемые шлюза приложения включают управление политиками SSL, tooend окончания поддержки SSL. Безопасность приложений теперь усиленное WAF (брандмауэр веб-приложения) непосредственно интегрируется в предложение hello Соединитель Active Directory. Это обеспечивает центральное расположение легко tooconfigure toomanage и защитить веб-приложений от общих веб-уязвимостей.

## <a name="benefits"></a>Преимущества

Здесь представлены Hello hello основных преимуществ, которые предоставляют брандмауэр шлюз приложений и веб-приложения:

### <a name="protection"></a>Защита

* Веб-приложения защиты от атак без изменения кода toobackend и веб-уязвимостей.

* Защита нескольких web приложений на hello одновременную за шлюз приложений. Шлюз приложений поддерживает размещение вверх too20 веб-сайтов за все могут быть защищены от атак с WAF что один шлюз.

### <a name="monitoring"></a>Мониторинг

* Выполняйте мониторинг веб-приложения для защиты от атак, используя журнал WAF в режиме реального времени. Этот журнал интегрирован с [монитора Azure](../monitoring-and-diagnostics/monitoring-overview.md) tootrack WAF оповещения и журналы и легко отслеживать тенденции.

* Скоро WAF будет интегрирован с центром безопасности Azure. Центр безопасности Azure позволяет операциям hello состояние безопасности всех ресурсов Azure.

### <a name="customization"></a>Настройка

* Hello возможности toocustomize WAF правил и правила группы toosuit требований приложения и избежать ложных положительных результатов.

## <a name="features"></a>Функции

Брандмауэр веб-приложения поставляется с предварительно настроенным CRS 3.0 по умолчанию или можно выбрать toouse 2.2.9. В предложениях CR 3.0 сократилось число ложноположительных результатов по сравнению с CR 2.2.9. Здравствуйте возможность слишком[настроить правила toosuit потребностями](application-gateway-customize-waf-rules-portal.md) предоставляется. Некоторые из распространенных web уязвимостей hello какие брандмауэр веб-приложения обеспечивает защиту от включает в себя:

* Защита от внедрения кода SQL.
* Защита от межсайтовых сценариев.
* Защита от распространенных сетевых атак, в том числе от внедрения команд, несанкционированных HTTP-запросов, разделения HTTP-запросов и атак с включением удаленного файла.
* Защита от нарушений протокола HTTP.
* Защита от аномалий протокола HTTP, например отсутствия агента пользователя узла и заголовков accept.
* Защита от программ-роботов, программ-обходчиков и сканеров.
* Обнаружение распространенных неправильных конфигураций приложений (Apache, IIS и т. д.).

Более подробный список правил и их защиты см. ниже hello [основные наборы правил](#core-rule-sets).

### <a name="core-rule-sets"></a>Основные наборы правил

Шлюз приложений поддерживает два набора правил: CRS 3.0 и CRS 2.2.9. Это основные наборы правил, защищающие веб-приложения от вредоносных действий.

#### <a name="owasp30"></a>OWASP_3.0

в предоставленном наборе правил core Hello 3.0 имеет 13 группы правил, как показано в следующей таблице hello. Каждая из этих групп правил содержит несколько правил, которые могут быть отключены.

|Группа правил|Описание|
|---|---|
|**[REQUEST-910-IP-REPUTATION](application-gateway-crs-rulegroups-rules.md#crs910)**|Содержит правила tooprotect от известных нежелательных сообщений или вредоносных действий.|
|**[REQUEST-911-METHOD-ENFORCEMENT](application-gateway-crs-rulegroups-rules.md#crs911)**|Содержит правила toolock списка методов (PUT, PATCH <..)|
|**[REQUEST-912-DOS-PROTECTION](application-gateway-crs-rulegroups-rules.md#crs912)**| Содержит правила tooprotect от атак отказа в обслуживании (DoS).|
|**[REQUEST-913-SCANNER-DETECTION](application-gateway-crs-rulegroups-rules.md#crs913)**| Содержит правила tooprotect от сканеры порт и среды.|
|**[REQUEST-920-PROTOCOL-ENFORCEMENT](application-gateway-crs-rulegroups-rules.md#crs920)**|Содержит правила tooprotect от протокола и кодирование проблемы.|
|**[REQUEST-921-PROTOCOL-ATTACK](application-gateway-crs-rulegroups-rules.md#crs921)**|Содержит правила tooprotect от внедрения заголовка, несанкционированном запроса и с разделением ответа|
|**[REQUEST-930-APPLICATION-ATTACK-LFI](application-gateway-crs-rulegroups-rules.md#crs930)**|Содержит правила tooprotect против атак, путь и имя файла.|
|**[REQUEST-931-APPLICATION-ATTACK-RFI](application-gateway-crs-rulegroups-rules.md#crs931)**|Содержит правила tooprotect от удаленного включения файлов (RFI)|
|**[REQUEST-932-APPLICATION-ATTACK-RCE](application-gateway-crs-rulegroups-rules.md#crs932)**|Содержит правила tooprotect снова удаленное выполнение кода.|
|**[REQUEST-933-APPLICATION-ATTACK-PHP](application-gateway-crs-rulegroups-rules.md#crs933)**|Содержит правила tooprotect от атак путем внедрения кода PHP.|
|**[REQUEST-941-APPLICATION-ATTACK-XSS](application-gateway-crs-rulegroups-rules.md#crs941)**|Содержит правила, обеспечивающие защиту от выполнения межсайтовых сценариев.|
|**[REQUEST-942-APPLICATION-ATTACK-SQLI](application-gateway-crs-rulegroups-rules.md#crs942)**|Содержит правила, обеспечивающие защиту от атак путем внедрения кода SQL.|
|**[REQUEST-943-APPLICATION-ATTACK-SESSION-FIXATION](application-gateway-crs-rulegroups-rules.md#crs943)**|Содержит правила tooprotect от атак Fixation сеанса.|

#### <a name="owasp229"></a>OWASP_2.2.9

в предоставленном наборе правил core Hello 2.2.9 имеет 10 групп правил, как показано в следующей таблице hello. Каждая из этих групп правил содержит несколько правил, которые могут быть отключены.

|Группа правил|Описание|
|---|---|
|**[crs_20_protocol_violations](application-gateway-crs-rulegroups-rules.md#crs20)**|Содержит правила tooprotect от нарушения протокола (недопустимые знаки, GET текст запроса, и т. д.)|
|**[crs_21_protocol_anomalies](application-gateway-crs-rulegroups-rules.md#crs21)**|Содержит правила tooprotect со сведениями неправильный заголовок.|
|**[crs_23_request_limits](application-gateway-crs-rulegroups-rules.md#crs23)**|Содержит правила tooprotect от аргументов или файлы, которые превышают ограничения.|
|**[crs_30_http_policy](application-gateway-crs-rulegroups-rules.md#crs30)**|Содержит правила tooprotect от запрещенных методов, заголовки и типы файлов. |
|**[crs_35_bad_robots](application-gateway-crs-rulegroups-rules.md#crs35)**|Содержит правила tooprotect от программ-обходчиков и сканеры.|
|**[crs_40_generic_attacks](application-gateway-crs-rulegroups-rules.md#crs40)**|Содержит правила tooprotect универсального атак (fixation сеанса, включение удаленных файлов, внедрение PHP, и т. д.)|
|**[crs_41_sql_injection_attacks](application-gateway-crs-rulegroups-rules.md#crs41sql)**|Содержит правила tooprotect от атак путем внедрения кода SQL|
|**[crs_41_xss_attacks](application-gateway-crs-rulegroups-rules.md#crs41xss)**|Содержит правила tooprotect от межсайтовых сценариев.|
|**[crs_42_tight_security](application-gateway-crs-rulegroups-rules.md#crs42)**|Содержит правила tooprotect от атак путем обхода|
|**[crs_45_trojans](application-gateway-crs-rulegroups-rules.md#crs45)**|Содержит правила tooprotect от программы-трояны.|

### <a name="waf-modes"></a>Режимы WAF

WAF шлюза приложения может быть настроенный toorun в hello, следующие два режима:

* **Режим обнаружения** — когда toorun, настроенного в режиме обнаружения, WAF шлюза приложения отслеживает и регистрирует все оповещения в файле журнала tooa. Ведение журнала диагностики для шлюза приложения должна быть включена с помощью hello **диагностики** раздела. Необходимо также tooensure, hello WAF журнала выбран и включен. В режиме обнаружения брандмауэр веб-приложения не блокирует входящие запросы.
* **Режим предотвращения** — блокировании toorun, настроенного в режиме защиты от шлюза приложений активно несанкционированного проникновения и атак на его правила. Hello злоумышленник получает 403 об исключении несанкционированного доступа и hello соединение будет разорвано. Режим предотвращения продолжается в журналах hello WAF toolog подобных атак.

### <a name="application-gateway-waf-reports"></a>Мониторинг WAF

Очень важно следить за hello работоспособности шлюза приложения. Наблюдение за работоспособностью hello веб-приложение брандмауэра и hello приложений, которые он защищает обеспечивается ведение журнала и интеграцию с монитора Azure, Центр безопасности Azure (ожидается в ближайшее время) и служба аналитики журналов.

![диагностика](./media/application-gateway-web-application-firewall-overview/diagnostics.png)

#### <a name="azure-monitor"></a>Azure Monitor

Каждый журнал шлюза приложений интегрирован с [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview.md).  Это позволяет tootrack диагностические сведения, включая журналы и оповещения WAF.  Эта возможность предоставляется в рамках hello ресурсов шлюза приложения hello портале в разделе hello **диагностики** вкладке или непосредственно через hello Azure монитор службы. Дополнительные сведения о включении журналов диагностики для шлюза приложения посетите toolearn [диагностику шлюза приложения](application-gateway-diagnostics.md)

#### <a name="azure-security-center"></a>Центр безопасности Azure

[Центр безопасности Azure](../security-center/security-center-intro.md) помогает предотвратить, обнаружить и вернуть toothreats Повышенная видимость и контроль над hello безопасность ресурсов Azure. Шлюз приложений теперь [интегрируется в центр безопасности Azure](application-gateway-integration-security-center.md). Azure центр обеспечения безопасности проверяет среды toodetect защиту веб-приложений. Теперь он, tooprotect WAF шлюза приложения может рекомендовать эти ресурсы уязвимым. WAF шлюза приложения можно создавать напрямую из центра безопасности Azure hello.  Эти экземпляры WAF интегрированы с центром обеспечения безопасности Azure и будет отправлять оповещения и сведения о работоспособности обратно tooAzure центра обеспечения безопасности для отчетов.

![Рисунок 1](./media/application-gateway-web-application-firewall-overview/figure1.png)

#### <a name="logging"></a>Ведение журналов

WAF шлюза приложений предоставляет подробные отчеты о каждой из обнаруженных угроз. Функция ведения журналов интегрирована с журналами системы диагностики Azure, и оповещения записываются в формате JSON. Эти журналы можно интегрировать с [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).

![imageURLroute](./media/application-gateway-web-application-firewall-overview/waf2.png)

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupId}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{appGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

## <a name="application-gateway-waf-sku-pricing"></a>Цена на SKU для WAF шлюза приложений

Брандмауэр веб-приложения предоставляется в новом номере SKU WAF. Этот номер SKU доступен только в модели инициализации диспетчера ресурсов Azure, а не в разделе hello классической модели развертывания. Кроме того, в пределах номера SKU WAF поставляются только экземпляры шлюза приложений среднего и крупного размера. Все ограничения hello для шлюза приложения также применяются toohello WAF SKU. Цена зависит от почасовой стоимости использования экземпляра шлюза и стоимости обработки данных. Почасовая стоимость использования номера SKU WAF и стандартного номера SKU отличается. Дополнительные сведения см. на [странице цен на шлюз приложений](https://azure.microsoft.com/pricing/details/application-gateway/). При обработке данных остаются расходов hello таким же. Плата за правило или группу правил отсутствует. Чтобы защитить несколько веб-приложений за hello же веб-приложение брандмауэра и отсутствуют дополнительные накладные расходы для поддержки нескольких приложений. 

Выставление счетов для WAF эффективно начинается 5/5/2017 г., пока затем hello шлюзы WAF SKU продолжает взиматься стандартные тарифы toobe.

## <a name="next-steps"></a>Дальнейшие действия

После изучения возможностей hello WAF, посетите [как tooconfigure веб-приложение брандмауэра на использование шлюза приложений](application-gateway-web-application-firewall-portal.md).

