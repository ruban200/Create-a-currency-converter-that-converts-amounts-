# Create-a-currency-converter-that-converts-amounts-
💱 Currency Converter Web App
A lightweight Flask-based web application that allows users to convert an amount from one currency to another using fixed exchange rates.

🌐 Demo
This project is for educational/demo purposes and does not use real-time exchange rates.

🚀 Features
Convert between popular currencies (USD, EUR, GBP, INR, JPY, CAD, AUD, CNY)

Simple UI with Tailwind CSS styling

Error handling for invalid inputs and unsupported currencies

Responsive design for mobile and desktop

🛠 Technologies Used
Python 3

Flask - Backend web framework

Tailwind CSS - Frontend styling

HTML & Jinja2 - Templating

📦 Installation
Clone the repo

bash
Copy
Edit
git clone https://github.com/your-username/currency-converter.git
cd currency-converter
Create a virtual environment (optional)

bash
Copy
Edit
python -m venv venv
source venv/bin/activate  # For Windows: venv\Scripts\activate
Install dependencies

bash
Copy
Edit
pip install flask
Run the app

bash
Copy
Edit
python app.py
Open your browser and go to:
http://127.0.0.1:5000

💡 How It Works
User enters an amount, selects From and To currencies.

The server uses a fixed exchange rate dictionary to:

Convert the amount to USD

Then convert USD to the target currency

Returns and displays the result

📁 File Structure
csharp
Copy
Edit
currency-converter/
│
├── app.py                 # Main Flask application
├── README.md              # Project documentation
└── (templates inlined using render_template_string)
📝 License
This project is licensed under the MIT License.

✍️ Author
Your Name – RUBAN

