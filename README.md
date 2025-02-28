# Prefect ETL Pipelines

A collection of ETL (Extract, Transform, Load) pipelines built with Prefect, designed for various data processing scenarios.

## Repository Structure

```
prefect-etl-pipelines/
├── etl-s3-upload-flow/       # Flow for uploading data to S3
├── etl-s3-notification-flow/ # Flow for handling S3 notifications
├── etc-cicd-flow/            # Flow for CI/CD processes
├── hello.py                  # Simple example Prefect flow
└── pyproject.toml            # Python project configuration
```

## Overview

This repository contains a set of modular, reusable ETL pipelines implemented using Prefect, a modern workflow management system. Each pipeline is designed to handle specific data processing tasks while maintaining a consistent structure and approach.

## Available Flows

### etl-s3-upload-flow

This flow handles the extraction of data from various sources and uploads it to Amazon S3. It demonstrates how to:
- Connect to data sources
- Transform data as needed
- Upload data to S3 buckets with proper error handling and retries

### etl-s3-notification-flow

This flow processes notifications from S3 (such as object creation events) and performs actions based on those events. It shows how to:
- Listen for S3 events
- Process newly uploaded files
- Trigger downstream processes based on file uploads

### etc-cicd-flow

This flow integrates with CI/CD pipelines to automate the testing and deployment of other flows. It demonstrates:
- Automated testing of Prefect flows
- Deployment of flows to production environments
- Integration with version control systems

## Getting Started

### Prerequisites

- Python 3.8+
- [Prefect](https://www.prefect.io/) 2.0+

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/prefect-etl-pipelines.git
   cd prefect-etl-pipelines
   ```

2. Create and activate a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. Install dependencies from pyproject.toml:
   ```bash
   pip install -e .
   ```

4. Set up Prefect:
   ```bash
   prefect config set PREFECT_API_URL=http://127.0.0.1:4200/api
   ```

## Usage

### Running the Hello World Flow

To test your Prefect setup, you can run the included hello.py flow:

```bash
python hello.py
```

### Running a Specific Flow

Navigate to the flow directory and run the main flow file:

```bash
cd etl-s3-upload-flow
python main.py
```

### Creating a Deployment

```bash
prefect deployment build etl-s3-upload-flow/main.py:s3_upload_flow -n "S3 Upload" -q default
prefect deployment apply s3_upload_flow-deployment.yaml
```

### Scheduling a Flow

```bash
prefect deployment set-schedule s3_upload_flow/S3\ Upload --cron "0 0 * * *"
```

## Best Practices

1. **Idempotency**: Design flows to be idempotent to avoid data duplication
2. **Error Handling**: Implement proper error handling and retries
3. **Logging**: Use Prefect's logging capabilities for debugging
4. **Parameterization**: Make flows configurable through parameters
5. **Monitoring**: Set up notifications and monitoring for flow runs

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/new-flow`
3. Commit your changes: `git commit -am 'Add new flow for XYZ'`
4. Push to the branch: `git push origin feature/new-flow`
5. Submit a pull request
