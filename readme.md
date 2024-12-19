# YOLOV9 for Building Type Detection
## Code structure

- **data**: Contains the following data and data files:
    - `new_street_view_images`: Directory containing raw street view images.
    - `instances_default.json`: COCO format annotations file.
    - `dataset.csv`: The initial dataset containing metadata for images.
    - `extracted_images`: Directory containing annotated images used for training model.
    - `yolo_dataset`: Contains the necessary folders for the YOLOv9 model, including `train`, `val`, and `test` datasets.
    - `metadata.csv`: Contains four columns: `image_id`, `pano_id`, `x`, and `y`.
    - `predicted_pictures.csv`: Contains three columns: `class`, `confidence`, and `image_id`.
    - `panoid_predicted_table.csv`: Contains three columns: `class`, `confidence`, `pano_id`, `x`, and `y`.
- **scripts**: Python scripts for preprocessing images and handling annotation files.
    - `scrap_images.py`: Script for scraping images from Google Street View.
    - `extract_images.py`: Script for extracting images to be used in model training.
    - `collect_metadata.py`:Script for generating a table with `image_id`, `pano_id`,and geographical coordinates(`x`, `y` for latitude and longitude )
    - `simple_categories_distribution.py`: Script for creating histograms to analyze the distribution of building categories.
    - `convert_coco_to_json.py`: Script for converting COCO annotation files to the format required for YOLOv9 training.
    - `yolov9_predictions.py`: Script for predicting images using trained weights and generating labels and pictures.
    - `collect_labels_of_test_images.py`: Script for collecting different building categories contained in each image from the test set under model prediction.
    - `merge_panoid_labels.py`: Script for merging the `pano_id` of images with their predicted building types and geographical coordinates.
- **figures**: Contains output metrics and predictions from the YOLOv9 models.
    - `parameters_output`: Directory containing model metrics and weights.
    - `prediction`: Directory containing predicted images and corresponding labels for each image.
- **yolov9**: Slightly modified version of YOLOV9 model
    - `train_dual.py`: Script for training the YOLOv9 model using the `yolov9-c` weights. The following parameters were adjusted:
        - **cfg**: Modified the model architecture configuration in `root:/yolov9_models/yolov9/models/detect/yolov9-c.yaml` to better suit the dataset.
        - **data**: Updated the dataset paths and categories for building type detection in `root:/yolov9_models/data/yolo_dataset/data.yaml`.
        - **epochs**:50
        - **batch_size**: 4
    - **general.py**: Modified `yolov9/ultis/general.py` at line 900, adding 10 new lines of code to enhance the generation of predictions. These changes were made to ensure better handling of the prediction output.
    - **general.py**: Modified the `Annotator` class in `yolov9/ultis/plot.py` to increase the transparency of the label text box for bounding boxes, improving the visibility of confidence values in predictions.
- **requirements.txt**: Lists all the necessary packages and dependencies required for the project.
    - `For pip users`: `pip install -r requirements.txt`
    - `For conda users`: `conda install --file requirements.txt`

