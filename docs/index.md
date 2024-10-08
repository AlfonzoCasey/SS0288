```
======================================================================
    Microsoft Product Support Services Application Note (Text File)
               SS0288: RELOCATABLE OBJECT MODULE FORMAT
======================================================================
   
This application note is divided into six text files, SS0288_1.TXT
through SS0288_6.TXT. The following provides a reference to the
text file location (section) of the contents.
   
                           TABLE OF CONTENTS
                          ==================
                                   
                                                               Section
                                                               -------
Introduction                                                         1
The Object Record Format                                             1
Frequent Object Record Subfields                                     1
Order of Records                                                     1
Record Specifics                                                     1
80H THEADR--Translator Header Record                                 1
82H LHEADR--Library Module Header Record                             2
88H COMENT--Comment Record                                           2
88H IMPDEF--Import Definition Record (Comment Class A0, Subtype 01)  2
88H EXPDEF--Export Definition Record (Comment Class A0, Subtype 02)  2
88H INCDEF--Incremental Compilation Record (Cmnt Class A0, Sub 03)   2
88H LNKDIR--C++ Directives Record (Comment Class A0, Subtype 05)     2
88H LIBMOD--Library Module Name Record (Comment Class A3)            2
88H EXESTR--Executable String Record (Comment Class A4)              2
88H INCERR--Incremental Compilation Error (Comment Class A6)         2
88H NOPAD--No Segment Padding (Comment Class A7)                     2
88H WKEXT--Weak Extern Record (Comment Class A8)                     2
88H LZEXT--Lazy Extern Record (Comment Class A9)                     3
88H PharLap Format Record (Comment Class AA)                         3
8AH or 8BH MODEND--Module End Record                                 3
8CH EXTDEF--External Names Definition Record                         3
8EH TYPDEF--Type Definition Record                                   3
90H or 91H PUBDEF--Public Names Definition Record                    3
94H or 95H LINNUM--Line Numbers Record                               3
96H LNAMES--List of Names Record                                     4
98H or 99H SEGDEF--Segment Definition Record                         4
9AH GRPDEF--Group Definition Record                                  4
9CH or 9DH FIXUPP--Fixup Record                                      4
A0H or A1H LEDATA--Logical Enumerated Data Record                    5
A2H or A3H LIDATA--Logical Iterated Data Record                      5
B0H COMDEF--Communal Names Definition Record                         5
B2H or B3H BAKPAT--Backpatch Record                                  5
B4H or B5H LEXTDEF--Local External Names Definition Record           5
B6H or B7H LPUBDEF--Local Public Names Definition Record             5
B8H LCOMDEF--Local Communal Names Definition Record                  5
BCH CEXTDEF--COMDAT External Names Definition Record                 5
C2H or C3H COMDAT--Initialized Communal Data Record                  5
C4H or C5H LINSYM--Symbol Line Numbers Record                        6
C6H ALIAS--Alias Definition Record                                   6
C8H or C9H NBKPAT--Named Backpatch Record                            6
CAH LLNAMES--Local Logical Names Definition Record                   6
Appendix 1: CodeView Extensions                                      6
Appendix 2: Microsoft MS-DOS Library Format                          6

======================================================================
    Microsoft Product Support Services Application Note (Text File)
               SS0288: RELOCATABLE OBJECT MODULE FORMAT
======================================================================
                                                   Revision Date: 5/92
                                                      No Disk Included

The following information applies to to the Microsoft products listed
below.

 --------------------------------------------------------------------
| INFORMATION PROVIDED IN THIS DOCUMENT AND ANY SOFTWARE THAT MAY    |
| ACCOMPANY THIS DOCUMENT (collectively referred to as an            |
| Application Note) IS PROVIDED "AS IS" WITHOUT WARRANTY OF ANY      |
| KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO    |
| THE IMPLIED WARRANTIES OF MERCHANTABILITY AND/OR FITNESS FOR A     |
| PARTICULAR PURPOSE. The user assumes the entire risk as to the     |
| accuracy and the use of this Application Note. This Application    |
| Note may be copied and distributed subject to the following        |
| conditions: 1) All text must be copied without modification and    |
| all pages must be included; 2) If software is included, all files  |
| on the disk(s) must be copied without modification [the MS-DOS(R)  |
| utility DISKCOPY is appropriate for this purpose]; 3) All          |
| components of this Application Note must be distributed together;  |
| and 4) This Application Note may not be distributed for profit.    |
|                                                                    |
|    Copyright 1992 Microsoft Corporation.  All Rights Reserved.     |
|    Microsoft, MS-DOS, QuickC, and QuickPascal are registered       |
|    trademarks and Windows, QuickBasic, and Visual Basic are        |
|    trademarks of Microsoft Corporation.                            |
|                                                                    |
 --------------------------------------------------------------------


APPLICABLE PRODUCTS
===================

This application note applies to all versions of the following
Microsoft language products:

   Microsoft Basic
   Microsoft C
   Microsoft C++
   Microsoft COBOL
   Microsoft FORTRAN
   Microsoft Macro Assembler (MASM)
   Microsoft Pascal
   Microsoft QuickBasic(TM)
   Microsoft QuickC(C)
   Microsoft QuickC for Windows(TM)
   Microsoft QuickPascal(C)
   Microsoft Visual Basic(TM)
   
   
                           TABLE OF CONTENTS
                          ==================
                                   
                                                               Section
                                                               -------
Introduction                                                         1
The Object Record Format                                             1
Frequent Object Record Subfields                                     1
Order of Records                                                     1
Record Specifics                                                     1
80H THEADR--Translator Header Record                                 1
82H LHEADR--Library Module Header Record                             2
88H COMENT--Comment Record                                           2
88H IMPDEF--Import Definition Record (Comment Class A0, Subtype 01)  2
88H EXPDEF--Export Definition Record (Comment Class A0, Subtype 02)  2
88H INCDEF--Incremental Compilation Record (Cmnt Class A0, Sub 03)   2
88H LNKDIR--C++ Directives Record (Comment Class A0, Subtype 05)     2
88H LIBMOD--Library Module Name Record (Comment Class A3)            2
88H EXESTR--Executable String Record (Comment Class A4)              2
88H INCERR--Incremental Compilation Error (Comment Class A6)         2
88H NOPAD--No Segment Padding (Comment Class A7)                     2
88H WKEXT--Weak Extern Record (Comment Class A8)                     2
88H LZEXT--Lazy Extern Record (Comment Class A9)                     3
88H PharLap Format Record (Comment Class AA)                         3
8AH or 8BH MODEND--Module End Record                                 3
8CH EXTDEF--External Names Definition Record                         3
8EH TYPDEF--Type Definition Record                                   3
90H or 91H PUBDEF--Public Names Definition Record                    3
94H or 95H LINNUM--Line Numbers Record                               3
96H LNAMES--List of Names Record                                     4
98H or 99H SEGDEF--Segment Definition Record                         4
9AH GRPDEF--Group Definition Record                                  4
9CH or 9DH FIXUPP--Fixup Record                                      4
A0H or A1H LEDATA--Logical Enumerated Data Record                    5
A2H or A3H LIDATA--Logical Iterated Data Record                      5
B0H COMDEF--Communal Names Definition Record                         5
B2H or B3H BAKPAT--Backpatch Record                                  5
B4H or B5H LEXTDEF--Local External Names Definition Record           5
B6H or B7H LPUBDEF--Local Public Names Definition Record             5
B8H LCOMDEF--Local Communal Names Definition Record                  5
BCH CEXTDEF--COMDAT External Names Definition Record                 5
C2H or C3H COMDAT--Initialized Communal Data Record                  5
C4H or C5H LINSYM--Symbol Line Numbers Record                        6
C6H ALIAS--Alias Definition Record                                   6
C8H or C9H NBKPAT--Named Backpatch Record                            6
CAH LLNAMES--Local Logical Names Definition Record                   6
Appendix 1: CodeView Extensions                                      6
Appendix 2: Microsoft MS-DOS Library Format                          6


INTRODUCTION
============

This document is intended to serve a purpose that up until now has
been performed by the LINK source code: to be the official definition
for the object module format (the information inside .OBJ files)
supported by Microsoft's language products. The goal is to include all
currently used or obsolete OMF record types, all currently used or
obsolete field values, and all extensions made by Microsoft, IBM, and
others.

The information provided here has been consolidated from many other
documents: "The MS-DOS Encyclopedia" by Microsoft Press, an OMF386
document from IBM that was made available by the Joint Development
Agreement, the "PharLap 386|Link Reference Manual," the Intel 8086
object module specification (Intel Technical Specification 121748-
001), and internal Microsoft documents. Where there have been
conflicts, the current LINK source code has decided which information
is correct.

The  audience  for  this document is expected to  be  technical,  with
background knowledge of the process by which source code is  converted
into an executable file in the MS-DOS or OS/2 environment. If you need
more  tutorial information, "The MS-DOS Encyclopedia" is a good  place
to start.


THE OBJECT RECORD FORMAT
========================

Record Format
-------------

All object records conform to the following format:

                          <------Record Length in Bytes----->
   1         2            <variable>    1
   Record    Record       Record        Checksum or 0
   Type      Length       Contents

The Record Type field is a 1-byte field containing the hexadecimal
number that identifies the type of object record.

The Record Length field is a 2-byte field that gives the length of the
remainder of the object record in bytes (excluding the bytes in the
Record Type and Record Length fields). The record length is stored
with the low-order byte first. An entire record occupies 3 bytes plus
the number of bytes in the Record Length field.

The Record Contents field varies in size and format, depending on the
record type.

The Checksum field is a 1-byte field that contains the negative sum
(modulo 256) of all other bytes in the record. In other words, the
checksum byte is calculated so that the low-order byte of the sum of
all the bytes in the record, including the checksum byte, equals 0.
Overflow is ignored. Some compilers write a 0 byte rather than
computing the checksum, so either form should be accepted by programs
that process object modules.
  
  NOTES
  
  The maximum size of the entire record (unless otherwise noted for
  specific record types) is 1024 bytes.

  For LINK386, the format is determined by the least-significant bit
  of the Record Type field. An odd Record Type indicates that certain
  numeric fields within the record contain 32-bit values; an even
  Record Type indicates that those fields contain 16-bit values. The
  affected fields are described with each record. Note that this
  principle does not govern the Use32/Use16 segment attribute (which
  is set in the ACBP byte of SEGDEF records); it simply specifies the
  size of certain numeric fields within the record. It is possible to
  use 16-bit OMF records to generate 32-bit segments, or vice versa.

  LINK ignores the value of the checksum byte, but some other
  utilities do not. Microsoft's Quick languages write a 0 byte instead
  of computing a checksum.


FREQUENT OBJECT RECORD SUBFIELDS
================================

The contents of each record are determined by the record type, but
certain subfields appear frequently enough to be explained separately.
The format of such fields is below.

Names
-----

A name string is encoded as an 8-bit unsigned count followed by a
string of count characters. The character set is usually some ASCII
subset. A null name is specified by a single byte of 0 (indicating a
string of length 0).

Indexed References
------------------

Certain items are ordered by occurrence and are referenced by index.
The first occurrence of the item has index number 1. Index fields may
contain 0 (indicating that they are not present) or values from 1
through 7FFF. The index number field in an object record can be either
1 or 2 bytes long. If the number is in the range 0-7FH, the high-order
bit (bit 7) is 0 and the low-order bits contain the index number, so
the field is only 1 byte long. If the index number is in the range 80-
7FFFH, the field is 2 bytes long. The high-order bit of the first byte
in the field is set to 1, and the high-order byte of the index number
(which must be in the range 0-7FH) fits in the remaining 7 bits. The
low-order byte of the index number is specified in the second byte of
the field. The code to decode an index is:
   
   if (first_byte & 0x80)
        index_word = (first_byte & 7F) * 0x100 + second_byte;
   else
        index_word = first_byte;

Type Indexes
------------

Type Index fields occupy 1 or 2 bytes and occur in PUBDEF, LPUBDEF,
COMDEF, LCOMDEF, EXTDEF, and LEXTDEF records. They are encoded as
described above for indexed references, but the interpretation of the
values stored is governed by whether the module has the "new" or "old"
object module format.

"Old" versions of the OMF (indicated by lack of a COMENT record with
comment class A1), have Type Index fields that contain indexes into
previously seen TYPDEF records. This format is no longer produced by
Microsoft products and is ignored by LINK if it is present. See the
section of this document on TYPDEF records for details on how this was
used.

"New" versions of the OMF (indicated by the presence of a COMENT
record with comment class A1), have Type Index fields that contain
proprietary CodeView information. For more information on CodeView,
see Appendix 1.
  
  NOTE: Currently, the linker does not perform type checking.

Ordered Collections
-------------------

Certain records and record groups are ordered so that the records may
be referred to with indexes (the format of indexes is described in the
"Indexed References" section of this document). The same format is
used whether an index refers to names, logical segments, or other
items.

The overall ordering is obtained from the order of the records within
the file together with the ordering of repeated fields within these
records. Such ordered collections are referenced by index, counting
from 1 (index 0 indicates unknown or not specified).

For example, there may be many LNAMES records within a module, and
each of those records may contain many names. The names are indexed
starting at 1 for the first name in the first LNAMES record
encountered while reading the file, 2 for the second name in the first
record, and so forth, with the highest index for the last name in the
last LNAMES record encountered.

The ordered collections are:

   Names       Ordered by occurrence of LNAMES records and
               names within each. Referenced as a name
               index.
               
   Logical     Ordered by occurrence of SEGDEF records in
   Segments    file. Referenced as a segment index.
               
   Groups      Ordered by occurrence of GRPDEF records in
               file. Referenced as a group index.
               
   External    Ordered by occurrence of EXTDEF, COMDEF,
   Symbols     LEXTDEF, and LCOMDEF records and symbols
               within each. Referenced as an external name
               index (in FIXUP subrecords).
               

Numeric 2- and 4-Byte Fields
----------------------------

Words and double words (16- and 32-bit quantities) are stored in Intel
byte order (lowest address is least significant).

Certain records, notably SEGDEF, PUBDEF, LPUBDEF, LINNUM, LEDATA,
LIDATA, FIXUPP, and MODEND, contain size, offset, and displacement
values that may be 32-bit quantities for Use32 segments. The encoding
is as follows:

 - When the least-significant bit of the record type byte is set (that
   is, the record type is an odd number), the numeric fields are 4
   bytes.

 - When the least-significant bit of the record type byte is clear,
   the fields occupy 2 bytes. The values are zero-extended when
   applied to Use32 segments.

  NOTE: See the description of SEGDEF records in this document for an
  explanation of Use16/Use32 segments.


ORDER OF RECORDS
================

The sequence in which the types of object records appear in an object
module is fairly flexible in some respects. Several record types are
optional, and if the type of information they carry is unnecessary,
they are omitted from the object module. In addition, most object
record types can occur more than once in the same object module. And
because object records are variable in length, it is often possible to
choose between combining information into one large record or breaking
it down into several smaller records of the same type.

An important constraint on the order in which object records appear is
the need for some types of object records to refer to information
contained in other records. Because the linker processes the records
sequentially, object records containing such information must precede
the records that refer to the information. For example, two types of
object records, SEGDEF and GRPDEF, refer to the names contained in an
LNAMES record. Thus, an LNAMES record must appear before any SEGDEF or
GRPDEF records that refer to it so that the names in the LNAMES record
are known to the linker by the time it processes the SEGDEF or GRPDEF
records.

The record order is chosen so that linker passes through an object
module are minimized. Microsoft LINK makes two passes through the
object modules: the first pass may be cut short by the presence of the
Link Pass Separator COMENT record; the second pass processes all
records.

For greatest linking speed, all symbolic information should occur at
the start of the object module. This order is recommended but not
mandatory. The general ordering is:

Identifier Record(s)
--------------------

    NOTE: This must be the first record.
   
   THEADR or LHEADR record

Records Processed by LINK Pass 1
--------------------------------
   
The following records may occur in any order but they must precede the
Link Pass Separator if it is present:
   
   COMENT records identifying object format and extensions
   
   COMENT records other than Link Pass Separator comment
   
   LNAMES or LLNAMES records providing ordered name list
   
   SEGDEF records providing ordered list of program segments
   
   GRPDEF records providing ordered list of logical segments
   
   TYPDEF records (obsolete)
   
   ALIAS records
   
   PUBDEF records locating and naming public symbols
   
   LPUBDEF records locating and naming private symbols
   
   COMDEF, LCOMDEF, EXTDEF, LEXTDEF, and CEXTDEF records
    
    NOTE: This group of records is indexed together, so external name
    index fields in FIXUPP records may refer to any of the record
    types listed.

Link Pass Separator (Optional)
------------------------------

COMENT class A2 record indicating that Pass 1 of the linker is
complete. When this record is encountered, LINK stops reading the
object file in Pass 1; no records after this comment are read in Pass
1. All the records listed above must come before this COMENT record.

For greater linking speed, all LIDATA, LEDATA, FIXUPP, BAKPAT, INCDEF,
and LINNUM records should come after the A2 COMENT record, but this is
not required. In LINK, Pass 2 begins again at the start of the object
module, so these records are processed in Pass 2 no matter where they
are placed in the object module.

Records Ignored by LINK Pass 1 and Processed by LINK Pass 2
-----------------------------------------------------------
   
The following records may come before or after the Link Pass
Separator:
   
   LIDATA, LEDATA, or COMDAT records followed by applicable FIXUPP
   records
   
   FIXUPP records containing only THREAD subrecords
   
   BAKPAT and NBKPAT FIXUPP records
   
   COMENT class A0, subrecord type 03 (INCDEF) records containing
   incremental compilation information for FIXUPP and LINNUM records
   
   LINNUM and LINSYM records providing line number and program code or
   data association

Terminator
----------
   
   MODEND record indicating end of module with optional start address
   

RECORD SPECIFICS
================

Details of each record (form and content), together with historical
notes and comments on usage, are presented in the sections that
follow.

Conflicts between various OMFs that overlap in their use of record
types or fields are marked.

Below is a combined list of record types defined by the Intel 8086 OMF
specification and record types added after that specification was
finished. Titles in square brackets ([]) indicate record types that
have been implemented and that are described in this document. Titles
not in square brackets indicate record types that have not been
implemented and are followed by a paragraph of description from the
Intel specification.

For unimplemented record types, a subtle distinction is made between
records that LINK ignores and those for which LINK generates an
"illegal object format" error condition.

Records Currently Defined
-------------------------
   
   6EH     RHEADR   R-Module Header Record
                    This record serves to identify a module that has
                    been processed (output) by LINK-86/LOCATE-86. It
                    also specifies the module attributes and gives
                    information on memory usage and need. This record
                    type is ignored by Microsoft LINK.
                    
   70H     REGINT   Register Initialization Record
                    This record provides information about the 8086
                    register/register-pairs: CS and IP, SS and SP, DS
                    and ES. The purpose of this information is for a
                    loader to set the necessary registers for
                    initiation of execution. This record type is
                    ignored by Microsoft LINK.
                    
   72H     REDATA   Relocatable Enumerated Data Record
                    This record provides contiguous data from which a
                    portion of an 8086 memory image may eventually be
                    constructed. The data may be loaded directly by
                    an 8086 loader, with perhaps some base fixups.
                    The record may also be called a Load-Time
                    Locatable (LTL) Enumerated Data Record. This
                    record type is ignored by Microsoft LINK.
                    
   74H     RIDATA   Relocatable Iterated Data Record
                    This record provides contiguous data from which a
                    portion of an 8086 memory image may eventually be
                    constructed. The data may be loaded directly by
                    an 8086 loader, but data bytes within the record
                    may require expansion. The record may also be
                    called a Load-Time Locatable (LTL) Iterated Data
                    Record. This record type is ignored by Microsoft
                    LINK.
                    
   76H     OVLDEF   Overlay Definition Record
                    This record provides the overlay's name, its
                    location in the object file, and its attributes.
                    A loader may use this record to locate the data
                    records of the overlay in the object file. This
                    record type is ignored by Microsoft LINK.
                    
   78H     ENDREC   End Record
                    This record is used to denote the end of a set of
                    records, such as a block or an overlay. This
                    record type is ignored by Microsoft LINK.
                    
   7AH     BLKDEF   Block Definition Record
                    This record provides information about blocks
                    that were defined in the source program input to
                    the translator that produced the module. A BLKDEF
                    record will be generated for every procedure and
                    for every block that contains variables. This
                    information is used to aid debugging programs.
                    This record type is ignored by Microsoft LINK.

   7CH     BLKEND   Block End Record
                    This record, together with the BLKDEF record,
                    provides information about the scope of variables
                    in the source program. Each BLKDEF record must be
                    followed by a BLKEND record. The order of the
                    BLKDEF, debug symbol records, and BLKEND records
                    should reflect the order of declaration in the
                    source module. This record type is ignored by
                    Microsoft LINK.
                  
   7EH     DEBSYM   Debug Symbols Record
                    This record provides information about all
                    local symbols, including stack and based symbols.
                    The purpose of this information is to aid debug-
                    ging programs. This record type is ignored by 
                    Microsoft LINK.
                          
   [80H]   [THEADR] [Translator Header Record]
                          
   [82H]   [LHEADR] [Library Module Header Record]
                          
   84H     PEDATA   Physical Enumerated Data Record
                    This record provides contiguous data,
                    from which a portion of an 8086 memory
                    image may be constructed. The data
                    belongs to the "unnamed absolute segment"
                    in that it has been assigned absolute
                    8086 memory addresses and has been
                    divorced from all logical segment
                    information. This record type is ignored
                    by Microsoft LINK.
                          
   86H     PIDATA   Physical Iterated Data Record
                    This record provides contiguous data,
                    from which a portion of an 8086 memory
                    image may be constructed. It allows
                    initialization of data segments and
                    provides a mechanism to reduce the size
                    of object modules when there is repeated
                    data to be used to initialize a memory
                    image. The data belongs to the "unnamed
                    absolute segment." This record type is
                    ignored by Microsoft LINK.
                          
   [88H]   [COMENT] [Comment Record]
                          
   [8AH/8BH] [MODEND] [Module End Record]
                          
   [8CH]   [EXTDEF] [External Names Definition Record]
                          
   [8EH]   [TYPDEF] [Type Definition Record]
                          
   [90H/91H] [PUBDEF] [Public Names Definition Record]
                          
   92H     LOCSYM   Local Symbols Record
                    This record provides information about
                    symbols that were used in the source
                    program input to the translator that
                    produced the module. This information is
                    used to aid debugging programs. This
                    record has a format identical to the
                    PUBDEF record. This record type is
                    ignored by Microsoft LINK.
                          
   [94H/95H] [LINNUM] [Line Numbers Record]
                          
   [96H]   [LNAMES] [List of Names Record]
                          
   [98H/99H] [SEGDEF] [Segment Definition Record]
                          
   [9AH]   [GRPDEF] [Group Definition Record]
                          
   [9CH/9DH] [FIXUPP] [Fixup Record]
                          
   9EH     (none)   Unnamed record
                    This record number was the only even
                    number not defined by the original Intel
                    specification. Apparently it was never
                    used.  This record type is ignored by
                    Microsoft LINK.
                          
   [A0H/A1H] [LEDATA] [Logical Enumerated Data Record]
                          
   [A2H/A3H] [LIDATA] [Logical Iterated Data Record]

   A4H     LIBHED   Library Header Record
                    This record is the first record in a library
                    file. It immediately precedes the modules
                    (if any) in the library. Following the
                    modules are three more records in the
                    following order: LIBNAM, LIBLOC, and LIBDIC.
                    This record type is ignored by Microsoft
                    LINK.
                        
   A6H     LIBNAM   Library Module Names Record
                    This record lists the names of all the
                    modules in the library. The names are listed
                    in the same sequence as the modules appear
                    in the library. This record type is ignored
                    by Microsoft LINK.
                        
   A8H     LIBLOC   Library Module Locations Record
                    This record provides the relative location,
                    within the library file, of the first byte
                    of the first record (either a THEADR or
                    LHEADR or RHEADR record) of each module in
                    the library. The order of the locations
                    corresponds to the order of the modules in
                    the library. This record type is ignored by
                    Microsoft LINK.
                        
   AAH     LIBDIC   Library Dictionary Record
                    This record gives all the names of public
                    symbols within the library. The public names
                    are separated into groups; all names in the
                    nth group are defined in the nth module of
                    the library. This record type is ignored by
                    Microsoft LINK.
                        
   [B0H]   [COMDEF] [Communal Names Definition Record]
                        
   [B2H/B3H] [BAKPAT] [Backpatch Record]
                        
   [B4H]   [LEXTDEF] [Local External Names Definition Record]
                        
   [B6H/B7H] [LPUBDEF] [Local Public Names Definition Record]
                        
   [B8H]   [LCOMDEF] [Local Communal Names Definition Record]
                        
   BAH/BBH COMFIX   Communal Fixup Record
                    Microsoft doesn't support this never-
                    implemented IBM extension. This record type
                    generates an error when it is encountered by
                    Microsoft LINK.
                        
   BCH     CEXTDEF  COMDAT External Names Definition Record
                        
   C0H     SELDEF   Selector Definition Record
                    Microsoft doesn't support this never-
                    implemented IBM extension. This record type
                    generates an error when it is encountered by
                    Microsoft LINK.
                        
   [C2H/C3] [COMDAT] [Initialized Communal Data Record]
                        
   [C4H/C5H] [LINSYM] [Symbol Line Numbers Record]
                        
   [C6H]   [ALIAS]  [Alias Definition Record]
                        
   [C8H/C9H] [NBKPAT] [Named Backpatch Record]
                        
   [CAH]   [LLNAMES] [Local Logical Names Definition Record]
                        
   [F0H]            [Library Header Record]
                    Although this is not actually an OMF record
                    type, the presence of a record with F0H as
                    the first byte indicates that the module is
                    a Microsoft library. The format of a library
                    file is given in Appendix 2.

   [F1H]            [Library End Record]
                        

80H THEADR--TRANSLATOR HEADER RECORD
====================================

Description
-----------

The THEADR record contains the name of the object module. This name
identifies an object module within an object library or in messages
produced by the linker.

History
-------

Unchanged.

Record Format
-------------

   1    2           1            <-String Length->  1
   80   Record      String       Name String        Checksum
        Length      Length
   
The String Length byte gives the number of characters in the name
string; the name string itself is ASCII. This name is usually that of
the file that contains a program's source code (if supplied by the
language translator), or may be specified directly by the programmer
(for example, TITLE pseudo-operand or assembler NAME directive).
  
  NOTES
  
  The name string is always present; a null name is allowed but not
  recommended (because it doesn't provide much information for a
  debugging program).
  
  In object modules generated by Microsoft compilers, the name string
  indicates the full path and filename of the file that contained the
  source code for the module.
  
  This record, or an LHEADR record must occur as the first object
  record. More than one header record is allowed (as a result of an
  object bind, or if the source arose from multiple files as a result
  of include processing).

Examples
--------

The following THEADR record was generated by the Microsoft C Compiler:

      0   1   2   3   4   5   6   7   8   9   A   B   C D  E  F  
0000  80  09  00  07  68  65  6C  6C  6F  2E  63  CB           ...hello.c
                                                        

Byte 00H contains 80H, indicating a THEADR record.

Bytes 01-02H contain 0009H, the length of the remainder of the record.

Bytes 03-0AH contain the T-module name. Byte 03H contains 07H, the
length of the name, and bytes 04H through 0AH contain the name itself
(HELLO.C).

Byte 0BH contains the Checksum field, 0CBH.


82H LHEADR--LIBRARY MODULE HEADER RECORD
========================================

Description
-----------

This record is very similar to the THEADR record. It is used to
indicate the name of a module within a library file (which has an
internal organization different from that of an object module).

History
-------

This record type was defined in the original Intel specification with
the same format but with a different purpose, so its use for libraries
should be considered a Microsoft extension.

Record Format
-------------

   1    2           1            <-String Length->  1
   82   Record      String       Name String        Checksum
        Length      Length


  NOTE: In LINK, THEADR, and LHEADR records are handled identically.
  See Appendix 2 for a complete description of Microsoft's library
  file format.

88H COMENT--COMMENT RECORD
==========================

Description
-----------

The COMENT record contains a character string that may represent a
plain text comment, a symbol meaningful to a program such as LIB or
LINK, or even binary-encoded identification data. An object module can
contain any number of COMENT records.

History
-------

New comment classes have been added or changed for LINK386. They are:
9D, A0, A1, A2, A4, AA, B0, and B1.

Comment class A2 was added for C version 5.0. Histories for comment
classes A0, A3, A4, A6, A7, and A8 are given later in this section.

68000 and big-endian comments were added for C version 7.0.

Record Format
-------------

The comment records are actually a group of items, classified by
comment class.

   1   2        1       1          <-Record Length Minus 3-> 1
   88  Record   Comment Comment    Commentary Byte String    Checksum
       Length   Type    Class      (optional)

Comment Type
------------

The Comment Type field is bit significant; its layout is
  
  <-------1 byte----------------------------------------------->
   NP     NL      0      0       0      0       0      0

where

   NP  (no purge bit) is set if the comment is to be preserved by
       utility programs that manipulate object modules. This bit can
       protect an important comment, such as a copyright message,
       from deletion.
       
   NL  (no list bit) is set if the comment is not to be displayed by
       utility programs that list the contents of object modules.
       This bit can hide a comment.

The remaining bits are unused and should be set to 0.

Comment Class and Commentary Byte String
----------------------------------------

The Comment Class field is an 8-bit numeric field that conveys
information by its value (accompanied by a null byte string) or
indicates the information to be found in the accompanying byte string.
The byte string's length is determined from the record length, not by
an initial count byte.

The values that have been defined (including obsolete values) are the
following:

   0        Translator     Translator; it may name the source
                           language or translator. We recommend
                           that the translator name and version,
                           plus the optimization level used for
                           compilation, be recorded here. Other
                           compiler or assembler options can be
                           included, although current practice
                           seems to be to place these under
                           comment class 9D.
                           
   1        Intel          Ignored by LINK. Comments of this class
            copyright      are used by QuickC for padding.
                           
   2 - 9B   Intel          The values from 9C through FF are
            reserved       ignored by Intel products.
                           
   81       Library        Replaced by comment class 9F; contents
            specifier--    are identical to 9F.
            obsolete       
            
   9C       MS-DOS         The byte string is then 2 bytes and
            version--      specifies the MS-DOS version number.
            obsolete       This comment class is not supported by
                           LINK.
                           
   9D       Memory model-  This information is currently generated
            -ignored       by the C compiler for use by the XENIX
                           linker; it is ignored by the MS-DOS and
                           OS/2 versions of LINK. The byte string
                           consists of from one to three ASCII
                           characters and indicates the following:
                           
                              0, 1, 2,   8086, 80186, 80286, or 
                              or 3       80386 instructions 
                                         generated, respectively
                       
                              O          Optimization performed on 
                                         code
                       
                              s, m, c,   Small, medium, compact, 
                              l, or h    large, or huge model
                       
                              A, B, C,   68000, 68010, 68020, or 
                              D          68030 instructions 
                                         generated, respectively
                       
   9E       DOSSEG         Sets Microsoft LINK's DOSSEG switch.
                           The byte string is null. This record is
                           included in the startup module in each
                           language library. It directs the linker
                           to use the standardized segment
                           ordering, according to the naming
                           conventions documented with MS-DOS,
                           OS/2, and accompanying language
                           products.
                           
   9F       Default        The byte string contains a library
            library        filename (without a lead count byte and
            search name    without an extension), which is
                           searched in order to resolve external
                           references within the object module.
                           The default library search can be
                           overridden with LINK's
                           /NODEFAULTLIBRARYSEARCH switch.
                           
   A0       OMF            This class consists of a set of
            extensions     records, identified by subtype (first
                           byte of commentary string). Values
                           supported by LINK are:
                           
            01     IMPDEF     Import definition record. See the
                              IMPDEF section in this document for
                              a complete description.
                              
            02     EXPDEF     Export definition record. See the
                              EXPDEF section in this document for
                              a complete description.
                              
            03     INCDEF     Incremental compilation record. See
                              the INCDEF section in this document
                              for a complete description.
                              
            04     Protected  LINK386 only; relevant only to 32-
                   memory     bit dynamic-link libraries (DLLs).
                   library    This comment record is inserted in
                              an object module by the compiler
                              when it encounters the _loadds
                              construct in the source code for a
                              DLL. LINK then sets a flag in the
                              header of the executable file (DLL)
                              to indicate that the DLL should be
                              loaded in such a way that its shared
                              data is protected from corruption.
                              The _loadds keyword tells the
                              compiler to emit modified function
                              prolog code, which loads the DS
                              segment register. (Normal functions
                              don't need this.)
                              
                              When the flag is set in the .EXE
                              header, the loader loads the
                              selector of a protected memory area
                              into DS while performing run-time
                              fixups (relocations). All other DLLs
                              and applications get the regular
                              DGROUP selector, which doesn't allow
                              access to the protected memory area
                              set up by the operating system.
                              
            05     LNKDIR     C++ linker directives record. See
                              the LNKDIR section of this document
                              for a complete description.
                              
            06     Big-       The target for this OMF is a big-
                   endian     endian machine, as opposed to little-
                              endian or Intel format. (For an
                              explanation of big-endian and little-
                              endian, see "On Holy Wars and a Plea
                              for Peace," by Danny Cohen, pages 48-
                              54 in "Computer," volume 14, number
                              10, October 1981.)
                              
            07     PRECOMP    When the CodeView information for
                              this object file is emitted, the
                              directory entry for $$TYPES is to be
                              emitted as sstPreComp instead of
                              sstTypes.
                              
            08-FF             Reserved by Microsoft.
                              
            NOTE: The presence of any unrecognized
            subtype (currently, anything greater than
            07) causes LINK to generate a fatal error.
            
   A1   "New OMF"     This comment class is now used solely to
        extension     indicate the version of the symbolic debug
                      information. If this comment class is not
                      present, the oldest format of CodeView
                      information is written to the .EXE file
                      produced by LINK. If the comment class is
                      present, the latest version format of
                      CodeView information is written.
                      
                      This comment class was previously used to
                      indicate that the obsolete method of
                      communal representation through TYPDEF and
                      EXTDEF pairs was not used and that COMDEF
                      records were used instead. In current
                      linkers, COMDEF records are always enabled,
                      even without this comment record present.
                      
                      The byte string is currently empty, but the
                      planned future contents will be a version
                      number (8-bit numeric field) followed by an
                      ASCII character string indicating the symbol
                      style. Values will be:
                      
                          n,'C','V  CodeView style
                      
                          n,'D','X'  AIX style
                      
   A2   LINK Pass     This record conveys information to the
                      linker about the organization of the file.
                      The value of the first byte of the
                      commentary string specifies the comment
                      subtype. Currently, a single subtype is
                      defined:
                   
                          01            Indicates the start of records 
                                        generated from LINK Pass 2. 
                                        Additional bytes may follow, 
                                        with their number determined 
                                        by the Record Length field, but 
                                        they will be ignored by LINK.
                                        
                                        See the "Order of Records" 
                                        section in this document for 
                                        information on which records must 
                                        come before and after this comment.
                                        
                                          Warning: It is assumed that 
                                          this comment will not be present 
                                          in a module whose MODEND record 
                                          contains a program starting
                                          address. If there are overlays, 
                                          LINK needs to see the starting 
                                          address on Pass 1 to define the 
                                          symbol $$MAIN.
                                        
        NOTE: This comment class may become obsolete with the advent of
        COMDAT records.
                        
   A3   LIBMOD        Library module comment record. Ignored by
                      LINK; used only by Microsoft's LIB utility.
                      See the LIBMOD section in this document for
                      a complete description.
                      
   A4   EXESTR        Executable string. See the EXESTR section in
                      this document for a complete description.
                      
   A6   INCERR        Incremental compilation error. See the
                      INCERR section in this document for a
                      complete description.
                      
   A7   NOPAD         No segment padding. See the NOPAD section in
                      this document for a complete description.
                      
   A8   WKEXT         Weak Extern record. See the WKEXT section in
                      this document for a complete description.
                      
   A9   LZEXT         Lazy Extern record. See the LZEXT section in
                      this document for a complete description.
                      
   AA   PharLap       Possibly obsolete; see the PharLap section
        format        in this document for a complete description.
                      
   B0   Initial IBM   Obsolete.
        OMF386        
        format.
        
   B1   Record order  Obsolete; part of initial IBM OMF386 format.
                      
   DA   Comment       For random comment.
                      
   DB   Compiler      For pragma comment(compiler); version
                      number.
                      
   DC   Date          For pragma comment(date stamp).
                      
   DD   Timestamp     For pragma comment(timestamp).
                      
   DF   User          For pragma comment(user). Sometimes used for
                      copyright notices.
                      
   E9   Dependency    Used to show the include files that were
        file          used to build this .OBJ file.
        (Borland)     
        
   FF   Command line  Shows the compiler options chosen. May be
        (QuickC)      obsolete. This record is also used by
                      Phoenix for library comments.
                      
   C0H-   Reserved     Reserved for user-defined comment classes.
   FFH                 
   and
   not
   other-
   wise
   used
   
  
  NOTES
  
  Microsoft LIB ignores the Comment Type field.
  
  A COMENT record can appear almost anywhere in an object module. Only
  two restrictions apply:
  
  - A COMENT record cannot be placed between a FIXUPP record and  the
    LEDATA or LIDATA record to which it refers.
  
  - A COMENT record cannot be the first or last record in an  object
    module. (The first record must always be THEADR or LHEADR and  the
    last must always be MODEND.)
  
Examples
--------

The following three examples are typical COMENT records taken from  an
object module generated by the Microsoft C Compiler.

This first example is a language-translator comment:

        0  1  2  3  4  5  6  7  8  9  A B C D E  F 
 0000   88 07 00 00 00 4D 53 20 43 6E              .....MS Cn
                                                
Byte 00H contains 88H, indicating that this is a COMENT record.

Bytes 01-02H contain 0007H, the length of the remainder of the record.

Byte  03H (the Comment Type field ) contains 00H. Bit 7 (no purge)  is
set  to  0, indicating that this COMENT record may be purged from  the
object  module  by a utility program that manipulates object  modules.
Bit 6 (no list) is set to 0, indicating that this comment need not  be
excluded from any listing of the module's contents. The remaining bits
are all 0.

Byte 04H (the Comment Class field) contains 00H, indicating that this
COMENT record contains the name of the language translator that
generated the object module.

Bytes 05H through 08H contain the name of the language  translator,
Microsoft C.

Byte 09H contains the Checksum field, 6EH.


The second example contains the name of an object library to be
searched bydefault when LINK processes the object module containing
this COMENT record:

        0  1  2  3  4  5  6  7  8  9  A  B  C D E F  
   0000 88 09 00 00 9F 53 4C 49 42 46 50 10        .....SLIBFP

Byte 04H (the Comment Class field) contains 9FH, indicating that this
record contains the name of a library for LINK to use to resolve
external references.

Bytes 05-0AH contain the library name, SLIBFP. In this example,  the
name refers to the Microsoft C Compiler's floating-point function
library, SLIBFP.LIB.

The last example indicates that LINK should write the most recent
format of CodeView information to the executable file.

      0  1  2  3  4  5  6  7   8  9  A  B   C  D   E  F  
0000  88 06 00 00 A1 01 43 56  37                        .....CV7

Byte 04H indicates the comment class, 0A1H.

Bytes 05-07H, which contain the comment string, are ignored by LINK.


88H IMPDEF--Import Definition Record (Comment Class A0, Subtype 01)
===================================================================

Description
-----------

This record describes the imported names for a module.

History
-------

This comment class and subtype is a Microsoft extension added for OS/2
and Windows.

Record Format
-------------

One import symbol is described; the subrecord format is
                                               
   1      1        <variable>   <variable>       2 or <variable>
   01     Ordinal  Internal     Module           Entry
          Flag     Name         Name             Ident

where:
   
   01              Identifies the subtype as an IMPDEF. It
                   determines the form of the Entry Ident field.
                   
   
   Ordinal Flag    Is a byte; if 0, the import is identified by
                   name. If nonzero, it is identified by ordinal. It
                   determines the form of the Entry Ident field.
                   
   Internal Name   Is in <count, char> string format and is the name
                   used within this module for the import symbol.
                   This name will occur again in an EXTDEF record.
                   
   Module Name     Is in <count, char> string format and is the name
                   of the module (a DLL) that supplies an export
                   symbol matching this import.
                   
   Entry Ident     Is an ordinal or the name used by the exporting
                   module for the symbol, depending upon the Ordinal
                   Flag.
                   
                   If this field is an ordinal (Ordinal Flag is
                   nonzero), it is a 16-bit word. If this is a name
                   and the first byte of the name is 0, then the
                   exported name is the same as the imported name
                   (in the Internal Name field). Otherwise, it is
                   the imported name in <count, char> string format
                   (as exported by Module Name).
                   
    
    NOTE: IMPDEF records are created by the utility IMPLIB, which
    builds an "import library" from a module definition file or DLL.

88H EXPDEF--EXPORT DEFINITION RECORD (COMMENT CLASS A0, SUBTYPE 02)
===================================================================

Description
-----------
   
This record describes the exported names for a module.
     
History
-------

This comment class and subtype is a Microsoft extension added for C
version 5.1.

Record Format
-------------

One exported entry point is described; the subrecord format is

   1      1        <variable>   <variable>       2
   02     Exported Exported     Internal         Export
          Flag     Name         Name             Ordinal
                                                 <conditional>

where:

  02                  Identifies the subtype as an EXPDEF.
                      
  Exported Flag       Is a bit-significant 8-bit field with the
                      following format:

       <-----------------------1 byte---------------------------->
       Ordinal  Resident    No           Parm Count
       Bit      Name        Data         
       1        1           1            <---------5 bits------->


         Ordinal Bit  Is set if the item is exported by ordinal; in
                      this case the Export Ordinal field is present.
                      
         Resident     Is set if the exported name is to be kept
         Name         resident by the system loader; this is an
                      optimization for frequently used items
                      imported by name.
                      
         No Data      Is set if the entry point does not use
                      initialized data (either instanced or global).
                      
         Parm Count   Is the number of parameter words. The Parm
                      Count field is set to 0 for all but callgates
                      to 16-bit segments.
                      
   Exported Name   Is in <count, char> string format. Name to be
                   used when the entry point is imported by name.
                   
   Internal Name   Is in <count, char> string format. If the name
                   length is 0, the internal name is the same as the
                   Exported Name field. Otherwise, it is the name by
                   which the entry point is known within this
                   module. This name will appear as a PUBDEF or
                   LPUBDEF name.
                   
   Export Ordinal  Is present if the Ordinal Bit field is set; it is
                   a 16-bit numeric field whose value is the ordinal
                   used (must be nonzero).
                   
          
  NOTES
  
  EXPDEFs are produced by Microsoft compilers when the keyword _export
  is used in a source file.
  
  Microsoft LINK limits the value of the Export Ordinal field to
  16,384 bytes (16K) or less.


88H INCDEF--INCREMENTAL COMPILATION RECORD
(COMMENT CLASS A0, SUBTYPE 03)
==========================================

Description
-----------

This record is used for incremental compilation. Every FIXUPP and
LINNUM record following an INCDEF record will adjust all external
index values and line number values by the appropriate delta. The
deltas are cumulative if there is more than one INCDEF record per
module.

History
-------

This comment class subtype is a Microsoft extension added for QuickC
version 2.0.

Record Format
-------------

The subrecord format is:

   1      2        2            <variable>
   03     EXTDEF   LINNUM       Padding
          Delta    Delta        

The EXTDEF Delta and LINNUM Delta fields are signed.

Padding (zeros) is added by QuickC to allow for expansion of the
object module during incremental compilation and linking.
  
  NOTE: Negative deltas are allowed.


88H LNKDIR--C++ DIRECTIVES RECORD (COMMENT CLASS A0, SUBTYPE 05)
=================================-------------------------------

Description
-----------

This record is used by the compiler to pass directives and flags to
the linker.

History
-------

This comment class and subtype is a Microsoft extension added for C
7.0.

Record Format
-------------

The subrecord format is:

   1      1        1                1
   05     Bit      Pseudocode       CodeView
          Flags    Version          Version

Bit Flags Field
---------------

The format of the Bit Flags byte is:

   8   1    1    1    1    1    1       1         1 (bits)
   05  0    0    0    0    0    Run     Omit      New
                                MPC     CodeView  .EXE
                                        $PUBLICS

The low-order bit, if set, indicates that LINK should output the new
.EXE format; this flag is ignored for all but linking of pseudocode (p-
code) applications. (Pseudocode requires a segmented executable.)

The second low-order bit indicates that LINK should not output the
$PUBLICS subsection of the CodeView information.

The third low-order bit indicates that MPC (the Make Pseudocode
utility) should be run.

Pseudocode Version Field
------------------------

This field is one byte indicating the pseudocode interpreter version
number.

CodeView Version Field
----------------------

This field is one byte indicating the CodeView version number.

  NOTE: The presence of this record in an object module will indicate
  the presence of global symbols records. The linker will not emit a
  $PUBLICS section for those modules with this comment record and a
  $SYMBOLS section.


88H LIBMOD--LIBRARY MODULE NAME RECORD (COMMENT CLASS A3)
=========================================================

Description
-----------

The LIBMOD comment record is used only by the LIB utility, not by
LINK. It gives the name of an object module within a library, allowing
LIB to preserve the source filename in the THEADR record and still
identify the module names that make up the library. Since the module
name is the base name of the .OBJ file that was built into the
library, it may be completely different from the final library name.

History
-------

This comment class and subtype is a Microsoft extension added for LIB
version 3.07 in MASM version 5.0.

Record Format
-------------

The subrecord format is:

   1      <variable>
   A3     Module Name

The record contains only the ASCII string of the module name, in
<count, char> format. The module name has no path and no extension,
just the base of the module name.

  NOTES
  
  LIB adds a LIBMOD record when an .OBJ file is added to a library and
  strips the LIBMOD record when an .OBJ file is removed from a
  library, so typically this record exists only in .LIB files.
  
  There will be one LIBMOD record in the library file for each object
  module that was combined to build the library.
  
  
88H EXESTR--EXECUTABLE STRING RECORD (COMMENT CLASS A4)
=======================================================

Description
-----------

The EXESTR comment record implements these ANSI and XENIX/UNIX
features in C:

   #pragma comment(exestr, <char-sequence>)
   #ident string

History
-------

This comment class and subtype is a Microsoft extension added for C
5.1.

Record Format
-------------

The subrecord format is:

   1      <variable>
   A4     Arbitrary Text

The linker will copy the text in the Arbitrary Text field byte for
byte to the end of the executable file. The text will not be included
in the program load image.
  
  NOTE: If CodeView information is present, the text will not be at
  the end of the file but somewhere before so as not to interfere with
  the CodeView signature.
  
  There is no limit to the number of EXESTR comment records.
  
  
88H INCERR--INCREMENTAL COMPILATION ERROR (COMMENT CLASS A6)
============================================================

Description
-----------

This comment record will cause the linker to terminate with a fatal
error similar to "invalid object--error encountered during incremental
compilation."

This behavior is useful when an incremental compilation fails and the
user tries to link manually. The object module cannot be deleted, in
order to preserve the base for the next incremental compilation.

History
-------

This comment class and subtype is a Microsoft extension added for
QuickC 2.0.

Record Format
-------------

The subrecord format is:

   1      
   A6     No Fields


88H NOPAD--NO SEGMENT PADDING (COMMENT CLASS A7)
================================================

Description
-----------

This comment record identifies a set of segments that are to be
excluded from the padding imposed with the /PADDATA or /PADCODE
options.

History
-------

This comment class and subtype is a Microsoft extension added for
COBOL. It was added to LINK to support MicroFocus COBOL version 1.2;
it was added permanently in LINK version 5.11 to support Microsoft
COBOL version 3.0.

Record Format
-------------

The subrecord format is:

   1      1 or 2
   A7     SEGDEF Index
          <---------repeated---------->

The SEGDEF Index field is the standard OMF index type of 1 or 2 bytes.
It may be repeated.


88H WKEXT--WEAK EXTERN RECORD (COMMENT CLASS A8)
================================================

Description
-----------

This record marks a set of external names as "weak," and for every
weak extern, the record associates another external name to use as the
default resolution.

History
-------

This comment class and subtype is a Microsoft extension added for
Basic version 7.0. There is no construct in Basic that produces it,
but the record type is manually inserted into Basic library modules.

The first user-accessible construct to produce a weak extern was added
for MASM version 6.0.

See the "Notes" section below for details on how and why this record
is used in Basic and MASM.

Record Format
-------------

The subrecord format is:

   1      1 or 2      1 or 2
   A8     Weak EXTDEF Default Resolution
          Index       EXTDEF Index
          <------------repeated------------>

The Weak EXTDEF Index field is the 1- or 2-byte index to the EXTDEF of
the extern that is weak.

The Default Resolution EXTDEF Index field is the 1- or 2-byte index to
the EXTDEF of the extern that will be used to resolve the extern if no
"stronger" link is found to resolve it.
  
  NOTES
  
  There are two ways to cancel the "weakness" of a weak extern; both
  result in the extern becoming a "strong" extern (the same as an
  EXTDEF). They are:
  
    -If a PUBDEF for the weak extern is linked in
    -If an EXTDEF for the weak extern is found in another module
     (including libraries)
  
  If a weak extern becomes strong, then it must be resolved with a
  matching PUBDEF, just like a regular EXTDEF. If a weak extern has
  not become strong by the end of the linking process, then the
  default resolution is used.
  
  If two weak externs for the same symbol in different modules have
  differing default resolutions, LINK will emit a warning.
  
  Weak externs do not query libraries for resolution; if an extern is
  still weak when libraries are searched, it stays weak and gets the
  default resolution. However, if a library module is linked in for
  other reasons (say, to resolve strong externs) and there are EXTDEFs
  for symbols that were weak, the symbols become strong.
  
  For example, suppose there is a weak extern for "var" with a default
  resolution name of "con". If there is a PUBDEF for "var" in some
  library module that would not otherwise be linked in, then the
  library module is not linked in, and any references to "var" are
  resolved to "con". However, if the library module is linked in for
  other reasons--for example, to resolve references to a strong extern
  named "bletch"-- then "var" will be resolved by the PUBDEF from the
  library, not to the default resolution "con".
  
  WKEXTs are best understood by explaining why they were added in the
  first place. The minimum Basic run-time library in the past
  consisted of a large amount of code that was always linked in, even
  for the smallest program. Most of this code was never called
  directly by the user, but it was called indirectly from other
  routines in other libraries, so it had to be linked in to resolve
  the external references.
  
  For instance, the floating-point library was linked in even if the
  user's program did not use floating-point operations, because the
  PRINT library routine contained calls to the floating-point library
  for support to print floating-point numbers.
  
  The solution was to make the function calls between the libraries
  into weak externals, with the default resolution set to a small stub
  routine. If the user never used a language construct or feature that
  needed the additional library support, then no strong extern would
  be generated by the compiler and the default resolution (to the stub
  routine) would be used. However, if the user accessed the library's
  routines or used constructs that required the library's support, a
  strong extern would be generated by the compiler to cancel the
  effect of the weak extern, and the library module would be linked
  in. This required that the compiler know a lot about which libraries
  are needed for which constructs, but the resulting executable was
  much smaller.
  
  The construct in MASM 6.0 that produces a weak extern is
  
      EXTERN var(con): byte
  
  which makes "con" the default resolution for weak extern "var".

96H LNAMES--LIST OF NAMES RECORD
================================

Description
-----------

The LNAMES record is a list of names that can be referenced by
subsequent SEGDEF and GRPDEF records in the object module.

The names are ordered by occurrence and referenced by index from
subsequent records. More than one LNAMES record may appear. The names
themselves are used as segment, class, group, overlay, and selector
names.

History
-------

This record has not changed since the original Intel 8086 OMF
specification.

Record Format
-------------
                                                        
   1     2             1           <--String Length--> 1
   96    Record        String      Name String         Checksum
         Length        Length
                                                        
                     <-----------repeated----------->

Each name appears in <count, char> format, and a null name is valid.
The character set is ASCII. Names can be up to 254 characters long.
  
  NOTE: Any LNAMES records in an object module must appear before the
  records that refer to them. Because it does not refer to any other
  type of object record, an LNAMES record usually appears near the
  start of an object module.

Examples
--------

The following LNAMES record contains the segment and class names
specified in all three of the following full-segment definitions:
   
   _TEXT     SEGMENT byte public 'CODE'
   _DATA     SEGMENT word public 'DATA'
   _STACK    SEGMENT para public 'STACK'      

The LNAMES record is:

     0  1  2  3  4  5  6  7  8  9  A  B  C  D  E  F  
0000 96 25 00 00 04 43 4F 44 45 04 44 41 54 41 05 53 .%...CODE.DATA.S.
0010 54 41 43 4B 05 5F 44 41 54 41 06 5F 53 54 41 43 TACK._DATA._STAC
0020 4B 05 5F 54 45 58 54 8B                         K._TEXT.

Byte 00H contains 96H, indicating that this is an LNAMES record.

Bytes 01-02H contain 0025H, the length of the remainder of the record.

Byte 03H contains 00H, a zero-length name.

Byte 04H contains 04H, the length of the class name CODE, which is
found in bytes 05-08H. Bytes 09-26H contain the class names DATA and
STACK and the segment names _DATA, _STACK, and _TEXT, each preceded by
1 byte that gives its length.

Byte 27H contains the Checksum field, 8BH.


98H OR 99H SEGDEF--SEGMENT DEFINITION RECORD
============================================

Description
-----------

The SEGDEF record describes a logical segment in an object module. It
defines the segment's name, length, and alignment, and the way the
segment can be combined with other logical segments at bind, link, or
load time.

Object records that follow a SEGDEF record can refer to it to identify
a particular segment. The SEGDEF records are ordered by occurrence,
and are referenced by segment indexes (starting from 1) in subsequent
records.

History
-------

Record type 99H is new for LINK386: the Segment Length field is 32
bits rather than 16 bits, there is one newly implemented alignment
type (page alignment), the B bit flag of the ACBP byte indicates a
segment of 4 GB, and the P bit flag of the ACBP byte is the
Use16/Use32 flag.

Starting with version 2.4, LINK ignores the Overlay Name Index field.
In versions 2.4 and later, command-line parameters to LINK, rather
than information contained in object modules, determine the creation
of run-time overlays.

The length does not include COMDAT records. If selected, their size is
added.

Record Format
-------------
   
   1      2        <variable>  2 or 4  1 or 2  1 or 2 1 or 2   1
   98     Record   Segment     Segment Segment Class  Overlay  Checksum
   or 99  Length   Attributes  Length  Name    Name   Name     
                                       Index   Index  Index

Segment Attributes Field
------------------------

The Segment Attributes field is a variable-length field;
its layout is:

  <-3 bits->  <-3 bits-> <-1 bit-> <-1 bit->  <-2 bytes-->  <--1 byte-->
  A           C          B         P          Frame Number  Offset
                                              <conditional> <conditional>

The fields have the following meanings:

   A     Alignment
         
         A 3-bit field that specifies the alignment required when
         this program segment is placed within a logical segment.
         Its values are:
         
           0    Absolute segment.
                
           1    Relocatable, byte aligned.
                
           2    Relocatable, word (2-byte, 16-bit) aligned.
                
           3    Relocatable, paragraph (16-byte) aligned.
                
           4    Relocatable, aligned on 256-byte boundary (a "page"
                in the original Intel specification).
                
           5    Relocatable, aligned on a double word (4-byte)
                boundary. This value is used by the PharLap OMF for
                the same alignment.
                
           6    This value is used by the PharLap OMF for page (4K)
                alignment. It is not supported by LINK.
                
           7    Not defined.
                
           The new values for LINK386 are A=4 and A=5. Double word
           alignment is expected to be useful as 32-bit memory paths
           become more prevalent. Page-align is useful for certain
           hardware-defined items (such as page tables) and error
           avoidance.
           
           If A=0, the conditional Frame Number and Offset fields
           are present and indicate the starting address of the
           absolute segment. LINK ignores the Offset field.
           
           Conflict: The original Intel specification included
           additional segment-alignment values not supported by
           Microsoft; alignment 5 now conflicts with the following
           LINK386 extensions:
           
           5    "unnamed absolute portion of memory address space"
                
           6    "load-time locatable (LTL), paragraph aligned if not
                part of any group"
                
    C    Combination
         
         A 3-bit field that describes how the linker can combine the
         segment with other segments. Under MS-DOS, segments with
         the same name and class can be combined in two ways: they
         can be concatenated to form one logical segment, or they
         can be overlapped. In the latter case, they have either the
         same starting address or the same ending address, and they
         describe a common area in memory. Values for the C field
         are:
         
           0    Private. Do not combine with any other program
                segment.
                
           1    Reserved by IBM. Not supported by Microsoft.
                
           2    Public. Combine by appending at an offset that meets
                the alignment requirement.
                
           3    Reserved by IBM. Not supported by Microsoft.
                
           4    As defined by Microsoft, same as C=2 (public).
                
           5    Stack. Combine as for C=2. This combine type forces
                byte alignment.
                
           6    Common. Combine by overlay using maximum size.
                
           7    As defined by Microsoft, same as C=2 (public).
                
           Conflict: The Intel specification lists C=1 as Common,
           not C=6.

  B     Big
        
        Used as the high-order bit of the Segment Length field. If
        this bit is set, the segment length value must be 0. If the
        record type is 98H and this bit is set, the segment is
        exactly 64K long. If the record type is 99H and this bit is
        set, the segment is exactly 2^32 bytes, or 4 GB, long.
        
          NOTE: A problem in the 286 chip makes code unreliable if
          it is executed between bytes 65,500 and 65,535. LINK
          warns of this problem if code segments reach that size.
        
  P     This bit corresponds to the bit field for segment
        descriptors, known as the B bit for data segments and the D
        bit for code segments in the Intel documentation.
        If 0, then the segment is no larger than 64K (if data), and
        16-bit addressing and operands are the default (if code).
        This is a Use16 segment.
       
        If nonzero, then the segment may be larger than 64K (if
        data), and 32-bit addressing and operands are the default
        (if code). This is a Use32 segment.
        
           NOTE: This is the only method for defining Use32 segments
           in the Microsoft OMF. The PharLap OMF uses an additional
           byte of bit flags at the end of the SEGDEF record to hold
           this and other flags (described later in this section).
           Even if the P bit is 0, the PharLap OMF assumes all
           segments are Use32.
  
Segment Length Field
--------------------

The Segment Length field is a 2- or 4-byte numeric quantity and
specifies the number of bytes in this program segment. For record type
98H, the length can be from 0 to 64K; if a segment is exactly 64K, the
segment length should be 0, and the B field in the ACBP byte should be
1. For record type 99H, the length can be from 0 to 4 GB; if a segment
is exactly 4 GB in size, the segment length should be 0 and the B
field in the ACBP byte should be 1.

Segment Name Index, Class Name Index, Overlay Name Index Fields
---------------------------------------------------------------

The three name indexes (Segment Name Index, Class Name Index, and
Overlay Name Index) refer to names that appeared in previous LNAMES
record(s). LINK ignores the Overlay Name Index field. The full name of
a segment consists of the segment and class names, and segments in
different object modules are normally combined according to the A and
C values if their full names are identical. These indexes must be
nonzero, although the name itself may be null.

The Segment Name Index field identifies the segment with a name. The
name need not be unique--other segments of the same name will be
concatenated onto the first segment with that name. The name may have
been assigned by the programmer, or it may have been generated by a
compiler.

The Class Name Index field identifies the segment with a class name
(such as CODE, FAR_DATA, or STACK). The linker places segments with
the same class name into a contiguous area of memory in the run-time
memory map.

The Overlay Name Index field identifies the segment with a run-time
overlay. It is ignored by current versions of the linker.

PharLap Extensions to This Record
---------------------------------

In the PharLap 32-bit OMF, there is an additional optional field that
follows the Overlay Name Index field. The reserved bits should always
be 0. The format of this field is

   <------------5 bits----------------> <--1 bit-->  <--2 bits-->
   Reserved                             U            AT

where AT is the access type for the segment and has the following
possible values
   
   0    Read only
   1    Execute only
   2    Execute/read
   3    Read/write

and U is the Use16/Use32 bit for the segment and has the following
possible values:
   
   0    Use16
   1    Use32
  
  Conflicts: The Microsoft-defined OMF has Use16/Use32 stored as the P
  bit of the ACBP field. Microsoft's OMF does not specify the access
  for the segment--it is specified in the .DEF file given to LINK.
  
  NOTES
  
  LINK imposes a limit of 255 SEGDEF records per object module.
  
  Certain name/class combinations are reserved for use by CodeView and
  have special significance to the linker: name $$TYPES with class
  name DEBTYP, and $$SYMBOLS with class name DEBSYM. See Appendix 1
  for more information.

Examples
--------

The following examples of Microsoft assembler SEGMENT directives show
the resulting values for the A field in the corresponding SEGDEF
object record:
   
   aseg  SEGMENT at 400h              ; A = 0
   bseg  SEGMENT byte public 'CODE'   ; A = 1
   cseg  SEGMENT para stack 'STACK'   ; A = 3

The following examples of assembler SEGMENT directives show the
resulting values for the C field in the corresponding SEGDEF object
record:

   aseg  SEGMENT at 400H            ; C = 0
   bseg  SEGMENT public 'DATA'      ; C = 2
   cseg  SEGMENT stack 'STACK'      ; C = 5
   dseg  SEGMENT common 'COMMON'    ; C = 6

In this first example, the segment is byte aligned:

        0   1  2  3  4  5  6  7  8  9  A  B  C  D E  F 
   0000 98  07 00 28 11 00 07 02 01 1E                 ....(.....
  

Byte 00H contains 98H, indicating that this is a SEGDEF record.

Bytes 01-02H contain 0007H, the length of the remainder of the record.

Byte 03H contains 28H (00101000B), the ACBP byte. Bits 7-5 (the A
field) contain 1 (001B), indicating that this segment is relocatable
and byte aligned. Bits 4-2 (the C field) contain 2 (010B), which
represents a public combine type. (When this object module is linked,
this segment will be concatenated with all other segments with the
same name.) Bit 1 (the B field) is 0, indicating that this segment is
smaller than 64K. Bit 0 (the P field) is ignored and should be 0, as
it is here.

Bytes 04-05H contain 0011H, the size of the segment in bytes.

Bytes 06-08H index the list of names defined in the module's LNAMES
record. Byte 06H (the Segment Name Index field) contains 07H, so the
name of this segment is the seventh name in the LNAMES record. Byte
07H (the Class Name Index field) contains 02H, so the segment's class
name is the second name in the LNAMES record. Byte 08H (the Overlay
Name Index field) contains 1, a reference to the first name in the
LNAMES record. (This name is usually null, as MS-DOS ignores it
anyway.)

Byte 09H contains the Checksum field, 1EH.

The second SEGDEF record declares a word-aligned segment. It differs
only slightly from the first.

     0  1  2  3  4  5  6  7  8  9  A B  C  D  E  F 
0000 98 07 00 48 0F 00 05 03 01 01                 .. H......

Bits 7-5 (the A field) of byte 03H (the ACBP byte) contain 2 (010B),
indicating that this segment is relocatable and word aligned.

Bytes 04-05H contain the size of the segment, 000FH.

Byte 06H (the Segment Name Index field) contains 05H, which refers to
the fifth name in the previous LNAMES record.

Byte 07H (the Class Name Index field) contains 03H, a reference to the
third name in the LNAMES record.


9AH GRPDEF--GROUP DEFINITION RECORD
===================================

Description
-----------

This record causes the program segments identified by SEGDEF records
to be collected together (grouped). For OS/2, the segments are
combined into a logical segment that is to be addressed through a
single selector. For MS-DOS, the segments are combined within the same
64K frame in the run-time memory map.

History
-------

The special group name "FLAT" was added for LINK386.

Record Format
-------------
   
   1    2        1 or 2     1        1 or 2       1
   9A   Record   Group Name FF       Segment      Checksum
        Length   Index      Index    Definition   
                            <-----repeated----->  

Group Name Field
----------------

The Group Name field is specified as an index into a previously
defined LNAMES name and must be nonzero.

Groups from different object modules are combined if their names are
identical.

Group Components
----------------

The group's components are segments, specified as indexes into
previously defined SEGDEF records.

The first byte of each group component is a type field for the
remainder of the component. LINK requires a type value of FFH and
always assumes that the component contains a segment index value. See
the "Notes" section below for other types defined by Intel.

The component fields are usually repeated so that all the segments
constituting a group can be included in one GRPDEF record.
  
  NOTES
  
  LINK imposes a limit of 31 GRPDEF records in a single object module
  and limits the total number of group definitions across all object
  modules to 31.
  
  This record is frequently followed by a THREAD FIXUPP record.
  
  The most common group is DGROUP, which is used to group the default
  data segments (_DATA, CONST, and _BSS).
  
  LINK does special handling of the pseudo-group name FLAT for LINK386
  only. All address references to this group are made as offsets from
  the Virtual Zero Address, which is the start of the memory image of
  the executable.
  
  The additional group component types defined by Intel and the fields
  that follow them are:
  
    FE   External Index
    FD   Segment Name Index, Class Name Index, Overlay Name Index
    FB   LTL Data field, Maximum Group Length, Group Length
    FA   Frame Number, Offset
    
  None of these types is supported by LINK.

Examples
--------

The example of a GRPDEF record below corresponds to the following
assembler directive:
   
   tgroup GROUP seg1,seg2,seg3

The GRPDEF record is:

     0   1  2   3  4   5  6  7  8   9  A   B  C  D  E F   
0000 9A  08 00  06 FF  01 FF 02 FF  03 55                 .....U

Byte 00H contains 9AH, indicating that this is a GRPDEF record.

Bytes 01-02H contain 0008H, the length of the remainder of the record.

Byte 03H contains 06H, the Group Name Index field. In this instance,
the index number refers to the sixth name in the previous LNAMES
record in the object module. That name is the name of the group of
segments defined in the remainder of the record.

Bytes 04-05H contain the first of three group component descriptor
fields. Byte 04H contains the required 0FFH, indicating that the
subsequent field is a segment index. Byte 05H contains 01H, a segment
index that refers to the first SEGDEF record in the object module.
This SEGDEF record declared the first of three segments in the group.

Bytes 06-07H represent the second group component descriptor, this one
referring to the second SEGDEF record in the object module.

Similarly, bytes 08-09H are a group component descriptor field that
references the third SEGDEF record.

Byte 0AH contains the Checksum field, 55H.


9CH OR 9DH FIXUPP--FIXUP RECORD
===============================

Description
-----------

The FIXUPP record contains information that allows the linker to
resolve (fix up) and eventually relocate references between object
modules. FIXUPP records describe the LOCATION of each address value to
be fixed up, the TARGET address to which the fixup refers, and the
FRAME relative to which the address computation is performed.

History
-------

Record type 9DH is new for LINK386; it has a Target Displacement field
of 32 bits rather than 16 bits, and the Location field of the Locat
word has been extended to 4 bits (using the previously unused higher
order S bit) to allow new LOCATION values of 9, 11, and 13.

Record Format
-------------
   
   1          2          <------from Record Length----->  1
   9C         Record     THREAD subrecord or              Checksum
   or 9D      Length     FIXUP subrecord                  
                         <--------repeated------------->  

Each subrecord in a FIXUPP object record either defines a thread for
subsequent use, or refers to a data location in the nearest previous
LEDATA or LIDATA record. The high-order bit of the subrecord
determines the subrecord type: if the high-order bit is 0, the
subrecord is a THREAD subrecord; if the high-order bit is 1, the
subrecord is a FIXUP subrecord. Subrecords of different types can be
mixed within one object record.

Information that determines how to resolve a reference can be
specified explicitly in a FIXUP subrecord, or it can be specified
within a FIXUP subrecord by a reference to a previous THREAD
subrecord. A THREAD subrecord describes only the method to be used by
the linker to refer to a particular target or frame. Because the same
THREAD subrecord can be referenced in several subsequent FIXUP
subrecords, a FIXUPP object record that uses THREAD subrecords may be
smaller than one in which THREAD subrecords are not used.

THREAD subrecords can be referenced in the same object record in which
they appear and also in subsequent FIXUPP object records.

THREAD Subrecord
----------------

There are four FRAME threads and four TARGET threads; not all need be
defined, and they can be redefined by later THREAD subrecords in the
same or later FIXUPP object records. The FRAME threads are used to
specify the Frame Datum field in a later FIXUP subrecord; the TARGET
threads are used to specify the Target Datum field in a later FIXUP
subrecord.

A THREAD subrecord does not require that a previous LEDATA or LIDATA
record occur.

The layout of the THREAD subrecord is as follows:

   <--------------1 byte-------------------->  <---1 or 2 bytes--->
   0      D       0      Method     Thred      Index
   1      1       1      3          2 (bits)   <---conditional---->

where:

   0      The high-order bit is 0 to indicate that this is a THREAD
          subrecord.
          
   D      Is 0 for a TARGET thread, 1 for a FRAME thread.
          
   Method Is a 3-bit field.
      
          For TARGET threads, only the lower two bits of the field
          are used; the high-order bit of the method is derived from
          the P bit in the Fix Data field of FIXUP subrecords that
          refer to this thread. (The full list of methods is given
          here for completeness.) This field determines the kind of
          index required to specify the Target Datum field.
          
            T0   Specified by a SEGDEF index.
                 
            T1   Specified by a GRPDEF index.
                 
            T2   Specified by a EXTDEF index.
                 
            T3   Specified by an explicit frame number (not
                 supported by LINK).
                 
            T4   Specified by a SEGDEF index only; the displacement
                 in the FIXUP subrecord is assumed to be 0.
                 
            T5   Specified by a GRPDEF index only; the displacement
                 in the FIXUP subrecord is assumed to be 0.
                 
            T6   Specified by a EXTDEF index only; the displacement
                 in the FIXUP subrecord is assumed to be 0.
                 
                 The index type specified by the TARGET thread
                 method is encoded in the Index field.
                 
                 For FRAME threads, the Method field determines the
                 Frame Datum field of subsequent FIXUP subrecords
                 that refer to this thread. Values for the Method
                 field are:
                 
                    F0    The FRAME is specified by a SEGDEF index.
                          
                    F1    The FRAME is specified by a GRPDEF index.
                          
                    F2    The FRAME is specified by a EXTDEF index.
                          LINK determines the FRAME from the external
                          name's corresponding PUBDEF record in
                          another object module, which specifies
                          either a logical segment or a group.
                          
                    F3    Invalid. (The FRAME is identified by an
                          explicit frame number; this is not
                          supported by LINK.)
                          
                    F4    The FRAME is determined by the segment
                          index of the previous LEDATA or LIDATA
                          record (that is, the segment in which the
                          location is defined).
                          
                    F5    The FRAME is determined by the TARGET's
                          segment, group, or external index.
                          
                    F6    Invalid.
                          
                          NOTE: The Index field is present for FRAME
                          methods F0, F1, and F2 only.
                          
   Thred  A 2-bit field that determines the thread number (0 through
          3, for the four threads of each kind).
   Index  A conditional field that contains an index value that
          refers to a previous SEGDEF, GRPDEF, or EXTDEF record. The
          field is present only if the thread method is 0, 1, or 2.
          (If method 3 were supported by LINK, the Index field would
          contain an explicit frame number.)

FIXUP Subrecord
---------------

A FIXUP subrecord gives the how/what/why/where/who information
required to resolve or relocate a reference when program segments are
combined or placed within logical segments. It applies to the nearest
previous LEDATA or LIDATA record, which must be defined before the
FIXUP subrecord. The FIXUP subrecord is as follows

   2      1               1 or 2         1 or 2          2 or 4
   Locat  Fix             Frame          Target          Target
          Data            Datum          Datum           Displacement
          <conditional>   <conditional>  <conditional>   

where the Locat field has an unusual format. Contrary to the usual
byte order in Intel data structures, the most significant bits of the
Locat field are found in the low-order, rather than the high-order,
byte
   
   <-----low-order byte----><----high-order byte--->
   1    M   Location        Data Record Offset
   1    1   4               10 (bits)

where:

   1          The high-order bit of the low-order byte is set to
              indicate a FIXUP subrecord.
              
   M          Is the mode; M=1 for segment-relative fixups, and M=0
              for self-relative fixups.
              
   Location   Is a 4-bit field that determines what type of LOCATION
              is to be fixed up:
              
                0    Low-order byte (8-bit displacement or low byte
                     of 16-bit offset).
                     
                1    16-bit offset.
                     
                2    16-bit base--logical segment base (selector).
                     
                3    32-bit Long pointer (16-bit base:16-bit
                     offset).
                     
                4    High-order byte (high byte of 16-bit offset).
                     LINK does not support this type.
                     
                5    16-bit loader-resolved offset, treated as
                     Location=1 by the linker.
                     
                     Conflict: The PharLap OMF uses Location=5 to
                     indicate a 32-bit offset, whereas Microsoft
                     uses Location=9.
                     
                6    Not defined, reserved.
                    
                       Conflict: The PharLap OMF uses Location=6 to
                       indicate a 48-bit pointer (16-bit base:32-bit
                       offset), whereas Microsoft uses Location=11.
                    
                7    Not defined, reserved.
                     
                9    32-bit offset.
                     
                11   48-bit pointer (16-bit base:32-bit offset).
                     
                13   32-bit loader-resolved offset, treated as
                     Location=9 by the linker.
                     
   Data       Indicates the position of the LOCATION to be fixed up
   Record     in the LEDATA or LIDATA record immediately preceding
   Offset     the FIXUPP record. This offset indicates either a byte
              in the Data Bytes field of an LEDATA record or a data
              byte in the Content field of a Data Block field in an
              LIDATA record.

The Fix Data bit layout is

   F    Frame  T    P    Targt
   1    3      1    1    2 (bits)

and is interpreted as follows:

   F        If F=1, the FRAME is given by a FRAME thread whose
            number is in the Frame field (modulo 4). There is no
            Frame Datum field in the subrecord.
            
            If F=0, the FRAME method (in the range F0 to F5) is
            explicitly defined in this FIXUP subrecord. The method
            is stored in the Frame field.
            
   Frame    A 3-bit numeric field, interpreted according to the F
            bit. The Frame Datum field is present and is an index
            field for FRAME methods F0, F1, and F2 only.
            
   T        If T=1, the TARGET is defined by a TARGET thread whose
            thread number is given in the 2-bit Targt field. The
            Targt field contains a number between 0 and 3 that
            refers to a previous THREAD subrecord containing the
            TARGET method. The P bit, combined with the two low-
            order bits of the Method field in the THREAD subrecord,
            determines the TARGET method.
            
            If T=0, the TARGET is specified explicitly in this FIXUP
            subrecord. In this case, the P bit and the Targt field
            can be considered a 3-bit field analogous to the Frame
            field.
            
   P        Determines whether the Target Displacement field is
            present.
            
            If P=1, there is no Target Displacement field.
            
            If P=0, the Target Displacement field is present. It is
            a 4-byte field if the record type is 9DH; it is a 2-byte
            field otherwise.
            
   Targt    A 2-bit numeric field, which gives the lower two bits of
            the TARGET method (if T=0) or gives the TARGET thread
            number (if T=1).

Frame Datum, Target Datum, and Target Displacement Fields
---------------------------------------------------------

The Frame Datum field is an index field that refers to a previous
SEGDEF, GRPDEF, or EXTDEF record, depending on the FRAME method.

Similarly, the Target Datum field contains a segment index, a group
index, or an external name index, depending on the TARGET method.

The Target Displacement field, a 16-bit or 32-bit field, is present
only if the P bit in the Fix Data field is set to 0, in which case the
Target Displacement field contains the offset used in methods 0, 1,
and 2 of specifying a TARGET.
  
  NOTES
  
  FIXUPP records are used to fix references in the immediately
  preceding LEDATA, LIDATA, or COMDAT record.
  
  The Frame field is the translator's way of telling the linker the
  contents of the segment register used for the reference; the TARGET
  is the item being referenced whose address was not completely
  resolved by the translator. In protected mode, the only legal
  segment register values are selectors; every segment and group of
  segments is mapped through some selector and addressed by an offset
  within the underlying memory defined by that selector.

Examples
--------

Due to the incredible length of the FIXUPP examples in "The MS-DOS
Encyclopedia," they are not repeated here. However, the examples are
highly recommended if you want to understand what is happening.

A0H OR A1H LEDATA--LOGICAL ENUMERATED DATA RECORD
=================================================

Description
-----------

This record provides contiguous binary data--executable code or
program data--that is part of a program segment. The data is
eventually copied into the program's executable binary image by the
linker.

The data bytes may be subject to relocation or fixing up as determined
by the presence of a subsequent FIXUPP record, but otherwise they
require no expansion when mapped to memory at run time.

History
-------

Record type A1H is new for LINK386; it has an Enumerated Data Offset
field of 32 bits rather than 16 bits.

Record Format
-------------
   
   1      2       1 or 2   2 or 4      <from Record Length>  1
   A0     Record  Segment  Enumerated  Data                  Checksum
   or A1  Length  Index    Data        Bytes                 
                           Offset

Segment Index Field
-------------------

The Segment Index field must be nonzero and is the index of a
previously defined SEGDEF record. This is the segment into which the
data in this LEDATA record is to be placed.

Enumerated Data Offset Field
----------------------------

The Enumerated Data Offset field is either a 2- or 4-byte field
(depending on the record type) that determines the offset at which the
first data byte is to be placed relative to the start of the SEGDEF
segment. Successive data bytes occupy successively higher locations.

Data Bytes Field
----------------

The maximum number of data bytes is 1024, so that a FIXUPP Location
field, which is 10 bits, can reference any of these data bytes. The
number of data bytes is computed from the Record Length field minus 5,
minus the size of the Segment Index field (1 or 2 bytes).
  
  NOTES
  
  Record type A1H has the offset stored as a 32-bit value. Record type
  A0H encodes the offset value as a 16-bit numeric field (zero-
  extended if applied to a Use32 segment).
  
  If an LEDATA record requires a fixup, a FIXUPP record must
  immediately follow the LEDATA record.
  
  Code for functions is output in LEDATA records currently. The
  segment for code is usually named _TEXT (or module_TEXT, depending
  on the memory model), unless #pragma alloc_text is used to specify a
  different code segment for the specified functions.
  
  For instantiated functions in C++, code will simply be output in
  COMDAT records that refer to the function and identify the
  function's segment.
  
  Data, usually generated by initialized variables (global or static),
  is output in LEDATA/LIDATA records referring to either a data
  segment or, possibly, a segment created for a based variable.

Examples
--------

The following LEDATA record contains a simple text string:

      0  1  2  3  4  5  6  7  8  9  A  B  C  D  E  F   
 0000 A0 13 00 02 00 00 48 65 6C 6C 6F 2C 20 77 6F 72......Hello, wor
 0010 6C 64 0D 0A 24 A8                              ld..$.

Byte 00H contains 0A0H, which identifies this as an LEDATA record.

Bytes 01-02H contain 0013H, the length of the remainder of the record.

Byte 03H (the Segment Index field) contains 02H, a reference to the
second SEGDEF record in the object module.

Bytes 04-05H (the Enumerated Data Offset field) contain 0000H. This is
the offset, from the base of the segment indicated by the Segment
Index field, at which the data in the Data Bytes field will be placed
when the program is linked. Of course, this offset is subject to
relocation by the linker because the segment declared in the specified
SEGDEF record may be relocatable and may be combined with other
segments declared in other object modules.

Bytes 06-14H (the Data Bytes field) contain the actual data.

Byte 15H contains the Checksum field, 0A8H.


A2H OR A3H LIDATA--LOGICAL ITERATED DATA RECORD
===============================================

Description
-----------

Like the LEDATA record, the LIDATA record contains binary data--
executable code or program data. The data in an LIDATA record,
however, is specified as a repeating pattern (iterated), rather than
by explicit enumeration.

The data in an LIDATA record can be modified by the linker if the
LIDATA record is followed by a FIXUPP record, although this is not
recommended.

History
-------

Record type A3H is new for LINK386; it has Iterated Data Offset and
Repeat Count fields of 32 bits rather than 16 bits.

Record Format
-------------

   1    2       1 or 2  2 or 4    <from Record Length>  1
   A2   Record  Segment Iterated  Data                  Checksum
   or   Length  Index   Data      Block                 
   A3                   Offset                          
                                  <-----------repeated----------->
   
Segment Index and Interated Data Offset Fields
----------------------------------------------

The Segment Index and Iterated Data Offset fields (2 or 4 bytes) are
the same as for an LEDATA record. The index must be nonzero. This
indicates the segment and offset at which the data in this LIDATA
record is to be placed when the program is loaded.

Data Block Field
----------------

The data blocks have the following form:
                       
   2 or 4    2         <from Block Count>
   Repeat    Block     Content
   Count     Count     

Repeat Count Field
------------------

The Repeat Count field is a 16-bit or 32-bit value that determines the
number of times the Content field is to be repeated. The Repeat Count
field is 32 bits only if the record type is A3H.
  
  Conflict: The PharLap OMF uses a 16-bit Repeat Count field, even in
  32-bit records.

Block Count Field
-----------------

The Block Count field is a 16-bit word whose value determines the
interpretation of the Content field, as follows:

   0      Indicates that the Content field that follows is a 1-byte
          count value followed by count data bytes. The data bytes
          will be mapped to memory, repeated as many times as are
          specified in the Repeat Count field.
          
   != 0   Indicates that the Content field that follows is composed
          of one or more Data Block fields. The value in the Block
          Count field specifies the number of Data Block fields
          (recursive definition).
          
  
  NOTES
  
  The Microsoft C Compiler generates LIDATA records for initialized
  data. For example:
   
      static int a[100] = { 1, };
  
  A FIXUPP record may occur after the LIDATA record; however, the
  fixup is applied before the iterated data block is expanded. It is a
  translator error for a fixup to reference any of the Count fields.

Example 1
---------
   
      02 00 02 00 03 00 00 00 02 40 41 02 00 00 00 02 50 51

is an iterated data block with 16-bit repeat counts that expands to:

      40 41 40 41 40 41 50 51 50 51 40 41 40 41 40 41 50 51 50 51

Here, the outer data block has a repeat count of 2 and a block count
of 2 (which means to repeat twice the result of expanding the two
inner data blocks). The first inner data block has repeat count = 3,
block count = 0. The content is 2 bytes of data (40 41); the repeat
count expands the data to a string of 6 bytes. The second (and last)
inner data block has a repeat count = 2, block count = 0, content 2
bytes of data (50 51). This expands to 4 bytes, which is concatenated
with the 6 bytes from the first inner data block. The resulting 10
bytes are then expanded by 2 (the repeat count of the outer data
block) to form the 20-byte sequence illustrated.

Example 2
---------

This sample LIDATA record corresponds to the following assembler
statement, which declares a 10-element array containing the strings
ALPHA and BETA:
   
   db   10 dup('ALPHA','BETA')

The LIDATA record is
   
      0  1  2  3  4  5  6  7  8  9  A  B  C  D  E  F
0000  A2 1B 00 01 00 00 0A 00 02 00 01 00 00 00 05 41 ...............A
0010  4C 50 48 41 01 00 00 00 04 42 45 54 41 A9       LPHA.....BETA.

Byte 00H contains 0A2H, identifying this as an LIDATA record.

Bytes 01-02H contain 1BH, the length of the remainder of the record.

Byte 03H (the Segment Index field) contains 01H, a reference to the
first SEGDEF record in this object module, indicating that the data
declared in this LIDATA record is to be placed into the segment
described by the first SEGDEF record.

Bytes 04-05H (the Iterated Data Offset field) contain 0000H, so the
data in this LIDATA record is to be located at offset 0000H in the
segment designated by the segment.

Bytes 06-1CH represent an iterated data block:

 - Bytes 06-07H contain the repeat count, 000AH, which indicates that
   the Content field of this iterated data block is to be repeated 10
   times.

 - Bytes 08-09H (the block count for this iterated data block) contain
   0002H, which indicates that the Content field of this iterated data
   block (bytes 0A-1CH) contains two nested iterated data block fields
   (bytes 0A-13H and bytes 14-1CH).

 - Bytes 0A-0BH contain 0001H, the repeat count for the first nested
   iterated data block. Bytes 0C-0DH contain 0000H, indicating that
   the Content field of this nested iterated data block contains data
   rather than more nested iterated data blocks. The Content field
   (bytes 0E-13H) contains the data; byte 0EH contains 05H, the number
   of subsequent data bytes; and bytes 0F-13H contain the actual data
   (the string ALPHA).

 - Bytes 14-1CH represent the second nested iterated data block, which
   has a format similar to that of the block in bytes 0A-13H. This
   second nested iterated data block represents the 4-byte string
   BETA.

 - Byte 1DH is the Checksum field, 0A9H.


B0H COMDEF--COMMUNAL NAMES DEFINITION RECORD
============================================

Description
-----------

The COMDEF record is a Microsoft extension to the basic set of 8086
object record types. It declares a list of one or more communal
variables (uninitialized static data, or data that may match
initialized static data in another compilation unit).

The size of such a variable is the maximum size defined in any module
naming the variable as communal or public. The placement of communal
variables is determined by the data type using established conventions
(noted below).

History
-------

The COMDEF record is recognized by versions 3.5 and later of LINK.

Record Format
-------------

  1  2      1      <String Length> 1 or 2 1    1 or 2 1 <from Data Type>    
  B0 Record String Communal        Type   Data Communal Checksum
     Length Length Name            Index  Type Length          
            <----------------repeated------------------>
             
Communal Name Field
-------------------

The name is in <count, char> string format, and the name may be null.
NEAR and FAR communals from different object files are matched at bind
or link time if their names agree; the variable's size is the maximum
of the sizes specified (subject to some constraints, as documented
below).

Type Index Field
----------------

This field encodes symbol information; it is parsed as an index field
(1 or 2 bytes) and is not inspected by current linkers. This field is
now used by CodeView instead of for its original purpose.

Data Type and Communal Length Fields

The Data Type field indicates the contents of the Communal Length
field. All Data Type values for NEAR data indicate that the Communal
Length field has only one numeric value: the amount of memory to be
allocated for the communal variable. All Data Type values for FAR data
indicate that the Communal Length field has two numeric values: the
first is the number of elements, and the second is the element size.

The Data Type field is one of the following hexadecimal values:

   61H   FAR data; the length is specified as the number of the
         elements followed by the element size in bytes
         
   62H   NEAR data; the length is specified as the number of bytes

The Communal Length field is a single numeric field or a pair of
numeric fields (as specified by the Data Type field), encoded as
follows:

                   Number    
   Value Range     of Bytes   Allocation
   ----------------------------------------------------------------
   0 through 128       1      This byte contains the value
  
   0 to 64K-1          3      First byte is 81H, followed by a 16-bit
                              word whose value is used

   0 to 16 MB-1        4      First byte is 84H, followed by a 3-byte
                              value

   -2 GB-1 to 2 GB-1   5      First byte is 88H, followed by a 4-byte
                              value

Groups of Communal Name, Type Index, Data Type, and Communal Length
fields can be repeated so that more than one communal variable can be
declared in the same COMDEF record.
  
  NOTES
  
  If a public or exported symbol with the same name is found in
  another module to which this module is bound or linked, LINK gives
  the error "symbol defined more than once."
  
  Communal variables cannot be resolved to dynamic links (that is,
  imported symbols).
  
  The records are ordered by occurrence, together with the items named
  in EXTDEF and LEXTDEF records (for reference in FIXUP subrecords).
  
  In older versions of the linker, any object module that contains
  COMDEF records is required to also contain one COMENT record with
  the comment class 0A1H, indicating that Microsoft extensions to the
  Intel object record specification are included in the object module.
  This COMENT record is no longer required; current versions of the
  linker always interpret COMDEF records.

Examples
--------

The following COMDEF record was generated by Microsoft C Compiler
version 4.0 for these public variable declarations:

   int   var;                   /* 2-byte integer */
   char  var2[32768];           /* 32768-byte array */
   char  far var3[10][2][20];   /* 400-byte array */

The COMDEF record is:

         0  1  2  3  4  5  6  7  8  9  A  B  C  D  E  F
0000 B0 20 00 04 5F 66 6F 6F 00 62 02 05 5F 66 6F 6F  . .._var.b.._var
0010 32 00 62 81 00 80 05 5F 66 6F 6F 33 00 61 81 90  2.b...._var3.a..
0020 01 01 99                                         ...

Byte 00H contains 0B0H, indicating that this is a COMDEF record.

Bytes 01-02H contain 0020H, the length of the remainder of the record.

Bytes 03-0AH, 0B-15H, and 16-21H represent three declarations for the
communal variables var, var2, and var3. The C compiler prepends an
underscore to each of the names declared in the source code, so the
symbols represented in this COMDEF record are _var, _var2, and _var3.

Byte 03H contains 04H, the length of the first Communal Name field in
this record. Bytes 04-07H contain the name itself (_var). Byte 08H
(the Type Index field) contains 00H, as required. Byte 09H (the Data
Type field) contains 62H, indicating that this is a NEAR variable.
Byte 0AH (the Communal Length field) contains 02H, the size of the
variable in bytes.

Byte 0BH contains 05H, the length of the second Communal Name field.
Bytes 0C-10H contain the name _var2. Byte 11H is the Type Index field,
which again contains 00H, as required. Byte 12H (the Data Type field)
contains 62H, indicating that _var2 is a NEAR variable.

Bytes 13-15H (the Communal Length field) contain the size in bytes of
the variable. The first byte of the Communal Length field (byte 13H)
is 81H, indicating that the size is represented in the subsequent two
bytes of data--bytes 14-15H, which contain the value 8000H.

Bytes 16-1BH represent the Communal Name field for _var3, the third
communal variable declared in this record. Byte 1CH (the Type Index
field) again contains 00H as required. Byte 1DH (the Data Type field)
contains 61H, indicating that this is a FAR variable. This means the
Communal Length field is formatted as a Number of Elements field
(bytes 1E-20H, which contain the value 0190H) and an Element Size
field (byte 21H, which contains 01H). The total size of this communal
variable is thus 190H times 1, or 400 bytes.

Byte 22H contains the Checksum field, 99H.


B2H OR B3H BAKPAT--BACKPATCH RECORD
===================================

Description
-----------

This record is for backpatches to LOCATIONs that cannot be
conveniently handled by a FIXUPP record at reference time (for
example, forward references in a one-pass compiler). It is essentially
a specialized fixup.

History
-------

Record type B2H is a Microsoft extension that was added for QuickC
version 1.0. Record type B3H is the 32-bit equivalent: the Offset and
Value fields are 32 bits rather than 16 bits.

Record Format
-------------

  1     2       1 or 2   1         2 or 4     2 or 4    1
  B2    Record  Segment  Location  Offset     Value     Checksum
  or B3 Length  Index    Type                         
  
                                   <-----repeated----->
                            
Segment Index Field
-------------------

Segment index to which all "backpatch" FIXUPP records are to be
applied. Note that, in contrast to FIXUPP records, these records do
not need to follow the data record to be fixed up. Hence, the segment
to which the backpatch applies must be specified explicitly.

Location Type Field
-------------------

Type of LOCATION to be patched; the only valid values are:
   
   0    8-bit low-order byte
   1    16-bit offset
   2    32-bit offset, record type B3H only (not supported yet)

Offset and Value Fields
-----------------------

These fields are 32 bits for record type B3H, and 16 bits for B2H.

The Offset field specifies the LOCATION to be patched (as an offset
into the SEGDEF record whose index is Segment Index).

The associated Value field is added to the LOCATION being patched
(unsigned addition, ignoring overflow). The Value field is a fixed
length (16 bits or 32 bits, depending on the record type) to make
object-module processing easier.
  
  NOTE: BAKPAT records can occur anywhere in the object module
  following the SEGDEF record to which they refer. They do not have to
  immediately follow the appropriate LEDATA record as FIXUPP records
  do.
  
  These records are buffered by the linker in Pass 2 until the end of
  the module, after the linker applies all other FIXUPP records. LINK
  then processes these records as fixups.

Examples
--------

For example, to generate a self-relative address whose TARGET is a
forward reference (JZ forwardlabel), the translator can insert the
negative offset of the next instruction (-*) from the start of the
SEGDEF record, followed by an additive backpatch (meaning that the
backpatch is added to the original value and the sum replaces the
original value) whose Value is the offset of the TARGET of the jump,
which is done last.


B4H OR B5H LEXTDEF--LOCAL EXTERNAL NAMES DEFINITION RECORD
==========================================================

Description
-----------

This record is identical in form to the EXTDEF record described
earlier. However, the symbols named in this record are not visible
outside the module in which they are defined.

History
-------

This record was a Microsoft extension for C 5.0. There is no semantic
difference between the B4H and B5H types.

Record Format
-------------

   1    2        1       <String Length>  1 or 2  1
   B4   Record   String  External         Type    Checksum
   B5   Length   Length  Name String      Index   
                 <--------------repeated------->
  
  NOTE: These records are associated with LPUBDEF and LCOMDEF records
  and ordered with the EXTDEF records by occurrence, so that they may
  be referenced by an external name index for fixups.
  
  The name string, when stored in LINK's internal data structures, is
  encoded with spaces and digits at the beginning of the name.

Examples
--------

This record type is produced in C from static functions, such as:
   
   static int var() { }


B6H OR B7H LPUBDEF--LOCAL PUBLIC NAMES DEFINITION RECORD
========================================================

Description
-----------

This record is identical in form to the PUBDEF record described
earlier. However, the symbols named in this record are not visible
outside the module in which they are defined.

History
-------

This record was a Microsoft extension for C 5.0. Record type B7H is
new for LINK386: the Local Offset field is 32 bits rather than 16
bits.

Record Format
-------------
   1  2       1 or 2 1 or 2 2      1      <String  2 or 4 1 or 2 1
                                           Length>  
   B6 Record  Base   Base    Base   String Local   Local   Type  Checksum
   or Length  Group  Segment Frame  Length Name    Offset  Index  
   B7                                      String 
                             <cond.><----------repeated---------->  
  
Examples
--------

In C, the static keyword on functions or initialized variables
produces LPUBDEF records. Uninitialized static variables produce
LCOMDEF records.


B8H LCOMDEF--LOCAL COMMUNAL NAMES DEFINITION RECORD
===================================================

Description
-----------

This record is identical in form to the COMDEF record described
previously. However, the symbols named in this record are not visible
outside the module in which they are defined.

History
-------

This record was a Microsoft extension for C 5.0.

Record Format
-------------

   1  2       1       <String      1      1      <from      1
                      Length>      or 2          Data Type>
   B8 Record  String  Communal     Type   Data   Communal   Checksum
      Length  Length  Name         Index  Type   Length          
              <--------------repeated---------------------->  

Examples
--------

In C, uninitialized static variables produce an LCOMDEF record.


BCH CEXTDEF--COMDAT EXTERNAL NAMES DEFINITION RECORD
====================================================

Description
-----------

This record serves the same purpose as the EXTDEF record described
earlier. However, the symbol named is referred to through a Logical
Name Index field. Such a Logical Name Index field is defined through
an LNAMES or LLNAMES record.

History
-------

The record is a Microsoft extension for C 7.0.

Record Format
-------------

                                            
   1    2      1 or 2          1 or 2       1
   BC   Record Logical Name    Type         Checksum
        Length Index           Index        
               <---------repeated-------->  
               
               
  NOTE: A CEXTDEF can precede the COMDAT to which it will be resolved.
  In this case, the location of the COMDAT is not known at the time
  the CEXTDEF is seen.

Examples
--------

This record is produced when a FIXUPP record refers to a COMDAT
symbol.


C2H OR C3H COMDAT--INITIALIZED COMMUNAL DATA RECORD
===================================================

Description
-----------

The purpose of the COMDAT record is to combine logical blocks of code
and data that may be duplicated across a number of compiled modules.

History
-------

The record is a Microsoft extension for C 7.0.

Record Format
-------------
 1  2      1      1      1      2 or 4 1 or  2      1 or 2 1    1     
 C2 Record Flags  Attrib Align  Enumer Type  Public Public Data Check
 or Length        -utes         -ated  Index Base   Name        Sum  
 C3                             Data                Index     
                                Offset                       
 
                                                    <repeated> 
                                                     
Flags Field
-----------

This field contains the following defined bits:

   01H   Continuation bit. If clear, this COMDAT record establishes
         a new instance of the COMDAT variable; otherwise, the data
         is a continuation of the previous COMDAT of the symbol.
         
   02H   Iterated data bit. If clear, the Data field contains
         enumerated data; otherwise, the Data field contains
         iterated data, as in an LIDATA record.
         
   04H   Local bit (effectively an "LCOMDAT"). This is used in
         preference to LLNAMES.
         
   08H   Data in code segment. If the application is overlayed, this
         COMDAT must be forced into the root text. Also, do not
         apply FARCALLTRANSLATION to this COMDAT.

Attributes Field
----------------
          
This field contains two 4-bit fields: the Selection Criteria to be
used, and the Allocation Type, an ordinal specifying the type of
allocation to be performed. Values are:

   Selection Criteria (High-Order 4 Bits):

   Bit       Selection Criteria
                       
   00H       No match  Only one instance of this COMDAT allowed.
                       
   10H       Pick Any  Pick any instance of this COMDAT.
                       
   20H       Same      Pick any instance, but instances must have
             Size      the same length or the linker will generate
                       an error.
                       
   30H       Exact     Pick any instance, but checksums of the
             Match     instances must match or the linker will
                       generate an error. Fixups are ignored.
                       
   40H -               Reserved.
   F0H

   Allocation Type (Low-Order 4 bits):
   
   Bit       Allocation 
                                  
   00H       Explicit Allocate in the segment specified in the
                      ensuing Base Group, Base Segment, and Base
                      Frame fields.
                                          
   01H       Far      Allocate as CODE16. The linker will create
             Code     segments to contain all COMDATs of this type.
                      
   02H       Far      Allocate as DATA16. The linker will create
             Data     segments to contain all COMDATs of this type.
                      
   03H       Code32   Allocate as CODE32. The linker will create
                      segments to contain all COMDATs of this type.
                      
   04H       Data32   Allocate as DATA32. The linker will create
                      segments to contain all COMDATs of this type.
                      
   05H -              Reserved.
   0FH

Align Field

These codes are based on the ones used by the SEGDEF record:
   
   0   Use value from SEGDEF
   1   Byte aligned
   2   Word aligned
   3   Paragraph (16 byte) aligned
   4   256-byte aligned
   5   Double word (4 byte) aligned
   6   Not defined
   7   Not defined

Enumerated Data Offset Field
----------------------------
          
This field specifies an offset relative to the beginning location of
the symbol specified in the Public Name Index field and defines the
relative location of the first byte of the Data field. Successive data
bytes in the Data field occupy higher locations of memory. This works
very much like the Enumerated Data Offset field in an LEDATA record,
but instead of an offset relative to a segment, this is relative to
the beginning of the COMDAT symbol.

Type Index Field
----------------

The Type Index field is encoded in index format; it contains either
proprietary CodeView-type information or an old-style TYPDEF index. If
this index is 0, there is no associated type data. Old-style TYPDEF
indexes are ignored by LINK. Current linkers do not perform type
checking.

Public Base Field
-----------------

This field is conditional and is identical to the public base fields
(Base Group, Base Segment, and Base Frame) stored in the PUBDEF
record. This field is present only if the Allocation Type field
specifies Explicit allocation.

Public Name Index Field
-----------------------

This field is a regular logical name index (1 or 2 bytes).

Data Field
----------

The Data field provides up to 1024 consecutive bytes of data. If there
are fixups, they must be emitted in a FIXUPP record that follows the
COMDAT record. The data can be either enumerated or iterated,
depending on the Flags field.

  NOTES
  
  Record type C3H has an Enumerated Data Offset field of 32 bits.
  
  While creating addressing frames, the linker will add the COMDAT
  data to the appropriate logical segments, adjusting their sizes. At
  that time, the offset at which the data will go inside the logical
  segment will be calculated. Next, the linker will create physical
  segments from adjusted logical segments, reporting any 64K boundary
  overflows.
  
  If the allocation type is not explicit, COMDAT code and data is
  accumulated by the linker and broken up into segments, so that the
  total can exceed 64K.
  
  In Pass 2, only the selected occurrence of COMDAT data will be
  stored in virtual memory, fixed up, and later written into the .EXE
  file.
  
  COMDATs are allocated in the order of their appearance in the .OBJ
  files if no explicit ordering is given.
  
  A COMDAT record cannot be continued across modules. A COMDAT record
  can be duplicated in a single module.
  
  If any COMDAT record on a given symbol has the local bit set, all
  the COMDAT records on that symbol have that bit set.

C4H OR C5H LINSYM--SYMBOL LINE NUMBERS RECORD
=============================================

Description
-----------

This record will be used to output line numbers for functions
specified through COMDAT records. Each LINSYM record is associated
with a preceding COMDAT record.

History
-------

This record is a Microsoft extension for C 7.0.

Record Format
-------------
   1     2       1      1 or 2  2       2 or 4     1
   C4    Record  Flags  Public  Line    Line       Checksum
   or    Length         Name    Number  Number     
   C5                   Index           Offset     
                                <---repeated--->   

Flags Field
-----------
          
This field contains one defined bit:
   
  01H   Continuation bit. If clear, this COMDAT record establishes a
        new instance of the COMDAT variable; otherwise, the data is a
        continuation of the previous COMDAT of the symbol.
   
Public Name Index Field
-----------------------

A regular logical name index, indicating the name of the base of the
LINSYM record.

Line Number Field
-----------------

An unsigned number in the range 0 to 65,535.

Line Number Offset Field
------------------------

The offset relative to the base specified by the symbol name base. The
size of this field depends on the record type.
  
  NOTES
  
  Record type C5H is identical to C4H except that the Line Number
  Offset field is 4 bytes instead of 2.
  
  This record is used to output line numbers for functions specified
  through COMDAT records. Often, the residing segment as well as the
  relative offsets of such functions is unknown at compile time, in
  that the linker is the final arbiter of such information. For such
  cases, the compiler will generate this record to specify the line
  number/offset pairs relative to a symbolic name.
  
  This record will also be used to discard duplicate LINNUM
  information. If the linker encounters two or more LINSYM records
  with matching symbolic names (corresponding to multiple COMDAT
  records with the same name), the linker will keep the one that
  corresponds to the retained COMDAT.
  
  LINSYM records must follow the COMDATs to which they refer. A LINSYM
  on a given symbol refers to the most recent COMDAT on the same
  symbol.
  
  LINSYMs inherit the "localness" of their COMDATs.


C6H ALIAS--ALIAS DEFINITION RECORD
==================================

Description
-----------

This record has been introduced to support link-time aliasing, a
method by which compilers or assemblers may direct the linker to
substitute all references to one symbol for another.

History
-------

The record is a Microsoft extension for FORTRAN version 5.1 (LINK
version 5.13).

Record Format
-------------

   1   2              <variable>   <variable>         1
   C6  Record Length  Alias Name   Substitute Name    Checksum
                      <-----------repeated--------->  
   
   Alias Name Field
   ----------------
   
   A regular length-preceded name of the alias symbol.
   
   Substitute Name Field
   ---------------------
   
   A regular length-preceded name of the substitute symbol.
   
  NOTES
  
  This record consists of two symbolic names: the alias symbol and the
  substitute symbol. The alias symbol behaves very much like a PUBDEF
  in that it must be unique. If a PUBDEF of an alias symbol is
  encountered later, the PUBDEF overrides the alias. If another ALIAS
  record with a different substitute symbol is encountered, a warning
  is emitted by the linker, and the second substitute symbol is used.
  
  When attempting to satisfy an external reference, if an ALIAS record
  whose alias symbol matches is found, the linker will halt the search
  for alias symbol definitions and will attempt to satisfy the
  reference with the substitute symbol.
  
  All ALIAS records must appear before the LINK Pass 2 record.


C8H OR C9H NBKPAT--NAMED BACKPATCH RECORD
=========================================

Description
-----------

The Named Backpatch record is similar to a BAKPAT record, except that
it refers to a COMDAT record, by logical name index, rather than an
LIDATA or LEDATA record. NBKPAT records must immediately follow the
COMDAT/FIXUPP block to which they refer.

History
-------

This record is a Microsoft extension for C 7.0.

Record Format
-------------
   
   1      2        1          1 or 2  2 or 4   2 or 4  1
   C8     Record   Location   Public  Offset   Value   Checksum
   or C9  Length   Type       Name
                                      <---repeated---> 
                                
Location Type Field
-------------------
          
Type of location to be patched; the only valid values are:
   
   0    8-bit byte
   1    16-bit word
   2    32-bit double word, record type C9H only

Public Name Index Field
-----------------------
          
Regular logical name index of the COMDAT record to be back patched.

Offset and Value Fields
-----------------------
   
These fields are 32 bits for record type C8H, 16 bits for C9H.

The Offset field specifies the location to be patched, as an offset
into the COMDAT.

The associated Value field is added to the location being patched
(unsigned addition, ignoring overflow). The Value field is a fixed
length (16 bits or 32 bits, depending on the record type) to make
object module processing easier.


CAH LLNAMES--LOCAL LOGICAL NAMES DEFINITION RECORD
==================================================

Description
-----------

The LLNAMES record is a list of local names that can be referenced by
subsequent SEGDEF and GRPDEF records in the object module.

The names are ordered by their occurrence, with the names in LNAMES
records and referenced by index from subsequent records. More than one
LNAMES and LLNAMES record may appear. The names themselves are used as
segment, class, group, overlay, COMDAT, and selector names.

History
-------

This record is a Microsoft extension for C 7.0.

Record Format
-------------
   
   1         2         1         <--String Length--> 1
   CA        Record    String    Name                Checksum
             Length    Length    String              
                       <----------repeated---------> 

Each name appears in <count, char> format, and a null name is valid.
The character set is ASCII. Names can be up to 254 characters long.

  NOTE: Any LLNAMES records in an object module must appear before the
  records that refer to them.
  

APPENDIX 1: CODEVIEW EXTENSIONS
===============================

Calling the following information "CodeView's OMF" is a misnomer,
since CodeView actually does very little to extend the OMF. Most
CodeView information is stored within the confines of the existing
OMF, except where noted below.

CodeView information is stored on a per-module basis in specially-
named logical segments. These segments are defined in the usual way
(SEGDEF records), but LINK handles them specially, and they do not end
up as segments in the .EXE file. These segment names are reserved:

   Segment Name        Class Name          Combine Type
   ------------        ----------          ------------

   $$TYPES             DEBTYP              Private
   $$SYMBOLS           DEBSYM              Private

The segment $$IMPORT should also be considered a reserved name,
although it is not used anymore. This segment was not part of any
object files but was emitted by the linker to get the loader to
automatically do fixups for CodeView information. The linker emitted a
standard set of imports, not just ones referenced by the program being
linked. Use of this segment may be revisited in the future.

CodeView-specific data is stored in LEDATA records for the $$TYPES and
$$SYMBOLS segments, in various proprietary formats. The $$TYPES
segment contains information on user-defined variable types; $$SYMBOLS
contains information about nonpublic symbols: stack, local, procedure,
block start, constant, and register symbols and code labels.

For instantiated functions in C 7.0, symbol information for CodeView
will be output in COMDAT records that refer to segment $$SYMBOLS and
have decorated names based on the function names. Type information
will still go into the $$TYPES segment in LEDATA records.

All OMF records that specify a Type Index field, including EXTDEF,
PUBDEF, and COMDEF records, use proprietary CodeView values. Since
many types are common, Type Index values in the range 0 through 511
(1FFH) are reserved for a set of predefined primitive types. Indexes
in the range 512 through 32767 (200H-7FFFH) index into the set of type
definitions in the module's $$TYPES segment, offset by 512. Thus 512
is the first new type, 513 the second, and so on.


APPENDIX 2: MICROSOFT MS-DOS LIBRARY FORMAT
===========================================

Libraries under MS-DOS are always multiples of 512-byte blocks.

The first record in the library is a header. This first record looks
very much like any other Microsoft object module format record.

  Library Header Record (<n> bytes)
  ---------------------------------
                                                             
   1     2                    4           2            1       <n - 10>
   Type  Record Length        Dictionary  Dictionary   Flags   Padding
                              Offest      Size
   (F0H)  (Page Size Minus 3)             in Blocks            
    
   The first byte of the record identifies the record's type, and the
   next two bytes specify the number of bytes remaining in the record.
   Note that this word field is byte-swapped (that is, the low-order
   byte precedes the high-order byte). The record type for this
   library header is F0H (240 decimal).
   
   The Record Length field specifies the page size within the library.
   Modules in a library always start at the beginning of a page. Page
   size is determined by adding three to the value in the Record
   Length field (thus the header record always occupies exactly one
   page). Legal values for the page size are given by 2 to the <n>,
   where <n> is greater than or equal to 4 and less than or equal to
   15.
   
   The four bytes immediately following the Record Length field are a
   byte-swapped long integer specifying the byte offset within the
   library of the first byte of the first block of the dictionary.
   
   The next two bytes are a byte-swapped word field that specifies the
   number of blocks in the dictionary. (The MS-DOS Library Manager
   cannot create a library whose dictionary would require more than
   251 512-byte pages.)
   
   The next byte contains flags describing the library. The current
   flag definition is:
   
     0x01 = case sensitive (applies to both regular and extended
     dictionaries)
     
   All other values are reserved for future use and should be 0.
   
   The remaining bytes in the library header record are not
   significant. This record deviates from the typical Microsoft OMF
   record in that the last byte is not used as a checksum on the rest
   of the record.

Immediately following the header is the first object module in the
library. It, in turn, is succeeded by all other object modules in the
library. Each module is in Microsoft OMF (that is, it starts with a
LHEADR record and ends with a MODEND record). Individual modules are
aligned so as to begin at the beginning of a new page. If, as is
commonly the case, a module does not occupy a number of bytes that is
exactly a multiple of the page size, then its last block will be
padded with as many null bytes as are required to fill it.

Following the last object module in the library is a record that
serves as a marker between the object modules and the dictionary. It
also resembles a Microsoft OMF record.

   Library End Record (marks end of objects and beginning of
   dictionary)

   1           2                 <n>
   Type (F1H)  Record Length     Padding
   
   The record's Type field contains F1H (241 decimal), and its Record
   Length field is set so that the dictionary begins on a 512-byte
   boundary. The record contains no further useful information; the
   remaining bytes are insignificant. As with the library header, the
   last byte is not a checksum.

Dictionary
----------
   
The remaining blocks in the library compose the dictionary. The number
of blocks in the dictionary is given in the library header. Note that
there should always be a prime number of blocks in the dictionary.

The dictionary is a hashed index to the library. Public symbols are
essentially hashed twice, though in fact, both hash indexes are
produced simultaneously. The first hash index, the block index, is
used to determine a block within the dictionary in which to place the
symbol. The second hash index, the bucket index, is used to choose a
bucket within the block for the symbol. Blocks always have 37 buckets;
they are the first 37 bytes of each block. If a bucket is full, it
contains a nonzero value that points to the text of the symbol. To
actually find the symbol, take the bucket value, multiply it by two,
and use the resulting number as a byte offset from the beginning of
the block.

Collisions (that is, two or more distinct symbols hashing to the same
block and bucket in the dictionary) are resolved by a technique known
as linear open addressing. At the same time the hash indexes are
produced, two hash deltas are also produced. If a symbol collides with
a symbol already installed in the dictionary, the librarian attempts
to find an empty bucket for it by adding the bucket delta to the
bucket index and using the result mod 37 as a new bucket index. If
this new bucket index points to a bucket that is empty, the librarian
will install the symbol in that bucket. If the bucket is not empty,
the delta is applied repeatedly until an empty bucket is found or
until it is determined that there are no empty buckets on the block.
If the latter is the case, the block delta is added to the block
index, and the result mod the number of blocks in the dictionary is
used as a new block index. With the new block index and the original
bucket index, the sequence is repeated until an empty bucket on some
block is found.

The number of blocks and the number of buckets are prime so that no
matter what values of hash indexes and deltas are produced for a
symbol, in the worst case, all possible block-bucket combinations will
be tried. Once a free block-bucket pair has been found for a symbol,
the pair and information concerning its place of definition must be
installed. Since a bucket is a single byte pointing into a 512-byte
block, the bucket can give at best a word offset within that block.
Thus, symbol entries within a dictionary must start on word
boundaries. Since bytes 0 through 36 of each dictionary block make up
the hash table, the first symbol entry will begin at byte 38
(decimal).

   Dictionary Record (length is the dictionary size in 512-byte
   blocks)

   37     1      <variable>  2                <conditional>
   HTAB   FFLAG  Name        Block Number      Align Byte
                 <-------------------repeated------------->
   
   Entries consist of the following: the first byte is the length of
   the symbol to follow, the following bytes are the text of the
   symbol, and the last two bytes are a byte-swapped word field that
   specifies the page number (counting the library header as the 0th
   page) at which the module defining the symbol begins.
   
   All entries may have at most one trailing null byte in order to
   align the next entry on a word boundary.
   
   It is possible for a dictionary block to be full without all its
   buckets being used. Such will be the case, for example, if symbol
   names are longer on average than nine characters each. Therefore,
   there must be some way to mark a block as full so that empty
   buckets will be ignored.
   
   Byte 37 decimal (counting from 0) is reserved for this purpose. If
   the block is not full, byte 37 will contain the word offset of the
   beginning of free space in the block, but if the block is full,
   byte 37 will contain the special value 255 decimal (FFH). Module
   names are stored in the LHEADR record of each module.
   
Extended Dictionary
-------------------

The extended dictionary is optional and indicates dependencies between
modules in the library. Versions of LIB earlier than 3.09 do not
create an extended dictionary. The extended dictionary is placed at
the end of the library.

The dictionary is preceded by these values:

   BYTE =0xF2 Extended Dictionary header
   WORD length of extended dictionary in bytes excluding first three
        bytes

Start of extended dictionary:

   WORD number of modules in library = N

Module table, indexed by module number, with N + 1 fixed-length
entries:

   WORD module page number
   WORD offset from start of extended dictionary to list of required
        modules

Last entry is null.

Dictionary Hashing Algorithm
----------------------------

The last part of each library file is a dictionary, which contains
indexes to all symbols in the library. The dictionary is divided into
512-byte pages. Each page consists of a 37-byte bucket table and a 475-
byte table of symbol entries.

To find the right spot in the dictionary for a given symbol, the
hashing algorithm is used. The hashing algorithm analyzes the name of
the symbol and produces two indexes: a page and a bucket index, which
together point to a single entry in the dictionary. The only problem
is that more than one symbol name can generate exactly the same
address. Because of this, the name found in the dictionary entry must
be compared with the symbol's name, and if they are not identical, a
correction to the address must be made. To make this correction
possible, the hashing algorithm, in addition to the base address
(page, bucket), also produces the correction values (delta-page, delta-
bucket), which are added to the base address if the symbol's name does
not match the name in an entry. The number of pages in the dictionary
must always be prime, so if the symbol is not found, the consecutive
adding of deltas produces the starting address again.

Below is psueudocode illustrating the hashing algorithm used by the
LIB (librarian) utility.

   extern char *symbol;   /* Symbol to find        */
   extern int dictlength;  /* Dictionary length in pages  */
   extern int buckets;   /* Number of buckets on one page */
   
   
   
   char *pb;  /* A pointer to the beginning of the symbol  */
   char *pe;  /*   "      end     "      */
   int slength;  /* Length of the symbol's name      */
   
   int page_index;   /*  Page index           */
   int page_index_delta;/*  Page index delta        */
   int page_offset;   /*  Page offset (bucket #)     */
   int page_offset_delta;/* Page offset delta        */
   
   unsigned c;
   
   slength = strlen(symbol);
   pb = symbol;
   pe = symbol + slength;
   page_index = 0;
   page_index_delta = 0;
   page_offset = 0;
   page_offset_delta = 0;
   
   while( slength-)
   {
        c = *(pf++) | 32; /* Convert character to lowercase */
        page_index = (page_index<<2) XOR c;    /* Hash */
        page_offset_delta = (page_offset_delta>>2)XORc;
        c = *(pe++) | 32;
        page_offset = (page_offset>>2) XOR c;     /* Hash */
        pageiindexdelta = (page_index_delta<<2) XOR c;
   }
   
   /* Calculate page index */
   page_index = page_index MODULO dictlength;
   
   
   /* Calculate page index delta */
   if((page_index_delta = page_index_delta MODULO dictlength) == 0)
        page_index_delta = 1;
   
   
   /* Calculate page offset */
   page_offset = page_offset MODULO buckets;
   
   
   /* Calculate page offset delta */
   if( (page_offset_delta = page_offset_delta MODULO buckets) == 0)
     page_offset_delta = 1;

```