# Knock-CMake

Knock-CMake is a project that allows the compilation of Knock using CMake on any Linux OS (or Windows WSL) with various processor architectures. 

Knock can Convert ACSM files to PDF/EPUBs with one command on Linux.

*This software does not utilize Adobe Digital Editions nor Wine. It is completely free and open-source software written natively for Linux.*

This is a special build script for knock utilizing CMake instead of Nix for better compability. You can find the original knock repository here: [https://github.com/BentonEdmondson/knock](https://github.com/BentonEdmondson/knock). Special thanks to Benton Edmondson and all the other knock contributors.

**As of Febebury 8th, 2025. The upstream knock repo is currently offline, the build scripts provided here is configured to use a [fork of knock](https://github.com/Alvin-He/knock-cmake/tree/knock-base-release-79).**
<sub><sup>All links in this readme referencing the upstream knock repo will be unusuable because of this, unfortunately.</sup></sub>

## Installation

NOTE: For x86-64 users, you may simply go to the [knock repository's release page](https://github.com/BentonEdmondson/knock/releases) to download a binary. The binary published by the upstream knock repository does not require any of the runtime dependencies here.

1. Get to [releases](https://github.com/Alvin-He/knock-cmake/releases) to get the latest release or clone this repo for the most up to date code.
    - *if older knock releases is needed, this repository's release version numbers should match up with the [upstream Knock repository's release page.](https://github.com/BentonEdmondson/knock/releases)*
2. Navigate to the folder that `knock-cmake` is installed in
3. If `apt` is your OS's package manager, then you may simply run `sudo python3 build.py` to build and install knock-cmake (this will take some time) 
    - if you are not using `apt`, then to go to [Dependencies](#dependencies) and install those manually using your package manager of choice, then run `python3 build.py` as normal
    - the error messages will provide you enough details to resolve any problems with installation, if not, create an [issue](https://github.com/Alvin-He/knock-cmake/issues/new)
    - if for some reason python3 can't be used, open `build.py`, go to the end of the file, and follow instructions there. 
4. `build.py` will generate the knock binary in `<knock-cmake download folder>/knock`. `cd`/navigate to that folder.
5. Then run `./knock ./path/to/book.acsm` to perform the conversion.
6. To clean up, move the knock binary to some other location, ex: your home directory or `~/`. ***MAKE SURE YOU HAVE MOVED THE KNOCK BINARY***; then run `sudo rm -r knock-cmake` to remove all the build artifacts. 
7. Optional: move the knock binary to `/usr/local/bin` if you want to be able to run knock from anywhere.

## Dependencies

Knock-cmake requires `libssl-dev, libcurl4-openssl-dev, zlib1g-dev, git, cmake, build-essential`(gcc, g++, etc.) in order to be built.

The then compiled binary needs libcurl, libopenssl and zlib as run time dependencies if you are planning to deploy it somewhere.

**NOTE: the version of knock published by the [upstream knock repository](https://github.com/BentonEdmondson/knock/) will run with out these dependencies, but this version of knock built by knock-cmake will NOT!**

## Contributing

If you have anything to add or want to optimize any of my cmake scripts, feel free to do so and open a pull request. 

There are no particular formatting guides, just if your code is not self-explanatory, add comments.

## License

This repository is licensed under GPLv3. Knock is also licensed under GPLv3. The linked libraries have various licenses.

## Motivation
Knock have always been my go to converter when I need to convert acsm ebook files to epub for easier reading and portability. Knock is great at this, but it is very inconvenient to have to start my linux machine every time I need to convert an ebook (My linux laptop isn't my main computer). Due to my unmatched laziness, I decided to make a web interface for knock so I don't have to always bother my self. However, the upstream knock repo only published a x86-64 kernel and wouldn't you know it, most web server are arm64.... :(. Soooooooo, why not make some cmake build files for knock. Wouldn't be too hard. Right? 

NO. I proceeded to take 4 days of my life making these for knock and the library it uses, [libgourou](https://forge.soutade.fr/soutade/libgourou) (also had to make libgourou's dependency [uPDFParser](https://forge.soutade.fr/soutade/uPDFParser) a cmake script too) (These 2 are very good libraries made by [soutade](https://forge.soutade.fr/soutade/), check them out!). Anyways, now that the CMake scripts exist, I will finally be able to make that web interface. I know there are web acsm to epub converters that exist already, but the ones I can find all seem broken. So when ever I finishes, I guess I will update here. 

I'll try my best to keep up with the upstream repo's updates. If you need an update before I update this repo for some reason, then just change the tags and commit hashes in get_git_repo calls in build.py for newer ones.  

If you need cmake scripts for libgourou or cmake scripts for uPDFParser, you can just download the scripts in /config. They should work standalone. 

