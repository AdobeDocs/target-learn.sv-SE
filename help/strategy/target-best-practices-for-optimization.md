---
title: Bästa tillvägagångssätt för optimering
description: Lär dig Adobe sex viktiga optimeringsfunktioner och hur du använder dem.
solution: Target
role: Leader, Architect, Developer, Admin
feature: Overview
level: Beginner
exl-id: dd29faea-bb67-4128-b261-fa407ba7158c
source-git-commit: d65720ae992a3079462ba59421c3b7a8d4f5ea7b
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 0%

---

# Bästa tillvägagångssätt för optimering med Adobe Target

Lär dig Adobe sex viktiga optimeringsfunktioner och hur du använder dem.

När det gäller att bygga upp en stark digital närvaro finns det ett antal utmaningar som ditt team kommer att ställas inför. Ni behöver inte bara engagera hundratals, till och med tusentals kunder, utan även en mängd unika beteenden och önskemål som förändras över tid, och det är upp till er att inte bara hålla jämna steg med dessa ändringar, utan också förutse dem och genomföra era strategier effektivt och korrekt. Det är en tävling mot konkurrenter i en ständig innehållsmaraton som kräver konstant upprepning och förstklassig teknik.

En lösning på den här mångfacetterade utmaningen är optimering med Adobe Target, som ser till att ni har en digital närvaro som är relevant, värdefull och fri från friktioner. Den tekniska arkitekturen och de kanaler som du distribuerar [!DNL Target] i varierar avsevärt mellan olika kunder, men vi har strukturerat en lista över bästa praxis och optimeringsstrategier som varje team kan använda för att utnyttja alla funktioner i det här kraftfulla verktyget.

## Optimering

Optimering definieras som&quot;åtgärden att göra den bästa eller mest effektiva användningen av en situation eller resurs&quot;. Det är det mest effektiva sättet att se till att ni har kvalitativa data som visar att de ändringar ni gör är värdefulla. För att optimera på ett verkligt sätt måste ni kunna mäta effekten och värdet av era insatser. Annars kommer de ändringar du gör att du får en högre kostnad med minimal vinst. För att uppnå detta effektivt måste ni börja med strategisk planering. Utan att ta med en strategisk plan i optimeringen skulle ni helt enkelt gissa.

### Sex grundläggande optimeringsfunktioner

1. **Strategize**: Identifiera möjligheter för aktiviteter som är anpassade till affärsmålen och som är baserade på data.
1. **Prioritera**: Rankning och schemalägg aktiviteter baserat på affärsjustering, ansträngningsnivå och potentiell påverkan.
1. **Designa**: Skapa färdiga visuella effekter av aktivitetsupplevelser och utveckla aktivitetsplaner med detaljerade kriterier.
1. **Bygg och kör**: Utveckla aktivitet inklusive [!DNL Target] konfiguration, kodutveckling och QA-testning.
1. **Analysera**: Starta [!DNL Target]-aktivitet för att skapa och övervaka prestanda under aktivitetens varaktighet.
1. **Agera och iterera**: Utveckla rekommendationer baserat på prestanda för test- eller personaliseringsaktivitet.

Eftersom vi vet att förändringen är en konstant bör vår optimeringsstrategi vara en iterativ körningscykel som uppfyller kundernas ständigt föränderliga behov (se bild 1 nedan).

![Optimering och personalisering](assets/optimize-and-personalize.png)

_Figur 1 - Optimeringsinteraktiv cykel_

## Bygga en optimeringsstrategi

Processen med att utveckla en optimeringsstrategi kan delas upp i: (1) Bygga en testaktivitetsplan och (2) Förstå optimeringsgrunderna.

1: Testverksamhetsplanen bör dokumenteras. Detta garanterar att du har en minimal kvalitetsstandard när det gäller programmet för testaktivitet. Testaktivitetsplanen ska innehålla:

* **Namn och beskrivning:** Intuitivt aktivitetsnamn och beskrivning av det som experimentet fokuserar på. &quot;Hur? Vad? När? Var? Varför?&quot;

* **Mål:** Syftet med aktiviteten och det anpassade affärsmålet är att den ska påverka.

* **Hypotes:** En hypotes är en förutsägelse som du skapar innan du kör ett experiment. Det står tydligt vad som testas, vad du tror att resultatet blir och varför du tror att det är fallet. Om du kör experimentet kommer du antingen att bevisa eller motbevisa din hypotes.

En fullständig hypotes består av tre delar:

* Om _variabel_
* Sedan _result_
* Eftersom _logisk_

* **Plats:** URL, sidavsnitt och enhetstyp.
* **Målmått:** Hur mäts om åtgärden lyckades?
* **Sekundära mått:** Andra värdefulla nyckeltal (KPI) att utvärdera i syfte att ytterligare förstå inverkan och planering av iterationer.
* **Aktivitetsmålgrupp:** Beskrivning av obligatorisk filtrering av testexponering.
* **Rapporterande målgrupper:** Lista med beskrivningar av besökarunderuppsättningar som ska användas för analys.
* **Experience Concepts:** Mockups, example wireframes och descriptions.

**Allmänt Obs!** Alla element på en webbsida som kan ge affärsvärde eller ge värdefulla insikter i besökarnas beteende kan testas. Några vanliga typer av testaktiviteter är:

* Rubriktext
* Innehållstext
* Knapptext
* Layout
* Fotografi
* Knappfärg
* Elementlayout
* Borttagning och tillägg av element
* Navigeringsordning
* Navigeringstaxonomi
* Sökbetoning

2: Det andra steget i strategin är att förstå optimeringsgrunderna, som innefattar förståelsen av testelementen i sig. Testelementen i Optimering är bland annat:

    A. Elementvärde
    
    Detta uppnås genom att man tar ett steg tillbaka för att fråga, varför det finns ett visst element på webbplatsen och har innehållet ett visst syfte? De här frågorna är ett bra ställe att börja på om sajten precis har avslutat en ny design eller om en ny funktion nyligen har lanserats. Den taktik som används för att fastställa elementvärdet kallas för Inkluderings-/uteslutningstestning. Inkluderings-/exkluderingstestning ger en bra läsning av värdet på sidan där elementet visas.
    
    B. Elementpresentation
    
    Här kan du tänka på elementets allmänna utseende och känsla och hur det påverkar den övergripande sidpresentationen. Den taktik som används för presentationen är att fokusera på att göra slagkraftiga ändringar av innehåll och elementsidor.
    
    C. Elementfunktion
    
    Här frågar vi om elementet på sidan gör vad det ska göra? Är interaktionen framgångsrik och fungerar den som den ska? Är interaktionen naturlig eller en friktionspunkt? Den taktik som används för funktionen är att skapa upplevelser som är fokuserade på lättanvända funktioner utan extra kostnadseffekt.

## Optimering jämfört med personalisering

Nu när vi har analyserat och listat strategikomponenterna är det viktigt att skilja mellan optimeringssatsningar och Personalization insatser. Optimering är ett sätt att få till det bästa eller effektivaste sättet att använda en situation eller en resurs, medan Personalization är ett sätt att utforma eller producera något som uppfyller någons individuella behov.

På en hög nivå:

* Optimeringen är inriktad på att testa vad som är effektivast och bäst resultat för ALLA som interagerar med er digitala närvaro.
* Personalization testar för att hitta det som är effektivast och bäst för SOME av dem som interagerar med er digitala närvaro.

När man fokuserar på optimering är de vanligaste testaktiviteterna:

* **A/B-testning:** Realtidstestning av två eller flera sidor eller sidelement mot varandra för att få kvantitativ insikt i kundernas önskemål.
* **Multivariata tester:** Jämföra kombinationer av erbjudanden mellan element på en sida för att se vilken kombination som fungerar bäst. Dessutom kommer multivariattestet att identifiera vilket element på sidan som ger bäst förbättring av konverteringarna.

När du fokuserar på Personalization ser du troligen samma testningsaktiviteter som i Optimering, men de är avsedda för mer specifika målgrupper. I A/B-testning kommer ni sannolikt att lägga till sidor och målgrupper i upplevelserna för att vidareutveckla er Personalization.

Personalization innehåller även testaktivitetstypen Experience Targeting, som levererar innehåll till specifika målgrupper baserat på en uppsättning definierade regler och kriterier. I takt med att du börjar växa och fördjupa dig i Personalization är det här också några av Target premiumfunktioner som:

* Typ av Automated Personalization-aktiviteter
* Typ av rekommendationsaktiviteter

## Optimering före personalisering

Med tanke på ovanstående förståelse rekommenderar Adobe att du Optimerar innan du personaliserar, och går från bred till granulerad Personalization. Om du vill utveckla Personalization-aktiviteter från breda till detaljerade, börjar du med att använda en personalisering (bred) från en till många (med A/B-testning) och går sedan över till en personalisering (granulär) (med hjälp av automatiserade personaliseringsaktiviteter).

Mer information finns i [QuickStart för personaliseringstestning och framtagning av färdplaner](https://experienceleague.adobe.com/en/perspectives/quickstart-for-personalization-testing-and-roadmap-creation).

Läs mer om strategi och tankeledarskap i navet [Perspective](https://experienceleague.adobe.com/en/perspectives) .
