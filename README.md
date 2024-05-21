## ProxyBack Audio Driver

A HAL virtual audio driver for macOS that sends all output to another audio device, and provides a hidden audio device to listen to audio output. Enabling a configurable virtual interface, where a client can change the audio output device (i.e. your speakers or headphones), and giving the client the ability to listen to that Audio Data.

### Installation

#### Manual installation

1. Download the latest release from this GitHub repository

2. Create the directory `HAL` if it does not exist. Open a terminal window, execute the following command and enter your administrator password when prompted:

        sudo mkdir /Library/Audio/Plug-Ins/HAL

3. Move the directory `ProxyAudioDriver.driver` to `/Library/Audio/Plug-Ins/HAL` and assign it the correct owner. Execute in the root directory of the unzipped file:

        sudo mv ./ProxyAudioDevice.driver /Library/Audio/Plug-Ins/HAL/
        sudo chown -R root:wheel /Library/Audio/Plug-Ins/HAL/ProxyAudioDevice.driver

4. Either reboot your system or reboot Core Audio by executing the following command:

        sudo launchctl kickstart -k system/com.apple.audio.coreaudiod

5. Run Proxy Audio Device Settings to configure the proxy output device's name, which output device the driver will proxy to, and how large you want its audio buffer to be.

### Building

Clone the repo, open the Xcode project and build the driver and the settings application. Then follow the above installation instructions to install it.


### Issues

If you make the audio buffer too small then the driver will introduce pops, crackles, or distortion. If you notice that then try increasing the buffer size.


### Possible Future Work

- Indicator in the settings app for when the proxy audio device overruns its buffer and causes audio artifacts
- Proxying more than two channels of audio
- Ability to increase the number of proxy devices
