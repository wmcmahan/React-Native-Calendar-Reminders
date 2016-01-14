# React-Native-CalendarReminders
React Native Module for IOS Calendar Reminders


## Install
```
npm install react-native-calendar-reminders
```
Then add RNCalendarReminders to project libraries.


## Usage

Require Native Module:
```javascript
var RNCalendarReminders = require('react-native-calendar-reminders');
```
The **EventKit.framework** will also need to be added to the project.


#### Request authorization to IOS EventStore

```javascript
RNCalendarReminders.authorizeEventStore((error, auth) => {...});
```


#### Fetch all current reminders from EventStore

```javascript
RNCalendarReminders.fetchAllReminders(reminders => {...});
```

#### Reminder Properties

| Property        | Value            | Description |
| --------------- |------------------| ----------- |
| id              | String (read only)             | Unique id for the reminder. |
| title           | String             | The title for the reminder. |
| startDate       | Date             | The start date of the task. |
| location        | String           | The location associated with the reminder. |
| notes           | String           | The notes associated with the reminder. |
| alarms          | Array            | The alarms associated with the reminder, as an array of alarm objects. |

#### Create reminder

```
RNCalendarReminders.saveReminder(title, settings);
```
Example:
```javascript
RNCalendarReminders.saveReminder('title', {
  location: 'location',
  notes: 'notes',
  startDate: '2016-10-01T09:45:00.000UTC'
});
```

#### Create reminder with alarms

###### Alarm options:

| Property        | Value            | Description |
| --------------- |------------------| ----------- |
| date           | Date or Number    | If a Date is given, an alarm will be set with an absolute date. If a Number is given, an alarm will be set with a relative offset (in minutes) from the start date. |
| location | Object             | The start date of the task. |

###### Alarm location properties:

| Property        | Value            | Description |
| --------------- |------------------| ----------- |
| title           | String  | The title of the location.|
| proximity | String             | A value indicating how a location-based alarm is triggered. Possible values: `enter`, `leave`, `none`. |
| radius | Number             | A minimum distance from the core location that would trigger the reminder's alarm. |
| coords | Object             | The geolocation coordinates, as an object with latitude and longitude properties |

Example with date:

```javascript
RNCalendarReminders.saveReminder('title', {
  location: 'location',
  notes: 'notes',
  startDate: '2016-10-01T09:45:00.000UTC',
  alarms: [{
    date: -1 // or absolute date
  }]
});
```
Example with location:

```javascript
RNCalendarReminders.saveReminder('title', {
  location: 'location',
  notes: 'notes',
  startDate: '2016-10-01T09:45:00.000UTC',
  alarms: [{
    location: {
      title: 'title',
      proximity: 'enter',
      radius: 500,
      coords: {
        latitude: 30.0000,
        longitude: 97.0000
      }
    }
  }]
});
```

#### Update reminder
Give an **reminder ID** to update and existing reminder.

```javascript
RNCalendarReminders.saveReminder('title', {
  id: 'id',
  location: 'location',
  notes: 'notes',
  startDate: '2016-10-02T09:45:00.000UTC'
});
```

#### Update reminder alarms
Give an **reminder ID** and **array of alarm options** to update and existing reminder. Note: This will overwrite any alarms already set on the reminder.

```javascript
RNCalendarReminders.addReminderAlarms({
  id: 'id',
  alarms: [{
    date: -2 // or absolute date
  }]
});
```

#### Update reminder with added alarm
Give an **reminder ID** and **alarm options object** to add new alarm.

```javascript
RNCalendarReminders.addReminderAlarm({
  id: 'id',
  alarms: {
    date: -3 // or absolute date
  }
});
```

#### Remove reminder

```javascript
RNCalendarReminders.removeReminder(eventId);
```
