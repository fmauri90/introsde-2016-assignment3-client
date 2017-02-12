# Assignment 03: SOAP Web Services

## [Introduction to Service Design and Engineering](https://github.com/IntroSDE) | [University of Trento](http://www.unitn.it/)

# Client

URL of my server: [https://secure-refuge-6052.herokuapp.com/](https://secure-refuge-6052.herokuapp.com/)  
Server repository: [https://github.com/abonte/introsde-2015-assignment-3-sever](https://github.com/abonte/introsde-2015-assignment-3-server)  
I worked alone

### Install
In order to execute the client you need the following technologies (in the brackets you see the version used to develop):

* Java (jdk1.8.0)
* ANT (version 1.9.4)

Then, clone the repository. Run in your terminal:

```
git clone https://github.com/abonte/introsde-2015-assignment-3-client && cd introsde-2015-assignment-3-client
```
### Getting Started
This project use an ant build script to automate the compilation and the execution of specific part of the Java application.  

To run the client:
```
ant execute.client
```

This command performs the following action:
* download and install ivy (dependency manager) and resolve the dependencies. Ivy and WebContent/WEB-INF/lib/ folders are generated;
* run wsimport -keep https://secure-refuge-6052.herokuapp.com/ ;
* create a build directory and compile the code in the src folder. You can find the compiled code in build folder;
* a log file is generated [client.log](client.log);


