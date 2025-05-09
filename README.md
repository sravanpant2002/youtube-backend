# YouTube Content Search API

A FastAPI-based API service that performs advanced YouTube content searches using both YouTube Data API and Google Custom Search API, with support for multiple API keys and intelligent quota management.

## Features

- Advanced YouTube content search using multiple API sources
- Support for multiple YouTube API keys with automatic rotation
- Google Custom Search integration for broader results
- Automatic quota management and error handling
- Brand-related link extraction from video descriptions
- Relevancy scoring and result ranking
- Asynchronous processing for better performance

## Prerequisites

- Python 3.9+
- YouTube Data API v3 API Keys
- Google Custom Search API Key and Search Engine ID
- FastAPI and dependencies

## Installation

1. Clone the repository:
```bash
git clone https://github.com/sravanpant/youtube-search-backend.git
cd youtube-search-backend
```

2. Create and activate a virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

## Configuration

1. Create a `.env` file in the project root with your API keys:
```env
YOUTUBE_API_KEY_1=your_first_youtube_api_key
YOUTUBE_API_KEY_2=your_second_youtube_api_key
...
YOUTUBE_API_KEY_21=your_21st_youtube_api_key
GOOGLE_CSE_API_KEY=your_google_cse_api_key
GOOGLE_CSE_ID=your_google_cse_id
```

## Usage

1. Start the server:
```bash
uvicorn main:app --reload
```

2. The API will be available at `http://localhost:8000`

3. Make API requests:
```bash
curl -X POST "http://localhost:8000/search" \
     -H "Content-Type: application/json" \
     -d '{
           "brand_name": "example brand, another brand",
           "max_results": 30,
           "min_views": 1000
         }'
```

## API Endpoints

### POST /search

Search for YouTube videos related to specified brands/keywords.

**Request Body:**
```json
{
    "brand_name": "string",  // Comma-separated keywords
    "max_results": int,      // Maximum number of results to return
    "min_views": int        // Minimum view count for videos
}
```

**Response:**
```json
[
    {
        "videoId": "string",
        "title": "string",
        "channelTitle": "string",
        "channelId": "string",
        "publishTime": "string",
        "viewCount": int,
        "likeCount": int,
        "commentCount": int,
        "subscriberCount": int,
        "duration": "string",
        "description": "string",
        "thumbnails": object,
        "videoLink": "string",
        "channelLink": "string",
        "relevancy_score": int,
        "brand_links": ["string"]
    }
]
```

## Project Structure

```
youtube-content-search/
├── main.py              # Main FastAPI application
├── models.py            # Pydantic models
├── utils.py            # Utility functions
├── requirements.txt    # Project dependencies
├── .env               # Environment variables
├── README.md          # Project documentation
```


## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- YouTube Data API v3
- Google Custom Search API
- FastAPI framework
- Async Python community

