
# University Search & Website Service  

A simple Flask‑based API pair + a Vue‑powered single‑page front‑end.  

---  

## Project Overview
This repo provides:

1. **Two Flask micro‑services** that share a single `UK_Universities.json` data file.  
   - **Listing service** – returns all university names or a filtered list.  
   - **Website service** – returns the website URLs for a given university name fragment.  

2. **A lightweight Vue 3 single‑page app** (`index.html`) that lets users search for universities, displays matching results, and shows the associated webpages inline.

The stack can be run locally, containerised, or deployed to IBM Code Engine, Render or any other similar service (static site + two web services).

---  

## API Services  

### Listing Service (`listing/app.py`)
| Endpoint | Method | Description |
|----------|--------|-------------|
| `/colleges` | `GET` | Returns **all** university names. |
| `/colleges/<name>` | `GET` | Returns names that **contain** the supplied `<name>` substring (case‑sensitive). |

**Response example**

```json
{
  "Colleges": [
    "University of Birmingham",
    "Birmingham City University",
    "University of Aberdeen"
  ]
}
```

### Website Service (websites/app.py)
| Endpoint | Method | Description |
|----------|--------|-------------|
| /websites/<name>	| GET	| Returns every web_pages entry for universities whose name contains <name>.

**Response example**

```json

{
  "Webpages": [
    "http://www.birmingham.ac.uk/",
    "http://www.bcu.ac.uk/"
  ]
}
```

Both services enable CORS (flask_cors.CORS) so they can be called directly from the front‑end.


### Front‑end Application

A single `index.html` file (Vue 3 CDN) provides:

    - **Search input** – user types a university fragment.
    - **Fetch** to the listing service → displays a deduplicated list of matching colleges.
    - **Click a college** → fetches its webpages from the website service and renders them inline (no new tab).

Key features

    - Loading spinners & error messages.
    - URL‑encoding of user input.
    - Simple, responsive styling without any build tools.

