File Validator iOS
==============

Validate files in the main bundle to prevent a user to change them. (to cheat on config files)

Just the first commit to save some work done this evening..

The idea is to compute a hash (SHA256) of a config file (for example a plist) plus a known secret (that will be compiled in the binary)

the repo comes with a static lib and an example, cocoapod spec will come with v0.1, this is just a first draft.

Usage
-----
`fingerprints.plist` is a plist that need to be added to your project target and containing all the filenames that you want to secure with the relative correct hash 
( without the script the way to fill this information is to run the validator and ... copy and paste the hash in the fingerprints plist)

usage is:
``` objective-c
[FVFileValidator setSecret:@"asda8r32ijiwesjza9sa9idsadi0saidas0kdo3"];
BOOL isValid = [FVFileValidator validateFile:@"filetosecure.plist"];
```
First we need to set a string as a secret. 
Calling validateFile: will return YES if the file is valid (the sha256 of filetosecure.plist + the secret matches the one defined in the fingerprints.plist)

forgetting to set the secret, create the fingerprints.plist, having the entry of the file we want to check in the fingerprints.plist will raise an Exception


TODO
-----

- [ ] ruby script for filling the fingerprints.plist with the right hashes as a pre build script to run in xcode
- [ ] some bit operation to obfuscate a bit the secret
