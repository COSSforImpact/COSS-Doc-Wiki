---
icon: elementor
---

# OpenSABER Solutioning Guidelines

### Purpose <a href="#p703167g68uc" id="p703167g68uc"></a>

This document outlines a set of broad guidelines for any adopter to lay a data foundation using OpenSABER. This document also intends to provide advisory guidance on fitment of OpenSaber as a registry infrastructure.

### Intended audience <a href="#cg9z0wja1q04" id="cg9z0wja1q04"></a>

Technical and solution experts exploring OpenSABER

### Terminology <a href="#x1lmumnon2pq" id="x1lmumnon2pq"></a>

**Subject** - The person or the thing that the data represents.

**Registry** - One logical instance that hosts data about one type of Subject, which is accessible via APIs, to manage Subject lifecycle and access.

**Custodian** - An entity that hosts and manages the registry using OpenSABER to hold data about/of subjects.

**Instance** - One or more of physical machines hosting OpenSABER instance which contains one or more Registries.

### What is OpenSABER? <a href="#d2y1gp0xn4m" id="d2y1gp0xn4m"></a>

OpenSABER is a software layer that helps build trusted electronic registries. It helps manage data and make it available via open APIs. OpenSABER allows the Custodian to host and make core master data available to their own and/or partner applications easily. OpenSABSER uses metadata files to define the schematic representation of the data about/of the Subject without writing much code. OpenSABER also allows Custodians to choose and configure an appropriate database (or datastore). The API signatures are quite generic and do not change with the database chosen, thereby providing flexibility to move data, should a need arise.

### Data ownership <a href="#id-481hjgm41pzv" id="id-481hjgm41pzv"></a>

Data ownership is a much debated topic and it is best we stop with saying OpenSABER is just a software allowing custodians to manage and host various subject master data. If the data is about a person, the person could be deemed as the owner for that data as per data privacy/ownership laws/rules under which custodian is governed. If the data is about a things or other items, then custodian must ensure data ownership is appropriately discussed before hosting the data within the registry.

### Is OpenSABER the right choice for a data custodian, like me? <a href="#tlddslip7au2" id="tlddslip7au2"></a>

Custodian is an entity that hosts and manages a registry using OpenSABER to hold data about/of subjects. It is not necessarily the owner of data. A strong yes to the following indicates that OpenSABER is indeed a right choice.

1. a) You, as the custodian, know about the source of data or b) You can legally host the data - basically you have access to the data and others trust you to provide such data.
2. You understand the subject data and its attributes well enough to manage the registry.
3. You know how to keep the data valid/approved and upto date.
4. You take extreme care to protect the data while hosting it including handling the security and privacy aspects.
5. You understand why you need a utility software layer to provide declarative data models, secure APIs, etc. and understands the value of such layer instead of just creating such system from scratch on top of a database.
6. You have access to technology teams who can understand the software, configure, and run a registry in production.

### Guidelines <a href="#n25yknpcv8a8" id="n25yknpcv8a8"></a>

The three pillars about data, namely, 1) Ingestion 2) Protection and 3) Usage govern the best design of a registry. It is imperative that the adopter spends significant time and think about each of these pillars in conjunction with the above inquiries that helped choose OpenSABER in the first place.

### Ingestion <a href="#jj54zm44e6ig" id="jj54zm44e6ig"></a>

1. Is the subject data available to you fully trustable? Or would you like to assign a different score of trust to that data
2. Are you getting this data from within your own organization or via partners or via crowdsourced mechanisms?
3. How many sources could give you the data about/of subject? Would they be providing same data or conflicting data or varying attributes? Also, think if there is a time dimension to this data.
4. Do you know who can certify this data is valid or approved?
5. What mechanism you can advise that the data is clean at the time of ingestion or eventually clean?

### Protection <a href="#m27frxtp1zg3" id="m27frxtp1zg3"></a>

1. What attributes of the data do you think must be encrypted and stored?
2. What attributes of the data for which you require explicit and mandatory approvals?
3. Who are the actors reading the data from the registry? What attributes of the data they need access to?
4. The read actors may not necessarily be the same as source. If so, can one source read data of another source?
5. What data attributes may need explicit consent for storing and accessing?
6. What data may need masking when accessing based on user roles.
7. What data may require you to notify (and provide access/lifecycle history) the subject?

### Usage <a href="#zf7m5pyep28m" id="zf7m5pyep28m"></a>

1. What data are you reading?
2. How the data read is going to be used? For what purpose?
3. Who are the beneficiary? - owner, custodian, 3rd party - In all scenarios, owner must be one beneficiary for sure and there could be others optionally.
4. Do you need a workflow while accessing in terms of explicit approvals, etc.?
5. Do you need role based access control to registry data?
