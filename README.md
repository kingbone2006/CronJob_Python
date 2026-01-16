README for CronJob_Python
​

Overview
CronJob_Python is a simple tool to periodically call multiple URLs using a Python script.
​
You only need to clone the repo, put your URLs into a .txt file, install Python, and run a single .py file.
​

Requirements
Python 3 installed on your machine (Windows, macOS, or Linux).
​

Internet connection to reach the URLs you want to ping or trigger.
​

Install Python
Go to the official Python download page: 
https://www.python.org/downloads/
 and download the latest stable Python 3 for your OS.
​

During installation on Windows, make sure to check “Add Python to PATH” so you can use the python command in your terminal or command prompt.
​

Getting Started
Clone the repository

Using HTTPS:

git clone https://github.com/kingbone2006/CronJob_Python.git
​

Then:

cd CronJob_Python
​

Add URLs to the .txt file

Open cron.txt (or the .txt file used by the script in this repo).
​

Each line should be a URL you want to call periodically, for example:

https://example.com/cron1

https://example.com/cron2

Run the Python script

Open a terminal/command prompt in the project folder.
​

Run (depending on the actual script name in the repo):

python main.py

or python cron.py

Keep the terminal open if the script is designed to loop and call the URLs continuously.
