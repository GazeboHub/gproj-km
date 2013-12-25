GKM Platform Tools
==================

## Overview

### Dependency: Platform Ontology

### Tool: Shared MIME Database Importer

* Refer to [XDG shared-mime-info specification](http://www.freedesktop.org/wiki/Specifications/shared-mime-info-spec/) and related [XML document](http://cgit.freedesktop.org/xdg/shared-mime-info/tree/freedesktop.org.xml.in)
* Goal: Utilize MIME _media type_ information for _method dispatching_ within _portal workflows_ and _workflow design_ components
    * Concerns
        * Montgolfier (GProj M1) Workflow relies heavily on specific formats having no standard MIME media types, for instance: _Markdown text_ (special subset of `text/plain`), _iThoughts mindmap_ (typically packaged as a zip-encoded archive file, type "itmz"), and _Cubetto Model_ (special subset of XML). 
        * Broadly, it may be a _fortuitous_ choice, to rely on a media type framework not _exclusively coupled_ to the set or formal MIME _media type_ specification documents, though any alternative model must represent a _normative_ and _scalable_ framework, in order to merit its application in this system.

### Deliverable: UML Profile for Platform Tools

* Extend SysML4UML - examples
    * Component [Stereotype] extends Block
    * Platform [Stereotype] extends Package
    * MediaType [Stereotype] extends ?? (cf. Ports onto UML and SysML?)
* Goal is to apply this profile in a tranform onto the platform ontology
    * Effectively, endeavor to emulate if not to inegrate SPEM structures onto SysML, as transformed onto OWL

### Tool: MIME Database Service

* Integrate Shared MIME Database Importer as toolchain component, in constructing the MIME database
* Develop and extend a CORBA-based OWL ontology service?
    * CORBA provides a stack of platform-agnostic protocols, decoupled from HTTP
    * This service would require a definition of:
        1. IDL interface definitions sufficient to present namely the Apache Jena API via CORBA
        2. ORB server binding for that IDL (Java)
        3. Prototype ORB client binding for that IDL (Java)
    * User auth in JacORB: howto
        * Option 1: Use SSL
            * If used for auth: 
                * Requires a PKI framework
                * Would represent a static auth method, in that usage, not involving user credential
                * Not recommended except in providing tunnel-level encryption in support of direct user auth protocols
        * Option 2: Kerberos or GSSUP via CORBA Security Attribute Service (SAS) Interceptors
            * _**Refer to JacORB 3.1 manual, clause 19**_
            * Kerberos auth would require thr avialability of a full Kerberos framework, on the service network (i.e LAN, WAN, Internet, VPN, etc). This results in a more complexservice configuration, but should be **strongly recommended** alternate to GSSUP
            * GSSUP : "GSS Username/Password." Entails sending raw credentials over the network. Not recommended.
* Aim for providing a simple MIME database
    * Use case: Define OWL mapping for Shared MIME database
    * Use case: Role in modeling, as in a SysML block diagram in which ports would be typed according to supported MIME media types on "file input" and "file output"
* Aim for delivery in an OSGi bundle
    * Activator
    * Service interfaces

### Tool: SysML Model Transform for Platform Ontology

