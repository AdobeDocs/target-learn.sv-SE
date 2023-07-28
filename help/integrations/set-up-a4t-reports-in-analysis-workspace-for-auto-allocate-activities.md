---
title: Konfigurera A4T-rapporter i [!DNL Analysis Workspace] for [!UICONTROL Auto-Allocate] Verksamhet
description: Hur jag konfigurerar A4T-rapporter i [!DNL Analysis Workspace] för att få det förväntade resultatet när programmet körs [!UICONTROL Auto-Allocate] verksamhet.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 99d49995ec7e3dd502a149376693e2770f3e2a9d
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 0%

---

# Konfigurera A4T-rapporter i [!DNL Analysis Workspace] for [!DNL Auto-Allocate] verksamhet

An [!DNL Auto-Allocate] aktivitet identifierar en vinnare bland två eller fler upplevelser och omfördelar automatiskt trafiken till vinnaren medan testet fortsätter att köras och lära sig. The [!UICONTROL Analytics for Target] (A4T)-integrering för [!UICONTROL Auto-Allocate] kan du se dina rapportdata i [!DNL Adobe Analytics]och du kan även optimera för anpassade händelser eller mätvärden som definieras i [!DNL Analytics].

Även om det finns omfattande analysfunktioner i [!DNL Adobe Analytics] [!DNL Analysis Workspace], några ändringar av standardinställningen **[!UICONTROL Analytics for Target]** kan behövas för att tolka [!DNL Auto-Allocate] verksamhet, på grund av nyanser i [kriterier för optimeringsmått](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

I den här självstudiekursen går vi igenom de rekommenderade ändringarna för analys [!DNL Auto-Allocate] verksamhet i [!DNL Analysis Workspace]. De viktigaste begreppen är:

* [!UICONTROL Visitors] ska alltid användas som normaliseringsmått i [!DNL Auto-Allocate] verksamhet.
* När måttet är en [!DNL Adobe Analytics] mätvärden varierar konverteringsgraden, beroende på vilken typ av optimeringskriterier som har definierats under aktivitetsinställningarna.
   * Täljaren för konverteringsgraden&quot;maximera konverteringsgraden för besökare&quot; är ett antal unika besökare *med ett positivt värde för mätvärdet*.
   * Den här metoden kräver inget ytterligare segment för att matcha konverteringsgraden som visas i [!DNL Target] Gränssnitt.
* Täljaren för konverteringsgraden&quot;maximize metric value per visitor&quot; är det reguljära måttvärdet i [!DNL Adobe Analytics]. Detta mått anges som standard i [!DNL Analytics for Target] panel i [!DNL Analysis Workspace].
   * Detta innebär: maximerar antalet besökare som konverterar (&quot;antal en gång per besökare&quot;).
   * Den här metoden kräver att ytterligare ett segment skapas i rapporteringen för att matcha konverteringsgraden som visas i [!DNL Target] Gränssnitt.
* När optimeringsmåttet är en [!DNL Target] definierat konverteringsmått, standardvärde **[!UICONTROL Analytics for Target]** panel i [!DNL Analysis Workspace] handtag som konfigurerar panelen.
* För alla [!UICONTROL Auto-Allocate] aktiviteter skapade före [!DNL Target Standard/Premium] 23.3.1-utgåvan (30 mars 2023) [!DNL Analytics Workspace] och [!DNL Target] visa samma värde för [!UICONTROL Confidence].

  För alla [!UICONTROL Auto-Allocate] verksamhet som skapats efter den 30 mars 2023, värdena för konfidensintervall som visas i [!DNL Analysis Workspace] speglar inte [mer konservativ statistik som används av [!UICONTROL Auto-Allocate]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html#section_98388996F0584E15BF3A99C57EEB7629){target=_blank} om dessa aktiviteter *båda* av följande villkor:

   * [!DNL Analytics] som rapportkälla (A4T)
   * [!DNL Analytics] optimeringsmått

  Konfidensmåtten ska tas bort från A4T-panelen. Referera i stället till dessa värden i [!DNL Target] rapportering.

## Skapa A4T för [!DNL Auto-Allocate] panel i [!DNL Analysis Workspace]

Skapa en A4T-panel för en [!DNL Auto-Allocate] rapporten börjar med **[!UICONTROL Analytics for Target]** panel i [!DNL Analysis Workspace], vilket visas nedan. Gör sedan följande val:

1. **[!UICONTROL Control Experience]**: Du kan välja vilken upplevelse du vill.
1. **[!UICONTROL Normalizing Metric]**: Välj besökare (Besökare inkluderas som standard i A4T-panelen). [!DNL Auto-Allocate] normaliserar alltid konverteringsgraden för unika besökare.
1. **[!UICONTROL Success Metrics]**: Välj samma mått som du använde när du skapade aktiviteten. Om det här var en [!DNL Target] definierade konverteringsmått, välj **Aktivitetskonvertering**. I annat fall väljer du [!DNL Adobe Analytics] mätvärden som du använde.

![[!UICONTROL Analytics for Target] panelinställningar för [!DNL Auto-Allocate] verksamhet.](assets/AAFigure1.png)

*Bild 1: [!UICONTROL Analytics for Target] panelinställningar för [!DNL Auto-Allocate] verksamhet.*

Du kan också komma fram till en färdig **[!UICONTROL Analytics for Target]** om du klickar på länken från rapportskärmen i [!DNL Adobe Target].

## [!DNL Target] [!UICONTROL Conversion] mätvärden eller [!DNL Analytics] mätvärden med optimeringskriterier för&quot;Maximera mätvärde per besökare&quot;

När målmåttet är antingen:

* Mått för målkonvertering
* Analysmått med optimeringskriteriet&quot;Maximera mätvärde per besökare&quot;

A4T-standardpanelen konfigurerar automatiskt rapporten.

Ett exempel på den här panelen visas för [!UICONTROL Revenue] mått, där Maximera måttvärde per besökare valdes som optimeringsvillkor när aktiviteten skapades. Som tidigare nämnts [!DNL Auto-Allocate] använder mer försiktiga konfidensberäkningar jämfört med dem som används i **[!UICONTROL Analytics for Target]** -panelen. Adobe rekommenderar att du tar bort konfidensmåttet från A4T-panelen samt relaterade värden för nedre och övre lyft. I stället refererar du till konfidensvärdena i [!DNL Target] rapportering.

>[!NOTE]
>
>Konfidensvärden i A4T-rapportering är mindre försiktiga än [!DNL Target] och kan i förtid visa en vinnare för en [!UICONTROL Auto-Allocate] aktivitet.


![[!UICONTROL Analytics for Target - AutoAllocate Report] panel](assets/AAFigure2.png)

*Bild 2: Rekommenderad rapport för [!DNL Auto-Allocate] aktiviteter med [!DNL Analytics] mätkriterierna&quot;Maximera måttvärde per besökare&quot;. För dessa typer av mätvärden [!DNL Target] definierade konverteringsvärden, standardvärden **[!UICONTROL Analytics for Target]**panel i [!DNL Analysis Workspace] kan användas.*

## [!DNL Analytics] mätvärden med optimeringskriterier för maximera unika besökare

Optimeringskriteriet&quot;Maximera unika besökare med konverteringsgrad&quot; avser antalet besökare för vilka måttvärdet är positivt. Om konverteringsgraden till exempel definieras som intäkt, skulle villkoret&quot;Maximera unika besökare med konverteringsgrad&quot; vara optimerat utifrån antalet unika besökare för vilka intäkterna var större än 0. Detta kriterium skulle med andra ord maximera antalet besökare som genererar intäkter, snarare än värdet av intäkterna.

>[!NOTE]
>
>Den konverteringsgrad som det hänvisas till här kan avse åtgärder som ligger utanför ordningarna, t.ex. klick, visningar osv. I dessa fall skulle kriteriet ändå vara att maximera antalet besökare som klickar eller visar sidan.

The [!DNL Analytics for Target] panel i [!DNL Analysis Workspace] måste ändras om detta optimeringskriterium används med ett [!DNL Adobe Analytics] mätvärden.

När det här optimeringskriteriet används är framgångsmåttet antalet unika besökare för vilka konverteringsmåttet var positivt. För att det här värdet ska kunna visas måste därför ett nytt segment skapas som filtrerar efter träffar med ett positivt värde för måttet.

Skapa det här segmentet på följande sätt:

1. Välj **[!UICONTROL Components]** > **[!UICONTROL Create Segment]** i [!DNL Analysis Workspace] verktygsfält.
1. Dra mätvärdena som användes när aktiviteten skapades från den vänstra panelen till **[!UICONTROL Definition]** segmentets ruta.
1. Välj värden för måttet som **större än** ett numeriskt värde på 0.
1. Från **[!UICONTROL Include]** nedrullningsbar meny, välja **[!UICONTROL Visitors]**.
1. Ge segmentet rätt namn.

Ett exempel på hur segmentet skapas visas i figuren nedan där framgångsmåttet är [!UICONTROL Visitors With Positive Revenue].

![[!UICONTROL Visitors with Positive Revenue] segment i [!DNL Analysis Workspace]](assets/AAFigure3.png)

*Bild 3: Skapa segment för [!DNL Adobe Analytics] mätvärden med optimeringskriterier lika med[!UICONTROL Maximize Unique Visitor Conversion Rate].&quot; I det här exemplet är måttet [!UICONTROL Revenue]och optimeringsmålet är att maximera antalet besökare med positiva intäkter.*

När rätt segment har skapats kan du ändra standardvärdet  **[!UICONTROL Analytics for Target]** panel i [!DNL Analysis Workspace] om du vill visa värdena för optimeringskriteriet. Detta uppnås genom att göra följande:

1. Lägg till en sekund **Unika besökare** mätvärden vid sidan av befintliga [!UICONTROL Visitors] metrisk kolumn.
2. Dra det nyskapade segmentet under den första kolumnen för att skapa en panel som liknar bild 4. Lägg märke till skillnaden i kolumnernas värden: antalet unika besökare med positiva intäkter bör vara en bråkdel av det totala antalet unika besökare som tilldelas varje upplevelse (se nedan).

   ![Figur 4.png](assets/AAFigure4.png)

   *Bild 4: Filtrering [!UICONTROL Unique Visitors] av det nya segmentet*

3. En konverteringsgrad kan [snabbt beräknad](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html) genom att markera både den första och den andra kolumnen, högerklicka, markera **[!UICONTROL Create Metric from selection]** > **[!UICONTROL Divide]**.

   Standardkonverteringsgraden bör tas bort och ersättas med det nya beräknade måttet, vilket visas i bilden nedan. Du kan behöva redigera det nya beräknade måttet för att kunna visas som en **[!UICONTROL Format]** > **[!UICONTROL Percent]** upp till två decimaler, som visas.

   ![Figur 5.png](assets/AAFigure5.png)

   *Bild 5: Den sista [!UICONTROL Auto-Allocate] panel som visar konverteringsgraden för ett binärformat intäktskonverteringsmått*

## Sammanfattning

Stegen i den här självstudiekursen visar hur du konfigurerar [!DNL Analysis Workspace] att visa [!UICONTROL Auto-Allocate] rapportdata.

Sammanfattning:

* När måttet är en [!DNL Target] definierad konverteringsmetod eller [!DNL Adobe Analytics] Mått med optimeringskriteriet&quot;Maximera mätvärde per besökare&quot; ska användas. Den standardpanel för arbetsytan som konfigurerats med besökare som normaliseringsmått ska användas.
* När måttet är en [!DNL Adobe Analytics] mätvärden med optimeringskriteriet&quot;Maximera konverteringsgraden för unika besökare&quot;, måste du fastställa andelen besökare med positivt mätvärde jämfört med det totala antalet besökare. Detta görs genom att skapa ett motsvarande segment som filtrerar [!UICONTROL Unique Visitor] på det måttet.
