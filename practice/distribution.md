# 2.1.0 Distribution

# 2.1.1 IPFS
In order for data to be something we all hold together, we need to build all of our technology on a distributed network that removes the single-point-of-failure problem.

Our library can and should work with data from all over the place, but we'll use IPFS as the lowest-common-denominator that other services integrate because it has five properties that we hold as vital:

* **Open** - IPFS is published as open source
* **Distributed** - It's a distributed network.
* **Content-Addressed** - IPFS uses "data-fingerprints" to index content.
* **Extensible** - We can build on top of IPFS.

# 2.1.2 Packages as Datasets
It's tempting to turn this library into one giant "package manager", that tracks files together as a method of managing complexity. While our system will support packaging data together, "files" (individual byte-streams) must be the most granular unit we work with.

Consider the following two files:

    a.txt
    b.txt

If we put those two files in a "package":

    package-a
      a.txt
      b.txt

We don't have 1 thing (the package), we now have three things, `a.txt`, `b.txt`, and `package-a`. This problem is shows up when we declare `package-b`:

    package-b
      b.txt
      c.txt

Now `b.txt` is in two places. If b.txt changes, that change will affect `b.txt`, `package-a`, and `package-b`. If we declare rules about how "packages" work, every service we work with will need to understand whatever rules we write, and adjust & react to each of these changes to keep their records up to date.

We need some sort of "folder", or "package" mechanism because managing an ocean of individual files is just silly-pants. So the answer is to require that anything that wants to look like a "package" be declared as a dataset that uses an already available format.

For example, we can publish a new file `package-a.csv`, that has the following contents:

    file,info
    a.txt,"this is a description of a.txt"
    b.txt,"this is a description of b.txt"

This has major advantages. Many, many software environments know how to work with .csv files, which means they can grock our "package" system without additional work. Also, eshaach "package" can declare whatever data is relevant to that collection of files, placing no limits on extensibility, to keep "packages" consistent, we use the convention of having "file" be the _first entry in each row_. The final upside is the "three things" are now explicit. We'll have:

    package-a.csv
    a.txt
    b.txt

All of which are files, and if we so desire later on we can just as easily publish `package-a.json`, with content stored in json format instead of csv.

It's worth noting "file" will actually be "hash" because we're working in a content-addressed system, we're calling it "file" here because `abdcd3a23456789765bacdfe3637442373y...` is just nasty, and makes it tougher to explain what's going on.

# 2.1.4 This stuff is new & complicated.
We adknowledge that this is very complex, and consider it our job to make these technologies easy to work with by building abstractions on top of these more difficult-to-use bits. It shouldn't be a requirement that a volunteer even know what IPFS is in order to contribute. Once we're up to speed it should get easier & easier for people of any skill level to contribute to the project.