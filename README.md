# Legion Labs Scoop Bucket

Contains dependencies not found in popular bucket or modified scripts of existing manifests used by Legion Labs.

> Visual Studio Build Tools and the Windows SDK don't support local install and they will prompt for elevation anyways. Run `scoop install sudo` prior to installing them and use the global flag as well for consistency.

| App                                        | Description                       | Install Command                             |
|--------------------------------------------|-----------------------------------|---------------------------------------------|
| [winsdk](bucket/winsdk.json)               | Windows 10 SDK                    | `sudo scoop install winsdk --global`        |
| [vs_buildtools](bucket/vs_buildtools.json) | Visual Studio Build Tools         | `sudo scoop install vs_buildtools --global` |

Add bucket using:

```powershell
scoop bucket add legionlabs https://github.com/legionlabs/scoop-bucket
```

### How to update

Some packages need manual updates for now, if the frequency of update is too high we're going to automate it.

#### winsdk and vs_buildtools

Both those packages rely on winget manifest definition to get the executables at the right version since the executables are addressed using their hash rather than the version scheme.

For winsdk look in for the folder with the higher version in [this location](https://github.com/microsoft/winget-pkgs/tree/master/manifests/m/Microsoft/WindowsSDK), for vs_buildtools look [here](https://github.com/microsoft/winget-pkgs/tree/master/manifests/m/Microsoft/VisualStudio/BuildTools)

After you identify the proper folder, open the yaml file it contains.
| Value in winget manifest          | Corresponding in scoop manifest   |
|-----------------------------------|-----------------------------------|
| PackageVersion                    | version                           |
| Installers[0].InstallerUrl        | architecture.64bit.url            |
| Installers[0].InstallerSha256     | architecture.64bit.hash           |

In case there is a major version bump you might need to pay attention to the parameters used un the `Custom` field.

### License

Legion Labs projects are dual-licensed under Apache 2.0 and MIT terms.

* [Apache 2.0](LICENSE-APACHE)
* [MIT](LICENSE-MIT)
