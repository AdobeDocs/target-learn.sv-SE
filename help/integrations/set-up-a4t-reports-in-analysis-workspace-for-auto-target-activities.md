---
title: Så här konfigurerar du A4T-rapporter i [!DNL Analysis Workspace] för [!DNL Auto-Target] aktiviteter
description: Hur konfigurerar jag A4T-rapporter i [!DNL Analysis Workspace]  för att få det förväntade resultatet när jag kör [!UICONTROL Auto-Target]-aktiviteter?
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=sv-SE#premium newtab=true" tooltip="Se vad som ingår i Target Premium."
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
thumbnail: null
kt: null
exl-id: 58006a25-851e-43c8-b103-f143f72ee58d
source-git-commit: 78e5b5f7fa8f4c1a08c06c6d2b0e1a5242cd464c
workflow-type: tm+mt
source-wordcount: '2430'
ht-degree: 0%

---

# Konfigurera A4T-rapporter i [!DNL Analysis Workspace] för [!DNL Auto-Target]-aktiviteter

>[!IMPORTANT]
>
>För [!UICONTROL Auto-Target]-aktiviteter måste du kontrollera rapporteringen i [!DNL Analytics Workspace] och manuellt skapa en A4T-panel.

Integrationen [!UICONTROL Analytics for Target] (A4T) för [!DNL Auto-Target]-aktiviteter använder HTML-algoritmerna ([!DNL Adobe Target] ensemble Machine Learning) för att välja den bästa upplevelsen för varje besökare utifrån deras profil, beteende och kontext, allt med ett [!DNL Adobe Analytics] målmått.

Även om det finns omfattande analysfunktioner i [!DNL Adobe Analytics] [!DNL Analysis Workspace] krävs några ändringar i standardpanelen **[!UICONTROL Analytics for Target]** för att [!DNL Auto-Target]-aktiviteter ska kunna tolkas korrekt, på grund av skillnader mellan experimentaktiviteter (manuell [!UICONTROL A/B Test] och [!UICONTROL Auto-Allocate]) och personaliseringsaktiviteter ([!UICONTROL [!UICONTROL Auto-Target]]).

I den här självstudiekursen går vi igenom de rekommenderade ändringarna för att analysera [!UICONTROL Auto-Target]-aktiviteter i [!DNL Analysis Workspace], som baseras på följande nyckelbegrepp:

* Dimensionen **[!UICONTROL Control vs Targeted]** kan användas för att skilja mellan [!UICONTROL Control]-upplevelser och de som hanteras av algoritmen [!UICONTROL Auto-Target] ensemble ML.
* Besök bör användas som normaliseringsmått vid visning av prestandadelningar på erfarenhetsnivå. Dessutom kan [Adobe Analytics standardberäkningsmetod omfatta besök där användaren inte ser aktivitetsinnehållet ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html?lang=sv-SE#metrics){target=_blank}, men detta standardbeteende kan ändras med ett segment med rätt omfång (se informationen nedan).
* Omfattad attribuering av besök-lookback, som också kallas &quot;besökslookback window&quot; (Besök-lookback-fönstret) för den föreskrivna attribueringsmodellen, används av [!DNL Adobe Target] ML-modellerna under deras utbildningsfaser, och samma (ej standard) attribueringsmodell bör användas när målmåttet bryts ned.

## Skapa A4T för panelen [!UICONTROL Auto-Target] i [!DNL Analysis Workspace]

Om du vill skapa en A4T för [!UICONTROL Auto-Target]-rapport börjar du med **[!UICONTROL Analytics for Target]**-panelen i [!DNL Analysis Workspace], som visas nedan, eller börjar med en friformstabell. Gör sedan följande val:

1. **[!UICONTROL Control Experience]**: Du kan välja vilken upplevelse som helst, men du kommer att åsidosätta det här alternativet senare. Observera att för [!UICONTROL Auto-Target]-aktiviteter är kontrollupplevelsen egentligen en kontrollstrategi, vilket antingen är till för a) Slumpmässigt fungerar bland alla upplevelser, eller b) En enda upplevelse (det här valet görs när aktiviteten skapas i [!DNL Adobe Target]). Även om du valde att (b), betecknade din [!UICONTROL Auto-Target]-aktivitet en specifik upplevelse som kontroll. Du bör fortfarande följa det tillvägagångssätt som beskrivs i den här självstudiekursen för att analysera A4T för [!UICONTROL Auto-Target] aktiviteter.
2. **[!UICONTROL Normalizing Metric]**: Välj [!UICONTROL Visits].
3. **[!UICONTROL Success Metrics]**: Även om du kan välja vilka mätvärden som ska rapporteras, bör du vanligtvis visa rapporter på samma mätvärden som valdes för optimering när aktiviteter skapades i [!DNL Target].

   ![[!UICONTROL Analytics for Target] panelinställningar för [!UICONTROL Auto-Target] aktiviteter.](assets/Figure1.png)

   *Figur 1: [!UICONTROL Analytics for Target] Panelinställningar för [!UICONTROL Auto-Target] aktiviteter.*

>[!TIP]
>
>Om du vill konfigurera [!UICONTROL Analytics for Target]-panelen för [!UICONTROL Auto-Target]-aktiviteter väljer du en kontrollupplevelse, väljer [!UICONTROL Visits] som normaliseringsmått och väljer samma målmått som valdes för optimering när [!DNL Target]-aktiviteten skapades.

## Använd dimensionen [!UICONTROL Control vs.Targeted] för att jämföra den [!DNL Target] ensemble ML-modellen med din kontroll

A4T-standardpanelen är utformad för klassiska (manuella) [!UICONTROL A/B Test]- eller [!UICONTROL Auto-Allocate]-aktiviteter där målet är att jämföra prestanda för enskilda upplevelser med kontrollupplevelsen. I [!UICONTROL Auto-Target]-aktiviteter bör dock den första orderjämförelsen vara mellan kontrollen *strategy* och målstrategin *strategy*. Med andra ord, fastställa lyften för den övergripande prestandan för den enemble ML-modellen [!UICONTROL Auto-Target] över kontrollstrategin.

Använd dimensionen **[!UICONTROL Control vs Targeted (Analytics for Target)]** om du vill utföra jämförelsen. Dra och släpp för att ersätta dimensionen **[!UICONTROL Target Experiences]** i A4T-standardrapporten.

Observera att den här ersättningen gör standardberäkningarna för [!UICONTROL Lift and Confidence] ogiltiga på A4T-panelen. För att undvika förvirring kan du ta bort dessa mått från standardpanelen och lämna följande rapport:

![[!UICONTROL Experiences by Activity Conversions]-panelen i [!DNL Analysis Workspace]](assets/Figure2.png)

*Bild 2: Den rekommenderade baslinjerapporten för [!DNL Auto-Target]-aktiviteter. Den här rapporten har konfigurerats för att jämföra riktad trafik (hanteras av den ensemble ML-modellen) med din kontrolltrafik.*

>[!NOTE]
>
>För närvarande är [!UICONTROL Lift and Confidence] siffror inte tillgängliga för [!UICONTROL Control vs Targeted] dimensioner för A4T-rapporter för [!UICONTROL Auto-Target]. Tills support har lagts till kan [!UICONTROL Lift and Confidence] beräknas manuellt genom att hämta [konfidensräknaren](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx?lang=sv-SE).

## Lägg till analysstatistik på erfarenhetsnivå

Om du vill få mer information om hur den ensemble ML-modellen fungerar kan du undersöka uppdelningar på erfarenhetsnivå för dimensionen **[!UICONTROL Control vs Targeted]**. I [!DNL Analysis Workspace] drar du dimensionen **[!UICONTROL Target Experiences]** till rapporten och delar sedan upp var och en av kontrolldimensionerna och de riktade dimensionerna separat.

![[!UICONTROL Experiences by Activity Conversions]-panelen i [!DNL Analysis Workspace]](assets/Figure3.png)

*Bild 3: Bryta ned den riktade dimensionen efter målupplevelser*

Här visas ett exempel på den resulterande rapporten.

![[!UICONTROL Experiences by Activity Conversions]-panelen i [!DNL Analysis Workspace]](assets/Figure4.png)

*Bild 4: En [!UICONTROL Auto-Target]-standardrapport med brytningar på erfarenhetsnivå. Observera att målmåttet kan vara annorlunda och att din kontrollstrategi kanske har en enda upplevelse.*

>[!TIP]
>
>I [!DNL Analysis Workspace] klickar du på kugghjulsikonen för att dölja procentsatserna i kolumnen [!UICONTROL Conversion Rate] för att behålla fokus på upplevelsekonverteringsgraden. Konverteringsgraden formateras sedan som decimaler, men tolkas som procenttal.

## Varför [!UICONTROL Visits] är rätt normaliseringsmått för [!UICONTROL Auto-Target]-aktiviteter

När du analyserar en [!UICONTROL Auto-Target]-aktivitet ska du alltid välja [!UICONTROL Visits] som standardmått för normalisering. [!UICONTROL Auto-Target]-personalisering väljer en upplevelse för en besökare en gång per besök (formellt, en gång per [!DNL Target]-session), vilket innebär att den upplevelse som visas för en besökare kan ändras vid varje enskilt besök. Om du använder [!UICONTROL Unique Visitors] som normaliseringsmått kan det faktum att en enskild användare kan få flera upplevelser (mellan olika besök) leda till förvirrande konverteringsgrader.

Ett enkelt exempel visar detta: tänk på ett scenario där två besökare anger en kampanj som bara har två upplevelser. Den första besökaren besöker två gånger. De tilldelas till Experience A vid det första besöket, men Experience B vid det andra besöket (eftersom deras profilstatus ändras vid det andra besöket). Efter det andra besöket konverterar besökaren genom att göra en beställning. Konverteringen tillskrivs den senast visade upplevelsen (upplevelse B). Den andra besökaren besöker också två gånger och visas Experience B båda gånger, men konverterar aldrig.

Låt oss jämföra rapporter på besökarnivå och besöksnivå:

| Upplevelse | Unika besökare | Besök | Konverteringar | Konverteringshastighet normaliserad av besökare | Besök-normaliserad konverteringsgrad |
| --- | --- | --- | --- | --- | --- |
| A | 1 | 1 | - | 0 % | 0 % |
| B | 2 | 3 | 1 | 50 % | 33,3 % |
| Summor | 2 | 4 | 1 | 50 % | 25 % |

*Tabell 1: Exempel på hur besökarnormaliserade rapporter och besöknormaliserade rapporter jämförs för ett scenario där beslut är snäva mot ett besök (och inte besökare, som med vanlig A/B-testning). De normaliserade värdena för besökare är förvirrande i det här scenariot.*

Som framgår av tabellen finns det en tydlig inkonsekvens i besökarnivånummer. Trots att det finns två unika besökare totalt är detta inte en summa unika besökare för varje upplevelse. Även om konverteringsgraden på besökarnivå inte nödvändigtvis är fel, så är konverteringsgraden på besöksnivå mer begriplig när man jämför enskilda upplevelser. Formeligen är analysenheten (&quot;besök&quot;) densamma som enheten för att fatta beslut, vilket innebär att man kan lägga till och jämföra analysdata på erfarenhetsnivå.

## Filter för faktiska besök i aktiviteten

Standardberäkningsmetoden [!DNL Adobe Analytics] för besök i en [!DNL Target]-aktivitet kan innehålla besök där användaren inte interagerade med [!DNL Target]-aktiviteten. Detta beror på hur [!DNL Target] aktivitetstilldelningar behålls i [!DNL Analytics]-besökarkontexten. Som en följd av detta kan antalet besök i aktiviteten [!DNL Target] ibland vara inflaterade, vilket resulterar i en minskning av konverteringsgraden.

Om du föredrar att rapportera besök där användaren faktiskt interagerade med aktiviteten [!UICONTROL Auto-Target] (antingen genom att gå in i aktiviteten, visa eller besöka aktiviteten, eller genom en konvertering) kan du:

1. Skapa ett specifikt segment som innehåller träffar från aktiviteten [!DNL Target] och sedan
1. Filtrera måttet [!UICONTROL Visits] med det här segmentet.

**Så här skapar du segmentet:**

1. Välj alternativet **[!UICONTROL Components > Create Segment]** i verktygsfältet [!DNL Analysis Workspace].
2. Ange **[!UICONTROL Title]** för ditt segment. I exemplet nedan heter segmentet [!DNL "Hit with specific Auto-Target activity"].
3. Dra dimensionen **[!UICONTROL Target Activities]** till segmentet **[!UICONTROL Definition]**.
4. Använd operatorn **[!UICONTROL equals]**.
5. Sök efter din specifika [!DNL Target]-aktivitet.
6. Klicka på kugghjulsikonen och välj sedan **[!UICONTROL Attribution model > Instance]** enligt bilden nedan.
7. Klicka på **[!UICONTROL Save]**.

![Segment i [!DNL Analysis Workspace]](assets/Figure5.png)

*Figur 5: Använd ett segment som det som visas här för att filtrera måttet [!UICONTROL Visits] i A4T-rapporten för [!UICONTROL Auto-Target]*

När segmentet har skapats använder du det för att filtrera måttet [!UICONTROL Visits], så måttet [!UICONTROL Visits] innehåller endast besök där användaren interagerade med aktiviteten [!DNL Target].

**Om du vill filtrera [!UICONTROL Visits] med det här segmentet:**

1. Dra det nyligen skapade segmentet från komponentverktygsfältet och hovra över basen för måttetiketten **[!UICONTROL Visits]** tills en blå **[!UICONTROL Filter by]**-prompt visas.
2. Släpp segmentet. Filtret används på det måttet.

Den sista panelen visas enligt följande:

![[!UICONTROL Experiences by Activity Conversions]-panelen i [!DNL Analysis Workspace]](assets/Figure6.png)

*Figur 6: Rapporteringspanelen med segmentet&quot;Träff med specifik aktivitet för automatisk målning&quot; tillämpat på måttet [!UICONTROL Visits]. Det här segmentet ser till att endast besök där en användare faktiskt interagerade med aktiviteten [!DNL Target] inkluderas i rapporten.*

## Se till att målvärdena och attribueringen är anpassade efter optimeringskriteriet

A4T-integreringen tillåter att [!UICONTROL Auto-Target] ML-modellen *tränas* med samma konverteringshändelsedata som [!DNL Adobe Analytics] använder för att *generera prestandarapporter*. Det finns dock vissa antaganden som måste användas för att tolka dessa data vid utbildning av ML-modellerna, som skiljer sig från de standardantaganden som gjordes under rapporteringsfasen i [!DNL Adobe Analytics].

Närmare bestämt använder [!DNL Adobe Target] ML-modellerna en besöksomfångsmodell för attribuering. Det innebär att ML-modellerna förutsätter att en konvertering måste ske vid samma besök som en visning av innehåll för aktiviteten för att konverteringen ska kunna&quot;tillskrivas&quot; det beslut som fattas av ML-modellen. Detta krävs för att [!DNL Target] ska kunna garantera att dess modeller tränas i rätt tid. [!DNL Target] kan inte vänta upp till 30 dagar på en konvertering (standardattribueringsfönstret för rapporter i [!DNL Adobe Analytics]) innan det inkluderas i utbildningsdata för dess modeller.

Skillnaden mellan attribueringen som används av modellerna [!DNL Target] (under utbildning) och standardattribueringen som används i frågedata (under rapportgenerering) kan således leda till avvikelser. Det kan till och med verka som om ML-modellerna fungerar dåligt, när frågan i själva verket är attribuering.

>[!TIP]
>
>Om ML-modellerna optimerar för ett mätvärde som tilldelas på ett annat sätt än de mätvärden som du visar i en rapport, kanske modellerna inte fungerar som förväntat. För att undvika detta bör du se till att målmåtten i din rapport använder samma metriska definition och attribuering som används av [!DNL Target] ML-modellerna.

Den exakta måttdefinitionen och attribueringsinställningarna beror på det [optimeringskriterium](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=sv-SE#supported){target=_blank} du angav när aktiviteten skapades.

### Måldefinierade konverteringar, eller [!DNL Analytics] mått med *Maximera måttvärde per besök*

När måttet är en [!DNL Target]-konvertering, eller ett [!DNL Analytics]-mått med **Maximera måttvärde per besök**, tillåter målmåttsdefinitionen att flera konverteringshändelser inträffar vid samma besök.

Följ de här stegen för att visa målmått som har samma attribueringsmetod som används av [!DNL Target] ML-modellerna:

1. Håll muspekaren över mållätarens kugghjulsikon:

   ![gearicon.png](assets/gearicon.png)

1. Bläddra till **[!UICONTROL Data settings]** från den resulterande menyn.
1. Välj **[!UICONTROL Use non-default  attribution model]** (om det inte redan är markerat).

   ![non-defaultattributionmodel.png](assets/non-defaultattributionmodel.png)

1. Klicka på **[!UICONTROL Edit]**.
1. Välj **[!UICONTROL Model]**: **[!UICONTROL Participation]** och **[!UICONTROL Lookback window]**: **[!UICONTROL Visit]**.

   ![ParticipationbyVisit.png](assets/ParticipationbyVisit.png)

1. Klicka på **[!UICONTROL Apply]**.

Med de här stegen ser du till att målmåttet i din rapport tilldelas till visningen av upplevelsen, om målmåtthändelsen inträffar *någon gång* (&quot;deltagande&quot;) vid samma besök som en upplevelse visades.

### [!DNL Analytics] mått med *unika konverteringsgrader för besök*

**Definiera besöket med positivt mätsegment**

I det scenario där du valde *Maximera konverteringsgraden för unikt besök* som optimeringskriterium, är den korrekta definitionen av konverteringsgraden den andel besök där mätvärdet är positivt. Detta kan uppnås genom att skapa en segmentfiltrering ned till besök med ett positivt värde för mätvärdet och sedan filtrera besöksmätningen.

1. Som tidigare väljer du alternativet **[!UICONTROL Components > Create Segment]** i verktygsfältet [!DNL Analysis Workspace].
2. Ange **[!UICONTROL Title]** för ditt segment.

   I exemplet nedan heter segmentet [!DNL "Visits with an order"].

3. Dra basmåttet som du använde i optimeringsmålet till segmentet.

   I exemplet nedan använder vi måttet **orders**, så att konverteringsgraden mäter andelen besök där en order registreras.

4. Välj **[!UICONTROL Include]** **Besök** längst upp till vänster i segmentdefinitionsbehållaren.
5. Använd operatorn **[!UICONTROL is greater than]** och ange värdet till 0.

   Om du anger värdet 0 innebär det att det här segmentet omfattar besök där ordermåttet är positivt.

6. Klicka på **[!UICONTROL Save]**.

![Figur7.png](assets/Figure7.png)

*Figur 7: Segmentdefinitionsfiltreringen till besök med en positiv ordning. Beroende på aktivitetens optimeringsmått måste du ersätta order med ett lämpligt mått*

**Använd detta för besök i aktivitetsfiltrerade mätvärden**

Det här segmentet kan nu användas för att filtrera besök med ett positivt antal order och där det var en träff för aktiviteten [!DNL Auto-Target]. Bearbetningen av ett mätvärde liknar den tidigare, och efter att det nya segmentet har tillämpats på det redan filtrerade besöksmätverket bör rapportpanelen se ut som i bild 8

![Figur8.png](assets/Figure8.png)

*Figur 8: Rapportpanelen med rätt konverteringsmått för unika besök: antalet besök där en träff från aktiviteten spelades in och där konverteringsmåttet (ordningarna i det här exemplet) inte var noll.*

## Slutligt steg: Skapa en konverteringsgrad som fångar magin ovan

Med ändringarna av [!UICONTROL Visit]- och målmåtten i de föregående avsnitten är den sista ändringen du bör göra i standardvärdet för A4T för rapportpanelen [!DNL Auto-Target] att skapa konverteringsgrader som har rätt förhållande - det korrigerade målmåttet - till ett lämpligt filtrerat besöksmått.

Gör detta genom att skapa en [!UICONTROL Calculated Metric] med följande steg:

1. Välj alternativet **[!UICONTROL Components > Create Metric]** i verktygsfältet [!DNL Analysis Workspace].
1. Ange en **[!UICONTROL Title]** för måttet. Exempel: &quot;Besökskorrigerad konverteringsgrad för aktivitet XXX.&quot;
1. Välj **[!UICONTROL Format]** = Procent och **[!UICONTROL Decimal Places]** = 2.
1. Dra det relevanta målmåttet för din aktivitet (till exempel [!UICONTROL Activity Conversions]) till definitionen och använd kugghjulsikonen på det här målmåttet för att justera attribueringsmodellen till (Deltagande|Besök), enligt beskrivningen ovan.
1. Välj **[!UICONTROL Add > Container]** i det övre högra hörnet av avsnittet **[!UICONTROL Definition]**.
1. Välj divisionsoperatorn ( max) mellan de två behållarna.
1. Dra det segment som du skapade tidigare - med namnet&quot;Träff med specifik [!UICONTROL Auto-Target] aktivitet&quot; - i den här självstudiekursen för den här specifika [!DNL Auto-Target]-aktiviteten.
1. Dra **[!UICONTROL Visits]**-måttet till segmentbehållaren.
1. Klicka på **[!UICONTROL Save]**.

>[!TIP]
>
> Du kan också skapa det här måttet med [funktionen för snabbberäknade mått](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=sv-SE).

Den fullständiga definitionen för beräknade mätvärden visas här.

![Figur9.png](assets/Figure9.png)

*Figur 7: Definitionen av besökskorrigerad och attribueringskorrigerad modellkonverteringsgrad. (Observera att det här måttet är beroende av ditt målmått och din aktivitet. Den här måttdefinitionen kan alltså inte återanvändas i olika aktiviteter.)*

>[!IMPORTANT]
>
>Frekvensmåttet [!UICONTROL Conversion] från A4T-panelen är inte länkat till konverteringshändelsen eller normaliseringsmåttet i tabellen. När du gör de ändringar som föreslås i den här självstudiekursen anpassas inte [!UICONTROL Conversion]-hastigheten automatiskt till ändringarna. Om du ändrar konverteringshändelseattributet eller normaliseringsmåttet (eller båda) måste du därför komma ihåg det som ett sista steg för att även ändra [!UICONTROL Conversion]-hastigheten, som visas ovan.

## Sammanfattning: Slutlig exempelpanel [!DNL Analysis Workspace] för [!UICONTROL Auto-Target]-rapporter

Om du kombinerar alla steg ovan till en enda panel visas i bilden nedan en fullständig vy över den rekommenderade rapporten för [!UICONTROL Auto-Target] A4T-aktiviteter. Den här rapporten är densamma som den som används av [!DNL Target] ML-modellerna för att optimera målmåttet. Rapporten innehåller alla nyanser och rekommendationer som diskuteras i den här självstudiekursen. Den här rapporten är också närmast de beräkningsmetoder som används i traditionella [!DNL Target]-rapportdrivna [!UICONTROL Auto-Target]-aktiviteter.

Klicka för att expandera bilden.

![Slutlig A4T-rapport i [!DNL Analysis Workspace]](assets/Figure10.png "A4T-rapport i Analysis Workspace"){width="600" zoomable="yes"}

*Figur 10: Den sista A4T [!UICONTROL Auto-Target] -rapporten i [!DNL Adobe Analytics] [!DNL Workspace] som kombinerar alla justeringar av måttdefinitioner som beskrivs i de föregående avsnitten i den här självstudien.*
