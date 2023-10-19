---
title: Konfigurera A4T-rapporter i [!DNL Analysis Workspace] for [!UICONTROL Auto-Allocate] Verksamhet
description: Hur konfigurerar jag [!UICONTROL Analytics for Target] (A4T) rapporter i [!DNL Adobe] [!DNL Analysis Workspace] vid körning [!UICONTROL Auto-Allocate] verksamhet.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: b22d51d7d231d67af179622755fb4f7ef83474a8
workflow-type: tm+mt
source-wordcount: '1450'
ht-degree: 0%

---

# Konfigurera A4T-rapporter i [!DNL Analysis Workspace] for [!DNL Auto-Allocate] verksamhet

An [!UICONTROL Auto-Allocate] aktivitet i [!DNL Adobe Target] identifierar en vinnare bland två eller flera upplevelser och omfördelar automatiskt besökstrafiken till vinnaren medan testet fortsätter att köras och lära sig. The [!UICONTROL Analytics for Target] (A4T)-integrering för [!UICONTROL Auto-Allocate] kan du visa rapportdata i [!DNL Adobe Analytics]och du kan optimera för anpassade händelser eller mätvärden som definieras i [!DNL Analytics].

Även om det finns omfattande analysfunktioner i [!DNL Adobe Analytics] [!DNL Analysis Workspace], några ändringar av standardinställningen [!UICONTROL Analytics for Target] kan behövas för att tolka [!UICONTROL Auto-Allocate] verksamhet. Dessa ändringar behövs på grund av nyanserna i [kriterier för optimeringsmått](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

Varje typ av optimeringsmått kräver en annan rapportkonfiguration i A4T, enligt följande:

* Använda [!DNL Analytics] mått

   * [!UICONTROL Maximize metric value per visitor]
   * [!UICONTROL Maximize unique visitor conversion rate]

* Använda [!DNL Target]-definierad konverteringsmetod

Den här självstudiekursen omfattar övergripande A4T-vägledning och kriteriespecifika rapportkonfigurationssteg.

## Analysstatistik med &quot;[!UICONTROL Maximize Metric Value Per Visitor]&quot; optimeringskriterier

**Definition**: (Totalt måttvärde) / (# av besökare)

Gör följande ändringar i A4T-rapporten om du vill konfigurera rapporten:

| Ändringar krävs | [!DNL Target]-utlöst rapport | A4T-panelrapport |
| --- | --- | --- |
| Maximera måttvärdet för [!DNL Analytics] mått | <ul><li>[!UICONTROL Confidence] mätvärden ska tas bort.</li><li>[!UICONTROL Lift (Low)] och [!UICONTROL Lift (High)] tas bort.</li><li>Avmarkera procentpresentationen i dialogrutan [!UICONTROL Conversion Rate] för att undvika förvirring. Mer information finns i [Generell vägledning](#guidance) nedan.</li><li>Konverteringsgradsmåttet ska bytas till &quot;Mått/besökare&quot;.</li></ul> | <ul><li>[!UICONTROL Confidence] mätvärden ska tas bort.</li><li>[!UICONTROL Lift (Low)] och [!UICONTROL Lift (High)] tas bort.</li><li>Avmarkera procentpresentationen i dialogrutan [!UICONTROL Conversion Rate] för att undvika förvirring. Mer information finns i [Generell vägledning](#guidance) nedan.</li><li>Konverteringsgradsmåttet ska bytas till &quot;Mått/besökare&quot;.</li><li>Se till att datum- och tidsintervallen justeras mot de värden du ser i dialogrutan [!DNL Target] rapport. Mer information finns i [Generell vägledning](#guidance) nedan.</li></ul> |

![Maximera mätvärdet för intäkter](/help/integrations/assets/maximize-metric-value-revenue.png)

## [!DNL Analytics] med &quot;[!UICONTROL Unique Visitor Conversion Rate]&quot; optimeringskriterier

**Definition**: (# av unika besökare med ett positivt värde för måttet) / (totalt antal unika besökare)

Exempel: Anta att optimeringsmåttet är [!UICONTROL Revenue]. Det finns fem unika besökare i aktiviteten och tre av dessa unika besökare gör ett köp. I det här exemplet = (3 besökare för vilka [!UICONTROL Revenue] är positivt) / (totalt 5 unika besökare) = 0,6 = 60 %.

>[!NOTE]
>
>Den konverteringsgrad som det hänvisas till här kan avse åtgärder som ligger utanför ordningarna, t.ex. klick, visningar osv. I dessa fall skulle kriteriet ändå vara att maximera antalet besökare som klickar eller visar sidan.

Gör följande ändringar i A4T-rapporten om du vill konfigurera rapporten:

| Ändringar krävs | Målutlöst rapport | A4T-panelrapport |
| --- | --- | --- |
| Maximera konverteringarna för en [!DNL Analytics] mått | <ul><li>[!UICONTROL Confidence] mätvärden ska tas bort.</li><li>Alla [!UICONTROL Lift] mätvärden ska tas bort.</li><li>Avmarkera procentpresentationen i dialogrutan [!UICONTROL Conversion Rate] för att undvika förvirring. (Mer information finns i [Generell vägledning](#guidance) nedan.</li></ul> | <ul><li>[!UICONTROL Confidence] mätvärden ska tas bort.</li><li>Alla [!UICONTROL Lift] mätvärden ska tas bort.</li><li>Skapa ett segment för att filtrera besökare med ett positivt mätvärde som visade den analyserade aktiviteten. Mer information finns i [Skapa ett segment](#segment) nedan.</li><li>Ersätt den automatiskt ifyllda [!UICONTROL Conversion Rate] så att det är indelningen mellan [!UICONTROL Unique visitors] med ett positivt mätvärde och unika besökare. Mer information finns i [Uppdatera konverteringsgraden](#update-conversion-metric) nedan.</li><li>Avmarkera procentpresentationen i dialogrutan [!UICONTROL Conversion Rate] för att undvika förvirring. Mer information finns i [Generell vägledning](#guidance) nedan.</li><li>Se till att datum- och tidsintervallen justeras mot de värden du ser i dialogrutan [!DNL Target] rapport. Mer information finns i [Generell vägledning](#guidance) nedan.</li></ul> |

### Standardrapport för A4T-panelen - ytterligare vägledning

Följande avsnitt innehåller mer information om ytterligare vägledning när du ställer in standardrapporten för A4T-panelen.

#### Skapa ett segment {#segment}

1. Klicka på **&quot;+&quot;-tecken** nästa **[!UICONTROL Segments]** till vänster.

   ![Plustecken bredvid segment i den vänstra listen.](/help/integrations/assets/plus-sign.png)

1. Ge segmentet rubriken&quot;Besökare med positivt mätvärde&quot;.
1. Under **[!UICONTROL Definition]**, bredvid **[!UICONTROL Include]**, markera **[!UICONTROL Visitor]**.
1. Under **[!UICONTROL Definition]** väljer du optimeringsmåttet i din aktivitet.

   I det här exemplet antar du [!UICONTROL Revenue] som optimeringsmått.

1. Välj &quot;[!UICONTROL is greater than]&quot; anger du sedan &quot;0&quot;.

   Inställningarna filtrerar för alla besökare med ett positivt mätvärde.

1. Klicka på **[!UICONTROL Save]**.

   ![Positivt mätvärde](/help/integrations/assets/positive-metric-value.png)

1. Lägg till det nya segmentet med namnet&quot;Besökare med positivt mätvärde&quot; på A4T-panelen.
1. Dra och släpp [!UICONTROL Unique Visitors] i samma kolumn som &quot;Visitors with Positive Metric Value&quot;.

   Den här konfigurationen skapar ett segment med alla unika besökare för vilka måttvärdet är positivt. I det här exemplet är alla unika besökare vars intäkter var större än noll.

#### Uppdatera [!UICONTROL Conversion Rate] mått {#update-conversion-metric}

1. Om du inte redan har gjort det tar du bort den befintliga [!UICONTROL Conversion Rate] från panelen enligt nedan.
1. Lägg till ett mått genom att klicka på plustecknet (+) bredvid **[!UICONTROL Metrics]** till vänster.
1. Namnge mätvärdet &quot;Conversion Rate&quot; och definiera det som &quot;([!UICONTROL Unique Visitors] med positivt mätvärde)&quot; dividerat med &quot;Unika besökare&quot;, vilket visas nedan.

   Lägg till det nya segmentet (stegen som definieras nedan) i&quot;Besökare med positivt mätvärde&quot;, divisionsoperatorn,&quot;Unika besökare&quot;-måttet i täljaren och&quot;Unika besökare&quot; som nämnare.

   ![Konverteringsgrad i A4T-panelen.](/help/integrations/assets/conversion-rate.png)

1. Klicka på **[!UICONTROL Save]**.

1. Dra och släpp det nya måttet &quot;Konverteringsgrad&quot; i den befintliga panelen.
1. Klicka på kugghjulsikonen och avmarkera **[!UICONTROL Percent]** eftersom det här värdet kan orsaka förvirring.

   Den korrekta konfigurationen av rapporten bör ge ett resultat som liknar följande bild:

   ![Unik besökskonverteringsfrekvens i A4T-panelrapport](/help/integrations/assets/a4t-aa-maximize-metric-value-revenue.png)

## [!DNL Target]-definierad konverteringsgrad

Gör följande ändringar i A4T-rapporten om du vill konfigurera rapporten:

| Ändringar krävs | Målutlöst rapport | A4T-panelrapport |
| --- | --- | --- |
| [!DNL Analytics] rapportera med [!DNL Target] konverteringsmått | <ul><li>[!UICONTROL Confidence] mätvärden ska tas bort.</li><li>[!UICONTROL Lift (Low)] och [!UICONTROL Lift (High)] tas bort.</li><li>Avmarkera procentpresentationen i dialogrutan [!UICONTROL Conversion Rate] för att undvika förvirring. Mer information finns i [Generell vägledning](#guidance) nedan.</li></ul> | <ul><li>[!UICONTROL Confidence] mätvärden ska tas bort.</li><li>[!UICONTROL Lift (Low)] och [!UICONTROL Lift (High)] tas bort.</li><li>Avmarkera procentpresentationen i dialogrutan [!UICONTROL Conversion Rate] för att undvika förvirring. Mer information finns i [Generell vägledning](#guidance) nedan.</li><li>Se till att datum- och tidsintervallen justeras mot de värden du ser i dialogrutan [!DNL Target] rapport. Mer information finns i [Generell vägledning](#guidance) nedan.</li></ul> |

Den korrekta konfigurationen av rapporten bör ge ett resultat som liknar följande bild:

![Aktivitetskonverteringar](/help/integrations/assets/optimized-table.png)

## Samlat riktlinjer för [!UICONTROL Analytics for Target] (A4T) {#guidance}

Du kan navigera till en färdig [!UICONTROL Analytics for Target] genom att klicka på länken från rapportskärmen i [!UICONTROL Adobe Target] (detta hänvisas senare till i denna handbok som[!DNL Target]-triggered report&quot;). Du kan även skapa A4T-panelen i [!DNL Analytics] (information senare i det här avsnittet).

I följande avsnitt anges vilka konfigurationer som krävs, beroende på vilken av dessa metoder du väljer. Följande steg fungerar dock som en allmän vägledning:

* Konfidensmåtten ska tas bort från A4T-panelen oavsett hur panelen skapas (båda beskrivs nedan). Referera i stället till dessa värden i [!DNL Target] rapportering. Dessutom kan aktivitetsvinnare identifieras i [!DNL Target] rapportering. Information om identifiering av aktivitetsvinnare finns i [Identifiera aktivitetsvinnaren](#winner) nedan.
>>
* För att undvika förvirring avmarkerar du &quot;[!UICONTROL Percent]&quot; presentation av [!UICONTROL Conversion Rate] mätvärden. Mer information finns i [Dölj procentandelen i [!UICONTROL Conversion Rate] kolumn](#hide-percentage) nedan.
>>
* Om du skapar en A4T-panel måste du se till att datum- och tidsintervallen matchar dem i [!DNL Target] rapport. Mer information finns i [Justera datum och tid på A4T-panelen](#aligning-date-and-time) nedan.

### Dölj procentandelen i [!UICONTROL Conversion Rate] kolumn {#hide-percentage}

1. Klicka på **växel** -ikonen bredvid titeln på [!UICONTROL Conversion Rate] kolumn.

   ![Kugghjulsikonen i kolumnen Konverteringsfrekvens](/help/integrations/assets/coversion-rate-gear-icon.png)

   The [!UICONTROL Column] visas i dialogrutan Inställningar:

   ![Dialogrutan Kolumninställningar](/help/integrations/assets/column-settings-dialog-box.png){width="200"}

1. Avmarkera **[!UICONTROL Percent]** kryssrutan.

   A4T-panelen innehåller nu inga procentsatser som konverteringsgrad och matchningar [!DNL Target], enligt nedan:

   ![Kolumnen Konverteringsgrad visar inga procentandelar](/help/integrations/assets/no-percentages.png)

### Justera datum och tid på A4T-panelen {#aligning-date-and-time}

1. Kontrollera datumintervallet som panelen refererar till för att se till att datumintervallet matchar intervallet för [!DNL Target] rapport.

   ![Datumintervall i A4T-panelen](/help/integrations/assets/date-range.png)

1. I [!DNL Analytics], ställer in tidsintervallet till 12.00-11.59.

### Identifiera aktivitetsvinnaren {#winner}

[!DNL Auto-Allocate] vinnarna väljs när det finns en vinnande konverteringsgrad med konfidensvärden som är större än eller lika med 95 %. Dessa värden ska refereras i [!DNL Target] rapporter, eftersom konfidensberäkningar avspeglar de mer konservativa metoderna [!DNL Target] rekommenderar [!UICONTROL Auto-Allocate] verksamhet. Mer information finns i [Statistiska garantier för automatisk fördelning](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/determine-winner.html#section_7AF3B93E90BA4B80BC9FC4783B6A389C){target=_blank} i *[!UICONTROL Adobe Target Business Practitioner Guide]*.

>[!NOTE]
>
Märken &quot;Ingen vinnare än&quot; och &quot;vinnare&quot; finns inte tillgängliga på A4T-panelen i [!DNL Analysis Workspace]. Vinnaren av märket &quot;stjärna&quot; visas också i [!DNL Target] rapporter för [!UICONTROL Auto-Allocate] aktiviteter ska ignoreras. Mer information finns i [Automatisk allokering](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#aa){target=_blank} in *A4T-stöd för Automatisk allokering och Automatiskt mål-aktiviteter* i *[!UICONTROL Adobe Target Business Practitioner Guide]*.

### Skapa A4T för [!UICONTROL Auto-Allocate] panel i [!DNL Analysis Workspace]

1. Skapa en A4T-panel för en [!UICONTROL Auto-Allocate] aktivitetsrapport, börja med [!UICONTROL Analytics for Target] panel i [!DNL Analysis Workspace], vilket visas nedan.

   ![Analyser för Target - rapporten Automatisk allokering](/help/integrations/assets/a4t-auto-allocate-report.png)

1. Gör följande val:

   * **[!UICONTROL Control Experience]**: Välj en upplevelse.
   * **[!UICONTROL Normalizing Metric]**: Välj **[!UICONTROL Visitors]** (ingår som standard i A4T-panelen). [!UICONTROL Auto-Allocate] normaliserar alltid konverteringsgraden för unika besökare.
   * **Success Metrics**: Välj samma (optimeringsmätning) mått som du använde när du skapade aktiviteten. Om det här var en [!DNL Target]-definierade konverteringsmått, välj **[!UICONTROL Activity Conversion]**. I annat fall väljer du [!DNL Adobe Analytics] mätvärden som du använde.









