# web_scraping

# Web Scraping "List of Largest Companies by Revenue" Using Python

## Overview

This project is focused on scraping the "List of Largest Companies by Revenue" from a specified website using Python. The goal is to extract relevant information such as the company names, revenue figures, and other pertinent details, and save this data into a structured format like CSV for further analysis.

## Requirements

Before you begin, ensure you have the following software and libraries installed:

1. **Python 3.x**: The programming language used for the project.
2. **pip**: Python package installer.
3. **Libraries**:
    - `requests`: For making HTTP requests to fetch the web page content.
    - `BeautifulSoup4`: For parsing the HTML content.
    - `pandas`: For storing the extracted data in a structured format.
    - `lxml`: An XML and HTML processing library used by BeautifulSoup4.

You can install the required libraries using pip:

```bash
pip install requests beautifulsoup4 pandas lxml
```

## Files in the Repository

- `scrape_companies.py`: The main Python script for scraping the data.
- `README.md`: This file, providing an overview of the project.
- `requirements.txt`: A file listing all required Python libraries.
- `output/`: A directory where the output CSV file will be saved.

## How to Run the Script

1. **Clone the Repository**:
    ```bash
    git clone https://github.com/yourusername/largest-companies-scraper.git
    cd largest-companies-scraper
    ```

2. **Install Dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

3. **Run the Script**:
    ```bash
    python scrape_companies.py
    ```

4. **Check the Output**:
    After running the script, check the `output/` directory for a CSV file containing the scraped data.

## Script Details

### `scrape_companies.py`

This script performs the following steps:

1. **Fetch the Web Page**:
    Uses the `requests` library to get the HTML content of the target webpage.

    ```python
    import requests

    url = 'https://example.com/largest-companies-by-revenue'
    response = requests.get(url)
    ```

2. **Parse the HTML**:
    Utilizes `BeautifulSoup4` to parse the fetched HTML content.

    ```python
    from bs4 import BeautifulSoup

    soup = BeautifulSoup(response.content, 'lxml')
    ```

3. **Extract Data**:
    Extracts relevant information such as company names, revenue, and other details from the parsed HTML.

    ```python
    companies = []
    table = soup.find('table', {'class': 'wikitable'})
    
    for row in table.find_all('tr')[1:]:
        columns = row.find_all('td')
        company = {
            'name': columns[0].text.strip(),
            'revenue': columns[1].text.strip(),
            # Add more fields as necessary
        }
        companies.append(company)
    ```

4. **Save Data**:
    Stores the extracted data into a CSV file using the `pandas` library.

    ```python
    import pandas as pd

    df = pd.DataFrame(companies)
    df.to_csv('output/largest_companies_by_revenue.csv', index=False)
    ```

## Notes

- **Error Handling**: The script includes basic error handling for network requests and HTML parsing. 
- **Dependencies**: Ensure all dependencies are correctly installed. Refer to `requirements.txt` for the complete list.
- **Website Structure**: The script assumes a specific structure for the target webpage. If the structure changes, the script may need modifications.

## Contributions

Contributions to this project are welcome. Please fork the repository and create a pull request with your changes. Ensure your code adheres to the PEP 8 style guide.

## License

This project is licensed under the MIT License. See the `LICENSE` file for more details.

---

Feel free to customize this README further to fit your project's specifics!
