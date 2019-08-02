# A Docker container for Gremlin 3.x


This Docker file creates a container running [Gremlin Tinkerpop](https://github.com/apache/tinkerpop), with a TinkerGraph and configured for use with Python ([gremlin-python](http://tinkerpop.apache.org/docs/current/reference/#gremlin-python)) under Ubuntu OS.
To build it, run the following command:
```
docker build -t gremlin-container .
```

The graph database is configured using the files in the "files/" folder.
Gremlin server will serve resquests on port 8182. The graph will be saved into a graphson file, each time the server is shut down.
It will also try to load the graph from this file (if it exists) each time the server is started.
See the [TinkerGraph configuration section](http://tinkerpop.apache.org/docs/current/reference/#_configuration_2) for more details.


You can then start the container using:
```
docker run -p 8182:8182 -v ~/:/graph_file -it --name gremlin gremlin-container
```

The server can be accessed on port 8182 and the graphson file will be saved in the home directory `~/`.
Alternatively, you can pull the image from DockerHub [here](https://hub.docker.com/r/bricaud/gremlin-server/).


A demo showing how to access the database with python is provided.
Python 3 is required as well as the gremlin-python module (use the version
that matches the gremlin-server version.) This
module
can be installed using:
```
pip install gremlinpython==3.4.b
```

To run the demo (and make a minimal test), simply write in the console:
```
python test_graph.py
```

A second in-memory graph instance named `g1` is also provided which can be used by unit tests in your application.
