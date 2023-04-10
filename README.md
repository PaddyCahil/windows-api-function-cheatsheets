# Windows API Cheatsheet

- snowcra5h@icloud.com
- https://twitter.com/snowcra5h

---

### File Operations
[CreateFile](https://docs.microsoft.com/en-us/windows/win32/api/fileapi/nf-fileapi-createfilea)
```c
HANDLE CreateFile(
  LPCTSTR lpFileName,
  DWORD dwDesiredAccess,
  DWORD dwShareMode,
  LPSECURITY_ATTRIBUTES lpSecurityAttributes,
  DWORD dwCreationDisposition,
  DWORD dwFlagsAndAttributes,
  HANDLE hTemplateFile
); // Opens an existing file or creates a new file.
```
[ReadFile](https://docs.microsoft.com/en-us/windows/win32/api/fileapi/nf-fileapi-readfile)
```c
BOOL ReadFile(
  HANDLE hFile,
  LPVOID lpBuffer,
  DWORD nNumberOfBytesToRead,
  LPDWORD lpNumberOfBytesRead,
  LPOVERLAPPED lpOverlapped
); // Reads data from the specified file.
```
[WriteFile](https://docs.microsoft.com/en-us/windows/win32/api/fileapi/nf-fileapi-writefile)
```c
BOOL WriteFile(
  HANDLE hFile,
  LPCVOID lpBuffer,
  DWORD nNumberOfBytesToWrite,
  LPDWORD lpNumberOfBytesWritten,
  LPOVERLAPPED lpOverlapped
); // Writes data to the specified file.
```
[CloseHandle](https://docs.microsoft.com/en-us/windows/win32/api/handleapi/nf-handleapi-closehandle)
```c
BOOL CloseHandle(
  HANDLE hObject
); // Closes an open handle.
```

### Process Management
[CreateProcess](https://docs.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-createprocessa)
```c
HANDLE CreateProcess(
  LPCTSTR lpApplicationName,
  LPTSTR lpCommandLine,
  LPSECURITY_ATTRIBUTES lpProcessAttributes,
  LPSECURITY_ATTRIBUTES lpThreadAttributes,
  BOOL bInheritHandles,
  DWORD dwCreationFlags,
  LPVOID lpEnvironment,
  LPCTSTR lpCurrentDirectory,
  LPSTARTUPINFO lpStartupInfo,
  LPPROCESS_INFORMATION lpProcessInformation
); // Creates a new process.
```
[WaitForSingleObject](https://docs.microsoft.com/en-us/windows/win32/api/synchapi/nf-synchapi-waitforsingleobject)
```c
DWORD WaitForSingleObject(
  HANDLE hHandle,
  DWORD dwMilliseconds
); // Waits for the specified object to become signaled.
```
[TerminateProcess](https://docs.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-terminateprocess)
```c
BOOL TerminateProcess(
  HANDLE hProcess,
  UINT uExitCode
); // Terminates the specified process.
```

### Memory Management
[VirtualAlloc](https://docs.microsoft.com/en-us/windows/win32/api/memoryapi/nf-memoryapi-virtualalloc)
```c
LPVOID VirtualAlloc(
  LPVOID lpAddress,
  SIZE_T dwSize,
  DWORD flAllocationType,
  DWORD flProtect
); // Reserves, commits, or changes the state of a region of memory within the virtual address space of the calling process.
```
[VirtualFree](https://docs.microsoft.com/en-us/windows/win32/api/memoryapi/nf-memoryapi-virtualfree)
```c
BOOL VirtualFree(
  LPVOID lpAddress,
  SIZE_T dwSize,
  DWORD dwFreeType
); // Releases, decommits, or releases and decommits a region of memory within the virtual address space of the calling process.
```

### Thread Management
[CreateThread](https://docs.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-createthread)
```c
HANDLE CreateThread(
  LPSECURITY_ATTRIBUTES lpThreadAttributes,
  SIZE_T dwStackSize,
  LPTHREAD_START_ROUTINE lpStartAddress,
  LPVOID lpParameter,
  DWORD dwCreationFlags,
  LPDWORD lpThreadId
); // Creates a thread to execute within the virtual address space of the calling process.
```
[ExitThread](https://docs.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-exitthread)
```c
VOID ExitThread(
  DWORD dwExitCode
); // Terminates the calling thread and returns the exit code to the operating system.
```
[GetExitCodeThread](https://docs.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-getexitcodethread)
```c
BOOL GetExitCodeThread(
  HANDLE hThread,
  LPDWORD lpExitCode
); // Retrieves the termination status of the specified thread.
```
[ResumeThread](https://docs.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-resumethread)
```c
DWORD ResumeThread(
  HANDLE hThread
); // Decrements a thread's suspend count. When the suspend count is decremented to zero, the execution of the thread is resumed.
```
[SuspendThread](https://docs.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-suspendthread)
```c
DWORD SuspendThread(
  HANDLE hThread
); // Suspends the specified thread.
```
[TerminateThread](https://docs.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-terminatethread)
```c
BOOL TerminateThread(
  HANDLE hThread,
  DWORD dwExitCode
); // Terminates the specified thread.
```
[CloseHandle](https://docs.microsoft.com/en-us/windows/win32/api/handleapi/nf-handleapi-closehandle)
```c
BOOL CloseHandle(
  HANDLE hObject
); // Closes an open handle.
```

### Dynamic-Link Library (DLL) Management
[LoadLibrary](https://docs.microsoft.com/en-us/windows/win32/api/libloaderapi/nf-libloaderapi-loadlibrarya)
```c
HMODULE LoadLibrary(
  LPCTSTR lpFileName
); // Loads a dynamic-link library (DLL) module into the address space of the calling process.
```
[GetProcAddress](https://docs.microsoft.com/en-us/windows/win32/api/libloaderapi/nf-libloaderapi-getprocaddress)
```c
FARPROC GetProcAddress(
  HMODULE hModule,
  LPCSTR lpProcName
); // Retrieves the address of an exported function or variable from the specified DLL.
```
[FreeLibrary](https://docs.microsoft.com/en-us/windows/win32/api/libloaderapi/nf-libloaderapi-freelibrary)
```c
BOOL FreeLibrary(
  HMODULE hModule
); // Frees the loaded DLL module and, if necessary, decrements its reference count.
```

### Synchronization
[CreateMutex](https://docs.microsoft.com/en-us/windows/win32/api/synchapi/nf-synchapi-createmutexa)
```c
HANDLE CreateMutex(
  LPSECURITY_ATTRIBUTES lpMutexAttributes,
  BOOL bInitialOwner,
  LPCTSTR lpName
); // Creates a named or unnamed mutex object.
```
[CreateSemaphore](https://docs.microsoft.com/en-us/windows/win32/api/synchapi/nf-synchapi-createsemaphorea)
```c
HANDLE CreateSemaphore(
  LPSECURITY_ATTRIBUTES lpSemaphoreAttributes,
  LONG lInitialCount,
  LONG lMaximumCount,
  LPCTSTR lpName
); // Creates a named or unnamed semaphore object.
```
[ReleaseMutex](https://docs.microsoft.com/en-us/windows/win32/api/synchapi/nf-synchapi-releasemutex)
```c
BOOL ReleaseMutex(
  HANDLE hMutex
); // Releases ownership of the specified mutex object.
```
[ReleaseSemaphore](https://docs.microsoft.com/en-us/windows/win32/api/synchapi/nf-synchapi-releasesemaphore)
```c
BOOL ReleaseSemaphore(
  HANDLE hSemaphore,
  LONG lReleaseCount,
  LPLONG lpPreviousCount
); // Increases the count of the specified semaphore object by a specified amount.
```

### Interprocess Communication
[CreatePipe](https://docs.microsoft.com/en-us/windows/win32/api/namedpipeapi/nf-namedpipeapi-createpipe)
```c
BOOL CreatePipe(
  PHANDLE hReadPipe,
  PHANDLE hWritePipe,
  LPSECURITY_ATTRIBUTES lpPipeAttributes,
  DWORD nSize
); // Creates an anonymous pipe and returns handles to the read and write ends of the pipe.
```
[CreateNamedPipe](https://docs.microsoft.com/en-us/windows/win32/api/winbase/nf-winbase-createnamedpipea)
```c
HANDLE CreateNamedPipe(
  LPCTSTR lpName,
  DWORD dwOpenMode,
  DWORD dwPipeMode,
  DWORD nMaxInstances,
  DWORD nOutBufferSize,
  DWORD nInBufferSize,
  DWORD nDefaultTimeOut,
  LPSECURITY_ATTRIBUTES lpSecurityAttributes
); // Creates a named pipe and returns a handle for subsequent pipe operations.
```
[ConnectNamedPipe](https://docs.microsoft.com/en-us/windows/win32/api/namedpipeapi/nf-namedpipeapi-connectnamedpipe)
```c
BOOL ConnectNamedPipe(
  HANDLE hNamedPipe,
  LPOVERLAPPED lpOverlapped
); // Enables a named pipe server process to wait for a client process to connect to an instance of a named pipe.
```
[DisconnectNamedPipe](https://docs.microsoft.com/en-us/windows/win32/api/namedpipeapi/nf-namedpipeapi-disconnectnamedpipe)
```c
BOOL DisconnectNamedPipe(
  HANDLE hNamedPipe
); // Disconnects the server end of a named pipe instance from a client process.
```
[CreateFileMapping](https://docs.microsoft.com/en-us/windows/win32/api/winbase/nf-winbase-createfilemappinga)
```c
HANDLE CreateFileMapping(
  HANDLE hFile,
  LPSECURITY_ATTRIBUTES lpFileMappingAttributes,
  DWORD flProtect,
  DWORD dwMaximumSizeHigh,
  DWORD dwMaximumSizeLow,
  LPCTSTR lpName
); // Creates or opens a named or unnamed file mapping object for a specified file.
```
[MapViewOfFile](https://docs.microsoft.com/en-us/windows/win32/api/memoryapi/nf-memoryapi-mapviewoffile)
```c
LPVOID MapViewOfFile(
  HANDLE hFileMappingObject,
  DWORD dwDesiredAccess,
  DWORD dwFileOffsetHigh,
  DWORD dwFileOffsetLow,
  SIZE_T dwNumberOfBytesToMap
); // Maps a view of a file mapping into the address space of the calling process.
```
[UnmapViewOfFile](https://docs.microsoft.com/en-us/windows/win32/api/memoryapi/nf-memoryapi-unmapviewoffile)
```c
BOOL UnmapViewOfFile(
  LPCVOID lpBaseAddress
); // Unmaps a mapped view of a file from the calling process's address space.
```
[CloseHandle](https://docs.microsoft.com/en-us/windows/win32/api/handleapi/nf-handleapi-closehandle)
```c
BOOL CloseHandle(
  HANDLE hObject
); // Closes an open handle.
```

### Winsock Cheat Sheet
[WSAStartup](https://docs.microsoft.com/en-us/windows/win32/api/winsock/nf-winsock-wsastartup)
```c
int WSAStartup(
    WORD wVersionRequired, 
    LPWSADATA lpWSAData
); // Initializes the Winsock library for an application. Must be called before any other Winsock functions.
```
[WSACleanup](https://docs.microsoft.com/en-us/windows/win32/api/winsock/nf-winsock-wsacleanup)
```c
int WSACleanup(
    void
); // Terminates the use of the Winsock library. Must be called once per each successful WSAStartup call.
```
[socket](https://docs.microsoft.com/en-us/windows/win32/api/winsock2/nf-winsock2-socket)
```c
SOCKET socket(
    int af, 
    int type, 
    int protocol
); // Creates a new socket for network communication.
```
[bind](https://docs.microsoft.com/en-us/windows/win32/api/winsock/nf-winsock-bind)
```c
int bind(
    SOCKET s, 
    const struct sockaddr *name, 
    int namelen
); // Binds a socket to a specific local address and port.
```
[listen](https://docs.microsoft.com/en-us/windows/win32/api/winsock/nf-winsock-listen)
```c
int listen(
    SOCKET s, 
    int backlog
); // Sets a socket to listen for incoming connections.
```
[accept](https://learn.microsoft.com/en-us/windows/win32/api/Winsock2/nf-winsock2-accept)
```c
SOCKET accept(
    SOCKET s, 
    struct sockaddr *addr, 
    int *addrlen
); // Accepts a new incoming connection on a listening socket.
```
[connect](https://learn.microsoft.com/en-us/windows/win32/api/winsock2/nf-winsock2-connect)
```c
int connect(
    SOCKET s, 
    const struct sockaddr *name, 
    int namelen
); // Initiates a connection on a socket to a remote address.
```
[send](https://learn.microsoft.com/en-us/windows/win32/api/winsock2/nf-winsock2-send)
```c
int send(
    SOCKET s, 
    const char *buf, 
    int len, 
    int flags
); // Sends data on a connected socket.
```
[recv](https://learn.microsoft.com/en-us/windows/win32/api/winsock2/nf-winsock2-recv)
```c
int recv(
    SOCKET s, 
    char *buf, 
    int len, 
    int flags
); // Receives data from a connected socket.
```
[closesocket](https://learn.microsoft.com/en-us/windows/win32/api/winsock2/nf-winsock2-closesocket)
```c
int closesocket(
    SOCKET s
); //Closes a socket and frees its resources.
```

### Registry Operations
[RegOpenKeyExW](https://learn.microsoft.com/en-us/windows/win32/api/winreg/nf-winreg-regopenkeyexw)
```c
LONG RegOpenKeyExW(
    HKEY hKey, 
    LPCWTSTR lpSubKey, 
    DWORD ulOptions, 
    REGSAM samDesired, 
    PHKEY phkResult
); // Opens the specified registry key.
```
[RegQueryValueExW](https://learn.microsoft.com/en-us/windows/win32/api/winreg/nf-winreg-regqueryvaluew)
```c
LONG RegQueryValueExW(
    HKEY hKey, 
    LPCWTSTR lpValueName, 
    LPDWORD lpReserved, 
    LPDWORD lpType, 
    LPBYTE lpData, 
    LPDWORD lpcbData
); // Retrieves the type and data of the specified value name associated with an open registry key.
```
[RegSetValueExW](https://learn.microsoft.com/en-us/windows/win32/api/winreg/nf-winreg-regsetvalueexw)
```c
LONG RegSetValueEx(
    HKEY hKey, 
    LPCWTSTR lpValueName, 
    DWORD Reserved, 
    DWORD dwType, 
    const BYTE *lpData, 
    DWORD cbData
); // Sets the data and type of the specified value name associated with an open registry key.
```
[RegCloseKey](https://docs.microsoft.com/en-us/windows/win32/api/winreg/nf-winreg-regclosekey)
```c
LONG RegCloseKey(
    HKEY hKey
); // Closes a handle to the specified registry key.
```

### Error Handling
[WSAGetLastError](https://docs.microsoft.com/en-us/windows/win32/api/winsock/nf-winsock-wsagetlasterror)
```c
int WSAGetLastError(
    void
); // Returns the error status for the last Windows Sockets operation that failed.
```
[WSASetLastError](https://docs.microsoft.com/en-us/windows/win32/api/winsock/nf-winsock-wsasetlasterror)
```c
void WSASetLastError(
    int iError
); // Sets the error status for the last Windows Sockets operation.
```
[WSAGetOverlappedResult](https://docs.microsoft.com/en-us/windows/win32/api/winsock2/nf-winsock2-wsagetoverlappedresult)
```c
BOOL WSAGetOverlappedResult(
    SOCKET s, 
    LPWSAOVERLAPPED lpOverlapped, 
    LPDWORD lpcbTransfer, 
    BOOL fWait, 
    LPDWORD lpdwFlags
); // Determines the results of an overlapped operation on the specified socket.
```
[WSAIoctl](https://docs.microsoft.com/en-us/windows/win32/api/winsock2/nf-winsock2-wsaioctl)
```c
int WSAIoctl(
    SOCKET s, 
    DWORD dwIoControlCode, 
    LPVOID lpvInBuffer, 
    DWORD cbInBuffer, 
    LPVOID lpvOutBuffer, 
    DWORD cbOutBuffer, 
    LPDWORD lpcbBytesReturned, 
    LPWSAOVERLAPPED lpOverlapped, 
    LPWSAOVERLAPPED_COMPLETION_ROUTINE lpCompletionRoutine
); // Controls the mode of a socket.
```
[WSACreateEvent](https://docs.microsoft.com/en-us/windows/win32/api/winsock2/nf-winsock2-wsacreateevent)
```c
WSAEVENT WSACreateEvent(
    void
); // Creates a new event object.
```
[WSASetEvent](https://docs.microsoft.com/en-us/windows/win32/api/winsock2/nf-winsock2-wsasetevent)
```c
BOOL WSASetEvent(
    WSAEVENT hEvent
); // Sets the state of the specified event object to signaled.
```
[WSAResetEvent](https://docs.microsoft.com/en-us/windows/win32/api/winsock2/nf-winsock2-wsaresetevent)
```c
BOOL WSAResetEvent(
    WSAEVENT hEvent
); // Sets the state of the specified event object to nonsignaled.
```
[WSACloseEvent](https://docs.microsoft.com/en-us/windows/win32/api/winsock2/nf-winsock2-wsacloseevent)
```c
BOOL WSACloseEvent(
    WSAEVENT hEvent
); // Closes an open event object handle.
```
[WSAWaitForMultipleEvents](https://docs.microsoft.com/en-us/windows/win32/api/winsock2/nf-winsock2-wsawaitformultipleevents)
```c
DWORD WSAWaitForMultipleEvents(
    DWORD cEvents, 
    const WSAEVENT *lphEvents, 
    BOOL fWaitAll, 
    DWORD dwTimeout, 
    BOOL fAlertable
); // Waits for multiple event objects and returns when the specified events are signaled or the time-out interval elapses.
```

## Unicode String Functions
```c
#include <wchar.h> // for wide character string routines
```

### String Length
```c
size_t wcslen(
    const wchar_t *str
); // Returns the length of the given wide string.
```

### String Copy
[wcscpy]
```c
wchar_t *wcscpy(
    wchar_t *dest, 
    const wchar_t *src
); // Copies the wide string from src to dest.
```
[wcsncpy]
```c
wchar_t *wcsncpy(
    wchar_t *dest, 
    const wchar_t *src, 
    size_t count
); // Copies at most count characters from the wide string src to dest.
```

### String Concatenation
[wcscat]
```c
wchar_t *wcscat(
    wchar_t *dest, 
    const wchar_t *src
); // Appends the wide string src to the end of the wide string dest.
```
[wcsncat]
```c
wchar_t *wcsncat(
    wchar_t *dest, 
    const wchar_t *src, 
    size_t count
); // Appends at most count characters from the wide string src to the end of the wide string dest.
```

### String Comparison
[wcscmp]
```c
int wcscmp(
    const wchar_t *str1, 
    const wchar_t *str2
); // Compares two wide strings lexicographically.
```
[wcsncmp]
```c
int wcsncmp(
    const wchar_t *str1, 
    const wchar_t *str2, 
    size_t count
); // Compares up to count characters of two wide strings lexicographically.
```
[_wcsicmp]
```c
int _wcsicmp(
    const wchar_t *str1, 
    const wchar_t *str2
); // Compares two wide strings lexicographically, ignoring case.
```
[_wcsnicmp]
```c
int _wcsnicmp(
    const wchar_t *str1, 
    const wchar_t *str2, 
    size_t count
); // Compares up to count characters of two wide strings lexicographically, ignoring case.
```

### String Search
[wcschr]
```c
wchar_t *wcschr(
    const wchar_t *str, 
    wchar_t c
); // Finds the first occurrence of the wide character c in the wide string str.
```
[wcsrchr]
```c
wchar_t *wcsrchr(
    const wchar_t *str, 
    wchar_t c
); // Finds the last occurrence of the wide character c in the wide string str.
```
[wcspbrk]
```c
wchar_t *wcspbrk(
    const wchar_t *str1, 
    const wchar_t *str2
); // Finds the first occurrence in the wide string str1 of any character from the wide string str2.
```
[wcsstr]
```c
wchar_t *wcsstr(
    const wchar_t *str1, 
    const wchar_t *str2
); // Finds the first occurrence of the wide string str2 in the wide string str1.
```
[wcstok]
```c
wchar_t *wcstok(
    wchar_t *str, 
    const wchar_t *delimiters
); // Splits the wide string str into tokens based on the delimiters.
```

### Character Classification and Conversion
[towupper]
```c
wint_t towupper(
    wint_t c
); // Converts a wide character to uppercase.
```
[towlower]
```c
wint_t towlower(
    wint_t c
); // Converts a wide character to lowercase.
```
[iswalpha]
```c
int iswalpha(
    wint_t c
); // Checks if the wide character is an alphabetic character.
```
[iswdigit]
```c
int iswdigit(
    wint_t c
); // Checks if the wide character is a decimal digit.
```
[iswalnum]
```c
int iswalnum(
    wint_t c
); // Checks if the wide character is an alphanumeric character.
```
[iswspace]
```c
int iswspace(
    wint_t c
); // Checks if the wide character is a whitespace character.
```
[iswxdigit]
```c
int iswxdigit(
    wint_t c
); // Checks if the wide character is a valid hexadecimal digit.
```
