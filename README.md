# Hardcoded Token Scanner

This tool is designed to scan web pages and their linked JavaScript files for hardcoded tokens. It can help identify potential security issues by detecting sensitive information that might be exposed in the source code.

## Features

- Fetches the content of a given URL and scans for specified hardcoded tokens.
- Also scans JavaScript files linked in the HTML.
- Provides context around each token found to aid in identifying the source and impact of the exposure.
- Customizable user-agent headers to mimic different types of requests.

## Installation

To use this tool, you'll need Python installed on your machine. You can install the required dependencies using pip:

```bash
pip install requests beautifulsoup4 termcolor


Usage

    Clone the repository:



    Run the script:

bash

python scanner.py

    Follow the prompts to enter the URL to scan and the suspected leaked keys (comma-separated).

Example

bash

Enter the URL to scan: http://example.com
Enter the suspected leaked keys (comma-separated): apiKey, secretToken

The tool will then fetch the content from the specified URL and scan for the provided tokens, printing the context around any occurrences it finds.
Custom Headers

The script includes a custom header for identifying your traffic. You can modify the headers dictionary in the script to include any headers you need.

python

headers = {
    'User-Agent': 'Your Custom User Agent'
}

Error Handling

The script includes basic error handling to manage exceptions that may occur during the fetching and scanning process. If an error occurs, it will print an error message and continue execution.
Contributing

Contributions are welcome! If you have suggestions for improvements or find a bug, please open an issue or submit a pull request.
