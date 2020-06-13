# SpoolSystem

SpoolSystem is a CNA script for Cobalt Strike which uses @itm4n's Print Spooler named pipe impersonation trick to gain SYSTEM privileges without creating any new process or relying on cross-process shellcode injection (if the `selfinject` method is used`).

## Running

The script supports two modes:

* selfinject: this is the one you probably want to use. It triggers the spoolss RPC method via self-injection within the current process. This is the best option for OPSEC, but ideally should be done in a process you don't mind crashing (just incase).
* spawn: this uses `bdllspawn` to trigger the spoolss RPC method, so launches another process (not as good for OPSEC)

Both modes allow a user with only `SeImpersonatePrivilege` to gain SYSTEM privileges within the current beacon session. This is useful if you have a privilege escalation that gives you `LOCAL SERVICE`, `NETWORK SERVICE` or similar, or for cases where `SeDebugPrivilege` has been removed. However it can also be used as a drop-in replacement for `getsystem`.

## Example

![example](spoolsystem.gif)

## References

* https://github.com/itm4n/PrintSpoofer
* https://itm4n.github.io/printspoofer-abusing-impersonate-privileges/
* https://github.com/leechristensen/SpoolSample
