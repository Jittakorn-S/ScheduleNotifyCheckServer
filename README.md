
# Schedule Notify Check Server

 

Schedule Notify Check Server is a .NET application designed to monitor server status by pinging them and sending notifications to a LINE group via a scheduled task. This tool is perfect for system administrators and developers who need to keep an eye on their servers' health and receive timely alerts.

## Features

  * **Server Status Pinging:** Checks the status of servers to see if they are online or offline.
  * **LINE Notifications:** Sends status updates and alerts directly to a specified LINE group.
  * **Scheduled Execution:** Designed to be run as a scheduled task for automated, regular checks.
  * **Easy Configuration:** All settings are managed through a simple `App.config` file.
  * **Error Logging:** Keeps a log of any errors that occur during execution for easier debugging.

## How It Works

The application reads a list of servers from a text file. It then checks which of these servers are marked as "Offline". If all servers are running normally, it sends a notification confirming that the system is healthy. If any servers are offline, the application will exit and can be configured to send an alert (though the current implementation sends a notification only when all systems are online). The main logic is executed on form load, and then the application closes itself, making it ideal for scheduled tasks.

## Installation and Usage

Follow these steps to get the Schedule Notify Check Server up and running:

### 1\. Prerequisites

  * Make sure you have **.NET Framework 4.8** installed on the machine where you will run the application.

### 2\. Configuration

Before running the application, you need to configure the `App.config` file with your specific settings.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
	<startup>
		<supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.8" />
	</startup>
	<appSettings>
		<add key="Token" value="your_line_notify_token_here"/>
		<add key="ReadFilePath" value="C:\path\to\your\server_status_file.txt"/>
		<add key="ReadFileRobin" value="C:\path\to\your\robin_check_file.txt"/>
		<add key="LogFile" value="C:\path\to\your\error_log.txt"/>
	</appSettings>
</configuration>
```

  * **`Token`**: Your LINE Notify token. You can get one from the [LINE Notify website](https://notify-bot.line.me/my/).
  * **`ReadFilePath`**: The full path to the text file that contains the server statuses. The application looks for the word "Offline" in this file.
  * **`ReadFileRobin`**: The path to a file containing information about "Robin" updates, which is appended to the success notification.
  * **`LogFile`**: The path where the error log file will be created.

### 3\. Setting Up the Scheduled Task

The application is designed to be run automatically using the Windows Task Scheduler.

1.  Open **Task Scheduler** on your Windows Server or PC.
2.  Create a new basic task.
3.  Set the trigger for how often you want to check the servers (e.g., daily, hourly).
4.  For the action, select "Start a program" and browse to the location of the `PingCheckServerDown.exe` file.
5.  Save the task.

## Code Overview

Here is a brief overview of the key files in the project:

  * **`Form1.cs`**: This is the heart of the application. The main logic for checking server status, reading configuration, and sending LINE notifications resides here.
  * **`App.config`**: The configuration file for all user-specific settings.
  * **`Program.cs`**: The main entry point for the application, which launches `Form1`.
  * **`AssemblyInfo.cs`**: Contains the assembly information for the project, such as title and version.
