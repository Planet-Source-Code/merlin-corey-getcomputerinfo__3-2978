<div align="center">

## GetComputerInfo


</div>

### Description

This code allows you to get windows version information, current windows User Name, and Computer Name (utilizing the windows API)... {For people searching: USERNAME COMPUTERNAME WINDOWSVERSION GETVERSION GETVERSIONEX GETUSERNAME GETCOMPUTERNAME}

Note: Updated this old code to be actual Win32 code and added the OS version stuff.
 
### More Info
 
This must be compiled as a windows project; if you're using MSVC++, check the project settings, link section, and change subsystem to "windows".


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Merlin Corey](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/merlin-corey.md)
**Level**          |Beginner
**User Rating**    |4.7 (28 globes from 6 users)
**Compatibility**  |C, C\+\+ \(general\), Microsoft Visual C\+\+, Borland C\+\+
**Category**       |[Validation/ Processing](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/validation-processing__3-16.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/merlin-corey-getcomputerinfo__3-2978/archive/master.zip)

### API Declarations

```
windows.h
lmcons.h
```


### Source Code

```
// Header for windows API
#include <windows.h>
// Header for various defines
#include <lmcons.h>
// Entry function for windows projects
int WINAPI WinMain(HINSTANCE hCur, HINSTANCE hPrev, LPSTR sCmd, int nShow)
{
	// Variable for output buffer
	TCHAR sMsg[1024];
	// Variable for username string
	TCHAR sUserName[UNLEN + 1];
	// Variable to computername string
	TCHAR sCompName[MAX_COMPUTERNAME_LENGTH + 1];
	// Variable for username length
  DWORD dwUserName = sizeof(sUserName);
  // Variable for compname length
  DWORD dwCompName = sizeof(sCompName);
	// Variable for os version structure
	OSVERSIONINFO osver;
	osver.dwOSVersionInfoSize = sizeof(OSVERSIONINFO);
	// Get OS Version info
	GetVersionEx(&osver);
	// Get User Name
  GetUserName(sUserName, &dwUserName);
  // Get Computer Name
  GetComputerName(sCompName, &dwCompName);
	// Copy to message buffer
	wsprintf(sMsg, "User %s is currently logged onto computer %s running Windows version %d.%d build %d %s",
		sUserName,
		sCompName,
		osver.dwMajorVersion,
		osver.dwMinorVersion,
		osver.dwBuildNumber,
		osver.szCSDVersion
		);
	// Display information
	MessageBox(NULL, sMsg, "Computer Information", MB_OK | MB_ICONINFORMATION);
  // End instance
  return (0);
}
```

