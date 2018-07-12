---
title: Cmdlets für Serverrollen und -dienste
TOCTitle: Cmdlets für Serverrollen und -dienste
ms:assetid: ff3561de-043e-4071-88f7-8de3cded52f6
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg415683(v=OCS.15)
ms:contentKeyID: 49296018
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Cmdlets für Serverrollen und -dienste

 

_**Letztes Änderungsdatum des Themas:** 2016-12-08_

Viele Microsoft Lync Server 2013-Komponenten werden als Serverrollen oder als Dienste ausgeführt. Zum Lieferumfang von Lync Server 2013 gehören verschiedene Cmdlets, mit denen Sie diese Serverrollen und -dienste verwalten können.

## Cmdlets für Serverrollen und -dienste

Viele (jedoch nicht alle) der Verwaltungsaufgaben im Rahmen der Verwaltung von Servern und Dienstrollen können über die Lync Server-Systemsteuerung ausgeführt werden. Beispielsweise können Sie mit der Lync Server-Systemsteuerung die Einstellungen für Archivierungsserver verwalten, nicht jedoch die Einstellungen für den Adressbuchserver. Alle diese Aufgaben können jedoch auch mithilfe von Cmdlets über die Lync Server-Verwaltungsshell oder aus einem Skript ausgeführt werden. Durch die Verwendung eines Skripts können bestimmte Aufgaben automatisiert werden. In der folgenden Liste werden Cmdlets aufgeführt, die im Rahmen der Verwaltung von Serverrollen und -diensten eingesetzt werden:

**[Cmdlets für Adressbuchserver](lync-server-2013-address-book-server-cmdlets.md)**

  - [Get-CsAddressBookConfiguration](get-csaddressbookconfiguration.md)

  - [New-CsAddressBookConfiguration](new-csaddressbookconfiguration.md)

  - [Remove-CsAddressBookConfiguration](remove-csaddressbookconfiguration.md)

  - [Set-CsAddressBookConfiguration](set-csaddressbookconfiguration.md)

<!-- end list -->

  - [Update-CsAddressBook](update-csaddressbook.md)

  - [Debug-CsAddressBookReplication](debug-csaddressbookreplication.md)

<!-- end list -->

  - [Test-CsAddressBookService](test-csaddressbookservice.md)

  - [Test-CsAddressBookWebQuery](test-csaddressbookwebquery.md)

**[Cmdlets für Archivierung und Überwachung](lync-server-2013-archiving-and-monitoring-cmdlets.md)**

  - [Get-CsArchivingConfiguration](get-csarchivingconfiguration.md)

  - [New-CsArchivingConfiguration](new-csarchivingconfiguration.md)

  - [Remove-CsArchivingConfiguration](remove-csarchivingconfiguration.md)

  - [Set-CsArchivingConfiguration](set-csarchivingconfiguration.md)

  - [Export-CsArchivingData](export-csarchivingdata.md)

  - [Invoke-CsArchivingDatabasePurge](invoke-csarchivingdatabasepurge.md)

  - [Get-CsArchivingPolicy](get-csarchivingpolicy.md)

  - [Grant-CsArchivingPolicy](grant-csarchivingpolicy.md)

  - [New-CsArchivingPolicy](new-csarchivingpolicy.md)

  - [Remove-CsArchivingPolicy](remove-csarchivingpolicy.md)

  - [Set-CsArchivingPolicy](set-csarchivingpolicy.md)

  - [Set-CsArchivingServer](set-csarchivingserver.md)

  - [Get-CsCdrConfiguration](get-cscdrconfiguration.md)

  - [New-CsCdrConfiguration](new-cscdrconfiguration.md)

  - [Remove-CsCdrConfiguration](remove-cscdrconfiguration.md)

  - [Set-CsCdrConfiguration](set-cscdrconfiguration.md)

  - [Set-CsMonitoringServer](set-csmonitoringserver.md)

  - [Get-CsQoEConfiguration](get-csqoeconfiguration.md)

  - [New-CsQoEConfiguration](new-csqoeconfiguration.md)

  - [Remove-CsQoEConfiguration](remove-csqoeconfiguration.md)

  - [Set-CsQoEConfiguration](set-csqoeconfiguration.md)

[Invoke-CsCdrDatabasePurge](invoke-cscdrdatabasepurge.md)

  - [Export-CsArchivingData](export-csarchivingdata.md)

  - [Invoke-CsQoEDatabasePurge](invoke-csqoedatabasepurge.md)

  - [Get-CsReportingConfiguration](get-csreportingconfiguration.md)

  - [New-CsReportingConfiguration](new-csreportingconfiguration.md)

  - [Remove-CsReportingConfiguration](remove-csreportingconfiguration.md)

  - [Set-CsReportingConfiguration](set-csreportingconfiguration.md)

  - [Get-CsTestUserCredential](get-cstestusercredential.md)

  - [Remove-CsTestUserCredential](remove-cstestusercredential.md)

  - [Set-CsTestUserCredential](set-cstestusercredential.md)

  - [Get-CsWatcherNodeConfiguration](get-cswatchernodeconfiguration.md)

  - [New-CsWatcherNodeConfiguration](new-cswatchernodeconfiguration.md)

  - [Remove-CsWatcherNodeConfiguration](remove-cswatchernodeconfiguration.md)

  - [Set-CsWatcherNodeConfiguration](set-cswatchernodeconfiguration.md)

  - [Test-CsWatcherNodeConfiguration](test-cswatchernodeconfiguration.md)

  - [New-CsExtendedTest](new-csextendedtest.md)

**[Cmdlets für Datenbanken und Verwaltungsserver](lync-server-2013-database-and-management-server-cmdlets.md)**

  - [Get-CsConfigurationStoreLocation](get-csconfigurationstorelocation.md)

  - [Remove-CsConfigurationStoreLocation](remove-csconfigurationstorelocation.md)

  - [Set-CsConfigurationStoreLocation](set-csconfigurationstorelocation.md)

  - [Install-CsDatabase](install-csdatabase.md)

  - [Test-CsDatabase](test-csdatabase.md)

  - [Uninstall-CsDatabase](uninstall-csdatabase.md)

  - [Invoke-CsDatabaseFailover](invoke-csdatabasefailover.md)

  - [Get-CsDatabaseMirrorState](get-csdatabasemirrorstate.md)

  - [Install-CsMirrorDatabase](install-csmirrordatabase.md)

  - [Uninstall-CsMirrorDatabase](uninstall-csmirrordatabase.md)

  - [Get-CsUserDatabaseState](get-csuserdatabasestate.md)

  - [Set-CsUserDatabaseState](set-csuserdatabasestate.md)

  - [Update-CsUserDatabase](update-csuserdatabase.md)

  - [Move-CsManagementServer](move-csmanagementserver.md)

  - [Set-CsManagementServer](set-csmanagementserver.md)

  - [Invoke-CsManagementServerFailover](invoke-csmanagementserverfailover.md)

**[Cmdlets für Edgeserver](lync-server-2013-edge-server-cmdlets.md)**

  - [Get-CsAccessEdgeConfiguration](get-csaccessedgeconfiguration.md)

  - [Set-CsAccessEdgeConfiguration](set-csaccessedgeconfiguration.md)

  - [Get-CsAVEdgeConfiguration](get-csavedgeconfiguration.md)

  - [New-CsAVEdgeConfiguration](new-csavedgeconfiguration.md)

  - [Remove-CsAVEdgeConfiguration](remove-csavedgeconfiguration.md)

  - [Set-CsAVEdgeConfiguration](set-csavedgeconfiguration.md)

  - [Test-CsAVEdgeConnectivity](test-csavedgeconnectivity.md)

  - [Set-CsEdgeServer](set-csedgeserver.md)

**[Cmdlets für sonstige Serverrollen](lync-server-2013-other-server-role-cmdlets.md)**

  - [Set-CsConferenceServer](set-csconferenceserver.md)

  - [Set-CsUserServer](set-csuserserver.md)

**[Cmdlets für Registrierung und Directors](lync-server-2013-registrar-and-director-cmdlets.md)**

  - [Set-CsDirector](set-csdirector.md)

  - [Reset-CsPoolRegistrarState](reset-cspoolregistrarstate.md)

  - [Set-CsRegistrar](set-csregistrar.md)

  - [Get-CsRegistrarConfiguration](get-csregistrarconfiguration.md)

  - [New-CsRegistrarConfiguration](new-csregistrarconfiguration.md)

  - [Remove-CsRegistrarConfiguration](remove-csregistrarconfiguration.md)

  - [Set-CsRegistrarConfiguration](set-csregistrarconfiguration.md)

  - [Test-CsRegistration](test-csregistration.md)

**[Cmdlets für Dienste](lync-server-2013-services-cmdlets.md)**

  - [Get-CsService](get-csservice.md)

  - [Get-CsWindowsService](get-cswindowsservice.md)

  - [Start-CsWindowsService](start-cswindowsservice.md)

  - [Stop-CsWindowsService](stop-cswindowsservice.md)

**[Cmdlets für die Problembehandlung von Serverrollen und -diensten](lync-server-2013-troubleshooting-server-roles-and-services-cmdlets.md)**

  - [Get-CsAudioTestServiceApplication](get-csaudiotestserviceapplication.md)

  - [Set-CsAudioTestServiceApplication](set-csaudiotestserviceapplication.md)

  - [Get-CsHealthMonitoringConfiguration](get-cshealthmonitoringconfiguration.md)

  - [New-CsHealthMonitoringConfiguration](new-cshealthmonitoringconfiguration.md)

  - [Remove-CsHealthMonitoringConfiguration](remove-cshealthmonitoringconfiguration.md)

  - [Set-CsHealthMonitoringConfiguration](set-cshealthmonitoringconfiguration.md)

  - [Get-CsDiagnosticConfiguration](get-csdiagnosticconfiguration.md)

  - [New-CsDiagnosticConfiguration](new-csdiagnosticconfiguration.md)

  - [Remove-CsDiagnosticConfiguration](remove-csdiagnosticconfiguration.md)

  - [Set-CsDiagnosticConfiguration](set-csdiagnosticconfiguration.md)

  - [New-CsDiagnosticsFilter](new-csdiagnosticsfilter.md)

  - [Get-CsDiagnosticHeaderConfiguration](get-csdiagnosticheaderconfiguration.md)

  - [New-CsDiagnosticHeaderConfiguration](new-csdiagnosticheaderconfiguration.md)

  - [Remove-CsDiagnosticHeaderConfiguration](remove-csdiagnosticheaderconfiguration.md)

  - [Set-CsDiagnosticHeaderConfiguration](set-csdiagnosticheaderconfiguration.md)

**[Cmdlets für Webserver und -dienste](lync-server-2013-web-server-and-services-cmdlets.md)**

  - [New-CsSimpleUrl](new-cssimpleurl.md)

  - [Get-CsSimpleUrlConfiguration](get-cssimpleurlconfiguration.md)

  - [New-CsSimpleUrlConfiguration](new-cssimpleurlconfiguration.md)

  - [Remove-CsSimpleUrlConfiguration](remove-cssimpleurlconfiguration.md)

  - [Set-CsSimpleUrlConfiguration](set-cssimpleurlconfiguration.md)

  - [New-CsSimpleUrlEntry](new-cssimpleurlentry.md)

  - [Set-CsWebServer](set-cswebserver.md)

  - [Get-CsWebServiceConfiguration](get-cswebserviceconfiguration.md)

  - [New-CsWebServiceConfiguration](new-cswebserviceconfiguration.md)

  - [Remove-CsWebServiceConfiguration](remove-cswebserviceconfiguration.md)

  - [Set-CsWebServiceConfiguration](set-cswebserviceconfiguration.md)

  - [New-CsWebTrustedCACertificate](new-cswebtrustedcacertificate.md)

  - [New-CsKerberosAccount](new-cskerberosaccount.md)

  - [Get-CsKerberosAccountAssignment](get-cskerberosaccountassignment.md)

  - [New-CsKerberosAccountAssignment](new-cskerberosaccountassignment.md)

  - [Remove-CsKerberosAccountAssignment](remove-cskerberosaccountassignment.md)

  - [Set-CsKerberosAccountAssignment](set-cskerberosaccountassignment.md)

  - [Test-CsKerberosAccountAssignment](test-cskerberosaccountassignment.md)

  - [Set-CsKerberosAccountPassword](set-cskerberosaccountpassword.md)

  - [Test-CsWebApp](test-cswebapp.md)

  - [Test-CsWebAppAnonymous](test-cswebappanonymous.md)

## Siehe auch

#### Weitere Ressourcen

[Lync Server PowerShell-Blog](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x407)

