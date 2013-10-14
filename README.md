oboparse.py
===========

Parses the [OBO format](http://www.geneontology.org/GO.format.obo-1_2.shtml) in python

By default it prints each "*stanza*" in the JSON format.

For example:

    curl http://www.geneontology.org/ontology/obo_format_1_2/gene_ontology_ext.obo | python oboparse.py 

Or you can use the [jq](http://stedolan.github.io/jq) to create a CSV with the terms:

    < gene_ontology_ext.obo python oboparse.py | jq -r '.| select(.["@type"]=="Term")|[.id, .name, .["def"], .is_obsolete//false] | @csv'
   
or a CSV containing the hierarchy of terms:

    < gene_ontology_ext.obo python oboparse.py | jq -r '.| select(.["@type"]=="Term" and .is_a)|{id, parent: .is_a[] }|[.id, .parent]|@csv'

