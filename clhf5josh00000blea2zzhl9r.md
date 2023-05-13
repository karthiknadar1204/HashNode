---
title: "Yet another YAML blog"
datePublished: Mon May 08 2023 18:04:15 GMT+0000 (Coordinated Universal Time)
cuid: clhf5josh00000blea2zzhl9r
slug: yet-another-yaml-blog
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1683520871103/ef6c8b97-db4f-4494-879d-088536637d01.png
tags: devops, yaml

---

Tired of dealing with data formats that make your head spin? Look no further than YAML! Say goodbye to the days of confusing code and hello to a user-friendly, easy-to-read language that makes data organization a breeze. YAML is perfect for those who want to keep their data organized and maintainable without having to decipher complicated code.

In my upcoming blog, we'll dive into the wonderful world of YAML and show you how to use it in a variety of ways, from configuring files to managing data serialization. We'll break down the syntax and structure of YAML and provide simple examples to help you get started.

So come along with me on this exciting journey and see for yourself how YAML can change the way you work with data!

## YAML

YAML is a human-readable data-serialization language. Yaml was initially called "Yet Another Markup Language". The abbreviation of YAML was changed to "YAML ain't markup language", this was done because in markup languages you can store documents and in YAML you can store data objects.YAML is a data format used to exchange data. It is similar to XML and JSON.

## What is a markup language?

**Now that we know that YAML is not a mark-up language, let us look into what is mark-up language and why is YAML not a mark-up language.**

Markup languages are used to create documents, web pages, and other digital content that can be displayed or processed by computers, printers, or other devices. Markup languages are typically composed of a set of rules, tags, and attributes that define the structure, formatting, and functionality of the document or content.

ex- HTML is a very popular mark-up language used to create layouts for web pages!!

but YAML is focused on representing data in a human-readable and machine-readable format. YAML is primarily used for data serialization, configuration files, and other similar purposes, hence it was named YAML ain't mark-up language.

## DATA SERIALISATION

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683520013528/e42e4846-05ed-407f-b040-cc6e633f86c9.png align="center")

Let's say you have an application that stores information about customers, such as their name, address, phone number, and email either in XML or JSON format. You want to serialize this data into a format that can be easily transmitted and stored in a file or database. YAML is often used in data serialization to convert data objects into a format that can be easily transmitted, stored, or processed by different applications or platforms.

Data serialization is the process of converting structured data such as objects, arrays and other data structures into a format that can be stored or transmitted in a database. This format is often a sequence of bytes that can be stored or transmitted over a network.

## DATA DESERIALISATION

Data deserialization is the process of converting YAML data, which is typically stored as a text file, into a structured data format that can be used by a computer program. During the deserialization of YAML, the YAML parser reads the text file and converts it into a data structure such as an object, array or dictionary in memory. The resulting data structure can be accessed and manipulated by a computer program.

## Why do we need Data Serialisation

Serialization is the process of converting an object's state, or its data, into a format that can be easily stored or transmitted. This makes it possible to save the object's state and recreate the object later in a new location or to exchange the object's data with another program or system. Objects are usually composed of several components, and transferring or delivering all of these parts typically requires significant coding effort. Serialization helps to solve this problem by providing a standard way to capture all of the object's data into a sharable format. This makes it easier to transmit and store the object's data without having to manually transfer each component of the object.

## Benefits of Yaml

* Easy to read and write: YAML uses a simple syntax that is easy to read and write. This makes it easier for developers to understand the data and modify it as needed.
    
* Human-readable: Unlike some other serialization formats, such as JSON or XML, YAML is designed to be read and edited by humans. This makes it ideal for configuration files and other settings that need to be easily understood and modified by people.
    

Supports complex data structures: YAML supports complex data structures, such as lists, maps, and nested objects, which makes it easy to represent and store data flexibly.

## Use of Yaml

* Configuration files: Many applications use YAML files to store configuration settings that define how the application should behave. These settings can include things like database connection strings, API keys, logging settings, and more.
    
* Data exchange: YAML can be used to exchange data between programs or systems. This is useful when two systems need to communicate with each other, but are written in different programming languages or run on different platforms
    
* Documentation: YAML can be used to generate documentation for software projects. By using YAML to define the structure and content of the documentation, it becomes easier to update and maintain the documentation over time.
    

## Syntax of YAML

1. Indentation: YAML uses indentation to define the structure of the data. Blocks of data are indented to indicate their parent-child relationship.
    
2. Comments: Comments in YAML begin with the "#" character and continue to the end of the line.
    
3. Data types: YAML supports several data types including scalars (strings, numbers, and booleans), sequences (arrays and lists), and mappings (key-value pairs).
    
4. Line breaks: Line breaks in YAML are significant and are used to separate data elements.
    
5. Key-value pairs: In YAML, key-value pairs are represented as a colon and a space (": ") separating the key from the value.
    

### LISTS IN YAML

*In a given YAML file, we can separate different documents representing different information using --- between them.*

```yaml
# In yaml,we can store "key:value" pairs
"apple": "i am a red fruit"
1: "This is Number one."
---
#list
 - papaya
 - kiwi
 - apple
 - banana
 - mango
---
# lists block style
fruit:
  - cherry
  - mango
  - banana
  - Apple
  - apple
```

![HI](https://cdn.hashnode.com/res/hashnode/image/upload/v1683523769128/256f4958-b581-4ffc-8209-beffe40f024b.png align="center")

```yaml
# storing list data in a single line in yaml
# we can store data in a single line in yaml using the flow style
cities: [new delhi, mumbai]

---
# storing data in key:value pair in a single line in yaml.
{mango: "yellow fruite" , age: 56}

...
```

*if we want to mark the end of a document in yaml, we terminate the file with ... .*

*YAML provides the ability to have values that span across multiple lines by using the "|" or "&gt;" symbols.*

*When using the "|" symbol, this is referred to as a "Literal Block Scalar" and it will include any newlines and trailing spaces.*

*On the other hand, using the "&gt;" symbol is referred to as a "Folded Block Scalar" and it will fold newlines to spaces, making it easier to read and edit. In both cases, the indentation is ignored, allowing for greater flexibility and ease of use.*

```yaml
# storing data in multiple lines in YAML
bio: | 
 Hey i am karthik nadar 
 I am a devops engineer
---
# Writing a single line in multiple lines in YAML
message: >
  Hey i am karthik nadar
  I am a devops engineer
  I like eating
  and i 
  also like dogs
...
```

## Datatypes in YAML

* String
    
* Integer
    
* Date and time
    
* Floating point numbers
    
* boolean
    
* null
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683567858503/1ca16749-992b-4afb-b291-6d9cf324eaa8.png align="center")

## Advanced Data-types in YAML

* Sequences
    
* Maps
    
* Pairs
    
* Sets
    
* Dictionary
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683568288917/d246a389-61af-49d0-9093-bdf2d229d256.png align="center")

## How to Reuse a particular property in Yaml using Anchors ?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1683568423972/54ce8885-a8ec-42ef-af31-429c5eaae7c2.png align="center")

## Conclusion

Thank you for joining me on this journey, and may your YAML files be forever readable and your applications forever scalable!

### Thank you for giving your valuable time to read my blog, do check out my socials:

[Github](https://github.com/karthiknadar1204)

[Twitter](https://twitter.com/Karthikreincar1)

[Linkedin](https://www.linkedin.com/in/karthik-nadar-b2155a25b/)