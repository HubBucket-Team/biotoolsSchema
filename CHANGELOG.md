# Changelog for biotoolsSchema
Description of changes are grouped as follows:
* **Added:** new features
* **Changed:** changes to existing functionality
* **Deprecated:** a once-stable feature that has been removed
* **Removed:** a deprecated feature that has been removed
* **Fixed:** a bug fix
* **Misc:** some miscellaneous other change

# June 03 2019 biotoolsSchema-3.1.0.xsd released

## Added
1. ```tool->relation``` elements added: "Details of a relationship this software shares with other software registered in bio.tools."

   * ```relation->biotoolsID``` : "bio.tools ID of an existing bio.tools entry which this software is related to."
   * ```relation->type``` : "Type of relation between this and another registered software."  (isNewVersionOf, hasNewVersion, uses, usedBy, include, includedIn)

2. ```download->type``` enum extended:

   * "Other" ("Other type of download for software - the default if a more specific type is not available.")
   * "Downloads page" ("Web page summarising general downloads available for the software.")


3. ```documentation->type``` enum extended:

   * "Command-line options" ("Information about the command-line interface to a tool.")
   * "FAQ" ("Frequently Asked Questions (and answers) about the software.")
   * "Release notes" ("Notes about a software release or changes to the software; a change log.")

4. ```link->type``` enum extended:

   * "Discussion forum" ("Online forum for user discussions about the software.")
   * "Service" ("An online service that provides access (an interface) to the software.")
   * "Other" ("Other type of link for software - the default if a more specific type is not available.")


## Changed

1.  ```summary->homepage``` is now of ```urlftptype``` simpleType (was ```urltype``` simpleType) to support those entries (old tools in rare cases) which only have an FTP site for a homepage.

2. ```function->cmd``` ```maxlen``` facet now 1000 (was 100)

3. ```labels->elixirPlatform``` documentation improved : "ELIXIR platform credited for developing or providing the software."  (*bio.tools* tool tip will be improved)

4. ```labels->elixirNode``` documentation improved : "ELIXIR node credited for developing or providing the software - the software is in Node Service Delivery Plan." (*bio.tools* tool tip will be improved)

5. More stringent regex patterns to enforce correct use of fullstop ('.') character (this was not escaped before, meaning any character could be given):

   * ```urlftptype``` simpleType as used in ```linkType``` complexType (for ```link->url``` and ```documentation->url```) and for ```summary->homepage```, ```download->uri``` and ```labels->topic->uri```.   Regex's are now ```http(s?)://[^\s/$.?#]*\.[^\s]*```   and   ```s?ftp://[^\s/$.?#]*\.[^\s]*```

   * ```dataType``` complexType (as used in ```function->input->data->uri```, ```function->output->data->uri```, ```function->input->format->uri``` and ```function->output->format->uri```).   Regex is now ```http://edamontology\.org/data_[0-9]{4}```

   * ```urltype``` simpleType as used in ```credit->url```.  Regex is now ```http(s?)://[^\s/$.?#]*\.[^\s]*```
   * ```doitype``` simpleType as used in ```publication->doi```.  Regex is now ```10\.[0-9]{4,9}[A-Za-z0-9:;\)\(_/.-]+```
   * ```function->operation->uri```.  Regex is now ```http://edamontology\.org/operation_[0-9]{4}```
   * *bio.tools* will be refactored if required

6. '''doiType''' simpleType pattern (as used in ```publication->doi```)
   * removed requirement for "doi" or "DOI" prefix (which technically isn't part of the DOI sytnax)
   * enforces correct use of fullstop ('.') character
   * supports ```[```, ```]```, ```<``` and ```>``` characters
   * Regex are now ```10\.[0-9]{4,9}/[A-Za-z0-9:;\)\(_/.-]+``` and ```10\.[0-9]{4,9}/[\[\]&lt;&gt;A-Za-z0-9:;\)\(_/.-]+```  (the second pattern is more restrictive than the first - once we're happy this is OK just this more restrictive one will be needed)
   * *bio.tools* annotations will be refactored if required

## Fixed

1. '''credit->orcidid''' pattern fixed:

   * removed requirement for "http(s?)://orcid.org/" prefix (which isn't  part of the ORCID sytnax)
   * added support for terminal 'X' character
   * Regex is now ```[0-9]{4}-[0-9]{4}-[0-9]{4}-[0-9]{3}[0-9X]```
   * *bio.tools* annotations will be refactored accordingly. 

## Deprecated
1. ```link->type``` enum restricted:

   * "Browser" ("A website for browsing data.") removed.  Any existing annotations in *bio.tools* will be replaced by type "Other".


## Misc
	
1. Pattern restricting a version number now appears in one place only (under ```versionType```) to avoid potential future inconsistencies.

2. Target and default namespace set to "https://bio.tools"
	
# August 01 2018 biotoolsSchema-3.0.0.xsd released


Changes since biotoolsSchema-3.0.0-rc-rev1.xsd released

## Changed
1. regex patterns on ```otherID->value``` improved:

   * case-insensitie prefixes *e.g.* "DOI" or "doi"
   * all regex values **must** be prefixed
2. ```elixirPlatform``` moved from ```credit``` to ```labels``` and is now optional (0 or 1)
3. ```elixirNode``` moved from ```credit``` to ```labels``` and is now optional (0 or 1)
4. Regex pattern of ```orcidid``` now supports "http" or "https" prefixes
5. ```summary->description``` ```maxlen``` facet now 100 (was 500)
6. Schema settings now are:

   * ```elementFormDefault``` == ```qualified```
   * ```attributeFormDefault``` == ```qualified```
   * No ```targetNamespace```

## Removed
1. ```download->containerFormat``` removed
2. ```download->diskFormat``` removed



# March 1 2018 biotoolsSchema-3.0.0-rc-rev1.xsd released
## Added

## Changed
1. All ```comment``` elements renamed to ```note```:

   * ```credit->note```
   * ```documentation->note```
   * ```download->note```
   * ```link->note```
   * ```function->note```
2. ```credit``` refactored such that at least one of ```credit->name```, ```credit->email``` or ```credit->url``` is mandatory.

## Deprecated

## Removed
1. ```elixirInfo``` element grouping removed.  These data can be handled internally by ELIXIR Hub (or can be reinstated in future).
2. ```apiSpec``` element grouping removed.  This can be reinstated as needed.
3. ```relation``` element grouping removed.  This can be reinstated as needed.
4. ```isAvailable``` elements removed: specification of information known to be unavailable (as required by the bio.tools [information standard](https://github.com/bio-tools/biotoolsSchemaDocs/blob/master/information_requirement.rst) will be handled internally by bio.tools

   * ```publication->isAvailable```
   * ```link->isAvailable```
   * ```documentation->isAvailable```
   * ```download->isAvailable```
5. ```credit``` grouping streamlined

   * ```credit->tel``` removed
   * ```credit->gridid``` removed

6. ```labels``` grouping streamlined

   * ```labels->goTermID``` removed (will be reinstated as needed)
   * ```labels->soTermID``` removed (will be reinstated as needed)
   * ```labels->taxID``` removed (will be reinstated as needed)
7. ```download->cmd``` removed
8. ```summary->shortDescription``` removed

## Fixed

## Misc


# January 26 2018 biotoolsSchema-3.0.0-rc.xsd released

## Added
1. ```isAvailable``` elements added to support the specification that an attribute is not available for a tool (as required by the bio.tools information standard (https://github.com/bio-tools/biotoolsSchemaDocs/blob/master/information_requirement.rst)

    1.1 ```publication->isAvailable```
    1.2 ```linkType``` complexType as used in ```link->isAvailable``` and ```documentation->isAvailable```
    1.3 ```download->isAvailable```
2. ```summary->otherID``` added ("A unique identifier of the software, typically assigned by an ID-assignment authority.")

    2.1 ```summary->otherID->value``` (1 only), ```minlen``` facet of 1, is the value of the identifier (with appropriate regexs as per type, see below)
    2.2 ```summary->otherID->type``` (0 or 1) is enum of the identifier type (doi, rrid, cpe, biotoolsID)
    2.3 ```summary->otherID->version``` (0...1)  (see below)
3. Version information refactored

    3.1 New ```versionType``` simpleType
    3.2 ```xs:token``` with facets ```minlen``` (1), ```maxlen``` (100)
    3.3 preserving pattern facet previously defined in ```summary->version```
4. Version elements added:

    4.1 ```summary->otherID->version``` (0...1) ("Version information (typically a version number) of the software applicable to this identififier.")
    4.2 ```download->version``` (0...1) added ("Version information (typically a version number) of the software applicable to this download.")
    4.3 ```publication->version``` (0...1) added ("Version information (typically a version number) of the software applicable to this publication.")
5. ```summary->biotoolsCURIE```added

    5.1 0...1 cardinality
    5.2 type of xs:anyURI
    5.3 regex is `biotools:[_a-zA-Z][_\-.0-9a-zA-Z]*`
6. ```function->cmd``` added ("Relevant command, command-line fragment or option for executing this function / running the tool in this mode.")

    6.1 Type is xs:token
    6.2 ```minLen``` facet of 1
    6.3 ```maxLen``` facet of 100
7. ```link->type``` enum extended:

    7.1 "Scientfic benchmark" ("Information about the scientific performance of a tool."
    7.2 "Technical monitoring" ("Information about the technical status of a tool."
8. ```documentation->type``` enum extended:

    8.1 "Governance" ("Information about the software governance model.")
    8.2 "Contributions policy ("Information about policy for making contributions to the software project.")
    8.3 "Installation instructions" ("Instructions how to install the software.")
    8.4 "Tutorial" ("A tutorial about using the software.")
    8.5 ```Governance``` added to ```documentation->type``` enum
9. ```labels->license``` enum extended with "Unlicensed" value

## Added / changed
1. ```publication->type``` enum, mulitple modifications:

    1.1 "Primary" (no change) The principal publication about the software itself; the article to cite when acknowledging use of the software.
    1.2 "Method" (new!) A publication describing a scientific method or algorithm implemented by the software.
    1.3 "Usage" (new!) A publication describing the application of the software to scientific research, a particular task or dataset.
    1.4 "Comparison" (was "Benchmark") A publication which assessed the performance of the software relative to other tools.
    1.5 "Review" (no change) A publication where the software was reviewed.
    1.6 "Other" (no change)

## Changed
1. Elements that were mandatory are now optional:

    1.1 ```function``` (now 0...many)
    1.2 ```labels->toolType``` (now 0...many)
    1.3 ```labels->topic``` (now 0...many)
    1.4 ```labels``` (now 0...1)
2. ```credit``` element group refactored (merging in attributes from old ```contact``` element group)

    2.1 Annotation chaned to "An individual or organisation that should be credited, or may be contacted about the software."
    2.2 ```credit->elixirPlatform``` and ```credit->elixirNode``` added (moved from ```elixirInfo```). In a credit one must specify 1) an ELIXIR platform or node name or 2) a credit with a name, a mandatory ID/means of contact and optional type and role (see the schema docs)
    2.3 ```credit->tel``` (telephone number) added ( ```minlen``` facet of 5, ```maxlen``` facet of 50)
    2.4 ```credit->typeRole``` cardinality changed to 0...many (was 0...1)
    2.5 ```credit->typeRole``` enum extended with "Primary contact" to indicate this credit is a primary contact for the software.
    2.6 ```credit->orcidId``` changed to ```credit->orcidid```
    2.7 ```credit->gridId``` changed to ```credit->gridid```
    2.8 ```credit->name``` now xs:token (was ```nameType``` simple type)
    2.9 ```credit->url``` now of ```urlTyp``` simpleType

3. ```download->cmd``` refactored

    3.1 xs:token (was ```textType``` simple type)
    3.2  ```minLen``` facet set to 1
    3.3  ```maxLen``` facet set to 100
4. ```biotoolsIdType``` refactored

    4.1 ```minLen``` facet removed (redundant).
    4.2 ```maxLen``` facet removed
5. ```relation->biotoolsID``` refactored

    5.1 type changed from ```biotoolsUrlType``` to ```biotoolsIdType``` simple type
    5.2 name changed to ```biotoolsID```
6. ```collectionID``` refactored

    6.1 type changes to nameType simpleType (was biotoolsCollectionIdType simpleType)
    6.2 ```minlen``` facet to 1, ```maxlen``` to 50
7. Changes to elements in ```summary``` group:

    7.1 ```summary->name``` element ```maxlen``` facet set to 100.
    7.2 ```summary->version``` now 0...many (was 0 or 1)
    7.3 ```summary->description``` ```maxlen``` facet now 500 (was 50)
    7.4 ```summary->shortDescription``` ```maxlen``` facet now 100 (enforcing that the short desriptions really must be short!)
    7.5 ```summary->shortDescription``` type set to ```textType``` (was ```xs:token```)
    7.6 ```summary->toolid``` renamed to ```summary->biotoolsID```
8. ```linkType->comment``` type set to textType (consistent with other free-text comments) (```linkType``` is complex type used by ```link->comment``` and ```documentation->comment``` elements)
9. ```doiType``` simpleType and "pmid" global element refactored, to drop support for PMIDs and DOIs with "PMID:" and "DOI:" prefix respectively (regex```s changed)



## Removed
1. ```summary->doi``` (use instead ```summary->otherID->value``` and set ```summary->otherID->type``` = doi)
2. ```summary->versionID``` (this no longer supported by bio.tools)
3. ```contact``` element grouping removed (the refactored ```credit``` should be used instead)
4. ```biotoolsCollectionIdType``` simpleType (no longer used)
5. biotoolsUrlType simpleType (no longer used)

## Fixed
1. ```credit->email``` duplicate pattern restriction removed



# November 17, 2016 biotoolsSchema-2.0.0.xsd released
Sorry, no bandwidth to provide summary of changes : please see the schema documentation.  changelog will be maintained properly henceforth!

# November 8, 2016 biotoolsSchema-2.0-beta04.xsd released
Sorry, no bandwidth to provide summary of changes : please see the schema documentation.

# November 3, 2016 biotoolsSchema-2.0-beta03.xsd released
Sorry, no bandwidth to provide summary of changes : please see the schema documentation.

# October 22, 2016 biotoolsXSD officially renamed to biotoolsSchema, biotoolsSchema-2.0-beta02.xsd released
Sorry, no bandwidth to provide summary of changes : please see the schema documentation.

# August 12, 2016  biotoolsXSD-2.0-beta01.xsd released
A complete revision of the schema.  Too many changes to list, therefore the highlights only are summarised below.  For more information please read the schema documentation.

## Added : new or restructured element groupings (see schema docs for details)
1. ```summary```: "Basic information about the software."
2. ```function```: "Details of the function(s) that this software provides, expressed in terms from the EDAM ontology."
3. ```labels```: "Miscellaneous scientific, technical and administrative details of the software, expressed in terms from controlled vocabularies."
4. ```relation```: "Details of a relationship this software shares with other software registered in bio.tools."
5. ```commandLineSpec```: "Details of the command-line interface to a tool, if appropriate."
6. ```apiSpec```: "Details of the API to a service, if appropriate, including service endpoints."
7. ```image```: "Details for a virtual machine image or container for the software."
8. ```download```: "Link to a miscellaneous download for the software, e.g. source code."  A controlled vocabulary for download types is defined.
9. ```documentation```: "A link to documentation about the software including training materials."  A controlled vocabulary for documentation types is defined.
10. ```publication```: "A publications about the software.".  A controlled vocabulary for publication types is defined.
11. ```contact```: "Details of a contact for the software, e.g. developer or helpdesk."  A controlled vocabulary for contact types/roles is defined.
12. ```credit```: "An individual or organisation that should be credited for the software."

## Added : new elements
1. ```biotoolsID```: "Unique ID that is assigned upon registration of the software in bio.tools."
2. ```doi```: "Canonical Digital Object Identifier of the software assigned by the software developer or service provider."
3. ```shortDescription```: "Short and concise textual description of the software function."
4. ```repository```: "Repository where source code, data and other files may be downloaded."
5. ```socialMedia```: "A website used by the software community including social networking sites, discussion and support fora, WIKIs etc."
6. ```function->comment```: " Concise textual description of the function(s), if this is not already obvious from the resource description."
7. ```goTermID```: "Gene function including molecular function, cellular component and biological process.  Miscellaneous ontology annotation. The ID of Gene Ontology (GO) concept(s) are specified."
8. ```soTermID```: Features which can be located on a biological sequence. The ID of Sequence Ontology (SO) concept(s) are specified.
9. ```taxId```: NCBI taxonomy ID of taxonomic group the software (particularly database portals) caters for.
10. ```status```: Label describing miscellaneous status of the software."  A controlled vocabulary is defined.
11. ```credit->orcidId``` : "Unique identifier (ORCID iD) of a person that is credited."
12. ```credit->gridId``` : "Unique identifier (GRID ID) of an organisation that is credited."

## Added : new enum values
1. New values to <license> enum:

   * "Other"
   * "Proprietary"
   * "Common Development and Distribution License (CDDL-1.0)"

2. New values to <language> enum:

   * "AWK"
   * "MATLAB"
   * "JSP"
   * "PyMOL"

## Changed : element name changes
1. ```resources``` -> ```tools```
2. ```resource``` -> ```tool```
3. ```functionName``` -> ```operation```
4. ```resourceType``` -> ```toolType```
5. ```platform``` -> ```operatingSystem```

## Changed : other
1. ```operation```, ```data```, ```format``` and ```topic``` elements now include ```uri``` and ```term``` elements.
2. ```collection``` : now restricted to accept a bio.tools ID of a software collection, rather than free-text.

## Removed
1. ```publications``` element group replaced by ```publication``` with new structure.
2. ```uses``` element group replaced by ```relation```.
3. ```interface``` element group removed, now handled by ```download``` and ```documentation```.  Note that ```interfaceType``` is removed completely (now subsumed in ```toolType```).
4. ```elixirInfo``` element group, ```maturity``` and ```cost``` removed, now handled by ```status```.
5. ```docs``` element group replaced by ```documentation```.
6. ```credits``` element group replaced by ```credit```.
7. ```canonicalID``` replaced by ```doi```.
8. ```accessibility``` now handled via ```status```.
9. ```tag``` removed: annotations are now restricted to controlled vocabulary terms defined in ```labels```.
10. ```functionHandle``` and ```dataHandle``` removed, now handed by ```commandLineSpec```.
11. ```functionDescription``` and ```dataDescription``` removed, now handled by ```function->comment```.
12. ```sourceRegistry``` removed, now handled by ```collection```.




# October 17th, 2015  biotoolsXSD-1.4.xsd released
## Added
* New ```docs->docsDownloadSource``` optional element : "Source code downloads page (URL)"
* New ```docs->docsDownloadBinaries``` optional element : "Software binaries downloads page (URL)"
* New ```docs->docsGithub optional``` element : "Github page (URL)"
* "Maintainer" added to ```contactRole``` enum
* "Other" added to ```resourceType" enum

## Changed
* ```publications``` is now optional
* ```functionHandle``` element ```maxLen``` facet increased to 300 (via ```maxLen``` facet on ```name``` simpleType; also set to 300)
* Parentheses added to ```pattern``` restriction on ```name``` element, which is now  [\p{Zs}A-Za-z0-9+\.,\-_:;()]*

## Misc
* docsDownload purpose changed from "Software or data downloads page (URL)" to "General downloads page (URL)"



# September 22nd, 2015  biotoolsXSD-1.3.xsd released

## Added
* "Artistic License 2.0" added to ```license``` enum
* "Icarus" added to ```language``` enum
* ```id``` attribute added to ```resource``` element.  This is the unique ID (URI) of the resource.
* Default value of "None" added to publicationsPrimaryID and publicationsOtherID



## Changed
**safe changes:**
* ```name``` element ```maxLen``` facet restriction increased to 200 characters
* ```+``` added to ```name``` simpleType pattern restriction, which is now [\p{Zs}A-Za-z0-9+\.,\-_:;]* 

**potentially breaking change:**

* ```maturity``` element enum values changed to:

  * "Early" (was "Nascent" or "Young" in biotoolsXSD 1.2)
  * "Stable" (was "Established" in biotoolsXSD 1.2)
  * "Deprecated" (was "Retiring" or "Extinct" in biotoolsXSD 1.2)

* ```platform``` enum value "Unix" removed (use "Linux" instead)

* ```resourceType``` element enum values removed: "Dataset", "Tool (query and retrieval), "Tool (analysis)", "Tool (deposition)", "Tool (visualiser)", "Tool (utility)", "Suite", "Framework", "Virtual machine", "Widget" and "Other"

* New ```resourceType``` enum values are as follows:

   * "Database" (was "Database" or "Dataset" in biotoolsXSD 1.2)
   * "Tool" (was "Tool", "Tool (query and retrieval), "Tool (analysis)", "Tool (deposition)", "Tool (visualiser)", "Tool (utility)" or "Workflow" in biotoolsXSD 1.2)
   * "Service" (new in biotoolsXSD 1.3)
   * "Workflow" (no change)
   * "Platform" (new in biotoolsXSD 1.3, was "Framework" or "Suite" in biotoolsXSD 1.2)
   * "Container" (new in biotoolsXSD 1.3, was "Virtual machine" in biotoolsXSD 1.2
   * "Library" (was "Library" or "Widget" in biotoolsXSD 1.2)

* The definition of these resource types are:

   * "Database" - A collection of data, datasets, a registry etc.
   * "Tool" - Software which you can download, install, configure and run yourself.
   * "Service" - Software provided as a service and available for immediate use, e.g. on the Web.
   * "Workflow" - A definition of a collection of tools, services etc. for running in a workflow system.
   * "Platform" - An integrated environment, including suites, workbenches, workflow systems, frameworks etc.
   * "Container" - A collection of data, tools, services etc. in a portable environment, e.g. VMs, Docker.
   * "Library" - A package of code for building/extending tools, including widgets, plug-ins, toolkits etc.

* ```interfaceType``` element enum values removed:  "REST API", "URL", "SQL" and "SPARQL"

* New ```interfaceType``` enum values are as follows:

   * "Command-line" (no change)
   * "Web UI" (no change)
   * "Desktop GUI" (no change)
   * "SOAP WS" (no change)
   * "HTTP WS" (new in biotoolsXSD 1.3, was "REST API" or "URL" in biotoolsXSD 1.2)
   * "API" (no change)
   * "QL" (new in biotoolsXSD 1.3, was "SQL" or "SPARQL" in biotoolsXSD 1.2)

* The definition of these interface types are:

* "Command line" - Text-based interface to a tool or service.

   * "Web UI" - Graphical user interface available on the Web.
   * "Desktop GUI" - Graphical user interface that runs on your own machine.
   * "SOAP WS" - Programmatic access provided via SOAP and WSDL file.
   * "HTTP WS" - Access provided via HTTP, including simple URLs, RESTful APIs etc.
   * "API" - Application programmers interface to a programming library.
   " "QL" - Query language interface to a database, e.g. SQL, SPARQL etc.



## Deprecated
* Use of the ```tag``` element is deprecated and will be removed in a future version.

## Removed
## Fixed
## Misc



# June 8th, 2015  biotoolsXSD-1.2.xsd released

## Added
* Bash added to enum of ```language``` element
* tag maxlen facet set to 50

## Changed
* maxLen facet restriction on all elements of type ```Text``` removed (was 512), such that the length restriction of 1000 (defined on ```Text```) applies
* Single space added to ```Name``` simpleType pattern restriction, which is now  [\p{Zs}A-Za-z0-9\.,\-_:;]*
* The following elements (all simpleType) changed type to simpleType ```Name```:
  * ```collection```
  * ```usesName```
  * ```function->input/output->dataHandle```
  * ```elxirInfo->elixirStatus```
  * ```elxirInfo->elixirNode```
  * ```function->functionHandle```

**potentially breaking change:**
* ```tag``` element (was complexType ontologyTerm) also changed to simpleType "Name"



# May 5th, 2015  biotoolsXSD-1.1.xsd released

## Added
* "accessibility" (optional) added:  whether resource is accessible to all or not: enum of "Public" or "Private"
* New simple type URLFTP which is URL supporting FTP URLs

## Changed
* ```publications``` (1 max.) **is now mandatory**, ```publications->publicationsPrimaryID``` is now mandatory (1 max.)
* "None" value added to valid patterns for ```CitationID``` simpleType, i.e. ```publications->publicationsPrimaryID``` may have a value of "None" if PMID, PMCID or DOI is not available.
* ```Name``` element pattern restriction added:  [A-Za-z0-9\.,\-_:;]*
* ```Name``` element maxLen facet restriction reduced from 100 to 50 characters
* "Dataset" value added to enum of resourceType
* ```docs->docsDownload``` type changed to URLFTP from URL
* ```docs->docsCitationInstructions``` changed to URLFTP from URL
* ```docs->docsTermsOfUse``` changed to URLFTP from URL
* ```interface->interfaceDocs``` changed to URLFTP from URL
* ```resourceType``` type changed to ```Name``` simpleType (enum of permitted values preserved)
* ```interfaceType``` type changed to ```Name``` simpleType (enum of permitted values preserved)
* ```maturity``` type changed to ```Name``` simpleType (enum of permitted values preserved)
* ```platform``` type changed to ```Name``` simpleType (enum of permitted values preserved)
* ```language``` type changed to ```Name``` simpleType (enum of permitted values preserved)
* ```license``` type changed to ```Name``` simpleType (enum of permitted values preserved)
* ```cost``` type changed to ```Name``` simpleType (enum of permitted values preserved)
* ```description``` maxLen facet restriction reduced from 1000 to 512 characters
* ```function->functionDescription``` maxLen facet restriction reduced from 1000 to 512 characters
* ```function->input/output->dataDescription``` maxLen facet restriction reduced from 1000 to 512 characters

## Fixed
* ```language``` enum value of "C Shapr" changed to "C#"
* ```language``` enum value of "Assembly" changed to "Assembly language"
* ```language``` enum value of "Methematica" changed to "Mathematica"
* ```language``` enum value of "R changed to "R"

