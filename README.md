# Septuagint Witness Processor

A Python application that filters the apparatus data for a specific witness and creates a new version of the Bible corresponding to the readings of that witness. This tool aims to enhance the usability of the Septuagint and its apparatus by researchers, easing the learning and understanding of the Septuagint in the religious studies research community.

## Introduction

The Septuagint Witness Processor reads a JSON file containing textual apparatus data, filters the variation units associated with a specified witness, and applies these variations to an OSIS XML Bible file. By generating a new version of the Bible text that reflects the readings of a particular manuscript witness, researchers can perform more focused studies on textual variations.

## Features

- **Filtering Apparatus Data**: Extracts variation units from a JSON apparatus file based on a specified witness ID.
- **Applying Variations**: Modifies an OSIS XML Bible file by applying the filtered variations to the corresponding verses.
- **Supports Complex Textual Operations**: Handles overlined characters, homoioteleuton, transpositions, and various textual conventions found in critical editions.
- **Customizable**: Easily adjust the witness ID and file paths to work with different data sets.

## Installation

### Prerequisites

- Python 3.6 or higher
- pip package manager

### Required Python Packages

- `lxml`

### Install Required Packages

You can install the required package using the following command:

```bash
pip install lxml
```

## Usage

### Input Files

1. **JSON Apparatus File (`GottAppParser_output_complete_20240929.json`):**
   - A JSON file containing the apparatus data structured according to the Critical Edition Ontology (CEO).
   - Generated from parsing the textual apparatus of the Septuagint.

2. **OSIS XML File (`genesis.xml`):**
   - An OSIS XML file of the Bible (specifically Genesis in this example).
   - Contains the original Bible text to which the variations will be applied.

### Output File

- **Updated OSIS XML File (`updated_508_genesis.xml`):**
  - The generated OSIS XML file reflecting the readings of the specified witness.

### Running the Processor

1. **Clone the Repository**

   ```bash
   git clone https://github.com/yourusername/septuagint_witness_processor.git
   cd septuagint_witness_processor
   ```

2. **Place Input Files**

   Ensure that the following files are placed in the project directory:

   - `GottAppParser_output_complete_20240929.json`
   - `genesis.xml`

3. **Edit the Script (Optional)**

   If you want to specify a different witness ID or file paths, edit the `__main__` section of the script:

   ```python
   if __name__ == "__main__":
       WITNESS_ID = '508'
       JSON_FILE_PATH = 'GottAppParser_output_complete_20240929.json'
       OSIS_XML_PATH = 'genesis.xml'
       OUTPUT_OSIS_PATH = f"updated_{WITNESS_ID}_genesis.xml"

       # Initialize and run the processor
       processor = SeptuagintWitnessProcessor(
           witness_id=WITNESS_ID,
           json_file_path=JSON_FILE_PATH,
           osis_xml_path=OSIS_XML_PATH,
           output_osis_path=OUTPUT_OSIS_PATH
       )
       processor.run()
   ```

4. **Run the Processor**

   ```bash
   python septuagint_witness_processor.py
   ```

   The script will process the input files and generate the updated OSIS XML file reflecting the readings of the specified witness.

### Example

Given a witness ID of `508`, the application will:

1. Load the apparatus data from `GottAppParser_output_complete_20240929.json`.
2. Filter the variation units associated with witness `508`.
3. Apply these variations to `genesis.xml`.
4. Save the updated Bible text to `updated_508_genesis.xml`.

## Detailed Description

### Class Structure

The application consists of the `SeptuagintWitnessProcessor` class, which encapsulates the functionality for filtering and processing variation units.

- **Initialization**: The class is initialized with the witness ID and file paths for the JSON apparatus file, OSIS XML file, and output OSIS XML file.
- **Filtering Variation Units**: The `filter_variation_units` method reads the JSON apparatus data and filters the variation units that include the specified witness.
- **Processing Variation Units**: The `process_variation_units` method applies the filtered variations to the OSIS XML file, modifying the verses accordingly.
- **Saving the Updated OSIS XML**: The `save_updated_osis_xml` method writes the modified XML tree to the output file.

### Handling Special Textual Features

- **Overlined Characters**: The processor replaces overlined characters with their corresponding full forms using the `OVERLINE_MAPPING` dictionary.
- **Homoioteleuton**: Processes similar endings in readings to correctly identify text ranges.
- **Transpositions**: Handles cases where text segments need to be transposed within a verse.
- **Textual Conventions**: Manages various textual conventions like abbreviations, deletions, additions, and more.

## Contributing

We welcome contributions from the community. Please follow these guidelines:

- **Fork the Repository**: Click on the "Fork" button at the top right corner of this page to create a copy of the repository on your GitHub account.

- **Create a New Branch**: It's good practice to create a new branch for each feature or bug fix:

  ```bash
  git checkout -b feature/your-feature-name
  ```

- **Make Your Changes**: Improve the code, add features, or fix bugs.

- **Ensure Code Quality:**

  - Follow PEP8 standards for Python code.
  - Add docstrings and comments where necessary.
  - Test your changes thoroughly.

- **Commit and Push:**

  ```bash
  git add .
  git commit -m "Description of your changes"
  git push origin feature/your-feature-name
  ```

- **Submit a Pull Request**: Go to your fork on GitHub and click on the "New Pull Request" button. Provide a detailed description of your changes.

## License

This project is licensed under the GNU General Public License v3.0. See the [LICENSE](LICENSE) file for details.

## Contact

For any questions or suggestions, please open an issue on the GitHub repository.

## Acknowledgements

- The [Critical Edition Ontology (CEO)](http://example.org/ceo/) for providing a structured framework.
- The religious studies research community for inspiring this project.
- [This article](https://abramkj.com/2013/01/11/how-to-read-and-understand-the-gottingen-septuagint-a-short-primer-part-2-apparatus/) for guidance on understanding the Göttingen Septuagint apparatus.

---

**Note:** This processor is designed to work with specific formats of the Septuagint apparatus and OSIS XML files. Ensure that your input files conform to the expected formats for optimal results.
