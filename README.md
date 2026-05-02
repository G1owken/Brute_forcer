# Folder_archiver

Encrypts folders into password-protected .7z archives. Passwords are auto-generated and saved as key files — nothing to configure or remember.

Made for personal use.

## Setup

Install 7zip archiver
pip install py7zr
python Encoder/main.py

Requires tkinter, which comes bundled with Python on Windows and macOS. On Linux: sudo apt install python3-tk

## Usage

On launch a dialog asks whether you want to encrypt or decrypt.

Encrypt: select a folder, confirm deletion of the original, done. The archive goes to Encoder/archives/, the key file to Encoder/passwords/.

Decrypt: select the .7z archive, then the corresponding key file, then the output directory. If extraction fails for any reason the archive and key are left untouched.

Passwords are 24 characters, generated via Python's secrets module — mix of uppercase, lowercase, digits and punctuation.

## Project structure

Encoder/
  main.py         entry point, all GUI dialogs
  archiver.py     creates the archive, writes the key file, deletes the original folder
  decoder.py      reads the key, decrypts and extracts
  password_gen.py random password generation
  archives/       output directory for .7z files (gitignored)
  passwords/      output directory for key .txt files (gitignored)

## Notes

The original folder is permanently deleted after encryption, not moved to trash. The confirmation dialog exists for that reason.

Key files store the archive name alongside the password. Don't edit them manually — the parser splits on ": " and will break if that line changes.

archives/ and passwords/ are both listed in .gitignore. Keep it that way, especially if the repo is public.

## Requirements

Python 3.8+
py7zr — https://github.com/miurahr/py7zr
