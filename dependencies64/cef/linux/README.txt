Chromium Embedded Framework (CEF) Minimal Binary Distribution for Linux
-------------------------------------------------------------------------------

Date:             January 21, 2022

CEF Version:      95.0.0-MediaHandler.2464+gb58eaf2+chromium-95.0.4638.69
CEF URL:          https://bitbucket.org/chromiumembedded/cef.git
                  @b58eaf2ac4e74d1a27127aa59b86433d6185e6d0

Chromium Version: 95.0.4638.69
Chromium URL:     https://chromium.googlesource.com/chromium/src.git
                  @66a46a9e6b68454d656207831ca3a6eb7332c7a4

This distribution contains the minimial components necessary to build and
distribute an application using CEF on the Linux platform. Please see
the LICENSING section of this document for licensing terms and conditions.


CONTENTS
--------

cmake       Contains CMake configuration files shared by all targets.

include     Contains all required CEF header files.

libcef_dll  Contains the source code for the libcef_dll_wrapper static library
            that all applications using the CEF C++ API must link against.

Release     Contains libcef.so and other components required to run the release
            version of CEF-based applications. By default these files should be
            placed in the same directory as the executable.

Resources   Contains resources required by libcef.so. By default these files
            should be placed in the same directory as libcef.so.


USAGE
-----

Building using CMake:
  CMake can be used to generate project files in many different formats. See
  usage instructions at the top of the CMakeLists.txt file.

Please visit the CEF Website for additional usage information.

https://bitbucket.org/chromiumembedded/cef/


REDISTRIBUTION
--------------

This binary distribution contains the below components.

Required components:

The following components are required. CEF will not function without them.

* CEF core library.
  * libcef.so

* Unicode support data.
  * icudtl.dat

* V8 snapshot data.
  * snapshot_blob.bin
  * v8_context_snapshot.bin

Optional components:

The following components are optional. If they are missing CEF will continue to
run but any related functionality may become broken or disabled.

* Localized resources.
  Locale file loading can be disabled completely using
  CefSettings.pack_loading_disabled. The locales directory path can be
  customized using CefSettings.locales_dir_path. 
 
  * locales/
    Directory containing localized resources used by CEF, Chromium and Blink. A
    .pak file is loaded from this directory based on the value of environment
    variables which are read with the following precedence order: LANGUAGE,
    LC_ALL, LC_MESSAGES and LANG. Only configured locales need to be
    distributed. If no locale is configured the default locale of "en-US" will
    be used. Without these files arbitrary Web components may display
    incorrectly.

* Other resources.
  Pack file loading can be disabled completely using
  CefSettings.pack_loading_disabled. The resources directory path can be
  customized using CefSettings.resources_dir_path.

  * chrome_100_percent.pak
  * chrome_200_percent.pak
  * resources.pak
    These files contain non-localized resources used by CEF, Chromium and Blink.
    Without these files arbitrary Web components may display incorrectly.

* ANGLE support.
  * libEGL.so
  * libGLESv2.so
  Support for rendering of HTML5 content like 2D canvas, 3D CSS and WebGL.
  Without these files the aforementioned capabilities may fail.

* SwANGLE support.
  * libvk_swiftshader.so
  * libvulkan.so.1
  * vk_swiftshader_icd.json
  Support for software rendering of HTML5 content like 2D canvas, 3D CSS and
  WebGL using SwiftShader's Vulkan library as ANGLE's Vulkan backend. Without
  these files the aforementioned capabilities may fail when GPU acceleration is
  disabled or unavailable.

* SwiftShader support
  * swiftshader/libEGL.so
  * swiftshader/libGLESv2.so
  Deprecated support for software rendering using SwiftShader's GL libraries.
  Used as an alternative to SwANGLE when the `--use-gl=swiftshader-webgl`
  command-line flag is specified.


LICENSING
---------

The CEF project is BSD licensed. Please read the LICENSE.txt file included with
this binary distribution for licensing terms and conditions. Other software
included in this distribution is provided under other licenses. Please visit
"about:credits" in a CEF-based application for complete Chromium and third-party
licensing information.
