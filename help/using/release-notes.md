---
title: Scopri le novità Note sulla versione - Servizio di conversione automatica dei moduli
description: Scopri le ultime funzionalità e i bug corretti per il servizio di conversione automatica dei moduli
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: forms
role: Admin, Developer
level: Beginner, Intermediate
exl-id: fccafbc9-28c1-4736-922c-24d675b25213
TQID: https://experienceleague.adobe.com/5c2zcJqsjOyH--SIp-DbEyQtflWnBy67-ja0BZY8aC8
product_v2: id: e8f6de9b-cf88-4405-8d10-15efa08c230eid: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
feature_v2: id: d49d6117-dd89-469c-a774-cc96b7eee433
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 0be767cc3d09331ea7a61c114a11bb0354b5f4ad
workflow-type: tm+mt
source-wordcount: 496
ht-degree: 51%

---

# Note sulla versione

Il servizio di conversione automatica dei moduli viene migliorato continuamente. Per rimanere aggiornato sugli ultimi sviluppi, visita questa pagina regolarmente. Questa pagina fornisce informazioni su:

* Accesso anticipato
* Versioni più recenti
* Nuove funzioni
* Miglioramenti
* Correzioni di bug
* Funzionalità obsolete
* Istruzioni speciali
* Modifiche programmate per il futuro

## 24 febbraio 2022 (AFC-2022.02.0) {#feb-2022}

* È stata aggiunta la possibilità a [convertire automaticamente le sezioni in frammenti](convert-existing-forms-to-adaptive-forms.md) per migliorare la velocità di rendering dei moduli convertiti e semplificare il caricamento di moduli di grandi dimensioni nell&#39;editor di moduli adattivi.

## 29 agosto 2021 (AFC-2021.08.0) {#aug-2021}

* È stata aggiunta la possibilità di convertire PDF forms in un modulo adattivo in italiano e portoghese.

## 29 luglio 2021 (AFC-2021.07.2) {#july-2021}

* È stata aggiunta la possibilità di convertire un modulo PDF in francese, tedesco e spagnolo in un modulo adattivo.

## 24 giugno 2021 (AFC-2021.06.2) {#june-2021}

### Miglioramenti {#june-2021-improvements}

È stata migliorata la precisione per il rilevamento automatico delle sezioni logiche nei moduli di origine e la loro conversione nei pannelli dei moduli adattivi corrispondenti.

## 3 marzo 2021 (AFC-2021.02.2) {#mar-2021}

### Miglioramenti {#march-2021-improvements}

Sono stati apportati miglioramenti all’organizzazione del contenuto dei moduli in gruppi di scelta e campi durante la conversione di un modulo di origine in un modulo adattivo.

## 2 febbraio 2021 (AFC-2021.01.2) {#feb-2021}

### Miglioramenti {#feb-2021-improvements}

Sono stati introdotti miglioramenti nell’organizzazione del contenuto dei moduli in pannelli e nella generazione di titoli per i pannelli durante la conversione di un modulo sorgente in un modulo adattivo.

## 16 luglio 2020 (AFC-2020.07.2) {#jul-2020}

### Novità {#whats-new-jul-2020-}

Aggiunto supporto della conversione di moduli PDF a colori in moduli adattivi.

### Miglioramenti {#jul-2020-improvements}

Miglioramenti della conversione automatica dei campi di testo, moduli e gruppi di scelta nei corrispondenti componenti dei moduli adattativi.

## 20 marzo 2020 (AFC-2020.03.1) {#mar-2020}

### Accesso anticipato {#early-access}

**Rilevamento automatico delle sezioni logiche in un modulo**

Per impostazione predefinita, il servizio crea un pannello di primo livello separato per ciascuna pagina di un modulo PDF. Ora è possibile utilizzare l’opzione **[!UICONTROL Auto-detect logical sections]** per eliminare i pannelli a livello di pagina (pannelli basati sul numero di pagina) e creare solo pannelli logici. Questa opzione, inoltre, unisce alla sezione logica precedente i campi che non appartengono ad alcuna sezione e unisce in un’unica sezione logica i campi di una sezione logica suddivisi su due pagine adiacenti. Ad esempio, se alcuni campi di una sezione logica si trovano alla fine della pagina 1 e altri si trovano all’inizio della pagina 2, tutti questi campi sono raggruppati in una singola sezione logica.

### Miglioramenti {#mar-2020-improvements}

**Miglioramenti nel rilevamento degli elenchi**

Il servizio ora è più efficiente nel rilevamento degli elenchi puntati e numerati.

### Istruzioni speciali {#special-instructions}

**Installazione del pacchetto del connettore del servizio di conversione automatica dei moduli**

Per utilizzare le funzioni e i miglioramenti più recenti forniti nella versione AFC-2020.03.1, è necessario il pacchetto del connettore 1.1.38 o versioni successive.

Se disponi già di un ambiente attivo del servizio di conversione automatica dei moduli (AEM 6.5 o AEM 6.5 LTS), per utilizzare le funzioni più recenti del servizio di conversione installa il service pack più recente, il pacchetto del componente aggiuntivo AEM Forms più recente e il pacchetto del connettore più recente nell’ordine indicato. Per AEM Forms as a Cloud Service, gli aggiornamenti vengono consegnati automaticamente. Per istruzioni dettagliate, vedi l’articolo [Configurazione del servizio di conversione automatica dei moduli](configure-service.md).

