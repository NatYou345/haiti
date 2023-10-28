# Usage

## CLI

```
$ haiti -h
HAITI (HAsh IdenTifIer) v2.0.0

Usage:
  haiti [options] list
  haiti samples (<ref> | <name>)
  haiti [options] <hash>
  haiti --ascii-art
  haiti -h | --help
  haiti --version

Commands:
  samples         Display hash samples for the given type
  list            Display a list of all the available hash types

Parameters:
  <hash>          Hash string to identify, read from STDIN if equal to "-"
  <ref>           hashcat or john the ripper reference
  <name>          Hash type name

Options:
  --no-color      Disable colorized output (NO_COLOR environment variable is respected too)
  -e, --extended  List all possible hash algorithms including ones using salt
  --short         Display in a short format: do not display hashcat and john the ripper references
  --hashcat-only  Show only hashcat references
  --john-only     Show only john the ripper references
  --ascii-art       Display the logo in colored ascii-art
  --debug         Display arguments
  -h, --help      Show this screen
  --version       Show version

Examples:
  haiti -e d41d8cd98f00b204e9800998ecf8427e
  haiti --no-color --short d41d8cd98f00b204e9800998ecf8427e
  b2sum /etc/os-release | awk '{print $1}' | haiti -
  haiti samples crc32

Project:
  author (https://pwn.by/noraj / https://twitter.com/noraj_rawsec)
  source (https://github.com/noraj/haiti)
  documentation (https://noraj.github.io/haiti)
```

## Library

Identify hashes:

```ruby
require 'haiti'

# Instantiate a HashIdentifier object that will automatically identify
# the hash type
hi = HashIdentifier.new('786a02f742015903c6c6fd852552d272912f4740e15847618a86e217f71f5419d25e1031afee585313896444934eb04b903a685b1448b755d56f701afe9be2ce')

# Loop over the hash type candidates and retrieve data
hi.type.each do |type|
  # name of the hash function
  name = type.name
  # hashcat ID
  hashcat_id = type.hashcat
  # John the Ripper reference
  john_ref = type.john
  # Hash with salt
  extended = type.extended
  # Samples / Examples of hashes of that type
  samples = type.samples
end
```

Find hash samples for a given hash type (by name or hashcat/john the ripper reference):

```ruby
require 'haiti'

HashIdentifier.samples('crc32')
HashIdentifier.samples(1100)
HashIdentifier.samples('MD6-256')
```

## Console

Launch `irb` with the library loaded.

```
$ haiti_console
irb(main):001:0>
```
