#Importing Header Files#
!apt-get update
!apt-get install -y wget curl unzip
!wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb 
!dpkg -i google-chrome-stable_current_amd64.deb 
!apt --fix-broken install -y 
# Install ChromeDriver
!wget https://chromedriver.storage.googleapis.com/112.0.5615.49/chromedriver_linux64.zip
!unzip chromedriver_linux64.zip
!mv chromedriver /usr/local/bin/ 
!pip install selenium webdriver-manag

#PART-1#
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.chrome.options import Options
from webdriver_manager.chrome import ChromeDriverManager
import time
from bs4 import BeautifulSoup

def get_village_details():
    chrome_options = Options()
    chrome_options.add_argument("--headless") 
    chrome_options.add_argument("--no-sandbox")
    chrome_options.add_argument("--disable-dev-shm-usage")
    chrome_options.add_argument("--remote-debugging-port=9222")  
    driver_path = ChromeDriverManager().install()
    service = Service(driver_path)
    driver = webdriver.Chrome(service=service, options=chrome_options)
    url = "https://www.yelp.com/biz/village-the-soul-of-india-hicksville"
    driver.get(url)
    time.sleep(5)
    page_source = driver.page_source
    soup = BeautifulSoup(page_source, 'html.parser')
    try:
        name = soup.find('h1').text.strip()
    except AttributeError:
        name = "No name found"
    
    try:
        address = soup.find('address').text.strip()
    except AttributeError:
        address = "No address found"
    
    menu_items = soup.find_all('span', class_='menu-item-details')
    menu = []
    for item in menu_items:
        name = item.text.strip()
        price = item.find_next('span').text.strip() if item.find_next('span') else "Price not available"
        menu.append((name, price))
    
    driver.quit()
    return name, address, menu

#PART-2
def display_village_menu():
    
    name, address, menu = get_village_details()
    print(f"Restaurant Name: {name}")
    print(f"Address: {address}")
    print("\nMenu Items:")
    for item in menu:
        print(f"{item[0]} - {item[1]}")
display_village_menu()

#PART-3
import random

def get_weather_data(location):

    try:
       
        temperature_fahrenheit = random.uniform(50, 100)  
        rain = random.uniform(0, 10)  
        snow = random.uniform(0, 5)  
        
        print(f"Mock Data for {location}:")
        print(f"Temperature: {temperature_fahrenheit:.2f}°F")
        print(f"Rain in the last hour: {rain:.2f} mm")
        print(f"Snow in the last hour: {snow:.2f} mm")
        
        return temperature_fahrenheit, rain, snow
    
    except Exception as e:
        print(f"Error in generating mock weather data: {e}")
        return None, None, None

def display_village_menu():
   
    location = "New York"
    print(f"Fetching mock weather details for: {location}")
    
    temp_fahrenheit, rain, snow = get_weather_data(location)
    
    if temp_fahrenheit is None:
        print("Failed to fetch weather data.")
    else:
  
        print(f"Temperature: {temp_fahrenheit:.2f}°F")
        print(f"Rain in the last hour: {rain:.2f}mm")
        print(f"Snow in the last hour: {snow:.2f}mm")
    

display_village_menu()
