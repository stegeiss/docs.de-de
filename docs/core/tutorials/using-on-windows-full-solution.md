---
title: "Erstellen einer vollständigen .NET Core-Lösung unter Windows mit Visual Studio 2017"
description: "Erfahren Sie, wie Sie eine vollständige .NET Core-Projektmappe in Visual Studio 2017 unter Windows erstellen."
keywords: .NET, .NET Core
author: bleroy
ms.author: mairaw
ms.date: 11/16/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: ba7e082c-a7c8-431e-a342-f67734b660f6
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 6b164198f5fbbae5ebc6164fc281dd7de8172b70
ms.contentlocale: de-de
ms.lasthandoff: 07/28/2017

---

# <a name="building-a-complete-net-core-solution-on-windows-using-visual-studio-2017"></a>Erstellen einer vollständigen .NET Core-Lösung unter Windows mit Visual Studio 2017

Visual Studio 2017 bietet eine umfassende Entwicklungsumgebung für die Entwicklung von .NET Core-Anwendungen. Die Verfahren in diesem Dokument beschreiben die erforderlichen Schritte zum Erstellen einer herkömmlichen .NET Core-Lösung, die wiederverwendbare Bibliotheken, Tests und das Verwenden von Bibliotheken von Drittanbietern vorsieht. 

## <a name="prerequisites"></a>Erforderliche Komponenten

Befolgen Sie die Anweisungen auf [unserer Seite über erforderliche Komponenten](../windows-prerequisites.md), um Ihre Umgebung anzupassen.

## <a name="a-solution-using-only-net-core-projects"></a>Eine Projektmappe nur mit .NET Core-Projekten

### <a name="writing-the-library"></a>Schreiben der Bibliothek

1. Klicken Sie in Visual Studio auf **Datei** > **Neu** > **Projekt**. Erweitern Sie im Dialogfeld **Neues Projekt** den Knoten **Visual C#**. Wählen Sie den Knoten **.NET Core** und anschließend den Knoten **Klassenbibliothek (.NET Standard)** aus. 

2. Geben Sie dem Projekt den Namen „Library“ und der Projektmappe den Namen „Golden“. Lassen Sie **Projektmappenverzeichnis erstellen** aktiviert. Klicken Sie auf **OK**.

3. Öffnen Sie im Projektmappen-Explorer das Kontextmenü für den Knoten **Abhängigkeiten**, und wählen Sie **NuGet-Pakete verwalten** aus.

4. Wählen Sie „nuget.org“ als **Paketquelle** aus, und klicken Sie auf die Registerkarte **Durchsuchen**. Suchen Sie nach **Newtonsoft.Json**. Klicken Sie auf **Installieren**, und akzeptieren Sie die Lizenzbedingungen. Das Paket sollte jetzt unter **Abhängigkeiten/NuGet** angezeigt und automatisch wiederhergestellt werden.

5. Benennen Sie die Datei `Class1.cs` in `Thing.cs` um. Akzeptieren Sie die Umbenennung der Klasse. Fügen Sie eine Methode hinzu: `public int Get(int number) => Newtonsoft.Json.JsonConvert.DeserializeObject<int>($"{number}");`

7. Wählen Sie im Menü **Erstellen** die Option **Projektmappe erstellen**.

   Die Projektmappe wird fehlerfrei erstellt.

### <a name="writing-the-test-project"></a>Schreiben des Testprojekts

1. Öffnen Sie in Projektmappen-Explorer das Kontextmenü des Knotens **Projektmappe**, und wählen Sie **Hinzufügen** > **Neues Projekt** aus. Wählen Sie im Dialogfeld **Neues Projekt** unter **Visual C#/.NET Core** die Option **Komponententestprojekt (.NET Core)** aus. Nennen Sie sie „Testbibliothek“, und klicken Sie auf „OK“. 

2. Öffnen Sie im Projekt **Testbibliothek** das Kontextmenü des Knotens **Abhängigkeiten**, und wählen Sie **Verweis hinzufügen** aus. Klicken Sie auf **Projekte**, überprüfen Sie das Projekt „Library“, und klicken Sie auf „OK“. Dadurch wird einen Verweis auf die Bibliothek aus dem Testprojekt hinzugefügt.

3. Benennen Sie die Datei `UnitTest1.cs` in `LibraryTests.cs` um, und übernehmen Sie die Klassenumbenennung. Fügen Sie oben in der Datei `using Library;` hinzu, und ersetzen Sie die `TestMethod1`-Methode durch den folgenden Code:
    ```csharp
    [TestMethod]
    public void ThingGetsObjectValFromNumber()
    {
        Assert.AreEqual(42, new Thing().Get(42));
    }
    ```

   Sie sollten nun die Projektmappe erstellen können. 
   
4. Wählen Sie im Menü **Test** zunächst **Fenster** und dann **Test-Explorer** aus, um das Test-Explorer-Fenster in Ihrem Arbeitsbereich zu öffnen. Nach wenigen Sekunden sollte der Test `ThingGetsObjectValFromNumber` im Test-Explorer angezeigt werden. Wählen Sie **Alle ausführen** aus.
   
   Der Test sollte erfolgreich verlaufen.

### <a name="writing-the-console-app"></a>Schreiben der Konsolenanwendung

1. Öffnen Sie im Projektmappen-Explorer das Kontextmenü für die Projektmappe, und fügen Sie ein neues Projekt des Typs **Konsolen-App (.NET Core)** hinzu. Nennen Sie es „App“.

2. Öffnen Sie im Projekt **App** das Kontextmenü des Knotens **Abhängigkeiten**, und wählen Sie **Hinzufügen** > **Verweis** aus. 

3. Aktivieren Sie im Dialogfeld **Verweis-Manager** die Option **Bibliothek** unter **Projekte** im Knoten **Projektmappe**, und klicken Sie auf **OK**.

6. Öffnen Sie das Kontextmenü für den Knoten **App**, und wählen Sie **Als Startprojekt festlegen** aus. Dadurch wird sichergestellt, dass bei Drücken von F5 oder STRG+F5 die Konsolen-App gestartet wird.

7. Öffnen Sie die Datei `Program.cs`, fügen Sie am Anfang der Datei eine `using Library;`-Anweisung und anschließend `Console.WriteLine($"The answer is {new Thing().Get(42)}.");` zur `Main`-Methode hinzu.

8. Legen Sie am Ende der hinzugefügten Zeile einen Haltepunkt fest.

9. Drücken Sie F5, um die Anwendung auszuführen.

   Die Anwendung sollte ohne Fehler erstellt werden, und Sie sollten beim Haltepunkt ankommen. Darüber hinaus sollten Sie prüfen können, ob die Ausgabe der Anwendung „42“ lautet.

