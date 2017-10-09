Прежде чем использовать hello Azure CLI с помощью диспетчера ресурсов команды и шаблоны toodeploy Azure ресурсы и рабочие нагрузки с помощью групп ресурсов, вам потребуется учетная запись с Azure. Если у вас нет учетной записи, бесплатную пробную версию Azure можно получить [здесь](https://azure.microsoft.com/pricing/free-trial/).

Если вы еще не установили hello Azure CLI и tooyour подключенных подписка, см. раздел [Install hello Azure CLI](../articles/cli-install-nodejs.md) режим hello слишком`arm` с `azure config mode arm`и подключения tooAzure hello `azure login` команды.

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI
Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

- Azure CLI 10 – нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](../articles/virtual-machines/linux/cli-manage.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a>Основные команды Azure Resource Manager в Azure CLI
В этой статье рассматриваются основные команды будет требуется toouse с toomanage Azure CLI и взаимодействия с ресурсами (в первую очередь виртуальных машин) в вашей подписке Azure.  Более подробные справки определенные параметры командной строки и параметры, можно использовать hello интерактивной справки и параметры, введя `azure <command> <subcommand> --help` или `azure help <command> <subcommand>`.

> [!NOTE]
> Эти примеры не включают операции на основе шаблонов, которые обычно рекомендуются для развертываний виртуальных машин в диспетчере ресурсов. Сведения см. в разделе [используйте hello Azure CLI с помощью диспетчера ресурсов Azure](../articles/xplat-cli-azure-resource-manager.md) и [развертывание и управление виртуальными машинами с помощью шаблонов диспетчера ресурсов Azure и Azure CLI hello](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

| Задача | Диспетчер ресурсов |
| --- | --- | --- |
| Создание hello основной виртуальной Машины |`azure vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password>`<br/><br/>(Получить hello `image-urn` из hello `azure vm image list` команды. Примеры см. в [этой статье](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).) |
| Создание виртуальной машины Linux |`azure  vm create [options] <resource-group> <name> <location> -y "Linux"` |
| Создание виртуальной машины Windows |`azure  vm create [options] <resource-group> <name> <location> -y "Windows"` |
| Вывод списка виртуальных машин |`azure  vm list [options]` |
| Получение информации о виртуальной машине |`azure  vm show [options] <resource_group> <name>` |
| Запуск виртуальной машины |`azure vm start [options] <resource_group> <name>` |
| Остановка виртуальной машины |`azure vm stop [options] <resource_group> <name>` |
| Освобождение виртуальной машины |`azure vm deallocate [options] <resource-group> <name>` |
| Перезапуск виртуальной машины |`azure vm restart [options] <resource_group> <name>` |
| Удаление виртуальной машины |`azure vm delete [options] <resource_group> <name>` |
| Запись виртуальной машины |`azure vm capture [options] <resource_group> <name>` |
| Создание виртуальной машины из образа пользователя |`azure  vm create [options] –q <image-name> <resource-group> <name> <location> <os-type>` |
| Создание виртуальной машины из специализированного диска |`azue  vm create [options] –d <os-disk-vhd> <resource-group> <name> <location> <os-type>` |
| Добавить tooa диска данных виртуальной Машины |`azure  vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]` |
| Удаление диска данных от виртуальной машины |`azure  vm disk detach [options] <resource-group> <vm-name> <lun>` |
| Добавление расширения tooa виртуальной Машины |`azure  vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>` |
| Добавьте расширение доступа к ВМ tooa виртуальной Машины |`azure vm reset-access [options] <resource-group> <name>` |
| Добавление расширения Docker tooa виртуальной Машины |`azure  vm docker create [options] <resource-group> <name> <location> <os-type>` |
| Удаление расширения виртуальной машины |`azure  vm extension set [options] –u <resource-group> <vm-name> <name> <publisher-name> <version>` |
| Получение сведений об использовании ресурсов виртуальной машины |`azure vm list-usage [options] <location>` |
| Получить все доступные размеры виртуальной машины |`azure vm sizes [options]` |

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные примеры команд CLI hello, помимо базовую функциональность для управления виртуальной Машины см. в разделе [использование hello Azure CLI с помощью диспетчера ресурсов Azure](../articles/virtual-machines/azure-cli-arm-commands.md).
