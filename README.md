# sec-depend-aider: Dependabot Pull Request Monitoring Automation 

<img width="1295" alt="sec-depend-aider-architecture" src="https://user-images.githubusercontent.com/88770278/178749028-30354162-439b-4c49-8b7c-14829302d8b3.png">

[Overview](#overview) \| [Quickstart](#quickstart) \| [Future Work](#future-work)

## Overview

Netskope utilizes Github Dependabot as one of the solutions to address the problem and in short, if Dependabot finds a vulnerability in a package your code depends on then it sends you an alert. If it can suggest a fix, it also sends a pull request to update your dependency manifest with the closest non-vulnerable version.

Naturally, Dependabot aligns with the Netskope principle of embedding security in developer workflow and is part of developer experience.

Netskope took one step further to embed security in developer experience. We developed an automation framework to monitor the pull requests created by Dependabot and feed it back to Jira into the right teams bucket, where developers can triage and remediate it holistically along with other areas of work. 

Additionally, the automation framework enables the Dependabot security alerts for all unarchived repos, if not enabled already.

## Quickstart

```
% python3 netskope_dependabot_analyzer.py
usage: netskope_dependabot_analyzer.py [-h] [-o ORGANIZATION] [-r CONFIG_REPO] [-w WAITING_PERIOD] [-c CONFIG_ORGANIZATION]

optional arguments:
  -h, --help            show this help message and exit
  -o ORGANIZATION, --organization ORGANIZATION
                        Github Organization Name
  -r CONFIG_REPO, --config-repo CONFIG_REPO
                        Custom Configuration Repository Name
  -w WAITING_PERIOD, --waiting-period WAITING_PERIOD
                        Waiting Period (default 15)
  -c CONFIG_ORGANIZATION, --config-organization CONFIG_ORGANIZATION
                        Custom Configuration Organization Name (default set to Github Organization Name)

```
- Create a repo to define the custom configuration (filename as custom-config.json in root directory of repo)
- Update parameter DEPENDABOT_JIRA_SEVERITY to reflect your Jira severity definition
- Set environment variables:
  - GITHUB_ACCESS_TOKEN
  - JIRA_SERVER
  - JIRA_API_USERNAME
  - JIRA_API_TOKEN

## Future Work
- [ ] Integrate the automation with GitHub Action to:
 - Run from a centralized repository across the organization in a scheduled manner
 - Run from each repository with events like pull request creation or push to a branch
- [ ] We started the automation with defining sink as Jira, but it can be easily reused for any technology, for example feeding the data into a SIEM for analytics
- [ ] Already in process for expanding the search query used in the automation to gather more datasets like GitHub Code and Secret Scanning Alerts
