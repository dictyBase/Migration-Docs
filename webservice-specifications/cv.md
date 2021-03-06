# Controlled vocabulary(cv) or ontology
Resources related to cv(controlled vocabulary)

![cvterm_model_for_data_api](https://cloud.githubusercontent.com/assets/48740/14930927/2c3bb4ca-0e2d-11e6-824c-caad8b61f239.png)

The diagram above represents various resources and their relationships that
are defined below in cv webservice specifications. The **cvterm** represents a
singular resource. By walking through the defined relationships, various
related resources could be reached from an instance of cvterm resource.  The
**predicate** will also have a similar structure.

## Available resources

* [/cvs/:id ](#cvsid)
* [/cvs ](#cvs)
* [/cvs/:id/cvterms/:id ](#cvsidcvtermsid)
* [/cvs/:id/cvterms ](#cvsidcvterms)
* [/cvs/:id/predicates/:id ](#cvsidpredicatesid)
* [/cvs/:id/predicates ](#cvsidpredicates)
* [Relationship resources](#relationship-resources)


## `/cvs/:id`
Resource for a particular cv. The `id` will be unique **ontology short name**  as defined is [OLS](http://www.ebi.ac.uk/ols/beta/ontologies)
or the **acronym** defined in [bioportal](http://bioportal.bioontology.org/ontologies?filter=OBO_Foundry)

**Document structure**

```json
{
    "data": {
        "type": "cv",
        "id": "eco",
        "attributes": {
            "name": "eco",
            "defintion": "This is evidence code ontology"
        },
        "relationships": {
            "cvterms": {
                "links": {
                    "related": "/cvs/eco/cvterms"
                }
            },
            "predicates": {
                "links": {
                    "related": "/cvs/eco/predicates"
                }
            }
        },
    },
    "links": {
        "self": "/cvs/ro"
    }
}
```
**Inclusion**

`cvterms` and `predicates` will be paginated.

----

## `/cvs`
Resource for collection of cvs.

**Document structure**

```json
{
    "links": {
        "self": "/cvs",
    },
    "data": [
        {
            "type": "cv",
            "id": "eco",
            "attributes": {
                "name": "",
                "defintion": ""
            },
            "links": {
                "self": "/cvs/eco"
            }
        },
        {
            "type": "cv",
            "id": "so",
            "attributes": {
                "name": "",
                "defintion": ""
            },
            "links": {
                "self": "/cvs/so"
            }
        }
    ]
}
```
-------

## `/cvs/:id/cvterms/:id`
The syntax of the cvterm `id` is defined [here](http://owlcollab.github.io/oboformat/doc/GO.format.obo-1_4.html#S.1.6).

**Document structure**
```json
{
    "links": {
        "self": "/cvs/eco/cvterms/ECO:0000006"
    },
    "data": {
        "type": "cvterm",
        "id": "ECO:0000006",
        "attributes": {
            "name": "experimental evidence",
            "defintion": "an evidence type that is  based on....",
            "iri": "http://purl.obolibrary.org/obo/ECO_0000006",
            "comment": "It has no comment",
            "alternate_ids": ["ECO:0000014", "ECO:001125"],
            "created_by": "bob",
            "creation_date": "2009-04-13T01:32:36Z",
            "relationships": {
                "synonyms": {
                    "links": {
                        "related": "/cvs/eco/cvterms/ECO:0000006/synonyms"
                    }
                },
                "dbxrefs": {
                    "links": {
                        "self": "/cvs/eco/cvterms/ECO:0000006/relationships/dbxrefs",
                        "related": "/cvs/eco/cvterms/ECO:0000006/dbxrefs"
                    }
                },
                "objects": {
                    "links": {
                        "self": "/cvs/eco/cvterms/ECO:0000006/relationships/objects",
                        "related": "/cvs/eco/cvterms/ECO:0000006/objects"
                    }
                },
                "subjects": {
                    "links": {
                        "self": "/cvs/eco/cvterms/ECO:0000006/relationships/subjects",
                        "related": "/cvs/eco/cvterms/ECO:0000006/subjects"
                    }
                },
                "ancestors": {
                    "links": {
                        "related": "/cvs/eco/cvterms/ECO:0000006/ancestors"
                    }
                },
                "descendants": {
                    "links": {
                        "related": "/cvs/eco/cvterms/ECO:0000006/descendants"
                    }
                },
                "connected": {
                    "links": {
                        "self": "/cvs/eco/cvterms/ECO:0000006/relationships/connected",
                        "related": "/cvs/eco/cvterms/ECO:0000006/connected"
                    }
                }
            }
        }
    }
}

```

**Inclusion**

`ancestors`,`descendants` and `connected` will be paginated.

## `/cvs/:id/cvterms`
**Document structure**

```json
{
    "links": {
        "self": "/cvs/eco/cvterms?page[number]=6&page[size]=10",
        "next": "/cvs/eco/cvterms?page[number]=7&page[size]=10",
        "prev": "/cvs/eco/cvterms?page[number]=5&page[size]=10",
        "last": "/cvs/eco/cvterms?page[number]=16&page[size]=10",
        "first": "/cvs/eco/cvterms?page[number]=1&page[size]=10"
    },
    "data": [
        {
            "type": "cvterm",
            "id": "ECO:0000014",
            "attributes": { # all attributes are included
                
            },
            "links": {
                "self": "/cvs/eco/cvterms/ECO:0000014"
            }
        },
        {
            "type": "cvterm",
            "id": "ECO:0000019",
            "attributes": { # all attributes are included
            },
            "links": {
                "self": "/cvs/eco/cvterms/ECO:0000025"
            }
        }
    ],
    "meta": {
        "pagination": {
            "records": 100,
            "total": 10,
            "size": 10,
            "number": 4
        }
    }
}
```

## `/cvs/:id/predicates/:id`
Predicates represents the relationship terms(edge labels) in cv. The predicate
id is also expressed in [shorthand
format](https://github.com/oborel/obo-relations/wiki/Identifier://github.com/oborel/obo-relations/wiki/Identifiers).
It is also known as [unprefixed
id](http://owlcollab.github.io/oboformat/doc/obo-syntax.html#5.9.3) and the
formal specification is described
[here](http://owlcollab.github.io/oboformat/doc/obo-syntax.html#2.5)

**Document structure**

```json
{
    "links": {
        "self": "/cvs/eco/predicates/ECO:9000000"
    },
    "data": {
        "type": "cvterm",
        "id": "ECO:9000000",
        "attributes": {
            "name": "used_in",
            "defintion": "use me",
            "iri": "http://purl.obolibrary.org/eco/ECO_9000000",
            "comment": "Think before you use",
            "alternate_ids": ["ECO:0000019", "ECO:9000001"],
            "cyclic": "true",
            "reflexive": "false",
            "symmetric": "true",
            "anti_symmetric": "true",
            "transitive": "false",
            "relationships": {
                "synonyms": {
                    "links": {
                        "related": "/cvs/eco/predicates/ECO:0000006/synonyms"
                    }
                },
                "dbxrefs": {
                    "links": {
                        "self": "/cvs/eco/predicates/ECO:0000006/relationships/dbxrefs"
                    }
                },
                "objects": {
                    "links": {
                        "self": "/cvs/eco/predicates/ECO:0000006/relationships/objects",
                        "related": "/cvs/eco/predicates/ECO:0000006/objects"
                    }
                },
                "subjects": {
                    "links": {
                        "self": "/cvs/eco/predicates/ECO:0000006/relationships/subjects",
                        "related": "/cvs/eco/predicates/ECO:0000006/subjects"
                    }
                },
                "ancestors": {
                    "links": {
                        "related": "/cvs/eco/predicates/ECO:0000006/ancestors"
                    }
                },
                "descendants": {
                    "links": {
                        "related": "/cvs/eco/predicates/ECO:0000006/descendants"
                    }
                },
                "connected": {
                    "links": {
                        "self": "/cvs/eco/predicates/ECO:0000006/relationships/connected",
                        "related": "/cvs/eco/predicates/ECO:0000006/connected"
                    }
                },
                "transitive_over": {
                    "links": {
                        "related": "/cvs/eco/predicates/ECO:0000004"
                    }
                },
                "inverse_of": {
                    "links": {
                        "related": "/cvs/eco/predicates/ECO:0000005"
                    }
                },
                "domain": {
                    "links": {
                        "related": "/cvs/eco/cvterms/ECO:0000000"
                    }
                },
                "range": {
                    "links": {
                        "related": "/cvs/eco/cvterms/ECO:0000001"
                    }
                }
            }
        }
    }
}
```

## `/cvs/:id/predicates`

**Document structure**

```json
{
    "links": {
        "self": "/cvs/eco/predicates?page[number]=6&page[size]=10",
        "next": "/cvs/eco/predicates?page[number]=7&page[size]=10",
        "prev": "/cvs/eco/predicates?page[number]=5&page[size]=10",
        "last": "/cvs/eco/predicates?page[number]=16&page[size]=10",
        "first": "/cvs/eco/predicates?page[number]=1&page[size]=10"
    },
    "data": [
        {
            "type": "cvterm",
            "id": "ECO:9000000",
            "attributes": { # all attributes are included
            },
            "links": {
                "self": "/cvs/eco/predicates/ECO:9000000"
            }
        },
        {
            "type": "cvterm",
            "id": "ECO:0000025",
            "attributes": { # all attributes are included
            },
            "links": {
                "self": "/cvs/eco/predicates/ECO:9000025"
            }
        }
    ]
}

```

## Relationship resources
Depending on the relationships, few of them represents individual resources
and can be manipulated independently of the related resources. Those distinct
resources are better explained with a diagram in the *related resources* page. 

The document structure of those resources are more or less identical to their
primary resources. Though they have a lengthy resource url, those really don't
have to remembered as they could be easily retrieved from their primary
resources anyway.
* [cv related resources](cv-related.md)

