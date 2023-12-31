# Basic Linux Commands
---


- [Which shell am i on ? ](### Which shell am i on ?)

---
### Which shell am i on ?
``` bash
echo $SHELL
```

### How to create a directory inside a non existing directory, again inside a non existing directory?
``` bash
mkdir -p hello/this/is/nested/dir 
```

### Add content into a file by `cat` command
**STEP 1** : `cat > target_file`

**STEP 2** : Type content

**STEP 3** : `CTRL + D` to save & exit 

### SSH
``` bash
ssh USER@HOST_ID
```

### Download a file on web

To print a file in stdout
``` bash
curl <URL>
```
To get the file
``` bash
curl <URL> -o <SOME_OUTPUT_FILE>
```
or
``` bash
wget <URL>
```

# RPM Package Manager

### Install packages
``` bash
rpm -i <package.rpm>
```
- **note** : RPM will not automatically arrange dependencies.

### Uninstall packages
``` bash
rpm -e <package.rpm>
```

### Query packages
``` bash
rpm -q <package.rpm>
```

# YUM Package Manager

### Install packages
``` bash
yum install <package>[-<version>]
```

### Uninstall packages
``` bash
yum remove <package>[-<version>]
```

### List repos
``` bash
yum repolist
```
- all there repos are store in `/etc/yum.repos.d/` directory

### List packages

``` bash
yum [--showduplicates] list <package>
```

here,
- `--showduplicates` flag is to list the duplicate packages installed.

# Linux `systemctl` command

### Start & Stop a Service
``` bash
systemctl start <services>
systemctl stop <services>
```

### Status of a Service
``` bash
systemctl status <services>
```

### Configure the service to start at Startup
``` bash
systemctl enable <services>
systemctl disable <services>
```

### Reload Services List
``` bash
systemctl deamon-reload
```


# HTML + CSS

I Practiced HTML and CSS by making a Card Element. 

![Card.png](Card.png)

- ## [HTML](card.html)

- ## [CSS](card.css)
