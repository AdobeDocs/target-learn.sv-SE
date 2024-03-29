---
title: Konfigurera A4T-rapporter i [!DNL Analysis Workspace] for [!DNL Auto-Target] Verksamhet
description: Hur jag konfigurerar A4T-rapporter i [!DNL Analysis Workspace] för att få det förväntade resultatet när programmet körs [!UICONTROL Auto-Target] aktiviteter?
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html#premium newtab=true" tooltip="Se vad som ingår i Target Premium."
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
source-wordcount: '2480'
ht-degree: 0%

---

# Ställ in A4T-rapporter i [!DNL Analysis Workspace] for [!DNL Auto-Target] verksamhet

>[!IMPORTANT]
>
>För [!UICONTROL Auto-Target] aktiviteter, du måste kontrollera rapporteringen i [!DNL Analytics Workspace] och skapa en A4T-panel manuellt.

The [!UICONTROL Analytics for Target] (A4T)-integrering för [!DNL Auto-Target] aktiviteter använder [!DNL Adobe Target] HTML-algoritmer (Enble Machine Learning) för att välja den bästa upplevelsen för varje besökare utifrån deras profil, beteende och sammanhang, allt med hjälp av en [!DNL Adobe Analytics] målmått.

Även om det finns omfattande analysfunktioner i [!DNL Adobe Analytics] [!DNL Analysis Workspace], några ändringar av standardinställningen **[!UICONTROL Analytics for Target]** panel krävs för korrekt tolkning [!DNL Auto-Target] aktiviteter, på grund av skillnader mellan experimentella aktiviteter (manuella [!UICONTROL A/B Test] och [!UICONTROL Auto-Allocate]) och personalisering ([!UICONTROL [!UICONTROL Auto-Target]]).

I den här självstudiekursen går vi igenom de rekommenderade ändringarna för analys [!UICONTROL Auto-Target] verksamhet i [!DNL Analysis Workspace], som bygger på följande nyckelbegrepp:

* The **[!UICONTROL Control vs Targeted]** kan användas för att skilja mellan [!UICONTROL Control] upplevelser jämfört med dem som [!UICONTROL Auto-Target] ensemble ML-algoritm.
* Besök bör användas som normaliseringsmått vid visning av prestandadelningar på erfarenhetsnivå. Dessutom [Adobe Analytics standardberäkningsmetod kan omfatta besök där användaren inte ser aktivitetsinnehållet](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html#metrics){target=_blank}, men det här standardbeteendet kan ändras med ett segment med rätt omfång (se informationen nedan).
* Attribuering med omfånget Besök-Lookback, som också kallas &quot;Besök-Lookback&quot; på den förskrivna attribueringsmodellen, används av [!DNL Adobe Target] ML-modeller under deras utbildningsfaser, och samma (ej standard) attribueringsmodell bör användas vid uppdelning av målmåttet.

## Skapa A4T för [!UICONTROL Auto-Target] panel i [!DNL Analysis Workspace]

Skapa en A4T för [!UICONTROL Auto-Target] rapport, antingen börja med **[!UICONTROL Analytics for Target]** panel i [!DNL Analysis Workspace], som visas nedan, eller börjar med en frihandstabell. Gör sedan följande val:

1. **[!UICONTROL Control Experience]**: Du kan välja vilken upplevelse som helst, men du kommer att åsidosätta det här alternativet senare. Observera att för [!UICONTROL Auto-Target] kontrollupplevelsen är en kontrollstrategi, som antingen är till för att a) slumpmässigt fungera bland alla upplevelser, eller b) skapa en enda upplevelse (valet görs när aktiviteten skapas i [!DNL Adobe Target]). Även om du valde att välja (b) [!UICONTROL Auto-Target] aktivitet som anger en specifik upplevelse som kontroll. Du bör fortfarande följa det tillvägagångssätt som beskrivs i den här självstudiekursen för att analysera A4T för [!UICONTROL Auto-Target] verksamhet.
2. **[!UICONTROL Normalizing Metric]**: Välj [!UICONTROL Visits].
3. **[!UICONTROL Success Metrics]**: Även om du kan välja vilka mätvärden som ska rapporteras bör du vanligtvis visa rapporter på samma mätvärden som valdes för optimering när aktiviteter skapades i [!DNL Target].

   ![[!UICONTROL Analytics for Target] panelinställningar för [!UICONTROL Auto-Target] verksamhet.](assets/Figure1.png)

   *Bild 1: [!UICONTROL Analytics for Target] panelinställningar för [!UICONTROL Auto-Target] verksamhet.*

>[!TIP]
>
>För att konfigurera [!UICONTROL Analytics for Target] panel för [!UICONTROL Auto-Target] -aktiviteter, välj valfri kontrollupplevelse, välja [!UICONTROL Visits] som normaliseringsmått och välj samma målmått som valdes för optimering under [!DNL Target] skapa aktiviteter.

## Använd [!UICONTROL Control vs.Targeted] dimension för att jämföra [!DNL Target] enemble ML model to your control

Standardpanelen för A4T är utformad för klassisk (manuell) [!UICONTROL A/B Test] eller [!UICONTROL Auto-Allocate] aktiviteter där målet är att jämföra de enskilda upplevelsernas resultat med kontrollupplevelsen. I [!UICONTROL Auto-Target] verksamheten, men den första orderjämförelsen bör vara mellan kontrollen *strategi* och målgruppen *strategi*. Med andra ord, fastställa lyften för den totala prestandan hos [!UICONTROL Auto-Target] ensemble ML-modell över kontrollstrategin.

Använd kommandot **[!UICONTROL Control vs Targeted (Analytics for Target)]** dimension. Dra och släpp för att ersätta **[!UICONTROL Target Experiences]** -dimension i standardrapporten för A4T.

Observera att den här ersättningen gör standardinställningen ogiltig [!UICONTROL Lift and Confidence] beräkningar på A4T-panelen. För att undvika förvirring kan du ta bort dessa mått från standardpanelen och lämna följande rapport:

![[!UICONTROL Experiences by Activity Conversions] panel i [!DNL Analysis Workspace]](assets/Figure2.png)

*Bild 2: Rekommenderad baslinjerapport för [!DNL Auto-Target] verksamhet. Den här rapporten har konfigurerats för att jämföra riktad trafik (hanteras av den ensemble ML-modellen) med din kontrolltrafik.*

>[!NOTE]
>
>För närvarande [!UICONTROL Lift and Confidence] tal är inte tillgängliga för [!UICONTROL Control vs Targeted] dimensioner för A4T-rapporter för [!UICONTROL Auto-Target]. Tills support har lagts till, [!UICONTROL Lift and Confidence] kan beräknas manuellt genom att ladda ned [konfidensräknare](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx).

## Lägg till analysstatistik på erfarenhetsnivå

För att få ytterligare insikter om hur den ensemble ML-modellen fungerar kan du undersöka uppdelningar på erfarenhetsnivå i **[!UICONTROL Control vs Targeted]** dimension. I [!DNL Analysis Workspace], dra **[!UICONTROL Target Experiences]** i rapporten och sedan separat bryt ned alla kontroller och måldimensioner.

![[!UICONTROL Experiences by Activity Conversions] panel i [!DNL Analysis Workspace]](assets/Figure3.png)

*Bild 3: Dela upp den riktade dimensionen efter Target Experiences*

Här visas ett exempel på den resulterande rapporten.

![[!UICONTROL Experiences by Activity Conversions] panel i [!DNL Analysis Workspace]](assets/Figure4.png)

*Bild 4: En standard [!UICONTROL Auto-Target] rapportera med uppdelningar på erfarenhetsnivå. Observera att målmåtten kan vara olika, och att din kontrollstrategi kan ha en enda upplevelse.*

>[!TIP]
>
>I [!DNL Analysis Workspace]klickar du på kugghjulsikonen för att dölja procentsatserna i [!UICONTROL Conversion Rate] för att fokusera på upplevelsekonverteringsgraden. Konverteringsgraden formateras sedan som decimaler, men tolkas som procenttal.

## Varför &quot;[!UICONTROL Visits]&quot; är rätt normaliseringsmått för [!UICONTROL Auto-Target] verksamhet

När en [!UICONTROL Auto-Target] aktivitet, välj alltid [!UICONTROL Visits] som standardmått för normalisering. [!UICONTROL Auto-Target] personalisering väljer en upplevelse för en besökare en gång per besök (formellt, en gång per [!DNL Target] -session), vilket innebär att den upplevelse som visas för besökaren kan ändras vid varje enskilt besök. Om du använder [!UICONTROL Unique Visitors] som normaliseringsmått skulle det faktum att en enskild användare kan få flera upplevelser (mellan olika besök) leda till förvirrande konverteringsgrader.

Ett enkelt exempel visar detta: tänk på ett scenario där två besökare anger en kampanj som bara har två upplevelser. Den första besökaren besöker två gånger. De tilldelas till Experience A vid det första besöket, men Experience B vid det andra besöket (eftersom deras profilstatus ändras vid det andra besöket). Efter det andra besöket konverterar besökaren genom att göra en beställning. Konverteringen tillskrivs den senast visade upplevelsen (upplevelse B). Den andra besökaren besöker också två gånger och visas Experience B båda gånger, men konverterar aldrig.

Låt oss jämföra rapporter på besökarnivå och besöksnivå:

| Upplevelse | Unika besökare | Besök | Konverteringar | Konverteringshastighet normaliserad av besökare | Besök-normaliserad konverteringsgrad |
| --- | --- | --- | --- | --- | --- |
| A | 1 | 1 | - | 0% | 0% |
| B | 2 | 3 | 1 | 50% | 33.3% |
| Summor | 2 | 4 | 1 | 50% | 25% |

*Tabell 1: Exempel på jämförelse av besökarnormaliserade rapporter och besöknormaliserade rapporter för ett scenario där beslut är snäva mot ett besök (och inte besökare, som med vanlig A/B-testning). Besökarnormaliserade värden är förvirrande i det här scenariot.*

Som framgår av tabellen finns det en tydlig inkonsekvens i besökarnivånummer. Trots att det finns två unika besökare totalt är detta inte en summa unika besökare för varje upplevelse. Även om konverteringsgraden på besökarnivå inte nödvändigtvis är fel, så är konverteringsgraden på besöksnivå mer begriplig när man jämför enskilda upplevelser. Formeligen är analysenheten (&quot;besök&quot;) densamma som enheten för att fatta beslut, vilket innebär att man kan lägga till och jämföra analysdata på erfarenhetsnivå.

## Filter för faktiska besök i aktiviteten

The [!DNL Adobe Analytics] standardräkningsmetod för besök på en [!DNL Target] aktiviteten kan omfatta besök där användaren inte interagerade med [!DNL Target] aktivitet. Det här beror på vägen [!DNL Target] aktivitetstilldelningar sparas i [!DNL Analytics] besökskontext. Som en följd av detta har antalet besök på [!DNL Target] Ibland kan aktiviteten vara inflammatorisk, vilket leder till en sänkning av konverteringsgraden.

Om du föredrar att rapportera besök där användaren faktiskt interagerade med [!UICONTROL Auto-Target] aktivitet (antingen genom att delta i aktiviteten, en displayhändelse, ett besök eller en konvertering) kan du:

1. Skapa ett specifikt segment som innehåller träffar från [!DNL Target] verksamhet i fråga, och sedan
1. Filtrera [!UICONTROL Visits] med detta segment.

**Så här skapar du segmentet:**

1. Välj **[!UICONTROL Components > Create Segment]** i [!DNL Analysis Workspace] verktygsfält.
2. Ange en **[!UICONTROL Title]** för segmentet. I exemplet nedan namnges segmentet [!DNL "Hit with specific Auto-Target activity"].
3. Dra **[!UICONTROL Target Activities]** dimension till segmentet **[!UICONTROL Definition]** -avsnitt.
4. Använd **[!UICONTROL equals]** -operator.
5. Sök efter din specifika [!DNL Target] aktivitet.
6. Klicka på kugghjulsikonen och välj sedan **[!UICONTROL Attribution model > Instance]** som visas i figuren nedan.
7. Klicka på **[!UICONTROL Save]**.

![Segment i [!DNL Analysis Workspace]](assets/Figure5.png)

*Bild 5: Använd ett segment som det som visas här för att filtrera [!UICONTROL Visits] mätvärden i A4T för [!UICONTROL Auto-Target] rapport*

När segmentet har skapats använder du det för att filtrera [!UICONTROL Visits] så att [!UICONTROL Visits] mätvärdet inkluderar endast besök där användaren interagerade med [!DNL Target] aktivitet.

**Filtrera [!UICONTROL Visits] med detta segment:**

1. Dra det nyligen skapade segmentet från komponentverktygsfältet och för markören över baslinjen på **[!UICONTROL Visits]** måttetikett tills en blå **[!UICONTROL Filter by]** visas.
2. Släpp segmentet. Filtret används på det måttet.

Den sista panelen visas enligt följande:

![[!UICONTROL Experiences by Activity Conversions] panel i [!DNL Analysis Workspace]](assets/Figure6.png)

*Bild 6: Rapporteringspanelen med segmentet&quot;Träff med specifik aktivitet&quot; tillämpat på [!UICONTROL Visits] mätvärden. Detta segment säkerställer att endast de besök där en användare faktiskt interagerade med [!DNL Target] rapporten innehåller de berörda verksamheterna.*

## Se till att målvärdena och attribueringen är anpassade efter optimeringskriteriet

A4T-integreringen tillåter [!UICONTROL Auto-Target] ML-modell som ska *utbildad* använda samma konverteringshändelsedata som [!DNL Adobe Analytics] använder till *generera resultatrapporter*. Det finns dock vissa antaganden som måste användas för att tolka dessa data när man utbilda ML-modellerna, som skiljer sig från de standardantaganden som gjorts under rapporteringsfasen i [!DNL Adobe Analytics].

I synnerhet [!DNL Adobe Target] ML-modeller använder en besöksomfångsmodell. Det innebär att ML-modellerna förutsätter att en konvertering måste ske vid samma besök som en visning av innehåll för aktiviteten för att konverteringen ska kunna&quot;tillskrivas&quot; det beslut som fattas av ML-modellen. Detta krävs för [!DNL Target] säkerställa att dess modeller får lämplig utbildning, [!DNL Target] kan inte vänta i upp till 30 dagar på en konvertering (standardattribueringsfönstret för rapporter i [!DNL Adobe Analytics]) innan den ingår i kursdata för sina modeller.

Skillnaden mellan den attribuering som används av [!DNL Target] modeller (under utbildning) jämfört med standardattribuering som används för att fråga efter data (under rapportgenerering) kan leda till avvikelser. Det kan till och med verka som om ML-modellerna fungerar dåligt, när frågan i själva verket är attribuering.

>[!TIP]
>
>Om ML-modellerna optimerar för ett mätvärde som tilldelas på ett annat sätt än de mätvärden som du visar i en rapport, kanske modellerna inte fungerar som förväntat. För att undvika detta bör du se till att målmåtten i rapporten använder samma metriska definition och attribuering som används av [!DNL Target] ML-modeller.

Exakt måttdefinition och attribueringsinställningar beror på [optimeringskriterium](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank} du angav när aktiviteten skapades.

### Måldefinierade konverteringar, eller [!DNL Analytics] med *Maximera måttvärde per besök*

När måttet är en [!DNL Target] konvertering, eller [!DNL Analytics] med **Maximera måttvärde per besök** kan målmåttsdefinitionen göra att flera konverteringshändelser inträffar vid samma besök.

Så här visar du målmått som har samma attribueringsmetod som används av [!DNL Target] ML-modeller, följ dessa steg:

1. Håll muspekaren över mållätarens kugghjulsikon:

   ![gearicon.png](assets/gearicon.png)

1. Bläddra till den resulterande menyn **[!UICONTROL Data settings]**.
1. Välj **[!UICONTROL Use non-default  attribution model]** (om det inte redan är markerat).

   ![non-defaultattributionmodel.png](assets/non-defaultattributionmodel.png)

1. Klicka på **[!UICONTROL Edit]**.
1. Välj **[!UICONTROL Model]**: **[!UICONTROL Participation]** och **[!UICONTROL Lookback window]**: **[!UICONTROL Visit]**.

   ![ParticipationbyVisit.png](assets/ParticipationbyVisit.png)

1. Klicka på **[!UICONTROL Apply]**.

Med dessa steg ser du till att målmåttet i din rapport tilldelas till visningen av upplevelsen, om målmåtthändelsen inträffar *när* (&quot;deltagande&quot;) i samma besök som en upplevelse visades.

### [!DNL Analytics] med *Unika konverteringshastigheter för besök*

**Definiera besöket med ett positivt mätsegment**

I scenariot där du valde *Maximera konverteringsgraden för unika besök* som optimeringskriterier är den korrekta definitionen av konverteringsgraden den andel besök där mätvärdet är positivt. Detta kan uppnås genom att skapa en segmentfiltrering ned till besök med ett positivt värde för mätvärdet och sedan filtrera besöksmätningen.

1. Som tidigare väljer du **[!UICONTROL Components > Create Segment]** i [!DNL Analysis Workspace] verktygsfält.
2. Ange en **[!UICONTROL Title]** för segmentet.

   I exemplet nedan namnges segmentet [!DNL "Visits with an order"].

3. Dra basmåttet som du använde i optimeringsmålet till segmentet.

   I exemplet nedan använder vi **order** mätvärden, så att konverteringsgraden mäter andelen besök där en order registreras.

4. Välj längst upp till vänster i segmentdefinitionsbehållaren **[!UICONTROL Include]** **Besök**.
5. Använd **[!UICONTROL is greater than]** och ange värdet till 0.

   Om du anger värdet 0 innebär det att det här segmentet omfattar besök där ordermåttet är positivt.

6. Klicka på **[!UICONTROL Save]**.

![Figur7.png](assets/Figure7.png)

*Bild 7: Segmentdefinitionsfiltrering till besök med en positiv ordning. Beroende på aktivitetens optimeringsmått måste du ersätta order med ett lämpligt mätvärde*

**Använd detta för besök i aktivitetsfiltrerade mätvärden**

Det här segmentet kan nu användas för att filtrera besök med ett positivt antal order och där det var en träff för [!DNL Auto-Target] aktivitet. Bearbetningen av ett mätvärde liknar den tidigare, och efter att det nya segmentet har tillämpats på det redan filtrerade besöksmätverket bör rapportpanelen se ut som i bild 8

![Figur8.png](assets/Figure8.png)

*Bild 8: Rapportpanelen med rätt konverteringsmått för unika besök: antalet besök där en träff från aktiviteten registrerades och där konverteringsmåttet (order i det här exemplet) inte var noll.*

## Slutligt steg: Skapa en konverteringsgrad som fångar magin ovan

Med ändringarna i [!UICONTROL Visit] och målmåtten i föregående avsnitt, den sista ändringen du bör göra i standardvärdet för A4T för [!DNL Auto-Target] ska man skapa konverteringsgrader som har rätt proportion - det korrigerade målmåttet - till ett lämpligt filtrerat besöksmått.

Gör detta genom att skapa en [!UICONTROL Calculated Metric] med följande steg:

1. Välj **[!UICONTROL Components > Create Metric]** i [!DNL Analysis Workspace] verktygsfält.
1. Ange en **[!UICONTROL Title]** för dina mätvärden. Exempel: &quot;Besökskorrigerad konverteringsgrad för aktivitet XXX.&quot;
1. Välj **[!UICONTROL Format]** = Procent och **[!UICONTROL Decimal Places]** = 2.
1. Dra relevanta målmått för din aktivitet (till exempel [!UICONTROL Activity Conversions]) till definitionen och använd kugghjulsikonen på det här målmåttet för att justera attribueringsmodellen till (Deltagande|Besök), enligt beskrivningen ovan.
1. Välj **[!UICONTROL Add > Container]** från det övre högra hörnet i **[!UICONTROL Definition]** -avsnitt.
1. Välj divisionsoperatorn ( max) mellan de två behållarna.
1. Dra det segment du skapade tidigare - med namnet&quot;Hit with specific [!UICONTROL Auto-Target] aktiviteten&quot; i den här självstudiekursen för [!DNL Auto-Target] aktivitet.
1. Dra **[!UICONTROL Visits]** mätvärden in i segmentbehållaren.
1. Klicka på **[!UICONTROL Save]**.

>[!TIP]
>
> Du kan också skapa det här måttet med [snabb beräknad mätfunktionalitet](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html).

Den fullständiga definitionen för beräknade mätvärden visas här.

![Figur 9.png](assets/Figure9.png)

*Figur 7: Definitionen av besökskorrigerad och attribueringskorrigerad modellkonverteringsgrad. (Observera att det här måttet är beroende av ditt målmått och din aktivitet. Den här måttdefinitionen kan alltså inte återanvändas i olika aktiviteter.)*

>[!IMPORTANT]
>
>The [!UICONTROL Conversion] tariffmåttet från A4T-panelen är inte länkat till konverteringshändelsen eller till det normaliserande måttet i tabellen. När du gör de ändringar som föreslås i den här självstudien [!UICONTROL Conversion] tariffen inte automatiskt anpassar sig till ändringarna. Om du gör ändringen av konverteringshändelseattributet eller normaliseringsmåttet (eller båda) måste du därför komma ihåg som ett sista steg för att även ändra [!UICONTROL Conversion] som visas ovan.

## Sammanfattning: Slutligt exempel [!DNL Analysis Workspace] panel för [!UICONTROL Auto-Target] rapporter

Om du kombinerar alla steg ovan till en enda panel visar bilden nedan en fullständig vy av den rekommenderade rapporten för [!UICONTROL Auto-Target] A4T-aktiviteter. Den här rapporten är densamma som den som används av [!DNL Target] ML-modeller för att optimera målmåtten. Rapporten innehåller alla nyanser och rekommendationer som diskuteras i den här självstudiekursen. Denna rapport ligger också närmast de beräkningsmetoder som använts i traditionell [!DNL Target]-rapportstyrd [!UICONTROL Auto-Target] verksamhet.

Klicka för att expandera bilden.

![Final A4T report in [!DNL Analysis Workspace]](assets/Figure10.png "A4T-rapport i Analysis Workspace"){width="600" zoomable="yes"}

*Bild 10: Den sista A4T-bilden [!UICONTROL Auto-Target] rapportera i [!DNL Adobe Analytics] [!DNL Workspace], som kombinerar alla justeringar av metriska definitioner som beskrivs i de föregående avsnitten i den här självstudien.*
