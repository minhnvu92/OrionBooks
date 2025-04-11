# OrionBooks API

A .NET 8 Web API for managing manga series, volumes, and pages using Google Sheets as a database.

## Prerequisites

- .NET 8 SDK
- Docker (optional)
- Google Cloud Platform account with Google Sheets API enabled
- Google Sheets service account credentials

## Setup

1. Clone the repository
2. Create a Google Cloud Project and enable the Google Sheets API
3. Create a service account and download the credentials JSON file
4. Create a Google Spreadsheet with the following sheets:
   - Series
   - Volumes
   - Pages
5. Share the spreadsheet with the service account email
6. Copy the credentials JSON file to the project root and name it `credentials.json`
7. Update the `appsettings.json` file with your spreadsheet ID

## Configuration

Update the following settings in `appsettings.json`:

```json
{
  "GoogleSheets": {
    "SpreadsheetId": "YOUR_SPREADSHEET_ID",
    "CredentialsPath": "credentials.json"
  }
}
```

## Running the Application

### Local Development

```bash
cd OrionBooks.API
dotnet run
```

### Docker

```bash
docker build -t orionbooks-api .
docker run -p 8080:80 orionbooks-api
```

## API Endpoints

### Series
- GET `/api/series` - Get all series (with optional filters)
- GET `/api/series/{id}` - Get a specific series by ID

### Volumes
- GET `/api/volumes/series/{seriesId}` - Get all volumes for a series
- GET `/api/volumes/{id}` - Get a specific volume by ID

### Pages
- GET `/api/pages/volume/{volumeId}` - Get all pages for a volume
- GET `/api/pages/{id}` - Get a specific page by ID

## Filtering Series

The `/api/series` endpoint supports the following query parameters:
- `author` - Filter by author name
- `date` - Filter by creation date
- `popularity` - Filter by minimum popularity score
- `category` - Filter by genre/category

Example: `/api/series?author=John&popularity=80&category=Action` 