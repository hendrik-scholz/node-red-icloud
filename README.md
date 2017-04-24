# node-red-icloud

node-red-icloud is a project to access iCloud services through Node-RED flows.

## Requirements

In order to use the Node-RED flows you need ...

* ... an installation of Node.js
* ... an installation of Node-RED

The Node-RED flow was developed on the following environment.

* Node.js version: v6.9.5
* Node-RED version: v0.16.2

The SoapUI project containing the test cases was created with SoapUI 5.3.0.

To create reminders in iCloud and synchronize them with your iPhone you need an iCloud account.

## Features

Currently, the following use cases are supported.

* You can create reminders for a specific date and/or geofence. A reminder will be generated in your iCloud account. If you have configured your iPhone to synchronize with iCloud, the created reminder will be sent to your phone.

* You can retrieve all reminder lists for your iCloud account.

* You can retrieve all reminders for a specific reminder list.

### Create Reminders

**Request**

* Request method: POST

* Endpoint: /reminders

| field      | description |
| ---------- | ----------- |
|appleId|the Apple ID of your iCloud account|
|password|the password of your iCloud account|
|reminderList|the name of the list you want to put the reminder on - If the list does not exist, the reminder is put on an existing one.|
|priority|from 1 (high) to 3 (low) - No priority is set if the field is missing or its value is null.|
|title|the title of the reminder|
|description|the description of the reminder|
|proximity|defines whether the geofence reminder triggers on arrival or departure, possible values: ARRIVE, DEPART|
|address|the address of the location - If the address is not given, the flow tries to determine the address by calling Nominatim using the geo position.|,
|locationName|the name of the location|,
|latitude|the latitude of the location the geofence is based on|
|longitude|the longitude of the location the geofence is based on|
|alarm|date and time of the alarm - format yyyy-mm-ddThh:mm:ss, e.g. 2017-01-01T00:00:00|

**Sample requests**

Set the Apple ID and the password of your iCloud account in one of the following requests and send the request to the create-reminder flow.

*date only*

```
{
"appleId":"",
"password":"",
"reminderList":"Reminders",
"priority":1,
"title":"Get a birthday present for Lisa",
"description":"Call Robert to ask what Lisa likes.",
"alarm":"2018-01-01T00:00:00"
}
```

*location only*

```
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
"longitude":"-0.162811"
}
```

*date and location*

```
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
"alarm":"2018-01-01T00:00:00"
}
```
### Get Reminder Lists

**Request**

* Request method: GET

* Endpoint: /reminderlists

| parameter  | description |
| ---------- | ----------- |
|appleId|the Apple ID of your iCloud account|
|password|the password of your iCloud account|

### Get Reminders from List

**Request**

* Request method: GET

* Endpoint: /reminder/:list

| parameter  | description |
| ---------- | ----------- |
|list|name of the list to retrieve the reminders from|
|appleId|the Apple ID of your iCloud account|
|password|the password of your iCloud account|

## Configuration

Logging to a file is turned off by default. Open the logging subflow to set a file name and activate logging. 

## Test

A SoapUI project can be found in the test folder to send test requests to the service running on your local machine. Set the your Apple ID and password in the custom properties on project level before running a test.

A load test can be found in the test suite 'RaspberryPi' of the SoapUI project. Configure the load test by setting the endpoint and parameters before running the test.