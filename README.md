# goVcenterRESTcli
Simple go client for using vcenter rest api

Sample user/pass json file

    cat ~/.vmwarepass.json
    {
    "host":"host1.virtualdc.local",
    "username":"staff@virtualdc.com",
    "secret":"wli#Lol-2Gbv#"
    }


First clone the repo and

    cd into /path/to/repo
    go build

Usage :

    ./vcenterapi -h

    -list
  
        Lists available virtual machines
        
    -start
  
        start vm700 vm701 #starts vms with name vm700 vm701
        
        
List vm's & get the vmid eg. 
--------------------------------------------------------------------------

O/p order - vmid , vmName          ,PoweredState  , Memory(MB) , Num of cpu

    ./vcenterapi -list | grep "192.45.9.19" 

    vm-236,Normal_Windows_192.45.9.191,POWERED_OFF,mem:32768,cpu:16

    vm-138,Normal_Windows_192.45.9.192,POWERED_OFF,POWERED_OFF,mem:32168,cpu:18

    vm-182,Normal_Windows_192.45.9.193,POWERED_OFF,POWERED_ON,mem:4096,cpu:8

--------------------------------------------------------------------------
Example usage (when vms are already powered on)
--------------------------------------------------------------------------
    ./vcenterapi -start vm-5646 vm-69521
    
    2022/03/01 00:19:00 [vm-5646 vm-69521]
    2022/03/01 00:19:03 &{0x1120700 {0xc0000f09a0} 0x11d0e00} 400
    2022/03/01 00:19:03 Problem starting vm-69521, already started state.
    2022/03/01 00:19:03 &{0x1120700 {0xc0000f0b00} 0x11d0e00} 400
    2022/03/01 00:19:03 Problem starting vm-5646, already started state.


--------------------------------------------------------------------------
Shutting down one or more vm's
--------------------------------------------------------------------------

    go run main.go -stop vm-51502 vm-5646 vm-69521
    2022/03/01 01:34:45 [vm-51502 vm-5646 vm-69521]
    2022/03/01 01:34:47 &{0x1120700 {0xc000100ab0} 0x11d0e00} 204
    2022/03/01 01:34:47 &{0x1120700 {0xc000100ab0} 0x11d0e00} 204
    2022/03/01 01:34:47 Machine/s stopped successfully.
    2022/03/01 01:34:47 Machine/s stopped successfully.
    2022/03/01 01:34:47 &{0x1120700 {0xc000100ab0} 0x11d0e00} 204
    2022/03/01 01:34:47 Machine/s stopped successfully.
if machines are already powered off the o/p is likely to be eg.:

    2022/03/01 01:36:46 &{0x1120700 {0xc0001f6c60} 0x11d0e00} 400
    2022/03/01 01:36:46 Problem stopping vm-5646, already in off state.


