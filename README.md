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

## Demo:

### Step 1:

```
~/ghbkp python ghscrape.py ikawrakow/ik_llama.cpp
I: Fetching all issues...
I: API Rate Limit (Req #1): 4997 points remaining, resets in 59m 55s.
I: Processed 100 issues...
I: API Rate Limit (Req #2): 4994 points remaining, resets in 59m 51s.
I: Processed 200 issues...
I: API Rate Limit (Req #3): 4991 points remaining, resets in 59m 50s.
I: Processed 216 issues...
I: Fetching all nested data for 216 items (2 pages)...
I: API Rate Limit (Req #4): 4990 points remaining, resets in 59m 50s.
I: Processed batch of 2 pages. 0 pages remaining.
I: Structuring final items for issues...
I: Finished issues: Found and processed 216 items.
I: Fetching all pull requests...
I: API Rate Limit (Req #5): 4885 points remaining, resets in 59m 47s.
I: Processed 100 pull_requests...
I: API Rate Limit (Req #6): 4780 points remaining, resets in 59m 44s.
I: Processed 200 pull_requests...
I: API Rate Limit (Req #7): 4675 points remaining, resets in 59m 40s.
I: Processed 300 pull_requests...
I: API Rate Limit (Req #8): 4570 points remaining, resets in 59m 35s.
I: Processed 400 pull_requests...
I: API Rate Limit (Req #9): 4465 points remaining, resets in 59m 28s.
I: Processed 500 pull_requests...
I: API Rate Limit (Req #10): 4360 points remaining, resets in 59m 24s.
I: Processed 600 pull_requests...
I: API Rate Limit (Req #11): 4255 points remaining, resets in 59m 24s.
I: Processed 604 pull_requests...
I: Fetching all nested data for 604 items (1 pages)...
I: API Rate Limit (Req #12): 4254 points remaining, resets in 59m 23s.
I: Processed batch of 1 pages. 1 pages remaining.
I: API Rate Limit (Req #13): 4253 points remaining, resets in 59m 23s.
I: Processed batch of 1 pages. 0 pages remaining.
I: Structuring final items for pull_requests...
I: Finished pull_requests: Found and processed 604 items.
I: Fetching all discussions...
W: Retriable error (RetriableError) on attempt 1/5: Server Error: 504 Gateway Timeout. Retrying...
I: API Rate Limit (Req #14): 4039 points remaining, resets in 59m 0s.
I: Processed 100 discussions...
I: API Rate Limit (Req #15): 3937 points remaining, resets in 59m 0s.
I: Processed 106 discussions...
I: Fetching all nested data for 106 items (1 pages)...
I: API Rate Limit (Req #16): 3936 points remaining, resets in 58m 59s.
I: Processed batch of 1 pages. 0 pages remaining.
I: Structuring final items for discussions...
I: Finished discussions: Found and processed 106 items.
I: Data successfully saved to ikawrakow__ik_llama.cpp.json
I: Total execution time: 60.84 seconds
```

### Step 2:

```
~/ghbkp python ghconvert.py ikawrakow__ik_llama.cpp.json 
Processing 216 issues...
Processing 604 pull_requests...
Processing 106 discussions...
Generating index.md summary file...
Successfully generated 926 Markdown files.
Files are in the 'ikawrakow__ik_llama.cpp' directory.
```

### Results

The results of this demo are available in the following repository: [ThomasBaruzier/ikawrakow-ik-llama.cpp-archive](https://github.com/ThomasBaruzier/ikawrakow-ik-llama.cpp-archive)
