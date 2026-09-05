# Energy Keeper

## Run on macOS

```sh
npm run start
```

## Build on Windows

Install SFML 3 (for example with vcpkg), then run this in PowerShell:

```powershell
cmake -S . -B build -DCMAKE_TOOLCHAIN_FILE=C:/vcpkg/scripts/buildsystems/vcpkg.cmake
cmake --build build --config Release
.\build\Release\EnergyKeeper.exe
```

The project uses SFML's cross-platform window layer, which uses the native Windows window system when built on Windows.

Sound effects are read from `sounds/`. The game checks those `.wav` files continuously while the window is open and temporarily disables any missing effect until its file appears again. Background music is selected randomly from `.wav` files in `Musics/` only; press `M` to mute or unmute all audio.

The `GENERATOR SPEED` button upgrades automatic energy production: level 1 requires level 11 and 30,000 Energy for a 0.5-second interval, level 2 requires level 26 and 50,000 Energy for 0.25 seconds, and level 3 requires level 31 and 100,000 Energy for 0.1 seconds.

The game automatically loads and saves progress in `energy_keeper.db` beside the executable. The file is binary-encoded and checksum-protected; edited or corrupted data is rejected. Local offline saves cannot be made fully tamper-proof because the game and its validation code are also on the player's machine.

## Build Windows x64 `.exe` from macOS

This requires MinGW-w64 and a Windows-targeted SFML 3 build. The output is a Windows 64-bit GUI executable:

```sh
cmake -S . -B build-win64 \
  -DCMAKE_TOOLCHAIN_FILE=path/to/mingw64-toolchain.cmake \
  -DCMAKE_PREFIX_PATH=path/to/sfml-win64 \
  -DENERGY_KEEPER_STATIC_SFML=ON \
  -DCMAKE_BUILD_TYPE=Release
cmake --build build-win64
```

Copy `EnergyKeeper.exe` together with `assets/`, `NotoSansThai.ttf`, and the three `.wav` files before running it on Windows.

## Assets

The button icons in `assets/` come from the Kenney Icon Font project and are licensed CC0.
The UI font is Noto Sans Thai, licensed under SIL Open Font License 1.1; its license is included as `NotoSansThai-OFL.txt`.
