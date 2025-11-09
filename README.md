# ghbkp

ghbkp is a tool for creating a local backup of a github repository's issues, pull requests, and discussions. It uses two scripts to first fetch the data into a single json file and then convert that file into a set of human-readable markdown files.

## Features

- Fetches complete data for issues, pull requests, and discussions.
- Retrieves all associated comments, review threads, and replies.
- Manages github graphql api pagination and rate limits.
- Converts the collected data into a directory of markdown files.
- Creates an index file that links to all generated documents.

## Usage

### Prerequisites

- Python 3.
- A github personal access token with `repo` and `read:discussion` scopes. [Create one here](https://github.com/settings/tokens/new).

### Step 1: Fetch repository data

This step uses `ghscrape.py` to connect to the github api and download all relevant data.

First, set your github personal access token as an environment variable.
```shell
export GITHUB_TOKEN="your_token_here"
```

Then, run the script with the target repository.
```shell
python ghscrape.py owner/repository_name
```
This command creates a file named `owner__repository_name.json`. An output file can be specified with the `-o` flag.

### Step 2: Convert data to markdown

This step uses `ghconvert.py` to process the json file from the previous step.

Run the script with the json file as input.
```shell
python ghconvert.py owner__repository_name.json
```
This command creates a directory named `owner__repository_name` that contains the markdown files. An output directory can be specified with the `-o` flag. The directory will contain subdirectories for issues, pull requests, and discussions, along with a main `index.md` file.
