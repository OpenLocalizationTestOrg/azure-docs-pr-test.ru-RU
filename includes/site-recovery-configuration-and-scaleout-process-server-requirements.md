| **Оборудование** | |
| --- |---|
| Количество ядер ЦП| 8 |
| ОЗУ| 12 ГБ|
| Количество дисков | 3 <br><br> — диск ОС;<br> — диск кэша сервера обработки;<br> — диск хранения (для восстановления размещения).|
| Свободное место на диске (кэш сервера обработки) | 600 ГБ
| Свободное место на диске (диск хранения) | 600 ГБ|
| **Программное обеспечение** | |
| Версия операционной системы | Windows Server 2012 R2 |
| Язык операционной системы | Английский (en-us)|
| Версия VMware vSphere PowerCLI | [PowerCLI 6.0](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1 "PowerCLI 6.0")|
| Роли Windows Server | Не включайте hello следующих ролей: <br> — доменные службы Active Directory; <br>— службы IIS; <br> — Hyper-V. |
| **Сеть** | |
| Тип карты сетевого интерфейса | VMXNET3 |
| Тип IP-адреса | Статическое |
| Доступ к Интернету | Hello сервер должен быть hello может tooaccess следующие URL-адреса, напрямую или через прокси-сервер: <br> - \*.accesscontrol.windows.net<br> - \*.backup.windowsazure.com <br>- \*.store.core.windows.net<br> - \*.blob.core.windows.net<br> - \*.hypervrecoverymanager.windowsazure.com <br> - https://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi (не требуется для сервера обработки масштабирования) <br> time.nist.gov <br> time.windows.com |
| порты; | 443 (оркестрация канала управления)<br>9443 (передача данных)|
