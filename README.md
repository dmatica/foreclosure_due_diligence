# Foreclosure Due Diligence
This project was developed as a proof-of-concept to streamline acquisition of information on upcoming foreclosure auctions. For the purpose of this project, we are using Beautiful Soup to scrape property addresses from the foreclosure auction site hosted by the [Sheriff's office in Somerset county, NJ](https://www.co.somerset.nj.us/government/elected-officials/sheriff-s-office/divisions/sheriff-sales), then using HERE's API to get the postal code for the addresses, followed by using Zillow's API to get more metrics about the properties, such as home and property size, number of bedrooms and bathrooms, and previous recorded tax assessment value.


*This script was written using Python 3.7, and compiled together into several cells of a Jupyter notebook.*  
## Usage
The first cell installs any necessary dependencies and imports the libraries necesssary to run. The second cell serves as a placeholder to store the API keys. For this script, I am using [HERE's](https://developer.here.com/) API for it's geocoding capabilities to acquire postal codes for the addresses scraped, and [Zillow's](https://www.zillow.com/howto/api/APIOverview.htm) API to get available information on the properties. Both APIs are available for free. To use Zillow's API, you are required to make a Zillow acount first, before generating a Zillow Web Services ID (ZWSID) to make API calls.  To use HERE's API, sign up for an account, and make a new project. For this project, you can use the Freemium plan, which allows up to 250,000 API calls per month.  HERE then gives you an APP ID and APP code for each specific project, both of which are needed to make API calls.  
![HERE App ID and App Code](/images/here_api.png)  

The third cell uses the [requests](http://docs.python-requests.org/en/master/) library to ping the website, followed by [Beautiful Soup 4](https://www.crummy.com/software/BeautifulSoup/) to grab the html contents of the webpage. 

>page = requests.get('https://www.co.somerset.nj.us/government/elected-officials/sheriff-s-office/divisions/sheriff-sales')  
>soup = BeautifulSoup(page.content, 'html.parser')  

![Somerset County Sheriff Sales Page](/images/webpage.png)

Next we want to find the html element that contains the upcoming listings for sale. Using the 'Inspect Element' feature in a web browser, we can hover over the table, and see that the table is contained in a div element, with the class "content_area".

![Inspect element](/images/webpage_inspect_element.png)

We can now use the `soup.find` feature of Beautiful Soup to find div elements with the "content_area" class.

>content_box = soup.find('div', attrs={'class': 'content_area'})  

