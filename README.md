# Chacal
Golang anti-vm framework for Red Team and Pentesters



<p align="center">
  <a href="https://github.com/p3tr0v/chacal">
    <img src="https://github.com/p3tr0v/chacal/blob/main/chacalWhite.png" alt="Logo" width="190" height="160">
  </a>

  
  <p align="center">
    Let Chacal hidde your malware in an assalt operation!
    <br />
    <br />
    <br />
  </p>
</p>

<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#dependencies">Dependencies</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li>
      <a href="#usage">Usage</a>
      <ul>
        <li><a href="#Anti-Debugging">Anti-Debugging </a></li>
        <li><a href="#Anti-Memory">Anti-Memory</a></li>
        <li><a href="#Anti-VM">Anti-VM</a></li>
      </ul>
    </li>
    <li><a href="#contact">Contact</a></li>
  </ol>
</details>




<!-- ABOUT THE PROJECT -->
## About The Project
Chacal is an anti-vm framework written in Golang in order to support Red Team and Pentesters in your assalts, in Windows environment!



<!-- GETTING STARTED -->
## Getting Started
Firstly, make sure that your dependencies are satisfied.

### Dependencies
Chacal has 3 dependencies:
* wmi
  ```
  go get github.com/StackExchange/wmi@v0.0.0-20210224194228-fe8f1750fd46
  ```
* go-ole
  ```
  go get github.com/go-ole/go-ole@v1.2.5 
  ```
* go-ps
  ```
  go get github.com/mitchellh/go-ps@v1.0.0 
  ```
  
### Installation
In your prompt type
  ```
  go get github.com/p3tr0v/chacal
  ```
## Usage
Into your program, import the packages used by Chacal
```
import (
      "github.com/p3tr0v/chacal/antidebug"
      "github.com/p3tr0v/chacal/antimem"
      "github.com/p3tr0v/chacal/antivm"
    )
```
### Anti-Debugging
` "github.com/p3tr0v/chacal/antidebug"` <br/>
Antidebug package implements strategies to avoid common programs that are used for debugging.

#### Process
`antidebug.ByProcessWatcher()` return boolean <br/>
This function look for common programs used for inspect process, like processhacker.exe, procmon.exe, xdbg.exe, etc. <br/>
Example:
```
if antidebug.ByProcessWatcher() { // Whether some debugger program founded, enter here.
  // exit or wait
}
```
#### Timming
`antidebug.ByTimmingDiff(time, int)` return boolean<br/>
Compare whether the difference between initial and end time is bigger than difference allowed (in seconds).
When debugging, some analisys use to take some time into a function.
Grag the time just in the begging of the function and later in the end, before go out, and ask Chacal to compare.<br/>
Example:
```
func myFuncHere(){
  initTime := time.Now() // grab the time here
  // do your actions here
  if antidebug.ByTimmingDiff(timeInit, 2){ // if your function takes 2 seconds or more, your malware must be debbuging. You chose your time.
    // exit or wait
  }
}
  ```

### Anti-Memory
` "github.com/p3tr0v/chacal/antimem"` <br/>
Antimem package implements strategies to avoid common programs that are used for inspect memory process.

#### Memory
`antimem.ByMemWatcher()` return boolean <br/>
This function look for common programs used for inspect memory, like rammap.exe, dumpit.exe, etc. <br/>
Example:
```
if antimem.ByMemWatcher() { // Whether some program used for inspect memory founded, enter here.
  // exit or wait
}
```

### Anti-VM
` "github.com/p3tr0v/chacal/antivm"` <br/>
Antivm package implements strategies to avoid virtualized environment.

#### Disk size
`antivm.BySizeDisk( int )` return boolean <br/>
Check total size disk, in GB. <br/>
Example:
```
if antivm.BySizeDisk(100) { // whether total disk size is less than 100 GB, enter here. You chose the size, always in GB.
  // exit or wait
}
```
#### Virtual disk
`antivm.IsVirtualDisk()` boolean <br/>
Check whether may be a virtual disk. <br/>
Example:
```
if antivm.IsVirtualDisk() { // If Chacal guess you are on virtual disk, enter here.
  // exit or wait
}
 ```

#### Known virtual MAC Address
`antivm.ByMacAddress()` boolean <br/>
Look for known virtualized MAC Address. <br/>
Example:
```
if antivm.ByMacAddress() { If Chacal guess you are on virtual MAC Address, enter here.
  // exit or wait
}
```
## Contact
Telegram: @p3tr0v <br/>
LinkedIn: Test your OSINT skills ;)


