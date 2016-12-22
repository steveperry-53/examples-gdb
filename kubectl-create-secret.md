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







