SteamVR Plugin for OpenHMD Drivers

Build with cmake:

    git clone --recursive https://github.com/ChristophHaag/SteamVR-OpenHMD.git
    cd SteamVR-OpenHMD
    mkdir build
    cd build
    cmake ..
    make

OpenHMD is included as a git submodule. An OpenHMD shared library will be built first and the steamvr plugin will link to this OpenHMD build first. If you want to package the SteamVR plugin, make sure you have libopenhmd.so in your library search path or package the openhmd library too and change the rpath.

Run:
First register the driver with SteamVR:

    ~/.local/share/Steam/SteamApps/common/SteamVR/bin/linux64/vrpathreg adddriver ~/SteamVR-OpenHMD/build

The directory given to vrpathreg should contain `driver.vrdrivermanifest` and `bin/linux64/driver_openhmd.so` as a subdirectory.

Then copy the steamvr.vrsettings file that disables the lighthouse and oculus default driver into Steam's config directory.

    cp ~/SteamVR-OpenHMD/steamvr/steamvr.vrsettings ~/.local/share/Steam/config/steamvr.vrsettings

Don't forget to make a backup if you have special SteamVR settings. Now run SteamVR and check ~/.local/share/Steam/logs/vrserver.txt for errors.

TODO:
* implement controllers when openhmd controller api https://github.com/OpenHMD/OpenHMD/pull/93 is merged
* Perspective/eye separation. Possibly only GetProjectionRaw needs to be fixed: https://github.com/ValveSoftware/openvr/wiki/IVRSystem::GetProjectionRaw. SteamVR-OSVR does https://github.com/OSVR/SteamVR-OSVR/blob/52bd105d7175d1750e00344f41e12cc7cf76d188/src/OSVRTrackedHMD.cpp#L241
