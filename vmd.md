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
Guides available on the internet:
http://pappulab.wustl.edu/~alex/vmd_guide.pdf
http://pages.jh.edu/pfleming/compbio/files/vmd-tutorial.pdf
http://www.sas.upenn.edu/~robertjo/html-physics/vmd/VMD%20User%20Guide.pdf
