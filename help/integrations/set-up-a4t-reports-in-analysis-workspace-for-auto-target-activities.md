---
title: Ställa in A4T-rapporter i Analysis Workspace för Automatisk målaktivitet
description: När ni har er integrering med Analytics for Target (A4T) på plats och ni kör Auto-Target-aktiviteter, hur kan ni se till att ni tolkar resultaten korrekt? Följ de här stegen för att konfigurera A4T-rapporter i Analysis Workspace så att du får förväntade resultat när du kör Auto-Target-aktiviteter.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 58006a25-851e-43c8-b103-f143f72ee58d
source-git-commit: e1acb84970b967625e0b6c7495067ed6456a6aa3
workflow-type: tm+mt
source-wordcount: '2575'
ht-degree: 0%

---

# Konfigurera A4T-rapporter i Analysis Workspace för [!DNL Auto-Target] verksamhet

Analytics för Target-integrering (A4T) för [!DNL Auto-Target] aktiviteter använder Adobe Target ML-algoritmer (Ensemble Machine Learning) för att välja den bästa upplevelsen för varje besökare utifrån deras profil, beteende och sammanhang, samtidigt som ett Adobe Analytics-målmått används.

Det finns omfattande analysfunktioner i Adobe Analytics Analysis Workspace, men några ändringar i standardinställningarna **[!UICONTROL Analytics for Target]** panel krävs för korrekt tolkning [!DNL Auto-Target] aktiviteter, på grund av skillnader mellan experimentella aktiviteter (manuell A/B och automatisk fördelning) och personaliseringsaktiviteter ([!DNL Auto-Target]).

I den här självstudiekursen går vi igenom de rekommenderade ändringarna för analys [!DNL Auto-Target] aktiviteter i Workspace, som bygger på följande nyckelbegrepp:

* The **[!UICONTROL Control vs Targeted]** kan användas för att skilja mellan olika Control-upplevelser och de som [!DNL Auto-Target] ensemble ML-algoritm.
* Besök bör användas som normaliseringsmått när du visar prestandaindelningar på Experience-nivå. Dessutom [Adobe Analytics standardberäkningsmetod kan omfatta besök där användaren inte ser aktivitetsinnehållet](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html?lang=en#metrics)men det här standardbeteendet kan ändras med ett segment med rätt omfång (se informationen nedan).
* Omfattad attribuering av besök-lookback, som också kallas besökslookback-fönstret i den förskrivna attribueringsmodellen, används av Adobe Target ML-modeller under deras utbildningsfaser, och samma (ej standard) attribueringsmodell bör användas när målmåttet bryts ned.

## Skapa A4T för [!DNL Auto-Target] panel i arbetsytan

Skapa en A4T för [!DNL Auto-Target] rapport, antingen börja med **[!UICONTROL Analytics for Target]** i arbetsytan, som visas nedan, eller börja med en friformstabell. Gör sedan följande val:

1. **[!UICONTROL Control Experience]**: Ni kan välja vilken erfarenhet ni vill; Du kommer dock att åsidosätta det här alternativet senare. Observera att för [!DNL Auto-Target] kontrollupplevelsen är i själva verket en kontrollstrategi, som antingen är till för att a) Slumpmässigt fungera bland alla upplevelser, eller b) En enda upplevelse (det här valet görs när en aktivitet skapas i Adobe Target). Även om du valde att välja (b) - [!DNL Auto-Target] aktivitet som har betecknat en specifik upplevelse som Kontroll - du bör fortfarande följa det tillvägagångssätt som beskrivs i den här självstudiekursen för att analysera A4T för [!DNL Auto-Target] verksamhet.
2. **[!UICONTROL Normalizing Metric]**: Välj Besök.
3. **[!UICONTROL Success Metrics]**: Även om du kan välja vilka mätvärden som ska rapporteras, bör du vanligtvis visa rapporter med samma mätvärden som valdes för optimering när aktiviteter skapades i Adobe Target.

![Figur 1.png](assets/Figure1.png)
*Bild 1: Analyser för konfiguration av målpanel för [!DNL Auto-Target] verksamhet.*

>[!NOTE]
>
>Om du vill konfigurera din Analytics för målpanelen för Automatisk målaktivitet väljer du en kontrollupplevelse, väljer Besök som normaliseringsmått och väljer samma målmått som valdes för optimering när målaktiviteten skapades.

## Använd måttet Kontroll kontra Mål för att jämföra Adobe Target enemble ML-modell med din kontroll

A4T-standardpanelen är utformad för klassiska (manuella) A/B-tester eller automatisk fördelning-aktiviteter där målet är att jämföra prestanda för enskilda upplevelser med kontrollupplevelsen. I [!DNL Auto-Target] den första orderjämförelsen bör dock vara mellan kontrollverksamheten *strategi* och målgruppen *strategi* (med andra ord, fastställa lyften för den totala prestandan hos [!DNL Auto-Target] ensemble ML model over the Control strategy).

Om du vill göra den här jämförelsen använder du **[!UICONTROL Control vs Targeted (Analytics for Target)]** dimension. Dra och släpp för att ersätta **[!UICONTROL Target Experiences]** -dimension i standardrapporten för A4T.

Observera att den här ersättningen gör standardberäkningarna för Lyft och pålitlighet ogiltiga på A4T-panelen. För att undvika förvirring kan du ta bort dessa mått från standardpanelen och lämna följande rapport:

![Figur 2.png](assets/Figure2.png)
*Bild 2: Rekommenderad baslinjerapport för [!DNL Auto-Target] verksamhet. Den här rapporten har konfigurerats för att jämföra riktad trafik (hanteras av den ensemble ML-modellen) med din Control-trafik.*

>[!NOTE]
>
>För närvarande är lyft- och konfidensvärden inte tillgängliga för kontrollvärden och måldimensioner för A4T-rapporter för Automatiskt mål. Tills support har lagts till kan Lyft och pålitlighet beräknas manuellt genom att ladda ned [konfidensräknare](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx?lang=en).

## Lägg till analysstatistik på Experience-nivå

För att få ytterligare insikter om hur den ensemble ML-modellen fungerar kan du undersöka uppdelningar på Experience-nivå i **[!UICONTROL Control vs Targeted]** dimension. Dra i arbetsytan **[!UICONTROL Target Experiences]** i rapporten och sedan separat bryt ned alla kontrolldimensioner och måldimensioner.

![Figur 3.png](assets/Figure3.png)
*Bild 3: Uppdelning av måldimensionen efter målupplevelser*

Här visas ett exempel på den resulterande rapporten.

![Figur 4.png](assets/Figure4.png)
*Bild 4: En standard [!DNL Auto-Target] rapportera med uppdelningar på Experience-nivå. Observera att dina målvärden kan vara olika och att din kontrollstrategi kan ha en enda upplevelse.*

>[!TIP]
>
>I Arbetsyta klickar du på kugghjulsikonen för att dölja procentvärdena i kolumnen Konverteringsgrad, så att du kan fokusera på upplevelsekonverteringsgraden. Observera att konverteringsgraden då kommer att formateras som decimaler, men tolka dem som procenttal.

## Därför är &quot;besök&quot; rätt normaliseringsmått för [!DNL Auto-Target] verksamhet

När en [!DNL Auto-Target] väljer du alltid Besök som standardmått för normalisering. [!DNL Auto-Target] personalisering väljer en upplevelse för en besökare en gång per besök (formellt en gång per Adobe Target-session), vilket innebär att den upplevelse som visas för en användare kan ändras vid varje besök. Om du använder unika besökare som normaliseringsmått kan det faktum att en enskild användare kan få flera upplevelser (mellan olika besök) leda till förvirrande konverteringsgrader.

Ett enkelt exempel visar detta: ett scenario där två besökare deltar i en kampanj som bara har två upplevelser. Den första besökaren besöker två gånger. De tilldelas till Experience A vid det första besöket, men Experience B vid det andra besöket (eftersom deras profilstatus ändras vid det andra besöket). Efter det andra besöket konverterar besökaren genom att göra en beställning. Konverteringen tillskrivs den senast visade upplevelsen (upplevelse B). Den andra besökaren besöker också två gånger och visas Experience B båda gånger, men konverterar aldrig.

Låt oss jämföra rapporter på besökarnivå och besöksnivå:

| Upplevelse | Unika besökare | Besök | Konverteringar | Besökarnorm. Konv. Hastighet | Besök norm. Konv. Hastighet |
| --- | --- | --- | --- | --- | --- |
| A | 1 | 1 | - | 0 % | 0 % |
| B | 2 | 3 | 1 | 50 % | 33,3 % |
| Summor | 2 | 4 | 1 | 50 % | 25 % |

*Tabell 1: Exempel på jämförelse av besökarnormaliserade rapporter och besöknormaliserade rapporter för ett scenario där besluten är snäva mot ett besök (och inte besökare, som med vanlig A/B-testning). Besökarnormaliserade värden är förvirrande i det här scenariot.*

Som framgår av tabellen finns det en tydlig inkonsekvens i besökarnivånummer. Trots att det finns två unika besökare totalt är detta inte en summa unika besökare för varje upplevelse. Även om konverteringsgraden på besökarnivå inte nödvändigtvis är fel, så är konverteringsgraden på besöksnivå mer begriplig när man jämför enskilda upplevelser. Formeligen är analysenheten (&quot;besök&quot;) densamma som enheten för att fatta beslut, vilket innebär att man kan lägga till och jämföra analysdata på erfarenhetsnivå.

## Filter för faktiska besök i aktiviteten

Adobe Analytics standardberäkningsmetod för besök i en Target-aktivitet kan omfatta besök där användaren inte interagerade med Target-aktiviteten. Detta beror på hur Target-aktivitetstilldelningar bevaras i Analytics-besökarkontexten. Resultatet är att antalet besök i Target-aktiviteten ibland kan öka, vilket leder till en minskning av konverteringsgraden.

Om du föredrar att rapportera besök där användaren faktiskt interagerade med aktiviteten Automatiskt mål (antingen genom att gå in i aktiviteten, visa/besöka eller genom en konvertering) kan du:

1. Skapa ett specifikt segment som innehåller träffar från målaktiviteten i fråga och sedan
1. Filtrera Visits-måttet med det här segmentet.

**Så här skapar du segmentet:**

1. Välj **[!UICONTROL Components > Create Segment]** i verktygsfältet Arbetsyta.
2. Ange **[!UICONTROL Title]** för segmentet. I exemplet nedan namnges segmentet [!DNL "Hit with specific Auto-Target activity"].
3. Dra **[!UICONTROL Target Activities]** dimension till segmentet **[!UICONTROL Definition]** -avsnitt.
4. Använd **[!UICONTROL equals]** -operator.
5. Sök efter din specifika Target-aktivitet.
6. Markera kugghjulsikonen och välj **[!UICONTROL Attribution model > Instance]** som visas i figuren nedan.
7. Klicka på **[!UICONTROL Save]**.

![Figur 5.png](assets/Figure5.png)
*Bild 5: Använd ett segment som det som visas här för att filtrera Visits-måttet i A4T för [!DNL Auto-Target] rapport*

När segmentet har skapats kan du använda det för att filtrera Visits-måttet, så i Visits-mätningen inkluderas endast besök där användaren interagerade med Target-aktiviteten.

**Så här filtrerar du besök med det här segmentet:**

1. Dra det nyligen skapade segmentet från komponentverktygsfältet och för markören över baslinjen på **[!UICONTROL Visits]** måttetikett tills en blå **[!UICONTROL Filter by]** visas.
2. Släpp segmentet. Filtret tillämpas på det måttet.

Den sista panelen visas enligt följande.

![Figur 6.png](assets/Figure6.png)
*Bild 6: Rapporteringspanelen med segmentet&quot;Träff med specifik aktivitet&quot; tillämpat på [!UICONTROL Visits] mätvärden. Detta garanterar endast besök där en användare faktiskt interagerade med målaktiviteten i fråga ingår i rapporten.*

## Se till att målmåtten och målattribueringen är anpassade efter optimeringskriteriet

A4T-integreringen tillåter [!DNL Auto-Target]XML-modell som ska *utbildad* använda samma konverteringshändelsedata som Adobe Analytics använder för *generera resultatrapporter*. Det finns dock vissa antaganden som måste användas för att tolka dessa data när man utbilda ML-modellerna, som skiljer sig från de standardantaganden som gjorts under rapporteringsfasen i Adobe Analytics.

Adobe Target ML-modeller använder en besöksomfångsmodell. Det innebär att de antar att en konvertering måste ske vid samma besök som en visning av aktivitetens innehåll, för att konverteringen ska&quot;tillskrivas&quot; det beslut som fattas av ML-modellen. Detta krävs för att Target ska kunna garantera snabb utbildning i sina modeller. Target kan inte vänta i upp till 30 dagar på en konvertering (standardattribueringsfönstret för rapporter i Adobe Analytics) innan det inkluderas i utbildningsdata för modellerna.

Skillnaden mellan den attribuering som används av Target:s modeller (under utbildning) och den standardattribuering som används i frågedata (under rapportgenerering) kan således leda till avvikelser. Det kan till och med verka som om ML-modellerna fungerar dåligt, när frågan i själva verket är attribuering.


>[!TIP]
>
>Om ML-modellerna optimerar för ett mätvärde som är tilldelat på ett annat sätt än det mätvärde du visar i en rapport, kanske modellerna inte fungerar som förväntat! För att undvika detta bör du se till att målmåtten i rapporten använder samma metriska definition och attribuering som används av Target:s ML-modeller.

Exakt måttdefinition och attribueringsinställningar beror på [optimeringskriterium](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#supported) du angav när aktiviteten skapades.


### Måldefinierade konverteringar eller analysstatistik med *Maximera måttvärde per besök*

När mätvärdet är en Target-konvertering eller en Analytics-mätning med **Maximera måttvärde per besök**kan målmåttsdefinitionen göra att flera konverteringshändelser inträffar vid samma besök.
Följ de här stegen för att visa målmått som har samma attribueringsmetod som används i Adobe Target ML-modeller:

1. Håll muspekaren över mållätarens kugghjulsikon:
   ![gearicon.png](assets/gearicon.png)
1. Bläddra till den resulterande menyn **[!UICONTROL Data settings]**.
1. Välj **[!UICONTROL Use non-default  attribution model]** (om det inte redan är markerat):
   ![non-defaultattributionmodel.png](assets/non-defaultattributionmodel.png)
1. Klicka på **[!UICONTROL Edit]**.
1. Välj **[!UICONTROL Model]**: **[!UICONTROL Participation]** och **[!UICONTROL Lookback window]**: **[!UICONTROL Visit]**.
   ![ParticipationbyVisit.png](assets/ParticipationbyVisit.png)
1. Klicka på **[!UICONTROL Apply]**.

Med de här stegen kan du försäkra dig om att målmåttet i din rapport tilldelas till visningen av upplevelsen, om målmåtthändelsen inträffar *när* (&quot;deltagande&quot;) i samma besök som en upplevelse visades.

### Analytics-statistik med *Unika konverteringshastigheter för besök*

**Definiera besöket med ett positivt mätsegment**

I scenariot där du valde *Maximera konverteringsgraden för unika besök* som optimeringskriterier är den korrekta definitionen av konverteringsgraden den andel besök där mätvärdet är positivt. Detta kan uppnås genom att skapa en segmentfiltrering ned till besök med ett positivt värde för mätvärdet och sedan filtrera besöksmätningen.


1. Som tidigare väljer du **[!UICONTROL Components > Create Segment]** i verktygsfältet Arbetsyta.
2. Ange **[!UICONTROL Title]** för segmentet. I exemplet nedan namnges segmentet [!DNL "Visits with an order"].
3. Dra basmåttet som du använde i optimeringsmålet till segmentet . I exemplet nedan använder vi **order** mätvärden, så att konverteringsgraden mäter andelen besök där en order registreras.
4. Välj längst upp till vänster i segmentdefinitionsbehållaren **[!UICONTROL Include]** **Besök**.
5. Använd **[!UICONTROL is greater than]** och ange värdet till 0 (d.v.s. segmentet omfattar besök där ordermåttet är positivt)
6. Klicka på **[!UICONTROL Save]**.

![Figur7.png](assets/Figure7.png)
*Bild 7: Segmentdefinitionsfiltrering till besök med en positiv ordning. Beroende på aktivitetens optimeringsmått måste du ersätta beställningar med ett lämpligt mätvärde*

**Använd detta för besök i aktivitetsfiltrerade mätvärden**

Det här segmentet kan nu användas för att filtrera besök med ett positivt antal order och där det var en träff för [!DNL Auto-Target]aktivitet. Hur man filtrerar ett mätvärde liknar det som var fallet tidigare, och efter att ha tillämpat det nya segmentet på det redan filtrerade besöksmätningen bör rapportpanelen se ut som i bild 8

![Figur8.png](assets/Figure8.png)
*Bild 8: Rapportpanelen med rätt konverteringsmått för unika besök, dvs. antalet besök där en träff från aktiviteten registrerades och där konverteringsmåttet (order i det här exemplet) inte var noll.*


## Slutligt steg: Skapa en konverteringsgrad som fångar magin ovan

Med ändringarna av värdena för Besök och Mål i föregående avsnitt bör du göra den slutliga ändringen i standardvärdet för A4T för [!DNL Auto-Target] ska man skapa konverteringsgrader som har rätt proportion - det korrigerade målmåttet - till ett lämpligt filtrerat besöksmått.

Gör detta genom att skapa ett beräknat mått enligt följande steg:

1. Välj **[!UICONTROL Components > Create Metric]** i verktygsfältet Arbetsyta.
1. Ange **[!UICONTROL Title]** för dina mätvärden. Exempel: &quot;Besökskorrigerad konverteringsgrad för aktivitet XXX.&quot;
1. Välj **[!UICONTROL Format]** = Procent och **[!UICONTROL Decimal Places]** = 2.
1. Dra relevanta målmått för din aktivitet (till exempel Aktivitetskonverteringar) till definitionen och använd kugghjulsikonen på det här målmåttet för att justera attribueringsmodellen till (Deltagande|Besök) enligt beskrivningen ovan.
1. Välj **[!UICONTROL Add > Container]** från det övre högra hörnet i **[!UICONTROL Definition]** -avsnitt.
1. Välj divisionsoperatorn ( max) mellan de två behållarna.
1. Dra det segment du skapade tidigare - med namnet&quot;Hit with specific [!DNL Auto-Target] aktiviteten&quot; i den här självstudiekursen - för [!DNL Auto-Target] aktivitet.
1. Dra **[!UICONTROL Visits]** mätvärden in i segmentbehållaren.
1. Klicka på **[!UICONTROL Save]**.

>[!TIP]
>
> Du kan också skapa det här måttet med [snabb beräknad mätfunktionalitet](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=en).

Den fullständiga definitionen för beräknade mätvärden visas här.

![Figur 9.png](assets/Figure9.png)
*Bild 9: Definitionen av besöks- och attribueringskorrigerad modellkonverteringsfaktor. (Observera att det här måttet är beroende av ditt målmått och din aktivitet. Den här måttdefinitionen kan alltså inte återanvändas i olika aktiviteter.)*

>[!IMPORTANT]
>
>Konverteringsgraden från A4T-panelen är inte länkad till konverteringshändelsen eller normaliseringsmåttet i tabellen. När du gör de ändringar som föreslås i den här självstudiekursen anpassas inte konverteringsgraden automatiskt till ändringarna. Om du ändrar något till en (eller båda) konverteringshändelseattribuering och normaliseringsmått måste du därför komma ihåg som ett sista steg för att även ändra konverteringsgraden, vilket visas ovan.

## Sammanfattning: Slutlig exempelarbetsyta för [!DNL Auto-Target] rapporter

Om du kombinerar alla steg ovan till en enda panel visar bilden nedan en fullständig vy av den rekommenderade rapporten för [!DNL Auto-Target] A4T-aktiviteter. Den här rapporten är densamma som den som används av Target maskininlärningsmodeller för att optimera målmätningen, och den innehåller alla nyanser och rekommendationer som diskuteras i den här självstudiekursen. Denna rapport är också närmast de beräkningsmetoder som används i traditionell Target-rapporteringsbaserad [!DNL Auto-Target] verksamhet.

![Figur10.png](assets/Figure10.png)
*Bild 10: Den sista A4T [!DNL Auto-Target] i Adobe Analytics Workspace, där alla justeringar av metriska definitioner som beskrivs i föregående avsnitt i det här dokumentet kombineras.*
