# Progetto MATLAB / Simulink

Repository per modelli Simulink (`.slx`), script e funzioni MATLAB (`.m`), dati e test del progetto. Questa guida spiega come scaricare il progetto, usarlo e contribuire.

> **Release richiesta:** MATLAB/Simulink **RXXXXx** (sostituire con la release usata). Un modello salvato con una release più recente non si apre con una più vecchia.

## Indice

1. [Contenuto del repository](#contenuto-del-repository)
2. [Come scaricare il progetto](#come-scaricare-il-progetto)
3. [Come aprirlo ed eseguirlo](#come-aprirlo-ed-eseguirlo)
4. [Dove mettere i file](#dove-mettere-i-file)
5. [Come contribuire](#come-contribuire)
6. [Regole per i modelli Simulink](#regole-per-i-modelli-simulink)
7. [Problemi comuni](#problemi-comuni)

## Contenuto del repository

```
.
├── README.md        questa guida
├── models/          modelli Simulink (.slx) e librerie
├── src/             script e funzioni MATLAB (.m)
├── data/            dati di input e parametri (.mat, .csv)
├── scripts/         script di setup e di esecuzione delle simulazioni
├── tests/           test automatici
├── docs/            documentazione, schemi, report
├── .gitignore       file esclusi dal versionamento (cache, autosave, risultati)
└── .gitattributes   gestione dei file binari (.slx, .mat)
```

## Come scaricare il progetto

**Senza Git (più semplice):** nella pagina del repository clicca **Code → Download ZIP** ed estrai l'archivio.

**Con Git (consigliato per collaborare):**

```bash
git clone https://github.com/Spopscorn/simulink-matlab-project.git
cd simulink-matlab-project
```

**Da MATLAB:** *Home → New → Project → From Git*, incolla l'URL del repository.

## Come aprirlo ed eseguirlo

1. Apri MATLAB e imposta come cartella corrente la radice del progetto.
2. Aggiungi le cartelle al path:
   ```matlab
   addpath(genpath(pwd))
   ```
3. Apri il modello principale (indicare qui il nome, es. `models/main_model.slx`):
   ```matlab
   open_system("models/main_model")
   ```
4. Esegui gli script di setup in `scripts/` prima della simulazione, se presenti.

Se il progetto contiene un file `.prj` (Simulink Project), basta aprirlo con `openProject("nome.prj")`: i path vengono impostati in automatico.

## Dove mettere i file

| Tipo di file | Cartella |
|---|---|
| Modelli e librerie Simulink `.slx` | `models/` |
| Funzioni e script MATLAB `.m` | `src/` |
| Dati di input, parametri, tabelle | `data/` |
| Script di avvio / batch di simulazioni | `scripts/` |
| Test (`matlab.unittest`, Simulink Test) | `tests/` |
| Documentazione, immagini, report | `docs/` |

Usa **percorsi relativi**, mai percorsi assoluti del tuo PC (`C:\Users\...`).

## Come contribuire

```bash
git switch main
git pull
git switch -c feature/descrizione-breve

# ... modifica i file, chiudi i modelli Simulink salvandoli ...

git add .
git commit -m "feat: descrizione della modifica"
git push -u origin feature/descrizione-breve
```

Poi apri una **Pull Request** verso `main` dalla pagina GitHub del repository.

Convenzioni sui messaggi di commit: `feat:` nuova funzionalità, `fix:` correzione, `docs:` documentazione, `refactor:` riorganizzazione.

## Regole per i modelli Simulink

- I file `.slx` sono binari: Git **non può unirli automaticamente**. Evita che due persone modifichino lo stesso modello nello stesso momento.
- In caso di conflitto confronta le versioni da MATLAB:
  ```matlab
  visdiff("versione_a.slx", "versione_b.slx")
  ```
- Spezza i modelli grandi con sottosistemi, librerie e model referencing: file più piccoli causano meno conflitti.
- Chiudi sempre il modello prima del commit, così il file è salvato.
- Non committare cartelle o file generati (`slprj/`, `*.slxc`, `*.autosave`, risultati di simulazione): sono già esclusi da `.gitignore`.
- Per dati molto pesanti (`.mat` grandi) valuta **Git LFS**; file singoli oltre 100 MB sono rifiutati da GitHub.

## Problemi comuni

| Problema | Soluzione |
|---|---|
| Il modello non si apre | Release di MATLAB diversa da quella indicata sopra |
| `git push` rifiuta la password | GitHub richiede un Personal Access Token, una chiave SSH o `gh auth login` |
| Funzioni o modelli non trovati | Esegui `addpath(genpath(pwd))` dalla radice del progetto |
| Conflitto su un `.slx` | Usa `visdiff` oppure scegli una versione con `git checkout --ours/--theirs <file>` |
| Repository lento o enorme | Controlla di non aver committato `slprj/` o grandi file `.mat` |

## Licenza

Nessuna licenza è stata ancora scelta: finché non ne viene aggiunta una (file `LICENSE`), il codice è visibile ma non può essere riutilizzato da altri senza permesso.
