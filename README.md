import requests
import csv

def fetch_and_save_posts(filename='posts.csv'):
    """
    Fetches posts from a public API and saves the title and body
    of each post into a CSV file.
    """
    try:
        # Define the API endpoint
        api_url = 'https://jsonplaceholder.typicode.com/posts'
        
        # Make the GET request to the API
        response = requests.get(api_url)
        response.raise_for_status()  # Raise an exception for bad status codes
        
        # Parse the JSON response
        posts_data = response.json()
            
            # Write the header row
            writer.writeheader()
            
            # Write each post to the CSV file
            for post in posts_data:
                writer.writerow({
                    'id': post.get('id'),
                    'title': post.get('title'),
                    
                })
        
        print(f"Successfully fetched {len(posts_data)} posts and saved them to {filename}")

    except requests.exceptions.RequestException as e:
        print(f"An error occurred while fetching data: {e}")
    except IOError as e:
        print(f"An error occurred while writing to the file: {e}")
    except Exception as e:
        print(f"An unexpected error occurred: {e}")

if __name__ == "__main__":
    fetch_and_save_posts()
