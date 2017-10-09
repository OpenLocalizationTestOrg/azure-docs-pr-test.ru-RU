


В этом разделе описываются следующие действия:

* включение данных в виртуальную машину Azure при ее подготовке;
* извлечение их для Windows и Linux;
* Использование специальных средств, доступных в некоторых системах toodetect и автоматически обрабатывать пользовательские данные.

> [!NOTE]
> В этой статье описывается, как пользовательские данные могут быть добавлены с помощью виртуальных Машин, созданных с помощью hello API управления службами Azure. toouse hello Azure ресурсов API-интерфейса управления. в статье toosee [hello пример шаблона](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a>Включение пользовательских данных в виртуальную машину Azure
Эта функция в настоящее время поддерживается только в hello [интерфейса командной строки Azure](https://github.com/Azure/azure-xplat-cli). Здесь мы создадим `custom-data.txt` файл, который содержит ваши данные, затем вставить, в toohello виртуальной Машины во время инициализации. Однако вы можете использовать любой из параметров hello для hello `azure vm create` команды hello следующий код демонстрирует один подход очень простой:

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a>Использование пользовательских данных в виртуальной машине hello
* Если ВМ Azure виртуальной Машины на основе Windows, то файл hello пользовательских данных сохраняется слишком`%SYSTEMDRIVE%\AzureData\CustomData.bin`. Несмотря на то, что она была tootransfer кодировке base64 из локального компьютера toohello hello новой виртуальной Машины, она будет автоматически декодировать и можно открыть или использовать немедленно.
  
  > [!NOTE]
  > Если hello файл существует, он будет переопределен. безопасность Hello в каталоге hello задано слишком**System: Full Control** и **Administrators: Full Control**.
  > 
  > 
* Если ВМ Azure представляет собой виртуальную Машину под управлением Linux, то hello пользовательских данных файл будет находиться в одно из следующих hello помещает в зависимости от вашей дистрибутив. Hello данные могут быть кодировке base64, поэтому может потребоваться сначала toodecode hello данных:
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a>Cloud-Init в Azure
Если из Ubuntu или CoreOS образа ВМ Azure, можно использовать toosend CustomData облачной конфигурации toocloud-init. Если же файл пользовательских данных является сценарием, пакет cloud-init может просто выполнить его.

### <a name="ubuntu-cloud-images"></a>Образы облаков Ubuntu
В большинстве изображений Azure Linux изменение «/ etc/waagent.conf» tooconfigure hello временный диск и замены файла ресурсов. Дополнительные сведения см. в [руководстве пользователя агента Linux Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Тем не менее, на изображениях облака Ubuntu hello, необходимо использовать облака init tooconfigure hello ресурсов диск (т. е hello «эфемерных») и переключения секций. См. следующие страницы на вики-сайте Ubuntu hello подробнее hello: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a>Дальнейшие действия: использование пакета cloud-init
Дополнительные сведения см. в разделе hello [документации init облака для Ubuntu](https://help.ubuntu.com/community/CloudInit).

<!--Link references-->
[Справочник по REST API управления добавлением службы роли](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[Интерфейс командной строки Azure](https://github.com/Azure/azure-xplat-cli)

