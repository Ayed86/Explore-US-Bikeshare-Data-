# Explore-US-Bikeshare-Data-
In this project, you will make use of Python to explore data related to bike share systems for three major cities in the United States—Chicago, New York City, and Washington. You will write code to import the data and answer interesting questions about it by computing descriptive statistics. You will also write a script that takes in raw input to create an interactive experience in the terminal to present these statistics.
What Software Do I Need?
To complete this project, the following software requirements apply:
•	You should have Python 3, NumPy, and pandas installed using Anaconda
•	A text editor, like Sublime or Atom.
•	A terminal application (Terminal on Mac and Linux or Cygwin on Windows).


Bike Share Data
Over the past decade, bicycle-sharing systems have been growing in number and popularity in cities across the world. Bicycle-sharing systems allow users to rent bicycles on a very short-term basis for a price. This allows people to borrow a bike from point A and return it at point B, though they can also return it to the same location if they'd like to just go for a ride. Regardless, each bike can serve several users per day.
Thanks to the rise in information technologies, it is easy for a user of the system to access a dock within the system to unlock or return bicycles. These technologies also provide a wealth of data that can be used to explore how these bike-sharing systems are used.
In this project, you will use data provided by Motivate, a bike share system provider for many major cities in the United States, to uncover bike share usage patterns. You will compare the system usage between three large cities: Chicago, New York City, and Washington, DC.
The Datasets
Randomly selected data for the first six months of 2017 are provided for all three cities. All three of the data files contain the same core six (6) columns:
•	Start Time (e.g., 2017-01-01 00:07:57)
•	End Time (e.g., 2017-01-01 00:20:53)
•	Trip Duration (in seconds - e.g., 776)
•	Start Station (e.g., Broadway & Barry Ave)
•	End Station (e.g., Sedgwick St & North Ave)
•	User Type (Subscriber or Customer)
The Chicago and New York City files also have the following two columns:
•	Gender
•	Birth Year
 
Data for the first 10 rides in the new_york_city.csv file
The original files are much larger and messier, and you don't need to download them, but they can be accessed here if you'd like to see them (Chicago, New York City, Washington). These files had more columns and they differed in format in many cases. Some data wrangling has been performed to condense these files to the above core six columns to make your analysis and the evaluation of your Python skills more straightforward.
Statistics Computed
You will learn about bike share use in Chicago, New York City, and Washington by computing a variety of descriptive statistics. In this project, you'll write code to provide the following information:
#1 Popular times of travel (i.e., occurs most often in the start time)
•	most common month
•	most common day of week
•	most common hour of day
#2 Popular stations and trip
•	most common start station
•	most common end station
•	most common trip from start to end (i.e., most frequent combination of start station and end station)
#3 Trip duration
•	total travel time
•	average travel time
#4 User info
•	counts of each user type
•	counts of each gender (only available for NYC and Chicago)
•	earliest, most recent, most common year of birth (only available for NYC and Chicago)
The Files
To answer these questions using Python, you will need to write a Python script. To help guide your work in this project, a template with helper code and comments is provided in a bikeshare.py file, and you will do your scripting in there also. You will need the three city dataset files too:
•	chicago.csv
•	new_york_city.csv
•	washington.csv
All four of these files are zipped up in the "all_project_files" document in the Resources tab in the sidebar on the left side of this page. (You may need to scroll down inside the Resources tab to see the "all_project_files" doc.) You can choose to download and unzip that "all_project_files" doc to access all four project files, and do your project work on your local machine.
If you'd prefer, the later Project Workspace page in the classroom here also has the bikeshare.py file and all the city dataset files included in it, and you can do all your work on the project with them there. If you choose this option, you don't need to download the files from the Resources tab.
Code Walkthrough
Code Walkthrough                                                                                                                                     
You may use the template provided in bikeshare.py to complete this project. You should feel free to change the template however you'd like, as long as your code provides the statistics shown in the template, and allows a user to give input on which data they would like to see.                                                                             
An Interactive Experience
The bikeshare.py file is set up as a script that takes in raw input to create an interactive experience in the terminal that answers questions about the dataset. The experience is interactive because depending on a user's input, the answers to the questions on the previous page will change! There are four questions that will change the answers:
1.	Would you like to see data for Chicago, New York, or Washington?
2.	Would you like to filter the data by month, day, or not at all?
3.	(If they chose month) Which month - January, February, March, April, May, or June?
4.	(If they chose day) Which day - Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, or Sunday?
The answers to the questions above will determine the city and timeframe on which you'll do data analysis. After filtering the dataset, users will see the statistical result of the data, and choose to start again or exit.
Remember that any time you ask users for input, there is a chance they may not enter what you expect, so your code should handle unexpected input well without failing. You need to anticipate raw input errors like using improper upper or lower case, typos, or users misunderstanding what you are expecting. Use the tips provided in the sections of the Scripting lesson in this course to make sure your code does not fail with an execution error due to unexpected raw input.
Your script also needs to prompt the user whether they would like want to see the raw data. If the user answers 'yes,' then the script should print 5 rows of the data at a time, then ask the user if they would like to see 5 more rows of the data. The script should continue prompting and printing the next 5 rows at a time until the user chooses 'no,' they do not want any more raw data to be displayed.
Note that this bikeshare.py file is simply a template you can use, but you are not required to use it. You can change the functions however you like as long as you have an ending product that meets the project requirements. Changes to the structure of bikeshare.py (e.g., adding and/or deleting helper functions) that you think make the code more efficient or have a better style are encouraged.

Option #2) You can work on your Python script on your local machine. To do this, you should download the necessary project files from the Resources tab (the folder icon in the left sidebar here).
If you choose this option #2, please submit your project using the button on the last page of this lesson, "Project: Explore US Bikeshare Data," where you will be able to upload your project files.
You should choose one of these two options above - don't try to submit your project in both places.
With either option, before you submit, make sure your project meets all the necessary elements of the Project Rubric.

# The answer:

import time
import pandas as pd
import numpy as np

CITY_DATA = { 'chicago': 'chicago.csv',
              'new york city': 'new_york_city.csv',
              'washington': 'washington.csv' }

def get_filters():
    """
    Asks user to specify a city, month, and day to analyze.

    Returns:
        (str) city - name of the city to analyze
        (str) month - name of the month to filter by, or "None" to apply no month filter
        (str) day - name of the day of week to filter by, or "None" to apply no day filter
    """
    print('Hello! Let\'s explore some US bikeshare data!')
    # get user input for city (chicago, new york city, washington).
    while True:
        cities= ['chicago','new york city','washington']
        city= input("\n Which city would you like to analyse? (Chicago, New york city, Washington) \n").lower()
        if city in cities:
            break
        else:
            print("\n Please enter a valid city name")    


    # get user input for month (january, february, ... , june or none)
    while True:
        months= ['January','February','March','April','June','May','None']
        month = input("\n Which month would you like to consider? (January, February, March, April, May, June)? Type 'None' for no month filter\n").title()
        if month in months:
            break
        else:
            print("\n Please enter a valid month")    


    # get user input for day of week (monday, tuesday, ... sunday or none)
    while True:
        days= ['Monday','Tuesday','Wednesday','Thursday','Friday','Saturday','Sunday','None']
        day = input("\n Which day of the week would you like to consider? (Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday)? Type 'None' for no day filter \n").title()         
        if day in days:
            break
        else:
            print("\n Please enter a valid day")    
    


    print('-'*40)
    return city, month, day


def load_data(city, month, day):
    """
    Loads data for the specified city and filters by month and day if applicable.

    Args:
        (str) city - name of the city to analyze
        (str) month - name of the month to filter by, or "None" to apply no month filter
        (str) day - name of the day of week to filter by, or "None" to apply no day filter
    Returns:
        df - Pandas DataFrame containing city data filtered by month and day
    """

    
    # load data file into a dataframe
    df = pd.read_csv(CITY_DATA[city])

    # convert the Start Time column to datetime
    df['Start Time'] = pd.to_datetime(df['Start Time'])

    # extract month and day of week from Start Time to create new columns
    df['month'] = df['Start Time'].dt.month
    df['day_of_week'] = df['Start Time'].dt.weekday_name


    # filter by month if applicable
    if month != 'None':
        # use the index of the months list to get the corresponding int
        months = ['January', 'February', 'March', 'April', 'May', 'June']
        month = months.index(month)+1
    
        # filter by month to create the new dataframe
        df = df[df['month']==month] 

    # filter by day of week if applicable
    if day != 'None':
        # filter by day of week to create the new dataframe
        df = df[df['day_of_week']==day]

    return df


def time_stats(df,month,day):
    """Displays statistics on the most frequent times of travel."""

    print('\nCalculating The Most Frequent Times of Travel...\n')
    start_time = time.time()

    # display the most common month
    if month =='None':
        pop_month= df['month'].mode()[0]
        months= ['January','February','March','April','May','June']
        pop_month= months[pop_month-1]
        print("The most Popular month is",pop_month)


    # display the most common day of week
    if day =='None':
        pop_day= df['day_of_week'].mode()[0]
        print("The most Popular day is",pop_day)


    # display the most common start hour
    df['Start Hour'] = df['Start Time'].dt.hour
    pop_hour=df['Start Hour'].mode()[0]
    print("The popular Start Hour is {}:00 hrs".format(pop_hour))


    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def station_stats(df):
    """Displays statistics on the most popular stations and trip."""
    print('\nCalculating The Most Popular Stations and Trip...\n')
    start_time = time.time()

    # display most commonly used start station
    pop_start_station= df['Start Station'].mode()[0]
    print("The most commonly used Start Station is {}".format(pop_start_station))


    # display most commonly used end station
    pop_end_station= df['End Station'].mode()[0]
    print("The most commonly used End Station is {}".format(pop_end_station))

    # display most frequent combination of start station and end station trip
    df['combination']=df['Start Station']+" "+"to"+" "+ df['End Station']
    pop_com= df['combination'].mode()[0]
    print("The most frequent combination of Start and End Station is {} ".format(pop_com))


    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def trip_duration_stats(df):
    """Displays statistics on the total and average trip duration."""

    print('\nCalculating Trip Duration...\n')
    start_time = time.time()

    # display total travel time
    total_duration=df['Trip Duration'].sum()
    minute,second=divmod(total_duration,60)
    hour,minute=divmod(minute,60)
    print("The total trip duration: {} hour(s) {} minute(s) {} second(s)".format(hour,minute,second))
    
    # display mean travel time
    average_duration=round(df['Trip Duration'].mean())
    m,sec=divmod(average_duration,60)
    if m>60:
        h,m=divmod(m,60)
        print("The total trip duration: {} hour(s) {} minute(s) {} second(s)".format(h,m,sec))
    else:
        print("The total trip duration: {} minute(s) {} second(s)".format(m,sec))

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def user_stats(df,city):
    """Displays statistics on bikeshare users."""

    print('\nCalculating User Stats...\n')
    start_time = time.time()

    # Display counts of user types
    user_counts= df['User Type'].value_counts()
    print("The user types are:\n",user_counts)


    # Display counts of gender
    if city.title() == 'Chicago' or city.title() == 'New York City':
        gender_counts= df['Gender'].value_counts()
        print("\nThe counts of each gender are:\n",gender_counts)
    
    # Display earliest, most recent, and most common year of birth
        earliest= int(df['Birth Year'].min())
        print("\nThe oldest user is born of the year",earliest)
        most_recent= int(df['Birth Year'].max())
        print("The youngest user is born of the year",most_recent)
        common= int(df['Birth Year'].mode()[0])
        print("Most users are born of the year",common)


    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)

def display_data(df):

    while True:
        response=['yes','no']
        choice= input("Would you like to view individual trip data (5 entries)? Type 'yes' or 'no'\n").lower()
        if choice in response:
            if choice=='yes':
                start=0
                end=5
                data = df.iloc[start:end,:9]
                print(data)
            break     
        else:
            print("Please enter a valid response")
    if  choice=='yes':       
            while True:
                choice_2= input("Would you like to view more trip data? Type 'yes' or 'no'\n").lower()
                if choice_2 in response:
                    if choice_2=='yes':
                        start+=5
                        end+=5
                        data = df.iloc[start:end,:9]
                        print(data)
                    else:    
                        break  
                else:
                    print("Please enter a valid response")              


def main():
    while True:
        city, month, day = get_filters()
        df = load_data(city, month, day)
        
        time_stats(df,month,day)
        station_stats(df)
        trip_duration_stats(df)
        user_stats(df,city)
        display_data(df)

        restart = input('\nWould you like to restart? Enter yes or no.\n')
        if restart.lower() != 'yes':
            break


if __name__ == "__main__":
	main()


