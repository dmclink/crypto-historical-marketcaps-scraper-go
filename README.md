# crypto-historical-marketcaps-scraper-go
Scrapes Coinmarketcap historical snapshots for the market cap list and stores them in a postgresql14 database

# Requirements
Go
PostgreSQL14
Chrome
ChromeDriver

# Setup Instructions
1. Create database in psql shell or equivalent
    - (optional) Create new user in psql shell with rights to CREATE SELECT and INSERT to table
    - (optional) If exporting the db to .csv file is desired, grant user pg_write_server_files rights or superuser
2. Rename db_sample.env to db.env
3. Fill in db.env by changing "default" to your datebase and psql information and save
4. Ensure version of ChromeDriver matches version of chrome installed on your system
5. Install or copy chromedriver.exe to root folder of this project
    - (Alternative 1) Change variable chromeDriverPath to absolute path of chromedriver.exe
    - (Alternative 2) Enter absolute path of chromedriver.exe at the error prompt after running program
