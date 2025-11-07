# MFA
This project sets up and analyzes a forced alignment pipeline using the Montreal Forced Aligner (MFA) to automatically align speech audio with phonetic transcriptions. It explores how alignment works and the factors influencing accuracy, such as acoustic models, transcription, and audio quality.
This repository provides a **complete automated workflow** for performing forced alignment using the **Montreal Forced Aligner (MFA)**.  
All commands can be executed directly via the included **Makefile**.

Model and Dictionary Used: **english_us_arpa**  
Tool Version: **Montreal Forced Aligner v2.2.x**

---

##  Project Structure
```
mfa-assignment/
 ├── dataset/
 │    ├── wav/              # Input audio files
 │    └── transcripts/      # Matching text files
 ├── output/                # Generated TextGrids
 ├── scripts/               # Bash automation scripts
 │    ├── setup.sh
 │    ├── align.sh
 │    └── train_g2p.sh
 ├── tools/                 # Evaluation scripts (OOV reports)
 ├── Makefile
 ├── README.md
 └── report.pdf
```

---

##  Setup Instructions (Makefile Workflow)

### 1️ Environment Setup
```bash
make setup
```
This will create a virtual environment, install MFA, and download the required models.

### 2️ Activate the Virtual Environment
```bash
make activate
```

### 3️ Align Dataset
```bash
make align
```
This runs:
```bash
mfa align dataset/ english_us_arpa english_us_arpa output/
```

### 4️ Evaluate Dataset (Optional)
```bash
make eval
```
Generates OOV coverage report via `tools/oov_report.py`.

### 5️ Clean Outputs
```bash
make clean
make deepclean
```

---

##  Example Alignment (HELLO WORLD)

| Tier | Segment | Start (s) | End (s) |
|------|----------|-----------|---------|
| Word | HELLO | 0.00 | 0.45 |
| Word | WORLD | 0.45 | 0.90 |

Phoneme alignment example:
```
HH 0.00–0.10, AH 0.10–0.25, L 0.25–0.40, OW 0.40–0.45,
W 0.45–0.55, ER 0.55–0.70, L 0.70–0.85, D 0.85–0.90
```

---

##  Custom G2P Dictionary (Optional)

To handle OOV words, train a G2P model and generate a new pronunciation dictionary:
```bash
make g2p
make align DICT_NAME=custom_g2p_dict.zip
```

---

##  Validation and Troubleshooting

- Run `mfa validate dataset/ english_us_arpa` before alignment.  
- Make sure every `.wav` file has a corresponding `.txt`.  
- Use mono 16kHz `.wav` files.  
- For dialectal data, retrain with `train_g2p.sh`.

---


**References:**
- Montreal Forced Aligner Documentation: [https://montreal-forced-aligner.readthedocs.io/](https://montreal-forced-aligner.readthedocs.io/)
- Praat Tool: [https://www.fon.hum.uva.nl/praat/](https://www.fon.hum.uva.nl/praat/)
