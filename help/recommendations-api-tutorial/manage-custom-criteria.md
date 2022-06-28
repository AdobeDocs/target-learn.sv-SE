---
title: Hantera anpassade villkor
description: I den här delen av självstudiekursen får utvecklare hjälp med att använda Adobe Target API:er för att hantera, skapa, lista, redigera, hämta och ta bort villkor för Adobe Target Recommendations.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: ee63bd3e-200a-4c08-b364-9f17a479033b
source-git-commit: cee2618bb92284da1f82d108a0aff0d39340a15b
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Hantera anpassade villkor

Ibland kan algoritmerna som tillhandahålls av [!DNL Recommendations] kan inte visa vissa objekt som du vill befordra. I sådana fall kan du med anpassade kriterier leverera en specifik uppsättning rekommenderade objekt för ett visst nyckelobjekt eller en viss kategori. Du definierar mappningen mellan nyckelobjektet eller kategorin och de rekommenderade objekten och importerar mappningen som ett anpassat villkor. Den här processen beskrivs i [dokumentation om anpassade kriterier](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=en). Så som beskrivs i den dokumentationen kan du skapa, redigera och ta bort anpassade villkor via [!DNL Target] användargränssnitt. Men [!DNL Target] innehåller även en uppsättning API:er för anpassade kriterier som gör att du kan hantera dina anpassade villkor mer ingående.

>[!IMPORTANT]
>
>Följ den här användarhandboken för anpassade villkor:
>
> Gör antingen allt (skapa, redigera, ta bort) för ett visst anpassat villkor med API:erna, eller gör allt (skapa, redigera, ta bort) med gränssnittet. Om du hanterar anpassade villkor med en kombination av användargränssnittet och API:t kan det leda till att information eller oväntade resultat hamnar i konflikt. Om du till exempel skapar ett anpassat villkor i användargränssnittet, men sedan redigerar det via API, återspeglas inte dina uppdateringar i användargränssnittet, även om det uppdateras i serverdelen, vilket visas via API:t.

## Skapa anpassade villkor

Skapa anpassade villkor med [Skapa API för anpassade kriterier](https://developers.adobetarget.com/api/recommendations/#operation/createCriteriaCustom)är syntaxen:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>Anpassade villkor som skapats med API:t Skapa anpassade kriterier, som beskrivs i den här övningen, visas i användargränssnittet där de finns kvar. Du kan inte redigera eller ta bort dem från användargränssnittet. Du kan redigera eller ta bort dem **via API** men hur som helst visas de även i [!DNL Target] Gränssnitt. Om du vill behålla möjligheten att redigera eller ta bort från användargränssnittet skapar du anpassade villkor med användargränssnittet per [dokumentationen](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=en)i stället för att använda Create Custom Criteria API.

Fortsätt bara med den här självstudiekursen när du har läst varningen ovan och är bekväm med att skapa nya anpassade villkor som inte kan tas bort från användargränssnittet.

1. Verifiera `TENANT_ID` och `API_KEY` for **Skapa anpassade villkor** referera till Postman miljövariabler som fastställts tidigare. Använd bilden nedan för att jämföra.

   ![CreateCustomCriteria1](assets/CreateCustomCriteria1.png)

2. Lägg till **Brödtext** as **råformat** JSON som definierar platsen för CSV-filen med anpassade villkor. Använd exemplet i [Skapa API för anpassade kriterier](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom) som en mall, ange `environmentId` och andra värden efter behov. I det här exemplet använder vi LAST_PURCHASED som nyckel.

   ![CreateCustomCriteria2](assets/CreateCustomCriteria2.png)

3. Skicka förfrågan och observera svaret, som innehåller information om de anpassade villkor du just skapade.

   ![CreateCustomCriteria3](assets/CreateCustomCriteria3.png)

4. Navigera i Adobe Target till **[!UICONTROL Recommendations]>[!UICONTROL Criteria]** och söka efter dina kriterier efter namn eller använda **Lista anpassat villkor-API** i nästa steg.

   ![CreateCustomCriteria4](assets/CreateCustomCriteria4.png)

I det här fallet har vi ett fel. Låt oss undersöka felet närmare genom att undersöka anpassade kriterier med hjälp av **Lista anpassat villkor-API**.

## Lista anpassade villkor

Använd [Lista anpassat villkor-API](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom). Syntaxen är:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. Verifiera `TENANT_ID` och `API_KEY` som tidigare och skicka begäran. Observera det anpassade villkors-ID:t i svaret, liksom information om felmeddelandet som nämndes tidigare.
   ![ListCustomCriteria](assets/ListCustomCriteria.png)

I det här fallet uppstod felet eftersom serverinformationen är felaktig, vilket innebär [!DNL Target] kan inte komma åt CSV-filen som innehåller den anpassade villkorsdefinitionen. Låt oss redigera de anpassade villkoren för att korrigera detta.

## Redigera anpassade villkor

Om du vill ändra detaljerna för en anpassad villkorsdefinition använder du [Redigera API för anpassade villkor](https://developers.adobetarget.com/api/recommendations/#operation/updateCriteriaCustom). Syntaxen är:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Verifiera `TENANT_ID` och `API_KEY`, som tidigare.
   ![RedigeraAnpassatKriterium1](assets/EditCustomCriteria1.png)

1. Ange villkor-ID för det (enkla) anpassade villkor som du vill redigera.
   ![RedigeraAnpassatKriterium2](assets/EditCustomCriteria2.png)

1. I Body anger du uppdaterad JSON med rätt serverinformation. (I det här steget anger du FTP-åtkomst till en server som du har åtkomst till.)
   ![RedigeraAnpassatKriterium3](assets/EditCustomCriteria3.png)

1. Skicka förfrågan och notera svaret.
   ![RedigeraAnpassatKriterium4](assets/EditCustomCriteria4.png)

Låt oss kontrollera om de uppdaterade anpassade villkoren har lyckats med **Hämta API för anpassade villkor**.

## Hämta anpassade villkor

Om du vill visa information om anpassade villkor för ett specifikt anpassat villkor använder du [Hämta API för anpassade villkor](https://developers.adobetarget.com/api/recommendations/#operation/getCriteriaCustom). Syntaxen är:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Ange villkor-ID för de anpassade villkor vars information du vill få. Skicka förfrågan och granska svaret.
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. Bekräfta att åtgärden lyckades. (Kontrollera i vårt fall att det inte finns några ytterligare FTP-fel.)
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. (Valfritt) Kontrollera att uppdateringen visas korrekt i användargränssnittet.
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## Ta bort anpassade villkor

Ta bort dina anpassade villkor med hjälp av ID:t som nämndes tidigare med [Ta bort API för anpassade villkor](https://developers.adobetarget.com/api/recommendations/#operation/deleteCriteriaCustom). Syntaxen är:

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Ange kriterier-ID:t för det (enkla) anpassade villkor som du vill ta bort. Klicka **Skicka**.
   ![TaBortAnpassatKriterium1](assets/DeleteCustomCriteria1.png)

1. Kontrollera att villkoren har tagits bort med Hämta anpassade villkor.
   ![TaBortAnpassatKriterium2](assets/DeleteCustomCriteria2.png)
I det här fallet anger det förväntade 404-felet att det inte går att hitta de borttagna villkoren.

>[!NOTE]
>Som en påminnelse tas inte villkoren bort från [!DNL Target] Gränssnittet togs bort eftersom det skapades med API:t Skapa anpassade villkor.

Grattis! Du kan nu skapa, lista, redigera, ta bort och få information om anpassade villkor med hjälp av [!DNL Recommendations] API. I nästa avsnitt använder du [!DNL Target] Leverans-API för att hämta rekommendationer.

[Nästa&quot;Hämta Recommendations med leverans-API:t på serversidan&quot; >](https://developer.adobe.com/target/before-administer/recs-api/fetch-recs-server-side-delivery-api/){target=&quot;_blank&quot;}
