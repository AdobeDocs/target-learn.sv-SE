---
title: Hämta och uppdatera exempelappen Web.Travel
description: 'Exempelappen We.Travel är förimplementerad med Adobe Mobile Services SDK v4. Du behöver bara uppdatera den så att den pekar på dina egna Experience Cloud Org- och Solution-konton.   '
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 244bcf7a-b59b-4dd1-bd05-0a55ce7a7132
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# Hämta och uppdatera exempelappen Web.Travel

Exempelappen We.Travel är förimplementerad med Adobe Mobile Services SDK v4. Du behöver bara uppdatera den så att den pekar på dina egna Experience Cloud-Org- och lösningskonton.

## Utbildningsmål

När lektionen är klar kan du:

* Ladda ned och öppna exempelappen We.Travel i Android Studio
* Verifiera och uppdatera SDK-inställningarna för mobila tjänster för [!DNL Target]

## Ladda ned appen We.Travel

* Hämta [sample-app-android-SDKv4-Base-Version.zip](assets/sample-app-android-SDKv4-Base-Version.zip)
* Dekomprimera zip-filen
* Öppna appen i Android Studio som ett befintligt projekt (ignorera alla fel om&quot;Ogiltig VCS-rotmappning&quot;)
* Kör appen i en emulator för att bekräfta att appen byggs och att du kan se hemskärmen
* Bläddra i appen och verifiera att du kan slutföra bokningsprocessen (välj ett betalningsalternativ och tryck bara på&quot;Fortsätt&quot; för att hoppa över faktureringsskärmen!)

   ![Öppna skärmen ](assets/wetravel_homeScreen.png)![appConfirmation](assets/wetravel_confirmationScreen.png)

## Verifiera och uppdatera SDK-inställningarna för mobila tjänster för [!DNL Target]

Adobe Mobile Services SDK har förinstallerats i appen We.Travel [enligt dokumentationen](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html?lang=en). Nu ska du uppdatera installationen så att den pekar på ditt eget [!DNL Target]-konto.

Skapa först en ny app i användargränssnittet för Mobile Services:

1. Logga in på gränssnittet [Adobe Mobile Services](https://mobilemarketing.adobe.com/).
1. Gå till [!UICONTROL Manage Apps] och klicka sedan på **[!UICONTROL Add]** för att lägga till ett nytt program som ska användas med den här självstudiekursen (**[!UICONTROL Manage Apps]** > **[!UICONTROL Add]**).
1. Välj en analysrapportsserie med icke-produktionsdata, ge appen ett namn, välj typen **[!UICONTROL Standard]** och klicka på **[!UICONTROL Save]**.
1. När appen har lagts till lägger du till din [!DNL Target]-klientkod på nästa skärm i avsnittet [!UICONTROL SDK Target Options] (du hittar din klientkod i gränssnittet [!DNL Target] under **[!UICONTROL Setup]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit Settings]**, bredvid knappen Hämta `at.js`).
1. Inställningen [!UICONTROL Request Timeout] avgör hur länge programmet väntar på svar från [!DNL Target]-servern innan timeout-instruktionerna körs. Lämna bara standardinställningen.
1. Aktivera [!UICONTROL Visitor ID Service] och kontrollera att [!UICONTROL Organization] är markerat i listrutan.
1. Spara ändringarna genom att klicka på **[!UICONTROL Save]** längst upp till höger i fönstret (inte den i [!UICONTROL Universal Links]-, [!UICONTROL App Links]- eller [!UICONTROL Push Services]-avsnittet).
1. Bläddra till hämtningsavsnittet för App SDK längst ned på sidan och hämta konfigurationsfilen:

   ![Hämta konfigurationsfilen](assets/config_file.jpg)

1. Ersätt `ADBMobileConfig.json`-filen i Android Studio-projektresursmappen (app > src > main > resurser).

1. Öppna nu filen `ADBMobileConfig.json` och kontrollera att den innehåller de förväntade ändringarna, som [!DNL Target]-klientkoden och din Analytics-information:
   ![Hämta konfigurationsfilen](assets/client_code.jpg)

Om du inte ser inställningarna bekräftar du att du klickade på den högra **[!UICONTROL Save]**-knappen i [!UICONTROL Mobile Services]-gränssnittet och kopierade filen till rätt plats.

Grattis! Du har uppdaterat SDK:n med din [!DNL Target]-kontoinformation! Vi gör ytterligare validering av konfigurationen när vi lägger till [!DNL Target]-begäranden i nästa lektion.

**[NÄSTA: &quot;Lägg till målförfrågningar&quot; >](add-requests.md)**
