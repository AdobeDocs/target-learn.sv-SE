---
title: Hantera anpassade villkor
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations innehåller en dedikerad uppsättning API:er som gör att du kan hantera din katalog med rekommenderade produkter och/eller innehåll. hantera era rekommendationsalgoritmer och -kampanjer, och leverera rekommendationer i JSON-, HTML- och XML-objekt som ska visas i webben, mobiler, e-post, IOT och andra kanaler.
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Adobe Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: 78b30bc0018527f9d8b2a5b50edee86e877d14c7
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 0%

---


# Hantera anpassade villkor

Ibland kan algoritmerna som tillhandahålls av [!DNL Recommendations] inte visa vissa objekt som du vill lyfta fram. I sådana fall kan du med anpassade kriterier leverera en specifik uppsättning rekommenderade objekt för ett visst nyckelobjekt eller en viss kategori. Du definierar mappningen mellan nyckelobjektet eller kategorin och de rekommenderade objekten och importerar mappningen som ett anpassat villkor. Den här processen beskrivs i dokumentationen [för](https://docs.adobe.com/content/help/en/target/using/recommendations/criteria/recommendations-csv.html)anpassade villkor. Som du kan se i den dokumentationen kan du skapa, redigera och ta bort anpassade villkor via [!DNL Target] användargränssnittet. Det finns dock [!DNL Target] även en uppsättning API:er för anpassade kriterier som gör att du kan hantera dina anpassade villkor mer ingående.

>[!IMPORTANT]
>
>Följ den här användarhandboken för anpassade villkor:
>
> Gör antingen allt (skapa, redigera, ta bort) för ett visst anpassat villkor med API:erna, eller gör allt (skapa, redigera, ta bort) med gränssnittet. Om du hanterar anpassade villkor med en kombination av användargränssnittet och API:t kan det leda till att information eller oväntade resultat hamnar i konflikt. Om du till exempel skapar ett anpassat villkor i användargränssnittet, men sedan redigerar det via API, återspeglas inte dina uppdateringar i användargränssnittet, även om det uppdateras i serverdelen, vilket visas via API:t.

## Skapa anpassade villkor

Om du vill skapa anpassade villkor med API:t [för](https://developers.adobetarget.com/api/recommendations/#operation/createCriteriaCustom)Skapa anpassade kriterier är syntaxen:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>Anpassade villkor som skapats med API:t Skapa anpassade kriterier, som beskrivs i den här övningen, visas i användargränssnittet där de finns kvar. Du kan inte redigera eller ta bort dem från användargränssnittet. Du kan redigera eller ta bort dem **via API**, men på båda sätten visas de i [!DNL Target] användargränssnittet. Om du vill behålla möjligheten att redigera eller ta bort från användargränssnittet skapar du anpassade villkor med användargränssnittet enligt [dokumentationen](https://docs.adobe.com/content/help/en/target/using/recommendations/criteria/recommendations-csv.html), i stället för att använda API:t Skapa anpassade kriterier.

Fortsätt bara med den här självstudiekursen när du har läst varningen ovan och är bekväm med att skapa nya anpassade villkor som inte kan tas bort från användargränssnittet.

1. Verifiera `TENANT_ID` och `API_KEY` för **Skapa anpassade villkor** refererar du till Postman-miljövariablerna som etablerats tidigare. Använd bilden nedan för att jämföra.

   ![CreateCustomCriteria1](assets/CreateCustomCriteria1.png)

2. Lägg till din **Body** som **rå** JSON som definierar platsen för den anpassade CSV-villkorsfilen. Använd exemplet i [Skapa API](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom) för anpassade kriterier som mall och ange dina `environmentId` och andra värden efter behov. I det här exemplet använder vi LAST_PURCHASED som nyckel.

   ![CreateCustomCriteria2](assets/CreateCustomCriteria2.png)

3. Skicka förfrågan och observera svaret, som innehåller information om de anpassade villkor du just skapade.

   ![CreateCustomCriteria3](assets/CreateCustomCriteria3.png)

4. Om du vill verifiera att dina anpassade villkor har skapats går du till **[!UICONTROL Recommendations]>[!UICONTROL Criteria]**i Adobe Target och söker efter villkoren efter namn, eller använder API:t för **listanpassade villkor**i nästa steg.

   ![CreateCustomCriteria4](assets/CreateCustomCriteria4.png)

I det här fallet har vi ett fel. Låt oss undersöka felet närmare genom att undersöka de anpassade villkoren med API:t för **anpassade kriterier**.

## Lista anpassade villkor

Om du vill hämta en lista över alla anpassade villkor tillsammans med information för varje, använder du API:t för [anpassade villkor](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom). Syntaxen är:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. Kontrollera `TENANT_ID` och `API_KEY` som tidigare och skicka begäran. Observera det anpassade villkors-ID:t i svaret, liksom information om felmeddelandet som nämndes tidigare.
   ![ListCustomCriteria](assets/ListCustomCriteria.png)

I det här fallet inträffade felet eftersom serverinformationen är felaktig, vilket innebär att det inte [!DNL Target] går att komma åt CSV-filen som innehåller den anpassade villkorsdefinitionen. Låt oss redigera de anpassade villkoren för att korrigera detta.

## Redigera anpassade villkor

Om du vill ändra informationen för en anpassad villkorsdefinition använder du API:t för [anpassade villkor](https://developers.adobetarget.com/api/recommendations/#operation/updateCriteriaCustom). Syntaxen är:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Verifiera `TENANT_ID` och `API_KEY`, som förut.
   ![EditCustomCriteria1](assets/EditCustomCriteria1.png)

1. Ange villkor-ID för det (enkla) anpassade villkor som du vill redigera.
   ![EditCustomCriteria2](assets/EditCustomCriteria2.png)

1. I Body anger du uppdaterad JSON med rätt serverinformation. (I det här steget anger du FTP-åtkomst till en server som du har åtkomst till.)
   ![EditCustomCriteria3](assets/EditCustomCriteria3.png)

1. Skicka förfrågan och notera svaret.
   ![EditCustomCriteria4](assets/EditCustomCriteria4.png)

Låt oss kontrollera om de uppdaterade anpassade villkoren har lyckats med hjälp av API:t **Hämta anpassade kriterier**.

## Hämta anpassade villkor

Om du vill visa information om anpassade villkor för ett specifikt anpassat villkor använder du API:t för [Hämta anpassade villkor](https://developers.adobetarget.com/api/recommendations/#operation/getCriteriaCustom). Syntaxen är:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Ange villkor-ID för de anpassade villkor vars information du vill få. Skicka förfrågan och granska svaret.
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. Bekräfta att åtgärden lyckades. (Kontrollera i vårt fall att det inte finns några ytterligare FTP-fel.)
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. (Valfritt) Kontrollera att uppdateringen visas korrekt i användargränssnittet.
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## Ta bort anpassade villkor

Ta bort anpassade villkor med API:t [Ta bort anpassade kriterier med hjälp av kriterier-ID:t](https://developers.adobetarget.com/api/recommendations/#operation/deleteCriteriaCustom)som beskrivs ovan. Syntaxen är:

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Ange kriterier-ID:t för det (enkla) anpassade villkor som du vill ta bort. Klicka på **Skicka**.
   ![DeleteCustomCriteria1](assets/DeleteCustomCriteria1.png)

1. Kontrollera att villkoren har tagits bort med Hämta anpassade villkor.
   ![DeleteCustomCriteria2](assets/DeleteCustomCriteria2.png)I det här fallet anger det förväntade 404-felet att det inte går att hitta de borttagna villkoren.

>[!NOTE]
>Som en påminnelse tas villkoren inte bort från [!DNL Target] användargränssnittet även om det togs bort, eftersom det skapades med API:t Skapa anpassade kriterier.

Grattis! Du kan nu skapa, lista, redigera, ta bort och få information om anpassade villkor med hjälp av [!DNL Recommendations] API:t. I nästa avsnitt använder du API:t för [!DNL Target] leverans för att hämta rekommendationer.

[Nästa&quot;Hämta Recommendations med leverans-API:t på serversidan&quot; >](fetch-recs-server-side-delivery-api.md)
