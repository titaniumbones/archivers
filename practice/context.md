# 2.3.0 Context

### 2.3.1 Metablocks
"Metablocks" is blockchain-inspired spec for writing timeseries attributed metadata. Given any subject (a content-addressed hash under the hood), any user can create a chain of timestamped metablocks that constructs their metadata in relation the the subject. 

Metablocks are a spec meant to built-upon. We shouldn't have users working on metadata through webapps or other user interfaces deal directly with metablocks. Instead they should be able to just input metadata & have the service record each of those additions as metablocks under the hood.

### 2.3.2 Metablock Subjects
Metblock subjects should be _ipns paths_, namely paths to an object history.

### 2.3.3 Consensus
Given any collection of metablocks it's possible to compute a _consensus object_, which is all of the top level metadata keys tallied by the number of metablocks that share the same value. 

Given two pieces of metadata about the same subject (in this case, say a file called `book.txt`):

    {
      "title" : "A Tale of Two Cities",
      "pages" : 234
    }

And:

    {
      "title" : "A Tale of Two Cities",
      "pages" : 456
    }

Their _consensus object_ would look like this:

    {
      "title" : {
        "A Tale of Two Cities" : 2
      }
      "pages" : {
        "234" : 1,
        "456" : 1
      }
    }

In practice the values will be hashes, but it's easier to just work with the real values for examples.

We have now generated a single metadata object from multiple metadata contributions. Where both metadata objects "agree" that value for `title` is "A Tale of Two Cities", they differ on the `pages` key.
