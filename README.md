# Number Classification FastAPI

A FastAPI application that analyzes and classifies numbers based on various mathematical properties.

## Overview

This API service takes a number as input and returns detailed information about its mathematical properties, including:

- Whether it's prime
- Whether it's a perfect number
- Whether it's an Armstrong number
- Whether it's even or odd
- The sum of its digits
- A fun fact about the number

## Mathematical Concepts

### Prime Numbers
A prime number is a natural number greater than 1 that is not a product of two smaller natural numbers. For example, 2, 3, 5, 7, 11, etc.

### Perfect Numbers
A perfect number is a positive integer that is equal to the sum of its proper positive divisors. For example, 6 is a perfect number because its proper divisors are 1, 2, and 3, and 1 + 2 + 3 = 6.

### Armstrong Numbers
An Armstrong number (also known as a narcissistic number) is a number that is equal to the sum of its own digits each raised to the power of the number of digits. For example, 153 is an Armstrong number because 1³ + 5³ + 3³ = 1 + 125 + 27 = 153.

## API Usage

### Endpoint

```
GET /?number={number}
```

### Query Parameters

- `number`: The number to analyze (required)

### Response Format

```json
{
  "number": 153,
  "is_prime": false,
  "is_perfect": false,
  "properties": ["armstrong", "odd"],
  "digit_sum": 9,
  "fun_fact": "153 is an Armstrong number because 1^3 + 5^3 + 3^3 = 153"
}
```

### Error Responses

Missing number parameter:
```json
{
  "number": null,
  "error": "Missing number parameter"
}
```

Invalid number format:
```json
{
  "number": "abc",
  "error": "Invalid number format"
}
```

## Setup and Deployment

### Prerequisites

- Python 3.7+
- FastAPI
- Uvicorn (for local development)

### Installation

1. Clone this repository:
   ```
   git clone https://github.com/yourusername/number-classification-fastapi.git
   cd number-classification-fastapi
   ```

2. Install dependencies:
   ```
   pip install fastapi uvicorn
   ```

### Running Locally

Start the server with:
```
uvicorn main:app --reload
```

The API will be available at `http://localhost:8000`

### Azure Ubuntu Server Deployment

Below are the steps used to deploy this application on an Azure Ubuntu server:

```bash
# Update and upgrade the system
sudo apt update
sudo apt upgrade

# Install Nginx
sudo apt install nginx
sudo systemctl start nginx
sudo systemctl enable nginx

# Install Python and pip
sudo apt install python3 -y
sudo apt install python3-pip -y
sudo apt install python3.12-venv

# Set up a Python virtual environment
python3.12 -m venv venv
source venv/bin/activate
pip install fastapi uvicorn requests

# Create and edit the main application file
nano main.py

# Configure Nginx as a reverse proxy
sudo nano /etc/nginx/sites-available/fastapi
# Add your Nginx configuration here

# Enable the Nginx configuration
sudo ln -s /etc/nginx/sites-available/fastapi /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx

# Run the FastAPI application
uvicorn main:app --host 0.0.0.0 --port 8000
```

For production use, consider setting up a systemd service to keep the application running and automatically start it on server reboot.

### Example Usage

To check properties of the number 153:
```
GET http://localhost:8000/?number=153
```

## License

[MIT License](LICENSE)
