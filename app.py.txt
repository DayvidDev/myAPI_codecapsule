import requests
from flask import Flask, jsonify

EXCHANGE_URL = 'https://openexchangerates.org/api/latest.json?app_id=a2b55638e43c439183199f9df5ade114'
EXCHANGE_PARAMS =  {'symbols':'ZAR,EUR,CAD'}

app = Flask(__name__) 

@app.route('/') # Create main page of web-application
def index():
    return "Welcome to my API!" # Display text on main page


@app.route('/get',methods=['GET']) # Add an endpoint to access our API
def get():
    exchange_data = requests.get(EXCHANGE_URL, EXCHANGE_PARAMS)  
    weather = requests.get(WEATHER_URL,params=WEATHER_PARAMS) 

    return jsonify({
        'usd_rates': exchange_data.json()['rates'],
        'curr_temp': weather.json()['current']['temperature']
    })


if __name__ == '__main__':
    app.run() # Run the application
