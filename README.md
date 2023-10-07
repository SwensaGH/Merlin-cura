![N|Solid](http://www.merlinautomationsolutions.com/images/merlin_l0g0_bk.png)

# Building, Testing, Releasing
```sh
delete ~/.conan 
delete c:\.conon
delete ~/AppDir/local/Uranium*,cura*,Merlin*
delete ~AppData\Roaming/Uranium*,cura*,Merlin*
```

## Install Conan
```sh
pip install conan --upgrade
conan config install https://github.com/ultimaker/conan-config.git
conan profile new default --detect --force
```
## Clone Merlin-Uranium
```sh
git clone https://github.com/SwensaGH/Merlin-Uranium
cd Uranium
```
### For development 
```sh
conan editable add . uranium/latest@sai/sai
```
### For production release
```sh
conan create . uranium/latest@sai/sai --build=missing --update
```
## Clone Merlin-Cura
```sh
git clone https://github.com/SwensaGH/Merlin-cura
cd Cura
```
### For development 
One time to setup Virtual Environment. You can delete venv directory and rerun to generate the venv directory<br>   
update the following packages to 5.2.2 to 5.3.0 (to latest in the future ) - conandata.yml <br>   
Also make sure you have the requirements for building curaengine - https://github.com/Ultimaker/CuraEngine/wiki/Building-CuraEngine-From-Source<br>   
This step builds the curaengine.exe <br>   
```sh
conan install . --build=missing --update -o cura:devtools=True -g VirtualPythonEnv
```

### For production release
```sh
conan create . cura/latest@sai/sai --build=missing --update
conan install cura/latest@sai/sai --build=missing --update -if cura_inst -g VirtualPythonEnv -o cura:devtools=True --json "cura_inst/conan_install_info.json"
.\cura_inst\Scripts\Activate.ps1
pyinstaller .\cura_inst\Ultimaker-Cura.spec
py .\cura_inst\packaging\NSIS\create_windows_installer.py D:\ultimaker\Cura D:\ultimaker\Cura\dist swensa-cura.exe
```
## Run Cura
```sh
venv\scripts\Activate.bat
python cura_app.py
```
 

