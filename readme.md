Automation Framework (Selenium + TestNG + Rest Assured)
1.Overview:

This repository contains a hybrid UI + API automation framework built using:

* Java (JDK 10+)

* Selenium WebDriver

* TestNG

* Rest Assured

* Maven

* Extent Reports + Allure Reports

* Log4j2 Logging

The framework automates:

* UI Tests on: https://the-internet.herokuapp.com/login

* API Tests on: https://jsonplaceholder.typicode.com/

2.Project Structure:

com.bank.framework/
│
├── src
│   └── test
│       ├── java
│       │   ├── apis/            # API clients and test classes
│       │   ├── base/            # BaseTest, BaseAPI, common setup/teardown
│       │   ├── factory/         # DriverFactory, BrowserFactory
│       │   ├── listeners/       # Allure, Extent, TestNG listeners
│       │   ├── pages/           # Page Object Model classes
│       │   ├── tests/           # UI + API tests
│       │   └── utils/           # Utilities: Waits, config, retry, data readers
│       │
│       └── resources
│           ├── config.properties # Browser, URL, timeouts
│           └── log4j2.xml        # Logging configuration
│
├── data/
│   ├── loginData.csv            # Data-driven CSV
│   └── loginData.json           # Data-driven JSON
│
├── logs/
│   └── framework.log            # Execution log file
│
├── reports/
│   ├── allure-results/          # Allure raw results
│   ├── screenshots/             # Screenshots on failure
│   ├── emailable-report.html    # TestNG report
│   └── ExtentReport.html        # Extent Report
│
├── DESIGN.md
├── retrospective.md
├── README.md
├── pom.xml
└── testng.xml


3. Framework Components:
------------------------
1️. Base Layer

Initializes and tears down WebDriver

Loads configuration file

Implements WebDriverWait

Captures failures, logs, and screenshots

2️. Page Object Model (POM)

Each page contains:

Web elements

Page actions

Business flows

Test readability and reuse

3️. API Layer

Using Rest Assured:

Request specifications

Payload builders

GET/POST tests

JSON validation

4️. Utilities

ConfigManager

DataUtil (CSV/JSON reader)

RetryAnalyzer

WaitUtil

Screenshot util

5️. Logging

Configured using Log4j2

All logs written to:

/logs/framework.log

6️. Listeners

Captures test start/end

Adds Allure steps

Adds Extent logs

Takes screenshots

4.Prerequisites:
----------------
| Tool   | Version            |
| ------ | ------------------ |
| Java   | 10 or above        |
| Maven  | 3.6+               |
| TestNG | Latest             |
| IDE    | Eclipse  

5. Viewing Reports:
------------------
1.Extent Report
After execution:
/reports/ExtentReport.html
2.Allure Report
Generate the HTML report:
allure serve reports/allure-results


6.Test Data Handling:
---------------------
Data-driven test examples are stored in:
/data/loginData.csv
/data/loginData.json



