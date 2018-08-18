# capsh

The capability-aware shell starts applications from inside Capsicum's
*capability mode*.
This allows for untrusted applications to be **sandboxed from inception**.

**Note:** currently, this software only works on a version of FreeBSD that
supports direct execution of `ld-elf.so.1` with an explicit file descriptor
argument, i.e., `12-CURRENT` post-`r318431`.


## Gsoc'18

I have been working on capsh as a part of my gsoc project.
The project wiki can be found [here](https://wiki.freebsd.org/SummerOfCode2018Projects/ObliviousSandboxingwithCapsicum)

The latest committs to this branch were a part of my work on this repository.

### Deliverables

The deliverables that I was able to cope up with were

1. Integrate capsh with [libpreopen](https://github.com/ShubhGupta2125/libpreopen)

2. Allow preopening of files in capsh using libpreopen such that applications which needed preopened files before entering the sandbox, could be used ensuring that the application just works!

3. Added the functionality in [libpreopen](https://github.com/ShubhGupta2125/libpreopen) which allowed preopening of sockets. I also tried to sandbox ```telnet``` by writing wrappers for "connect" call and the DNS lookup(getaddrinfo). It threw an unfortunate Bus error which needs debugging and will be a part of my continued work on the same project.

4. Integrated [libucl](https://github.com/vstakhov/libucl/tree/master/src) inside capsh to parse policy files such as [this](https://github.com/ShubhGupta2125/capsh/blob/filePolicy/src/file.conf) is a policy file for ```file```. The policy files are parsed for preopening the required directories and files needed to the application. It also specifies to run a blind file preoping mechanism or to check for hostnames in the argument if the blind variable is set to 1.

5. Tried to write policy files for various policy files for different applications. ```file``` gives the required output when the policy file is given to capsh.

6. Tried writing the policy file for a complex application like clang, but faced an unfortunate error with the rtld runtime linker, which needs to be debuggedby rebuilding the freebsd source code and will be my milestone for continued work on this project.

7. All applications that need just a preopened file to enter a sandbox can now work successfully using capsh. A curated list of all these applications is under the work right now, and will be formulated here soon.



