.. include:: ../../../Includes.txt


.. _fal-architecture-overview:

========
Overview
========

The FAL architecture consists of three layers:

Usage Layer
 This layer consists of the File References, which represent the relationships to files from any structure that can use them (pages, content elements or any custom structure defined by extensions).

Storage Layer
  This layer is composed of several parts. First, there are the files and their associated metadata. Then, each file is associated with a Storage.

Driver Layer
 This layer is the deepest layer. It consists of the drivers that manage the actual access and manipulation of files. It is invisible to both the frontend and the backend as it only works in the background.

In fact, the drivers are explicitly not part of the public interface. Developers will only interact with File, Folder, FileReference, or Storage objects, but never with a Driver object unless they actually develop one.

This layered architecture makes it easy to use different drivers to access files while maintaining a consistent interface for both developers (in terms of the API) and end users (via the backend).
