# ggf
import requests
import json

def get_weather(api_key, location):
    base_url = "https://api.openweathermap.org/data/2.5/weather"
    params = {
        "q": location,
        "appid": api_key,
        "units": "metric"  # Use Celsius for temperature
    }

    try:
        response = requests.get(base_url, params=params)
        data = json.loads(response.text)

        if response.status_code == 200:
            return data
        else:
            return None
    except Exception as e:
        print("An error occurred:", e)
        return None
        # gui.py

import tkinter as tk
from tkinter import messagebox
from weather import get_weather

class WeatherApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Weather App")

        self.label = tk.Label(root, text="Enter City or Zip Code:")
        self.label.pack()

        self.entry = tk.Entry(root)
        self.entry.pack()

        self.button = tk.Button(root, text="Get Weather", command=self.get_weather)
        self.button.pack()

        self.result_label = tk.Label(root, text="")
        self.result_label.pack()

    def get_weather(self):
        location = self.entry.get()
        weather_data = get_weather(api_key, location)

        if weather_data:
            temperature = weather_data["main"]["temp"]
            description = weather_data["weather"][0]["description"]
            message = f"Temperature: {temperature}°C\nDescription: {description.capitalize()}"
            self.result_label.config(text=message)
        else:
            messagebox.showerror("Error", "Failed to fetch weather data.")

# Create the main application window
if __name__ == "__main__":
    root = tk.Tk()
    app = WeatherApp(root)
    root.mainloop()
    # app.py

import tkinter as tk
from gui import WeatherApp

# Replace with your OpenWeatherMap API key
api_key = "YOUR_API_KEY"

# Create the main application window
if __name__ == "__main__":
    root = tk.Tk()
    app = WeatherApp(root)
    root.mainloop()
