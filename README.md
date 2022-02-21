# krbGuess
cqure官网倒闭了，搬运krbGuess


KrbGuess is a small and simple tool which can be used during security testing to guess valid usernames against a Kerberos environment. It allows you to do this by studying the response from a TGT request to the KDC server. The tool works against both Microsoft Active Directory, MIT and Heimdal Kerberos implementations. In addition it will detect if an account lacks pre-authentication.

The tool is supplied with a file containing a list of usernames and requests a TGT for each user and then waits for the response. If the KDC responds with a valid TGT or with an error message stating that pre-authentication is required, a valid username has been discovered. Several guesses can be run in parallel (currently only against a single KDC) in order to improve performance.

Be careful not to run with to many threads and low timeouts as it will bring the KDC to its knees during the time of the test. The default values have been tuned against a virtual machine, and currently eat somewhere around 80% CPU which gives me roughly 700 guesses per second. In most cases the network throughput won’t be the performance bottleneck. So far I’m seeing that 2-3MBit of queries is generating a sustained 100% CPU load against both Heimdal on Ubuntu and Windows 2003.

 

The tool is written in Java and does not rely on any Kerberos libraries to perform the guessing. In order to successfully run the tool against a system it needs at least the realm, dictionary and a server parameters to be set. eg.

```
Java –jar kerbguess.jar –r [domain] –d [user list] –s [DC IP]
```
