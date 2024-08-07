CasparCG Server (Sofie-specific fork of CasparCG Server)
===============

Thank you for your interest in CasparCG Server, a professional software used to
play out and record professional graphics, audio and video to multiple outputs.
CasparCG Server has been in 24/7 broadcast production since 2006.

The CasparCG Server works on Windows and Linux.

System Requirements
-------------------

- A graphics card (GPU) capable of OpenGL 4.5 is required.
- An Nvidia GPU is recommended, but other GPU's will likely work fine.
- Only Intel CPU's have been tested and are known to work

### Windows

 - Only Windows 10 is supported

### Linux

 - Ubuntu 22.04 are supported

Getting Started
---------------

1. Download a release from (http://casparcg.com/downloads).
   Alternatively, newer testing versions can be downloaded from (http://builds.casparcg.com) or [built from source](BUILDING.md)

2. Install any optional non-GPL modules

3. Configure the server by editing the self-documented "casparcg.config" file in a text editor.

4.
   1. Windows: start `casparcg_auto_restart.bat`, or `casparcg.exe` and `scanner.exe` separately.
   1. Linux: start the `run.sh` program or use tools/linux/start_docker.sh to run within docker (documentation is at the top of the file).

5. Connect to the Server from a client software, such as the "CasparCG Client"
   which is available as a separate download.

Documentation
-------------

The most up-to-date documentation is always available at
https://github.com/CasparCG/help/wiki

Ask questions in the forum: https://casparcgforum.org/

Resolving Common Issues On Linux
--------------------------------

Common problems you may encounter when running on newer and unsupported
Ubuntu editions:

1. HTML producer freezes and/or throws "Fontconfig error" message
Add below line to run.sh script:
export FONTCONFIG_PATH=/etc/fonts

2. HTML producer throws "GTK theme error" message
Install gnome-themes-standard package:
sudo apt install gnome-themes-standard

4. Error while loading libcgmanager.so.0
Install central cgroup manager daemon (client library):
sudo apt install libcgmanager0

5. Error while loading shared libraries: libgconf-2.so.4
Install GNOME configuration database system:
sudo apt -y install libgconf2-4

6. lib/libz.so.1: version `ZLIB_1.2.9' not found
cd your_casparcg_directory/lib/
sudo mv libz.so.1 libz.so.1.old
sudo ln -s /lib/x86_64-linux-gnu/libz.so.1

Development
-----------

See [BUILDING](BUILDING.md) for instructions on how to build the CasparCG Server from source manually.

License
---------

CasparCG Server is distributed under the GNU General Public License GPLv3 or
higher, see [LICENSE](LICENSE) for details.

CasparCG Server uses the following third party libraries:
- FFmpeg (http://ffmpeg.org/) under the GPLv2 Licence.
  FFmpeg is a trademark of Fabrice Bellard, originator of the FFmpeg project.
- Threading Building Blocks (http://www.threadingbuildingblocks.org/) library under the GPLv2 Licence.
- FreeImage (http://freeimage.sourceforge.net/) under the GPLv2 License.
- SFML (http://www.sfml-dev.org/) under the zlib/libpng License.
- GLEW (http://glew.sourceforge.net) under the modified BSD License.
- boost (http://www.boost.org/) under the Boost Software License, version 1.0.
