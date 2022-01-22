# Mission to Mars

## 1.0 Purpose

Senior data scientist, Robin, does freelance work in astronomy in her spare time and dreams of working for NASA in the future.  She wants to write a web scraping application that can pull all her data together in one place.  She needs to understand how web pages are structured so that she can write a Python script to navigate the pages she is interested in and collect the right information.  Since the data she is collecting is, in general, unstructured she has chosen to use a MongoDB document based database to hold the data that her is collecting. To put it all together in a web application, Robin will need to use the Flask web framework.  

## 2.0 How The  Program Works

The set up of this application is quite complex so I thought it would be helpful for Robin if I included figure 1 below taken from section 10.0.4 of the "Bootcamp: CARL-VIRT-DATA-PT-11-2021-U-B-TTH" course material.

![/Resources/1_The_Web_Scraping_Process.png](/Resources/1_The_Web_Scraping_Process.png "***Figure 1 - The Web Scraping Process***")

***Figure 1 - The Web Scraping Process***

With all of the pieces correctly configured there is sit the challenge of making sure that everything is up and running in the correct location on Robin's computer so that it will reliably perform every time she want to use it.   The steps below should be followed to achieve this outcoming:

#### Step 1 - Start Anaconda

There is a app.cmd file that I created in the main Mission-to-Mar directory called Start_Ananconda.cmd, double click the file and Anaconda will be launch in the right location to be affective.  The code for the part of the process is shown in the code fence below.

```bash
:: call <anaconda_dir>/Scripts/activate.bat <anaconda_dir>
Call %windir%\System32\cmd.exe "/K" C:\Users\Greg\anaconda3\Scripts\activate.bat C:\Users\Greg\anaconda3\envs\PythonData
```

#### Step 2 - Start Flask

Now that Anaconda is running in the right directory we can simple set the FLASK_APP to the Python file app.py and run Flask, as shown in the code fence below.

```bash
:: For our FLASK_APP environment variable, we want to modify the path that will run our app.py file so that we can run our file.
set FLASK_APP=app.py
flask run
```

#### Step 3 - Open Browser at LocalHost:5000

This last step seems trivial, however it is often overlooked - trust me I had done it myself.  Flask in listening at 127.0.0.1 (i.e. the localhost) on port number 5000, you need to go to this address to get the response you are looking for.  The Python code in the app.py knows to look in the "templates" folder for the index.html file that the Robin is expecting to see for her application.

## 3.0 Results