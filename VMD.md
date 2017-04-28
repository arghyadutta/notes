# VMD reference
```vmd
topo readlammpsdata file.extension molecular
vmd > pbc box
vmd > pbc wrap -compound residue  
Info) 100.0% complete (frame 0)
vmd > pbc box -cemter com
error: pbcbox: unknown option: -cemter
vmd > pbc box -center com

```
