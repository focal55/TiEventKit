# TiEventKit

Titanium Appcelerator module that implements iOS Event Kit framework.

## Supports

* iOS 4.0+
* Titanium SDK 3.4.1.GA

## What can I do with this module?

You can create Events in user default calendar and set the Event Alarm if desired. In iOS 6, the user will be asked by permissions to access her calendar. In iOS 5, you don't need user permissions.

Each event have this attributes:

* title (STRING)
* location (STRING)
* notes (STRING)
* begin (DATE)
* end (DATE)
* allDay (BOOL)
* alarmOffset (INT)

NOTE: The date format is: *"yyyy-MM-dd hh:mm:ss Z"*.

## Creating an Event

For compatibilty, you first need to ask authorization by user before create an Event. If user have granted the permission to access her Calendar, it will always return TRUE in event callback method. So, here is a simple usage of method:

	var EK = require("ti.eventkit");
	
	// Request authorization to user
	EK.requestAuthorization(function(e) {
	
		// If user have authorized this application…
		if (e.authorized == true) {
		
			// Create the Event
			EK.createCalendarEvent({
				title: "Codestrong",
				notes: "We will hack a lot.",
				location: "San Francisco",
				begin: "2012-10-21 08:00:00 GMT",
				end: "2012-10-23 18:00:00 GMT"
                alarmOffset: -300
			});

			Ti.UI.createAlertDialog({
				title: "Calendar",
				message: "This event will be AWESOME!",
				buttonNames: ["YEAH!", "OK"]
			}).show();
			
		} else {
			Ti.UI.createAlertDialog({
				title: "Calendar",
				message: "You have to allow this application to access your Calendar",
				buttonNames: ["OK"]
			}).show();
		}
	});

## Event Alarms

In order to set an Event Alarm, set alarmOffset to a negative value in the form of seconds. For example if you would like the alarm 5 minutes before the event set alarmOffset to -300. Here is a chart that matches options in the iOS Event edit screen.

5  min  = -300

15 min  = -900

30 min  = -1800

1 hour  = -3600

2 hours = -7200

1 day   = -86400

2 days  = -172800

1 week  = -604800

## Development History

This is a branch off of https://github.com/Nyvra/TiEventKit who implemented the Authorization capability neccessary for iOS 6+. This fork continues the development of this module by adding the following functionality.

1. Event Alarms configurations (aka event reminders).
