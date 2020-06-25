---
title: Anpassa layouter
seo-title: Anpassa layouter
description: 'I den sista lektionen ska vi bygga två personaliseringsaktiviteter i Target för våra målgrupper. Vi läser in och visar aktiviteterna i appen och validerar att innehållet visas vid rätt tidpunkt på rätt plats.  '
seo-description: I den sista lektionen ska vi bygga två personaliseringsaktiviteter i Target för våra målgrupper. Vi läser in och visar aktiviteterna i appen och validerar att innehållet visas vid rätt tidpunkt på rätt plats.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 0%

---


# Anpassa layouter

Nu är det dags att sammanföra allt och skapa personaliserade upplevelser. En _aktivitet_ är den [!DNL Target] mekanism som länkar samman platser, målgrupper och erbjudanden, så att när en förfrågan görs från appen svarar på [!DNL Target] det personaliserade innehållet. Vi bygger två personaliseringsaktiviteter i [!DNL Target] och validerar att personaliserat innehåll visas för rätt användare vid rätt tidpunkt och på rätt plats.

## Utbildningsmål

När lektionen är klar kan du:

* Build Activities in Adobe Target
* Validera aktiviteterna i exempelappen

## Skapa aktiviteter i Adobe Target

Lär dig hur du skapar aktiviteter för engagerande användare och sammanhangsbaserade erbjudanden.

### First Activity - &quot;Engage Users&quot;

Here is a summary of the activity we&#39;ll build:

| Audience | Platser | Erbjudanden |
|---|---|---|
| New Mobile App Users | web_engage_home, wetravel_engage_search | Hem: Engagera nya användare, sök: Engagera nya användare |
| Returnerar användare av mobilappar | web_engage_home, wetravel_engage_search | Hem: Returnerande användare, default_content |

Gör följande i [!DNL Target] gränssnittet:

1. Välj **[!UICONTROL Activities]** > **[!UICONTROL Create Activity]** > **[!UICONTROL Experience Targeting]**.

   ![Skapa aktivitet](assets/activity_create_1.jpg)

1. Klicka på **[!UICONTROL Mobile App]**.
1. Markera **[!UICONTROL Form composer]**.
1. Markera arbetsytan (samma arbetsyta som du använde i tidigare lektioner).
1. Select your Property  (the same property you used in previous lessons).
1. Klicka på **[!UICONTROL Next]**.

   ![Skapa aktivitet](assets/activity_create_2.jpg)

1. Change the activity title to **[!UICONTROL Engage Users]**.
1. Välj **[!UICONTROL ellipsis]** > **[!UICONTROL Change Audience]**.
   ![Nya mobilappsanvändare ändrar målgrupp](assets/activity_create_3.jpg)
1. Ställ in målgruppen på **[!UICONTROL New Mobile App Users]**.
1. Klicka på **[!UICONTROL Done]**.
   ![Ny målgrupp för mobilappsanvändare](assets/activity_create_4.jpg)

1. Change the location to _wetravel_engage_home_.
1. Select the dropdown arrow next to Default Content and select **[!UICONTROL Change HTML Offer]**.

   ![Ny målgrupp för mobilappsanvändare](assets/activity_create_5.jpg)

1. Välj **[!UICONTROL Home: Engage New Users]** erbjudandet.
1. Välj **[!UICONTROL Done]**.

   ![Ny målgrupp för mobilappsanvändare](assets/activity_create_6.jpg)

1. Välj **[!UICONTROL Add Location]**.
   ![Ny målgrupp för mobilappsanvändare](assets/activity_create_7.jpg)

1. Välj platsen _wetravel_engage_search_ .
1. Ändra HTML-erbjudandet.

   ![Ny målgrupp för mobilappsanvändare](assets/activity_create_8.jpg)

1. Välj **[!UICONTROL Search: Engage New Users]** erbjudandet.
1. Klicka på **[!UICONTROL Done]**.

   ![Ny målgrupp för mobilappsanvändare](assets/activity_create_9.jpg)

Ni har just kopplat samman en målgrupp med platser och erbjudanden, vilket skapar en personaliserad upplevelse för de nya mobilappsanvändarna! Nu bör upplevelsen se ut så här:

![Upplev en slutversion](assets/activity_engage_users_a_final.jpg)

Skapa nu en upplevelse för återkommande användare av mobilappar:

1. Markera **[!UICONTROL Add Experience Targeting]** till vänster.
1. Välj publik **[!UICONTROL Returning Mobile App Users]**.
1. Välj **[!UICONTROL Done]**.
   ![Returnera målgrupp för mobilappsanvändare](assets/activity_create_11.jpg)

Använd nu samma process som vi använde tidigare för att konfigurera den nya upplevelsen. Konfigurationen för den returnerade användarupplevelsen för mobilappar bör se ut så här:

![Returnerar slutanvändare för mobilappar](assets/activity_engage_users_b_final.jpg)

Vi fortsätter till nästa skärm i konfigurationen:

1. Klicka **[!UICONTROL Next]** för att gå till **[!UICONTROL Targeting]** skärmen.
1. Använd standardinställningarna för Riktning. Om du hade upplevelser för överlappande målgrupper (t.ex. _New York Users_ och _First Time Users_), kan du ordna prioritetsordningen på den här skärmen.
1. Klicka **[!UICONTROL Next]** för att gå vidare till **[!UICONTROL Goals & Settings]**.

   ![Aktivera användaraktivitet - standardmålanpassning](assets/activity_engage_users_targeting.jpg)

Nu ska vi slutföra aktivitetsinställningarna:

1. Ställ in **[!UICONTROL Primary Goal]** på **[!UICONTROL Conversion]**.
1. Ange åtgärden till **[!UICONTROL Viewed an mbox]** > _wetravel_context_dest_ (eftersom den här platsen finns på bekräftelseskärmen kan vi använda den för att mäta konverteringar).

   ![Engagera användare - aktivitet - mål](assets/activity_create_12.jpg)

1. Behåll alla andra inställningar på skärmen till standardinställningarna.
1. Klicka **[!UICONTROL Save & Close]** för att spara aktiviteten.
1. Activate the **[!UICONTROL Activity]** on the next screen.

![Experience B Audience](assets/activity_create_13.jpg)

Our first activity is now live and ready to test!

### Second Activity - &quot;Contextual Offers&quot;

Here is a summary of the second activity we&#39;ll build:

| Audience | Plats | Erbjudanden |
| --- | --- | --- |
| Mål: San Diego | web_context_dest | Kampanj för San Diego |
| Mål: Los Angeles | web_context_dest | Kampanj för Los Angeles |

Upprepa samma process som ovan för nästa aktivitet -&quot;Kontextuella erbjudanden&quot;. Slutkonfigurationen för båda upplevelserna visas nedan:

#### San Diego

![Contextual Offers - Experience A](assets/activity_contextual_a_final.jpg)

#### Los Angeles

![Sammanhangsbaserade erbjudanden - upplevelse B](assets/activity_contextual_b_final.jpg)

I steget Mål och inställningar ändrar vi det primära målet till den plats där bokningsbekräftelseskärmen visas:

1. Under **[!UICONTROL Reporting Settings]** anger du **[!UICONTROL Primary Goal]** till **[!UICONTROL Conversion]**.
1. Ange åtgärden till **[!UICONTROL Viewed an mbox]** > _wetravel_context_dest_ (i den här aktiviteten är det här måttet praktiskt taget meningslöst eftersom det här också är den plats som levererar upplevelsen).
1. Klicka på **[!UICONTROL Save & Close]**.

![Contextual Offers - Experience](assets/activity_create_14.jpg)

Aktivera aktiviteten på nästa skärm.

Nu är vår andra aktivitet live och redo att testa!

## Validate the Home Offer

Kör Emulatorn och håll utkik efter det första erbjudandet som ska visas längst ned på startskärmen. Om du är en återkommande användare med fem eller fler appstarter visas _erbjudandet om återkoppling_ . Om du är en ny användare (mindre än fem program startas) bör du se det _nya_ meddelandet:

![Bekräfta erbjudandet](assets/layout_home_validate.jpg)

Om det nya användarerbjudandet inte visas provar du med att rensa data för emulatorn. Då återställs programmet till 1 nästa gång du startar det. Detta görs under **[!UICONTROL Tools]** > **[!UICONTROL AVD Manager]**. Du kan också behöva starta om Android Studio om Logcat inte fungerar som det ska:

![Svepemulator](assets/layout_home_validate_avd_wipe.jpg)

Du kan också validera svaret i Logcat genom att filtrera efter _wetravel_engage_home_:

![Verifiera erbjudande - Logcat](assets/layout_home_validate_logcat.jpg)

## Validera sökerbjudandet

Välj **[!UICONTROL San Jose]** som din **[!UICONTROL Departure]** och **[!UICONTROL San Diego]** som din **[!UICONTROL Destination]** och klicka på **[!UICONTROL Find Bus]** för att söka efter tillgängliga bussar.

På resultatskärmen bör du se _meddelandet om att använda filter_ . Om du är en återkommande användare med 5 eller fler appar startas visas inget meddelande här eftersom standardinnehållet har angetts för den här platsen (som är tom):

![Validera sökerbjudande](assets/layout_search_validate.jpg)

## Validera sammanhangsbaserade erbjudanden på Tack-skärmen

Now continue through the booking process:

* Select a bus on the results screen.
* Välj en plats på utcheckningsskärmen.
* Select **[!UICONTROL Credit Card]** on the payment screen (leave the payment info blank - no actual booking will take place).

Since San Diego was selected as the destination, you should see the _DJ SAM_ offer banner on the confirmation screen:

![Validate Context Offer - San Diego](assets/layout_context_san_diego.jpg)

Now select **[!UICONTROL Done]** and try another booking with Los Angeles as the destination. The confirmation screen should display the _Universal Studios_ banner:

![Bekräfta kontexterbjudande - Los Angeles](assets/layout_context_los_angeles.jpg)

## Slutsats

Grattis! Detta avslutar huvuddelen av självstudiekursen för Adobe Target SDK 4.x för Android. Nu har du kunskapen att implementera personalisering i Android-appar! Du kan använda den här dokumentationen och demoappen som referens för dina framtida projekt.

Nästa: Funktionsflaggning är en annan funktion som kan implementeras med Adobe Target i Android. Mer information om flaggning av funktioner finns i nästa lektion.

**[NÄSTA: Funktionsflaggning >](feature-flagging.md)**
