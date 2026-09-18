# Subject Heading Display Normalization Rules

# Primo VE Subject Heading Normalization Rules

This repository contains Ex Libris Primo VE normalization rules developed by the [Inclusive Language Team](https://library.uregina.ca/about/inclusivelanguage), a collaborative effort at the University of Regina's Dr. John Archer Library & Archives, alongside the libraries of its federated colleges: Luther College, the First Nations University of Canada, and Campion College. This work is done in consultation with the campus community, and benefits from the input and expertise of individuals and groups both within and external to libraries and archives.

## What these rules do

Each rule reads subject heading data from a MARC field, reformats it, and writes the result into the Primo Normalized XML (PNX) record, which powers what patrons see and can search in Primo VE/NDE. Each rule applies a list of string substitutions that replace an outdated or harmful heading with its updated equivalent.

The substitution terms implemented in these rules are drawn from:

- [Saskatchewan Indigenous Subject Headings (SkISH)](https://librarianship.ca/news/sk-indigenous-subject-headings)
- [Manitoba Archival Information Network (MAIN) Indigenous Subject Headings](https://main.lib.umanitoba.ca/indigenous-subject-headings)
- [Université Laval's RVM revisions for Indigenous vocabulary](https://rvmweb.bibl.ulaval.ca/rvmweb/contenu/contenu.do?chemin=%2fautochtones-revision-du-vocabulaire)
- [Homosaurus](https://homosaurus.org/), an international linked-data
  vocabulary of LGBTQ+ terms

For more information display normalization rules, see [Ex Libris's documentation on normalization rules](https://knowledge.exlibrisgroup.com/Primo/Product_Documentation/020Primo_VE/Primo_VE_(English)/050Display_Configuration/Configuring_Normalization_Rules_for_Display_and_Local_Fields) and [local fields](https://knowledge.exlibrisgroup.com/Primo/Product_Documentation/020Primo_VE/Primo_VE_(English)/050Display_Configuration/040Configuring_Local_Display_and_Search_Fields_for_Primo_VE) and [Moran Vardi's Developer Network blog post of norm rule examples](https://developers.exlibrisgroup.com/blog/primo-ve-normalization-rule-examples/)

## Why use local fields?

These rules write into local fields (07 and 08) rather than normalizing the display value of the subject heading fields (650, 600, 610, etc.) directly. Applying the substitutions directly to those fields' display normalization would create a mismatch between what is displayed and what is indexed for search: the record would show the updated heading (e.g. "Indigenous Peoples -- North America"), but the underlying search index would still be built from the original heading (e.g. "Indians of North America"). That mismatch means the updated heading is not searchable at all, and clicking it as a link returns no results. Using local fields lets both the display value and the search index be built consistently from the same substitution logic, so the updated heading is both shown to patrons and actually searchable/clickable.

## Files

Field 07 (`local_field_07_display` and `local_field_07_search`) drives the subject headings shown on the full bibliographic record, sourced from MARC fields 600, 610, 653, 656, 657, 658, 662, and 880.

Field 08 (`local_field_08_display` and `local_field_08_search`) drives the subject facets shown in the sidebar when browsing search results, sourced from MARC field 650.

For each pair, the `_display` file builds the heading or facet value shown to the patron, and the `_search` file builds the matching index entry, using the same term substitutions, so what a patron sees is also what they can click or search on successfully.
