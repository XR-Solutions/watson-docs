# Forensic Use
Watson serves as a powerful tool to help crime scene investigators do their job. Designed to streamline and enhance investigative processes, this application combines natural language interaction, heads-up display (HUD) features and extensibility. Whether analyzing crime scenes, examining digital evidence, or reconstructing events, Watson empowers users with innovative capabilities. In the subsequent sections, we'll delve into the specific extensions that make this application indispensable for forensic work.

## On Site Reporting

![Screenshot of the reporting tool](/images/app-screenshots/screenshot-reporting-tool.png)

Forensic work demands precision, efficiency, and meticulous attention to detail. At a crime scene, numerous actions must be taken promptly. However, the sheer volume of tasks can lead to chaos, and critical steps might inadvertently be overlooked. Additionally, time constraints and external pressures further exacerbate the situation. Enter the **Reporting Extension** within Watson, a solution designed to prevent oversight and streamline investigative processes.

**Key Features:**
1. **Prioritization of High-Impact Tasks:** Our app ensures that investigators focus on high-priority actions first. Whether it’s securing evidence, documenting findings, or conducting initial assessments, the app guides forensic officers toward critical tasks.

2. **Real-Time Notetaking:** Imagine a forensic officer noticing something unusual during an examination but lacking the immediate time to investigate further. With our built-in reporting tool, investigators can create location-specific notes. These notes remain visible at all times, serving as reminders to complete necessary actions.

3. **Proximity-Based Reminders:** As the forensic officer approaches the location of an anomaly, the app dynamically displays relevant notes. This proximity-based feature ensures that no crucial steps are forgotten, even amidst the chaos of a crime scene. This feature is shared between different users on the same crime scene. This further enhances collaboration during an investigation.

## Chain of Custody and Evidence
During forensic investigations, acquiring evidence is paramount. However, once evidence is obtained, ensuring its integrity—free from manipulation or contamination—is equally critical. This is where the concepts of Chain of Custody (CoC) and Chain of Evidence (CoE) come into play. 

**CoC** involves meticulously documenting the handling and transfer of evidence. By filling out our specific forms, investigators track who interacted with the evidence, what actions were taken, and when. From the initial securement of evidence to the case’s conclusion, CoC ensures a transparent record of custody.

**CoE** complements CoC by maintaining a chronological trail of evidence-related activities. It encompasses everything from collection and preservation to analysis and presentation. Whether the investigation spans months or even years, CoE ensures the reliability and admissibility of evidence.

> For further details, you can explore this resource: [Chain of Custody and Evidence](https://www.forensicon.nl/chain-of-custody-and-evidence/)

<!-- TODO: screenshot of the RAG tool -->
## Forensic Guidelines (RAG)
In forensic investigations, the proper handling and preservation of evidence are critical. Whether dealing with common types of traces or more specialized materials, established procedures ensure their safekeeping. These protocols are meticulously outlined in the Forensic Operational (FO) standards. Accessible through the secure police database known as KOMPOL, these standards provide comprehensive guidance. 

KOMPOL is not accessible by anyone. Law enforcement professionals can access them via the extranet. Alternatively, investigators can generate a printed reference book containing all the relevat procedures. This physical resource ensures easy access to the FO norms.

**Where Watson comes in to play**

Forensic officers (FOs) must exercise caution when entering a crime scene. Each entry carries the risk of introducing external contamination. To minimize this risk, FOs should limit their movements in and out of the crime scene. However, if a specific procedure slips their mind, they can turn to the Watson assistant. By asking Watson, FOs can quickly retrieve and hear the relevant FO norms, allowing them to continue their work seamlessly. This assistant uses generative AI in combination with reletvant documents, which have previously been retrieved from KOMPOL, to summarize relevant articles to the user and cite their sources.

<!-- TODO: screenshot of the Point of Origin tool -->
## Point of Origin visualisation
Bloodstain pattern analysis plays a crucial role in forensic science, helping reconstruct events involving bloodshed. By examining bloodstains, analysts aim to understand their origin and the forces that caused them. Let’s delve into the specifics:

There are two types of bloodstain patterns. Passive and Active Patterns. **Passive Patterns** result from blood flow due to gravity or movement of the target. Examples include blood pooling around a body or transfer patterns (such as bloody shoe prints). **Active Patterns** are formed by external forces acting on blood. For instance, impact spatter from a gunshot wound or blood propelled during an altercation.

**Determining the point of origin**
The point of origin is the location from which blood was projected. Analysts calculate trajectories from multiple blood spatters and extend them to a common point. However, this process can be time-consuming and visually challenging. Watson can assist by calculating the angle of impact and direction for each bloodstain. By connecting these lines, we easily identify the point of origin for all blood spatters. Additionally, capturing a screenshot allows easy sharing of trajectories and point of origin information among fellow forensic officers.

> We recommend the following [article](https://www.sciencedirect.com/science/article/pii/S2352340918301902) in bloodstain pattern analysis by Dr. Attinger. Due to time constraints we were not able to automate point of origin calculations and could not implement his teams work.

<!-- TODO: screenshot of the bullet trajectory tool -->
## Bullet trajectory reconstruction
n the aftermath of a shooting incident, multiple bullet trajectories emerge. Determining the origin and path of these bullets is crucial for forensic investigations. This process is known as bullet trajectory reconstruction. By examining bullet impact points and damage patterns, investigators infer the direction of bullet travel. Currently, experts use physical tools such as wires, rods, lasers, and mathematical calculations to reconstruct bullet paths. However, these methods have limitations.

Capturing laser trajectories photographically can be challenging due to their fleeting nature. Keeping wires tight during reconstruction can be cumbersome. And visualizing trajectory calculations can be difficult for non-experts, including judges.

This is where Augmented (AR) or Mixed Reality (MR) can improve this process. By projecting a virtual laser-like line directly onto the investigator's eyewear, AR/MR simplifies trajectory visualization. Judges and other stakeholders can easily grasp the reconstructed bullet paths.

