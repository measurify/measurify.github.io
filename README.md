A **cloud-based, abstract, measurement-oriented API** for managing smart things in IoT ecosystems. Measurify (formerly called Atmosphere IoT Framework [1]) focus on the concept of **measurement**, as this type of data is very common in IoT, which makes it easier and more effective the process of abstraction needed to target different domains and operational contexts.

We tested the framework and its workflow in **three industrial research projects** analyzing data and enabling new services in the health and automotive domains. Our experience showed the benefits – especially in terms of **development efficiency and effectiveness** - of exploiting Measurify, which does not tie the development to a proprietary commercial platform, nor requires the huge set-up times needed to start from scratch a solution. Furthermore, customizing Measurify based on new requirements has proven to be easily feasible, also keeping abstraction for reusability.

Measurify ia a project designed, developed and maintained by **[Elios Lab](https://elios.diten.unige.it/)** of University of Genoa. **[Wondertech](http://www.wondertechweb.com/)** contributes to the development and maintenance of the source code.

In order to support the IoT developer community, Measurify is released open source under **MIT licence**.

## Table of contents

1. [Main Concepts](#main-concepts)
2. [Use cases](#use-cases)
3. [References](#references)

## Main concepts

Measurify was designed to represent the application context and its elements as interrelated software objects, onto which to build applications. These objects are modeled as **resources**, with own models and functionalities, accessible through a set of RESTful API interface.

At the core of these resources are the essential elements that are common in the IoT environment: **Thing, Feature, Device, and Measurement**: a Thing represents the subject of a Measurement; a Feature describes the (typically physical) quantitity measured by a Device; each item in a Feature has a name and a unit; a Device is a tool providing Measurements regarding a Thing; finally, a Measurement represents a value of a Feature measured by a Device for a specific Thing. The following figure shows the relations among resources, highlighting the central role of the Measurement concept. The figure provides also a simple example in the context of collecting weather information (e.g. temperature and wind speed).

![Resources relations focusing around the Measurement resource](images/figure1.png?raw=true "Figure 1")

The concept of Measurement **abstracts the values posted to and retrieved from the Cloud**. Its structure must match the type of measured Feature. Each measurement is a **vector of samples**. They could be samples collected at different times (taken at intervals specified by the “delta” field), a single value or a set of statistical information (e.g., average, stdev, etc.). Each sample can be a **scalar** (e.g. a temperature), a **vector** (e.g. the orientation in space) or a **tensor** of numbers (e.g., general multidimensional data points). In the previous example, we have just a single scalar sample for the Measurement.

The Feature resource is used to validate the value array of each received measurement. This is shown in the previous figure, where the attributes "type" and "dimension" (0 for scalar, 1 for vectors, 2 for tensors) from the Feature resource must match the Sample's value array type and its depth, respectively.

Other supplementary resources are **User, Log, Login, Script, Tag, Constraint, and Computation**.

For a detailed description of each resource, please refere to [API Swagger Doc](https://github.com/measurify/server)

## Use cases

Atmosphere has been employed in three industrial research projects, one in the health/smart home sector and two in automotive that has put Atmosphere in challenging experimentation set-ups, with different settings.

### Hi-Drive

[Hi-Drive](https://www.hi-drive.eu/) **EU-funded Hi-Drive** will push automated driving further towards high automation. The goal is to make driving automation robust and reliable by taking intelligent vehicle technologies to conditions and scenarios neither extensively tested nor demonstrated earlier in European and overseas traffic. Hi-Drive addresses a number of key challenges which are currently hindering the progress of developments in vehicle automation. The project’s ambition is to considerably extend the operational design domain from the present situation, which frequently demands interventions from the human driver. With these aims, Hi-Drive associates a consortium of 41 European partners covering the main impact areas which affect users and the transport system, and enhance societal benefits. The project work includes outreach activities on business innovation and standardisation. Measurify provides shared data storage back-end [2] [3] [4].

### L3Pilot

[L3Pilot](https://www.l3pilot.eu/) is a **Horizon 2020 research project** aimed at assessing the impact of automated driving (AD) on public roads, testing the Society of Automotive Engineers (SAE) Level 3 (and some Level 4) functions. The pilots will involve 1,000 test subjects, 100 cars, by 12 vehicle owners (either Original Equipment Manufacturers, or suppliers), across 10 European countries. The project uses the Field opErational teST support Action (FESTA) methodology, driven by a set of research questions and hypotheses on technical aspects, user acceptance, driving and travel behavior, as well as the impact on traffic and safety. In order to answer such research questions, the project has defined a data toolchain (now available open-source), that translates the proprietary vehicular signals to a shared format, and processes them to extract the driving scenario (e.g., “lane change”, “cut-in”) and other event information. Filtered data, aggregated from all the pilot sites, will be analyzed for an overall impact assessment. Atmosphere provides shared data storage back-end [5] [6].

### Fabric

[Fabric](https://www.fabric-project.eu/www.fabric-project.eu/index.html) is **7th Framework Programme European industrial research project** which implemented an on-road testbed for  Dynamic Wireless Charging (DWC) of electrical vehicles [7]. In this context, we realized a charging process metering service for the vehicles passing through the charging lane [8]. The system senses and computes on the edge information about the charging process and stores it on Atmosphere’s cloud server to support new electro-mobility (e-mobility) services (e.g., billing, energy-aware car navigation) which can be implemented by relevant companies (e.g., energy providers, navigation providers). The road-side DWC sub-system sends to Atmosphere data representing the state of each consecutive charging grid. The vehicle-side DWC subsystem generates a stream of measurements recording the vehicle-coil alignment (which is key to power transfer efficiency) and the charging parameters and battery status.

### Health at Home (H@H)

[H@H]() is a research project funded by the **Italian Ministry of Education and Research (MIUR)** and aimed at supporting the elderly with Chronic Health Failure (CHF) [9]. The project developed a complete IoT Cloud service consisting of the Home Monitoring Sensor System (front-end), the Home Gateway (middleware), and a Remote Cloud (back-end). Through the Gateway, several physiological quantities (electrocardiogram signal, heart rate, breathing waveform, breathing rate, oxygen saturation, blood pressure, glycemia, etc.) are collected and provided to the cloud. Through a web-based user interface, a clinician can view the measurements, and modify the pharmacological therapy according to the symptoms. Atmosphere acted as the backbone of the application in order to implement the H@H API described in [10].

## References

[1] R. Berta, A.  Kobeissi, F. Bellotti, A. De Gloria. **Atmosphere, an Open Source Measurement-Oriented Data Framework for IoT**. IEEE Transactions on Industrial Informatics. 2020. [LINK](https://doi.org/10.1109/TII.2020.2994414)

[2] M. Fresta, A. Capello, F. Bellotti, L. Lazzaroni, M. Cossu, R. Berta. **Supporting a .csv-based Workflow in MongoDB for Data Analysts**. 32nd IEEE International Symposium on Industrial Electronics, Helsinki, Finland, 2023. [LINK](https://doi.org/10.1109/ISIE51358.2023.10228044)

[3] M. Fresta, F Bellotti, A. Capello, M. Cossu, L. Lazzaroni, A. De Gloria, R. Berta. **Efficient Uploading of.Csv Datasets into a Non-Relational Database Management System**.  Applications in Electronics Pervading Industry, Environment and Society. ApplePies 2022. Lecture Notes in Electrical Engineering, vol 1036. Springer, Cham. [LINK](https://doi.org/10.1007/978-3-031-30333-3_2)

[4] A. Capello, M. Fresta, F. Bellotti, H. Haghighi, J. Hiller, S. Mozaffari, R. Berta. **Exploiting Big Data for Experiment Reporting: The Hi-Drive Collaborative Research Project Case**. Sensors, Vol. 23, No. 18, September 2023 [LINK](https://doi.org/10.3390/s23187866)

[5] J. Hiller, S. Koskinen, R. Berta, M. Osman, B. Nagy, F. Bellotti, A. Rahman, E. Svanberg, H. Weber, E. H. Arnold, M. Dianati, A. De Gloria. **The L3Pilot data management toolchain for a level 3 vehicle automation pilot**. Electronics. Vol. 9, No. 5, May 2020 [LINK](https://doi.org/10.3390/electronics9050809)

[6] F. Bellotti, R. Berta, A. Kobeissi, N. Osman, E. Arnold, M. Dianati, B. Nagy, A. De Gloria, **Designing an IoT Framework for Automated Driving Impact Analysis**, 30th IEEE Intelligent Vehicle Symposium, Paris, June 2019 [LINK](https://doi.org/10.1109/IVS.2019.8813989)

[7] A. Kobeissi, F. Bellotti, R. Berta, and A. De Gloria, **Towards an IoT-enabled Dynamic Wireless Charging Metering Service for Electrical Vehicles**, 4th AEIT International Conference of Electric and Electronic Technologies for Automotive, Turin, Italy, 2019 [LINK](https://doi.org/10.23919/EETA.2019.8804571)

[8] V. Cirimele, M. Diana, F. Bellotti, R. Berta, A. Kobeissi, N. El Sayyed, J. Colussi, A. La Ganga, P. Guglielmi, and A. De Gloria, **The Fabric ICT platform for managing Wireless Dynamic Charging Road lanes**, IEEE Transactions on Vehicular Technology (IEEE TVT), Vol. 69, No. 3, March 2020. [LINK](https://doi.org/10.1109/TVT.2020.2968211)

[9] L. Pescosolido, R. Berta, L. Scalise, G. M. Revel, A. De Gloria and G. Orlandi, **An IoT-inspired cloud-based web service architecture for e-Health applications**, 2016 IEEE International Smart Cities Conference (ISC2), Trento, 2016, pp. 1-4 [LINK](https://doi.org/10.1109/ISC2.2016.07580759)

[10] A. Monteriù, M.R. Prist, E. Frontoni, S. Longhi, F. Pietroni, S. Casacci, L. Scalise, A. Cenci, L. Romeo, R. Berta, L. Pescosolido, G. Orlandi, G.M. Revel, **A smart sensing architecture for domestic monitoring: methodological approach and experimental validation**, Sensors, Vol. 18, No. 7, July 2018 [LINK](https://doi.org/10.3390/s18072310)

[11] M. Fresta, A. Dabbous, F. Bellotti, A. Capello, L. Lazzaroni, A. Pighetti, R. Berta.
 **Low-Cost, Edge-Cloud, End-to-End System Architecture for Human Activity Data Collection**. Applications in Electronics Pervading Industry, Environment and Society. ApplePies 2023. Lecture Notes in Electrical Engineering, vol 1110. Springer, Cham. [LINK](https://doi.org/10.1007/978-3-031-48121-5_64)

[12] A. Dabbous, M. Fresta, F. Bellotti, R. Berta. **Arduino Nano-based System for Tennis Shot Classification**. 54th Annual Meeting of the Italian Electronics Society, SIE 2023, Noto, Italy, 2023. [LINK](https://doi.org/10.1007/978-3-031-48711-8_43)