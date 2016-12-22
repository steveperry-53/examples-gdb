**gdb kubectl**

GNU gdb (GDB) 7.9-gg19
...
(gdb) **info func CreateSecretDockerRegistry**

All functions matching regular expression "CreateSecretDockerRegistry":

File go:
void k8s.io/kubernetes/pkg/kubectl/cmd.CreateSecretDockerRegistry(struct k8s.io/kubernetes/pkg/kubectl/cmd/util.Factory *, io.Writer, struct k8s.io/kubernetes/vendor/github.com/spf13/cobra.Command *, struct []string, error);
void k8s.io/kubernetes/pkg/kubectl/cmd.NewCmdCreateSecretDockerRegistry(struct k8s.io/kubernetes/pkg/kubectl/cmd/util.Factory *, io.Writer, struct k8s.io/kubernetes/vendor/github.com/spf13/cobra.Command *);
void k8s.io/kubernetes/pkg/kubectl/cmd.NewCmdCreateSecretDockerRegistry.func1(struct k8s.io/kubernetes/vendor/github.com/spf13/cobra.Command *, struct []string);

(gdb) **b k8s.io/kubernetes/pkg/kubectl/cmd.CreateSecretDockerRegistry**

Breakpoint 1 at 0x4a8170: file /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go, line 168.

(gdb) **r create secret docker-registry gdbsecret --docker-username=steve53 --docker-password=xxxxxxxxxxx --docker-email=seperry53@gmail.com**

Starting program: /usr/local/google/home/stevepe/google-cloud-sdk/bin/kubectl create secret docker-registry gdbsecret --docker-username=steve53 --docker-password=SteveDock@#16 --docker-email=seperry53@gmail.com

Breakpoint 1, k8s.io/kubernetes/pkg/kubectl/cmd.CreateSecretDockerRegistry (f=0xc820368000, cmdOut=..., cmd=0xc8203a1680, args=..., ~r4=...)
    at /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go:168
168	/go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go: No such file or directory.

(gdb) **n**

169	in /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go

(gdb) **n**

170	in /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go

(gdb) **n**

173	in /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go

(gdb) **n**

174	in /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go

(gdb) **info locals**

value = 0xc820607a9f ""
requiredFlag = 0x1 <error: Cannot access memory at address 0x1>
name = 0x7fffffffdeca "gdbsecret"
generatorName = 0xc8202a585b "\000\000\000\000\000\260\231\221\002\000\000\000\000\023\000\000\000\000\000\000\000\200X* \310", '\000' <repeats 11 times>, "\220X* \310", '\000' <repeats 11 times>, "\240X* \310", '\000' <repeats 11 times>, "\260X* \310", '\000' <repeats 11 times>, "\300X* \310", '\000' <repeats 11 times>, "\320X* \310", '\000' <repeats 11 times>, "\340X* \310", '\000' <repeats 11 times>, "\360X* \310", '\000' <repeats 12 times>, "Y* \310", '\000' <repeats 11 times>, "\020Y* \310", '\000' <repeats 11 times>, " Y* \310", '\000' <repeats 11 times>, "\060Y*"...
generator = {tab = 0x5, data = 0xed2a17 <k8s.io/kubernetes/vendor/github.com/spf13/pflag.boolConv+135>}
err = {tab = 0x0, data = 0x0}
requiredFlags = {array = 0xc8202d32c0, len = 859533105238, cap = 5}

(gdb) **info args**

Possibly a few more steps (gdb) n

Here's a bit of the source code in pkg/kubectl/cmd/create_secret.go:

    requiredFlags := []string{"docker-username", "docker-password", "docker-email", "docker-server"}
	  for _, requiredFlag := range requiredFlags {
		if value := cmdutil.GetFlagString(cmd, requiredFlag); len(value) == 0 {
			return cmdutil.UsageError(cmd, "flag %s is required", requiredFlag)
       }

(gdb) **info locals**

value = 0xc8204e5050 "steve53"
requiredFlag = 0x27fe220 "docker-username"
name = 0x7fffffffdeca "gdbsecret"
generatorName = 0xc8204e502b "\000\000\000\000\000\260\231\221\002\000\000\000\000\023\000\000\000\000\000\000\000\346\336\377\377\377\177\000\000\a\000\000\000\000\000\000\000steve53\000\000\000\000\000\000\000\000\000PPN \310\000\000\000\a\000\000\000\000\000\000\000\200PN \310", '\000' <repeats 11 times>, "\220PN \310", '\000' <repeats 11 times>, "\240PN \310", '\000' <repeats 11 times>, "\260PN \310", '\000' <repeats 11 times>, "\300PN \310", '\000' <repeats 11 times>, "\320PN \310", '\000' <repeats 11 times>, "\340PN \310", '\000' <repeats 11 times>, "\360PN \310", '\000' <repeats 12 times>, "QN"...
generator = {tab = 0x5, data = 0xed2a17 <k8s.io/kubernetes/vendor/github.com/spf13/pflag.boolConv+135>}
err = {tab = 0x0, data = 0x0}
requiredFlags = {array = 0xc8205ddb70, len = 4, cap = 4}

The requiredFlags variable is a slice of 4 strings. The underlying array is at 0xc8205ddb70.

Show 8 addresses starting at 0xc8205ddb70.

(gdb) **x /8a 0xc8205ddb70**

0xc8205ddb70:	0x27fe220	0xf
0xc8205ddb80:	0x27fe200	0xf
0xc8205ddb90:	0x27fe1f0	0xc
0xc8205ddba0:	0x27fe210	0xd

We see that the first string in the slice starts at 0x27fe220 and has length 0xf.

Show 16 character-formatted bytes starting at 0x27fe220

(gdb) **x /16cb 0x27fe220**
0x27fe220:	100 'd'	111 'o'	99 'c'	107 'k'	101 'e'	114 'r'	45 '-'	117 'u'
0x27fe228:	115 's'	101 'e'	114 'r'	110 'n'	97 'a'	109 'm'	101 'e'	0 '\000'

So the first strig in the slice is "docker-username".

Similarly, show the other strings in the slice.

(gdb) **x /16cb 0x27fe200**

0x27fe200:	100 'd'	111 'o'	99 'c'	107 'k'	101 'e'	114 'r'	45 '-'	112 'p'
0x27fe208:	97 'a'	115 's'	115 's'	119 'w'	111 'o'	114 'r'	100 'd'	0 '\000'

(gdb) **x /16cb 0x27fe1f0**

0x27fe1f0:	100 'd'	111 'o'	99 'c'	107 'k'	101 'e'	114 'r'	45 '-'	101 'e'
0x27fe1f8:	109 'm'	97 'a'	105 'i'	108 'l'	0 '\000'	0 '\000'	0 '\000'	0 '\000'

(gdb) **x /16cb 0x27fe210**

0x27fe210:	100 'd'	111 'o'	99 'c'	107 'k'	101 'e'	114 'r'	45 '-'	115 's'
0x27fe218:	101 'e'	114 'r'	118 'v'	101 'e'	114 'r'	0 '\000'	0 '\000'	0 '\000'

So the strings in the slice are:

* "docker-username"
* "docker-password"
* "docker-email"
* "docker-server"

The code iterates over the requiredFlags slice. At this point we are somewhere in
that iteration. Let's look at the current requiredFlag:

(gdb) **p requiredFlag**

$1 = 0x27fe220 "docker-username"

Take a few more steps and look at requiredFlag again.

(gdb) **n**

(gdb) **p requiredFlag**

$3 = 0x27fe200 "docker-password"

When I tried to continue stepping through the code, I got stuck. The debugger displayed
something like [New LWP] and then hung. (NWP is new lightweight process.)

Workaround: Set a breakpoint farther down in the code, somewhere around line 180.

(gdb) **disassemble /m**

...

179	in /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go
   0x00000000004a84b9 <+841>:	xor    %ebx,%ebx
   0x00000000004a84bb <+843>:	mov    %rbx,0xa8(%rsp)
   0x00000000004a84c3 <+851>:	mov    %rbx,0xb0(%rsp)

180	in /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go
   0x00000000004a84cb <+859>:	mov    0x218(%rsp),%rbx
   0x00000000004a84d3 <+867>:	mov    %rbx,(%rsp)
   0x00000000004a84d7 <+871>:	lea    0x23587f2(%rip),%rbx        # 0x2800cd0

(gdb) **b *0x00000000004a84cb**

Breakpoint 2 at 0x4a84cb: file /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go, line 180.

(gdb) **continue**

Breakpoint 2, k8s.io/kubernetes/pkg/kubectl/cmd.CreateSecretDockerRegistry (f=0xc820240480, cmdOut=..., cmd=0xc820474b40, 
    args=..., ~r4=...)
    at /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go:180
180	in /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go

(gdb) **info locals**
value = 0xc82013d800 "https://index.docker.io/v1/"
requiredFlag = 0x27fe210 "docker-server"
name = 0x7fffffffdeca "gdbsecret"
generatorName = 0xc8202ce5fb "\000\000\000\000\000\260\231\221\002\000\000\000\000\023\000\000\000\000\000\000\000\346\336\377\377\377\177\000\000\a\000\000\000\000\000\000\000steve53\000\000\000\000\000\000\000\000\000 \346, \310\000\000\000\a\000\000\000\000\000\000\000\000\337\377\377\377\177\000\000\r\000\000\000\000\000\000\000SteveDock@#16\000\000\000P\346, \310\000\000\000\r\000\000\000\000\000\000\000\035\337\377\377\377\177\000\000\023\000\000\000\000\000\000\000\340\327\023 \310\000\000\000\023\000\000\000\000\000\000\000କ\002\000\000\000\000\033\000\000\000\000\000\000\000\000\330\023 \310\000\000\000\033\000\000\000\000\000\000\000\300\346, \310", '\000' <repeats 11 times>, "\320\346,"...
generator = {tab = 0x0, data = 0x0}
err = {tab = 0x0, data = 0x0}
requiredFlags = {array = 0xc82035fb70, len = 4, cap = 4}

At this point we should be able to see generatorName.

(gdb) **p generatorName**
$1 = 0xc82013d820 "secret-for-docker-registry/v1"

So we're going to generate a secret for a V1 Docker registry.

Got another hang with [New LWP].

Workaround: Set a breakpoint farther down in the code, say around line 191.

(gdb) disassemble /m

191	in /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go
192	in /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go
193	in /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go
194	in /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go
195	in /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go
   0x00000000004a8764 <+1524>:	mov    0x218(%rsp),%rbx
   0x00000000004a876c <+1532>:	mov    %rbx,(%rsp)
   
(gdb) **b *0x00000000004a8764**

Breakpoint 2 at 0x4a8764: file /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go, line 195.

(gdb) **continue**

Continuing.

Breakpoint 2, k8s.io/kubernetes/pkg/kubectl/cmd.CreateSecretDockerRegistry (f=0xc820415d40, cmdOut=..., cmd=0xc8203a1440, 
    args=..., ~r4=...)
    at /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go:195
195	in /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go

(gdb) **info locals**

value = 0xc82011bae0 "https://index.docker.io/v1/"
requiredFlag = 0x27fe210 "docker-server"
name = 0x7fffffffdeca "gdbsecret"
generatorName = 0xc82011bb00 "secret-for-docker-registry/v1"
generator = {tab = 0x7ffff7f88040, data = 0xc820225860}
err = {tab = 0x0, data = 0x0}
requiredFlags = {array = 0xc820281b70, len = 4, cap = 4}

For generator, we have data = 0xc820225860.

Show 8 addresses starting at 0xc82022586.

(gdb) **x /8a 0xc820225860**

0xc820225860:	0x7fffffffdeca	0x9
0xc820225870:	0xc8204f3f47	0x7
0xc820225880:	0xc82011bb20	0x13
0xc820225890:	0xc8203da1c0	0xd

It looks like we have four strings of length 0x9, 0x7, 0x13, 0xd.
Take a look at each one.

Show 9 character-formatted bytes starting at 0x7fffffffdeca.

(gdb) **x /9cb 0x7fffffffdeca**

0x7fffffffdeca:	103 'g'	100 'd'	98 'b'	115 's'	101 'e'	99 'c'	114 'r'	101 'e'
0x7fffffffded2:	116 't'

So the value of generator.Name is "gdbsecret". This will become
the name of the Secret itself.

Similarly, find the values of other fields of generator.

(gdb) **x /7cb 0xc8204f3f47**  
0xc8204f3f47:	115 's'	116 't'	101 'e'	118 'v'	101 'e'	53 '5'	51 '3'

(gdb) **x /13cb 0xc82011bb20**

0xc82011bb20:	115 's'	101 'e'	112 'p'	101 'e'	114 'r'	114 'r'	121 'y'	53 '5'
0xc82011bb28:	51 '3'	64 '@'	103 'g'	109 'm'	97 'a'

(gdb) **x /19cb 0xc82011bb20**

0xc82011bb20:	115 's'	101 'e'	112 'p'	101 'e'	114 'r'	114 'r'	121 'y'	53 '5'
0xc82011bb28:	51 '3'	64 '@'	103 'g'	109 'm'	97 'a'	105 'i'	108 'l'	46 '.'
0xc82011bb30:	99 'c'	111 'o'	109 'm'

## References

https://golang.org/doc/gdb

https://blog.codeship.com/using-gdb-debugger-with-go/
















