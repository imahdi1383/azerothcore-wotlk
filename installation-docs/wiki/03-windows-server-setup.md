<!--
This file is a copy of (https://www.azerothcore.org/wiki/windows-server-setup)
-->

Windows Server Setup
====================

| Installation Guide |  |
| --- | --- |
| This article is a part of the Installation Guide. You can read it alone or click the previous link to easily move between the steps. |  |
| [<< Step 2: Core Installation](windows-core-installation) | [Step 4: Database Installation >>](database-installation) |

**Table of contents**

- [Windows Server Setup](#windows-server-setup)
  - [Option 1: Download Pre-Extracted Files](#option-1-download-pre-extracted-files)
  - [Option 2: Extract Files Yourself](#option-2-extract-files-yourself)
  - [Config Files: Worldserver and Authserver](#config-files-worldserver-and-authserver)
    - [Updating DataDir](#updating-datadir)
    - [(Optional) Config options by environment variable](#optional-config-options-by-environment-variable)
  - [Help](#help)

Now that you have the source compiled, you need to add the necessary client data. You can either download pre-extracted files or use the compiled extractors to extract the files yourself. Once the data is ready, you must update the **DataDir** option in your **worldserver.conf** file to point to the directory containing the data.

Some files are optional but highly recommended:

| Directory |  |
| --- | --- |
| dbc | Mandatory |
| maps | Mandatory |
| vmaps | HIGHLY RECOMMENDED |
| mmaps | HIGHLY RECOMMENDED |
| cameras | Recommended |

Option 1: Download Pre-Extracted Files
--------------------------------------

If you intend to use an enUS client you can download the data files below. If you intend to use any other language client you will need to [extract](#option-2-extract-files-yourself) the data yourself.

[Data files enUS (AC Data v19)](https://github.com/wowgaming/client-data/releases/)

1. Download the files above.
2. Create a new folder within the build folder called **Data**. i.e **C:\Build\bin\RelWithDebInfo\Data**
3. Extract the files from the zip file and place them within the **Data** folder.
4. Edit the [DataDir](#updating-datadir) config option to the location of your folder.

Option 2: Extract Files Yourself
--------------------------------

**(Not needed if you downloaded the files above)**

1. Browse into your build directory (**C:\Build\bin\RelWithDebInfo\**) and copy the following files into your World of Warcraft folder (where the wow.exe is located).

```
mapextractor.exe
mmaps_generator.exe
vmap4extractor.exe
vmap4assembler.exe
mmaps-config.yaml
```

2. Browse into **C:\Azerothcore\apps\extractor** and copy "**extractor.bat**" into your World of Warcraft folder with the previous files.
3. Create **mmaps** and **vmaps** folders in your World of Warcraft directory.
4. Launch extractor.bat and select your extractor options.

**Important:** 
  

* **dbc**, **maps** AND **vmaps** are needed to make server work properly!
* Do not attempt to stop the **vmaps** extraction process. It is finished when it prints "Press any key...". It will create two new folders: **buildings** and **vmaps**. The **buildings** folder is completely useless post-running and can be safely deleted.
* Don't run another task before the first is finished or you will have errors.
* If you stop vmap4extractor before finish you will need to delete the Buildings directory before start again.
* **Optional but extremely recommended: Extract mmaps.** Do not attempt to stop this process while it is extracting.

5. Create a new folder in **C:\Build\bin\RelWithDebInfo** called **Data**
6. Move the vmaps, maps, dbc, cameras into the **Data** folder.

Config Files: Worldserver and Authserver
----------------------------------------

First, find the two default config files (named **worldserver.conf.dist** and **authserver.conf.dist**) and copy them. Then rename the copies to their namesakes without the .dist extension. You can find them within C:\Build\bin\RelWithDebInfo\configs\ (may vary).

Open the .conf files and scroll down to LoginDatabaseInfo, WorldDatabaseInfo, and CharacterDatabaseInfo and enter MySQL login information for the server to be able to access your database.

On a newly compiled configuration, you will have the following values by default

```
LoginDatabaseInfo     = "127.0.0.1;3306;acore;acore;acore_auth" worldserver.conf / authserver.conf
WorldDatabaseInfo     = "127.0.0.1;3306;acore;acore;acore_world" worldserver.conf
CharacterDatabaseInfo = "127.0.0.1;3306;acore;acore;acore_characters" worldserver.conf
```

They follow this structure:

```
Variablename = "MySQLIP;Port;Username;Password;database"
```

The following steps must be verified:

* The hostname (127.0.0.1) can stay the same if AzerothCore is being installed on the same computer that you run WoW on.
  If not, follow the instruction in [Realmlist Table](realmlist).
* The port (3306) is the standard configured value. If you changed the default port in your MySQL settings, you must change it accordingly.
  The username and password can be variable. You can choose to either:

  + use default acore / acore username and password pair.
  + create a unique login within a User Manager within your preferred database management tool (commonly identified by an icon that looks like a person or people) and give it the necessary permissions (SELECT, INSERT, UPDATE, DELETE permissions are sufficient, and is much safer).

### Updating DataDir

1. In your **worldserver.conf** file locate the **DataDir** option.
2. Edit it to the path of your folder. i.e **C:\Build\bin\RelWithDebInfo\Data**

**Tip:** For most \*\*worldserver.conf\*\* setting changes, you can simply type .reload config in-game to see changes instantly without restarting the server.

**Warning:** The AzerothCore Team and Owners DO NOT in any case sponsor nor support illegal public servers. If you use these projects to run an illegal public server and not for testing and learning it is your own personal choice.

### (Optional) Config options by environment variable

It is possible to load config options via environment variables, which you can read about [here](config-overrides-with-env-var).

Help
----

If you are still having problems, check:

* [FAQ](faq)
* [Common Errors](common-errors)
* [How to ask for help](how-to-ask-for-help)
* [Join our Discord Server](https://discord.gg/gkt4y2x), but it is not a 24/7 support channel. A staff member will answer you whenever they have time.

| Installation Guide |  |
| --- | --- |
| This article is a part of the Installation Guide. You can read it alone or click the previous link to easily move between the steps. |  |
| [<< Step 2: Core Installation](windows-core-installation) | [Step 4: Database Installation >>](database-installation) |