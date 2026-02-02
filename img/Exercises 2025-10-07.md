UNIX treats file directories in the same fashion as files; that is, both are defined by the same type of data structure, called an inode. As with files, directories include a nine- bit protection string. If care is not taken, this can create access control problems. For example, consider a file with protection mode 644 (octal) contained in a directory with protection mode 730. How might the file be compromised in this case?
  
Short answer: even though the file is `644` (group/others cannot write the file), the directory being `730` gives the directory’s group the ability to _unlink / replace_ directory entries. That lets a group member remove the original file and put a malicious/replaced file in its place — so the file can be compromised despite its `644` bits.

Why (step-by-step):

- Unix permissions on _directories_ are different in meaning from file permissions:
    
    - directory **r** = list names (readdir),
        
    - directory **w** = create/delete/rename entries,
        
    - directory **x** = traverse / access an entry by name (search).
        
- Decode the modes:
    
    - `644` for the file = owner `rw-`, group `r--`, others `r--`.
        
    - `730` for the directory = owner `rwx` (7), group `wx` (3 → write + execute, _no_ read), others `---`.
        
- Because the directory has group `w`:
    
    - members of the directory’s group can _remove (unlink) and create_ directory entries — even if they cannot write the contents of the file itself.
        
    - with the execute bit present, they can access a file by name (they can enter the directory / operate on known filenames) even though they cannot list it.
        
- Practical compromise:
    
    - A group member who knows the filename can `unlink` (delete) it and then create a new file with the same name containing attacker-controlled contents (or symlink it somewhere else). The process that later opens the filename will then read the attacker’s file. The original file’s write-protection does not prevent deletion; deletion is governed by the _directory_ write bit.
        
    - If no sticky bit is set, directory write permission lets group members remove _other users’_ files in that directory.
        

Mitigations:

- Remove group write on the directory if group should not be able to modify entries: e.g.
    
    `chmod 750 somedir    # owner rwx, group r-x, others none`
    
- If you want the directory writable by many users but want to prevent them deleting each other’s files, set the sticky bit (like `/tmp`):
    
    `chmod +t somedir     # makes e.g. 1730 -> prevents deletion except by file owner or dir owner/root`
    
- Ensure correct ownership/group for the directory and files (`chown` / `chgrp`) so only intended principals have group privileges.
    

Wrap up: file permissions protect content, but directory permissions control creation/deletion/placement of names. A writable directory (for the attacker’s principal) is often enough to replace a supposedly protected file.

## Notes and PWs for OverTheWire challenge
`The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`

bandit1: `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`