---
title: Cmdlets für Infrastruktur und Bereitstellung
TOCTitle: Cmdlets für Infrastruktur und Bereitstellung
ms:assetid: 0a6e872a-9f70-4f23-a4a5-8820dbf55370
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398153(v=OCS.15)
ms:contentKeyID: 49293122
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlets für Infrastruktur und Bereitstellung

 

_**Letztes Änderungsdatum des Themas:** 2016-12-08_

Die in Microsoft Lync Server 2013 enthaltenen Cmdlets für Infrastruktur und Bereitstellung unterstützen Sie bei der anfänglichen Einrichtung und Bereitstellung des Produkts. Nach der Bereitstellung von Lync Server kann mithilfe dieser Cmdlets überprüft werden, ob die Komponenten wie erwartet funktionieren. Darüber hinaus können Sie mit diesen Cmdlets Replikationseinstellungen verwalten sowie die Lync Server-Topologie, -Richtlinien und -Konfigurationseinstellungen sichern und wiederherstellen.

## Cmdlets für Infrastruktur und Bereitstellung

Administratoren müssen die Cmdlets für Infrastruktur und Bereitstellung nur selten direkt aufrufen. Dies liegt daran, dass diese Cmdlets automatisch aufgerufen werden, wenn Sie das Setup oder den Topologie-Generator ausführen. (Eine Ausnahme stellt das Cmdlet **Export-CsConfiguration** dar, mit dem Sie eine Sicherungskopie Ihrer Lync Server-Topologie, -Richtlinien und -Konfigurationseinstellungen erstellen können.) Falls erforderlich, können die Cmdlets für Infrastruktur und Bereitstellung jedoch über die Lync Server-Verwaltungsshell oder aus einem Skript ausgeführt werden. Durch die Verwendung eines Skripts können bestimmte Aufgaben automatisiert werden. In der folgenden Liste werden Cmdlets aufgeführt, die im Rahmen von Infrastruktur und Bereitstellung eingesetzt werden:

**[Active Directory-Cmdlets](lync-server-2013-active-directory-cmdlets.md)**

  -   
    [Disable-CsAdDomain](disable-csaddomain.md)

  -   
    [Enable-CsAdDomain](enable-csaddomain.md)

  -   
    [Get-CsAdDomain](get-csaddomain.md)

  -   
    [Disable-CsAdForest](disable-csadforest.md)

  -   
    [Enable-CsAdForest](enable-csadforest.md)

  -   
    [Get-CsAdForest](get-csadforest.md)

  -   
    [Get-CsAdServerSchema](get-csadserverschema.md)

  -   
    [Install-CsAdServerSchema](install-csadserverschema.md)

**[Cmdlets für die Replikation](lync-server-2013-replication-cmdlets.md)**

  -   
    [Debug-CsInterPoolReplication](debug-csinterpoolreplication.md)

  -   
    [Invoke-CsManagementStoreReplication](invoke-csmanagementstorereplication.md)

  -   
    [Get-CsManagementStoreReplicationStatus](get-csmanagementstorereplicationstatus.md)

  -   
    [Enable-CsReplica](enable-csreplica.md)

  -   
    [Test-CsReplica](test-csreplica.md)

  -   
    [Get-CsUserReplicatorConfiguration](get-csuserreplicatorconfiguration.md)

  -   
    [New-CsUserReplicatorConfiguration](new-csuserreplicatorconfiguration.md)

  -   
    [Remove-CsUserReplicatorConfiguration](remove-csuserreplicatorconfiguration.md)

  -   
    [Set-CsUserReplicatorConfiguration](set-csuserreplicatorconfiguration.md)

**[Topologie-Cmdlets](lync-server-2013-topology-cmdlets.md)**

  -   
    [Get-CsPool](get-cspool.md)

  -   
    [Get-CsSite](get-cssite.md)

  -   
    [Set-CsSite](set-cssite.md)

  -   
    [Enable-CsTopology](enable-cstopology.md)

  -   
    [Get-CsTopology](get-cstopology.md)

  -   
    [Publish-CsTopology](publish-cstopology.md)

  -   
    [Test-CsTopology](test-cstopology.md)

  -   
    [Export-CsConfiguration](export-csconfiguration.md)

  -   
    [Import-CsConfiguration](import-csconfiguration.md)

  -   
    [Get-CsServerVersion](get-csserverversion.md)

  -   
    [Disable-CsComputer](disable-cscomputer.md)

  -   
    [Enable-CsComputer](enable-cscomputer.md)

  -   
    [Get-CsComputer](get-cscomputer.md)

  -   
    [Test-CsComputer](test-cscomputer.md)

  -   
    [Get-CsNetworkInterface](get-csnetworkinterface.md)

**[Cmdlets für Sicherung und hohe Verfügbarkeit](lync-server-2013-backup-and-high-availability-cmdlets.md)**

  - [Get-CsBackupServiceConfiguration](get-csbackupserviceconfiguration.md)

  - [Remove-CsBackupServiceConfiguration](remove-csbackupserviceconfiguration.md)

  - [Set-CsBackupServiceConfiguration](set-csbackupserviceconfiguration.md)

  - [Get-CsBackupServiceStatus](get-csbackupservicestatus.md)

  - [Invoke-CsBackupServiceSync](invoke-csbackupservicesync.md)

  - [Debug-CsIntraPoolReplication](debug-csintrapoolreplication.md)

  - [Backup-CsPool](backup-cspool.md)

  - [Get-CsPoolBackupRelationship](get-cspoolbackuprelationship.md)

  - [Get-CsPoolFabricState](get-cspoolfabricstate.md)

  - [Invoke-CsPoolFailBack](invoke-cspoolfailback.md)

  - [Invoke-CsPoolFailOver](invoke-cspoolfailover.md)

  - [Get-CsPoolUpgradeReadinessState](get-cspoolupgradereadinessstate.md)

  - [Invoke-CsStorageServiceFlush](invoke-csstorageserviceflush.md)

  - [Sync-CsUserData](sync-csuserdata.md)

  - [Remove-CsUserStoreBackupData](remove-csuserstorebackupdata.md)

## Siehe auch

#### Weitere Ressourcen

[Lync Server PowerShell-Blog](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x407)

