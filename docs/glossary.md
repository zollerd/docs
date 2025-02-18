# Glossary

After years of providing services and products on firmware
market we recognize that it is poisoned by incorrect and
confusing terminology. In following glossary we would like to
explain most used terms from Dasharo Documentation. We try to
refer to standards, literature and community best practices to
keep content added by us minimalistic.

## Embedded Firmware

We use definition explained in first chapter of
["Embedded Firmware Solutions"](https://www.apress.com/gp/book/9781484200711) book
by Jiming Sun, Marc Jones, Stefan Reinauer and Vincent Zimmer.

Firmware is "layer of software between the hardware and the
operating system (OS), with the main purpose to initialize and
abstract enough hardware so that the operating systems and
their drivers can further configure the hardware to its full
functionality."

Rising complexity of hardware initialization and need for its
manageability created need for BMC (Board Management
Controllers), EC (Environmental Controllers) and even more
specialized one like USB Power Delivery firmware. What may
make that firmware also covered by above definition.

## Dasharo Hardware Compatibility List Report

Dasharo HCL Report dumps most important information about platform and backup
SPI NOR flash. Gathered information can be used for future analysis, debugging
and recovery. Optionally scripts upload dump to Dasharo HCL Backup Server, so
Dasharo Team can improve open source firmware product line and support
customers in case of issues.

As temporary solution we use 3mdeb NextCloud as Dasharo HCL Backup Server.

Dasharo HCL Reports are also used during open source firmware port feasibilty
analysis, so if you are interested in Dasharo support for your hardware, feel
free to [reach us](mailto:leads@3mdeb.com).

Please note Dasharo HCL Report may contain sensitive information like serial
numbers. Please do not make this information public. Dasharo Team respect your
privacy.

## Dasharo Blobs Transmission

Unfortunately, some hardware platforms cannot be fully functional without
binary blobs in the firmware. Some binary blobs have no EULA or any other
license discussing redistributability. To avoid issues, Dasharo Blobs
Transmission scripts extract blobs from SPI NOR flash backup and patch Dasharo
open-source firmware distribution before initial deployment.
