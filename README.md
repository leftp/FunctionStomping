# FunctionStomping
![image](https://img.shields.io/badge/C%2B%2B-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white) ![image](https://img.shields.io/badge/Rust-black?style=for-the-badge&logo=rust&logoColor=#E57324) ![image](https://img.shields.io/badge/Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white)<br />

## Description
This is a brand-new technique for shellcode injection to evade AVs and EDRs. This technique is inspired by Module Stomping and has some similarities. <del>As to this date (23-01-2022) also <a href="https://github.com/hasherezade/hollows_hunter">hollows-hunter</a> doesn't find it.</del><br /><br />
The big advantage of this technique is that it isn't overwritting an entire module or pe, just one function and the target process can still use any other function from the target module.<br /><br />
The disadvantage is that it won't work for every function in the wild (but it will work for most of them), the exact explanation is in my blog: <a href="https://idov31.github.io/2022-01-28-function-stomping/">The Good, The Bad And The Stomped Function</a>.<br /><br />
<b>NOTE: It is possible that AV will flag this, if the signature is a signature of msfvenom/metasploit it is fine! you just need to change the shellcode or encrypt it.</b>

**UPDATE:** Apperantly this isn't the first PoC avaliable and RastaMouse wrote a [blog post](https://offensivedefence.co.uk/posts/module-stomping/) that does the exact same thing that FunctionStomping does in C#.

## Usage
You either include the header to your program like this:
```cpp
#include "functionstomping.hpp"

int main() {
    // Just get the pid in any way and pass it to the function.
    DWORD pid = 3110;
    FunctionStomping(pid);
    return 0;
}
```

Or use the rust program:
```bash
cd functionstomping
cargo b
functionstomping.exe <pid>
```

After you ran this program you <b>MUST</b> call the function from the remote process! (If you used the default function CreateFile then you must call to it from the remote process!).

## Setup
Currently, the shellcode to run is just to pop a calculator, but all you need to do is replace the ```unsigned char shellcode[]``` with your shellcode. I used C++ 17 and VS2019 to compile the program with the C++ header and rust version 2021 to compile the rust program (you can see the dependencies in the Cargo.toml).

## POC
<img src="images/poc.png" />


## Disclaimer
I'm not responsible in any way for any kind of damage that is done to your computer / program as cause of this project. I'm happily accept contribution, make a pull request and I will review it!

## Acknowledgments
https://github.com/countercept/ModuleStomping<br />
https://www.cyberark.com/resources/threat-research-blog/masking-malicious-memory-artifacts-part-iii-bypassing-defensive-scanners<br />
https://offensivedefence.co.uk/posts/module-stomping/
