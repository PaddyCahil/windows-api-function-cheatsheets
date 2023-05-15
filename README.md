<div align="center">
  <img src="https://github.com/snowcra5h/windows-api-function-cheatsheets/blob/main/API%20CheatSheets.gif" width="300" alt="WINAPI" style="margin-bottom: 10px;">
  <p>snowcra5h@icloud.com</p>
  <p><a href="https://twitter.com/snowcra5h" target="_blank" rel="noopener noreferrer">https://twitter.com/snowcra5h</a></p>
</div>

# Windows API Function Calls
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
[OpenProcess](https://learn.microsoft.com/en-us/windows/win32/api/processthreadsapi/nf-processthreadsapi-openprocess)
```c
HANDLE OpenProcess(
  [in] DWORD dwDesiredAccess,
  [in] BOOL  bInheritHandle,
  [in] DWORD dwProcessId
); // Opens an existing local process object. e.g., try to open target process
```
```c
hProc = OpenProcess( PROCESS_CREATE_THREAD | PROCESS_QUERY_INFORMATION | PROCESS_VM_OPERATION | PROCESS_VM_READ | PROCESS_VM_WRITE, FALSE, (DWORD) pid);
```
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
[CreateToolhelp32Snapshot](https://learn.microsoft.com/en-us/windows/win32/api/tlhelp32/nf-tlhelp32-createtoolhelp32snapshot)
```c
HANDLE CreateToolhelp32Snapshot(
  [in] DWORD dwFlags,
  [in] DWORD th32ProcessID
); // used to obtain information about processes and threads running on a Windows system.
```
[Process32First](https://learn.microsoft.com/en-us/windows/win32/api/tlhelp32/nf-tlhelp32-process32first)
```c
BOOL Process32First(
  [in]      HANDLE           hSnapshot,
  [in, out] LPPROCESSENTRY32 lppe
); // used to retrieve information about the first process encountered in a system snapshot, which is typically taken using the CreateToolhelp32Snapshot function.
```
[Process32Next](https://learn.microsoft.com/en-us/windows/win32/api/tlhelp32/nf-tlhelp32-process32next)
```c
BOOL Process32Next(
  [in]  HANDLE           hSnapshot,
  [out] LPPROCESSENTRY32 lppe
); // used to retrieve information about the next process in a system snapshot after Process32First has been called. This function is typically used in a loop to enumerate all processes captured in a snapshot taken using the CreateToolhelp32Snapshot function.
```

### Memory Management
[VirtualAlloc](https://docs.microsoft.com/en-us/windows/win32/api/memoryapi/nf-memoryapi-virtualalloc)
```c
LPVOID VirtualAlloc(
  LPVOID lpAddress,
  SIZE_T dwSize,                // Shellcode must be between 0x1 and 0x10000 bytes (page size)
  DWORD flAllocationType,       // #define MEM_COMMIT 0x00001000
  DWORD flProtect               // #define PAGE_EXECUTE_READWRITE 0x00000040  
); // Reserves, commits, or changes the state of a region of memory within the virtual address space of the calling process.
```
tags: #DEP

[VirtualFree](https://docs.microsoft.com/en-us/windows/win32/api/memoryapi/nf-memoryapi-virtualfree)
```c
BOOL VirtualFree(
  LPVOID lpAddress,
  SIZE_T dwSize,
  DWORD dwFreeType
); // Releases, decommits, or releases and decommits a region of memory within the virtual address space of the calling process.
```
[VirtualProtect function (memoryapi.h)](https://learn.microsoft.com/en-us/windows/win32/api/memoryapi/nf-memoryapi-virtualprotect)
```c
BOOL VirtualProtect(
  LPVOID lpAddress,
  SIZE_T dwSize,
  DWORD  flNewProtect,
  PDWORD lpflOldProtect
); // Changes the protection on a region of committed pages in the virtual address space of the calling process.
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

---

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

--- 

## Win32 Structs Cheat Sheet
### Common Structs
[**`SYSTEM_INFO`**](https://docs.microsoft.com/en-us/windows/win32/api/sysinfoapi/ns-sysinfoapi-system_info)
```cpp
#include <sysinfoapi.h>
// Contains information about the current computer system, including the architecture and type of the processor, the number of processors, and the page size.
typedef struct _SYSTEM_INFO {
    union {
        DWORD dwOemId;
        struct {
            WORD wProcessorArchitecture;
            WORD wReserved;
        } DUMMYSTRUCTNAME;
    } DUMMYUNIONNAME;
    DWORD dwPageSize;
    LPVOID lpMinimumApplicationAddress;
    LPVOID lpMaximumApplicationAddress;
    DWORD_PTR dwActiveProcessorMask;
    DWORD dwNumberOfProcessors;
    DWORD dwProcessorType;
    DWORD dwAllocationGranularity;
    WORD wProcessorLevel;
    WORD wProcessorRevision;
} SYSTEM_INFO;
```
[**`FILETIME`**](https://docs.microsoft.com/en-us/windows/win32/api/minwinbase/ns-minwinbase-filetime)
```cpp
#include <minwinbase.h>
// Represents the number of 100-nanosecond intervals since January 1, 1601 (UTC). Used for file and system time.
typedef struct _FILETIME {
    DWORD dwLowDateTime;
    DWORD dwHighDateTime;
} FILETIME;
```
[**`STARTUPINFO`**](https://docs.microsoft.com/en-us/windows/win32/api/processthreadsapi/ns-processthreadsapi-startupinfoa)
```cpp
#include <processthreadsapi.h>
// Specifies the window station, desktop, standard handles, and appearance of the main window for a process at creation time.
typedef struct _STARTUPINFOA {
    DWORD  cb;
    LPSTR  lpReserved;
    LPSTR  lpDesktop;
    LPSTR  lpTitle;
    DWORD  dwX;
    DWORD  dwY;
    DWORD  dwXSize;
    DWORD  dwYSize;
    DWORD  dwXCountChars;
    DWORD  dwYCountChars;
    DWORD  dwFillAttribute;
    DWORD  dwFlags;
    WORD   wShowWindow;
    WORD   cbReserved2;
    LPBYTE lpReserved2;
    HANDLE hStdInput;
    HANDLE hStdOutput;
    HANDLE hStdError;
} STARTUPINFOA, *LPSTARTUPINFOA;
```
[**`PROCESS_INFORMATION`**](https://docs.microsoft.com/en-us/windows/win32/api/processthreadsapi/ns-processthreadsapi-process_information)
```cpp
#include <processthreadsapi.h>
// Contains information about a newly created process and its primary thread.
typedef struct _PROCESS_INFORMATION {
    HANDLE hProcess;
    HANDLE hThread;
    DWORD  dwProcessId;
    DWORD  dwThreadId;
} PROCESS_INFORMATION, *LPPROCESS_INFORMATION;
```
[**`PROCESSENTRY32`**](https://learn.microsoft.com/en-us/windows/win32/api/tlhelp32/ns-tlhelp32-processentry32)
```c
#include <tlhelp32.h>
typedef struct tagPROCESSENTRY32 {
  DWORD     dwSize;
  DWORD     cntUsage;
  DWORD     th32ProcessID;
  ULONG_PTR th32DefaultHeapID;
  DWORD     th32ModuleID;
  DWORD     cntThreads;
  DWORD     th32ParentProcessID;
  LONG      pcPriClassBase;
  DWORD     dwFlags;
  CHAR      szExeFile[MAX_PATH];
} PROCESSENTRY32;
```

[**`SECURITY_ATTRIBUTES`**](https://docs.microsoft.com/en-us/previous-versions/windows/desktop/legacy/aa379560(v=vs.85))
```cpp
// Determines whether the handle can be inherited by child processes and specifies a security descriptor for a new object.
typedef struct _SECURITY_ATTRIBUTES {
    DWORD  nLength;
    LPVOID lpSecurityDescriptor;
    BOOL   bInheritHandle;
} SECURITY_ATTRIBUTES, *LPSECURITY_ATTRIBUTES;
```
[**`OVERLAPPED`**](https://docs.microsoft.com/en-us/windows/win32/api/minwinbase/ns-minwinbase-overlapped)
```cpp
#inluce <minwinbase.h>
// Contains information used in asynchronous (also known as overlapped) input and output (I/O) operations.
typedef struct _OVERLAPPED {
    ULONG_PTR Internal;
    ULONG_PTR InternalHigh;
    union {
        struct {
            DWORD Offset;
            DWORD OffsetHigh;
        } DUMMYSTRUCTNAME;
        PVOID Pointer;
    } DUMMYUNIONNAME;
    HANDLE hEvent;
} OVERLAPPED, *LPOVERLAPPED;
```
[**`GUID`**](https://docs.microsoft.com/en-us/windows/win32/api/guiddef/ns-guiddef-guid)
```cpp
#include <guiddef.h>
// Represents a globally unique identifier (GUID), used to identify objects, interfaces, and other items.
typedef struct _GUID {
    unsigned long  Data1;
    unsigned short Data2;
    unsigned short Data3;
    unsigned char  Data4[8];
} GUID;
```
[**`MEMORY_BASIC_INFORMATION`**](https://docs.microsoft.com/en-us/windows/win32/api/winnt/ns-winnt-memory_basic_information)
```cpp
#include <winnt.h>
// Contains information about a range of pages in the virtual address space of a process.
typedef struct _MEMORY_BASIC_INFORMATION {
    PVOID  BaseAddress;
    PVOID  AllocationBase;
    DWORD  AllocationProtect;
    SIZE_T RegionSize;
    DWORD  State;
    DWORD  Protect;
    DWORD  Type;
} MEMORY_BASIC_INFORMATION, *PMEMORY_BASIC_INFORMATION;
```
[**`SYSTEMTIME`**](https://docs.microsoft.com/en-us/windows/win32/api/minwinbase/ns-minwinbase-systemtime)
```cpp
#include <minwinbase.h>
// Specifies a date and time, using individual members for the month, day, year, weekday, hour, minute, second, and millisecond.
typedef struct _SYSTEMTIME {
    WORD wYear;
    WORD wMonth;
    WORD wDayOfWeek;
    WORD wDay;
    WORD wHour;
    WORD wMinute;
    WORD wSecond;
    WORD wMilliseconds;
} SYSTEMTIME, *PSYSTEMTIME, *LPSYSTEMTIME;
```
[**`COORD`**](https://docs.microsoft.com/en-us/windows/console/coord-str)
```cpp
// Defines the coordinates of a character cell in a console screen buffer, where the origin (0,0) is at the top-left corner.
typedef struct _COORD {
    SHORT X;
    SHORT Y;
} COORD, *PCOORD;
```
[**`SMALL_RECT`**](https://docs.microsoft.com/en-us/windows/console/small-rect-str)
```cpp
//  Defines the coordinates of the upper left and lower right corners of a rectangle.
typedef struct _SMALL_RECT {
    SHORT Left;
    SHORT Top;
    SHORT Right;
    SHORT Bottom;
} SMALL_RECT;
```
[**`CONSOLE_SCREEN_BUFFER_INFO`**](https://docs.microsoft.com/en-us/windows/console/console-screen-buffer-info-str)
```cpp
// Contains information about a console screen buffer.
typedef struct _CONSOLE_SCREEN_BUFFER_INFO {
    COORD      dwSize;
    COORD      dwCursorPosition;
    WORD       wAttributes;
    SMALL_RECT srWindow;
    COORD      dwMaximumWindowSize;
} CONSOLE_SCREEN_BUFFER_INFO, *PCONSOLE_SCREEN_BUFFER_INFO;
```
[**`WSADATA`**](https://docs.microsoft.com/en-us/windows/win32/api/winsock/ns-winsock-wsadata)
```cpp
#include <winsock.h>
// Contains information about the Windows Sockets implementation.
typedef struct WSAData {
    WORD           wVersion;
    WORD           wHighVersion;
    unsigned short iMaxSockets;
    unsigned short iMaxUdpDg;
    char FAR       *lpVendorInfo;
    char           szDescription[WSADESCRIPTION_LEN+1];
    char           szSystemStatus[WSASYS_STATUS_LEN+1];
} WSADATA, *LPWSADATA;
```
[**`CRITICAL_SECTION`**]([struct RTL_CRITICAL_SECTION (nirsoft.net)](https://www.nirsoft.net/kernel_struct/vista/RTL_CRITICAL_SECTION.html))
```c++
// Represents a critical section object, which is used to provide synchronization access to a shared resource.
typedef struct _RTL_CRITICAL_SECTION {
    PRTL_CRITICAL_SECTION_DEBUG DebugInfo;
    LONG LockCount;
    LONG RecursionCount;
    HANDLE OwningThread;
    HANDLE LockSemaphore;
    ULONG_PTR SpinCount;
} RTL_CRITICAL_SECTION, *PRTL_CRITICAL_SECTION;
```
[**`WSAPROTOCOL_INFO`**](https://docs.microsoft.com/en-us/windows/win32/api/winsock2/ns-winsock2-wsaprotocol_infoa)
```c++
#include <winsock2.h>
// Contains Windows Sockets protocol information.
typedef struct _WSAPROTOCOL_INFOA {
    DWORD          dwServiceFlags1;
    DWORD          dwServiceFlags2;
    DWORD          dwServiceFlags3;
    DWORD          dwServiceFlags4;
    DWORD          dwProviderFlags;
    GUID           ProviderId;
    DWORD          dwCatalogEntryId;
    WSAPROTOCOLCHAIN ProtocolChain;
    int            iVersion;
    int            iAddressFamily;
    int            iMaxSockAddr;
    int            iMinSockAddr;
    int            iSocketType;
    int            iProtocol;
    int            iProtocolMaxOffset;
    int            iNetworkByteOrder;
    int            iSecurityScheme;
    DWORD          dwMessageSize;
    DWORD          dwProviderReserved;
    CHAR           szProtocol[WSAPROTOCOL_LEN+1];
} WSAPROTOCOL_INFOA, *LPWSAPROTOCOL_INFOA;
```
[**`MSGHDR`**](https://docs.microsoft.com/en-us/windows/win32/api/ws2tcpip/ns-ws2tcpip-_msghdr)
```c++
#include <ws2def.h>
// Contains message information for use with the `sendmsg` and `recvmsg` functions.
typedef struct _WSAMSG {
    LPSOCKADDR       name;
    INT              namelen;
    LPWSABUF         lpBuffers;
    ULONG            dwBufferCount;
    WSABUF           Control;
    ULONG            dwFlags;
} WSAMSG, *PWSAMSG, *LPWSAMSG;
```

### Win32 Sockets Structs Cheat Sheet (winsock.h)
[**`SOCKADDR`**](https://docs.microsoft.com/en-us/windows/win32/api/winsock/ns-winsock-sockaddr)
```cpp
// A generic socket address structure used for compatibility with various address families.
typedef struct sockaddr {
    u_short sa_family;
    char    sa_data[14];
} SOCKADDR, *PSOCKADDR, *LPSOCKADDR;
```
[**`SOCKADDR_IN`**](https://docs.microsoft.com/en-us/windows/win32/api/winsock/ns-winsock-sockaddr_in)
```cpp
// Represents an IPv4 socket address, containing the IPv4 address, port number, and address family.
typedef struct sockaddr_in {
    short          sin_family;
    u_short        sin_port;
    struct in_addr sin_addr;
    char           sin_zero[8];
} SOCKADDR_IN, *PSOCKADDR_IN, *LPSOCKADDR_IN;
```
[**`LINGER`**](https://docs.microsoft.com/en-us/windows/win32/api/winsock/ns-winsock-linger)
```cpp
// Used to set the socket option SO_LINGER, which determines the action taken when unsent data is queued on a socket and a `closesocket` is performed.
typedef struct linger {
    u_short l_onoff;
    u_short l_linger;
} LINGER, *PLINGER, *LPLINGER;
```
[**`TIMEVAL`**](https://docs.microsoft.com/en-us/windows/win32/api/winsock/ns-winsock-timeval)
```cpp
// Represents a time interval, used with the `select` function to specify a timeout period.
typedef struct timeval {
    long tv_sec;
    long tv_usec;
} TIMEVAL, *PTIMEVAL, *LPTIMEVAL;
```
[**`FD_SET`**](https://docs.microsoft.com/en-us/windows/win32/api/winsock/ns-winsock-fd_set)
```cpp
// Represents a set of sockets used with the `select` function to check for socket events.
typedef struct fd_set {
    u_int fd_count;
    SOCKET fd_array[FD_SETSIZE];
} fd_set, *Pfd_set, *LPfd_set;
```

### Win32 Sockets Structs Cheat Sheet (winsock2.h)
[**`IN_ADDR`**](https://learn.microsoft.com/en-us/windows/win32/api/winsock2/ns-winsock2-in_addr)
```cpp
// Represents an IPv4 address.
typedef struct in_addr {
    union {
        struct {
            u_char s_b1, s_b2, s_b3, s_b4;
        } S_un_b;
        struct {
            u_short s_w1, s_w2;
        } S_un_w;
        u_long S_addr;
    } S_un;
} IN_ADDR, *PIN_ADDR, *LPIN_ADDR;
```

### Win32 Sockets Structs Cheat Sheet (ws2def.h)
[**`ADDRINFO`**](https://learn.microsoft.com/en-us/windows/win32/api/ws2def/ns-ws2def-addrinfow)
```cpp
#include <ws2def.h>
// Contains information about an address for use with the `getaddrinfo` function, and is used to build a linked list of addresses.
typedef struct addrinfoW {
    int             ai_flags;
    int             ai_family;
    int             ai_socktype;
    int             ai_protocol;
    size_t          ai_addrlen;
    PWSTR           *ai_canonname;
    struct sockaddr *ai_addr;
    struct addrinfo *ai_next;
} ADDRINFOW, *PADDRINFOW;
```
[**`WSABUF`**](https://learn.microsoft.com/en-us/windows/win32/api/ws2def/ns-ws2def-wsabuf)
```cpp
#include <ws2def.h>
// Contains a pointer to a buffer and its length. Used for scatter/gather I/O operations.
typedef struct _WSABUF {
    ULONG len;
    __field_bcount(len) CHAR FAR *buf;
} WSABUF, FAR * LPWSABUF;
```
[**`SOCKADDR_IN6`**](https://docs.microsoft.com/en-us/windows/win32/api/ws2ipdef/ns-ws2ipdef-sockaddr_in6)
```cpp
#include <ws2ipdef.h>
// Represents an IPv6 socket address, containing the IPv6 address, port number, flow info, and address family.
typedef struct sockaddr_in6 {
    short          sin6_family;
    u_short        sin6_port;
    u_long         sin6_flowinfo;
    struct in6_addr sin6_addr;
    u_long         sin6_scope_id;
} SOCKADDR_IN6, *PSOCKADDR_IN6, *LPSOCKADDR_IN6;
```
[**`IN6_ADDR`**](https://learn.microsoft.com/en-us/windows/win32/api/in6addr/ns-in6addr-in6_addr)
```cpp
#include <in6addr.h>
// Represents an IPv6 address.
typedef struct in6_addr {
    union {
        u_char Byte[16];
        u_short Word[8];
    } u;
} IN6_ADDR, *PIN6_ADDR, *LPIN6_ADDR;
```
