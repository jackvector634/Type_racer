Typeracer Activity Tracker


Here's a polished version of your Twitter blog:

Title: Typeracer Activity Tracker

Activity Score: Words Per Minute (WPM)

I recently worked on a GitHub Actions project that tracks your typing speed on Typeracer. Using the Typeracer API and a provided username, this project fetches your WPM score every 24 hours through a CRON job and automatically updates your GitHub README.md with a visual plot of your performance.

typeracer-readme generates typeracer graph for profile readme

<a href="">
  <img src="https://raw.githubusercontent.com/jackvector634/Type_racer/typeracer-readme/dark_graph.png" alt="typeracer graph" height="260"/>
</a>


# how it works
  getting data from typeracer with your username
  
  1000 at a time, looping until it gets all racing data
  
  generate two theme graphs (light and dark) images, and data.json file

# setup workflow
  copy script.py and requirements.txt into root directory of your repo
  
  copy typeracer_graph.yml yaml file into .github/workflows directory

# configure script.py
  username variable
   
  start_date variable (YYYY-MM-DD)
  
  average-window

# adding graph to readme
  add image with `src = "https://raw.githubusercontent.com/YOUR_USERNAME/YOUR_REPOSITORY/typeracer-readme/dark_graph.png"`
   
  typeracer-readme above determines the branch in which images are saved

We retrieve typing race data in JSON format from Typeracer, with details like race number, WPM, timestamp, and accuracy. Here's an example of the data:

```json
[
    {
        "gn": 1,
        "wpm": 35,
        "t": 1672856487,
        "un": "john_doe",
        "p": "The quick brown fox jumps over the lazy dog.",
        "r": 95
    },
    {
        "gn": 2,
        "wpm": 38,
        "t": 1672856500,
        "un": "john_doe",
        "p": "Pack my box with five dozen liquor jugs.",
        "r": 98
    },
    {
        "gn": 3,
        "wpm": 42,
        "t": 1672856520,
        "un": "john_doe",
        "p": "How razorback-jumping frogs can level six piqued gymnasts.",
        "r": 99
    }
]
This project fetches up to 1000 races at a time, covering all races from a specified start date up to the present. To handle the data, we use date conversion functions like date_to_js_timestamp(date_str) and js_timestamp_to_date(timestamp) to manage Unix timestamps.

Finally, the race numbers and WPM values are extracted, averaged, and plotted against each other, giving a clear visual representation of your progress over time.

