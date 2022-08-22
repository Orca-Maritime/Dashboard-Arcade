### Tips & Tricks

Open Preview to the Side (ctrl+K V)

# **ESRI Arcade Expressions**

This Markdown (.md) file will hold all of the Arcade expressions used by Orca Maritime GIS Team.
These code chunks will be able to copy and paste into Arcade Windows.

## **Symbology**

### *MK18 Ground Truth* 

`
var type = $feature.mine_type;
var status = $feature.status;
var result = when(
type == 'Distractor', 'Distractor',
type == 'MLO', 'MLO', 
type == 'Project', 'Project',
status == 'USBL', 'MK18-USBL',
status == 'Plumbed', 'MK18',
status == 'Planned', 'MK18',
'MK18')
return result
`

## **Popups**

### *Download SHP*

### 