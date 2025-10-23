# Web-Scraper-for-News-Headlines
import requests
from bs4 import BeautifulSoup

URL = "https://www.bbc.com/news"

response = requests.get(URL)
response.raise_for_status()  

soup = BeautifulSoup(response.text, "html.parser")

headlines = soup.find_all("h2")
headline_list = []
for h in headlines:
    text = h.get_text(strip=True)
    if text and len(text) > 10 and text not in headline_list:
        headline_list.append(text)


with open("headlines.txt", "w", encoding="utf-8") as file:
    for line in headline_list:
        file.write(line + "\n")

print(f"{len(headline_list)} headlines saved successfully to 'headlines.txt'")
