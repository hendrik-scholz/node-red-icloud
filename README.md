# node-red-icloud

node-red-icloud is a project to access iCloud services through Node-RED flows.

## Requirements

In order to use the Node-RED flows you need ...

* ... an installation of Node.js
* ... an installation of Node-RED

The Node-RED flow was developed on the following environment.

* Node.js version: v0.10.25
* Node-RED version: v0.13.1

To synchronize reminders with your iPhone you need an iCloud account.

## Features

Currently, the following use case is supported:

You can create geofence reminders using the flow create-geofence-reminder. Send the following request to the service and a reminder will be generated in your iCloud account. If you have configured your iPhone to synchronize with iCloud, the created reminder will be sent to your phone.

Sample request:

{
"appleId":"",
"password":"",
"reminderList":"Reminders",
"priority":1,
"title":"Get a birthday present for Lisa",
"description":"Call Robert to ask what Lisa likes.",
"proximity":"ARRIVE",
"address":"Harrods, 87-135 Brompton Road, London SW1X 7XL",
"locationName":"Harrods",
"latitude":"51.4992917",
"longitude":"-0.162811",
"alarm":"2017-01-01T00:00:00"
}

## Configuration

Logging to a file is turned off by default. Open the logging subflow to set a file name and activate logging. 

## Test

A SoapUI project can be found in the test folder to send a test request to the service running on your local machine.