---
layout: default
title: Transformers
parent: Components
nav_order: 1
---

# Transformers
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

# Introduction

The AMP concept of a transformer is the most fundamental component which a
software developer hoping to tweak the AMP framework will encounter. The
transformer is a component which <em>transforms</em> input data objects into
output data products.

Some examples of transformers may help in understanding:
- Conceptual examples:
  - Generating a thumbnail image output from a high-resolution input image
  - Extracting header information from a scientific file
  - Transforming an XML file into a JSON equivalent
  - etc.
- Live examples:
  - [BasicS3ObjectMetadataTransformer](https://github.com/archive-manager-and-processor/amp-cloud/blob/master/aws/transformers/basic-s3-object-metadata/src/main/java/gov/nasa/pds/amp/BasicS3ObjectMetadataTransformer.java) - which is a transformer that
  takes as input an Amazon Simple Storage Service (S3) object and generates very
  basic object metadata as its output, including: object size, path, mime type,
  etc.

The key idea of a transformer is to provide functionality for a developer to
create their own transformer which can be plugged into the AMP framework, such
that AMP will transform file-archive data as the developer needs.

# Core Transformers

A set of basic AMP Transformers that are ready to use out-of-the-box are bundled
with the AMP Cloud Environment and the AMP Cluster Environment.

These include the following.

## Basic Metadata Transformer

This transformer extracts basic file metadata from file-archive assets. It can
be used to understand a file archive at an individual file level or at an
aggregate level (after the Transformer data is pushed to Elasticsearch).

Depending on the AMP Environment being deployed, whether a specific AMP Cloud
Environment (i.e. different cloud provider) or the AMP Cluster Environment, a
version of the basic metadata Transformer is provided. See the below for
current iterations of the Basic Metadata Transformer.

| AMP Environment | Basic Metadata Transformer  |
|---|---|---|---|---|
| AMP AWS Cloud Environment | [BasicS3ObjectMetadataTransformer](https://github.com/archive-manager-and-processor/amp-cloud/tree/master/aws/transformers/basic-s3-object-metadata) |

## Thumbnail Generator Transformer

TBD.

## Document Content Extractor Transformer

TBD.

# Creating Your Own Transformer

The AMP Framework is designed to be extensible, and thus the generation of
custom Transformers is a core functionality. Below is a guide on the process.

## Adhere to the Transformer output schema

In order to allow the diversity of AMP environments to execute Transformers in
a consistent manner, such that the output of Transformers may be interoperable,
AMP requires a schema standard to be adhered to.

Please reference the schema here: [transformer-output.schema.json](https://github.com/archive-manager-and-processor/archive-manager-and-processor.github.io/blob/master/docs/schemas/transformer-output.schema.json)

It is a very simple schema, defined in the JavaScript Object Notation (JSON)
standard, and requires only a single field to be defined, namely ``uri`` -
which specifies the full Universal Resource Identifier path to a particular
resource.

Here is an example of a Transformer output that adheres to:

```
{
  'uri': '/mnt/data/project1/subfolder5/large-image.jpeg',
  'size': 325147995,
  'content-type': 'image/jpg',
  'md5': '8bd3ab114fb8483adc5b0ad7422d193a'
}
```

<br/>
### Summary:

Your custom Transformer must <strong>generate output in the JSON
standard</strong>, include <strong>a ``uri`` field</strong> that points to the
full path of the location of your file resource, and <strong>optionally include
zero or more fields</strong> as you see fit.


## Develop a Transformer

TBD.

### AMP AWS Cloud Environment

TBD.

### AMP Spark Cluster Environment

TBD.
