# Lab 5 - working with providers

1. In the Registry locate the DontPrettyPath property under HKEY_CURRENT_USER\software\microsoft\Windows\CurrentVersion\explorer\Advanced.

    `Set-ItemProperty -Path HKCU:\software\microsoft\Windows\CurrentVersion\Explorer\Advanced -PSProperty DontPrettyPath -Value 1`

2. Create a new directory called `c:\Labs`.

    `New-Item -Path c:\Labs -Type Directory` or just `mkdir c:\Labs`.

3. Create a zero-length file named `c:\Labs\test.txt`.

    `New-Item -Path c:\Labs\test.txt -Type File`

4. Is it possible to use `Set-Item` to change the contents of `C:\Labs\test.txt` to `TESTING`? Or do you get an error? If you get an error, why?
                                                         
    ```powershell 
    PS C:\> set-item -Value "TESTING" -Path C:\Labs\test.txt
    set-item : Provider operation stopped because the provider 
    does not support this operation.
    ```

    No, provider isn't made to do it.

5. Using the Environment provider, display the value of the system environment variable `%TEMP%`.

    `Get-Item -Path env:TEMP`


6. What is the difference between the `-Filter`, `-Include` and `-Exclude` parameters of `Get-ChildItem`?

    `Get-Help Get-ChildItem -Parameter Filter`
    `Get-Help Get-ChildItem -Parameter Include`
    `Get-Help Get-ChildItem -Parameter Exclude`

`-Filter` specifies a filter to qualify the Path parameter.
`-Include` specifies, as a string array, an item or items that this cmdlet includes in the operation.
`-Exclude` specifies, as a string array, a property or property that this cmdlet excludes from the operation.