# win2012_in-place_upgrade
windows 2012 in-place upgrade to 2016 or 2019


# win2012_in-place_upgrade

### Background:

This will guide you in-place unattend upgrade from windows 2012 to 2016 or 2019 with simple .ini file without creating unattend.xml or autounattend.xml file

### NOTE: 

Please have tested in your Dev, Stage environment before you plan for your Production upgrade.

### Using command line or powershell:

### step 1: Create setupconfig.ini file

    [SetupConfig]
    Quiet
    Auto=Upgrade
    ImageIndex=2
    telemetry=disable
    dynamicupdate=disable
    compat=IgnoreWarning
    copylogs=C:\temp\win_upgrade_logs

### step 2: command or powershell to execute the setup:

    cmd:
        <windows_2016_or_2019_source>\setup.exe /ConfigFile <setupconfig.ini>
    
    setup.cmd
        start /wait c:\windows_2016_or_2019_source\setup.exe /ConfigFile <setupconfig.ini>

    powershell:
        $setup = "c:\windows_2016_or_2019_source\setup.exe"
        $param = "/ConfigFile c:\windows_2016_or_2019_source\setupconfig.ini"
        Start-process -FilePath $setup -Argumentlist $param

### Using command line or powershell:

If you are using chef to upgrade, use try this:

        windows_package('Windows_upgrade_2019') do
            action :install
            source 'c:\windows_2016_or_2019_source\setup.exe'
            installer_type :custom
            options '/ConfigFile c:\windows_2016_or_2019_source\setupconfig.ini'
            timeout 3600
        end

## Contributors :

    - Author:: Prabu Jaganathan ((mailto:jaganp.architect@gmail.com))

```text

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```