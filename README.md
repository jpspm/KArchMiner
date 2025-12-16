# KArchMiner: A Dataset of Architectural Patterns in Kotlin Open Source Projects

The dataset is avaliable [here](https://drive.google.com/file/d/19K5jzvNNWRCuH9olf2jDDTHVByRLYjOp/view?usp=sharing)
## ✨ Overview

KArchMiner is a curated and extensible dataset of open-source Kotlin repositories, automatically analyzed to infer their architectural patterns. The dataset was constructed by mining GitHub repositories associated with **Kotlin Multiplatform** and **Jetpack Compose** development.

The goal of KArchMiner is to provide an empirical foundation for systematic analyses of how architectural patterns, such as Model-View-Controller (MVC), Model-View-ViewModel (MVVM), Model-View-Intent (MVI), Clean Architecture, and VIPER, are implemented in real-world Kotlin systems, addressing the significant lack of publicly available datasets in this domain.

## 🔑 Key Features

* **Inferred Architectural Patterns:** Patterns are detected through static analysis and dependency graph modeling, based on class roles and inter-class dependencies.
* **Scope:** The dataset comprises **1,193 repositories**.
* **Detailed Content:** Includes architectural metadata, dependency graphs, and full source code snapshots for reproducibility.
* **Reproducible Organization:** Data structure is organized in a reproducible and extensible manner, indexed by a repository-specific hash.

## 🏗️ Methodology

The construction of the KArchMiner dataset followed an automated and reproducible pipeline implemented in Python.

### 1. Classification Pipeline

The process involved steps from repository selection to architecture inference.



* **Repository Selection:** The GitHub REST API was used to collect repositories containing Kotlin code and explicitly referencing Kotlin Multiplatform or Jetpack Compose development.
* **File Extraction and Parsing:** All `.kt` source files were located and parsed using regular expressions to identify class declarations, data classes, interfaces, and other types. Repositories that did not contain a `MainActivity.kt` file (used as a proxy indicator for Android-based presentation-layer structure) were excluded.
* **Class Role Identification:** Architectural roles (**View**, **ViewModel**, **Model**, **Repository**, **Presenter**, **Interactor**, **Router**, **UseCase**, etc.) were assigned based on naming conventions, imports, and annotations.
* **Dependency Graph Construction:** Each repository was modeled as a directed graph (using NetworkX) where nodes represented classes with their roles, and edges indicated dependencies inferred from import statements or dependency injection patterns.
* **Architecture Inference:** Architectural patterns were automatically classified by analyzing structural relationships and dependency chains within the graph.

### 2. Dataset Structure

The results of the analysis are stored in a structured dataset.



[Image of the Dataset Structure]


* **`summary.json`:** Provides a consolidated overview of the dataset, grouping repositories according to their inferred architectures and mapping each hash to the repository owner and name.
* **`Repo_Hash/` Directories:** Each repository-specific directory contains:
    * **`analysis.json`:** Architectural classification metadata, including the original URL, the inferred pattern, the rationale, and a list of identified Kotlin classes.
    * **`graph.png`:** An illustration of the dependency graph.
    * **`repo_clone/`:** A full folder with the original source code snapshot.

## 📊 Architecture Distribution

The distribution across the six categorized architectural types among the **1,193 repositories** is as follows:

| Architecture Type | Number of Repositories |
| :--- | :--- |
| **MVVM** | 721 |
| **MVC** | 305 |
| **MVI** | 140 |
| **VIPER** | 15 |
| **Clean Architecture** | 9 |
| **MVP** | 3 |

## 💡 Use Cases

KArchMiner is designed to support various empirical software engineering investigations:

* **Architecture Smell Detection and Anti-pattern Analysis:** Enables systematic comparison of code smell prevalence and good practices across different architectural patterns.
* **Architectural Testability Evaluation:** Supports the automatic evaluation of software architecture testability using the ADTEM method, by extracting architectural metrics (cohesion, coupling, dependency).
* **Sustainability and Evolution Analysis:** Allows researchers to identify recurring structural issues, assess architectural trade-offs, and observe evolution trends in Kotlin Multiplatform projects.

## ⚠️ Threats to Validity

Users should consider the following threats to validity when interpreting the dataset results:

* **Construct Validity:** Architectural patterns are **inferred through static analysis heuristics** (naming conventions, directory structure, dependencies). Projects that deviate from common conventions may be misclassified, and the inferred architecture should be interpreted as an **approximation of the implemented structure** (*architecture-as-implemented*), not an absolute ground truth.
* **External Validity:** KArchMiner is constructed **exclusively from open-source GitHub repositories**. This limits the generalizability of findings to proprietary or industrial codebases, as open-source projects may differ in scale and development constraints.
