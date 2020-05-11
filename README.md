A **cloud-based, abstract, measurement-oriented API** for managing smart things in IoT ecosystems. Measurify focus on the concept of **measurement**, as this type of data is very common in IoT, which makes it easier and more effective the process of abstraction needed to target different domains and operational contexts.

We tested the framework and its workflow in **three industrial research projects** analyzing data and enabling new services in the health and automotive domains. Our experience showed the benefits – especially in terms of **development efficiency and effectiveness** - of exploiting Measurify, which does not tie the development to a proprietary commercial platform, nor requires the huge set-up times needed to start from scratch a solution. Furthermore, customizing Measurify based on new requirements has proven to be easily feasible, also keeping abstraction for reusability.

Measurify ia a project designed, developed and maintained by **[Elios Lab](https://elios.diten.unige.it/)** of University of Genoa. **[Wondertech](http://www.wondertechweb.com/)** contributes to the development and maintenance of the source code.

In order to support the IoT developer community, Measurify is released open source under **MIT licence**.

## Table of contents

1. [Main Concepts](#main-concepts)
2. [Getting Started](#getting-started)
3. [Use cases](#use-cases)
4. [References](#references)

## Main concepts

Measurify was designed to represent the application context and its elements as interrelated software objects, onto which to build applications. These objects are modeled as **resources**, with own models and functionalities, accessible through a set of RESTful API interface.

At the core of these resources are the essential elements that are common in the IoT environment: **Thing, Feature, Device, and Measurement**: a Thing represents the subject of a Measurement; a Feature describes the (typically physical) quantitity measured by a Device; each item in a Feature has a name and a unit; a Device is a tool providing Measurements regarding a Thing; finally, a Measurement represents a value of a Feature measured by a Device for a specific Thing. The following figure shows the relations among resources, highlighting the central role of the Measurement concept. The figure provides also a simple example in the context of collecting weather information (e.g. temperature and wind speed).

![Resources relations focusing around the Measurement resource](images/figure1.png?raw=true "Figure 1")

The concept of Measurement **abstracts the values posted to and retrieved from the Cloud**. Its structure must match the type of measured Feature. Each measurement is a **vector of samples**. They could be samples collected at different times (taken at intervals specified by the “delta” field), a single value or a set of statistical information (e.g., average, stdev, etc.). Each sample can be a **scalar** (e.g. a temperature), a **vector** (e.g. the orientation in space) or a **tensor** of numbers (e.g., general multidimensional data points). In the previous example, we have just a single scalar sample for the Measurement.

The Feature resource is used to validate the value array of each received measurement. This is shown in the previous figure, where the attributes "type" and "dimension" (0 for scalar, 1 for vectors, 2 for tensors) from the Feature resource must match the Sample's value array type and its depth, respectively.

Other supplementary resources are **User, Log, Login, Script, Tag, Constraint, and Computation**.

For a detailed description of each resource, please refere to [API Swagger Doc](TBD)

## Quick start

Clone code and run the container

    git clone https://github.com/Atmosphere-IoT-Framework/api
    docker-compose up 

## Use cases

Atmosphere has been employed in three industrial research projects, one in the health/smart home sector and two in automotive that has put Atmosphere in challenging experimentation set-ups, with different settings.

### Health at Home (H@H)

[H@H]() is a research project funded by the **Italian Ministry of Education and Research (MIUR)** and aimed at supporting the elderly with Chronic Health Failure (CHF) [1]. The project developed a complete IoT Cloud service consisting of the Home Monitoring Sensor System (front-end), the Home Gateway (middleware), and a Remote Cloud (back-end). Through the Gateway, several physiological quantities (electrocardiogram signal, heart rate, breathing waveform, breathing rate, oxygen saturation, blood pressure, glycemia, etc.) are collected and provided to the cloud. Through a web-based user interface, a clinician can view the measurements, and modify the pharmacological therapy according to the symptoms. Atmosphere acted as the backbone of the application in order to implement the H@H API described in [2].  

### Fabric

[Fabric](https://www.fabric-project.eu/www.fabric-project.eu/index.html) is **7th Framework Programme European industrial research project** which implemented an on-road testbed for  Dynamic Wireless Charging (DWC) of electrical vehicles [3]. In this context, we realized a charging process metering service for the vehicles passing through the charging lane [4]. The system senses and computes on the edge information about the charging process and stores it on Atmosphere’s cloud server to support new electro-mobility (e-mobility) services (e.g., billing, energy-aware car navigation) which can be implemented by relevant companies (e.g., energy providers, navigation providers). The road-side DWC sub-system sends to Atmosphere data representing the state of each consecutive charging grid. The vehicle-side DWC subsystem generates a stream of measurements recording the vehicle-coil alignment (which is key to power transfer efficiency) and the charging parameters and battery status.

### L3Pilot

[L3Pilot](https://www.l3pilot.eu/) is a **Horizon 2020 research project** aimed at assessing the impact of automated driving (AD) on public roads, testing the Society of Automotive Engineers (SAE) Level 3 (and some Level 4) functions. The pilots will involve 1,000 test subjects, 100 cars, by 12 vehicle owners (either Original Equipment Manufacturers, or suppliers), across 10 European countries. The project uses the Field opErational teST support Action (FESTA) methodology, driven by a set of research questions and hypotheses on technical aspects, user acceptance, driving and travel behavior, as well as the impact on traffic and safety. In order to answer such research questions, the project has defined a data toolchain (now available open-source), that translates the proprietary vehicular signals to a shared format, and processes them to extract the driving scenario (e.g., “lane change”, “cut-in”) and other event information. Filtered data, aggregated from all the pilot sites, will be analyzed for an overall impact assessment. Atmosphere provides shared data storage back-end [5].

## References

[1] A. Monteriù, M.R. Prist, E. Frontoni, S. Longhi, F. Pietroni, S. Casacci, L. Scalise, A. Cenci, L. Romeo, R. Berta, L. Pescosolido, G. Orlandi, G.M. Revel, **A smart sensing architecture for domestic monitoring: methodological approach and experimental validation**, Sensors, Vol. 18 Issue 7, July 2018

[2] L. Pescosolido, R. Berta, L. Scalise, G. M. Revel, A. De Gloria and G. Orlandi, **An IoT-inspired cloud-based web service architecture for e-Health applications**, 2016 IEEE International Smart Cities Conference (ISC2), Trento, 2016, pp. 1-4

[3] V. Cirimele, M. Diana, F. Bellotti, R. Berta, A. Kobeissi, N. El Sayyed, J. Colussi, A. La Ganga, P. Guglielmi, and A. De Gloria, **The Fabric ICT platform for managing Wireless Dynamic Charging Road lanes**, in press of IEEE Transactions on Vehicular Technology (IEEE TVT), 2019

[4] A. Kobeissi, F. Bellotti, R. Berta, and A. De Gloria, **Towards an IoT-enabled Dynamic Wireless Charging Metering Service for Electrical Vehicles**, 4th AEIT International Conference of Electric and Electronic Technologies for Automotive, Turin, Italy, 2019

[5] F. Bellotti, R. Berta, A. Kobeissi, N. Osman, E. Arnold, M. Dianati, B. Nagy, A. De Gloria, **Designing an IoT Framework for Automated Driving Impact Analysis**, 30th IEEE Intelligent Vehicle Symposium, Paris, June 2019
