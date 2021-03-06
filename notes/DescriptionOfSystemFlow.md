
Madame web app <--> Madame server <--> Lexitags server


Common use case:
User comes to site -> Basic site generated from template on server

The user enters URL of page to tag:
	-> URL gets sent to proxy module on server
	-> Proxy fetches the HTML of the target URL
	-> Proxy comments out script and iframe tags
	-> Proxy replaces relative image URIs with absolute image URIs.
	-> Proxy sends back an object containing the sites head and body tag
	-> The content of the body tag is used to populate the content container in the web app.

The user highlights a word on the page to add meta data to:
	-> The text of the highlighted selection gets sent to the lexitags server for disambiguation
	-> The results from lexitags are filtered
		-> If the results contain WordNet terms, then the DBPedia results are filtered away
	-> The results are then sorted
		-> Primarily by source, WordNet terms first, then the first and second level schema.org terms
		-> Secondarily they are sorted lexically
	-> Then the results are displayed on the web page 

	If the user cannot find a match with the highlighted text, 
	it is posible to write your own word into a search box. 
	The semantics of this word will then be linked to the highlighted text.

The user click the sense of the word which match the intended semantics of the highlighted word
	-> The term, either a WN synset or a DBP entity gets sent to the mapping module on the server
	-> The mapping module find the mappings into other ontologies 
		that most closely matches the semantics of the term.
	-> The server returns the entity types that best fit the term, and their namespaces
		-> If no schema.org mapping is found, schema:Thing is returned as it is always correct.
	-> The web app adds a tag which surrounds the selected text, and adds the entity value to it using RDFa
		-> This new tag contains keywords which will highlight it on the page
	-> The web app then asks the server for the schema.org properties of it's schema type(s).
	-> The server returns all the applicable properties
	-> The web app adds all the returned properties to the markup of the page with empty values

The user clicks a marked up section
	-> The web app displays all the possible attributes the section can have
		-> If values have already been inserted, these are shown as the default values
	-> The user inputs the values the attributes should have
	-> When the submit button is click, the attributes get updated to the correct values

The user clicks the export button
	-> The html on the page is cleaned
		-> Temporary markup(tooltips, popover) is removed
		-> Attributes without values are removed
	-> The html is sent to the server
		-> The exporter comments in the script and iframe tags
		-> The html is put in the database
	-> The server returns the id of the new web page
	-> The web app displays the URL to the new marked up website. 