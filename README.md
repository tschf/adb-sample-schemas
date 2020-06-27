# Oracle Database Sample Schemas - For Autonomous

This is a variation on Oracle db-sample-schemas. It uses sys for its connections
where ATP expects a connection against admin.

The copyright notice from the original code base:

Copyright (c) 2019 Oracle

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## Key Points about Differences

1. The `sh` schema already exists, and is not modifiable. So that we have more 
flexibility, we are renaming this `sales_hist`.
2. The order entry (`oe`) schema tries to grant the role XDBADMIN to the schema.
It is not possible for us to give this grant, so the whole XML part of this schema
has been ommitted.
3. Info Exchange (`ix`) schema tries to do a bunch of ADM things. These grants were
failing as I was testing, so have intentionally been excluded from the release.
While this is installed, I think it doesn't serve any use at this stage.

## Installing the sample schema - steps

Requirements: sqlplus + sqlldr

1. Create an ATP
2. Clone this repo
3. Update paths based on where you cloned it to:

```sh
perl -p -i.bak -e 's#__SUB__CWD__#'$(pwd)'#g' *.sql */*.sql */*.dat
```

4. Connecct to your DB as admin user:

```
sqlplus admin/"7VFFYxaVxESzgbMZtdzwYyLEFAQrLm"@db202006251431_high
```

Run the `mksample` script.

```
@mksample "mTaxT7sHHzxM9GDRkD6c3BGRtR9sDk" "Abc2020Hxxxxxxxxxxx" "Abc2020Oxxxxxxxxxxx" "Abc2020Pxxxxxxxxxxx" "Abc2020xxxxxxxxxxxI" "Abc2020Sxxxxxxxxxxx" "Abc2020Bxxxxxxxxxxx" data temp /tmp/log2020_3 sampledb_high
```

Params are:

1. admin schema password
2. HR pasword
3. OE password
4. PM password
5. IX password
6. SALES_HIST password
7. BI password
8. Data tablespace
9. Temp tablespace
10. Log folder for installation process
11. Connect string (TNS Name entry)