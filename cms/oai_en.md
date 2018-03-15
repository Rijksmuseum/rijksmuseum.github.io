### The OAI API collection
The Rijksmuseum OAI API Collection is a set of more than 110,000 descriptions of objects (metadata) and digital images from the Rijksmuseum collection. The works of art and implements in the set date from ancient times through to the late 19th century and provide an excellent overview of the richness, diversity and beauty of the Dutch and international heritage. Unfortunately, copyright restrictions mean that we are not yet able to include any works from the 20th or 21st centuries.

### Request an OAI API key
Request an OAI API key.  You can do this via the advanced settings of your Rijksstudio account ([www.rijksmuseum.nl/rijksstudio](http://www.rijksmuseum.nl/rijksstudio)). Please indicate whether your request concerns the API or the OAI API. For the OAI API you will receive a confirmation for the activation. This will take up to three working days.

### The OAI API
The data sets are provided via a simple XML web service which is based on the OAI/PMH protocol. In short, the system works as follows:
Every request must be accompanied by the OAI API key provided in the OAI api key parameter.
http://www.rijksmuseum.nl/api/oai2/[YOUR_KEY]/

The verb parameter can be used to ‘ask’ the OAI API to retrieve the data. The following verbs can be used to retrieve all the data:

**ListRecords:** requests the entire set of data. As well as the verb, the request must also include a set or a resumption token.
http://www.rijksmuseum.nl/api/oai2/[YOUR_KEY]/?verb=ListRecords&set=collectie_online&metadataPrefix=oai_dc
This request will return the first 100 records in the data set 'collectie online'. A resumption token element is included at the end to return the next 100 records in the data set.
http://www.rijksmuseum.nl/api/oai2/[YOUR_KEY]/?verb=ListRecords&resumptiontoken=1231-nssdfs2qle-2324

**GetRecord:** requests a specific record.
As well as the verb, an identifier must also be included.
http://www.rijksmuseum.nl/api/oai2/[YOUR_KEY]/?verb=GetRecord&identifier=oai:rijksmuseum.nl/collection:COLLECT.5216&metadataPrefix=oai_dc
We have posted an example harvester on GitHub to help you get started quickly.

**Object descriptions**
Each object description is included in the XML file as a record, with the field definitions of the records being based on the Dublin Core field definitions. See www.dublincore.org for more information on this XML format.
An example of a description of an object in the Rijksmuseum collection can be found here: The Night Watch (SK-C-5)

#### What kind of data can you expect to find in our metadata?
We supply the following fields per object:

Header:
Identifier: an identifier for each object
Date stamp: date when the object was last changed.

_Metadata:_

**Dc: identifier**
We allocate an object number to every object. This number is important because it is used to locate the object. Example of an object number: SK-C-5. Every object also has a second identifier which comprises the name from the database that was the source of the metadata and the record number. The combination of these two pieces of information makes this identifier unique and not subject to change. Example: COLLECT.5216.

**Dc: language**
All of our object descriptions are written in Dutch. The standard value for this field is “Dutch”.

**Dc: publisher**
The Rijksmuseum is the publisher of this source. The value for this field is Rijksmuseum, Amsterdam.

**Dc: rights**
The metadata are made available under a CC0 licence. The images are in the public domain.

**Dc: date**
Dating the source. We attach a start and an end date to our sources. The dating is exact if both dates are the same (the Night Watch is dated 1642 – 1642, for example). The start and end date will be different if we have been unable to date the object exactly. There are also sources that were completely impossible to date, in which case the ‘dc: date’ field has been omitted completely.

**Dc: description**
Description of the object.

**Dc: format**
We supply two different types of dc: format fields. The links to the images and the object description on our website are included in the first two fields.
The first link, http://www.rijksmuseum.nl/assetimage2.jsp?id=SK-A-4878, is the link to the images.
The second link, http://www.rijksmuseum.nl/collectie/zoeken/asset.jsp?id=SK-A-4878, is the link to the details page.

The subsequent format fields specify the dimensions, materials and technique involved for the object in question. The dimensions in the initial fields are either for the entire object or per component. A long list of measurement data can be supplied in the case of complex objects (e.g. a cupboard, cabinet or an interior). Most paintings only have a height and a width. Materials and techniques are specified as follows:
<dc:format>material: paper</dc:format>
<dc:format>material: opaque water colour</dc:format>
<dc:format>technique: engraving (pressure process)</dc:format>
<dc:format>technique: etching</dc:format>
<dc:format>technique: white opaque water colour</dc:format>
<dc:format>technique: blue pencil</dc:format>

**Dc: creator**
This field contains the names of the creators and the roles they played in the creation of the object. Examples:
<dc:creator>printmaker: Coornhert, Dirck Volckertsz</dc:creator>
<dc:creator>according to design by: Heemskerck, Maarten van</dc:creator>
<dc:creator>publisher: Cock, Hieronymus</dc:creator>

**Dc: title**
Objects can have various different titles and the dc:title tag will supply all of these titles. The first title is the current title, while the other titles are either former titles or series titles.
The status of the title is stated between brackets after the title. The current title of the Night Watch is: 'Officers and other riflemen of Amsterdam’s district II under the command of Captain Frans Banninck Cocq and Lieutenant Willem van Ruytenburch, known as ‘The Night Watch’.  The Night Watch used to be called ‘The Company of Captain Frans Banninck Cocq and Lieutenant Willem van Ruytenburch, known as ‘The Night Watch’.

**Dc: type**
Type of object. This field is entered hierarchically. The example below concerns an ‘historical print’ belonging to the type of objects called ‘prints’.
<dc:type>print</dc:type>
<dc:type>historical print</dc:type>

**Dc: subject**
This field contains the people, places and subjects depicted in the artwork. At the moment, we have mainly recorded historical figures and places.
Icon class codes are also included in the subject field. Icon class codes are widely used as a classification system when providing access to works of art. For more information, go to http://www.iconclass.org/

**Dc: coverage**
This field contains the location where and the period when the object was created. The creation period is always given as a quarter of a century, e.g. first quarter of the 16thcentury, second quarter of the 16th century, third quarter of the 16th century or fourth quarter of the 16th century.

**Dc: contributor**
In this field we have recorded the people (or organisations) that played a role in the acquisition of an object. We use this field to express the credit due to our donors and lenders for their contributions.

### Images
The Rijksmuseum images are available in JPEG format. The images have been saved at 300 dpi and the size of the files (on average) is between 2 MB and 5 MB. The images were recorded in controlled conditions and show the actual colours.

Images can be downloaded, but we advise you instead (if possible) to create a link to the images on our webserver so that you always access the best and most up-to-date images. The Rijksmuseum uses other quality standards and file formats for publications and other printing forms. Please fill out the form on the [Photoservice page](/en/photoservice) if you would like to use our images for such applications.

The metadata includes the url for the image of the object. This url is always for the largest image size (2500x2500 pixels). A parameter can be included with this url so that the user can change the scale and reduce the size of the image to 100x100 or 200x200.
Full image of The Night Watch: http://www.rijksmuseum.nl/media/assets/SK-C-5
The Night Watch at 100 x 100: http://www.rijksmuseum.nl/media/assets/SK-C-5&100x100
The Night Watch at 200 x 200: http://www.rijksmuseum.nl/media/assets/SK-C-5&200x200

If you want a different size, we advise you to change the scale of the image yourself.
