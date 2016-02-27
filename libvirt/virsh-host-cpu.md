### List host CPU capabilities using virsh

List host CPU capabilities using `virsh`. This can be useful to pin down the exact functionality you want in your libvirt guests `<cpu>` tags.

```sh
# virsh capabilities | virsh cpu-baseline /dev/stdin
<cpu mode='custom' match='exact'>
  <model fallback='forbid'>IvyBridge</model>
  <vendor>Intel</vendor>
  <feature policy='require' name='invtsc'/>
  <feature policy='require' name='osxsave'/>
  <feature policy='require' name='pcid'/>
  <feature policy='require' name='pdcm'/>
  <feature policy='require' name='xtpr'/>
  <feature policy='require' name='tm2'/>
  <feature policy='require' name='est'/>
  <feature policy='require' name='smx'/>
  <feature policy='require' name='vmx'/>
  <feature policy='require' name='ds_cpl'/>
  <feature policy='require' name='monitor'/>
  <feature policy='require' name='dtes64'/>
  <feature policy='require' name='pbe'/>
  <feature policy='require' name='tm'/>
  <feature policy='require' name='ht'/>
  <feature policy='require' name='ss'/>
  <feature policy='require' name='acpi'/>
  <feature policy='require' name='ds'/>
</cpu>
```

- Source(s)
  - [1](https://kashyapc.fedorapeople.org/virt/openstack/devstack-nvmx.txt)
