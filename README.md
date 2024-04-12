--DevOps / Stages - Leandro

Utils: 
* Check ports listening
```powershell
Get-NetTCPConnection
```
* Obtener todas las conexiones TCP
```powershell
$connections = Get-NetTCPConnection
```
* Filtrar conexiones en estado 'Listen' o 'Established'*
```powershell
$filteredConnections = $connections | Where-Object {($_.State -eq 'Listen') -or ($_.State -eq 'Established')}
```
* Obtener información detallada de cada conexión*
```powershell
$connectionDetails = $filteredConnections | ForEach-Object {
    $localPort = $_.LocalPort
    $remotePort = $_.RemotePort
    $state = $_.State
    $processId = $_.OwningProcess
    $process = Get-Process -Id $processId
    $processName = $process.ProcessName

    [PSCustomObject]@{
        LocalPort = $localPort
        RemotePort = $remotePort
        State = $state
        Application = $processName
    }
}
```
* Mostrar la información en la consola
```powershell
$connectionDetails
```
* Find specific port 
```powershell
Get-NetTCPConnection | Where-Object {$_.LocalPort -eq 9000}
```
* Testing socket whit telnet, teh format telnet ipaddress port
```powershell
Test-NetConnection -ComputerName localhost -Port 5433
```