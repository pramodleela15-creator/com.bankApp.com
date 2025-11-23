
1.Overview:
===========

This document describes a scalable, hybrid UI + API automation framework built using Java, Selenium WebDriver, TestNG, Rest Assured, Allure, Extent Reports, and Maven.

The framework targets:
----------------------
UI Tests using demo site: https://the-internet.herokuapp.com/login
-------------------------

API Tests using demo API: https://jsonplaceholder.typicode.com/
-------------------------

Designed for real-world banking application with CI/CD and parallel execution.
------------------------------------------------------------------------------

2.High-Level Architecture Diagram:
==================================

                   +-----------------------------+
                   |         TestNG Suite        |
                   | (testng.xml: UI + API sets) |
                   +--------------+--------------+
                                  |
       --------------------------------------------------------
       |                                                      |
+-------------+                                      +----------------+
| UI Tests    |                                      | API Tests      |
| (Selenium)  |                                      | (Rest Assured) |
+------+------+                                      +-------+--------+
       |                                                      |
+------+------+                                      +--------+--------+
| Page Objects |                                      | API Clients     |
| (POM)        |                                      | (Payloads, Req) |
+------+------+                                      +--------+--------+
       |                                                      |
+------+------+                                      +--------+--------+
| WebDriverMgr |                                      | BaseAPI Class   |
+--+-----------+                                      +-----------------+
   |
   v
+------------------------+
| Test Utilities         |
| Logging (Log4j2)       |
| Data (JSON/CSV)        |
| Retry + Wait helpers   |
+------------------------+
   |
   v
+-------------------------+
| Reporting Layer         |
| Allure + Extent Reports |
+-------------------------+
   |
   v
+------------------+
| CI/CD (GitHub)   |
| Maven build      |
+------------------+


3. Rationale for Key Design Choices:
===================================

✔ Selenium WebDriver + TestNG
------------------------------

TestNG provides suite management, groups, retries, parallel execution.

Selenium allows flexible browser support and grid scalability.

✔ Page Object Model (POM)
--------------------------

Separates locators & actions → better maintainability.

Reduces duplication & improves readability.

✔ Rest Assured for API
------------------------

Fluent Java DSL for request-building.

Easily integrates into TestNG and reporting.

✔ Maven
--------

Dependency management

Standard structure

Integrates with CI easily

✔ Dual Reporting (Allure + Extent)
-----------------------------------

Allure → high-level detailed dashboard + attachments

Extent → beautiful HTML report for managers

✔ Log4j2
---------

Debugging, error tracing, and audit trail.

4. Framework Structure:
=======================

com.bank.framework/                     <-- Project root
│
├── src
│   ├── main
│   │   └── java                         <-- (Usually for app code – empty in your case)
│   │
│   └── test
│       ├── java
│       │   ├── apis/                    <-- API test modules
│       │   ├── base/                    <-- BaseTest, BaseAPI, Driver setup
│       │   ├── factory/                 <-- DriverFactory, BrowserFactory
│       │   ├── listeners/               <-- TestNG listeners (Allure, Extent, Log listeners)
│       │   ├── pages/                   <-- POM: LoginPage, HomePage, etc.
│       │   ├── tests/                   <-- Test classes: Login tests, API tests
│       │   └── utils/                   <-- Utilities: WaitUtil, ConfigManager, Excel/JSON reader
│       │
│       └── resources
│           ├── config.properties        <-- URL, browser configs
│           └── log4j2.xml               <-- Logging configuration
│
├── data/
│   ├── loginData.csv                    <-- Data-driven testing file
│   └── loginData.json                   <-- JSON-based test data
│
├── logs/
│   └── framework.log                    <-- Log4j2 detailed logs (as seen in screenshot)
│
├── reports/
│   ├── allure-results/                  <-- Allure raw results
│   ├── screenshots/                     <-- Screenshot on failure
│   ├── emailable-report.html            <-- TestNG default HTML report
│   └── ExtentReport.html                <-- Extent HTML report (shown in screenshot)
│
├── target/                              <-- Maven build output
│
├── test-output/                         <-- TestNG output (index.html etc.)
│
├── DESIGN.md                            <-- Your documentation file
├── retrospective.md                     <-- Project retrospective notes
├── README.md                            <-- Project description
├── pom.xml                              <-- Dependencies + plugins
├── jenkinsFile                          <-- (Optional) CI/CD pipeline script
└── testng.xml                           <-- Master TestNG suite

5. High-Level Explanation of Each Folder:
=========================================
1. src/test/java/
-----------------

This contains all framework code:

base → BaseTest, WebDriver initialization, teardown

factory → DriverFactory, browser selection

listeners → AllureListener, ExtentListener

pages → All Page Objects

tests → UI + API test classes

utils → Helpers (waits, data readers, retry logic)

2. src/test/resources/
---------------------

config.properties → browser, URL, timeouts

log4j2.xml → your logging setup

3. data/
-------

Test data separated for:

CSV

JSON

4. logs/
-------

framework.log → execution logs (your screenshot shows LoginTest & BaseTest logs here)

5. reports/
----------

Contains:

Allure results

Extent report

Screenshots

TestNG email report

6. testng.xml
--------------

Defines your test suite:

loginSuccess

loginFailure

API tests

7. Clean, Final Architecture:
============================

📁 com.bank.framework
│
├── 📁 src
│   └── 📁 test
│       ├── 📁 java
│       │   ├── apis
│       │   ├── base
│       │   ├── factory
│       │   ├── listeners
│       │   ├── pages
│       │   ├── tests
│       │   └── utils
│       └── 📁 resources
│           ├── config.properties
│           └── log4j2.xml
│
├── 📁 data
│
├── 📁 logs
│
├── 📁 reports
│
├── pom.xml
├── testng.xml
├── DESIGN.md
└── README.md

8. Handling Flaky Tests:
=========================
✔ Smart Wait Utilities

Explicit waits with custom conditions

Avoid Thread.sleep

✔ Retry Analyzer

Auto retry failed tests

9.Handling Sensitive Test Data
✔ Externalized Test Data

JSON/CSV stored under /data

No credentials inside code

✔ Encrypted or Masked

Sensitive credentials masked in logs

Environment files encrypted / .gitignore the actual secrets

✔ CI/CD Best Practice

Use GitHub Secrets for:

usernames

passwords

tokens

✔ Secure Logging

Do NOT print raw passwords

Log4j2 masking pattern applied


