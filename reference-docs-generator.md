**gdb gen-apidocs**

(gdb) **r --config-dir=gen-apidocs/generators --munge-groups=false**

Immediately (or fairly soon) enter CTRL-C

(gdb) **b github.com/kubernetes-incubator/reference-docs/gen-apidocs/generators/api.NewConfig**

Breakpoint 1 at 0x73b7d0: file /home/seperry53/src/github.com/kubernetes-incubator/reference-docs/gen-apidocs/generators/api/config.go, line 86.

(gdb) **continue**

This runs to completion because the NewConfig function has already executed.
But now don't quit gdb. Instead, run the program again, now that the breakpoint is set.

(gdb) **r --config-dir=gen-apidocs/generators --munge-groups=false**

Thread 1 "gen-apidocs" hit Breakpoint 1, ...
86      func NewConfig() *Config {

If you like, set a second breakpoint at a line number in the source file.

(gdb) **b line-number**

(gdb) **p config.ResourceCategories.array[0].Resources.array[0]**

$23 = (struct github.com/kubernetes-incubator/reference-docs/gen-apidocs/generators/api.Resource *) 0xc4200fe0c0

(gdb) **set print pretty on**

(gdb) `p *(config.ResourceCategories.array[0].Resources.array[2])`

`$27 = {
  Name = 0xc4201b2170 "DaemonSet", 
  Version = 0xc4201b2188 "v1beta2", 
  Group = 0xc4201b21a0 "apps", 
  InlineDefinition = {
    array = 0x0, 
    len = 0, 
    cap = 0
  }, 
  DescriptionWarning = 0x0 "", 
  DescriptionNote = 0x0 "", 
  ConceptGuide = 0x0 "", 
  RelatedTasks = {
    array = 0x0, 
    len = 0, 
    cap = 0
  }, 
  IncludeDescription = 0x0 "", 
  LinkToMd = 0x0 "", 
  Definition = 0x0
}`

(gdb) `p *(config.ResourceCategories.array[1].Resources.array[2])`

$28 = {
  Name = 0xc4201b23f8 "Service", 
  Version = 0xc4201b2410 "v1", 
  Group = 0xc4201b2420 "core", 
  InlineDefinition = {
    array = 0x0, 
    len = 0, 
    cap = 0
  }, 
  DescriptionWarning = 0x0 "", 
  DescriptionNote = 0x0 "", 
  ConceptGuide = 0x0 "", 
  RelatedTasks = {
    array = 0x0, 
    len = 0, 
    cap = 0
  }, 
  IncludeDescription = 0x0 "", 
  LinkToMd = 0x0 "", 
  Definition = 0x0
}

(gdb) `p *(config.ResourceCategories.array[2].Resources.array[2])`

$29 = {
  Name = 0xc4202cbf00 "PersistentVolumeClaim", 
  Version = 0xc4201b24d0 "v1", 
  Group = 0xc4201b24e0 "core", 
  InlineDefinition = {
    array = 0x0, 
    len = 0, 
    cap = 0
  }, 
  DescriptionWarning = 0x0 "", 
  DescriptionNote = 0xc420020d90 "A <a href=\"#persistentvolume-v1-core\">PersistentVolume</a> must be allocated in the cluster to use this.", 
  ConceptGuide = 0x0 "", 
  RelatedTasks = {
    array = 0x0, 
    len = 0, 
    cap = 0
  }, 
  IncludeDescription = 0x0 "", 
  LinkToMd = 0x0 "", 
  Definition = 0x0
}

(gdb) **p config.ResourceCategories.array[0].Resources.array**

$30 = (struct github.com/kubernetes-incubator/reference-docs/gen-apidocs/generators/api.Resource **) 0xc4200663c0
(gdb) p config.ResourceCategories.array[0].Resources
$31 = {
  array = 0xc4200663c0, 
  len = 9, 
  cap = 9
}
