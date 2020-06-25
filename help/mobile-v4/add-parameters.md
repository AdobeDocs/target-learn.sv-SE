---
title: Lägg till parametrar i begäranden
description: I den här lektionen ska vi lägga till Adobe-livscykelvärden och anpassade parametrar till de Target-begäranden som lades till i den föregående lektionen. Dessa mått och parametrar kommer att användas för att skapa personaliserade målgrupper senare i självstudiekursen.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 0%

---


# Lägg till parametrar i begäranden

I den här lektionen ska vi lägga till Adobes livscykelvärden och anpassade parametrar till de [!DNL Target] förfrågningar som lades till i föregående lektion. Dessa mått och parametrar kommer att användas för att skapa personaliserade målgrupper senare i självstudiekursen.

## Utbildningsmål

När lektionen är klar kan du:

* Lägg till Adobes livscykelstatistik för mobila enheter
* Lägga till parametrar i en förhämtningsbegäran
* Lägga till parametrar till en aktiv plats
* Validera parametrarna för båda förfrågningarna

## Lägg till livscykelparametrar

Låt oss aktivera [Adobes mobilstatistik](https://docs.adobe.com/content/help/en/mobile-services/android/metrics.html). Detta lägger till parametrar i platsförfrågningar som innehåller omfattande information om användarens enhet och hur appen används. Vi bygger målgrupper i nästa lektion med hjälp av data som tillhandahålls i livscykelbegäran.

Om du vill aktivera livscykelmått öppnar du hemaktivitetskontrollen igen och lägger till `Config.collectLifecycleData(this);` i funktionen onResume():

![Begäran om livscykel](assets/lifecycle_code.jpg)

### Validera livscykelparametrar för förhämtningsbegäran

Kör emulatorn och använd Logcat för att validera livscykelparametrarna. Filtrera efter &quot;prefetch&quot; för att hitta prefetch-svaret och leta efter de nya parametrarna:
![Livscykelvalidering](assets/lifecycle_validation.jpg)

Även om vi bara har lagt `Config.collectLifecycleData()` till HomeActivity-kontrollen bör du också se livscykelvärdena som skickas med Target-begäran på TackYou-skärmen.

## Lägg till parametern at_property i förhämtningsbegäran

Egenskaper för Adobe Target definieras i gränssnittet och används för att [!DNL Target] skapa gränser för personalisering av appar och webbplatser. Parametern at_property identifierar den specifika egenskap där dina erbjudanden och aktiviteter finns tillgängliga och underhålls. Vi ska lägga till en egenskap till förhämtnings- och live-platsförfrågningarna.

>[!NOTE] Beroende på vilken licens du har kan du eventuellt se egenskapsalternativen i [!DNL Target] gränssnittet. Om du inte har de här alternativen, eller om du inte använder Egenskaper i ditt företag, går du vidare till nästa avsnitt i den här lektionen.

Du kan hämta at_property-värdet i [!DNL Target] gränssnittet under [!UICONTROL Setup] > [!UICONTROL Properties].  Håll markören över egenskapen, markera kodfragmentsikonen och kopiera `at_property` värdet:

![Kopiera till_egenskap](assets/at_property_interface.jpg)

Lägg till den som en parameter för varje plats i förhämtningsbegäran enligt följande:
![Lägg till parametern](assets/params_at_property.jpg)at_property Här är den uppdaterade koden för `targetPrefetchContent()` funktionen (kom ihåg att uppdatera _[!UICONTROL your at_property value goes here]_platshållartexten!):

```java
public void targetPrefetchContent() {
        List<TargetPrefetchObject> prefetchList = new ArrayList<>();

        Map<String, Object> params1;
        params1 = new HashMap<String, Object>();
        params1.put("at_property", "your at_property value goes here");

        prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, params1));
        prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, params1));
        Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
            @Override
            public void call(final Boolean status) {
                HomeActivity.this.runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        String cachingStatus = status ? "YES" : "NO";
                        System.out.println("Received Response from prefetch : " + cachingStatus);
                        engageMessage();
                        setUp();

                    }
                });
            }};
        Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
    }
```

### Kommentarer om parametrar

För framtida projekt kanske du vill implementera ytterligare parametrar. Metoden tillåter tre `createTargetPrefetchObject()` typer av parametrar: `locationParams`, `orderParams`och `productParams`. Mer [information om hur du lägger till de här parametrarna i förhämtningsbegäran](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-mob-target-prefetch-android.html)finns i dokumentationen.

Observera också att olika platsparametrar kan läggas till på varje plats i förhämtningsbegäran. Du kan t.ex. skapa en annan karta med namnet param2, lägga in en ny parameter och sedan ange param2 på en plats och param1 på den andra platsen. Här är ett exempel:

```java
prefetchList.add(Target.createTargetPrefetchObject(location1_name, params1);
prefetchList.add(Target.createTargetPrefetchObject(location2_name, params2);
```

## Validera parametern at_property i förhämtningsbegäran

Kör nu emulatorn och använd Logcat för att verifiera att at_property visas på förhämtningsbegäran och svar för båda platserna:
![Validera parametern at_property](assets/parameters_at_property_validation.jpg)

## Lägg till anpassade parametrar i Live-platsbegäran

Begäran om aktiv plats (wetravel_context_dest) lades till i föregående lektion så att vi kunde visa en relevant befordran på den sista bekräftelseskärmen i bokningsprocessen. Vi vill anpassa kampanjen utifrån användarens destination och för att göra det lägger vi till den som en parameter i begäran. Vi ska också lägga till en parameter för troppens ursprung och at_property-värdet.

Lägg till följande parametrar i funktionen targetLoadRequest() i kontrollenheten TackYouActivity:
![Lägg till parametrar i Live Location Request](assets/parameters_live_location.jpg)Här är den uppdaterade koden för funktionen targetLoadRequest() (se till att uppdatera platshållartexten&quot;add your at_property value here&quot;!):

```java
public void targetLoadRequest(final ArrayList<Recommandation> recommandations) {
    Map<String, Object> locationParams = new HashMap<>();
    locationParams.put("at_property","add your at_property value here");
    locationParams.put("locationSrc", (""+Utility.getInSharedPreference(ThankYouActivity.this,Constant.departure,"")));
    locationParams.put("locationDest", (""+Utility.getInSharedPreference(ThankYouActivity.this,Constant.destination,"")));

    Target.loadRequest(Constant.wetravel_context_dest, "", null, null, locationParams, new Target.TargetCallback<String>() {
        @Override
        public void call(final String response) {
        try {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    AppDialogs.dialogLoaderHide();
                    filterRecommendationBasedOnOffer(recommandations, response);
                    recommandationbAdapter.notifyDataSetChanged();
                }
            });
        } catch (Exception e) {
            e.printStackTrace();
        }
        }
    });
    Target.clearPrefetchCache();
}
```

### Validera de anpassade parametrarna i Live-platsbegäran

Kör emulatorn och öppna Logcat. Filtrera efter en av parametrarna för att verifiera att begäran innehåller de parametrar som krävs:
![Validera de anpassade parametrarna i Live-platsbegäran](assets/parameters_live_location_validation.jpg)

>[!NOTE] Begäranden och parametrar för orderbekräftelse: Även om de inte används i det här demoprojektet registreras orderinformationen vanligtvis i en verklig implementering så att orderdetaljer kan användas som mått/mått. [!DNL Target] I dokumentationen finns instruktioner om hur du [implementerar begäran om orderbekräftelse och parametrarna](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-target-methods.html).

>[!NOTE] Analytics för Target (A4T): Adobe Analytics kan konfigureras som rapportkälla för [!DNL Target]. På så sätt kan alla mått som samlas in av Target SDK visas i Adobe Analytics. Mer information finns i [A4T-översikten](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/a4t.html) .

Snyggt jobbat! Nu när parametrarna finns på plats är vi redo att använda dessa parametrar för att skapa målgrupper och erbjudanden i Adobe Target.

**[NÄSTA: &quot;Skapa publiker och erbjudanden&quot; >](create-audiences-and-offers.md)**
