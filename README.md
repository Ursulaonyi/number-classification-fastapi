# Number Classification API

This API takes a number as input and returns various mathematical properties about it, along with a fun fact.

## Features

- Determines if a number is prime
- Determines if a number is perfect
- Identifies Armstrong numbers
- Determines if a number is odd or even
- Calculates the sum of digits
- Provides a fun fact about the number using the Numbers API

## API Specification

### Endpoint

```
GET /api/classify-number?number={your-number}
```

### Response Format (200 OK)

```json
{
    "number": 371,
    "is_prime": false,
    "is_perfect": false,
    "properties": ["armstrong", "odd"],
    "digit_sum": 11,
    "fun_fact": "371 is an Armstrong number because 3^3 + 7^3 + 1^3 = 371"
}
```

### Error Response (400 Bad Request)

```json
{
    "number": "alphabet",
    "error": true
}
```

## Mathematical Properties Explained

### Prime Number
A number that is only divisible by 1 and itself. Example: 7, 11, 13, etc.

### Perfect Number
A number where the sum of its proper divisors equals the number itself. Example: 6 (1+2+3=6), 28 (1+2+4+7+14=28).

### Armstrong Number
A number that equals the sum of its own digits each raised to the power of the number of digits. Example: 371 = 3³ + 7³ + 1³ = 27 + 343 + 1 = 371.

### Digit Sum
The sum of all individual digits in the number. Example: For 371, digit sum = 3 + 7 + 1 = 11.

## Installation & Deployment

### Prerequisites
- Ubuntu server
- Python 3.7+ (we'll be using Python 3.12)
- Nginx

### Server Setup

1. Update and upgrade your server:
```bash
sudo apt update
sudo apt upgrade
```

2. Install Nginx:
```bash
sudo apt install nginx
sudo systemctl start nginx
sudo systemctl enable nginx
```

3. Install Python and pip:
```bash
sudo apt install python3 -y
sudo apt install python3-pip -y
sudo apt install python3.12-venv
```

4. Create and activate a virtual environment:
```bash
python3.12 -m venv venv
source venv/bin/activate
```

5. Install the required packages:
```bash
pip install fastapi uvicorn requests
```

6. Create the main.py file:
```bash
nano main.py
```

7. Configure Nginx:
```bash
sudo nano /etc/nginx/sites-available/fastapi
```

8. Create a symbolic link and check the configuration:
```bash
sudo ln -s /etc/nginx/sites-available/fastapi /etc/nginx/sites-enabled/
sudo nginx -t
```

9. Reload Nginx to apply changes:
```bash
sudo systemctl reload nginx
```

10. Run the application:
```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```

For production deployment, consider setting up a service to keep the application running.

## Technologies Used

- FastAPI: A modern, fast web framework for building APIs
- Uvicorn: ASGI server for running the FastAPI application
- Nginx: Web server acting as a reverse proxy
- Requests: HTTP library for making requests to the Numbers API

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Author

Ursula Okafo