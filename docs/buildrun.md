# Building, Running, and Developing

### Building

Windows 10 64-bit or Windows Server 2019, and Git for Windows is required. The build script will take care of downloading, verifying, and extracting the right versions of the various dependencies:

```text
C:\Projects> git clone https://github.com/amnezia-vpn/amneziawg-windows-client
C:\Projects> cd amneziawg-windows-client
C:\Projects\amneziawg-windows-client> build
```

### Running

After you've built the application, run `amd64\amneziawg.exe` or `x86\amneziawg.exe` to install the manager service and show the UI.

```text
C:\Projects\amneziawg-windows-client> amd64\amneziawg.exe
```

Alternatively, you can craft your own installer using the `quickinstall.bat` script.

### Optional: Localizing

To translate AmneziaWG UI to your language:

1. Upgrade `resources.rc` accordingly. Follow the pattern.

2. Make a new directory in `locales\` containing the language ID:

  ```text
  C:\Projects\amneziawg-windows-client> mkdir locales\<langID>
  ```

3. Configure and run `build` to prepare initial `locales\<langID>\messages.gotext.json` file:

   ```text
   C:\Projects\amneziawg-windows-client> set GoGenerate=yes
   C:\Projects\amneziawg-windows-client> build
   C:\Projects\amneziawg-windows-client> copy locales\<langID>\out.gotext.json locales\<langID>\messages.gotext.json
   ```

4. Translate `locales\<langID>\messages.gotext.json`. See other language message files how to translate messages and how to tackle plural. For this step, the project is currently using [CrowdIn](https://crowdin.com/translate/WireGuard); please make sure your translations make it there in order to be added here.

5. Run `build` from the step 3 again, and test.

6. Repeat from step 4.

### Optional: Creating the Installer

The installer build script will take care of downloading, verifying, and extracting the right versions of the various dependencies:

```text
C:\Projects\amneziawg-windows-client> cd installer
C:\Projects\amneziawg-windows-client\installer> build
```

### Optional: Signing Binaries

Add a file called `sign.bat` in the root of this repository with these contents, or similar:

```text
set SigningProvider=/sha1 8BC932FDFF15B892E8364C49B383210810E4709D
set TimestampServer=http://timestamp.entrust.net/rfc3161ts2
```

After, run the above `build` commands as usual, from a shell that has [`signtool.exe`](https://docs.microsoft.com/en-us/windows/desktop/SecCrypto/signtool) in its `PATH`, such as the Visual Studio 2017 command prompt.

### Alternative: Building from Linux

You must first have Mingw and ImageMagick installed.

```text
$ sudo apt install mingw-w64 imagemagick
$ git clone https://github.com/amnezia-vpn/amneziawg-windows-client
$ cd amneziawg-windows-client
$ make
```

You can deploy the 64-bit build to an SSH host specified by the `DEPLOYMENT_HOST` environment variable (default "winvm") to the remote directory specified by the `DEPLOYMENT_PATH` environment variable (default "Desktop") by using the `deploy` target:

```text
$ make deploy
```

### [`awg(8)`](https://github.com/amnezia-vpn/amneziawg-tools/blob/master/src/man/wg.8) Support for Windows

The command line utility [`awg(8)`](https://github.com/amnezia-vpn/amneziawg-tools/blob/master/src/man/wg.8) works well on Windows. Being a Unix-centric project, it compiles with a build script:

```text
$ git clone https://github.com/amnezia-vpn/amneziawg-tools
$ cd amneziawg-tools
$ build
```

It interacts with AmneziaWG instances run by the main AmneziaWG for Windows program.

When building on Windows, the aforementioned `build.bat` script takes care of building this.
