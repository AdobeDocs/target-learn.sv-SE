---
title: Hämta och uppdatera exempelappen Web.Travel
seo-title: Hämta exempelappen och verifiera SDK för mobiltjänster
description: 'Exempelappen We.Travel är förimplementerad med Adobe Mobile Services SDK v4. Du behöver bara uppdatera den så att den pekar på dina egna Experience Cloud Org- och Solution-konton.   '
seo-description: Exempelappen We.Travel är förimplementerad med Adobe Mobile Services SDK v4. Du behöver bara uppdatera den så att den pekar på dina egna Experience Cloud Org- och Solution-konton.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---


# Hämta och uppdatera exempelappen Web.Travel

Exempelappen We.Travel är förimplementerad med Adobe Mobile Services SDK v4. Du behöver bara uppdatera den så att den pekar på dina egna Experience Cloud-Org- och lösningskonton.

## Utbildningsmål

När lektionen är klar kan du:

* Ladda ned och öppna exempelappen We.Travel i Android Studio
* Verifiera och uppdatera SDK-inställningarna för mobiltjänster för [!DNL Target]

## Ladda ned appen We.Travel

* Hämta [sample-app-android-SDKv4-Base-Version.zip](assets/sample-app-android-SDKv4-Base-Version.zip)
* Dekomprimera zip-filen
* Öppna appen i Android Studio som ett befintligt projekt (ignorera alla fel om&quot;Ogiltig VCS-rotmappning&quot;)
* Kör appen i en emulator för att bekräfta att appen byggs och att du kan se hemskärmen
* Bläddra i appen och verifiera att du kan slutföra bokningsprocessen (välj ett betalningsalternativ och tryck bara på&quot;Fortsätt&quot; för att hoppa över faktureringsskärmen!)

   ![Öppna skärmen](assets/wetravel_homeScreen.png)![appConfirmation](assets/wetravel_confirmationScreen.png)

## Verifiera och uppdatera SDK-inställningarna för mobiltjänster för [!DNL Target]

Adobe Mobile Services SDK har förinstallerats i appen We.Travel [enligt dokumentationen](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html). Nu ska du uppdatera installationen så att den pekar på ditt eget [!DNL Target] konto.

Skapa först en ny app i användargränssnittet för Mobile Services:

1. Logga in i gränssnittet [för](https://mobilemarketing.adobe.com)Adobe Mobile Services.
1. Gå till [!UICONTROL Manage Apps]och klicka sedan på **[!UICONTROL Add]** för att lägga till ett nytt program som du kan använda med den här självstudiekursen (**[!UICONTROL Manage Apps]** > **[!UICONTROL Add]**).
1. Välj en Analytics-rapportserie med icke-produktionsdata, ge appen ett namn, välj **[!UICONTROL Standard]** typ och klicka på **[!UICONTROL Save]**.
1. När appen har lagts till lägger du till din [!DNL Target] klientkod på nästa skärm i [!UICONTROL SDK Target Options] -avsnittet (du hittar klientkoden i [!DNL Target] -gränssnittet under **[!UICONTROL Setup]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit Settings]**, bredvid `at.js` knappen Hämta).
1. Inställningen avgör [!UICONTROL Request Timeout] hur länge programmet väntar på svar från [!DNL Target] servern innan timeoutinstruktionerna körs. Lämna bara standardinställningen.
1. Aktivera [!UICONTROL Visitor ID Service] och kontrollera att du [!UICONTROL Organization] är markerad i listrutan.
1. Spara ändringarna genom att klicka **[!UICONTROL Save]** längst upp till höger i fönstret (inte den i [!UICONTROL Universal Links], [!UICONTROL App Links] alternativen eller [!UICONTROL Push Services] avsnittet).
1. Bläddra till hämtningsavsnittet för App SDK längst ned på sidan och hämta konfigurationsfilen:

   ![Hämta konfigurationsfilen](assets/config_file.jpg)

1. Ersätt `ADBMobileConfig.json` filen i projektresursmappen för Android Studio (app > src > main > assets).

1. Öppna nu `ADBMobileConfig.json` filen och kontrollera att den innehåller de förväntade ändringarna, som din [!DNL Target] klientkod och dina Analytics-uppgifter:
   ![Hämta konfigurationsfilen](assets/client_code.jpg)

Om du inte ser inställningarna bekräftar du att du klickade på rätt **[!UICONTROL Save]** knapp i [!UICONTROL Mobile Services] gränssnittet och kopierade filen till rätt plats.

Grattis! Du har uppdaterat SDK med din [!DNL Target] kontoinformation! Vi kommer att göra ytterligare validering av konfigurationen efter att vi lagt till [!DNL Target] begäranden i nästa lektion.

**[NÄSTA: &quot;Lägg till Target-förfrågningar&quot; >](add-requests.md)**
