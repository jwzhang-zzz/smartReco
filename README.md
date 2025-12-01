# SmartReco
This repository contains a preliminary version of SmartReco, a framework for detecting read-only reentrancy (ROR) vulnerability in Ethereum smart contracts. 
## Structure
|         **Folder**         |                        **Usage**                        |
|:--------------------------:|:-------------------------------------------------------:|
|            data            |         Including DApp builder dataset and ground-truth dataset of read-only reentrancy        |
| smartReco_dynamic_analysis |  Including replay and verfication modules of SmartReco  |
|  smartReco_static_analysis | Including static analysis module of cross-DApp analysis |
## Installation
SmartReco contains 2 parts, and you need to install them respectively.
### SmartReco_dynamic_analysis
SmartReco builds dynamic analysis module based on `ityFuzz` and `Rust`. You first need to install Rust through https://rustup.rs/.

You need to have libssl-dev (OpenSSL) and libz3-dev installed on your system. On Linux, you probably also need to install Clang >= 12.0.0
```
# Ubuntu:
sudo apt install libssl-dev libz3-dev pkg-config cmake build-essential clang
# macOS:
brew install openssl z3
```
Then, you can use cargo to build `smartReco_dynamic_analysis`.
```
cd smartReco_dynamic_analysis
git submodule update --recursive --init
cd cli
cargo build
```
`smartReco_dynamic_analysis` use a local service to send RPC requests and fetch data from Etherscan. You need to install requirements in `proxy`
```
pip install proxy/requirement.txt -r
```
### SmartReco_static_analysis
SmartReco builds static analysis module based on `Python` and `Slither`. You can refer to `requirements` to install all package.
```
pip install requirements -r
```
## Quickstart
### Start Server
Before start detecting smart contracts, you first need to start the local service in `smartReco_dynamic_analysis`.
```
cd smartReco_dynamic_analysis
python proxy/main.py
```
And you will find the local service is running at `127.0.0.1:5003`
### Detect ROR
You can detect ROR by just provide the smart contract address, and SmartReco will automatically detect whether there is ROR vulnerability in the contract.
```
# demo
cd smartReco_static_analysis/code
python smartReco.py -t 0xf1859145906b08c66fb99e167a1406ac00a2079e --etherscan-key xxx # You need to provide at least one etherscan key or the analysis may be terminated due to network issues or limitations imposed by Etherscan.
```
And the result will generate in `record_data\verify\0xf1859145906b08c66fb99e167a1406ac00a2079e` folder

## Citation
If you use **SmartReco** or data in this repository in your research, please cite the following paper:
```bibtex
@inproceedings{smartreco,
  title={SmartReco: Detecting Read-Only Reentrancy via Fine-Grained Cross-DApp Analysis},
  author={Zhang, Jingwen and Zheng, Zibin and Nan, Yuhong and Ye, Mingxi and Ning, Kaiwen and Zhang, Yu and Zhang, Weizhe},
  booktitle={Proceedings of the IEEE/ACM 47th International Conference on Software Engineering},
  pages={1--12},
  year={2025}
}
