A torrent file is an independent session of transfer. To distribute a file, say an Ubuntu image, we would create a torrent holding the meta information about it while the actual content is split into pieces and distributed in the network.

## Lifecycle of a Torrent

Torrent is alive so long as there is at least a seeder, seeding the pieces in the network. Once all the nodes who can share the pieces have left the network, the download of the network stops, and the torrent ends until a new seeder pops up.

## What torrent file holds

The `.torrent` file holds all critical meta yet static information about the content, like

- `announce` - holds the URL of the tracker
- `created by` - name and version of the program who created it
- `creation date` - time at which the torrent was created
- `encoding` - encoding of the strings in `info` dictionary
- `comment` - some additional comments
- `info` - a dictionary that describes files in the torrent

The `info` dictionary holds the information about the file that is being shared through the torrent. If the torrent is about the Ubuntu image, it will hold info like `name`, `length`, and `md5sum` of the actual file.

Given that the file is split into equal-length pieces, the `info` dictionary also holds

- `pieces` - SHA1 of every piece of the file concatenated
- `piece length` - number of bytes in each piece

This information is used in identifying and fetching pieces from the network.

## Bencoding

Torrent files are encoded with a custom encoding called Bencoding. It supports data types such as Strings, Integers, List, and Dictionaries (which can only hold string keys).

Strings are encoded as `<length>:<string>`. Hence, a string `arpit` will be encoded as `5:arpit`.

Integers are encoded as `i<integer>e`. Hence, an integer `10` will be encoded as `i10e`.

Lists are encoded as `l<becoded values>e`. Hence, the list `["a","b", 1 ]` will be encoded as `l1:a1:bi1e1`.

Dictionaries are encoded as `d<key1><value1><key2><value2>e`. Hence, a dictionary `{"a": 1, "b": 2}` will be encoded as `d1:ai1e1:bi2ee`.