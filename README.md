## FX_ReadyToGo


The official repository :  [FuXi](https://github.com/tpys/FuXi/tree/main).


## Installation

The files shall be organized as the following hierarchy:

```plain
├──FuXi_EC
│   ├── short
│   ├── short.onnx
│   ├── medium
│   ├── medium.onnx
│   ├── long
│   ├── long.onnx

├──Input
│   ├── 2023-10-12-06-00.nc --> FuXi model input data generated using the netcf files of ECMWF HRES data


```

1. Install xarray 

```bash
conda install -c conda-forge xarray dask netCDF4 bottleneck
```

2. Install onnxruntime

```bash
pip install -r requirements.txt
```


## Demo

```bash 
python fuxi.py --model model_dir --input input_file --num_steps 20 20 20
```
eg:
```python
python fuxi.py --model FuXi_EC  --input Input/2023-10-12-06-00.nc --num_steps 20 20 20

```

## Data preparation 

The `input.nc` file contains preprocessed data from the origin ERA5 files. The file has a shape of (2, 70, 721, 1440), where the first dimension represents two time steps. The second dimension represents all variable and level combinations, named in the following exact order:

```plain
'Z50', 'Z100', 'Z150', 'Z200', 'Z250', 'Z300', 'Z400', 'Z500', 'Z600', 'Z700', 'Z850', 'Z925', 'Z1000', 
'T50', 'T100', 'T150', 'T200', 'T250', 'T300', 'T400', 'T500', 'T600', 'T700', 'T850', 'T925', 'T1000', 
'U50', 'U100', 'U150', 'U200', 'U250', 'U300', 'U400', 'U500', 'U600', 'U700', 'U850', 'U925', 'U1000', 
'V50', 'V100', 'V150', 'V200', 'V250', 'V300', 'V400', 'V500', 'V600', 'V700', 'V850', 'V925', 'V1000', 
'R50', 'R100', 'R150', 'R200', 'R250', 'R300', 'R400', 'R500', 'R600', 'R700', 'R850', 'R925', 'R1000', 
'T2M', 'U10', 'V10', 'MSL', 'TP'
```

The last five variables ('T2M', 'U10', 'V10', 'MSL', 'TP') are surface variables, while the remaining variables represent atmosphere variables with numbers representing pressure levels.


**_NOTE:_**

- The variable 'Z' represents geopotential and not geopotential height.
- The variable 'TP' represents total precipitation accumulated over a period of 6 hours.