---
title: "cargo-wix"
enableToc: false
tags:
- tool
- windows
---
`cargo-wix` is a tool to create windows installers. 

if there are multiple `.exe` files where `main.exe` depends on the others,
a [bundle](https://volks73.github.io/cargo-wix/cargo_wix/index.html#bundles) can be created.

generating a windows guid in powershell: `[guid]::NewGuid()`
[guid tutorial](https://winaero.com/generate-new-guid-in-windows-10/#:~:text=Type%20or%20copy%2Dpaste%20the,in%20the%20traditional%20Registry%20format.)

**setting custom default directory:**
[helpful stackoverflow answer](https://stackoverflow.com/questions/7328748/harvesting-files-leads-to-lght0231-error)

add this element: 
`<SetDirectory Id="INSTALLFOLDER" Value="[WindowsVolume]custom_dir"/>`
where the `Value` is the custom directory `[WindowsVolume]` is the base path, like `C:\`

with `cargo-wix` generated `.wix` file, replace the `Id` of the Directory element
with name `PFiles` from `$(var.PlatformProgramFilesFolder)` to `INSTALLFOLDER`.

then add the `ComponentGuidGenerationSeed` property to the Directory element with 
the id of `APPLICATIONFOLDER`
`<Directory Id='APPLICATIONFOLDER' Name='focal_point' ComponentGuidGenerationSeed="c75138eb-a0a8-4d47-a5fa-41cf7145c4cc">`
