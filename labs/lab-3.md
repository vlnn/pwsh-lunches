# Lab 3 - using the help systemks

1. Run `Update-Help` to get latest help locally and ensure the privileges are elevated.

    `Update-Help -Verbose -Force -ErrorAction SilentlyContinue`

    (see https://stackoverflow.com/questions/39834452/powershell-fails-with-update to the get reasoning)

2. Find any cmdlets capable of converting other cmdlets' output into HTML?

    `PS C:\Repos\pwsh> Get-Help -Name HTML`

    ``` powershell
    NAME
    ConvertTo-Html
    SYNOPSIS
    Converts .NET objects into HTML that can be displayed in a Web browser.
    ...
    ```

    *or*

    `PS C:\Repos\pwsh> Get-Help -Verb Convert  -Category Cmdlet`

    ```powershell
    Name                              Category  Module                    Synopsis
    ----                              --------  ------                    --------
    Convert-Path                      Cmdlet    Microsoft.PowerShell.M... Converts a path from a PowerShell path to a PowerShell provider path.
    Convert-String                    Cmdlet    Microsoft.PowerShell.U... Formats a string to match examples.
    ConvertFrom-Csv                   Cmdlet    Microsoft.PowerShell.U... Converts object properties in comma-separated value (CSV) format into CSV...
    ConvertFrom-Json                  Cmdlet    Microsoft.PowerShell.U... Converts a JSON-formatted string to a custom object.
    ConvertFrom-String                Cmdlet    Microsoft.PowerShell.U... Extracts and parses structured properties from string content.
    ConvertFrom-StringData            Cmdlet    Microsoft.PowerShell.U... Converts a string containing one or more key and value pairs to a hash ta...
    ConvertTo-Csv                     Cmdlet    Microsoft.PowerShell.U... Converts .NET objects into a series of comma-separated value (CSV) strings.
    ConvertTo-Html                    Cmdlet    Microsoft.PowerShell.U... Converts .NET objects into HTML that can be displayed in a Web browser.
    ...
    ```

3. Any cmdlets redirecting to printer or file?

    `PS C:\Repos\pwsh> Get-Help redirection`
    ```powershell
    TOPIC
        about_Redirection

    SHORT DESCRIPTION
        Explains how to redirect output from Windows PowerShell to text files.

    LONG DESCRIPTION
        By default, Windows PowerShell sends its command output to the Windows
        PowerShell console. However, you can direct the output to a text
        file, and you can redirect error output to the regular output stream.

        You can use the following methods to redirect output:

            - Use the Out-File cmdlet, which sends command output to a text file.

            Typically, you use the Out-File cmdlet when you need to use its
            parameters, such as the Encoding, Force, Width, or NoClobber
            parameters.

            - Use the Tee-Object cmdlet, which sends command output to a text file

            and then sends it to the pipeline.

            - Use the Windows PowerShell redirection operators.

        ...
    ```
... so either **Out-File** or **Tee-Object** depending on the problem?

4. How many cmdlets are there to work with processes?

    `PS C:\Repos\pwsh> get-command -noun process`

    ```powershell
    CommandType     Name                                               Version    Source
    -----------     ----                                               -------    ------
    Cmdlet          Debug-Process                                      3.1.0.0    Microsoft.PowerShell.Management
    Cmdlet          Get-Process                                        3.1.0.0    Microsoft.PowerShell.Management
    Cmdlet          Start-Process                                      3.1.0.0    Microsoft.PowerShell.Management
    Cmdlet          Stop-Process                                       3.1.0.0    Microsoft.PowerShell.Management
    Cmdlet          Wait-Process                                       3.1.0.0    Microsoft.PowerShell.Management
    ```

    ... so 5? Lets check in powershell way:
    `PS C:\Repos\pwsh> (get-command -noun process).Count`

    `5`

5. What cmdlet\(s\) you could use to `Write` an `EventLog`?

    `PS C:\Repos\pwsh> get-command  -verb write -noun eventlog`

    ```powershell
    CommandType     Name                                               Version    Source
    -----------     ----                                               -------    ------
    Cmdlet          Write-EventLog                                     3.1.0.0    Microsoft.PowerShell.Management
    ```

6. What are the commands to create, modify, export or import `aliases`?

    `PS C:\Repos\pwsh> get-command -noun alias`

    ```powershell
    CommandType     Name                                               Version    Source
    -----------     ----                                               -------    ------
    Cmdlet          Export-Alias                                       3.1.0.0    Microsoft.PowerShell.Utility
    Cmdlet          Get-Alias                                          3.1.0.0    Microsoft.PowerShell.Utility
    Cmdlet          Import-Alias                                       3.1.0.0    Microsoft.PowerShell.Utility
    Cmdlet          New-Alias                                          3.1.0.0    Microsoft.PowerShell.Utility
    Cmdlet          Set-Alias                                          3.1.0.0    Microsoft.PowerShell.Utility
    ```

7. Is there a way to `transcript` everything from the shell?

    `PS C:\Repos\pwsh> get-help transcript`

    ```powershell
    Name                              Category  Module                    Synopsis
    ----                              --------  ------                    --------
    Start-Transcript                  Cmdlet    Microsoft.PowerShell.Host Creates a record of all or part of a PowerShell session to a text file.
    Stop-Transcript                   Cmdlet    Microsoft.PowerShell.Host Stops a transcript.
    ```

8. How to limit number of results of `Get-EventLog` in output?


    8.1 Acquintaince the cmdlet first

    `PS C:\Repos\pwsh> (get-command get-eventlog).parameters | where newest`

    ```powershell
    Key                 Value
    ---                 -----
    ComputerName        System.Management.Automation.ParameterMetadata
    Newest              System.Management.Automation.ParameterMetadata
    After               System.Management.Automation.ParameterMetadata
    Before              System.Management.Automation.ParameterMetadata
    UserName            System.Management.Automation.ParameterMetadata
    InstanceId          System.Management.Automation.ParameterMetadata
    Index               System.Management.Automation.ParameterMetadata
    EntryType           System.Management.Automation.ParameterMetadata
    Source              System.Management.Automation.ParameterMetadata
    Message             System.Management.Automation.ParameterMetadata
    AsBaseObject        System.Management.Automation.ParameterMetadata
    List                System.Management.Automation.ParameterMetadata
    AsString            System.Management.Automation.ParameterMetadata
    Verbose             System.Management.Automation.ParameterMetadata
    Debug               System.Management.Automation.ParameterMetadata
    ErrorAction         System.Management.Automation.ParameterMetadata
    WarningAction       System.Management.Automation.ParameterMetadata
    InformationAction   System.Management.Automation.ParameterMetadata
    ErrorVariable       System.Management.Automation.ParameterMetadata
    WarningVariable     System.Management.Automation.ParameterMetadata
    InformationVariable System.Management.Automation.ParameterMetadata
    OutVariable         System.Management.Automation.ParameterMetadata
    OutBuffer           System.Management.Automation.ParameterMetadata
    PipelineVariable    System.Management.Automation.ParameterMetadata
    ```

    8.2 Get help about param `Newest`

    `PS C:\Repos\pwsh> get-help get-eventlog -parameter newest`

    ``` powershell
    -Newest <Int>
        Begins with the newest events and gets the specified number of events. The number of events is required, for example `-Newest 100` . Specifies
        the maximum number of events that are returned.

        Required?                    false
        Position?                    named
        Default value                None
        Accept pipeline input?       False
        Accept wildcard characters?  false
    ```

    8.3 Try to use it

    `PS C:\Repos\pwsh> get-eventlog Security -newest 4`

    ```powershell
    Index Time          EntryType   Source                 InstanceID Message
    ----- ----          ---------   ------                 ---------- -------
    3573373 Jun 14 18:56  SuccessA... Microsoft-Windows...         4672 Special privileges assigned to new logon....
    3573372 Jun 14 18:56  SuccessA... Microsoft-Windows...         4624 An account was successfully logged on....
    3573371 Jun 14 18:56  SuccessA... Microsoft-Windows...         4672 Special privileges assigned to new logon....
    3573370 Jun 14 18:56  SuccessA... Microsoft-Windows...         4624 An account was successfully logged on....
    ```

9. How to get the list of `services` installed on this computer\?

    ```powershell
    PS C:\Repos\pwsh> get-command -noun service

    CommandType     Name                                               Version    Source
    -----------     ----                                               -------    ------
    Cmdlet          Get-Service                                        3.1.0.0    Microsoft.PowerShell.Management
    Cmdlet          New-Service                                        3.1.0.0    Microsoft.PowerShell.Management
    Cmdlet          Restart-Service                                    3.1.0.0    Microsoft.PowerShell.Management
    Cmdlet          Resume-Service                                     3.1.0.0    Microsoft.PowerShell.Management
    Cmdlet          Set-Service                                        3.1.0.0    Microsoft.PowerShell.Management
    Cmdlet          Start-Service                                      3.1.0.0    Microsoft.PowerShell.Management
    Cmdlet          Stop-Service                                       3.1.0.0    Microsoft.PowerShell.Management
    Cmdlet          Suspend-Service                                    3.1.0.0    Microsoft.PowerShell.Management
    ```

    ```powershell
    PS C:\Repos\pwsh> get-service

    Status   Name               DisplayName
    ------   ----               -----------
    Stopped  AarSvc_155789      Agent Activation Runtime_155789
    Stopped  AeXAgentSrvHost    AeXAgentSrvHost
    Running  AeXNSClient        Symantec Management Agent
    ...
    ```

10. How to get list of `processses` running on this computer?

    10.1 Get the command name
    `PS C:\Repos\pwsh> get-command -noun process`

    ```powershell
    CommandType     Name                                               Version    Source
    -----------     ----                                               -------    ------
    Cmdlet          Debug-Process                                      3.1.0.0    Microsoft.PowerShell.Management
    Cmdlet          Get-Process                                        3.1.0.0    Microsoft.PowerShell.Management
    ...
    ```

    10.2 Get the list of processes

    `PS C:\Repos\pwsh> get-process`

    ```powershell
    Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName
    -------  ------    -----      -----     ------     --  -- -----------
        204      17     3716       6164       1.09  12996   2 AeXAgentUIHost
    1157      48    42660       7572   6,846.97  11996   0 AeXNSAgent
    ...
    ```

11.  Find what is the width of file created with `Out-File` by default? What are parameters to customize this?
    
`PS C:\Repos\pwsh> get-help out-file -parameter width`

```powershell
    -Width <Int>
        Specifies the number of characters in each line of output. Any additional characters are truncated, not wrapped. If this parameter is not
        used, the width is determined by the characteristics of the host. The default for the PowerShell console is 80 characters.
```

... so, 80?

12. What is parameter disabling the overwrite of existing file when using `Out-File` ?

    ```powershell
    (get-help out-file).Parameters
    ...
    -NoClobber [<SwitchParameter>]
            NoClobber prevents an existing file from being overwritten and displays a message that the file already exists. By default, if a file
            exists in the specified path, `Out-File` overwrites the file without warning.

            Required?                    false
            Position?                    named
            Default value                False
            Accept pipeline input?       False
            Accept wildcard characters?  false
    ...
    ```

13. How to make a list of all existing `aliases` in the system?

    ``` powershell
    PS C:\Repos\pwsh> Get-Alias

    CommandType     Name                                               Version    Source
    -----------     ----                                               -------    ------
    Alias           % -> ForEach-Object
    Alias           ? -> Where-Object
    Alias           ac -> Add-Content
    ...
    ```

14. Using aliases get list of processes running

    ``` powershell
    PS C:\Repos\pwsh> ps -c localhost

    Handles  NPM(K)    PM(K)      WS(K)     CPU(s)     Id  SI ProcessName
    -------  ------    -----      -----     ------     --  -- -----------
        204      18     3760       6200             12996   0 AeXAgentUIHost
    1157      48    42784       7820             11996   0 AeXNSAgent
        299      22    28412      16136              3892   0 AotListener
    ...
    ```

15. How many cmdlets can deal with common objects?

    ```PS C:\Repos\pwsh> get-command -noun object

    CommandType     Name                                               Version    Source
    -----------     ----                                               -------    ------
    Cmdlet          Compare-Object                                     3.1.0.0    Microsoft. PowerShell. Utility
    Cmdlet          ForEach-Object                                     3.0.0.0    Microsoft. PowerShell. Core
    Cmdlet          Group-Object                                       3.1.0.0    Microsoft. PowerShell. Utility
    Cmdlet          Measure-Object                                     3.1.0.0    Microsoft. PowerShell. Utility
    Cmdlet          New-Object                                         3.1.0.0    Microsoft. PowerShell. Utility
    Cmdlet          Select-Object                                      3.1.0.0    Microsoft. PowerShell. Utility
    Cmdlet          Sort-Object                                        3.1.0.0    Microsoft. PowerShell. Utility
    Cmdlet          Tee-Object                                         3.1.0.0    Microsoft. PowerShell. Utility
    Cmdlet          Where-Object                                       3.0.0.0    Microsoft. PowerShell. Core

    PS C:\Repos\pwsh> (get-command -noun object). Count
    9

    ```

16. Where to find info about arrays?

    ```powershell
    PS C:\Repos\pwsh> get-help arrays
    TOPIC
        about_Arrays

    SHORT DESCRIPTION
        Describes arrays, which are data structures designed to store
        collections of items.

    LONG DESCRIPTION
        An array is a data structure that is designed to store a collection
        of items. The items can be the same type or different types.

        Beginning in Windows PowerShell 3.0, a collection of zero or one
        object has some properties of arrays.
    ```
