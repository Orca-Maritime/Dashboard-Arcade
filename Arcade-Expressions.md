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

### Ground Truth


#### *Serial Number - MK18*
```
var sn = $feature["sn_case"];
var result = IIF(IsEmpty(sn) == True, 'N/A', sn);
return result
```

#### *MK5 Compatiable - MK18*
```
var mk5 = $feature.mk5;
var result = IIf(mk5 == 'X', 'Yes', 'No');
return result
```

#### *MAG - MK18*
```
var mag = $feature.mag;
var result = WHEN(
    mag == 'NO', 'No',
    mag == 'YES', 'Yes',
    'No');
    
return result
```

#### *Report Date - MK18*
```
var diversLog = $feature.diverslog;
var result = Replace(diversLog, '-', '/');
return result
```

#### *Water Depth - MK18*
```
var wdm = round($feature.h2o_dep_m, 1);
var wdf = round($feature.h2o_dep_ft);
var result = wdf + " (ft)/" + wdm + " (m)";
return result
```

#### *Tether Length - MK18*
```
var tlm = round($feature.tether_m, 1) ;
var tlf = $feature.tether_ft;
var mineType = $feature.mine_type;
var result = When(
mineType == 'Bottom', 'N/A',
mineType == 'Moored', tlf + " (ft)/" + tlm + " (m)",
'N/A');
return result
```

#### *Case Depth - MK18*
```
var cdm = round($feature.case_dep_m, 1);
var cdf = $feature.case_dep_f;
var mineType = $feature.mine_type;
var result = When(
mineType == 'Bottom', 'N/A',
mineType == 'Moored', cdf + " (ft)/" + cdm + " (m)",
'N/A');
return result
```

#### *Case Altitude - MK18*
```
var cam = round($feature.case_alt_m,1);
var caf = $feature.case_alt_f;
var mineType = $feature.mine_type;
var result = When(
mineType == 'Bottom', 'N/A',
mineType == 'Moored', caf + " (ft)/" + cam + " (m)",
'N/A');
return result
```

### Sonar Footprints

#### *Download SHP - SF*
```
var dwn = $feature["down_shp"];
var result = IIF(isEmpty(dwn) == True, 'Download Unavailable', "Download SHP");
return result
```

#### *Download GeoTiff - SF*
```
var dwn = $feature["down_tif"];
var result = IIF(isEmpty(dwn) == True, 'Download Unavailable', "Download GeoTiff");
return result
```

#### *Mailto - SF*
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

#### *Year - SF*
```
var yearText = Text($feature.year);
var result = replace(yearText, ',', '');
return result
```

#### *Date - SF (San Diego)*
```
var d = $feature.date;
var utc = toUTC(d);
var date_text = Text(utc, "M/D/Y");
return date_text
```

### Contacts & Known Features

#### *ROV Timestamp - C&KF*
```
var rov = $feature["rov_timest"];
var empty = IsEmpty(rov);
var result = when(
    empty == True, 'N/A',
    rov == " ", 'N/A',
    rov);
return result
```

#### *AUV Timestamp - C&KF*
```
var auv = $feature["auv_timest"];
var empty = IsEmpty(auv);
var result = when(
    empty == True, 'N/A',
    auv == " ", 'N/A',
    auv);
return result
```

#### *Training Field - C&KF*
```
var trainingField = DomainName($feature,"field");
var result = IIF(trainingField == "NO DESIGNATION", 'No Designation', trainingField);
return result
```

#### *Water Depth - C&KF*
```
var meters = round($feature["depth__m_"], 1);
var feet = round((meters * 3.28084), 0);
var result = When(
    meters == 0, 'Unknown',
    IsEmpty(meters) == True, 'Unkown',
    feet + " (ft)/" + meters + " (m)");
return result
```
Ted