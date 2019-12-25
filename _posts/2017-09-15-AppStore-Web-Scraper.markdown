---
title: "AppStore: Web Scraper for iTunes"
layout: post
date: 2017-09-15 22:10
tag: python
image:
headerImage: true
projects: true
hidden: true # don't count this post in blog pagination
description: "This is a web scraper which pull data of whole applications from AppStore daily using clusters."
category: project
author: ferhatyaman
externalLink: false
---

# AppStore 

This is a web scraper which pull data of whole applications from iTunes daily using clusters. Main purpose of that project was collecting some specific information of applications on AppStore such as update date, permissions, number of download. We are trying to keep track changes of those information daily, to find out how those apps are secure. 

My main challance was learning python environment and using remote job assignment to control cluster to collect information. I have used RabbitMQ message broker system to update database remotely. System is designed as one master server which keep database inside and consumes messages coming from worker clusters which run web scrapers. I have used 20-30 cluster as worker. 

Finally, system is collecting data of 1.3 million applications in 8-10 hours. 

## Getting Started

This proccess has several step. It also has severeal requirements before run.

### Prerequisites

1. There should be rabbitmq-server on your server or your localhost.(However this is long-running process. If there is a static ip server or if connection on the localhost is not break, you can use this server.)
2. New user should be added for credential on rabbitmq management system.
3. There should be a grid-system which has 20-30 cluster which has anaconda module.

### Running the process
1. Install rabbitmq and start the server
2. Run the appReader.py which creates appStore.db database which has information of apps.

* **Note:** this step may take 7-8 hours to execute. Be patient.
* **Note:** I also upload an example database which has 1.3 million app id 
3. After Step 2 done, Run the new_task.py which sends information rabbitmq server.
4. Run the worker.py on clusters
	1. Download environment.yml, appStore.sh, Makefile, worker.py on your cluster workspace.
	2. Run 'make' command how many cluster you want to work
5. After Step 3 done, Run read_responds.py which updates appStore.db which you created on Step 2

After all steps, information of applications is ready.

1. Static IP: localhost
2. Rabbitmq Credentials:
	1. user: username
	2. password: password
3. Create a virtual environment for python codes

This project is conducted at BU Secure Systems Lab(BUSec LAB) with guidance of **Prof. Manuel EGELE**. Thanks to him, I have completed the project and learn a lot stuff. 
