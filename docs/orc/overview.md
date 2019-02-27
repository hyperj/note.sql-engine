# Overview

ORC（Optimized Row Columnar）使用特定的`Readers`和`Writers`，通过轻量级的数据压缩，如字典编码，位组装，差分编码和游程编码，而显著减小的生成文件，也可以配合zlib、Snappy使用。ORC 支持投影、下推、向量化、轻量级索引等特性。

![](../assets/images/orc/OrcFileLayout.png)

## File Tail

- Postscript
- Footer
    - Stripe Information
    - Type Information
    - Column Statistics
    - User Metadata
    - File Metadata

## Compression

## Run Length Encoding

- Base 128 Varint
- Byte Run Length Encoding
- Boolean Run Length Encoding
- Integer Run Length Encoding, version 1
- Integer Run Length Encoding, version 2
    - Short Repeat - used for short sequences with repeated values
    - Direct - used for random sequences with a fixed bit width
    - Patched Base - used for random sequences with a variable bit width
    - Delta - used for monotonically increasing or decreasing sequences

## Stripes

## Column Encodings

- SmallInt, Int, and BigInt Columns
- Float and Double Columns
- String, Char, and VarChar Columns
- Boolean Columns
- TinyInt Columns
- Binary Columns
- Decimal Columns
- Date Columns
- Timestamp Columns
- Struct Columns
- List Columns
- Map Columns
- Union Columns

## Indexes

- Row Group Index
- Bloom Filter Index

## Reference

- [Docs](http://orc.apache.org/docs/)
- [Github](https://github.com/apache/orc)
- [ORC Specification](https://orc.apache.org/specification/)
- [orc_proto.proto](https://s.apache.org/orc_proto)