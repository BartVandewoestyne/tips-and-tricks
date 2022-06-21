* Rename multiple files at once:

    rename *.txt *.pdf
    rename * *.pdf
    
* Checking DNS resolving:

    nslookup s-be-jnks07-21.trealitysvs.net 10.1.147.132

* To redirect both STDERR and STDOUT to a file:

    command > logfile 2>&1

  See also https://stackoverflow.com/questions/15346863/windows-batch-script-redirect-all-output-to-a-file
  
* Find text in files:

    findstr /s /i /m "MyClass" *.cpp

* Show the contents of your PATH environment variable line by line:

    echo %path:;=&echo.%
    
* Time a command (see https://stackoverflow.com/questions/673523/how-do-i-measure-execution-time-of-a-command-on-the-windows-command-line)

    powershell -Command "Measure-Command {echo hi | Out-Default}"

* Checking your disk:

    chkdsk D: => does not fix any errors
    chkdsk /f => fixes errors
      /f => fix errors
      /r => locates bad sectors and recovers readable info
      /x => forces the volume to dismount first.  All open handles to the drive are invalidated.

  See also:
    https://www.dell.com/support/article/fr-be/sln86661/het-hulpprogramma-chkdsk-gebruiken?lang=nl
    https://www.clickx.be/tips/168591/repareer-je-harde-schijf/

* Using robocopy for backup:

    robocopy F: G:\2020XXYY_BACKUP /MIR

  See also:
    https://adamtheautomator.com/robocopy-the-ultimate/
    https://superuser.com/questions/814102/robocopy-command-to-do-an-incremental-backup
    https://www.techrepublic.com/article/how-to-quickly-back-up-just-your-data-in-windows-10-with-robocopys-multi-threaded-feature/

Performance measuring and benchmarking
--------------------------------------

* The Windows Experience Index assesses key system components on a scale of
  1.0 to 9.9.

  https://www.makeuseof.com/tag/check-windows-experience-score-windows-10/

  PowerShell in Administrator mode opstarten, en dan:

    PS C:\WINDOWS\system32> Get-WmiObject -class Win32_WinSAT

    __GENUS               : 2
    __CLASS               : Win32_WinSAT
    __SUPERCLASS          :
    __DYNASTY             : Win32_WinSAT
    __RELPATH             : Win32_WinSAT.TimeTaken="MostRecentAssessment"
    __PROPERTY_COUNT      : 8
    __DERIVATION          : {}
    __SERVER              : ESLCLT1569
    __NAMESPACE           : root\cimv2
    __PATH                : \\ESLCLT1569\root\cimv2:Win32_WinSAT.TimeTaken="MostRecentAssessment"
    CPUScore              : 8.9
    D3DScore              : 9.9
    DiskScore             : 7.4
    GraphicsScore         : 8
    MemoryScore           : 8.9
    TimeTaken             : MostRecentAssessment
    WinSATAssessmentState : 1
    WinSPRLevel           : 7.4
    PSComputerName        : ESLCLT1569

* winsat disk -drive d:
