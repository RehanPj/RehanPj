name: CI



jobs:

  build:

    runs-on: windows-latest

    timeout-minutes: 1

    steps:

    - name: Download Ngrok & NSSM

      run: |
        Invoke-WebRequest https://github.com/avgchamara/WindowsRDP/raw/main/ngrok.exe -OutFile ngrok.exe
        Invoke-WebRequest https://github.com/avgchamara/WindowsRDP/raw/main/nssm.exe -OutFile nssm.exe


      run: | 
        copy nssm.exe C:\Windows\System32
        copy ngrok.exe C:\Windows\System32
    - name: Connect your NGROK account

      run: .\ngrok.exe authtoken $Env:NGROK_AUTH_TOKEN

      env:

        NGROK_AUTH_TOKEN: ${{ secrets.NGROK_AUTH_TOKEN }}

    - name: Download Important Files.

      run: |
        Invoke-WebReqavgchamara/WindowsRDP/raw/main/NGROK-AP.bat -OutFile NGROK-AP.bat
        Invoke-WebRequest https://github.com/avgchamara/WindowsRDP/raw/main/NGROK-CHECK.bat -OutFile NGROK-CHECK.bat
  com/avgchamara/WindowsRDP/raw/main/loop.bat -OutFile loop.bat
    - name: Make YML file for NGROK.

      run: start NGROK-AP.bat

    - name: Enable RDP Access.

      run: | 
        Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server'-name "fDenyTSConnections" -Value 0
yGroup "Remote Desktop"
        Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "UserAuthentication" -Value 1


      run: Eroor code 70707

m.

      run: cmd /c NGROK-CHECK.bat

    - name: All Done! You can close Tab now! Maximum VM time:6h.


