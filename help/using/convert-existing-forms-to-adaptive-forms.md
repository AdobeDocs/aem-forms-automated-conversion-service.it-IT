---
title: Conversione di PDF forms in moduli adattivi
description: Eseguire il servizio di conversione automatica dei moduli (AFCS) per convertire PDF forms in moduli adattivi
feature: Adaptive Forms, Foundation Components
role: Admin, Developer
level: Beginner, Intermediate
source-git-commit: 02e808d6d777078d148f073835e24fd20712eade
workflow-type: tm+mt
source-wordcount: '1783'
ht-degree: 8%

---

# Conversione di PDF forms in moduli adattivi {#convert-print-forms-to-adaptive-forms}

Il servizio AFCS (Automated Forms Conversion Service) di AEM Forms, basato su Adobe Sensei, converte automaticamente il PDF forms in moduli adattivi facili da usare e reattivi<!--foundation and [core components](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction)-->. Che si utilizzi PDF forms non interattivo, Acro Forms o PDF forms basato su XFA, il servizio AFCS (Automated Forms Conversion Service) può facilmente convertire questi moduli in moduli adattivi. Per informazioni sulle funzionalità, sul flusso di lavoro di conversione e sulle informazioni di onboarding, consulta il servizio [Automated Forms Conversion](introduction.md).

## Prerequisiti {#pre-requisites}

* [**Configura il servizio di conversione**](configure-service.md)

* **Prepara i [modelli](https://helpx.adobe.com/experience-manager/6-5/forms/using/template-editor.html) da applicare ai moduli convertiti:** L&#39;utilizzo di un modello consente di applicare un branding coerente in tutti i moduli adattivi. Inoltre, il servizio di conversione automatica dei moduli (AFCS) non estrae e utilizza l’intestazione e il piè di pagina dei documenti PDF di origine. È possibile utilizzare modelli di modulo adattivi per specificare intestazione e piè di pagina. L’intestazione e il piè di pagina specificati nel modello vengono applicati al modulo adattivo durante la conversione. Quando si crea una cartella per i modelli, selezionare l&#39;opzione **[!UICONTROL Browse configurations]** per tutti.

* **Prepara i [temi](https://helpx.adobe.com/experience-manager/6-5/forms/using/themes.html) da applicare ai moduli convertiti:** L&#39;utilizzo di un tema consente di applicare uno stile coerente a tutti i moduli adattivi dell&#39;organizzazione.

* **(facoltativo)** [**Converti il PDF forms di origine nel modulo Adobe Sign**](frequently-asked-questions.md)

## Avviare il processo di conversione {#start-the-conversion-process}

Dopo aver connesso l’istanza di AEM con AEM Forms Conversion Service, puoi convertire il PDF forms in moduli adattivi. Per convertire i moduli, effettuare le seguenti operazioni nell&#39;ordine indicato:

* [Carica PDF forms sul server AEM Forms](convert-existing-forms-to-adaptive-forms.md#upload-pdf-forms-to-your-aem-forms-server)
* [Eseguire la conversione](convert-existing-forms-to-adaptive-forms.md#run-the-conversion)
* [Rivedere e correggere i moduli convertiti](review-correct-ui-edited.md)

### Carica PDF forms sul server AEM Forms {#upload-pdf-forms-to-your-aem-forms-server}

Il servizio di conversione converte i PDF forms disponibili nell’istanza AEM Forms in moduli adattivi. Se necessario, puoi caricare tutti i PDF forms contemporaneamente o in modo graduale. Prima di caricare i moduli, considera quanto segue:

* Mantenere il numero di moduli in una cartella inferiore a 15 e il numero totale di pagine in una cartella inferiore a 50.
* Mantieni le dimensioni della cartella inferiori a 10 MB. Non mantenere i moduli in una sottocartella.
* Mantieni il numero di pagine in un modulo inferiore a 15.
* Non caricare i moduli protetti. Il servizio non converte i moduli protetti da password e protetti.
* Non caricare moduli di origine con spazi nel nome file. Rimuovere lo spazio dal nome del file prima di caricare i moduli.
* Non caricare [portfolio PDF](https://helpx.adobe.com/it/acrobat/using/overview-pdf-portfolios.html). Il servizio non converte un Portfolio PDF in un modulo adattivo.
* Leggi le sezioni [Problemi noti](known-issues.md) e [Best practice e considerazioni](styles-and-pattern-considerations-and-best-practices.md) e apporta modifiche consigliate ai moduli.

Per caricare i moduli da convertire in una cartella nell’istanza AEM Forms, effettua le seguenti operazioni:

1. Accedi all’istanza di AEM Forms.
1. Toccare **[!UICONTROL Adobe Experience Manager]** ![](assets/adobeexperiencemanager.png) > **[!UICONTROL Navigation]** ![](assets/compass.png) > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Toccare **[!UICONTROL Create]**> **[!UICONTROL Folder]**. Specificare **Titolo** e **Nome** della cartella. Toccare **[!UICONTROL Create]**. Viene creata una cartella.
1. Tocca per aprire la cartella appena creata.
1. Toccare **[!UICONTROL Create]**> **[!UICONTROL File Upload]**. Selezionare i moduli da caricare, fare clic su **[!UICONTROL Open]** e quindi su **[!UICONTROL Upload]**. I moduli vengono caricati.

### Eseguire la conversione {#run-the-conversion}

Dopo aver caricato i moduli e configurato il servizio, effettua le seguenti operazioni per avviare la conversione:

1. Nell&#39;istanza di AEM Forms, toccare **[!UICONTROL Adobe Experience Manager]** ![Finestra di dialogo Impostazioni conversione](assets/adobeexperiencemanager.png) > **[!UICONTROL Navigation]** ![](assets/compass.png) > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Selezionare un modulo o la cartella contenente PDF forms (moduli da convertire) e toccare **[!UICONTROL Start Automated Conversion]**. Viene visualizzata la finestra di dialogo **[!UICONTROL Conversion Settings]**.

   ![Specificare le configurazioni](assets/conversion-settings-dialog.png)

   **Conversione di PDF in componenti core modulo adattivo**

   <span class="preview"> Questa funzione si trova nel programma per i primi utilizzatori. Per partecipare al programma per i primi utilizzatori, richiedi l’accesso alla funzionalità inviando una e-mail dal tuo account ufficiale all’indirizzo aem-forms-ea@adobe.com. </span>

   Per convertire PDF forms in moduli basati su Foundation è necessaria l&#39;impostazione di conversione sopra riportata. Per convertire un modulo PDF in un modulo adattivo basato su Componenti core:

   1. Verifica di aver abilitato [Componenti core](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/introduction) nell&#39;istanza di AEM Forms. Se non è abilitato, puoi [abilitare i componenti core nel tuo ambiente AEM 6.5](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/forms/adaptive-forms-core-components/enable-adaptive-forms-core-components) o [Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/enable-adaptive-forms-core-components).
   1. Seleziona un tema e un modello di modulo adattivo basato su [Componenti core](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components) come illustrato nell&#39;immagine seguente:
      ![Seleziona modello di modulo adattivo](assets/select-af-template-1.png).
   1. Tocca **[!UICONTROL Start Conversion]** per convertire il PDF in un modulo basato su Componenti core.
   >[!NOTE]
   > * Proprietà come l’associazione dati o lo schema del modello dati non sono disponibili per i moduli adattivi basati su componenti core, ma sono disponibili anche per i componenti di base.
   > * [I moduli convertiti](#review-and-correct-the-converted-forms) non sono stati revisionati e corretti perché non sono disponibili per i moduli basati su componenti core.


1. Nella scheda **[!UICONTROL Basic]** della finestra di dialogo Impostazioni di conversione:

   * **[!UICONTROL Select a cloud configuration]**. Quando selezioni una configurazione, sono già specificati il modello e il tema predefiniti. Se necessario, puoi specificare un modello o un tema diverso.
   * Specifica una posizione in cui salvare i moduli adattivi generati e lo schema corrispondente. È possibile utilizzare percorsi predefiniti o specificare percorsi personalizzati.
   * Utilizza l&#39;opzione **Genera moduli adattivi senza associazioni del modello dati** per selezionare se desideri generare un modulo adattivo con o senza associazioni al modello dati.
Se non selezioni questa opzione, il servizio di conversione associa automaticamente i moduli adattivi a uno schema JSON e crea un’associazione dati tra i campi disponibili nel modulo adattivo e lo schema JSON. Nel campo **[!UICONTROL Save generated data model schema at]** viene visualizzata la posizione predefinita per il salvataggio dello schema JSON generato. Puoi anche personalizzare la posizione per salvare lo schema generato.
Se selezioni questa opzione, il servizio di conversione genera un modulo adattivo senza associazioni del modello di dati. Dopo una conversione riuscita, puoi associare un modulo adattivo a un modello dati modulo, a uno schema XML o a uno schema JSON. Per ulteriori informazioni, consulta [Creazione di un modulo adattivo](https://helpx.adobe.com/experience-manager/6-5/forms/using/creating-adaptive-form.html).

   <!--

   Comment Type: draft

   <note type="note">
   <p>The XDP or XFA-based PDF form is not used to generate the Document of Record. The conversion service auto-generates the Document of Record only if you enable the Tools &gt; Cloud Services &gt; Automated Forms Conversion Configuration &gt; <strong>&lt;Properties of selected configuration&gt; &gt;</strong> Advanced &gt; Generate Document of Record option.</p>
   <p> </p>
   </note>
   -->

1. Nella scheda **[!UICONTROL Additional]** della finestra di dialogo Impostazioni di conversione,
   * Selezionare l&#39;opzione **[!UICONTROL Extract fragment from adaptive forms]** per consentire al servizio di conversione di identificare, estrarre e scaricare frammenti di modulo per i moduli convertiti. Quando si seleziona l&#39;opzione **[!UICONTROL Extract fragment from adaptive forms]**, le opzioni per specificare i percorsi per il salvataggio dei frammenti di modulo estratti e degli schemi di frammenti di modulo corrispondenti sono abilitate.
   * Specifica il percorso di **[!UICONTROL existing adaptive form fragments]**, se disponi di alcuni frammenti di moduli adattivi basati su schema JSON e meno adattivi a livello di schema e intendi utilizzarli in moduli adattivi generati automaticamente. Il servizio di conversione rileva la presenza di frammenti di moduli adattivi basati su schema JSON disponibili e meno adattivi dallo schema con PDF forms di input (solo PDF forms non interattivo). In caso di corrispondenza, nei moduli adattivi corrispondenti viene utilizzato il frammento di modulo adattivo corrispondente.

   >[!NOTE]
   >
   >
   > * È possibile utilizzare solo l&#39;opzione **[!UICONTROL  Extract Fragment]** o **[!UICONTROL Use existing adaptive form fragments]** alla volta. Non è possibile utilizzare entrambe le opzioni contemporaneamente.
   > * È possibile utilizzare l&#39;opzione **[!UICONTROL Use existing adaptive form fragments]** solo con PDF forms non interattivo. Altri tipi di modulo non sono ancora supportati.
   > * Con il servizio di conversione automatica è possibile utilizzare solo frammenti non associati o frammenti associati a uno schema JSON. Non utilizzare frammenti XFA. Frammenti XFA non supportati.
   >

   * Selezionare l&#39;opzione **[!UICONTROL Auto-detect multi-column layout of input forms]** per mantenere il layout del modulo di origine per schermi di grandi dimensioni, come desktop e notebook. Questa opzione è utile per mantenere il layout a più colonne dei moduli di origine. Ad esempio, quando un PDF di origine ha un layout a due colonne, il servizio genera un modulo adattivo di output con un layout a due colonne per schermi di grandi dimensioni e un layout a una colonna per dispositivi con schermo di piccole dimensioni come i telefoni cellulari. La funzione presenta alcuni problemi noti con la struttura dello schema dell’origine dati. Per informazioni dettagliate, consulta l&#39;articolo [problemi noti](known-issues.md).
   * Per impostazione predefinita, il servizio crea un pannello di primo livello separato per ciascuna pagina di un modulo PDF. È ora possibile utilizzare l&#39;opzione **[!UICONTROL Auto-detect logical sections]** per non creare pannelli a livello di pagina (pannelli basati sul numero di pagina) e creare solo pannelli logici. Questa opzione, inoltre, unisce alla sezione logica precedente i campi che non appartengono ad alcuna sezione e unisce in un’unica sezione logica i campi di una sezione logica suddivisi su due pagine adiacenti. Ad esempio, se alcuni campi di una sezione logica si trovano alla fine della pagina 1 e altri si trovano all’inizio della pagina 2, tutti questi campi sono raggruppati in una singola sezione logica.

     >[!NOTE]
     > Per utilizzare la funzione **[!UICONTROL Auto-detect logical sections]** è necessario il pacchetto del connettore 1.1.38 o versioni successive.

* (Solo per AEM Forms as a Cloud Service) L&#39;opzione [Converti automaticamente sezioni in frammenti] si applica a PDF forms con più di 15 pagine. Converte le sezioni di primo livello rilevate in frammenti. Inoltre, consente il caricamento lento di tutti i frammenti creati. Consente di migliorare la velocità di rendering dei moduli convertiti e di caricare più facilmente i moduli di grandi dimensioni nell’editor di moduli adattivi.

  >[!NOTE]
  > Non utilizzare il modello di layout dinamico quando si utilizza l’opzione Converti automaticamente sezioni in frammenti.
  > Utilizza l’editor di revisione e correzione per unire i pannelli di piccole dimensioni a uno di grandi dimensioni. Consente di ridurre il numero di frammenti nel modulo adattivo convertito.
  > Se si verifica l’eccezione &quot;Troppe chiamate&quot;,
  >
  > * ristrutturare il modulo per creare una gerarchia semplificata
  > * [aumenta il valore del parametro sling.max.calls]a un numero sufficiente finché l&#39;eccezione non scompare.
  > * [aumentare le dimensioni della cache](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/configure-aem-forms/configure-adaptive-forms-cache.html). L&#39;errore si verifica se il modulo è troppo complesso, presenta un numero elevato di tabelle e una struttura gerarchica a più livelli.

1. Toccare **[!UICONTROL Start Conversion]**. La conversione viene avviata. L’avanzamento della conversione viene visualizzato nella cartella o nel modulo fino a quando la conversione non è in corso. Al termine della conversione, il messaggio viene sostituito da un altro messaggio di stato (Convertito, Parzialmente convertito o Conversione non riuscita). Al termine della conversione, sull’indirizzo e-mail configurato viene inviato anche un messaggio e-mail di stato:

   * In caso di conversione corretta, il modulo adattivo convertito e lo schema correlato vengono scaricati nel percorso specificato nella scheda **[!UICONTROL Basic]** della finestra di dialogo di conversione. I frammenti di modulo e lo schema corrispondente vengono scaricati solo se l’opzione Estrai frammento è selezionata prima di avviare la conversione.
   * In caso di conversione non riuscita, il messaggio **[!UICONTROL Conversion Failed]** viene visualizzato se la conversione di tutti i moduli di input non riesce oppure se il messaggio **[!UICONTROL Partially Failed]** viene visualizzato quando solo alcuni di tutti i moduli di input non riescono a eseguire la conversione. Un&#39;e-mail di stato viene inviata al [indirizzo e-mail configurato](configure-service.md#configureemailnotification) e un errore viene registrato nel file error.log.

   Se si converte un modulo PDF basato su XFA in un modulo adattivo, il servizio di conversione associa automaticamente il modulo PDF al modulo adattivo convertito come modello del documento di record. Dopo la conversione, puoi aprire le proprietà del modulo adattivo per visualizzare il modello del documento record nella sezione **[!UICONTROL Document of Record Template Configuration]** della scheda **[!UICONTROL Form Model]**. </br>

   Il servizio di conversione carica automaticamente il modulo PDF nel modulo adattivo convertito come modello del documento di record solo se si abilita l&#39;opzione **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** > **[!UICONTROL Properties of selected configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL Generate Document of Record]**.

   <!--

   Comment Type: draft

   <note type="note">
   <p>By default, the adaptive form produces a JSON schema instead of XML schema on submission. JSON schema of a converted adaptive form is complaint with XML schema of an XFA-based form. You can use the <a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString">org.apache.sling.commons.json.xml API</a> to convert a JSON schema to XML schema. You can also use the following sample code for conversion:</p>
   <p><code class="code">import org.apache.sling.commons.json.JSONException;
   <discoiqbr /> import org.apache.sling.commons.json.JSONObject;
   <discoiqbr /> import org.apache.sling.commons.json.xml.XML;
   <discoiqbr />
   <discoiqbr /> public class ConversionUtils {
   <discoiqbr />
   <discoiqbr /> public static String jsonToXML(String jsonString) throws JSONException {
   <discoiqbr /> //https://sling.apache.org/apidocs/sling5/org/apache/sling/commons/json/xml/XML.html#toString(java.lang.Object)
   <discoiqbr /> //jar - http://maven.ibiblio.org/maven2/org/apache/sling/org.apache.sling.commons.json/2.0.18/
   <discoiqbr /> //Note: Need to extract boundData part before converting to XML
   <discoiqbr /> return XML.toString(new JSONObject(jsonString));
   <discoiqbr /> }
   <discoiqbr /> }</code><br /> </p>
   </note>
   -->

   >[!NOTE]
   >
   >Se il processo di conversione richiede più di 60 minuti e il modulo PDF non viene ancora convertito in un modulo adattivo, crea una cartella nell’istanza AEM Forms, carica il modulo PDF nella cartella appena creata e riavvia la conversione.

## Rivedere e correggere i moduli convertiti {#review-and-correct-the-converted-forms}

I moduli del mondo reale hanno requisiti di acquisizione dati complessi. Una volta completata la conversione automatica, i clienti possono rivedere la qualità della conversione del modulo e apportare i necessari aggiornamenti al modulo. AEM Forms fornisce un editor di [revisione e correzione](review-correct-ui-edited.md) per apportare le modifiche necessarie. Consente di migliorare l’identificazione automatica dei campi modulo e di convertire i campi identificati da un tipo all’altro. È ad esempio possibile identificare il layout a due colonne di un modulo e modificare un campo identificato automaticamente come pulsante di scelta in un campo a più scelte.
