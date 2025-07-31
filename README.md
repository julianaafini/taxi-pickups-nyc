# NYC Taxi Pickups Analysis

## Table of Contents

* [Project Overview](#project-overview)

* [Features](#features)

* [Technologies Used](#technologies-used)

* [Getting Started](#getting-started)

* [Project Structure](#project-structure)

* [Data](#data)

* [Analysis Highlights](#analysis-highlights)

## Project Overview

This project, documented in the `taxi_pickups_nyc_analysis.ipynb` Jupyter Notebook, performs an analysis of NYC taxi pickup data. It explores the dataset using various Python libraries, including Spark for large-scale data processing and cuDF/cuML for GPU-accelerated computations, alongside traditional Pandas and scikit-learn. The notebook demonstrates data loading, basic statistical analysis, and geographical plotting of pickup locations.

## Features

* **Data Loading & Schema Definition**: Defines a precise schema for the taxi data and loads it efficiently.

* **Statistical Summary**: Calculates and displays key statistics about the taxi trips (e.g., number of unique medallions/licenses, min/max pickup/dropoff times, max trip time/distance/amount).

* **Geographical Plotting**: Visualizes taxi pickup locations on a scatter plot to identify patterns and potential data anomalies.

* **Multi-framework Approach**: Integrates Pandas, Apache Spark, and RAPIDS (cuDF/cuML) for flexible data handling and analysis, demonstrating different approaches for various dataset sizes.

## Technologies Used

* **Python**: The primary programming language.

* **Jupyter Notebook**: For interactive development and analysis.

* **Pandas**: For general data manipulation and analysis.

* **Apache Spark (PySpark)**: For distributed data processing and SQL queries on large datasets.

* **cuDF / cuML (RAPIDS)**: For GPU-accelerated dataframes and machine learning tasks, offering significant speedups for compatible hardware.

* **Matplotlib**: For data visualization.

* **gdown**: For downloading files from Google Drive.

* **scikit-learn**: For clustering algorithms (though not explicitly shown in the provided snippet, it's typically used for KMeans).

* **NumPy**: For numerical operations.

## Getting Started

### Prerequisites

To run this notebook, you'll need a Python environment with the following libraries installed. Some libraries like `pyspark` and `rapidsai` (cuDF/cuML) might require specific environments or GPU access, especially if running on Google Colab.

```bash
pip install gdown pyspark==4.0.0.dev2 pandas numpy matplotlib scikit-learn
```
For GPU acceleration with RAPIDS (cuDF/cuML), you will need a CUDA-enabled GPU and might need to follow specific installation instructions, often provided by the RAPIDS team for platforms like Google Colab. The notebook attempts to install RAPIDS utilities:

```bash
!git clone https://github.com/rapidsai/rapidsai-csp-utils.git
!python rapidsai-csp-utils/colab/pip-install.py
```

**Note**: The RAPIDS installation step might fail if your environment (e.g., Google Colab runtime) is not configured with a GPU. Ensure you select a GPU runtime if you intend to use cuDF/cuML.

### Data Setup

The dataset is hosted on Google Drive. You'll need to make it accessible to your environment.

1. **Access the Dataset**

2. **Google Colab Setup**:
   If you are running this in Google Colab, it's recommended to "Add Shortcut to your Drive" for the shared folder. Then, mount your Google Drive in the Colab notebook:

```bash
from google.colab import drive
drive.mount('/content/drive')
```

### Running the Notebook

1. Open `taxi_pickups_nyc_analysis.ipynb` in a Jupyter Notebook or JupyterLab environment.

2. Execute the cells sequentially. Pay attention to the installation cells and data setup steps.

## Project Structure

* `taxi_pickups_nyc_analysis.ipynb`: The main Jupyter Notebook containing all the code for data loading, analysis, and visualization.

* `data/`: (Expected, but not included in this repository) This directory is where your taxi pickup datasets (`.csv.gz` files) should be stored.

* `checkpoint/`: (Created during runtime) A directory used by Spark for checkpointing.

* `rapidsai-csp-utils/`: (Cloned during runtime) A temporary directory containing utilities for RAPIDS installation in Colab.

## Data

The project utilizes compressed CSV files (`.csv.gz`) containing NYC taxi trip records. The notebook defines a `StructType` schema to ensure proper data parsing, including fields such as:

* `medallion`

* `hack_license`

* `pickup_datetime`

* `dropoff_datetime`

* `trip_time_in_secs`

* `trip_distance`

* `pickup_longitude`

* `pickup_latitude`

* `dropoff_longitude`

* `dropoff_latitude`

* `payment_type`

* `fare_amount`

* `surcharge`

* `mta_tax`

* `tip_amount`

* `tolls_amount`

* `total_amount`

Three dataset sizes are mentioned:

* `FILENAME_large`: 12.3 GB compressed

* `FILENAME_small`: 135 MB compressed (used in the provided snippet for initial statistics and plotting)

* `FILENAME_tiny`: 6.8 MB compressed (recommended for quick development and testing)

## Analysis Highlights

The notebook provides initial insights into the dataset:

* **Basic Statistics**: Shows the count of unique medallions and licenses, and the min/max timestamps, trip times, distances, and total amounts.

* **Pickup Location Plotting**: Visualizes 1000 random pickup locations to quickly identify geographical patterns or outliers. This helps in understanding the spatial distribution of taxi activity and detecting invalid coordinate values.

