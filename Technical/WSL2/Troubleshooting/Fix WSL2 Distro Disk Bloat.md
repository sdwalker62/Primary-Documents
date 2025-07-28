==Note that they `Hyper-V` tools are not available to those running Windows * Home only Pro and above.==

The first thing you will need to do is clean up unnecessary files (ran on `wsl2` distro):

```bash
sudo fstrim -av
```

Since we are using Windows Home we cannot rely on tools like `optimize-vhd` to automate this process, instead we will use `diskpart`.

Note that on my machine the virtual hard disk we are shrinking is located at:
`"C:\Users\samue\AppData\Local\Packages\CanonicalGroupLimited.Ubuntu_79rhkp1fndgsc\LocalState\ext4.vhdx"`

Here is the series of steps in order:

### Powershell

Start by shutting down the current `wsl2` process and entering the `diskpart` utility:
```powershell
wsl.exe --shutdown
diskpart
```

### Diskpart Window

In the window that opens run the following commands. Most should run quickly, only the compact command should take any significant time.
```bash
select vdisk file="C:\Users\samue\AppData\Local\Packages\CanonicalGroupLimited.Ubuntu_79rhkp1fndgsc\LocalState\ext4.vhdx"
attach vdisk readonly
compact vdisk
detach vdisk
exit
```

