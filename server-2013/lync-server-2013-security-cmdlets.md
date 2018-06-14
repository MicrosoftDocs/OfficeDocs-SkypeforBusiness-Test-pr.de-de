---
title: Sicherheits-Cmdlets
TOCTitle: Sicherheits-Cmdlets
ms:assetid: 9a6c654d-287d-434e-8d93-409f0d623f5a
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Gg398799(v=OCS.15)
ms:contentKeyID: 49294867
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Sicherheits-Cmdlets

 

_**Letztes Änderungsdatum des Themas:** 2016-12-08_

Die in Microsoft Lync Server 2013 enthaltenen Sicherheits-Cmdlets werden hauptsächlich zum Verwalten von Authentifizierung, Benutzerrechten und Berechtigungen verwendet. Zum Verwalten der Authentifizierung stehen zahlreiche Cmdlets zur Verfügung, darunter Cmdlets für die Authentifizierung unter Verwendung von Zertifikaten oder einer persönlichen Identifikationsnummer (PIN). Zusätzlich stehen verschiedene Cmdlets bereit, mit denen Sie die neue rollenbasierte Zugriffssteuerung zum Delegieren der Verwaltungsfunktionen von Lync Server nutzen können.

## Sicherheits-Cmdlets

Viele Aufgaben im Rahmen der Sicherheitsverwaltung können über die Lync Server-Systemsteuerung ausgeführt werden. Eine wichtige Ausnahme stellen die Cmdlets für Benutzerberechtigungen dar. Alle Aufgaben im Rahmen der Sicherheitsverwaltung können jedoch auch mithilfe von Cmdlets über die Lync Server-Verwaltungsshell oder aus einem Skript ausgeführt werden. Durch die Verwendung eines Skripts können bestimmte Aufgaben automatisiert werden. In der folgenden Liste werden Cmdlets aufgeführt, die im Rahmen der Verwaltung von Sicherheitseinstellungen eingesetzt werden:

**[Cmdlets für Zertifikate und Authentifizierung](lync-server-2013-certificate-and-authentication-cmdlets.md)**

  - [Get-CsCertificate](get-cscertificate.md)

  - [Import-CsCertificate](import-cscertificate.md)

  - [Remove-CsCertificate](remove-cscertificate.md)

  - [Request-CsCertificate](request-cscertificate.md)

  - [Set-CsCertificate](set-cscertificate.md)

  - [Test-CsCertificateConfiguration](test-cscertificateconfiguration.md)

  - [Get-CsClientCertificate](get-csclientcertificate.md)

  - [Revoke-CsClientCertificate](revoke-csclientcertificate.md)

  - [Lock-CsClientPin](lock-csclientpin.md)

  - [Set-CsClientPin](set-csclientpin.md)

  - [Unlock-CsClientPin](unlock-csclientpin.md)

  - [Get-CsClientPinInfo](get-csclientpininfo.md)

  - [New-CsKerberosAccount](new-cskerberosaccount.md)

  - [Get-CsKerberosAccountAssignment](get-cskerberosaccountassignment.md)

  - [New-CsKerberosAccountAssignment](new-cskerberosaccountassignment.md)

  - [Remove-CsKerberosAccountAssignment](remove-cskerberosaccountassignment.md)

  - [Set-CsKerberosAccountAssignment](set-cskerberosaccountassignment.md)

  - [Test-CsKerberosAccountAssignment](test-cskerberosaccountassignment.md)

  - [Set-CsKerberosAccountPassword](set-cskerberosaccountpassword.md)

  - [Get-CsPinPolicy](get-cspinpolicy.md)

  - [Grant-CsPinPolicy](grant-cspinpolicy.md)

  - [New-CsPinPolicy](new-cspinpolicy.md)

  - [Remove-CsPinPolicy](remove-cspinpolicy.md)

  - [Set-CsPinPolicy](set-cspinpolicy.md)

  - [Get-CsProxyConfiguration](get-csproxyconfiguration.md)

  - [New-CsProxyConfiguration](new-csproxyconfiguration.md)

  - [Remove-CsProxyConfiguration](remove-csproxyconfiguration.md)

  - [Set-CsProxyConfiguration](set-csproxyconfiguration.md)

  - [Get-CsSipDomain](get-cssipdomain.md)

  - [New-CsSipDomain](new-cssipdomain.md)

  - [Remove-CsSipDomain](remove-cssipdomain.md)

  - [Set-CsSipDomain](set-cssipdomain.md)

**[Cmdlets für Benutzerrechte und Berechtigungen](lync-server-2013-user-rights-and-permissions-cmdlets.md)**

  - [Get-CsAdminRole](get-csadminrole.md)

  - [New-CsAdminRole](new-csadminrole.md)

  - [Remove-CsAdminRole](remove-csadminrole.md)

  - [Set-CsAdminRole](set-csadminrole.md)

  - [Update-CsAdminRole](update-csadminrole.md)

  - [Get-CsAdminRoleAssignment](get-csadminroleassignment.md)

  - [Grant-CsOUPermission](grant-csoupermission.md)

  - [Revoke-CsOUPermission](revoke-csoupermission.md)

  - [Test-CsOUPermission](test-csoupermission.md)

  - [Grant-CsSetupPermission](grant-cssetuppermission.md)

  - [Revoke-CsSetupPermission](revoke-cssetuppermission.md)

  - [Test-CsSetupPermission](test-cssetuppermission.md)

**[Cmdlets für die Interoperabilität](lync-server-2013-interoperability-cmdlets.md)**

  - [Get-CsOAuthConfiguration](get-csoauthconfiguration.md)

  - [Set-CsOAuthConfiguration](set-csoauthconfiguration.md)

  - [Get-CsOAuthServer](get-csoauthserver.md)

  - [New-CsOAuthServer](new-csoauthserver.md)

  - [Remove-CsOAuthServer](remove-csoauthserver.md)

  - [Set-CsOAuthServer](set-csoauthserver.md)

  - [Get-CsPartnerApplication](get-cspartnerapplication.md)

  - [New-CsPartnerApplication](new-cspartnerapplication.md)

  - [Remove-CsPartnerApplication](remove-cspartnerapplication.md)

  - [Set-CsPartnerApplication](set-cspartnerapplication.md)

## Siehe auch

#### Weitere Ressourcen

[Lync Server PowerShell-Blog](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x407)

