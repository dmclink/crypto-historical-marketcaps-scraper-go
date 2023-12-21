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
    - (optional) Adjust configs constants as necessary. If program panics with "runtime error: index out of range" it is likely that scrollDelay is too low or viewportScrollMult is too high
        - const tableName - Program will check for/create a table with this name
        - const skipNoMcap - CMC begins ranking coins ordered by descending price where no supply or market cap is known. Leaving this const true will skip these coins, speeding up row processing and saving storage in database especially for later snapshot dates. Set to false to include them
        - const maxRows - Program will only insert this number of rows into database. Setting to zero or negative value will let the program run without limit. Setting to lower amount can greatly reduce scroll time and row processing time. Depending on your machine's memory, higher (eg 4000) maxRows on later snapshot dates may cause memory errors and slow your machine. As of 12/20/2023, there are no snapshot dates with more than 3000 coins that have marketcap data  
        - const exportCSV - If set to true, program will export database to .csv file after it finishes scraping up to current date