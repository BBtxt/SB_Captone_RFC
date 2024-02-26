# Project Proposal for SpringBoard Capstone Project * Movie Thing *

## Abstract

The goal of this project is to create a a web app that will allow users to search for movies based off of the subscription services that they already have. The app will recommend movies and tv shows based off of criteria such as genre, language, streaming location, popularity, and release date. The app will also allow users to create a watchlist and will notify them when a movie or tv show is available on a streaming service that they have access to.

## Design

The app will be designed with a combination of Flask, HTML, CSS. The app will use the TMDB Api to pull in movie and TV show data. The app will also use the JustWatch API to pull in streaming service data. The app will use a combination of user input and data from the APIs to recommend movies and TV shows to the user. The app will also use user input to create a watchlist and notify the user when a movie or TV show is available on a streaming service that they have access to. To ensure that there are no issues with querying the APIs, the app will use drop down menus and check boxes to limit the amount of user input required. This will also allow the app to be more user friendly.

## Database

The app will use a PSQL Database to store user information and watchlist data.

User Table:

- user_id (primary key)
- username > string
- email > string
- password > string
  
Watchlist Table:

- watchlist_id
- user_id (foreign key)
- movie_id (maybe store the movie name)
- tv_show_id (maybe store the tv show name)
- streaming_service_id (maybe store the streaming service name)
- liked (boolean)
- disliked (boolean)
- Cover Image URL
  
  - Some consideration when designing the watchlist table, It maybe easier for now to store the movie/TV show as string once the the user adds it to the watchlist. This will result in less queries to the TMDB API. However, this will result in a larger database. Also, mapping the movie/TV show to the streaming service will be a challenge. The Downside of this approach is that there will be no way to update the watchlist if the movie/TV show is removed from the streaming service. The upside is that it will be easier to implement.

## Routes

    HomePage (/)
    - Scrolling banner of popular movies and TV shows
    - Login/Sign Up button 
    - Navbar
      -Name of the app on right, login/sign, watchlist up on left (based on user session state) 

    Registration Page (/signup)
    - Form to register for the app (WTFORMS)
      - username
      - email
      - password
    - Sign Up button
      - Maybe set up a email confirmation
    - Navbar
    -Redirects 
        - If user is already logged in, redirect to Dashboard
        - If user is not logged in, show the registration html

    Dashboard (/dashboard/<username>)
    - Navbar
    - first div
        - Welcome user by username
        - Show list of active streaming services
        - Show list of favorite genres
      - second div
        - Search bar
        - Dropdown menu for streaming services
        - Dropdown menu for genres
        - Dropdown menu for language
        - Dropdown menu for release date
        - Dropdown menu for popularity
        - Search button
      - third div
        - List watchlist
          - Show title, poster, streaming service, date added, maybe a remove button or description
  
    Search Results Page (/search)

    - Navbar
    - Only pull 5 results at a time
      - custom logic to randomize the results
      - change the results on refresh
    - List of movies and TV shows based off of user input
      - Show title, poster, streaming service, date added, maybe a remove button or description
      - show card with movie/tv show details
      - show card with streaming service details
      - Add to watchlist button 
        - JS to change styles on click
        - JS to add to watchlist (use AJAX to update database keeps user on the same page)
  
    Watchlist Page (/watchlist)

    Navbar
    - show 5 results at a time
      - need figure out how to keep the watchlist in the same order maybe use a timestamp (fifo queue)
      - keep order if more than 5 results especially if the user needs more than one page
    - List watchlist
      - Show title, poster, streaming service, date added, maybe a remove button or description
      - show card with movie/tv show details
      - show card with streaming service details
      - Remove from watchlist button 
        - JS to change styles on click
        - JS to remove from watchlist (use AJAX to update database keeps user on the same page)
    
    Edit User Page (/edit/<username>)

    - Navbar
    - Form to edit user information (WTFORMS)
      - username
      - email
      - password
      - add/remove streaming services
        - drop down menu (multiple select)
      - add/remove favorite genres
        - drop down menu (multiple select)
  
## Testing

    - Test routes
    - Test database queries
    - Test API queries
    - Test user input
      - Streaming services icons
      - Genre names
      - Search input
      - Validation
    - Test user session
        - Login
        - Logout
        - Registration
        - Edit user information
        - Delete user account
  
## Schedule 
    1. Week 1
        - Set up Flask app
          - Models
          - forms
          - routes
        - Set up PSQL database
        - JS for watchlist
        - TMDB API
        - JustWatch API
        - Tests
        - bare bones HTML/CSS
    2. Week 2
        - Finish HTML/CSS
        - Finish JS
        - Finish API queries
        - Finish tests
    3. Week 3  
        - Deploy d8
        - Add Cool Features:
          - Scrolling banner
          - Scrolling watchlist
          - Vibey CSS
          - random movie/tv show generator (based off of user preferences)
          - hide disliked shows
          - email confirmation
          - delete account popup
          - infinite scroll on watchlist/search results/dashoard banner

