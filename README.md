# HPE Log Processing System

A modular system designed for processing and analyzing HPE server logs at scale. This system implements a sophisticated architecture for efficient log extraction, processing, and analysis across multiple machines.

## System Architecture

The system implements a modular architecture with the following key components:

- **Client Nodes**: Handle local log extraction and processing on individual machines
- **Master Node**: Further log analysis for key information extraction
- **Orchestrator**: Manages workflow for individual machine processing, ensuring proper data handling and cleanup

### External Service Integrations

- **MongoDB**: Primary database for storing processed log analysis data and metadata
- **MinIO**: Scalable object storage system for raw log files
- **Jenkins**: CI/CD pipeline support for automated deployment and testing

## Features

- **Automated Log Extraction**: Extract and process .tar.gz archives containing server logs
- **Secure Data Storage**: 
  - Raw logs stored in MinIO with machine-specific prefixes
  - Processed data stored in MongoDB for analysis
- **Advanced Error Handling**:
  - Comprehensive logging at all levels
  - Automatic cleanup on failures
- **Jenkins CI/CD Integration**:
  - Automated agent configuration
  - WebSocket-based communication
  - Dedicated work directories for isolation

## Prerequisites

- Python 3.13.2
- Required Python packages:
```
minio
python-dotenv
pymongo
requests
```

Install dependencies using:
```bash
pip install -r requirements.txt
```

## Installation and Setup

1. **Environment Configuration**
   - Create a `.env` file in the project root with the following variables:
   ```
   MONGO_DB=log_analysis_db
   MONGO_COLLECTION=<machine_name>
   MONGO_URI=<your_mongodb_connection_string>
   MINIO_ACCESS_KEY=<your_minio_access_key>
   MINIO_SECRET_KEY=<your_minio_secret_key>
   ```

2. **MongoDB Setup**
   - Ensure MongoDB is running and accessible
   - Create database 'log_analysis_db'
   - Collections will be automatically created per machine

3. **MinIO Configuration**
   - Set up MinIO server
   - Create bucket: 'hpe-log-analysis'
   - Configure access permissions

4. **Jenkins Integration**
   - Configure Jenkins pipeline using provided Jenkinsfile
   - Set up required credentials in Jenkins
   - Configure WebSocket communication

## Project Structure

- `master.py`: Master node implementation for workflow orchestration
- `client.py`: Client node implementation for local processing
- `orchestrator.py`: Manages individual machine workflow
- `LogExtraction.py`: Core log processing and extraction logic
- `prepare_machine.py`: Machine setup and configuration
- `shared_tasks.py`: Common utilities and shared functions
- `mongo_test.py`: MongoDB connection testing
- `verify_mongo.py`: MongoDB verification utilities
- `Dockerfile`: Container configuration for deployment
- `jenkinsfile`: Jenkins pipeline configuration

## Usage Instructions


1. **Create /machines directory in root of project and paste some machine log folders**:
```bash
mkdir -p machines
```

2. **Run Client Processing**:
```bash
python client.py
```

3. **Start the Master Node**:
```bash
python master.py
```

### Configuration Options

- Set machine name via `MONGO_COLLECTION` environment variable
- Configure MongoDB connection via `MONGO_URI`
- Set MinIO credentials via environment variables

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

Proprietary - All rights reserved

