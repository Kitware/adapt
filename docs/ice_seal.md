
# Monitoring Arctic Mammal Populations
We can consider the case study of [ice seal research](https://www.fisheries.noaa.gov/alaska/marine-mammal-protection/ice-seal-research-alaska) to demonstrate how VIAME-ADAPT integration adds value to the research workflow:

1. The ADAPT graphical user interface (GUI) sets mission metadata and the geospatial regions where data will be collected.
The ADAPT payload is flown on a sUAS, controlling camera settings and synchrozing exposures with intertial navigation system (INS) measurements, to collect images of ice seals. The coherent collection of imagery with INS measurenents along with computer vision processing allows geo-registration of the imagery.
2. After the mission, collected data is automatically uploaded to another computer or data curation server once internet access is available.
3. A biologist uses VIAME's web-based annotation tools to indicate each occurance of a seal in the collected imagery along with providing a classiciations for size and species.
4. These annotations are passed to VIAME's deep-neural-network object-detector training tools to train a model to detect and classify seals within imagery. Due to the geo-registration provided by the ADAPT collection, seal size in meters can be inferred to more-accurately classify seal age and reduce false alarms.
5. The VIAME-trained model is uploaded onto the ADAPT payload, allowing seals to be detected in-flight during the next mission. Images that the detector deems sufficiently unlikely to contain any seals are autonomously removed according to user-specified policies to allow longer flights before saturating onboard storage. When subsequent acquired images overlap in their ground coverage, image-feature tracking is used to track and suppress redundant detections.
6. Once the sUAS returns to base, summary analytics (e.g., numbers and locations of detected seals, seal density per km<sup>2</sup>) are immediately downloaded to help plan ensuing missions.
7. To further refine the accuracy of the seal-detection model, biologists adjudicate selected detections as true or false positives as well as annotate additional imagery where false negatives may be present, looping back to step 4.

![ADAPT Workflow](img/adapt_workflow.png)
