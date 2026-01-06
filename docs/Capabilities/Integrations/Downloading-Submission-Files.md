[Home](index) > [Capabilities](Capabilities) > [Integrations](Integrations) > **Downloading Submission Files**
***

This guide describes how to programmatically download file attachments from CHEFS form submissions using a Python utility. This integration is useful for archiving uploaded files, processing attachments, and external system integration.

## Overview

The CHEFS File Downloader is a Python utility that:
- Retrieves form submissions from the CHEFS API
- Programmatically downloads all file attachments from specified file upload components
- Supports filtering submissions by status, date range, and other criteria to download specific attachments
- Handles multiple file upload components in a single form
- Provides secure configuration through environment variables or config files

## Prerequisites

- Python 3.9 or higher (Python 3.6+ technically supported, but 3.9+ recommended)
- Python `requests` library (`pip install requests`)
- CHEFS Form ID
- CHEFS API Token (see [Generating API Keys](../Data-Management/Generating-API-keys) for instructions)
- Internet connectivity to CHEFS API

### Finding Your Form ID

Your CHEFS Form ID can be found in the form URL:

**From the Form Designer**:
```
https://submit.digital.gov.bc.ca/app/form/design?f=<FORM_ID>
```

**From the Form Submission Page**:
```
https://submit.digital.gov.bc.ca/app/form/submit?f=<FORM_ID>
```

**From the Form Management Page**:
```
https://submit.digital.gov.bc.ca/app/form/manage?f=<FORM_ID>
```

The Form ID is the UUID value after `?f=` in the URL (e.g., `aeb3b705-1de5-4f4e-a4e6-0716b7671034`).

## Installation

1. **Copy the Python script** from the [Python Script](#python-script) section below and save it as `download_chefs_files.py` (or any name you prefer)

2. **Install required Python package**:
   ```bash
   pip install requests
   ```

3. **Create configuration file** (`config.json`) in the same directory as your Python script:
   ```bash
   touch config.json
   ```

4. **Edit `config.json`** with your CHEFS credentials and settings

## Configuration

### Basic Setup

Edit `config.json` with the following required fields:

```json
{
  "form_id": "your-form-id-uuid",
  "api_token": "your-api-token",
  "version": "0",
  "base_url": "https://submit.digital.gov.bc.ca/",
  "file_component": ["simplefile"],
  "api_params": {}
}
```

### Configuration Parameters

| Parameter | Type | Required | Description | Default |
|-----------|------|----------|-------------|---------|
| `form_id` | string | Yes | Your CHEFS form ID (UUID format) | - |
| `api_token` | string | Yes | Your CHEFS API token | - |
| `version` | string | No | The form version number. If format is JSON (not CSV), setting this to 0 will export all versions | `"0"` |
| `base_url` | string | No | CHEFS API base URL | `"https://submit.digital.gov.bc.ca/"` |
| `file_component` | array | No | File upload component names in your form | `["simplefile"]` |
| `api_params` | object | No | Additional API filtering parameters | `{}` |

### Environment Variables

For production deployments, use environment variables which override `config.json`:

```bash
export CHEFS_FORM_ID="your-form-id"
export CHEFS_API_TOKEN="your-api-token"
export CHEFS_VERSION="0"
export CHEFS_BASE_URL="https://submit.digital.gov.bc.ca/"
```

### API Parameters

Use `api_params` in `config.json` to filter which submissions to process for file downloads:

```json
{
  "api_params": {
    "status": "COMPLETED",
    "deleted": false,
    "drafts": false,
    "preference": {
      "minDate": "2024-01-01T00:00:00Z",
      "maxDate": "2024-12-31T23:59:59Z"
    }
  }
}
```

**Available Parameters**:
- `status` (string): Filter by submission status (e.g., `"COMPLETED"`, `"DRAFT"`, `"ASSIGNED"`)
- `deleted` (boolean): Set to true to include deleted submissions
- `drafts` (boolean): Set to true to include draft submissions
- `preference` (object): Date range filters with `minDate` and `maxDate` (ISO 8601 format)

### Multiple File Components

If your form has multiple file upload fields:

```json
{
  "file_component": [
    "document_upload",
    "supporting_files",
    "attachment"
  ]
}
```

## Usage

### Basic Usage

```bash
python download_chefs_files.py
```

(Replace `download_chefs_files.py` with whatever you named your script)

### With Environment Variables

```bash
export CHEFS_FORM_ID="abc123def456"
export CHEFS_API_TOKEN="token789xyz"
python download_chefs_files.py
```

### Example Configurations

**Download files from completed submissions from 2024**:
```json
{
  "form_id": "your-form-id",
  "api_token": "your-token",
  "api_params": {
    "status": "COMPLETED",
    "preference": {
      "minDate": "2024-01-01T00:00:00Z",
      "maxDate": "2024-12-31T23:59:59Z"
    }
  }
}
```

**Download files from all submissions (including drafts and deleted)**:
```json
{
  "form_id": "your-form-id",
  "api_token": "your-token",
  "api_params": {}
}
```

## Output

### Submissions Data
The script retrieves submission data from the API but does **not save it to disk**. The JSON response is used internally to locate and download file attachments. If you need to save submission data, you'll need to modify the script.

### Downloaded Files
File attachments are downloaded to the `files/` directory (created automatically) with the naming format:
```
{confirmation_id}_{original_filename}
```

**Example**:
- Original: `contract.pdf`
- Downloaded as: `53D442D3_contract.pdf`

**Note**: Only files from the specified `file_component` fields are downloaded. The script processes all submissions returned by the API query and downloads their associated files.

## Security Considerations

- **Never commit** `config.json` with real credentials to version control
- **Use environment variables** for production deployments
- **Rotate API tokens** regularly

## Logging and Debugging

The tool provides detailed logging output:

```
INFO | 2026-01-02 11:06:38 -0500 | Export URL: https://submit.digital.gov.bc.ca/app/api/v1/forms/...
INFO | 2026-01-02 11:06:38 -0500 | Params: {'format': 'json', 'type': 'submissions', 'status': 'COMPLETED'}
INFO | 2026-01-02 11:06:39 -0500 | Submissions returned: 5
INFO | 2026-01-02 11:06:40 -0500 | Downloaded: contract.pdf -> 53D442D3_contract.pdf
INFO | 2026-01-02 11:06:40 -0500 | Total files downloaded: 5
```

## Troubleshooting

### 401 Unauthorized Error
- Verify `form_id` and `api_token` are correct
- Check that API token hasn't expired
- Ensure credentials are properly set in `config.json` or environment variables

### Missing File Components
- Verify the `file_component` names match exactly with your form schema
- Check form configuration to confirm component names

### Connection Errors
- Verify network connectivity to CHEFS API
- Check `base_url` is correct for your environment
- Confirm firewall/proxy settings allow API access

## API Documentation

For complete CHEFS API documentation including all available parameters, visit:
[CHEFS API Swagger Documentation](https://submit.digital.gov.bc.ca/app/api/v1/docs#tag/Submission/operation/export)

## Python Script

Download or copy the complete Python script below:

```python
import requests
import base64
import logging
import json
import os

logging.basicConfig(level=logging.INFO, format="%(levelname)s | %(asctime)s | %(message)s", datefmt='%Y-%m-%d %H:%M:%S %z')

# Load configuration from config.json or environment variables
def _load_config():
    """Load configuration from config.json with env var overrides"""
    config_file = os.path.join(os.path.dirname(__file__), 'config.json')
    config = {}
    
    if os.path.exists(config_file):
        try:
            with open(config_file, 'r') as f:
                config = json.load(f)
        except Exception as e:
            logging.warning(f"Could not read config.json: {e}")
    
    # Environment variables override config file
    config['form_id'] = os.getenv("CHEFS_FORM_ID") or config.get("form_id")
    config['api_token'] = os.getenv("CHEFS_API_TOKEN") or config.get("api_token")
    config['version'] = os.getenv("CHEFS_VERSION") or config.get("version", "0")
    config['base_url'] = os.getenv("CHEFS_BASE_URL") or config.get("base_url", "https://submit.digital.gov.bc.ca/")
    config['file_component'] = config.get("file_component", ["simplefile"])
    config['api_params'] = config.get("api_params", {})
    
    return config

config = _load_config()

def get_chefs_submissions_json(form_id, api_token, version):
    """
    Returns the JSON response from the CHEFS API for the specified form ID, API token, and version.

    Args:
        form_id (str): The form ID. View read me for more information.
        api_token (str): The API token. View read me for more information.
        version (str): The version of the form.
    
    Returns:
        dict: The JSON response from the CHEFS API.
        
    Raises:
        ValueError: If required credentials are missing.
    """
    # Validate required credentials
    if not form_id or not api_token:
        raise ValueError("Missing required credentials: CHEFS_FORM_ID and CHEFS_API_TOKEN must be set")
    
    # Ensure a local directory exists for downloaded files
    files_dir = os.path.join(os.path.dirname(__file__), 'files')
    os.makedirs(files_dir, exist_ok=True)

    username_password = f'{form_id}:{api_token}'
    base64_encoded_credentials = base64.b64encode(username_password.encode("utf-8")).decode("utf-8")

    headers = {
        "Authorization": f"Basic {base64_encoded_credentials}"
    }
    base_url = config.get('base_url', 'https://submit.digital.gov.bc.ca')
    # Remove trailing slash if present
    base_url = base_url.rstrip('/')
    
    url = f"{base_url}/app/api/v1/forms/{form_id}/export"
    params = {
        "format": "json",
        "type": "submissions"
    }
    
    # Merge with optional API parameters
    api_params = config.get('api_params', {})
    if isinstance(api_params, dict):
        params.update(api_params)
    
    logging.info(f"Export URL: {url}")
    logging.info(f"Params: {params}")
    response = requests.get(url, headers=headers, params=params)
    if response.status_code != 200:
        logging.error(f"Export request failed: {response.status_code} {response.text}")
        return response
    # this is the actuall submission response.
    try:
        data = response.json()
    except Exception as e:
        logging.error(f"Failed to parse JSON response: {e}")
        return response

    if not isinstance(data, list):
        logging.warning(f"Unexpected response shape (not a list). Keys: {list(data.keys()) if isinstance(data, dict) else type(data)}")
        return response

    logging.info(f"Submissions returned: {len(data)}")

    downloaded = 0
    file_components = config.get('file_component', ['simplefile'])
    # Ensure file_components is a list
    if isinstance(file_components, str):
        file_components = [file_components]
    
    for submission in data:
        # Extract confirmation ID from form metadata
        confirmation_id = "UNKNOWN"
        if "form" in submission and "confirmationId" in submission["form"]:
            confirmation_id = submission["form"]["confirmationId"]
        else:
            logging.warning(f"Submission missing 'form.confirmationId'. Available keys: {list(submission.keys())}")
        
        # Process each file upload component
        for file_component in file_components:
            if file_component not in submission:
                logging.warning(f"Submission missing '{file_component}' field. Available keys: {list(submission.keys())}")
                continue
            attachment = submission[file_component]
            for att_info in attachment:
                data_id = att_info["data"]["id"]
                original_name = att_info["originalName"]
                # Use confirmation ID and original filename
                name_parts = original_name.rsplit('.', 1)
                if len(name_parts) == 2:
                    filename = f"{confirmation_id}_{name_parts[0]}.{name_parts[1]}"
                else:
                    filename = f"{confirmation_id}_{original_name}"
                attachment_url = f"{base_url}/app/api/v1/files/{data_id}"
                att_response = requests.get(attachment_url, headers=headers, stream=True)
                if att_response.status_code == 200:
                    # Open a local file for writing the downloaded content
                    file_path = os.path.join(files_dir, filename)
                    with open(file_path, 'wb') as file:
                        # Stream the content in chunks to avoid large memory usage
                        for chunk in att_response.iter_content(chunk_size=8192):
                            file.write(chunk)
                    logging.info(f"Downloaded: {original_name} -> {filename}")
                    downloaded += 1
                else:
                    logging.info(f"Failed to download file. Status code: {att_response.status_code}, Message: {att_response.text}")
    logging.info(f"Total files downloaded: {downloaded}")
    return response

if __name__ == "__main__":
    try:
        response = get_chefs_submissions_json(config['form_id'], config['api_token'], config['version'])
    except ValueError as e:
        logging.error(f"Configuration error: {e}")
        exit(1)
    except Exception as e:
        logging.error(f"Unexpected error: {e}")
        exit(1)
```

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)
