Hello Azure CLI 2.0 позволяет вам toocreate и управления ресурсами на macOS, Linux и Windows Azure. В этой статье подробно описываются некоторые наиболее распространенные команды toocreate hello и управление виртуальными машинами (ВМ).

В этой статье требуется hello Azure CLI версия 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Получить tooupgrade [установить CLI Azure 2.0](/cli/azure/install-azure-cli). Вы также можете использовать [Cloud Shell](/azure/cloud-shell/quickstart) из своего браузера.

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a>Основные команды Azure Resource Manager в Azure CLI
Более подробные справки определенные параметры командной строки и параметры, можно использовать hello интерактивной справки и параметры, введя `az <command> <subcommand> --help`.

### <a name="create-vms"></a>Создание виртуальных машин
| Задача | Команды интерфейса командной строки Azure |
| --- | --- |
| Создание группы ресурсов | `az group create --name myResourceGroup --location eastus` |
| Создание виртуальной машины Linux | `az vm create --resource-group myResourceGroup --name myVM --image ubuntults` |
| Создание виртуальной машины Windows | `az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter` |

### <a name="manage-vm-state"></a>Управление состоянием виртуальной машины
| Задача | Команды интерфейса командной строки Azure |
| --- | --- |
| Запуск виртуальной машины | `az vm start --resource-group myResourceGroup --name myVM` |
| Остановка виртуальной машины | `az vm stop --resource-group myResourceGroup --name myVM` |
| Освобождение виртуальной машины | `az vm deallocate --resource-group myResourceGroup --name myVM` |
| Перезапуск виртуальной машины | `az vm restart --resource-group myResourceGroup --name myVM` |
| Повторное развертывание виртуальной машины | `az vm redeploy --resource-group myResourceGroup --name myVM` |
| Удаление виртуальной машины | `az vm delete --resource-group myResourceGroup --name myVM` |

### <a name="get-vm-info"></a>Получение сведений о виртуальной машине
| Задача | Команды интерфейса командной строки Azure |
| --- | --- |
| Вывод списка виртуальных машин | `az vm list` |
| Получение информации о виртуальной машине | `az vm show --resource-group myResourceGroup --name myVM` |
| Получение сведений об использовании ресурсов виртуальной машины | `az vm list-usage --location eastus` |
| Получить все доступные размеры виртуальной машины | `az vm list-sizes --location eastus` |

## <a name="disks-and-images"></a>Диски и образы
| Задача | Команды интерфейса командной строки Azure |
| --- | --- |
| Добавить tooa диска данных виртуальной Машины | `az vm disk attach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk --size-gb 128 --new ` |
| Удаление диска данных от виртуальной машины | `az vm disk detach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk` |
| Изменение размера диска | `az disk update --resource-group myResourceGroup --name myDataDisk --size-gb 256` |
| Моментальный снимок диска | `az snapshot create --resource-group myResourceGroup --name mySnapshot --source myDataDisk` |
| Создание образа виртуальной машины | `az image create --resource-group myResourceGroup --source myVM --name myImage` |
| Создание виртуальной машины на основе образа | `az vm create --resource-group myResourceGroup --name myNewVM --image myImage` |


## <a name="next-steps"></a>Дальнейшие действия
Дополнительные примеры hello командах CLI см. в разделе hello [Создание и управление виртуальными машинами Linux с hello Azure CLI](../articles/virtual-machines/linux/tutorial-manage-vm.md) учебника.

