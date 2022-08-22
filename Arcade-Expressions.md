### Tips & Tricks

Open Preview to the Side (ctrl+K V)

# **ESRI Arcade Expressions**

This Markdown (.md) file will hold all of the Arcade expressions used by Orca Maritime GIS Team.
These code chunks will be able to copy and paste into Arcade Windows.

## **Symbology**

### *MK18 Ground Truth* 

```
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
```

## **Popups**

### *Download SHP*
```
var dwn = $feature["down_shp"];
var result = IIF(isEmpty(dwn) == True, 'Download Unavailable', "Download SHP");
return result
```

### *Download GeoTiff*
```
var dwn = $feature["down_tif"];
var result = IIF(isEmpty(dwn) == True, 'Download Unavailable', "Download GeoTiff");
return result
```

### *Mailto*
```
var name = $feature.name;
var email = "gis@orcamaritime.com";
var subject = "Request: " + name;
var body = "If requesting more than three files please consolidate all of the mission names to one list in one email. Thank you."
var params = {subject: subject,
              body: body};

var url = "mailto:" + email + "?" + UrlEncode(params);
//url = Replace(url, "TextFormatting.NewLine", "%0D%0A");
return url;
```

### *Year*
```
var yearText = Text($feature.year);
var result = replace(yearText, ',', '');
return result
```
