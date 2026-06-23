# Student Engagement Detection

This project trains a Convolutional Neural Network (CNN) to classify a student's visual engagement state from images. The notebook prepares an image dataset, trains a TensorFlow/Keras model, evaluates it, and shows prediction examples with optional face detection.

## What the model predicts

The notebook is configured for six image classes:

- `confused`
- `engaged`
- `frustrated`
- `Looking Away`
- `bored`
- `drowsy`

These classes can also be grouped conceptually as:

- **Engaged:** `confused`, `engaged`, `frustrated`
- **Not engaged:** `Looking Away`, `bored`, `drowsy`

## Repository contents

| File | Purpose |
| --- | --- |
| `student_eng.ipynb` | Main Jupyter notebook for dataset preparation, model training, evaluation, and prediction visualization. |
| `requirements.txt` | Python packages needed to run the notebook. |
| `data_of_student_engagement` | Placeholder/data file currently included in the repository. |

## Dataset expected by the notebook

The notebook expects a ZIP file containing the dataset in this folder structure:

```text
archive.zip
├── Engaged/
│   ├── confused/
│   ├── engaged/
│   └── frustrated/
└── Not engaged/
    ├── Looking Away/
    ├── bored/
    └── drowsy/
```

By default, the notebook looks for the ZIP file at:

```text
./archive.zip
```

You can change `zip_path` in the first notebook cell if your dataset ZIP has a different name or location.

## Setup instructions

### 1. Create a virtual environment

```bash
python3 -m venv .venv
source .venv/bin/activate
```

On Windows PowerShell, use:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

### 2. Install dependencies

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

### 3. Add the dataset

Place your dataset ZIP file in the project root:

```text
student_engagement/archive.zip
```

### 4. Start Jupyter

```bash
jupyter notebook
```

Open `student_eng.ipynb` and run the cells from top to bottom.

## What the notebook does

1. Extracts the dataset ZIP file.
2. Flattens the nested dataset into six class folders.
3. Splits the images into train and test folders.
4. Loads images with TensorFlow/Keras generators.
5. Trains a CNN classifier.
6. Evaluates model accuracy and loss.
7. Builds a confusion matrix and classification report.
8. Displays sample predictions.
9. Optionally detects faces with OpenCV and predicts engagement state.
10. Saves the trained model as `engagement_model.h5`.

## Output files created when running the notebook

The notebook creates these folders/files locally:

```text
./dataset/
./flat_dataset/
./train/
./test/
./engagement_model.h5
```

These generated files are not required to be committed to Git.

## Common problems and fixes

### `FileNotFoundError: archive.zip`

Make sure your dataset ZIP is present in the project root or update this variable in the notebook:

```python
zip_path = BASE_DIR / "archive.zip"
```

### TensorFlow installation issues

TensorFlow support depends on your Python version and operating system. If installation fails, try Python 3.10 or 3.11 in a fresh virtual environment.

### OpenCV face detection finds no faces

The face detector only works well on clear, front-facing faces. Poor lighting, side profiles, or small faces may not be detected.

### Low accuracy

Try these improvements:

- Add more balanced training images for each class.
- Increase training epochs.
- Use transfer learning with a pretrained model such as MobileNetV2 or EfficientNet.
- Check for mislabeled images.

## Notes for new users

- Run notebook cells in order because later cells depend on variables created earlier.
- Keep class folder names exactly the same as shown above unless you also update the notebook.
- The model classifies images based on visual patterns only; it should not be used as the only measure of student engagement in real classrooms.
