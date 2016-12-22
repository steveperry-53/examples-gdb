**gdb kubectl**
GNU gdb (GDB) 7.9-gg19
...
(gdb) **info func CreateSecretDockerRegistry**
All functions matching regular expression "CreateSecretDockerRegistry":

File go:
void k8s.io/kubernetes/pkg/kubectl/cmd.CreateSecretDockerRegistry(struct k8s.io/kubernetes/pkg/kubectl/cmd/util.Factory *, io.Writer, struct k8s.io/kubernetes/vendor/github.com/spf13/cobra.Command *, struct []string, error);
void k8s.io/kubernetes/pkg/kubectl/cmd.NewCmdCreateSecretDockerRegistry(struct k8s.io/kubernetes/pkg/kubectl/cmd/util.Factory *, io.Writer, struct k8s.io/kubernetes/vendor/github.com/spf13/cobra.Command *);
void k8s.io/kubernetes/pkg/kubectl/cmd.NewCmdCreateSecretDockerRegistry.func1(struct k8s.io/kubernetes/vendor/github.com/spf13/cobra.Command *, struct []string);
(gdb) #
(gdb) #
(gdb) **b k8s.io/kubernetes/pkg/kubectl/cmd.CreateSecretDockerRegistry**
Breakpoint 1 at 0x4a8170: file /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go, line 168.
(gdb) #
(gdb) #
(gdb) **r create secret docker-registry gdbsecret --docker-username=steve53 --docker-password=xxxxxxxxxxx --docker-email=seperry53@gmail.com**
Starting program: /usr/local/google/home/stevepe/google-cloud-sdk/bin/kubectl create secret docker-registry gdbsecret --docker-username=steve53 --docker-password=SteveDock@#16 --docker-email=seperry53@gmail.com

Breakpoint 1, k8s.io/kubernetes/pkg/kubectl/cmd.CreateSecretDockerRegistry (f=0xc820368000, cmdOut=..., cmd=0xc8203a1680, args=..., ~r4=...)
    at /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go:168
168	/go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go: No such file or directory.
(gdb) #
(gdb) #
(gdb) **n**
169	in /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go
(gdb) **n**
170	in /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go
(gdb) **n**
173	in /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go
(gdb) **n**
174	in /go/src/k8s.io/kubernetes/_output/dockerized/go/src/k8s.io/kubernetes/pkg/kubectl/cmd/create_secret.go
(gdb) #
(gdb) #
(gdb) **info locals**
value = 0xc820607a9f ""
requiredFlag = 0x1 <error: Cannot access memory at address 0x1>
name = 0x7fffffffdeca "gdbsecret"
generatorName = 0xc8202a585b "\000\000\000\000\000\260\231\221\002\000\000\000\000\023\000\000\000\000\000\000\000\200X* \310", '\000' <repeats 11 times>, "\220X* \310", '\000' <repeats 11 times>, "\240X* \310", '\000' <repeats 11 times>, "\260X* \310", '\000' <repeats 11 times>, "\300X* \310", '\000' <repeats 11 times>, "\320X* \310", '\000' <repeats 11 times>, "\340X* \310", '\000' <repeats 11 times>, "\360X* \310", '\000' <repeats 12 times>, "Y* \310", '\000' <repeats 11 times>, "\020Y* \310", '\000' <repeats 11 times>, " Y* \310", '\000' <repeats 11 times>, "\060Y*"...
generator = {tab = 0x5, data = 0xed2a17 <k8s.io/kubernetes/vendor/github.com/spf13/pflag.boolConv+135>}
err = {tab = 0x0, data = 0x0}
requiredFlags = {array = 0xc8202d32c0, len = 859533105238, cap = 5}
(gdb) #
(gdb) #
(gdb) **info args**
f = 0xc820368000
cmdOut = {tab = 0x7ffff7f71210, data = 0xc820036010}
cmd = 0xc8203a1680
args = {array = 0xc820295440, len = 1, cap = 4}
~r4 = {tab = 0x0, data = 0x0}
