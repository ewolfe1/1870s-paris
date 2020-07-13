# Notebook to facilitate data extraction for businesses in Paris.

## Background info on data source

Primary source for this data is digitized business directories from Gallica:  
[https://gallica.bnf.fr/ark:/12148/cb32695639f/date](https://gallica.bnf.fr/ark:/12148/cb32695639f/date). These files are available as PDF or OCR text download.

This notebook works best if the specific section of text is copied from the entire document and saved as a .txt or .docx file(s) to a directory.

The entries are generally formatted "Florist Name, Street Street, Street Number." Sometimes businesses have additional information printed between the Name and Street information, e.g.  
[https://gallica.bnf.fr/ark:/12148/bpt6k9668579h/f15.item.r=fleurs%20naturelles](https://gallica.bnf.fr/ark:/12148/bpt6k9668579h/f15.item.r=fleurs%20naturelles)

## Sample data

Here are three examples of the data formats, though entries mostly follow the first pattern.

*  Dieu, Clichy, 6.
* Pontine, passage de l'Opéra, galerie de l'Horloge, 1.
* Havard et Cie, ® 1867, leurs roupies et bouquets , expédition franc de port et d'emballage, plantes d'appartement, de serre et pleine terre, graines de toutes sortes, Auber, 11.

## How this notebook works

*Note that, due primarily to OCR issues, this process is imperfect and will need manual review and a good bit of data cleanup. However, it should greatly speed up the process of data entry.*

1. Attempt to extract each business as a separate line. This is done using regular expressions and pattern matching.
2. Parse each line to extract the Business Name, Street Number, Street Name. Additional text is collected separately.
3. Using the pandas library, collect the parsed data into a structured format:
    * Full line
    * Business Name
    * Street Number
    * Street Name
    * Extra text
    * Source of the data (i.e. original document - to facilitate easier data cleanup)
4. Cleanup the Street Name (e.g., expand "boul." to "boulevard")
    * Note that if no street type is listed, "rue" is assumed (e.g. "Clichy" becomes "rue Clichy")
5. Write out parsed data to an Excel spreadsheet for easier review.
    * Filename follows the format "business_list_TIMESTAMP.xlsx" (e.g., business_list_20200702141735.xlsx)
