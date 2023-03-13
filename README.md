conan config install https://github.com/ultimaker/conan-config.git 


Uranium
-------------------------------------------------------------------------------------
---dev---
conan editable add . uranium/latest@sai/sai

--prod---
conan create . uranium/latest@sai/sai --build=missing --update


cura
-------------------------------------------------------------------------------------
--dev--
conan install . --build=missing --update -o cura:devtools=True -g VirtualPythonEnv



--prod--
conan create . cura/latest@sai/sai --build=missing --update

conan install cura/latest@sai/sai --build=missing --update -if cura_inst -g VirtualPythonEnv -o cura:devtools=True --json "cura_inst/conan_install_info.json"

.\cura_inst\Scripts\Activate.ps1

pyinstaller .\cura_inst\Ultimaker-Cura.spec

py .\cura_inst\packaging\NSIS\create_windows_installer.py D:\ultimaker\Cura D:\ultimaker\Cura\dist swensa-cura.exe


