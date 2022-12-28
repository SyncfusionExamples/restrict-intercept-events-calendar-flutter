# How to prevent multiple assignments of the same time events in the Flutter Calendar?

A quick-start example to help you to prevent multiple assignments of the same time events in the Flutter Calendar.

Using the appointment editor application, you can prevent multiple events from being assigned at the same time in the Flutter event calendar widget.

In this sample,  using the `_isInterceptExistingAppointment` method the start and end time of the new event is compared to the already created event collection. This method checks whether the calendar already has an event for the same start time and end time. If the new event has the same time as the already added collection it returns the alert dialog. Otherwise, a new appointment will be created at the mentioned time

For more details, you can refer to our [KB](https://www.syncfusion.com/kb/11411/how-to-prevent-multiple-assignments-of-the-same-time-events-in-the-flutter-calendar) documentation.

## Requirements to run the demo
* [VS Code](https://code.visualstudio.com/download)
* [Flutter SDK v1.22+](https://flutter.dev/docs/development/tools/sdk/overview)
* [For more development tools](https://flutter.dev/docs/development/tools/devtools/overview)

## How to run this application
To run this application, you need to first clone or download the ‘create a flutter maps widget in 10 minutes’ repository and open it in your preferred IDE. Then, build and run your project to view the output.

## Further help
For more help, check the [Syncfusion Flutter documentation](https://help.syncfusion.com/flutter/introduction/overview),
 [Flutter documentation](https://flutter.dev/docs/get-started/install).