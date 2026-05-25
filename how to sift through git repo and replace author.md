
1)
```
git filter-repo --force --email-callback '
    return b"leakrull@proton.me"
' --name-callback '
    return b"leakrullp"
'
```
2)
```
git remote add origin https://github.com/leakrullp/repo-name.git
```
3)
```
git push -u origin main --force
```
4)

