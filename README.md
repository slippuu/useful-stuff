# Useful Stuff
Just some useful things I've found and collected over the years, mainly as my own ability to store information but hopefully you find some of the things useful as well.

## Useful Info
`$` denotes User Priv

`!` denotes Admin Priv

## Contents
- [Move WSL instance to a new computer](##-move-wsl-instance-to-new-computer)
- [PWSH - Easy Python Venv Activation](##-pwsh---easy-python-venv-activation)

## Move WSL instance to new computer
On the original computer:
```pwsh
$ wsl --export <distro> <export file>.tar
```

On the new computer:
```pwsh
! wsl --install
$ wsl --unregister Ubuntu
$ mkdir $env:USERPROFILE\WSL\instances\<new distro>
$ wsl --import <new distro> $env:USERPROFILE\WSL\instances\<new distro> <export file>.tar --version 2
$ wsl --set-default <new distro>
$ wsl ~
```

```bash
$ sudo -e /etc/wsl.conf
```
Add:
```
[user]
default=<username>
```
## Pwsh - Easy Python Venv Activation
Add to `$profile`
```pwsh
function venv {
  param (
    [string]$venvPath
  )
  if (Test-Path $venvPath) {
    & "$venvPath\.venv\Scripts\Activate.ps1
  } else {
    Write-Host "Virutal Environment not found. Please rerun from a location with a valid .venv folder."
  }
}
```
Example usage: `venv .`
