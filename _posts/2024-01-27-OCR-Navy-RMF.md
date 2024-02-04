---
title: "[Current Project] - Using OCR for validating RMF Boundary Diagrams - Python"
excerpt: ""
classes: wide
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
![topology-diagram](assets/images/RMF/TopologyDiagram.pdf)


# Asset List 
The next step is to create a sample asset list in excel to depict the devices within the delineated diagram. I will create three different asset list, albeit only differing slighlty: One asset list will contain all the devices in the diagram, another with one devices missing from the diagram, and another that shows the asset list missing a device shown in the diagram. After applying OCR, the three asset list will serve as the reference for testing. 


