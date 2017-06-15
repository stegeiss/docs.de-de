---
title: "EDM-Generator (EdmGen.exe) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: fe8297a1-1fc3-48ce-8eeb-f70f63f857aa
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# EDM-Generator (EdmGen.exe)
EdmGen.exe ist ein Befehlszeilentool, das für die Arbeit mit [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]\-Modell\- und Zuordnungsdateien verwendet wird.  Mit dem Tool **EdmGen.exe** können folgende Aufgaben ausgeführt werden:  
  
-   Herstellen einer Verbindung zu einer Datenquelle mithilfe eines datenquellenspezifischen .NET Framework\-Datenanbieters, und Erstellen der Dateien für das konzeptionelle Modell \(CSDL\), das Speichermodell \(SSDL\) und die Zuordnungen \(MSL\), die von [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] verwendet werden.  Weitere Informationen finden Sie unter [Vorgehensweise: Generieren von Modell\- und Zuordnungsdateien mithilfe von EdmGen.exe](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md).  
  
-   Überprüfen eines bestehenden Modells.  Weitere Informationen finden Sie unter [Gewusst wie: Überprüfen von Modell\- und Zuordnungsdateien mithilfe von EdmGen.exe](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-validate-model-and-mapping-files.md).  
  
-   Erstellen einer C\#\- oder Visual Basic\-Codedatei, die die Objektklassen enthält, die aus einer Datei für das konzeptionelle Modell \(CSDL\) generiert wurden.  Weitere Informationen finden Sie unter [Gewusst wie: Verwenden von 'EdmGen.exe' zum Generieren von Objektebenencode](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-object-layer-code.md).  
  
-   Generieren einer C\#\- oder Visual Basic\-Codedatei, die die vorab generierten Sichten für ein vorhandenes Modell enthält.  Weitere Informationen finden Sie unter [How to: Pre\-Generate Views to Improve Query Performance](http://msdn.microsoft.com/de-de/b18a9d16-e10b-4043-ba91-b632f85a2579).  
  
 Das Tool EdmGen.exe wird im [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)]\-Verzeichnis installiert.  Dieses befindet sich meist unter C:\\Windows\\Microsoft.NET\\Framework\\v4.0.  Bei 64\-Bit\-Systemen befindet es sich unter C:\\Windows\\Microsoft.NET\\Framework64\\v4.0.  Zusätzlich können Sie mithilfe der Eingabeaufforderung von Visual Studio auf das Tool EdmGen.exe zugreifen. \(Klicken Sie auf **Start**, zeigen Sie auf **Programme**, **Microsoft Visual Studio 2010**, **Visual Studio Tools**, und klicken Sie dann auf **Visual Studio 2010\-Eingabeaufforderung**.\)  
  
## Syntax  
  
```  
EdmGen /mode:choice [options]  
```  
  
## Modus  
 Wenn Sie das Tool **EdmGen.exe** verwenden, müssen Sie einen der folgenden Modi angeben.  
  
|Modus|Beschreibung|  
|-----------|------------------|  
|`/mode:ValidateArtifacts`|Überprüft die CSDL\-, SSDL\- und MSL\-Dateien und zeigt alle Fehler und Warnungen an.<br /><br /> Diese Option erfordert mindestens eines der Argumente `/inssdl` oder `/incsdl`.  Wenn `/inmsl` angegeben wird, sind auch die Argumente `/inssdl` und `/incsdl` erforderlich.|  
|`/mode:FullGeneration`|Verwendet die in der `/connectionstring`\-Option angegebenen Informationen zur Datenbankverbindung, und erstellt die CSDL\-, SSDL\-, .MSL\-, Objektebenen\- und Sichtdateien.<br /><br /> Diese Option erfordert ein `/connectionstring`\-Argument sowie entweder ein `/project`\-Argument oder die Argumente `/outssdl`, `/outcsdl`, `/outmsdl`, `/outobjectlayer`, `/outviews`, `/namespace` und `/entitycontainer`.|  
|`/mode:FromSSDLGeneration`|Generiert CSDL\- und MSL\-Dateien, Quellcode und Sichten mithilfe der angegebenen SSDL\-Datei.<br /><br /> Diese Option erfordert das `/inssdl`\-Argument und entweder ein `/project`\-Argument oder die Argumente `/outcsdl`, `/outmsl`, `/outobjectlayer`, `/outviews`, `/namespace,` und `/entitycontainer`.|  
|`/mode:EntityClassGeneration`|Erstellt eine Quellcodedatei, die die mithilfe der CSDL\-Datei generierten Klassen enthält.<br /><br /> Diese Option erfordert das `/incsdl`\-Argument sowie das `/project`\-Argument oder das `/outobjectlayer`\-Argument.  Das `/language`\-Argument ist optional.|  
|`/mode:ViewGeneration`|Erstellt eine Quellcodedatei, die die aus den CSDL\-, SSDL\- und MSL\-Dateien generierten Sichten enthält.<br /><br /> Diese Option erfordert die Argumente `/inssdl`, `/incsdl` und `/inmsl,` sowie entweder das `/project`\-Argument oder das `/outviews`\-Argument.  Das `/language`\-Argument ist optional.|  
  
## Optionen  
  
|Option|Beschreibung|  
|------------|------------------|  
|`/p[roject]:`\<string\>|Gibt den zu verwendenden Projektnamen an.  Der Projektname wird für die standardmäßige Namespaceeinstellung, die Namen der Modell\- und Zuordnungsdateien, den Namen der Objektquelldatei und den Namen der Quelldatei für das Generieren von Ansichten verwendet.  Der Entitätencontainername wird auf "\<project\>Context" festgelegt.|  
|`/prov[ider]:`\<string\>|Der Name des [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)]\-Datenanbieters zum Erstellen der Speichermodelldatei \(SSDL\).  Der Standardanbieter ist der [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)]\-Anbieter für SQL Server \(<xref:System.Data.SqlClient?displayProperty=fullName>\).|  
|`/c[onnectionstring]:`\<connection string\>|Gibt die Zeichenfolge an, die verwendet wird, um eine Verbindung mit der Datenquelle herzustellen.|  
|`/incsdl:`\<file\>|Gibt die CSDL\-Datei oder ein Verzeichnis an, in dem sich die CSDL\-Dateien befinden.  Dieses Argument kann mehrmals angegeben werden, damit Sie mehrere Verzeichnisse oder CSDL\-Dateien angeben können.  Das Angeben mehrerer Verzeichnisse ist beim Erstellen von Klassen \(`/mode:EntityClassGeneration`\) oder Sichten \(`/mode:ViewGeneration`\) hilfreich, wenn das konzeptionelle Modell in mehrere Dateien aufgeteilt ist.  Dies kann auch nützlich sein, wenn Sie mehrere Modelle \(`/mode:ValidateArtifacts`\) überprüfen möchten.|  
|`/refcsdl:`\<file\>|Gibt die zusätzliche CSDL\-Datei bzw. \-Dateien an, die verwendet werden, um die Verweise in der CSDL\-Quelldatei aufzulösen.  \(Die CSDL\-Quelldatei ist die mit der `/incsdl`\-Option angegebene Datei\).  Die `/refcsdl`\-Datei enthält Typen, von denen die CSDL\-Quelldatei abhängt.  Dieses Argument kann mehrmals angegeben werden.|  
|`/inmsl:`\<file\>|Gibt die MSL\-Datei oder ein Verzeichnis an, in dem sich die MSL\-Dateien befinden.  Dieses Argument kann mehrmals angegeben werden, um mehrere Verzeichnisse oder MSL\-Dateien anzugeben.  Das Angeben mehrerer Dateien ist beim Erstellen von Sichten \(`/mode:ViewGeneration`\) hilfreich, wenn das konzeptionelle Modell in mehrere Dateien aufgeteilt ist.  Dies kann auch nützlich sein, wenn Sie mehrere Modelle \(`/mode:ValidateArtifacts`\) überprüfen möchten.|  
|`/inssdl:`\<file\>|Gibt die SSDL\-Datei oder ein Verzeichnis an, in dem sich die SSDL\-Datei befindet.  Dieses Argument kann mehrmals angegeben werden, damit Sie mehrere Verzeichnisse oder SSDL\-Dateien angeben können.  Dies kann auch nützlich sein, wenn Sie mehrere Modelle `(/mode:ValidateArtifacts)` überprüfen möchten.|  
|`/outcsdl:`\<file\>|Gibt den Namen der CSDL\-Datei an, die erstellt wird.|  
|`/outmsl:`\<file\>|Gibt den Namen der MSL\-Datei an, die erstellt wird.|  
|`/outssdl:`\<file\>|Gibt den Namen der SSDL\-Datei an, die erstellt wird.|  
|`/outobjectlayer:`\<file\>|Gibt den Namen der Quellcodedatei an, die die mit der CSDL\-Datei generierten Objekte enthält.|  
|`/outviews:`\<file\>|Gibt den Namen der Quellcodedatei an, die die generierten Sichten enthält.|  
|`/language:`\[VB&#124;CSharp\]|Gibt die Sprache für die erstellten Quellcodedateien an.  Die Standardsprache ist C\#.|  
|`/namespace:`\<string\>|Gibt den zu verwendenden Namespace für das Modell an.  Der Namespace wird beim Ausführen von `/mode:FullGeneration` oder `/mode:FromSSDLGeneration` in der CSDL\-Datei festgelegt.  Beim Ausführen `/mode:EntityClassGeneration` wird der Namespace nicht verwendet.|  
|`/entitycontainer:`\<string\>|Gibt den Namen an, der dem `<EntityContainer>`\-Element in den generierten Modell\- und Zuordnungsdateien hinzugefügt wird.|  
|`/pl[uralize]`|Wendet für das Englische geltende Regeln für Singular\- und Pluralbildung auf die Namen von `Entity`, `EntitySet` und `NavigationProperty` im konzeptionellen Modell an.  Diese Option führt die folgenden Aktionen aus:<br /><br /> -   Alle `EntityType`\-Namen werden in den Singular gesetzt.<br />-   Alle `EntitySet`\-Namen werden in den Plural gesetzt.<br />-   Für jede `NavigationProperty`, die höchstens eine Entität zurückgibt, wird der Name in den Singular gesetzt.<br />-   Für jede `NavigationProperty`, die mehrere Entitäten zurückgibt, wird der Name in den Plural gesetzt.|  
|`/SupressForeignKeyProperties or /nofk`|Verhindert, dass Fremdschlüsselspalten als skalare Eigenschaften von Entitätstypen im konzeptionellen Modell verfügbar gemacht werden.|  
|`/help` oder `?`|Zeigt Befehlssyntax und Optionen für das Tool an.|  
|`/nologo`|Unterdrückt die Anzeige der Copyrightmeldung.|  
|`/targetversion:` \<string\>|Die Version von .NET Framework, die zum Kompilieren des generierten Codes verwendet wird.  Unterstützt werden Version 4 und 4.5.  Der Standardwert ist 4.|  
  
## In diesem Abschnitt  
 [Vorgehensweise: Generieren von Modell\- und Zuordnungsdateien mithilfe von EdmGen.exe](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md)  
  
 [Gewusst wie: Verwenden von 'EdmGen.exe' zum Generieren von Objektebenencode](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-object-layer-code.md)  
  
 [Gewusst wie: Überprüfen von Modell\- und Zuordnungsdateien mithilfe von EdmGen.exe](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-validate-model-and-mapping-files.md)  
  
## Siehe auch  
 [ADO.NET Entity Data Model  Tools](http://msdn.microsoft.com/de-de/91076853-0881-421b-837a-f582f36be527)   
 [Entity Data Model](../../../../../docs/framework/data/adonet/entity-data-model.md)   
 [CSDL\-, SSDL\- und MSL\-Spezifikationen](../../../../../docs/framework/data/adonet/ef/language-reference/csdl-ssdl-and-msl-specifications.md)