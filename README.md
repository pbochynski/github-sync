# Overview

github-sync.js is a small script to keep in sync labels and milestones across many repositories and organizations. You can also use it to sync github.com repositories with your github enterprise installation. 

## Installation

Checkout repository and run:
```
npm install
```
## Authorization / authentication
To write changes to the target repositories you need to provide a token. You can get one from GitHub -> Settings -> Developers Settings -> Personal access tokens. If you work with different instances of github you can provide separate access tokens: source-token and target token. Both fallback to the token option and finally to anonymous access. Please be aware that github rate limiting is very aggressive for anonymous access, so you will be probably blocked after few tries.

## Dry-run mode
If you are not sure what will happen after execute the command you can run the script with `--dry-run` option. It will run in the read only mode and will write down all the operations that should be executed.

## Update-only mode
Update only mode can be useful if you do not want to create all the labels or milestones in the target reposiotries, but you want to unify descriptions, colors (for labels) or due dates (for milestones).

## Usage examples

Synchronize labels starting with area/ and stale label from https://github.com/org/repo repository to all repositories in https://github.com/org2 organization'):
```
github-sync.js labels -s org/repo -t org2 -l "area/.*" stale --token github_token
```

Synchronize milestones 1.18, 1.19, and 1.20 from https://github.com/org/repo repository to Github Enterprise repo https://github.example.com/org/repo:
```
github-sync.js milestones -s org/repo --source-token github_token -t org/repo --target-base-url "https://github.example.com/api/v3" --target-token github_enterprise_token -l 1.18 1.19 1.20
```

Create/update all labels from org/repo in all repositories in the organization org2 and in repository org3/repo:
```
github-sync.js labels -s org/repo -t org2 org3/repo --token github_token
```

Display create/update operations to sync all milestones from org/repo to all repositories in that organization:
```
github-sync.js milestones -s org/repo -t org --dry-run
```

Only update descriptions and due dates for all milestones from org to match milestones from org/repo:
```
github-sync.js milestones -s org/repo -t org --update-only
```

## Contribution
If you find some problems feel free to create issues / pull requests.
