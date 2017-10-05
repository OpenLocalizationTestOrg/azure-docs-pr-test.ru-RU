# Обзор
## [About Azure virtual machines (Сведения о виртуальных машинах Azure)](../../virtual-machines-windows-about.md)
## [Диски и виртуальные жесткие диски](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
## [Виртуальные сети](../../../virtual-network/virtual-networks-overview.md)
## [Часто задаваемые вопросы](faq.md)
## [Сравнение службы приложений Azure, виртуальных машин, Service Fabric и облачных служб](../../../app-service-web/choose-web-site-cloud-service-vm.md)
## [Контейнеры](../../virtual-machines-windows-containers.md)

# Начало работы
## [Создание виртуальной машины с помощью портала](tutorial.md)
## [Вход на виртуальную машину](connect-logon.md)
## [Установка Azure PowerShell](/powershell/azure/overview)
## [Установка Azure CLI](../../../cli-install-nodejs.md)

# Практическое руководство

## Использование хранилища
### [Подключение диска данных](attach-disk.md)
### [Отключение диска данных](detach-disk.md)
### [Использование диска D: в качестве диска данных](../../virtual-machines-windows-change-drive-letter.md)

## Сеть
### [Как настроить конечные точки](setup-endpoints.md)
### [Подключение виртуальных машин с помощью виртуальной сети или облачной службы](connect-vms.md)
### [Подключение классических виртуальных сетей к виртуальным сетям Resource Manager](../../../vpn-gateway/vpn-gateway-connect-different-deployment-models-powershell.md)
### [Создание балансировщика нагрузки](../../../load-balancer/load-balancer-get-started-internet-classic-portal.md)
### [Как создать группы безопасности сети (классические) в PowerShell](../../../virtual-network/virtual-networks-create-nsg-classic-ps.md)

## Развернуть
### [Создание настраиваемой виртуальной машины](createportal.md)
### [Создание и настройка виртуальной машины с помощью Azure PowerShell](create-powershell.md)
### [Запись виртуальной машины Windows](capture-image.md)
### [Создание и передача виртуального жесткого диска с помощью PowerShell](createupload-vhd.md)
### [Автоматизация развертывания виртуальной машины Azure с помощью Chef](../../virtual-machines-windows-chef-automation.md)
### [Создание виртуальных машин и управление ими в Visual Studio](manage-visual-studio.md)
### [Создание виртуальной машины для веб-приложения с помощью Visual Studio](web-app-visual-studio.md)
### [Выполнение ресурсоемкой задачи в Java-коде](java-run-compute-intensive-task.md)
### [Веб-приложение Hello World на Django](python-django-web-app.md)

## Настройка
### [Сброс службы удаленного рабочего стола или ее пароля](../../virtual-machines-windows-reset-rdp.md)
### [Установка и настройка Symantec Endpoint Protection](install-symantec.md)
### [Установка и настройка Trend Micro Deep Security как услуги](install-trend.md)
### [Настройка группы доступности](configure-availability.md)
### [Изменение размера виртуальной машины Windows, созданной в классической модели развертывания](resize-vm.md)
### [Обслуживание](planned-maintenance-schedule.md)

## Управление
### [Переход с классической модели на модель Resource Manager](../../virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
### [Управление виртуальными машинами с помощью Azure PowerShell](manage-psh.md)
### [Сведения об агенте и расширениях виртуальной машины](agents-and-extensions.md)
### [Управление расширениями виртуальной машины](manage-extensions.md)
### [Расширение пользовательских сценариев для виртуальных машин](extensions-customscript.md)
### [Включение пользовательских данных в виртуальную машину Azure](inject-custom-data.md)

## План
### [Сведения об образах](about-images.md)
### [Размеры виртуальных машин](../../virtual-machines-windows-sizes.md)
### [Плановое обслуживание для виртуальных машин Azure](../../virtual-machines-windows-planned-maintenance.md)
### [Руководство по реализации служб инфраструктуры Azure](../../virtual-machines-windows-infrastructure-subscription-accounts-guidelines.md)

## Управление рабочими нагрузками
### [Высокопроизводительные вычислительные системы (HPC)](../../virtual-machines-windows-hpcpack-cluster-options.md)
#### [Автоматическое масштабирование ресурсов](hpcpack-cluster-node-autogrowshrink.md)
#### [Управление вычислительными узлами](hpcpack-cluster-node-manage.md)
#### [Создание кластера](hpcpack-cluster-powershell-script.md)
#### [Настройка кластера для выполнения приложений MPI](hpcpack-rdma-cluster.md)
#### [Запуск рабочих нагрузок Excel и SOA](../../virtual-machines-windows-excel-cluster-hpcpack.md)
#### [Создание головного узла с помощью образа Marketplace](../../virtual-machines-windows-hpcpack-cluster-headnode.md)
#### [Отправка заданий из локальной среды в Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md)
### [MongoDB](install-mongodb.md)
### [MySQL](mysql-2008r2.md)
### [Oracle](../../workloads/oracle/oracle-considerations.md)
### [SAP](sap-get-started.md)
### [SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)
### [Tomcat](java-run-tomcat-app-server.md)

## Устранение неполадок
### [Подключения к удаленному рабочему столу](../../virtual-machines-windows-troubleshoot-rdp-connection.md)
####[Подробное руководство по устранению неполадок с подключением к удаленному рабочему столу](../../virtual-machines-windows-detailed-troubleshoot-rdp.md)
### [Доступ к приложению](../../virtual-machines-windows-troubleshoot-app-connection.md)
### [Неполадки в классическом развертывании при создании виртуальной машины](troubleshoot-deployment-new-vm.md)
### [Неполадки в классическом развертывании при перезагрузке или изменении размера существующей виртуальной машины](virtual-machines-windows-classic-restart-resize-error-troubleshooting.md)
### [Сброс пароля удаленного рабочего стола](reset-rdp.md)
### [Подключение виртуального жесткого диска для устранения неполадок виртуальной машины](troubleshoot-recovery-disks-portal.md)

# Справочные материалы
## [PowerShell](/powershell/azure/overview)
## [Интерфейс командной строки Azure](/cli/azure/vm)
## [Java](/java/api)
## [.NET](/dotnet/api/microsoft.azure.management.compute)
## [Создание шаблонов Resource Manager](../../../resource-group-authoring-templates.md)
## [Шаблоны, созданные сообществом](https://azure.microsoft.com/documentation/templates)
## [REST для вычислений](/rest/api/compute)
## [REST для сети](/rest/api)
## [REST для службы хранилища](/rest/api/storageservices)

# Ресурсы
## [Стратегия развития Azure](https://azure.microsoft.com/roadmap/?category=compute)
## [Цены](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)
## [Калькулятор цен](https://azure.microsoft.com/pricing/calculator/)
## [Доступность по регионам](https://azure.microsoft.com/regions/services/)
## [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-virtual-machine)
## [Видеоролики](https://azure.microsoft.com/documentation/videos/index/?services=virtual-machines)
