# The Case for a Network Calculus Heuristic: Using Insights from Data for Tighter Bounds

This repository contains the dataset used for the paper [_"The Case for a Network Calculus Heuristic: Using Insights from Data for Tighter Bounds"_](https://dx.doi.org/10.1109/ITC30.2018.10060) published at the [2018 International Workshop on Network Calculus and Applications (NetCal 2018)](https://itc30.org/en/workshops/netcal.html). We refer to the paper for a full explanation of the methodology used for generating the dataset.


## Reading the dataset

The dataset is split in two files:

- `dataset_itc30nc.networks.pb.gz` describes the network of servers with their rate and latency parameter, and the flows with their path, and their rate and burst parameters.
- `dataset_itc30nc.results.pb.gz` contains numerical evaluations of the networks using [DiscoDNC v2.4.0](https://github.com/NetCal/DiscoDNC).

Each file is encoded using [Protocol Buffers](https://developers.google.com/protocol-buffers/). The data structure is defined in `dataset_itc30nc.proto` and can be compiled to various target languages (e.g. Java, Python, Objective-C, and C++) using the `protoc` command line utility.

### Example code in python

We first compile the `.proto` file to python:

```
$ sudo apt install python3-protobuf
$ git clone https://github.com/fabgeyer/dataset-itc30nc
$ cd dataset-itc30nc
$ protoc --python_out=. dataset_itc30nc.proto
```

The following script can then be used for reading the data:

```python
import gzip
import dataset_itc30nc_pb2 as pb2

def parse(filename_networks, filename_results):
	networks = pb2.Dataset()
	with gzip.open(filename_networks, 'rb') as fhandle:
		networks.ParseFromString(fhandle.read())
	print(networks)
	
	results = pb2.Results()
	with gzip.open(filename_results, 'rb') as fhandle:
		results.ParseFromString(fhandle.read())
```


## Citation

If you use this dataset for your research, please include the following reference in any resulting publication:

```bibtex
@inproceedings{Geyer_ITC30NC,
	author    = {Geyer, Fabien and Carle, Georg},
	title     = {{The Case for a Network Calculus Heuristic: Using Insights from Data for Tighter Bounds}},
	booktitle = {Proceedings of the 2018 International Workshop on Network Calculus and Applications},
	year      = {2018},
	month     = sep,
	address   = {Vienna, Austria},
	doi       = {10.1109/ITC30.2018.10060},
}
```

## License

The data in this repository is licensed under [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/).
