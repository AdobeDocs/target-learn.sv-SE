---
title: Konfigurera A4T-rapporter i [!DNL Analysis Workspace] för [!UICONTROL Auto-Allocate]-aktiviteter
description: Hur konfigurerar jag [!UICONTROL Analytics for Target] (A4T)-rapporter i  [!DNL Adobe] [!DNL Analysis Workspace] när [!UICONTROL Auto-Allocate]-aktiviteter körs.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 190a67832f378e15090115420bfaf8a4af4b9cb9
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 0%

---

# Konfigurera A4T-rapporter i [!DNL Analysis Workspace] för [!DNL Auto-Allocate]-aktiviteter

En [[!UICONTROL Auto-Allocate]-aktivitet](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=sv-SE){target=_blank} i [!DNL Adobe Target] identifierar en vinnare bland två eller fler upplevelser och omfördelar automatiskt besökstrafiken till vinnaren medan testet fortsätter att köras och lära sig. Integreringen [!UICONTROL Analytics for Target] (A4T) för [!UICONTROL Auto-Allocate] gör att du kan visa rapportdata i [!DNL Adobe Analytics], och du kan optimera för anpassade händelser eller mått som definieras i [!DNL Analytics].

Även om det finns omfattande analysfunktioner i [!DNL Adobe Analytics] [!DNL Analysis Workspace] kan det behövas några ändringar av standardpanelen [!UICONTROL Analytics for Target] för att [!UICONTROL Auto-Allocate]-aktiviteter ska kunna tolkas korrekt. Dessa ändringar behövs på grund av nyanserna i [kriterierna för optimeringsmått](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=sv-SE#supported){target=_blank}.

Varje typ av optimeringsmått kräver en annan rapportkonfiguration i A4T, enligt följande:

* Använda ett [!DNL Analytics]-mått

   * [!UICONTROL Maximize metric value per visitor]
   * [!UICONTROL Maximize unique visitor conversion rate]

* Använda ett [!DNL Target]-definierat konverteringsmått

Den här självstudiekursen omfattar övergripande A4T-vägledning och kriteriespecifika rapportkonfigurationssteg.

## Analysstatistik med optimeringskriterier för [!UICONTROL Maximize Metric Value Per Visitor]

**Definition**: (övergripande måttvärde) / (# av besökare)

Gör följande ändringar i A4T-rapporten om du vill konfigurera rapporten:

| Ändringar krävs | [!DNL Target]-utlöst rapport | A4T-panelrapport |
| --- | --- | --- |
| Maximera måttvärde för ett [!DNL Analytics]-mått | <ul><li>Ta bort [!UICONTROL Confidence] mått.</li><li>Ta bort [!UICONTROL Lift (Low)] och [!UICONTROL Lift (High)]. Behåll [!UICONTROL Lift (Med)].</li><li>Avmarkera procentpresentationen från kolumnen [!UICONTROL Conversion Rate] för att undvika förvirring. Se [Generell vägledning för A4T](#guidance) nedan.</li><li>Byt namn på [!UICONTROL Conversion]-tariffen till &quot;Mått/besökare&quot;.</li></ul> | <ul><li>Ta bort [!UICONTROL Confidence] mått.</li><li>Ta bort [!UICONTROL Lift (Low)] och [!UICONTROL Lift (High)] Behåll [!UICONTROL Lift (Med)].</li><li>Avmarkera procentpresentationen från kolumnen [!UICONTROL Conversion Rate] för att undvika förvirring. Se [Generell vägledning för A4T](#guidance) nedan.</li><li>Byt namn på [!UICONTROL Conversion]-tariffen till &quot;Mått/besökare&quot;.</li><li>Se till att datum- och tidsintervallen justeras mot de värden som du ser i rapporten [!DNL Target]. Se [Generell vägledning för A4T](#guidance) nedan.</li></ul> |

![Maximera måttvärde för intäkter](/help/integrations/assets/maximize-metric-value-revenue.png)

## [!DNL Analytics]-mått med [!UICONTROL Unique Visitor Conversion Rate]-optimeringsvillkor

**Definition**: (# av unika besökare med ett positivt värde för måttet) / (totalt antal unika besökare)

Exempel: Anta att optimeringsmåttet är [!UICONTROL Revenue]. Det finns fem unika besökare i aktiviteten och tre av dessa unika besökare gör ett köp. I det här exemplet är det här värdet = (3 besökare för vilka [!UICONTROL Revenue] är positiv) / (5 totalt unika besökare) = 0,6 = 60 %.

>[!NOTE]
>
>Den konverteringsgrad som det hänvisas till här kan avse åtgärder som ligger utanför ordningarna, t.ex. klick, visningar osv. I dessa fall skulle kriteriet ändå vara att maximera antalet besökare som klickar eller visar sidan.

Gör följande ändringar i A4T-rapporten om du vill konfigurera rapporten:

| Ändringar krävs | Målutlöst rapport | A4T-panelrapport |
| --- | --- | --- |
| Maximera konverteringar för ett [!DNL Analytics]-mått | <ul><li>Ta bort [!UICONTROL Confidence] mått.</li><li>Ta bort alla tre [!UICONTROL Lift]-måtten.</li><li>Avmarkera procentpresentationen från kolumnen [!UICONTROL Conversion Rate] för att undvika förvirring. Se [Generell vägledning för A4T](#guidance) nedan.</li></ul> | <ul><li>Ta bort [!UICONTROL Confidence] mått.</li><li>Ta bort alla tre [!UICONTROL Lift]-måtten.</li><li>Skapa ett segment för att filtrera besökare med ett positivt mätvärde som visade aktiviteten som analyserades. Se [Skapa ett segment](#segment) nedan.</li><li>Ersätt det automatiskt ifyllda [!UICONTROL Conversion Rate]-måttet så att det är indelningen mellan [!UICONTROL Unique visitors] med ett positivt mätvärde och unika besökare. Se [Uppdatera konverteringsgraden ](#update-conversion-metric) nedan.</li><li>Avmarkera procentpresentationen från kolumnen [!UICONTROL Conversion Rate] för att undvika förvirring. Se [Generell vägledning för A4T](#guidance) nedan.</li><li>Se till att datum- och tidsintervallen justeras mot de värden som du ser i rapporten [!DNL Target]. Se [Generell vägledning för A4T](#guidance) nedan.</li></ul> |

### Standardrapport för A4T-panelen - ytterligare vägledning

Följande avsnitt innehåller mer information om ytterligare vägledning när du ställer in standardrapporten för A4T-panelen.

#### Skapa ett segment {#segment}

1. Klicka på tecknet **&quot;+&quot;** bredvid **[!UICONTROL Segments]** i den vänstra listen.

   ![Plustecken bredvid segment i den vänstra listen.](/help/integrations/assets/plus-sign.png)

1. Ge segmentet rubriken&quot;Besökare med positivt mätvärde&quot;.
1. Under **[!UICONTROL Definition]**, bredvid **[!UICONTROL Include]**, väljer du **[!UICONTROL Visitor]**.
1. Under **[!UICONTROL Definition]** väljer du optimeringsmåttet i din aktivitet.

   I det här exemplet antar du [!UICONTROL Revenue] som optimeringsmått.

1. Välj operatorn [!UICONTROL is greater than] och ange sedan 0.

   Inställningarna filtrerar för alla besökare med ett positivt mätvärde.

1. Klicka på **[!UICONTROL Save]**.

   ![Positivt måttvärde](/help/integrations/assets/positive-metric-value.png)

1. Lägg till det nya segmentet med namnet&quot;Besökare med positivt mätvärde&quot; på A4T-panelen.
1. Dra och släpp måttet [!UICONTROL Unique Visitors] i samma kolumn som &quot;Besökare med positivt mätvärde&quot;.

   Den här konfigurationen skapar ett segment med alla unika besökare för vilka måttvärdet är positivt. I det här exemplet är alla unika besökare vars intäkter var större än noll.

#### Uppdatera måttet [!UICONTROL Conversion Rate] {#update-conversion-metric}

1. Om du inte redan har gjort det, tar du bort den befintliga kolumnen [!UICONTROL Conversion Rate] från panelen enligt anvisningarna nedan.
1. Lägg till ett mått genom att klicka på plustecknet (+) bredvid avsnittet **[!UICONTROL Metrics]** i den vänstra listen.
1. Namnge måttet &quot;Konverteringsgrad&quot; och definiera det som &quot;([!UICONTROL Unique Visitors] med positivt mätvärde)&quot; dividerat med &quot;Unika besökare&quot;, så som visas nedan.

   Lägg till det nya segmentet (stegen som definieras nedan) i&quot;Besökare med positivt mätvärde&quot;, divisionsoperatorn,&quot;Unika besökare&quot;-måttet i täljaren och&quot;Unika besökare&quot; som nämnare.

   ![Konverteringsfrekvens i A4T-panelen.](/help/integrations/assets/conversion-rate.png)

1. Klicka på **[!UICONTROL Save]**.

1. Dra och släpp det nya mätvärdet för konverteringsgrad i den befintliga panelen.
1. Klicka på kugghjulsikonen och avmarkera kryssrutan **[!UICONTROL Percent]** eftersom det här värdet kan orsaka förvirring.

   Den korrekta konfigurationen av rapporten bör ge ett resultat som liknar följande bild:

   ![Unik besökskonverteringsfrekvens i A4T-panelrapport](/help/integrations/assets/a4t-aa-maximize-metric-value-revenue.png)

## [!DNL Target]-definierad konverteringsgrad

Gör följande ändringar i A4T-rapporten om du vill konfigurera rapporten:

| Ändringar krävs | Målutlöst rapport | A4T-panelrapport |
| --- | --- | --- |
| [!DNL Analytics] rapporterar med [!DNL Target] konverteringsmått | <ul><li>Ta bort [!UICONTROL Confidence] mått.</li><li>Ta bort [!UICONTROL Lift (Low)] och [!UICONTROL Lift (High)]. Håll kvar (Med).</li><li>Avmarkera procentpresentationen från kolumnen [!UICONTROL Conversion Rate] för att undvika förvirring. Se [Generell vägledning för A4T](#guidance) nedan.</li></ul> | <ul><li>Ta bort [!UICONTROL Confidence] mått.</li><li>Ta bort [!UICONTROL Lift (Low)] och [!UICONTROL Lift (High)]. Behåll [!UICONTROL Lift (Med)].</li><li>Avmarkera procentpresentationen från kolumnen [!UICONTROL Conversion Rate] för att undvika förvirring. Se [Generell vägledning för A4T](#guidance) nedan.</li><li>Se till att datum- och tidsintervallen justeras mot de värden som du ser i rapporten [!DNL Target]. Se [Generell vägledning för A4T](#guidance) nedan.</li></ul> |

Den korrekta konfigurationen av rapporten bör ge ett resultat som liknar följande bild:

![Aktivitetskonverteringar](/help/integrations/assets/optimized-table.png)

## Generell vägledning för A4T {#guidance}

Du kan navigera till en fördefinierad [!UICONTROL Analytics for Target]-panel genom att klicka på länken från rapportskärmen i [!UICONTROL Target] (detta hänvisas senare till i den här guiden som den [!DNL Target]-utlösta rapporten). Du kan också skapa A4T-panelen i [!DNL Analytics] (mer information senare i det här avsnittet).

I följande avsnitt anges vilka konfigurationer som krävs, beroende på vilken av dessa metoder du väljer. Följande steg fungerar dock som en allmän vägledning för A4T:

* Ta bort konfidensmåtten från A4T-panelen oavsett hur panelen skapas (båda beskrivs nedan). Referera i stället dessa värden i [!DNL Target]-rapportering. Dessutom kan aktivitetsvinnare identifieras i [!DNL Target]-rapporter. Information om identifiering av aktivitetsvinnare finns i avsnittet [Identifiera aktivitetsvinnaren](#winner) nedan.
&#x200B;>>
* För att undvika missförstånd avmarkerar du presentationen [!UICONTROL Percent] av måttet [!UICONTROL Conversion Rate]. Se [Dölj procentandelen i kolumnen [!UICONTROL Conversion Rate] nedan](#hide-percentage).
&#x200B;>>
* Om du skapar en A4T-panel måste du se till att datum- och tidsintervallen matchar dem i din [!DNL Target]-rapport. Se [Justera datum och tid på A4T-panelen](#aligning-date-and-time) nedan.

### Dölj procentandelen från kolumnen [!UICONTROL Conversion Rate] {#hide-percentage}

1. Klicka på **kugghjulsikonen** bredvid rubriken för kolumnen [!UICONTROL Conversion Rate].

   ![Kugghjulsikonen i kolumnen Konverteringsgrad](/help/integrations/assets/coversion-rate-gear-icon.png)

   I dialogrutan [!UICONTROL Column]-inställningar visas:

   ![Dialogrutan Kolumninställningar](/help/integrations/assets/column-settings-dialog-box.png){width="200"}

1. Avmarkera kryssrutan **[!UICONTROL Percent]**.

   A4T-panelen innehåller nu inga procentsatser som [!UICONTROL Conversion Rate] och matchar [!DNL Target], vilket visas nedan:

   ![Kolumnen Konverteringsgrad visar inga procentandelar](/help/integrations/assets/no-percentages.png)

### Justera datum och tid på A4T-panelen {#aligning-date-and-time}

1. Under varje panel kontrollerar du det datumintervall som panelen refererar till för att se till att datumintervallet matchar intervallet för rapporten [!DNL Target].

   ![Datumintervall i A4T-panelen](/help/integrations/assets/date-range.png)

1. I [!DNL Analytics] ställer du in tidsintervallet till 12:00am - 11:59pm.

### Identifiera aktivitetsvinnaren {#winner}

[!DNL Auto-Allocate] aktivitetsvinnare väljs när det finns en vinnande konverteringsgrad med konfidensvärden som är större än eller lika med 95 %. Dessa värden bör refereras i [!DNL Target]-rapporterna, eftersom konfidensberäkningar avspeglar de mer konservativa metoderna som [!DNL Target] rekommenderar för [!UICONTROL Auto-Allocate]-aktiviteter. Se [Statistiska garantier för automatisk allokering](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/determine-winner.html?lang=sv-SE#section_7AF3B93E90BA4B80BC9FC4783B6A389C){target=_blank} i *[!UICONTROL Adobe Target Business Practitioner Guide]*.

>[!NOTE]
>
>Märken &quot;Ingen vinnare än&quot; och &quot;vinnare&quot; är inte tillgängliga på A4T-panelen i [!DNL Analysis Workspace]. Vinnarmärket &quot;star&quot; som visas i [!DNL Target] rapporter för [!UICONTROL Auto-Allocate]-aktiviteter ska också ignoreras. Se [Automatisk allokering](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=sv-SE#aa){target=_blank} i *Stöd för Automatisk allokering och Automatisk målaktiviteter* i *[!UICONTROL Adobe Target Business Practitioner Guide]*.

### Skapa A4T för panelen [!UICONTROL Auto-Allocate] i [!DNL Analysis Workspace]

1. Om du vill skapa en A4T-panel för en [!UICONTROL Auto-Allocate]-aktivitetsrapport börjar du med [!UICONTROL Analytics for Target]-panelen i [!DNL Analysis Workspace] enligt nedan.

   ![Analyser för mål - rapport om automatisk allokering](/help/integrations/assets/a4t-auto-allocate-report.png)

1. Gör följande val:

   * **[!UICONTROL Control Experience]**: Välj en upplevelse.
   * **[!UICONTROL Normalizing Metric]**: Välj **[!UICONTROL Visitors]** (ingår som standard i A4T-panelen). [!UICONTROL Auto-Allocate] normaliserar alltid konverteringsgraden för unika besökare.
   * **Resultatmått**: Välj samma (optimering) mått som du använde när aktiviteten skapades. Om detta var ett [!DNL Target]-definierat konverteringsmått väljer du **[!UICONTROL Activity Conversion]**. Annars väljer du det [!DNL Adobe Analytics]-mått som du använde.









