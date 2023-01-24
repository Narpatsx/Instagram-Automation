# Instagram Automation Feed and Story

Automate post Instagram feed and Instagram story.

# Steps
1. *Instagram account*

|key name|description|
|--------|--------------|
|IG\_USERNAME|Instagram username|
|IG\_PASSWORD|Instagram password|
|QUOTES\_API\_KEY|API-Ninjas API key, you can get it from https://api-ninjas.com/api/quotes|

2. *Use this template or Clone this repository and push to your Github*
https://github.com/dhohirpradana/Instagram-Automation.git

3. *Set Github Secrets*
Go to your repository -> Settings -> Secrets -> Action -> Set Your IG_USERNAME, IG_PASSWORD

4. (*if .github/workflows/main.yml not exists)* *Create Workflow*
Go to your repository -> Actions -> New workflow -> Setup a workflow yourself -> whatever.yaml
Set when to run the script

```javascript
name: Instagram Automation

# Controls when the workflow will run
on:
  # Triggers the workflow on push events but only for the master branch
  push:
    branches: [ master ]
  
  # Triggers the workflow with scheduler
  schedule:
    - cron: '0 17 * * *'
    - cron: '0 05 * * *'

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      # Checks out your repository under $GITHUB_WORKSPACE, so your job can access it
      - uses: actions/checkout@v2
      - name: Use Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '16.x'

      - name: Install ts-node
        run: npm install -g ts-node
          
      - name: Install dependencies
        run: npm install
        
      - name: Run node script
        env:
          IG_USERNAME: '${{ secrets.IG_USERNAME }}'
          IG_PASSWORD: '${{ secrets.IG_PASSWORD }}'
          # UNSPLASH_ACCESS_KEY: '${{ secrets.UNSPLASH_ACCESS_KEY }}'
          QUOTES_API_KEY: '${{ secrets.QUOTES_API_KEY }}'
        run: ts-node app.ts
```

5. Save

# Good Luck
[![Instagram Automation](https://github.com/dhohirpradana/Instagram-Automation/actions/workflows/node.yml/badge.svg)](https://github.com/dhohirpradana/Instagram-Automation/actions/workflows/node.yml)
