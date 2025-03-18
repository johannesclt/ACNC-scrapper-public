# ACNC Scraper

A comprehensive tool for scraping, analyzing, and managing data from the Australian Charities and Not-for-profits Commission (ACNC) website.

## Features

- **Multiple Search Modes**: Search by property (size/state), by ABN, or using a CSV file
- **Rich Data Extraction**: Collects organization details, financial data, board members, and charity programs
- **Database Management**: Stores all data in a SQLite database for easy management and updating
- **Cache Management**: Intelligent caching to avoid unnecessary re-scraping
- **Export Options**: Export to CSV or Excel formats, with consolidated or table-specific outputs
- **Parallel Processing**: Efficient multi-threading for faster data retrieval
- **Robust Error Handling**: Retry logic and detailed logging for reliable operation

## Installation

1. Clone the repository:
   ```
   git clone https://github.com/johannesclt/ACNC_Scrapper.git
   cd acnc-scraper
   ```

2. Create a virtual environment (recommended):
   ```
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. Install dependencies:
   ```
   pip install -r requirements.txt
   ```

4. Download ChromeDriver:
   - Download the version matching your Chrome browser from: https://chromedriver.chromium.org/downloads
   - Alternatively, if you installed `webdriver-manager`, the script can handle this automatically

## Usage

### Basic Usage

```bash
# Clear cache to ensure fresh data
python acnc_scraper.py clearcache

# Search by ABN
python acnc_scraper.py abn --abn 12345678901 --no-headless

# Search by property (e.g., all Medium charities in Victoria)
python acnc_scraper.py peakbody --size Medium --state Victoria --no-headless

# Process organizations from a CSV file
python acnc_scraper.py csv --csv your_file.csv --no-headless
```

### Common Options

- `--no-headless`: Run with a visible browser window (useful for debugging)
- `--force-scrape`: Ignore cached data and scrape everything again
- `--chromedriver "path/to/chromedriver"`: Specify a custom ChromeDriver path
- `--output "output_file.csv"`: Specify output file for results

### Advanced Usage

```bash
# Update only board members for a specific ABN
python acnc_scraper.py board --abn 12345678901

# Export all database contents to CSV
python acnc_scraper.py export --consolidated

# Check database integrity and repair issues
python acnc_scraper.py checkdb

# Show statistics about the database
python acnc_scraper.py stats

# Migrate data to PostgreSQL (requires psycopg2-binary)
python acnc_scraper.py postgres --host localhost --port 5432 --dbname acnc --user postgres --password mysecretpassword
```

## Troubleshooting

If you encounter issues:

1. Try running with `--no-headless` to see what's happening
2. Check the `acnc_scraper.log` file for detailed error messages
3. Run `python acnc_scraper.py checkdb` to verify database integrity
4. Try using a specific ChromeDriver path with `--chromedriver`
5. Clear the cache with `python acnc_scraper.py clearcache`

## Project Structure

- `acnc_scraper.py` - Main script and command-line interface
- `config.py` - Configuration settings
- `db_manager.py` - Database operations
- `cache_manager.py` - Cache clearing functions
- `web_scraper.py` - Web scraping operations
- `modes.py` - Various scraping modes
- `utils.py` - Utility functions

## License

This project is licensed under the MIT License - see the LICENSE file for details.
