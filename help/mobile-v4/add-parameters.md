---
title: Lägg till parametrar i begäranden
description: I den här lektionen ska vi lägga till Adobe livscykelvärden och anpassade parametrar i Target-begäranden som lades till i den föregående lektionen. Dessa mått och parametrar kommer att användas för att skapa personaliserade målgrupper senare i självstudiekursen.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 0250e55f-a233-4060-84e1-86d1f88a6106
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---

# Lägg till parametrar i begäranden

I den här lektionen ska vi lägga till livscykelvärden och anpassade parametrar för Adobe i [!DNL Target]-begäranden som lades till i den föregående lektionen. Dessa mått och parametrar kommer att användas för att skapa personaliserade målgrupper senare i självstudiekursen.

## Utbildningsmål

När lektionen är klar kan du:

* Lägg till livscykelstatistik för Adobe mobila livscykel
* Lägga till parametrar i en förhämtningsbegäran
* Lägga till parametrar till en aktiv plats
* Validera parametrarna för båda förfrågningarna

## Lägg till livscykelparametrar

Låt oss aktivera [Adobe mobil livscykelstatistik](https://experienceleague.adobe.com/docs/mobile-services/android/metrics.html?lang=sv-SE). Detta lägger till parametrar i platsförfrågningar som innehåller omfattande information om användarens enhet och hur appen används. Vi bygger målgrupper i nästa lektion med hjälp av data som tillhandahålls i livscykelbegäran.

Om du vill aktivera livscykelmått öppnar du HomeActivity-kontrollen igen och lägger till `Config.collectLifecycleData(this);` i onResume()-funktionen:

![Livscykelbegäran](assets/lifecycle_code.jpg)

### Validera livscykelparametrar för förhämtningsbegäran

Kör emulatorn och använd Logcat för att validera livscykelparametrarna. Filtrera efter &quot;prefetch&quot; för att hitta prefetch-svaret och leta efter de nya parametrarna:
![Livscykelvalidering](assets/lifecycle_validation.jpg)

Även om vi bara har lagt till `Config.collectLifecycleData()` i HomeActivity-styrenheten bör du också se livscykelvärdena som skickas med Target-begäran på TackYou-skärmen.

## Lägg till parametern at_property i förhämtningsbegäran

Adobe Target-egenskaper definieras i [!DNL Target]-gränssnittet och används för att skapa gränser för personalisering av appar och webbplatser. Parametern at_property identifierar den specifika egenskap där dina erbjudanden och aktiviteter finns tillgängliga och underhålls. Vi ska lägga till en egenskap till förhämtnings- och direktplatsförfrågningarna.

>[!NOTE]
>
>Beroende på din licens kan du eventuellt se egenskapsalternativen i gränssnittet [!DNL Target]. Om du inte har de här alternativen, eller om du inte använder Egenskaper i ditt företag, går du vidare till nästa avsnitt i den här lektionen.

Du kan hämta at_property-värdet i [!DNL Target]-gränssnittet under [!UICONTROL Setup] > [!UICONTROL Properties].  Håll markören över egenskapen, markera ikonen för kodfragment och kopiera värdet `at_property`:

![Kopiera vid_egenskap](assets/at_property_interface.jpg)

Lägg till den som en parameter för varje plats i förhämtningsbegäran enligt följande:
![Lägg till parametern at_property](assets/params_at_property.jpg)
Här är den uppdaterade koden för funktionen `targetPrefetchContent()` (kom ihåg att uppdatera platshållartexten för _[!UICONTROL your at_property value goes here]_!):

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

För framtida projekt kanske du vill implementera ytterligare parametrar. Metoden `createTargetPrefetchObject()` tillåter tre typer av parametrar: `locationParams`, `orderParams` och `productParams`. I dokumentationen finns [mer information om hur du lägger till de här parametrarna i förhämtningsbegäran](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html?lang=sv-SE).

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
![Lägg till parametrar i Live-platsbegäran](assets/parameters_live_location.jpg)
Här är den uppdaterade koden för funktionen targetLoadRequest() (se till att uppdatera platshållartexten&quot;add your at_property value here&quot;!):

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
![Verifiera anpassade parametrar i Live-platsbegäran](assets/parameters_live_location_validation.jpg)

>[!NOTE]
>
>Begäranden och parametrar för orderbekräftelse: Även om de inte används i det här demoprojektet registreras orderinformationen vanligtvis i en verklig implementering så att [!DNL Target] kan använda orderdetaljer som mått/dimensioner. I dokumentationen finns instruktioner om hur du [implementerar beställningsbekräftelsebegäran och parametrar](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-target-methods.html?lang=sv-SE).

>[!NOTE]
>
>Analyser för mål (A4T): Adobe Analytics kan konfigureras som rapportkälla för [!DNL Target]. Detta gör att alla mått som samlas in av mål-SDK kan visas i Adobe Analytics. Mer information finns i [A4T-översikten](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=sv-SE).

Snyggt jobbat! Nu när parametrarna finns på plats är vi redo att använda dessa parametrar för att skapa målgrupper och erbjudanden i Adobe Target.

**[NÄSTA :&quot;Skapa publiker och erbjudanden&quot; >](create-audiences-and-offers.md)**
