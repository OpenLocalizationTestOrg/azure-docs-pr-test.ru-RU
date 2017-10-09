## <a name="public-ip-address"></a>Общедоступный IP-адрес
Ресурс общедоступного IP-адреса предоставляет зарезервированный или динамический общедоступный IP-адрес для Интернета. Несмотря на то, что вы сможете создать общедоступный IP-адрес в виде отдельного объекта, необходимо tooassociate его tooactually tooanother объекта используйте адрес hello. Можно связать балансировщик нагрузки tooa открытый IP адрес, шлюз приложений или toothose Сетевых Internet tooprovide доступ к ресурсам.  

| Свойство | Описание | Примеры значений |
| --- | --- | --- |
| **publicIPAllocationMethod** |Определяет, если IP-адрес hello *статических* или *динамическое*. |static, dynamic |
| **idleTimeoutInMinutes** |Определяет hello аут времени бездействия, значение по умолчанию 4 минуты. Если дополнительные пакеты для данного сеанса не получено в течение этого времени, hello сеанс завершен. |любое значение от 4 до 30 |
| **ipAddress** |Tooobject назначить IP-адрес. Это свойство доступно только для чтения. |104.42.233.77 |

### <a name="dns-settings"></a>Параметры DNS
Общедоступные IP-адреса иметь дочерний объект с именем **dnsSettings** содержащий hello следующие свойства:

| Свойство | Описание | Примеры значений |
| --- | --- | --- |
| **domainNameLabel** |Узел для разрешения имен. |www, ftp, vm1 |
| **fqdn** |Полное имя для hello общедоступный IP-адрес. |www.westus.cloudapp.azure.com |
| **reverseFqdn** |Полное доменное имя, которое разрешает toohello IP-адрес и зарегистрирован в DNS, как запись PTR. |www.contoso.com. |

Пример общедоступного IP-адреса в формате JSON:

    {
       "name": "PIP01",
       "location": "North US",
       "tags": { "key": "value" },
       "properties": {
          "publicIPAllocationMethod": "Static",
          "idleTimeoutInMinutes": 4,
          "ipAddress": "104.42.233.77",
          "dnsSettings": {
             "domainNameLabel": "mylabel",
             "fqdn": "mylabel.westus.cloudapp.azure.com",
             "reverseFqdn": "contoso.com."
          }
       }
    } 

### <a name="additional-resources"></a>Дополнительные ресурсы
* См. дополнительные сведения об [общедоступных IP-адресах](../articles/virtual-network/virtual-networks-reserved-public-ip.md).
* Узнайте об [общедоступных IP-адресах уровня экземпляра](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).
* Чтение hello [справочной документации REST API](https://msdn.microsoft.com/library/azure/mt163638.aspx) для открытого IP-адресов.

