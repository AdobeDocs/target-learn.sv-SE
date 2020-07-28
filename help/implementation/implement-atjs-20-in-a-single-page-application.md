---
title: Implementera Adobe Target.js 2.0 i ett Single Page Application (SPA)
seo-title: Implementera Adobe Target.js 2.0 i ett Single Page Application (SPA)
description: Den senaste versionen av at.js innehåller många funktioner som gör det möjligt för ditt företag att utföra personalisering på nästa generations klienttekniker. Den nya versionen fokuserar på att uppgradera at.js för att få harmonisk interaktion med Single page applications (SPA).
audience: developer
difficulty: 3
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: 37443ae4c1cdda387c8db0053201d520fa1ec224
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# Implementera Adobe Target.js 2.0 i ett Single Page Application (SPA)

Den senaste versionen av `at.js` innehåller många funktioner som gör det möjligt för ditt företag att utföra personalisering på nästa generations klienttekniker. Den nya versionen fokuserar på uppgradering `at.js` för att få harmonisk interaktion med applikationer för en enda sida (SPA).

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## Implementera at.js 2.0 i en SPA

* Implementera `at.js` 2.0 i &lt;head> i Single Page-programmet.
* Implementera `adobe.target.triggerView()` funktionen när du visar ändringar i SPA-filen. Du kan använda olika tekniker för att göra detta, t.ex. avlyssna ändringar i URL-hash, lyssna efter anpassade händelser som utlösts av SPA eller bädda in `triggerView()` koden direkt i programmet. Du bör välja det alternativ som fungerar bäst för ditt specifika enkelsidiga program.
* Vynamnet är den första parametern i `triggerView()` funktionen. Använd enkla, tydliga och unika namn för att göra dem enkla att välja i Target visuella upplevelsedisposition.
* Du kan utlösa vyer i små vyändringar, liksom i andra sammanhang än SPA, t.ex. halvvägs nedåt och en oändlig rullningssida.
* `at.js` 2.0 och `triggerView()` kan implementeras via en tagghanteringslösning som Adobe Experience Platform Launch.

## at.js 2.0 Begränsningar

Tänk på följande begränsningar i `at.js` 2.0 innan du uppgraderar:

* Spårning över flera domäner stöds inte i `at.js` 2.0
* Parametrarna mboxOverride.browserIp och mboxSession URL stöds inte i `at.js` 2.0
* De gamla funktionerna mboxCreate, mboxDefine, mboxUpdate är borttagna i `at.js` 2.0. Standardinnehåll visas och inga nätverksbegäranden görs.

## Bibliotekets sidfotskod som används i videon

Koden nedan lades till i bibliotekets sidfot i `at.js` biblioteket under videon. Det aktiveras när appen först läses in och sedan när någon hash-ändring görs i appen. Den använder en rensad version av hash som visningsnamn och&quot;home&quot; när hash-filen är tom. Observera att koden söker efter texten&quot;reagerar/&quot; i URL:en för att identifiera SPA:n, som troligen behöver uppdateras på webbplatsen. Tänk också på att det kan vara lämpligare för din SPA att avaktivera anpassade händelser `triggerView()` eller genom att bädda in koden direkt i din app.

```javascript
function sanitizeViewName(viewName) {
  if (viewName.startsWith('#')) {
    viewName = viewName.substr(1);
  }
  if (viewName.startsWith('/')) {
    viewName = viewName.substr(1);
  }
  return viewName;
}
function triggerView(viewName) {
  viewName = sanitizeViewName(viewName) || 'home';
  // Validate if the Target Libraries are available on your website
  if (typeof adobe != 'undefined' && adobe.target && typeof adobe.target.triggerView === 'function') {
    adobe.target.triggerView(viewName);
    console.log('AT: View triggered on page load: '+viewName)
  }
}
//fire triggerView when the SPA loads and when the hash changes in the SPA
if(window.location.pathname.indexOf('react/') >-1){
    triggerView(location.hash);
}
window.onhashchange = function() {
    if(window.location.pathname.indexOf('react/') >-1){
        triggerView(location.hash);
    }
}
```

## Ytterligare resurser

* [Understanding How at.js 2.0 Works (Architecture Diagrams)](understanding-how-atjs-20-works.md)
* [Använd Adobe Target Visual Experience Composer för Single Page-program (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [Uppgradera från dokumentationen för at.js 1.x till at.js 2.0](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/upgrading-from-atjs-1x-to-atjs-20.html)