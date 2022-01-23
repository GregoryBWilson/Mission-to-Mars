



# Mission to Mars

## 1.0 Purpose

Senior data scientist, Robin, does freelance work in astronomy in her spare time and dreams of working for NASA in the future.  She wants to write a web scraping application that can pull all of her data together in one place.  She needs to understand how web pages are structured so that she can write a Python script to navigate the pages she is interested in and collect the right information.  Since the data she is collecting is, in general, unstructured she has chosen to use a MongoDB document based database to hold the data that she is collecting. To put it all together in a web application, Robin will need to use the Flask web framework.  

## 2.0 How The  Program Works

The set up of this application is quite complex, so I thought it would be helpful for Robin if I included figure 1 below, taken from section 10.0.4 of the "Bootcamp: CARL-VIRT-DATA-PT-11-2021-U-B-TTH" course material.  The user interacting with the application via a web browser serves up data scraped from various websites and stored in a MongoDB database.

![/Resources/1_The_Web_Scraping_Process.png](/Resources/1_The_Web_Scraping_Process.png "***Figure 1 - The Web Scraping Process***")

***Figure 1 - The Web Scraping Process***

With all of the pieces correctly configured there is still the challenge of making sure that everything is up and running in the correct location on Robin's computer so that it will reliably perform every time she wants to use it.   The steps below should be followed to achieve this outcoming:

#### Step 1 - Start Anaconda

There is a app.cmd file that I created in the main Mission-to-Mar directory called Start_Ananconda.cmd, double click the file and Anaconda will be launched in the right location to be effective.  The code for this part of the process is shown in the code fence below.

```bash
:: call <anaconda_dir>/Scripts/activate.bat <anaconda_dir>
Call %windir%\System32\cmd.exe "/K" C:\Users\Greg\anaconda3\Scripts\activate.bat C:\Users\Greg\anaconda3\envs\PythonData
```

#### Step 2 - Start Flask

Now that Anaconda is running in the right directory we can simply set the FLASK_APP to the Python file app.py and run Flask, as shown in the code fence below.

```bash
:: For our FLASK_APP environment variable, we want to modify the path that will run our app.py file so that we can run our file.
set FLASK_APP=app.py
flask run
```

#### Step 3 - Open Browser at LocalHost:5000

This last step seems trivial, however, it is often overlooked - trust me I have done it myself.  Flask in listening at 127.0.0.1 (i.e. the localhost) on port number 5000, so you need to go to this address to get the response you are looking for.  The Python code in the app.py knows to look in the "templates" folder for the index.html file that Robin is expecting to correctly display the data in her application.

## 3.0 Results

### 3.1 Mission to Mars Scraping Application

In figure 2 below you can see the the web scraping application that Robin was looking for has been completed and made to look highly professional.

![/Resources/2_The_Final_Product.png](/Resources/2_The_Final_Product.png "***Figure 2 - The Web Scraping Final Product***")

***Figure 2 - The Web Scraping Final Product***

### 3.2 Changes Made Using Bootstap 3

Changes to the application index.html file were facilitated using Bootstrap 3 which has a number of very convenient built in features.  The first change that I made was to the button to so it appears in red to remind Robin that she needs to press the button to retrieve new data into her application - see the code fence below.

```html
        <!-- <p><a class="btn btn-primary btn-lg" href="/scrape" role="button">Scrape New Data</a></p> -->
        <p><a class="btn btn-danger btn-lg" href="/scrape" role="button">Scrape New Data</a></p>
```

The latest news is very important so I bumped it up from an h4 to an h3 header, and also underlined it.

```html
              <!-- <h4 class="media-heading">{{ mars.news_title }}</h4> -->
              <h3 class="media-heading"><u>{{ mars.news_title }}</u></h3>
```

The paragraph about the latest news was then emphasized using the class "lead", which ended up looking very good. 

```html
              <!-- <p>{{ mars.news_paragraph }}</p> -->
              <p class="lead">{{ mars.news_paragraph }}</p>
```

I felt that the Mars Facts heading was way too small so I made it h2, the same as the other headings.

```html
            <!-- <h4>Mars Facts</h4> -->
            <h2>Mars Facts</h2>
```

Finally the hemispheres were nicely formatted as thumbnails as seen in the code fence below.

```python
        {% for hemisphere in mars.hemispheres %}
        <div class="col-md-3">
          <div class="thumbnail">
            <img src="{{hemisphere.img_url}}" alt="..."/>
            <div class="caption">
              <h3>{{hemisphere.title}}</h3>
            </div>
          </div>
        </div>
        {% endfor %}
```



### 3.3 Mobile Ready Application

Inspecting the web scarping application we can see, as demonstrated in figure 4 below, using an iPhone 12 Pro example, that Robin's scraping application is mobile ready.

![/Resources/3_Mobile_Ready_Application.png](/Resources/3_Mobile_Ready_Application.png "***Figure 3 - Mobile Ready Application***")

***Figure 3 - Mobile Ready Application***



### 3.4 Mongo Database Updated

Figure 4 below is a fully expanded view of the mars_app database showing that it has been updated with all of the scraped data including images and titles. 



![/Resources/4_Mongo_Database_Updated.png](/Resources/4_Mongo_Database_Updated.png "***Figure 4 - Mongo Database Updated***")

***Figure 4 - Mongo Database Updated***



## 4.0 Summary

Robin now has a web application that scapes:

- Latest news title and content from https://redplanetscience.com
- Featured image from https://spaceimages-mars.com
- Mars facts from https://galaxyfacts-mars.com
- Full-resolution images and titles of the four hemisphere images of Mars from https://marshemispheres.com

Her content is professionally presented with various Bootstrap 3 components and easily updated with the push of a button to get new data as needed.  All of the data is also conveniently stored in a NoSQL MongoDB database. 

Hopefully NASA will soon be contacting Robin.
