# Introduction

MaxMind DB is a binary file format that stores data indexed by IP address
subnets (IPv4 or IPv6).

This repository was inspired of [MaxMind's spec of their DB format](https://github.com/maxmind/MaxMind-DB).

It contains a simple script that generates a sample City database from a JSON
file.

# MMDB file generator

The Perl script `json2mmdb.pl` was based on [MaxMind's test data generator](https://github.com/maxmind/MaxMind-DB/blob/master/test-data/write-test-data.pl).

Run Perl using `perlbrew`. Follow [install instructions](https://perlbrew.pl/).
(The copy-pastable `curl` command is recommended.)

```sh
# Initialize Perl environment
perlbrew init
perlbrew install perl-5.16.0
perlbrew switch perl-5.16.0

# Install CPAN Minus
curl -L https://cpanmin.us | perl - App::cpanminus

# Install Perl modules required by the script
perlbrew exec cpanm Devel::Refcount MaxMind::DB::Reader::XS MaxMind::DB::Writer::Tree Net::Works::Network GeoIP2 Data::Printer Text::CSV_XS File::Slurp JSON::XS

# Run MMDB file generator
./json2mmdb.pl
```

It generates the file `GeoIP2-City-sample.mmdb` that can be used as sample database in tests.

You can also pass a file name (without extension) as argument to the command:

```sh
./json2mmdb.pl GeoIP2-City # Will generate GeoIP2-City.mmdb file from GeoIP2-City.json
```
