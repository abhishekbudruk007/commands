# Python 3.9 Installation on Fedora 7.9

#### Reference Links

* https://computingforgeeks.com/install-latest-python-on-centos-linux/ 
                                                                                                                                                                                 
#### Installation of Python on Fedora/Centos 8/Centos 7 

##### Step 1 — Install Python Dependencies

```
sudo yum -y install epel-release
sudo yum -y update
```


*Install required software development tools required to build Python 3.9 on CentOS 8 / CentOS 7:*
  ``` 
  sudo yum groupinstall "Development Tools" -y
   
  sudo yum install openssl-devel libffi-devel bzip2-devel -y
  ```

  *Confirm gcc is available*
  
  ```
    gcc --version
  ```

##### Step 2 — Download latest Python 3.9 Archive

  *Ensure wget is installed*

  ```
    sudo yum install wget -y
  ``` 
  
  *Use wget to download the latest Python 3.9 release.*
```
wget https://www.python.org/ftp/python/3.9.10/Python-3.9.10.tgz
```

*Extract the archive file using tar*
```
tar xvf Python-3.9.10.tgz
``` 
*Switch to the directory created from the file extraction:*
```
cd Python-3.9*/
``` 

##### Step 3 — Install Python 3.9 on Fedora
  
*Run the command below to configure Python installation.*
```
./configure --enable-optimizations
```
*Build Python 3.9 on Fedora*
```
sudo make altinstall
```

##### Step 4 - Check if Python 3.9 is installed on Fedora 
*Run below command to confirm successful installation of Python 3.9*
```
$ python3.9 --version
Python 3.9.10
```

*Pip3.9 must have been installed as well*
```
$ pip3.9 --version
pip 21.2.4 from /usr/local/lib/python3.9/site-packages/pip (python 3.9)
```

*Upgrade Pip*

```
$ /usr/local/bin/python3.9 -m pip install --upgrade pip
```