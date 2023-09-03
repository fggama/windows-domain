# Windows Domain Controller y Active Directory

## DNS 

Para Windows 10 ver _Remote Server Admin Tools_ (RSAT)

>``ipconfig /displaydns  ``  
>``Get-DnsServer -Computername "213.169.1.105"``  
>``nslookup  ``  
>``[System.Net.Dns]::GetHostEntry('example.com').AddressList.IPAddressToString``  
>``dsquery server -limit 0``  
>``Resolve-DnsName example.com``  
>``Test-Connection 10.0.100.60``

### Obtener información  
``Get-DnsServerForwarder -computer 10.0.0.50``
``Get-DnsServerZone -computername 10.0.0.50``

## Información en Active Directory
>``Get-ADComputer -Filter * | Select-Object DNSHostName, @{name="Ip";Expression={(Test-Connection $_.DNSHostname -Count 1).IPV4Address.IPAddressToString}}``  
>``Get-ADComputer -Identity "SRV-ADN" -Properties *``  
>``Get-ADComputer -Filter 'Name -like "User01*"' -Properties IPv4Address | FT Name,DNSHostName,IPv4Address -A``  
>``Get-ADComputer -LDAPFilter "(name=*laptop*)" -SearchBase "CN=Computers,DC= User01,DC=com"``  

### Lista de equipos aplicando filtro
>``Get-ADComputer -Filter *``

### Propiedades de un objeto ADComputer
>``Get-ADComputer<computer>-Properties ALL | Get-Member``

### Información del Dominio
>``Get-ADDomain``  
>``Get-ADDomain -Identity example.com``

### Información del Domain Controller
>````nltest /dclist:example.com````  
>````nltest /dsgetdc:example /force /gc````

>``Get-ADDomainController -Discover``  
>``Get-ADDomainController -Discover -Domain "user01.com"``  
>``Get-ADDomainController -Discover -Site "Default-First-Site-Name"``  
>``Get-ADDomainController -Discover -Site "Default-First-Site-Name" -ForceDiscover``  
>``Get-ADDomainController -Identity "TK5-CORP-DC-10.user01.com" -Server "user01.com" -Credential "corp\administrator"``  

### Sincronización
>````
>Sync-ADObject -Object "DC=example,DC=com" -Source "SRV-ADA" -Destination "SRV-ADX"
>````

>````
>repadmin /syncall
>````
