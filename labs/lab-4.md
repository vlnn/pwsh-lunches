# Lab 4 - running commands

1. Display a list of running processes

    `Get-Process`

2. Display the 100 most recent entries from the Application event log.

    `Get-EventLog -LogName Application -Newest 100`

3. Display the list of all commands that are of the cmdlet type.

    `Get-Command -CommandType Cmdlet`

4. Display a list of all aliases.

    `Get-Alias`

5. Make a new alias for launching notepad from powershell prompt.

    `Set-Alias -Name nd -Value "notepad.exe"`

6. Display a list of services that begin with the letter **M**.

    `Get-Service -Name M*`

7. Display a list of all Windows Firewall rules.

    `help Get-*Firew*`

    ```
    Name                              Category  Module                    Synopsis
    ----                              --------  ------                    --------
    Get-NetFirewallAddressFilter      Function  NetSecurity               Retrieves address filter objects from the target computer.
    Get-NetFirewallApplicationFilter  Function  NetSecurity               Retrieves application filter objects from the target computer.
    Get-NetFirewallInterfaceFilter    Function  NetSecurity               Retrieves interface filter objects from the target computer.
    Get-NetFirewallInterfaceTypeFi... Function  NetSecurity               Retrieves interface type filter objects from the target computer.
    Get-NetFirewallPortFilter         Function  NetSecurity               Retrieves port filter objects from the target computer.
    Get-NetFirewallProfile            Function  NetSecurity               Displays settings that apply to the per-profile configurations of the Windows Firewall with Adv...
    Get-NetFirewallRule               Function  NetSecurity               Retrieves firewall rules from the target computer.
    ...
    ```

    `Get-NetFirewallRule`

8. Display a list of just **inbound** Windows Firewall rules.
    `help Get-NetFirewallRule`
    (see the `-Direction` param there)
    `Get-NetFirewallRule -Direction Inbound`
