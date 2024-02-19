---
title: "[Current Project] - Using OCR for validating RMF Boundary Diagrams - Python"
excerpt: ""
classes: wide

gallery:
  - url: /assets/images/RMF/Perfect.PNG
    image_path: /assets/images/RMF/Perfect.PNG
    alt: "perfect"
    title: "Perfect List"
  - url: /assets/images/RMF/NotPerfect.PNG
    image_path: /assets/images/RMF/NotPerfect.PNG
    alt: "notperfect"
    title: "Not a Perfect List"
  - url: /assets/images/RMF/MissingDeviceList.PNG
    image_path: /assets/images/RMF/MissingDeviceList.PNG
    alt: "missingdevicelist"
    title: "Nissing Devices from List"
  - url: /assets/images/RMF/MissingDeviceDiagram.PNG
    image_path: /assets/images/RMF/MissingDeviceDiagram.PNG
    alt: "missingdevicediagram"
    title: "Missing Devices from diagram"
---

# Page under construction...

# NAVY RMF
The Navy Risk Management Framework (RMF) is a structured approach aimed at managing cybersecurity risks within information systems. The process encompasses system identification, categorization based on impact levels, and the selection and implementation of security controls. Through rigorous assessments, the effectiveness of these controls is evaluated, leading to authorization decisions by an Authorizing Official (AO). Continuous monitoring and documentation are integral parts of the process, ensuring that information systems not only meet security standards but also adapt to evolving threats.

The RMF process emphasizes a commitment to ongoing risk management, periodic assessments, and continuous improvement throughout the lifecycle of information systems. By addressing emerging vulnerabilities and staying aligned with evolving security requirements, the Navy aims to maintain a robust cybersecurity posture in its information systems.


# Boundary/Topology Diagram
The Navy Risk Management Framework (RMF) process, when incorporating boundary diagrams, involves several key steps. Initially, a boundary diagram is created to define the scope and context of the information system. The process starts with system preparation, where the system and its purpose are identified, and the boundary diagram helps establish clear system boundaries.Throughout the Navy RMF process, the boundary diagram serves as a visual aid to ensure a clear understanding of the information system's components, relationships, and interactions. This visual representation contributes to effective risk management and compliance with security standards.

The boundary diagram adheres to a specific standard and is consistently cross-referenced with an asset list. I won't delve into the detailed requirements of the boundary diagram but I will aim to simplify it. This project, functioning as a proof of concept, may seem overly excessive in its application. Nevertheless, it serves as a venture driven by my curiosity and a commitment to refining my skills in Machine Learning.


Most requirements follow the [DISN CPG](https://www.disa.mil/~/media/files/disa/services/disn-connect/references/disn_cpg.pdf), section **E.5**. 

# General Steps
1. Create a simplified Topology Diagram
2. Create an asset
3. Apply OCR in the Topology Diagram
4. Cross Reference result in Asset List.
5. Determine missing data.
6. Add other functionality to verify that the diagram adheres to requirements set forth by DISN CPG.



# Topology Diagram
In this section, I created a sample topology diagram following some requirements in the DISN CPG. In the diagram below, we have 3 external devices, and 4 devices withinn the delineated authorization boundary marked in red. Note that within the boundary, Device names, Manufacturer, Model, OS, and IP Address are clearly expressed. 

<object data="../assets/images/RMF/TopologyDiagram.pdf" width="50%" height="50%" type='application/pdf'></object>

# Asset List 
The next step is to create a sample asset list in excel to depict the devices within the delineated diagram. I will create four different asset list, albeit only differing slighlty: One asset list will be perfect (Test Case 1), another list with a missing row (Test Case 1), another list with incorrect details(Test Case 3), and lastly, a list with extra device not shown in the diagram (Test Case 4). After applying OCR, the four asset list will serve as the reference for testing. 

{% include gallery caption="From Left to right: Perfect List, Not a Perfect List (Values are wrong), Missing Device from List, and Missing Device from Diagram" %}

# A Simple Method  
Since the network topology diagram is (usually) created digitally, then tools such as [pdfminer](https://pypi.org/project/pdfminer/) or [pdfminer.six](https://github.com/pdfminer/pdfminer.six) allows for an easy method to mine text in the pdf file. For example, simply executing commands:
~~~ python
from pdfminer.high_level import extract_text

text = extract_text("example.pdf")
print(text)\
~~~
would give us the all text within the document. The raw mined data is unorganized and the use of find and compare is simple. For example, all text are mined - text outside the delineated boundary are also listed. This means that our raw mined text will be a longer list than our asset list. If we were to map (find and compare) raw text to mined text by brute force, then devices such as "External Device 1" will return as a missing text in the asset list (Recall that the asset list is only for the delineated boundary). However, the inverse is achievable. If we were to compare the asset list to the liat of all devices in the diagram, then Test Case 1, Test Case 2 and Test Case 3 are simple to implement. 

I plan to use pdfminer for this simple implementation. Using an asset list, I will find and compare all Device Name, Manufacturer, etc., to the mined text to check that it does *exist*, not whether it is correct for that particular column. This implementation will be built last due to ease. I plan to first implement a complex method so that we can map the diagram to asset list Using this method allows for better data organization and integrity. Likewise, it will asllows us to be able to create an asset list from the diagram.

# Applying OpenCV in the Topology Diagram  
I aim to divide the diagram into two parts. A snapshot of the devices outside the boundary and another for the device inside the delineated boundary. This will remove the excess raw data of the devices outside the boundary. 

I will be using OpenCV to determine the edges, however, there are some obstacles along the way. 

1) I want the program to be general use, hence, not only should it work for my diagram but also others.
2) Since data flow between boxes (devices) exist, OpenCV will sometimes commit to thinking that it is an edge/contour boundary.
3) Not all boxes are captured or too much are captured.

Below is an example of case (3). In the image below, while not properly using the right parameters, it is easy to capture every possible means openCV captures a "rectangle". Hence, it is essential to find a way to either use multiple imaging processes and/or use better parameters. 
![image](/assets/images/RMF/Figure_1.png)
[under construction]
