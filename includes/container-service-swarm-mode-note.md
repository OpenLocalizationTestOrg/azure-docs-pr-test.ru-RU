> [!NOTE]
> orchestrator помощью Docker Swarm Hello в службе контейнера Azure использует устаревший автономный группу мелких объектов. В настоящее время интегрирован hello [режим группу мелких объектов](https://docs.docker.com/engine/swarm/) (в Docker 1.12 и более поздние версии) не является поддерживаемой orchestrator в службе контейнера Azure. Toodeploy кластере режима группу мелких объектов в Azure, используйте открытым исходным кодом hello [модуль ACS](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), предоставленного сообществом [шаблоном краткого руководства](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), или Docker решения в hello [Azure Marketplace ](https://azuremarketplace.microsoft.com).
> 
> 

