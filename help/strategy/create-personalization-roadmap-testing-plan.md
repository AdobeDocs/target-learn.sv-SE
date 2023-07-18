---
title: QuickStart för personaliseringstestning och framtagning av färdplaner
description: Lär dig ett ramverk som du kan använda för att börja validera personaliseringsaktiviteter och skapa en personaliseringskarta som kan köras via Adobe Target och Adobe Analytics.
solution: Target,Analytics
level: Intermediate
role: Leader, Architect, Developer, Admin
exl-id: c0b6f9a0-7074-4e25-81e6-9781a54e2156
source-git-commit: 20bd1eb17ef6e287f7b76e14f727456e12d6f115
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 0%

---

# QuickStart för personaliseringstestning och framtagning av färdplaner

Personaliseringen kan vara kraftfull, men den måste valideras genom tester för att säkerställa att den verkligen ger mervärde. Testning är den mest effektiva strategin för att identifiera vilka, hur och vad ni ska personalisera.

När vi lanserar 2000-talets andra årtionde skiljer organisationer som er från mängden med föråldrade strategier för kundanpassning och felaktig dataanalys. Det här är designen av personalisering, en era där konsumenterna har kommit att förvänta sig ingenting mindre än en anpassad upplevelse. Personalisering på företagsnivå är en komplicerad och ständigt föränderlig process, men om den utförs effektivt kommer den att maximera kundnöjdheten och avsevärt öka avkastningen.

I följande artikel finns ett ramverk som du kan använda för att börja validera personaliseringsaktiviteter och skapa en personaliseringskarta som kan köras via Adobe Target och Adobe Analytics. Adobe QuickStart-ramverket innehåller:

1. **Identifiera personaliseringsmöjligheter** - utnyttja dataanalys för att identifiera möjligheter att påverka viktiga resultatindikatorer på er webbplats, i enlighet med organisationens verksamhetsmål.

1. **Utveckla användningsexempel** - Definiera mål för er personalisering med specifika besökarattribut i åtanke, var tydlig när det gäller hur det kuraterade innehållet kommer att förbättra besökarens upplevelse, i förväg fastställa hur framgången kommer att se ut och vilka åtgärder som kan vidtas från testresultaten.

1. **Skapa en färdplan** - sammanställa en lista och prioritera användningsfall för personalisering, se till att era insatser fokuserar på värdefulla aktiviteter, förväntas förfina och revidera användningsfall och färdplan som bygger på inlärningar.

1. **Designa och kör** - skapa och starta Adobe Target-aktiviteter för att leverera välstrukturerat innehåll till era prioriterade målgrupper.

1. **Vidta åtgärder för resultat** - analysera aktivitetsprestanda och sammanfatta aktivitetsresultat, insikter, rekommendationer och nästa steg.

## Steg 1: Identifiera personaliseringsmöjligheter{#personalization}

Det här är utgångspunkten när du börjar skapa en personaliseringsplan. När ni kör ett lyckat personaliseringsprogram är det viktigt att ni fokuserar på era centrala affärsmål och viktiga resultatindikatorer. Personaliseringsarbetet bör anpassas till detta för att ge värde. Paul Morris, Adobe Business Consultant, säger: &quot;Om allt du gör uppfyller dessa mål är det högst troligt att ditt program kommer att öka värdet. Men om ni har ett utspridt tillvägagångssätt för testning kommer ni förmodligen att finna vissa vinster, men det övergripande programmet blir inte nästan lika framgångsrikt.&quot;

>[!NOTE]
>
>Om ni inte omedelbart vet vilka era centrala affärsmål är är det viktigt att identifiera dem så snart som möjligt. Se till att:


* Upprätta en anpassning mellan era affärsmål och er användbara hypotes. På så sätt kan ni prioritera användningsfall som ger ert företag störst värde.

* Gör era mål mätbara för spårningsändamål och korrelera med intäktseffekten.

* Justering av varje affärsmöjlighet ska påverka ett enda målmått.

Ibland kan man ha mål som från början verkar immateriella också, som varumärkesvärde eller lojalitet. Det är viktigt att ni kan mäta dessa för att kunna använda dem som målmått för personaliseringsaktiviteter. Vanligtvis kan dessa typer av mål fortfarande anpassas till intäktseffekter som kundlivslängd eller anskaffningskostnader.Se till att du regelbundet granskar programresultaten i förhållande till dina huvudverksamhetsmål för att se till att värdet styrs från ditt personaliseringsprogram.

Fokusera på dataanalys för att identifiera specifika delar av webbplatsen som kan förbättras. Adobe rekommenderar att man börjar med Adobe Analytics för att generera riktade användningsfall. Om du har ett analysteam på plats kan du be dem att titta på följande:

1. Personliga förformulärstabeller - En funktion som ger obegränsade uppdelningar och kan hjälpa dig att besvara frågor eller antaganden som du har.
1. Avancerad segmentering - Med segmenterings-IQ kan du jämföra besökare i olika delar av webbplatsen.
1. Juristiska recensioner - Identifiera vilka delar av webbplatsen som skulle kunna dra störst nytta av personalisering. Med dessa granskningar kan ni ta ett steg tillbaka och gå igenom webbplatsen som kunden skulle.
1. Konkurrentanalys - Det kan hända att andra företag ställs inför samma utmaningar som ni. Denna analys är inte begränsad till företag i samma bransch.

Målet med detta steg är att generera åtgärdbara insikter i form av en hypotes. En hypotes är en förutsägelse som du skapar innan du kör ett experiment. Det står tydligt vad som ändras, vad du tror att resultatet blir och varför du tror att det är fallet. Om du kör experimentet kan du bevisa eller motbevisa din hypotes. I slutet av det här steget bör du ha en uppsättning hypoteser för personaliseringsmöjligheter som förbättrar er webbplats och hur nöjda besökarna är.

## Steg 2: Utveckla användningsexempel{#use-cases}

Börja med de hypoteser som genereras i steg 1 och utveckla sedan dina aktiviteter kring dem. Nu kan du utveckla förformstabellerna som skapats i steg 1A; var och en av nyckeltalen har en uppsättning hypoteser, som sedan blir individuella tester inom Adobe Target. Om du har svårt att ta dig till den här punkten kan du börja så enkelt som möjligt, till exempel fokusera på de besökare som kommer tillbaka och besöker webbplatsen. Fundera på hur du kan skräddarsy din hemsida för återkommande besökare. När du har fått en uppsättning hypoteser måste du definiera varje aktivitet för att effektivt prioritera varje användningsfall.

1. Definiera de prioriterade målgrupper som ni vill leverera personaliserat innehåll till, med tanke på de unika besökarattribut som definierar vilka de är och vad de vill ha (t.ex. befintliga kunder kontra potentiella kunder) Prioriterade målgruppers önskemål och behov bör anpassas till era affärsmål

1. Identifiera den specifika plats på besökarens resa där personaliserat innehåll kommer att vara den mest effektiva platsen. Fokusera på sidor där ni förväntar er besökare med olika typer av personligheter eller besökare med olika behov/avsikter.

1. Börja planera lite designarbete av din variant. Innehållet bör noggrant struktureras utifrån målgruppens specifika behov och önskemål, med tanke på var de befinner sig på sin resa. Rätt innehåll bör vara distinkt och differentierat.

## Steg 3: Skapa en färdplan, sammanställning och prioritering av användningsfall

Sammanställ en omfattande lista över personaliseringsmöjligheter som åtminstone fångar upp platsen, idén och prioriteten för personaliseringsaktiviteterna.

Prioriteringssteget är uppdelat i två faktorer:

**Värde:** Använd branschanalyser, jämförelser och liknande användningsexempel från det förgångna för att förstå det förväntade värde som var och en av dina hypoteser kan ge. Du vill att ditt värde ska länkas direkt till ett av dina KBO (Key Business Outcome) och vara i ett standardformat så att alla användningsfall kan jämföras med varandra. Den vanligaste metoden är att tillämpa ett penningvärde för varje användningsfall för jämförelse.

* Kostnad - Det är en naturlig kostnad att bygga ut dina designvarianter inom Target och sedan den potentiella lanseringen. Nu måste du beräkna kostnaden för varje användningsfall. Kostnaden omfattar tid och resurser som krävs för att skapa testupplevelser, schemaläggning och analys efter testet.

Adobe rekommenderar att du rangordnar varje användningsfall på en skala från 1-5. där 1 är enkel och 5 är komplex. Du har nu en uppsättning prioriterade aktiviteter som du kan testa i Adobe Target. Dessa aktiviteter kommer att utgöra grunden för din årliga personalisering. Adobe rekommenderar att man regelbundet gör en ny utvärdering av färdplanen för personalisering. Inlärningarna från varje aktivitet bör påverka era framtida prioriteringar för färdplanen. Insatser och rekommendationer kommer att bli mer effektiva om de vidtas i rätt tid. Prioriteringarna under hela året kan ändras, men med en iterativ metod kan du vara säker på att du alltid har en strategisk handlingsplan och att du kan följa upp målen för ditt team och ditt företag.

## Steg 4: Designa och kör

Genom att utnyttja den dokumentation som skapats för att integrera personaliseringen i praktiken kan du skapa en personaliseringsaktivitet i Target och leverera välstrukturerat innehåll till era prioriterade målgrupper. Se till att aktivitetstypen, inställningarna, upplevelserna och rapportfunktionerna är anpassade efter målen för användningsfallet. Design, QA och Launch av er personalisering är mest effektiva när ni går med i befintliga organisationsprocesser.

## Steg 5: Vidta åtgärder för resultat

När personaliseringsaktiviteten har engagerat ett representativt urval av besökare kan ni börja analysera och utnyttja insikterna för att vägleda nästa steg. Var datadriven i er analys, knyt rekommendationer till er fallhypotes och tydligt illustrera effekten på affärsmålen.

### Mer information

Vi rekommenderar att du tittar på den här videon som beskriver vart och ett av dessa steg: [https://adobecustomersuccess.adobeconnect.com/pvsqvdvunpai/](https://adobecustomersuccess.adobeconnect.com/pvsqvdvunpai/)

Läs mer om strategi och tankeledarskap på [Nöjda kunder](https://experienceleague.adobe.com/docs/customer-success/customer-success/overview.html) nav.