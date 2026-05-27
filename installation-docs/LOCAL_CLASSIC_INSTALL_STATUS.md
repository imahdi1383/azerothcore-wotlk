# Local AzerothCore Classic Installation Status

Date: 2026-05-27

## Completed

- Configured CMake build in `C:/Build`.
- Built AzerothCore with `RelWithDebInfo`.
- Copied required runtime DLLs next to the server binaries:
  - `libmysql.dll`
  - `legacy.dll`
  - `libcrypto-3-x64.dll`
  - `libssl-3-x64.dll`
- Created runtime config files from `.dist` files:
  - `C:/Build/bin/RelWithDebInfo/configs/authserver.conf`
  - `C:/Build/bin/RelWithDebInfo/configs/worldserver.conf`
  - `C:/Build/bin/RelWithDebInfo/configs/dbimport.conf`
- Downloaded and extracted official AC Data v19 enUS to:
  - `C:/Build/bin/RelWithDebInfo/Data`
- Set `DataDir` in `worldserver.conf` to:
  - `C:/Build/bin/RelWithDebInfo/Data`
- Created MySQL user/databases with AzerothCore defaults:
  - user: `acore`
  - password: `acore`
  - databases: `acore_auth`, `acore_characters`, `acore_world`
- Populated and updated databases with `dbimport.exe`.
- Verified server startup:
  - `authserver.exe` listened on port `3724`.
  - `worldserver.exe` listened on port `8085`.
  - `worldserver.exe` reached the `AC>` console prompt.

## Run Server

Open one PowerShell window:

```powershell
cd C:/Build/bin/RelWithDebInfo
./authserver.exe
```

Open a second PowerShell window:

```powershell
cd C:/Build/bin/RelWithDebInfo
./worldserver.exe
```

Create a test account in the `worldserver.exe` console:

```text
account create USERNAME PASSWORD
account set gmlevel USERNAME 3 -1
```

## Client Requirement

AzerothCore is only the server. A separate World of Warcraft 3.3.5a client is required to play.

After installing or extracting the client, find `Wow.exe` in the client folder and set the client realmlist file to:

```text
set realmlist 127.0.0.1
```

The realmlist file is commonly located in one of these paths inside the WoW client folder:

- `Data/realmlist.wtf`
- `Data/enUS/realmlist.wtf`
- `Data/enGB/realmlist.wtf`

Then run `Wow.exe` and log in with the account created in `worldserver.exe`.
