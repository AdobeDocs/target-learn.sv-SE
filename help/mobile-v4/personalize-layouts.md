---
title: Anpassa layouter
description: I den sista lektionen bygger vi två personaliseringsaktiviteter i Target för våra målgrupper. Lär dig hur du läser in och visar aktiviteterna i appen och validerar att innehållet visas vid rätt tidpunkt på rätt plats.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
author: Daniel Wright
exl-id: a9f033d9-9f72-4154-88f5-d36423a404d0
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# Anpassa layouter

Nu är det dags att sammanföra allt och skapa personaliserade upplevelser. En _aktivitet_ är [!DNL Target]-mekanismen som länkar platserna, målgrupperna och erbjudandena tillsammans, så att [!DNL Target] svarar på det anpassade innehållet när förfrågan görs från appen. Vi skapar två personaliseringsaktiviteter i [!DNL Target] och validerar att det anpassade innehållet visas för rätt användare vid rätt tidpunkt och på rätt plats.

## Utbildningsmål

När lektionen är klar kan du:

* Bygg aktiviteter i Adobe Target
* Validera aktiviteterna i exempelappen

## Skapa aktiviteter i Adobe Target

Lär dig skapa aktiviteter för engagerande användare och sammanhangsbaserade erbjudanden.

### Första aktiviteten -&quot;Engagera användare&quot;

Här är en sammanfattning av aktiviteten vi ska bygga:

| Målgrupp | Platser | Erbjudanden |
|---|---|---|
| Nya mobilappsanvändare | web_engage_home, wetravel_engage_search | Hem: Engagera nya användare, sök: Engagera nya användare |
| Returnerar användare av mobilappar | web_engage_home, wetravel_engage_search | Hem: Returnerande användare, default_content |

Gör följande i gränssnittet [!DNL Target]:

1. Välj **[!UICONTROL Activities]** > **[!UICONTROL Create Activity]** > **[!UICONTROL Experience Targeting]**.

   ![Skapa aktivitet](assets/activity_create_1.jpg)

1. Klicka på **[!UICONTROL Mobile App]**.
1. Välj **[!UICONTROL Form composer]**.
1. Markera arbetsytan (samma arbetsyta som du använde i tidigare lektioner).
1. Välj din egenskap (samma egenskap som du använde i tidigare lektioner).
1. Klicka på **[!UICONTROL Next]**.

   ![Skapa aktivitet](assets/activity_create_2.jpg)

1. Ändra aktivitetstiteln till **[!UICONTROL Engage Users]**.
1. Välj **[!UICONTROL ellipsis]** > **[!UICONTROL Change Audience]**.
   ![Nya mobilappsanvändare ändrar målgrupp](assets/activity_create_3.jpg)
1. Ange målgruppen till **[!UICONTROL New Mobile App Users]**.
1. Klicka på **[!UICONTROL Done]**.
   ![Ny målgrupp för mobilappsanvändare](assets/activity_create_4.jpg)

1. Ändra platsen till _wetravel_engage_home_.
1. Markera listrutepilen bredvid Standardinnehåll och välj **[!UICONTROL Change HTML Offer]**.

   ![Ny målgrupp för mobilappsanvändare](assets/activity_create_5.jpg)

1. Välj erbjudandet **[!UICONTROL Home: Engage New Users]**.
1. Välj **[!UICONTROL Done]**.

   ![Ny målgrupp för mobilappsanvändare](assets/activity_create_6.jpg)

1. Välj **[!UICONTROL Add Location]**.
   ![Ny målgrupp för mobilappsanvändare](assets/activity_create_7.jpg)

1. Välj platsen _wetravel_engage_search_.
1. Ändra HTML.

   ![Ny målgrupp för mobilappsanvändare](assets/activity_create_8.jpg)

1. Välj erbjudandet **[!UICONTROL Search: Engage New Users]**.
1. Klicka på **[!UICONTROL Done]**.

   ![Ny målgrupp för mobilappsanvändare](assets/activity_create_9.jpg)

Ni har just kopplat samman en målgrupp med platser och erbjudanden, vilket skapar en personaliserad upplevelse för de nya mobilappsanvändarna! Nu bör upplevelsen se ut så här:

![Upplev en slutversion](assets/activity_engage_users_a_final.jpg)

Skapa nu en upplevelse för återkommande användare av mobilappar:

1. Välj **[!UICONTROL Add Experience Targeting]** till vänster.
1. Välj målgrupp **[!UICONTROL Returning Mobile App Users]**.
1. Välj **[!UICONTROL Done]**.
   ![Returnerar målgrupp för mobilappsanvändare](assets/activity_create_11.jpg)

Använd nu samma process som vi använde tidigare för att konfigurera den nya upplevelsen. Konfigurationen för den returnerade användarupplevelsen för mobilappar bör se ut så här:

![Slutgiltigt returnerade mobilappsanvändare](assets/activity_engage_users_b_final.jpg)

Vi fortsätter till nästa skärm i konfigurationen:

1. Klicka på **[!UICONTROL Next]** för att gå till skärmen **[!UICONTROL Targeting]**.
1. Använd standardinställningarna för Riktning. Om du hade upplevelser för överlappande målgrupper (t.ex. _New York-användare_ och _förstagångsanvändare_) kan du ordna prioritetsordningen på den här skärmen.
1. Klicka på **[!UICONTROL Next]** om du vill gå vidare till **[!UICONTROL Goals & Settings]**.

   ![Aktivera användaraktivitet - standardmålinställning](assets/activity_engage_users_targeting.jpg)

Nu ska vi slutföra aktivitetsinställningarna:

1. Ange **[!UICONTROL Primary Goal]** som **[!UICONTROL Conversion]**.
1. Ange åtgärden till **[!UICONTROL Viewed an mbox]** > _wetravel_context_dest_ (eftersom den här platsen finns på bekräftelseskärmen kan vi använda den för att mäta konverteringar).

   ![Aktivera användaraktivitet - mål](assets/activity_create_12.jpg)

1. Behåll alla andra inställningar på skärmen till standardinställningarna.
1. Klicka på **[!UICONTROL Save & Close]** för att spara aktiviteten.
1. Aktivera **[!UICONTROL Activity]** på nästa skärm.

![Upplevelse B-målgrupp](assets/activity_create_13.jpg)

Vår första aktivitet är nu levande och redo att testas!

### Andra aktiviteten -&quot;Kontextuella erbjudanden&quot;

Här är en sammanfattning av den andra aktiviteten vi ska bygga:

| Målgrupp | Plats | Erbjudanden |
| --- | --- | --- |
| Mål: San Diego | web_context_dest | Kampanj för San Diego |
| Destination: Los Angeles | web_context_dest | Kampanj för Los Angeles |

Upprepa samma process som ovan för nästa aktivitet -&quot;Kontextuella erbjudanden&quot;. Slutkonfigurationen för båda upplevelserna visas nedan:

#### San Diego

![Sammanhangsbaserade erbjudanden - Upplevelse A](assets/activity_contextual_a_final.jpg)

#### Los Angeles

![Sammanhangsbaserade erbjudanden - upplevelse B](assets/activity_contextual_b_final.jpg)

I steget Mål och inställningar ändrar vi det primära målet till den plats där bokningsbekräftelseskärmen visas:

1. Under **[!UICONTROL Reporting Settings]** anger du **[!UICONTROL Primary Goal]** till **[!UICONTROL Conversion]**.
1. Ställ in åtgärden på **[!UICONTROL Viewed an mbox]** > _wetravel_context_dest_ (i den här aktiviteten är det här måttet praktiskt taget meningslöst eftersom det också är den plats som levererar upplevelsen).
1. Klicka på **[!UICONTROL Save & Close]**.

![Sammanhangsbaserade erbjudanden - upplevelse](assets/activity_create_14.jpg)

Aktivera aktiviteten på nästa skärm.

Nu är vår andra aktivitet live och redo att testa!

## Validera erbjudandet

Kör Emulatorn och håll utkik efter det första erbjudandet som ska visas längst ned på startskärmen. Om du är en återkommande användare med fem eller fler appstarter visas erbjudandet _Välkommen tillbaka_. Om du är en ny användare (mindre än fem program startas) bör du se meddelandet _ny användare_:

![Verifiera erbjudandet](assets/layout_home_validate.jpg)

Om det nya användarerbjudandet inte visas provar du med att rensa data för emulatorn. Då återställs programmet till 1 nästa gång du startar det. Detta görs under **[!UICONTROL Tools]** > **[!UICONTROL AVD Manager]**. Du kan också behöva starta om Android Studio om Logcat inte fungerar som det ska:

![Rensa emulator](assets/layout_home_validate_avd_wipe.jpg)

Du kan också validera svaret i Logcat genom att filtrera för _wetravel_engage_home_:

![Verifiera erbjudandet - Logcat](assets/layout_home_validate_logcat.jpg)

## Validera sökerbjudandet

Välj **[!UICONTROL San Jose]** som din **[!UICONTROL Departure]** och **[!UICONTROL San Diego]** som din **[!UICONTROL Destination]** och klicka på **[!UICONTROL Find Bus]** för att söka efter tillgängliga bussar.

På resultatskärmen bör du se meddelandet _use filters_. Om du är en återkommande användare med 5 eller fler appar startas visas inget meddelande här eftersom standardinnehållet har angetts för den här platsen (som är tom):

![Verifiera sökerbjudandet](assets/layout_search_validate.jpg)

## Validera kontextuella erbjudanden på Tack-skärmen

Fortsätt nu genom bokningsprocessen:

* Välj en buss på resultatskärmen.
* Välj en plats på utcheckningsskärmen.
* Välj **[!UICONTROL Credit Card]** på betalningsskärmen (lämna betalningsinformationen tom - ingen faktisk bokning görs).

Eftersom San Diego valdes som mål bör du se bannern _DJ SAM_ på bekräftelseskärmen:

![Verifiera kontexterbjudande - San Diego](assets/layout_context_san_diego.jpg)

Välj nu **[!UICONTROL Done]** och försök med en annan bokning med Los Angeles som mål. Bekräftelseskärmen ska visa bannern _Universal Studios_:

![Verifiera kontexterbjudande - Los Angeles](assets/layout_context_los_angeles.jpg)

## Slutsats

Grattis! Detta avslutar huvuddelen av självstudiekursen för Adobe Target SDK 4.x för Android. Nu har du kunskapen att implementera personalisering i Android-appar! Du kan använda den här dokumentationen och demoappen som referens för dina framtida projekt.

Därefter: Funktionsflaggning är en annan funktion som kan implementeras med Adobe Target i Android. Läs nästa lektion om hur du flaggar funktioner.

**[NÄSTA : Funktionsflaggning >](feature-flagging.md)**
