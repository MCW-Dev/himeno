# HIMENO Benchmark
The Himeno benchmark [1] version 3.0 is a test program measuring the cpu performance in MFLOPS.Point-Jacobi method is employed in this Pressure Poisson equation solver as this method can be easily vectorized and be parallelized.

The size of this kernel benchmark can be choosen from the following sets of 
 ```
 [mimax][mjmax][mkmax]:
 small : 33,33,65
 small : 65,65,129
 midium: 129,129,257
 large : 257,257,513
 ext.large: 513,513,1025
 ```

# How to run:
### Compilation :
`cc himenobmtxpa.c -O3  -mavx2 -o himenobmtxpa`
#### Note:
Include the CFLAG -mavx2 only if the machine provides AVX2 support (To check AVX2 support use the command : `grep avx2 /proc/cpuinfo` )
### Execution :
`himenobmtxpa s`

# Modification
* A slight change have been made to the original code: `The method to create an array`
* In the original version an array is created dynamically using a single pointer and uses the Macro to access data. 
* In the modified version, an Array is created also dynamically using a pointer to a triple pointer and this makes the access of data quicker than in the original version
* This difference improves the score ultimately
* The results obtained with the original version can be compared with the one obtained with this version, because no kernel of the code from the original version is changed
* The blog[2] had also tried the same but for the version 2.0 with openmp parallelization. The kernel dimensions and also the method to declare Array have been changed in version 3.0 from version 2.0

# References
[1] http://accc.riken.jp/en/supercom/himenobmt, download at http://accc.riken.jp/en/supercom/himenobmt/download/98-source/
[2] https://blogs.fau.de/hager/archives/7850
