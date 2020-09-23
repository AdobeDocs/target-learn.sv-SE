---
title: Hämta Recommendations med leverans-API
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations innehåller en dedikerad uppsättning API:er som gör att du kan hantera din katalog med rekommenderade produkter och/eller innehåll. hantera era rekommendationsalgoritmer och -kampanjer, och leverera rekommendationer i JSON-, HTML- och XML-objekt som ska visas i webben, mobiler, e-post, IOT och andra kanaler.
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: c221f434ce9daec03dbb4d897343775b40b14462
workflow-type: tm+mt
source-wordcount: '1454'
ht-degree: 0%

---


# Hämtning [!DNL Recommendations] med leverans-API

Adobe Target- och Adobe Target-API: [!DNL Recommendations] erna kan användas för att leverera svar på webbsidor, men kan också användas i icke-HTML-baserade upplevelser som appar, skärmar, konsoler, e-post, kioskdatorer och andra visningsenheter. Med andra ord, när [!DNL Target] bibliotek och JavaScript inte kan användas, tillåter **[!DNL Target]Delivery API** fortfarande att vi får tillgång till alla [!DNL Target] funktioner för att leverera personaliserade upplevelser.

>[!NOTE]
>
> När du begär innehåll som innehåller faktiska rekommendationer (rekommenderade produkter eller objekt) använder du [!DNL Target] leverans-API:t.

Om du vill hämta rekommendationer skickar du ett Adobe Target Delivery API POST-anrop med lämplig sammanhangsberoende information, som kan innehålla ett användar-ID (som kan användas med profilspecifika rekommendationer som användarens nyligen visade objekt), relevant mbox-namn, mbox-parametrar, profilparametrar eller andra attribut. Svaret inkluderar rekommenderade entity.ids (och kan inkludera andra entitetsdata) i JSON- eller HTML-format, som sedan kan visas i enheten.

I [leverans-API](https://developers.adobetarget.com/api/delivery-api/) för Adobe Target finns alla funktioner som finns i en [!DNL Target] standardförfrågan.

>[!NOTE]
>Leverans-API:
>* Gör att ni kan hämta upplevelser eller erbjudanden för en plats och en målgrupp på ett RESTful-sätt.
>* Ingen autentisering krävs.
>* Endast POST.
>* Bearbetar inte cookies eller omdirigeringssamtal.
>* Kräver eller känner inte igen&quot;användarroller&quot;. Det hämtar bara innehåll eller rapporterar händelser till [!DNL Target] edge-servrar.


Följ de här stegen för att använda API:t för leverans för att leverera [!DNL Target] upplevelser, inklusive rekommendationer:

1. Skapa en [!DNL Target] aktivitet (A/B, XT, AP eller [!DNL Recommendations]) med den formulärbaserade dispositionen (inte Visual Experience Composer).
2. Använd leverans-API:t för att få ett svar på förfrågningar som genereras av den [!DNL Target] aktivitet du just skapade.

<!-- Q: Why are BOTH steps necessary for this? If you have a Form-based recommendation defined for an mbox, what's the point/benefit of ALSO having the Delivery API step in to retrieve results? Why can't you just have the Form-based Rec deliver the results in the destination device...?? A: See use case below... it's when you want to "intercept" the pending results in order to do more stuff prior to displaying the results. Things like real-time comparisons to inventory levels. -->

## Skapa en rekommendation med den formulärbaserade Experience Composer

Om du vill skapa rekommendationer som kan användas med leverans-API:t använder du den [formulärbaserade dispositionen](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html).

1. Först skapar och sparar du en JSON-baserad design som du kan använda i dina rekommendationer. Exempel-JSON, plus bakgrundsinformation om hur JSON-svar kan returneras när en formulärbaserad aktivitet konfigureras, finns i dokumentationen om [Skapa rekommendationsdesign](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-design/create-design.html). I det här exemplet heter designen *Simple JSON.*

   ![server-side-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

2. Gå [!DNL Target]till **[!UICONTROL Activities]>[!UICONTROL Create Activity]>[!UICONTROL Recommendations]** och markera **[!UICONTROL Form]**.

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

3. Markera en egenskap och klicka på **[!UICONTROL Next]**.
4. Definiera den plats där du vill att användarna ska få rekommendationens svar. I exemplet nedan används en plats med namnet *api_charter*. Välj din JSON-baserade design, som skapades tidigare, med namnet *Simple JSON.*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
5. Spara och aktivera rekommendationen. Det kommer att generera resultat. [När resultatet är klart](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html)kan du använda leverans-API:t för att hämta dem.

## Använda leverans-API

Syntaxen för [leverans-API](https://developers.adobetarget.com/api/delivery-api/#tag/Delivery-API) är:

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. Observera att klientkoden krävs. Du hittar din klientkod i Adobe Target genom att navigera till **[!UICONTROL Recommendations]>[!UICONTROL Settings]**. Observera **[!UICONTROL Client Code]** värdet i **[!UICONTROL Recommendation API Token]** avsnittet.
   ![client-code.png](assets/client-code.png)
1. När du har fått din klientkod konstruerar du ett leverans-API-anrop. Exemplet nedan börjar med det **[!UICONTROL Web Batched Mboxes Delivery API Call]** som anges i [Delivery API Postman-samlingen](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection)och gör relevanta ändringar. Exempel:
   * objekten för **webbläsare** och **adress** har tagits bort från **brödtexten**, eftersom de inte behövs för icke-HTML-användning
   * *api_charter* listas som platsnamn i det här exemplet
   * entity.id anges eftersom den här rekommendationen baseras på innehållets likhet, vilket kräver att en aktuell artikelnyckel skickas till [!DNL Target].
      ![server-side-Delivery-API-call.png](assets/server-side-delivery-api-call2.png)Kom ihåg att konfigurera frågeparametrarna korrekt. Se till exempel till att ange`{{CLIENT_CODE}}` det som behövs. <!--Q: In the updated call syntax, entity.id is listed as a profileParameter instead of an mboxParameter as in older versions. --> <!--Q: Old image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Old accompanying text: "Note this recommendation is based on Content Similar products based on the entity.id sent via mboxParameters." -->
      ![client-code3](assets/client-code3.png)
1. Skicka begäran. Detta körs mot *api_charter* -platsen, som har en aktiv rekommendation som körs på den, som definieras med din JSON-design som kommer att visa en lista över rekommenderade enheter.
1. Få ett svar baserat på JSON-designen.
   ![server-side-create-recs-json-response2.png](assets/server-side-create-recs-json-response2.png)Svaret innehåller nyckel-ID samt enhets-ID för de rekommenderade entiteterna.

Om du använder leverans-API:t med [!DNL Recommendations] på det här sättet kan du utföra ytterligare steg innan du visar rekommendationer till besökaren på en annan enhet än HTML. Du kan till exempel ta svaret från leverans-API:t för att utföra en ytterligare sökning i realtid av information om entitetsattribut (lager, pris, klassificering och så vidare) från ett annat system (till exempel en CMS-, PIM- eller e-handelsplattform) innan du visar det slutliga resultatet.

Med den metod som beskrivs i den här självstudiekursen kan du få vilket program som helst som kan utnyttja svaret från [!DNL Target] att tillhandahålla personaliserade rekommendationer.

## Exempelimplementeringar

Följande resurser innehåller exempel på olika implementeringar som inte är HTML-fokuserade. Tänk på att varje implementering blir unik på grund av det system och de enheter som används.

| Resurs | Detaljer |
| --- | --- |
| [Använda RESTful-API:er i AEM](https://helpx.adobe.com/experience-manager/using/restful-services.html) | Så här skapar och driftsätter du ett Adobe Experience Manager OSGi-paket som förbrukar data från en RESTful-webbtjänst från en annan leverantör. |
| [Adobe Target Everywhere - Implementera serversidan eller i IoT](https://expleague.azureedge.net/labs/L733/index.html) | Adobe Summit 2019 Lab som ger en praktisk upplevelse för React-applikationer som utnyttjar Adobe Target serversides-API:er. |
| [Adobe Target i en mobilapp utan Adobe SDK](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | Den här guiden visar hur du konfigurerar Adobe Target i din mobilapp utan att installera Adobe SDK. Den här lösningen använder Tealium SDK-webbvyn och Remote Commands-modulen för att skicka och ta emot begäranden till Adobe Visitor API (Experience Cloud) och Adobe Target API. |
| [Så här fungerar Adobe Target i mobilappar](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html) | Hur [!DNL Target] fungerar Mobile SDK? |
| [Konfigurera API: [!DNL Target] extension in Experience Platform Launch and Implementing [!DNL Target] erna](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | Steg för att konfigurera [!DNL Target] tillägget i Experience Platform Launch, lägga till [!DNL Target] tillägget i programmet och implementera API: [!DNL Target] er för att begära aktiviteter, förhämta erbjudanden och ange visuellt förhandsgranskningsläge. |
| [Adobe Target Node Client](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | Open-sourced [!DNL Target] Node.js SDK v1.0 |
| [Översikt över serversidan](https://docs.adobe.com/content/help/en/target/using/implement-target/server-side/api-and-sdk-overview.html) | Information om Adobe Target Server Side delivery APIs, Server Side Batch Delivery APIs, Node.js SDK och Adobe Target API: [!DNL Recommendations] er. |
| [Adobe Campaign Content Recommendations in Email](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | Blogg som beskriver hur du kan utnyttja innehållsrekommendationer i e-post via Adobe Target och Adobe I/O Runtime i Adobe Campaign. |

## Hantera [!DNL Recommendations] inställningar med API:er

Rekommendationer konfigureras oftast i användargränssnittet i Adobe Target och används eller nås via API: [!DNL Target] erna, av skäl som de som nämns i avsnitten ovan. Denna API-samordning är vanlig. Ibland kanske användare vill utföra alla åtgärder via API:er, både konfiguration och användning av resultat. Även om det är mycket mindre vanligt kan användare absolut konfigurera, köra *och* utnyttja resultatet av rekommendationer helt och hållet med API:erna.

Vi lärde oss i ett [tidigare avsnitt](manage-catalog.md) hur vi hanterar Adobe Target Recommendations-enheter och levererar dem på serversidan. På samma sätt kan du med Adobe I/O hantera villkor, kampanjer, samlingar och designmallar utan att behöva logga in på Adobe Target. En fullständig lista över alla [!DNL Recommendations] API:er finns [här](http://developers.adobetarget.com/api/recommendations/), men här finns en sammanfattning för referens.

| Resurs | Detaljer |
| --- | --- |
| [Samlingar](http://developers.adobetarget.com/api/recommendations/#tag/Collections) | Visa, skapa, hämta, redigera och ta bort samlingar. |
| [Kriterier](http://developers.adobetarget.com/api/recommendations/#tag/Criteria) | Lista och hämta villkor. |
| [Designs](http://developers.adobetarget.com/api/recommendations/#tag/Designs) | Lista, skapa, hämta, redigera, ta bort och validera designer. |
| [Enheter](http://developers.adobetarget.com/api/recommendations/#tag/Entities) | Spara, ta bort och hämta enheter. |
| [Erbjudanden](http://developers.adobetarget.com/api/recommendations/#tag/Promotions) | Visa, skapa, hämta, redigera och ta bort kampanjer. |
| [Kategorivillkor](http://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | Visa, skapa, hämta, redigera och ta bort kategorivillkor. |
| [Anpassade villkor](http://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | Visa, skapa, hämta, redigera och ta bort anpassade villkor. |
| [Artikelvillkor](http://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | Visa, skapa, hämta, redigera och ta bort objektvillkor. |
| [Popularitetskriterier](http://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | Visa, skapa, hämta, redigera och ta bort popularitetskriterier. |
| [Kriterier för profilattribut](http://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | Visa, skapa, hämta, redigera och ta bort villkor för profilattribut. |
| [Senaste villkor](http://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | Lista, skapa, hämta, redigera och ta bort senaste villkor. |
| [Sekvensvillkor](http://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | Visa, skapa, hämta, redigera och ta bort sekvensvillkor. |

## Referensdokumentation

* [Adobe Target API-dokumentation](https://developers.adobetarget.com/api/#getting-started)
* [Adobe Target Delivery API](https://developers.adobetarget.com/api/delivery-api/)
* [Integrera [!DNL Recommendations] med e-post](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## Sammanfattning och granskning

Grattis! När du är klar med den här självstudiekursen har du lärt dig att:
* [Hantera katalogen med Recommendations API](manage-catalog.md)
* [Hantera anpassade villkor med Recommendations API](manage-custom-criteria.md)
* [Använda leverans-API:t med Recommendations](fetch-recs-server-side-delivery-api.md)
