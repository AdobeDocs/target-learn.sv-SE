---
title: Optimera er implementering av Adobe Target
description: Få en översikt över Adobe Target implementering och struktur. Lär dig hur du förstår och granskar din organisations konfiguration. Lär dig vanliga felsökningstekniker och tips om hur du skapar en kunskapsdatabas för ditt team.
solution: Target
feature: Overview
role: Leader, User
exl-id: 49b69f41-0993-437c-bb69-84392be427df
source-git-commit: 20bd1eb17ef6e287f7b76e14f727456e12d6f115
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 0%

---

# Optimera er implementering av Adobe Target

Om du inte är van vid din organisation och vill bekanta dig med vad som är på plats från en testnings- och optimeringspraxis hjälper den här artikeln dig att komma igång. Vi börjar med en översikt över Adobe Target implementering och struktur. Du får lära dig att förstå och granska hur din organisation är konfigurerad. Slutligen diskuterar vi vanliga felsökningstekniker och tips om hur du skapar en kunskapsdatabas för ditt team.

Adobe Target är ett verktyg som gör det möjligt att testa och rikta unikt innehåll till olika besökare. [Gå till den här guiden](https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en) om du vill se en översikt över tillgängliga funktioner.

## Målgenomförande och struktur

Innan vi börjar dyka upp i implementeringsprocessen för Adobe Target eller hur den är uppbyggd är det bra att först förstå några grundläggande saker om programvaran.

Adobe Target är ett verktyg som gör det möjligt att testa och målinrikta unikt innehåll för olika besökare utan att ändra den interna webbplatskoden. Målet ändrar tillfälligt slutanvändarens upplevelse och spårar även användarens beteende efter att ändringen har visats. Target ger också möjlighet att ändra slutanvändarnas upplevelse baserat på profilinformation eller tidigare åtgärder.

Det finns tre typer av grundläggande målaktiviteter:

1. A/B-test
2. Multivariata tester (MVT)
3. Upplevelsetestning

**A/B-testet** jämför två eller flera upplevelser för att se vilka som förbättrar konverteringarna bäst under en fördefinierad testperiod. A/B-testet är ett mycket kontrollerat experiment med trafikmätningar, uppdelat i procent i stället för i regel, vilket gör att du kan:

* för att analysera testdata.
* för att få kunskap om er målgrupp.
* för att avgöra vilken upplevelse som fungerar bäst.

**Multivariata tester** (MVT) jämför kombinationer av erbjudanden mellan element på en sida för att se vilken kombination som fungerar bäst för en viss målgrupp. Det här testet identifierar också vilket element på sidan som bäst förbättrar konverteringarna under en förspecificerad testperiod. MVT ger:

* Ett sätt att visa flera erbjudanden i flera olika element.
* En metod för att testa den resulterande unika upplevelsen mot ett specifikt mål.
* Insikt om vilka element som har störst negativ eller positiv inverkan på besökarinteraktioner.

**Experience testing** (Experience testing) levererar innehåll till en viss målgrupp baserat på en uppsättning marknadsföringsdefinierade regler och kriterier. Med den här metoden kan du rikta specifikt innehåll mot en viss målgrupp baserat på en uppsättning definierade allokeringsregler.

Hur fungerar Target?

Här är ett högnivåexempel på hur Target fungerar:

1. En besökare begär en sida från servern och den visas i webbläsaren.
1. En cookie för första part anges i besökarens webbläsare för att lagra beteendet.
1. Därefter ringer sidan Adobe Target.
1. Innehållet visas baserat på reglerna för användarens aktivitet.
1. Adobe Target samlar in specifika mätvärden enligt definitionen i aktivitetskonfigurationen för att mäta testupplevelsernas påverkan.

Target bygger på en&quot;global Mbox&quot; som ger möjlighet att påverka vad som helst på sidan. Den här funktionen distribueras på sidan antingen som en hårdkodad länk till filen at.js eller som levereras med en tagghanterare som Adobe Launch.

## Förstå er nuvarande implementering

Adobe rekommenderar att du granskar implementeringen av målanvändargränssnittet tillsammans med tagghanteraren och implementeringen av sidinläsning för att få en förståelse för den aktuella implementeringen.

**Så här granskar du [!DNL Target]-användargränssnittet:**

1. Börja granska [!DNL Target]-gränssnittet:

   * Granska teknikstacken [!DNL Target]
   * Bekräfta tillgängliga funktioner
   * Identifiera var distributionen finns

1. Granska aktiviteter för bästa praxis:

   * Granska historiska kampanjer för programmognad

1. Inaktivera gamla aktiviteter:

   * Arkivera och rensa [!DNL Target]-resurs som inte längre har aktuell eller framtida användning

1. Granska målgrupper.

1. Granska miljödefinitioner och associerade domäner.

1. Granska profilskript för tillämplighet

   * Alla profilskript körs för varje målanrop
   * Bibehåll samtalseffektivitet genom att ta bort icke tillämpliga skript

Så här granskar du tagghanteraren och sidinläsningen:

1. Bekräfta följande i tagghanteraren:

   * Distributionen av den förväntade [!DNL Target] JavaScript-koden
   * Lämplig lösning för att dölja innehåll
   * Ange nödvändiga regler för att fylla i [!DNL Target]-anropen med förväntade parametrar

1. Bekräfta följande under sidinläsning:

   * Matchande versionsnummer för begärande-URL och [!DNL Target] begärande-URL
   * Populerat upplevelsebaserat moln-ID-värde (molninnehåll)
   * Visa förväntade integreringsvärden (molninnehåll)
   * Fyllda [!DNL Target] parametrar på lämpliga sidor

## [!DNL Target] granskningsaktiviteter

Om du vill undvika att gå igenom varje sida manuellt för att granska [!DNL Target]-aktiviteter kan du använda Adobe Auditor för att få en förståelse för det aktuella tekniska tillståndet för implementeringen. Adobe Auditor drivs av ObservePoint och kan konfigureras för att köras manuellt för att identifiera implementeringsproblem på hög nivå på din webbplats.

Adobe Auditor tillhandahåller

* Hälsa på hög plats
* Snabba utlysningar för implementeringsfrågor

Adobe rekommenderar att man utför manuella revisioner varje månad för att

* Identifiera sidor utan taggar
* Identifiera inkonsekventa versioner
* Läs om inaktuella versioner
* Ange detaljerad information som kan exporteras

## Vanlig felsökning

>[!NOTE]
>
>Adobe rekommenderar att du installerar Adobe Experience Platform Debugger.

Här följer allmänna felsökningstips när du går in i upplevelsen:

### Cache och cookies**

* Clearing av cacheminne och cookies
* Var försiktig i privat läge (till exempel: privat läge i Firefox kan blockera [!DNL Target])

### Är du kvalificerad för aktiviteten?

* Kontrollera att du har utfört samma steg som målgruppen använde i aktiviteten
* Använd `mboxTrace` eller svarstoken för att kontrollera profil- och segmentvärden

### Allmänna felsökningstips vid validering av visuella/funktionella

Om finns i [!DNL Target]-upplevelsen och du inte ser den förväntade visuella upplevelsen:

Kontrollera [!DNL Target]-svaret:

* Om koden inte körs:

1. Kontrollera aktiviteter som är i konflikt
1. Kontakta kundtjänst

* Om koden körs:

1. Arbeta om koden i det scenariot

## Underhålla ett kunskapsarkiv

En kunskapsdatabas är en onlineplattform som används för att dokumentera och dela information. Kunskapsdatabasen innehåller information som är specifik för din implementering och kan innehålla teamspecifik information.

Helst bör databasen tillåta redigering och automatiskt sparande inom plattformen. När konfigurationen är klar är det enkelt att underhålla och hålla den uppdaterad. Innehåll i kunskapsdatabasen struktureras baserat på användarroller.

Vanliga dokument i en kunskapsdatabas är:

* **Översiktsdokument** - ett dokument som används för att tydligt förklara programmens mål, mål, processer och struktur
* **Identifieringsdatabas** - ett dokument som används för att hantera och prioritera potentiella idéer som inte är klara för testprocessen
* **Programfärdplan** - ett dokument som används för att hantera alla aspekter av testningsaktiviteter när idéer är klara att starta testprocessen
* **Dokument för aktivitetsplan** - ett dokument som används för att skapa information som behövs för att skapa och starta aktiviteter
* **Dokument för aktivitetsplan** - ett dokument som används för att förmedla resultat och rekommenderade nästa steg till intressenter
* **Programkontrollpanel** - ett dokument som används för att spåra programmets prestanda, avslut och intäktsfördelar över tid.

Mer information finns i vårt [webbinarium](https://adobecustomersuccess.adobeconnect.com/p4p7xlp7dh42mp4/) med Senior Consultant, Wilder Freed.

Läs mer om strategi och tankeledarskap på navet [Nöjda kunder](https://experienceleague.adobe.com/docs/customer-success/customer-success/overview.html).
