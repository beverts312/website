---
title: "Bash"
type: docs
---

Here is an example of error handling:  

```bash
some-executable  
if [[ $? -ne 0 ]] ; then
        echo "If we hit this block there was an error"
fi
```



This function can be used to determine the Operating System \(atleast ones I care about\):

```bash
setOs() {
    MY_OS=""

    case "$OSTYPE" in
        darwin*)  MY_OS="darwin" ;; 
        linux*)   MY_OS="linux" ;;
    esac

    if [[ "$MY_OS" -eq "linux" ]] && [[ -r /etc/debian_version ]] ; then
        MY_OS="debian"
    elif [[ "$MY_OS" -eq "linux" ]] && [[ -r /etc/fedora-release ]] ; then
        MY_OS="fedora"
    elif [[ "$MY_OS" -eq "linux" ]] && [[ -r /etc/oracle-release ]] ; then
        MY_OS="oel"
    elif [[ "$MY_OS" -eq "linux" ]] && [[ -r /etc/centos-release  ]] ; then
        MY_OS="centos"
    elif [[ "$MY_OS" -eq "linux" ]] && [[ -r /etc/redhat-release  ]] ; then
        MY_OS="rhel"
    elif [[ "$MY_OS" -ne "darwin" ]] ; then
        echo "Could not determine OS"
        exit 1
    fi
}
```



