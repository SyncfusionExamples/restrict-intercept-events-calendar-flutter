# How to prevent multiple assignments of the same time events in the Flutter event calendar (SfCalendar)?

In the flutter event calendar widget, you can prevent the multiple events assignment for the same time using the custom appointment with the appointment editor application.

## Step 1:
In initState(), set the default values for calendar view.

```xml
CalendarView _calendarView;
@override
void initState() {
  _calendarView = CalendarView.month;
  super.initState();
}
```
 

## Step 2:
Create a custom class Meeting with required fields (For creating appointments mandatory fields are from and to).

```xml
class Meeting {
  Meeting(
      {@required this.from,
      @required this.to,
      this.background = Colors.green,
      this.isAllDay = false,
      this.eventName = '',
      this.startTimeZone = '',
      this.endTimeZone = '',
      this.description = ''});
 
  final String eventName;
  final DateTime from;
  final DateTime to;
  final Color background;
  final bool isAllDay;
  final String startTimeZone;
  final String endTimeZone;
  final String description;
}
```
## Step 3:
You can map those properties of the Meeting class with a calendar widget by using the ‘CalendarDataSource’ override methods properties.

```xml
Class DataSource extends CalendarDataSource {
  DataSource(List<Meeting> source) {
    appointments = source;
  }
 
  @override
  bool isAllDay(int index) => appointments[index].isAllDay;
 
  @override
  String getSubject(int index) => appointments[index].eventName;
 
  @override
  String getStartTimeZone(int index) => appointments[index].startTimeZone;
 
  @override
  String getNotes(int index) => appointments[index].description;
 
  @override
  String getEndTimeZone(int index) => appointments[index].endTimeZone;
 
  @override
  Color getColor(int index) => appointments[index].background;
 
  @override
  DateTime getStartTime(int index) => appointments[index].from;
 
  @override
  DateTime getEndTime(int index) => appointments[index].to;
}
``` 

## Step 4:
You can schedule meetings for a day by setting the `From` and `To` properties of the Meeting class. Create a collection of `Meetings`  data and assign it to the `appointments` property of `CalendarDataSource`.

```xml
List<Meeting> getMeetingDetails() {
  final List<Meeting> meetingCollection = <Meeting>[];
 
  final DateTime today = DateTime.now();
  final Random random = Random();
  for (int month = -1; month < 2; month++) {
    for (int day = -5; day < 5; day++) {
      for (int hour = 9; hour < 18; hour += 5) {
        meetingCollection.add(Meeting(
          from: today
              .add(Duration(days: (month * 30) + day))
              .add(Duration(hours: hour)),
          to: today
              .add(Duration(days: (month * 30) + day))
              .add(Duration(hours: hour + 2)),
          background: _colorCollection[random.nextInt(9)],
          startTimeZone: ‘’,
          endTimeZone: ‘’,
          description: ‘’,
          isAllDay: false,
          eventName: eventNameCollection[random.nextInt(7)],
        ));
      }
    }
  }
  return meetingCollection;
}
```
## Step 5:
You have added the method (_isInterceptExistingAppointment) for checking the start and end time of the new event equals to the already created event collection. When adding a new event for calendar, the_isInterceptExistingAppointment method checks whether the calendar already have an event for the same start time and end time. If the new event has same time with already added collection it returns the alert dialog. Otherwise, new appointment will be created in the mentioned time. Please find the following code snippet for the same.

```xml
dynamic _isInterceptExistingAppointments(DateTime date, Meeting selectedAppointment) {
  if(date == null ||events ==null || events.appointments == null || events.appointments.isEmpty)
    return null;
  for (int i = 0; i < events.appointments.length; i++) {
    var appointment = events.appointments[i];
    if (appointment != selectedAppointment && (date.isAfter(appointment.from) || _isSameDateTime(date, appointment.from)) && date.isBefore(appointment.to)) {
      return appointment;
    }
  }
  return null;
}
```
**[View document in Syncfusion Flutter Knowledge base](https://www.syncfusion.com/kb/11411/how-to-prevent-multiple-assignments-of-the-same-time-events-in-the-flutter-event-calendar)**

**Screenshot**

<img alt="interceptingalert"  src="http://www.syncfusion.com/uploads/user/kb/flut/flut-789/flut-789_img1.png" width="300" height="500" />|
