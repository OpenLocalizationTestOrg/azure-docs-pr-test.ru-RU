Чтобы использовать интерфейс командной строки Azure (CLI) с командами и шаблонами Resource Manager для развертывания ресурсов Azure и рабочих нагрузок с помощью групп ресурсов, вам потребуется учетная запись Azure. Если у вас нет учетной записи, бесплатную пробную версию Azure можно получить [здесь](https://azure.microsoft.com/pricing/free-trial/).

Если вы еще не установили интерфейс командной строки Azure и не подключили его к своей подписке, см. статью [Установка Azure CLI](../articles/cli-install-nodejs.md), в которой режим `arm` устанавливается с помощью команды `azure config mode arm`, а подключение к Azure — с помощью команды `azure login`.

## <a name="cli-versions-to-complete-the-task"></a>Версии интерфейса командной строки для выполнения задачи
Вы можете выполнить задачу, используя одну из следующих версий интерфейса командной строки.

- Azure CLI 10 — интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager (в этой статье).
- [Azure CLI 2.0](../articles/virtual-machines/linux/cli-manage.md) — интерфейс командной строки следующего поколения для модели развертывания с помощью Resource Manager.

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a>Основные команды Azure Resource Manager в Azure CLI
В этой статье рассматриваются основные команды в интерфейсе командной строки Azure для управления и взаимодействия с ресурсами (в основном виртуальными машинами) в подписке Azure.  Чтобы получить подробные сведения о конкретных параметрах командной строки, можно использовать интерактивную справку по командам, к которой можно получить доступ с помощью команд `azure <command> <subcommand> --help` или `azure help <command> <subcommand>`.

> [!NOTE]
> Эти примеры не включают операции на основе шаблонов, которые обычно рекомендуются для развертываний виртуальных машин в диспетчере ресурсов. Дополнительные сведения см. в статье [Использование интерфейса командной строки Azure с диспетчером ресурсов Azure](../articles/xplat-cli-azure-resource-manager.md) и [Развертывание виртуальных машин и управление ими с помощью шаблонов диспетчера ресурсов Azure и интерфейса командной строки Azure](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

| Задача | Диспетчер ресурсов |
| --- | --- | --- |
| Создание самой простой виртуальной машины |`azure vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password>`<br/><br/>(Получите `image-urn` из команды `azure vm image list`. Примеры см. в [этой статье](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).) |
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
| Добавление диска данных в виртуальную машину |`azure  vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]` |
| Удаление диска данных от виртуальной машины |`azure  vm disk detach [options] <resource-group> <vm-name> <lun>` |
| Добавление универсального расширения в виртуальную машину |`azure  vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>` |
| Добавление в виртуальную машину расширения VM Access |`azure vm reset-access [options] <resource-group> <name>` |
| Добавление в виртуальную машину расширения Docker |`azure  vm docker create [options] <resource-group> <name> <location> <os-type>` |
| Удаление расширения виртуальной машины |`azure  vm extension set [options] –u <resource-group> <vm-name> <name> <publisher-name> <version>` |
| Получение сведений об использовании ресурсов виртуальной машины |`azure vm list-usage [options] <location>` |
| Получить все доступные размеры виртуальной машины |`azure vm sizes [options]` |

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные примеры команд интерфейса командной строки, которые не относятся к основным командам для управления виртуальными машинами, см. в статье [Использование Azure CLI с Azure Resource Manager](../articles/virtual-machines/azure-cli-arm-commands.md).
