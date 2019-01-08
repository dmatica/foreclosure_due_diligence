# Foreclosure Due Diligence
This project was developed as a proof-of-concept to streamline acquisition of information on upcoming foreclosure auctions. For the purpose of this project, we are using Beautiful Soup to scrape property addresses from the foreclosure auction site hosted by the [Sheriff's office in Somerset county, NJ](https://www.co.somerset.nj.us/government/elected-officials/sheriff-s-office/divisions/sheriff-sales), then using HERE's API to get the postal code for the addresses, followed by using Zillow's API to get more metrics about the properties, such as home and property size, number of bedrooms and bathrooms, and previous recorded tax assessment value.

## Getting started
We start off by using the `requests` [library](http://docs.python-requests.org/en/master/) to ping the website linked above, followed by [Beautiful Soup 4](https://www.crummy.com/software/BeautifulSoup/) to grab specific content of interest. 

>page = requests.get('https://www.co.somerset.nj.us/government/elected-officials/sheriff-s-office/divisions/sheriff-sales')  
>soup = BeautifulSoup(page.content, 'html.parser')  
>content_box = soup.find('div', attrs={'class': 'content_area'})  
