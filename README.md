# YAML-CSV Converter API

## Overview

The **YAML-CSV Converter API** is a Python Flask application designed to facilitate the conversion between YAML and CSV file formats. This application is useful for data processing tasks where you need to transform structured data from one format to another. It supports both conversion directions: from YAML to CSV and from CSV to YAML.

## Features

- Convert YAML files to CSV format.
- Convert CSV files to YAML format.
- Easy-to-use API interface.
- CI/CD pipeline for automated testing and deployment.
- Dockerization, making it portable and easily usable no matter your system.

## Project Structure

Here's the structure of the project:

```
yaml_csv_converter_API/
├── yaml_csv_converter.py   # Main conversion logic
├── test_app.py             # Unit tests for the converter using the API
├── app.py                  # Flask application for the APIfied version of the task
├── Dockerfile              # Docker configuration for containerization
├── input/output files      # Examples for you to try
├── requirements.txt        # Dependencies required for the project
└── README.md               # Project documentation
```

## Installation

To use the YAML to CSV Converter API, follow these steps:

### Prerequisites

- Python 3.11 (for local deployment)
- pip (Python package manager)
- Docker installed on your system

## Usage

1. **Clone the repository**:

   ```bash
   git clone https://github.com/salcamo/yaml-csv-converter-API.git
   cd yaml_csv_converter-wheel
   ```

2. **Install the requirements**:

   You can install the requirements locally by running:

   ```bash
   pip install -r requirements.txt
   ```

   Alternatively, you can also install it in a virtual environment:

   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows use `venv\Scripts\activate`
   pip install -r requirements.txt
   ```

## Usage

### Running the API Locally

To run the API locally:
```bash
python app.py
```
This will run the Flask API on http://localhost:5000.

### Using Docker

To build and run the Docker container:

```bash
docker build -t yaml-csv-api .
docker run -p 5000:5000 yaml-csv-api
```

## API Endpoints
- **`/yaml-to-csv`** (POST): Convert YAML to CSV.
    - Upload a YAML file or send raw YAML data in the request body.
    - Example ```bash
    curl -F "file=@input.yaml" http://localhost:5000/yaml-to-csv --output output.csv
    ```
- **`/csv-to-yaml`** (POST): Convert YAML to CSV.
    - Upload a CSV file or send raw CSV data in the request body.
    - Example ```bash
    curl -F "file=@input.csv" http://localhost:5000/csv-to-yaml --output output.yaml
    ```

## CI/CD Pipeline

The CI/CD pipeline is set up using GitHub Actions to automate testing, packaging, and deployment processes. The pipeline will:

1. **Run tests** using pytest.
2. **Build a Docker image** containing the library.
3. **Push the Docker image** to Docker Hub.

When anyone push changes to the main branch.

### CI/CD Configuration

The pipeline configuration is defined in the `.github/workflows/ci-cd.yml` file. And you can check the last executions in the "Actions" tab.

### Secrets Configuration

Make sure to add your Docker Hub username and password as secrets in your GitHub repository settings. Use the following keys:

- `DOCKER_USERNAME`: Your Docker Hub username
- `DOCKER_PASSWORD`: Your Docker Hub password

## 1. Error Handling

The converter functions implement basic error handling using Python's `try-except` blocks. This helps catch and report errors that may occur during file reading, writing, or conversion. 

### Example Error Handling

Here’s an example of how errors are handled in the conversion functions:

```python
def csv_to_yaml(csv_data):
    """Converts CSV data to YAML format."""
    input_stream = io.StringIO(csv_data)
    try:
        ***

    except Exception as e:
        raise ValueError(***{str(e)}")
```

## 2. Scalability and Adaptability

The YAML to CSV Converter is designed to be adaptable for future data sources and volumes. Here are a few strategies to ensure future scalability:

- **Asynchronous Processing**: Implement asynchronous I/O operations to handle larger files without blocking.
- **Batch Processing**: Extend the functionality to process multiple files in parallel.
- **Configuration Management**: Allow users to specify different data formats.

## 3. Performance Considerations

- **Processing Time**: The processing time may vary based on the size of the input files and the complexity of the data structures. For larger files, we can consider profiling the code to identify potential bottlenecks.
- **Resource Utilization**: When deployed in a Docker container, we can monitor resource usage (CPU, memory) to ensure efficient operation.