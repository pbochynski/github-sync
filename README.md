github-sync.js is a small script to keep in sync labels and milestones across many repositories and organizations. You can use it also to sync github.com repositories with your github enterprise installation. To write changes to the target repositories you need to provide a token. If you work in 

# Installation

Checkout repository and run:
```
npm install
```

# Usage examples

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