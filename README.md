# ToysGroup · Analisi delle vendite e dei rivenditori con Python

Esercitazione finale del Modulo 4 · *Python for Data Science*.

## Scenario

**ToysGroup** distribuisce giocattoli tramite una rete di rivenditori in diverse aree geografiche europee. I dati, forniti dal docente, sono esportati in quattro file di formato diverso. Il notebook li legge, li pulisce, li analizza e li usa per costruire modelli di regressione, classificazione e clustering.

| File | Formato | Contenuto |
|---|---|---|
| `products.csv` | CSV | anagrafica prodotti: ProductID, ProductName, Category, ListPrice |
| `regions.xlsx` | Excel | anagrafica regioni: RegionID, State, SalesRegion |
| `sales.json` | JSON | vendite (una riga per transazione): SalesID, ProductID, RegionID, ResellerID, SalesDate, Quantity, SalesAmount |
| `resellers.csv` | CSV | rivenditori: ResellerID, RegionID, Ordini12m, GiorniUltimoOrdine, ScontoMedio, Reclami, Churn |

Le chiavi di collegamento sono `ProductID` e `RegionID`. `Churn = 1` indica un rivenditore che non riordina da oltre 6 mesi.

## Struttura del repository

```
.
├── README.md
├── ToysGroup_esercitazione.ipynb   # notebook con tutti i task
└── data/
    ├── products.csv
    ├── regions.xlsx
    ├── sales.json
    └── resellers.csv
```

## Task svolti

| Task | Argomento | Contenuto principale |
|---|---|---|
| 1 | Python di base | liste di dizionari, dict e set; fasce di prezzo con list comprehension; funzione `fatturato_categoria()`; ciclo `while` sul fatturato cumulato |
| 2 | Lettura e ispezione | `.shape`, `.info()`, `.head()`, `.tail()`, `.describe()`; prezzo unitario con NumPy; selezioni con `.loc[]` e `.iloc[]` |
| 3a | Dati mancanti, filtri e ordinamento | conteggio dei NaN; imputazione con la mediana e `dropna()`; filtro sul 90° percentile con `.query()` |
| 3b | Aggregazioni e merge | `merge()` di vendite, prodotti e regioni; fatturato per categoria e per regione; separazione e ricomposizione con `concat()` |
| 3c | Serie temporali | conversione delle date, accessor `.dt`, fatturato mensile e `pct_change()`, flag delle vendite recenti |
| 4 | Visualizzazione | linee (Matplotlib), boxplot e heatmap (Seaborn), barre interattive (Plotly) |
| 5 | Regressione lineare | correlazioni mensili; regressione semplice e multipla; R² su train e test; previsione di tre mesi; validazione incrociata |
| 6a | Classificazione del churn | regressione logistica, matrici di confusione con soglia 0,5 e 0,3, Accuracy/Precision/Recall, AUC |
| 6b | Clustering | K-Means con metodo del gomito; profilo dei segmenti di rivenditori e quota di churn |
| 7 | Debugging e versioning | correzione di quattro frammenti di codice con il supporto di un assistente AI |

Ogni cella di codice è preceduta da una cella Markdown con il numero del task e la risposta richiesta.

## Risultati principali

- **Fatturato totale** (vendite con importo disponibile): 560.075,50 €, in crescita ogni anno (+28% nel 2024, +21% nel 2025).
- **Categoria con il fatturato più alto:** Outdoor (circa il 59% del totale), trainata dal prezzo delle biciclette.
- **Regressione:** il fatturato mensile cresce in media di circa 304 € al mese, ma la forte variabilità tra mesi rende poco affidabili le previsioni puntuali.
- **Churn:** la regressione logistica con soglia 0,3 individua 10 rivenditori in churn su 14 nel test (Recall 0,71; AUC 0,76).
- **Segmentazione:** quattro segmenti di rivenditori; il segmento "Dormienti" ha il churn più alto (51%), mentre i "Clienti di valore in calo" rappresentano la priorità per le azioni di fidelizzazione.

## Istruzioni di esecuzione

1. **Clonare il repository**
   ```bash
   git clone <URL-del-repository>
   cd <nome-del-repository>
   ```

2. **Installare le librerie** (Python 3.10 o superiore; il notebook è stato sviluppato con Python 3.13 e Pandas 3)
   ```bash
   pip install pandas numpy openpyxl matplotlib seaborn plotly nbformat scikit-learn
   ```
   `openpyxl` serve per leggere il file Excel; `nbformat` per visualizzare i grafici Plotly nel notebook.

3. **Aprire il notebook** in Jupyter o in VS Code e lanciare **Run All** (esegui tutto): le celle vanno eseguite in ordine dall'inizio. I file di dati devono trovarsi nella cartella `data/`, accanto al notebook.

## Note

- Il grafico a barre del Task 4 è realizzato con **Plotly** ed è interattivo: GitHub non lo visualizza nell'anteprima del notebook. Per vederlo occorre aprire il notebook in Jupyter o VS Code.
- Tutte le divisioni casuali (train/test, K-Means) usano `random_state=42`, quindi i risultati sono riproducibili.
- Con versioni di Pandas precedenti alla 3.0, le colonne di testo risultano di tipo `object` invece di `str` e le date di tipo `datetime64[ns]` invece di `datetime64[us]`; i risultati non cambiano.
