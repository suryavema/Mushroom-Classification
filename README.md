# Mushroom Classification (Random Forest, Python)

Classify mushrooms as **edible (e)** or **poisonous (p)** from the UCI Mushroom dataset using a Random Forest model. This repo includes code to:
1) train a model on **all features** and plot **feature importance**, and  
2) train a compact model on **5 key features** and **classify real mushrooms** by name/traits.

> ⚠️ **Disclaimer**: This project is for learning only. Do **not** use it to decide whether a mushroom is safe to eat.

## Dataset
- `mushrooms.csv` — UCI Mushroom dataset with categorical attributes and target column `class` (`e`/`p`).
- `Attribute Information.txt` — feature value legend (e.g., odor: `n=none`, `f=foul`, etc.).

## Project Files
- `mainModel.py` — trains a Random Forest on **all features**, reports accuracy, and plots feature importances. Optionally saves `featureimp.png`.  
- `testModel.py` — re-trains a Random Forest on **5 important & easy-to-identify features** (`odor`, `gill-color`, `gill-size`, `spore-print-color`, `gill-spacing`) and classifies a few **example species** after mapping their categorical codes to the same label encodings used for training.
- `MushroomClassification.ipynb` — end‑to‑end, step‑by‑step notebook version (optional for readers who prefer notebooks).
- `Presentation.pptx` — project slides.

## Quickstart

### 1) Environment
```bash
python -V                 # Python 3.10+ recommended
python -m venv .venv
# Windows
.venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate

pip install -U pip
pip install numpy pandas scikit-learn matplotlib jupyter
```

### 2) Train with **all** features & view feature importance
```bash
python mainModel.py
```
This prints test accuracy and shows a horizontal **feature importance** bar chart.
- To save the figure, open `mainModel.py` and **uncomment** the `plt.savefig("featureimp.png", ...)` line, then run again.

### 3) Train compact model & classify real mushrooms
```bash
python testModel.py
```
This script:
- encodes all columns consistently (`LabelEncoder`),
- trains a Random Forest on 5 selected features,
- maps sample mushrooms (e.g., *Agaricus bisporus*, *Amanita phalloides*) into the same encodings,
- prints a small table with predicted class labels.

### Typical outputs
- Console accuracy for both models (train/test split = 80/20, `random_state=42`).
- `featureimp.png` (if saved) under the project root.

## How it works

### Encoding & mapping
All categorical columns are converted to numeric labels with `LabelEncoder`. The scripts keep a **`labelmap`** dict so that new, real samples coded with letters (like `odor='n'`) can be converted to the exact numeric IDs used during training.

### Models
- **All-features model**: trains on every column except `class`, and visualizes `feature_importances_`.
- **Compact model**: uses only five key features for easier real‑world entry, while keeping high accuracy on the dataset split.

## Project Structure
```
.
├─ mushrooms.csv
├─ Attribute Information.txt
├─ mainModel.py
├─ testModel.py
├─ MushroomClassification.ipynb
├─ Presentation.pptx
└─ README.md
```



## Notes & limitations
- The dataset contains only categorical fields from a specific guide; generalization to all species is **not guaranteed**.
- Random Forest provides strong accuracy here, but don’t deploy as a safety‑critical tool.
- If you plan to save and reuse a model, export with `joblib.dump(model, "model.pkl")` and load later with `joblib.load(...)` ensuring you reuse the **same encoders**.

## Next Steps
- Add `requirements.txt` with pinned versions (e.g., scikit-learn, pandas).
- Save trained model and encoders (`joblib`) and provide a small **CLI** or **Gradio** UI for interactive predictions.
- Add **unit tests** (e.g., shape checks, labelmap integrity).
- Convert the notebook to HTML in a `docs/` folder for readers who don’t use Jupyter.
- Consider **stratified** splits and cross‑validation for more robust metrics.
- Track experiments with a seed and a fixed list of features in a config file.


