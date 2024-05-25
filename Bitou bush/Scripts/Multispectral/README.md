## Processing pipeline for DL U-Net model training
![image](https://github.com/Narmilan-A/Remote-Weed-detection/assets/140802455/0c1300b6-cb96-423b-948b-c8b7e145a8c1)

### Brief explanation of unet_training.py
| Main steps                           | Brief Explanation                                                                                                                  |
|--------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| Import Libraries                     | Import Python libraries: NumPy, OS, Pandas, OpenCV, Matplotlib, Seaborn, scikit-image for image processing, GDAL for geospatial data handling, scikit-learn and Keras for model development. |
| Calculate Vegetation Indices         | Define `calculate_veg_indices` function to compute various vegetation indices from multispectral images.                          |
| Tile Images and Masks and define paths | Split images and masks into tiles with specified size and overlap, and specify root directories for images and masks. Retrieve files and preprocess tiles. |
| Convert Masks to Categorical         | Convert mask data to categorical representation using one-hot encoding.                                                             |
| Train-Test Split                     | Split data into training and testing sets using scikit-learn’s `train_test_split` function.                                        |
| U-Net Architecture                   | Define U-Net model architecture with convolutional and deconvolutional layers for semantic segmentation.                           |
| Model Compilation                    | Compile U-Net model with Adam optimizer and categorical cross-entropy loss.                                                         |
| Model Training                       | Train model on training data and validate it using testing data. Save best model checkpoint based on validation loss.               |
| Confusion Matrix and Classification Report | Predict on test data, calculate confusion matrix and classification report. Plot confusion matrix as heatmap.                 |
| IoU Calculation                      | Calculate and save Intersection over Union (IoU) for each class in segmentation.                                                    |

### Brief explanation of unet_testing.py
| Main steps                           | Brief Explanation                                                                                                                  |
|--------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| Import Necessary Libraries          | Import Python libraries: NumPy, OS, Pandas, OpenCV, Matplotlib, Seaborn, scikit-image, GDAL, scikit-learn, and Keras for various tasks. |
| Define the Root Directory           | Define `root folder` variable as the absolute path where the code operates.                                                         |
| Load U-Net Model                    | Load U-Net model from saved file using Keras `load_model` function.                                                                 |
| Calculate Vegetation Indices        | Define `calculate_veg_indices` function to compute vegetation indices for input images.                                             |
| Tile Images and Masks               | Set tile size and overlap percentage, specify root directory for input images and masks, retrieve files, split into tiles, preprocess, and append to lists. |
| Predict and Evaluate Using Confusion Matrix | Use loaded U-Net model to predict masks, compute and visualize confusion matrix, save heatmap.                                |
| Confusion Matrix and Classification Report | Predict on test data, compute confusion matrix and classification report, save both to files.                                  |
| Calculate and Save IoU for Each Class | Calculate IoU for each class, save results to text file, compute and save average IoU.                                             |

### Brief explanation of unet_prediction.py
| Main steps                           | Brief Explanation                                                                                                                  |
|--------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| Import Necessary Libraries          | Import Python libraries: NumPy, OS, Pandas, OpenCV, Matplotlib, Seaborn, scikit-image, GDAL, scikit-learn, and Keras for various tasks. |
| Define the Root Directory           | Define `root folder` variable as the absolute path where the code operates.                                                         |
| Load U-Net Model                    | Load U-Net model from saved file using Keras `load_model` function.                                                                 |
| Calculate Vegetation Indices        | Define `calculate_veg_indices` function to compute vegetation indices for input images.                                             |
| Tile Images and Masks               | Set tile size and overlap percentage, specify root directory for input images and masks, retrieve files, split into tiles, preprocess, and append to lists. |
| Prediction                          | Loop through each image file, apply preprocessing steps, extract patches, resize patches if necessary, predict using U-Net model, merge patches, save predicted image in ENVI format. |

### Brief explanation of label_rasterizing.py
| Main steps                  | Brief Explanation                                                                                                   |
|-----------------------------|---------------------------------------------------------------------------------------------------------------------|
| Import Libraries           | Import necessary libraries: `gdal`, `ogr` from the `osgeo` package, `os`, and `glob` for file and directory operations. |
| Shape to raster function   | This function converts a shapefile to a raster mask based on a reference image's spatial extent and resolution. |
| Main function              | The main function orchestrates the rasterization process by iterating through input images and calling the shape to raster function for each, saving the output masks. |

### Brief explanation of unet_kfold_cross_validation.py
| Main steps                  | Brief Explanation                                                                                                   |
|-----------------------------|---------------------------------------------------------------------------------------------------------------------|
| Import Libraries           | Import necessary libraries: `numpy`, `os`, `pandas`, `cv2`, `matplotlib`, `seaborn`, `exposure` from skimage, `convolve` from `scipy.ndimage`, `time`, `random`, and `tensorflow` modules. Also, import specific functions from `osgeo` (`gdal`) and scikit-learn (`train_test_split`, `KFold`). Import necessary functions and classes from Keras. |
| Define Parameters          | Set various parameters controlling the operations, such as applying vegetation indices, Gaussian blur, mean filter, convolution, and band deletion. Specify image dimensions, tile size, overlap percentage, test size, learning rate, batch size, and epochs. Define class names and number of classes.                                           |
| Define Functions           | Define functions for post-index calculation, calculation of vegetation indices, applying Gaussian blur, applying mean filter, and defining the UNet model architecture.                                                                                                                                                                                       |
| Load and Preprocess Data   | Load image and mask files, filter them based on dimensions, apply preprocessing steps such as equalization, vegetation index calculation, band deletion, convolution, Gaussian blur, and mean filter. Split data into training and testing sets.                                                                   |
| Train Model                | Define and compile the UNet model, apply K-Fold cross-validation, train the model for each fold, save the best model based on validation loss, and evaluate each fold's performance. Save model outcomes and evaluation results to files.                                                                  |
| Visualize Results          | Plot and save graphs of validation accuracy and loss across folds, including average and standard deviation lines.                                                                                                                             |