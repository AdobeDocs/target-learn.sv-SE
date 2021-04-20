---
title: Anpassa layouter
description: 'I den sista lektionen bygger vi två personaliseringsaktiviteter i Target för våra målgrupper. Lär dig hur du läser in och visar aktiviteterna i appen och validerar att innehållet visas vid rätt tidpunkt på rätt plats.  '
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 0%

---


# Anpassa layouter

Nu är det dags att sammanföra allt och skapa personaliserade upplevelser. En _aktivitet_ är [!DNL Target]-mekanismen som länkar samman platser, målgrupper och erbjudanden, så att [!DNL Target] svarar med det anpassade innehållet när begäran görs från appen. Vi bygger två personaliseringsaktiviteter i [!DNL Target] och validerar att anpassat innehåll visas för rätt användare vid rätt tidpunkt och på rätt plats.

## Utbildningsmål

När lektionen är klar kan du:

* Bygg aktiviteter i Adobe Target
* Validera aktiviteterna i exempelappen

## Skapa aktiviteter i Adobe Target

Lär dig hur du skapar aktiviteter för engagerande användare och sammanhangsbaserade erbjudanden.

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
1. Ställ in målgruppen på **[!UICONTROL New Mobile App Users]**.
1. Klicka på **[!UICONTROL Done]**.
   ![Ny målgrupp för mobilappsanvändare](assets/activity_create_4.jpg)

1. Ändra platsen till _wetravel_engage_home_.
1. Markera listrutepilen bredvid Standardinnehåll och välj **[!UICONTROL Change HTML Offer]**.

   ![Ny målgrupp för mobilappsanvändare](assets/activity_create_5.jpg)

1. Välj **[!UICONTROL Home: Engage New Users]**-erbjudandet.
1. Välj **[!UICONTROL Done]**.

   ![Ny målgrupp för mobilappsanvändare](assets/activity_create_6.jpg)

1. Välj **[!UICONTROL Add Location]**.
   ![Ny målgrupp för mobilappsanvändare](assets/activity_create_7.jpg)

1. Välj platsen _wetravel_engage_search_.
1. Ändra HTML-erbjudandet.

   ![Ny målgrupp för mobilappsanvändare](assets/activity_create_8.jpg)

1. Välj **[!UICONTROL Search: Engage New Users]**-erbjudandet.
1. Klicka på **[!UICONTROL Done]**.

   ![Ny målgrupp för mobilappsanvändare](assets/activity_create_9.jpg)

Ni har just kopplat samman en målgrupp med platser och erbjudanden, vilket skapar en personaliserad upplevelse för de nya mobilappsanvändarna! Nu bör upplevelsen se ut så här:

![Upplev en slutversion](assets/activity_engage_users_a_final.jpg)

Skapa nu en upplevelse för återkommande användare av mobilappar:

1. Välj **[!UICONTROL Add Experience Targeting]** till vänster.
1. Välj målgrupp **[!UICONTROL Returning Mobile App Users]**.
1. Välj **[!UICONTROL Done]**.
   ![Returnera målgrupp för mobilappsanvändare](assets/activity_create_11.jpg)

Använd nu samma process som vi använde tidigare för att konfigurera den nya upplevelsen. Konfigurationen för den returnerade användarupplevelsen för mobilappar bör se ut så här:

![Returnerar slutanvändare för mobilappar](assets/activity_engage_users_b_final.jpg)

Vi fortsätter till nästa skärm i konfigurationen:

1. Klicka på **[!UICONTROL Next]** för att gå vidare till skärmen **[!UICONTROL Targeting]**.
1. Använd standardinställningarna för Riktning. Om ni hade överlappande upplevelser för målgrupper (t.ex. _New York-användare_ och _förstagångsanvändare_) kan ordna prioritetsordningen på den här skärmen.
1. Klicka på **[!UICONTROL Next]** om du vill gå vidare till **[!UICONTROL Goals & Settings]**.

   ![Aktivera användaraktivitet - standardmålanpassning](assets/activity_engage_users_targeting.jpg)

Nu ska vi slutföra aktivitetsinställningarna:

1. Ange **[!UICONTROL Primary Goal]** som **[!UICONTROL Conversion]**.
1. Ställ in åtgärden på **[!UICONTROL Viewed an mbox]** > _wetravel_context_dest_ (eftersom den här platsen finns på bekräftelseskärmen kan vi använda den för att mäta konverteringar).

   ![Engagera användare - aktivitet - mål](assets/activity_create_12.jpg)

1. Behåll alla andra inställningar på skärmen till standardinställningarna.
1. Klicka på **[!UICONTROL Save & Close]** för att spara aktiviteten.
1. Aktivera **[!UICONTROL Activity]** på nästa skärm.

![Experience B Audience](assets/activity_create_13.jpg)

Vår första aktivitet är nu levande och redo att testas!

### Andra aktiviteten -&quot;Kontextuella erbjudanden&quot;

Här är en sammanfattning av den andra aktiviteten vi ska bygga:

| Målgrupp | Plats | Erbjudanden |
| --- | --- | --- |
| Mål: San Diego | web_context_dest | Kampanj för San Diego |
| Mål: Los Angeles | web_context_dest | Kampanj för Los Angeles |

Upprepa samma process som ovan för nästa aktivitet -&quot;Kontextuella erbjudanden&quot;. Slutkonfigurationen för båda upplevelserna visas nedan:

#### San Diego

![Sammanhangsbaserade erbjudanden - Upplev A](assets/activity_contextual_a_final.jpg)

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

Kör Emulatorn och håll utkik efter det första erbjudandet som ska visas längst ned på startskärmen. Om du är en återkommande användare med 5 eller fler appar startas visas _välkomsterbjudandet_. Om du är en ny användare (mindre än fem program startas) bör du se meddelandet _ny användare_:

![Bekräfta erbjudandet](assets/layout_home_validate.jpg)

Om det nya användarerbjudandet inte visas provar du med att rensa data för emulatorn. Då återställs programmet till 1 nästa gång du startar det. Detta görs under **[!UICONTROL Tools]** > **[!UICONTROL AVD Manager]**. Du kan också behöva starta om Android Studio om Logcat inte fungerar som det ska:

![Svepemulator](assets/layout_home_validate_avd_wipe.jpg)

Du kan också validera svaret i Logcat genom att filtrera för _wetravel_engage_home_:

![Verifiera erbjudande - Logcat](assets/layout_home_validate_logcat.jpg)

## Validera sökerbjudandet

Välj **[!UICONTROL San Jose]** som **[!UICONTROL Departure]** och **[!UICONTROL San Diego]** som **[!UICONTROL Destination]** och klicka på **[!UICONTROL Find Bus]** för att söka efter tillgängliga bussar.

På resultatskärmen ska du se meddelandet _use filters_. Om du är en återkommande användare med 5 eller fler appar startas visas inget meddelande här eftersom standardinnehållet har angetts för den här platsen (som är tom):

![Validera sökerbjudande](assets/layout_search_validate.jpg)

## Validera sammanhangsbaserade erbjudanden på Tack-skärmen

Fortsätt nu genom bokningsprocessen:

* Välj en buss på resultatskärmen.
* Välj en plats på utcheckningsskärmen.
* Välj **[!UICONTROL Credit Card]** på betalningsskärmen (lämna betalningsinformationen tom - ingen faktisk bokning görs).

Eftersom San Diego valdes som mål bör du se erbjudandebanderollen _DJ SAM_ på bekräftelseskärmen:

![Bekräfta kontexterbjudande - San Diego](assets/layout_context_san_diego.jpg)

Välj **[!UICONTROL Done]** och prova en annan bokning med Los Angeles som mål. Bekräftelseskärmen ska visa banderollen _Universal Studios_:

![Verifiera kontexterbjudande - Los Angeles](assets/layout_context_los_angeles.jpg)

## Slutsats

Grattis! Detta avslutar huvuddelen av självstudiekursen för Adobe Target SDK 4.x för Android. Nu har du kunskapen att implementera personalisering i Android-appar! Du kan använda den här dokumentationen och demoappen som referens för dina framtida projekt.

Nästa: Funktionsflaggning är en annan funktion som kan implementeras med Adobe Target i Android. Mer information om flaggning av funktioner finns i nästa lektion.

**[NÄSTA: Funktionsflaggning >](feature-flagging.md)**
