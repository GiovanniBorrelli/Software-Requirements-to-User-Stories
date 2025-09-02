# Introduzione

Negli sviluppi software moderni, la trasformazione automatica dei requisiti software
in user stories rappresenta una fase critica per garantire coerenza, chiarezza e tracciabilità delle funzionalità. Tuttavia, i metodi tradizionali di generazione automatica,
come reti neurali artificiali, SVM o algoritmi genetici, mostrano limiti significativi:
non catturano completamente tutte le informazioni chiave (“who”, “what” e “why”),
richiedono elevati costi computazionali e non producono output immediatamente
utilizzabili.
Questo lavoro propone un approccio basato su Large Language Models (LLM) per
automatizzare la generazione di user stories a partire dai requisiti software. Sono state
analizzate diverse tecniche di prompt engineering, tra cui few-shot, meta-prompting
e prompt directional stimulus, e confrontati due modelli LLM, LLaMA e Mistral,
utilizzando metriche automatiche standard di valutazione testuale (BLEU, ROUGE,
METEOR e BERTScore).
I risultati mostrano che i LLM producono user stories coerenti, complete e semanticamente corrette, superando le limitazioni dei metodi precedenti. Alcune tecniche
di prompt hanno migliorato ulteriormente le performance, mentre LLaMA ha mostrato vantaggi leggermente superiori rispetto a Mistral. Complessivamente, il lavoro
conferma la validità e la promettente applicabilità dei LLM nel contesto analizzato,
indicando che questo approccio rappresenta attualmente la soluzione più efficace
per automatizzare la conversione dei requisiti software in user stories.

# Creazione del Dataset
Su Kaggle è disponibile un dataset1
costituito da requisiti software estratti da
PURE2
(PUblic REquirements). PURE è una una raccolta di documenti, ottenuti dal
Web, al cui interno sono presenti dei requisiti software. Ad ogni requisito è assegnato
un ID che indica il documento di provenienza. A ogni documento corrisponde un
progetto diverso.
Sono stati selezionati tre documenti (CCHIT Certified 2011 Ambulatory EHR
Criteria 20110517, LACountyEHR Requirements, iTRUST): il primo contiene 300
requisiti, mentre gli altri due ne contengono 1.200 ciascuno. Tutti e tre i progetti
appartengono all’ambito medico, in particolare alle EHR (Electronic Health Records),
ossia cartelle cliniche elettroniche, poiché la maggior parte dei documenti del dataset
ha natura medica. Ogni tecnica di prompt engineering è stata applicata a tutti e tre
i progetti, con l’obiettivo di calcolare successivamente la media dei risultati. Infine,
per generare le user stories a partire dai requisiti software, è stato utilizzato ChatGPT
come oracolo, interrogato tramite il sito ufficiale.

(https://www.kaggle.com/datasets/computerscience3/public-requirementspure-dataset)
(https://zenodo.org/record/1414117)

Sono riportate le principali tecniche (
https://www.promptingguide.ai/it/techniques) di prompt engineering esplorate:
1. Zero-shot: il modello affronta il compito senza esempi preliminari, basandosi
unicamente sulla propria conoscenza pre-addestrata.
2. Few-shot: il modello riceve un numero limitato di esempi prima di eseguire il
compito, così da imitare lo schema fornito.
3. Chain of Thought: il modello esplicita i passaggi logici intermedi per giungere
alla risposta, migliorando la coerenza del ragionamento.
4. Self-consistency: combina approccio few-shot e chain of thought, fornendo
esempi e incoraggiando il modello a ragionare per step, così da produrre
risposte più affidabili.
5. Prompt Generate Knowledge: sfrutta la conoscenza pregressa del modello per
arricchire la trasformazione in user stories con contesto aggiuntivo.
6. Prompt Chaining: suddivide la generazione in passaggi sequenziali (ad esempio attore, funzionalità, obiettivo) per comporre gradualmente una user story
completa.
7. Prompt with Directional Stimulus: introduce indizi e linee guida per orientare
la risposta del modello verso una forma desiderata.
8. Meta-prompting: pone l’enfasi sulla struttura della risposta (ad esempio il
formato delle user stories), piuttosto che sul contenuto specifico.
9. Reflection: induce il modello a rivedere e criticare la propria risposta iniziale,
per poi proporne una versione revisionata e migliorata.
10. Prompt Ensemble: consiste nella combinazione delle tre tecniche più efficaci
identificate sperimentalmente, con l’obiettivo di unire i rispettivi punti di forza
e ottenere user stories più accurate e consistenti.

# Dettagli implementativi

Il codice è stato eseguito su Colab, potete eseguirlo senza nessun prerequisito o libreria richiesta, c'è anche una versione più veloce e leggera dove il modello llama è già montato e caricato. Inoltre, c'è anche una implementazione, stavolta in locale sul vostro pc, del RAG. Più in basso è presente un tutorial per eseguirlo. Nel dataset, la lista di requisiti non è esaustiva, ed è presente per rendere giusto un'idea della loro struttura.

How to implement RAG code.
Watch this tutorial: https://www.youtube.com/watch?v=Oe-7dGDyzPM
1. Clone this repo on VScode: https://github.com/AllAboutAI-YT/easy-local-rag (or my fork, in case the repo gets updated)
2. install ollama from ollama.com
3. open windows powershell on project path (...\easy-local-rag)
4. write: ollama pull mxbai-embed-large
5. write: ollama pull llama3
6. on VSCode terminal on project path, write: python upload.py
7. upload the pdf file(s)
8. write: python localrag.py
9. now you can ask questions

Chatgpt Chain of thoughts results: https://chatgpt.com/share/25c1d162-cd6e-4937-85ee-025496d9fe54 
300 software requirements, 100 for message.
