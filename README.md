# dcat-4C-ap

This is an extension of the DCAT Application Profile v3.0 in LinkML. It is intended to be used by NFDI4Chem & NFDI4Cat 
as a core that can further be extended in profiles to provide domain specific metadata for a dataset.

## Website

[https://StroemPhi.github.io/dcat-4C-ap](https://StroemPhi.github.io/dcat-4C-ap)

## Repository Structure

* [examples/](examples/) - example data
* [project/](project/) - project files (do not edit these)
* [src/](src/) - source files (edit these)
  * [dcat_4c_ap](src/dcat_4c_ap)
    * [schema](src/dcat_4c_ap/schema) -- LinkML schema
      (edit this)
    * [datamodel](src/dcat_4c_ap/datamodel) -- generated
      Python datamodel
* [tests/](tests/) - Python tests

## Developer Documentation

Requirements:
*  Poetry must be installed
   * `pipx install poetry`
*  `make setup` to install Poetry env
*  If you want you could run `poetry run python src/dcat_ap_shacl_2_linkml.py` to recreate the [dcat_ap_linkml.yaml](src%2Fdcat_4c_ap%2Fschema%2Fdcat_ap_linkml.yaml) from the [dcat_ap_shacl.jsonld](src%2Fdcat_ap_shacl.jsonld)
* To build the docs locally run: 
  * Docs for the autogenerated DCAT-AP LinkML representation

    ``` 
    poetry run gen-doc  -d docs "src/dcat_4C_ap/schema/dcat_ap_linkml.yaml" --template-directory "src/docgen/" && poetry run mkdocs serve
    ```
  
  * Docs for the domain agnostic DCAT-AP extension
    ```
    poetry run gen-doc  -d docs "src/dcat_4C_ap/schema/dcat_4nfdi_ap.yaml" --template-directory "src/docgen/" && poetry run mkdocs serve
    ```
  
  * Docs for the chemistry-specific DCAT-AP extension
    ```
    poetry run gen-doc  -d docs "src/dcat_4C_ap/schema/dcat_4c_ap.yaml" --template-directory "src/docgen/" && poetry run mkdocs serve
    ```
* To validate a test dataset against the model it conforms to run:
  
  * Validate all example Datasets using the Python test
  ```
  make test-python
  ```
  
  * Validate a single example dataset using LinkML's validator framework
    * Validate original DCAT-AP conform example
      ```
      poetry run linkml validate src/data/examples/Dataset001_dcat_ap.yaml -s src/dcat_4c_ap/schema/dcat_4c_ap.yaml -C Dataset
      ```
    * Validate domain agnostic DCAT-AP extension conform example
      ```
      poetry run linkml validate src/data/examples/Dataset001_dcat_4nfdi_ap.yaml -s src/dcat_4c_ap/schema/dcat_4c_ap.yaml  -C NFDIDataset
      ```
    * Validate a NMR spectroscopy-specific DCAT-AP extension conform example
      ```
      poetry run linkml validate src/data/examples/Dataset001_dcat_4c_ap_NMRDataset.yaml -s src/dcat_4c_ap/schema/dcat_4c_ap.yaml -C NMRDataset
      ```

  * To convert the test datasets of each DCAT-AP profile into a TTL graph run:
    * Convert original DCAT-AP conform example
       ```
      poetry run linkml-convert -t ttl src/data/examples/Dataset001_dcat_ap.yaml -s src/dcat_4C_ap/schema/dcat_4c_ap.yaml -P "_base=https://search.nfdi4chem.de/dataset/" -C Dataset
      ```
    * Convert domain agnostic DCAT-AP extension conform example
      ```
      poetry run linkml-convert -t ttl src/data/examples/Dataset001_dcat_4nfdi_ap.yaml -s src/dcat_4C_ap/schema/dcat_4c_ap.yaml -P "_base=https://search.nfdi4chem.de/dataset/" -C NFDIDataset
      ```
    * Convert a NMR spectroscopy-specific DCAT-AP extension conform example
      ```
      poetry run linkml-convert -t ttl src/data/examples/Dataset001_dcat_4c_ap_NMRDataset.yaml -s src/dcat_4C_ap/schema/dcat_4c_ap.yaml -P "_base=https://search.nfdi4chem.de/dataset/" -C NMRDataset
      ```
    * Convert a ChemicalEntity DCAT-AP extension conform example
      ```
      poetry run linkml-convert -t ttl src/data/examples/Molecule001.yaml -s src/dcat_4C_ap/schema/dcat_4c_ap.yaml -P "_base=https://search.nfdi4chem.de/dataset/" -C ChemicalEntity
      ```
    * Convert a ChemicalSample DCAT-AP extension conform example
      ```
      poetry run linkml-convert -t ttl src/data/examples/Sample001.yaml -s src/dcat_4C_ap/schema/dcat_4c_ap.yaml -P "_base=https://search.nfdi4chem.de/dataset/" -C ChemicalSample
      ```

* Use the `make` command to generate project artefacts:
  * `make all`: make everything
  * `make deploy`: deploys site


## Credits

This project was made with
[linkml-project-cookiecutter](https://github.com/linkml/linkml-project-cookiecutter).
