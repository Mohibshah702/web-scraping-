# web-scraping-
web scraping code from coursera
pip install requests
pip install beautifulsoup4
import requests 
import re
from bs4 import BeautifulSoup
course_urls=["https://www.coursera.org/learn/get-started-with-python/",
    "https://www.coursera.org/projects/first-python-program-ust/",
    "https://www.coursera.org/specializations/data-science-python/",
    "https://www.coursera.org/learn/python-programming-fundamentals/",
    "https://www.coursera.org/learn/data-analysis-with-python/"]
    for url in course_urls:
    page = requests.get(url)
    if page.status_code == 200:
        soup = BeautifulSoup(page.text, 'html.parser')
        txt = str(soup)
        result = re.findall(r'(\d+,\d+,?\d+)</span></strong> already enrolled', txt)
        if result:
            print("Enrollment count for", url, ":", result[0])
        else:
            print("Enrollment count not found for", url)
    else:
        print("Failed to retrieve the page", url, ". Status code:", page.status_code)
        
