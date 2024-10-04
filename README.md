# wslmgt
Check and shrink WSL disk usage


## Usage

```
Program : wslmgt  by peter@forret.com
Version : v0.0.0 (2024-10-04 15:15)
Purpose : list and manage wsl volumes
Usage   : wslmgt [-h] [-Q] [-V] [-f] [-L <LOG_DIR>] [-T <TMP_DIR>] <action> <input?>
Flags, options and parameters:
    -h|--help        : [flag] show usage [default: off]
    -Q|--QUIET       : [flag] no output [default: off]
    -V|--VERBOSE     : [flag] also show debug messages [default: off]
    -f|--FORCE       : [flag] do not ask for confirmation (always yes) [default: off]
    -L|--LOG_DIR <?> : [option] folder for log files   [default: /home/pforret/log/wslmgt]
    -T|--TMP_DIR <?> : [option] folder for temp files  [default: /tmp/wslmgt]
    <action>         : [choice] action to perform  [options: list,action2,check,env,update]
    <input>          : [parameter] input file/text (optional)
```

## wslmgt list

```bash
$ wslmgt list
⏳  WSL Volumes: actual size on disk
56G : Ubuntu20.04 : ext4.vhdx : [windows user]
28G : Ubuntu22.04 : ext4.vhdx : [windows user]
⏳  WSL Images : used disk space
41G : Ubuntu-20.04 : /dev/sdf: [wsl user]
28G : Ubuntu-22.04 : /dev/sde: [wsl user]
✴️: Ubuntu-24.04 is WSL1: no VHDX disk that can be shrunk
```

## wslmgt shrink

```bash
$ wslmgt shrink
 
Run the following in a Powershell (Run As Administrator):
(don't type the '>' and whatever's in front of it, your Powershell will show this)
PS C:\WINDOWS\system32> wsl.exe --shutdown
PS C:\WINDOWS\system32> diskpart
DISKPART> select vdisk file=c:\Users\[user]\AppData\Local\Packages\[...Ubuntu20.04LTS_...]\LocalState\ext4.vhdx

DiskPart successfully selected the virtual disk file.

DISKPART> compact vdisk

  100 percent completed
  
DiskPart successfully compacted the virtual disk file.

DISKPART> exit
```

