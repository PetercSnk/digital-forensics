# What is Hashing?
Hashing is the process of converting data into a fixed
length string. Data is converted using certain alorithms
called hash functions.

# How Hashing Works
### Input
The input data can be in almost any format such as a
strings, numbers, images, files, or directories.
### Hash Function
In order to convert data into a fixed-length string,
hash functions divide data into equal-sized blocks.
Block sizes will often range between 160 and 512 bits.
For example, the SHA1 hash uses 512 bit blocks, running
this algorithm on 1024 bits of data will divide it into
two blocks where both blocks will be hashed then 
combined.
### Output
The output of a hash function is the hash value, which
should ideally be unique for each input.

# Hashing Properties
### Deterministic
Using the same input data and hashing algorithm should
always result in the same hash value. When two different
inputs have the same hash value this is known as a
collision.
### Computation Speed
An effective hashing algorithm should be able to process
blocks quickly into a hash value.
### Irreversible
Hash functions should make it impossible to recreate the
original data from the hash value.

# Uses
### Detecting Changes in Data
Hashing is an effective method of checking whether two
sets of data are the same. An example of this is checking
whether your downloaded file is the same as the original
by comparing their hash values.
### Privacy
In most cases when storing passwords in a database the
hash value is stored and not the plain text password.
This is useful incase of unauthorised access as the
intruder cannot use these hashed values by themselves.
