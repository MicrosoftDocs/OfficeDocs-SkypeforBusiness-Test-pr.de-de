---
title: Windows PowerShell-Cmdlets, -Parameter und Parameterwerte
TOCTitle: Windows PowerShell-Cmdlets, -Parameter und Parameterwerte
ms:assetid: 04615700-099f-4ac5-a801-ddeffccb9e4f
ms:mtpsurl: https://technet.microsoft.com/de-de/library/Dn362765(v=OCS.15)
ms:contentKeyID: 56269244
ms.date: 06/01/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Windows PowerShell-Cmdlets, -Parameter und Parameterwerte

 

_**Letztes Änderungsdatum des Themas:** 2015-06-22_

Wenn Sie mit dem Befehlsfenster vertraut sind, das in allen Versionen von Windows verfügbar ist (oder sich mit MS-DOS auskennen), dürften Sie keine Probleme damit haben, sich in Windows PowerShell einzuarbeiten. Geben Sie im Befehlsfenster einen Befehl ein, und drücken Sie die EINGABETASTE. Nun führt der Computer den Befehl oder eine ausführbare Datei aus. Wenn Sie beispielsweise Informationen zu allen Dateien und Ordnern im aktuellen Verzeichnis abrufen möchten, geben Sie an der Eingabeaufforderung den folgenden Befehl ein und drücken dann die EINGABETASTE:

    dir

Damit werden Informationen zu allen Dateien und Ordnern im aktuellen Verzeichnis zurückgegeben:

``` 
    Directory: C:\

03/21/2013  03:39 PM    <DIR>          Deploy
03/21/2013  02:55 PM    <DIR>          Intel
07/26/2012  12:33 AM    <DIR>          PerfLogs
04/10/2013  10:29 AM    <DIR>          Program Files
04/08/2013  10:28 AM    <DIR>          Program Files (x86)
03/22/2013  08:44 AM    <DIR>          Users
04/11/2013  03:00 PM    <DIR>              Windows
03/13/2013  02:53 PM                 117   pldok.log
03/21/2013  03:35 PM                 769   RHDSetup.exe
03/21/2013  03:37 PM            207   Setup.doc
              3 File(s)        1,093 bytes
              7 Dir(s)21,386,002,432 bytes free
```

Diese Ausgabe erhalten Sie beispielsweise, wenn Sie nur den Namen eines Befehls oder einer ausführbaren Datei eingeben. Viele der Befehle, die im Befehlsfenster ausgeführt werden, akzeptieren jedoch auch *Argumente*. Argumente sind weitere Informationen, die an den Befehl übergeben werden und das Verhalten des Befehls ändern. Wenn Sie beispielsweise nur die Namen und keine weiteren Informationen wie Größe oder Erstellungsdatum der Dateien und Ordner im aktuellen Verzeichnis anzeigen möchten, fügen Sie dem Befehl "dir" das Argument **/b** hinzu, wenn Sie den Befehl ausführen:

    dir /b

Wenn Sie das Argument **/b** hinzufügen, gibt der Befehl **dir** nur die Namen der Dateien und Ordner im aktuellen Verzeichnis zurück:

    Deploy
    Intel
    PerfLogs
    Program Files
    Program Files (x86)
    Users
    Windows
    pldok.log
    RHDSetup.exe
    setup.doc

Beim vorherigen Befehl ist das Argument **/b** das einzig erforderliche Argument, um die zurückgegebenen Daten auf Datei- und Ordnernamen zu begrenzen. Dies ist bei Befehlszeilenbefehlen häufig der Fall: Es muss lediglich ein Argument vorhanden sein, um das Verhalten des Befehls zu ändern. (Das heißt in diesem Fall, dass Sie das Argument **/b** einschließen, um weitere Informationen auszublenden, oder das Argument **/b** ausschließen, um zusätzliche Informationen anzuzeigen). Es kann jedoch auch vorkommen, dass Sie einen *Argumentwert* angeben müssen. Bei einem Argumentwert handelt es sich um zusätzliche Informationen, die an das Argument selbst übergeben werden. Mit dem Argument **/o** können Sie beispielsweise angeben, wie die mit dem Befehl **dir** zurückgegebenen Daten sortiert werden sollen. Neben anderen Optionen haben Sie auch die Möglichkeit, mit dem Argumentwert **e** nach Dateinamenerweiterung oder mit dem Argumentwert **s** nach Dateigröße zu sortieren. Mit dem folgenden Befehl werden die zurückgegebenen Daten beispielsweise nach Dateinamenerweiterung sortiert. Wie Sie sehen, wird der Argumentwert **e** direkt nach dem Argument **/o** eingegeben:

    dir /oe

Auf Basis unseres Beispielordners sehen die zurückgegebenen Daten alphabetisch sortiert nach Dateinamenerweiterung nun wie folgt aus:

``` 
    Directory: C:\

03/21/2013  03:39 PM    <DIR>          Deploy
03/21/2013  02:55 PM    <DIR>          Intel
07/26/2012  12:33 AM    <DIR>          PerfLogs
04/10/2013  10:29 AM    <DIR>          Program Files
04/08/2013  10:28 AM    <DIR>          Program Files (x86)
03/22/2013  08:44 AM    <DIR>          Users
04/11/2013  03:00 PM    <DIR>              Windows
03/21/2013  03:37 PM            207   setup.doc
03/21/2013  03:35 PM                 769   RHDSetup.exe
03/13/2013  02:53 PM                 117   pldok.log
              3 File(s)        1,093 bytes
              7 Dir(s)21,386,002,432 bytes free
```

Schauen Sie genau hin, dann sehen Sie, wovon wir sprechen:

setup. **doc**  
RHDSetup. **exe**  
pldok. **log**

Obwohl in Windows PowerShell eine andere Terminologie verwendet wird, ist der grundlegende Ansatz für die Arbeit mit Windows PowerShell der gleiche wie beim Befehlsfenster: Sie geben Befehle ein, fügen die erforderlichen Argumente und Argumentwerte hinzu und drücken dann die EINGABETASTE, um diese Befehle auszuführen. Aber wie schon gesagt, in Windows PowerShell wird eine andere Terminologie als in der Befehlsshell verwendet. In Windows PowerShell werden die Befehle, die Sie ausführen, als *Cmdlets* bezeichnet. Die Argumente, die an ein Cmdlet übergeben werden, werden *Parameter* genannt, und die Werte, die an einen Parameter übergeben werden, sind die *Parameterwerte*.

Die vorstehenden Definitionen sind jedoch ein wenig vereinfacht. Cmdlets sind im Wesentlichen Minianwendungen, die nur in der Windows PowerShell-Umgebung ausgeführt werden können. Sie können jedoch auch andere Befehle und Anwendungen in Windows PowerShell ausführen, wozu auch die meisten der Befehle und Anwendungen gehören, die in einem Befehlsfenster ausgeführt werden können. Wenn Sie beispielsweise den Editor in Windows PowerShell starten möchten, müssen Sie lediglich den folgenden Befehl eingeben und dann die EINGABETASTE drücken:

    notepad.exe

Wenn es jedoch um die Verwaltung von Skype for Business Online geht, bevorzugen die meisten Administratoren Windows PowerShell-Cmdlets für anstehende Verwaltungsaufgaben. Zurzeit gibt es nur sehr wenige andere Befehlstypen oder Anwendungen, die für die Verwaltung von Skype for Business Online genutzt werden können. Manchmal können die Skype for Business Online-Cmdlets ohne zusätzliche Argumente verwendet werden (wie schon gesagt, Argumente werden in Verbindung mit Windows PowerShell als Parameter bezeichnet). Mit dem folgenden Befehl wird beispielsweise das Cmdlet [Get-CsOnlineUser](get-csonlineuser.md) ohne zusätzliche Parameter aufgerufen. Der Befehl selbst ruft Informationen zu allen Skype for Business Online-Benutzern ab:

    Get-CsOnlineUser

Die meisten der Skype for Business Online-Cmdlets akzeptieren jedoch auch Parameter (und Parameterwerte). Schauen Sie sich den folgenden Befehl an:

    Get-CsOnlineUser -Identity "kenmyer@litwareinc.com"

Dieser Befehl besteht aus drei Teilen:

  - Dem Cmdlet **Get-CsOnlineUser**

  - Dem Parameter Identity. Beachten Sie, dass den Parametern in Windows PowerShell immer ein Minuszeichen (-) vorangestellt wird. Der Parameter UnassignedUser wird beim gleichen Cmdlet also mit der folgenden Syntax angegeben:
    
        -UnassignedUser
    
    Sie sollten also nicht nur wissen, dass Parametern ein Minuszeichen vorangestellt werden muss, sondern auch den wesentlichen Unterschied zum Befehlsfenster erkennen, in dem Argumenten ein Schrägstrich (/) vorangestellt wird:
    
    ``` 
    /b
    ```

  - Der Parameterwert <strong>kenmyer@litwareinc.com</strong>.

Dieser Befehl gibt übrigens Informationen zu einem bestimmten Benutzer zurück, dem Benutzer mit der Identität kenmyer@litwareinc.com.

## Siehe auch

#### Konzepte

[Einführung in Windows PowerShell und Lync Online](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

