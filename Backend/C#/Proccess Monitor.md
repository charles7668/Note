# Process Monitor in C\#

This guide demonstrates how to implement a process monitor in C# using Windows Management Instrumentation (WMI).

## Prerequisites

- Install `System.Management` from NuGet.

## Monitoring with Elevated Privileges

To monitor process start and stop events with elevated privileges, use the following code:

```c#
using System;
using System.Management;

class ProcessMonitor {
    public static void Main() {
        var startWatch = new ManagementEventWatcher(
            new WqlEventQuery("SELECT * FROM Win32_ProcessStartTrace"));
        startWatch.EventArrived += StartWatch_EventArrived;
        startWatch.Start();

        var stopWatch = new ManagementEventWatcher(
            new WqlEventQuery("SELECT * FROM Win32_ProcessStopTrace"));
        stopWatch.EventArrived += StopWatch_EventArrived;
        stopWatch.Start();

        Console.WriteLine("Press any key to exit...");
        while (!Console.KeyAvailable) System.Threading.Thread.Sleep(50);

        startWatch.Stop();
        stopWatch.Stop();
    }

    private static void StopWatch_EventArrived(object sender, EventArrivedEventArgs e) {
        Console.WriteLine($"Process stopped: {e.NewEvent.Properties["ProcessName"].Value}");
    }

    private static void StartWatch_EventArrived(object sender, EventArrivedEventArgs e) {
        Console.WriteLine($"Process started: {e.NewEvent.Properties["ProcessName"].Value}");
    }
}
```

## Monitoring without Elevated Privileges

To monitor processes without elevated privileges, modify the query strings as shown below:

Start Watch

```c#
string queryString = "SELECT * FROM __InstanceCreationEvent WITHIN .025 WHERE TargetInstance ISA 'Win32_Process'";
ManagementEventWatcher managementEventWatcher = new ManagementEventWatcher(@"\\.\root\CIMV2", queryString);
managementEventWatcher.EventArrived += ProcessStartEventArrived;
managementEventWatcher.Start();
```

For monitoring process termination, use the following query string:

```c#
string queryString = "SELECT * FROM __InstanceDeletionEvent WITHIN .025 WHERE TargetInstance ISA 'Win32_Process'";
```

## References

- [c# - .NET Process Monitor - Stack Overflow](https://stackoverflow.com/questions/1986249/net-process-monitor)
- [c# - Monitor new processes as a non-admin - Stack Overflow](https://stackoverflow.com/questions/38963224/monitor-new-processes-as-a-non-admin)
