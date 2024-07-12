---
title: Generare documenti di record durante la conversione
description: Percorsi consigliati per generare un DoR in base al tipo di moduli di origine utilizzati per la conversione.
solution: Experience Manager Forms
feature: Adaptive Forms
topic: Administration
topic-tags: forms
role: Admin, Developer
level: Beginner, Intermediate
page-status-flag: never-activated
contentOwner: khsingh
exl-id: c24313cd-2b9b-4209-9505-a8e14d8dc530
source-git-commit: c2392932d1e29876f7a11bd856e770b8f7ce3181
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---

# Workflow di abilitazione della generazione di documenti di record consigliati per i moduli adattivi {#recommended-workflows-dor-generation}

Il documento di record (DoR) consente di conservare una registrazione delle informazioni fornite e di inviarle in un modulo adattivo in modo da potervi fare riferimento in un secondo momento.
Il DoR utilizza un modello base per definirne il layout. Puoi generare un DoR utilizzando un modello predefinito o associando qualsiasi altro modello al modulo adattivo.

![Documento di record generato](assets/document_of_record.gif)

Per ulteriori informazioni sulla generazione di un documento record, vedere [Generate Document of Record for adaptive forms](https://helpx.adobe.com/experience-manager/6-5/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.html).

Il servizio di Automated forms conversion [ (AFCS)](/help/using/introduction.md) converte i seguenti moduli di origine in moduli adattivi:

* PDF forms non interattivi
* Acro Forms
* PDF forms basati su XFA

In base al modulo di origine utilizzato per la conversione, è possibile generare un documento record utilizzando:

* un modello predefinito
* modulo di origine come modello: se selezioni questa opzione, il servizio di conversione associa automaticamente il modulo di origine al modulo adattivo convertito come modello DoR.
* associa qualsiasi altro modello al modulo adattivo convertito

Nella tabella seguente viene illustrato un esempio dell&#39;effetto del modello DoR utilizzato sul layout del DoR generato:

<table> 
 <tbody>
 <tr>
  <td><p><strong>Source Form</strong></p></td>
  <td><p><strong>DoR generato</strong></p></td> 
   </tr>
  <tr>
   <td><img src="assets/source_xdp_updated.png"/></td>
   <td><p>Se si utilizza il modello predefinito per generare DoR:</br><img src="assets/source_form_default_updated.png"/></td>
   </tr>
   <tr>
   <td></td>
   <td><p>Se si utilizza il modulo di origine come modello per generare DoR:</br></p><img src="assets/source_form_dor_updated.png"/></td>
   </tr>
  </tbody>
</table>

Come illustrato nella tabella, se si utilizza il modulo di origine come modello, il DoR mantiene il layout del modulo di origine.
Questo articolo descrive i percorsi consigliati per generare un DoR basato sui tre tipi di moduli di origine.

<table> 
 <tbody> 
  <tr> 
   <th><strong>Source Form</strong></th> 
   <th><strong>Metodi per generare il DoR</strong></th> 
  </tr> 
  <tr> 
   <td><p>PDF forms non interattivi</p></td> 
   <td> 
    <ul> 
     <li><a href="#generate-document-of-record-using-cloud-configuration">Abilita la generazione DoR prima della conversione del modulo adattivo per generare DoR utilizzando un modello predefinito</a></li> 
     <li><a href="#edit-adaptive-form-properties-generate-document-of-record">Modifica le proprietà del modulo adattivo dopo la conversione del modulo adattivo per abilitare la generazione DoR utilizzando l’impostazione predefinita o qualsiasi altro modello di modulo</a></li> 
    </ul> </td> 
  </tr>
  <tr> 
   <td><p>Acro Forms o PDF forms basati su XFA</p></td> 
   <td> 
    <ul> 
     <li><a href="#use-input-form-as-template-to-generate-document-of-record">Abilita la generazione DoR prima della conversione del modulo adattivo per generare DoR utilizzando il modulo di origine come modello</a></li> 
     <li><a href="#edit-adaptive-form-properties-to-generate-document-of-record">Modifica le proprietà del modulo adattivo dopo la conversione del modulo adattivo per abilitare la generazione DoR utilizzando il modello predefinito, il modulo di origine come modello o qualsiasi altro modello di modulo</a></li> 
    </ul> </td> 
  </tr>    
 </tbody> 
</table>

## Genera documento di record per PDF forms non interattivi {#generate-document-of-record-non-interactive-pdf}

Se si utilizza un modulo di PDF non interattivo come modulo di origine per il servizio di Automated forms conversion (AFCS), è possibile:

* abilitare la generazione DoR prima della conversione del modulo adattivo per generare DoR utilizzando un modello predefinito
* o modificare le proprietà dei moduli adattivi dopo la conversione dei moduli adattivi per abilitare la generazione DoR utilizzando l’impostazione predefinita o qualsiasi altro modello di modulo

### Abilita generazione DoR prima della conversione per generare DoR utilizzando il modello predefinito {#generate-document-of-record-using-cloud-configuration}

1. Selezionare **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** > Proprietà della configurazione cloud utilizzata per la conversione > **[!UICONTROL Advanced]** > opzione **[!UICONTROL Generate Document of Record]**.

   ![Genera documento di record utilizzando la configurazione cloud](assets/generate_dor_cloud_config.gif)

1. Tocca **[!UICONTROL Save & Close]** per salvare le impostazioni.

1. [Esegui la conversione](/help/using/convert-existing-forms-to-adaptive-forms.md). Assicurati di utilizzare la configurazione cloud modificata nel passaggio 1 di queste istruzioni.
All’invio del modulo adattivo convertito, il DoR viene generato automaticamente utilizzando il modello predefinito.

### Modifica le proprietà del modulo adattivo dopo la conversione per abilitare la generazione DoR {#edit-adaptive-form-properties-generate-document-of-record}

Se non abiliti la generazione DoR prima di convertire il modulo di origine in un modulo adattivo, puoi comunque farlo dopo la conversione.

1. [Esegui la conversione](/help/using/convert-existing-forms-to-adaptive-forms.md) nel modulo PDF non interattivo per generare un modulo adattivo.

1. Seleziona il modulo adattivo nella cartella **[!UICONTROL output]** e tocca **[!UICONTROL Properties]**.

1. Nella scheda **[!UICONTROL Form Model]**, espandere la sezione **[!UICONTROL Document of Record Template Configuration]** e selezionare **[!UICONTROL Generate Document of Record]**.

   ![Genera documento di record](assets/generate_dor_af_properties.png)

1. Tocca **[!UICONTROL Save & Close]** per salvare le impostazioni.

All’invio del modulo adattivo convertito, il DoR viene generato automaticamente utilizzando il modello predefinito. Se si desidera associare qualsiasi altro modello DoR al modulo adattivo convertito, è possibile selezionare l&#39;opzione **[!UICONTROL Associate form template as the Document of Record template]**.

## Genera documento di record per PDF forms basati su Acro Forms o XFA {#generate-document-of-record-acroform-xfaform}

Se si utilizza un modulo Acro o un modulo PDF basato su XFA come modulo di origine per il servizio di Automated forms conversion (AFCS), è possibile:

* abilitare la generazione DoR prima della conversione del modulo adattivo per generare DoR utilizzando il modulo di origine come modello

* o modificare le proprietà dei moduli adattivi dopo la conversione dei moduli adattivi per abilitare la generazione DoR utilizzando come modello predefinito il modello di modulo di origine o qualsiasi altro modello di modulo

### Abilita generazione DoR prima della conversione per generare DoR utilizzando il modello del modulo di origine {#use-input-form-as-template-to-generate-document-of-record}

1. Selezionare **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Automated Forms Conversion Configuration]** > Proprietà della configurazione cloud utilizzata per la conversione > **[!UICONTROL Advanced]** > opzione **[!UICONTROL Generate Document of Record]**.

1. Tocca **[!UICONTROL Save & Close]** per salvare le impostazioni.

1. [Esegui la conversione](/help/using/convert-existing-forms-to-adaptive-forms.md). Assicurati di utilizzare la configurazione cloud modificata nel passaggio 1 di queste istruzioni.
Il servizio di conversione associa automaticamente il modulo Acro Form o il modulo PDF basato su XFA al modulo adattivo convertito come modello DoR.
È possibile aprire le proprietà del modulo adattivo per visualizzare il modello DoR nella sezione **[!UICONTROL Document of Record Template Configuration]** della scheda **[!UICONTROL Form Model]**.

   ![Modifica le proprietà del modulo adattivo per generare il documento record](assets/generate_dor_af_properties_xdp_acro.png)

   All’invio del modulo adattivo convertito, il DoR viene generato automaticamente utilizzando il modello di modulo di origine.

### Modifica le proprietà del modulo adattivo dopo la conversione per abilitare la generazione DoR {#edit-adaptive-form-properties-to-generate-document-of-record}

1. [Esegui la conversione](/help/using/convert-existing-forms-to-adaptive-forms.md) nel modulo PDF non interattivo per generare un modulo adattivo.

1. Seleziona il modulo adattivo nella cartella **[!UICONTROL output]** e tocca **[!UICONTROL Properties]**.

1. Nella scheda **[!UICONTROL Form Model]**, espandi la sezione **[!UICONTROL Document of Record Template Configuration]** e seleziona **[!UICONTROL Generate Document of Record]** per abilitare la generazione DoR utilizzando il modello predefinito.
È inoltre possibile selezionare l&#39;opzione **[!UICONTROL Associate form template as the Document of Record template]** e selezionare il modello per abilitare la generazione DoR utilizzando il modello di modulo di origine o qualsiasi altro modello di modulo.

1. Tocca **[!UICONTROL Save & Close]** per salvare le impostazioni.
