


## <a name="using-vm-extensions"></a>Использование расширений виртуальной машины
Расширений ВМ Azure реализуют поведение и функции, которые либо помогают другие программы, которые работают на виртуальных машинах Azure (например, hello **WebDeployForVSDevTest** расширение позволяет развернуть решения Visual Studio tooWeb на ВМ Azure) или укажите Здравствуйте, возможность toointeract с toosupport ВМ hello другие правила поведения (например, можно использовать расширения Access ВМ hello из hello Azure CLI, tooreset клиентов REST и PowerShell или изменения значений удаленного доступа на ВМ Azure).

> [!IMPORTANT]
> Полный список расширений по поддерживаемым ими функциям hello см. в разделе [расширений ВМ Azure и компоненты](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Поскольку каждое расширение ВМ поддерживает конкретную функцию, именно то, что можно и нельзя выполнить с помощью расширения зависит от расширения hello. Таким образом перед изменением ВМ, убедитесь, что вы прочитали hello документацию для расширения виртуальной Машины требуется toouse hello. Одни расширения ВМ нельзя удалить, а другие имеют такие свойства, изменение которых радикальным образом меняет реакцию ВМ на события.
> 
> 

Ниже перечислены наиболее распространенные задачи Hello:

1. Поиск доступных расширений.
2. Обновление загруженных расширений.
3. Добавление расширений.
4. Удаление расширений.

## <a name="find-available-extensions"></a>Поиск доступных расширений
Вы можете найти расширения и дополнительную информацию, используя:

* PowerShell
* Использование кросс-платформенного интерфейса командной строки Azure (Azure CLI)
* Интерфейс API REST управления службой

### <a name="azure-powershell"></a>Azure PowerShell
Некоторые модули имеют командлетов PowerShell, которые являются определенной toothem, что упрощает их конфигурации из PowerShell; но hello следующие командлеты действуют для всех расширений ВМ.

Можно использовать следующие командлеты tooobtain сведения о доступных расширениях hello.

* Для экземпляров веб-ролей или рабочих ролей, можно использовать hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) командлета.
* Для экземпляров виртуальных машин можно использовать hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) командлета.
  
   Здравствуйте, например, следующая примере кода показано, как toolist сведения для hello **IaaSDiagnostics** расширение с помощью PowerShell.
  
      PS C:\> Get-AzureVMAvailableExtension -ExtensionName IaaSDiagnostics
  
      Publisher                   : Microsoft.Azure.Diagnostics
      ExtensionName               : IaaSDiagnostics
      Version                     : 1.2
      Label                       : Microsoft Monitoring Agent Diagnostics
      Description                 : Microsoft Monitoring Agent Extension
      PublicConfigurationSchema   :
      PrivateConfigurationSchema  :
      IsInternalExtension         : False
      SampleConfig                :
      ReplicationCompleted        : True
      Eula                        :
      PrivacyUri                  :
      HomepageUri                 :
      IsJsonExtension             : True
      DisallowMajorVersionUpgrade : False
      SupportedOS                 :
      PublishedDate               :
      CompanyName                 :

### <a name="azure-command-line-interface-azure-cli"></a>Интерфейс командной строки Azure (Azure CLI)
Некоторые модули имеют Azure CLI-команд, определенных toothem (hello расширение ВМ Docker является одним из примеров), который может упростить их конфигурации; но hello следующие команды работают для всех расширений ВМ.

Можно использовать hello **список расширений ВМ azure** tooobtain сведения о доступных расширениях команды и использовать hello **–-json** параметр toodisplay все доступные сведения о одно или несколько расширений. Если вы не используете расширение, hello команда возвращает JSON-описание всех доступных расширений.

Привет, в следующем примере кода показано, как toolist hello сведения для hello **IaaSDiagnostics** расширение с помощью Azure CLI "hello" **список расширений ВМ azure** команда и использует hello **–-json** параметр tooreturn полные сведения.

    $ azure vm extension list -n IaaSDiagnostics --json
    [
      {
        "publisher": "Microsoft.Azure.Diagnostics",
        "name": "IaaSDiagnostics",
        "version": "1.2",
        "label": "Microsoft Monitoring Agent Diagnostics",
        "description": "Microsoft Monitoring Agent Extension",
        "replicationCompleted": true,
        "isJsonExtension": true
      }
    ]



### <a name="service-management-rest-apis"></a>REST API управления службой
Можно использовать следующие API-интерфейс REST tooobtain сведения о доступных расширениях hello.

* Для экземпляров веб-ролей или рабочих ролей, можно использовать hello [перечисления доступных расширений](https://msdn.microsoft.com/library/dn169559.aspx) операции. версии hello toolist доступных расширений, можно использовать [перечисление версий расширения](https://msdn.microsoft.com/library/dn495437.aspx).
* Для экземпляров виртуальных машин можно использовать hello [перечисления расширений ресурсов](https://msdn.microsoft.com/library/dn495441.aspx) операции. версии hello toolist доступных расширений, можно использовать [перечисление версий расширения ресурса](https://msdn.microsoft.com/library/dn495440.aspx).

## <a name="add-update-or-disable-extensions"></a>Добавление, обновление или отключение расширений
Расширения можно добавить при создании экземпляра или могут быть добавлены tooa, на котором запущен экземпляр. Расширения можно обновить, отключить или удалить. Эти действия можно выполнять с помощью командлетов Azure PowerShell или с помощью операций API REST управления службами hello. Tooinstall необходимые параметры и настройки некоторых расширений. Для расширений поддерживаются общедоступные и частные параметры.

### <a name="azure-powershell"></a>Azure PowerShell
С помощью командлетов Azure PowerShell — hello простым способом tooadd и обновления расширений. При использовании командлетов расширения hello, большая часть конфигурации hello hello расширения выполняется за вас. В некоторых случаях может потребоваться tooprogrammatically добавить расширение. При необходимости toodo это, необходимо предоставить hello конфигурации расширения hello.

Можно использовать следующие командлеты tooknow, требуется ли для расширения Настройка общедоступных и частных параметров hello.

* Для экземпляров веб-ролей или рабочих ролей, можно использовать hello **Get-AzureServiceAvailableExtension** командлета.
* Для экземпляров виртуальных машин можно использовать hello **Get-AzureVMAvailableExtension** командлета.

### <a name="service-management-rest-apis"></a>REST API управления службой
При получении списка доступных расширений с помощью API-интерфейсов REST hello, вы получите информацию о том, как настроить toobe hello расширения. Возвращаемая информация Hello может показывать сведения о параметрах, представленных общедоступной схемы и частной схемы. Значения общедоступных параметров возвращаются в запросах об экземплярах hello. Значения частных параметров не возвращаются.

Можно использовать следующие API-интерфейс REST tooknow, требуется ли для расширения Настройка общедоступных и частных параметров hello.

* Для экземпляров веб-ролей или рабочих ролей hello **PublicConfigurationSchema** и **PrivateConfigurationSchema** элементы содержат данные hello в ответ hello из hello [списка Доступные расширения](https://msdn.microsoft.com/library/dn169559.aspx) операции.
* Для экземпляров виртуальных машин hello **PublicConfigurationSchema** и **PrivateConfigurationSchema** элементы содержат данные hello в ответ hello из hello [списка Расширения ресурсов](https://msdn.microsoft.com/library/dn495441.aspx) операции.

> [!NOTE]
> Кроме того, расширения могут использовать конфигурации, заданные с помощью JSON. Если такие типы расширений используются, только hello **SampleConfig** используется элемент.
> 
> 

