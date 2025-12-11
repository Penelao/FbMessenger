# FbMessenger
## Installazione
- Installare opera
- Installare [tampermonkey](https://addons.opera.com/en/extensions/details/tampermonkey-beta/)
  <img width="1770" height="1191" alt="image" src="https://github.com/user-attachments/assets/037498c6-21e9-4611-a813-0f365c0435e2" />
- Su opera andare nelle estensioni
  <img width="1791" height="924" alt="image" src="https://github.com/user-attachments/assets/d592f08a-b9eb-46dc-bf8f-8229fb03a02d" />
- abilitare la dev mode come da immagine
  <img width="1780" height="276" alt="image" src="https://github.com/user-attachments/assets/e2c8f2f6-4b5c-43ca-8448-d00f9369a7e5" />
- cliccare "dettagli" su Tampermonkey
  <img width="1695" height="708" alt="image" src="https://github.com/user-attachments/assets/0b9d0d64-00be-48d5-911a-2fd535f127d8" />
- in fondo ai dettagli abilitare come da terza immagine
  <img width="1746" height="1548" alt="image" src="https://github.com/user-attachments/assets/35e4751f-3128-46b5-b3ab-97084d751d4c" />
## Setup tampermonkey
- loggare su fb(bisogna avere fb in italiano altrimenti potrebbe esserci qualcosa da sistemare) e andare a questa [pagina](https://www.facebook.com/settings/?tab=blocking)
  <img width="1119" height="1035" alt="image" src="https://github.com/user-attachments/assets/c0549ac2-9461-4d09-bc03-2a5f7bd53039" />
- rimanendo su quella pagina cliccare sull'estensione di tampermonkey
  <img width="951" height="921" alt="image" src="https://github.com/user-attachments/assets/610bbdfc-fd22-42c4-8c7d-ce1a9e765bb0" />
- cliccare crea nuovo script e si aprira una nuova scheda
  <img width="781" height="1173" alt="image" src="https://github.com/user-attachments/assets/ce9745d6-5f37-4cec-9f8f-a3c3e4b58dd5" />
- nell'editor sovrascrivere con il codice qui sotto
  ```js
  // ==UserScript==
  // @name         New Userscript
  // @namespace    http://tampermonkey.net/
  // @version      2025-12-11
  // @description  try to take over the world!
  // @author       You
  // @match        https://www.facebook.com/settings/?tab=blocking
  // @icon         https://www.google.com/s2/favicons?sz=64&domain=facebook.com
  // @grant        none
  // ==/UserScript==
  
  (async function() {
      'use strict';
  
          try{
  	const openDialog = await waitForElm("[aria-label='Modifica configurazione del blocco message']");
  	openDialog.click();
  
  	const dialog = await waitForElm("[role='dialog']:not([aria-label^='Caricamento'])");
  
  	const dialogButtons = await waitForAllElm("[role='button']", dialog, 1);
  
  	dialogButtons[1].click();
  
      const blockButtons = await waitForAllElm("[aria-label='Blocca']");
  	for(const block of blockButtons) {
          console.log("31", block);
  		block.click();
  		const confirm = await waitForElm("[aria-label^='Conferma il blocco']");
  		confirm.click();
          await sleep(1000);
  	}
      location.reload()
      } catch(e) {
         console.log("err", e)
          debugger;
      }
      function sleep(ms) {
      return new Promise(resolve => setTimeout(resolve, ms));
      }
      function waitForElm(selector, target = document) {
      return new Promise(resolve => {
          if (target.querySelector(selector)) {
              return resolve(target.querySelector(selector));
          }
  
          const observer = new MutationObserver(mutations => {
              if (target.querySelector(selector)) {
                  observer.disconnect();
                  resolve(target.querySelector(selector));
              }
          });
  
          // If you get "parameter 1 is not of type 'Node'" error, see https://stackoverflow.com/a/77855838/492336
          observer.observe(target?.body ?? target, {
              childList: true,
              subtree: true
          });
      });
  }
  
  function waitForAllElm(selector, target = document, min=0) {
      console.log("selector", selector);
          console.log("targ", target);
      console.log("min", min);
      return new Promise(resolve => {
          if (target.querySelectorAll(selector).length>min) {
              console.log("subi", target.querySelectorAll(selector));
              return resolve(target.querySelectorAll(selector));
          }
  
          const observer = new MutationObserver(mutations => {
              if (target.querySelectorAll(selector).length>min) {
                  console.log("dopo", target.querySelectorAll(selector));
                  observer.disconnect();
                  resolve(target.querySelectorAll(selector));
              }
          });
  
          // If you get "parameter 1 is not of type 'Node'" error, see https://stackoverflow.com/a/77855838/492336
          observer.observe(target.body ?? target, {
              childList: true,
              subtree: true
          });
      });
  }
  
      // Your code here...
  })();

  ```
- salvare lo script
  <img width="1746" height="1665" alt="image" src="https://github.com/user-attachments/assets/e29360af-8fd7-470f-a9fb-7d89fcd90812" />
- tornare sulla scheda delle impostazioni di facebook del punto prima e aggiornare la pagina(non aprire altre pagine di fb), in automatico dovrebbe iniziare a cliccare blocco messaggi e bloccare gli utenti, solitamente gli utenti sono a gruppo di dieci quindi finito un gruppo dovrebbe ri-aggiornare la pagina e ricominciare fino a quando non trova piu utenti da bloccare se si vede che non si blocca dovrebbe fare da solo e lo si puo lasciare girare se si blocca subito c'e qualcosa di rotto momentaneamente come scritto sotto lo script e riabilitarlo dopo un po'(video allegato su tg)
- una volta completato puoi ricliccare tampermonkey dal menu delle estensioni e disabilitare lo script
  <img width="951" height="921" alt="image" src="https://github.com/user-attachments/assets/610bbdfc-fd22-42c4-8c7d-ce1a9e765bb0" />
  <img width="747" height="1107" alt="image" src="https://github.com/user-attachments/assets/f5d1e6e3-c9c7-4b37-88d9-cfeec47e29f4" />





