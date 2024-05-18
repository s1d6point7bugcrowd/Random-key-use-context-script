import requests
from bs4 import BeautifulSoup
import re
from termcolor import colored

# Function to get user input safely
def get_input(prompt):
 try:
 return input(prompt)
 except Exception as e:
 print(colored(f"Error while receiving input: {e}", 'red'))
 return None

# Custom header for identifying traffic
headers = {
 'User-Agent': ''
}

def fetch_and_scan(url, tokens):
 """
 Fetches the content of the URL and scans for hardcoded tokens.
 Also fetches and scans JavaScript files found in the HTML.
 """
 try:
 response = requests.get(url, headers=headers, timeout=10) # Including timeout
 response.raise_for_status() # Check for HTTP errors
 content = response.text
 soup = BeautifulSoup(content, 'html.parser')

 # Scan the main page content
 scan_content(url, content, tokens)

 # Find and scan linked JavaScript files
 for script_tag in soup.find_all('script', src=True):
 script_url = script_tag['src']
 if not script_url.startswith('http'):
 script_url = f"{url.rstrip('/')}/{script_url.lstrip('/')}"
 scan_content(script_url, requests.get(script_url, headers=headers, timeout=10).text, tokens) # Including timeout

 except requests.RequestException as e:
 print(colored(f"Failed to fetch {url}: {e}", 'red'))

def scan_content(url, content, tokens):
 """
 Scans the provided content for the tokens and prints the surrounding context.
 """
 for token in tokens:
 if token in content:
 print(colored(f"Token {token} found in {url}", 'green'))
 start_index = content.find(token)
 # Print context around the token occurrence
 context_start = max(content.rfind('\n', 0, start_index) - 1, 0)
 context_end = content.find('\n', start_index + len(token), len(content))
 context = content[context_start:context_end]
 highlighted_context = context.replace(token, colored(token, 'yellow', 'on_red'))
 print("Context surrounding token occurrence:")
 print(highlighted_context)
 print("---------------------------------------")

if __name__ == "__main__":
 input_url = get_input("Enter the URL to scan: ")
 input_tokens_str = get_input("Enter the suspected leaked keys (comma-separated): ")
 if input_url and input_tokens_str:
 tokens = [token.strip() for token in input_tokens_str.split(',')]
 fetch_and_scan(input_url, tokens)

