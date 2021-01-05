---
title: "Homomorphic Encryption on Mesh smoothing!"
categories:
  - project
  
tags:
  - ODU
  - IEEE
  - cryptography
  - NSF
last_modified_at: 2020-12-08T16:20:02-05:00
---
## Abstract
The development of Fully Homomorphic Encryption (FHE) schemes has generated considerable interest in cryptography. In this paper, we examine the problem of performing a polygonal mesh smoothing on encrypted data. Specifically, we focus on two tasks: developing a polygonal mesh smoothing algorithm under FHE, as well as computing the difference of efficiency of two homomorphic schemes using the identical mesh smoothing algorithm. Due to the high overhead of homomorphic computation, the implementation of the mesh smoothing algorithm was restricted to a naïve Laplacian smoothing approach. We first test low polygons triangular mesh structures on the order of a few thousand vertex points. We construct a working custom implementation of the Laplacian smoothing algorithm that works in both the homomorphic schemes of Cheon-Kim-Kim-Song (CKKS) and Paillier. By taking advantage of CKSS batched computation, we show that it was more efficient than the older Paillier cryptosystem. Lastly, we perform smoothing on encrypted datasets with multiple iterations across the surface of the mesh. By using these methods, we demonstrate the viability of using high-level FHE, not just CKKS, for large scale cloud based mesh smoothing computation and other statistical analysis.



## Objective
+ Examine different schemes and libraries of Fully Homomorphic Encryption. 
+ Evaluate methods of surface smoothing that can be utilize with FHE.
+ Determine a naïve approach of Laplacian smoothing in CKKS and Paillier. 


## Background
+ Only some arithmetic computations can be done with FHE (multiplication and addition). 
+ FHE comes with a high overhead, thus having costly computations.
+ Homomorphic encryption schemes like Paillier has been researched in the use of electronic voting.

![image-center](/assets/images/xxx){: .align-center} // insert image here

## Significance
+ Computations on encrypted data does not forsake privacy that may be identifiable to a user or a client. 
+ Cloud services offer more computation resources that may not be available to a user with a normal and convention PC or network. 
+ Cloud-based data analytics can be achieved using FHE. Information can be sent through a cloud using FHE from various departments and localizations without identifiable records from the clients. 

## General Theory
A mesh object is encrypted using a homomorphic encryption scheme. A naïve Laplacian smoothing is implemented at (b) when the data is encrypted using homomorphic encryption. The decrypted mesh (c) should have noticeable smoothen difference than the original.

#### insert image here 
*A naïve Laplacian smoothing is implemented at (b) when the data is encrypted using homomorphic encryption. The decrypted mesh (c) should have noticeable smoothen difference than the original.*


## Softwares and Tools
### CKKS
Cheon-Kim-Kim-Song or CKKS is type of scheme introduced in Microsoft SEAL. Unlike BFV, CKKS can handle real numbers with deep approximate computations (floating-point values). CKKS also offers to batch of vectors using SIMD. In this project, we focused on the usage of CKKS due to the real number application. Vertex points are represented in floating-point numbers and not integers, which would use the BFV schema instead. It is possible to use the BFV schema instead, but it would require multiplying the floating-point values by a fixed degree to create an integer value (i.e .001 x 1000 = 1). However, this would result in more computations to be done within thousands and thousands of vertex points.  

### PAILLIER CRYPTOSYSTEM
Paillier cryptosystem is another schema developed for homomorphic encryption. Compared to the CKKS scheme, the Paillier cryptosystem does not have SIMD for efficient computation. Several research studies have employed Paillier cryptosystem into various applications. For instance, a research study examined the use of Paillier with electronic voting . Paillier is homomorphic only in addition (two ciphertext can be added unbounded) and multiplication (plaintext constant with a ciphertext). For this research, we encrypted the values sequentially and followed an identical smoothing algorithm used in the plaintext control. The Laplacian algorithm functions as intended for the Paillier cryptosystem due to the use of only ciphertext addition and constant multiplication. 

### OPENMESH
In conjunction with using Paillier and SEAL, this paper used the OpenMesh software library to read in mesh file formats that are either in PLY, OFF, OBJ, STL, and other extensions. This advantage allows us to be able to be universal in applying our smoothing algorithm. However, we controlled the experiment under STL objects. 

> IEEE preprinted version. 
