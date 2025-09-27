# nifuzzer
nifuzzer is a tool for generating payloads using the ABNF grammar, which is used in RFC to describe various data types and structures. It is possible to add individual parts of a complex rule so that they are tracked when generating values. This tool can be used as an add-on, pre-generation element for your fuzzer or an existing fuzzer.

### Install
You need to install requirements.txt so that the tool can work
```
pip3 install -r requirements.txt
```

### Usage
Python version 3 is required to run the tool. To run help, enter
```
python3 pre_fuzz.py -h
```
To easily generate 1000 values of the URI rule according to RFC 3986, enter
```
python3 pre_fuzz.py -r 3986 -f URI -c 1000
```
The generated values by default will be in the 'fuzz.json' file. To change the output file, enter
```
python3 pre_fuzz.py -r 3986 -f URI -c 1000 -o rfc3986
```
To generate values that track individual parts of the rule, enter
```
python3 pre_fuzz.py -r 3986 -f URI -c 1000 -p scheme,userinfo,host,port,path,query,fragment
```

### Test
The tool was tested using libraries for validating and parsing URL-addresses of the following programming languages:
* [Python](test/python/)
* [Go](test/golang/)
* [Java](test/java/)
* [NodeJS](test/nodejs/)
* [PHP](test/php/)
* [Perl](test/perl/)
* [Ruby](test/ruby/)

##### Results
The results of testing the validation libraries are shown in the first figure. The second figure shows the average validation value for each programming language. It can be seen that valid payloads are generated, which reduces the chance that these tool-generated values ​​will be useless, meaning they won't even reach the core software functions without passing the validation check.
![](https://github.com/inechakhin/nifuzzer/tree/main/test/charts/val_res.png)
![](https://github.com/inechakhin/nifuzzer/tree/main/test/charts/avg_val_res.png)

The results of testing the parsing libraries are shown in the third figure. It's clear that a variety of input data is generated, allowing us to find many different places in the program that trigger interesting behavior.
![](https://github.com/inechakhin/nifuzzer/tree/main/test/charts/pars_res.png)