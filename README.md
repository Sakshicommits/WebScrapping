# WebScrapping
#Monitoring Amazon product price every hour
from bs4 import BeautifulSoup
import time
import requests
def function1():
    url=(r'https://www.amazon.in/Toyshine-Geometric-Building-Stacker-Stacking/dp/B07SYJXQTR/ref=pd_ci_mcx_pspc_dp_d_2_i_1')
    #header={"User-Agent": "Mozilla/5.0"}
    contents=requests.get(url)
    contentsSoup=BeautifulSoup(contents.content,'html.parser')
    #print(contents)
    product_name=contentsSoup.find(id='productTitle').get_text().strip()
    rating=contentsSoup.find(id='acrCustomerReviewText').get_text().strip('ratings')
    price=contentsSoup.find(class_="a-price-whole").get_text().strip('.')
    discount=contentsSoup.find(class_="a-size-large a-color-price savingPriceOverride aok-align-center reinventPriceSavingsPercentageMargin savingsPercentage").get_text().strip()[1:]
    import csv
    Headings=['Title','Price','Total Reviews','Disount']
    Entries=[product_name,price,rating,discount]
    with open('AmazonWeb.csv','a+',newline='',encoding='UTF8') as web:
        book=csv.writer(web)
        book.writerow(Entries)
#Calling function every hour        
while(True):
    function1()
    time.sleep(3600)

#Reading dataframe 
import pandas as pd
df=pd.read_csv(r'C:\Users\AmazonWeb.csv')
df    

    
        
