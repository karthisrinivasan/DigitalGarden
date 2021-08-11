# Magic Layout
[[GM]]
- Box tool
	- Left click -> lower left corner position
	- Right click -> upper right corner
	- Shift+right click -> move by upper right corner
	- Middle click -> copy paint into box

- Commands
	- g -> grid
	- ; -> shift focus  layout -> console, enter after command to return to layout
	- s -> select
	- a / shift+a -> select all (minor difference, not sure)
	- select, then 'what' -> which layers are under the selection
	- 'array xsize ysize' -> grid of copies of selected item

A very common error message in magic is:
> The box isn't in a window on the edit cell.
This means that the box isn't drawn on the layout window where you are trying to invoke some function like painting that depends on the presence of the box. 

A common error message related to the cursor is something like the following:
> Unknown command: 'paint' 'm1' at (460, -11)  
> Did you point to the correct window?
This error message happens because Magic can have more than one layout window present at a time, with different layouts in each, and Magic needs to know definitively _which_ window is the intended recipient of each command.

