# Neural-Enhanced-Linear-Cryptanalysis-of-DES
## Setup (once)

```powershell
pip install numpy==1.23.5 tensorflow==2.10.1
```

## How to read each case

- **Train**: build neural distinguisher model.
- **Attack (DL)**: key recovery using trained model.
- **Attack (Matsui)**: classical baseline.
- **Accuracy**: quick model quality check (only where `obtain_accuracy.py` exists).

---

## Case 1: One-bit (`DES attack/one bit/L3..L6`)

Use this pattern inside each `Lx` folder:

```powershell
mkdir neural_network
python single_dl_for_....py
python attack_single_dl_for_....py
python attack_single_mastui_for_....py
# optional
python obtain_accuracy.py
```

Concrete entry scripts by round:

- **L3**: `single_dl_for_l3.py`, `attack_single_dl_for_l3.py`, `attack_single_mastui_for_l3.py`
- **L4**: `single_dl_for_l4v2.py`, `attack_single_dl_for_l4v2.py`, `attack_single_mastui_for_l4v2.py`, `obtain_accuracy.py`
- **L5**: `single_dl_for_l5v2.py`, `attack_single_dl_for_l5v2.py`, `attack_single_mastui_for_l5v2.py`, `obtain_accuracy.py`
- **L6**: `single_dl_for_l6v2.py`, `attack_single_dl_for_l6v2.py`, `attack_single_mastui_for_l6v2.py`, `obtain_accuracy.py`

---

## Case 2: Multiple-bits (`DES attack/multiple bits/L3..L6`)

### L3

```powershell
cd "DES attack\multiple bits\L3"
python multiple_dl_for_l3.py
python "attack_multiple_dl_for_l3_for 4 round.py"
python "attack_multiple_dl_for_l3_for 5 round.py"
python "attack_multiple_matsui_for_l3_for 4 round.py"
python "attack_multiple_matsui_for_l3_for 5 round.py"
```

### L4

```powershell
cd "DES attack\multiple bits\L4"
python multiple_dl_for_l4.py
python "attack_multiple_dl_for_l4_for 5 round.py"
```

### L5

```powershell
cd "DES attack\multiple bits\L5"
python multiple_dl_for_l5.py
```

### L6

`multiple_dl_for_l6.py` does not auto-start training. Train manually, then run attacks:

```powershell
cd "DES attack\multiple bits\L6"
python -c "from multiple_dl_for_l6 import train_model; train_model(80)"
python "attack_multiple_dl_for_l6_for 8 round.py"
python "attack_multiple_matsui_for_l6_for 8 round.py"
```

---

## Outputs

- Model: `*_model.json`, `*_weight.h5`
- Curves/logs: `*.txt` (pickle)
- Attack results: `*.npy`

## Practical note

Defaults are heavy (`2**24` data, many loops). For a quick smoke test, reduce:

- `train_data_size`
- `epochs`
- attack loop variable `num`

