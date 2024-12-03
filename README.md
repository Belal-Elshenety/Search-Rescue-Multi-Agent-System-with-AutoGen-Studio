# **Search & Rescue Multi-Agent System with AutoGen Studio**

## **Overview**

This project was developed for **CSC 480: Artificial Intelligence** at **California Polytechnic State University, San Luis Obispo (Cal Poly SLO)**. The goal of this project is to design a high-level **multi-agent system** tailored for **search and rescue operations**.

The system leverages **agentic workflows** using **AutoGen Studio** to emulate the structure and functions of the **Incident Command Search & Rescue System**. Each agent corresponds to a specific role in a real-world search and rescue team, with responsibilities ranging from field operations to logistical support.

Additionally, the project integrates **three specialized skills** for the agents:
- **Medical Team Lead**:
  - `drug_side_effects()` - Analyzes and provides insights into potential side effects of drugs used in the operation.
  - `get_nearest_hospitals()` - Locates and retrieves information on nearby hospitals for emergency care.
- **Search Team Lead**:
  - `fetch_terrain_data()` - Fetches digital elevation models (DEM) to assess the terrain and assist in navigation during search operations.

Below is a diagram illustrating the hierarchy and roles within the system, along with their interdependencies:

![Search & Rescue Hierarchy](./docs/AgenticSystemDesign.png)

---

### **Key Features**
- Implements a multi-agent system for search and rescue operations.
- Models the behavior and hierarchy of the **Incident Command System**.
- Incorporates **agentic workflows** for streamlined role delegation and task management.
- Integrates specific AI-driven skills to enhance operational capabilities:
  - Drug information analysis.
  - Terrain data retrieval.
  - Emergency hospital localization.

---

## **Installation**

### Prerequisites
- Anaconda or Miniconda installed

### Steps

1. **Clone the Repository**:  
   Clone the project from GitHub and navigate into the project directory.  
   ```bash
   git clone https://github.com/Belal-Elshenety/Search-Rescue-Multi-Agent-System-with-AutoGen-Studio.git
   cd Search-Rescue-Multi-Agent-System-with-AutoGen-Studio
   ```

2. **Set Up the Environment**:  
   Navigate to the `dependencies` folder and create the Conda environment:  
   ```bash
   cd dependencies
   conda env create -f environment.yml
   ```

3. **Activate the Environment**:  
   Activate the newly created Conda environment:  
   ```bash
   conda activate csc480
   ```

4. **Run AutoGen Studio**:  
   Launch AutoGen Studio locally:  
   ```bash
   autogenstudio ui
   ```

## Uploading and Configuring Objects in AutoGen Studio

After launching AutoGen Studio, you must upload and configure the objects (models, agents, skills, and workflows) to fully set up the system. Each object type has its own setup requirements, outlined below:

---

### 1. Models
Models are the backbone of your system. They require API keys to function properly.

#### Steps:
1. Navigate to the **Models** section in AutoGen Studio.
2. Click **Upload** and select the JSON file for the model (e.g., `models/*.json`).
3. After uploading, open the model configuration in AutoGen Studio.
4. Add the required API keys for the model under the **API Key** section.
   - Gemini: Through [Google AI Studio](https://aistudio.google.com/app/) or [Google Cloud Console](https://console.cloud.google.com)
   - Llama 3.1: Through [Groq Dev Console](https://console.groq.com)
5. Save the model configuration.

---

### 2. Skills
Skills are specific functionalities that agents can utilize. These also require secrets like API keys to function.

#### Steps:
1. Navigate to the **Skills** section.
2. Click **Upload** and select the JSON file for the skill (e.g., `skills/*.json`).
3. Open each skill and add the required API keys under the **Secrets** section
    -  fetch_terrain_data: OPENTOPO_API_KEY from [OpenTopography](https://opentopography.org/), and GOOGLE_API_KEY, which is a Google Maps Key from [Google Cloud Console](https://console.cloud.google.com)
    - get_nearest_hospitals: Google_API_Key, Google Maps Key from [Google Cloud Console](https://console.cloud.google.com)
    - drug_side_effects: SERPER_API_KEY, Serper API Key from [Serper](https://serper.dev/)
4. Save the skill configuration.

---

### 3. Agents
Agents represent the roles in the Search & Rescue system. Each agent must have its subordinate agents and skills manually configured.

#### Steps:
1. Navigate to the **Agents** section.
2. Click **Upload** and select the JSON file for the agent (e.g., `agents/*.json`).
3. Open each agent configuration and:
   - Add subordinate agents manually (if applicable).
   - Add skills (if applicable).
   - Ensure that all necessary dependencies are connected, as outlined in the project diagram.
4. Save the agent configuration.
5. Note: Agents are **not launched automatically**. You will need to manually launch them after configuration.

#### Agent Configuration Table

| **Agent**            | **Subordinate Agents**                                         | **Implemented Skills**         |
|-----------------------|---------------------------------------------------------------|---------------------------------|
| Incident Commander    | Logistics Section Chief, Operations Section Chief, Planning Section Chief, Safety Officer |                                 |
| Logistics Section Chief | Medical Team Lead, Rescue Team Lead, Search Team Lead       |                                 |
| Operations Section Chief | Medical Team Lead, Rescue Team Lead, Search Team Lead, Planning Section Chief |                                 |
| Planning Section Chief |                                                               |                                 |
| Safety Officer        | Medical Team Lead, Rescue Team Lead, Search Team Lead         |                                 |
| Communication Unit    | Logistics Section Chief, Operations Section Chief, Planning Section Chief |                                 |
| Search Team Lead      |                                                               | fetch_terrain_data             |
| Rescue Team Lead      |                                                               |                                 |
| Medical Team Lead     |                                                               | get_nearest_hospitals, drug_side_effects |

---

### 4. Workflows
Workflows define the interactions between agents and skills. These must be configured with specific agents.

#### Steps:
1. Navigate to the **Workflows** section.
2. Click **Upload** and select the JSON file for the workflow (e.g., `workflows/*.json`).
3. Open the workflow and:
   - Add the **UserProxy Agent** as the initiator.
   - Add the **Incident Commander** as the receiver.
   - Ensure all required agents and skills are properly linked within the workflow.
4. Save the workflow.

---

### Summary of Configurations

| **Object Type** | **Configuration Details**                                   |
|------------------|------------------------------------------------------------|
| Models           | Add API keys in the secrets section.                       |
| Skills           | Add API keys in the secrets section.                       |
| Agents           | Add subordinate agents, implemented skills, and launch them manually. |
| Workflows        | Add UserProxy as initiator and Incident Commander as receiver. |

---

### Notes
- Each object type must be uploaded in the correct category.
- Ensure all API keys are valid and correctly placed in their respective sections.
- Follow the table above for a quick overview of configuration steps.
- Refer to the project diagram for agent dependencies and relationships.

By following these steps, you will have the project fully configured in AutoGen Studio.
