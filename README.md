![MIKES DATA WORK GIT REPO](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_01.png "Mikes Data Work")        

# Find SQL Tables With Heavily Fragmented Indexes With SQL
**Post Date: March 30, 2015**        



## Contents    
- [About Process](##About-Process)  
- [SQL Logic](#SQL-Logic)  
- [Build Info](#Build-Info)  
- [Author](#Author)  
- [License](#License)       

## About-Process

<p>Here's quick way to find Tables that have heavily fragmented indexes. This is designed to find tables that are above 70% fragmentation. It's a good idea to incorporate this into a regularly scheduled maintenance job, and just REBUILD those that are above 70% to 80% fragmentation. Anything below this point can simply be REORGANIZED.</p>   


## SQL-Logic
```SQL
select
'database_name' = db_name(sddips.database_id)
,   'table_name' = object_name(sddips.object_id)
,   'object type' = ist.table_type
,   'fragmentation' = left(sddips.avg_fragmentation_in_percent, 4) from
sys.dm_db_index_physical_stats (db_id(), null, null, null, null) sddips
join information_schema.TABLES ist on object_name(sddips.object_id) = ist.table_name where
ist.table_type = 'base table' and sddips.avg_fragmentation_in_percent &gt; 70 order by
sddips.avg_fragmentation_in_percent desc;

```

[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

[![Gist](https://img.shields.io/badge/Gist-MikesDataWork-<COLOR>.svg)](https://gist.github.com/mikesdatawork)
[![Twitter](https://img.shields.io/badge/Twitter-MikesDataWork-<COLOR>.svg)](https://twitter.com/mikesdatawork)
[![Wordpress](https://img.shields.io/badge/Wordpress-MikesDataWork-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)


## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Mikes Data Work](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_02.png "Mikes Data Work")

