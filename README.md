# sec-depend-aider: Dependabot Pull Request Monitoring Automation 

<img width="1295" alt="sec-depend-aider-architecture" src="https://user-images.githubusercontent.com/88770278/178749028-30354162-439b-4c49-8b7c-14829302d8b3.png">

[Problem Statement](#problem-statement) \| [Overview](#solution-overview) \| [Quickstart](#quickstart) \| [Future Work](#future-work)

## Problem Statement

Today, open source software provides the foundation for the vast majority of applications across all industries, and software development has slowly moved towards software assembling. Because of this change in the way we deliver the software, new attack surfaces have evolved and software security is facing new challenges, such as [Log4j](https://logging.apache.org/log4j/2.x/), [the SolarWinds Supply Chain Attack](https://www.sans.org/blog/what-you-need-to-know-about-the-solarwinds-supply-chain-attack/), and [others](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610).

## Solution Overview

Netskope utilizes Github Dependabot as one of the solutions to address the problem. Dependabot keeps your dependencies up to date by informing you of any security vulnerabilities in your dependencies, and automatically opens pull requests to upgrade your dependencies to the next available secure version when a Dependabot alert is triggered, or to the latest version when a release is published. 

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
