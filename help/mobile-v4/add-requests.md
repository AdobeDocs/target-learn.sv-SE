---
title: Lägg till Adobe Target-begäranden
description: 'Adobe Mobile Services SDK (v4) innehåller metoder och funktioner för Adobe Target som gör att du kan anpassa din app med olika upplevelser för olika användare.   '
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 0%

---


# Lägg till Adobe Target-begäranden

Adobe Mobile Services SDK (v4) innehåller Adobe Target metoder och funktioner som gör att du kan anpassa din app med olika upplevelser för olika användare. Normalt görs en eller flera förfrågningar från appen till Adobe Target för att hämta det personaliserade innehållet och mäta effekten av det innehållet.

I den här lektionen ska du förbereda appen We.Travel för personalisering genom att implementera [!DNL Target] förfrågningar.

## Förutsättningar

Var noga med att [hämta och uppdatera exempelappen](download-and-update-the-sample-app.md).

## Utbildningsmål

När lektionen är klar kan du:

* Cachelagra flera [!DNL Target] erbjudanden (dvs. personaliserat innehåll) med en förhämtningsförfrågan i batch
* Läs in förhämtade [!DNL Target] platser
* Läsa in en [!DNL Target] plats i realtid (ej förhämtad)
* Rensa förhämtade platser från cache
* Validera förhämtade begäranden och begäranden i realtid

## Terminologi

Nedan finns några viktiga Target-termer som vi kommer att använda i resten av kursen.

* **Begäran:**  en nätverksbegäran till Adobe Target-servrarna
* **Erbjudande:**  ett kodfragment eller annat textbaserat innehåll, som definieras i [!DNL Target] användargränssnittet (eller med API), som levereras som svar. Vanligtvis JSON när [!DNL Target] används i inbyggda mobilappar.
* **Plats:**  ett användardefinierat namn som ges till en begäran, som används i gränssnittet för att associera erbjudanden med specifika förfrågningar [!DNL Target]
* **Batchbegäran:**  en enda begäran som innehåller flera platser
* **Förhämtningsbegäran:**  en enda begäran som hämtar erbjudanden och cachelagrar dem i minnet för framtida bruk i appen
* **Förhämtningsbegäran för grupp:**  en enda förfrågan som förhämtar erbjudanden för flera platser
* **Målgrupp:**  en grupp besökare som definieras i [!DNL Target] gränssnittet eller som delas till [!DNL Target] från andra Adobe-program (t.ex. &quot;iPhone X-besökare&quot;,&quot;besökare i Kalifornien&quot;,&quot;First App Open&quot;)
* **Aktivitet:**  en [!DNL Target] konstruktion som definieras i [!DNL Target] användargränssnittet (eller med API) och som länkar platser, erbjudanden och målgrupper för att skapa en personaliserad upplevelse

## Lägg till en förhämtningsbegäran för grupp

Den första begäran som vi implementerar i We.Travel är en förhämtningsbegäran i grupp med två [!DNL Target] platser på hemskärmen. I en senare lektion kommer vi att konfigurera erbjudanden för dessa platser som visar meddelanden som hjälper nya användare genom bokningsprocessen.

En förhämtningsbegäran hämtar [!DNL Target] innehåll så lite som möjligt genom att cacha serversvaret från Adobe Target (erbjudande). En begäran om batchförhämtning hämtar och cachelagrar flera erbjudanden, som var och en är kopplad till en annan plats. Alla förhämtade platser cachelagras på enheten för framtida bruk i användarsessionen. Genom att förhämta flera platser på hemskärmen kan vi hämta erbjudanden som kan användas senare när besökaren navigerar genom appen. Mer information om förhämtningsmetoder finns i [förhämtningsdokumentationen](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-mob-target-prefetch-android.html) .

### Lägg till förhämtningsbegäran för grupp

Vi uppdaterar HomeActivity-kontrollen (hemskärmens källkod), som finns under app > main > java > com.wetravel > Controller. Vi lägger till de två kodblocken som visas i rött:

Vi börjar med HomeActivity-kontrollen (hemskärmens källkod) som finns under app > main > java > com.wetravel > Controller.

Vi lägger till de två kodblocken som visas i rött:

![Förhämtningskod för HomeActivity](assets/homeactivity.jpg)

Rulla ned till slutet av HomeActivity-koden och lägg till koden som anges nedan efter `setHeader()` funktionen och *ersätta* den aktuella `onResume()` funktionen:

```java
@Override
protected void onResume() {
    super.onResume();
    targetPrefetchContent();
}

public void targetPrefetchContent() {
    List<TargetPrefetchObject> prefetchList = new ArrayList<>();
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, null));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, null));
    Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
        @Override
        public void call(final Boolean status) {
            HomeActivity.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    String cachingStatus = status ? "YES" : "NO";
                    System.out.println("Received Response from prefetch : " + cachingStatus);
                    setUp();

                }
            });
        }};
    Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
}
```

Din utvecklingsmiljö kommer antagligen att varna dig om att du inte har [!DNL Target] klasserna importerade i filen. Se till att importera [!DNL Target] klasserna högst upp i HomeActivity-kontrollenheten enligt vad som visas i rött nedan:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

![Importera Target-klasser](assets/import.jpg)

Felen &quot;cannot find symbol variable wetravel_engage_home&quot; och &quot;cannot find symbol variable wetravel_engage_search&quot; visas förmodligen också. Lägg till dessa i `Constant.java` filen (i app > src > main > java > com > weravel > Utils):

```java
public static final String wetravel_engage_home = "wetravel_engage_home";
public static final String wetravel_engage_search = "wetravel_engage_search";
```

![Lägg till platsnamnen i filen Constant.java](assets/constants.jpg)

### Förklaring av begärandekod för batchförhämtning

| Code | Beskrivning |
|--- |--- |
| `targetPrefetchContent()` | En användardefinierad funktion (ingår inte i SDK) som använder [!DNL Target] metoder för att hämta och cachelagra två [!DNL Target] platser. |
| `prefetchContent()` | SDK- [!DNL Target] metoden som skickar förhämtningsbegäran |
| `Constant.wetravel_engage_home` | Förhämtat [!DNL Target] platsnamn som visar erbjudandeinnehållet på hemskärmen |
| `Constant.wetravel_engage_search` | Förhämtat [!DNL Target] platsnamn som visar erbjudandeinnehållet på skärmen Sökresultat. Eftersom detta är en andra plats i förhämtningen kallas denna förhämtningsbegäran för en&quot;förhämtningsbatchbegäran&quot;. |
| setUp() | En användardefinierad funktion som återger appens hemskärm efter att erbjudandena [!DNL Target] har hämtats i förväg |

### Om asynkron jämfört med synkron

Med den kod vi just har implementerat görs förhämtningsbegäran som ett synkront, blockerande anrop, precis innan hemskärmen återges. När vi klistrade in den nya koden i HomeActivity-kontrollen flyttade vi funktionskörningen från `setUp()` `onResume()` funktionen till efter Target-begäran. Detta kan vara bra i scenarier där du vill anpassa innehåll när appen först öppnas, eftersom det ser till att personaliserat innehåll från Target-servrarna har returnerats (eller timeout) innan den första skärmen återges. Om du vill tillåta att begäranden läses in asynkront (i bakgrunden), anropar du `setUp()` i `onCreate()` funktionen i stället.

### Validera begäran om batchförhämtning

Bygg om appen och öppna Android-emulatorn. (I följande skärmbilder används Pixel 2 på Android Q version 9+, API-nivå 29). Prefetch-svaret ska vara &quot;prefetch response receive&quot;:

När hemskärmen återges bör förhämtningsbegäran läsas in. Med Logcat kan du filtrera för [!DNL "Target"] att se begäran och svar:

![Validera begäranden på hemskärmen](assets/prefetch_validation.jpg)

Om du inte ser något positivt svar kontrollerar du inställningarna i `ADBMobileConfig.json` fil- och kodsyntaxen i filen HomeActivity.

Två platser cachelagras nu till enheten. Platsnamnen kommer snart att läsas in i [!DNL Target] gränssnittet, där de kan väljas i olika listrutor när du använder dem i en aktivitet.

### Lägg till inläsningsbegäranden för varje cachelagrad plats

Nu när platserna är förhämtade och deras svar cachelagrade till enheten lägger vi till den metod som hämtar erbjudandeinnehållet från cachen så att du kan använda den för att uppdatera programmet. `Target.loadRequest()` Vi lägger till en ny anpassad metod som kallas `engageMessage()` som körs med förhämtningsbegäran. `engageMessage()` ringer `Target.loadRequest()`. `engageMessage()` kör innan `setUp()` för att se till att inläsningsbegäran anropas innan skärmen konfigureras.

Lägg först till anropet och metoden för platsen weravel_engage_home i HomeActivity: `engageMessage()`

![Lägg till första inläsningsbegäran](assets/wetravel_engage_home_loadRequest.jpg)

Här är den uppdaterade koden:

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
    public void engageMessage() {
        Target.loadRequest(Constant.wetravel_engage_home, "", null, null, null,
            new Target.TargetCallback<String>(){
                @Override
                public void call(final String s) {
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            System.out.println("Engage Message : " + s);
                            if(s != null && !s.isEmpty()) Utility.showToast(getApplicationContext(), s);
                        }
                    });
                }
            });
    }
```

Lägg nu till `engageMessage()` anropet och metoden för platsen wetravel_engage_search i SearchBusActivity. Observera att `engageMessage()` anropet är inställt i `onResume()` metoden före anropet till `setUpSearch()` så att det körs innan skärmen är konfigurerad:

![Lägg till andra inläsningsbegäran](assets/wetravel_engage_search_loadRequest.jpg)

Här är den uppdaterade koden:

```java
    @Override
    public void onResume() {
        super.onResume();
        engageMessage();
        setUpSearch();
    }
    public void engageMessage() {
        Target.loadRequest(Constant.wetravel_engage_search, "", null, null, null,
                new Target.TargetCallback<String>(){
                    @Override
                    public void call(final String s) {
                        runOnUiThread(new Runnable() {
                            @Override
                            public void run() {
                                System.out.println("Engage Message : " + s);
                                if(s != null && !s.isEmpty()) Utility.showToast(getApplicationContext(), s);
                            }
                        });
                    }
                });
    }
```

Eftersom du just har lagt till Target-metoder i SearchBusActivity, måste du importera [!DNL Target] klasserna:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

## Lägg till en begäran i realtid

Nästa begäran som vi lägger till i appen blir en begäran i realtid på Tack-skärmen. Med&quot;realtid&quot; menar vi att både begäran kommer att göras och att svaret kommer att tillämpas omedelbart (inte cachelagras senare). I en senare lektion kommer vi att bygga en upplevelse med denna begäran, som är anpassad efter användarens resa.

Låt oss lägga till en förfrågan i realtid på Tack-skärmen. I filen TackYouActivity gör vi de ändringar som visas i rött:
![Lägg till en plats i realtid på Tack-skärmen](assets/thankyou.jpg)

Bläddra till slutet av filen TackAktivitet. Kommentera de tre raderna i `getRecommandations()` funktionen och lägg till anropet till `targetLoadRequest()` funktionen:

```java
// AppDialogs.dialogLoaderHide();
// recommandations.addAll(recommandation.recommandations);
// recommandationbAdapter.notifyDataSetChanged();
```

Lägg till den här kodraden i `getRecommandations()` funktionen:

```java
targetLoadRequest(recommandation.recommandations);
```

Nu måste vi definiera `targetLoadRequest()` funktionen:
![Lägg till en plats i realtid på Tack-skärmen](assets/thankyou2.jpg)

Lägg till det här kodblocket efter `filterRecommendationBasedOnOffer()` funktionen:

```java
public void targetLoadRequest(final ArrayList<Recommandation> recommandations) {
    Target.loadRequest(Constant.wetravel_context_dest, "", null, null, null, new Target.TargetCallback<String>() {
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
}
```

Eftersom du just har lagt till Target-metoder i TackYouActivity måste du importera Target-klasserna:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

### targetLoadRequest(), kodförklaring

| Code | Beskrivning |
|--- |--- |
| `targetLoadRequest()` | En användardefinierad funktion (ingår inte i SDK) som startar `Target.loadRequest()` som läser in och visar platsen wetravel_context_dest |
| `Target.loadRequest()` | SDK-metoden som skickar begäran till Target-servern |
| Constant.wetravel_context_dest | Platsnamnet som tilldelats den begäran som vi kommer att använda senare när vi skapar aktiviteten i [!DNL Target] gränssnittet |
| `filterRecommendationBasedOnOffer()` | En användardefinierad funktion i appen som hämtar platserbjudandet från Target-svaret och avgör hur appen ska ändras baserat på erbjudandets innehåll |
| `recommandations.addAll()` | En användardefinierad funktion i appen som kördes som standard när TackYou-skärmen lästes in, men som nu körs när Target-svaret har tagits emot och tolkats av `filterRecommendationBasedOnOffer()` |

Det här var en mer sofistikerad uppdatering som vi gjorde i appen med den begäran vi lade till på startskärmen, så vi ska titta på vad vi gjorde:

1. Vi avbröt appens tidigare beteende att visa tre standardkampanjer genom att kommentera kodraderna
1. Vi sa åt programmet att istället köra en ny funktion, som vi godtyckligt kallar targetLoadRequest
1. Vi definierade `targetLoadRequest` funktionen för att göra en begäran till Target med metoden Target.loadRequest och kör omedelbart `filterRecommendationBasedOnOffer()` funktionen när [!DNL Target] erbjudandesvaret tas emot
1. Funktionen tolkar `filterRecommendationBasedOnOffer()` svaret och avgör vilka kampanjer som ska användas på skärmen

Detta är ett mycket vanligt användningsmönster när du använder [!DNL Target] i mobilappar.  Det är båda mycket kraftfullt, eftersom du kan anpassa praktiskt taget alla aspekter av din mobilapp. Det kräver också samordning mellan programkoden och de erbjudanden som vi senare kommer att definiera i [!DNL Target] gränssnittet. På grund av den här samordningen kan vissa användningsexempel kräva att du uppdaterar din app i appbutiken för att starta aktiviteten.

### Validera begäran i realtid

Öppna Android-emulatorn och gå igenom alla steg för att boka en resa: Hem > Busssökresultat > Platsval, Betalningsalternativ (alla betalningsalternativ med tomma data fungerar).

På den sista Tack-skärmen tittar du på Logcat för svaret. Svaret ska vara &quot;Standardinnehåll returnerades för &quot;wetravel_context_dest&quot;:

![Lägg till en plats i realtid på Tack-skärmen](assets/thankyou_validation.jpg)

## Rensa förhämtade platser från cache

Det kan finnas situationer där förhämtade platser måste rensas under en session. När en bokning görs är det till exempel klokt att rensa de cachelagrade platserna eftersom användaren nu är&quot;engagerad&quot; och förstår bokningsprocessen. Om de bokar en annan resa under sessionen behöver de inte de ursprungliga platserna på startskärmen och sökresultatskärmen för att vägleda bokningen. Det skulle vara vettigare att rensa platserna från cacheminnet och förhämta nya erbjudanden för kanske en rabatterad andra bokning eller ett annat relevant scenario. Logik kan läggas till på startskärmen och sökresultatskärmen för att hämta nya platser i förväg om en bokning har gjorts under sessionen.

I det här exemplet rensar vi förhämtade platser för sessionen när en bokning görs. Detta görs genom att anropa `Target.clearPrefetchCache()` funktionen. Ställ in funktionen inuti `targetLoadRequest()` funktionen så som visas nedan:

```java
Target.clearPrefetchCache()
```

![Rensa förhämtade platser från cache](assets/clearPrefetch.jpg)

Grattis! Din app har nu ramverket för personalisering. I nästa lektion ska vi förbättra våra personaliseringsfunktioner genom att lägga till parametrar till dessa platser.

**[NÄSTA: &quot;Lägg till parametrar&quot; >](add-parameters.md)**
