---
title: Serialisieren mit einer XML-Deklaration (C#)| Microsoft-Dokumentation
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: c237fa4a-a042-40fd-886f-17b54c66bb75
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 5c0389630c7fc4b8aa394974b7e42cce2a5101a4
ms.lasthandoff: 03/13/2017

---
# <a name="serializing-with-an-xml-declaration-c"></a>Serialisieren mit einer XML-Deklaration (C#)
In diesem Thema wird beschrieben, wie Sie steuern können, ob die Serialisierung eine XML-Deklaration generiert.  
  
## <a name="xml-declaration-generation"></a>Generierung einer XML-Deklaration  
 Beim Serialisieren in <xref:System.IO.File> oder <xref:System.IO.TextWriter> mithilfe der Methoden <xref:System.Xml.Linq.XElement.Save%2A?displayProperty=fullName> oder <xref:System.Xml.Linq.XDocument.Save%2A?displayProperty=fullName> wird eine XML-Deklaration generiert. Beim Serialisieren in einen <xref:System.Xml.XmlWriter> bestimmen die (in einem <xref:System.Xml.XmlWriterSettings>-Objekt angegebenen) Writer-Einstellungen, ob eine XML-Deklaration generiert wird.  
  
 Bei der Serialisierung in eine Zeichenfolge mit der `ToString`-Methode enthält der resultierende XML-Code keine XML-Deklaration.  
  
### <a name="serializing-with-an-xml-declaration"></a>Serialisieren mit einer XML-Deklaration  
 Das folgende Beispiel erstellt ein <xref:System.Xml.Linq.XElement>, speichert das Dokument in einer Datei und gibt die Datei dann an die Konsole aus:  
  
```csharp  
XElement root = new XElement("Root",  
    new XElement("Child", "child content")  
);  
root.Save("Root.xml");  
string str = File.ReadAllText("Root.xml");  
Console.WriteLine(str);  
```  
  
 Dieses Beispiel erzeugt die folgende Ausgabe:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<Root>  
  <Child>child content</Child>  
</Root>  
```  
  
### <a name="serializing-without-an-xml-declaration"></a>Serialisieren ohne eine XML-Deklaration  
 Das folgende Beispiel zeigt, wie man ein <xref:System.Xml.Linq.XElement> in einem <xref:System.Xml.XmlWriter> speichert.  
  
```csharp  
StringBuilder sb = new StringBuilder();  
XmlWriterSettings xws = new XmlWriterSettings();  
xws.OmitXmlDeclaration = true;  
  
using (XmlWriter xw = XmlWriter.Create(sb, xws)) {  
    XElement root = new XElement("Root",  
        new XElement("Child", "child content")  
    );  
    root.Save(xw);  
}  
Console.WriteLine(sb.ToString());  
```  
  
 Dieses Beispiel erzeugt die folgende Ausgabe:  
  
```xml  
<Root><Child>child content</Child></Root>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Serializing XML Trees (C#) (Serialisieren von XML-Strukturen (C#))](../../../../csharp/programming-guide/concepts/linq/serializing-xml-trees.md)