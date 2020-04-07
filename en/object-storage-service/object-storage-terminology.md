---
title: "Object Storage - Terminology"
slug: object-storage-terminology
---


**Swift:** Name of the software we use to provide the object storage service.

**Object:** Every element stored in Swift is called an Object. Files you upload to Swift are therefore called Objects.

**Bucket:** This is an entity that is used to group objects together. Every object in Swift is stored in a Bucket. It is at the bucket level that are defined Access Control Lists (public or private), so any object in a public bucket will be public and any object in a private bucket will be private. Buckets are also called Containers.

**Folder:** Our Object Storage supports the notion of 'pseudo-hierarchical containers', which is a means of using object naming to emulate a bucket (or folder) hierarchy without actually implementing one in the storage system.
