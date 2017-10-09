UnifiedSetup.exe [/ ServerMode < CS-PS >] [/ Диск_установки <DriveLetter>] [/ MySQLCredsFilePath <MySQL credentials file path>] [/ VaultCredsFilePath <Vault credentials file path>] [/ EnvType < VMWare/NonVMWare >] [/ PSIP < toobe IP адрес, используемый для передачи данных] [/CSIP <IP address of CS toobe registered with>] [/ PassphraseFilePath <Passphrase file path>]

Параметры

* /ServerMode. (Обязательный параметр.) Указывает ли серверах hello конфигурации и процесс должен быть установлен или hello только сервер обработки. Входные значения: CS, PS.
* InstallLocation. Папка Hello в какой hello компоненты установлены.
* /MySQLCredsFilePath. (Обязательный параметр.) в какой hello MySQL хранятся учетные данные сервера путь к файлу Hello. Hello файл должен быть в следующем формате:
* [MySQLCredentials]
* MySQLRootPassword = "<Password>"
* MySQLUserPassword = "<Password>"
* /VaultCredsFilePath. (Обязательный параметр.) расположение файла учетных данных хранилища hello Hello
* /EnvType. (Обязательный параметр.) Тип установки Hello. Значения: VMware, NonVMware.
* /PSIP и /CSIP. (Обязательный параметр.) Hello IP-адрес сервера обработки hello и конфигурации сервера.
* /PassphraseFilePath. (Обязательный параметр.) Hello расположение файла hello парольную фразу.
* /BypassProxy. необязательный параметр. Указывает, что на сервере конфигурации hello подключается tooAzure без учетной записи-посредника.
* /ProxySettingsFilePath. необязательный параметр. Параметры прокси-сервера (прокси-сервер по умолчанию hello требует проверки подлинности или пользовательский прокси-сервер). Hello файл должен быть в следующем формате:
* [ProxySettings]
* ProxyAuthentication = "Да/Нет"
* Proxy IP = "IP-адрес>"
* ProxyPort = "<Port>"
* ProxyUserName="<User Name>"
* ProxyPassword="<Password>"
* DataTransferSecurePort. необязательный параметр. Hello номер порта для репликации данных.
* SkipSpaceCheck. необязательный параметр. Пропускает проверку пространства для кэша.
* AcceptThirdpartyEULA. (Обязательный параметр.) Принимает лицензионное соглашение стороннего hello.
* ShowThirdpartyEULA. (Обязательный параметр.) Отображает лицензионное соглашение со сторонним разработчиком. Если оно задано как источник данных, все остальные параметры игнорируются.
