from flask import Flask, render_template_string, request

app = Flask(__name__)

# Exchange rates (as of July 2023, relative to USD)
EXCHANGE_RATES = {
    'USD': 1.0,
    'EUR': 0.92,
    'GBP': 0.79,
    'JPY': 143.88,
    'CAD': 1.33,
    'AUD': 1.47,
    'CNY': 7.23,
    'INR': 82.47
}

def convert_currency(amount, from_currency, to_currency):
    if from_currency not in EXCHANGE_RATES or to_currency not in EXCHANGE_RATES:
        raise ValueError("Unsupported currency")
    
    # Convert to USD first, then to target currency
    amount_in_usd = amount / EXCHANGE_RATES[from_currency]
    converted_amount = amount_in_usd * EXCHANGE_RATES[to_currency]
    return round(converted_amount, 2)

@app.route('/', methods=['GET', 'POST'])
def currency_converter():
    result = None
    error = None
    
    if request.method == 'POST':
        try:
            amount = float(request.form['amount'])
            from_currency = request.form['from_currency'].upper()
            to_currency = request.form['to_currency'].upper()
            
            if from_currency not in EXCHANGE_RATES or to_currency not in EXCHANGE_RATES:
                error = "One or more currencies not supported"
            else:
                result = convert_currency(amount, from_currency, to_currency)
                
        except ValueError:
            error = "Please enter a valid amount"
    
    return render_template_string('''
        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>Currency Converter</title>
            <script src="https://cdn.tailwindcss.com"></script>
            <style>
                .bg-gradient {
                    background: linear-gradient(135deg, #6b73ff 0%, #000dff 100%);
                }
                .result-box {
                    transition: all 0.3s ease;
                }
            </style>
        </head>
        <body class="bg-gray-100 min-h-screen flex items-center justify-center p-4">
            <div class="w-full max-w-md">
                <div class="bg-gradient text-white rounded-t-lg p-6 shadow-lg">
                    <h1 class="text-2xl font-bold text-center">Currency Converter</h1>
                </div>
                
                <div class="bg-white rounded-b-lg shadow-lg p-6">
                    <form method="POST" class="space-y-4">
                        <div>
                            <label for="amount" class="block text-gray-700 font-medium mb-2">Amount</label>
                            <input type="number" step="0.01" id="amount" name="amount" 
                                class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
                                placeholder="Enter amount" required>
                        </div>
                        
                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label for="from_currency" class="block text-gray-700 font-medium mb-2">From</label>
                                <select id="from_currency" name="from_currency" 
                                    class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                                    {% for currency in currencies %}
                                        <option value="{{ currency }}" {% if currency == 'USD' %}selected{% endif %}>{{ currency }}</option>
                                    {% endfor %}
                                </select>
                            </div>
                            
                            <div>
                                <label for="to_currency" class="block text-gray-700 font-medium mb-2">To</label>
                                <select id="to_currency" name="to_currency" 
                                    class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500" required>
                                    {% for currency in currencies %}
                                        <option value="{{ currency }}" {% if currency == 'EUR' %}selected{% endif %}>{{ currency }}</option>
                                    {% endfor %}
                                </select>
                            </div>
                        </div>
                        
                        <button type="submit" 
                            class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-4 rounded-lg transition duration-200">
                            Convert
                        </button>
                    </form>
                    
                    {% if result is not none %}
                    <div class="result-box mt-6 p-4 bg-blue-50 border border-blue-200 rounded-lg">
                        <h3 class="text-lg font-semibold text-gray-800 mb-1">Conversion Result</h3>
                        <p class="text-lg">
                            {{ request.form.get('amount', '') }} {{ request.form.get('from_currency', '') }} = 
                            <span class="font-bold text-blue-600">{{ result }}</span> {{ request.form.get('to_currency', '') }}
                        </p>
                    </div>
                    {% endif %}
                    
                    {% if error %}
                    <div class="result-box mt-6 p-4 bg-red-50 border border-red-200 rounded-lg">
                        <p class="text-red-600">{{ error }}</p>
                    </div>
                    {% endif %}
                    
                    <div class="mt-6 text-center text-sm text-gray-500">
                        <p>Exchange rates are fixed values (not live data)</p>
                    </div>
                </div>
            </div>
        </body>
        </html>
    ''', currencies=sorted(EXCHANGE_RATES.keys()), result=result, error=error)

if __name__ == '__main__':
    app.run(debug=True)
