---
title: 'HDF5 - 강력한 데이터저장 방식'
date: '2017-1-4 10:00'
layout: post
published: true
---

HDF5는 데이터를 저장하고 관리하기 위한 모델, 라이브러리, 파일형식이다. 제한없이 다양한 형태의 데이터형을 지원하여 복잡한 대규모 데이터에 대한 유연하고 효과적인 입출력을 위해서 고안되었다.

```python
#
# This example creates an HDF5 file compound.h5 and an empty datasets /DSC in it.
#
import h5py
import numpy as np
#
# Create a new file using default properties.
#
file = h5py.File('compound.h5','w')
#
# Create a dataset under the Root group.
#
comp_type = np.dtype([('Orbit', 'i'), ('Location', np.str_, 6), ('Temperature (F)', 'f8'), ('Pressure (inHg)', 'f8')])
dataset = file.create_dataset("DSC",(4,), comp_type)
data = np.array([(1153, "Sun   ", 53.23, 24.57), (1184, "Moon  ", 55.12, 22.95), (1027, "Venus ", 103.55, 31.23), (1313, "Mars  ", 1252.89, 84.11)], dtype = comp_type)
dataset[...] = data
#
# Close the file before exiting
#
file.close()
file = h5py.File('compound.h5', 'r')
dataset = file["DSC"]
print "Reading Orbit and Location fields..."
orbit = dataset['Orbit']
print "Orbit: ", orbit
location = dataset['Location']
print "Location: ", location
data = dataset[...]
print "Reading all records:"
print data
print "Second element of the third record:", dataset[2, 'Location']
file.close()
```


