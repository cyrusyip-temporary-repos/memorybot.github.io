---
title: "MATLAB 练习"
---

# MATLAB 练习

## timeSelect

````matlab
clear;clc
filedir = 'D:\datapath\subject01';
filelist = dir(fullfile(filedir, '*.mat'));

for i = 1:numel(filelist)
    filename = filelist(i).name;
    T_indices = strfind(filename, 'T');
    last_T_index = T_indices(end);
    time = str2double(filename(last_T_index+1:last_T_index+6));
    filelist(i).time = time;
end

clearvars -except filelist
time_lower = 123000;
time_upper = 133000;
filtered_filelist = filelist([filelist.time] >= time_lower & [filelist.time] <= time_upper);

````

## findNaN

```matlab
nan_positions = {};

for i = 1:size(statdatas_HG.seens, 1)
    for j = 1:size(statdatas_HG.seens, 2)
        nan_positions{end+1} = find(isnan(statdatas_HG.seens{i, j}));
    end
end

nan_positions = cell2mat(nan_positions);
```

