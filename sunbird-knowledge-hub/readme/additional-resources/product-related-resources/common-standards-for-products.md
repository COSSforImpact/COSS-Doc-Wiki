---
icon: elementor
---

# Common Standards for Products

Common Standards for Products in Sunbird/DIKSHA

### Overview <a href="#lmtm0cjvl557" id="lmtm0cjvl557"></a>

There is a need to define certain minimal standards in any functionality that is developed as part of Sunbird/DIKSHA products and solutions. This helps in:

1. Creating a better and consistent user experience
2. Developing extensible and reusable technical design
3. Providing common understanding across product, development and QA teams
4. Repeating the standard requirements for each new feature as part of PRD (thereby avoids risk of missing them)

This document captures such minimum common standards that need to be followed across all products and solutions in Sunbird/DIKSHA. These standards apply to all applications (portal, mobile app and desktop app) unless otherwise specified.

These common standards have to be followed unless explicitly stated otherwise in individual PRDs. This is by no means a finalized list of standards. It will get updated over time.

### Minimum Common Standards <a href="#id-6lumt8bxd9m8" id="id-6lumt8bxd9m8"></a>

### Lists <a href="#pf3ugrnlxilc" id="pf3ugrnlxilc"></a>

**Sorting**

For any list, unless otherwise specified, sorting should be by default (in ascending order)

* Alphabetical, in case the list items are alphabetic or alpha-numeric strings
* Numerical in case the list items are numbers

Apart from the default implementation, technical design should allow following flexibility in modifying sorting for a specific list:

1. Sort the list in the same order as list items are configured
2. Modify the sorting logic of a list with a custom logic
3. Configure Ascending or Descending order

Following is the sorting to be followed for the common set of lists in Sunbird:

1. Board: Alphabetical
2. Grade: KG (if exists), Class 1 to 12
3. Medium: Alphabetical
4. Subject: Alphabetical
5. Languages list in supported languages: Order in which they are configured
6. Topics: Alphanumeric
7. Licenses: Order in which they are configured

**Default Values**

If a list is having only one item in it, that item has to be selected by default, in the case of mandatory fields that user should enter.

**Auto Suggest from the List**

A List should be configurable to support auto-suggest items from the list upon user typing.

### Tables <a href="#id-4pb3m9nf4cw6" id="id-4pb3m9nf4cw6"></a>

All tables should have sorting enabled for each column (both ascending and descending). Sorting is alphanumeric in case of alphanumeric and is numerical in case of numbers.

Default field to sort and the sorting order should be configurable for each table.

### Content Listing <a href="#cvofcojbqopq" id="cvofcojbqopq"></a>

TBD

### Field Labels and Texts <a href="#ccv8a0wux07j" id="ccv8a0wux07j"></a>

Please refer to : [https://docs.google.com/presentation/d/1CDSFibP-\_ttIzUCCZsUYznLAJxLhaTJkZLL7MmZWUBk](https://docs.google.com/presentation/d/1CDSFibP-\_ttIzUCCZsUYznLAJxLhaTJkZLL7MmZWUBk)

### Languages <a href="#sucf96ig5zqs" id="sucf96ig5zqs"></a>

**Content**

Any operation related to content (any type of content - textbook, resource, question, course etc.) should be tested at least for:

* English
* Urdu
* Hindi
* Tamil

**Interface**

All supported languages?

Criteria based on which the languages are selected:

### Performance <a href="#id-8mgf8qlrxexa" id="id-8mgf8qlrxexa"></a>

**Response Time**

Less than 2 secs for any operation, unless otherwise specified. Any response time more than 2 secs should always have a progress icon.
