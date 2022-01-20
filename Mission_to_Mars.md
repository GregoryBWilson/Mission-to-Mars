```python
# Import Splinter and BeautifulSoup
from splinter import Browser
from bs4 import BeautifulSoup as soup
from webdriver_manager.chrome import ChromeDriverManager
import pandas as pd
```


```python
# Set up Splinter
executable_path = {'executable_path': ChromeDriverManager().install()}
browser = Browser('chrome', **executable_path, headless=False)
```

    
    
    ====== WebDriver manager ======
    Current google-chrome version is 97.0.4692
    Get LATEST chromedriver version for 97.0.4692 google-chrome
    Driver [C:\Users\Greg\.wdm\drivers\chromedriver\win32\97.0.4692.71\chromedriver.exe] found in cache
    


```python
# Visit the mars nasa news site
url = 'https://redplanetscience.com'
browser.visit(url)
# Optional delay for loading the page
browser.is_element_present_by_css('div.list_text', wait_time=1)
```




    True




```python
# Parse the HTML
# Notice how we've assigned slide_elem as the variable
# to look for the <div /> tag and its descendent (the other tags within the <div /> element)? 
html = browser.html
news_soup = soup(html, 'html.parser')
slide_elem = news_soup.select_one('div.list_text')
```


```python
slide_elem.find('div', class_='content_title')
```




    <div class="content_title">NASA Mars Mission Connects With Bosnian and Herzegovinian Town</div>




```python
# Use the parent element to find the first `a` tag and save it as `news_title`
news_title = slide_elem.find('div', class_='content_title').get_text()
news_title
```




    'NASA Mars Mission Connects With Bosnian and Herzegovinian Town'




```python
# Use the parent element to find the paragraph text
news_p = slide_elem.find('div', class_='article_teaser_body').get_text()
news_p
```




    'A letter from NASA was presented to the mayor of Jezero, Bosnia-Herzegovina, honoring the connection between the town and Jezero Crater, the Mars 2020 rover landing site.'



### JPL Space Images Featured Image


```python
# Visit URL
url = 'https://spaceimages-mars.com'
browser.visit(url)
```


```python
# Find and click the full image button
full_image_elem = browser.find_by_tag('button')[1]
full_image_elem.click()
```


```python
# Parse the resulting html with soup
html = browser.html
img_soup = soup(html, 'html.parser')
```


```python
# Find the relative image url
img_url_rel = img_soup.find('img', class_='fancybox-image').get('src')
img_url_rel
```




    'image/featured/mars2.jpg'




```python
# Use the base URL to create an absolute URL
img_url = f'https://spaceimages-mars.com/{img_url_rel}'
img_url
```




    'https://spaceimages-mars.com/image/featured/mars2.jpg'



## Mars Facts


```python
# Instead of scraping each row, or the data in each <td />, 
# we're going to scrape the entire table with Pandas' .read_html() function.
df = pd.read_html('https://galaxyfacts-mars.com')[0]
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Mars - Earth Comparison</td>
      <td>Mars</td>
      <td>Earth</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Diameter:</td>
      <td>6,779 km</td>
      <td>12,742 km</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mass:</td>
      <td>6.39 × 10^23 kg</td>
      <td>5.97 × 10^24 kg</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Moons:</td>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Distance from Sun:</td>
      <td>227,943,824 km</td>
      <td>149,598,262 km</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.columns=['description', 'Mars', 'Earth']
df.set_index('description', inplace=True)
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Mars</th>
      <th>Earth</th>
    </tr>
    <tr>
      <th>description</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Mars - Earth Comparison</th>
      <td>Mars</td>
      <td>Earth</td>
    </tr>
    <tr>
      <th>Diameter:</th>
      <td>6,779 km</td>
      <td>12,742 km</td>
    </tr>
    <tr>
      <th>Mass:</th>
      <td>6.39 × 10^23 kg</td>
      <td>5.97 × 10^24 kg</td>
    </tr>
    <tr>
      <th>Moons:</th>
      <td>2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Distance from Sun:</th>
      <td>227,943,824 km</td>
      <td>149,598,262 km</td>
    </tr>
    <tr>
      <th>Length of Year:</th>
      <td>687 Earth days</td>
      <td>365.24 days</td>
    </tr>
    <tr>
      <th>Temperature:</th>
      <td>-87 to -5 °C</td>
      <td>-88 to 58°C</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.to_html()
```




    '<table border="1" class="dataframe">\n  <thead>\n    <tr style="text-align: right;">\n      <th></th>\n      <th>Mars</th>\n      <th>Earth</th>\n    </tr>\n    <tr>\n      <th>description</th>\n      <th></th>\n      <th></th>\n    </tr>\n  </thead>\n  <tbody>\n    <tr>\n      <th>Mars - Earth Comparison</th>\n      <td>Mars</td>\n      <td>Earth</td>\n    </tr>\n    <tr>\n      <th>Diameter:</th>\n      <td>6,779 km</td>\n      <td>12,742 km</td>\n    </tr>\n    <tr>\n      <th>Mass:</th>\n      <td>6.39 × 10^23 kg</td>\n      <td>5.97 × 10^24 kg</td>\n    </tr>\n    <tr>\n      <th>Moons:</th>\n      <td>2</td>\n      <td>1</td>\n    </tr>\n    <tr>\n      <th>Distance from Sun:</th>\n      <td>227,943,824 km</td>\n      <td>149,598,262 km</td>\n    </tr>\n    <tr>\n      <th>Length of Year:</th>\n      <td>687 Earth days</td>\n      <td>365.24 days</td>\n    </tr>\n    <tr>\n      <th>Temperature:</th>\n      <td>-87 to -5 °C</td>\n      <td>-88 to 58°C</td>\n    </tr>\n  </tbody>\n</table>'




```python
browser.quit()
```


```python

```
