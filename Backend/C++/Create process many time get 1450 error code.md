# Getting Error Code 1450 When Creating And Terminate Processes Too Many Times

This is a note for Windows OS: sometimes, if you create and terminate processes many times, you may encounter error code 1450. This error means that there are not enough system resources to create a process.

The problem may be due to forgetting to close handles when terminating processes. Therefore, we need to completely close the process handle after terminating the process.

Keeping handle references will block the system from releasing resources.

## Reference

- [Terminating a Process - Win32 apps | Microsoft Learn](https://learn.microsoft.com/en-us/windows/win32/procthread/terminating-a-process)
- [TerminateProcess function (processthreadsapi.h) - Win32 apps | Microsoft Learn](https://learn.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-terminateprocess)
- [CreateProcessA function (processthreadsapi.h) - Win32 apps | Microsoft Learn](https://learn.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-createprocessa)
- [CloseHandle function (handleapi.h) - Win32 apps | Microsoft Learn](https://learn.microsoft.com/en-us/windows/win32/api/handleapi/nf-handleapi-closehandle)
