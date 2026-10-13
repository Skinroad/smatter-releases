# smatter.club release records

This repository holds the signatures and checksums of every released version of the smatter.club bot. It exists so that anyone can check a download against a record that our own servers cannot change.

There is no code here, and no program to download.

## What is in a folder

Each signed release list has a folder, `signed-list-N`. The number only goes up.

| File | What it is |
|---|---|
| `release-list.json` | The versions a bot may install or update to, when the list was signed, and until when it is good |
| `release-list.sig` | The signature over that file |
| `statement.json` | One version's statement: its version, its commit, and the size and SHA-256 of its bundle, its installer and every file in the bundle |
| `statement.sig` | The signature over that file |
| `Trading-Dashboard-Setup.exe.sha256` | The SHA-256 of that version's installer |

A folder with only the first two files is a list that was signed without a new version: a version was withdrawn, or the list was renewed.

## Checking a downloaded installer

In PowerShell, in the folder you downloaded the installer to:

```powershell
(Get-FileHash .\Trading-Dashboard-Setup.exe -Algorithm SHA256).Hash.ToLower()
```

Compare the result with the first 64 characters of `Trading-Dashboard-Setup.exe.sha256` in the folder of your version. If they differ, do not run the file, and write to hello@smatter.club.

## The signatures

Signatures are ECDSA P-256 with SHA-256 over the exact bytes of the `.json` file, in the fixed 64-byte form (r followed by s). The bot, its updater and its installer check them with public keys that are built into them, before anything is installed or run.

## Contact

hello@smatter.club
