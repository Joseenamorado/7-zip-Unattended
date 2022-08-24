<# 7-zip-Unattended
Install unattended  from powershell by Jose R.
#>

$uri = 'https://d3.7-zip.org/a/7z2201-x64.exe'
$out= "C:\7z2201-x64.exe"
Invoke-WebRequest -uri $uri -OutFile $out

#localiza la ruta en donde se encuentra archivo de desinstalacion
#locate the path where the uninstall file is located

$validatepath = Test-Path "C:\Program Files (x86)\7-Zip"
$validatepath2 = Test-Path "C:\Program Files\7-Zip"


if
($validatepath -eq $true){
#desintalación si encuentra la ubicacion C:\Program Files
#uninstall if it finds the location C:\Program Files
Start-Process "C:\Program Files (x86)\7-Zip\Uninstall.exe" -ArgumentList "/s"
Start-Sleep -s 60
}
elseif
($validatepath2 -eq $true){
#desintalación si encuentra la ubicacion C:\Program Files (x86)
#uninstall if it finds the location C:\Program Files (x86)
Start-Process "C:\Program Files\7-Zip\Uninstall.exe" -ArgumentList "/S"
Start-Sleep -s 60
}

#instalacion 7zip
#install 7zip
Start-Process -FilePath "C:\7z2201-x64.exe" -ArgumentList "/S"

Sleep -Seconds 30
Remove-Item "C:\7z2201-x64.exe"
