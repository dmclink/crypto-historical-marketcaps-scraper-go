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
6. Run
    - (optional) Adjust constants as necessary. If program quits on "Error finding \"Rank" column" it is likely that scrollDelay is too low or viewportScrollMult is too high
    - (optional) Rename constant tableName if desired. Program will check for/create a table with this name
    - (optional) Adjust const skipNoMcap if desired. CMC begins ranking coins ordered by descending price where no supply or market cap is known. Leaving this const true will skip these coins, speeding up row processing and saving storage in database especially for later snapshot dates. Set to false to include them